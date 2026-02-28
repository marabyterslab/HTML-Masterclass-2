# Neue semantische Elemente nutzen

### Neue semantische Elemente nutzen

Stell dir eine Webseite vor, die vor zehn oder fünfzehn Jahren gebaut wurde. Wenn du dir den Quellcode ansiehst, wirst du sehr wahrscheinlich ein Muster erkennen: eine Flut von `<div>`-Elementen. Du findest `<div id="header">`, `<div class="navigation">`, `<div id="main-content">`, `<div class="sidebar">` und `<div id="footer">`. Diese Struktur funktionierte und funktioniert technisch immer noch. Browser stellen sie dar, und mit CSS kannst du sie gestalten.

Das Problem dabei ist die fehlende Bedeutung, die Semantik. Ein `<div>` ist ein generischer Container ohne eigenen Sinn. Es sagt dem Browser, dem Screenreader oder der Suchmaschine nur: "Hier ist eine Box". Was in dieser Box ist – ob eine Kopfzeile, eine Navigation oder der Hauptinhalt –, muss aus den `id`- oder `class`-Attributen erraten werden. Das ist, als würdest du ein Buch schreiben, in dem jedes Strukturelement – Überschrift, Absatz, Fußnote, Zitat – einfach nur "Abschnitt" genannt wird. Du könntest es lesen, aber es wäre mühsam, die Struktur zu erfassen.

Mit HTML5 wurde dieses Problem adressiert. Anstatt uns auf generische Container zu verlassen, bekamen wir eine Reihe neuer Elemente, die genau für diese gängigen Seitenbereiche gedacht sind. Sie transportieren von Haus aus eine klare Bedeutung. Wenn du diese Elemente verwendest, wird dein Code nicht nur sauberer und lesbarer für dich und andere Entwickler, sondern er wird auch für Maschinen verständlicher.

#### Die zentralen Bausteine einer modernen Seite

Lass uns die wichtigsten neuen semantischen Elemente ansehen, die das Rückgrat fast jeder modernen Webseite bilden. Sie ersetzen die alten `<div>`-Konstrukte und geben deiner Seite eine klare, logische Struktur.

**`<header>`**

Das `<header>`-Element repräsentiert den Kopfbereich einer Seite oder eines Abschnitts. Hier findest du typischerweise das Logo, den Seitentitel, vielleicht eine Suchleiste und die Hauptnavigation. Wichtig ist, es nicht mit dem `<head>`-Element zu verwechseln. Das `<head>`-Element enthält Metadaten über das Dokument (wie den Titel, der im Browser-Tab erscheint), während der `<header>` der sichtbare Kopfbereich auf der Seite selbst ist.

Eine Seite kann mehrere `<header>`-Elemente haben. Du kannst zum Beispiel einen Haupt-Header für die gesamte Webseite und separate Header für einzelne Artikel (`<article>`) oder Abschnitte (`<section>`) haben.

```html
<body>
  <header>
    <img src="logo.png" alt="Firmenlogo">
    <h1>Meine fantastische Webseite</h1>
    <!-- Die Navigation wird oft hier platziert, aber gehört semantisch in ein <nav>-Element -->
  </header>

  <main>
    <!-- Hauptinhalt der Seite -->
  </main>
</body>
```

**`<nav>`**

Wie der Name schon sagt, ist das `<nav>`-Element für Navigationsblöcke vorgesehen. Es umschließt die primären Links, die den Benutzer durch deine Webseite oder zu wichtigen externen Seiten führen. Das können die Hauptnavigation im Header, ein Inhaltsverzeichnis oder eine Seitennavigation sein.

Nicht jede Gruppe von Links gehört in ein `<nav>`-Element. Eine Liste von Links im Footer (wie Impressum, Datenschutz) benötigt nicht zwingend ein `<nav>`. Es ist für die Hauptnavigationsblöcke reserviert.

```html
<header>
  <h1>Meine Webseite</h1>
  <nav>
    <ul>
      <li><a href="/">Startseite</a></li>
      <li><a href="/ueber-uns">Über uns</a></li>
      <li><a href="/produkte">Produkte</a></li>
      <li><a href="/kontakt">Kontakt</a></li>
    </ul>
  </nav>
</header>
```

**`<main>`**

Das `<main>`-Element ist eines der wichtigsten semantischen Tags. Es umschließt den Hauptinhalt deines Dokuments. Das ist der Inhalt, der auf dieser spezifischen Seite einzigartig ist und nicht aus wiederkehrenden Elementen wie dem Header, Footer oder einer Sidebar besteht.

Eine entscheidende Regel: Ein Dokument sollte nur **ein** `<main>`-Element enthalten. Es repräsentiert den Kern, den eigentlichen Grund, warum ein Besucher diese Seite aufgerufen hat. Für assistierende Technologien wie Screenreader ist dies ein extrem wichtiger Ankerpunkt, der es Benutzern erlaubt, direkt zum Wesentlichen zu springen.

```html
<body>
  <header>
    <!-- ... Header-Inhalt ... -->
  </header>
  
  <main>
    <h2>Willkommen auf unserer Produktseite</h2>
    <p>Hier finden Sie alle Informationen zu unserem neuesten Produkt.</p>
    <!-- ... weiterer einzigartiger Inhalt ... -->
  </main>

  <footer>
    <!-- ... Footer-Inhalt ... -->
  </footer>
</body>
```

**`<footer>`**

Der `<footer>` ist das Gegenstück zum `<header>`. Er enthält Informationen, die typischerweise am Ende einer Seite oder eines Abschnitts stehen. Dazu gehören Copyright-Hinweise, Kontaktinformationen, Links zu Impressum und Datenschutz oder sekundäre Navigationslinks. Ähnlich wie der `<header>` kann auch ein `<footer>` für die gesamte Seite oder für einzelne Sektionen wie einen `<article>` verwendet werden.

```html
<footer>
  <p>&copy; 2023 Meine fantastische Webseite</p>
  <ul>
    <li><a href="/impressum">Impressum</a></li>
    <li><a href="/datenschutz">Datenschutz</a></li>
  </ul>
</footer>
```

**`<article>` und `<section>`**

Diese beiden Elemente werden oft verwechselt, aber sie dienen unterschiedlichen Zwecken.

Ein `<article>`-Element ist für in sich geschlossene, unabhängige Inhalte gedacht. Der Inhalt sollte auch außerhalb des Kontexts der Seite Sinn ergeben, als könnte man ihn als eigenständige Einheit syndizieren (z. B. in einem RSS-Feed). Typische Beispiele sind ein Blogbeitrag, ein Forenpost, ein Nachrichtenartikel oder ein einzelnes Produkt in einer Liste.

Ein `<section>`-Element hingegen dient der thematischen Gruppierung von Inhalten. Es ist generischer als ein `<article>`. Denk an Kapitel in einem Buch. Eine `<section>` sollte fast immer eine Überschrift (`<h1>` - `<h6>`) haben, die ihr Thema benennt.

Die Beziehung ist flexibel:
*   Ein `<article>` kann in mehrere `<section>`s unterteilt sein (z. B. ein langer Blogbeitrag mit den Abschnitten "Einleitung", "Hauptteil", "Fazit").
*   Eine `<section>` kann mehrere `<article>`s enthalten (z. B. eine "Neueste Nachrichten"-Sektion, die mehrere kurze Artikel-Teaser auflistet).

```html
<!-- Beispiel für <article> mit <section>s -->
<article>
  <header>
    <h2>Die Kunst des semantischen HTML</h2>
    <p>Veröffentlicht am 15. Oktober</p>
  </header>
  
  <section>
    <h3>Warum Semantik wichtig ist</h3>
    <p>...</p>
  </section>
  
  <section>
    <h3>Die wichtigsten Elemente im Überblick</h3>
    <p>...</p>
  </section>
  
  <footer>
    <p>Tags: HTML, Webentwicklung</p>
  </footer>
</article>
```

**`<aside>`**

Das `<aside>`-Element ist für Inhalte gedacht, die nur lose mit dem Hauptinhalt der Seite in Beziehung stehen. Es ist "beiseite" gestellter Inhalt. Klassische Beispiele sind eine Sidebar mit weiterführenden Links, Werbeblöcke, Biografien des Autors oder Glossareinträge, die sich auf den Haupttext beziehen. Der Inhalt im `<aside>` kann entfernt werden, ohne dass der Hauptinhalt seinen Sinn verliert.

```html
<main>
  <article>
    <h2>Der Alpen-Murmeltier</h2>
    <p>Das Alpenmurmeltier (Marmota marmota) ist eine Tierart aus der Ordnung der Nagetiere...</p>
  </article>

  <aside>
    <h3>Verwandte Themen</h3>
    <ul>
      <li><a href="/tiere/steinadler">Der Steinadler</a></li>
      <li><a href="/regionen/alpen">Die Alpen</a></li>
    </ul>
  </aside>
</main>
```

#### Das Refactoring: Von "Div-Suppe" zu klarer Struktur

Sehen wir uns ein konkretes Beispiel an, wie du eine alte, auf `<div>`s basierende Struktur in modernes, semantisches HTML überführst.

**Vorher: Legacy-HTML mit `<div>`s**

```html
<div id="page-wrapper">
  <div id="header">
    <h1>Meine alte Webseite</h1>
    <div class="nav">
      <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">Blog</a></li>
      </ul>
    </div>
  </div>

  <div id="content">
    <div class="main-column">
      <h2>Ein Blogbeitrag</h2>
      <p>Dies ist der Text meines Blogbeitrags...</p>
    </div>
    <div class="sidebar">
      <h3>Archiv</h3>
      <ul>
        <li><a href="#">Januar 2023</a></li>
      </ul>
    </div>
  </div>

  <div id="footer">
    <p>&copy; 2023 by me.</p>
  </div>
</div>
```

Dieser Code ist funktional, aber seine Struktur ist nur durch die Namen der IDs und Klassen verständlich.

**Nachher: Modernes HTML5 mit semantischen Elementen**

```html
<body> <!-- Der page-wrapper div ist meist überflüssig -->
  <header>
    <h1>Meine moderne Webseite</h1>
    <nav>
      <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">Blog</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <h2>Ein Blogbeitrag</h2>
      <p>Dies ist der Text meines Blogbeitrags...</p>
    </article>
  </main>

  <aside>
    <h3>Archiv</h3>
    <ul>
      <li><a href="#">Januar 2023</a></li>
    </ul>
  </aside>

  <footer>
    <p>&copy; 2023 by me.</p>
  </footer>
</body>
```

Das Ergebnis ist auf den ersten Blick sehr ähnlich, aber die Vorteile sind gewaltig:

1.  **Lesbarkeit:** Der Code dokumentiert sich selbst. Jeder Entwickler, der diesen Code sieht, versteht sofort die Rolle der einzelnen Blöcke. `<header>` ist der Header, `<nav>` die Navigation. Es gibt keine Unklarheiten.
2.  **Barrierefreiheit (Accessibility):** Für einen Screenreader-Nutzer ist die zweite Version ein Segen. Die Software erkennt die semantischen Elemente als "Landmarks" (Orientierungspunkte). Der Nutzer kann Befehle geben wie "Springe zur Hauptnavigation" oder "Gehe zum Hauptinhalt" und muss sich nicht durch Dutzende von `div`-Containern kämpfen.
3.  **Suchmaschinenoptimierung (SEO):** Suchmaschinen wie Google analysieren die Struktur deiner Seite, um deren Inhalt zu verstehen. Wenn du klar signalisierst, was der Hauptinhalt (`<main>`) und was nur nebensächliche Information (`<aside>`) ist, hilfst du der Suchmaschine, deine Seite korrekt zu indizieren und zu bewerten.

#### Wann du `<div>` und `<span>` weiterhin brauchst

Bedeutet das nun, dass `<div>` und `<span>` schlecht sind und vermieden werden sollten? Auf keinen Fall. Sie haben immer noch einen wichtigen Platz. Du solltest sie immer dann verwenden, wenn es **kein passendes semantisches Element** gibt. Ihr Zweck ist die Gruppierung von Elementen für rein stilistische oder funktionale Zwecke, die keine eigene semantische Bedeutung haben.

*   **`<div>`:** Ein Block-Level-Container. Perfekt, um eine Gruppe von Elementen für ein CSS-Layout (z.B. mit Flexbox oder Grid) zu umschließen oder um einen Bereich für ein JavaScript-Widget zu definieren.
*   **`<span>`:** Ein Inline-Container. Ideal, um ein einzelnes Wort oder einen Satz innerhalb eines Absatzes zu markieren, um es anders zu formatieren (z.B. eine andere Farbe) oder mit JavaScript zu manipulieren.

Die goldene Regel lautet: Beginne mit der semantischen Struktur. Frage dich bei jedem Inhalt: Was *ist* das? Ist es ein Artikel? Eine Navigation? Nur wenn die Antwort "Es ist einfach nur eine Gruppe von Dingen, die zusammengehören" lautet, greifst du zu `<div>`.
