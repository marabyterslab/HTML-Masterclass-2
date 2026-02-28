# Ersetzung durch CSS

# Ersetzung durch CSS: Die Trennung von Inhalt und Design

In den frühen Tagen des Webs war die Welt eine andere. HTML war nicht nur für die Struktur eines Dokuments zuständig, sondern auch für sein Aussehen. Wenn du einen Text zentrieren oder die Hintergrundfarbe einer Seite ändern wolltest, hast du das direkt im HTML-Code mit speziellen Attributen gemacht. Diese Vorgehensweise, so praktisch sie damals schien, führte schnell zu unübersichtlichem, schwer wartbarem und unflexiblem Code.

Stell dir vor, du müsstest die Farbe aller Überschriften auf einer Website mit hundert Unterseiten ändern. Mit der alten Methode müsstest du jede einzelne HTML-Datei öffnen und das `color`-Attribut in jedem `<font>`-Tag anpassen – ein Albtraum für jeden Entwickler.

Die Lösung für dieses Problem ist eines der fundamentalsten Prinzipien der modernen Webentwicklung: die **Trennung von Inhalt (Struktur) und Präsentation (Design)**. HTML soll beschreiben, *was* etwas ist – eine Überschrift, ein Absatz, eine Liste, eine Tabelle. CSS (Cascading Style Sheets) hingegen soll beschreiben, *wie* diese Elemente aussehen sollen – welche Farbe sie haben, wie groß die Schrift ist, wo sie positioniert sind.

In diesem Kapitel tauchen wir tief in die Praxis ein und sehen uns an, wie du veraltete, präsentationsbezogene HTML-Attribute durch saubere und mächtige CSS-Regeln ersetzt. Dies ist ein entscheidender Schritt beim Refactoring von altem Code und eine wesentliche Fähigkeit für das Schreiben von modernem, semantischem HTML.

### Farben und Hintergründe: Von `bgcolor` zu `background-color`

Eines der häufigsten Relikte aus der Vergangenheit ist das `bgcolor`-Attribut. Es wurde verwendet, um die Hintergrundfarbe von Elementen wie dem `<body>`, Tabellen (`<table>`) oder einzelnen Tabellenzellen (`<td>`) festzulegen.

**Altes HTML:**

```html
<body bgcolor="#f0f8ff">
  <table bgcolor="#ffffff" border="1">
    <tr>
      <td bgcolor="#dddddd">Zelle 1</td>
      <td>Zelle 2</td>
    </tr>
  </table>
</body>
```

Dieser Code vermischt die Dokumentenstruktur direkt mit Designanweisungen. Wenn du die Hintergrundfarbe der gesamten Seite ändern möchtest, musst du das `<body>`-Tag anfassen.

**Moderner Ansatz mit HTML und CSS:**

Der erste Schritt ist, das HTML von diesen Stil-Attributen zu befreien. Das HTML-Dokument konzentriert sich wieder voll auf seine Aufgabe: die Struktur.

**Modernes HTML:**

```html
<body>
  <table class="data-table">
    <tr>
      <td class="highlight-cell">Zelle 1</td>
      <td>Zelle 2</td>
    </tr>
  </table>
</body>
```

Beachte, dass wir Klassen (`class`) wie `data-table` und `highlight-cell` eingeführt haben. Diese dienen als Haken oder Selektoren, an denen wir unsere CSS-Regeln aufhängen können. Das Styling selbst lagern wir in eine separate CSS-Datei oder in einen `<style>`-Block im `<head>` des Dokuments aus.

**Zugehöriges CSS:**

```css
body {
  background-color: #f0f8ff; /* Ersetzt <body bgcolor="..."> */
}

.data-table {
  background-color: #ffffff; /* Ersetzt <table bgcolor="..."> */
  border: 1px solid #cccccc; /* Ersetzt auch das border-Attribut, mehr dazu später */
}

.data-table .highlight-cell {
  background-color: #dddddd; /* Ersetzt <td bgcolor="..."> */
}
```

Der Vorteil liegt auf der Hand: Das Design ist jetzt an einem zentralen Ort. Eine Änderung der Hintergrundfarbe der hervorgehobenen Zellen erfordert nur noch eine Anpassung an einer einzigen Stelle in der CSS-Datei, egal wie viele solcher Zellen es auf deiner Website gibt.

### Ausrichtung: Das `align`-Attribut und seine CSS-Pendants

Das `align`-Attribut war allgegenwärtig. Man fand es in Absätzen (`<p>`), Überschriften (`<h1>`), `<div>`-Containern und Tabellenzellen, um Inhalte links, rechts oder zentriert auszurichten.

**Altes HTML:**

```html
<h1 align="center">Willkommen auf meiner Webseite</h1>
<p align="right">Ein kleiner Text am rechten Rand.</p>
<div align="center">
  <p>Dieser ganze Block ist zentriert.</p>
</div>
```

Auch hier gilt: Die Ausrichtung ist eine reine Design-Entscheidung und gehört nicht ins HTML. Die moderne Lösung verwendet die CSS-Eigenschaft `text-align`.

**Modernes HTML:**

```html
<h1 class="text-center">Willkommen auf meiner Webseite</h1>
<p class="text-right">Ein kleiner Text am rechten Rand.</p>
<div class="text-center">
  <p>Dieser ganze Block ist zentriert.</p>
</div>
```

**Zugehöriges CSS:**

```css
.text-center {
  text-align: center;
}

.text-right {
  text-align: right;
}

/* Du könntest auch direkt die Elemente ansprechen, wenn alle so sein sollen */
h1 {
  text-align: center;
}
```

Die Eigenschaft `text-align` wirkt sich auf den Inline-Inhalt eines Block-Elements aus. Wenn du ein Block-Element selbst (wie ein `<div>` mit einer festen Breite) innerhalb seines Elternelements zentrieren möchtest, war `align="center"` eine unsaubere Abkürzung. Der moderne Weg dafür ist `margin: auto;`.

**Beispiel für die Zentrierung eines Blocks:**

**Modernes HTML:**
```html
<div class="container">
  Ein zentrierter Container.
</div>
```

**Zugehöriges CSS:**
```css
.container {
  width: 80%; /* Ein Block-Element braucht eine feste Breite, um zentriert zu werden */
  margin-left: auto;
  margin-right: auto;
  /* Kurzform: margin: 0 auto; */
  background-color: #eee;
  padding: 20px;
}
```
Dieser Ansatz ist weitaus präziser und flexibler als das alte `align`-Attribut.

### Der schlimmste Übeltäter: Das `<font>`-Tag

Nichts schreit so laut "90er-Jahre-Web" wie das `<font>`-Tag. Es war die einzige Möglichkeit, Schriftart, -größe und -farbe für einzelne Textabschnitte zu definieren.

**Altes HTML:**

```html
<p>
  Dies ist normaler Text. <font face="Arial" size="4" color="red">Dieser Teil ist wichtig!</font> Wieder normaler Text.
</p>
```

Dieser Code ist nicht nur unschön, sondern auch semantisch leer. Das `<font>`-Tag sagt nichts über die Bedeutung des Textes aus, nur über sein Aussehen. Zudem verwendet es für die Größe (`size`) eine Skala von 1 bis 7, die absolut und unflexibel ist.

**Moderner Ansatz mit HTML und CSS:**

Im modernen HTML verwenden wir semantische Tags, um die Bedeutung des Textes hervorzuheben. Wenn der Text wichtig ist, nutzen wir `<strong>`. Wenn er einfach nur anders aussehen soll, ohne eine besondere Bedeutung zu haben, ist ein `<span>` eine gute Wahl.

**Modernes HTML:**

```html
<p>
  Dies ist normaler Text. <strong class="highlight">Dieser Teil ist wichtig!</strong> Wieder normaler Text.
</p>
```

**Zugehöriges CSS:**

```css
.highlight {
  font-family: Arial, sans-serif; /* Ersetzt face="Arial" */
  font-size: 1.2em;              /* Ersetzt size="4" auf flexible Weise */
  color: red;                    /* Ersetzt color="red" */
}
```

Durch die Verwendung von CSS-Eigenschaften wie `font-family`, `font-size` und `color` erhalten wir die volle Kontrolle. Wir können exakte Schriftgrößen in Pixeln, relativen Einheiten (`em`, `rem`) oder Prozent angeben. Die `font-family`-Eigenschaft erlaubt uns zudem, eine Liste von Ausweich-Schriftarten (Font-Stack) anzugeben, falls die erste Wahl auf dem System des Nutzers nicht verfügbar ist.

### Abmessungen, Rahmen und Abstände

Attribute wie `width`, `height`, `border`, `cellspacing`, `cellpadding` (bei Tabellen) sowie `hspace` und `vspace` (bei Bildern) waren ebenfalls weit verbreitet, um das Layout direkt im HTML zu steuern.

**Altes HTML mit einer Tabelle und einem Bild:**

```html
<table width="500" border="1" cellpadding="10" cellspacing="0">
  <!-- ... Tabelleninhalt ... -->
</table>

<img src="bild.jpg" hspace="20" vspace="10" align="left">
<p>Dieser Text umfließt das Bild mit horizontalem (hspace) und vertikalem (vspace) Abstand.</p>
```

**Moderner Ansatz mit HTML und CSS:**

Das HTML wird wieder auf seine reine Struktur reduziert.

**Modernes HTML:**

```html
<table class="info-table">
  <!-- ... Tabelleninhalt ... -->
</table>

<img src="bild.jpg" class="floated-image">
<p>Dieser Text umfließt das Bild mit sauberem CSS-Abstand.</p>
```

**Zugehöriges CSS:**

```css
.info-table {
  width: 500px;
  border: 1px solid black;
  border-collapse: collapse; /* Dies ist die moderne Entsprechung für cellspacing="0" */
}

.info-table td, .info-table th {
  padding: 10px; /* Dies ersetzt cellpadding="10" */
  border: 1px solid black;
}

.floated-image {
  float: left; /* Ersetzt align="left" für das Umfließen */
  margin-top: 10px;
  margin-bottom: 10px;
  margin-right: 20px;
  /* Ersetzt hspace und vspace durch präzise margin-Werte */
}
```

Die CSS-Eigenschaften `width`, `height`, `border`, `padding` und `margin` sind die Grundbausteine des CSS Box Models. Sie geben dir eine viel granularere und konsistentere Kontrolle über das Layout als die alten HTML-Attribute. `border-collapse` ist ein schönes Beispiel dafür, wie CSS spezialisierte Probleme (wie die doppelten Rahmen in Tabellen) elegant löst.

Der Wechsel von präsentationsbezogenen HTML-Attributen zu CSS ist mehr als nur eine technische Aufräumaktion. Es ist ein fundamentaler Wandel in der Denkweise. Du beginnst, deine Dokumente inhaltlich zu strukturieren und das Design als eine separate, flexible Schicht zu betrachten, die du darüber legst. Diese Trennung macht deinen Code nicht nur sauberer und einfacher zu warten, sondern auch zugänglicher für Screenreader, performanter durch gecachte Stylesheets und unendlich viel flexibler für zukünftige Redesigns.
