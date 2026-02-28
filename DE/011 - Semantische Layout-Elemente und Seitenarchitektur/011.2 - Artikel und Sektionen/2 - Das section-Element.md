# Das section-Element

### Das `<section>`-Element

Wenn du beginnst, die semantischen Elemente von HTML5 zu erkunden, stößt du unweigerlich auf das `<section>`-Element. Auf den ersten Blick wirkt es vielleicht wie ein Allzweck-Container, ähnlich dem altbekannten `<div>`. Doch diese Annahme greift zu kurz. Das `<section>`-Element hat eine klare und wichtige Aufgabe: Es gruppiert thematisch zusammengehörige Inhalte und verleiht deiner Webseite eine logische Struktur, die sowohl für Menschen als auch für Maschinen verständlich ist.

Denk an ein Buch. Ein Buch ist in Kapitel unterteilt, und jedes Kapitel behandelt ein bestimmtes Thema oder einen Teil der Geschichte. Genau das ist die Rolle eines `<section>`-Elements auf einer Webseite. Es ist ein Kapitel deines Dokuments.

#### Die goldene Regel: Eine Sektion braucht eine Überschrift

Die wichtigste Regel, die du dir im Umgang mit `<section>` merken solltest, ist diese: Eine Sektion sollte fast immer eine Überschrift haben. Die Überschrift (ein `<h1>` bis `<h6>`-Element) definiert das Thema der Sektion und macht ihren Zweck unmissverständlich klar. Ohne eine Überschrift ist eine Sektion wie ein unbenanntes Kapitel in einem Buch – man weiß nicht, worum es geht, bis man anfängt zu lesen.

Suchmaschinen und assistierende Technologien, wie zum Beispiel Screenreader für sehbehinderte Nutzer, verlassen sich auf diese Überschriften, um die Struktur einer Seite zu verstehen. Ein Screenreader-Nutzer kann von Überschrift zu Überschrift springen, um schnell einen Überblick über den Inhalt zu bekommen und direkt zu dem Abschnitt zu navigieren, der ihn interessiert. Eine `<section>` ohne Überschrift ist in diesem Kontext oft nur semantisches Rauschen.

Schauen wir uns ein korrektes Beispiel an:

```html
<main>
  <h1>Mein Reiseblog</h1>
  <p>Willkommen auf meinem Blog, hier teile ich meine Abenteuer!</p>

  <section>
    <h2>Meine Reise durch die Alpen</h2>
    <p>Die Alpenüberquerung war eine unglaubliche Erfahrung. Die majestätischen Gipfel, die klaren Bergseen ...</p>
    <img src="alpen.jpg" alt="Ein sonniger Tag in den Alpen.">
  </section>

  <section>
    <h2>Städtetrip nach Rom</h2>
    <p>Rom, die ewige Stadt, hat mich verzaubert. Das Kolosseum bei Sonnenuntergang zu sehen, war ein unvergesslicher Moment.</p>
    <p>Die italienische Küche ist natürlich auch ein Highlight...</p>
  </section>
</main>
```

In diesem Beispiel ist die Struktur sonnenklar. Die Seite hat eine Hauptüberschrift (`<h1>`). Darunter gibt es zwei thematische Sektionen: eine über die Alpenreise und eine über den Städtetrip nach Rom. Jede Sektion wird durch eine `<h2>`-Überschrift eingeleitet, die ihren Inhalt beschreibt.

#### Abgrenzung: `<section>` vs. `<div>`

Eine der häufigsten Quellen der Verwirrung ist die Frage: Wann nehme ich `<section>` und wann `<div>`? Die Antwort liegt in der Semantik, also der Bedeutung.

Ein `<div>` ist ein generischer, nicht-semantischer Container. Es hat absolut keine eigene Bedeutung. Du verwendest es ausschließlich, um Inhalte zu gruppieren, die du gemeinsam formatieren oder per JavaScript manipulieren möchtest, wenn es kein passenderes semantisches Element gibt. Ein `<div>` sagt dem Browser nur: "Diese Elemente hier gehören irgendwie zusammen, aber frag mich nicht, warum."

Ein `<section>` hingegen trägt Bedeutung. Es sagt dem Browser und anderen Programmen: "Dieser Block von Inhalten bildet eine eigenständige, thematische Einheit innerhalb dieses Dokuments."

Stell dir eine Webseite vor. Du möchtest vielleicht den gesamten Inhalt in einen zentrierten Container mit einer maximalen Breite packen. Dieser Container hat keine thematische Bedeutung für den Inhalt der Seite selbst, er dient rein dem Layout. Das ist ein perfekter Anwendungsfall für ein `<div>`.

```html
<body>
  <div class="wrapper">
    <!-- Der gesamte Seiteninhalt kommt hier rein -->
    <header>...</header>
    <main>
      <section>
        <h2>Über uns</h2>
        <p>Wir sind eine Firma, die tolle Dinge herstellt.</p>
      </section>
    </main>
    <footer>...</footer>
  </div>
</body>
```

Innerhalb dieses Layout-Wrappers verwenden wir dann `<section>` für die inhaltlichen Blöcke wie "Über uns", weil dieser Block ein klares Thema hat.

**Faustregel:** Wenn du überlegst, ein `<section>` zu verwenden, frage dich: "Kann ich diesem Inhaltsblock eine sinnvolle Überschrift geben?" Wenn die Antwort "Nein" lautet, weil es nur ein Styling-Container ist, dann ist `<div>` wahrscheinlich die bessere Wahl.

#### Abgrenzung: `<section>` vs. `<article>`

Die Unterscheidung zwischen `<section>` und `<article>` ist subtiler, aber genauso wichtig. Beide Elemente gruppieren Inhalte, aber ihre kontextuelle Bedeutung ist unterschiedlich.

Ein `<article>`-Element ist für in sich geschlossene, eigenständige Inhalte gedacht. Der Inhalt eines `<article>` sollte so beschaffen sein, dass er theoretisch aus der Seite herausgenommen und an anderer Stelle (z.B. in einem RSS-Feed, auf einer anderen Webseite oder in einer App) wiederverwendet werden könnte und dort immer noch Sinn ergibt. Typische Beispiele sind:
*   Ein Blogbeitrag
*   Ein Zeitungsartikel
*   Ein Forenpost
*   Ein einzelner Produkt-Eintrag in einem Online-Shop
*   Ein Kommentar eines Nutzers

Ein `<section>`-Element hingegen gruppiert Inhalte, deren Bedeutung oft eng mit dem umgebenden Dokument verknüpft ist. Die Sektionen einer Produktseite – "Technische Daten", "Kundenbewertungen", "Zubehör" – ergeben einzeln, aus dem Kontext gerissen, weniger Sinn. Sie sind Teile eines größeren Ganzen.

Schauen wir uns das an einem Blog an. Die Startseite eines Blogs könnte eine Liste der neuesten Beiträge zeigen. Jeder dieser Beiträge wäre ein `<article>`.

```html
<main>
  <h1>Neueste Beiträge</h1>

  <article>
    <h2>Titel des ersten Beitrags</h2>
    <p>Eine kurze Zusammenfassung des Beitrags...</p>
    <a href="/beitrag-1">Weiterlesen</a>
  </article>

  <article>
    <h2>Titel des zweiten Beitrags</h2>
    <p>Eine kurze Zusammenfassung des Beitrags...</p>
    <a href="/beitrag-2">Weiterlesen</a>
  </article>
</main>
```

Wenn du nun auf einen dieser Beiträge klickst und auf die Detailseite kommst, ist der Hauptinhalt dieser Seite ebenfalls ein `<article>`. Innerhalb dieses einen Artikels könntest du jedoch `<section>`-Elemente verwenden, um ihn weiter zu untergliedern:

```html
<main>
  <article>
    <h1>Titel des ersten Beitrags</h1>
    <p>Veröffentlichungsdatum, Autor, etc.</p>

    <section>
      <h2>Die Einleitung: Worum geht es?</h2>
      <p>Hier steht der einleitende Text des Blogbeitrags.</p>
    </section>

    <section>
      <h2>Der Hauptteil: Eine detaillierte Analyse</h2>
      <p>Hier folgt die ausführliche Analyse des Themas...</p>
    </section>

    <section>
      <h2>Fazit und Ausblick</h2>
      <p>Zusammenfassend lässt sich sagen, dass...</p>
    </section>
  </article>
</main>
```

Hier siehst du das Zusammenspiel perfekt: Der gesamte Beitrag ist ein eigenständiges `<article>`. Die logischen Unterkapitel innerhalb dieses Artikels ("Einleitung", "Hauptteil", "Fazit") sind `<section>`-Elemente, die den Artikel strukturieren.

#### Verschachtelung von `<section>`-Elementen

So wie ein Buch Kapitel und Unterkapitel haben kann, kannst du auch `<section>`-Elemente ineinander verschachteln. Dies ist nützlich, um eine komplexe Hierarchie von Themen und Unterthemen abzubilden. Wichtig ist dabei, dass du die Überschriften-Ebenen (`h1` bis `h6`) entsprechend anpasst, um die logische Struktur beizubehalten.

Ein übergeordnetes Thema hat eine höhere Überschriften-Ebene (z.B. `<h2>`), während die untergeordneten Sektionen eine niedrigere Ebene (z.B. `<h3>`) verwenden.

```html
<section>
  <h2>Kapitel 1: Die Grundlagen</h2>
  <p>Hier werden die grundlegenden Konzepte erklärt.</p>
  
  <section>
    <h3>Kapitel 1.1: Das erste Konzept</h3>
    <p>Details zum ersten Konzept...</p>
  </section>

  <section>
    <h3>Kapitel 1.2: Das zweite Konzept</h3>
    <p>Details zum zweiten Konzept...</p>
  </section>
</section>
```

Diese saubere Gliederung durch verschachtelte Sektionen und korrekte Überschriften-Hierarchien ist ein Segen für die Barrierefreiheit und die Maschinenlesbarkeit deiner Webseite.

#### Wann du `<section>` *nicht* verwenden solltest

Zusammenfassend lässt sich sagen, dass du `<section>` nicht verwenden solltest, wenn:

1.  **Es nur für das Styling ist:** Wenn du einen Container nur für CSS-Zwecke benötigst (z.B. ein Flexbox-Container oder ein Grid-Wrapper), nutze ein `<div>`.
2.  **Es keine natürliche Überschrift für den Inhalt gibt:** Wenn du dir keine passende Überschrift für den Block ausdenken kannst, ist es wahrscheinlich keine thematische Sektion.
3.  **Ein spezifischeres semantisches Element besser passt:** HTML bietet viele spezialisierte Elemente, die als Sektionen fungieren. Nutze immer das spezifischste Element, das zutrifft. Verwende `<nav>` für die Hauptnavigation, `<aside>` für eine Seitenleiste mit ergänzenden Informationen, `<header>` für den Kopfbereich und `<footer>` für den Fußbereich einer Seite oder eines Artikels. Ein `<section>` ist ein generisches Gliederungselement – wenn es ein "besseres" Wort gibt, nutze es.

Die bewusste Entscheidung für oder gegen ein `<section>`-Element ist ein wichtiger Schritt auf dem Weg zu professionellem, semantisch reichem HTML. Es geht nicht nur darum, wie eine Seite aussieht, sondern auch darum, was sie bedeutet. Indem du `<section>` korrekt einsetzt, schaffst du eine klarere, zugänglichere und für Suchmaschinen besser verständliche Struktur für deine digitalen Inhalte.
