# Strukturierung des Inhalts

### Strukturierung des Inhalts

Wenn du den `<body>`-Tag als eine leere Leinwand betrachtest, dann sind die HTML-Elemente, die du darin platzierst, deine Pinselstriche und Farbtupfer. Doch ohne eine durchdachte Struktur wird aus der Leinwand schnell ein unübersichtliches Chaos. Die Kunst der Webentwicklung liegt nicht nur darin, Inhalte anzuzeigen, sondern sie so zu organisieren, dass sie für Menschen und Maschinen gleichermaßen verständlich sind. Es geht um die Semantik – die Bedeutung – deines Inhalts.

Stell dir vor, du bekommst ein Buch ohne Kapitel, ohne Überschriften und ohne Absätze; nur eine endlose Wand aus Text. Du könntest es zwar lesen, aber es wäre mühsam, den Überblick zu behalten, zu einer bestimmten Stelle zurückzukehren oder die Hauptthemen zu erfassen. Genau diese Aufgabe der Gliederung übernimmt HTML für deine Webseite. Du sagst dem Browser (und anderen Programmen wie Suchmaschinen oder Screenreadern), was ein Titel ist, was ein normaler Absatz, was eine Liste und was ein Zitat ist.

#### Bausteine der Struktur: Block- und Inline-Elemente

Um diese Struktur zu schaffen, stellt dir HTML grundlegend zwei Arten von Bausteinen zur Verfügung: Block-Elemente und Inline-Elemente. Das Verständnis dieses Konzepts ist fundamental, da es das Layout und den Fluss deiner Seite maßgeblich beeinflusst.

**Block-Elemente**
Ein Block-Element kannst du dir wie einen eigenständigen Kasten oder Baustein vorstellen. Es verhält sich nach zwei einfachen Regeln:
1.  Es beginnt immer in einer neuen Zeile.
2.  Es nimmt standardmäßig die gesamte verfügbare Breite seines Elternelements ein, egal wie viel oder wie wenig Inhalt es hat.

Typische Block-Elemente sind Überschriften (`<h1>` bis `<h6>`), Absätze (`<p>`), Listen (`<ul>`, `<ol>`), Listenelemente (`<li>`) und das allgegenwärtige `<div>`. Wenn du zwei `<p>`-Tags direkt hintereinander schreibst, werden sie im Browser nicht nebeneinander, sondern untereinander dargestellt. Jeder Absatz ist ein eigener Block.

```html
<p>Dies ist der erste Absatz. Er nimmt die gesamte Breite ein.</p>
<p>Dies ist der zweite Absatz. Er beginnt in einer neuen Zeile unter dem ersten.</p>
```

**Inline-Elemente**
Inline-Elemente verhalten sich anders. Sie sind wie Wörter oder Sätze innerhalb eines Textflusses. Sie erzeugen keinen Zeilenumbruch und nehmen nur so viel Platz ein, wie ihr Inhalt benötigt. Sie fließen einfach mit dem Text mit.

Typische Inline-Elemente sind Links (`<a>`), Hervorhebungen (`<strong>` für starke Wichtigkeit, `<em>` für Betonung), Bilder (`<img>`) und das generische `<span>`-Element. Du nutzt sie, um Teile eines Textes auszuzeichnen, ohne den Textfluss zu unterbrechen.

```html
<p>
  Innerhalb dieses Absatzes gibt es einen <a href="#">Link</a>, 
  ein <strong>wichtiges Wort</strong> und eine <em>betonte Stelle</em>. 
  Alle diese Elemente bleiben in derselben Zeile.
</p>
```

#### Vom `<div>`-Dschungel zur semantischen Klarheit

In den früheren Tagen des Webs, bevor HTML5 die Bühne betrat, war die Strukturierung komplexer Layouts oft eine eintönige Angelegenheit. Entwickler griffen fast ausschließlich zum `<div>`-Element, einem generischen Block-Container ohne jede semantische Bedeutung. Eine typische Webseite sah im Code dann so aus:

```html
<!-- Die alte Art, mit divs zu strukturieren -->
<div id="header">
  <h1>Meine Webseite</h1>
  <div class="nav">
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">Über uns</a></li>
      <li><a href="#">Kontakt</a></li>
    </ul>
  </div>
</div>

<div id="main-content">
  <div class="article">
    <h2>Titel des Artikels</h2>
    <p>Hier steht der Inhalt des Artikels...</p>
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
  <p>&copy; 2023 Meine Webseite</p>
</div>
```

Auf den ersten Blick funktioniert das. Mithilfe von IDs und Klassen (`id="header"`, `class="nav"`) können wir die Bereiche per CSS gestalten. Aber der Code selbst verrät uns nichts über die *Bedeutung* der einzelnen Bereiche. Ein `<div>` ist einfach nur ein `<div>`. Eine Suchmaschine oder ein Screenreader für sehbehinderte Nutzer weiß nicht, dass `<div id="header">` der Kopfbereich der Seite ist oder `<div class="nav">` die Hauptnavigation enthält. Sie sehen nur neutrale Boxen.

HTML5 hat genau dieses Problem adressiert und eine Reihe neuer, semantischer Elemente eingeführt, die den verschiedenen Bereichen einer Webseite eine klare Bedeutung zuweisen. Diese Elemente machen deinen Code nicht nur lesbarer und wartbarer, sondern verbessern auch die Zugänglichkeit (Accessibility) und die Suchmaschinenoptimierung (SEO) deiner Seite.

#### Die wichtigsten semantischen Strukturelemente

Werfen wir einen Blick auf die wichtigsten dieser neuen Bausteine, die das Fundament moderner Webseiten bilden.

*   **`<header>`**: Dieses Element repräsentiert den Kopfbereich einer Seite oder eines Abschnitts. Hier findest du typischerweise das Logo, den Titel der Webseite und oft auch die Hauptnavigation. Wichtig ist: Eine Seite kann mehrere `<header>`-Elemente haben. Ein `<article>` kann zum Beispiel seinen eigenen kleinen Header mit Autor und Datum haben.

*   **`<nav>`**: Das `<nav>`-Element ist speziell für die Hauptnavigationsblöcke deiner Seite gedacht. Du solltest es für die primären Links verwenden, die den Nutzer durch deine Webseite führen (z.B. die Hauptmenüleiste), und nicht für jede einzelne Link-Sammlung (wie Links im Footer).

*   **`<main>`**: Dieses Element ist für den Hauptinhalt deines Dokuments reserviert. Der Inhalt innerhalb von `<main>` sollte einzigartig für die jeweilige Seite sein und nicht auf anderen Seiten wiederholt werden (wie z.B. Sidebars oder Footer). Jede Seite sollte genau ein `<main>`-Element haben.

*   **`<article>`**: Ein `<article>` ist ein in sich geschlossener, unabhängiger Inhaltsblock, der theoretisch auch für sich allein stehen und weiterverbreitet werden könnte (z.B. in einem RSS-Feed). Beispiele sind ein Blogbeitrag, ein Zeitungsartikel, ein Forenpost oder ein einzelner Kommentar.

*   **`<section>`**: Das `<section>`-Element dient dazu, Inhalte thematisch zu gruppieren. Im Gegensatz zu einem `<article>` muss der Inhalt einer `<section>` nicht zwingend für sich allein stehen können. Eine Homepage könnte zum Beispiel in Sektionen wie „Über uns“, „Unsere Dienstleistungen“ und „Kundenstimmen“ unterteilt sein. Jede `<section>` sollte idealerweise eine eigene Überschrift (`<h1>`-`<h6>`) haben.

*   **`<aside>`**: Dieses Element ist für Inhalte gedacht, die nur am Rande mit dem Hauptinhalt zu tun haben. Das klassische Beispiel ist eine Sidebar mit weiterführenden Links, Werbung oder einer Autorenbiografie.

*   **`<footer>`**: Ähnlich wie der `<header>` markiert der `<footer>` den Fußbereich einer Seite oder eines Abschnitts. Hier stehen typischerweise Copyright-Informationen, Kontaktadressen, Impressumslinks oder sekundäre Navigationslinks.

#### Eine typische Seitenstruktur in der Praxis

Schauen wir uns nun an, wie die alte `<div>`-Struktur mit den neuen semantischen HTML5-Elementen aussieht. Der Unterschied in der Lesbarkeit und Klarheit ist sofort ersichtlich.

```html
<!-- Die moderne, semantische Art -->
<body>

  <header>
    <h1>Meine Webseite</h1>
    <nav>
      <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">Über uns</a></li>
        <li><a href="#">Kontakt</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <h2>Titel des Artikels</h2>
      <p>Hier steht der Inhalt des Artikels...</p>
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
    <p>&copy; 2023 Meine Webseite</p>
  </footer>

</body>
```

Dieser Code ist quasi selbsterklärend. Jeder, der ihn liest – ob Mensch oder Maschine – versteht sofort die Rolle der einzelnen Bereiche. Der Header ist der Header, die Navigation ist die Navigation, und der Hauptinhalt ist klar vom Beiwerk getrennt.

#### Die Daseinsberechtigung von `<div>` und `<span>`

Bedeutet die Einführung all dieser neuen Elemente, dass `<div>` und `<span>` nun überflüssig sind? Keineswegs. Ihre Rolle hat sich lediglich gewandelt. Sie sind deine Werkzeuge für die Fälle, in denen es **kein passendes semantisches Element** gibt.

Du wirst `<div>` weiterhin häufig verwenden, um Elemente rein für Layout- und Gestaltungszwecke zu gruppieren. Stell dir vor, du möchtest zwei Absätze zusammenfassen und ihnen einen gemeinsamen Rahmen oder eine Hintergrundfarbe geben. Es gibt kein semantisches Element für "eine Gruppe von Absätzen mit einem Rahmen". Hier ist ein `<div>` die perfekte, semantisch neutrale Lösung.

```html
<div class="hervorgehobener-bereich">
  <p>Dieser erste Absatz gehört zur Gruppe.</p>
  <p>Dieser zweite Absatz ebenfalls. Das div dient nur als Container für das Styling.</p>
</div>
```

Gleiches gilt für `<span>`. Wenn du ein einzelnes Wort oder eine kurze Phrase innerhalb eines Textes hervorheben möchtest, für die weder `<strong>` noch `<em>` passt – zum Beispiel, um es per CSS einzufärben oder mit JavaScript zu manipulieren –, dann ist `<span>` die richtige Wahl.

Die goldene Regel lautet: Nutze immer das spezifischste, semantisch passendste Element, das zur Verfügung steht. Nur wenn du keines findest, greifst du auf `<div>` für Block-Gruppierungen oder `<span>` für Inline-Gruppierungen zurück. Deine Fähigkeit, den Inhalt deiner Webseite sinnvoll und semantisch korrekt zu strukturieren, ist eine der wichtigsten Grundlagen, auf denen all deine weiteren HTML-, CSS- und JavaScript-Kenntnisse aufbauen werden.
