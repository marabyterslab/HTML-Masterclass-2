# Pagination und Blättern

### Pagination und Blättern: Inhalte aufteilen und navigierbar machen

Stell dir vor, du betreibst einen Blog mit 500 Artikeln oder einen Onlineshop mit 2000 Produkten. Würdest du all diese Inhalte auf einer einzigen, endlos langen Seite anzeigen? Wahrscheinlich nicht. Die Seite würde ewig laden, wäre unübersichtlich und für deine Besucher eine echte Geduldsprobe. Genau hier kommt die Pagination, auch Blättern oder Paginierung genannt, ins Spiel. Sie ist eine der fundamentalsten Navigationsformen im Web und dient dazu, große Mengen zusammengehöriger Inhalte in überschaubare, leicht verdauliche "Seiten" aufzuteilen.

Das Ziel ist klar: eine bessere Benutzererfahrung und eine optimierte Ladezeit. Statt alles auf einmal zu laden, präsentierst du nur einen kleinen Teil – zum Beispiel 10 Produkte oder 12 Blogartikel – und bietest eine klare Navigation an, um zu den nächsten oder vorherigen Inhalten zu gelangen.

#### Die semantische Grundlage: HTML für die Seitensteuerung

Eine Paginierung ist im Kern nichts anderes als eine Gruppe von Links. Und wie du bereits weißt, ist es entscheidend, solche Navigationselemente semantisch korrekt auszuzeichnen. Das hilft nicht nur Suchmaschinen, die Struktur deiner Seite zu verstehen, sondern ist auch für die Barrierefreiheit, insbesondere für Nutzer von Screenreadern, unerlässlich.

Die robusteste und am weitesten verbreitete Methode, eine Paginierung in HTML aufzubauen, folgt einer klaren Struktur:

1.  Ein `<nav>`-Element umschließt die gesamte Navigation. Dadurch wird signalisiert: Hier befindet sich ein wichtiger Navigationsblock.
2.  Innerhalb des `<nav>`-Elements verwenden wir eine ungeordnete Liste (`<ul>`). Eine Liste ist perfekt geeignet, da die Seitenzahlen eine Sammlung zusammengehöriger Navigationselemente darstellen.
3.  Jeder einzelne Navigationspunkt (also jede Seitenzahl, der "Weiter"-Button etc.) wird zu einem Listenelement (`<li>`).
4.  Innerhalb des Listenelements befindet sich der eigentliche Link (`<a>`), der zur entsprechenden Seite führt.

Schauen wir uns ein minimales Grundgerüst an:

```html
<nav aria-label="Seitennavigation">
  <ul>
    <li><a href="/artikel?seite=1">1</a></li>
    <li><a href="/artikel?seite=2">2</a></li>
    <li><a href="/artikel?seite=3">3</a></li>
    <li><a href="/artikel?seite=4">4</a></li>
  </ul>
</nav>
```

In diesem einfachen Beispiel siehst du die grundlegende Struktur. Das `aria-label`-Attribut im `<nav>`-Tag ist ein wichtiger Zusatz für die Barrierefreiheit. Es gibt dem Navigationsblock einen aussagekräftigen Namen ("Seitennavigation"), den Screenreader vorlesen können. Ohne dieses Label wüsste ein blinder Nutzer nur, dass eine Navigation beginnt, aber nicht, wofür sie dient.

#### Ein vollständiges Paginierungs-Element erstellen

In der Praxis besteht eine Paginierung aus mehr als nur ein paar Seitenzahlen. Übliche Komponenten sind:

*   **"Zurück"- und "Weiter"-Links:** Diese ermöglichen eine schnelle lineare Navigation, ohne eine bestimmte Seitenzahl anklicken zu müssen.
*   **Kennzeichnung der aktiven Seite:** Die aktuelle Seite, auf der sich der Nutzer befindet, sollte klar erkennbar und idealerweise nicht klickbar sein.
*   **Auslassungspunkte ("…"):** Bei einer sehr großen Anzahl von Seiten ist es nicht sinnvoll, alle Zahlen anzuzeigen. Auslassungspunkte deuten an, dass es weitere, nicht direkt angezeigte Seiten gibt.
*   **Links zur ersten und letzten Seite:** Diese sind hilfreich, um schnell an den Anfang oder das Ende der Inhaltsliste zu springen.

Lass uns unser Grundgerüst zu einem vollständigen, praxisnahen Beispiel ausbauen:

```html
<nav aria-label="Blog-Seitennavigation">
  <ul>
    <!-- "Zurück"-Link, eventuell deaktiviert auf der ersten Seite -->
    <li><a href="/blog?seite=2" aria-label="Zurück zur vorherigen Seite">&laquo;</a></li>

    <!-- Link zur ersten Seite -->
    <li><a href="/blog?seite=1">1</a></li>
    
    <!-- Aktuelle Seite -->
    <li><a href="/blog?seite=2" aria-current="page">2</a></li>

    <!-- Weitere Seiten -->
    <li><a href="/blog?seite=3">3</a></li>
    <li><a href="/blog?seite=4">4</a></li>

    <!-- Auslassungspunkt -->
    <li class="disabled" aria-hidden="true"><span>…</span></li>

    <!-- Link zur letzten Seite -->
    <li><a href="/blog?seite=25">25</a></li>

    <!-- "Weiter"-Link -->
    <li><a href="/blog?seite=3" aria-label="Weiter zur nächsten Seite">&raquo;</a></li>
  </ul>
</nav>
```

Analysieren wir die wichtigen Ergänzungen in diesem Code:

*   **`aria-label` für Pfeile:** Die Symbole `&laquo;` ( « ) und `&raquo;` ( » ) sind visuell verständlich, aber für einen Screenreader nicht aussagekräftig. Mit `aria-label="Zurück zur vorherigen Seite"` geben wir diesen Links eine klare, verständliche Beschreibung.
*   **`aria-current="page"` für die aktive Seite:** Dies ist der moderne und semantisch korrekte Weg, die aktuelle Seite zu kennzeichnen. Das `aria-current`-Attribut teilt assistiven Technologien explizit mit: "Dies ist der Link für die Seite, auf der du dich gerade befindest." Browser können dieses Attribut auch für das Styling mit CSS nutzen. Oft wird der Link der aktuellen Seite auch durch ein `<span>`- oder `<strong>`-Element ersetzt, um ihn nicht klickbar zu machen. Die Variante mit `<a>` und `aria-current` ist jedoch oft vorzuziehen, da sie die visuelle Konsistenz wahrt und von Screenreadern besser interpretiert wird.
*   **Auslassungspunkte:** Der Auslassungspunkt (`…`) ist in ein `<span>` innerhalb eines `<li>` gepackt. Er ist rein visuell und hat keine Funktion, weshalb wir ihn für Screenreader mit `aria-hidden="true"` ausblenden können. Eine CSS-Klasse wie `.disabled` kann genutzt werden, um ihn optisch von den klickbaren Elementen abzuheben.

Die URLs in den `href`-Attributen (`/blog?seite=2`) sind typische Beispiele. Hier wird über einen URL-Parameter (`?seite=`) die gewünschte Seitenzahl an den Server übermittelt, der dann die entsprechenden Inhalte ausliefert. Die genaue Implementierung hängt von der serverseitigen Technologie (z.B. PHP, Python, Node.js) ab, aber die HTML-Struktur bleibt dieselbe.

#### Gestaltung mit CSS: Vom Listenpunkt zur Navigationsleiste

Ohne CSS wäre unsere Paginierung nur eine schnöde Liste untereinander. Die Magie passiert erst, wenn wir sie gestalten. Das grundlegende Ziel ist es, die Listenelemente horizontal nebeneinander anzuordnen und ihnen ein klares, klickbares Aussehen zu geben.

Mit modernen CSS-Techniken wie Flexbox ist das ein Kinderspiel.

```css
/* Grundlegende Gestaltung für den Navigations-Container */
.pagination-nav ul {
  display: flex; /* Ordnet die Listenelemente horizontal an */
  padding-left: 0;
  list-style: none; /* Entfernt die Aufzählungspunkte */
  gap: 8px; /* Fügt einen kleinen Abstand zwischen den Elementen hinzu */
}

/* Styling für die einzelnen Links */
.pagination-nav ul li a,
.pagination-nav ul li span {
  display: block;
  padding: 10px 15px;
  border: 1px solid #ddd;
  text-decoration: none;
  color: #007bff;
  background-color: #fff;
  border-radius: 4px;
  transition: background-color 0.2s, color 0.2s;
}

/* Hover-Effekt für klickbare Links */
.pagination-nav ul li a:hover {
  background-color: #f0f0f0;
}

/* Styling für die aktive Seite, basierend auf dem ARIA-Attribut */
.pagination-nav ul li a[aria-current="page"] {
  background-color: #007bff;
  color: #fff;
  border-color: #007bff;
  font-weight: bold;
  cursor: default; /* Zeigt an, dass dieses Element nicht klickbar ist */
}

/* Styling für deaktivierte Elemente wie die Auslassungspunkte */
.pagination-nav ul li.disabled span {
  color: #6c757d;
  background-color: transparent;
  border-color: transparent;
}
```

Um diesen CSS-Code anzuwenden, müsstest du deinem `<nav>`-Element natürlich noch die entsprechende Klasse geben: `<nav class="pagination-nav" ...>`.

Dieses CSS-Beispiel zeigt, wie die Trennung von Inhalt (HTML) und Präsentation (CSS) funktioniert. Das HTML gibt die Struktur und Bedeutung vor, während das CSS für das gesamte Erscheinungsbild verantwortlich ist. Besonders hervorzuheben ist der Selektor `a[aria-current="page"]`. Er greift direkt auf das Attribut zu, das wir für die Barrierefreiheit hinzugefügt haben. Das ist ein perfektes Beispiel dafür, wie semantisches, barrierefreies HTML auch die CSS-Gestaltung vereinfachen kann.

#### Alternativen zur klassischen Pagination

Obwohl die klassische Seitennavigation bewährt und weit verbreitet ist, gibt es je nach Anwendungsfall auch andere Ansätze, um große Datenmengen darzustellen:

*   **"Mehr laden"-Button:** Statt Seitenzahlen gibt es am Ende der Liste einen Button ("Weitere Produkte laden"). Bei einem Klick werden die nächsten Inhaltselemente dynamisch per JavaScript nachgeladen und an die bestehende Liste angehängt. Dies vermeidet einen kompletten Seiten-Neuladevorgang.
*   **Unendliches Scrollen (Infinite Scrolling):** Hier werden neue Inhalte automatisch nachgeladen, sobald der Nutzer das Ende der sichtbaren Liste erreicht. Dies ist typisch für soziale Medien-Feeds (z.B. Instagram, X). Der Vorteil ist ein nahtloses Browsing-Erlebnis. Der Nachteil: Es gibt kein klares Ende, der Footer der Seite ist oft schwer erreichbar, und es kann schwierig sein, einen bestimmten Inhalt wiederzufinden.

Für Anwendungsfälle, in denen Nutzer gezielt nach Informationen suchen (z.B. in einem Onlineshop, einem Archiv oder bei Suchergebnissen), ist die klassische Pagination oft die überlegene Methode. Sie gibt dem Nutzer ein Gefühl für den Umfang der Gesamtdatenmenge und ermöglicht es ihm, direkt zu einer bestimmten Seite zu springen. Die Kontrolle bleibt vollständig beim Nutzer – und das ist ein zentraler Aspekt einer guten User Experience.
