# Analyse bekannter Websites

### Analyse bekannter Websites: Ein Blick unter die Haube

Die Theorie semantischer HTML-Elemente ist das eine. Zu verstehen, wie `<header>`, `<main>`, `<article>` oder `<footer>` funktionieren, ist die Grundlage. Doch die wahre Meisterschaft erlangst du erst, wenn du siehst, wie diese Bausteine in der realen Welt zu komplexen, funktionierenden und erfolgreichen Websites zusammengesetzt werden. Der beste Weg, dies zu lernen, ist, von den Profis zu lernen – indem du ihre Arbeit analysierst.

In diesem Kapitel werfen wir gemeinsam einen Blick unter die Motorhaube einiger typischer Website-Layouts. Wir zerlegen ihre Struktur und finden heraus, warum bestimmte semantische Elemente an bestimmten Stellen eingesetzt werden. Das Werkzeug unserer Wahl ist dabei immer dasselbe und bereits in deinem Browser eingebaut: die Entwicklertools.

#### Dein wichtigstes Werkzeug: Der Inspektor

Bevor wir in die Analyse einsteigen, musst du mit deinem wichtigsten Werkzeug vertraut werden. Jeder moderne Browser (Chrome, Firefox, Edge, Safari) verfügt über sogenannte Entwicklertools (Developer Tools oder kurz DevTools). Du öffnest sie meist mit der Taste `F12` oder über einen Rechtsklick auf eine beliebige Stelle der Webseite und die Auswahl von „Untersuchen“ oder „Element untersuchen“.

Sobald sie geöffnet sind, siehst du eine neue Leiste oder ein neues Fenster, das in mehrere Reiter unterteilt ist. Für uns ist der Reiter „Elemente“ (Elements) oder „Inspektor“ (Inspector) entscheidend. Hier siehst du den vollständigen HTML-Code der Seite, so wie der Browser ihn gerade darstellt.

Das Geniale daran: Es ist interaktiv. Wenn du mit der Maus über eine Codezeile im Inspektor fährst, wird das entsprechende Element auf der Webseite visuell hervorgehoben. Umgekehrt kannst du auch ein Werkzeug (meist ein kleines Viereck mit einem Pfeil) im Inspektor auswählen, auf ein Element auf der Webseite klicken und sofort zur passenden Stelle im HTML-Code springen.

Diese Funktion ist dein Röntgengerät für das Web. Sie erlaubt es dir, die verborgene Knochenstruktur jeder Seite sichtbar zu machen. Nutze sie, während du dieses Kapitel liest, und untersuche die von dir täglich besuchten Websites.

#### Fallstudie 1: Das klassische Nachrichtenportal

Stell dir eine typische Nachrichtenseite vor, zum Beispiel die Startseite von Spiegel Online, der ZEIT oder der New York Times. Visuell siehst du sofort eine klare Gliederung:
*   Ganz oben: ein Logo und die Hauptnavigation (Politik, Wirtschaft, Sport etc.).
*   Darunter: ein großer Bereich für die Top-Nachricht des Tages, oft mit einem großen Bild.
*   Daneben oder darunter: Listen mit weiteren Artikeln aus verschiedenen Ressorts.
*   An der Seite: eine Spalte (Sidebar) mit Werbung, Wetterinformationen oder Links zu den meistgelesenen Artikeln.
*   Ganz unten: ein breiter Fußbereich (Footer) mit rechtlichen Hinweisen, Kontaktinformationen und Links zu sozialen Netzwerken.

Wie wird diese visuelle Struktur in semantisches HTML übersetzt? Schauen wir uns den Code an.

**Der Seitenkopf (`<header>`)**
Der gesamte obere Bereich mit Logo und Hauptnavigation wird fast immer von einem `<header>`-Element umschlossen. Das signalisiert klar: Hier beginnt die Seite, das ist der Kopfbereich. Innerhalb dieses Headers befindet sich dann oft ein `<a>`-Tag für das Logo und ein `<nav>`-Element für die Hauptnavigation.

```html
<header>
  <a href="/" id="logo">Logo der Nachrichtenseite</a>
  <nav>
    <ul>
      <li><a href="/politik">Politik</a></li>
      <li><a href="/wirtschaft">Wirtschaft</a></li>
      <li><a href="/sport">Sport</a></li>
    </ul>
  </nav>
</header>
```

**Der Hauptinhalt (`<main>`)**
Alles, was den einzigartigen Inhalt dieser spezifischen Seite ausmacht – also die Nachrichtenartikel –, befindet sich innerhalb des `<main>`-Tags. Dieses Element sollte es nur einmal pro Seite geben. Es grenzt den Kerninhalt klar von wiederkehrenden Elementen wie dem Header oder Footer ab.

**Artikel und Sektionen (`<article>` und `<section>`)**
Innerhalb von `<main>` wird es interessant. Ein Nachrichtenportal besteht aus vielen einzelnen, in sich geschlossenen Inhaltseinheiten: den Artikeln. Jede dieser Einheiten ist ein perfekter Kandidat für das `<article>`-Element. Ein `<article>` ist portabel – man könnte ihn theoretisch aus der Seite herausnehmen und er würde für sich allein immer noch Sinn ergeben, zum Beispiel in einem RSS-Feed.

Diese Artikel werden oft thematisch gruppiert. So gibt es vielleicht einen Bereich für „Top-Nachrichten“ und einen anderen für „Aus dem Sport“. Solche Gruppierungen sind ein idealer Anwendungsfall für das `<section>`-Element. Eine `<section>` bündelt inhaltlich zusammengehörige Elemente.

Die Struktur könnte also so aussehen:

```html
<main>
  <section>
    <h2>Top-Nachrichten</h2>
    <article>
      <h3>Großer Titel des Hauptartikels</h3>
      <p>Ein kurzer Anreißertext, der zum Weiterlesen anregt...</p>
    </article>
    <article>
      <h3>Titel eines weiteren wichtigen Artikels</h3>
      <p>Ein weiterer Anreißertext...</p>
    </article>
  </section>

  <section>
    <h2>Sport</h2>
    <article>
      <h3>Fußball-Ergebnisse vom Wochenende</h3>
      <p>Kurze Zusammenfassung der Spiele...</p>
    </article>
  </section>
</main>
```

**Die Seitenleiste (`<aside>`)**
Die Sidebar mit Inhalten, die sich zwar auf die Seite beziehen, aber nicht Teil des Hauptinhaltsstroms sind (wie Werbung, Links zu anderen Artikeln oder ein Wetter-Widget), gehört in ein `<aside>`-Element. Das Wort „aside“ bedeutet „beiseite“ oder „nebenbei“, was seine Funktion perfekt beschreibt. Oftmals wird das `<aside>`-Element auf derselben Ebene wie das `<main>`-Element platziert, direkt davor oder danach im Code.

```html
<body>
  <header>...</header>
  
  <main>
    <!-- Die Sektionen und Artikel von oben -->
  </main>

  <aside>
    <h3>Meistgelesen</h3>
    <ul>
      <li><a href="...">Artikel 1</a></li>
      <li><a href="...">Artikel 2</a></li>
    </ul>
    <div class="ad">Werbung</div>
  </aside>

  <footer>...</footer>
</body>
```

**Der Fußbereich (`<footer>`)**
Ganz am Ende der Seite finden wir den `<footer>`. Er enthält typischerweise Copyright-Informationen, Links zum Impressum, zur Datenschutzerklärung, zu den Nutzungsbedingungen oder eine Sitemap. Es sind die abschließenden Informationen zur gesamten Website.

#### Fallstudie 2: Ein Entwickler-Blog

Ein Blog hat oft eine einfachere Struktur als ein großes Nachrichtenportal, folgt aber denselben semantischen Prinzipien. Der Fokus liegt hier meist auf einem einzigen, langen Artikel pro Seite.

**Die Struktur einer Blogpost-Seite**
Visuell siehst du einen Header, vielleicht mit dem Namen des Blogs und einer kleinen Navigation. Darunter folgt der Hauptteil: der Blogartikel selbst, mit Titel, Datum, Autor und dem eigentlichen Text. Ganz unten befindet sich wieder ein Footer.

Die HTML-Struktur spiegelt das wider:
*   Ein globaler `<header>` für die Seite.
*   Ein globales `<footer>` für die Seite.
*   Ein `<main>`-Element, das den eigentlichen Blogbeitrag umschließt.

Der entscheidende Unterschied liegt innerhalb von `<main>`. Hier gibt es in der Regel nur ein einziges, dominantes `<article>`-Element. Dieser Blogbeitrag ist der Star der Seite.

Interessant wird es innerhalb dieses `<article>`-Elements. Denn auch ein Artikel kann einen eigenen Kopf- und Fußbereich haben.

```html
<main>
  <article>
    <header>
      <h1>Der ultimative Guide zu semantischem HTML</h1>
      <p>
        Veröffentlicht am <time datetime="2023-10-27">27. Oktober 2023</time> 
        von Max Mustermann
      </p>
    </header>

    <p>Hier beginnt der eigentliche Fließtext des Artikels. Er kann Absätze, Bilder, Codeblöcke und vieles mehr enthalten.</p>
    
    <!-- ... viel mehr Inhalt ... -->

    <footer>
      <p>Kategorien: <a href="/html">HTML</a>, <a href="/webdev">Webentwicklung</a></p>
      <p>Tags: #semantik, #bestpractice</p>
    </footer>
  </article>
</main>
```

Beachte hier, wie das `<header>`-Element innerhalb des `<article>`-Elements verwendet wird. Es dient nicht dem Kopf der gesamten Seite, sondern spezifisch dem Kopf des Artikels. Es enthält die Metadaten des Beitrags. Genauso verhält es sich mit dem `<footer>` innerhalb des `<article>`-Tags. Er enthält abschließende Informationen zum Artikel, wie Kategorien oder Tags. Dies zeigt eindrucksvoll, wie kontextabhängig semantische Elemente sein können.

#### Fallstudie 3: Die Produktseite eines Online-Shops

Produktseiten sind wieder ein anderer Fall. Der Hauptinhalt ist kein Fließtext, sondern eine Sammlung von Informationen, die ein Produkt beschreiben und zum Kauf anregen sollen.

**Visuelle und strukturelle Gliederung**
Eine typische Produktseite hat einen Seiten-Header mit Suche und Warenkorb. Der `<main>`-Bereich ist oft zweigeteilt:
1.  Ein oberer Bereich mit Produktbildern, Produkttitel, Preis und dem „In den Warenkorb“-Button.
2.  Ein unterer Bereich mit detaillierten Beschreibungen, technischen Daten und Kundenbewertungen.

Wie lässt sich das semantisch abbilden?

Der gesamte Produktbereich innerhalb von `<main>` kann als ein in sich geschlossenes Element betrachtet werden. Man könnte ihn also in ein `<article>`-Tag packen, denn ein Produkt in einem Katalog ist durchaus eine eigenständige, verteilbare Einheit.

Innerhalb dieses Artikels bieten sich wieder `<section>`-Elemente an, um die verschiedenen Informationsblöcke zu gliedern.

```html
<main>
  <article class="product">
    <header>
      <h1>Produktname des fantastischen Geräts</h1>
    </header>

    <section class="product-gallery-and-purchase">
      <!-- Hier wären Bilder, Preis und der Kaufen-Button -->
      <div class="gallery">...</div>
      <div class="purchase-box">
        <span class="price">99,99 €</span>
        <button>In den Warenkorb</button>
      </div>
    </section>

    <section class="product-description">
      <h2>Beschreibung</h2>
      <p>Eine ausführliche Beschreibung der tollen Eigenschaften dieses Produkts.</p>
    </section>
    
    <section class="product-reviews">
      <h2>Kundenbewertungen</h2>
      <!-- Hier folgen die einzelnen Bewertungen -->
    </section>
  </article>
</main>
```

Diese Struktur schafft eine klare, logische Hierarchie. Jede `<section>` hat ein klares Thema, das durch eine Überschrift (`<h2>`) eingeleitet wird. Dies ist nicht nur für Menschen gut lesbar, sondern auch für Suchmaschinen und assistierende Technologien von unschätzbarem Wert. Sie können sofort erkennen: „Aha, hier beginnt die Produktbeschreibung“ oder „Hier kommen die Kundenbewertungen“.

#### Was du daraus mitnehmen solltest

Die Analyse dieser drei typischen Fälle zeigt ein klares Muster: Es gibt keine dogmatische, einzig richtige Art, eine Seite zu strukturieren. Aber es gibt sehr logische und bewährte Muster, die auf den semantischen Bedeutungen der HTML-Elemente aufbauen.

*   **`<header>`, `<main>`, `<footer>`** bilden das grobe Grundgerüst fast jeder Seite.
*   **`<article>`** wird für in sich geschlossene, eigenständige Inhalte verwendet (Nachrichten, Blogposts, Produkte).
*   **`<section>`** dient der thematischen Gruppierung von Inhalten innerhalb eines größeren Kontexts.
*   **`<nav>`** ist für die Hauptnavigationsblöcke reserviert.
*   **`<aside>`** enthält ergänzende, aber nicht essenzielle Informationen.

Mach es dir zur Gewohnheit, beim Surfen immer wieder die Entwicklertools zu öffnen. Schau dir an, wie deine Lieblings-Websites aufgebaut sind. Du wirst schnell ein Auge für gute und schlechte Strukturen entwickeln. Diese Fähigkeit, den Code hinter der Fassade zu lesen und zu verstehen, ist ein entscheidender Schritt auf deinem Weg, selbst professionelle und durchdachte Webseiten zu erstellen.
