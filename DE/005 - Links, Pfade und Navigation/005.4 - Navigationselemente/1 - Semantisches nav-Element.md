# Semantisches nav-Element

### Das semantische `nav`-Element: Der Wegweiser deiner Webseite

Stell dir eine große, unübersichtliche Bibliothek ohne Schilder vor. Du suchst die Abteilung für Science-Fiction, aber alles, was du siehst, sind endlose Reihen von generischen Bücherregalen. Du müsstest jedes Regal einzeln prüfen, um zu finden, was du suchst. Eine mühsame und frustrierende Aufgabe.

Vor der Einführung von HTML5 fühlte sich das Web für Maschinen – wie Suchmaschinen-Crawler oder Screenreader für Menschen mit Sehbehinderungen – oft genauso an. Entwicklerinnen und Entwickler nutzten für Navigationsleisten meist ein generisches `<div>`-Element, dem sie eine ID oder eine Klasse gaben, zum Beispiel `<div id="navigation">`. Für einen menschlichen Betrachter, der die Webseite visuell erfasst, war das kein Problem. Das Design machte klar: „Das hier ist die Navigation.“ Für eine Maschine war es aber nur ein weiteres namenloses Regal, eine simple Box ohne besondere Bedeutung. Sie wusste nicht, dass die Links in diesem `<div>` die Hauptwegweiser der gesamten Seite sind.

Hier kommt das `<nav>`-Element ins Spiel. Es ist ein semantisches Element, das genau dieses Problem löst. Es ist wie ein großes, leuchtendes Schild in der Bibliothek, auf dem „Navigation“ steht.

#### Was ist das `<nav>`-Element und wofür nutzt du es?

Das `<nav>`-Element ist ein Container, der speziell dafür vorgesehen ist, die wichtigsten Navigationsblöcke deiner Webseite zu umfassen. Wenn du eine Gruppe von Links hast, die den Benutzer durch die Hauptbereiche deiner Website oder durch die wichtigsten Abschnitte einer einzelnen Seite führen, dann ist `<nav>` das richtige Werkzeug für dich.

Indem du deine Hauptnavigation in `<nav>`-Tags einschließt, teilst du dem Browser, den Suchmaschinen und vor allem den assistiven Technologien (wie Screenreadern) unmissverständlich mit: „Achtung, hier folgt ein zentraler Navigationsbereich.“

Ein typisches und bewährtes Muster für eine Hauptnavigation sieht so aus:

```html
<nav>
  <ul>
    <li><a href="/">Startseite</a></li>
    <li><a href="/ueber-uns/">Über uns</a></li>
    <li><a href="/produkte/">Produkte</a></li>
    <li><a href="/kontakt/">Kontakt</a></li>
  </ul>
</nav>
```

Warum eine ungeordnete Liste (`<ul>`)? Weil eine Navigation im Grunde genau das ist: eine Liste von Navigationspunkten. Diese Struktur ist nicht nur logisch und semantisch korrekt, sondern bietet auch eine solide Grundlage für das spätere Styling mit CSS. Jeder Menüpunkt ist ein Listeneintrag (`<li>`), der einen Link (`<a>`) enthält.

#### Wann du das `<nav>`-Element *nicht* verwenden solltest

Die Macht der Semantik liegt auch darin, Elemente korrekt und nicht inflationär zu verwenden. Nicht jede Gruppe von Links auf deiner Seite gehört automatisch in ein `<nav>`-Element. Die offizielle HTML-Spezifikation besagt, dass `<nav>` für **wichtige Navigationsblöcke** ("major navigational blocks") gedacht ist.

Hier sind einige Beispiele, bei denen ein `<nav>`-Element in der Regel unangebracht wäre:

1.  **Footer-Links:** Viele Websites haben im Footer Links zu Impressum, Datenschutz, AGB oder Social-Media-Profilen. Obwohl dies Links sind, bilden sie selten die *Hauptnavigation* der Seite. Sie sind eher ergänzende, rechtliche oder administrative Verweise. Hierfür reicht es oft aus, sie einfach in das `<footer>`-Element zu platzieren, eventuell innerhalb einer Liste, aber ohne ein umschließendes `<nav>`.
2.  **Pagination:** Eine Link-Gruppe am Ende eines Blogartikels, die zur nächsten oder vorherigen Seite führt (`« Vorherige Seite | Nächste Seite »`), ist eine Form der Navigation, aber keine *Hauptnavigation*.
3.  **Links im Fließtext:** Einzelne Links, die du innerhalb eines Absatzes setzt, um auf andere Artikel oder externe Quellen zu verweisen, sind Teil des Inhalts und gehören selbstverständlich nicht in ein `<nav>`-Element.

Die Faustregel lautet: Frage dich, ob die Link-Sammlung eine primäre Methode ist, um sich auf deiner Website zu orientieren. Wenn ja, nutze `<nav>`. Wenn es sich um eine untergeordnete oder kontextbezogene Link-Gruppe handelt, verzichte darauf.

#### Mehrere `<nav>`-Elemente auf einer Seite

Es ist absolut legitim und oft sogar notwendig, mehr als ein `<nav>`-Element auf einer einzelnen Seite zu verwenden. Eine Webseite kann verschiedene wichtige Navigationsbereiche haben.

Stell dir einen langen, ausführlichen Wikipedia-Artikel vor. Dort findest du typischerweise zwei zentrale Navigationsbereiche:

1.  **Die Hauptnavigation der Website:** Ganz oben oder an der Seite, mit Links zu „Startseite“, „Zufälliger Artikel“, „Spenden“ etc. Diese Navigation ist auf jeder Seite von Wikipedia gleich.
2.  **Die Inhaltsverzeichnis-Navigation:** Am Anfang des Artikels befindet sich eine Box mit Links, die zu den einzelnen Überschriften und Abschnitten *innerhalb desselben Artikels* springen.

Beide sind wichtige Navigationsblöcke, aber sie dienen unterschiedlichen Zwecken. In so einem Fall ist es absolut korrekt, beide in eigene `<nav>`-Elemente zu packen.

```html
<body>
  <!-- Hauptnavigation der gesamten Website -->
  <header>
    <h1>Meine großartige Webseite</h1>
    <nav aria-label="Hauptnavigation">
      <ul>
        <li><a href="/">Startseite</a></li>
        <li><a href="/blog/">Blog</a></li>
        <li><a href="/projekte/">Projekte</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <h2>Ein langer, spannender Artikel</h2>

      <!-- In-Page-Navigation für diesen Artikel -->
      <nav aria-label="Inhaltsverzeichnis">
        <h3>Inhalt</h3>
        <ul>
          <li><a href="#kapitel1">Kapitel 1: Die Anfänge</a></li>
          <li><a href="#kapitel2">Kapitel 2: Die Entwicklung</a></li>
          <li><a href="#kapitel3">Kapitel 3: Der Durchbruch</a></li>
        </ul>
      </nav>

      <section id="kapitel1">
        <h3>Kapitel 1: Die Anfänge</h3>
        <p>...</p>
      </section>
      <!-- weitere Sektionen -->
    </article>
  </main>
</body>
```

#### Der entscheidende Vorteil: Barrierefreiheit

Du hast im obigen Beispiel vielleicht das Attribut `aria-label` bemerkt. Das ist kein Zufall und führt uns zum größten Gewinn durch die Verwendung des `<nav>`-Elements: die Barrierefreiheit (Accessibility).

Das `<nav>`-Element erzeugt automatisch eine sogenannte **Landmark-Rolle**. Landmarks sind für Screenreader wie Leuchttürme auf einer Webseite. Ein Nutzer, der auf einen Screenreader angewiesen ist, kann sich zu Beginn eine Liste aller Landmarks auf der Seite ausgeben lassen (z. B. „Kopfbereich“, „Navigation“, „Hauptinhalt“, „Fußbereich“) und direkt zu dem Bereich springen, der ihn interessiert. Anstatt sich durch die gesamte Seite lesen lassen zu müssen, kann er direkt zur Navigation springen, um sich einen Überblick zu verschaffen.

Wenn du nun, wie im Beispiel oben, zwei `<nav>`-Elemente verwendest, würde ein Screenreader zweimal „Navigation“ ansagen. Das ist verwirrend. Woher soll der Nutzer wissen, welche Navigation welche ist?

Genau hier kommt `aria-label` ins Spiel. Mit diesem Attribut gibst du jeder Navigation einen einzigartigen, verständlichen Namen. Der Screenreader sagt dann nicht mehr nur „Navigation“, sondern zum Beispiel „Hauptnavigation“ und „Inhaltsverzeichnis“. Der Nutzer kann sofort unterscheiden, welche Navigation er ansteuern möchte. Dies ist ein kleiner, aber unglaublich wichtiger Schritt, um deine Webseite für alle Menschen zugänglich zu machen.

#### Styling und das große Ganze

Ein semantisches Element wie `<nav>` definiert nur die *Bedeutung* seines Inhalts, nicht sein Aussehen. Standardmäßig ist `<nav>` ein Block-Element, genau wie ein `<div>`. Du kannst es mit CSS nach Belieben gestalten. Ob deine Navigation horizontal oder vertikal, dezent oder auffällig ist, entscheidest allein du mit deinen CSS-Regeln.

```css
/* Eine einfache Gestaltung für unsere Navigation */
nav {
  background-color: #333;
  padding: 1rem;
}

nav ul {
  list-style: none; /* Entfernt die Aufzählungspunkte */
  margin: 0;
  padding: 0;
  display: flex; /* Ordnet die Elemente nebeneinander an */
  gap: 1.5rem; /* Fügt Abstand zwischen den Elementen hinzu */
}

nav a {
  color: white;
  text-decoration: none;
  font-weight: bold;
}

nav a:hover {
  color: #a4d4ff;
}
```

Die Verwendung von `<nav>` ist also kein rein akademisches Konzept. Es ist eine praktische Entscheidung, die deinen Code sauberer, deine Webseite zugänglicher und die Struktur für Suchmaschinen verständlicher macht. Du gibst einem wichtigen Teil deiner Seite einen klaren Namen und eine eindeutige Rolle – und schaffst damit eine bessere Erfahrung für Maschinen und vor allem für Menschen.
