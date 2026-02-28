# Semantische Abschnitte

### Semantische Abschnitte

Erinnerst du dich an die Anfänge des Webs oder hast du vielleicht alte Webseiten-Quelltexte gesehen? Oft glichen sie einem Meer aus `<div>`-Elementen. Es gab `<div id="header">`, `<div class="navigation">`, `<div id="main-content">` und `<div id="footer">`. Technisch funktionierte das, aber es hatte einen entscheidenden Nachteil: Für eine Maschine, sei es eine Suchmaschine wie Google oder ein Screenreader für sehbehinderte Nutzer, waren all diese Boxen einfach nur … Boxen. Ein `<div>` hat keine inhaltliche Bedeutung. Es ist ein neutraler Container. Man konnte zwar durch IDs und Klassen Hinweise geben, aber es war keine standardisierte, verlässliche Methode.

Mit HTML5 änderte sich das grundlegend. Anstatt uns nur auf ein einziges Werkzeug für die grobe Strukturierung zu verlassen, bekamen wir einen ganzen Werkzeugkasten voller spezialisierter Elemente. Diese Elemente nennen wir **semantische Abschnitte**. „Semantisch“ bedeutet, dass sie eine eigene, klar definierte Bedeutung tragen. Sie sagen dem Browser, den Suchmaschinen und assistiven Technologien nicht nur, *wie* etwas aussehen soll, sondern vor allem, *was* es ist.

Die Verwendung dieser Elemente ist keine reine Formsache, sondern ein entscheidender Faktor für moderne Webentwicklung. Sie verbessert:

1.  **Barrierefreiheit (Accessibility):** Ein Screenreader kann nun eine Seite intelligent vorlesen. Er kann dem Nutzer anbieten: „Möchtest du direkt zur Navigation springen? Oder zum Hauptinhalt?“ Das ist nur möglich, weil die Elemente `<nav>` und `<main>` unmissverständlich ihre Rolle kommunizieren.
2.  **Suchmaschinenoptimierung (SEO):** Suchmaschinen können den Inhalt deiner Seite besser verstehen und indexieren. Wenn du wichtige Schlüsselwörter in einem `<header>` oder innerhalb eines `<article>` platzierst, wird dies anders gewichtet, als wenn sie in einem `<footer>` stehen.
3.  **Wartbarkeit (Maintainability):** Für dich und andere Entwickler wird der Code sofort lesbarer. Ein Blick auf die Struktur verrät sofort, wo der Kopfbereich, die Navigation oder der Hauptteil zu finden ist, ohne dass man sich durch unzählige `<div>`-Verschachtelungen kämpfen muss.

Werfen wir einen genauen Blick auf die wichtigsten semantischen Elemente, die den `<body>` deiner Webseite strukturieren.

#### `<header>` – Der Kopfbereich

Das `<header>`-Element repräsentiert den Kopfbereich einer Seite oder eines Abschnitts. Verwechsle es bitte nicht mit dem `<head>`-Tag des HTML-Dokuments! Während `<head>` Metadaten enthält, die nicht sichtbar sind, beinhaltet `<header>` sichtbare einleitende Inhalte.

Typischerweise findest du in einem `<header>`:

*   Das Logo der Webseite
*   Den Titel oder die Hauptüberschrift (`<h1>`)
*   Eine untergeordnete Tagline oder einen Slogan
*   Manchmal auch die Hauptnavigation oder ein Suchfeld

Eine Webseite kann mehrere `<header>`-Elemente haben. Du kannst zum Beispiel einen Haupt-`<header>` für die gesamte Seite und zusätzlich einen eigenen `<header>` für einen Blogbeitrag (`<article>`) verwenden, der dann den Titel des Beitrags und das Veröffentlichungsdatum enthält.

```html
<body>
  <header>
    <img src="logo.png" alt="Firmenlogo">
    <h1>Meine fantastische Webseite</h1>
    <p>Der beste Ort für alles Fantastische.</p>
  </header>

  <main>
    <!-- ... Hauptinhalt ... -->
  </main>
</body>
```

#### `<nav>` – Die Navigation

Das `<nav>`-Element ist für die primären Navigationsblöcke deiner Webseite gedacht. Das sind die Links, die den Nutzer zu den wichtigsten Bereichen deiner Seite führen (z. B. „Home“, „Über uns“, „Produkte“, „Kontakt“).

Nicht jede Gruppe von Links gehört in ein `<nav>`-Element. Eine Linkliste im `<footer>` (z. B. zu Impressum und Datenschutz) oder eine Liste von Blog-Kategorien in einer Seitenleiste benötigen nicht zwingend ein `<nav>`. Die Faustregel lautet: Wenn es die Hauptnavigation der Seite oder eines wichtigen Abschnitts ist, nutze `<nav>`.

```html
<header>
  <!-- ... Logo und Titel ... -->
  <nav>
    <ul>
      <li><a href="/">Startseite</a></li>
      <li><a href="/blog">Blog</a></li>
      <li><a href="/kontakt">Kontakt</a></li>
    </ul>
  </nav>
</header>
```

#### `<main>` – Der Hauptinhalt

Dieses Element ist so einfach wie genial. Das `<main>`-Element umschließt den zentralen, einzigartigen Inhalt eines Dokuments. Es sollte all das enthalten, was nicht zum wiederkehrenden Beiwerk wie Kopfzeile, Navigation oder Fußzeile gehört.

Die wichtigste Regel für `<main>` ist: Es darf **nur einmal pro Seite** verwendet werden. Sein Inhalt sollte für das jeweilige Dokument einzigartig sein.

```html
<body>
  <header>
    <!-- ... Header-Inhalt ... -->
  </header>

  <main>
    <h1>Der Titel des eigentlichen Inhalts</h1>
    <p>Hier steht der Text, weswegen der Nutzer auf diese Seite gekommen ist. Alles andere ist nur der Rahmen.</p>
  </main>

  <footer>
    <!-- ... Footer-Inhalt ... -->
  </footer>
</body>
```

#### `<article>` – Der in sich geschlossene Inhalt

Ein `<article>` ist ein in sich geschlossener, unabhängiger Inhaltsblock, der prinzipiell auch für sich allein stehen und weiterverteilt werden könnte (z. B. in einem RSS-Feed). Stell dir die Frage: „Ergibt dieser Inhalt auch dann noch Sinn, wenn ich ihn aus dem Kontext der restlichen Seite herausnehme?“ Wenn die Antwort „Ja“ ist, ist `<article>` wahrscheinlich das richtige Element.

Perfekte Beispiele für `<article>` sind:

*   Ein Blogbeitrag
*   Ein Zeitungsartikel
*   Ein Forenbeitrag
*   Ein einzelnes Produkt in einer Produktliste
*   Ein vom Nutzer verfasster Kommentar

Artikel können auch ineinander verschachtelt werden, zum Beispiel ein Blogbeitrag (`<article>`) mit Kommentaren (jeder ein eigenes `<article>`).

```html
<main>
  <article>
    <h2>Wie man den perfekten Kaffee kocht</h2>
    <p>Veröffentlicht am 15. Oktober von Jane Doe</p>
    <p>Der erste Schritt zum perfekten Kaffee ist die Auswahl der richtigen Bohnen...</p>
    <!-- weiterer Inhalt des Artikels -->
  </article>

  <article>
    <h2>10 Tipps für produktives Arbeiten</h2>
    <p>Veröffentlicht am 12. Oktober von Jane Doe</p>
    <p>Produktivität ist kein Zufall. Mit diesen zehn Tipps...</p>
    <!-- weiterer Inhalt des Artikels -->
  </article>
</main>
```

#### `<section>` – Der thematische Abschnitt

Das `<section>`-Element ist eines der am häufigsten missverstandenen Elemente. Es gruppiert Inhalte, die thematisch zusammengehören. Im Gegensatz zu einem `<article>` ist eine `<section>` nicht zwangsläufig unabhängig und für sich alleinstehend. Sie ist ein Teil eines größeren Ganzen.

Eine sehr gute Regel ist: Eine `<section>` sollte fast immer eine eigene Überschrift (`<h1>` - `<h6>`) haben. Wenn du keinen passenden Titel für den Abschnitt findest, ist es möglicherweise kein `<section>`, sondern eher ein `<div>`, das du nur für Styling-Zwecke benötigst.

Auf einer Homepage könntest du zum Beispiel Sektionen für „Unsere Dienstleistungen“, „Das Team“ und „Kundenstimmen“ haben.

```html
<main>
  <h1>Willkommen auf unserer Agentur-Webseite</h1>
  <p>Wir helfen dir, deine digitalen Ziele zu erreichen.</p>

  <section>
    <h2>Unsere Dienstleistungen</h2>
    <ul>
      <li>Webdesign</li>
      <li>SEO</li>
      <li>Social Media Marketing</li>
    </ul>
  </section>

  <section>
    <h2>Lerne unser Team kennen</h2>
    <p>Wir sind eine Gruppe von kreativen Köpfen...</p>
  </section>
</main>
```

#### `<aside>` – Der Seitenbereich

Das `<aside>`-Element ist für Inhalte gedacht, die nur lose mit dem Hauptinhalt auf der Seite in Verbindung stehen. Man kann es sich oft als klassische Seitenleiste (Sidebar) vorstellen. Der Inhalt in einem `<aside>` könnte entfernt werden, ohne dass der Hauptinhalt seinen Sinn verliert.

Beispiele für `<aside>`-Inhalte:

*   Links zu verwandten Artikeln
*   Eine Autorenbiografie am Ende eines Blogbeitrags
*   Werbeanzeigen
*   Eine Glossar-Definition

```html
<main>
  <article>
    <h1>Die Geschichte des Internets</h1>
    <p>Alles begann in den 1960er Jahren mit einem Projekt namens ARPANET...</p>
  </article>
  
  <aside>
    <h3>Verwandte Themen</h3>
    <ul>
      <li>Die Erfindung des World Wide Web</li>
      <li>Wichtige Persönlichkeiten der Tech-Geschichte</li>
    </ul>
  </aside>
</main>
```

#### `<footer>` – Der Fußbereich

Ähnlich wie der `<header>` stellt der `<footer>` den Fußbereich einer Seite oder eines Abschnitts dar. Er enthält typischerweise Informationen über den Autor, Copyright-Hinweise, Links zu rechtlichen Dokumenten (Impressum, Datenschutz) oder Kontaktinformationen.

Auch `<footer>`-Elemente können mehrfach auf einer Seite vorkommen. Eine Seite kann einen globalen `<footer>` ganz am Ende haben, und ein `<article>` kann seinen eigenen kleinen `<footer>` mit Informationen wie Tags oder Teilen-Buttons haben.

```html
<body>
  <!-- ... header, nav, main ... -->

  <footer>
    <p>&copy; 2023 Meine fantastische Webseite</p>
    <nav>
      <a href="/impressum">Impressum</a>
      <a href="/datenschutz">Datenschutz</a>
    </nav>
  </footer>
</body>
```

#### Das Gesamtbild: Eine typische Seitenstruktur

Wenn wir all diese Elemente zusammensetzen, ergibt sich eine klare und aussagekräftige Struktur. Betrachten wir das Skelett einer typischen Blog-Seite:

```html
<body>
  <!-- Globaler Header der Seite -->
  <header>
    <img src="logo.svg" alt="Logo">
    <nav>
      <!-- Hauptnavigation -->
    </nav>
  </header>

  <!-- Der einzigartige Hauptinhalt dieser Seite -->
  <main>
    <!-- Der Blogbeitrag als eigenständige Einheit -->
    <article>
      <!-- Der Kopfbereich des Artikels -->
      <header>
        <h1>Titel des Blogbeitrags</h1>
        <p>Gepostet von Max Mustermann am <time datetime="2023-10-27">27. Oktober 2023</time></p>
      </header>

      <p>Hier beginnt der eigentliche Text des Beitrags...</p>
      
      <!-- Ein thematischer Unterabschnitt innerhalb des Artikels -->
      <section>
        <h2>Ein tiefergehender Blick auf das Thema</h2>
        <p>Weitere Details und Analysen...</p>
      </section>

      <!-- Der Fußbereich des Artikels -->
      <footer>
        <p>Tags: #HTML #Webentwicklung</p>
      </footer>
    </article>

    <!-- Seitenleiste mit ergänzenden Informationen -->
    <aside>
      <h2>Über den Autor</h2>
      <p>Max Mustermann ist seit 10 Jahren Webentwickler...</p>
      
      <h2>Neueste Beiträge</h2>
      <ul>
        <!-- Links zu anderen Artikeln -->
      </ul>
    </aside>
  </main>

  <!-- Globaler Footer der Seite -->
  <footer>
    <p>&copy; 2023 Der Blog. Alle Rechte vorbehalten.</p>
    <a href="/kontakt">Kontakt</a>
  </footer>
</body>
```

#### Und was ist mit `<div>`?

Hat das gute alte `<div>`-Element damit ausgedient? Keineswegs! Seine Rolle hat sich nur geändert. Du solltest ein `<div>` immer dann verwenden, wenn es kein anderes, semantisch passenderes Element für deine Zwecke gibt. Sein Hauptzweck ist nun die reine Gruppierung von Elementen für Styling- (via CSS) oder Verhaltens-Zwecke (via JavaScript).

Wenn du zum Beispiel zwei Blöcke nebeneinander anordnen möchtest und dafür einen Flexbox-Container benötigst, gibt es dafür kein semantisches Element. Hier ist ein `<div>` die perfekte Wahl.

```html
<!-- Korrekte Verwendung von div für reines Layout -->
<div class="flex-container">
  <section>
    <h2>Teil 1</h2>
    <p>Inhalt...</p>
  </section>
  <aside>
    <h3>Randnotiz</h3>
    <p>Inhalt...</p>
  </aside>
</div>
```

Denke an semantische Elemente als die tragenden Wände und Räume deines Hauses. Sie definieren, was wo ist und welche Funktion es hat. Ein `<div>` ist wie eine Trockenbauwand, die du einziehst, um ein Bild aufzuhängen oder die Raumaufteilung aus rein ästhetischen Gründen zu verändern. Sie hat keine tragende, strukturelle Bedeutung. Indem du diese Werkzeuge bewusst und korrekt einsetzt, baust du nicht nur Webseiten, sondern schaffst robuste, zugängliche und zukunftssichere digitale Architekturen.
