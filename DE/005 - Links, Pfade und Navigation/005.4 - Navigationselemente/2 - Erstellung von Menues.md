# Erstellung von Menüs

### Die Erstellung von Menüs: Das Rückgrat der Seitennavigation

Eine Website ohne Navigation ist wie eine Stadt ohne Straßenschilder – ein Labyrinth, in dem sich deine Besucher schnell verloren fühlen. Die Navigation, meist in Form eines Menüs, ist das zentrale Steuerelement, das den Nutzern den Weg zu den verschiedenen Bereichen deiner Seite weist. In diesem Kapitel schauen wir uns an, wie du semantisch korrekte und funktionale Navigationsmenüs mit HTML erstellst. Das visuelle Design überlassen wir dabei vorerst CSS; unser Fokus liegt auf der soliden, sauberen Struktur.

#### Die semantische Grundlage: Listen als Basis

Auf den ersten Blick könnte man denken, ein Menü sei einfach nur eine Ansammlung von Links. Man könnte sie also einfach hintereinander in den Code schreiben:

```html
<a href="/startseite.html">Startseite</a>
<a href="/ueber-uns.html">Über uns</a>
<a href="/produkte.html">Produkte</a>
<a href="/kontakt.html">Kontakt</a>
```

Technisch gesehen würde das sogar funktionieren. Die Links wären klickbar und würden zu den entsprechenden Seiten führen. Aber aus semantischer Sicht ist dieser Ansatz mangelhaft. Ein Menü ist nicht nur eine lose Sammlung, sondern eine *Liste* von Navigationspunkten. Und genau dafür hat HTML das passende Werkzeug: Listen.

Für Navigationsmenüs verwenden wir in der Regel eine ungeordnete Liste (`<ul>`), da die Reihenfolge der Menüpunkte meist keine numerische Hierarchie darstellt. Jeder Menüpunkt wird zu einem Listeneintrag (`<li>`), der wiederum den eigentlichen Link (`<a>`) enthält.

So sieht die korrekte Grundstruktur für ein Menü aus:

```html
<ul>
  <li><a href="/startseite.html">Startseite</a></li>
  <li><a href="/ueber-uns.html">Über uns</a></li>
  <li><a href="/produkte.html">Produkte</a></li>
  <li><a href="/kontakt.html">Kontakt</a></li>
</ul>
```

Warum dieser Mehraufwand?
1.  **Semantik und Bedeutung:** Du teilst dem Browser und anderen Maschinen (wie Suchmaschinen-Crawlern oder Screenreadern) mit, dass diese Links zusammengehören und eine logische Gruppe in Form einer Liste bilden.
2.  **Barrierefreiheit:** Screenreader für sehbehinderte Nutzer erkennen diese Struktur als Liste. Sie können dem Nutzer ansagen: "Navigation, Liste mit vier Einträgen. Eintrag eins: Link 'Startseite'. Eintrag zwei: Link 'Über uns'..." Das ist unendlich viel hilfreicher als nur eine Aneinanderreihung von Links vorzulesen.
3.  **Styling mit CSS:** Eine Listenstruktur ist mit CSS wesentlich einfacher und flexibler zu gestalten. Du kannst das `<ul>`-Element als Container für das gesamte Menü und die `<li>`-Elemente für die einzelnen Menüpunkte gezielt ansprechen.

#### Das `<nav>`-Element: Ein Zuhause für die Navigation

Um die Semantik noch weiter zu verbessern, hat HTML5 das `<nav>`-Element eingeführt. Dieses Element ist ein sogenanntes "Sectioning Element" und dient dazu, einen Block von Navigationslinks zu umschließen. Es signalisiert unmissverständlich: "Alles, was sich hier drin befindet, ist ein primärer Navigationsbereich der Seite."

Unsere Liste von vorhin wird also in ein `<nav>`-Element eingehüllt:

```html
<nav>
  <ul>
    <li><a href="/startseite.html">Startseite</a></li>
    <li><a href="/ueber-uns.html">Über uns</a></li>
    <li><a href="/produkte.html">Produkte</a></li>
    <li><a href="/kontakt.html">Kontakt</a></li>
  </ul>
</nav>
```

Das `<nav>`-Element verändert für sich allein genommen nichts am Aussehen deiner Seite. Seine Aufgabe ist rein struktureller und semantischer Natur. Eine Webseite kann mehrere `<nav>`-Elemente enthalten, zum Beispiel für die Hauptnavigation im Header, eine Brotkrümel-Navigation (Breadcrumbs) unterhalb des Headers oder eine zusätzliche Linksammlung im Footer. Es sollte jedoch nur für die wirklich wichtigen, globalen Navigationsbereiche verwendet werden, nicht für jede beliebige Gruppe von Links.

#### Strukturierung von Untermenüs (Dropdowns)

Selten bestehen Websites nur aus einer einzigen Ebene. Oft gibt es Unterseiten, die in der Navigation als Untermenü oder Dropdown-Menü dargestellt werden. Die logische und semantisch korrekte Art, dies in HTML abzubilden, ist die Verschachtelung von Listen.

Wenn ein Menüpunkt, zum Beispiel "Produkte", weitere Unterpunkte wie "Laptops", "Smartphones" und "Zubehör" hat, fügst du einfach eine weitere `<ul>` in das `<li>`-Element des übergeordneten Punktes ein.

Schau dir die Struktur genau an:

```html
<nav>
  <ul>
    <li><a href="/startseite.html">Startseite</a></li>
    <li><a href="/ueber-uns.html">Über uns</a></li>
    <li>
      <a href="/produkte.html">Produkte</a>
      <ul>
        <li><a href="/produkte/laptops.html">Laptops</a></li>
        <li><a href="/produkte/smartphones.html">Smartphones</a></li>
        <li><a href="/produkte/zubehoer.html">Zubehör</a></li>
      </ul>
    </li>
    <li><a href="/kontakt.html">Kontakt</a></li>
  </ul>
</nav>
```

Das ist der entscheidende Punkt: Die verschachtelte Liste (`<ul>`) ist ein direktes Kindelement des `<li>`-Elements, nicht des `<a>`-Elements. Der Listeneintrag "Produkte" enthält also zwei Dinge: den Link zur Hauptseite der Produkte und die Liste mit den Links zu den Unterkategorien.

Diese saubere HTML-Struktur ist die perfekte Grundlage. Das Ein- und Ausblenden des Untermenüs bei einem Mausklick oder beim Überfahren mit der Maus (Hover) wird später ausschließlich mit CSS und/oder JavaScript realisiert. HTML liefert nur das stabile und logische Gerüst.

#### Styling-Grundlagen mit CSS – Vom Gerüst zum Design

Ohne CSS sieht unsere Navigation einfach wie eine normale Liste mit Aufzählungszeichen aus. Das ist nicht das, was wir uns unter einem Menü vorstellen. Lass uns einen kurzen Ausblick darauf werfen, wie CSS diese Struktur in ein ansprechendes, horizontales Menü verwandelt.

Nehmen wir unsere einfache Navigation ohne Untermenü:

**HTML:**
```html
<nav class="main-nav">
  <ul>
    <li><a href="/startseite.html">Startseite</a></li>
    <li><a href="/ueber-uns.html">Über uns</a></li>
    <li><a href="/produkte.html">Produkte</a></li>
    <li><a href="/kontakt.html">Kontakt</a></li>
  </ul>
</nav>
```

**CSS:**
```css
/* Grundlegende Zurücksetzungen für das Menü */
.main-nav ul {
  list-style-type: none; /* Entfernt die Aufzählungszeichen (Punkte) */
  margin: 0;
  padding: 0;
  background-color: #333; /* Dunkler Hintergrund für das Menü */
  overflow: hidden; /* Ein einfacher Trick, um den Hintergrund zu enthalten */
}

/* Die einzelnen Menüpunkte anordnen */
.main-nav li {
  float: left; /* Lässt die Listenelemente nebeneinander schweben */
}

/* Das Aussehen der Links gestalten */
.main-nav li a {
  display: block; /* Macht den gesamten Bereich klickbar, nicht nur den Text */
  color: white; /* Weiße Schriftfarbe */
  text-align: center;
  padding: 14px 16px; /* Innenabstand für mehr Fläche */
  text-decoration: none; /* Entfernt die Unterstreichung */
}

/* Visuelles Feedback beim Überfahren mit der Maus */
.main-nav li a:hover {
  background-color: #111; /* Dunklerer Hintergrund bei Hover */
}
```

Mit diesen wenigen CSS-Regeln verwandelt sich unsere simple HTML-Liste in ein klassisches, horizontales Navigationsmenü. Dies unterstreicht das Prinzip der Trennung von Belangen: HTML ist für die Struktur und Bedeutung zuständig, CSS für die Präsentation und das Aussehen. Moderne Ansätze würden hier vielleicht Flexbox oder Grid anstelle von `float` verwenden, aber das Grundprinzip bleibt dasselbe.

#### Barrierefreiheit im Blick: Die aktive Seite markieren

Ein kleines, aber wichtiges Detail für eine gute Benutzererfahrung und Barrierefreiheit ist die Kennzeichnung des aktuell aktiven Menüpunkts. Besucher sollten auf einen Blick erkennen können, auf welcher Seite sie sich gerade befinden.

Visuell wird dies oft durch eine andere Hintergrundfarbe, eine fette Schrift oder einen kleinen Rand erreicht. Dies kannst du mit einer CSS-Klasse, z.B. `.active`, umsetzen.

Für Screenreader gibt es zusätzlich das ARIA-Attribut (Accessible Rich Internet Applications) `aria-current="page"`. Dieses Attribut teilst dem Screenreader explizit mit, dass dieser Link zur aktuell angezeigten Seite führt.

Wenn der Besucher sich also auf der "Über uns"-Seite befindet, würde der HTML-Code so aussehen:

```html
<nav>
  <ul>
    <li><a href="/startseite.html">Startseite</a></li>
    <li><a href="/ueber-uns.html" class="active" aria-current="page">Über uns</a></li>
    <li><a href="/produkte.html">Produkte</a></li>
    <li><a href="/kontakt.html">Kontakt</a></li>
  </ul>
</nav>
```

Die Klasse `.active` wird dann im CSS verwendet, um das besondere Aussehen zu definieren, während `aria-current="page"` die Barrierefreiheit für assistierende Technologien sicherstellt.

Die Erstellung von Menüs ist ein perfektes Beispiel dafür, wie wichtig sauberes, semantisches HTML ist. Eine gut durchdachte Struktur aus `<nav>`, `<ul>` und `<li>` ist nicht nur professionell und wartbar, sondern bildet auch die unverzichtbare Grundlage für ansprechendes Design, Funktionalität und eine inklusive, barrierefreie Website.
