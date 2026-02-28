# Wann div und span vermeiden

### Die Kunst des Weglassens: Wann du `<div>` und `<span>` vermeiden solltest

Die Elemente `<div>` und `<span>` sind so etwas wie das Schweizer Taschenmesser in deinem HTML-Werkzeugkasten. Sie sind unglaublich vielseitig und nützlich, aber genau wie ein echtes Schweizer Taschenmesser nicht immer das beste Werkzeug für jede Aufgabe ist, solltest du auch `<div>` und `<span>` mit Bedacht einsetzen. Ihr größter Vorteil ist gleichzeitig ihr größter Nachteil: Sie haben keinerlei semantische Bedeutung. Sie sagen nichts über den Inhalt aus, den sie umschließen. Sie sind einfach nur generische Container.

In der modernen Webentwicklung streben wir nach semantischem HTML. Das bedeutet, wir wollen Elemente verwenden, die die Bedeutung und Struktur unseres Inhalts so präzise wie möglich beschreiben. Ein gut strukturiertes, semantisches Dokument ist leichter zu verstehen – nicht nur für dich und andere Entwickler, sondern auch für Maschinen wie Suchmaschinen-Crawler und Screenreader, die blinden oder sehbehinderten Nutzern den Inhalt vorlesen.

Die übermäßige Verwendung von `<div>`-Elementen, oft als „Divitis“ bezeichnet, ist ein häufiges Problem in weniger durchdachtem Code. Es führt zu unübersichtlichen, schwer zu wartenden und semantisch armen HTML-Strukturen. Dieses Kapitel soll dir helfen, ein Gespür dafür zu entwickeln, wann ein spezifischeres, semantisches Element die bessere Wahl ist und wann der Griff zum generischen Container wirklich gerechtfertigt ist.

#### Alternativen zum `<div>`: Gib deiner Struktur eine Bedeutung

Ein `<div>` ist ein generisches Block-Level-Element. Es wird typischerweise verwendet, um größere Abschnitte einer Seite zu gruppieren, oft zu Layout- oder Styling-Zwecken. Bevor du jedoch ein `<div>` schreibst, halte kurz inne und frage dich: „Welche Art von Inhalt gruppiere ich hier eigentlich?“ Die Antwort führt dich oft zu einem passenderen HTML5-Element.

##### Für die Hauptbereiche deiner Seite

Früher war es üblich, eine Webseite komplett mit `<div>`-Elementen zu strukturieren. Das sah dann oft so aus:

```html
<!-- Die veraltete "Divitis"-Methode -->
<div id="header">
  <h1>Meine Webseite</h1>
  <div id="nav">
    <ul>...</ul>
  </div>
</div>

<div id="main-content">
  <div class="article">
    <h2>Titel des Artikels</h2>
    <p>Hier steht der Inhalt...</p>
  </div>
  <div id="sidebar">
    <p>Werbung oder Links...</p>
  </div>
</div>

<div id="footer">
  <p>&copy; 2023 Ich</p>
</div>
```

Dieser Code funktioniert, aber er ist semantisch leer. Ein Screenreader weiß nicht, dass `<div id="nav">` die Hauptnavigation ist. Eine Suchmaschine muss raten, welcher Teil der Hauptinhalt ist.

HTML5 gibt uns für genau diese Zwecke ausdrucksstarke Elemente an die Hand. Die moderne, semantisch korrekte Version sieht so aus:

```html
<!-- Die semantisch korrekte Methode -->
<header>
  <h1>Meine Webseite</h1>
  <nav>
    <ul>...</ul>
  </nav>
</header>

<main>
  <article>
    <h2>Titel des Artikels</h2>
    <p>Hier steht der Inhalt...</p>
  </article>
  <aside>
    <p>Werbung oder Links...</p>
  </aside>
</main>

<footer>
  <p>&copy; 2023 Ich</p>
</footer>
```

Hier ist eine Übersicht der wichtigsten strukturellen Elemente, die du anstelle von `<div>` verwenden solltest:

*   **`<header>`:** Für den Kopfbereich einer Seite oder eines Abschnitts. Hier findest du oft das Logo, den Seitentitel und die Hauptnavigation.
*   **`<nav>`:** Umschließt die Hauptnavigationselemente deiner Seite.
*   **`<main>`:** Definiert den Hauptinhalt des Dokuments. Es sollte pro Seite nur ein `<main>`-Element geben.
*   **`<article>`:** Für in sich geschlossene, eigenständige Inhalte, die potenziell auch außerhalb der Seite Sinn ergeben würden, wie ein Blogbeitrag, ein Forenpost oder ein Nachrichtenartikel.
*   **`<section>`:** Gruppiert thematisch zusammengehörige Inhalte. Im Gegensatz zu einem `<article>` ist eine `<section>` nicht zwingend eigenständig. Eine gute Faustregel: Eine `<section>` sollte fast immer eine eigene Überschrift (`<h2>` bis `<h6>`) haben.
*   **`<aside>`:** Für Inhalte, die nur lose mit dem Hauptinhalt zu tun haben, wie eine Seitenleiste (Sidebar), Werbeblöcke oder eine Autorenbio.
*   **`<footer>`:** Für den Fußbereich der Seite oder eines Abschnitts. Hier stehen oft Copyright-Informationen, Kontaktlinks oder Impressumsangaben.

##### Für Abbildungen und Zitate

Auch für kleinere, spezifischere Gruppierungen gibt es oft bessere Alternativen als ein `<div>`.

*   **`<figure>` und `<figcaption>`:** Wenn du ein Bild, ein Diagramm oder ein Codebeispiel mit einer dazugehörigen Beschriftung hast, ist `<div>` die falsche Wahl. Verwende stattdessen `<figure>` für das Element selbst und `<figcaption>` für die Bildunterschrift. Dies schafft eine starke semantische Verbindung zwischen dem Inhalt und seiner Beschreibung.

    *Schlecht:*
    ```html
    <div class="image-container">
      <img src="katze.jpg" alt="Eine schlafende Katze">
      <p class="caption">Meine Katze Minka beim Mittagsschlaf.</p>
    </div>
    ```

    *Gut:*
    ```html
    <figure>
      <img src="katze.jpg" alt="Eine schlafende Katze">
      <figcaption>Meine Katze Minka beim Mittagsschlaf.</figcaption>
    </figure>
    ```

*   **`<blockquote>`:** Für längere, blockförmige Zitate. Umschließe den zitierten Text nicht einfach mit einem `<div class="quote">`, sondern nutze das dafür vorgesehene `<blockquote>`-Element. Du kannst mit dem `cite`-Attribut sogar die Quelle angeben.

#### Alternativen zum `<span>`: Gib deinem Text eine Bedeutung

Ein `<span>` ist das Inline-Gegenstück zum `<div>`. Es wird verwendet, um einen kleinen Teil eines Textes oder anderer Inline-Inhalte zu gruppieren, meist um ihn gezielt mit CSS zu formatieren oder mit JavaScript zu manipulieren. Genau wie beim `<div>` gilt auch hier: Frage dich zuerst, *warum* du diesen Textteil hervorheben möchtest. Die Antwort verrät dir oft das richtige semantische Element.

##### Für Betonung und Wichtigkeit

Der häufigste Fehler ist die Verwendung von `<span>` für simple Textformatierungen wie Fett oder Kursiv.

*   **`<em>` (Emphasis):** Anstelle von `<span style="font-style: italic;">` solltest du `<em>` verwenden, wenn du einem Wort oder einer Phrase eine Betonung geben möchtest, die die Bedeutung des Satzes verändert. Screenreader ändern hier oft die Betonung ihrer Stimme. Beispiel: „Ich habe das *wirklich* nicht gewollt.“
*   **`<strong>` (Strong Importance):** Anstelle von `<span style="font-weight: bold;">` solltest du `<strong>` verwenden, um auszudrücken, dass ein Teil des Textes von großer Wichtigkeit, Ernsthaftigkeit oder Dringlichkeit ist. Beispiel: „**Achtung:** Betreten verboten!“
*   **`<i>` (Idiomatic Text):** Dieses Element ist für Text, der sich vom Rest abhebt, aber nicht besonders betont oder wichtig ist. Das können Fachbegriffe, Schiffsnamen, Gedankengänge oder anderssprachige Phrasen sein. Es wird standardmäßig kursiv dargestellt. Beispiel: Der Begriff *Responsive Design* ist zentral für die moderne Webentwicklung.
*   **`<b>` (Bring Attention To):** Ähnlich wie `<i>`, aber für Text, der visuell hervorgehoben werden soll, ohne ihm zusätzliche Wichtigkeit zu verleihen. Das sind oft Schlüsselwörter in einem Text oder Produktnamen in einer Rezension. Es wird standardmäßig fett dargestellt.

##### Für spezifische Textarten

HTML bietet eine ganze Reihe von Elementen für sehr spezifische Arten von Inline-Text:

*   **`<mark>`:** Um einen Textabschnitt hervorzuheben oder zu markieren, quasi wie mit einem Textmarker. Nützlich, um Suchergebnisse in einem Text zu kennzeichnen.
*   **`<code>`:** Für einen kurzen Ausschnitt aus Computer-Code. Beispiel: Die Funktion heißt `getElementById()`.
*   **`<time>`:** Um ein Datum oder eine Uhrzeit zu kennzeichnen. Mit dem `datetime`-Attribut kannst du eine maschinenlesbare Version bereitstellen. Beispiel: `<time datetime="2024-10-26">26. Oktober 2024</time>`.
*   **`<q>`:** Für kurze, in den Fließtext eingebettete Zitate. Browser setzen hier automatisch Anführungszeichen.
*   **`<abbr>`:** Für Abkürzungen oder Akronyme. Mit dem `title`-Attribut kannst du die volle Bedeutung angeben. Beispiel: `<abbr title="Hypertext Markup Language">HTML</abbr>`.
*   **`<kbd>`:** Für Tastatureingaben. Beispiel: Drücke <kbd>Strg</kbd> + <kbd>C</kbd> zum Kopieren.

#### Wann `<div>` und `<span>` doch die richtige Wahl sind

Nach all diesen Alternativen fragst du dich vielleicht, ob es überhaupt noch legitime Anwendungsfälle für `<div>` und `<span>` gibt. Die Antwort ist ein klares Ja. Sie sind immer dann die richtige Wahl, wenn es **kein passendes semantisches Element** gibt und du einen Container rein für gestalterische oder funktionale Zwecke benötigst.

##### 1. Rein für das Layout

Manchmal musst du Elemente gruppieren, die semantisch nichts miteinander zu tun haben, nur um ein bestimmtes Layout (z. B. mit Flexbox oder CSS Grid) zu erzeugen.

Stell dir eine Produktkarte vor, die ein Bild, eine Überschrift, einen Absatz und einen Button enthält. Diese Elemente bilden zwar eine visuelle Einheit, aber es gibt kein semantisches HTML-Element für eine „Produktkarte“. Hier ist ein `<div>` als Wrapper perfekt geeignet:

```html
<div class="product-card">
  <img src="produkt.jpg" alt="Ein tolles Produkt">
  <h3>Tolles Produkt</h3>
  <p>Eine kurze Beschreibung des Produkts, die Lust auf mehr macht.</p>
  <button>In den Warenkorb</button>
</div>
```
Das `<div>` dient hier ausschließlich als Container für das Styling, das alle inneren Elemente zu einer optischen Einheit zusammenfasst.

##### 2. Als Haken für JavaScript

Wenn du einen bestimmten Bereich deiner Seite mit JavaScript manipulieren möchtest, zum Beispiel um einen Graphen zu zeichnen oder dynamische Inhalte zu laden, ist ein `<div>` mit einer `id` oder einer spezifischen Klasse oft der sauberste Weg.

```html
<!-- Dieser Container wird von JavaScript befüllt -->
<div id="chart-container"></div>
```
Hier gibt es keinen Inhalt, über den man eine semantische Aussage treffen könnte. Das `<div>` ist lediglich ein Platzhalter und ein Ziel für dein Skript.

Ähnliches gilt für `<span>`. Wenn du beispielsweise einzelne Buchstaben eines Wortes animieren möchtest, gibt es kein semantisches Element für einen einzelnen Buchstaben. Hier ist es absolut legitim, jeden Buchstaben in ein `<span>` zu packen, um ihn ansprechen zu können:

```html
<h1>
  <span>W</span>
  <span>i</span>
  <span>l</span>
  <span>l</span>
  <span>k</span>
  <span>o</span>
  <span>m</span>
  <span>m</span>
  <span>e</span>
  <span>n</span>
</h1>
```

Der Schlüssel ist, immer zuerst die semantischen Optionen zu prüfen. Nur wenn keine davon passt, greifst du zu `<div>` und `<span>`. Sie sind deine Werkzeuge der letzten Wahl, nicht deine Standardlösung. Indem du diese Regel befolgst, schreibst du saubereren, zugänglicheren und zukunftssicheren Code.
