# Zeilenumbrüche mit br

### Zeilenumbrüche mit `<br>`

Stell dir vor, du schreibst einen Text in einem einfachen Texteditor. Wenn du an das Ende einer Zeile kommst und weiterschreibst, fügt der Editor automatisch einen Umbruch ein, damit der Text in den sichtbaren Bereich passt. Was aber, wenn du mitten im Satz an eine ganz bestimmte Stelle einen harten, erzwungenen Zeilenumbruch setzen möchtest, so als würdest du die Enter-Taste drücken? In HTML gibt es genau dafür ein Element: den Zeilenumbruch, dargestellt durch das `<br>`-Tag.

Auf den ersten Blick wirkt das `<br>`-Element (von englisch „break“) simpel und nützlich. Es tut genau das, was sein Name verspricht: Es bricht die Zeile um. Doch in der Praxis ist es eines der am häufigsten falsch verwendeten Elemente in HTML. Um es korrekt einzusetzen, musst du den Unterschied zwischen einem thematischen und einem rein visuellen Umbruch verstehen.

#### Die Anatomie eines Zeilenumbruchs

Das `<br>`-Tag ist ein sogenanntes „leeres“ oder „void“-Element. Das bedeutet, es hat keinen Inhalt und benötigt daher keinen schließenden Tag. Du schreibst einfach `<br>` an der Stelle, an der der Umbruch stattfinden soll.

Früher, zu Zeiten von XHTML, hast du vielleicht die selbstschließende Schreibweise `<br />` gesehen. In modernem HTML5 ist das nicht mehr nötig. Die einfache Form `<br>` ist vollkommen korrekt und der empfohlene Standard.

Sehen wir uns ein einfaches Beispiel an:

```html
<p>Dies ist die erste Zeile.<br>Und dies ist die zweite Zeile, die direkt darunter beginnt.</p>
```

Im Browser wird dieser Code wie folgt dargestellt:

Dies ist die erste Zeile.
Und dies ist die zweite Zeile, die direkt darunter beginnt.

Ohne das `<br>`-Tag würde der Browser den Text als eine einzige durchgehende Zeile behandeln und den Umbruch nur dann vornehmen, wenn der Platz im Anzeigebereich nicht mehr ausreicht. Das `<br>` zwingt den Browser, an exakt dieser Stelle eine neue Zeile zu beginnen, unabhängig vom verfügbaren Platz.

#### Der entscheidende Unterschied: `<br>` versus `<p>`

Hier liegt der Kern des Verständnisses und die Quelle der meisten Fehler. Viele Einsteiger nutzen das `<br>`-Tag, um Abstände zwischen Absätzen zu erzeugen. Sie schreiben etwa so etwas:

```html
<!-- FALSCHE Verwendung von <br> -->
<p>
  Das ist der erste Absatz. Er enthält einige Sätze über ein bestimmtes Thema.
  <br><br>
  Das soll wohl der zweite Absatz sein. Aber semantisch ist er keiner.
</p>
```

Warum ist das falsch? Weil HTML mehr ist als nur eine Ansammlung von Anweisungen für das Aussehen. Es ist eine Sprache zur *Strukturierung von Inhalten*. Ein `<p>`-Tag (Paragraph) hat eine semantische Bedeutung: Es umschließt einen in sich geschlossenen Gedanken oder Themenblock. Ein `<br>`-Tag hat keine solche Bedeutung. Es ist ein rein präsentationsbezogener Umbruch *innerhalb* eines Blocks.

Wenn du zwei `<br>`-Tags verwendest, um einen Abstand zu erzeugen, sagst du dem Browser und assistiven Technologien wie Screenreadern: „Dies ist immer noch derselbe Absatz, aber bitte füge hier aus visuellen Gründen eine Leerzeile ein.“

Die korrekte, semantische Herangehensweise für zwei separate Absätze ist folgende:

```html
<!-- KORREKTE Verwendung von <p> -->
<p>Das ist der erste Absatz. Er enthält einige Sätze über ein bestimmtes Thema.</p>
<p>Das ist der zweite Absatz. Er behandelt ein neues Thema und ist klar vom ersten getrennt.</p>
```

Diese Struktur hat enorme Vorteile:

1.  **Semantische Korrektheit:** Suchmaschinen und Screenreader verstehen, dass es sich um zwei getrennte Gedankengänge handelt. Ein Screenreader kann zwischen den Absätzen eine deutliche Pause machen, was das Hörerlebnis erheblich verbessert.
2.  **Flexibilität im Styling:** Mit CSS kannst du nun jeden Absatz gezielt gestalten. Du kannst den Abstand zwischen den Absätzen, die Schriftart, die Einrückung der ersten Zeile und vieles mehr präzise steuern. Bei der `<br>`-Variante hättest du keine Möglichkeit, den „zweiten“ Absatz anders zu formatieren als den ersten, da beide Teil desselben `<p>`-Elements sind.
3.  **Wartbarkeit:** Dein Code bleibt sauber und lesbar. Die Struktur des Dokuments spiegelt die logische Gliederung deines Inhalts wider, nicht nur dessen zufälliges Aussehen.

Die goldene Regel lautet also: **Verwende `<br>` niemals, um vertikalen Abstand zu erzeugen.** Vertikaler Abstand ist eine Frage des Layouts und der Präsentation. Und für Präsentation ist ausschließlich CSS zuständig. Wenn du mehr Abstand zwischen Absätzen möchtest, schreibst du eine einfache CSS-Regel:

```css
p {
  margin-bottom: 24px; /* Fügt einen Abstand von 24 Pixeln nach jedem Absatz ein */
}
```

Damit trennst du die Struktur (HTML) sauber von der Gestaltung (CSS) – ein Grundprinzip moderner Webentwicklung.

#### Wann ist der Einsatz von `<br>` sinnvoll?

Nach all der Kritik könnte man meinen, das `<br>`-Tag sei überflüssig oder schlecht. Das ist es keineswegs. Es hat sehr spezifische und legitime Anwendungsfälle, bei denen der Zeilenumbruch Teil des *Inhalts* selbst ist und nicht nur eine gestalterische Entscheidung.

**1. Gedichte und Liedtexte**

Dies ist das klassische Lehrbuchbeispiel. In einem Gedicht ist der Zeilenumbruch ein wesentliches stilistisches und inhaltliches Element. Jede Zeile hat eine Bedeutung und ihre Position ist nicht willkürlich.

```html
<p>
  Zwei Wege boten sich im gelben Walde dar,<br>
  und leider konnt ich nicht beide gehn,<br>
  und da ich nur ein Wandrer war,<br>
  blieb ich lang stehn und schaute, so weit ich konnt,<br>
  zu einem hin, wo im Unterholz er sich verlor;
</p>
```

Hier wäre es semantisch falsch, jede Zeile in ein eigenes `<p>`-Tag zu packen, da das gesamte Gedicht oder zumindest eine Strophe eine zusammenhängende Einheit bildet. Das `<br>`-Tag erhält diese Einheit und sorgt gleichzeitig für die korrekte visuelle Darstellung, die vom Autor beabsichtigt war.

**2. Adressen**

Eine Postanschrift ist ein weiterer perfekter Anwendungsfall. Die einzelnen Teile einer Adresse (Name, Straße, Ort) gehören logisch zusammen, müssen aber aus Gründen der Lesbarkeit und Konvention untereinander stehen.

```html
<address>
  Max Mustermann<br>
  Musterstraße 123<br>
  12345 Musterstadt<br>
  Deutschland
</address>
```

Auch hier bildet die gesamte Adresse einen einzigen semantischen Block (der idealerweise vom `<address>`-Tag umschlossen wird), aber die Zeilenumbrüche sind ein fester Bestandteil des Datenformats. Die Verwendung von separaten `<p>`-Tags wäre hier unangebracht und würde die logische Zusammengehörigkeit der Adressteile aufbrechen.

#### Fazit: Ein Werkzeug mit Bedacht wählen

Das `<br>`-Element ist ein präzises Werkzeug für eine sehr spezifische Aufgabe: das Einfügen eines Zeilenumbruchs, der untrennbar zum Inhalt gehört. Es ist ein Fehler, es als billigen Ersatz für CSS-Margins oder als Mittel zur Erzeugung von Layouts zu missbrauchen. Solch ein Missbrauch führt zu semantisch falschem, schwer wartbarem und für assistive Technologien schlecht zugänglichem HTML-Code.

Bevor du also das nächste Mal ein `<br>` in deinen Code einfügst, halte kurz inne und frage dich: „Ist dieser Zeilenumbruch Teil der Bedeutung meines Inhalts, so wie in einem Gedicht oder einer Adresse? Oder versuche ich nur, visuellen Abstand zu schaffen?“

Wenn die Antwort Letzteres ist, lass das `<br>`-Tag weg und greife zu CSS. Dein Code wird es dir danken, und du machst einen wichtigen Schritt hin zu professionellem, sauberem und semantischem HTML.
