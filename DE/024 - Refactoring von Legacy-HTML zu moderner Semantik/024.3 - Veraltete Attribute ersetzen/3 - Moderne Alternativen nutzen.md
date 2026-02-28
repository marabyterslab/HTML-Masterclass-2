# Moderne Alternativen nutzen

### Moderne Alternativen nutzen: Von veralteten Attributen zu sauberem CSS

Eine der wichtigsten Aufgaben beim Refactoring von älterem HTML-Code ist das konsequente Ersetzen von veralteten, präsentationsbezogenen Attributen. In den Anfängen des Webs war es üblich, das Aussehen von Elementen direkt im HTML zu definieren. HTML war damals sowohl für die Struktur als auch für das Design zuständig. Diese Praxis ist heute überholt und widerspricht dem fundamentalen Prinzip der **Trennung von Belangen** (Separation of Concerns).

Dieses Prinzip besagt, dass die drei Säulen des Webs klar voneinander getrennt sein sollten:

1.  **HTML** für die Struktur und Bedeutung des Inhalts.
2.  **CSS** für die Präsentation und das visuelle Design.
3.  **JavaScript** für die Interaktivität und das Verhalten.

Wenn du Design-Informationen aus deinem HTML entfernst und sie stattdessen in ein externes CSS-Stylesheet auslagerst, gewinnst du enorm an Flexibilität, Wartbarkeit und Effizienz. Dein HTML wird sauberer und semantischer, und dein CSS wird zur zentralen Schaltstelle für das gesamte visuelle Erscheinungsbild deiner Website.

Schauen wir uns die häufigsten veralteten Attribute an und wie du sie durch moderne CSS-Eigenschaften ersetzt.

#### Textausrichtung: Das `align`-Attribut

Eines der am häufigsten anzutreffenden Relikte ist das `align`-Attribut, das auf Elementen wie Absätzen (`<p>`), Überschriften (`<h1>`-`<h6>`) oder Containern (`<div>`) verwendet wurde.

**Der alte Weg:**

```html
<h1 align="center">Willkommen auf meiner Webseite</h1>
<p align="right">Ein kleiner Text am rechten Rand.</p>
<div align="center">
  <p>Dieser ganze Bereich ist zentriert.</p>
</div>
```

Dieses Vorgehen ist problematisch. Wenn du die Ausrichtung aller Überschriften auf deiner gesamten Website ändern möchtest, müsstest du jede einzelne HTML-Datei bearbeiten.

**Der moderne Ansatz mit CSS:**

Der saubere Weg ist, die Ausrichtung über die CSS-Eigenschaft `text-align` zu steuern. Am besten verwendest du dafür Klassen, um die Styles wiederverwendbar zu machen, oder du sprichst die Elemente direkt über ihren Tag-Namen an, wenn die Regel global gelten soll.

Dein HTML wird dadurch extrem schlank:

```html
<h1 class="text-center">Willkommen auf meiner Webseite</h1>
<p class="text-right">Ein kleiner Text am rechten Rand.</p>
<div class="text-center">
  <p>Dieser ganze Bereich ist zentriert.</p>
</div>
```

Das zugehörige CSS könnte so aussehen:

```css
.text-center {
  text-align: center;
}

.text-right {
  text-align: right;
}

/* Oder, wenn alle h1-Elemente zentriert sein sollen: */
h1 {
  text-align: center;
}
```

Der Vorteil liegt auf der Hand: Eine einzige Änderung in deiner CSS-Datei genügt, um die Ausrichtung auf hunderten von Seiten anzupassen.

#### Farben und Hintergründe: `bgcolor`, `text`, `link` & Co.

Früher wurden Farben für den Hintergrund der Seite, den Text und Links direkt im `<body>`-Tag definiert.

**Der alte Weg:**

```html
<body bgcolor="#FFFFFF" text="#000000" link="#0000FF" vlink="#800080">
  <p>Dies ist ein Absatz mit schwarzem Text auf weißem Hintergrund.</p>
  <a href="#">Ein blauer Link</a>
</body>
```

Diese Methode ist extrem unflexibel und mischt globale Design-Entscheidungen direkt in die Dokumentenstruktur.

**Der moderne Ansatz mit CSS:**

Alle diese Attribute haben direkte Entsprechungen in CSS, die du im Stylesheet für das `body`-Element und für die Anker-Tags (`<a>`) definierst.

Dein HTML ist minimalistisch:

```html
<body>
  <p>Dies ist ein Absatz mit schwarzem Text auf weißem Hintergrund.</p>
  <a href="#">Ein blauer Link</a>
</body>
```

Dein CSS regelt das komplette Erscheinungsbild:

```css
body {
  background-color: #FFFFFF;
  color: #000000;
  font-family: sans-serif; /* Hier kannst du gleich weitere globale Styles definieren */
}

a:link {
  color: #0000FF; /* Farbe für unbesuchte Links */
}

a:visited {
  color: #800080; /* Farbe für besuchte Links */
}

a:hover {
  text-decoration: underline; /* Zusätzlicher Style für den Hover-Zustand */
}
```

Du hast nun nicht nur die alten Attribute ersetzt, sondern auch gleich die Möglichkeit, zusätzliche Zustände wie `:hover` (wenn die Maus über dem Link ist) oder `:focus` (für Tastaturnavigation) zu definieren, was die Benutzerfreundlichkeit und Barrierefreiheit verbessert.

#### Tabellen-Styling: `border`, `cellpadding` und `cellspacing`

Tabellen waren früher ein Hauptwerkzeug für das Layout von Webseiten – eine Praxis, die heute glücklicherweise durch CSS-Grid und Flexbox abgelöst wurde. Für die Darstellung von tabellarischen Daten sind sie aber weiterhin das richtige semantische Element. Ihr Aussehen sollte jedoch ausschließlich über CSS gesteuert werden.

**Der alte Weg:**

```html
<table border="1" cellpadding="10" cellspacing="5" width="100%">
  <tr>
    <td>Zelle 1</td>
    <td>Zelle 2</td>
  </tr>
</table>
```

**Der moderne Ansatz mit CSS:**

Die Attribute `border`, `cellpadding` (Innenabstand der Zelle) und `cellspacing` (Abstand zwischen den Zellen) werden durch CSS-Eigenschaften wie `border`, `padding` und `border-collapse` ersetzt.

Das saubere HTML:

```html
<table class="data-table">
  <tr>
    <td>Zelle 1</td>
    <td>Zelle 2</td>
  </tr>
</table>
```

Das flexible CSS:

```css
.data-table {
  width: 100%;
  border-collapse: collapse; /* Lässt Zell-Ränder zusammenfallen, ersetzt cellspacing="0" */
}

.data-table td,
.data-table th {
  border: 1px solid #ccc; /* Ersetzt border="1" */
  padding: 10px;          /* Ersetzt cellpadding="10" */
  text-align: left;
}
```

Mit `border-collapse: collapse;` erzielst du einen sauberen, modernen Look für Tabellenränder, der mit dem alten `cellspacing`-Attribut nur schwer zu erreichen war. Außerdem hast du die volle Kontrolle über Rahmenfarben, -stärken und -stile.

#### Größenangaben: `width` und `height`

Die Attribute `width` und `height` sind ein spezieller Fall. Auf Elementen wie `<div>`, `<p>` oder `<td>` sind sie rein präsentationsbezogen und sollten durch CSS ersetzt werden.

**Der alte Weg (bei einem Layout-Element):**

```html
<td width="200">Diese Spalte ist 200 Pixel breit.</td>
```

**Der moderne Ansatz mit CSS:**

```html
<td class="sidebar-column">Diese Spalte ist 200 Pixel breit.</td>
```

```css
.sidebar-column {
  width: 200px;
}
```

Der große Vorteil von CSS ist, dass du viel flexiblere Einheiten nutzen kannst, z.B. Prozent (`%`), Viewport-Breite (`vw`) oder relative Einheiten (`rem`). Außerdem kannst du `min-width` und `max-width` verwenden, um dein Layout responsiv zu gestalten.

**Eine wichtige Ausnahme: Bilder und Medien**

Bei `<img>`, `<video>` und `<iframe>` sind die Attribute `width` und `height` **nicht** veraltet. Im Gegenteil: Sie sind sogar extrem wichtig für die Performance deiner Webseite. Wenn du diese Attribute direkt im HTML angibst, weiß der Browser schon vor dem Laden der Bilddatei, wie viel Platz er dafür reservieren muss. Das verhindert den sogenannten **Cumulative Layout Shift (CLS)** – ein unschönes Springen des Layouts, während die Seite lädt.

**Best Practice für Bilder:**

```html
<img src="katze.jpg" width="400" height="300" alt="Eine süße Katze">
```

Das CSS sorgt dann dafür, dass das Bild responsiv bleibt, ohne seine Proportionen zu verzerren:

```css
img {
  max-width: 100%;
  height: auto;
}
```

Diese Kombination gibt dem Browser die anfänglichen Maße für die Platzreservierung und erlaubt es dem CSS gleichzeitig, das Bild bei Bedarf kleiner zu skalieren, ohne es zu verzerren.

#### Typografie: Das `<font>`-Element

Das `<font>`-Element ist der Inbegriff veralteten HTMLs. Es wurde verwendet, um Schriftart, -größe und -farbe für einzelne Textabschnitte festzulegen.

**Der alte Weg:**

```html
<p>Dies ist normaler Text, aber <font face="Arial" color="red" size="5">dieser Teil</font> ist anders.</p>
```

Dieses Element ist rein präsentationsbezogen und hat keinerlei semantische Bedeutung. Es beschreibt nicht, *was* der Text ist, sondern nur, *wie er aussieht*.

**Der moderne, semantische Ansatz:**

Stattdessen überlegst du dir, *warum* dieser Text anders aussehen soll. Ist er besonders wichtig? Ist er eine Warnung? Verwende ein semantisch passendes Element und style es mit CSS. Oft ist ein `<span>` mit einer Klasse eine gute, neutrale Wahl.

Das HTML beschreibt die Bedeutung:

```html
<p>Dies ist normaler Text, aber <span class="warning-text">dieser Teil</span> ist anders.</p>
```

Das CSS kümmert sich um das Aussehen:

```css
.warning-text {
  font-family: Arial, sans-serif;
  color: red;
  font-size: 1.25em; /* Verwende relative Einheiten für bessere Skalierbarkeit */
  font-weight: bold;
}
```

Indem du eine Klasse wie `warning-text` verwendest, machst du deinen Code selbsterklärend. Du (oder ein Kollege) weißt in einem Jahr noch genau, warum dieser Text rot und fett ist.

#### Jenseits der Präsentation: Verhaltensattribute

Auch wenn sie nicht direkt der Präsentation dienen, gibt es Attribute, die das *Verhalten* von Elementen steuern und deren Logik heute besser in separaten JavaScript-Dateien aufgehoben ist. Das bekannteste Beispiel sind die `on...`-Event-Handler wie `onclick`.

**Der alte Weg (Inline-JavaScript):**

```html
<button onclick="alert('Formular wurde gesendet!');">Senden</button>
```

**Der moderne Ansatz (Unobtrusive JavaScript):**

Das JavaScript wird komplett aus dem HTML entfernt und in eine eigene Datei ausgelagert. Das HTML enthält nur noch einen eindeutigen Bezeichner, z.B. eine ID.

Dein HTML:

```html
<button id="submit-button">Senden</button>
```

Deine JavaScript-Datei (`main.js`):

```javascript
document.addEventListener('DOMContentLoaded', function() {
  const submitButton = document.getElementById('submit-button');
  
  if (submitButton) {
    submitButton.addEventListener('click', function() {
      alert('Formular wurde gesendet!');
    });
  }
});
```

Dieser Ansatz, bekannt als "unobtrusive JavaScript", verbessert die Wartbarkeit deines Codes erheblich. Deine HTML-Struktur bleibt sauber, und die gesamte Logik ist an einem zentralen Ort gebündelt.

Indem du diese alten Muster durch moderne, auf der Trennung von Belangen basierende Techniken ersetzt, hebst du die Qualität deines Codes auf ein professionelles Niveau. Dein HTML wird zu einem reinen, aussagekräftigen Strukturdokument, das leicht zu lesen, zu warten und für Maschinen (wie Suchmaschinen und Screenreader) verständlich ist.
