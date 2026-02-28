# Planung der Dokumentstruktur

### Planung der Dokumentstruktur

Bevor du auch nur eine einzige Zeile Code schreibst, beginnt die Entwicklung einer Webseite im Kopf – oder besser noch, auf einem Blatt Papier oder in einem Grafikprogramm. So wie ein Architekt nicht einfach anfängt, Ziegelsteine aufeinanderzuschichten, solltest du deine Webseite nicht einfach aus `<div>`-Elementen zusammensetzen. Eine durchdachte Struktur ist das Fundament für alles, was folgt: Design, Funktionalität, Zugänglichkeit und Auffindbarkeit in Suchmaschinen. Die Planung der Dokumentstruktur ist der Prozess, bei dem du den Inhalt deiner Seite in logische Blöcke unterteilst und entscheidest, welches HTML-Element am besten geeignet ist, um jeden dieser Blöcke semantisch korrekt darzustellen.

#### Vom Konzept zum Drahtgitter (Wireframe)

Stell dir eine typische Webseite vor, zum Beispiel einen Blog. Du kannst die Seite wahrscheinlich sofort in grobe Bereiche unterteilen:

1.  **Kopfbereich (Header):** Ganz oben, meist mit dem Logo und der Hauptnavigation.
2.  **Hauptinhaltsbereich (Main Content):** Der zentrale Teil der Seite, der den einzigartigen Inhalt dieser spezifischen Seite enthält – im Falle eines Blogs wäre das der eigentliche Artikel.
3.  **Seitenleiste (Sidebar):** Oft rechts oder links vom Hauptinhalt, mit weiterführenden Informationen wie einer Liste der letzten Beiträge, Kategorien oder Werbung.
4.  **Fußbereich (Footer):** Ganz unten auf der Seite, mit Informationen wie dem Copyright, Links zum Impressum, Datenschutz und Kontakt.

Diese visuelle Aufteilung ist der erste und wichtigste Schritt. Man nennt diesen Entwurf, der sich nur auf die Anordnung und die groben Inhalte konzentriert, ein **Wireframe**. Es ist quasi der Bauplan deiner Webseite. Erst wenn dieser Plan steht, beginnst du mit der Übersetzung in HTML-Code.

#### Die Übersetzung in semantisches HTML

HTML5 hat uns eine Reihe von Elementen geschenkt, die genau dafür gemacht sind, diese logischen Bereiche einer Webseite abzubilden. Diese semantischen Layout-Elemente beschreiben die *Bedeutung* ihres Inhalts und nicht nur, wie er aussieht. Lass uns die typischen Blöcke unseres Wireframes den passenden HTML-Elementen zuordnen.

**`<header>` – Der Kopfbereich**

Das `<header>`-Element ist für den einleitenden Inhalt einer Seite oder eines Abschnitts gedacht. In der Regel findest du hier das Logo der Webseite, den Titel der Seite und die Hauptnavigation. Es ist wichtig zu verstehen, dass eine Seite mehrere `<header>`-Elemente haben kann. Der wichtigste ist der der gesamten Seite (oft direkt im `<body>`), aber auch ein Blogartikel (`<article>`) kann einen eigenen, kleineren `<header>` mit dem Titel des Artikels und dem Veröffentlichungsdatum haben.

```html
<header>
  <img src="logo.svg" alt="Mein Firmenlogo">
  <nav>
    <!-- Navigationslinks hier -->
  </nav>
</header>
```

**`<nav>` – Die Navigation**

Das `<nav>`-Element ist speziell für die Hauptnavigationsblöcke deiner Seite vorgesehen. Das umfasst typischerweise das Hauptmenü im Kopfbereich, kann aber auch für eine Inhaltsverzeichnis-Navigation innerhalb eines langen Artikels verwendet werden. Packe nicht jeden einzelnen Link auf deiner Seite in ein `<nav>`-Tag. Eine Liste von Links im Footer zum Impressum und Datenschutz benötigt zum Beispiel nicht zwingend ein `<nav>`-Element, da sie nicht die primäre Seitennavigation darstellt.

```html
<nav>
  <ul>
    <li><a href="/">Startseite</a></li>
    <li><a href="/ueber-uns.html">Über uns</a></li>
    <li><a href="/kontakt.html">Kontakt</a></li>
  </ul>
</nav>
```

**`<main>` – Der einzigartige Hauptinhalt**

Dies ist eines der wichtigsten semantischen Elemente. Das `<main>`-Tag umschließt den Hauptinhalt des Dokuments. Dieser Inhalt sollte für die jeweilige Seite einzigartig sein und nicht auf anderen Seiten wiederholt werden (wie es bei Kopf- und Fußzeilen der Fall ist). Jede Seite sollte genau **ein** `<main>`-Element haben. Suchmaschinen und assistierende Technologien (wie Screenreader für blinde Nutzer) verlassen sich auf dieses Element, um direkt zum Kern der Seite zu springen.

**`<article>` – Der in sich geschlossene Inhalt**

Ein `<article>`-Element repräsentiert einen vollständigen, in sich geschlossenen und potenziell eigenständig verteilbaren Inhalt. Klassische Beispiele sind ein Blogbeitrag, ein Forenpost, ein Zeitungsartikel oder ein einzelnes Produkt in einem Onlineshop. Wenn du den Inhalt herausnehmen und er für sich allein immer noch Sinn ergeben würde, ist `<article>` wahrscheinlich das richtige Element.

**`<section>` – Die thematische Gruppierung**

Das `<section>`-Element ist etwas allgemeiner. Es gruppiert thematisch zusammengehörige Inhalte. Eine `<section>` sollte typischerweise eine Überschrift (`<h1>` - `<h6>`) haben, die ihren Inhalt beschreibt. Der Unterschied zu `<article>` kann manchmal subtil sein. Eine gute Faustregel: Ein `<article>` ist ein eigenständiges Stück Inhalt, während eine `<section>` ein Teil eines größeren Ganzen ist. Die Startseite einer Nachrichten-Website könnte zum Beispiel mehrere `<section>`-Elemente haben: eine für "Inland", eine für "Sport" und eine für "Kultur". Jede dieser Sektionen könnte dann mehrere Teaser enthalten, die jeweils in einem `<article>`-Element gekapselt sind.

**`<aside>` – Die Seitenleiste**

Das `<aside>`-Element ist für Inhalte gedacht, die nur am Rande mit dem Hauptinhalt zu tun haben. Es ist die perfekte Wahl für die Seitenleiste (Sidebar). Inhalte in einem `<aside>` können zum Beispiel Links zu ähnlichen Artikeln, eine Autorenbiografie, Werbung oder eine Tag-Cloud sein. Der Inhalt sollte sich zwar auf die Seite beziehen, aber sein Fehlen würde den Hauptinhalt nicht unvollständig machen.

**`<footer>` – Der Fußbereich**

Ähnlich wie der `<header>` markiert der `<footer>` den Abschluss eines Bereichs. Meistens denkst du dabei an den Fußbereich der gesamten Seite mit Copyright-Informationen, Kontaktlinks und rechtlichen Hinweisen. Aber genau wie der `<header>` kann auch ein `<article>` oder eine `<section>` einen eigenen `<footer>` haben, der zum Beispiel Informationen über den Autor oder Veröffentlichungsdatum enthält.

#### Die Rolle von `<div>` und `<span>` im modernen Web

Jetzt fragst du dich vielleicht: Was ist mit dem guten alten `<div>`? Ist es überflüssig geworden? Keineswegs. Das `<div>`-Element hat einfach keine semantische Bedeutung. Es ist ein generischer Container. Du solltest es immer dann verwenden, wenn du Inhalte gruppieren musst, aber keines der oben genannten semantischen Elemente passt. Der häufigste Anwendungsfall ist die reine Gruppierung für Styling-Zwecke mit CSS oder zur Manipulation mit JavaScript. Wenn du zum Beispiel einen Container benötigst, um deinem Hauptinhalt und deiner Seitenleiste ein gemeinsames Flexbox- oder Grid-Layout zu geben, ist ein `<div>` um `<main>` und `<aside>` herum eine vollkommen legitime Wahl.

Das `<span>`-Element ist das Inline-Äquivalent zum `<div>`. Es wird verwendet, um einen kleinen Teil eines Textes oder eines anderen Inline-Inhalts zu gruppieren, ebenfalls meist für Styling oder JavaScript.

#### Ein praktisches Beispiel: Die Struktur eines Blogartikels

Lass uns all diese Elemente zusammensetzen, um die Struktur für eine typische Blogartikel-Seite zu planen.

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Der ultimative Leitfaden für semantisches HTML</title>
</head>
<body>

  <!-- Seitenweiter Header mit Logo und Hauptnavigation -->
  <header>
    <a href="/"><img src="logo.png" alt="Logo von Web-Wissen"></a>
    <nav>
      <ul>
        <li><a href="/html/">HTML</a></li>
        <li><a href="/css/">CSS</a></li>
        <li><a href="/js/">JavaScript</a></li>
      </ul>
    </nav>
  </header>

  <!-- Container für das Hauptlayout (z.B. für Flexbox/Grid) -->
  <div class="container">

    <!-- Der einzigartige Hauptinhalt der Seite -->
    <main>
      <article>
        <!-- Der Header des Artikels selbst -->
        <header>
          <h1>Der ultimative Leitfaden für semantisches HTML</h1>
          <p>Veröffentlicht am <time datetime="2023-10-27">27. Oktober 2023</time> von Alex Meier</p>
        </header>
        
        <p>Dies ist die Einleitung in unseren Artikel über die Wichtigkeit von semantischem HTML...</p>
        
        <!-- Eine thematische Sektion innerhalb des Artikels -->
        <section>
          <h2>Warum ist Semantik so wichtig?</h2>
          <p>Es gibt drei Hauptgründe: Zugänglichkeit, SEO und Wartbarkeit...</p>
        </section>
        
        <!-- Eine weitere thematische Sektion -->
        <section>
          <h2>Die wichtigsten Elemente im Überblick</h2>
          <p>Hier beschreiben wir die Elemente wie &lt;main&gt;, &lt;nav&gt; und &lt;article&gt; im Detail...</p>
        </section>
        
        <!-- Der Footer des Artikels -->
        <footer>
          <p>Kategorien: <a href="/html/">HTML</a>, <a href="/webdev/">Webentwicklung</a></p>
        </footer>
      </article>
    </main>

    <!-- Seitenleiste mit ergänzenden Informationen -->
    <aside>
      <h3>Neueste Beiträge</h3>
      <ul>
        <li><a href="#">CSS Grid verstehen</a></li>
        <li><a href="#">Einführung in JavaScript</a></li>
      </ul>
      
      <h3>Über den Autor</h3>
      <p>Alex Meier entwickelt seit über 10 Jahren Webseiten und liebt sauberen Code.</p>
    </aside>

  </div> <!-- Ende des .container -->

  <!-- Seitenweiter Footer -->
  <footer>
    <p>&copy; 2023 Web-Wissen</p>
    <nav>
      <a href="/impressum.html">Impressum</a> | 
      <a href="/datenschutz.html">Datenschutz</a>
    </nav>
  </footer>

</body>
</html>
```

In diesem Beispiel siehst du, wie die verschiedenen semantischen Elemente ineinandergreifen, um eine klare und logische Hierarchie zu schaffen. Diese Struktur ist nicht nur für dich als Entwickler leicht zu lesen, sondern auch für Maschinen. Ein Screenreader kann einem Nutzer jetzt ankündigen: "Hauptnavigation", "Hauptinhalt" oder "Seitenleiste", was die Navigation auf der Seite enorm erleichtert. Eine Suchmaschine versteht, dass der Inhalt im `<article>`-Tag der wichtigste auf dieser Seite ist. Und ein anderer Entwickler, der deinen Code in sechs Monaten übernimmt, wird dir für diese Klarheit danken.

Die Planung deiner Dokumentstruktur ist also kein optionaler Schritt, sondern eine wesentliche Disziplin für die Erstellung professioneller, robuster und zukunftssicherer Webseiten.
