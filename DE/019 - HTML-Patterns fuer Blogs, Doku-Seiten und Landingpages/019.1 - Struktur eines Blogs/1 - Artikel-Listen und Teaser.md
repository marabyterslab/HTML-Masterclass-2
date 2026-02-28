# Artikel-Listen und Teaser

### Artikel-Listen und Teaser: Das Herzstück deines Blogs

Besuchst du die Startseite eines Nachrichtenportals, eines Magazins oder eines Blogs, siehst du fast immer das gleiche Muster: eine Liste von Artikeln. Jeder Eintrag in dieser Liste gibt dir einen kleinen Vorgeschmack – einen Teaser – auf den vollständigen Inhalt und lädt dich zum Weiterlesen ein. Diese Übersichtsseiten sind das primäre Navigationsinstrument für deine Leser. Eine saubere, semantisch korrekte Struktur ist hier nicht nur eine technische Feinheit, sondern entscheidend für die Benutzerfreundlichkeit, Suchmaschinenoptimierung (SEO) und Barrierefreiheit.

Schauen wir uns an, wie du solche Listen und Teaser mit modernem HTML aufbaust.

#### Der einzelne Teaser als atomare Einheit

Bevor wir eine ganze Liste erstellen, zerlegen wir das Problem und konzentrieren uns auf das kleinste, aber wichtigste Element: einen einzelnen Artikel-Teaser. Ein Teaser ist eine in sich geschlossene Einheit. Er repräsentiert einen Beitrag und könnte theoretisch auch an anderer Stelle (z. B. in einem RSS-Feed oder auf einer Partnerseite) für sich allein stehen.

Genau für solche in sich geschlossenen, verteilbaren Inhalte gibt es in HTML das perfekte Element: `<article>`.

Ein typischer Teaser besteht aus mehreren Teilen:
*   Einer Überschrift, die meist auch der Link zum vollständigen Artikel ist.
*   Metadaten wie das Veröffentlichungsdatum, der Autor oder die Kategorien.
*   Einem Vorschaubild.
*   Einem kurzen Textauszug (Anrisstext oder Exzerpt).
*   Einem expliziten "Weiterlesen"-Link.

Setzen wir das in eine grundlegende HTML-Struktur um:

```html
<article class="post-teaser">
  <h2 class="post-teaser__title">
    <a href="/blog/die-kunst-des-minimalistischen-webdesigns">Die Kunst des minimalistischen Webdesigns</a>
  </h2>
  
  <p class="post-teaser__meta">
    Veröffentlicht am <time datetime="2023-10-26">26. Oktober 2023</time> von Alex Meier
  </p>
  
  <img src="/images/minimalist-design.jpg" alt="Ein aufgeräumter Schreibtisch mit Laptop und einer einzelnen Pflanze." class="post-teaser__image">
  
  <p class="post-teaser__excerpt">
    Minimalismus ist mehr als nur "weniger ist mehr". In diesem Artikel tauchen wir tief in die Prinzipien ein, die ein minimalistisches Design nicht nur schön, sondern auch unglaublich benutzerfreundlich machen.
  </p>
  
  <a href="/blog/die-kunst-des-minimalistischen-webdesigns" class="post-teaser__read-more">Weiterlesen</a>
</article>
```

Analysieren wir diese Struktur:

1.  **`<article>`**: Das Wurzelelement. Es signalisiert, dass alles darin eine eigenständige Einheit ist. Screenreader und Suchmaschinen verstehen sofort: "Hier beginnt ein Artikel."
2.  **`<h2>`**: Die Überschrift des Teasers. In der Hierarchie der Blog-Startseite, die vielleicht eine `<h1>` mit dem Titel "Unser Blog" hat, ist `<h2>` eine logische Wahl für die einzelnen Artikelüberschriften.
3.  **`<a>`**: Der Link umschließt den Text der Überschrift. Das ist ein gängiges und erwartetes Verhalten für Nutzer.
4.  **`<time>`**: Dieses semantische Element ist Gold wert. Während der Nutzer "26. Oktober 2023" liest, liefert das `datetime`-Attribut eine maschinenlesbare Version des Datums (`2023-10-26`). Das hilft Suchmaschinen, den Artikel chronologisch einzuordnen, und ermöglicht Browser-Erweiterungen, Kalendereinträge zu erstellen.
5.  **`<img>`**: Ein einfaches Bild. Der `alt`-Text ist hier unerlässlich, um den Inhalt des Bildes für sehbehinderte Nutzer und Suchmaschinen zu beschreiben.
6.  **`<p>`**: Absätze für die Metadaten und den Auszug halten den Text sauber strukturiert.

#### Vom Einzelstück zur Liste: Die Sammlung der Teaser

Ein einzelner Teaser macht noch keine Blog-Startseite. Wir brauchen eine Liste von ihnen. Die naheliegende, aber oft übersehene HTML-Struktur dafür ist eine tatsächliche Liste. Du hast die Wahl zwischen einer ungeordneten Liste (`<ul>`) für eine chronologische oder thematische Auflistung und einer geordneten Liste (`<ol>`) für eine Rangliste (z. B. "Die 10 beliebtesten Artikel").

Für eine typische Blog-Übersicht ist `<ul>` die semantisch korrekteste Wahl. Jeder Artikel-Teaser wird zu einem Listenelement (`<li>`).

Das Ganze wird oft von einem `<section>`-Element umschlossen, das die gesamte Artikelliste als einen zusammengehörigen Bereich der Seite definiert.

```html
<section aria-labelledby="blog-section-title">
  <h2 id="blog-section-title">Neueste Beiträge</h2>
  
  <ul class="post-list">
    
    <li class="post-list__item">
      <article class="post-teaser">
        <!-- Kompletter Teaser von oben -->
        <h3 class="post-teaser__title">
          <a href="/blog/die-kunst-des-minimalistischen-webdesigns">Die Kunst des minimalistischen Webdesigns</a>
        </h3>
        <p class="post-teaser__meta">
          Veröffentlicht am <time datetime="2023-10-26">26. Oktober 2023</time>
        </p>
        <!-- ... Rest des Teasers ... -->
      </article>
    </li>
    
    <li class="post-list__item">
      <article class="post-teaser">
        <h3 class="post-teaser__title">
          <a href="/blog/css-grid-verstehen">CSS Grid in 10 Minuten verstehen</a>
        </h3>
        <p class="post-teaser__meta">
          Veröffentlicht am <time datetime="2023-10-22">22. Oktober 2023</time>
        </p>
        <!-- ... Rest des Teasers ... -->
      </article>
    </li>

    <!-- Weitere Listenelemente ... -->

  </ul>
</section>
```

Was ist hier neu und wichtig?

*   **`<section>`**: Gruppiert den gesamten Bereich. Das `aria-labelledby`-Attribut verknüpft die Sektion programmatisch mit ihrer Überschrift (`<h2>`). Das ist ein Pluspunkt für die Barrierefreiheit, da Screenreader-Nutzer so den Kontext des Bereichs besser verstehen.
*   **`<ul>` und `<li>`**: Diese Struktur kommuniziert klar: "Es folgt eine Liste von gleichartigen Elementen." Ein Screenreader würde ankündigen: "Liste mit 2 Elementen." Würdest du stattdessen nur `<div>`-Elemente verwenden, ginge diese wertvolle semantische Information verloren.
*   **Überschriften-Hierarchie**: Beachte, dass die Überschrift innerhalb des `<article>` nun zu einer `<h3>` geworden ist. Wenn die gesamte Sektion eine `<h2>` ("Neueste Beiträge") hat, ist es logisch, dass die Überschriften der untergeordneten Artikel eine Ebene tiefer (`<h3>`) angesiedelt sind. Eine korrekte Überschriften-Hierarchie ist für die Gliederung und Navigation einer Seite unerlässlich.

#### Fortgeschrittene Muster und bewährte Praktiken

Die obige Struktur ist ein solides, semantisches Fundament. Darauf aufbauend gibt es einige verbreitete Muster, die die Benutzererfahrung weiter verbessern.

##### Die klickbare Karte

Modernes Design favorisiert oft "Karten" (Cards), bei denen der gesamte Teaser-Bereich klickbar ist, nicht nur die Überschrift oder der "Weiterlesen"-Link. Die intuitive, aber problematische Umsetzung wäre, das gesamte `<article>`-Element in ein `<a>`-Tag zu packen. Obwohl dies in HTML5 technisch valide ist, führt es oft zu Problemen bei der Barrierefreiheit, da verschachtelte interaktive Elemente (falls du später z.B. klickbare Tags einfügst) schwierig zu bedienen sind.

Eine elegantere und robustere Methode trennt Struktur (HTML) und Verhalten (CSS/JS). Der Link bleibt im HTML nur an der wichtigsten Stelle: der Überschrift. Mit CSS können wir diesen Link dann so gestalten, dass er die gesamte Fläche der Karte einnimmt.

Hier ist das HTML dafür. Es ist fast identisch mit unserem Original, was seine Stärke beweist:

```html
<article class="post-teaser is-clickable">
  <h3 class="post-teaser__title">
    <a href="/blog/die-kunst-des-minimalistischen-webdesigns">
      Die Kunst des minimalistischen Webdesigns
      <!-- Der Link wird per CSS über die ganze Karte gespannt -->
    </a>
  </h3>
  <p class="post-teaser__meta">...</p>
  <!-- ... Rest des Teasers ... -->
</article>
```

Der Trick liegt im CSS. Du würdest dem `<article>`-Element `position: relative` geben und dem `<a>`-Tag `position: absolute` zusammen mit `top: 0; left: 0; width: 100%; height: 100%;`. Ein Pseudo-Element (`::after`) auf dem Link kann hier helfen, die Klickfläche zu erzeugen, ohne das Layout des Textes zu beeinflussen. Der entscheidende Punkt ist: Das HTML bleibt sauber und semantisch, während das visuelle Verhalten eine reine Stil-Angelegenheit wird.

##### Semantische Gruppierung von Metadaten

Unser Beispiel packt die Metadaten in einen einfachen `<p>`-Tag. Das ist in Ordnung, aber wir können es noch besser machen. Ein `<article>` kann, genau wie eine `<body>`, einen eigenen `<header>` und `<footer>` haben.

*   Der `<header>` eines Artikels enthält typischerweise die primären Informationen wie die Überschrift und das Veröffentlichungsdatum.
*   Der `<footer>` eignet sich hervorragend für sekundäre Informationen wie Kategorien, Tags oder den Autor.

So könnte ein verfeinerter Teaser aussehen:

```html
<article class="post-teaser">
  <header class="post-teaser__header">
    <h3 class="post-teaser__title">
      <a href="/blog/die-kunst-des-minimalistischen-webdesigns">Die Kunst des minimalistischen Webdesigns</a>
    </h3>
    <p class="post-teaser__meta">
      Veröffentlicht am <time datetime="2023-10-26">26. Oktober 2023</time>
    </p>
  </header>
  
  <div class="post-teaser__content">
    <img src="/images/minimalist-design.jpg" alt="..." class="post-teaser__image">
    <p class="post-teaser__excerpt">
      Minimalismus ist mehr als nur "weniger ist mehr"...
    </p>
  </div>
  
  <footer class="post-teaser__footer">
    <p class="post-teaser__tags">
      Kategorien: <a href="/kategorie/design">Design</a>, <a href="/kategorie/webdev">WebDev</a>
    </p>
  </footer>
</article>
```
Diese Struktur ist noch ausdrucksstärker. Sie gruppiert zusammengehörige Informationen logisch und bietet klare Haken für das Styling mit CSS, ohne auf zu viele generische Klassen angewiesen zu sein. Die Verwendung von `<header>` und `<footer>` innerhalb eines `<article>` ist ein Zeichen für hochwertiges, durchdachtes HTML.
