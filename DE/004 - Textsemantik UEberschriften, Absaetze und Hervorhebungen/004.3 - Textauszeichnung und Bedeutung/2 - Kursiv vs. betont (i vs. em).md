# Kursiv vs. betont (i vs. em)

### Kursiv ist nicht gleich betont: Der feine Unterschied zwischen `<i>` und `<em>`

Auf den ersten Blick scheinen die HTML-Tags `<i>` und `<em>` wie visuelle Zwillinge. Wenn du beide in einer einfachen HTML-Datei verwendest und sie im Browser betrachtest, wirst du in der Regel dasselbe Ergebnis sehen: kursiv gesetzten Text. Diese Beobachtung führt viele Einsteiger zu der Annahme, die beiden Tags seien austauschbar. Doch das ist ein Trugschluss, der direkt ins Herz der modernen Webentwicklung führt – zur fundamentalen Unterscheidung zwischen Präsentation und Semantik.

In diesem Kapitel tauchen wir tief in diesen feinen, aber entscheidenden Unterschied ein. Du wirst lernen, warum die Wahl zwischen `<i>` und `<em>` weit mehr ist als eine stilistische Entscheidung. Es ist eine Aussage über die Bedeutung deines Inhalts.

#### Die Semantik im Fokus: Was bedeutet dein Text?

Bevor wir die Tags einzeln betrachten, lass uns das Grundprinzip wiederholen, das für das gesamte moderne HTML gilt: HTML ist für die Struktur und die Bedeutung (Semantik) deines Inhalts zuständig. CSS ist für die visuelle Darstellung (Präsentation) verantwortlich.

Wenn du einen Textabschnitt mit einem HTML-Tag umschließt, gibst du diesem Text eine besondere Bedeutung. Du sagst dem Browser, Screenreadern, Suchmaschinen und anderen Programmen: „Dieser Teil des Textes ist nicht einfach nur Text – er ist eine Überschrift, ein Zitat, eine Liste oder eben etwas Hervorgehobenes.“ Wie diese Hervorhebung *aussieht*, ist eine zweite, davon getrennte Frage, die du mit CSS beantwortest.

Die Tatsache, dass die meisten Browser `<em>` standardmäßig kursiv darstellen, ist nur eine Konvention, eine visuelle Starthilfe. Du könntest mit CSS genauso gut festlegen, dass `<em>`-Texte fett, unterstrichen, rot oder sogar größer dargestellt werden. Die semantische Bedeutung des Tags aber bleibt unverändert.

#### `<em>`: Die Betonung, die den Sinn verändert

Das `<em>`-Tag steht für „emphasis“, also Betonung oder Hervorhebung. Es wird verwendet, um einem Wort oder einer Phrase eine Betonung zu geben, die den Sinn des Satzes verändert. Denk an die gesprochene Sprache: Je nachdem, welches Wort du in einem Satz betonst, ändert sich die gesamte Aussage.

Schauen wir uns ein einfaches Beispiel an:

> Ich liebe HTML.

Dieser Satz ist eine neutrale Aussage. Nun setzen wir das `<em>`-Tag an verschiedenen Stellen ein und beobachten, wie sich die implizite Bedeutung verschiebt.

1.  **Betonung auf „Ich“:**
    ```html
    <p><em>Ich</em> liebe HTML.</p>
    ```
    Die implizite Aussage hier ist: *Ich* bin es, der HTML liebt (und vielleicht nicht du oder jemand anderes). Die Betonung liegt auf der Person.

2.  **Betonung auf „liebe“:**
    ```html
    <p>Ich <em>liebe</em> HTML.</p>
    ```
    Hier wird die Stärke des Gefühls betont. Es ist nicht nur ein Mögen oder eine oberflächliche Zuneigung, sondern eine tiefe, echte Liebe.

3.  **Betonung auf „HTML“:**
    ```html
    <p>Ich liebe <em>HTML</em>.</p>
    ```
    In diesem Fall liegt der Fokus auf dem Objekt der Zuneigung. Ich liebe *HTML* (und nicht etwa CSS oder JavaScript).

In allen drei Fällen ändert die Betonung die Nuance und den Fokus des Satzes. Genau das ist der semantische Zweck von `<em>`. Du teilst dem Browser und assistiven Technologien wie Screenreadern mit, dass dieser Teil des Textes eine besondere Betonung in der „Stimme“ des Dokuments erhalten soll. Ein Screenreader *kann* seine synthetische Stimme an dieser Stelle leicht verändern, um die Betonung hörbar zu machen, ähnlich wie ein Mensch es beim Vorlesen tun würde.

Die Verwendung von `<em>` ist also eine inhaltliche Entscheidung, die die Interpretation des Textes beeinflusst.

#### `<i>`: Eine andere Stimme, ein anderer Ton

Das `<i>`-Tag hat eine bewegte Geschichte. In den frühen Tagen des Web stand es schlicht für „italic“ (kursiv) und war ein rein präsentationsbezogenes Tag. Es sagte dem Browser: „Stell diesen Text kursiv dar.“ Das widerspricht aber dem Prinzip der Trennung von Inhalt und Präsentation.

Deshalb wurde die Bedeutung des `<i>`-Tags in HTML5 neu definiert und präzisiert. Es steht heute nicht mehr für eine bestimmte Formatierung, sondern kennzeichnet einen Text, der sich in Ton oder Art vom umgebenden Text unterscheidet, ohne dass er eine besondere Betonung oder Wichtigkeit erhält. Man könnte es als eine Art „alternative Stimme“ betrachten.

Typische und korrekte Anwendungsfälle für das `<i>`-Tag sind:

*   **Fachbegriffe oder technische Termini:**
    ```html
    <p>Das Konzept des <em>World Wide Web</em> wurde von Tim Berners-Lee entwickelt.</p>
    ```

*   **Fremdsprachige Wörter oder Phrasen:**
    ```html
    <p>Nach einem langen Tag sagte er nur noch: <i>C'est la vie</i>.</p>
    ```

*   **Schiffsnamen, Buchtitel oder Filmtitel:**
    ```html
    <p>Der Film <i>Inception</i> spielt mit der Wahrnehmung der Realität.</p>
    ```

*   **Gedanken einer Figur in einer Erzählung:**
    ```html
    <p><i>Was, wenn ich es einfach versuche?</i>, dachte sie bei sich.</p>
    ```

In all diesen Fällen ist der markierte Text nicht wichtiger oder stärker betont als der Rest des Satzes. Er ist einfach nur … anders. Er hebt sich stilistisch oder taxonomisch ab. Es ist eine Kennzeichnung, die sagt: „Dieser Teil gehört in eine andere Kategorie.“

Im Gegensatz zu `<em>` signalisiert `<i>` keine Änderung der Wichtigkeit. Es ist eine neutrale Abgrenzung. Ein Screenreader würde hier normalerweise keine Änderung in der Betonung vornehmen, da der Inhalt nicht als wichtiger markiert ist.

#### Die Macht der Trennung: HTML-Semantik und CSS-Styling

Jetzt, wo der semantische Unterschied klar ist, wird auch deutlich, warum die Trennung von HTML und CSS so mächtig ist. Stell dir vor, du hast eine Website für ein internationales Publikum. Du könntest entscheiden, dass alle fremdsprachigen Wörter (korrekt mit `<i>` ausgezeichnet) nicht nur kursiv, sondern auch in einer leicht anderen Farbe dargestellt werden sollen, um sie besser erkennbar zu machen.

Gleichzeitig möchtest du, dass betonte Textstellen (`<em>`) besonders ins Auge fallen und daher nicht nur kursiv, sondern auch fett sind.

Mit CSS ist das ein Kinderspiel:

```css
/* Styling für fremdsprachige Wörter, Fachbegriffe etc. */
i {
  font-style: italic;
  color: #555; /* Ein dezentes Dunkelgrau */
}

/* Styling für inhaltlich betonte Passagen */
em {
  font-style: italic;
  font-weight: bold; /* Zusätzlich fett, um die Betonung zu verstärken */
  color: #c00;    /* Und in einem auffälligen Rot */
}
```

Mit diesem CSS hast du eine klare visuelle Unterscheidung geschaffen, die direkt auf der semantischen Bedeutung deines HTMLs basiert. Du hast nicht einfach nur das Aussehen verändert, du hast die Bedeutung sichtbar gemacht. Wenn du dich später entscheidest, dass Betonung besser durch Unterstreichung funktioniert, änderst du eine einzige Zeile in deiner CSS-Datei, und deine gesamte Website passt sich an – ohne dass du ein einziges `<em>`-Tag in deinem HTML anrühren musst. Das ist wartbarer, flexibler und professioneller Code.

#### Ein kurzer Blick auf die Verwandtschaft: `<b>` vs. `<strong>`

Das gleiche Prinzip, das wir für `<i>` und `<em>` besprochen haben, gilt auch für ihre „fetten“ Gegenstücke: `<b>` und `<strong>`.

*   **`<strong>`**: Dieses Tag steht für „strong importance“. Es kennzeichnet Text, der von großer Wichtigkeit, Dringlichkeit oder Ernsthaftigkeit ist. Es ist semantisch noch stärker als `<em>`. Es verändert nicht nur die Nuance, sondern hebt die Wichtigkeit des Inhalts hervor. Beispiele sind Warnungen oder entscheidende Passagen in einem Text.
    ```html
    <p><strong>Achtung:</strong> Betreten der Baustelle verboten.</p>
    ```

*   **`<b>`**: Ähnlich wie das `<i>`-Tag wurde auch das `<b>`-Tag (früher für „bold“) neu definiert. Es dient heute dazu, Text stilistisch vom Rest abzuheben, ohne ihm zusätzliche Wichtigkeit zu verleihen. Man nutzt es für Schlüsselwörter in einem Absatz, Produktnamen in einer Rezension oder andere Textteile, die ins Auge fallen sollen, ohne als inhaltlich wichtiger markiert zu werden.
    ```html
    <p>In diesem Tutorial lernst du die Grundlagen von <b>React</b> und <b>Vue.js</b> kennen.</p>
    ```

Auch hier gilt: `<strong>` ist eine Aussage über die Wichtigkeit des Inhalts, `<b>` ist eine stilistische Abgrenzung ohne zusätzliche semantische Gewichtung. Standardmäßig werden beide fett dargestellt, aber mit CSS kannst du das Aussehen frei gestalten.

Deine Aufgabe als Entwickler ist es, dem Browser und anderen Maschinen die *Bedeutung* deines Inhalts zu vermitteln, nicht nur, wie er aussehen soll. Die bewusste Entscheidung zwischen `<em>` und `<i>` oder `<strong>` und `<b>` ist ein grundlegender Schritt auf diesem Weg. Es ist der Kern von semantischem HTML und der Unterschied zwischen einem, der nur Code schreibt, und einem echten Web-Handwerker, der langlebige und zugängliche digitale Erlebnisse schafft.
