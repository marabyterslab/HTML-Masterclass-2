# Code-Blöcke und Syntax-Highlighting

### Code-Blöcke und Syntax-Highlighting: Code verständlich präsentieren

Wenn du eine Dokumentationsseite erstellst, ist eines deiner wichtigsten Werkzeuge die Fähigkeit, Code-Beispiele klar und verständlich darzustellen. Egal, ob du eine API erklärst, die Nutzung einer Komponente zeigst oder ein Tutorial schreibst – der Code ist oft das Herzstück deiner Inhalte. Ihn einfach als normalen Text in einen Absatz zu packen, wäre nicht nur unschön, sondern auch unprofessionell und schwer lesbar. Hier kommen spezielle HTML-Elemente und Techniken ins Spiel, die genau für diesen Zweck geschaffen wurden.

#### Die semantische Grundlage: `<pre>` und `<code>`

HTML bietet uns zwei grundlegende Bausteine, um Code korrekt auszuzeichnen: das `<code>`-Element und das `<pre>`-Element. Oft werden sie zusammen verwendet, aber sie haben unterschiedliche Aufgaben.

##### Das `<code>`-Element für Inline-Code

Das `<code>`-Element ist für kurze, einzelne Code-Ausschnitte gedacht, die direkt im Fließtext vorkommen. Stell dir vor, du erwähnst einen Funktionsnamen, eine Variable oder einen HTML-Tag in einem Satz. Mit `<code>` markierst du diesen Teil als Computercode.

Browser stellen den Inhalt von `<code>`-Tags standardmäßig in einer Monospace-Schriftart dar (wie Courier oder Consolas), was ihn sofort visuell vom restlichen Text abhebt.

Ein Beispiel im Text:
Um ein Element anhand seiner ID zu finden, verwendest du die JavaScript-Funktion `getElementById()`. Der dazugehörige CSS-Selektor wäre `#meinElement`.

So sieht der HTML-Code dafür aus:
```html
<p>
  Um ein Element anhand seiner ID zu finden, verwendest du die
  JavaScript-Funktion <code>getElementById()</code>.
  Der dazugehörige CSS-Selektor wäre <code>#meinElement</code>.
</p>
```
Das ist einfach und effektiv für kleine Schnipsel. Aber was ist mit ganzen Code-Blöcken?

##### Das `<pre>`-Element für vorformatierten Text

Wenn du mehrzeilige Code-Beispiele hast, stehst du vor einem Problem: HTML ignoriert standardmäßig Leerzeichen und Zeilenumbrüche. Mehrere Leerzeichen werden zu einem zusammengefasst und ein Zeilenumbruch im Code-Editor hat keine Auswirkung auf die Darstellung im Browser. Genau hier setzt das `<pre>`-Element (kurz für "preformatted") an.

Alles, was du in ein `<pre>`-Tag schreibst, wird exakt so dargestellt, wie du es eingegeben hast – inklusive aller Einrückungen, Leerzeichen und Zeilenumbrüche. Auch hier wird standardmäßig eine Monospace-Schriftart verwendet.

##### Die perfekte Kombination: `<pre>` und `<code>`

Für die semantisch korrekte und robusteste Darstellung von Code-Blöcken kombinierst du beide Elemente. Das `<pre>`-Element sorgt für die Erhaltung des Layouts (Whitespace), während das `<code>`-Element den Inhalt als Code kennzeichnet. Diese Kombination ist der Goldstandard für die Auszeichnung von Code-Blöcken in HTML.

```html
<pre><code>
function gruss(name) {
  // Zeigt eine einfache Begrüßung an
  console.log(`Hallo, ${name}! Willkommen auf unserer Doku-Seite.`);
}

gruss('Entwickler');
</code></pre>
```

Wenn du diesen HTML-Code in einem Browser öffnest, siehst du einen sauber formatierten, aber noch recht eintönigen Block aus grau-schwarzem Text. Es ist funktional, aber es fehlt die visuelle Hilfe, die wir aus unseren Code-Editoren gewohnt sind. Es fehlt die Magie der Farben.

#### Syntax-Highlighting: Farbe ins Spiel bringen

Syntax-Highlighting ist der Prozess, bei dem verschiedene Teile des Codes (wie Schlüsselwörter, Variablen, Strings, Kommentare) farblich hervorgehoben werden. Das ist keine reine Dekoration; es erfüllt wichtige Funktionen:

*   **Lesbarkeit:** Es wird sofort klar, was ein Befehl, was ein Text und was ein Kommentar ist. Das menschliche Auge kann die Struktur des Codes viel schneller erfassen.
*   **Fehlererkennung:** Ein Tippfehler in einem Schlüsselwort oder ein nicht geschlossener String fällt durch die fehlende oder falsche Färbung oft sofort auf.
*   **Strukturverständnis:** Logische Blöcke, Funktionen und Schleifen werden visuell gruppiert, was das Verständnis der Code-Architektur erleichtert.

HTML und CSS allein können kein echtes Syntax-Highlighting durchführen. Sie wissen nicht, was ein "Schlüsselwort" in JavaScript oder eine "Property" in CSS ist. Diese Logik muss von außen kommen, und zwar in der Regel durch eine JavaScript-Bibliothek.

#### Wie funktioniert Syntax-Highlighting im Browser?

Die grundlegende Idee hinter den meisten Syntax-Highlighting-Bibliotheken ist faszinierend und clever. Sie durchlaufen auf deiner Webseite einen Prozess, der sich in etwa so beschreiben lässt:

1.  **Finden:** Die JavaScript-Bibliothek sucht im DOM (Document Object Model) deiner Seite nach allen `<pre><code>`-Blöcken.
2.  **Analysieren (Parsing):** Für jeden gefundenen Block liest das Skript den reinen Textinhalt aus. Anhand einer vordefinierten Grammatik für die jeweilige Programmiersprache (z. B. JavaScript, Python, PHP) zerlegt es den Code in seine Bestandteile, die sogenannten "Tokens". Ein Token kann ein Schlüsselwort (`function`), ein String (`'Hallo Welt'`), ein Kommentar (`// Das ist ein Kommentar`) oder ein Operator (`=`) sein.
3.  **Umschließen:** Nachdem der Code in Tokens zerlegt wurde, baut die Bibliothek den HTML-Inhalt des `<code>`-Elements dynamisch neu auf. Jeder Token wird in ein `<span>`-Element mit einer spezifischen CSS-Klasse eingewickelt.
4.  **Stylen:** Ein passendes CSS-Stylesheet, das du ebenfalls einbindest, enthält die Regeln für diese Klassen und weist ihnen die entsprechenden Farben und Schriftstile zu.

Schauen wir uns das an unserem vorherigen Beispiel an. Der ursprüngliche HTML-Code war:

```html
<pre><code>function gruss(name) { ... }</code></pre>
```

Nachdem eine Bibliothek wie **Prism.js** ihre Arbeit getan hat, sieht der Code im Browser-Inspektor vielleicht so aus:

```html
<pre><code class="language-js">
  <span class="token keyword">function</span>
  <span class="token function">gruss</span>
  <span class="token punctuation">(</span>
  <span class="token parameter">name</span>
  <span class="token punctuation">)</span>
  <span class="token punctuation">{</span>
    <span class="token comment">// Zeigt eine einfache Begrüßung an</span>
    <span class="token maybe-class-name">console</span>
    <span class="token punctuation">.</span>
    <span class="token method function property-access">log</span>
    <span class="token punctuation">(</span>
    <span class="token template-string">
      <span class="token template-punctuation string">`</span>
      <span class="token string">Hallo, </span>
      <span class="token interpolation">
        <span class="token interpolation-punctuation punctuation">${</span>
        <span class="token expression">name</span>
        <span class="token interpolation-punctuation punctuation">}</span>
      </span>
      <span class="token string">! Willkommen auf unserer Doku-Seite.</span>
      <span class="token template-punctuation string">`</span>
    </span>
    <span class="token punctuation">)</span>
    <span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
</code></pre>
```

Das begleitende CSS-Stylesheet würde dann Regeln enthalten wie:

```css
/* Beispiel aus einem Prism-Theme */
.token.keyword {
  color: #c792ea;
}
.token.comment {
  color: #546e7a;
  font-style: italic;
}
.token.string {
  color: #c3e88d;
}
```

Das Ergebnis ist ein wunderschön formatierter und leicht lesbarer Code-Block, genau wie du ihn aus deiner Entwicklungsumgebung kennst.

#### Praktische Umsetzung mit einer Bibliothek wie Prism.js

Es gibt mehrere großartige Bibliotheken für Syntax-Highlighting, darunter `highlight.js`, `Shiki` oder `Prism.js`. Prism.js ist besonders bei Einsteigern beliebt, weil es leicht, erweiterbar und einfach zu integrieren ist.

So fügst du Prism.js zu deiner Dokumentationsseite hinzu:

**Schritt 1: Dateien einbinden**

Der einfachste Weg ist die Nutzung eines CDN (Content Delivery Network). Du fügst einfach eine CSS-Datei im `<head>` und eine JavaScript-Datei am Ende des `<body>` deiner HTML-Seite ein.

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Doku mit Code-Blöcken</title>
  <!-- 1. Prism.js Theme (CSS) einbinden -->
  <link href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism-okaidia.min.css" rel="stylesheet" />
</head>
<body>

  <h1>Beispiel: Ein JavaScript-Code-Block</h1>
  <p>Hier ist eine Funktion, um zwei Zahlen zu addieren:</p>

  <!-- Schritt 2: Deinen Code-Block vorbereiten -->
  <pre><code class="language-js">
function addiere(a, b) {
  // Gibt die Summe von a und b zurück
  return a + b;
}

const ergebnis = addiere(5, 10);
console.log(`Das Ergebnis ist: ${ergebnis}`);
  </code></pre>


  <!-- 3. Prism.js Core (JavaScript) einbinden -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/components/prism-core.min.js"></script>
  <!-- 4. Benötigte Sprachen laden -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/plugins/autoloader/prism-autoloader.min.js"></script>

</body>
</html>
```

**Schritt 2: Den Code-Block korrekt auszeichnen**

Damit Prism weiß, welche Grammatik es anwenden soll, musst du dem `<code>`-Element eine Klasse im Format `language-xxx` hinzufügen, wobei `xxx` die Abkürzung für die Sprache ist (z. B. `js`, `css`, `html`, `php`).

In unserem Beispiel haben wir `class="language-js"` verwendet. Prism's Autoloader erkennt diese Klasse und lädt automatisch die Grammatik für JavaScript nach, um den Code korrekt zu färben.

#### Nützliche Erweiterungen und Best Practices

Moderne Dokumentationsseiten bieten oft mehr als nur gefärbten Code. Viele Syntax-Highlighting-Bibliotheken bieten Plugins für zusätzliche Funktionalität:

*   **Zeilennummern:** Zeigt Nummern neben jeder Codezeile an, was die Referenzierung in Erklärungen erleichtert (`"siehe Zeile 5"`).
*   **"In Zwischenablage kopieren"-Button:** Ein kleiner Button am Rand des Code-Blocks, der es dem Benutzer ermöglicht, den gesamten Code-Schnipsel mit einem Klick zu kopieren. Dies ist ein enormes Plus für die Benutzerfreundlichkeit.
*   **Hervorheben von Zeilen:** Die Möglichkeit, bestimmte Zeilen farblich zu markieren, um die Aufmerksamkeit auf einen wichtigen Teil des Codes zu lenken.

Diese Funktionen werden in der Regel durch das Hinzufügen weiterer JavaScript-Plugins und entsprechender CSS-Klassen aktiviert.

Achte bei der Auswahl eines Farbschemas (Themes) immer auf einen guten Kontrast, um die Lesbarkeit für alle Nutzer, auch solche mit Sehschwächen, zu gewährleisten. Ein dunkles Theme auf einer dunklen Seite oder ein helles Theme auf einer hellen Seite funktioniert in der Regel am besten.

Durch die korrekte Verwendung von `<pre>` und `<code>` schaffst du eine solide, semantische Basis. Mit der Ergänzung durch eine JavaScript-Bibliothek für das Syntax-Highlighting verwandelst du deine einfachen Textblöcke in professionelle, lesbare und benutzerfreundliche Code-Beispiele – ein unverzichtbares Element jeder hochwertigen technischen Dokumentation.
