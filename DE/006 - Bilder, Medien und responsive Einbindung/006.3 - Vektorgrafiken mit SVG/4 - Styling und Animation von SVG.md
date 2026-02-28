# Styling und Animation von SVG

### Styling und Animation von SVG: Vektoren zum Leben erwecken

Nachdem du die grundlegenden Formen und Strukturen von SVG kennengelernt hast, tauchen wir nun in den Bereich ein, der SVG seine wahre Magie verleiht: das Styling und die Animation. Eine reine Vektorgrafik ist nur ein Gerüst. Erst durch Farben, Linienstärken und Bewegung wird sie zu einem lebendigen Teil deiner Webseite. Das Schöne an SVG ist, dass du dafür die Werkzeuge nutzen kannst, die du bereits aus der Webentwicklung kennst: CSS. Gleichzeitig bietet SVG aber auch eigene, mächtige Mechanismen, um Grafiken zum Leben zu erwecken.

#### SVG mit CSS gestalten: Drei Wege zum Ziel

Die Verknüpfung von SVG und CSS ist extrem eng. Du kannst SVG-Elemente fast genauso ansprechen und gestalten wie HTML-Elemente. Es gibt drei primäre Methoden, um Stilregeln auf deine SVGs anzuwenden.

**1. Präsentationsattribute (Presentation Attributes)**

Der direkteste Weg, ein SVG-Element zu stylen, ist die Verwendung von Präsentationsattributen. Dabei schreibst du die Stilinformationen direkt als Attribute in das SVG-Tag. Dies ist vergleichbar mit Inline-Styles in HTML.

```html
<svg width="200" height="200" viewBox="0 0 100 100">
  <rect 
    x="10" 
    y="10" 
    width="80" 
    height="80"
    fill="cornflowerblue"
    stroke="navy"
    stroke-width="3"
  />
</svg>
```

In diesem Beispiel werden die Füllfarbe (`fill`), die Konturfarbe (`stroke`) und die Konturstärke (`stroke-width`) direkt am `<rect>`-Element definiert. Dieser Ansatz ist schnell und einfach für einzelne, simple Grafiken. Sein großer Nachteil ist jedoch die schlechte Wartbarkeit. Wenn du den Stil von zehn gleichen Rechtecken ändern möchtest, musst du zehn verschiedene Stellen im Code anpassen.

**2. Internes CSS mit dem `<style>`-Block**

Eine deutlich sauberere Methode ist die Verwendung eines `<style>`-Blocks direkt innerhalb deiner `<svg>`-Definition. Hier kannst du CSS-Regeln definieren, die für die Elemente innerhalb dieser SVG-Grafik gelten. Du kannst dabei ganz normale CSS-Selektoren wie Element-Selektoren, Klassen oder IDs verwenden.

```html
<svg width="200" height="200" viewBox="0 0 100 100">
  <style>
    .my-box {
      fill: cornflowerblue;
      stroke: navy;
      stroke-width: 3;
    }
    .my-box:hover {
      fill: lightcoral;
    }
  </style>
  <rect class="my-box" x="10" y="10" width="80" height="80" />
</svg>
```

Dieser Ansatz trennt die Struktur (das `<rect>`-Element) von der Präsentation (die CSS-Regeln). Du kannst jetzt die Klasse `.my-box` mehreren Elementen zuweisen und ihren Stil an einer einzigen Stelle zentral verwalten. Wie du siehst, funktionieren sogar Pseudoklassen wie `:hover`, was interaktive Effekte ermöglicht.

**3. Externes CSS-Stylesheet**

Für eine Webseite ist es die beste Praxis, Stile in einer separaten `.css`-Datei zu verwalten. Das gilt auch für SVGs, die du direkt in dein HTML einbettest (Inline-SVG). Du kannst Klassen und IDs in deinem SVG-Markup verwenden und diese wie gewohnt in deinem globalen Stylesheet ansprechen.

**Dein HTML (`index.html`):**

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>SVG mit externem CSS</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>SVG mit externem CSS</h1>
  <svg width="200" height="200" viewBox="0 0 100 100" aria-labelledby="svgTitle">
    <title id="svgTitle">Ein stilisiertes Quadrat</title>
    <rect class="styled-box" x="10" y="10" width="80" height="80" />
  </svg>
</body>
</html>
```

**Dein CSS (`style.css`):**

```css
body {
  font-family: sans-serif;
  text-align: center;
}

.styled-box {
  fill: darkcyan;
  stroke: black;
  stroke-width: 4px; /* Hier ist die Einheit wichtig */
  transition: all 0.3s ease-in-out;
}

.styled-box:hover {
  fill: orange;
  transform: rotate(15deg) scale(1.1);
  transform-origin: center;
}
```

Diese Methode ist die flexibelste und am besten wartbare. Du hältst deine Stile an einem Ort, was die Konsistenz über die gesamte Webseite sicherstellt. Beachte, dass CSS-Eigenschaften wie `transform` auch auf SVG-Elemente angewendet werden können und eine fantastische Grundlage für Animationen bilden.

**Wichtige Styling-Eigenschaften für SVG**

Neben den bereits gezeigten gibt es einige spezifische Eigenschaften, die für SVG besonders relevant sind:

*   `fill`: Bestimmt die Füllfarbe eines Shapes.
*   `stroke`: Legt die Farbe der Kontur fest.
*   `stroke-width`: Definiert die Dicke der Kontur.
*   `stroke-linecap`: Bestimmt das Aussehen der Enden einer offenen Linie (z. B. `butt`, `round`, `square`).
*   `stroke-linejoin`: Legt fest, wie Ecken von Linien dargestellt werden (z. B. `miter`, `round`, `bevel`).
*   `opacity`: Steuert die Transparenz des gesamten Elements (Füllung und Kontur).
*   `fill-opacity` und `stroke-opacity`: Ermöglichen die getrennte Steuerung der Transparenz für Füllung und Kontur.

---

### SVG zum Leben erwecken: Animation

Statische Vektorgrafiken sind nützlich, aber animierte SVGs können die Aufmerksamkeit der Nutzer fesseln und komplexe Informationen auf verständliche Weise vermitteln. Es gibt zwei Hauptansätze, um SVGs zu animieren: CSS und SMIL (Synchronized Multimedia Integration Language).

**1. Animation mit CSS**

Wenn du bereits mit CSS-Transitions und Keyframe-Animationen vertraut bist, hast du Glück: Dieselben Techniken lassen sich hervorragend auf SVG-Elemente anwenden.

**CSS Transitions**

Transitions sind ideal für einfache Zustandsänderungen, zum Beispiel bei einem Hover-Effekt. Im obigen Beispiel mit dem externen Stylesheet haben wir bereits eine Transition verwendet:

```css
.styled-box {
  /* ... andere Stile */
  transition: all 0.3s ease-in-out;
}

.styled-box:hover {
  fill: orange;
  transform: rotate(15deg) scale(1.1);
  transform-origin: center;
}
```

Wenn du mit der Maus über das Rechteck fährst, animiert der Browser den Übergang der `fill`- und `transform`-Eigenschaften sanft über 0,3 Sekunden, anstatt sie abrupt zu ändern. Du kannst fast jede CSS-Eigenschaft animieren, die einen numerischen Wert hat, wie z. B. `fill`, `stroke`, `stroke-width`, `opacity` und `transform`.

**CSS Keyframe-Animationen**

Für komplexere, sich wiederholende oder mehrstufige Animationen sind `@keyframes` die richtige Wahl. Du definierst eine Animationssequenz und wendest sie dann mit der `animation`-Eigenschaft auf ein Element an.

Stellen wir uns einen einfachen Ladeindikator vor, der pulsiert:

```html
<svg width="100" height="100" viewBox="0 0 100 100">
  <circle class="pulsing-circle" cx="50" cy="50" r="40" />
</svg>
```

```css
.pulsing-circle {
  fill: steelblue;
  transform-origin: center;
  animation: pulse 2s infinite ease-in-out;
}

@keyframes pulse {
  0% {
    transform: scale(1);
    opacity: 1;
  }
  50% {
    transform: scale(1.1);
    opacity: 0.7;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}
```

In diesem Beispiel wird der Kreis innerhalb von zwei Sekunden auf 110 % seiner Größe skaliert und leicht transparent, bevor er wieder in seinen Ausgangszustand zurückkehrt. Dank `infinite` läuft diese Animation in einer Endlosschleife.

**2. Animation mit SMIL (SVG-Native Animation)**

SMIL ist eine XML-basierte Sprache und ein integraler Bestandteil des SVG-Standards. Sie ermöglicht es dir, Animationen direkt im SVG-Markup zu deklarieren. Auch wenn CSS-Animationen oft als moderner gelten und eine bessere Performance bei einfachen Transformationen bieten, hat SMIL einige einzigartige Fähigkeiten, die CSS nicht beherrscht.

Die grundlegenden Animationselemente von SMIL sind:

*   `<animate>`: Animiert ein einzelnes Attribut über eine Zeitspanne.
*   `<animateTransform>`: Animiert ein Transformationsattribut (`transform`).
*   `<animateMotion>`: Bewegt ein Element entlang eines definierten Pfades.

**Beispiel für `<animate>`**

Stellen wir uns einen Kreis vor, dessen Farbe sich von Rot zu Blau ändert.

```html
<svg width="100" height="100" viewBox="0 0 100 100">
  <circle cx="50" cy="50" r="40" fill="red">
    <animate 
      attributeName="fill"
      from="red"
      to="blue"
      dur="3s"
      repeatCount="indefinite"
    />
  </circle>
</svg>
```

Hier wird das Attribut `fill` des Kreises animiert. Die Animation startet bei `red`, endet bei `blue`, dauert 3 Sekunden (`dur`) und wiederholt sich unendlich (`repeatCount="indefinite"`). Das ist deklarativ, leicht verständlich und vollständig in der SVG-Datei enthalten.

**Beispiel für `<animateTransform>`**

Für Transformationen wie Rotationen ist `<animateTransform>` die bessere Wahl.

```html
<svg width="100" height="100" viewBox="0 0 100 100">
  <rect x="25" y="25" width="50" height="50" fill="darkviolet">
    <animateTransform
      attributeName="transform"
      type="rotate"
      from="0 50 50"
      to="360 50 50"
      dur="5s"
      repeatCount="indefinite"
    />
  </rect>
</svg>
```

Dieses Rechteck dreht sich innerhalb von 5 Sekunden einmal vollständig um seinen Mittelpunkt (`50 50`).

**Die Superkraft von SMIL: Pfadanimation und Morphing**

Die wahre Stärke von SMIL liegt in Animationen, die mit CSS nur schwer oder gar nicht umsetzbar sind.

**Pfadanimation mit `<animateMotion>`**

Du kannst ein Element exakt entlang eines SVG-Pfades bewegen lassen.

```html
<svg width="400" height="200" viewBox="0 0 400 200">
  <!-- Der Pfad, der als Bewegungspfad dient (kann unsichtbar sein) -->
  <path id="motionPath" d="M 50,100 C 150,20 250,180 350,100" stroke="lightgrey" fill="none" />

  <!-- Das Element, das sich bewegt -->
  <circle cx="0" cy="0" r="10" fill="tomato">
    <animateMotion dur="5s" repeatCount="indefinite">
      <mpath href="#motionPath" />
    </animateMotion>
  </circle>
</svg>
```

Der rote Kreis folgt nun perfekt der geschwungenen Kurve des `<path>`. Das ist unglaublich mächtig für Infografiken oder komplexe visuelle Effekte.

**Morphing von Pfaden**

Eine weitere beeindruckende Fähigkeit ist das "Morphing" – die fließende Umwandlung einer Form in eine andere. Dies geschieht durch die Animation des `d`-Attributs eines `<path>`-Elements. Voraussetzung ist, dass der Start- und Endpfad die gleiche Anzahl an Ankerpunkten haben.

```html
<svg width="200" height="100" viewBox="0 0 200 100">
  <path fill="mediumseagreen">
    <animate
      attributeName="d"
      dur="3s"
      repeatCount="indefinite"
      values="M 20,50 Q 50,20 80,50 T 140,50;  /* Startform: Welle */
              M 20,50 L 80,50 L 80,80 L 20,80 Z; /* Zielform: Quadrat (angepasst) */
              M 20,50 Q 50,20 80,50 T 140,50"  /* Zurück zur Welle */
    />
  </path>
</svg>
```

Die Animation wechselt hier zwischen den in `values` definierten Pfaddaten und erzeugt einen flüssigen Übergang.

#### Wann solltest du was verwenden?

*   **CSS:** Nutze CSS für die meisten interaktiven Animationen (z. B. `:hover`), für einfache Transformationen und wenn die Animationen konsistent mit dem Rest deiner Webseite sein sollen. Die Performance ist oft besser, da Browser CSS-Transformationen auf der GPU beschleunigen können.
*   **SMIL:** Wähle SMIL, wenn du Animationen benötigst, die untrennbar mit der SVG-Grafik verbunden sein sollen (z. B. wenn die SVG-Datei eigenständig verwendet wird). Greife unbedingt zu SMIL für komplexe Pfadanimationen, Form-Morphing und präzise, zeitlich abgestimmte Animationen innerhalb der Grafik.

Indem du Styling und Animation beherrschst, verwandelst du einfache SVG-Strukturen in ausdrucksstarke, interaktive und nützliche Komponenten für deine Webprojekte.
