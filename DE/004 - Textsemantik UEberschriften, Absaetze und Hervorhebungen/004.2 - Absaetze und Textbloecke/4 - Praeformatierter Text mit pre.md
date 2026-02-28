# Präformatierter Text mit pre

### Präformatierter Text mit `<pre>`: Wenn jeder Leerschritt zählt

In der Welt von HTML herrscht normalerweise eine klare Regel: Der Browser ist dein Aufräumdienst. Wenn du in deinem HTML-Code mehrere Leerzeichen hintereinander schreibst, fasst der Browser sie zu einem einzigen zusammen. Wenn du Zeilenumbrüche mit der Enter-Taste einfügst, ignoriert er sie einfach. Dieses Verhalten ist in den meisten Fällen äußerst praktisch. Es erlaubt dir, deinen Code für eine bessere Lesbarkeit zu formatieren, ohne dass diese Formatierung das Aussehen deiner Webseite beeinflusst. Ein Absatz bleibt ein Absatz, egal wie viele Leerzeilen du im Editor dazwischen lässt.

Doch was, wenn genau diese Leerzeichen und Zeilenumbrüche eine entscheidende Bedeutung haben? Was, wenn die Einrückung nicht nur der Übersicht im Code dient, sondern ein wesentlicher Teil des Inhalts ist? Stell dir vor, du möchtest ein Code-Beispiel, ein Gedicht oder eine ASCII-Zeichnung auf deiner Webseite darstellen. Hier würde das automatische „Aufräumen“ des Browsers die gesamte Struktur und damit den Sinn zerstören.

Genau für diese Fälle gibt es das `<pre>`-Element. Der Name steht für „preformatted“ – also vorformatiert. Alles, was du innerhalb eines `<pre>`-Tags platzierst, wird vom Browser exakt so dargestellt, wie du es in deinem HTML-Dokument geschrieben hast. Jeder Leerschritt, jede Tabulator-Einrückung und jeder Zeilenumbruch bleibt erhalten.

#### Die Superkraft der exakten Darstellung

Sehen wir uns das an einem einfachen Beispiel an. Angenommen, du möchtest eine simple Baumstruktur mit Textzeichen darstellen. Ohne das `<pre>`-Element würde dein Code so aussehen:

```html
<p>
Projektordner
  ├── index.html
  ├── css
  │   └── style.css
  └── js
      └── script.js
</p>
```

Der Browser würde diesen Code nehmen, alle überflüssigen Leerzeichen und Zeilenumbrüche entfernen und das Ergebnis als eine einzige, unleserliche Zeile ausgeben:

`Projektordner ├── index.html ├── css │ └── style.css └── js └── script.js`

Die gesamte Struktur ist verloren gegangen. Wenn du diesen Inhalt jedoch in ein `<pre>`-Element einbettest, ändert sich alles:

```html
<pre>
Projektordner
  ├── index.html
  ├── css
  │   └── style.css
  └── js
      └── script.js
</pre>
```

Das Ergebnis im Browser ist nun eine exakte Kopie dessen, was du im Editor siehst. Jeder Leerschritt und jede neue Zeile wird respektiert, und die visuelle Hierarchie bleibt intakt.

Eine weitere Eigenschaft des `<pre>`-Elements ist, dass der Browser den Inhalt standardmäßig in einer Schriftart mit fester Zeichenbreite (monospace) darstellt, wie zum Beispiel Courier oder Consolas. Bei diesen Schriftarten nimmt jedes Zeichen exakt den gleichen horizontalen Platz ein. Ein „i“ ist also genauso breit wie ein „m“. Das ist entscheidend für die korrekte Ausrichtung von spaltenbasierten Inhalten wie Code oder ASCII-Art.

#### Der häufigste Anwendungsfall: Code-Beispiele

Der mit Abstand häufigste und wichtigste Einsatzbereich für das `<pre>`-Element ist die Darstellung von Quellcode. In fast jeder Programmiersprache ist die Einrückung (Indentation) von entscheidender Bedeutung für die Lesbarkeit. Manchmal ist sie, wie in Python, sogar Teil der Syntax.

Wenn du also ein Code-Snippet auf deiner Webseite präsentieren möchtest, ist `<pre>` dein Werkzeug der Wahl. Allerdings gibt es hier eine wichtige Feinheit zu beachten. HTML-Code selbst enthält Zeichen, die für den Browser eine besondere Bedeutung haben, allen voran die spitzen Klammern `<` und `>`. Würdest du versuchen, ein HTML-Snippet direkt in ein `<pre>`-Tag zu schreiben, würde der Browser es als Teil deiner Seite interpretieren und nicht als anzuzeigenden Text.

```html
<!-- FALSCH! Der Browser wird hier versuchen, ein h1- und ein p-Element zu rendern. -->
<pre>
  <h1>Eine Überschrift</h1>
  <p>Ein Absatztext.</p>
</pre>
```

Um das zu verhindern, musst du diese Sonderzeichen durch ihre HTML-Entitäten ersetzen. Die wichtigsten sind:
*   `<` wird zu `&lt;` (less than)
*   `>` wird zu `&gt;` (greater than)
*   `&` wird zu `&amp;` (ampersand)

Der korrekte Weg, das obige Beispiel darzustellen, wäre also:

```html
<pre>
  &lt;h1&gt;Eine Überschrift&lt;/h1&gt;
  &lt;p&gt;Ein Absatztext.&lt;/p&gt;
</pre>
```

#### Die semantische Ergänzung: Das `<code>`-Element

Während `<pre>` dem Browser sagt, *wie* der Text formatiert werden soll (nämlich gar nicht, er soll die Vorformatierung beibehalten), gibt es ein weiteres Element, das ihm sagt, *was* der Text ist: das `<code>`-Element.

Semantisch korrekt ist es, Code-Blöcke sowohl in `<pre>` als auch in `<code>` zu verschachteln.

```html
<pre><code>
function gruss(name) {
  console.log("Hallo, " + name + "!");
}
</code></pre>
```

Diese Kombination ist die bewährte Methode und kommuniziert unmissverständlich deine Absicht:
1.  **`<pre>`:** Kümmert sich um die Präsentation. Es sorgt für die Erhaltung von Leerräumen und Zeilenumbrüchen und wählt eine Monospace-Schriftart.
2.  **`<code>`:** Kümmert sich um die Semantik. Es teilt dem Browser, Suchmaschinen und assistiven Technologien (wie Screenreadern) mit, dass es sich bei diesem Textblock um Computercode handelt.

Diese Trennung von Präsentation und Bedeutung ist ein Kernprinzip von gutem HTML. Während das `<code>`-Element auch allein für kurze Code-Schnipsel innerhalb eines Fließtextes verwendet werden kann (z. B. `Die Funktion `<code>`getElementById()`</code>` ist sehr nützlich.`), ist für mehrzeilige Blöcke die Kombination mit `<pre>` der Goldstandard.

#### Mehr als nur Code: Weitere Einsatzmöglichkeiten

Obwohl Code das Haupteinsatzgebiet ist, glänzt das `<pre>`-Element auch in anderen Nischen:

*   **ASCII-Art:** Die kunstvollen Bilder, die nur aus Textzeichen bestehen, sind vollständig von der exakten Positionierung jedes Zeichens abhängig. `<pre>` ist die einzige Möglichkeit, sie korrekt im Web darzustellen.
*   **Gedichte und Songtexte:** Hier sind Zeilenumbrüche und Einrückungen oft ein stilistisches Mittel, das den Rhythmus und die Betonung vorgibt. Mit `<pre>` stellst du sicher, dass das Werk so angezeigt wird, wie es vom Autor beabsichtigt war.
*   **Konsolenausgaben oder Log-Dateien:** Wenn du die Ausgabe eines Kommandozeilen-Programms oder den Inhalt einer Log-Datei exakt wiedergeben möchtest, ist `<pre>` unverzichtbar, um die tabellarische Struktur und die Abstände zu bewahren.

#### Umgang mit langen Zeilen und Styling

Ein potenzielles Problem bei der Verwendung von `<pre>` sind sehr lange Zeilen, die nicht automatisch umbrochen werden. Das kann dazu führen, dass der Inhalt über den Rand deines Layouts hinausragt und einen horizontalen Scrollbalken für die gesamte Seite erzwingt, was aus Nutzersicht sehr störend ist.

Glücklicherweise lässt sich das mit ein wenig CSS leicht beheben. Du kannst dem `<pre>`-Element eine Eigenschaft geben, die entweder einen Scrollbalken nur für diesen Block hinzufügt oder einen automatischen Zeilenumbruch erzwingt.

**Option 1: Scrollbalken für den Block**
Diese Lösung bewahrt die Integrität der langen Zeilen und ist oft für Code-Beispiele die beste Wahl.

```css
pre {
  overflow-x: auto; /* Fügt einen horizontalen Scrollbalken hinzu, wenn nötig */
}
```

**Option 2: Automatischer Zeilenumbruch**
Diese Option bricht lange Zeilen um, damit sie in den verfügbaren Platz passen. Das kann die Lesbarkeit von Code beeinträchtigen, ist aber für reinen Text oft besser geeignet.

```css
pre {
  white-space: pre-wrap; /* Erhält Leerräume und Zeilenumbrüche, bricht aber lange Zeilen um */
}
```

Darüber hinaus wird ein `<pre>`-Block oft visuell vom restlichen Text abgehoben, um seine besondere Natur zu betonen. Ein typisches Styling könnte so aussehen:

```css
pre {
  background-color: #f4f4f4; /* Ein heller Hintergrund */
  border: 1px solid #ddd;   /* Ein dezenter Rahmen */
  border-radius: 4px;       /* Abgerundete Ecken */
  padding: 1em;             /* Innenabstand */
  overflow-x: auto;         /* Scrollbalken für lange Zeilen */
}

code {
  font-family: 'Courier New', Courier, monospace; /* Sicherstellen, dass die Schriftart passt */
}
```

Das `<pre>`-Element mag auf den ersten Blick wie ein einfaches Werkzeug wirken, aber es löst ein fundamentales Problem bei der Darstellung von Text im Web. Es gibt dir die Kontrolle zurück, wenn die automatische Formatierung des Browsers nicht erwünscht ist, und ermöglicht es dir, Inhalte, deren Struktur ebenso wichtig ist wie ihr Inhalt, präzise und originalgetreu zu präsentieren.
