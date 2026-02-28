# Sichtbarer Inhalt der Seite

### Sichtbarer Inhalt der Seite: Der `<body>`-Bereich

Nachdem wir uns mit der grundlegenden Struktur eines HTML-Dokuments und dem unsichtbaren `<head>`-Bereich beschäftigt haben, kommen wir nun zum Herzstück jeder Webseite: dem `<body>`-Bereich. Stell dir deine HTML-Datei wie ein Theater vor. Der `<head>` ist der Backstage-Bereich – hier liegen die Skripte, die Regieanweisungen und die Informationen über die Schauspieler. Wichtig, aber für das Publikum unsichtbar. Der `<body>` hingegen ist die Bühne selbst. Alles, was du innerhalb des `<body>`-Tags platzierst, ist das, was dein Publikum – die Besucher deiner Webseite – am Ende im Browserfenster zu sehen bekommt.

Der `<body>`-Tag umschließt den gesamten sichtbaren Inhalt einer HTML-Seite. Es gibt ihn pro Dokument genau einmal, und er befindet sich direkt nach dem schließenden `</head>`-Tag.

Ein minimales, aber vollständiges HTML-Gerüst sieht also so aus:

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Der Titel im Browser-Tab</title>
</head>
<body>
  <!-- Hier spielt die Musik! Alle Texte, Bilder, Videos und Links kommen hier hinein. -->
  <h1>Hallo Welt!</h1>
  <p>Dies ist der erste sichtbare Absatz auf meiner Seite.</p>
</body>
</html>
```

Innerhalb des `<body>` verwenden wir eine Vielzahl von HTML-Elementen, um unsere Inhalte zu strukturieren und ihnen eine Bedeutung zu geben. Diese Elemente lassen sich grob in verschiedene Kategorien einteilen.

#### Textstrukturierung: Die Grundlagen

Die häufigste Form von Inhalt im Web ist Text. HTML gibt uns mächtige Werkzeuge an die Hand, um diesen Text nicht nur darzustellen, sondern ihm auch eine logische Hierarchie und Bedeutung zu verleihen.

**Überschriften (`<h1>` bis `<h6>`)**

Überschriften sind das Rückgrat deiner Inhaltsstruktur. Sie gliedern deine Seite in logische Abschnitte und sind essenziell für die Lesbarkeit – sowohl für Menschen als auch für Suchmaschinen. Stell sie dir wie die Kapitel- und Abschnittsüberschriften in einem Buch vor.

- `<h1>`: Die Hauptüberschrift der Seite. Es sollte pro Seite nur eine einzige `<h1>` geben. Sie beschreibt das zentrale Thema des Dokuments.
- `<h2>`: Unterüberschriften, die die Hauptthemen der Seite gliedern.
- `<h3>` bis `<h6>`: Dienen der weiteren Untergliederung.

Wichtig ist hierbei die Hierarchie. Du solltest keine Ebenen überspringen, also nicht von einer `<h2>` direkt zu einer `<h4>` springen. Die visuelle Darstellung (Schriftgröße, Fettdruck) wird vom Browser standardmäßig festgelegt, aber du solltest Überschriften niemals nur wegen ihres Aussehens wählen. Ihre primäre Aufgabe ist die Strukturierung. Das Design übernimmst du später mit CSS.

```html
<body>
  <h1>Die Kunst des Kaffeekochens</h1>
  <p>Eine Einführung in die Welt des Kaffees.</p>
  
  <h2>Wahl der richtigen Bohne</h2>
  <p>Hier erfährst du alles über Arabica und Robusta.</p>
  
  <h3>Arabica: Die Feinschmeckerbohne</h3>
  <p>Details zu den feinen Aromen...</p>
  
  <h2>Die Zubereitungsmethoden</h2>
  <p>Von der French Press bis zum Siebträger.</p>
</body>
```

**Absätze (`<p>`)**

Der `<p>`-Tag (Paragraph) ist das Arbeitspferd für Fließtext. Jeder Absatz, den du schreibst, sollte von `<p>`-Tags umschlossen sein. Der Browser fügt dann automatisch einen visuellen Abstand zwischen den Absätzen ein, was die Lesbarkeit enorm verbessert.

**Hervorhebungen (`<strong>` und `<em>`)**

Manchmal möchtest du bestimmte Wörter oder Sätze im Text hervorheben. Dafür gibt es semantische Tags:

- `<strong>`: Kennzeichnet Inhalt von großer Wichtigkeit, Dringlichkeit oder Ernsthaftigkeit. Browser stellen dies standardmäßig fett dar. Es signalisiert: "Dieser Teil ist wirklich wichtig!"
- `<em>`: Kennzeichnet eine Betonung (Emphasis), die die Bedeutung eines Satzes verändert. Browser stellen dies standardmäßig kursiv dar. Es ist vergleichbar mit einer betonten Aussprache.

Beispiel:
```html
<p>Du musst den <strong>roten</strong> Knopf unter keinen Umständen drücken.</p>
<p>Ich bin <em>wirklich</em> überrascht, dich hier zu sehen.</p>
```
Früher wurden hierfür die Tags `<b>` (bold) und `<i>` (italic) verwendet. Diese beschreiben aber nur das Aussehen und tragen keine semantische Bedeutung. `<strong>` und `<em>` sind die moderne und korrekte Wahl, da sie die *Bedeutung* des Inhalts beschreiben, nicht seine Präsentation.

#### Listen, Bilder und Links

Neben reinem Text besteht eine Webseite natürlich aus weiteren Elementen.

**Listen (`<ul>`, `<ol>`, `<li>`)**

Listen sind perfekt, um Informationen übersichtlich zu gruppieren.
- `<ul>` (Unordered List): Eine ungeordnete Liste für Aufzählungen, bei denen die Reihenfolge keine Rolle spielt. Die einzelnen Punkte werden meist mit einem Aufzählungszeichen dargestellt.
- `<ol>` (Ordered List): Eine geordnete Liste für Anleitungen oder Ranglisten, bei denen die Reihenfolge wichtig ist. Die Punkte werden automatisch nummeriert.
- `<li>` (List Item): Jeder einzelne Punkt in einer Liste, egal ob geordnet oder ungeordnet, wird mit einem `<li>`-Tag umschlossen.

```html
<h2>Einkaufsliste</h2>
<ul>
  <li>Milch</li>
  <li>Eier</li>
  <li>Brot</li>
</ul>

<h2>Anleitung: Tee kochen</h2>
<ol>
  <li>Wasser zum Kochen bringen.</li>
  <li>Teebeutel in eine Tasse geben.</li>
  <li>Heißes Wasser darübergießen.</li>
</ol>
```

**Bilder (`<img>`)**

Ein Bild sagt mehr als tausend Worte. Mit dem `<img>`-Tag bindest du Bilder in deine Seite ein. Dieses Tag ist ein sogenanntes "leeres" Element, es hat also kein schließendes Tag. Die wichtigsten Attribute sind:

- `src` (Source): Hier gibst du den Pfad zur Bilddatei an.
- `alt` (Alternative Text): Eine kurze Beschreibung des Bildinhalts. Dieser Text wird angezeigt, wenn das Bild nicht geladen werden kann, und ist unerlässlich für die Barrierefreiheit, da Screenreader ihn blinden oder sehbehinderten Nutzern vorlesen.

```html
<img src="bilder/sonnenuntergang.jpg" alt="Ein malerischer Sonnenuntergang am Meer">
```

**Links (`<a>`)**

Das World Wide Web lebt von Verknüpfungen. Der Anker-Tag `<a>` (Anchor) macht aus einem Text oder Bild einen klickbaren Hyperlink. Das entscheidende Attribut ist `href` (Hypertext Reference), das das Ziel des Links angibt.

```html
<p>Besuche unsere <a href="https://beispiel.com">Partner-Webseite</a> für mehr Informationen.</p>
```

#### Struktur schaffen: Von `<div>` zu semantischen Elementen

Bisher haben wir Elemente kennengelernt, die konkrete Inhalte repräsentieren. Aber wie ordnen wir diese Elemente zu größeren Blöcken an?

**Der generische Container: `<div>`**

Der `<div>`-Tag (Division) ist ein Block-Level-Container ohne eigene semantische Bedeutung. Seine einzige Aufgabe ist es, andere Elemente zu gruppieren. Du kannst ihn dir wie eine unsichtbare Box vorstellen, in die du zusammengehörige Inhalte packst, um sie später gemeinsam mit CSS zu gestalten oder mit JavaScript zu manipulieren.

```html
<div class="produkt-box">
  <h2>Premium-Kaffee</h2>
  <img src="kaffee.jpg" alt="Eine Tasse dampfender Kaffee">
  <p>Unser bester Kaffee aus fairem Anbau.</p>
  <a href="/kaufen">Jetzt kaufen</a>
</div>
```

**Die Revolution: Semantische HTML5-Elemente**

Während `<div>` extrem nützlich ist, sagt es nichts über die Art des Inhalts aus. HTML5 hat eine Reihe von neuen Elementen eingeführt, die `<div>` in vielen Fällen ersetzen und dem Browser sowie Suchmaschinen klare Hinweise auf die Struktur deiner Seite geben. Sie funktionieren wie `<div>`-Container, haben aber eine Bedeutung.

- `<header>`: Definiert den Kopfbereich einer Seite oder eines Abschnitts. Hier findest du oft das Logo, den Seitentitel und die Hauptnavigation.
- `<nav>`: Umschließt die primären Navigationslinks deiner Webseite.
- `<main>`: Beinhaltet den einzigartigen Hauptinhalt der Seite. Inhalte wie Header, Footer oder Seitenleisten gehören hier nicht hinein. Es sollte nur ein `<main>`-Element pro Seite geben.
- `<section>`: Gruppiert thematisch zusammengehörige Inhalte, typischerweise mit einer eigenen Überschrift. Stell es dir wie ein Kapitel in einem Buch vor.
- `<article>`: Repräsentiert einen in sich geschlossenen, unabhängigen Inhalt, der auch für sich allein stehen könnte, z. B. ein Blogbeitrag, ein Zeitungsartikel oder ein Forumspost.
- `<aside>`: Für Inhalte, die nur lose mit dem Hauptinhalt in Verbindung stehen, wie eine Seitenleiste (Sidebar) mit weiterführenden Links, Werbung oder einer Autorenbiografie.
- `<footer>`: Definiert den Fußbereich einer Seite oder eines Abschnitts. Hier stehen typischerweise Copyright-Informationen, Kontaktadressen oder Links zu Impressum und Datenschutz.

Eine gut strukturierte Webseite könnte so aussehen:

```html
<body>

  <header>
    <h1>Mein Blog</h1>
    <nav>
      <ul>
        <li><a href="/">Startseite</a></li>
        <li><a href="/ueber-mich">Über mich</a></li>
        <li><a href="/kontakt">Kontakt</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <h2>Meine erste Reise</h2>
      <p>Der erste Absatz meines Reiseberichts...</p>
      <section>
        <h3>Tag 1: Ankunft</h3>
        <p>Details über den ersten Tag...</p>
      </section>
      <section>
        <h3>Tag 2: Erkundung</h3>
        <p>Details über den zweiten Tag...</p>
      </section>
    </article>
    
    <aside>
      <h3>Beliebte Beiträge</h3>
      <ul>
        <li><a href="#">Reise nach Italien</a></li>
        <li><a href="#">Tipps für Backpacker</a></li>
      </ul>
    </aside>
  </main>
  
  <footer>
    <p>&copy; 2023 Mein Blog. Alle Rechte vorbehalten.</p>
  </footer>

</body>
```
Dieser Code ist nicht nur für Menschen leichter zu lesen, sondern auch für Maschinen. Ein Screenreader kann einem Nutzer nun ansagen: "Navigation", "Hauptinhalt" oder "Fußzeile", was die Orientierung auf der Seite erheblich erleichtert.

Der `<body>` ist also weit mehr als nur ein weißes Blatt Papier. Er ist eine strukturierte Leinwand, auf der du mit Hilfe semantischer HTML-Elemente eine klare, verständliche und zugängliche Geschichte für deine Besucher und für die Technologien des Webs erzählst.
