# HTML für Struktur

### HTML für Struktur: Das Fundament jeder Webseite

Stell dir eine Webseite wie ein Haus vor. Bevor du Wände streichst, Möbel auswählst oder die Elektrik installierst, brauchst du ein solides Fundament, tragende Wände und ein Dach. Du brauchst eine klare Struktur, die dem Haus Form und Stabilität gibt. Im Web ist HTML genau das: der Rohbau, das Skelett deiner Webseite.

CSS (Cascading Style Sheets) ist dann der Innenarchitekt, der für die Farben, die Schriftarten und das Layout der Möbel sorgt. JavaScript ist die Technik im Haus – die elektrischen Rollläden, die Alarmanlage oder der Aufzug. Ohne die grundlegende Struktur des Hauses gäbe es aber nichts, was man gestalten oder mit Technik ausstatten könnte.

Deine primäre Aufgabe beim Schreiben von HTML ist es also, dem Inhalt eine sinnvolle und logische Struktur zu geben. Du definierst, was eine Überschrift ist, was ein Absatz, was eine Liste und welche Bereiche zusammengehören. Diese Trennung von Inhalt (Struktur), Präsentation (Design) und Verhalten (Interaktivität) ist das zentrale Prinzip moderner Webentwicklung.

#### Die Kunst der Bedeutung: Semantisches HTML

Wenn wir von "Struktur" sprechen, meinen wir nicht nur, Elemente ineinander zu schachteln. Wir meinen vor allem **Semantik**. Ein semantisches HTML-Element beschreibt seine Bedeutung – den Sinn und Zweck seines Inhalts.

Ein frühes Beispiel, das den Unterschied verdeutlicht, ist der `<b>`-Tag (bold) im Vergleich zum `<strong>`-Tag. Beide lassen den Text im Browser standardmäßig fett erscheinen. Doch ihre Bedeutung ist grundverschieden:

*   `<b>Text</b>`: Dieser Tag sagt dem Browser nur: "Stelle diesen Text fett dar." Er hat keine tiefere Bedeutung. Es ist ein rein visueller Hinweis.
*   `<strong>Text</strong>`: Dieser Tag sagt dem Browser: "Dieser Text hat eine starke Wichtigkeit." Die fette Darstellung ist nur die *Standardinterpretation* dieser Wichtigkeit.

Warum ist dieser Unterschied so wichtig? Weil nicht nur Menschen mit Sehkraft deine Webseite betrachten. Suchmaschinen-Crawler, Screenreader für blinde oder sehbehinderte Nutzer und andere automatisierte Systeme lesen deinen Code. Sie können nichts sehen. Sie sind auf die semantische Bedeutung angewiesen, die du mit deinen HTML-Tags vermittelst. Ein Screenreader wird Text in einem `<strong>`-Tag mit einer anderen Betonung vorlesen, weil er dessen Wichtigkeit versteht. Eine Suchmaschine wird diesen Text als relevanter für das Thema der Seite einstufen.

Deine Aufgabe ist es also, das HTML-Element zu wählen, das die *Bedeutung* deines Inhalts am besten beschreibt, nicht das, was optisch am besten passt. Die Optik ist der Job von CSS.

#### Warum die Trennung so entscheidend ist

Die konsequente Nutzung von HTML für die Struktur hat mehrere unschätzbare Vorteile, die weit über sauberen Code hinausgehen.

1.  **Zugänglichkeit (Barrierefreiheit):** Ein semantisch korrekt aufgebautes Dokument ist die Grundlage für Barrierefreiheit im Web. Ein blinder Nutzer navigiert mit seinem Screenreader nicht mit der Maus, sondern springt von Überschrift zu Überschrift, von Link zu Link oder von einem strukturellen Bereich zum nächsten. Wenn du deine Hauptüberschrift als `<div style="font-size: 32px; font-weight: bold;">` anstatt als `<h1>` auszeichnest, ist sie für diesen Nutzer nur ein beliebiger Textblock. Nutzt du hingegen `<h1>`, `<h2>`, `<nav>` (für die Navigation) und `<main>` (für den Hauptinhalt), gibst du ihm eine klare Landkarte deiner Seite an die Hand.

2.  **Suchmaschinenoptimierung (SEO):** Suchmaschinen wie Google sind im Grunde blinde, aber sehr intelligente Nutzer. Sie analysieren die Struktur deiner HTML-Datei, um den Inhalt zu verstehen und zu bewerten. Der Inhalt einer `<h1>`-Überschrift wird als extrem wichtig für das Thema der Seite angesehen. Text in einem `<p>`-Tag ist Fließtext. Elemente in einer `<ul>` (unsortierte Liste) sind zusammengehörige Punkte. Eine saubere, semantische Struktur hilft Suchmaschinen, deine Inhalte besser zu indizieren und führt somit zu einem besseren Ranking.

3.  **Wartbarkeit und Zusammenarbeit:** Wenn die Struktur klar von der Darstellung getrennt ist, wird die Pflege der Webseite um ein Vielfaches einfacher. Stell dir vor, du möchtest die Farbe aller Unterüberschriften auf deiner Webseite ändern. Bei einem sauberen Aufbau änderst du eine einzige Zeile in deiner CSS-Datei, die sich auf alle `<h2>`-Elemente bezieht. Hättest du die Farbe direkt im HTML-Code bei jedem Element einzeln definiert, müsstest du Dutzende oder Hunderte von Dateien anfassen. Es ermöglicht auch eine effizientere Zusammenarbeit im Team: Der Content-Manager kann sich auf den Inhalt und die HTML-Struktur konzentrieren, während der Designer im CSS arbeitet, ohne Gefahr zu laufen, die inhaltliche Struktur zu beschädigen.

#### Ein Blick in die Praxis: Gut vs. Schlecht

Um den Unterschied greifbar zu machen, schauen wir uns ein einfaches Beispiel an: einen kleinen Blogbeitrag.

**Der "Div-Suppen"-Ansatz (die schlechte Methode)**

Früher, als die semantischen Möglichkeiten von HTML begrenzt waren, wurden Webseiten oft ausschließlich mit dem universalen `<div>`-Container gebaut. Das Ergebnis ist zwar optisch irgendwie machbar, aber strukturell eine Wüste – man nennt es abfällig "Div-Suppe".

```html
<div class="header">
  <div class="logo">Mein Blog</div>
  <div class="nav">
    <span>Home</span>
    <span>Über mich</span>
    <span>Kontakt</span>
  </div>
</div>

<div class="main-content">
  <div class="post-title">HTML ist das Fundament</div>
  <div class="post-meta">Veröffentlicht am 15. Oktober</div>
  <div class="post-body">
    Der erste Absatz über die Wichtigkeit von HTML. Es legt die Struktur fest...
  </div>
</div>

<div class="footer">
  © 2023 Mein Blog
</div>
```

Dieser Code *funktioniert* irgendwie, wenn man das passende CSS hinzufügt. Aber für eine Maschine ist er bedeutungslos. "header", "post-title" und "nav" sind nur beliebige Namen, die keine standardisierte Bedeutung haben. Es ist eine Ansammlung von Boxen ohne inneren Zusammenhang.

**Der semantische Ansatz (die richtige Methode)**

Mit modernem, semantischem HTML können wir denselben Inhalt so auszeichnen, dass seine Bedeutung sofort klar wird.

```html
<header>
  <p class="logo">Mein Blog</p>
  <nav>
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/ueber-mich">Über mich</a></li>
      <li><a href="/kontakt">Kontakt</a></li>
    </ul>
  </nav>
</header>

<main>
  <article>
    <h1>HTML ist das Fundament</h1>
    <p>Veröffentlicht am 15. Oktober</p>
    <p>
      Der erste Absatz über die Wichtigkeit von HTML. Es legt die Struktur fest...
    </p>
  </article>
</main>

<footer>
  <p>© 2023 Mein Blog</p>
</footer>
```

Dieser Code ist eine Offenbarung. Jedes Element erklärt sich selbst:
*   `<header>`: Der Kopfbereich der Seite.
*   `<nav>`: Ein Navigationsmenü. Die Liste `<ul>` signalisiert eine Gruppe zusammengehöriger Links.
*   `<main>`: Der einzigartige Hauptinhalt dieser Seite.
*   `<article>`: Ein in sich geschlossener, eigenständiger Inhalt – perfekt für einen Blogbeitrag.
*   `<h1>`: Die wichtigste Überschrift des Dokuments.
*   `<p>`: Ein Textabsatz.
*   `<footer>`: Der Fußbereich der Seite.

Dieser Code ist nicht nur für Menschen leichter lesbar, sondern gibt auch Screenreadern, Suchmaschinen und anderen Tools eine perfekte Blaupause deiner Seite. Sie wissen sofort, wo die Navigation ist, was der Hauptinhalt ist und wie dieser gegliedert ist.

#### Deine wichtigsten Werkzeuge für die Struktur

HTML5 hat eine ganze Reihe von semantischen Elementen eingeführt, die dir helfen, deine Seiten klar zu gliedern. Hier sind einige der wichtigsten:

*   **`<header>`**: Für den Kopfbereich einer Seite oder eines Abschnitts. Enthält oft das Logo, den Seitentitel und die Hauptnavigation.
*   **`<nav>`**: Umschließt die Hauptnavigationselemente.
*   **`<main>`**: Enthält den zentralen, einzigartigen Inhalt der Seite. Es sollte nur ein `<main>`-Element pro Seite geben.
*   **`<section>`**: Definiert einen thematischen Abschnitt innerhalb eines Dokuments, der typischerweise eine eigene Überschrift hat.
*   **`<article>`**: Für in sich geschlossene, potenziell wiederverwendbare Inhalte wie einen Blogbeitrag, einen Foren-Post oder einen Zeitungsartikel.
*   **`<aside>`**: Für Inhalte, die nur lose mit dem Hauptinhalt in Beziehung stehen, wie eine Seitenleiste (Sidebar) mit weiterführenden Links oder Werbung.
*   **`<footer>`**: Für den Fußbereich einer Seite oder eines Abschnitts. Enthält oft Copyright-Informationen, Kontaktlinks oder Impressum.
*   **`<h1>` - `<h6>`**: Für Überschriften. Ihre Hierarchie ist entscheidend: Die `<h1>` ist die Hauptüberschrift, `<h2>` sind Unterthemen davon, `<h3>` Unterthemen der `<h2>` und so weiter. Die Hierarchie sollte niemals aus rein visuellen Gründen übersprungen werden.

Die Beherrschung dieser Elemente ist der erste und wichtigste Schritt auf dem Weg zu einem professionellen Webentwickler. Bevor du auch nur eine Zeile CSS oder JavaScript schreibst, muss dein HTML-Dokument als reiner Text eine saubere, logische und semantisch korrekte Struktur aufweisen. Es ist das stabile Fundament, auf dem alles andere aufbaut. Ein wackeliges Fundament mag eine Weile halten, aber früher oder später wird das ganze Haus Risse bekommen. Nimm dir also die Zeit, deine Strukturen sorgfältig zu planen und mit den richtigen Werkzeugen zu bauen.
