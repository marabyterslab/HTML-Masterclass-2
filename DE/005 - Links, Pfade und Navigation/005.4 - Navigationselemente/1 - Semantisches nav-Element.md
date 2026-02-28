# Semantisches nav-Element

### Das semantische `nav`-Element: Der Wegweiser deiner Webseite

Stell dir vor, du betrittst ein riesiges, unbekanntes Gebäude. Was ist das Erste, wonach du suchst? Wahrscheinlich nach Schildern – Wegweisern, die dir sagen, wo du die Toiletten, den Ausgang oder die Information findest. Ohne diese Orientierungspunkte wärst du verloren. Auf einer Webseite ist die Navigation genau das: der zentrale Wegweiser für deine Besucher.

Vor der Einführung von HTML5 gab es kein spezifisches Element, um diesen so wichtigen Bereich einer Seite zu kennzeichnen. Wir Entwickler behalfen uns mit generischen `div`-Containern, denen wir verräterische IDs oder Klassen gaben:

```html
<!-- Die "alte" Methode vor HTML5 -->
<div id="navigation">
  <ul>
    <li><a href="/">Startseite</a></li>
    <li><a href="/ueber-uns/">Über uns</a></li>
    <li><a href="/produkte/">Produkte</a></li>
    <li><a href="/kontakt/">Kontakt</a></li>
  </ul>
</div>
```

Das funktioniert. Ein Mensch, der den Code liest, versteht sofort, was gemeint ist. Aber für Maschinen – wie Suchmaschinen-Crawler oder assistive Technologien wie Screenreader – ist ein `div` einfach nur ein `div`. Es ist eine bedeutungslose Box. Die ID `navigation` ist nur ein Hauch von einem Hinweis, aber keine feste, maschinenlesbare Zusage.

Hier kommt das `<nav>`-Element ins Spiel. Es ist die Antwort von HTML5 auf dieses Problem und ein Eckpfeiler des semantischen Webs.

#### Was genau ist das `<nav>`-Element?

Das `<nav>`-Element ist ein semantisches HTML-Element, das speziell dafür vorgesehen ist, einen Block mit primären Navigationslinks zu umschließen. Es signalisiert dem Browser und anderen Programmen unmissverständlich: „Achtung, der Inhalt hier drin ist dazu da, um auf dieser Webseite oder zu anderen Webseiten zu navigieren.“

Wenn du also den obigen Code semantisch korrekt umschreiben würdest, sähe er so aus:

```html
<!-- Die moderne, semantische Methode mit HTML5 -->
<nav>
  <ul>
    <li><a href="/">Startseite</a></li>
    <li><a href="/ueber-uns/">Über uns</a></li>
    <li><a href="/produkte/">Produkte</a></li>
    <li><a href="/kontakt/">Kontakt</a></li>
  </ul>
</nav>
```

Auf den ersten Blick mag der Unterschied gering erscheinen. Die Funktionalität für einen sehenden Benutzer, der eine Maus benutzt, ist identisch. Die wahre Stärke liegt jedoch in der Bedeutung (der Semantik), die du dem Dokument damit verleihst.

#### Wann du `<nav>` verwenden solltest

Die goldene Regel lautet: Verwende `<nav>` für **wichtige, globale oder seiteninterne Navigationsblöcke**. Nicht jeder einzelne Link auf deiner Seite gehört in ein `<nav>`-Element. Es ist für die Hauptverkehrsadern deiner Webseite reserviert.

Typische Anwendungsfälle sind:

**1. Die Hauptnavigation der Webseite**
Dies ist der klassischste Fall. Die Menüleiste, die sich typischerweise im Header befindet und auf die wichtigsten Bereiche deiner Website verweist (Startseite, Über uns, Produkte, Blog, Kontakt), ist der perfekte Kandidat für `<nav>`.

```html
<header>
  <!-- Logo und andere Header-Inhalte hier -->
  <nav>
    <ul>
      <li><a href="/">Startseite</a></li>
      <li><a href="/blog/">Blog</a></li>
      <li><a href="/kontakt/">Kontakt</a></li>
    </ul>
  </nav>
</header>
```

**2. Ein Inhaltsverzeichnis innerhalb einer langen Seite**
Wenn du einen sehr langen Artikel oder eine Dokumentationsseite hast, kannst du ein Inhaltsverzeichnis am Anfang platzieren, das zu den einzelnen Abschnitten springt. Auch diese Sammlung von Sprunglinks ist ein primärer Navigationsblock für den Inhalt dieser speziellen Seite und sollte in `<nav>` eingeschlossen werden.

```html
<article>
  <h1>Die Geschichte des Internets</h1>
  
  <nav>
    <h2>Inhaltsverzeichnis</h2>
    <ul>
      <li><a href="#kapitel1">Kapitel 1: Die Anfänge</a></li>
      <li><a href="#kapitel2">Kapitel 2: Das World Wide Web</a></li>
      <li><a href="#kapitel3">Kapitel 3: Das moderne Web</a></li>
    </ul>
  </nav>

  <section id="kapitel1">
    <h2>Kapitel 1: Die Anfänge</h2>
    <p>... langer Text ...</p>
  </section>
  
  <section id="kapitel2">
    <h2>Kapitel 2: Das World Wide Web</h2>
    <p>... noch mehr langer Text ...</p>
  </section>

  <!-- etc. -->
</article>
```

**3. Paginierung (Seitenumbrüche)**
Eine Linkleiste am Ende einer Blog-Übersicht oder einer Produktgalerie, mit der du zur nächsten oder vorherigen Seite blättern kannst, ist ebenfalls eine Form der Navigation.

```html
<nav>
  <a href="/artikel/seite/1/">« Vorherige Seite</a>
  <a href="/artikel/seite/3/">Nächste Seite »</a>
</nav>
```

**4. Breadcrumbs (Brotkrumen-Navigation)**
Breadcrumbs zeigen dem Benutzer, wo er sich in der Hierarchie der Website befindet. Da sie ein klares Navigationsinstrument sind, ist `<nav>` hier die richtige Wahl.

```html
<nav>
  <a href="/">Startseite</a> &gt; 
  <a href="/produkte/">Produkte</a> &gt; 
  <span>Smartphones</span>
</nav>
```

#### Wann du `<nav>` *nicht* verwenden solltest

So nützlich das `<nav>`-Element auch ist, seine übermäßige Verwendung verwässert seine Bedeutung. Wenn alles als Navigation markiert ist, ist nichts mehr wirklich Navigation.

Vermeide `<nav>` in diesen Fällen:

**1. Für eine einfache Liste von Links im Footer**
Fast jede Webseite hat im Footer Links zu Impressum, Datenschutz, AGB und vielleicht einigen Social-Media-Profilen. Obwohl dies technisch gesehen Links sind, stellen sie nicht die primäre Navigation der Seite dar. Der `<footer>` selbst ist semantisch stark genug, um diese Links zu beherbergen. Ein `<nav>` wäre hier überflüssig und würde assistiven Technologien nur eine weitere, weniger wichtige „Navigation“ melden.

```html
<!-- Gut so, ohne <nav> -->
<footer>
  <p>&copy; 2023 Meine Firma</p>
  <ul>
    <li><a href="/impressum/">Impressum</a></li>
    <li><a href="/datenschutz/">Datenschutz</a></li>
  </ul>
</footer>
```

**2. Für einzelne Links im Fließtext**
Ein Link, der mitten in einem Absatz platziert ist, um auf eine andere Quelle zu verweisen, ist einfach nur ein `<a>`-Element und benötigt keinen umschließenden Container.

**3. Für eine Liste von Social-Media-Buttons**
Wenn die Buttons nur auf externe Profile verweisen und nicht das primäre Mittel zur Navigation deiner Inhalte sind, sind sie in einem einfachen `<div>` oder direkt im `<footer>` besser aufgehoben.

#### `<nav>` und die Barrierefreiheit: Ein unschlagbares Team

Der größte Gewinn durch die Verwendung von `<nav>` liegt im Bereich der Barrierefreiheit (Accessibility). Für Benutzer von Screenreadern, die sich den Inhalt einer Webseite vorlesen lassen, ist das `<nav>`-Element ein wahrer Segen.

Screenreader erkennen `<nav>` als einen sogenannten „Landmark Role“. Das bedeutet, sie können dem Benutzer direkt ankündigen: „Navigation“. Der Benutzer hat dann die Möglichkeit, direkt zu dieser Navigation zu springen, um sich schnell zu orientieren, oder sie komplett zu überspringen, um sofort zum Hauptinhalt der Seite zu gelangen. Mit einem generischen `<div>` wäre das nicht ohne Weiteres möglich.

**Was, wenn du mehrere `<nav>`-Elemente auf einer Seite hast?**

Stell dir vor, du hast eine Hauptnavigation im Header und ein seiteninternes Inhaltsverzeichnis (wie im Beispiel oben). Beide sind legitime Anwendungsfälle für `<nav>`. Für einen Screenreader-Benutzer kann dies jedoch verwirrend sein, da ihm zweimal „Navigation“ angesagt wird.

Um hier Klarheit zu schaffen, solltest du die verschiedenen `<nav>`-Elemente mit einem `aria-label`-Attribut beschriften. Dieses Attribut gibt dem Navigationsblock einen zugänglichen Namen, den der Screenreader vorlesen kann.

```html
<!-- Hauptnavigation im Header -->
<header>
  <nav aria-label="Hauptnavigation">
    <ul>
      <li><a href="/">Startseite</a></li>
      <li><a href="/blog/">Blog</a></li>
    </ul>
  </nav>
</header>

<!-- Hauptinhalt der Seite -->
<main>
  <article>
    <h1>Ein langer Artikel</h1>
    
    <!-- In-Page-Navigation -->
    <nav aria-label="Inhaltsverzeichnis des Artikels">
      <ul>
        <li><a href="#kapitel1">Zu Kapitel 1</a></li>
        <li><a href="#kapitel2">Zu Kapitel 2</a></li>
      </ul>
    </nav>
    
    <!-- ... Rest des Artikels -->
  </article>
</main>
```

Jetzt würde ein Screenreader ansagen: „Navigation, Hauptnavigation“ und „Navigation, Inhaltsverzeichnis des Artikels“. Der Benutzer weiß sofort, worum es sich bei den jeweiligen Blöcken handelt, und kann gezielt die für ihn relevante Navigation ansteuern.

#### Die innere Struktur: Listen sind deine Freunde

Rein technisch gesehen kannst du in ein `<nav>`-Element alles packen, was du möchtest. Die bewährte und semantisch korrekteste Praxis ist jedoch, die Navigationslinks in einer ungeordneten Liste (`<ul>`) zu strukturieren.

Warum? Eine Navigation ist im Grunde nichts anderes als eine Liste von Zielen. Ein `<ul>` repräsentiert eine Liste von Elementen, deren Reihenfolge nicht entscheidend ist, und `<li>` (list item) umschließt jeden einzelnen Menüpunkt. Der eigentliche Link ist dann das `<a>`-Element innerhalb des `<li>`.

Diese Struktur ist:
*   **Semantisch sauber:** Sie beschreibt exakt, was der Inhalt ist – eine Liste von Links.
*   **Leicht zu stylen:** Du kannst mit CSS gezielt das `<ul>`, die `<li>`-Elemente und die `<a>`-Tags ansprechen, um deine Navigation horizontal anzuordnen, Abstände hinzuzufügen und Hover-Effekte zu erzeugen.
*   **Maximal barrierefrei:** Screenreader verstehen Listenstrukturen sehr gut und können dem Benutzer mitteilen, wie viele Elemente sich in der Navigation befinden.

Das `<nav>`-Element ist also weit mehr als nur ein Ersatz für `<div id="nav">`. Es ist ein klares Bekenntnis zu einem strukturierteren, verständlicheren und zugänglicheren Web. Indem du es bewusst und korrekt einsetzt, baust du nicht nur Webseiten, sondern schaffst verlässliche Wegweiser im digitalen Raum – für Menschen und Maschinen gleichermaßen.
