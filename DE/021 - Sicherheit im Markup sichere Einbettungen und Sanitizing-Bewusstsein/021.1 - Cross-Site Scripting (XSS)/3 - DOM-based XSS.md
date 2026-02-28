# DOM-based XSS

### DOM-based XSS: Der clientseitige Angriff

In den vorherigen Abschnitten haben wir uns mit Reflected und Stored XSS beschäftigt. Bei beiden Varianten spielte der Server eine zentrale Rolle: Er hat entweder eine schädliche Eingabe direkt zurückgespiegelt oder sie gespeichert und später an andere Nutzer ausgeliefert. Jetzt betreten wir eine andere Arena, die des clientseitigen Codes. Willkommen in der Welt des DOM-based Cross-Site Scripting.

Was DOM-based XSS so besonders – und heimtückisch – macht, ist sein Schauplatz: Alles spielt sich ausschließlich im Browser des Nutzers ab. Der bösartige Code berührt oft nicht einmal den Server. Das macht diese Art von Angriff für serverseitige Sicherheitsmaßnahmen wie Web Application Firewalls (WAFs) oft unsichtbar. Die Schwachstelle liegt nicht darin, wie der Server eine Seite generiert, sondern wie der JavaScript-Code auf der bereits geladenen Seite mit Daten umgeht.

#### Das Document Object Model (DOM) als Tatort

Um DOM-based XSS zu verstehen, musst du das DOM nicht nur als eine Baumstruktur von HTML-Elementen sehen, sondern als eine lebendige, veränderbare Repräsentation deiner Webseite im Speicher des Browsers. JavaScript hat die Macht, dieses DOM zu lesen und zu manipulieren: Es kann Elemente hinzufügen, entfernen, deren Inhalt ändern oder auf Ereignisse reagieren.

Genau hier liegt die Gefahr. Ein DOM-based XSS-Angriff findet statt, wenn ein clientseitiges Skript Daten aus einer vom Nutzer kontrollierbaren Quelle liest und diese Daten unsicher in das DOM schreibt, sodass sie als ausführbarer Code interpretiert werden.

Lass uns das in seine Bestandteile zerlegen:

1.  **Die Quelle (Source):** Das ist der Ort, aus dem die unsicheren Daten stammen. Im Browser gibt es viele solcher Quellen, die von außen manipuliert werden können. Ein klassisches Beispiel ist die URL selbst.
    *   `location.search`: Der Query-String-Teil der URL (alles nach dem `?`).
    *   `location.hash`: Der Fragment-Teil der URL (alles nach dem `#`).
    *   `document.cookie`: Daten, die in Cookies gespeichert sind.
    *   `document.referrer`: Die URL der Seite, von der der Nutzer kam.

2.  **Die Senke (Sink):** Das ist die Funktion oder Eigenschaft, die die unsicheren Daten verwendet und potenziell gefährlichen Code ausführt. Hier wird die Falle zugeschnappt.
    *   `element.innerHTML`: Schreibt eine Zeichenkette als HTML in ein Element. Der Browser parst diese Zeichenkette und führt eventuell enthaltene Skripte aus.
    *   `document.write()`: Schreibt direkt in den Dokumentenstrom.
    *   `eval()`: Führt eine Zeichenkette als JavaScript-Code aus. Dies ist fast immer eine schlechte Idee.
    *   `setTimeout()` / `setInterval()`: Wenn der erste Parameter ein String ist, wird er wie mit `eval()` ausgeführt.

Der Angriffspfad ist also: **Quelle → Dein JavaScript-Code → Senke**. Die Schwachstelle ist dein Code, der die Brücke zwischen einer unsicheren Quelle und einer gefährlichen Senke schlägt.

#### Ein praktisches Beispiel: Die personalisierte Begrüßung

Stell dir vor, du hast eine einfache Webseite, die Besucher persönlich begrüßen soll. Der Name des Besuchers soll aus dem URL-Fragment (dem Teil nach dem `#`) gelesen und auf der Seite angezeigt werden.

Deine HTML-Datei `welcome.html` könnte so aussehen:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <title>Willkommen!</title>
</head>
<body>
    <h1>Willkommen auf unserer Seite, <span id="username">Gast</span>!</h1>

    <script>
        // Lies den Namen aus dem URL-Fragment
        let name = location.hash.substring(1); // .substring(1) entfernt das '#'

        // Wenn ein Name vorhanden ist, zeige ihn an
        if (name) {
            document.getElementById('username').innerHTML = name;
        }
    </script>
</body>
</html>
```

Ein normaler Aufruf sieht harmlos aus:
`https://deine-seite.com/welcome.html#Maria`

Das Skript liest "Maria" aus `location.hash`, und die `h1`-Überschrift wird zu "Willkommen auf unserer Seite, Maria!". Alles funktioniert wie erwartet.

Jetzt kommt der Angreifer. Er erkennt, dass der Inhalt von `location.hash` direkt in die `innerHTML`-Eigenschaft geschrieben wird. `innerHTML` ist eine bekannte, gefährliche Senke. Der Angreifer präpariert nun eine spezielle URL und schickt sie an ein Opfer, zum Beispiel per E-Mail oder in einem Forum:

`https://deine-seite.com/welcome.html#<img src=x onerror=alert('XSS-Angriff!')>`

Was passiert, wenn das Opfer diesen Link anklickt?

1.  Der Browser fordert die Seite `welcome.html` vom Server an. Wichtig: Der Teil `#<img ...>` wird **nicht** an den Server gesendet. Der Server sieht nur eine Anfrage für `/welcome.html`. Aus seiner Sicht ist alles in Ordnung.
2.  Die Seite wird geladen. Dein JavaScript-Code wird ausgeführt.
3.  `location.hash` enthält den Wert `"#<img src=x onerror=alert('XSS-Angriff!')>"`.
4.  Dein Skript liest diesen Wert und schreibt ihn per `innerHTML` in das `span`-Element mit der ID `username`.
5.  Das DOM wird aktualisiert. Der Browser sieht nun neuen HTML-Code innerhalb des `span`-Elements: `<img src=x onerror=alert('XSS-Angriff!')>`.
6.  Der Browser versucht, dieses Bild zu laden. Die Quelle `src=x` ist ungültig, was einen Fehler auslöst.
7.  Der `onerror`-Event-Handler des Bildes wird ausgelöst.
8.  Der JavaScript-Code im `onerror`-Attribut – `alert('XSS-Angriff!')` – wird ausgeführt.

Ein `alert()` ist nur ein harmloser Proof-of-Concept. Ein echter Angreifer würde hier Code einfügen, der die Session-Cookies des Nutzers stiehlt, seine Tastatureingaben aufzeichnet oder ihn auf eine Phishing-Seite weiterleitet. Und das alles, ohne dass dein Server jemals den bösartigen Code gesehen hat.

#### Gegenmaßnahmen: Den clientseitigen Code absichern

Da die Schwachstelle im clientseitigen Code liegt, muss auch die Verteidigung dort ansetzen. Die gute Nachricht ist, dass du die volle Kontrolle darüber hast.

##### 1. Vermeide gefährliche Senken

Die einfachste Regel lautet: Wenn du nur Text anzeigen willst, nutze auch nur Methoden, die Text verarbeiten. Die gefährliche `innerHTML`-Eigenschaft hat ein sicheres Gegenstück: `textContent`.

Lass uns den verwundbaren Code von oben korrigieren:

```javascript
// ...
if (name) {
    // SICHER: textContent interpretiert die Eingabe als reinen Text.
    document.getElementById('username').textContent = name;
}
```

Wenn ein Angreifer nun die bösartige URL von vorhin verwendet, passiert Folgendes: Das `span`-Element enthält danach den *sichtbaren Text* `<img src=x onerror=alert('XSS-Angriff!')>`. Der Browser wird diesen String nicht als HTML parsen, sondern ihn einfach als Zeichenkette anzeigen. Der Angriff ist damit vollständig abgewehrt.

Merke dir als Faustregel:
*   Verwende **`textContent`**, wenn du Text in ein Element einfügen willst.
*   Verwende **`element.setAttribute()`** für Attribute, aber sei vorsichtig bei `href`, `src` oder `style`.
*   Verwende **niemals** `innerHTML`, `outerHTML` oder `document.write()` mit Daten, die du nicht selbst kontrollierst.

##### 2. Clientseitiges Sanitizing, wenn HTML sein muss

Manchmal musst du aber tatsächlich HTML-Code von einem Nutzer entgegennehmen und darstellen – zum Beispiel in einem Kommentarfeld mit Formatierungsoptionen. In diesem Fall reicht `textContent` nicht aus.

Hier kommt das **Sanitizing** (Bereinigen) ins Spiel. Bevor du den HTML-String in eine gefährliche Senke wie `innerHTML` schreibst, musst du ihn durch einen "Filter" schicken, der alle potenziell gefährlichen Elemente und Attribute entfernt. Dazu gehören `<script>`-Tags, `onerror`-Attribute, `javascript:`-URLs in `href`-Attributen und vieles mehr.

**Schreibe niemals deinen eigenen Sanitizer!** Das ist eine extrem komplexe und fehleranfällige Aufgabe. Verlasse dich stattdessen auf etablierte und gut gewartete Bibliotheken. Eine der bekanntesten und vertrauenswürdigsten ist **DOMPurify**.

So würde die sichere Implementierung mit DOMPurify aussehen:

Zuerst bindest du die Bibliothek in dein Projekt ein:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/dompurify/3.0.6/purify.min.js"></script>
```

Dann passt du deinen Code an, um die Eingabe zu bereinigen, bevor du sie verwendest:

```javascript
// ...
if (name) {
    // 1. Bereinige die Eingabe mit DOMPurify
    let cleanName = DOMPurify.sanitize(name);

    // 2. Schreibe erst dann den bereinigten HTML-Code ins DOM
    document.getElementById('username').innerHTML = cleanName;
}
```

Wenn der Angreifer jetzt seinen Payload schickt, wird DOMPurify aktiv. Es analysiert den String `<img src=x onerror=alert('XSS-Angriff!')>` und erkennt das gefährliche `onerror`-Attribut. Die Bibliothek entfernt es. Übrig bleibt nur noch `<img src=x>`. Dieser harmlose Rest wird dann ins DOM geschrieben. Der Angriff scheitert.

##### 3. Content Security Policy (CSP)

Als zusätzliche Verteidigungslinie kannst du eine Content Security Policy (CSP) einsetzen. Dies ist ein HTTP-Header, den dein Server mitsenden kann und der dem Browser strenge Regeln auferlegt, welche Inhalte ausgeführt werden dürfen. Du könntest zum Beispiel Inline-Skripte (`<script>...</script>` und Event-Handler wie `onerror`) komplett verbieten. Eine solche Regel hätte den oben gezeigten Angriff ebenfalls verhindert, selbst wenn dein JavaScript-Code verwundbar gewesen wäre. CSP ist eine mächtige, aber fortgeschrittene Technik, die als "Sicherheitsnetz" dient.

DOM-based XSS ist eine subtile Bedrohung, die ein tiefes Verständnis für das Zusammenspiel von JavaScript und dem DOM erfordert. Als moderner Webentwickler arbeitest du täglich an der Front, an der diese Angriffe stattfinden. Indem du unsichere Quellen und gefährliche Senken kennst und konsequent sichere Programmierpraktiken anwendest, baust du robuste und widerstandsfähige Anwendungen, die deine Nutzer schützen.
