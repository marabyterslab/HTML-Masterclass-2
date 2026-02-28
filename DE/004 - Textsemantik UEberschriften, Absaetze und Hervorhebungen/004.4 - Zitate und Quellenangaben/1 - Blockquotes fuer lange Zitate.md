# Blockquotes für lange Zitate

### Blockzitate für lange Zitate: Wenn ein Satz nicht ausreicht

Manchmal stößt du beim Schreiben von Inhalten für deine Website auf Passagen aus anderen Quellen, die so prägnant oder wichtig sind, dass du sie wörtlich übernehmen möchtest. Ein kurzer Satz lässt sich leicht mit dem `<q>`-Element in den Fließtext integrieren. Was aber, wenn das Zitat einen ganzen Absatz oder sogar mehrere umfasst? Hierfür bietet HTML ein spezielles Element, das genau für diesen Zweck geschaffen wurde: das `<blockquote>`-Element.

#### Was ist ein Blockzitate?

Ein Blockzitat, im Englischen "blockquote", ist ein HTML-Element, das einen ganzen Inhaltsblock als Zitat aus einer anderen Quelle kennzeichnet. Im Gegensatz zum inline-Element `<q>`, das sich nahtlos in einen Satz einfügt, ist `<blockquote>` ein Block-Level-Element. Das bedeutet, es erzeugt einen eigenen, vom umgebenden Text abgesetzten Absatz.

Stell es dir wie in einem gedruckten Buch vor: Längere Zitate werden oft leicht eingerückt und mit etwas Abstand zum Haupttext dargestellt, um sie visuell hervorzuheben. Genau diese semantische und strukturelle Aufgabe erfüllt `<blockquote>` im Web.

Die grundlegende Syntax ist denkbar einfach:

```html
<blockquote>
  <p>Das ist der erste Absatz eines längeren Zitats, das ich von einer anderen Webseite oder aus einem Buch übernommen habe.</p>
  <p>Es kann sogar mehrere Absätze umfassen, die alle zusammen als eine Einheit zitiert werden.</p>
</blockquote>
```

Wichtig ist hierbei die Erkenntnis: Du nutzt `<blockquote>` nicht, weil du einen Text einrücken möchtest, sondern weil der Inhalt **semantisch** ein Zitat ist. Die visuelle Darstellung (die Einrückung) ist nur eine Standardformatierung der meisten Browser. Das tatsächliche Aussehen solltest du immer über CSS steuern. Der Missbrauch von `<blockquote>` nur für visuelle Effekte ist eine der häufigsten Fehlerquellen in der HTML-Semantik und schadet der Barrierefreiheit und Suchmaschinenoptimierung deiner Seite.

#### Die Quelle angeben mit dem `cite`-Attribut

Ein Zitat ohne Quellenangabe ist oft nur halb so viel wert. HTML bietet eine Möglichkeit, die Herkunft eines Zitats maschinenlesbar anzugeben: das `cite`-Attribut. In dieses Attribut fügst du eine URL ein, die direkt zur Quelle des Zitats führt.

```html
<blockquote cite="https://www.beispiel-quelle.de/artikel/ueber-zitate">
  <p>Ein Zitat ist die wörtliche oder nur inhaltliche Übernahme einer Aussage oder eines Textes an einer anderen Stelle.</p>
</blockquote>
```

Ein entscheidender Punkt, den du verstehen musst: Der Inhalt des `cite`-Attributs wird vom Browser **nicht** angezeigt. Er ist eine Metainformation, die für Maschinen gedacht ist. Suchmaschinen, Browser-Erweiterungen oder andere automatisierte Systeme können diese URL auslesen, um den Kontext und die Herkunft des Zitats zu verstehen. Für deine menschlichen Besucher bleibt diese Information jedoch unsichtbar.

#### Die sichtbare Quellenangabe: Ein Fall für `<figure>` und `<figcaption>`

Da das `cite`-Attribut für den Nutzer unsichtbar ist, brauchen wir eine Methode, um die Quelle auch für Menschen lesbar darzustellen. Schließlich gehört es zum guten Stil, den Autor oder das Werk zu nennen, aus dem man zitiert.

Die moderne und semantisch korrekteste Art, ein Blockzitat mit seiner sichtbaren Quellenangabe zu verbinden, ist die Verwendung der Elemente `<figure>` und `<figcaption>`.

*   **`<figure>`:** Dieses Element dient als Container für in sich geschlossene Inhalte, die aus dem Haupttextfluss herausgenommen werden könnten, ohne dessen Verständnis zu beeinträchtigen. Das können Bilder, Diagramme, Code-Beispiele oder eben auch Zitate sein.
*   **`<figcaption>`:** Dieses Element repräsentiert die Beschriftung oder Legende für den Inhalt des übergeordneten `<figure>`-Elements.

Indem du dein `<blockquote>` und die dazugehörige Quellenangabe in ein `<figure>`-Element packst, schaffst du eine logische Einheit. Die Quellenangabe selbst platzierst du in einem `<figcaption>`-Element.

Schauen wir uns ein vollständiges Beispiel an:

```html
<figure>
  <blockquote cite="https://developer.mozilla.org/de/docs/Web/HTML/Element/blockquote">
    <p>Das HTML-Element &lt;blockquote&gt; (oder HTML Block Quotation Element) kennzeichnet, dass der eingeschlossene Text ein erweitertes Zitat ist.</p>
  </blockquote>
  <figcaption>— MDN Web Docs, <cite>Element &lt;blockquote&gt;</cite></figcaption>
</figure>
```

Analysieren wir dieses Beispiel im Detail:

1.  **`<figure>`:** Der äußere Container, der Zitat und Quellenangabe logisch miteinander verbindet.
2.  **`<blockquote>`:** Das eigentliche Zitat. Das `cite`-Attribut verweist auf die maschinenlesbare Quelle.
3.  **`<figcaption>`:** Die für Menschen sichtbare Beschriftung. Hier nennen wir den Autor ("MDN Web Docs") und den Titel des Werks.
4.  **`<cite>`:** Achte auf das `<cite>`-Element innerhalb der `<figcaption>`. Dieses spezielle Element wird verwendet, um den Titel eines Werkes auszuzeichnen (z. B. ein Buch, ein Artikel, ein Film, ein Lied). Es ist semantisch falsch, den Namen einer Person in `<cite>` zu packen. Der Name des Autors steht als normaler Text da, während der Titel des Artikels korrekt als Werkzitat markiert ist.

Diese Struktur ist robust, semantisch aussagekräftig und bietet eine hervorragende Grundlage für die Gestaltung mit CSS.

#### Gestaltung von Blockzitaten mit CSS

Wie bereits erwähnt, ist die Standarddarstellung von Blockzitaten durch den Browser meist eine einfache Einrückung. Das ist funktional, aber selten ästhetisch ansprechend. Mit CSS hast du die volle Kontrolle über das Aussehen.

Ein gängiges Muster ist es, den linken Einzug des Browsers zu entfernen und stattdessen einen markanten linken Rand (border) zu setzen. Auch eine andere Schriftart oder -farbe kann die Lesbarkeit verbessern.

Hier ist ein einfaches CSS-Beispiel, das auf unserer `<figure>`-Struktur aufbaut:

```css
figure {
  margin: 2em 0; /* Etwas Abstand oben und unten */
}

blockquote {
  margin: 0; /* Standard-Einzug des Browsers entfernen */
  padding: 1em 1.5em;
  border-left: 5px solid #007bff; /* Ein blauer Rand links */
  background-color: #f8f9fa; /* Ein leichter Hintergrund */
  font-style: italic; /* Kursive Schrift für das Zitat */
  color: #333;
}

blockquote p {
  margin-bottom: 0.5em; /* Abstand zwischen Absätzen im Zitat */
}

blockquote p:last-child {
  margin-bottom: 0; /* Keinen Abstand nach dem letzten Absatz */
}

figcaption {
  margin-top: 0.5em;
  text-align: right; /* Quellenangabe rechtsbündig */
  font-size: 0.9em;
  color: #6c757d;
}

figcaption cite {
  font-style: normal; /* Oft wird <cite> standardmäßig kursiv dargestellt, was wir hier aufheben */
}
```

Mit diesem CSS-Code wird aus unserem semantischen HTML ein ansprechend gestaltetes Element. Das Zitat hebt sich klar vom Rest des Textes ab, ist als solches erkennbar und die Quellenangabe ist sauber zugeordnet.

Durch die Verwendung von `<blockquote>` tust du also weit mehr, als nur Text einzurücken. Du gibst dem Inhalt eine klare Bedeutung, verbesserst die Zugänglichkeit für Screenreader, die ein Zitat als solches ankündigen können, und lieferst Suchmaschinen wertvolle kontextuelle Informationen. Du strukturierst deinen Inhalt auf eine Weise, die sowohl für Menschen als auch für Maschinen verständlich, logisch und korrekt ist.
