# Pagination und Blättern

### Pagination und Blättern: Inhalte aufteilen und navigierbar machen

Stell dir vor, du besuchst einen Online-Shop mit Tausenden von Produkten oder einen Blog mit Hunderten von Artikeln. Würden all diese Inhalte auf einer einzigen, endlos langen Seite geladen, wäre das eine Katastrophe – sowohl für die Ladezeit deiner Webseite als auch für die Geduld deiner Besucher. Hier kommt die Pagination ins Spiel, eine fundamentale Technik, um große Datenmengen in verdauliche, überschaubare „Seiten“ aufzuteilten.

Pagination ist mehr als nur eine technische Notwendigkeit; sie ist ein entscheidendes Navigationselement, das dem Nutzer Orientierung, Kontrolle und ein Gefühl für den Umfang des Inhalts gibt. Anstatt von einer riesigen Informationsflut erschlagen zu werden, kann der Nutzer gezielt von Seite zu Seite blättern, ähnlich wie in einem Buch oder Katalog.

#### Warum Pagination unverzichtbar ist

Bevor wir uns die technische Umsetzung in HTML ansehen, lass uns kurz die drei Hauptgründe verstehen, warum Pagination so wichtig ist:

1.  **Performance:** Das Laden von 10 oder 20 Elementen pro Seite ist deutlich schneller als das Laden von 1000 Elementen auf einmal. Das reduziert die Serverlast und sorgt für eine schnelle, reaktionsfähige Benutzererfahrung, was besonders auf mobilen Geräten mit langsamerer Internetverbindung entscheidend ist.
2.  **Benutzerfreundlichkeit (Usability):** Eine klare Seitenstruktur hilft Nutzern, sich zurechtzufinden. Sie können abschätzen, wie viele Inhalte es gibt, und gezielt zu einer bestimmten Seite springen. Die Position ist immer klar („Du befindest dich auf Seite 3 von 15“), was ein Gefühl von Kontrolle vermittelt.
3.  **Organisation:** Inhalte werden logisch gruppiert. Ein Nutzer kann sich besser an die Position eines bestimmten Artikels erinnern („Ich glaube, das war auf Seite 2 oder 3“), als wenn er durch eine endlose Liste scrollen müsste.

#### Die grundlegende HTML-Struktur einer Pagination

Im Kern ist eine Paginierung nichts anderes als eine Liste von Links. Daher ist die semantisch korrekteste Art, sie in HTML abzubilden, eine Navigationsleiste (`<nav>`), die eine geordnete oder ungeordnete Liste (`<ol>` oder `<ul>`) enthält. In den meisten Fällen wird eine ungeordnete Liste (`<ul>`) verwendet, da die Seitenzahlen zwar eine Reihenfolge haben, aber die Navigationselemente selbst nicht hierarchisch geordnet sind.

Jeder Link zu einer Seite wird als Listenelement (`<li>`) mit einem Anker-Tag (`<a>`) darin platziert.

Hier ist ein ganz einfaches, grundlegendes Beispiel für eine Pagination, die zu den ersten vier Seiten eines Blogs verlinkt. Angenommen, wir befinden uns gerade auf der zweiten Seite:

```html
<nav>
  <ul>
    <li><a href="blog-seite-1.html">1</a></li>
    <li><strong>2</strong></li>
    <li><a href="blog-seite-3.html">3</a></li>
    <li><a href="blog-seite-4.html">4</a></li>
  </ul>
</nav>
```

In diesem einfachen Beispiel haben wir die aktuelle Seite (Seite 2) nicht als Link, sondern als reinen Text dargestellt, der mit `<strong>` hervorgehoben ist. Das ist eine gängige Praxis, denn ein Link, der auf die Seite zeigt, auf der man sich bereits befindet, ist überflüssig und kann für Nutzer verwirrend sein.

#### Eine professionelle und zugängliche Pagination erstellen

Das obige Beispiel ist funktional, aber wir können es deutlich verbessern, insbesondere im Hinblick auf Semantik und Barrierefreiheit (Accessibility). Eine professionelle Pagination berücksichtigt auch Nutzer, die auf Hilfstechnologien wie Screenreader angewiesen sind.

Lass uns unser Beispiel erweitern und bewährte Praktiken anwenden:

1.  **Das `<nav>`-Element mit `aria-label`:** Ein `<nav>`-Element signalisiert, dass es sich um einen Navigationsblock handelt. Wenn du mehrere `<nav>`-Elemente auf einer Seite hast (z. B. eine Hauptnavigation und eine Pagination), solltest du ihnen mit `aria-label` eine eindeutige Bezeichnung geben. Das hilft Screenreader-Nutzern zu verstehen, welchen Zweck die jeweilige Navigation erfüllt.

2.  **Die aktuelle Seite mit `aria-current` markieren:** Anstatt die aktuelle Seite einfach nur als Text darzustellen, ist es besser, sie ebenfalls als Link zu belassen (oder als Textelement), aber mit dem Attribut `aria-current="page"` zu versehen. Dieses ARIA-Attribut teilt assistiven Technologien explizit mit: „Dies ist die aktuell aktive Seite in diesem Navigationsset.“

3.  **„Vorwärts“- und „Zurück“-Links:** Fast jede Pagination hat Schaltflächen, um zur vorherigen oder nächsten Seite zu springen. Diese sind für eine flüssige Navigation unerlässlich.

4.  **Deaktivierte Zustände:** Wenn sich der Nutzer auf der ersten Seite befindet, sollte der „Zurück“-Link nicht klickbar sein. Befindet er sich auf der letzten Seite, gilt dasselbe für den „Weiter“-Link. Dies wird oft visuell durch eine andere Farbe (z. B. Grau) und durch die Entfernung der Klick-Funktionalität erreicht. Semantisch können wir hierfür ein `<span>`-Element anstelle eines `<a>`-Elements verwenden oder einem `<a>`-Element das Attribut `aria-disabled="true"` hinzufügen.

Sehen wir uns an, wie eine solche verbesserte Pagination aussehen könnte. Stell dir vor, wir haben 20 Seiten und befinden uns auf Seite 5.

```html
<nav aria-label="Seitenavigation der Suchergebnisse">
  <ul class="pagination">
    <!-- "Zurück"-Link -->
    <li class="page-item">
      <a class="page-link" href="/suche?seite=4">Zurück</a>
    </li>

    <!-- Link zur ersten Seite -->
    <li class="page-item">
      <a class="page-link" href="/suche?seite=1">1</a>
    </li>

    <!-- Auslassungszeichen -->
    <li class="page-item disabled">
      <span class="page-link">…</span>
    </li>

    <!-- Seiten um die aktuelle Seite herum -->
    <li class="page-item">
      <a class="page-link" href="/suche?seite=4">4</a>
    </li>
    <li class="page-item active">
      <a class="page-link" href="/suche?seite=5" aria-current="page">5</a>
    </li>
    <li class="page-item">
      <a class="page-link" href="/suche?seite=6">6</a>
    </li>

    <!-- Auslassungszeichen -->
    <li class="page-item disabled">
      <span class="page-link">…</span>
    </li>

    <!-- Link zur letzten Seite -->
    <li class="page-item">
      <a class="page-link" href="/suche?seite=20">20</a>
    </li>

    <!-- "Weiter"-Link -->
    <li class="page-item">
      <a class="page-link" href="/suche?seite=6">Weiter</a>
    </li>
  </ul>
</nav>
```

In diesem Code-Beispiel siehst du mehrere wichtige Konzepte in Aktion:
*   Das `aria-label` beschreibt den Zweck der Navigation klar.
*   Die aktuelle Seite (5) ist mit `aria-current="page"` markiert. CSS-Klassen wie `.active` werden oft zusätzlich für das visuelle Styling verwendet.
*   Auslassungszeichen (`…`), die in einem nicht klickbaren `<span>` stehen, deuten an, dass es weitere Seiten zwischen den angezeigten Zahlen gibt. Das hält die Navigationsleiste kompakt, selbst bei sehr vielen Seiten.
*   Die URLs verwenden Query-Parameter (`?seite=...`). Dies ist eine sehr gängige Methode, um paginierte Inhalte auf dynamischen Webseiten zu steuern. Der Server liest diesen Parameter aus und liefert die entsprechenden Inhalte.

#### `rel="next"` und `rel="prev"` für Suchmaschinen

Ein weiteres Detail, das oft übersehen wird, aber für die Suchmaschinenoptimierung (SEO) von Bedeutung ist, sind die `rel`-Attribute. Wenn du „Vorwärts“- und „Zurück“-Links hast, kannst du sie mit `rel="next"` und `rel="prev"` anreichern.

```html
<!-- Im Link, der zur nächsten Seite führt -->
<a href="/suche?seite=6" rel="next">Weiter</a>

<!-- Im Link, der zur vorherigen Seite führt -->
<a href="/suche?seite=4" rel="prev">Zurück</a>
```

Diese Attribute geben Suchmaschinen wie Google einen expliziten Hinweis auf die Beziehung zwischen den paginierten Seiten. Sie helfen dem Crawler zu verstehen, dass diese Seiten eine zusammenhängende Sequenz bilden, was die Indexierung verbessern und Probleme mit doppeltem Inhalt vermeiden kann.

#### Alternativen zur klassischen Pagination

Obwohl die klassische Seitennavigation die am weitesten verbreitete und oft auch die benutzerfreundlichste Methode ist, gibt es Alternativen, die je nach Anwendungsfall sinnvoll sein können:

*   **"Mehr laden"-Button:** Statt Seitenzahlen wird am Ende der Inhaltsliste ein Button angezeigt. Ein Klick darauf lädt per JavaScript die nächsten Elemente und hängt sie an die bestehende Liste an. Dies vermeidet einen kompletten Seiten-Neuladevorgang, kann aber die Orientierung erschweren, da es keine festen "Seiten" mehr gibt.
*   **Infinite Scrolling (Endloses Scrollen):** Hier werden neue Inhalte automatisch nachgeladen, sobald der Nutzer das Ende der Seite erreicht. Dies ist typisch für soziale Feeds (z. B. Instagram, Twitter), wo der Fokus auf dem schnellen Konsum von immer neuen Inhalten liegt. Der große Nachteil: Der Nutzer verliert komplett die Orientierung, kann sich keine Position merken und erreicht niemals eine Fußzeile.

Für Inhalte, bei denen Nutzer möglicherweise zurückkehren und etwas Bestimmtes wiederfinden möchten (z. B. in einem Forum, einem Produktkatalog oder einem Archiv), bleibt die klassische Pagination mit nummerierten Seiten die robusteste und verlässlichste Navigationsmethode. Sie basiert auf einfachen HTML-Links und funktioniert daher auch ohne JavaScript, was sie zu einer grundsoliden und zugänglichen Lösung macht. Deine Aufgabe als Webentwickler ist es, diese Links semantisch korrekt und barrierefrei zu strukturieren.
