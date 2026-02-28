# Bedeutung von h1 bis h6

### Die Hierarchie der Überschriften: Die Bedeutung von `<h1>` bis `<h6>`

Wenn du ein Buch aufschlägst oder einen Zeitungsartikel liest, ist das Erste, was dein Auge erfasst, die Struktur. Große, fette Überschriften kündigen neue Kapitel an, etwas kleinere Überschriften unterteilen diese Kapitel in Abschnitte und noch kleinere markieren spezifische Unterthemen. Diese visuelle Hierarchie hilft dir, den Inhalt schnell zu erfassen, zu überfliegen und zu verstehen, worum es geht, noch bevor du ein einziges Wort des Fließtextes gelesen hast.

Im Web funktioniert das ganz genauso, nur dass die Werkzeuge dafür die HTML-Überschriften-Tags sind: `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>` und `<h6>`. Auf den ersten Blick mag es so aussehen, als sei ihr einziger Zweck, Text in verschiedenen Größen darzustellen – von sehr groß (`<h1>`) bis sehr klein (`<h6>`). Das ist jedoch ein weit verbreitetes Missverständnis. Ihre wahre Kraft liegt nicht in der Optik, sondern in der Semantik – also in der Bedeutung, die sie dem Inhalt verleihen.

#### Die Überschrift als Gliederung deines Dokuments

Stell dir deine HTML-Seite wie ein Word-Dokument oder ein Buch vor. Jedes gut strukturierte Dokument hat eine klare Gliederung. Diese Gliederung ist nicht willkürlich; sie folgt einer logischen Ordnung. Genau diese Ordnung baust du mit den Überschriften-Tags in HTML nach.

*   **`<h1>`**: Dies ist die Hauptüberschrift deiner Seite. Sie ist vergleichbar mit dem Titel eines Buches. Pro Seite sollte es idealerweise nur eine einzige `<h1>`-Überschrift geben, denn sie fasst das zentrale Thema der gesamten Seite zusammen. Sie sagt sowohl dem Besucher als auch der Suchmaschine: "Das ist das Wichtigste, worum es hier geht."

*   **`<h2>`**: Diese Überschriften sind wie die Kapitelüberschriften in einem Buch. Sie unterteilen den Hauptinhalt, der von der `<h1>` angekündigt wurde, in die wichtigsten logischen Abschnitte.

*   **`<h3>`**: Wenn ein Kapitel (also ein `<h2>`-Abschnitt) weiter unterteilt werden muss, kommen die `<h3>`-Tags ins Spiel. Sie sind die Unterkapitel oder Sektionsüberschriften.

*   **`<h4>` bis `<h6>`**: Diese Ebenen dienen dazu, die Struktur noch feiner zu gliedern. Eine `<h4>` unterteilt einen `<h3>`-Abschnitt, eine `<h5>` eine `<h4>` und so weiter. In der Praxis wirst du `<h5>`- und `<h6>`-Tags eher selten verwenden, aber sie existieren, um auch sehr komplexe und tief verschachtelte Inhalte sauber strukturieren zu können.

Die entscheidende Regel hierbei ist: Die Hierarchie muss eingehalten werden. Du würdest in einem Buch auch kein Unter-Unterkapitel direkt nach dem Buchtitel erwarten. Genauso solltest du in HTML keine Ebenen überspringen. Es ist ein logischer Fehler, von einer `<h2>` direkt zu einer `<h4>` zu springen und die `<h3>`-Ebene auszulassen. Eine solche Lücke in der Struktur verwirrt sowohl assistierende Technologien als auch Suchmaschinen.

**Falsch – Übersprungene Ebene:**
```html
<h1>Der ultimative Guide für Zimmerpflanzen</h1>
<p>Einleitungstext...</p>
<h2>Die beliebtesten Pflanzenarten</h2>
<p>Text über beliebte Pflanzen...</p>
<h4>Pflege der Monstera Deliciosa</h4> <!-- FEHLER: h3 wurde übersprungen -->
<p>Details zur Pflege...</p>
```

**Richtig – Korrekte Hierarchie:**
```html
<h1>Der ultimative Guide für Zimmerpflanzen</h1>
<p>Einleitungstext...</p>
<h2>Die beliebtesten Pflanzenarten</h2>
<p>Text über beliebte Pflanzen...</p>
<h3>Monstera Deliciosa</h3>
<p>Details zur Pflanze...</p>
<h4>Pflege der Monstera Deliciosa</h4>
<p>Details zur Pflege...</p>
```

#### Warum die korrekte Struktur so entscheidend ist

Die Einhaltung dieser Hierarchie ist aus zwei fundamentalen Gründen von größter Bedeutung: Zugänglichkeit (Accessibility) und Suchmaschinenoptimierung (SEO).

**1. Zugänglichkeit für alle Nutzer**

Stell dir vor, du könntest eine Webseite nicht sehen. Wie würdest du ihren Inhalt erfassen? Menschen mit Sehbehinderungen nutzen sogenannte Screenreader – Programme, die den Inhalt einer Webseite vorlesen. Diese Nutzer lesen eine Seite selten von Anfang bis Ende durch. Stattdessen lassen sie sich oft zuerst eine Liste aller Überschriften vorlesen, um einen schnellen Überblick über die Struktur und die Themen der Seite zu bekommen. Das ist vergleichbar damit, wie sehende Nutzer eine Seite überfliegen und die großen Überschriften scannen.

Eine saubere Überschriften-Hierarchie (`<h1>`, `<h2>`, `<h3>`...) fungiert für einen Screenreader-Nutzer wie ein interaktives Inhaltsverzeichnis. Er kann von Überschrift zu Überschrift springen und direkt zu dem Abschnitt navigieren, der ihn interessiert. Wenn du jedoch Überschriften-Ebenen überspringst oder Tags nur wegen ihres Aussehens verwendest (`<h3>` für kleinen Text, obwohl er keine Unterüberschrift ist), zerstörst du dieses Inhaltsverzeichnis. Die Seite wird unlogisch, schwer zu navigieren und im schlimmsten Fall unbenutzbar.

**2. Verständlichkeit für Suchmaschinen (SEO)**

Suchmaschinen wie Google sind im Grunde "blinde" Nutzer. Sie sehen nicht das schicke Design deiner Webseite, sondern analysieren den HTML-Code, um den Inhalt zu verstehen und zu katalogisieren. Die Überschriften-Struktur ist dabei einer der wichtigsten Anhaltspunkte, um die Relevanz und Thematik einer Seite zu bewerten.

*   Die `<h1>`-Überschrift signalisiert das Hauptkeyword oder das primäre Thema der Seite.
*   Die `<h2>`-Überschriften teilen der Suchmaschine die Hauptunterthemen mit.
*   Die weiteren Ebenen (`<h3>`, `<h4>` etc.) geben detaillierteren Kontext und zeigen die logische Beziehung der Inhalte zueinander auf.

Eine gut strukturierte Seite ist für eine Suchmaschine leichter zu "verstehen". Sie kann den Inhalt besser einordnen und relevanteren Suchanfragen zuordnen, was sich positiv auf dein Ranking auswirken kann. Eine Seite ohne oder mit einer kaputten Überschriften-Hierarchie ist wie ein Buch ohne Inhaltsverzeichnis – der Crawler muss viel mehr Arbeit investieren, um den Zusammenhang zu erkennen.

#### Der häufigste Fehler: Styling mit den falschen Werkzeugen

Der wahrscheinlich größte Fehler, den Anfänger machen, ist die Verwechslung von Struktur und Präsentation. Du siehst eine `<h3>` und denkst: "Perfekt, diese Textgröße passt genau an diese Stelle", obwohl der Text inhaltlich gar keine Überschrift der dritten Ebene ist. Oder umgekehrt: Du brauchst eine Hauptüberschrift, aber das Standard-Aussehen der `<h1>` ist dir zu groß, also nimmst du stattdessen eine `<h2>`.

Das ist der falsche Ansatz. Die goldene Regel der Webentwicklung lautet: **HTML ist für die Struktur und Bedeutung zuständig, CSS ist für das Aussehen zuständig.**

Wenn du einen Text hast, der semantisch eine Hauptüberschrift ist, musst du ihn mit `<h1>` auszeichnen, ganz egal, wie er aussehen soll. Wenn dir die Standard-Schriftgröße oder -Farbe nicht gefällt, änderst du sie mit CSS.

**Beispiel: Eine `<h1>`-Überschrift anpassen**

Nehmen wir an, deine Hauptüberschrift soll kleiner und in einem unauffälligen Grau erscheinen. Du verwendest trotzdem das `<h1>`-Tag, weil es die wichtigste Überschrift ist. Das Aussehen steuerst du dann über CSS.

**HTML:**
```html
<h1>Mein minimalistischer Blog</h1>
```

**CSS:**
```css
h1 {
  font-size: 24px;       /* Kleinere Schriftgröße als der Browser-Standard */
  font-weight: normal;   /* Nicht mehr fett */
  color: #555;          /* Dunkelgrauer Text */
  margin-bottom: 40px;   /* Mehr Abstand nach unten */
}
```
Das Ergebnis ist eine Überschrift, die optisch genau deinen Wünschen entspricht, aber für Screenreader und Suchmaschinen immer noch die korrekte semantische Bedeutung einer Hauptüberschrift hat.

Wenn du umgekehrt einfach nur einen Textabschnitt optisch hervorheben möchtest, ohne dass er eine strukturelle Bedeutung hat, solltest du niemals ein Überschriften-Tag verwenden. Nutze stattdessen ein neutrales Element wie `<p>` oder `<span>` und weise ihm eine CSS-Klasse zu.

**Falsch – Semantischer Missbrauch:**
```html
<h3>Wichtiger Hinweis!</h3>
<p>Dieser Text ist keine Überschrift, sollte aber groß und fett sein.</p>
```

**Richtig – Trennung von Struktur und Stil:**
```html
<p class="important-notice">Wichtiger Hinweis!</p>
<p>Dieser Text wird über eine CSS-Klasse formatiert.</p>
```

**CSS dazu:**
```css
.important-notice {
  font-size: 1.5em; /* 1.5 mal so groß wie der normale Text */
  font-weight: bold;
  color: red;
}
```

Indem du diese Prinzipien verinnerlichst, schreibst du nicht nur Code, der funktioniert, sondern du erstellst robuste, zugängliche und suchmaschinenfreundliche Webseiten. Die korrekte Verwendung von `<h1>` bis `<h6>` ist kein Detail, sondern ein fundamentaler Baustein für qualitativ hochwertiges HTML.
