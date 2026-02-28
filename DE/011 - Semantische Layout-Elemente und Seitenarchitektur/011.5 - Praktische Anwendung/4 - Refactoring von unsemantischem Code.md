# Refactoring von unsemantischem Code

### Vom `<div>`-Dschungel zur klaren Struktur: Refactoring für semantisches HTML

Stell dir vor, du betrittst einen Raum, in dem alles – Bücher, Kleidung, Werkzeug, Geschirr – in identischen, unbeschrifteten grauen Kisten gelagert ist. Du könntest den Raum vielleicht nutzen, indem du jede einzelne Kiste öffnest, aber es wäre mühsam, ineffizient und für jeden neuen Besucher eine riesige Hürde. Genau dieses Szenario spiegelt eine Webseite wider, die fast ausschließlich aus `<div>`-Elementen aufgebaut ist. Man spricht hier oft vom „Div-Dschungel“ oder von „Divitis“.

Refactoring von unsemantischem Code bedeutet, diese grauen Kisten gegen passende, klar beschriftete Behälter auszutauschen: ein Bücherregal für die Bücher, einen Kleiderschrank für die Kleidung und so weiter. Du änderst nichts am Inhalt selbst, sondern nur an der Art, wie er verpackt und strukturiert ist. Das Ergebnis ist eine saubere, verständliche und zugängliche Ordnung.

#### Der Ausgangspunkt: Ein typisches unsemantisches Layout

In der Praxis wirst du oft auf Code stoßen, der funktional ist, aber dem es an semantischer Bedeutung fehlt. Visuell mag die Seite perfekt aussehen, doch unter der Haube verbirgt sich eine Struktur, die für Maschinen (wie Suchmaschinen-Crawler oder Screenreader) und für andere Entwickler schwer zu deuten ist.

Ein klassisches Beispiel für ein solches Layout könnte so aussehen:

```html
<body>
  <div id="header">
    <div class="logo">Mein Logo</div>
    <div class="nav">
      <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">Über uns</a></li>
        <li><a href="#">Kontakt</a></li>
      </ul>
    </div>
  </div>

  <div id="main-content">
    <div class="post">
      <div class="post-title">Mein erster Blogbeitrag</div>
      <p>Das ist der Inhalt meines ersten Beitrags. Hier steht viel spannender Text.</p>
    </div>
    <div class="post">
      <div class="post-title">Ein weiterer Beitrag</div>
      <p>Auch hier gibt es wieder interessante Informationen zu lesen.</p>
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
</body>
```

Dieser Code funktioniert. Mit dem passenden CSS wird er genau so aussehen, wie er soll. Das Problem ist die fehlende Semantik. Ein `div` mit der ID `header` *sagt* uns Menschen, dass es der Kopfbereich ist, aber für eine Maschine ist `div` einfach nur ein generischer Container ohne eigene Bedeutung.

#### Der Refactoring-Prozess: Schritt für Schritt zu mehr Bedeutung

Dein Ziel ist es, diese generischen `<div>`-Container durch HTML5-Elemente zu ersetzen, die genau den Zweck des Inhalts beschreiben.

**1. Identifiziere die Hauptregionen der Seite**

Schau dir die oberste Ebene der Struktur an. Fast jede Webseite lässt sich in vier bis fünf Hauptbereiche unterteilen:

*   **Header:** Der Kopfbereich, meist mit Logo und Hauptnavigation.
*   **Main Content:** Der Hauptinhalt, der für die jeweilige Seite einzigartig ist.
*   **Sidebar:** Zusätzliche, oft kontextbezogene Informationen.
*   **Footer:** Der Fußbereich mit rechtlichen Hinweisen, Kontaktinformationen oder sekundären Links.

In unserem Beispiel sind das die `div`s mit den IDs `header`, `main-content`, `sidebar` und `footer`. Diese schreien förmlich danach, durch ihre semantischen Pendants ersetzt zu werden.

*   `div id="header"` wird zu `<header>`.
*   `div id="main-content"` wird zu `<main>`.
*   `div id="sidebar"` wird zu `<aside>`.
*   `div id="footer"` wird zu `<footer>`.

Schon allein durch diese erste Änderung gewinnt die Struktur enorm an Klarheit.

```html
<body>
  <header>
    <!-- ... Inhalt des Headers ... -->
  </header>

  <main>
    <!-- ... Inhalt des Hauptbereichs ... -->
  </main>

  <aside>
    <!-- ... Inhalt der Sidebar ... -->
  </aside>

  <footer>
    <!-- ... Inhalt des Footers ... -->
  </footer>
</body>
```

**2. Verfeinere die Inhaltsblöcke**

Jetzt, wo die grobe Struktur steht, gehst du eine Ebene tiefer.

**Die Navigation:**
Innerhalb unseres `<header>`-Elements befindet sich die Navigation. Der `div` mit der Klasse `nav` ist ein perfekter Kandidat für das `<nav>`-Element. Dieses Element signalisiert unmissverständlich, dass es sich hier um einen primären Navigationsblock handelt.

Vorher:
`<div class="nav">...</div>`

Nachher:
`<nav>...</nav>`

**Die Beiträge:**
Im `<main>`-Bereich finden wir die Blogbeiträge. Jeder Beitrag ist in einem `<div class="post">` gekapselt. Ein Blogbeitrag ist eine in sich geschlossene, eigenständige Informationseinheit. Er könnte auch in einem RSS-Feed oder auf einer anderen Seite erscheinen und würde immer noch Sinn ergeben. Das ist die exakte Definition für den Einsatz des `<article>`-Elements.

Vorher:
`<div class="post">...</div>`

Nachher:
`<article>...</article>`

**Die Überschriften:**
Innerhalb jedes Beitrags gibt es ein `<div class="post-title">`. Dies ist eindeutig eine Überschrift. Statt eines `div`s solltest du hier die passenden Überschriften-Tags (`<h1>` bis `<h6>`) verwenden. Da es sich um die Hauptüberschrift des jeweiligen Artikels handelt, ist ein `<h1>` oder `<h2>` (je nach Seitenarchitektur) die richtige Wahl. Nehmen wir hier an, es ist die wichtigste Überschrift innerhalb des Artikels.

Vorher:
`<div class="post-title">Mein erster Blogbeitrag</div>`

Nachher:
`<h1>Mein erster Blogbeitrag</h1>`

Die Verwendung korrekter Überschriften-Tags ist nicht nur semantisch wertvoll, sondern auch fundamental für die Barrierefreiheit und Suchmaschinenoptimierung. Sie erzeugt eine klare Gliederung deines Dokuments.

#### Das Ergebnis: Eine saubere, semantische Struktur

Wenn du alle diese Schritte anwendest, transformiert sich der ursprüngliche Code in eine Version, die nicht nur für Menschen, sondern auch für Maschinen verständlich ist.

```html
<body>
  <header>
    <div class="logo">Mein Logo</div> <!-- Ein div für's Styling ist hier okay -->
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
      <h1>Mein erster Blogbeitrag</h1>
      <p>Das ist der Inhalt meines ersten Beitrags. Hier steht viel spannender Text.</p>
    </article>
    <article>
      <h1>Ein weiterer Beitrag</h1>
      <p>Auch hier gibt es wieder interessante Informationen zu lesen.</p>
    </article>
  </main>

  <aside>
    <h2>Verwandte Links</h2> <!-- Eine Überschrift ist auch hier sinnvoll -->
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

#### Die Rolle von `section` und die letzte Bastion des `div`

Du fragst dich vielleicht, wo das `<section>`-Element in diesem Prozess bleibt. Eine `<section>` gruppiert thematisch zusammengehörige Inhalte. Im Gegensatz zu einem `<article>` muss eine `<section>` nicht für sich allein stehen können. Eine Kontaktseite könnte zum Beispiel in Sektionen unterteilt sein: eine `<section>` für die Adresse, eine für das Kontaktformular und eine für eine Anfahrtskarte. Jede dieser Sektionen sollte idealerweise eine eigene Überschrift haben.

Und was ist mit dem `<div>`? Hat es ausgedient? Keineswegs. Das `<div>`-Element bleibt dein wichtigstes Werkzeug, wenn es **kein** passendes semantisches Element gibt. Sein einziger Zweck ist es, Inhalte für Styling- (via CSS) oder Skripting-Zwecke (via JavaScript) zu gruppieren. Wenn du einen Container nur benötigst, um darauf ein Flexbox- oder Grid-Layout anzuwenden, und der Container selbst keine inhaltliche Bedeutung hat, dann ist ein `<div>` die absolut richtige Wahl.

Refactoring ist eine kontinuierliche Praxis. Wenn du ein Projekt übernimmst oder deinen eigenen alten Code betrachtest, nimm dir die Zeit, die Struktur zu analysieren. Der Austausch unsemantischer Elemente gegen ihre aussagekräftigen Gegenstücke ist eine der wirkungsvollsten Maßnahmen, um die Qualität, Wartbarkeit, Zugänglichkeit und SEO-Performance deiner Webseite nachhaltig zu verbessern. Es ist der Wandel von einer Ansammlung anonymer Kisten zu einem perfekt organisierten, für jeden verständlichen System.
