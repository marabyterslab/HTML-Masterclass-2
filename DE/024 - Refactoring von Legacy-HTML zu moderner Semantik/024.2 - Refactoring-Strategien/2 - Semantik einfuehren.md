# Semantik einführen

### Strategie 1: Semantik einführen – Von `<div>` zu Bedeutung

Wenn du auf älteren Code blickst, wirst du einem Muster immer wieder begegnen: einer Flut von `<div>`-Elementen. `div`-Elemente, die mit IDs wie `header`, `main-nav` oder Klassen wie `content-wrapper` und `footer-box` versehen sind. Visuell mag das Ergebnis perfekt sein. Die Seite sieht so aus, wie sie aussehen soll. Aber unter der Haube fehlt etwas Entscheidendes: Bedeutung.

Diese Art von Code ist wie ein Roman, der nur aus Absätzen besteht, ohne Überschriften, Kapitel oder Seitenzahlen. Du kannst ihn lesen, aber es ist unendlich schwer, dich darin zurechtzufinden, die Struktur zu erfassen oder schnell zu einem bestimmten Punkt zu springen. Genau hier setzt die Refactoring-Strategie an, Semantik in dein HTML einzuführen.

#### Was ist Semantik wirklich?

Semantik im Web bedeutet, dass deine HTML-Elemente nicht nur beschreiben, wie etwas *aussieht*, sondern auch, was es *ist*. Ein `<div>` ist ein generischer Container ohne eigene Bedeutung. Es ist eine leere Kiste. Ein `<header>`-Element hingegen sagt unmissverständlich: „Ich bin der Kopfbereich dieses Dokuments oder dieses Abschnitts.“ Ein `<nav>`-Element ruft: „Ich bin die Hauptnavigation!“

Diese Bedeutung ist nicht für das menschliche Auge gedacht, das die gerenderte Seite betrachtet. Sie ist für Maschinen:

1.  **Suchmaschinen (wie Google):** Sie können eine Seite mit semantischem HTML viel besser verstehen. Ein `<h1>` ist die wichtigste Überschrift, ein `<main>` enthält den Kerninhalt, und ein `<footer>` die Abschlussinformationen. Das hilft ihnen, deine Inhalte korrekt zu indizieren und zu bewerten.
2.  **Screenreader und andere assistive Technologien:** Für Menschen mit Sehbehinderungen sind semantische Elemente überlebenswichtig. Ein Screenreader kann „Navigation“ ansagen und dem Benutzer anbieten, direkt dorthin zu springen, wenn er auf ein `<nav>`-Element trifft. Bei einem `<div class="nav">` kann er nur raten.
3.  **Browser und zukünftige User-Agents:** Browser können semantische Elemente für spezielle Funktionen nutzen, wie den „Reader-Modus“, der den `<main>`-Inhalt extrahiert, um ihn ablenkungsfrei darzustellen.
4.  **Andere Entwickler (und dein zukünftiges Ich):** Semantischer Code ist selbsterklärend. Wenn du oder ein Kollege in sechs Monaten den Code öffnet, ist sofort klar, welche Aufgabe welcher Teil des Markups hat, ohne sich durch unzählige Klassen- und ID-Namen wühlen zu müssen.

Das Refactoring von nicht-semantischem zu semantischem HTML ist also kein kosmetischer Eingriff. Es ist eine grundlegende Verbesserung der Qualität, Zugänglichkeit und Zukunftsfähigkeit deines Codes.

#### Der klassische Fall: Die „Div-Suppe“

Lass uns ein typisches Beispiel für Legacy-HTML betrachten. Eine einfache Seitenstruktur, wie sie vor einem Jahrzehnt gang und gäbe war:

```html
<div id="page-wrapper">
  <div id="header">
    <img src="logo.png" alt="Firmenlogo">
    <div class="navigation">
      <ul>
        <li><a href="/">Startseite</a></li>
        <li><a href="/ueber-uns">Über uns</a></li>
        <li><a href="/kontakt">Kontakt</a></li>
      </ul>
    </div>
  </div>

  <div id="main-content">
    <div class="post">
      <div class="post-title">Willkommen auf unserer Webseite!</div>
      <div class="post-body">
        <p>Dies ist der erste Absatz unseres Hauptinhalts. Wir freuen uns, dich hier zu begrüßen.</p>
      </div>
    </div>
  </div>

  <div id="sidebar">
    <h3>Verwandte Links</h3>
    <ul>
      <li><a href="#">Link 1</a></li>
      <li><a href="#">Link 2</a></li>
    </ul>
  </div>

  <div id="footer">
    <p>&copy; 2024 Unsere Firma. Alle Rechte vorbehalten.</p>
  </div>
</div>
```

Dieser Code funktioniert. Mit dem passenden CSS wird er auch gut aussehen. Aber er ist „stumm“. Er kommuniziert keine Bedeutung. Der Browser weiß nicht, dass `#header` der Kopfbereich ist oder `#main-content` den wichtigsten Inhalt enthält.

#### Der Refactoring-Prozess: Bedeutung hinzufügen

Unsere Aufgabe ist es nun, diese `<div>`-Struktur schrittweise durch semantische HTML5-Elemente zu ersetzen.

**Schritt 1: Die Haupt-Seitenstruktur identifizieren**

Zuerst suchen wir die großen, übergeordneten Blöcke, die auf fast jeder Webseite existieren: Header, Navigation, Hauptinhalt und Footer.

-   `<div id="header">` ist eindeutig der Kopfbereich. Er wird zu `<header>`.
-   `<div class="navigation">` ist die Navigation. Sie wird zu `<nav>`.
-   `<div id="main-content">` ist der primäre Inhalt. Er wird zu `<main>`.
-   `<div id="sidebar">` ist ein seitlicher Bereich mit Zusatzinformationen. Dafür ist `<aside>` perfekt.
-   `<div id="footer">` ist der Fußbereich. Er wird zu `<footer>`.

Der erste Refactoring-Durchgang transformiert das Grundgerüst:

```html
<body> <!-- Der #page-wrapper ist oft unnötig -->
  <header>
    <img src="logo.png" alt="Firmenlogo">
    <nav>
      <ul>
        <li><a href="/">Startseite</a></li>
        <li><a href="/ueber-uns">Über uns</a></li>
        <li><a href="/kontakt">Kontakt</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <div class="post">
      <div class="post-title">Willkommen auf unserer Webseite!</div>
      <div class="post-body">
        <p>Dies ist der erste Absatz unseres Hauptinhalts. Wir freuen uns, dich hier zu begrüßen.</p>
      </div>
    </div>
  </main>

  <aside>
    <h3>Verwandte Links</h3>
    <ul>
      <li><a href="#">Link 1</a></li>
      <li><a href="#">Link 2</a></li>
    </ul>
  </aside>

  <footer>
    <p>&copy; 2024 Unsere Firma. Alle Rechte vorbehalten.</p>
  </footer>
</body>
```

**Wichtiger Hinweis zum CSS:** Wenn du diese Änderung vornimmst, wird dein Styling wahrscheinlich kaputtgehen. Das alte CSS hat auf IDs wie `#header` gezielt. Du musst deine Stylesheets ebenfalls anpassen, um die neuen Element-Selektoren (`header`, `nav`, `main` etc.) zu verwenden. Ein guter Ansatz ist, Klassen beizubehalten, wenn sie für das Styling benötigt werden, aber die strukturelle ID zu entfernen.

Vorher:
```css
#header {
  background-color: #f1f1f1;
  padding: 20px;
}
```

Nachher:
```css
header {
  background-color: #f1f1f1;
  padding: 20px;
}
```

**Schritt 2: Die Inhaltsstruktur verfeinern**

Nachdem das grobe Layout semantisch ist, blicken wir tiefer in den Inhalt, insbesondere in das `<main>`-Element. Hier finden wir die Struktur eines Beitrags, die ebenfalls nur aus `div`s besteht.

-   `<div class="post">`: Dies ist ein in sich geschlossener, eigenständiger Inhalt. Ein Blogbeitrag, ein Produkt, ein Forenpost. Das perfekte Element dafür ist `<article>`. Ein `<article>` könnte theoretisch aus dem Seitenkontext gerissen und für sich allein (z. B. in einem RSS-Feed) stehen und immer noch Sinn ergeben.
-   `<div class="post-title">`: Dies ist die Überschrift des Beitrags. Ein `<div>` ist hier falsch. Es sollte eine Überschriften-Ebene sein, typischerweise ein `<h1>` oder `<h2>`, je nach Seitenstruktur.
-   `<div class="post-body">`: Dieser Container ist nach der Umstellung auf `<article>` und eine echte Überschrift oft überflüssig. Der Inhalt kann direkt im `<article>` stehen.

Wenden wir diese Erkenntnisse an:

```html
<main>
  <article>
    <h2>Willkommen auf unserer Webseite!</h2>
    <p>Dies ist der erste Absatz unseres Hauptinhalts. Wir freuen uns, dich hier zu begrüßen.</p>
  </article>
</main>
```

**Schritt 3: Unterscheidung zwischen `<section>` und `<article>`**

Ein häufiger Punkt der Verwirrung ist der Unterschied zwischen `<section>` und `<article>`. Die Regel ist:

-   **`<article>`:** Ist für eigenständige Inhalte, die syndiziert werden könnten.
-   **`<section>`:** Gruppiert thematisch zusammengehörige Inhalte. Eine `section` ist ein Teil eines größeren Ganzen und ergibt isoliert betrachtet nicht unbedingt Sinn. Fast jede `<section>` sollte eine eigene Überschrift haben.

Stell dir vor, unsere Willkommensseite hätte mehrere Bereiche: einen über die Firma, einen über die Produkte und einen mit Kundenstimmen. Diese wären keine eigenständigen Artikel, sondern thematische Abschnitte der Startseite. Die Struktur sähe dann so aus:

```html
<main>
  <section>
    <h2>Über unsere Firma</h2>
    <p>Wir sind ein führender Anbieter von...</p>
  </section>
  <section>
    <h2>Unsere Produkte</h2>
    <p>Entdecke unser innovatives Sortiment...</p>
  </section>
  <section>
    <h2>Was unsere Kunden sagen</h2>
    <blockquote>"Ein fantastischer Service!"</blockquote>
  </section>
</main>
```
Hier siehst du auch den Einsatz von `<blockquote>` für ein Zitat – ein weiteres kleines, aber wichtiges semantisches Detail, das einem einfachen `<p>` oder `<div>` vorzuziehen ist.

#### Das Endergebnis

Vergleichen wir unseren finalen, semantischen Code mit dem ursprünglichen `div`-Konstrukt.

**Finaler Code:**
```html
<body>
  <header>
    <img src="logo.png" alt="Firmenlogo">
    <nav>
      <ul>
        <li><a href="/">Startseite</a></li>
        <li><a href="/ueber-uns">Über uns</a></li>
        <li><a href="/kontakt">Kontakt</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <h2>Willkommen auf unserer Webseite!</h2>
      <p>Dies ist der erste Absatz unseres Hauptinhalts. Wir freuen uns, dich hier zu begrüßen.</p>
    </article>
  </main>

  <aside>
    <h3>Verwandte Links</h3>
    <ul>
      <li><a href="#">Link 1</a></li>
      <li><a href="#">Link 2</a></li>
    </ul>
  </aside>

  <footer>
    <p>&copy; 2024 Unsere Firma. Alle Rechte vorbehalten.</p>
  </footer>
</body>
```

Dieser Code ist nicht nur sauberer und kürzer, sondern er trägt seine Bedeutung nach außen. Er ist für Maschinen lesbar, für assistive Technologien eine Offenbarung und für Entwickler eine Freude in der Wartung. Das Einführen von Semantik ist einer der wirkungsvollsten Schritte, die du beim Refactoring von Legacy-HTML unternehmen kannst. Du verwandelst ein stummes Layout-Gerüst in ein eloquentes, strukturiertes Dokument, das im modernen Web zu Hause ist.
