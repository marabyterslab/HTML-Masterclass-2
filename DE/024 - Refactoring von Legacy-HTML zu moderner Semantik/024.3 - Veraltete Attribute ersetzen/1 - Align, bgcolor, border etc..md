# Align, bgcolor, border etc.

### Relikte der Vergangenheit: Attribute wie `align`, `bgcolor` und `border` ersetzen

Wenn du in die Tiefen älterer Webseiten oder in Codebases blickst, die schon einige Jahre auf dem Buckel haben, wirst du unweigerlich auf eine Reihe von HTML-Attributen stoßen, die heute als veraltet gelten. Attribute wie `align`, `bgcolor`, `border` oder `width` direkt im HTML-Markup waren einst das Standardwerkzeug, um das Aussehen einer Webseite zu gestalten. Sie waren pragmatisch und direkt: Du wolltest einen Text zentrieren? `<p align="center">`. Du wolltest eine Tabellenzelle einfärben? `<td bgcolor="yellow">`.

Diese Vorgehensweise entsprang einer Zeit, in der die Grenzen zwischen der Struktur eines Dokuments (HTML) und seiner visuellen Darstellung (dem späteren CSS) noch stark verschwommen waren. Die Philosophie war einfach: Das HTML-Dokument sollte nicht nur seinen Inhalt beschreiben, sondern auch, wie dieser Inhalt auszusehen hat.

Heute wissen wir es besser. Die goldene Regel der modernen Webentwicklung lautet: **Trennung von Belangen (Separation of Concerns)**. HTML ist ausschließlich für die Struktur und die semantische Bedeutung deines Inhalts zuständig. CSS kümmert sich um das gesamte visuelle Erscheinungsbild – von Farben und Schriftarten bis hin zu Layout und Ausrichtung. JavaScript ist für die Interaktivität und das Verhalten verantwortlich.

Die alten, präsentationsbezogenen Attribute durchbrechen dieses Prinzip fundamental. Sie mischen Stilinformationen direkt in die Struktur, was zu einer Reihe von Problemen führt:

*   **Schlechte Wartbarkeit:** Wenn du das Design deiner Webseite ändern möchtest, musst du jede einzelne HTML-Datei durchgehen und jedes Attribut manuell anpassen. Eine globale Änderung der Hintergrundfarbe aller Tabellenköpfe wird so zu einem Albtraum.
*   **Mangelnde Flexibilität:** Das Design ist fest an die Struktur gekoppelt. Du kannst nicht einfach unterschiedliche Stile für dieselbe Struktur auf verschiedenen Geräten (Responsive Design) oder für verschiedene Kontexte anwenden, ohne das HTML zu duplizieren oder zu verändern.
*   **Aufgeblähter Code:** Das ständige Wiederholen von Stil-Attributen bläht deine HTML-Dokumente unnötig auf.
*   **Geringere Barrierefreiheit:** Screenreader und andere assistierende Technologien verlassen sich auf eine saubere, semantische HTML-Struktur, um den Inhalt korrekt zu interpretieren. Visuelle Anweisungen im Markup können diesen Prozess stören.

In diesem Kapitel schauen wir uns die häufigsten veralteten Attribute an und wie du sie elegant und korrekt durch modernes CSS ersetzt. Dieser Prozess ist ein Kernbestandteil des Refactorings von Legacy-Code und eine essenzielle Fähigkeit für jeden professionellen Webentwickler.

#### Ausrichtung mit `align`

Das `align`-Attribut war das Schweizer Taschenmesser für die horizontale Ausrichtung. Man konnte es auf Absätze, Überschriften, `div`-Container und vor allem auf Tabellenelemente anwenden.

**Legacy-HTML:**

```html
<h1 align="center">Willkommen auf meiner Webseite</h1>
<p align="right">Ein Text, der rechtsbündig ist.</p>
<div align="center">
  <p>Dieser ganze Bereich ist zentriert.</p>
</div>
```

Dieses Vorgehen ist nicht mehr zeitgemäß. Die Ausrichtung ist eine rein visuelle Eigenschaft und gehört daher ins CSS. Die moderne Lösung ist die `text-align`-Eigenschaft.

**Modernes HTML & CSS:**

Zuerst bereinigst du dein HTML von den `align`-Attributen. Um die Elemente gezielt ansprechen zu können, vergibst du Klassen.

**HTML:**

```html
<h1 class="text-center">Willkommen auf meiner Webseite</h1>
<p class="text-right">Ein Text, der rechtsbündig ist.</p>
<div class="text-center">
  <p>Dieser ganze Bereich ist zentriert.</p>
</div>
```

**CSS:**

```css
.text-center {
  text-align: center;
}

.text-right {
  text-align: right;
}

/* Du könntest auch direkt die Tags stylen, 
   aber Klassen sind flexibler. */
h1 {
  text-align: center;
}
```

Der Vorteil liegt auf der Hand: Dein HTML beschreibt nur noch, *was* die Elemente sind (eine Überschrift, ein Absatz). Dein CSS beschreibt, *wie* sie aussehen. Möchtest du später alle zentrierten Texte linksbündig machen, änderst du eine einzige Zeile in deiner CSS-Datei.

#### Farben und Hintergründe: `bgcolor`, `background` und `color`

Ähnlich wie bei der Ausrichtung wurden Farben direkt im Markup definiert. `bgcolor` setzte die Hintergrundfarbe, während `color` (oft im `<font>`-Tag) die Textfarbe bestimmte. Das `background`-Attribut wurde genutzt, um ein Hintergrundbild festzulegen.

**Legacy-HTML:**

```html
<body bgcolor="#f0f8ff" text="#000000">
  <p>
    <font color="red">Dieser Text ist rot.</font>
  </p>
  <table bgcolor="white">
    <tr bgcolor="#cccccc">
      <th>Kopfzeile</th>
    </tr>
    <td background="bg-tile.gif">Zelle mit Hintergrundbild.</td>
  </table>
</body>
```

Der `<font>`-Tag ist selbst komplett veraltet und ein Paradebeispiel für die Vermischung von Inhalt und Präsentation. All diese Aufgaben werden heute von CSS-Eigenschaften übernommen: `background-color`, `background-image` und `color`.

**Modernes HTML & CSS:**

**HTML:**

```html
<body>
  <p class="warning-text">Dieser Text ist rot.</p>
  <table>
    <thead>
      <tr>
        <th>Kopfzeile</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="cell-with-bg">Zelle mit Hintergrundbild.</td>
      </tr>
    </tbody>
  </table>
</body>
```

**CSS:**

```css
body {
  background-color: #f0f8ff;
  color: #000000; /* Standard-Textfarbe für die gesamte Seite */
}

.warning-text {
  color: red;
}

table {
  background-color: white;
}

/* Zielgerichtetes Styling für den Tabellenkopf */
table th {
  background-color: #cccccc;
}

.cell-with-bg {
  background-image: url('bg-tile.gif');
}
```

Auch hier siehst du die klare Trennung. Das HTML ist sauber und semantisch (wir nutzen sogar `<thead>` und `<tbody>` für eine bessere Struktur). Das gesamte Design wird zentral und wiederverwendbar im CSS gesteuert. CSS bietet zudem weitaus mächtigere Optionen für Hintergründe, wie `background-repeat`, `background-position` oder `background-size`, die mit dem alten `background`-Attribut undenkbar waren.

#### Tabellen-Styling: `border`, `cellspacing` und `cellpadding`

Tabellen sind ein klassisches Feld, auf dem sich unzählige veraltete Attribute tummeln. `border` definierte die Dicke des Rahmens um die Tabelle, `cellspacing` den Abstand *zwischen* den Zellen und `cellpadding` den Innenabstand *innerhalb* einer Zelle.

**Legacy-HTML:**

```html
<table border="1" cellspacing="0" cellpadding="10" width="100%">
  <tr>
    <td>Inhalt 1</td>
    <td>Inhalt 2</td>
  </tr>
</table>
```

Diese Attribute sind zwar sehr direkt, aber auch extrem unflexibel. Du kannst beispielsweise nicht die Farbe oder den Stil des Rahmens ändern.

**Modernes HTML & CSS:**

Die CSS-Pendants sind `border`, `border-spacing` (ersetzt `cellspacing`) und `padding` (ersetzt `cellpadding`). Um das klassische Aussehen einer Tabelle mit `cellspacing="0"` nachzubilden, wird oft die Eigenschaft `border-collapse: collapse;` verwendet.

**HTML:**

```html
<table class="data-table">
  <tr>
    <td>Inhalt 1</td>
    <td>Inhalt 2</td>
  </tr>
</table>
```

**CSS:**

```css
.data-table {
  width: 100%;
  border-collapse: collapse; /* Lässt Zell-Ränder verschmelzen, ersetzt cellspacing="0" */
  /* border-spacing: 0; */ /* Alternative zu border-collapse, wenn Ränder getrennt bleiben sollen */
}

/* Wende den Rahmen auf die Zellen und die Tabelle selbst an */
.data-table,
.data-table th,
.data-table td {
  border: 1px solid #333; /* Dicke, Stil und Farbe des Rahmens */
}

/* Innenabstand für alle Zellen definieren */
.data-table th,
.data-table td {
  padding: 10px; /* Ersetzt cellpadding="10" */
}
```

Mit CSS hast du die volle Kontrolle. Du kannst unterschiedliche Ränder für Kopf- und Datenzellen festlegen, den Rahmen gestrichelt oder gepunktet darstellen und Hover-Effekte hinzufügen – alles Dinge, die mit den alten HTML-Attributen unmöglich waren.

#### Dimensionen: `width` und `height`

Die Attribute `width` und `height` sind ein Sonderfall. Auf den meisten Elementen wie `<div>`, `<p>` oder `<td>` gelten sie als veraltet und sollten durch die CSS-Eigenschaften `width` und `height` ersetzt werden.

**Legacy-HTML (schlecht):**

```html
<td width="200">Diese Spalte ist 200 Pixel breit.</td>
```

**Modernes CSS (gut):**

```css
.sidebar-cell {
  width: 200px;
}
```

**Eine wichtige Ausnahme: `<img>`**

Bei `<img>`-Tags ist die Verwendung der Attribute `width` und `height` nicht nur erlaubt, sondern explizit erwünscht und gilt als Best Practice.

**Modernes HTML (sehr gut):**

```html
<img src="katze.jpg" width="400" height="300" alt="Eine süße Katze">
```

Warum ist das so? Wenn du dem Browser die Dimensionen eines Bildes direkt im HTML mitteilst, kann er den benötigten Platz auf der Seite sofort reservieren, noch bevor das Bild vollständig geladen ist. Dies verhindert einen sogenannten **Layout Shift** – das unschöne Springen des Seiteninhalts, wenn Bilder nachladen und plötzlich Platz beanspruchen. Die `width`- und `height`-Attribute definieren hier das Seitenverhältnis des Bildes. Mit CSS kannst du das Bild dann immer noch responsiv gestalten, ohne das Seitenverhältnis zu verlieren:

```css
img {
  max-width: 100%;
  height: auto; /* Sorgt dafür, dass die Höhe proportional angepasst wird */
}
```

Diese Kombination aus HTML-Attributen zur Platzreservierung und CSS für flexibles Verhalten ist der moderne Standard im Umgang mit Bildern.

Der Umstieg von präsentationsbezogenen HTML-Attributen auf eine saubere Trennung mit CSS ist mehr als nur eine kosmetische Korrektur. Es ist ein fundamentaler Schritt hin zu robusterem, wartbarerem und zukunftssicherem Code. Jedes Mal, wenn du ein altes `align` oder `bgcolor` durch eine CSS-Klasse ersetzt, investierst du in die Qualität und Langlebigkeit deines Projekts.
