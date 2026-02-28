# Hero-Bereich und Teaser

### Der erste Eindruck zählt: Hero-Bereich und Teaser

Wenn ein Besucher auf deiner Webseite landet, hast du nur wenige Sekunden Zeit, um seine Aufmerksamkeit zu fesseln und ihm zu vermitteln, worum es bei dir geht. Diese entscheidende erste Begegnung findet in einem Bereich statt, den wir im Webdesign als „Hero-Bereich“ bezeichnen. Er ist das digitale Aushängeschild, das Erste, was man sieht, noch bevor man nach unten scrollt. Direkt danach folgen in der Regel die „Teaser“, kleine Appetithäppchen, die den Besucher tiefer in deine Seite hineinziehen sollen. Lass uns diese beiden fundamentalen Bausteine einer Startseite im Detail betrachten.

#### Der Hero-Bereich: Deine digitale Visitenkarte

Stell dir den Hero-Bereich wie das Cover eines Buches oder das Plakat für einen Film vor. Er muss in einem Augenblick das Thema, die Stimmung und den Hauptnutzen kommunizieren. Er befindet sich immer „above the fold“, also in dem Bereich des Bildschirms, der ohne Scrollen sichtbar ist. Seine Aufgabe ist es, die wichtigste Frage jedes neuen Besuchers zu beantworten: „Bin ich hier richtig und was bringt mir das?“

Ein typischer Hero-Bereich besteht aus drei Kernelementen:

1.  **Eine kraftvolle visuelle Komponente:** Meist ein großflächiges, hochauflösendes Bild, eine subtile Video-Schleife oder eine ansprechende Illustration, die sofort eine emotionale Verbindung herstellt.
2.  **Eine prägnante Botschaft:** Diese besteht aus einer Hauptüberschrift (der Headline) und oft einer unterstützenden Unterüberschrift (der Subline). Die Headline ist der Ort für dein zentrales Wertversprechen.
3.  **Eine klare Handlungsaufforderung (Call-to-Action, CTA):** Ein auffälliger Button, der den Nutzer zur wichtigsten Aktion leitet, die er auf deiner Seite ausführen soll – sei es „Jetzt kaufen“, „Mehr erfahren“ oder „Kostenlos registrieren“.

**Die semantische Struktur des Hero-Bereichs**

Für die Umsetzung in HTML ist es entscheidend, die richtigen semantischen Tags zu verwenden. Das hilft nicht nur Suchmaschinen, den Inhalt deiner Seite zu verstehen, sondern ist auch für die Barrierefreiheit (Accessibility) unerlässlich.

Der Hero-Bereich befindet sich in der Regel innerhalb des `<header>`-Elements der Seite, da er oft das Logo und die Hauptnavigation umgibt. Der inhaltliche Teil des Hero-Bereichs selbst wird jedoch am besten als eine eigene `<section>` ausgezeichnet.

Die Hauptüberschrift muss zwingend ein `<h1>`-Tag sein. Jede HTML-Seite sollte genau eine `<h1>` haben, und sie sollte die Kernaussage der gesamten Seite zusammenfassen. Der Hero-Bereich ist der perfekte Ort dafür. Die unterstützende Subline wird klassischerweise in einem `<p>`-Tag untergebracht. Der Call-to-Action ist fast immer ein Link (`<a>`), da er den Nutzer zu einer anderen Seite oder einem anderen Abschnitt führt. Auch wenn er aussieht wie ein Button, ist seine Funktion die Navigation – und dafür ist der `<a>`-Tag gedacht.

Schauen wir uns ein grundlegendes HTML-Gerüst für einen Hero-Bereich an:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meine Webseite</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <header class="site-header">
        <!-- Hier könnten Logo und Navigation platziert werden -->

        <section class="hero">
            <div class="hero-content">
                <h1>Die Zukunft des kreativen Arbeitens</h1>
                <p>Entdecke Tools und Techniken, die deinen Workflow revolutionieren und dir mehr Zeit für das Wesentliche geben.</p>
                <a href="/features" class="cta-button">Entdecke die Features</a>
            </div>
        </section>

    </header>

    <!-- ... der Rest der Seite folgt hier ... -->

</body>
</html>
```

In diesem Beispiel siehst du die klare Struktur:

*   Ein `<header>` umschließt den gesamten oberen Bereich.
*   Eine `<section>` mit der Klasse `hero` definiert den eigentlichen Hero-Bereich. Das hilft, ihn logisch vom Rest des Headers (wie z. B. einer Navigationsleiste) zu trennen.
*   Ein `<div>` mit der Klasse `hero-content` dient als Container, um die Textelemente und den Button zu gruppieren. Das ist nützlich für die spätere Positionierung mit CSS (z. B. um den Inhalt zu zentrieren).
*   Die `<h1>`, `<p>` und `<a>`-Tags sind semantisch korrekt für ihre jeweiligen Inhalte eingesetzt.

Die visuelle Magie – das Hintergrundbild, die zentrierte Ausrichtung des Textes, die Gestaltung des Buttons – wird vollständig über CSS gesteuert. Das HTML liefert hierfür lediglich das saubere und bedeutungsvolle Fundament.

#### Die Teaser: Wege in die Tiefe deiner Webseite

Nachdem der Hero-Bereich die Aufmerksamkeit des Besuchers gewonnen hat, besteht die nächste Aufgabe darin, sein Interesse zu kanalisieren und ihn zu weiterem Engagement zu bewegen. Hier kommen die Teaser ins Spiel. Sie sind wie Wegweiser, die auf die wichtigsten Inhalte oder Bereiche deiner Webseite hinweisen.

Teaser sind in der Regel in einem Raster oder einer Reihe direkt unterhalb des Hero-Bereichs angeordnet. Jeder Teaser stellt ein bestimmtes Thema, ein Produkt, einen Blogartikel oder eine Dienstleistung vor und besteht typischerweise aus:

*   Einem Bild oder einem Icon.
*   Einer kurzen, ansprechenden Überschrift.
*   Einem kurzen Beschreibungstext.
*   Einem Link zum weiterführenden Inhalt.

Ihre Aufgabe ist es nicht, alles zu erklären, sondern neugierig zu machen – eben „anzuteasern“.

**Die semantische Struktur von Teasern**

Eine Gruppe von Teasern bildet eine logische Einheit, daher ist es sinnvoll, sie in einem `<section>`-Element zusammenzufassen. Jeder einzelne Teaser ist ein in sich geschlossenes Inhaltselement. Für solche Elemente bietet HTML5 den `<article>`-Tag an. Ein `<article>` repräsentiert eine unabhängige, eigenständige Komposition in einem Dokument. Ein Teaser für einen Blogbeitrag oder ein Produkt passt perfekt in dieses Schema.

Innerhalb des `<article>`-Tags verwenden wir dann wieder bekannte Elemente:

*   Ein `<img>` für das Teaserbild. Denke hier an das `alt`-Attribut für die Barrierefreiheit!
*   Eine Überschrift, in der Regel eine `<h2>` oder `<h3>`, je nach Hierarchie deiner Dokumentenstruktur. Da die `<h1>` bereits im Hero-Bereich vergeben ist, ist `<h2>` hier eine logische Wahl.
*   Ein `<p>` für den kurzen Anreißertext.
*   Ein `<a>`-Tag für den Link, der oft als „Weiterlesen“ oder „Details anzeigen“ beschriftet ist.

Eine moderne und benutzerfreundliche Methode ist es, den gesamten Teaser-Block klickbar zu machen. Das erreichst du, indem du das gesamte `<article>`-Element in einen `<a>`-Tag einbettest. Das ist in HTML5 vollkommen valide, solange der Link keine weiteren interaktiven Elemente wie Buttons oder andere Links enthält.

Hier ist ein Beispiel für einen Teaser-Bereich, der auf den Hero-Bereich folgt:

```html
<!-- ... direkt nach dem schließenden </header>-Tag ... -->

<main>
    <section class="teaser-grid">
        <a href="/services/consulting" class="teaser-link">
            <article class="teaser-card">
                <img src="images/consulting.jpg" alt="Zwei Personen im Gespräch über einem Plan">
                <h2>Strategische Beratung</h2>
                <p>Wir analysieren deine Ziele und entwickeln eine maßgeschneiderte Strategie für deinen Erfolg.</p>
            </article>
        </a>

        <a href="/products/software" class="teaser-link">
            <article class="teaser-card">
                <img src="images/software-ui.jpg" alt="Screenshot einer modernen Benutzeroberfläche">
                <h2>Unsere Software</h2>
                <p>Leistungsstarke und intuitive Tools, die sich nahtlos in deinen Arbeitsalltag integrieren.</p>
            </article>
        </a>

        <a href="/blog/case-studies" class="teaser-link">
            <article class="teaser-card">
                <img src="images/success-graph.jpg" alt="Ein aufsteigender Graph symbolisiert Erfolg">
                <h2>Erfolgsgeschichten</h2>
                <p>Lies in unseren Fallstudien, wie wir anderen Unternehmen geholfen haben, zu wachsen.</p>
            </article>
        </a>
    </section>
</main>

<!-- ... weiterer Inhalt der Startseite ... -->
```

In diesem Code-Beispiel:

*   Das `<main>`-Element umschließt den Hauptinhalt der Seite und trennt ihn vom `<header>`.
*   Eine `<section>` mit der Klasse `teaser-grid` dient als Container für alle Teaser. Der Klassenname deutet bereits an, dass diese Sektion wahrscheinlich mit CSS Grid oder Flexbox als Raster dargestellt wird.
*   Jeder Teaser besteht aus einem `<a>`-Tag, der ein `<article>`-Element umschließt, um die gesamte Karte klickbar zu machen.
*   Die `<article>`-Tags enthalten die semantisch korrekten Elemente für Bild, Überschrift und Text.

Zusammengenommen bilden der Hero-Bereich und die Teaser eine kraftvolle Einheit. Der Hero fängt den Besucher mit einer starken, fokussierten Botschaft ein. Die Teaser nehmen diesen Impuls auf und bieten ihm klare, attraktive Optionen für den nächsten Schritt. Eine gut durchdachte HTML-Struktur ist dabei das unsichtbare, aber unverzichtbare Skelett, das diesen wichtigen Teil der User Journey stabil, verständlich und zugänglich macht.
