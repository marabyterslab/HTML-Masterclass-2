# Gefahr von innerHTML

### Die Gefahr von `innerHTML`: Wenn der Browser blind vertraut

In der Welt der Webentwicklung gibt es Werkzeuge, die so praktisch und mächtig sind, dass man sie am liebsten für alles verwenden würde. Die Eigenschaft `innerHTML` ist ein solcher Kandidat. Auf den ersten Blick ist sie ein Traum: Mit einer einzigen Zuweisung kannst du komplexe HTML-Strukturen in ein DOM-Element einfügen, ohne mühsam jedes einzelne Element von Hand erstellen zu müssen. Ein simpler String genügt, und wie von Zauberhand erscheint eine fertige Komponente auf deiner Webseite.

Stell dir vor, du möchtest eine Willkommensnachricht für einen Benutzer anzeigen:

```javascript
// Der Name des Benutzers kommt aus einer Variable
const userName = "Alex";

// Wir suchen uns das passende DOM-Element
const welcomeBox = document.getElementById('welcome-message');

// Und füllen es mit einem dynamischen HTML-String
welcomeBox.innerHTML = `<h1>Willkommen zurück, ${userName}!</h1><p>Wir hoffen, du hast einen tollen Tag.</p>`;
```

Das Ergebnis ist genau das, was du erwartest. Der Browser nimmt den String, interpretiert ihn als HTML und rendert ihn im `welcome-box`-Container. Das ist schnell, lesbar und unglaublich effizient. Doch genau in dieser Einfachheit und Macht liegt eine der größten und am häufigsten ausgenutzten Sicherheitslücken im Web: Cross-Site Scripting (XSS).

#### Das Kernproblem: Blinder Gehorsam

Das grundlegende Missverständnis bei `innerHTML` ist die Annahme, es würde einfach nur Text und HTML-Tags einfügen. Das ist nur die halbe Wahrheit. Wenn du `innerHTML` einen String zuweist, passiert im Hintergrund etwas Entscheidendes: Der Browser *parst* diesen String. Das bedeutet, er liest ihn nicht nur, sondern interpretiert ihn aktiv als HTML-Code und führt ihn aus. Er behandelt den String mit demselben Vertrauen wie den ursprünglichen HTML-Code, den er vom Server erhalten hat.

Und genau hier liegt die Gefahr. Was passiert, wenn der String, den du einfügst, nicht von dir selbst stammt, sondern von einer externen Quelle? Was, wenn er aus einem Kommentarfeld, einem Benutzernamenfeld oder einem URL-Parameter kommt?

Schauen wir uns ein einfaches Gästebuch an. Ein Benutzer kann einen Kommentar hinterlassen, der dann für alle anderen sichtbar auf der Seite angezeigt wird. Der Code dafür könnte so aussehen:

```javascript
// Funktion, die einen neuen Kommentar hinzufügt
function addComment(userInput) {
  const commentSection = document.getElementById('comments');
  const newComment = document.createElement('div');
  newComment.innerHTML = userInput; // Die gefährliche Zeile!
  commentSection.appendChild(newComment);
}

// Angenommen, ein Benutzer gibt diesen "Kommentar" ein:
const maliciousInput = "<script>alert('Deine Sitzung wurde gestohlen!');</script>";

addComment(maliciousInput);
```

Wenn dieser Code ausgeführt wird, fügt er nicht einfach den Text `<script>alert(...)</script>` in die Seite ein. Nein, der Browser sieht den `<script>`-Tag und sagt sich: "Ah, hier ist ausführbarer JavaScript-Code! Den muss ich sofort ausführen." Im nächsten Moment erscheint ein Alert-Fenster auf dem Bildschirm des ahnungslosen Besuchers.

Dieser einfache `alert` ist nur die Spitze des Eisbergs. Ein Angreifer kann weitaus bösartigeren Code einschleusen. Statt eines Alerts könnte das Skript:

*   **Cookies stehlen:** Mit `document.cookie` kann das Skript die Session-Cookies des Benutzers auslesen und an den Server des Angreifers senden. Damit kann der Angreifer die Sitzung des Benutzers kapern und sich als dieser ausgeben.
*   **Benutzer umleiten:** `window.location.href = 'https://boesartige-seite.de'` leitet den Benutzer auf eine Phishing-Seite um, die exakt so aussieht wie deine, aber dazu dient, Passwörter abzugreifen.
*   **Formulare manipulieren:** Das Skript könnte das Ziel eines Login-Formulars ändern, sodass die Zugangsdaten nicht an deinen Server, sondern an den des Angreifers gesendet werden.
*   **Keylogger installieren:** Es könnte einen Event-Listener für Tastatureingaben registrieren und alles, was der Benutzer tippt, aufzeichnen und versenden.

Das Gefährliche daran ist, dass dieser Code im Kontext deiner Webseite und mit den Rechten des angemeldeten Benutzers ausgeführt wird. Der Browser kann nicht unterscheiden, ob das Skript von dir oder von einem Angreifer stammt. Er führt es einfach aus.

#### Mehr als nur `<script>`-Tags

Ein weit verbreiteter Irrglaube ist, dass es ausreicht, das Wort "script" aus der Benutzereingabe zu filtern. Das ist ein fataler Fehler. Angreifer sind kreativ und kennen unzählige Wege, JavaScript auszuführen, ohne explizit einen `<script>`-Tag zu verwenden.

Hier sind nur einige Beispiele für bösartige Eingaben, die eine `innerHTML`-Zuweisung ausnutzen können:

```html
<!-- Ein Bild, das nicht geladen werden kann, führt den onerror-Handler aus -->
<img src="x" onerror="alert('XSS über ein Bild!')">

<!-- Ein SVG-Bild kann eingebettetes Skript enthalten -->
<svg onload="alert('XSS über SVG!')">

<!-- Ein Link mit dem javascript:-Protokoll -->
<a href="javascript:alert('XSS über einen Link!')">Unschuldiger Link</a>

<!-- Ein Video, das beim Suchen einen Fehler auslöst -->
<video><source onerror="alert('XSS über Video!')">
```

Der Versuch, all diese und viele weitere Vektoren manuell durch das Filtern von Zeichenketten (Blacklisting) zu blockieren, ist zum Scheitern verurteilt. Es ist ein endloses Katz-und-Maus-Spiel, das du als Entwickler fast immer verlieren wirst.

#### Die sicheren Alternativen

Glücklicherweise gibt es robuste und einfache Wege, Inhalte sicher in eine Webseite einzufügen, ohne die Tür für XSS-Angriffe weit aufzustoßen. Die goldene Regel lautet: **Behandle jede Benutzereingabe als reinen Text, nicht als ausführbaren Code**, es sei denn, du weißt genau, was du tust.

##### 1. Die erste Wahl: `textContent`

Wenn du wirklich nur Text einfügen möchtest – und das ist in den meisten Fällen der Fall –, dann ist die Eigenschaft `textContent` dein bester Freund. `textContent` tut genau das, was sein Name verspricht: Es interpretiert den zugewiesenen String als reinen Text. HTML-Tags werden nicht geparst, sondern als literale Zeichen angezeigt.

Nehmen wir unser Gästebuchbeispiel von vorhin und ersetzen `innerHTML` durch `textContent`:

```javascript
function addCommentSafely(userInput) {
  const commentSection = document.getElementById('comments');
  const newComment = document.createElement('div');
  newComment.textContent = userInput; // Sicher!
  commentSection.appendChild(newComment);
}

const maliciousInput = "<script>alert('Deine Sitzung wurde gestohlen!');</script>";

addCommentSafely(maliciousInput);
```

Was passiert jetzt? Auf der Webseite wird nun exakt der Text `"<script>alert('Deine Sitzung wurde gestohlen!');</script>"` angezeigt. Der Browser führt nichts aus. Er zeigt die Zeichen `<` und `>` einfach an. Die Gefahr ist gebannt.

##### 2. Der strukturierte Weg: `createElement` und `appendChild`

Manchmal möchtest du jedoch bewusst eine DOM-Struktur erstellen. Anstatt einen HTML-String zusammenzubasteln, solltest du die nativen DOM-Methoden verwenden. Das ist zwar etwas mehr Schreibarbeit, aber dafür absolut sicher und explizit.

Angenommen, du möchtest den Benutzernamen in einem `<strong>`-Tag und den Kommentartext in einem `<p>`-Tag ausgeben:

```javascript
function addStructuredComment(username, commentText) {
  const commentSection = document.getElementById('comments');

  // Erstelle die DOM-Elemente manuell
  const commentContainer = document.createElement('div');
  const userElement = document.createElement('strong');
  const textElement = document.createElement('p');

  // Fülle sie sicher mit textContent
  userElement.textContent = username;
  textElement.textContent = commentText;

  // Baue die Struktur zusammen
  commentContainer.appendChild(userElement);
  commentContainer.appendChild(textElement);
  
  commentSection.appendChild(commentContainer);
}

// Selbst wenn der Benutzername oder Kommentar bösartigen Code enthält,
// wird er nur als Text dargestellt.
addStructuredComment(
  "Angreifer", 
  "<img src='x' onerror='alert(\"Hoppla!\")'>"
);
```

Dieser Ansatz trennt die Struktur (die du als Entwickler definierst) sauber von den Daten (die vom Benutzer kommen). Es gibt keine Möglichkeit, dass der `commentText` aus seinem `<p>`-Tag ausbricht und als HTML interpretiert wird.

##### 3. Der fortgeschrittene Weg: HTML Sanitizing

Es gibt legitime Anwendungsfälle, in denen Benutzer eine begrenzte Auswahl an HTML-Formatierungen verwenden dürfen sollen, zum Beispiel in einem Rich-Text-Editor für Blogartikel. Hier sind sowohl `innerHTML` (zu unsicher) als auch `textContent` (zu restriktiv) ungeeignet.

Die Lösung heißt **HTML Sanitizing** (Säuberung). Ein Sanitizer ist ein spezielles Werkzeug, das einen HTML-String entgegennimmt, ihn parst und eine bereinigte Version zurückgibt. Dabei wird eine Whitelist von erlaubten Tags (z. B. `<b>`, `<i>`, `<ul>`, `<li>`) und Attributen (z. B. `href` für `<a>`-Tags, aber nicht `onclick`) angewendet. Alles, was potenziell gefährlich ist – `<script>`-Tags, `onerror`-Attribute, `javascript:`-Links –, wird restlos entfernt.

**Wichtig:** Schreibe niemals deinen eigenen Sanitizer! Das ist eine hochkomplexe Aufgabe, bei der man leicht Fehler machen kann. Verwende stattdessen etablierte und gut getestete Bibliotheken. Eine der bekanntesten im JavaScript-Ökosystem ist **DOMPurify**.

So einfach kann die Verwendung aussehen:

```javascript
// Zuerst musst du die DOMPurify-Bibliothek einbinden.
// Angenommen, userInput kommt von einem Rich-Text-Editor.
const dirtyHTML = `Hallo! <b>Das ist fett.</b> <img src="x" onerror="alert('Gefahr!')">`;

// Säubere den String mit DOMPurify
const cleanHTML = DOMPurify.sanitize(dirtyHTML);

// Jetzt kannst du den gesäuberten String sicher mit innerHTML verwenden
const outputElement = document.getElementById('output');
outputElement.innerHTML = cleanHTML;
```

Das Ergebnis im `outputElement` wäre: `Hallo! <b>Das ist fett.</b> <img src="x">`. Der gefährliche `onerror`-Handler wurde entfernt.

Moderne Browser beginnen auch, eine native Sanitizer API bereitzustellen, die diesen Prozess in Zukunft noch einfacher machen wird.

Die Eigenschaft `innerHTML` ist ein mächtiges, aber zweischneidiges Schwert. Ihre unbedachte Verwendung mit von außen kommenden Daten ist eines der größten Einfallstore für Sicherheitslücken. Indem du standardmäßig auf sichere Alternativen wie `textContent` und die programmatische DOM-Erstellung setzt und nur in Ausnahmefällen auf robuste Sanitizing-Bibliotheken zurückgreifst, baust du sicherere und widerstandsfähigere Webanwendungen. Vertraue niemals Eingaben, die du nicht selbst kontrollierst.
