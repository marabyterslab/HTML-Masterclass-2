# SVG für Daten

### SVG: Die Leinwand für deine Daten

Wenn du an Bilder im Web denkst, kommen dir wahrscheinlich Formate wie JPEG, PNG oder GIF in den Sinn. Das sind Rastergrafiken – im Grunde eine Ansammlung von Pixeln. Zoomst du zu weit hinein, siehst du die einzelnen Quadrate und das Bild wird unscharf. Für Fotos ist das perfekt, aber wenn es um die Visualisierung von Daten geht, betreten wir eine Welt, in der Präzision, Skalierbarkeit und Interaktivität entscheidend sind. Hier kommt SVG ins Spiel.

SVG steht für **Scalable Vector Graphics**. Der Name verrät schon die zwei wichtigsten Eigenschaften: Es ist skalierbar und es basiert auf Vektoren. Anstatt Pixel zu speichern, beschreibt eine SVG-Datei Formen, Linien und Kurven durch mathematische Anweisungen. Ein Kreis wird nicht als eine Ansammlung von farbigen Pixeln gespeichert, sondern als Anweisung: "Zeichne einen Kreis mit diesem Mittelpunkt, diesem Radius und dieser Farbe." Das Ergebnis ist eine Grafik, die du unendlich vergrößern kannst, ohne dass sie jemals an Schärfe verliert.

Das wirklich Revolutionäre an SVG für uns Webentwickler ist jedoch, dass es kein binäres Dateiformat wie ein JPEG ist. Eine SVG-Datei ist reiner XML-Code, also Text, den du direkt in dein HTML-Dokument schreiben kannst.

```html
<svg width="100" height="100">
  <circle cx="50" cy="50" r="40" stroke="black" stroke-width="3" fill="red" />
</svg>
```

Dieser kleine Code-Schnipsel erzeugt einen roten Kreis mit einem schwarzen Rand. Du kannst diesen Code lesen, verstehen und verändern. Und genau hier liegt die Brücke zur Datenvisualisierung: Was wir mit Code beschreiben können, können wir auch dynamisch mit Code *erzeugen*. SVG wird so von einem reinen Bildformat zu einer programmierbaren Leinwand direkt in deinem Browser.

#### Die Bausteine von SVG

Um Daten visualisieren zu können, musst du die grundlegenden Werkzeuge von SVG kennen. Stell dir das `<svg>`-Element als deine Leinwand vor. Mit den Attributen `width` und `height` legst du seine Größe im Dokument fest. Im Inneren dieser Leinwand platzierst du dann geometrische Formen.

Die wichtigsten Grundformen sind:

*   `<rect>`: Ein Rechteck. Du definierst es über die Position der oberen linken Ecke (`x`, `y`) sowie seine Breite (`width`) und Höhe (`height`). Perfekt für Balkendiagramme.
*   `<circle>`: Ein Kreis. Benötigt den Mittelpunkt (`cx`, `cy`) und den Radius (`r`).
*   `<ellipse>`: Eine Ellipse. Ähnlich wie ein Kreis, aber mit zwei Radien (`rx` und `ry`).
*   `<line>`: Eine einfache Linie. Du gibst die Start- (`x1`, `y1`) und Endkoordinaten (`x2`, `y2`) an. Ideal für Gitterlinien oder Achsen in einem Diagramm.
*   `<polyline>`: Eine Serie von verbundenen geraden Linien. Nützlich für Liniendiagramme.
*   `<polygon>`: Eine geschlossene Form aus verbundenen geraden Linien.
*   `<path>`: Das mächtigste Element. Mit ihm kannst du beliebige Formen, inklusive komplexer Kurven, zeichnen.

Jede dieser Formen kann mit Attributen wie `fill` (Füllfarbe), `stroke` (Linienfarbe), `stroke-width` (Liniendicke) und `opacity` (Deckkraft) gestaltet werden.

Ein einfaches Balkendiagramm könnte also aus mehreren `<rect>`-Elementen bestehen. Ein Streudiagramm (Scatter Plot) wäre eine Sammlung von `<circle>`-Elementen. Ein Liniendiagramm ließe sich mit einem `<polyline>`- oder `<path>`-Element realisieren.

#### Vom Datensatz zur Visualisierung

Die wahre Magie beginnt, wenn du Daten und SVG mit JavaScript verbindest. Stell dir vor, du hast einen einfachen Datensatz, der die Verkaufszahlen für verschiedene Produkte repräsentiert:

```javascript
const salesData = [
  { product: 'Apfel', unitsSold: 120 },
  { product: 'Banane', unitsSold: 210 },
  { product: 'Kirsche', unitsSold: 85 },
  { product: 'Dattel', unitsSold: 150 }
];
```

Dein Ziel ist es, diese Daten als einfaches Balkendiagramm darzustellen.

**1. Die HTML-Grundlage**

Zuerst brauchst du einen leeren SVG-Container in deinem HTML. Dies ist die Leinwand, die JavaScript später mit Leben füllen wird.

```html
<div id="chart-container">
  <svg id="barchart" width="500" height="300"></svg>
</div>
```

**2. Die JavaScript-Logik**

Nun schreibst du ein Skript, das die Daten nimmt und für jeden Dateneintrag ein SVG-Element erzeugt.

```javascript
// Unsere Daten
const salesData = [
  { product: 'Apfel', unitsSold: 120 },
  { product: 'Banane', unitsSold: 210 },
  { product: 'Kirsche', unitsSold: 85 },
  { product: 'Dattel', unitsSold: 150 }
];

// Die SVG-Leinwand auswählen
const svg = document.getElementById('barchart');
const svgWidth = parseInt(svg.getAttribute('width'));
const svgHeight = parseInt(svg.getAttribute('height'));

// Einige Parameter für das Diagramm festlegen
const barPadding = 10;
const barWidth = (svgWidth / salesData.length) - barPadding;
let currentX = 0;

// Durch die Daten iterieren und Balken erstellen
salesData.forEach(item => {
  // Die Höhe des Balkens muss skaliert werden, damit sie in unsere SVG-Leinwand passt.
  // Wir finden den Maximalwert, um die Skala zu bestimmen.
  const maxValue = 250; // In einem echten Szenario würdest du das Maximum dynamisch ermitteln.
  const barHeight = (item.unitsSold / maxValue) * svgHeight;

  // Ein <rect>-Element erzeugen
  const rect = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
  rect.setAttribute('x', currentX);
  rect.setAttribute('y', svgHeight - barHeight); // Y-Koordinate startet oben, daher müssen wir von der Gesamthöhe abziehen.
  rect.setAttribute('width', barWidth);
  rect.setAttribute('height', barHeight);
  rect.setAttribute('fill', '#4a90e2');
  
  // Den neuen Balken zur SVG hinzufügen
  svg.appendChild(rect);
  
  // Die X-Position für den nächsten Balken aktualisieren
  currentX += barWidth + barPadding;
});
```

Ein wichtiger Punkt hier ist die Zeile `document.createElementNS(...)`. Da SVG-Elemente in einem anderen *Namespace* als HTML-Elemente leben, musst du diese spezielle Methode anstelle des üblichen `document.createElement()` verwenden. Der erste Parameter, `'http://www.w3.org/2000/svg'`, teilt dem Browser mit, dass du ein SVG-Element erstellen möchtest.

Das Ergebnis ist ein dynamisch generiertes Balkendiagramm. Wenn sich deine `salesData` ändern – zum Beispiel durch eine API-Abfrage – kannst du einfach das Skript erneut ausführen, und das Diagramm aktualisiert sich. Du malst nicht einfach ein Bild; du definierst ein System, das Daten in eine visuelle Repräsentation übersetzt.

#### Interaktivität und Styling

Da SVG-Elemente Teil des DOM sind, verhalten sie sich wie ganz normale HTML-Elemente. Das bedeutet:

1.  **Du kannst sie mit CSS stylen:** Anstatt `fill` oder `stroke` als Attribute direkt im Element zu setzen, kannst du Klassen vergeben und das Styling in eine separate CSS-Datei auslagern. Das macht deinen Code sauberer und wiederverwendbarer.

    ```css
    .bar {
      fill: #4a90e2;
      transition: fill 0.3s ease;
    }

    .bar:hover {
      fill: #2a70c2;
    }
    ```

    ```javascript
    // Im JavaScript dann einfach die Klasse setzen:
    rect.setAttribute('class', 'bar');
    ```

2.  **Du kannst Event-Listener hinzufügen:** Du möchtest einen Tooltip mit dem genauen Wert anzeigen, wenn der Nutzer mit der Maus über einen Balken fährt? Kein Problem.

    ```javascript
    rect.addEventListener('mouseover', () => {
      console.log(`Produkt: ${item.product}, Verkauft: ${item.unitsSold}`);
      // Hier könntest du die Logik für einen Tooltip einfügen.
    });

    rect.addEventListener('mouseout', () => {
      // Logik zum Ausblenden des Tooltips.
    });
    ```

Diese Fähigkeit, auf Benutzerinteraktionen zu reagieren, hebt SVG-Visualisierungen fundamental von statischen Bildern ab. Du schaffst keine reinen Abbildungen, sondern interaktive Daten-Werkzeuge.

#### Barrierefreiheit nicht vergessen

Ein weiterer unschätzbarer Vorteil von textbasiertem SVG ist die Barrierefreiheit. Für einen Screenreader ist ein PNG-Bild nur das, was sein `alt`-Attribut beschreibt. Eine SVG-Grafik ist jedoch eine Struktur aus Elementen. Du kannst sie mit speziellen Tags anreichern, um Nutzern mit assistiven Technologien eine reichhaltigere Erfahrung zu bieten.

*   `<title>`: Gibt einen Titel für das SVG-Element oder die gesamte Grafik an. Dies wird oft als Tooltip im Browser angezeigt.
*   `<desc>` (description): Bietet eine längere, detailliertere Beschreibung des Inhalts.

```html
<svg width="500" height="300" role="img" aria-labelledby="chartTitle">
  <title id="chartTitle">Balkendiagramm der Verkaufszahlen</title>
  <desc>Ein Diagramm, das die Verkaufszahlen von vier Produkten zeigt.</desc>
  
  <!-- Hier folgen die <rect>-Elemente für die Balken -->
  <g>
    <rect class="bar" x="0" y="100" width="100" height="200">
      <title>Apfel: 120 Einheiten</title>
    </rect>
    <!-- ... weitere Balken ... -->
  </g>
</svg>
```

Indem du jedem Balken einen eigenen `<title>` gibst, kann ein Screenreader die genauen Daten vorlesen, wenn der Nutzer durch das Diagramm navigiert. Mit dem `<g>`-Element (group) kannst du zudem zusammengehörige Elemente gruppieren und die Struktur deiner Visualisierung semantisch verbessern.

SVG ist weit mehr als nur ein alternatives Bildformat. Es ist eine offene, standardisierte und unglaublich mächtige Technologie, die perfekt an der Schnittstelle von HTML, CSS und JavaScript angesiedelt ist. Es gibt dir die volle Kontrolle, um aus rohen Daten lebendige, interaktive und für alle zugängliche Visualisierungen direkt im Browser zu erschaffen.
