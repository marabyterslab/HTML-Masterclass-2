# Strukturierung des Inhalts

### Strukturierung des Inhalts

Nachdem wir im vorherigen Kapitel den grundsätzlichen Aufbau eines HTML-Dokuments mit `<html>`, `<head>` und `<body>` kennengelernt haben, tauchen wir nun tief in den `<body>`-Bereich ein. Hier spielt die eigentliche Musik, denn alles, was ein Benutzer im Browserfenster sieht, wird innerhalb dieses Tags definiert. Doch einfach nur Text und Bilder wahllos auf eine Seite zu werfen, führt schnell zu Chaos – für dich als Entwickler, für Suchmaschinen und vor allem für Menschen, die auf Hilfstechnologien wie Screenreader angewiesen sind.

Die Kunst besteht darin, deinem Inhalt eine klare und logische Struktur zu geben. HTML ist hierfür dein wichtigstes Werkzeug. Stell dir vor, du schreibst ein Buch. Du würdest es auch nicht als einen einzigen, unendlichen Textblock verfassen. Du nutzt Kapitel, Überschriften, Absätze, Listen und Zitate, um dem Leser das Verständnis zu erleichtern. Genau das Gleiche tun wir in HTML, nur dass unsere Werkzeuge keine Druckerpresse, sondern sogenannte "Tags" sind.

#### Die Semantik – Das Fundament guter Struktur

Bevor wir uns die einzelnen Elemente ansehen, musst du ein zentrales Konzept verstehen: **Semantisches HTML**. Das klingt komplizierter, als es ist. Es bedeutet lediglich, dass du HTML-Tags entsprechend ihrer Bedeutung (ihrer Semantik) verwendest und nicht aufgrund ihres Aussehens.

Früher, in den wilden Anfangstagen des Webs, nutzten Entwickler Tabellen, um Layouts zu erstellen, oder `<b>`-Tags, nur um Text fett zu machen. Das ist heute ein absolutes No-Go. Ein `<h1>`-Tag sagt nicht "mach diesen Text groß und fett", sondern "dies ist die Hauptüberschrift der Seite". Wie diese Überschrift *aussieht*, wird später ausschließlich mit CSS festgelegt.

Warum ist das so wichtig?

*   **Barrierefreiheit (Accessibility):** Ein Screenreader für einen blinden Benutzer kann eine Seite nur dann sinnvoll vorlesen, wenn er die Struktur versteht. Er kann sagen: "Hier beginnt die Hauptnavigation" oder "Überschrift Ebene 2: Kontaktdaten". Bei einer Seite voller nichtssagender `<div>`-Container ist das unmöglich.
*   **Suchmaschinenoptimierung (SEO):** Suchmaschinen wie Google analysieren die Struktur deiner Seite, um den Inhalt zu verstehen. Eine klare Hierarchie mit einer `<h1>`, gefolgt von `<h2>`-Überschriften und sinnvollen Absätzen, hilft der Suchmaschine, die Relevanz deiner Inhalte besser einzuschätzen.
*   **Wartbarkeit:** Für dich und andere Entwickler ist ein semantisch strukturierter Code unendlich viel einfacher zu lesen, zu verstehen und zu pflegen. Du siehst auf einen Blick, welcher Teil der Seite der Header, der Hauptinhalt oder der Footer ist.
*   **Flexibilität:** Da die Struktur (HTML) und das Aussehen (CSS) getrennt sind, kannst du das Design deiner Webseite komplett ändern, ohne ein einziges HTML-Tag anfassen zu müssen.

#### Die groben Bausteine deiner Seite

Eine typische Webseite lässt sich in große, logische Bereiche unterteilen. HTML5 hat uns dafür eine Reihe von wunderbaren, semantischen Tags an die Hand gegeben, die die alten, generischen `<div>`-Elemente für das Grundlayout weitgehend ablösen.

**`<header>` – Der Kopfbereich**

Der `<header>`-Bereich enthält in der Regel einführende Inhalte für die gesamte Seite oder einen bestimmten Abschnitt. Das sind typischerweise das Logo, der Seitentitel und oft auch die Hauptnavigation. Wichtig: Eine Seite kann mehrere `<header>`-Elemente haben. Du könntest zum Beispiel auch einen `<header>` innerhalb eines Blogartikels (`<article>`) verwenden, der den Titel und den Autor des Artikels enthält.

```html
<header>
  <img src="logo.png" alt="Firmenlogo">
  <h1>Meine Fantastische Webseite</h1>
</header>
```

**`<nav>` – Die Navigation**

Das `<nav>`-Element ist speziell für die Hauptnavigationsblöcke deiner Seite gedacht. Das sind die Links, die den Benutzer zu den wichtigsten Bereichen deiner Website führen.

```html
<nav>
  <ul>
    <li><a href="/">Startseite</a></li>
    <li><a href="/ueber-uns.html">Über uns</a></li>
    <li><a href="/kontakt.html">Kontakt</a></li>
  </ul>
</nav>
```

**`<main>` – Der Hauptinhalt**

Dies ist eines der wichtigsten Strukturelemente. Das `<main>`-Tag umschließt den einzigartigen Hauptinhalt deines Dokuments. Inhalte, die sich auf jeder Seite wiederholen, wie die Navigation oder der Footer, gehören hier nicht hinein. Pro Seite sollte es nur *ein* `<main>`-Element geben.

**`<footer>` – Der Fußbereich**

Der `<footer>` enthält typischerweise Informationen, die am Ende einer Seite oder eines Abschnitts stehen. Das können Copyright-Hinweise, Links zum Impressum, Kontaktinformationen oder sekundäre Navigationslinks sein. Ähnlich wie der `<header>` kann auch ein `<footer>` mehrfach auf einer Seite vorkommen.

**`<aside>` – Die Seitenleiste**

Das `<aside>`-Element ist für Inhalte gedacht, die nur lose mit dem Hauptinhalt der Seite verbunden sind. Klassische Beispiele sind eine Liste mit weiterführenden Links, eine Werbeanzeige oder eine Autorenbiografie am Rande eines Blogartikels.

Ein Grundgerüst könnte also so aussehen:

```html
<body>
  <header>
    <h1>Webseiten-Titel</h1>
    <nav>
      <!-- Navigationslinks hier -->
    </nav>
  </header>

  <main>
    <h2>Hauptinhalt der Seite</h2>
    <p>Hier steht der einzigartige Content, der diese Seite ausmacht...</p>
  </main>

  <aside>
    <h3>Verwandte Themen</h3>
    <p>Links und Infos, die nur am Rande relevant sind.</p>
  </aside>

  <footer>
    <p>&copy; 2023 Meine Webseite. Alle Rechte vorbehalten.</p>
  </footer>
</body>
```

#### Inhalt gliedern mit Sections und Articles

Innerhalb deines `<main>`-Bereichs wirst du den Inhalt weiter unterteilen wollen. Dafür gibt es vor allem zwei Elemente, deren Unterscheidung anfangs etwas knifflig sein kann: `<article>` und `<section>`.

**`<article>` – Der in sich geschlossene Inhalt**

Ein `<article>` ist für einen in sich geschlossenen, unabhängigen Inhalt gedacht, der potenziell auch an anderer Stelle wiederverwendet werden könnte (z. B. in einem RSS-Feed). Ein Blogbeitrag, ein Forenpost, ein Zeitungsartikel oder ein einzelnes Produkt in einem Onlineshop sind perfekte Kandidaten für ein `<article>`-Element.

**`<section>` – Die thematische Gruppierung**

Ein `<section>`-Element gruppiert Inhalte, die thematisch zusammengehören. Im Gegensatz zum `<article>` ergibt eine `<section>` für sich alleinstehend oft keinen Sinn. Eine Webseite über ein Buch könnte zum Beispiel Sections für "Einleitung", "Handlung" und "Charaktere" haben. Jede dieser Sections ist ein thematischer Block, aber keine davon wäre ein eigenständiger Artikel.

Die goldene Regel lautet: Frage dich, ob der Inhalt auch für sich alleine stehen und sinnvoll sein könnte. Wenn ja, ist es wahrscheinlich ein `<article>`. Wenn nein, aber es ist eine klare thematische Gruppierung, ist es eine `<section>`.

**Und was ist mit `<div>`?**

Das `<div>`-Element ist der nicht-semantische Container. Es hat absolut keine eigene Bedeutung. Du solltest es immer nur dann verwenden, wenn kein anderes, semantisch passenderes Element zur Verfügung steht. Sein Hauptzweck ist es, Elemente für reines Styling mit CSS oder für die Manipulation mit JavaScript zu gruppieren. Ein typischer Anwendungsfall wäre ein Container, der zwei Spalten deines Layouts zusammenfasst, nur um ihnen einen gemeinsamen Hintergrund zu geben.

#### Die Feinstruktur – Überschriften, Absätze und mehr

Wenn du deine grobe Struktur mit den oben genannten Elementen geschaffen hast, geht es an die Feinarbeit im Inneren dieser Blöcke.

**Überschriften (`<h1>` - `<h6>`)**

Überschriften sind das Rückgrat deiner inhaltlichen Gliederung. Sie definieren eine Hierarchie.

*   `<h1>`: Die Hauptüberschrift der gesamten Seite. Es sollte pro Seite nur eine einzige geben.
*   `<h2>`: Unterüberschriften, die die Hauptthemen gliedern.
*   `<h3>` bis `<h6>`: Weitere Unterteilungen.

Verwende Überschriften niemals, um Text einfach nur größer darzustellen! Ihre Aufgabe ist es, die Struktur deines Dokuments zu definieren. Die visuelle Darstellung ist alleinige Aufgabe von CSS.

**Absätze (`<p>`)**

Das `<p>`-Element (Paragraph) ist das Arbeitstier für Fließtext. Jeder Textabsatz sollte in ein eigenes `<p>`-Tag eingeschlossen werden. Browser fügen standardmäßig einen kleinen Abstand zwischen Absätzen ein, was die Lesbarkeit enorm verbessert.

**Listen (`<ul>`, `<ol>`, `<li>`)**

Für Aufzählungen gibt es zwei Arten von Listen:

*   `<ul>` (Unordered List): Eine unsortierte Liste, deren Punkte typischerweise mit Aufzählungszeichen (Bullets) dargestellt werden.
*   `<ol>` (Ordered List): Eine sortierte Liste, deren Punkte automatisch nummeriert werden (1, 2, 3, ...).
*   `<li>` (List Item): Jedes einzelne Element innerhalb einer `<ul>`- oder `<ol>`-Liste muss von einem `<li>`-Tag umschlossen werden.

```html
<!-- Unsortierte Liste -->
<ul>
  <li>Milch</li>
  <li>Brot</li>
  <li>Eier</li>
</ul>

<!-- Sortierte Liste -->
<ol>
  <li>Recherche durchführen</li>
  <li>Entwurf schreiben</li>
  <li>Korrektur lesen</li>
</ol>
```

**Zitate (`<blockquote>` und `<q>`)**

Wenn du Text von einer anderen Quelle zitierst, solltest du die dafür vorgesehenen Tags verwenden.

*   `<blockquote>`: Für längere, mehrzeilige Zitate, die als eigener Block dargestellt werden.
*   `<q>`: Für kurze, inline-Zitate innerhalb eines Satzes. Browser setzen hier automatisch Anführungszeichen.

```html
<p>Wie Einstein schon sagte:</p>
<blockquote>
  Phantasie ist wichtiger als Wissen, denn Wissen ist begrenzt.
</blockquote>
<p>Er beschrieb es als <q>ein heiliges Geschenk der Neugier</q>.</p>
```

#### Textauszeichnung – Wenn Worte mehr bedeuten

Manchmal möchtest du einzelne Wörter oder Satzteile innerhalb eines Fließtextes hervorheben. Auch hier gilt wieder: Nutze das semantisch korrekte Element.

*   `<strong>`: Kennzeichnet Text von großer Wichtigkeit, Ernsthaftigkeit oder Dringlichkeit. Browser stellen dies standardmäßig fett dar. Es geht aber um die inhaltliche *Bedeutung*, nicht um das Aussehen.
*   `<em>`: Kennzeichnet eine Betonung (Emphasis), die die Bedeutung eines Satzes verändert. Browser stellen dies standardmäßig kursiv dar.

Ein Beispiel für den Unterschied:

```html
<p><strong>Achtung:</strong> Betreten der Baustelle verboten!</p>
<p>Ich bin <em>wirklich</em> müde.</p>
```

Die alten Tags `<b>` (bold) und `<i>` (italic) existieren zwar noch, sollten aber nur verwendet werden, wenn es keine semantische Bedeutung gibt, sondern der Text aus stilistischen Gründen (z. B. ein Fachbegriff, ein Schiffname) anders aussehen soll, ohne ihm mehr Gewicht zu verleihen. In den meisten Fällen sind `<strong>` und `<em>` die bessere Wahl.

Zuletzt gibt es noch das `<span>`-Element. Es ist das inline-Pendant zum `<div>`. Es hat keine semantische Bedeutung und dient lediglich dazu, ein oder mehrere Wörter zu umschließen, um sie gezielt mit CSS zu stylen oder mit JavaScript zu bearbeiten, wenn kein anderes Element passt.

Indem du diese Prinzipien und Elemente anwendest, baust du nicht nur Webseiten, die gut aussehen, sondern die eine solide, verständliche und zukunftssichere Struktur haben. Das ist die wahre Grundlage professioneller Webentwicklung.
