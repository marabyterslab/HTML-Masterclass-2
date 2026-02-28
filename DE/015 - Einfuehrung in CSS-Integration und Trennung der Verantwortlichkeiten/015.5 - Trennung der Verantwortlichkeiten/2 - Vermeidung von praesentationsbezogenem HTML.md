# Vermeidung von präsentationsbezogenem HTML

### Vermeidung von präsentationsbezogenem HTML

Stell dir vor, du baust ein Haus. Das Fundament, die tragenden Wände, die Decken und das Dach bilden die Struktur – das Gerüst, das alles zusammenhält. Das ist dein HTML. Die Farbe der Wände, die Art der Bodenbeläge, die Vorhänge und die Möbel sind die Gestaltung, die dem Haus seinen Charakter und sein Aussehen verleihen. Das ist dein CSS.

In den Anfängen des Webs war diese Trennung noch nicht so klar. Die Architekten (Webentwickler) haben die Wandfarbe direkt in den Bauplan (HTML-Code) geschrieben. Das war praktisch, solange die Häuser klein und einfach waren. Aber stell dir vor, du möchtest die Farbe aller Wände im ganzen Haus ändern. Du müsstest den gesamten Bauplan durchgehen und jede einzelne Wand neu spezifizieren. Genau dieses Problem führte zur Entwicklung von CSS und dem fundamentalen Prinzip der „Trennung der Verantwortlichkeiten“ (Separation of Concerns).

Dein HTML-Dokument hat eine einzige, klare Aufgabe: Es soll die **Struktur und die semantische Bedeutung deines Inhalts** beschreiben. Es sagt dem Browser, was eine Überschrift, was ein Absatz, was eine Liste und was ein wichtiger Textabschnitt ist. Es sollte aber keine Ahnung davon haben, ob diese Überschrift rot, grün oder blau ist, ob sie zentriert oder linksbündig dargestellt wird oder welche Schriftart sie verwendet. Diese Verantwortung liegt ausschließlich bei CSS.

#### Relikte aus einer vergangenen Ära: Was du nicht mehr verwenden solltest

Um zu verstehen, was modernes, sauberes HTML ausmacht, hilft ein Blick auf die Methoden, die heute als veraltet gelten. Du wirst diesen Elementen und Attributen vielleicht in altem Code oder in schlecht gepflegten Tutorials begegnen, aber in deinen eigenen Projekten haben sie nichts mehr zu suchen.

**Das `<font>`-Element**

Das `<font>`-Element war der Inbegriff für präsentationsbezogenes HTML. Mit ihm konnte man Schriftart, -größe und -farbe direkt im HTML festlegen.

*Veraltetes Beispiel:*
```html
<p>
  Hier ist normaler Text, aber <font color="blue" size="5" face="Arial">dieser Teil</font> ist blau und groß.
</p>
```

Dieses Vorgehen ist ein Albtraum für die Wartung. Wenn du die Farbe von „blau“ auf „dunkelgrau“ ändern möchtest, musst du jede einzelne Stelle im HTML-Code finden und anpassen.

*Moderner, korrekter Ansatz:*
Der Inhalt wird mit semantisch passenden Elementen ausgezeichnet, zum Beispiel einem `<span>`, wenn es keine andere semantische Bedeutung hat, und mit einer Klasse versehen.

HTML:
```html
<p>
  Hier ist normaler Text, aber <span class="hervorhebung">dieser Teil</span> ist anders gestaltet.
</p>
```
CSS:
```css
.hervorhebung {
  color: blue;
  font-size: 1.5em; /* em ist eine relative Einheit, was flexibler ist */
  font-family: Arial, sans-serif;
}
```
Der Vorteil liegt auf der Hand: Du kannst das Aussehen aller Elemente mit der Klasse `hervorhebung` an einer einzigen Stelle in deiner CSS-Datei ändern.

**Präsentationsattribute**

Neben ganzen Elementen gab es eine Vielzahl von Attributen, die ausschließlich der visuellen Gestaltung dienten. Dazu gehören:

*   `bgcolor`: Legte die Hintergrundfarbe eines Elements fest.
*   `color`: Legte die Textfarbe fest (z. B. im `<body>`-Tag).
*   `align`: Richtete Inhalt horizontal aus (z. B. in `<p align="center">`).
*   `width` und `height`: Wurden oft direkt an Tabellenzellen oder anderen Elementen verwendet, um Layouts zu erzwingen.
*   `border`: Legte einen Rahmen um ein Element fest (z. B. `<table border="1">`).

*Veraltetes Beispiel:*
```html
<body bgcolor="#f0f0f0" text="black">
  <p align="center">
    Dies ist ein zentrierter Absatz auf einem grauen Hintergrund.
  </p>
  <table width="100%" border="1">
    <!-- ... Tabelleninhalt ... -->
  </table>
</body>
```
*Moderner, korrekter Ansatz:*

HTML:
```html
<body>
  <p class="zentriert">
    Dies ist ein zentrierter Absatz.
  </p>
  <table>
    <!-- ... Tabelleninhalt ... -->
  </table>
</body>
```
CSS:
```css
body {
  background-color: #f0f0f0;
  color: black;
}

.zentriert {
  text-align: center;
}

table {
  width: 100%;
  border: 1px solid #ccc;
}
```

**Das `<center>`-Element**

Ein weiteres klares Beispiel ist das `<center>`-Element. Seine einzige Aufgabe war es, den gesamten Inhalt, der sich darin befand, horizontal zu zentrieren.

*Veraltetes Beispiel:*
```html
<center>
  <h1>Willkommen auf meiner Webseite!</h1>
  <p>Schön, dass du da bist.</p>
</center>
```
*Moderner, korrekter Ansatz:*
Wir verwenden einen Container, zum Beispiel ein `<div>` oder, wenn es der Hauptbereich der Seite ist, ein `<main>`-Element, und weisen ihm per CSS die Zentrierung zu.

HTML:
```html
<div class="container-zentriert">
  <h1>Willkommen auf meiner Webseite!</h1>
  <p>Schön, dass du da bist.</p>
</div>
```
CSS:
```css
.container-zentriert {
  text-align: center;
}
```

#### Die semantische Neuausrichtung von `<b>` und `<i>`

Jetzt wird es ein wenig subtiler. Die Elemente `<b>` (für „bold“, also fett) und `<i>` (für „italic“, also kursiv) sind nicht veraltet. Ihre Bedeutung hat sich jedoch grundlegend geändert. Früher waren sie rein präsentationsbezogen. Heute haben sie eine semantische Bedeutung, die zufällig oft mit einer fetten oder kursiven Darstellung einhergeht.

*   `<b>`: Das „Bring Attention To“-Element. Es wird verwendet, um auf Wörter oder Sätze aufmerksam zu machen, ohne ihnen eine besondere Wichtigkeit oder Betonung zu verleihen. Typische Beispiele sind Schlüsselwörter in einem Text, Produktnamen in einer Rezension oder der erste Satz eines Artikels.
*   `<i>`: Das „Idiomatic Text“-Element. Es kennzeichnet Text, der sich stilistisch vom umgebenden Text unterscheidet. Beispiele sind Fachbegriffe, fremdsprachige Wörter (z.B. der lateinische Name einer Pflanzenart), Gedanken einer Figur in einer Geschichte oder ein Schiffname.

Wenn du Text als **wichtig** oder **betont** auszeichnen möchtest, solltest du stattdessen die dafür vorgesehenen semantischen Elemente verwenden:

*   `<strong>`: Kennzeichnet Inhalt von großer Wichtigkeit, Ernsthaftigkeit oder Dringlichkeit. Browser stellen dies standardmäßig fett dar, aber ein Screenreader kann es auch mit einer anderen Betonung vorlesen.
*   `<em>` (für „Emphasis“): Kennzeichnet eine Betonung, die die Bedeutung eines Satzes verändert. Browser stellen dies standardmäßig kursiv dar.

*Beispiel für korrekte semantische Verwendung:*
```html
<p>
  Das wohl bekannteste Werk von Van Gogh ist <i>Die Sternennacht</i>.
  Es ist <strong>extrem wichtig</strong>, die Anweisungen genau zu befolgen.
  Du musst den <b>Reset-Knopf</b> drücken, <em>nicht</em> den Power-Knopf.
</p>
```
Hier siehst du, dass die Wahl des Tags von der Absicht abhängt, nicht vom gewünschten Aussehen. Wenn du einfach nur einen Textabschnitt aus rein ästhetischen Gründen fett formatieren willst, ohne dass er eine besondere semantische Bedeutung hat, dann ist die korrekte Methode, ihm eine Klasse zu geben und dies über CSS zu steuern.

HTML:
```html
<p>
  In unserem Logo ist der <span class="logo-text-fett">Markenname</span> besonders hervorgehoben.
</p>
```
CSS:
```css
.logo-text-fett {
  font-weight: bold;
}
```

#### Inline-Styles: Die moderne Versuchung

Auch wenn die alten Tags und Attribute weitgehend verschwunden sind, gibt es eine moderne Methode, Präsentation und Struktur zu vermischen: das `style`-Attribut.

```html
<p style="color: red; font-size: 20px; background-color: yellow;">
  Dieser Text ist ein Beispiel für schlechte Praxis.
</p>
```

Obwohl dies technisch funktioniert, widerspricht es dem Prinzip der Trennung der Verantwortlichkeiten genauso stark wie die alten Methoden.

*   **Spezifität:** Inline-Styles haben eine sehr hohe Spezifität und sind daher schwer mit externem CSS zu überschreiben. Das führt oft zu Frustration bei der Fehlersuche.
*   **Wartbarkeit:** Genau wie beim `<font>`-Tag musst du jede einzelne HTML-Datei bearbeiten, um eine Designänderung vorzunehmen.
*   **Keine Wiederverwendbarkeit:** Du kannst diesen Stil nicht einfach auf einen anderen Absatz anwenden, ohne den gesamten Code zu kopieren und einzufügen. Eine CSS-Klasse hingegen kannst du beliebig oft wiederverwenden.

Inline-Styles haben nur sehr wenige legitime Anwendungsfälle, zum Beispiel wenn Stile dynamisch mit JavaScript generiert werden müssen (z.B. die Position eines sich bewegenden Elements). Für statische Webseiten solltest du sie konsequent vermeiden.

#### Warum diese Trennung so entscheidend ist

Die konsequente Trennung von HTML und CSS ist keine akademische Spitzfindigkeit. Sie bringt handfeste, praktische Vorteile mit sich, die deine Arbeit als Entwickler einfacher und deine Webseiten besser machen.

1.  **Wartbarkeit:** Eine Designänderung (z.B. ein neues Farbschema für die Marke) erfordert nur die Anpassung einiger CSS-Dateien, nicht von hunderten von HTML-Dateien.
2.  **Flexibilität:** Du kannst für dieselbe HTML-Struktur völlig unterschiedliche Designs erstellen, indem du einfach das Stylesheet austauschst. Ein klassisches Beispiel ist ein alternatives „Dark Mode“-Stylesheet oder ein spezielles Stylesheet für den Druck (`media="print"`), das Navigation und Werbung ausblendet.
3.  **Barrierefreiheit (Accessibility):** Screenreader und andere Hilfstechnologien verlassen sich auf eine saubere, semantische HTML-Struktur, um den Inhalt zu interpretieren. Präsentations-Tags wie `<center>` oder eine übermäßige Nutzung von `<b>` statt `<strong>` erzeugen „Lärm“ und machen es für Nutzer mit Einschränkungen schwerer, die Seite zu verstehen.
4.  **SEO (Suchmaschinenoptimierung):** Suchmaschinen wie Google analysieren die semantische Struktur deiner Seite, um deren Inhalt zu verstehen. Korrekt verwendete Überschriften (`<h1>`, `<h2>`, ...), `<strong>`-Tags und andere semantische Elemente helfen der Suchmaschine, die Hierarchie und die wichtigen Teile deines Inhalts zu erkennen, was sich positiv auf dein Ranking auswirken kann.

Indem du dein HTML frei von jeglicher Präsentation hältst, schreibst du nicht nur sauberen und professionellen Code. Du baust ein robustes, flexibles und zukunftssicheres Fundament für deine Webprojekte. Dein HTML beschreibt, *was* der Inhalt ist, und dein CSS kümmert sich darum, *wie* er aussieht. Halte diese beiden Welten getrennt, und du wirst auf lange Sicht ein viel glücklicherer und effizienterer Entwickler sein.
