# Display-Eigenschaften (block, inline, flex, grid)

### Die `display`-Eigenschaft: Wie Elemente ihren Platz finden

Stell dir vor, du baust mit Legosteinen. Manche Steine sind groß und blockartig, sie nehmen eine ganze Reihe für sich in Anspruch. Andere sind klein und fügen sich nahtlos zwischen andere Steine ein. In der Welt von CSS verhalten sich HTML-Elemente ganz ähnlich, und die Eigenschaft, die dieses Verhalten steuert, ist eine der wichtigsten, die du kennenlernen wirst: `display`.

Jedes HTML-Element hat von Natur aus einen voreingestellten `display`-Wert. Ein Absatz (`<p>`) verhält sich anders als ein Link (`<a>`). Zu verstehen, warum das so ist und wie du dieses Verhalten gezielt ändern kannst, ist der Schlüssel zu jedem denkbaren Web-Layout. Die `display`-Eigenschaft bestimmt die grundlegende „Persönlichkeit“ eines Elements – wie es den Raum auf der Seite beansprucht und wie es mit seinen Nachbarn interagiert. Lass uns die wichtigsten Werte dieser Eigenschaft erkunden.

#### `display: block` – Die Bausteine deines Layouts

Elemente mit `display: block` sind die soliden Grundpfeiler deiner Webseite. Sie verhalten sich wie die großen Legosteine: Sie beanspruchen so viel Platz wie möglich und respektieren keine anderen Elemente neben sich in derselben Zeile.

Die wichtigsten Merkmale von Block-Elementen sind:

*   **Sie beginnen immer in einer neuen Zeile.** Egal, wie viel Platz in der vorherigen Zeile noch frei war, ein Block-Element erzwingt einen Zeilenumbruch.
*   **Sie nehmen standardmäßig die volle verfügbare Breite ein.** Ein `<div>` oder ein `<p>` erstreckt sich von links nach rechts über seinen gesamten Elterncontainer, auch wenn sein Inhalt nur wenige Wörter umfasst.
*   **Du kannst ihnen eine exakte `width` und `height` geben.** Auch `margin` und `padding` werden in alle vier Richtungen (oben, rechts, unten, links) vollständig respektiert.

Typische Beispiele für Elemente, die von Natur aus `display: block` sind, kennst du bereits:

*   `<div>`
*   `<h1>` bis `<h6>`
*   `<p>`
*   `<ul>`, `<ol>`, `<li>`
*   `<form>`
*   `<header>`, `<footer>`, `<section>`, `<article>`

Schauen wir uns ein einfaches Beispiel an. Zwei `<div>`-Elemente stehen im HTML direkt hintereinander.

```html
<div class="box box-1">Box 1</div>
<div class="box box-2">Box 2</div>
```

Ohne jegliches CSS würden sie untereinander dargestellt. Geben wir ihnen mit CSS etwas Stil, um ihr Verhalten zu verdeutlichen:

```css
.box {
  background-color: #e0f7fa;
  border: 1px solid #00acc1;
  padding: 20px;
  margin: 10px;
}
```

Das Ergebnis ist eindeutig: Jede Box beginnt in einer neuen Zeile und füllt die verfügbare Breite aus. Sie stapeln sich vertikal, genau wie es sich für `block`-Elemente gehört.

#### `display: inline` – Fließend im Text

Im Gegensatz zu den starren Blöcken verhalten sich Elemente mit `display: inline` wie Wörter in einem Satz. Sie fügen sich in den Textfluss ein und beanspruchen nur so viel Platz, wie ihr Inhalt tatsächlich benötigt.

Die charakteristischen Eigenschaften von Inline-Elementen sind:

*   **Sie erzwingen keinen Zeilenumbruch.** Sie reihen sich nahtlos aneinander, solange in der Zeile Platz ist.
*   **Ihre Breite und Höhe werden durch ihren Inhalt bestimmt.** Die Eigenschaften `width` und `height` haben auf sie keine Wirkung.
*   **Vertikaler `margin` und `padding` haben nur begrenzte Wirkung.** Ein `margin-top` oder `margin-bottom` schiebt keine anderen Elemente weg. Horizontales `margin` und `padding` (links und rechts) funktionieren hingegen wie erwartet.

Elemente, die standardmäßig `display: inline` sind, werden oft zur Textauszeichnung oder für interaktive Elemente innerhalb eines Textes verwendet:

*   `<a>` (Links)
*   `<span>` (ein generischer Container zur Gruppierung von Inline-Inhalten)
*   `<strong>`, `<em>` (Textbetonung)
*   `<img>` (Bilder, ein Sonderfall, der als „replaced element“ gilt, sich aber grundlegend wie `inline` verhält)
*   `<input>`, `<button>` (Formularelemente)

Hier ein Beispiel, das den Unterschied verdeutlicht. Wir formatieren ein `<span>`-Element innerhalb eines Absatzes:

```html
<p>
  Dies ist ein normaler Satz, aber dieser Teil hier,
  <span class="highlight">der hervorgehoben ist</span>,
  ist ein Inline-Element. Er bleibt einfach Teil des Textflusses.
</p>
```

```css
.highlight {
  background-color: #ffecb3;
  padding: 5px;
  border: 1px solid #ffa000;
}
```

Du siehst, dass der `<span>`-Tag den Satz nicht unterbricht. Er nimmt nur den Platz ein, den sein Inhalt benötigt, und der Text fließt einfach um ihn herum weiter. Hättest du versucht, ihm eine `width` von `300px` zu geben, hätte das keinerlei Effekt gehabt.

Eine interessante Mischform ist `display: inline-block`. Ein solches Element verhält sich nach außen wie ein `inline`-Element (es reiht sich neben andere), aber nach innen wie ein `block`-Element (du kannst ihm `width`, `height`, `margin` und `padding` in alle Richtungen geben). Das war lange Zeit eine beliebte Methode, um zum Beispiel Navigationsleisten zu erstellen, bevor modernere Techniken aufkamen.

#### `display: flex` – Die flexible Revolution

Viele Jahre lang waren komplexe Layouts in CSS eine Herausforderung. Man behalf sich mit Tricks wie `float` oder der eben erwähnten `inline-block`-Technik. Mit der Einführung von Flexbox (`display: flex`) änderte sich alles. Flexbox ist ein eindimensionales Layout-Modell, das entwickelt wurde, um Elemente in einer Reihe oder einer Spalte anzuordnen und auszurichten.

Das Grundkonzept ist einfach: Du definierst einen Container, den sogenannten **Flex-Container**, indem du ihm `display: flex` gibst. Alle direkten Kindelemente dieses Containers werden automatisch zu **Flex-Items**.

```html
<div class="flex-container">
  <div class="flex-item">1</div>
  <div class="flex-item">2</div>
  <div class="flex-item">3</div>
</div>
```

```css
.flex-container {
  display: flex;
  background-color: #f3e5f5;
  padding: 10px;
}

.flex-item {
  background-color: #ab47bc;
  color: white;
  padding: 20px;
  margin: 5px;
}
```

Sobald du `display: flex` auf den Container anwendest, passiert etwas Magisches: Die Items, die standardmäßig `div`-Elemente und damit `block`-Elemente wären, ordnen sich plötzlich nebeneinander an. Flexbox gibt dir nun eine Reihe von mächtigen Eigenschaften, um diese Items zu steuern.

Wichtige Eigenschaften für den Flex-Container:

*   **`flex-direction`**: Bestimmt die Hauptachse. `row` (Standard) ordnet die Items horizontal an, `column` vertikal.
*   **`justify-content`**: Richtet die Items entlang der Hauptachse aus. Werte wie `flex-start`, `flex-end`, `center`, `space-between` oder `space-around` verteilen den verfügbaren Platz.
*   **`align-items`**: Richtet die Items entlang der Querachse aus (also vertikal bei `row` und horizontal bei `column`). `flex-start`, `flex-end`, `center` oder `stretch` sind hier gängige Werte.

Allein mit diesen drei Eigenschaften lassen sich unglaublich viele Layout-Aufgaben elegant lösen. Das vertikale Zentrieren eines Elements, das früher kompliziert war, ist mit Flexbox ein Kinderspiel:

```css
.container-zum-zentrieren {
  display: flex;
  justify-content: center; /* Zentriert horizontal */
  align-items: center;      /* Zentriert vertikal */
  height: 300px;
  border: 1px dashed grey;
}
```

Flexbox ist die erste Wahl für Komponentenlayouts, Navigationsleisten, Kartengruppen und jede Situation, in der du eine Gruppe von Elementen in einer Dimension anordnen und verteilen möchtest.

#### `display: grid` – Die Macht über zwei Dimensionen

Wenn Flexbox die Revolution für eindimensionale Layouts war, dann ist CSS Grid (`display: grid`) die totale Befreiung für zweidimensionale Layouts. Grid wurde speziell dafür entwickelt, komplexe Seitenlayouts zu erstellen, die sowohl aus Zeilen als auch aus Spalten bestehen.

Ähnlich wie bei Flexbox definierst du einen **Grid-Container** mit `display: grid`. Dessen direkte Kindelemente werden zu **Grid-Items**. Der entscheidende Unterschied ist, dass du auf dem Container ein explizites Raster definierst.

```html
<div class="grid-container">
  <div class="grid-item">Header</div>
  <div class="grid-item">Sidebar</div>
  <div class="grid-item">Main Content</div>
  <div class="grid-item">Footer</div>
</div>
```

Jetzt definieren wir das Raster im CSS. Wir möchten ein Raster mit zwei Spalten und zwei Zeilen.

```css
.grid-container {
  display: grid;
  grid-template-columns: 200px 1fr; /* 1. Spalte 200px, 2. Spalte den Rest */
  grid-template-rows: auto 1fr auto;   /* Zeilenhöhen anpassen */
  gap: 15px; /* Abstand zwischen allen Zellen */
  height: 500px;
}

.grid-item {
  background-color: #dcedc8;
  border: 1px solid #689f38;
  padding: 20px;
  text-align: center;
}
```

Mit `grid-template-columns` und `grid-template-rows` zeichnest du quasi das Skelett deines Layouts. Die `fr`-Einheit (fractional unit) ist dabei besonders nützlich: Sie teilt den verfügbaren Platz anteilig auf. `1fr 1fr 1fr` würde drei gleich breite Spalten erzeugen.

Grid gibt dir die volle Kontrolle darüber, wo welches Element platziert wird. Du kannst Items über mehrere Spalten oder Zeilen spannen (`grid-column`, `grid-row`) und so komplexe, asymmetrische Layouts erstellen, die früher nur mit verschachtelten Tabellen oder unzähligen `div`-Containern möglich waren.

Grid eignet sich perfekt für das übergeordnete Seitenlayout – die Anordnung von Header, Sidebar, Hauptinhalt und Footer. Es ist das mächtigste Werkzeug, das CSS für die makroskopische Strukturierung deiner Webseite bietet.

Die Wahl zwischen `block`, `inline`, `flex` und `grid` hängt also immer von deiner Absicht ab. Möchtest du einen einfachen, gestapelten Inhalt? `block` ist dein Freund. Möchtest du Text formatieren? `inline` ist die richtige Wahl. Brauchst du eine flexible Anordnung von Elementen in einer Reihe oder Spalte? Greif zu `flex`. Planst du ein ganzes Seitenlayout in zwei Dimensionen? `grid` ist das Werkzeug, das du suchst. Mit dem Verständnis dieser vier `display`-Werte hältst du den Schlüssel zu modernem und robustem CSS-Layout in der Hand.
