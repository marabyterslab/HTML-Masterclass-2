# Canvas-Element Grundlagen

### Canvas-Element Grundlagen: Deine digitale Leinwand

Stell dir vor, du hättest in deinem Browserfenster eine leere Leinwand, auf der du mit Code malen, zeichnen und animieren kannst. Genau das ist das HTML-`canvas`-Element. Anders als andere HTML-Elemente wie `<p>`, `<img>` oder `<div>`, die eine vordefinierte Struktur und Bedeutung haben, ist `<canvas>` im Grunde nur ein rechteckiger Bereich auf deiner Webseite – ein Behälter für Grafiken, die du dynamisch mit JavaScript erstellst.

Es besitzt keinen eigenen Inhalt und keine eigene Form, bis du ihm mit JavaScript Leben einhauchst. Das macht es zu einem unglaublich mächtigen Werkzeug für Datenvisualisierung, Spieleentwicklung, Fotobearbeitung und Echtzeit-Grafikanwendungen direkt im Browser.

#### Die Einrichtung: Das HTML-Fundament

Alles beginnt mit einem einfachen HTML-Tag. Um eine Leinwand zu erstellen, fügst du das `<canvas>`-Element in den `<body>` deines HTML-Dokuments ein:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Canvas Grundlagen</title>
    <style>
        canvas {
            border: 1px solid black; /* Ein Rahmen, um die Leinwand sichtbar zu machen */
        }
    </style>
</head>
<body>
    <h1>Meine erste Zeichnung</h1>
    <canvas id="meineLeinwand" width="600" height="400">
        Dein Browser unterstützt das Canvas-Element leider nicht.
    </canvas>
    <script src="zeichnung.js"></script>
</body>
</html>
```

Schauen wir uns die wichtigsten Teile genauer an:

*   **`id="meineLeinwand"`**: Eine ID ist unerlässlich, damit du das Canvas-Element später in deinem JavaScript-Code gezielt ansprechen kannst.
*   **`width="600"` und `height="400"`**: Diese Attribute definieren die Größe der Zeichenfläche in Pixeln. Es ist entscheidend, die Größe direkt über diese HTML-Attribute festzulegen und nicht nur über CSS. Wenn du die Größe ausschließlich mit CSS (`width: 600px;`) änderst, skalierst du nur das Element selbst, nicht aber die zugrunde liegende Zeichenfläche. Das führt zu verzerrten und unscharfen Grafiken. Die HTML-Attribute bestimmen die Auflösung, CSS die Anzeigegröße.
*   **Fallback-Inhalt**: Der Text zwischen den `<canvas>`-Tags wird nur in sehr alten Browsern angezeigt, die das Element nicht unterstützen. Es ist eine gute Praxis, hier eine alternative Information bereitzustellen.

Ohne JavaScript bleibt diese Leinwand jedoch leer. Die eigentliche Magie geschieht, wenn wir beginnen, darauf zu zeichnen.

#### Der Rendering-Kontext: Deine Werkzeugkiste

Um auf der Leinwand zeichnen zu können, benötigst du einen sogenannten "Rendering-Kontext". Stell ihn dir als deine Werkzeugkiste vor, die alle Pinsel, Farben und Funktionen enthält, die du zum Malen brauchst. Der gebräuchlichste Kontext ist der 2D-Kontext, mit dem du zweidimensionale Formen, Linien und Texte zeichnen kannst.

In deiner JavaScript-Datei (hier `zeichnung.js`) holst du dir zuerst das Canvas-Element und dann seinen Kontext:

```javascript
// 1. Das Canvas-Element aus dem DOM holen
const canvas = document.getElementById('meineLeinwand');

// 2. Den 2D-Rendering-Kontext abrufen
const ctx = canvas.getContext('2d');
```

Die Variable `canvas` ist nun eine Referenz auf unser HTML-Element. Die Variable `ctx` (eine gängige Abkürzung für "Context") ist das Herzstück unserer Arbeit. Ab jetzt werden fast alle Zeichenoperationen über dieses `ctx`-Objekt aufgerufen.

#### Das Koordinatensystem: Wo ist was?

Bevor du den ersten Strich ziehst, musst du das Koordinatensystem des Canvas verstehen. Es ist einfach, aber unterscheidet sich von dem, was du vielleicht aus dem Mathematikunterricht kennst.

*   Der Ursprung `(0, 0)` befindet sich in der **oberen linken Ecke** der Leinwand.
*   Die **X-Achse** verläuft von links nach rechts.
*   Die **Y-Achse** verläuft von **oben nach unten**.

Ein Punkt bei `(50, 100)` befindet sich also 50 Pixel vom linken Rand und 100 Pixel vom oberen Rand entfernt. Dieses System ist in der Computergrafik weit verbreitet und du wirst dich schnell daran gewöhnen.

#### Grundlegende Formen: Rechtecke

Die einfachsten Formen, die du zeichnen kannst, sind Rechtecke. Der 2D-Kontext bietet dafür drei grundlegende Methoden:

*   `fillRect(x, y, breite, höhe)`: Zeichnet ein ausgefülltes Rechteck.
*   `strokeRect(x, y, breite, höhe)`: Zeichnet den Umriss eines Rechtecks.
*   `clearRect(x, y, breite, höhe)`: Löscht einen rechteckigen Bereich und macht ihn wieder transparent.

Bevor du zeichnest, solltest du Farbe und Stil festlegen. Dafür gibt es zwei wichtige Eigenschaften des Kontexts:

*   `fillStyle`: Bestimmt die Füllfarbe für Formen.
*   `strokeStyle`: Bestimmt die Linienfarbe für Umrisse.

Hier ist ein Beispiel, das diese Konzepte kombiniert:

```javascript
// JavaScript-Code in 'zeichnung.js'

const canvas = document.getElementById('meineLeinwand');
const ctx = canvas.getContext('2d');

// Ein rotes, gefülltes Rechteck zeichnen
ctx.fillStyle = 'red'; // Farbe als CSS-Farbwert (Name, Hex, RGB, etc.)
ctx.fillRect(50, 50, 150, 100); // Start bei (50, 50), 150px breit, 100px hoch

// Einen blauen Umriss für ein anderes Rechteck zeichnen
ctx.strokeStyle = 'blue';
ctx.lineWidth = 5; // Die Liniendicke festlegen
ctx.strokeRect(250, 50, 150, 100);

// Einen Teil des ersten Rechtecks wieder löschen
ctx.clearRect(75, 75, 50, 50);
```

Wenn du diese Seite öffnest, siehst du ein rotes Rechteck mit einem Loch, daneben den blauen Umriss eines zweiten Rechtecks.

#### Pfade: Der Weg zur kreativen Freiheit

Rechtecke sind nützlich, aber die wahre Stärke des Canvas liegt im Zeichnen von benutzerdefinierten Pfaden. Ein Pfad ist eine Sequenz von Punkten, die durch Linien oder Kurven verbunden sind. Stell es dir so vor, als würdest du einen Stift auf ein Blatt Papier setzen, ihn bewegen und am Ende entscheiden, ob du die gezogene Linie nachzeichnest oder die umschlossene Form ausmalst.

Der Prozess folgt immer diesen Schritten:

1.  **Pfad beginnen**: Mit `ctx.beginPath()` signalisierst du, dass du eine neue, unabhängige Form zeichnen möchtest. Das ist wichtig, da sonst alte Pfade erneut gezeichnet werden könnten.
2.  **Pfad definieren**: Du bewegst deinen virtuellen Stift mit Methoden wie:
    *   `moveTo(x, y)`: Setzt den Startpunkt, ohne eine Linie zu zeichnen.
    *   `lineTo(x, y)`: Zeichnet eine gerade Linie vom aktuellen Punkt zum neuen Punkt `(x, y)`.
    *   `arc(x, y, radius, startWinkel, endWinkel, gegenUhrzeigersinn)`: Zeichnet einen Bogen oder einen Kreis.
3.  **(Optional) Pfad schließen**: Mit `ctx.closePath()` wird eine gerade Linie vom Endpunkt zurück zum Startpunkt gezogen.
4.  **Pfad rendern**: Erst jetzt wird der definierte Pfad sichtbar gemacht:
    *   `ctx.stroke()`: Zeichnet den Umriss des Pfades.
    *   `ctx.fill()`: Füllt die vom Pfad umschlossene Fläche.

Lass uns ein einfaches Dreieck zeichnen:

```javascript
// Weiter im 'zeichnung.js'

// Ein grünes Dreieck
ctx.beginPath();          // Neuen Pfad starten
ctx.moveTo(100, 200);     // Startpunkt unten links
ctx.lineTo(200, 200);     // Linie nach unten rechts
ctx.lineTo(150, 150);     // Linie zur Spitze oben in der Mitte
ctx.closePath();          // Pfad schließen (Linie von Spitze zum Start)

ctx.fillStyle = 'green';
ctx.fill();               // Das Dreieck füllen

// Eine lilafarbene Linie daneben
ctx.beginPath();          // Wichtig: Neuen Pfad für die Linie starten!
ctx.moveTo(300, 150);
ctx.lineTo(400, 250);

ctx.strokeStyle = 'purple';
ctx.lineWidth = 3;
ctx.stroke();             // Nur den Pfad (die Linie) zeichnen
```

#### Kreise und Bögen zeichnen

Die `arc()`-Methode ist etwas komplexer, aber sehr mächtig. Sie benötigt Zentrum, Radius und Winkel. Wichtig ist hierbei, dass die Winkel in **Radiant** angegeben werden, nicht in Grad. Ein voller Kreis entspricht `2 * Math.PI`.

Ein einfacher Kreis lässt sich so zeichnen:

```javascript
// Ein oranger Kreis
ctx.beginPath();
ctx.arc(450, 300, 50, 0, 2 * Math.PI); // x, y, Radius, Startwinkel 0, Endwinkel 2*PI

ctx.fillStyle = 'orange';
ctx.fill();
```

#### Text hinzufügen

Natürlich kannst du auch Text auf deine Leinwand schreiben. Ähnlich wie bei Rechtecken gibt es Methoden zum Füllen und Umreißen:

*   `fillText(text, x, y)`
*   `strokeText(text, x, y)`

Zuvor kannst du die Schriftart und -größe über die `font`-Eigenschaft festlegen, die eine ähnliche Syntax wie die CSS `font`-Eigenschaft verwendet.

```javascript
// Text auf der Leinwand platzieren
ctx.font = '30px Arial';
ctx.fillStyle = 'black';
ctx.fillText('Hallo Canvas!', 250, 350);
```

#### Ein erstes Datenvisualisierungsbeispiel: Ein Balkendiagramm

Nun führen wir alles zusammen und wenden es auf das Kernthema dieses Moduls an: die Datenvisualisierung. Angenommen, wir haben ein einfaches Array von Daten, das wir als Balkendiagramm darstellen möchten.

```javascript
// Die Daten, die wir visualisieren wollen
const daten = [75, 120, 90, 200, 150];
const balkenBreite = 50;
const balkenAbstand = 20;
const startX = 50;
const startY = 380; // Startpunkt auf der y-Achse (unten)

ctx.font = '16px sans-serif';
ctx.fillStyle = '#333';

// Eine Schleife über unsere Daten
for (let i = 0; i < daten.length; i++) {
    const datenpunkt = daten[i];
    
    // Die x-Position für jeden Balken berechnen
    const x = startX + i * (balkenBreite + balkenAbstand);
    
    // Die y-Position (Startpunkt oben) und Höhe des Balkens
    const y = startY - datenpunkt;
    const hoehe = datenpunkt;

    // Balken zeichnen
    ctx.fillStyle = '#008cba';
    ctx.fillRect(x, y, balkenBreite, hoehe);

    // Beschriftung unter dem Balken hinzufügen
    ctx.fillStyle = '#333';
    ctx.fillText(datenpunkt, x + balkenBreite / 4, startY + 15);
}
```

Dieser Codeblock durchläuft das `daten`-Array. Für jeden Wert berechnet er die Position und Größe eines Rechtecks und zeichnet es mit `fillRect`. Die Höhe des Balkens (`hoehe`) entspricht direkt dem Datenwert, und die `y`-Position wird von unten (`startY`) nach oben berechnet, da unser Koordinatensystem oben beginnt. Das Ergebnis ist ein einfaches, aber effektives Balkendiagramm – vollständig dynamisch mit JavaScript auf einer leeren Leinwand erstellt.

Das `canvas`-Element öffnet eine Tür zu einer Welt visueller Kreativität, die weit über die Grenzen von Standard-HTML und CSS hinausgeht. Mit diesen Grundlagen bist du nun gerüstet, um deine eigenen Datenvisualisierungen, Grafiken und interaktiven Elemente zu schaffen.
