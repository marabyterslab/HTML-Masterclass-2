# Nav für Navigation

### Das `<nav>`-Element: Der Wegweiser deiner Webseite

Stell dir eine Webseite für einen Moment nicht als Code, sondern als ein physisches Gebäude vor. Vielleicht ist es eine große Bibliothek, ein Kaufhaus oder ein Museum. Wenn du dieses Gebäude betrittst, was ist eines der ersten Dinge, nach denen du suchst? Wahrscheinlich ein Schild, ein Inhaltsverzeichnis oder eine Informationstafel, die dir sagt: "Belletristik ist hier drüben", "Die Herrenabteilung ist im zweiten Stock" oder "Die Dinosaurier-Ausstellung befindet sich am Ende des Ganges." Ohne diese Wegweiser wärst du verloren und würdest frustriert umherirren.

Im Web ist das nicht anders. Deine Nutzer brauchen eine klare Orientierung, um sich auf deiner Seite zurechtzufinden. Genau für diesen Zweck wurde das `<nav>`-Element geschaffen. Es ist der digitale Wegweiser, das zentrale Verzeichnis deiner Webseite.

#### Mehr als nur ein `<div>`

Früher, bevor semantische Elemente in HTML5 zum Standard wurden, war es üblich, Navigationen so zu bauen:

```html
<!-- Die alte Methode -->
<div id="navigation">
  <ul>
    <li><a href="/">Startseite</a></li>
    <li><a href="/ueber-uns/">Über uns</a></li>
    <li><a href="/kontakt/">Kontakt</a></li>
  </ul>
</div>
```

Funktionell ist daran nichts auszusetzen. Ein `<div>` ist ein generischer Container, und mit einer ID wie `"navigation"` oder einer Klasse wie `"nav"` konnten Entwickler und Browser (über CSS-Selektoren) verstehen, was gemeint war. Aber es war eine reine Konvention. Ein `<div>` hat für sich genommen keine Bedeutung. Es ist eine leere Kiste, deren Inhalt nur durch ihren Aufkleber (`id` oder `class`) identifiziert wird.

Das `<nav>`-Element ändert das grundlegend. Es sagt unmissverständlich: "Alles, was sich in mir befindet, ist ein Block von Navigationslinks." Diese Aussage ist nicht nur eine Konvention für dich als Entwickler, sondern eine fest verankerte Information für Maschinen – allen voran für Suchmaschinen und assistierende Technologien wie Screenreader.

Das moderne, semantisch korrekte Äquivalent sieht so aus:

```html
<nav>
  <ul>
    <li><a href="/">Startseite</a></li>
    <li><a href="/ueber-uns/">Über uns</a></li>
    <li><a href="/kontakt/">Kontakt</a></li>
  </ul>
nav>
```

Der Code ist fast identisch, aber seine Bedeutung ist eine völlig andere. Du verwendest nun ein spezialisiertes Werkzeug für eine spezifische Aufgabe.

#### Wann solltest du `<nav>` verwenden?

Die entscheidende Regel für die Verwendung von `<nav>` lautet: Es ist für die **Hauptnavigation** gedacht. Das bedeutet, nicht jede Gruppe von Links auf deiner Seite gehört automatisch in ein `<nav>`-Element.

**Typische Anwendungsfälle für `<nav>` sind:**

1.  **Die Hauptnavigation der Webseite:** Dies ist der klassische Fall. Meistens findest du sie im Header der Seite und sie enthält die Links zu den wichtigsten Bereichen wie "Home", "Produkte", "Blog", "Über uns" und "Kontakt".

    ```html
    <header>
      <!-- Logo, Slogan etc. -->
      <nav>
        <!-- Hauptmenü hier -->
      </nav>
    </header>
    ```

2.  **Ein Inhaltsverzeichnis innerhalb einer Seite:** Wenn du einen sehr langen Artikel oder eine Dokumentationsseite hast, kann ein Block mit Links, die zu verschiedenen Abschnitten desselben Dokuments springen, ebenfalls als primäre Navigation für diesen Inhalt angesehen werden.

    ```html
    <article>
      <h1>Die Geschichte der Webentwicklung</h1>
      <nav>
        <h2>Inhaltsverzeichnis</h2>
        <ul>
          <li><a href="#kapitel1">Kapitel 1: Die Anfänge</a></li>
          <li><a href="#kapitel2">Kapitel 2: Der Browserkrieg</a></li>
          <li><a href="#kapitel3">Kapitel 3: Das Aufkommen von CSS</a></li>
        </ul>
      </nav>
      <section id="kapitel1">
        <h2>Kapitel 1: Die Anfänge</h2>
        <p>... langer Text ...</p>
      </section>
      <!-- weitere Sektionen -->
    </article>
    ```

3.  **Breadcrumbs (Brotkrumennavigation):** Diese zeigen dem Nutzer, wo er sich in der Hierarchie der Webseite befindet (z. B. Startseite > Produkte > Laptops). Da dies ein wesentliches Navigationselement ist, ist die Verwendung von `<nav>` hier ebenfalls angebracht.

    ```html
    <nav aria-label="Brotkrumen">
      <ol>
        <li><a href="/">Startseite</a></li>
        <li><a href="/produkte/">Produkte</a></li>
        <li><a aria-current="page">Laptops</a></li>
      </ol>
    </nav>
    ```
    *Hinweis: Das `aria-label` hilft assistiven Technologien, den Zweck dieser speziellen Navigation noch genauer zu beschreiben.*

#### Wann solltest du `<nav>` NICHT verwenden?

Genauso wichtig ist es zu wissen, wann `<nav>` unangebracht ist.

*   **Fußzeilen-Links:** Die typischen Links im `<footer>` einer Seite (wie Impressum, Datenschutz, AGB) sind keine primäre Seitennavigation. Sie sind eher rechtliche oder organisatorische Metainformationen. Sie können einfach in einer Liste innerhalb des `<footer>`-Elements stehen, ohne ein umgebendes `<nav>`.
*   **Social-Media-Links:** Eine Liste von Links zu deinen Profilen auf Twitter, Instagram oder LinkedIn ist in der Regel keine Navigation *innerhalb* deiner Webseite.
*   **Pagination:** Links zu "Nächste Seite" und "Vorherige Seite" am Ende einer Blog-Übersicht sind eine Form der Navigation, aber sie gelten nicht als primärer Navigationsblock. Einfache `<a>`-Tags sind hier oft ausreichend.

Die Faustregel lautet: Wenn du dieselbe Navigationsleiste auf fast jeder Seite deiner Website wiederholen würdest, dann ist es sehr wahrscheinlich ein Kandidat für ein `<nav>`-Element.

#### Der Gewinn: Semantik und Barrierefreiheit

Warum ist dieser Unterschied so wichtig? Die Vorteile liegen in drei Bereichen: Suchmaschinenoptimierung (SEO), Barrierefreiheit (Accessibility) und Code-Wartbarkeit.

1.  **Für Suchmaschinen:** Eine Suchmaschine wie Google analysiert die Struktur deiner Seite, um deren Inhalt zu verstehen. Wenn sie ein `<nav>`-Element findet, weiß sie sofort: "Aha, das sind die wichtigsten Links dieser Webseite." Dies hilft ihr, eine "Sitemap" deiner Seitenarchitektur zu erstellen und die verlinkten Seiten als relevant einzustufen. Ein Link in einer Hauptnavigation hat für eine Suchmaschine tendenziell mehr Gewicht als ein Link, der irgendwo in einem Fließtext vergraben ist.

2.  **Für die Barrierefreiheit:** Dies ist der vielleicht größte Gewinn. Nutzer, die auf Screenreader angewiesen sind (z. B. blinde oder sehbehinderte Menschen), navigieren nicht visuell. Ein Screenreader erkennt das `<nav>`-Element als einen sogenannten **"Landmark"** (eine wichtige Orientierungsmarke). Der Nutzer kann sich dann alle Landmarks einer Seite ansagen lassen (z. B. "Banner", "Navigation", "Hauptinhalt", "Fußzeile") und direkt zu dem gewünschten Bereich springen. Stell dir vor, du müsstest dir bei jedem Seitenaufruf erst das Logo, den Werbebanner und eine Cookie-Warnung vorlesen lassen, bevor du zum eigentlichen Menü kommst. Mit `<nav>` kann der Nutzer diesen ganzen Vorspann überspringen und direkt zur Navigation springen. Ein `<div>` bietet diese Funktionalität nicht von Haus aus.

3.  **Für dich als Entwickler:** Semantischer Code ist selbsterklärend. Wenn du oder ein Kollege in sechs Monaten den Code öffnet, ist sofort klar, was der Zweck dieses Abschnitts ist. `<nav>` schreit förmlich "Ich bin die Navigation!", während `<div class="menu">` erst interpretiert werden muss. Das macht deinen Code lesbarer, sauberer und einfacher zu warten.

Das `<nav>`-Element ist also weit mehr als nur ein Container. Es ist ein Kommunikationsmittel. Es kommuniziert die Struktur und den Zweck eines Teils deiner Webseite an Maschinen und Menschen gleichermaßen und macht dein Webprojekt damit robuster, zugänglicher und professioneller. Es ist ein kleines, aber mächtiges Werkzeug in deinem Arsenal für den Bau einer durchdachten und benutzerfreundlichen Seitenarchitektur.
