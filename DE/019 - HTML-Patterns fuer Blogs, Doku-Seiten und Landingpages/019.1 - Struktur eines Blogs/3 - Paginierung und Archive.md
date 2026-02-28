# Paginierung und Archive

### Paginierung und Archive: Ordnung im Inhalts-Dschungel

Ein Blog lebt und wächst. Was mit einer Handvoll Artikel beginnt, kann schnell zu einer beachtlichen Sammlung von hunderten oder sogar tausenden Beiträgen anwachsen. In diesem Moment wird eine der wichtigsten Herausforderungen für dich als Entwickler sichtbar: Wie ermöglichst du es deinen Nutzern, diesen riesigen Berg an Informationen nicht nur zu konsumieren, sondern auch gezielt zu durchsuchen und zu entdecken?

Einfach alle Beiträge auf einer einzigen, endlos langen Seite aufzulisten, ist keine Lösung. Es wäre ein Albtraum für die Ladezeiten und würde jeden Besucher sofort überfordern. Stattdessen haben sich zwei grundlegende Muster etabliert, die Ordnung ins Chaos bringen und die Navigation durch umfangreiche Inhalte erst ermöglichen: die Paginierung und das Archiv. Beide dienen demselben Ziel, aber auf sehr unterschiedliche Weise.

#### Paginierung – Schritt für Schritt durch den Inhalt

Die Paginierung, auch Seitennummerierung genannt, ist dir mit Sicherheit schon unzählige Male im Web begegnet. Ob in Onlineshops, Suchergebnissen oder eben auf Blogs – sie ist das Standardwerkzeug, um eine lange Liste von Elementen in verdauliche, seitenweise Häppchen aufzuteilen.

Die Idee ist simpel: Anstatt alle 500 Blogbeiträge auf einmal anzuzeigen, zeigst du nur eine überschaubare Anzahl, zum Beispiel die zehn neuesten. Am Ende dieser Liste bietest du dem Nutzer dann Links an, um zur nächsten Seite (also zu den Beiträgen 11 bis 20), zur vorherigen oder zu einer ganz bestimmten Seite zu springen.

Die Vorteile liegen auf der Hand:
1.  **Performance:** Der Browser muss nur eine kleine Teilmenge der Daten laden und darstellen, was die Ladezeit der Seite drastisch verkürzt.
2.  **Benutzerfreundlichkeit (Usability):** Eine Liste von zehn Einträgen ist leicht zu überblicken. Der Nutzer wird nicht von einer endlosen Wand aus Text und Bildern erschlagen und kann sich auf den aktuellen Ausschnitt konzentrieren.

**Die semantische Umsetzung in HTML**

Eine Paginierung ist im Kern eine Navigationshilfe. Daher ist das `<nav>`-Element der perfekte semantische Container dafür. Es signalisiert sowohl dem Browser als auch assistiven Technologien wie Screenreadern, dass es sich hier um einen Block mit wichtigen Navigationslinks handelt.

Innerhalb des `<nav>`-Elements ist eine geordnete Liste (`<ol>`) die beste Wahl für die Seitenlinks. Warum eine geordnete Liste und keine ungeordnete (`<ul>`)? Weil die Seiten eine klare, logische und numerische Reihenfolge haben. Seite 2 folgt auf Seite 1, und Seite 3 folgt auf Seite 2. Eine `<ol>` spiegelt diese inhärente Ordnung semantisch korrekt wider.

Ein typisches und robustes HTML-Muster für eine Paginierung sieht so aus:

```html
<nav aria-label="Seitennavigation">
  <ol class="pagination">
    
    <!-- Link zur vorherigen Seite, oft nur angezeigt, wenn man nicht auf Seite 1 ist -->
    <li class="pagination__item">
      <a href="/blog/seite/1" class="pagination__link" aria-label="Vorherige Seite">«</a>
    </li>
    
    <!-- Link zur ersten Seite -->
    <li class="pagination__item">
      <a href="/blog/seite/1" class="pagination__link">1</a>
    </li>
    
    <!-- Aktuelle Seite: Kein Link, sondern nur Text, aber klar markiert -->
    <li class="pagination__item pagination__item--current">
      <span class="pagination__link" aria-current="page">2</span>
    </li>
    
    <!-- Link zur nächsten Seite -->
    <li class="pagination__item">
      <a href="/blog/seite/3" class="pagination__link">3</a>
    </li>

    <!-- Auslassungspunkte, wenn es viele Seiten gibt -->
    <li class="pagination__item pagination__item--disabled">
      <span class="pagination__link">…</span>
    </li>
    
    <!-- Link zur letzten Seite -->
    <li class="pagination__item">
      <a href="/blog/seite/25" class="pagination__link">25</a>
    </li>
    
    <!-- Link zur nächsten Seite, oft nur angezeigt, wenn man nicht auf der letzten Seite ist -->
    <li class="pagination__item">
      <a href="/blog/seite/3" class="pagination__link" aria-label="Nächste Seite">»</a>
    </li>
    
  </ol>
</nav>
```

Analysieren wir dieses Muster genauer:

*   **`<nav aria-label="Seitennavigation">`**: Der Container. Das `aria-label`-Attribut gibt dem Navigationsblock einen zugänglichen Namen, was besonders für Screenreader-Nutzer hilfreich ist, die so direkt wissen, um welche Art von Navigation es sich handelt.
*   **`<ol>`**: Die geordnete Liste, die die Reihenfolge der Seiten semantisch korrekt abbildet.
*   **`<li>` und `<a>`**: Jede klickbare Seitenzahl ist ein Listeneintrag mit einem Link darin.
*   **`aria-current="page"`**: Dies ist ein entscheidendes Detail für die Barrierefreiheit. Das Element, das die aktuelle Seite repräsentiert, ist kein Link – schließlich befindest du dich bereits dort. Es ist oft ein `<span>` oder `<strong>`. Mit `aria-current="page"` teilst du assistiven Technologien explizit mit: „Dies ist die aktuelle Seite in diesem Set.“
*   **Auslassungspunkte (`…`)**: Bei einer großen Anzahl von Seiten ist es nicht praktikabel, alle Seitenzahlen anzuzeigen. Ein Ellipsis-Symbol (`…`) zeigt an, dass Seiten übersprungen wurden. Es ist üblicherweise kein klickbares Element.
*   **Links für „Vorherige“ und „Nächste“**: Diese sind essenziell für eine flüssige Navigation. Symbole wie `«` und `»` oder Pfeile sind gängig. Ein `aria-label` ist hier wichtig, um die Funktion des Links eindeutig zu beschreiben, da das Symbol allein nicht für jeden verständlich ist.

Die Paginierung ist also die Methode der Wahl, wenn ein Nutzer linear und sequenziell durch eine große Menge gleichartiger Inhalte blättern möchte, ohne ein spezifisches Ziel vor Augen zu haben.

#### Archive – Die Bibliothek deines Blogs

Während die Paginierung einem Spaziergang auf einem langen Pfad gleicht, ist das Archiv eher wie eine Bibliothek mit verschiedenen Abteilungen. Es bietet alternative Wege, um Inhalte zu finden, meist basierend auf Metadaten wie dem Veröffentlichungsdatum, Kategorien oder Schlagwörtern (Tags). Archive sind nicht für das lineare Durchstöbern gedacht, sondern für das gezielte Auffinden von Beiträgen zu einem bestimmten Thema oder aus einem bestimmten Zeitraum.

Typischerweise findest du Archive in der Seitenleiste (`<aside>`) oder im Footer eines Blogs. Auch hier ist `<nav>` das semantisch korrekte Elternelement, da es sich um eine Form der Seitennavigation handelt.

**Das chronologische Archiv**

Die gängigste Form ist das Archiv, das nach Datum sortiert ist – meist nach Jahr und Monat. Es beantwortet die Frage eines Nutzers: „Was wurde im Mai 2023 geschrieben?“

Strukturell eignet sich hierfür eine verschachtelte, ungeordnete Liste (`<ul>`). Die erste Ebene repräsentiert die Jahre, die zweite Ebene die Monate innerhalb eines Jahres.

```html
<aside>
  <nav aria-labelledby="archive-heading">
    <h3 id="archive-heading">Archiv nach Monat</h3>
    <ul class="archive-list">
      <li>
        <span>2024</span>
        <ul class="archive-list__months">
          <li><a href="/archiv/2024/07">Juli (3)</a></li>
          <li><a href="/archiv/2024/06">Juni (5)</a></li>
          <li><a href="/archiv/2024/05">Mai (2)</a></li>
        </ul>
      </li>
      <li>
        <span>2023</span>
        <ul class="archive-list__months">
          <li><a href="/archiv/2023/12">Dezember (6)</a></li>
          <li><a href="/archiv/2023/11">November (4)</a></li>
          <!-- ... weitere Monate -->
        </ul>
      </li>
    </ul>
  </nav>
</aside>
```

Wichtige Punkte in diesem Beispiel:

*   **`<aside>`**: Da das Archiv oft ergänzende, aber nicht zentrale Inhalte darstellt, ist die Platzierung in einem `<aside>`-Element semantisch sinnvoll.
*   **`aria-labelledby="archive-heading"`**: Anstatt ein `aria-label` zu verwenden, verknüpfen wir hier das `<nav>`-Element mit einer sichtbaren Überschrift (`<h3>`). Das `id`-Attribut der Überschrift wird im `aria-labelledby`-Attribut des `<nav>`-Elements referenziert. Das ist eine elegante Methode, um Kontext zu schaffen, ohne Informationen zu duplizieren.
*   **Verschachtelte Listen**: Die `<ul>`-Struktur bildet die Hierarchie von Jahren und Monaten perfekt ab. Das Jahr selbst ist oft kein Link, sondern nur ein Text (z.B. in einem `<span>`), der die darunterliegenden Monats-Links gruppiert.
*   **Anzahl der Beiträge**: Es ist eine gängige Praxis, die Anzahl der Beiträge pro Monat in Klammern anzugeben (z.B. „Juli (3)“). Dies gibt dem Nutzer einen Hinweis darauf, wie viel Inhalt ihn erwartet.

**Das thematische Archiv (Kategorien und Tags)**

Neben der zeitlichen Sortierung ist die thematische Gliederung fundamental. Hier kommen Kategorien und Schlagwörter (Tags) ins Spiel. Kategorien sind in der Regel breiter gefasst und bilden die Hauptthemen deines Blogs ab (z.B. „Webentwicklung“, „Design“, „Marketing“). Tags sind spezifischer und können einen Beitrag feingranularer beschreiben (z.B. „CSS Grid“, „Flexbox“, „JavaScript ES6“).

Strukturell sind beide sehr ähnlich und werden meist als einfache, nicht verschachtelte Listen von Links dargestellt.

```html
<aside>
  <nav aria-labelledby="category-heading">
    <h3 id="category-heading">Kategorien</h3>
    <ul class="category-list">
      <li><a href="/kategorie/webentwicklung">Webentwicklung (42)</a></li>
      <li><a href="/kategorie/design">Design (28)</a></li>
      <li><a href="/kategorie/produktivitaet">Produktivität (15)</a></li>
    </ul>
  </nav>
</aside>
```

Die Struktur ist hier denkbar einfach: eine Navigationsbox mit einer Überschrift und einer ungeordneten Liste von Links. Jeder Link führt zu einer Seite, die alle Beiträge der entsprechenden Kategorie auflistet – und diese Kategorieseite selbst wird dann wahrscheinlich wieder eine Paginierung verwenden, wenn sie viele Beiträge enthält.

Damit schließt sich der Kreis. Paginierung und Archive sind keine konkurrierenden, sondern sich ergänzende Werkzeuge. Während die Paginierung eine lange, gefilterte Liste von Beiträgen navigierbar macht, erstellen die Archive genau diese gefilterten Listen erst. Gemeinsam bilden sie das Rückgrat der Inhaltsnavigation eines jeden erfolgreichen Blogs und sorgen dafür, dass deine wertvollen Inhalte auch dann noch gefunden werden, wenn sie längst nicht mehr auf der Startseite stehen.
