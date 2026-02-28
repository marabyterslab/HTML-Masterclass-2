# Landmark-Roles (banner, main, navigation)

### Landmark-Rollen: Wegweiser für assistierende Technologien

Stell dir vor, du betrittst eine fremde Stadt ohne Stadtplan und ohne Straßenschilder. Du wüsstest nicht, wo das Rathaus, der Marktplatz oder der Bahnhof ist. Du müsstest dich mühsam von Block zu Block vorarbeiten, um die Struktur der Stadt zu verstehen. Für Nutzer von assistierenden Technologien, wie zum Beispiel Screenreadern, kann eine Webseite ohne klare Struktur genauso unübersichtlich sein.

Hier kommen die Landmark-Rollen von ARIA ins Spiel. Sie sind wie die großen, unübersehbaren Wahrzeichen einer Stadt: der Eiffelturm, das Brandenburger Tor, die Freiheitsstatue. Sie geben einer Seite eine übergeordnete, verständliche Gliederung. Ein Screenreader-Nutzer kann sich diese Landmarks ansagen lassen und direkt zu dem Bereich springen, der ihn interessiert – sei es die Hauptnavigation, der Inhalt oder der Kopfbereich der Seite. Das spart enorm viel Zeit und Mühe.

Bevor wir uns die einzelnen Rollen ansehen, gilt eine goldene Regel, die du dir für den gesamten Umgang mit ARIA merken solltest: **Verwende immer zuerst semantische HTML5-Elemente, wenn sie existieren.** ARIA ist dazu da, Lücken zu füllen, nicht um solides, natives HTML zu ersetzen. Die Entwickler von HTML5 haben die wichtigsten Landmark-Rollen bereits in Form von eigenen Elementen im Standard verankert. Du solltest ARIA-Rollen also nur dann einsetzen, wenn du aus bestimmten Gründen (zum Beispiel bei älterem Code oder durch ein Content-Management-System) gezwungen bist, unspezifische Elemente wie `<div>` zu verwenden.

In diesem Kapitel konzentrieren wir uns auf drei der fundamentalsten Landmark-Rollen: `navigation`, `banner` und `main`.

#### `role="navigation"` – Der Kompass deiner Webseite

Jede gute Webseite braucht eine Navigation. Sie ist der zentrale Wegweiser, der den Nutzern hilft, sich zurechtzufinden. Um diesen Bereich für assistierende Technologien klar als Navigation zu kennzeichnen, gibt es die Rolle `navigation`.

**Die beste Methode: Das `<nav>`-Element**

HTML5 bietet uns hierfür das perfekte semantische Element: `<nav>`. Wann immer du einen Block mit den primären Navigationslinks deiner Seite erstellst, solltest du ihn in ein `<nav>`-Element einschließen.

```html
<nav>
  <ul>
    <li><a href="/">Startseite</a></li>
    <li><a href="/ueber-uns">Über uns</a></li>
    <li><a href="/produkte">Produkte</a></li>
    <li><a href="/kontakt">Kontakt</a></li>
  </ul>
</nav>
```

Ein Browser, der dieses Element interpretiert, weiß sofort: "Aha, das hier ist ein Navigationsbereich." Assistierende Technologien geben diese Information direkt an den Nutzer weiter. Das `<nav>`-Element trägt die Rolle `navigation` sozusagen von Geburt an in sich. Du musst sie nicht extra hinzufügen.

**Der Fallback: `role="navigation"` für `<div>`s**

Manchmal hast du keine Wahl. Vielleicht arbeitest du an einem alten Projekt, das noch vor HTML5 entstanden ist, oder ein Framework generiert Code, den du nicht direkt ändern kannst. In solchen Fällen besteht die Navigation oft nur aus einem `<div>`. Dieses `<div>` hat für sich genommen keine semantische Bedeutung – es ist nur ein neutraler Container.

Hier kommt ARIA ins Spiel. Du kannst diesem `<div>` die Rolle `navigation` explizit zuweisen, um die fehlende Semantik nachzurüsten.

```html
<div role="navigation">
  <ul>
    <li><a href="/">Startseite</a></li>
    <li><a href="/ueber-uns">Über uns</a></li>
    <li><a href="/produkte">Produkte</a></li>
    <li><a href="/kontakt">Kontakt</a></li>
  </ul>
</div>
```

Das Ergebnis für den Endnutzer ist praktisch identisch. Der Screenreader wird diesen Bereich ebenfalls als "Navigation" ankündigen. Du hast die semantische Lücke erfolgreich geschlossen, ohne die Struktur zu zerstören.

**Umgang mit mehreren Navigationen**

Webseiten haben oft mehr als nur eine Navigation. Denk an eine Hauptnavigation im Kopfbereich, eine sekundäre Navigation in der Fußzeile und vielleicht eine Brotkrümelnavigation (Breadcrumbs) unterhalb des Headers. Wenn du mehrere `<nav>`-Elemente oder Blöcke mit `role="navigation"` hast, solltest du sie unterscheidbar machen. Ansonsten hört der Nutzer nur "Navigation", "Navigation", "Navigation" und weiß nicht, welche gemeint ist.

Dafür verwendest du das Attribut `aria-label`. Es gibt dem Element einen zugänglichen Namen, den der Screenreader vorlesen kann.

```html
<!-- Hauptnavigation im Header -->
<nav aria-label="Hauptnavigation">
  <ul>
    <li>...</li>
  </ul>
</nav>

...

<!-- Fußzeilennavigation im Footer -->
<nav aria-label="Fußzeilennavigation">
  <ul>
    <li><a href="/impressum">Impressum</a></li>
    <li><a href="/datenschutz">Datenschutz</a></li>
  </ul>
</nav>
```

So kann der Nutzer gezielt zur "Hauptnavigation" oder zur "Fußzeilennavigation" springen.

#### `role="banner"` – Das Aushängeschild deiner Seite

Der `banner`-Bereich ist quasi das Firmenschild deiner Webseite. Er befindet sich typischerweise ganz oben auf der Seite und enthält Elemente, die auf der gesamten Website gleich bleiben, wie das Logo, den Namen der Seite und oft auch die Hauptnavigation. Er signalisiert dem Nutzer: "Hier beginnt die Seite."

**Die beste Methode: Das `<header>`-Element**

Auch hier hat HTML5 ein passendes Element parat: `<header>`. Ein `<header>`-Element, das ein direkter Nachkomme des `<body>`-Elements ist, erhält automatisch die implizite ARIA-Rolle `banner`.

```html
<body>
  <header>
    <a href="/">
      <img src="logo.png" alt="Firmenlogo von PixelPerfekt">
    </a>
    <h1>PixelPerfekt Webdesign</h1>
    <nav aria-label="Hauptnavigation">
      <!-- ... Navigationslinks ... -->
    </nav>
  </header>
  
  <!-- ... Rest der Seite ... -->
</body>
```

Wichtig ist hier die Position: Nur ein `<header>` auf der obersten Ebene der Seitenstruktur gilt als `banner`. Du kannst `<header>`-Elemente nämlich auch innerhalb von anderen Elementen wie `<article>` oder `<section>` verwenden, um zum Beispiel den Kopfbereich eines Blogartikels zu kennzeichnen. Dort haben sie aber nicht die Rolle `banner`.

Eine grundlegende Regel für die `banner`-Rolle lautet: Es sollte pro Seite nur ein einziges Element mit dieser Rolle geben. Schließlich hat eine Stadt auch nur ein zentrales Ortsschild.

**Der Fallback: `role="banner"` für `<div>`s**

Wenn du wieder einmal mit einem `<div>` als Container für den Kopfbereich arbeiten musst, kannst du die Semantik mit ARIA nachrüsten.

```html
<div role="banner">
  <a href="/">
    <img src="logo.png" alt="Firmenlogo von PixelPerfekt">
  </a>
  <h1>PixelPerfekt Webdesign</h1>
  <nav aria-label="Hauptnavigation">
    <!-- ... Navigationslinks ... -->
  </nav>
</div>
```

Funktional ist das für den Screenreader-Nutzer gleichwertig. Er kann gezielt zum "Banner"-Bereich springen, um schnell zum Logo oder zum Seitentitel zu gelangen.

#### `role="main"` – Das Herzstück deiner Seite

Nachdem der Nutzer den Header (`banner`) und die Navigation (`navigation`) passiert hat, möchte er zum eigentlichen Inhalt – dem Grund, warum er diese spezielle Seite besucht hat. Dieser Kerninhalt wird durch die Landmark-Rolle `main` gekennzeichnet. Alles, was nicht zum Header, Footer oder zu seitenweiten Navigationselementen gehört, sondern den einzigartigen Inhalt dieser einen Seite darstellt, gehört hier hinein.

Diese Landmark ist besonders wichtig, da sie Nutzern von assistierenden Technologien ermöglicht, direkt zum Wesentlichen zu springen und wiederkehrende Blöcke wie den Header und die Navigation zu überspringen.

**Die beste Methode: Das `<main>`-Element**

HTML5 stellt uns dafür das `<main>`-Element zur Verfügung. Es ist glasklar in seiner Bedeutung und sollte den gesamten Hauptinhalt deiner Seite umschließen.

```html
<body>
  <header>
    <!-- ... Banner-Inhalt ... -->
  </header>
  
  <main>
    <h2>Die Kunst des semantischen HTML</h2>
    <p>In diesem Artikel erfährst du, warum die Wahl der richtigen HTML-Tags so entscheidend für die Zugänglichkeit und die Suchmaschinenoptimierung ist.</p>
    <article>
      <h3>Kapitel 1: Die Grundlagen</h3>
      <p>...</p>
    </article>
  </main>
  
  <footer>
    <!-- ... Fußzeilen-Inhalt ... -->
  </footer>
</body>
```

Wie beim `banner` gibt es auch hier eine strikte Regel: Eine Seite darf nur ein einziges `<main>`-Element enthalten. Der Hauptinhalt ist per Definition einzigartig.

**Der Fallback: `role="main"` für `<div>`s**

Solltest du das `<main>`-Element nicht verwenden können, greifst du auf ARIA zurück, um einem `<div>` diese wichtige Rolle zuzuweisen.

```html
<div role="main">
  <h2>Die Kunst des semantischen HTML</h2>
  <p>In diesem Artikel erfährst du, warum die Wahl der richtigen HTML-Tags so entscheidend für die Zugänglichkeit und die Suchmaschinenoptimierung ist.</p>
  <!-- ... weiterer Hauptinhalt ... -->
</div>
```

Das Ergebnis ist dasselbe: Screenreader erkennen diesen Bereich als Hauptinhalt und bieten eine Möglichkeit an, direkt dorthin zu navigieren.

Indem du diese drei fundamentalen Landmark-Rollen – entweder durch native HTML-Elemente oder als ARIA-Fallback – konsequent einsetzt, schaffst du eine robuste und verständliche Grundstruktur für deine Webseite. Du baust die wichtigsten Wegweiser auf, die es jedem Nutzer, unabhängig von seinen Fähigkeiten, ermöglichen, sich schnell und effizient auf deiner Seite zu orientieren. Es ist ein einfacher, aber unglaublich wirkungsvoller Schritt hin zu einem inklusiveren Web.
