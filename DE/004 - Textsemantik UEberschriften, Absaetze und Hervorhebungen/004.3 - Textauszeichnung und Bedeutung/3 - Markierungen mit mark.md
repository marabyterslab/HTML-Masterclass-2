# Markierungen mit mark

# Markierungen mit `<mark>`: Relevanz im Kontext

Stell dir vor, du liest ein gedrucktes Buch und möchtest eine Stelle für später hervorheben. Wahrscheinlich greifst du zu einem Textmarker und fährst über die Zeilen, die dir in diesem Moment wichtig erscheinen. Diese Markierung verändert nicht die ursprüngliche Bedeutung des Textes. Sie sagt nicht, dass dieser Satz wichtiger ist als alle anderen im Buch, sondern nur, dass er für *dich* und *deinen aktuellen Lesezweck* von besonderer Relevanz ist.

Genau für diese Art der Hervorhebung gibt es in HTML ein semantisches Element: den `<mark>`-Tag. Er ist das digitale Äquivalent zu deinem Leuchtstift.

### Was `<mark>` bedeutet – und was nicht

In der Welt der semantischen Textauszeichnung ist es entscheidend, das richtige Werkzeug für die richtige Aufgabe zu wählen. Du könntest Text auch fett (`<strong>`) oder kursiv (`<em>`) darstellen, um ihn hervorzuheben. Doch diese Elemente haben eine ganz andere Bedeutung.

-   `<strong>`: Signalisiert starke Wichtigkeit, Dringlichkeit oder Ernsthaftigkeit. Der Inhalt innerhalb von `<strong>`-Tags ist von fundamentaler Bedeutung für das Verständnis des Gesamttextes. Ein Warnhinweis wäre ein klassischer Fall.
-   `<em>`: Dient der Betonung (Emphasis). Es verändert die Betonung beim gesprochenen Wort und kann so die Bedeutung eines Satzes leicht verändern. Es ist die subtile Nuance, die du durch deine Stimme erzeugst.

Das `<mark>`-Element spielt in einer anderen Liga. Es weist auf Text hin, der in einem bestimmten **Kontext** relevant ist. Der markierte Text ist nicht per se wichtiger oder betonter als der Rest, aber er rückt durch eine bestimmte Situation in den Fokus. Wenn dieser Kontext wegfällt, verliert die Markierung ihre spezielle Bedeutung.

Die einfachste Art, sich das zu merken, ist der Gedanke an einen Textmarker: Die gelbe Farbe auf dem Papier macht den Satz nicht wichtiger, sie macht ihn nur für deine aktuelle Aufgabe – zum Beispiel das Lernen für eine Prüfung – leichter auffindbar.

### Der klassische Anwendungsfall: Suchergebnisse

Der wohl häufigste und verständlichste Anwendungsfall für `<mark>` ist die Hervorhebung von Suchbegriffen auf einer Ergebnisseite.

Stell dir vor, du hast einen Blogartikel über die Zubereitung von Kaffee. Ein Nutzer sucht auf deiner Webseite nach dem Wort „Filter“. Um ihm das Finden der relevanten Passagen zu erleichtern, hebst du jedes Vorkommen von „Filter“ im Text hervor.

```html
<article>
  <h3>Die perfekte Tasse Kaffee</h3>
  <p>Die Wahl der richtigen Bohne ist der erste Schritt. Doch ebenso wichtig ist die Methode. 
  Viele schwören auf den Handaufguss mit einem Porzellan-<mark>Filter</mark>. 
  Dieser sorgt für ein klares Aroma. Achte darauf, das <mark>Filter</mark>papier vorher 
  mit heißem Wasser auszuspülen, um den Papiergeschmack zu neutralisieren.</p>
</article>
```

In diesem Beispiel ist das Wort „Filter“ nicht von Natur aus wichtiger als „Bohne“ oder „Aroma“. Aber im Kontext der Nutzersuche wird es zur relevantesten Information. Für einen anderen Nutzer, der nach „Aroma“ sucht, wäre genau dieses Wort markiert. Die Hervorhebung ist also dynamisch und kontextabhängig – ein perfekter Job für `<mark>`.

### Zitate und Referenzen gezielt beleuchten

Ein weiterer hervorragender Einsatzort für `<mark>` ist das Zitieren von Textpassagen. Oft möchtest du aus einem langen Zitat nur einen bestimmten Teilaspekt hervorheben, um deine eigene Argumentation zu stützen.

Nehmen wir an, du schreibst einen Artikel über Webdesign und zitierst einen Experten. Dich interessiert aber nur der Teil, in dem er über die Bedeutung von Kontrast spricht.

```html
<p>Wie die berühmte Designerin Eva Schmidt in ihrem Buch "Das digitale Auge" schreibt, ist die Ästhetik nicht alles:</p>
<blockquote>
  <p>Ein häufiger Fehler von Anfängern ist die alleinige Fokussierung auf die Farbwahl.
  Dabei wird oft übersehen, dass <mark>Lesbarkeit der wichtigste Aspekt der
  Benutzerfreundlichkeit ist</mark>. Ohne ausreichenden Kontrast zwischen Text und
  Hintergrund ist selbst die schönste Schrift nutzlos.</p>
</blockquote>
<p>Dieser Punkt zur Lesbarkeit ist entscheidend für den Erfolg jeder Webseite.</p>
```

Im Originaltext von Eva Schmidt ist der markierte Satz vielleicht nicht wichtiger als der Rest des Absatzes. Aber für *deinen* Artikel, in dem du genau diesen Punkt unterstreichen willst, ist er von zentraler Relevanz. Du leuchtest mit dem `<mark>`-Tag quasi mit einer Taschenlampe auf den Teil des Zitats, über den du als Nächstes sprechen möchtest.

### Styling mit CSS: Deinem Textmarker eine persönliche Note geben

Standardmäßig rendern die meisten Browser den Inhalt eines `<mark>`-Elements mit einem leuchtend gelben Hintergrund, ganz so wie der klassische Textmarker. Das ist eine sinnvolle Voreinstellung, aber du bist keinesfalls daran gebunden.

Da `<mark>` ein ganz normales HTML-Element ist, kannst du es mit CSS nach Belieben gestalten. Das ist nicht nur eine Frage des Geschmacks, sondern auch der Barrierefreiheit und der Anpassung an dein Corporate Design.

Du könntest zum Beispiel einen sanfteren Farbton wählen, der besser zu deiner Webseite passt.

```css
mark {
  background-color: #a4e4fc; /* Ein sanftes Hellblau */
  color: #1a1a1a; /* Dunkler Text für guten Kontrast */
  padding: 2px 4px; /* Etwas Luft um den Text */
  border-radius: 3px; /* Leicht abgerundete Ecken */
}
```

Mit diesem CSS würde jede `<mark>`-Hervorhebung auf deiner Seite nicht mehr grell gelb, sondern in einem dezenten Hellblau erscheinen. Die Trennung von Inhalt (HTML) und Präsentation (CSS) bleibt dabei sauber gewahrt. Du änderst nur das Aussehen, nicht die semantische Bedeutung.

### Ein Wort zur Barrierefreiheit

Die visuelle Hervorhebung durch `<mark>` ist eine großartige Hilfe für sehende Nutzer. Doch was ist mit Menschen, die Screenreader verwenden?

Standardmäßig wird das `<mark>`-Element von den meisten Screenreadern nicht speziell angesagt. Ein Nutzer hört also den Text, aber nicht die Information, dass dieser markiert ist. Das ist in der Regel auch so gewollt, denn die Markierung soll eine rein visuelle Hilfe sein und die Bedeutung des Textes nicht verändern. Der Satz muss auch ohne die Hervorhebung verständlich und vollständig sein.

Die größte Herausforderung bei der Barrierefreiheit liegt in der visuellen Gestaltung. Der Standardkontrast von schwarzem Text auf gelbem Grund ist meist ausreichend. Wenn du die Farben jedoch per CSS anpasst, musst du unbedingt darauf achten, dass der Kontrast zwischen Text- und Hintergrundfarbe hoch genug ist. Werkzeuge zur Kontrastprüfung helfen dir dabei, die Richtlinien der WCAG (Web Content Accessibility Guidelines) einzuhalten, damit auch Menschen mit Sehschwächen den markierten Text problemlos lesen können.

Der `<mark>`-Tag ist ein kleines, aber feines Werkzeug in deinem semantischen HTML-Baukasten. Er erlaubt dir, Text auf eine Weise hervorzuheben, die klar kommuniziert: „Dieser Teil hier ist nicht generell am wichtigsten, aber für den aktuellen Moment, für diese spezifische Aufgabe, solltest du hier hinschauen.“ Es ist die Kunst, Relevanz im Kontext auszudrücken – präzise und bedeutungsvoll.
