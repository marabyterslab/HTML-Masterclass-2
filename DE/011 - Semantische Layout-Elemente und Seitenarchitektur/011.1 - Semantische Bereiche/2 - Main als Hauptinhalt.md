# Main als Hauptinhalt

### Das `<main>`-Element: Der Kern deiner Seite

Stell dir eine Webseite wie eine Zeitung oder ein Magazin vor. Es gibt einen Titelkopf (den `<header>`), vielleicht eine Fußzeile mit den Verlagsinformationen (den `<footer>`) und oft auch Werbung oder Querverweise an den Rändern (die `<aside>`). Aber der eigentliche Grund, warum du die Zeitung in die Hand nimmst, ist der Hauptartikel – der zentrale, einzigartige Inhalt. Genau diese Rolle übernimmt in HTML das `<main>`-Element.

Das `<main>`-Tag wurde eingeführt, um dem Browser, Suchmaschinen und assistiven Technologien unmissverständlich zu signalisieren: „Hier beginnt der Hauptinhalt dieses Dokuments.“ Es umschließt den Content, der für die jeweilige Seite spezifisch und zentral ist. Alles, was sich auf vielen Seiten wiederholt – wie die Navigation, das Logo, das Copyright oder die Sidebar mit den „Top 10 Artikeln“ – gehört *nicht* in das `<main>`-Element.

#### Eine einfache Regel: Es kann nur einen geben

Eine der wichtigsten Regeln für die Verwendung von `<main>` ist seine Einzigartigkeit. Pro HTML-Dokument darf es nur **ein einziges** `<main>`-Element geben. Das leuchtet ein, denn eine Seite hat in der Regel auch nur einen primären inhaltlichen Fokus. Wären mehrere `<main>`-Bereiche erlaubt, würde das Konzept seinen semantischen Wert verlieren. Es wäre nicht mehr klar, was der eigentliche Kern der Seite ist.

Zudem sollte das `<main>`-Element kein Nachfahre eines `<article>`, `<aside>`, `<footer>`, `<header>` oder `<nav>`-Elements sein. Es ist ein fundamentaler Baustein der Seitenarchitektur und steht hierarchisch auf einer Ebene mit diesen Elementen, meist direkt als Kind des `<body>`.

Sehen wir uns eine typische Grundstruktur einer Webseite an:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Mein fantastischer Blog</title>
</head>
<body>

    <header>
        <h1>Mein fantastischer Blog</h1>
        <nav>
            <ul>
                <li><a href="/">Startseite</a></li>
                <li><a href="/ueber-mich">Über mich</a></li>
                <li><a href="/kontakt">Kontakt</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <!-- Hier kommt der einzigartige Inhalt dieser Seite hin -->
        <article>
            <h2>Die Kunst der semantischen HTML-Elemente</h2>
            <p>In diesem Beitrag erforschen wir, warum semantisches HTML so wichtig für moderne Webentwicklung ist...</p>
            <p>...</p>
        </article>
    </main>

    <footer>
        <p>&copy; 2023 Mein fantastischer Blog. Alle Rechte vorbehalten.</p>
    </footer>

</body>
</html>
```

In diesem Beispiel siehst du klar die Aufteilung:
*   Der `<header>` enthält den Titel und die Hauptnavigation – Elemente, die auf jeder Seite des Blogs gleich wären.
*   Der `<footer>` enthält die Copyright-Information, ebenfalls ein wiederkehrendes Element.
*   Das `<main>`-Element umschließt den Blogartikel selbst. Dieser Artikel ist der Grund, warum ein Besucher genau *diese* URL aufgerufen hat. Er ist der einzigartige Hauptinhalt.

#### Warum die Mühe? Die Vorteile von `<main>`

Vielleicht fragst du dich, warum du nicht einfach ein `<div>` mit einer ID wie `id="main-content"` verwenden kannst. Technisch würde das für das Styling mit CSS genauso funktionieren. Der entscheidende Unterschied liegt jedoch in der Semantik – der Bedeutung, die du dem Inhalt verleihst.

**1. Barrierefreiheit (Accessibility)**

Der wohl größte Gewinn durch die Nutzung von `<main>` liegt im Bereich der Barrierefreiheit. Nutzer von Screenreadern, also Software, die den Bildschirminhalt vorliest, müssen sich nicht durch Dutzende von Navigationslinks und wiederkehrende Kopfzeilen kämpfen, um zum eigentlichen Inhalt zu gelangen.

Moderne Screenreader erkennen das `<main>`-Element als eine sogenannte „Landmark“ (einen Orientierungspunkt). Sie bieten dem Nutzer eine Tastenkombination, um direkt zum Hauptinhalt zu springen. Dies ist eine enorme Erleichterung und verbessert die Nutzererfahrung für Menschen mit Sehbehinderungen drastisch. Das Fehlen dieses Elements zwingt sie, sich mühsam durch die gesamte Seite zu navigieren, jedes Mal, wenn sie eine neue Seite laden.

**2. Suchmaschinenoptimierung (SEO)**

Auch Suchmaschinen wie Google profitieren von einer klaren Struktur. Indem du den Hauptinhalt mit `<main>` kennzeichnest, hilfst du dem Such-Crawler zu verstehen, welcher Teil deiner Seite den wichtigsten und relevantesten Inhalt für eine Suchanfrage enthält. Während dies kein magischer Schalter für ein Top-Ranking ist, ist es ein wichtiger Teil einer sauberen, technischen SEO-Strategie. Es signalisiert der Suchmaschine, dass du die Struktur deines Inhalts verstehst und ihn bestmöglich aufbereitest.

**3. Lesbarkeit und Wartbarkeit des Codes**

Dein Code wird für dich und andere Entwickler sofort verständlicher. Wenn du eine HTML-Datei öffnest und auf den ersten Blick `<header>`, `<main>` und `<footer>` siehst, ist die grobe Architektur der Seite sofort klar. Du weißt genau, wo du suchen musst, wenn du den Hauptinhalt bearbeiten willst. Ein `<div id="content">` ist weniger aussagekräftig als ein natives `<main>`-Element. Diese semantische Klarheit macht die Wartung und Weiterentwicklung deines Projekts einfacher.

#### Abgrenzung zu anderen semantischen Elementen

Gerade am Anfang kann die Abgrenzung von `<main>` zu `<article>` und `<section>` für Verwirrung sorgen. Lass uns das kurz klären:

*   **`<main>` vs. `<article>`:** Das `<main>`-Element ist der Container für den *gesamten Hauptinhalt einer Seite*. Ein `<article>` hingegen ist ein in sich geschlossener, potenziell wiederverwendbarer Inhaltsblock. Ein Blogbeitrag ist ein perfektes Beispiel für ein `<article>`. Auf der Detailseite eines Blogbeitrags würde das `<article>`-Element *innerhalb* von `<main>` liegen. Auf einer Übersichtsseite (z.B. der Blog-Homepage) könnte dein `<main>`-Element *mehrere* `<article>`-Elemente enthalten, nämlich die Vorschauen der einzelnen Beiträge.

*   **`<main>` vs. `<section>`:** Ein `<section>`-Element gruppiert thematisch zusammengehörigen Inhalt. Dein `<main>`-Bereich kann problemlos mehrere `<section>`s enthalten. Stell dir eine Produktseite in einem Onlineshop vor. Der `<main>`-Bereich würde alles umfassen, was dieses Produkt beschreibt. Innerhalb dieses `<main>`-Bereichs könntest du eine `<section>` für die Produktbeschreibung, eine weitere `<section>` für die technischen Daten und eine dritte `<section>` für Kundenbewertungen haben.

Hier ein Beispiel für eine solche Produktseite:

```html
<body>
    <header>
        <!-- Logo, Navigation, Warenkorb etc. -->
    </header>

    <main>
        <h1>Fantastisches Produkt XYZ</h1>
        
        <section aria-labelledby="beschreibung">
            <h2 id="beschreibung">Produktbeschreibung</h2>
            <p>Dieses Produkt wird dein Leben verändern. Es ist aus nachhaltigen Materialien gefertigt...</p>
            <!-- Weitere Bilder und Texte -->
        </section>

        <section aria-labelledby="tech-daten">
            <h2 id="tech-daten">Technische Daten</h2>
            <ul>
                <li>Gewicht: 2.5kg</li>
                <li>Maße: 30x20x10cm</li>
                <li>Material: Recyceltes Adamantium</li>
            </ul>
        </section>

        <section aria-labelledby="bewertungen">
            <h2 id="bewertungen">Kundenbewertungen</h2>
            <article>
                <p>"Bestes Produkt aller Zeiten!" - Anna B.</p>
            </article>
            <article>
                <p>"Ich kann nicht mehr ohne leben." - Max M.</p>
            </article>
        </section>
    </main>

    <footer>
        <!-- Copyright, rechtliche Links etc. -->
    </footer>
</body>
```

Du siehst, wie `<main>` als übergeordneter Container für den gesamten produkt-spezifischen Inhalt dient, der wiederum durch `<section>`-Elemente logisch unterteilt ist.

#### Styling und Verhalten

Standardmäßig ist das `<main>`-Element ein Block-Level-Element, genau wie ein `<div>`. Es hat keine speziellen visuellen Eigenschaften. Du kannst es mit CSS nach Belieben gestalten. Eine sehr gebräuchliche Anwendung ist die Zentrierung des Hauptinhalts auf großen Bildschirmen:

```css
main {
    max-width: 960px; /* Maximale Breite des Inhaltsbereichs */
    margin-left: auto;
    margin-right: auto;
    padding: 2rem; /* Etwas Innenabstand */
}
```

Die Verwendung des `<main>`-Elements ist ein einfacher, aber wirkungsvoller Schritt hin zu professionellerem, zugänglicherem und verständlicherem HTML-Code. Es ist ein klares Bekenntnis zur semantischen Struktur und zeigt, dass du nicht nur darüber nachdenkst, wie eine Seite aussieht, sondern auch, was sie bedeutet.
