# Thematische Trennung mit hr

### Thematische Trennung mit `<hr>`

In der Welt der Typografie und des Buchdrucks gibt es seit Jahrhunderten Konventionen, um einen thematischen Bruch oder einen Szenenwechsel innerhalb eines Kapitels zu signalisieren. Manchmal sind es drei kleine Sternchen (⁂), manchmal eine einfache Leerzeile mehr als üblich oder ein kleines Ornament. Diese visuellen Hinweise sagen dem Leser: „Achtung, hier endet ein Gedankengang und ein neuer beginnt.“

In HTML haben wir ein spezielles Element für genau diesen Zweck: das `<hr>`-Element. Doch um dieses kleine, aber feine Element ranken sich viele Missverständnisse, die oft auf seine Geschichte zurückzuführen sind.

#### Vom Strich zur Bedeutung: Die Evolution des `<hr>`

In den frühen Tagen des Webs, in den Zeiten von HTML4 und davor, stand `<hr>` für „Horizontal Rule“, also eine horizontale Linie. Sein einziger Zweck war es, eine sichtbare Trennlinie über die gesamte Breite des verfügbaren Raums zu zeichnen. Webentwickler nutzten es inflationär, um Layouts zu strukturieren, Sektionen visuell voneinander abzugrenzen oder einfach nur als dekoratives Element. Das Element hatte keine tiefere, semantische Bedeutung – es war reines Design.

Mit der Einführung von HTML5 änderte sich das grundlegend. Die Bedeutung des `<hr>`-Elements wurde neu definiert. Es steht nicht mehr für eine horizontale Linie, sondern für einen **thematischen Bruch** (Thematic Break) auf Absatzebene. Seine Aufgabe ist es nun, einen Wechsel des Themas innerhalb eines zusammenhängenden Textblocks zu signalisieren. Die Tatsache, dass Browser es standardmäßig immer noch als horizontale Linie darstellen, ist lediglich ein visueller Vorschlag, ein Überbleibsel aus alten Zeiten. Die eigentliche Kraft des Elements liegt nun in seiner Bedeutung, nicht in seinem Aussehen.

Stell dir vor, du schreibst eine Kurzgeschichte. Innerhalb eines Kapitels möchtest du von der Perspektive einer Figur zur Perspektive einer anderen wechseln oder einen Zeitsprung von einigen Stunden machen. Anstatt ein neues Kapitel zu beginnen, signalisierst du diesen Übergang. Genau hier kommt `<hr>` ins Spiel.

```html
<article>
  <h2>Ein unerwarteter Fund</h2>
  <p>Anna durchforstete den staubigen Dachboden ihrer Großmutter. Alte Truhen, vergessene Bücher und Spinnweben waren ihre einzigen Begleiter. In einer kleinen Holzkiste, versteckt unter einem Stapel vergilbter Zeitungen, fand sie ein altes Tagebuch. Der Ledereinband war brüchig, die Seiten rochen nach Geschichte. Sie schlug die erste Seite auf und begann zu lesen.</p>
  
  <hr>
  
  <p>Jahre zuvor saß ein junger Mann namens Klaus am selben Schreibtisch und schrieb genau in dieses Buch. Die Tinte floss frisch auf das Papier, während er von seinen Träumen erzählte, die Welt zu bereisen. Er wusste nicht, dass seine Worte Jahrzehnte später von seiner eigenen Enkelin gefunden werden würden, die auf demselben staubigen Dachboden saß.</p>
</article>
```

In diesem Beispiel markiert das `<hr>`-Element den Sprung in der Zeit und der Perspektive. Es trennt nicht zwei komplett unabhängige Themen, sondern signalisiert einen scharfen Bruch *innerhalb* des übergeordneten Themas („Ein unerwarteter Fund“). Es ist eine inhaltliche Zäsur, kein visueller Schnörkel.

#### Wann du `<hr>` nicht verwenden solltest

Das wichtigste Learning über das moderne `<hr>` ist zu wissen, wann man es *nicht* einsetzt. Da sein Zweck rein semantisch ist, solltest du es niemals für rein visuelle Zwecke missbrauchen.

**Falsch: Dekorative Linien**

Wenn du nur eine Trennlinie unter einer Überschrift oder zwischen verschiedenen Designelementen möchtest, ist CSS die richtige Wahl. Eine Eigenschaft wie `border-bottom` an einem anderen Element ist hierfür perfekt geeignet.

```html
<!-- FALSCH: Missbrauch von <hr> für reines Design -->
<h2>Unsere Produkte</h2>
<hr>

<!-- RICHTIG: Styling mit CSS -->
<h2 class="section-title">Unsere Produkte</h2>
```

```css
/* Das dazugehörige CSS für die richtige Variante */
.section-title {
  padding-bottom: 10px;
  border-bottom: 2px solid #ccc;
}
```

Die Verwendung von CSS hält deine HTML-Struktur sauber und semantisch korrekt. Dein Markup beschreibt den Inhalt, während CSS das Aussehen definiert.

**Falsch: Trennung von Hauptbereichen**

Ein weiterer häufiger Fehler ist die Verwendung von `<hr>`, um große Inhaltsbereiche wie `<section>`-Elemente voneinander zu trennen. Die semantische Gliederung deiner Seite wird bereits durch die Strukturelemente selbst erreicht. Ein `<section>`-Element definiert für sich allein einen thematisch zusammengehörigen Bereich. Ein zusätzliches `<hr>` zwischen zwei `<section>`-Elementen ist überflüssig und semantisch falsch, da der Bruch bereits durch die Struktur impliziert wird.

```html
<!-- FALSCH: <hr> zwischen Sektionen ist redundant -->
<section>
  <h3>Über uns</h3>
  <p>Informationen über das Unternehmen...</p>
</section>

<hr> 

<section>
  <h3>Unsere Mission</h3>
  <p>Unsere Ziele und Visionen...</p>
</section>
```

Die Trennung der Sektionen ist durch die Elemente `<section>` und deren Überschriften (`<h3>`) bereits eindeutig gegeben. Ein Browser und auch Hilfstechnologien wie Screenreader verstehen diese Struktur ohne ein zusätzliches `<hr>`.

#### Die visuelle Gestaltung von `<hr>` mit CSS

Obwohl die primäre Funktion von `<hr>` semantisch ist, bedeutet das nicht, dass du es nicht gestalten darfst. Im Gegenteil: Du kannst die Standardlinie des Browsers komplett überschreiben und sie so anpassen, dass sie den thematischen Bruch in deinem Design angemessen repräsentiert.

Die Standarddarstellung eines `<hr>`-Elements ist oft eine unschöne, eingekerbte 3D-Linie. Der erste Schritt ist daher meistens, diesen Standardstil zu entfernen.

```css
hr {
  border: none; /* Entfernt den 3D-Rahmen in den meisten Browsern */
  border-top: 1px solid #ddd; /* Fügt eine einfache, saubere Linie hinzu */
  height: 1px; /* Stellt sicher, dass die Höhe konsistent ist */
  margin: 2em 0; /* Sorgt für vertikalen Abstand */
}
```

Mit dieser Basis kannst du kreativ werden. Vielleicht möchtest du keine durchgehende Linie, sondern etwas Subtileres. Wie wäre es mit einem Farbverlauf?

```css
hr.gradient {
  border: 0;
  height: 1px;
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.75), rgba(0, 0, 0, 0));
}
```

Eine besonders elegante Technik ist die Verwendung von Pseudo-Elementen wie `::before` und `::after`, um Ornamente oder Symbole hinzuzufügen – ganz im Stil klassischer Buchtypografie.

```html
<p>...das Ende einer Szene.</p>
<hr class="fancy">
<p>...der Beginn der nächsten Szene.</p>
```

```css
hr.fancy {
  border: 0;
  height: 20px;
  background-color: transparent; /* Die Linie selbst unsichtbar machen */
  position: relative; /* Wichtig für die Positionierung des Pseudo-Elements */
  text-align: center;
}

/* Das Pseudo-Element ::before wird zum eigentlichen Symbol */
hr.fancy::before {
  content: '⁂'; /* Hier kannst du ein beliebiges Zeichen oder Symbol einfügen */
  font-size: 1.5em;
  color: #888;
}
```

Diese CSS-Regel macht die ursprüngliche Linie des `<hr>` unsichtbar und fügt stattdessen mittig das Asterismus-Symbol (⁂) ein. Plötzlich sieht dein thematischer Bruch nicht mehr wie eine schnöde Linie aus, sondern wie ein bewusst gesetztes typografisches Element. Dies unterstreicht die semantische Bedeutung perfekt: Es ist ein Bruch, aber seine visuelle Repräsentation ist flexibel und liegt ganz in deiner Hand.

#### Barrierefreiheit

Zum Schluss noch ein kurzer, aber wichtiger Gedanke zur Barrierefreiheit. Für sehende Benutzer ist der thematische Bruch visuell erkennbar. Aber was ist mit Nutzern von Screenreadern? Moderne Screenreader erkennen das `<hr>`-Element und geben es in der Regel als „Separator“ oder „Trennlinie“ aus. Damit wird auch für nicht-sehende Nutzer klar, dass an dieser Stelle eine inhaltliche Zäsur stattfindet. Dies funktioniert aber nur, wenn du das Element korrekt und semantisch einsetzt. Ein rein dekorativer `<div>` mit einem CSS-Rand würde diese wichtige Information nicht übermitteln.

Indem du das `<hr>`-Element bewusst und gemäß seiner modernen Definition als thematischen Bruch einsetzt, schreibst du nicht nur sauberen und zukunftssicheren Code, sondern schaffst auch eine reichere und verständlichere Erfahrung für alle deine Nutzer.
