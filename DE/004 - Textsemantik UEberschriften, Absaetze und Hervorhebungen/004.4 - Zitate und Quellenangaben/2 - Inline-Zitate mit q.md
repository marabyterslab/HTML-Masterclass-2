# Inline-Zitate mit q

### Kurze Zitate im Fließtext: Das `<q>`-Element

In der Welt des Schreibens und der Texterstellung zitieren wir ständig. Manchmal sind es lange, nachdenkliche Passagen, die wir von einem anderen Autor übernehmen. Oft sind es aber auch nur kurze, prägnante Aussagen, ein einzelner Satz oder sogar nur ein paar Worte, die wir direkt in unseren eigenen Text einfließen lassen. Denk an einen Satz wie: „Meine Mutter sagte immer, ich solle <q>erst denken, dann sprechen</q>.“

Für genau solche Fälle bietet HTML ein spezielles, semantisches Element: das `<q>`-Tag. Das „q“ steht für „quote“ (englisch für Zitat). Es ist das perfekte Werkzeug, um kurze Zitate auszuzeichnen, die direkt im Fließtext, also *inline*, vorkommen.

Auf den ersten Blick könnte man sich fragen: Warum sollte ich das tun? Ich kann doch einfach Anführungszeichen auf meiner Tastatur tippen. Das Ergebnis sieht doch genauso aus, oder?

Die Antwort darauf ist ein klares Jein. Optisch mag das Ergebnis zunächst identisch sein, aber semantisch – also für die Bedeutung deines Codes – macht es einen gewaltigen Unterschied. Wenn du schlichte Anführungszeichen (`"..."`) verwendest, sind das für den Browser und für Suchmaschinen einfach nur Textzeichen. Sie haben keine besondere Bedeutung. Wenn du hingegen das `<q>`-Element nutzt, teilst du dem Computer unmissverständlich mit: „Achtung, der Text, der hier folgt, ist ein direktes Zitat. Er stammt nicht von mir, dem ursprünglichen Autor dieser Seite.“

Diese semantische Klarheit hat handfeste Vorteile.

#### Automatische und korrekte Anführungszeichen

Der wohl offensichtlichste Vorteil ist, dass der Browser die Anführungszeichen für dich setzt. Du schreibst deinen Text ohne sie und umschließt das Zitat lediglich mit `<q>` und `</q>`.

```html
<p>In seinem berühmten Vortrag betonte er immer wieder den Leitsatz: <q>Einfachheit ist die höchste Form der Raffinesse.</q></p>
```

Der Browser rendert diesen Code und fügt die passenden Anführungszeichen automatisch hinzu. Das Ergebnis im Webbrowser sieht dann so aus:

> In seinem berühmten Vortrag betonte er immer wieder den Leitsatz: „Einfachheit ist die höchste Form der Raffinesse.“

Aber es wird noch besser. Welche Anführungszeichen sind die „richtigen“? Das hängt von der Sprache und dem Land ab.

*   Im Deutschen verwenden wir typischerweise die Gänsefüßchen „unten und oben“ („...“).
*   Im Englischen stehen sie beide oben (“...”).
*   Im Französischen werden oft Guillemets verwendet (« ... »).

Wenn du deine HTML-Seite korrekt mit dem `lang`-Attribut im `<html>`-Tag auszeichnest (z. B. `<html lang="de">`), weiß der Browser, welche typografischen Regeln gelten. Er wählt dann automatisch die korrekten Anführungszeichen für die jeweilige Sprache aus. Das ist ein enormer Vorteil für die Internationalisierung und sorgt für eine typografisch saubere Darstellung, ohne dass du dir darüber Gedanken machen musst.

Was passiert bei verschachtelten Zitaten? Auch das regelt der Browser elegant. Wenn du ein Zitat innerhalb eines anderen Zitats hast, verwendet der Browser in der Regel die sekundäre Form der Anführungszeichen. Im Deutschen wären das die einfachen Anführungszeichen (‚...‘).

```html
<p>Sie erklärte mir: <q>Mein Professor sagte immer <q>Lesen ist ein Gespräch mit den Toten</q>, und das hat mich tief beeindruckt.</q></p>
```

Die gerenderte Ausgabe im Browser wäre:

> Sie erklärte mir: „Mein Professor sagte immer ‚Lesen ist ein Gespräch mit den Toten‘, und das hat mich tief beeindruckt.“

Ohne das `<q>`-Element müsstest du dich selbst um die korrekte Platzierung und Art der verschiedenen Anführungszeichen kümmern – eine potenzielle Fehlerquelle, die du dir so elegant sparst.

#### Die Quelle angeben mit dem `cite`-Attribut

Ein Zitat ohne Quelle ist oft nur eine Behauptung. Das `<q>`-Element bietet eine eingebaute Möglichkeit, die Quelle des Zitats maschinenlesbar anzugeben: das `cite`-Attribut. In dieses Attribut fügst du eine URL ein, die zur Quelle des Zitats führt. Das kann ein Link zu einem Online-Artikel, einem Interview oder einer Seite sein, die das zitierte Buch beschreibt.

```html
<p>Wie Tim Berners-Lee, der Erfinder des World Wide Web, einmal sagte: <q cite="https://www.w3.org/People/Berners-Lee/FAQ.html#Spelling">The power of the Web is in its universality.</q></p>
```

**Wichtig zu verstehen:** Der Inhalt des `cite`-Attributs wird standardmäßig **nicht** im Browser angezeigt. Er ist eine Metainformation für Maschinen – für Suchmaschinen, Browser-Erweiterungen oder andere Tools, die den Kontext deiner Inhalte verstehen wollen. Er dient dazu, die Herkunft des Zitats eindeutig und nachvollziehbar zu dokumentieren.

Wenn du die Quelle auch für deine menschlichen Leser sichtbar machen möchtest, musst du sie zusätzlich im Text nennen. Eine gängige und semantisch korrekte Methode ist die Verwendung des `<cite>`-Elements, das wir in einem anderen Kapitel genauer betrachten. Eine Kombination könnte so aussehen:

```html
<p>
  Wie im <cite>Web Accessibility Initiative (WAI) Leitfaden</cite> steht: 
  <q cite="https://www.w3.org/WAI/fundamentals/accessibility-intro/">Web accessibility means that websites, tools, and technologies are designed and developed so that people with disabilities can use them.</q>
</p>
```

Hier bietest du die Information sowohl für den Menschen (sichtbarer Text im `<cite>`-Tag) als auch für die Maschine (unsichtbarer Link im `cite`-Attribut) an.

#### Der Unterschied zu `<blockquote>`

Vielleicht kennst du bereits das `<blockquote>`-Element. Beide Elemente dienen der Auszeichnung von Zitaten, doch ihr Anwendungsbereich ist streng voneinander getrennt. Die Unterscheidung ist einfach und basiert auf der fundamentalen Trennung von Block- und Inline-Elementen in HTML.

*   **`<q>` ist ein Inline-Element.** Es wird für kurze Zitate verwendet, die Teil eines Satzes oder Absatzes sind. Es bricht den Textfluss nicht auf, sondern fügt sich nahtlos ein.
*   **`<blockquote>` ist ein Block-Level-Element.** Es wird für längere, eigenständige Zitate verwendet, die einen oder mehrere Absätze umfassen. Ein `<blockquote>` wird vom Browser typischerweise als eigener, oft eingerückter Textblock dargestellt und erzeugt einen visuellen Bruch zum umgebenden Text.

Stell es dir so vor:
Wenn du jemanden zitierst, indem du sagst „Und dann meinte sie nur <q>Das ist unglaublich!</q> und ging“, verwendest du `<q>`.
Wenn du jedoch einen ganzen Absatz aus einem Buch rezensierst und ihn als eigenständigen Block auf deiner Seite darstellen willst, verwendest du `<blockquote>`.

Hier ein Beispiel, das den Unterschied verdeutlicht:

```html
<!-- Korrekte Verwendung von <q> für ein kurzes Inline-Zitat -->
<p>Sein Fazit war kurz und bündig: <q>Es hat sich gelohnt.</q></p>

<!-- Korrekte Verwendung von <blockquote> for einen längeren, eigenständigen Zitatblock -->
<blockquote cite="https://example.com/source-url">
  <p>Dies ist ein längeres Zitat, das für sich allein steht. Es könnte mehrere Sätze umfassen und wird visuell vom Rest des Textes abgesetzt. Es stellt einen eigenen Gedankenblock dar und ist nicht direkt in einen anderen Satz integriert.</p>
</blockquote>
```

Die Wahl zwischen `<q>` und `<blockquote>` ist also keine Frage des Geschmacks, sondern eine Frage der Struktur und der semantischen Bedeutung. Ein kurzes Zitat im Satz? Immer `<q>`. Ein eigenständiger Zitatblock? Immer `<blockquote>`.

#### Gestaltung mit CSS

Obwohl der Browser eine sinnvolle Standarddarstellung für `<q>`-Elemente liefert, hast du mit CSS die volle Kontrolle über das Aussehen. Du kannst zum Beispiel die Farbe oder den Schriftschnitt des zitierten Textes ändern, um ihn hervorzuheben.

```css
q {
  color: #555;
  font-style: italic;
}
```

Eine besonders interessante CSS-Eigenschaft im Zusammenhang mit `<q>` ist `quotes`. Mit ihr kannst du die vom Browser automatisch gesetzten Anführungszeichen überschreiben und deine eigenen definieren.

```css
/* Definiert französische Guillemets als äußere und innere Anführungszeichen */
q {
  quotes: "«" "»" "‹" "›";
}
```

Die Eigenschaft `quotes` erwartet Paare von Zeichenketten: das erste Paar für die erste Zitatebene (öffnend und schließend), das zweite Paar für die zweite (verschachtelte) Ebene und so weiter. Dies gibt dir die ultimative typografische Kontrolle, falls die Standardeinstellungen des Browsers nicht deinen Designvorgaben entsprechen.

Das `<q>`-Element ist ein kleines, aber mächtiges Werkzeug in deinem semantischen HTML-Baukasten. Es trennt Inhalt von Präsentation, verbessert die Zugänglichkeit und Internationalisierung deiner Webseite und macht deinen Code für Maschinen verständlicher. Jedes Mal, wenn du versucht bist, Anführungszeichen für ein kurzes Zitat zu tippen, halte kurz inne und greife stattdessen zum `<q>`-Tag. Es ist der professionellere und zukunftssicherere Weg.
