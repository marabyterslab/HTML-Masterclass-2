# Sichtbarer Inhalt der Seite

### Der `<body>`: Die Bühne für deinen Inhalt

Wenn das `<head>`-Element die Backstage-Crew deines Web-Projekts ist – die unsichtbaren Helfer, die alles vorbereiten –, dann ist das `<body>`-Element die große Bühne. Alles, was ein Besucher deiner Webseite sieht, hört und womit er interagiert, befindet sich hier. Texte, Bilder, Videos, Links, Buttons, Formulare – der gesamte sichtbare und erlebbare Inhalt hat seinen Platz zwischen dem öffnenden `<body>` und dem schließenden `</body>`-Tag.

Stell dir eine leere HTML-Datei vor. Sie ist wie ein leeres Theater. Erst wenn du den Vorhang zum `<body>`-Bereich öffnest und die Bühne mit Schauspielern (Inhalten) und Kulissen (Strukturelementen) füllst, beginnt die Vorstellung für dein Publikum.

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Meine Webseite</title>
</head>
<body>
  <!-- Hier spielt die Musik! Alles, was der Nutzer sieht, kommt hier hinein. -->
</body>
</html>
```

Innerhalb des `<body>`-Elements verwendest du eine Vielzahl von HTML-Tags, um deinen Inhalt zu strukturieren und ihm Bedeutung zu verleihen. Diese Tags sind die fundamentalen Bausteine jeder Webseite. Lass uns die wichtigsten kennenlernen.

#### Die Grundbausteine des Inhalts

Bevor wir große Layout-Strukturen bauen, brauchen wir das Material dafür. Die folgenden Elemente sind das tägliche Brot der Webentwicklung und bilden die Basis für fast jeden Inhalt.

**Überschriften: `<h1>` bis `<h6>`**

Überschriften gliedern deinen Inhalt und schaffen eine visuelle und semantische Hierarchie. Stell sie dir wie die Kapitel- und Abschnittsüberschriften in einem Buch vor. Die `<h1>`-Überschrift ist die wichtigste und sollte in der Regel nur einmal pro Seite vorkommen – sie ist der Titel deiner Seite, wie der Buchtitel. Die folgenden Überschriften `<h2>` bis `<h6>` unterteilen den Inhalt in immer feinere Abschnitte.

Es geht hier nicht nur um die Schriftgröße, die der Browser standardmäßig vergibt. Suchmaschinen und Screenreader (Vorlese-Software für sehbehinderte Menschen) nutzen diese Hierarchie, um die Struktur und die Wichtigkeit der Inhalte zu verstehen.

```html
<body>
  <h1>Der Haupttitel der Seite</h1>
  <p>Ein kurzer einleitender Text.</p>
  
  <h2>Ein wichtiger Unterabschnitt</h2>
  <p>Text, der zu diesem Abschnitt gehört.</p>
  
  <h3>Ein Detailaspekt des Unterabschnitts</h3>
  <p>Noch mehr Text, der dieses Detail erklärt.</p>
  
  <h2>Ein weiterer wichtiger Unterabschnitt</h2>
  <p>Und so weiter...</p>
</body>
```

**Absätze: `<p>`**

Das `<p>`-Element (für "paragraph") ist das Arbeitstier für Fließtext. Jeder Textabsatz, den du auf deiner Seite siehst, sollte in einem `<p>`-Tag stehen. Browser fügen automatisch einen kleinen Abstand zwischen den Absätzen ein, was die Lesbarkeit enorm verbessert.

**Links: `<a>`**

Das World Wide Web wäre ohne Links nicht "wide". Das `<a>`-Element (für "anchor", also Anker) erzeugt einen Hyperlink. Sein wichtigstes Attribut ist `href` (Hypertext Reference), das die Zieladresse des Links angibt. Der Inhalt zwischen dem öffnenden und schließenden `<a>`-Tag ist der klickbare Teil.

```html
<p>Besuche unsere <a href="https://beispiel.de">Partnerseite</a> für weitere Informationen.</p>
```

**Bilder: `<img>`**

Bilder machen das Web lebendig. Das `<img>`-Element (für "image") ist ein sogenanntes leeres oder inhaltsloses Element, da es keinen schließenden Tag hat. Es benötigt zwei essenzielle Attribute:
*   `src` (source): Der Pfad zur Bilddatei.
*   `alt` (alternative text): Eine kurze Beschreibung des Bildinhalts. Dieser Text wird angezeigt, wenn das Bild nicht geladen werden kann, und ist entscheidend für die Barrierefreiheit, da Screenreader ihn vorlesen.

```html
<img src="bilder/sonnenuntergang.jpg" alt="Ein malerischer Sonnenuntergang am Meer">
```

**Listen: `<ul>`, `<ol>` und `<li>`**

Wenn du Informationen aufzählen möchtest, sind Listen das richtige Werkzeug. HTML unterscheidet zwei Haupttypen:
*   `<ul>` (unordered list): Eine unsortierte Liste, typischerweise mit Aufzählungszeichen (Bullet Points).
*   `<ol>` (ordered list): Eine sortierte, nummerierte Liste.

Jeder einzelne Punkt in einer Liste wird durch ein `<li>`-Element (list item) dargestellt.

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

#### Struktur für das große Ganze: Semantische Elemente

Eine Webseite besteht selten nur aus einer losen Ansammlung von Absätzen und Bildern. Sie hat eine klare Struktur: einen Kopfbereich, eine Navigation, einen Hauptinhaltsbereich und einen Fußbereich. Früher wurde dies alles mit generischen `<div>`-Boxen gebaut. Modernes HTML bietet jedoch semantische Elemente, die genau beschreiben, welche Art von Inhalt sich in ihnen befindet. Das macht deinen Code nicht nur für dich lesbarer, sondern auch für Maschinen verständlicher.

Stell dir deine Webseite wie ein Haus vor. Du könntest alle Räume einfach "Raum" nennen, aber es ist viel sinnvoller, sie als "Küche", "Wohnzimmer" und "Schlafzimmer" zu bezeichnen. Genau das tun semantische HTML-Elemente.

*   **`<header>`**: Der Kopfbereich einer Seite oder eines Abschnitts. Hier findest du typischerweise das Logo, den Seitentitel und vielleicht die Hauptnavigation. Nicht zu verwechseln mit dem `<head>`-Element!
*   **`<nav>`**: Definiert einen Block mit Navigationslinks. Eine Seite kann mehrere `<nav>`-Bereiche haben, zum Beispiel eine Hauptnavigation im Header und eine Sitemap im Footer.
*   **`<main>`**: Dieses Element sollte den Hauptinhalt deiner Seite umschließen. Der Inhalt innerhalb von `<main>` sollte einzigartig für diese spezifische Seite sein und nicht auf anderen Seiten wiederholt werden (wie z.B. die Navigation oder der Footer). Es sollte nur ein `<main>`-Element pro Seite geben.
*   **`<article>`**: Umschließt einen in sich geschlossenen, unabhängigen Inhalt, der auch für sich allein stehen könnte – wie ein Blogbeitrag, ein Zeitungsartikel oder ein Forumspost.
*   **`<section>`**: Gruppiert thematisch zusammengehörige Inhalte. Eine `section` hat typischerweise eine eigene Überschrift. Du könntest zum Beispiel eine Homepage in Sektionen wie "Über uns", "Unsere Produkte" und "Kundenstimmen" unterteilen.
*   **`<aside>`**: Beinhaltet Inhalte, die nur lose mit dem Hauptinhalt in Verbindung stehen, wie eine Seitenleiste (Sidebar) mit weiterführenden Links, Werbung oder einer Autorenbiografie.
*   **`<footer>`**: Der Fußbereich einer Seite oder eines Abschnitts. Hier stehen üblicherweise Copyright-Informationen, Kontaktadressen, Links zum Impressum und Datenschutz.

Ein typisches Layout mit diesen Elementen könnte so aussehen:

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
      <h2>Die Kunst des HTML</h2>
      <p>HTML ist mehr als nur eine Ansammlung von Tags...</p>
    </article>
    
    <article>
      <h2>Warum Semantik wichtig ist</h2>
      <p>Ein gut strukturierter Code ist die halbe Miete...</p>
    </article>
  </main>
  
  <aside>
    <h3>Neueste Beiträge</h3>
    <ul>
      <li><a href="#">Titel 1</a></li>
      <li><a href="#">Titel 2</a></li>
    </ul>
  </aside>

  <footer>
    <p>&copy; 2023 Mein Blog. Alle Rechte vorbehalten.</p>
  </footer>

</body>
```

#### Die Allzweck-Container: `<div>` und `<span>`

Manchmal gibt es für eine bestimmte Gruppierung von Elementen einfach kein passendes semantisches Tag. Für diese Fälle gibt es zwei neutrale Container, deren Hauptzweck es ist, Inhalte für Styling mit CSS oder für die Manipulation mit JavaScript zu bündeln.

*   **`<div>`**: Das `div`-Element (division) ist ein block-level Container. Das bedeutet, es erzeugt einen eigenen Block, der standardmäßig die gesamte verfügbare Breite einnimmt und einen Zeilenumbruch vor und nach sich erzwingt. Du nutzt es, um größere Bereiche zu gruppieren, für die es kein semantisches Äquivalent wie `<section>` oder `<article>` gibt. Zum Beispiel könntest du eine Gruppe aus einem Bild und einer Bildunterschrift in ein `<div>` packen, um sie gemeinsam zu gestalten.

*   **`<span>`**: Das `span`-Element ist ein inline Container. Im Gegensatz zum `<div>` erzeugt es keinen Zeilenumbruch und fügt sich nahtlos in den Textfluss ein. Du verwendest es, um kleine Teile innerhalb eines Textes zu markieren, zum Beispiel ein einzelnes Wort, um es farblich hervorzuheben oder ihm eine spezielle Schriftart zuzuweisen.

```html
<div class="product-card">
  <h2>Ein tolles Produkt</h2>
  <p>
    Dieses Produkt ist wirklich <span class="highlight">außergewöhnlich</span>. 
    Kaufe es jetzt!
  </p>
</div>
```

Der `<body>` ist also weit mehr als nur ein Behälter. Er ist der Raum, in dem du mit einer durchdachten Kombination aus semantischen Strukturelementen und fundamentalen Inhalts-Tags eine verständliche, zugängliche und ansprechende Benutzererfahrung schaffst. Jedes Element, das du hier platzierst, trägt zur Geschichte bei, die deine Webseite erzählt.
