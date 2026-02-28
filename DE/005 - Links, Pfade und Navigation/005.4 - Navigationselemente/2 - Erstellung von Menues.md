# Erstellung von Menüs

### Erstellung von Menüs

Wenn du eine Website besuchst, ist eines der ersten Elemente, mit denen du interagierst, wahrscheinlich die Navigation. Sie ist der Wegweiser deiner digitalen Welt, der Kompass, der deine Besucher von einer Seite zur nächsten führt. Ein gut strukturiertes Menü ist daher nicht nur eine Ansammlung von Links, sondern das Rückgrat der Benutzerführung. In diesem Kapitel tauchen wir tief in die Erstellung von semantisch korrekten und funktionalen Navigationsmenüs ein.

#### Das Fundament: Eine Liste von Links

Was ist ein Menü im Grunde genommen? Es ist eine Liste von Navigationspunkten. Genau aus diesem Grund ist das semantisch korrekteste HTML-Element für den Aufbau eines Menüs eine Liste. In den meisten Fällen verwenden wir eine ungeordnete Liste (`<ul>`), da die Reihenfolge der Hauptnavigationspunkte in der Regel keine hierarchische oder nummerische Bedeutung hat. Jeder Menüpunkt wird dann zu einem Listenelement (`<li>`), das wiederum den eigentlichen Link (`<a>`) enthält.

Stell dir eine einfache Navigation für eine persönliche Webseite vor. Sie könnte Links zu "Home", "Über mich", "Projekte" und "Kontakt" enthalten. Die grundlegende HTML-Struktur dafür würde so aussehen:

```html
<ul>
  <li><a href="/index.html">Home</a></li>
  <li><a href="/ueber-mich.html">Über mich</a></li>
  <li><a href="/projekte.html">Projekte</a></li>
  <li><a href="/kontakt.html">Kontakt</a></li>
</ul>
```

Ohne jegliches Styling wird der Browser dies als eine einfache Liste mit Aufzählungszeichen darstellen. Das sieht noch nicht nach einer schicken Navigationsleiste aus, aber die Struktur ist perfekt. Sie ist logisch, semantisch korrekt und für Maschinen wie Suchmaschinen-Crawler oder Screenreader für Menschen mit Sehbehinderung sofort verständlich.

#### Das `<nav>`-Element: Ein klares Signal senden

Um die semantische Bedeutung unserer Navigation noch weiter zu verstärken, hat HTML5 das `<nav>`-Element eingeführt. Dieses Element dient als Container für die primären Navigationsblöcke einer Seite. Wenn du deine Liste von Links mit `<nav>` umschließt, signalisierst du dem Browser und assistiven Technologien unmissverständlich: "Achtung, hier beginnt ein wichtiger Navigationsbereich."

Unsere Struktur erweitert sich also wie folgt:

```html
<nav>
  <ul>
    <li><a href="/index.html">Home</a></li>
    <li><a href="/ueber-mich.html">Über mich</a></li>
    <li><a href="/projekte.html">Projekte</a></li>
    <li><a href="/kontakt.html">Kontakt</a></li>
  </ul>
</nav>
```

Eine Webseite kann durchaus mehrere `<nav>`-Elemente enthalten. Du könntest zum Beispiel eine Hauptnavigation im Kopfbereich der Seite haben und eine weitere, sekundäre Navigation mit Links zu Impressum und Datenschutz im Fußbereich. Das `<nav>`-Element sollte jedoch für die wichtigsten Navigationsgruppen reserviert sein, nicht für jede einzelne Ansammlung von Links.

#### Vom Listenpunkt zur Navigationsleiste: Die Magie von CSS

Die korrekte HTML-Struktur ist die eine Hälfte der Miete. Die andere ist das visuelle Erscheinungsbild, das wir mit CSS (Cascading Style Sheets) steuern. Lass uns unsere schmucklose Liste Schritt für Schritt in eine ansprechende, horizontale Navigationsleiste verwandeln.

**1. Grundlegende Anpassungen: Aufzählungszeichen und Abstände entfernen**

Zuerst stören uns die Aufzählungszeichen und die Standardabstände (Einrückungen), die der Browser für Listen vorsieht. Diese entfernen wir.

```css
/* Ziel ist das nav-Element und die darin enthaltene ul */
nav ul {
  list-style-type: none; /* Entfernt die Aufzählungszeichen */
  margin: 0;             /* Entfernt den äußeren Abstand */
  padding: 0;            /* Entfernt den inneren Abstand (Einrückung) */
}
```

**2. Horizontale Ausrichtung: Die Listenelemente nebeneinander anordnen**

Jetzt kommt der entscheidende Schritt. Wir müssen die Listenelemente (`<li>`), die standardmäßig untereinander (als Block-Elemente) dargestellt werden, dazu bringen, sich nebeneinander aufzureihen. Eine moderne und flexible Methode hierfür ist die Verwendung von Flexbox. Wir machen den `<ul>`-Container zu einem Flex-Container.

```css
nav ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  display: flex; /* Macht die ul zum Flex-Container */
}
```

Allein durch `display: flex;` werden die Kind-Elemente (unsere `<li>`) automatisch nebeneinander platziert.

**3. Styling der Links: Lesbarkeit und Interaktion**

Nun kümmern wir uns um die Links (`<a>`) selbst. Wir möchten die Unterstreichung entfernen, ihnen etwas "Luft" zum Atmen geben (durch Innenabstand, `padding`) und die Farbe anpassen.

```css
/* Wir zielen auf alle a-Tags innerhalb unserer nav */
nav a {
  display: block; /* Wichtig, damit padding korrekt angewendet wird */
  padding: 15px 20px; /* 15px oben/unten, 20px links/rechts */
  text-decoration: none; /* Entfernt die Unterstreichung */
  color: #333; /* Eine dunkle Textfarbe */
  font-family: Arial, sans-serif; /* Eine saubere Schriftart */
}

/* Ein kleiner Effekt, wenn man mit der Maus darüber fährt (Hover-Effekt) */
nav a:hover {
  background-color: #f4f4f4; /* Eine leichte Hintergrundfarbe beim Hover */
  color: #007bff; /* Ändert die Textfarbe beim Hover */
}
```

Wenn du diese CSS-Regeln auf dein HTML anwendest, hast du bereits eine saubere, funktionale und horizontale Navigationsleiste erstellt.

#### Hierarchien schaffen: Dropdown-Menüs

Oft reicht eine einzige Ebene in der Navigation nicht aus. Unter dem Punkt "Projekte" möchtest du vielleicht Unterpunkte wie "Webentwicklung", "Grafikdesign" und "Fotografie" anbieten. Dies realisieren wir mit verschachtelten Listen.

Die HTML-Struktur dafür ist denkbar logisch: Ein Untermenü ist einfach eine weitere `<ul>`, die *innerhalb* des `<li>`-Elements des übergeordneten Menüpunkts platziert wird.

```html
<nav>
  <ul>
    <li><a href="/index.html">Home</a></li>
    <li><a href="/ueber-mich.html">Über mich</a></li>
    <li>
      <a href="/projekte.html">Projekte</a>
      <!-- Hier beginnt das Untermenü -->
      <ul>
        <li><a href="/projekte/web.html">Webentwicklung</a></li>
        <li><a href="/projekte/design.html">Grafikdesign</a></li>
        <li><a href="/projekte/foto.html">Fotografie</a></li>
      </ul>
      <!-- Hier endet das Untermenü -->
    </li>
    <li><a href="/kontakt.html">Kontakt</a></li>
  </ul>
</nav>
```

Mit CSS steuern wir nun die Sichtbarkeit. Das Untermenü soll standardmäßig verborgen sein und nur erscheinen, wenn der Benutzer mit der Maus über den übergeordneten Punkt "Projekte" fährt.

Dafür benötigen wir das Konzept der Positionierung. Das Elternelement (`<li>`) erhält `position: relative;`, damit sich das Kindelement (die verschachtelte `<ul>`) daran orientieren kann. Das Untermenü selbst bekommt `position: absolute;`, damit es aus dem normalen Dokumentenfluss herausgenommen wird und über dem restlichen Inhalt schweben kann, ohne diesen zu verschieben.

```css
/* Das Elternelement für das Dropdown */
nav li {
  position: relative; /* Notwendig für die Positionierung des Untermenüs */
}

/* Das Untermenü standardmäßig verstecken */
nav ul ul {
  display: none;
  position: absolute; /* Aus dem Fluss nehmen und positionieren */
  top: 100%; /* Direkt unter dem Elternelement starten */
  left: 0;
  background-color: white; /* Hintergrund, damit es nicht durchsichtig ist */
  box-shadow: 0 2px 5px rgba(0,0,0,0.1); /* Ein dezenter Schatten */
  min-width: 200px; /* Mindestbreite für die Unterpunkte */
}

/* Das Untermenü anzeigen, wenn über das Elternelement gehovert wird */
nav li:hover > ul {
  display: block; /* Macht das Untermenü sichtbar */
}

/* Styling für die Links im Untermenü */
nav ul ul li {
  /* Da das übergeordnete ul ein Flex-Container ist, müssen wir hier die Block-Anordnung wiederherstellen */
  display: block;
}

nav ul ul a {
  /* Etwas angepasstes Styling für Dropdown-Links */
  padding: 10px 15px;
}
```

Mit dieser Kombination aus verschachteltem HTML und gezieltem CSS hast du ein voll funktionsfähiges Dropdown-Menü erstellt.

#### Ein Blick auf Barrierefreiheit und mobile Geräte

Ein reines Hover-Menü ist für Benutzer, die keine Maus verwenden können (z. B. Tastaturbenutzer oder Nutzer von Touch-Geräten), problematisch. Eine vollständig barrierefreie Navigation erfordert oft etwas JavaScript, um Klick-Events zu verwalten, und ARIA-Attribute (`aria-haspopup`, `aria-expanded`), um assistiven Technologien den Zustand des Menüs mitzuteilen. Dies geht über reines HTML und CSS hinaus, aber es ist wichtig, die Struktur von Anfang an so zu planen, dass sie erweiterbar ist.

Für mobile Geräte, auf denen der Platz begrenzt ist, hat sich das sogenannte "Hamburger-Menü" durchgesetzt. Dabei wird die Navigation standardmäßig hinter einem Icon (oft drei horizontale Striche, die an einen Hamburger erinnern) versteckt. Ein Klick oder Tippen auf dieses Icon klappt die Navigation aus. Auch hierfür ist die HTML-Grundstruktur eine `<nav>` mit einer Liste. Die Logik zum Ein- und Ausblenden wird dann typischerweise mit JavaScript umgesetzt, während das Layout mit Media Queries in CSS an die Bildschirmgröße angepasst wird.

Die Erstellung von Menüs ist ein perfektes Beispiel dafür, wie HTML die Struktur vorgibt und CSS das Design formt. Eine saubere, semantische HTML-Basis ist dabei immer der Ausgangspunkt für eine Navigation, die nicht nur gut aussieht, sondern auch für jeden und auf jedem Gerät zugänglich und verständlich ist.
