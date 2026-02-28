# Struktur einer Landingpage

### Struktur einer Landingpage

Eine Landingpage ist keine gewöhnliche Webseite. Sie ist ein hochspezialisiertes Werkzeug mit einem einzigen, klar definierten Ziel: die Konversion. Ob es darum geht, ein Produkt zu verkaufen, E-Mail-Adressen zu sammeln oder Anmeldungen für ein Webinar zu generieren – alles an einer Landingpage ist diesem einen Ziel untergeordnet. Deine Aufgabe als Entwickler ist es, dieser zielgerichteten Botschaft eine ebenso klare und logische Struktur mit semantischem HTML zu geben. Eine gute Struktur sorgt nicht nur für sauberen Code, sondern verbessert auch die Suchmaschinenoptimierung (SEO) und die Barrierefreiheit.

Stell dir die Struktur einer Landingpage wie das Skelett eines Sprinters vor: Jedes Teil ist optimiert, um das Ziel so schnell und effizient wie möglich zu erreichen. Es gibt keinen überflüssigen Ballast.

#### Das Grundgerüst: Header, Main, Footer

Auch wenn eine Landingpage oft wie eine einzige, durchgehende Seite wirkt, profitiert sie von der grundlegenden semantischen Dreiteilung, die du bereits kennst: `<header>`, `<main>` und `<footer>`.

*   **`<header>`:** Auf einer Landingpage ist der Header oft minimalistisch. Manchmal enthält er nur das Logo des Unternehmens. Der Grund dafür ist einfach: Du willst Ablenkungen vermeiden. Eine umfangreiche Navigation, die auf andere Teile der Website verweist, würde den Besucher nur vom eigentlichen Ziel weglocken.
*   **`<main>`:** Dies ist das Herzstück deiner Landingpage. Hier findet die gesamte Überzeugungsarbeit statt. Der `<main>`-Bereich umschließt alle inhaltlichen Abschnitte, die den Nutzer zur Konversion führen sollen.
*   **`<footer>`:** Der Footer enthält in der Regel die notwendigen, aber für die Konversion zweitrangigen Informationen wie Impressum, Datenschutz und eventuell Kontaktinformationen.

Ein einfaches Grundgerüst könnte so aussehen:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Das ultimative Produkt - Landingpage</title>
</head>
<body>

    <header>
        <!-- Minimalistisch: oft nur ein Logo -->
        <img src="logo.svg" alt="Firmenlogo">
    </header>

    <main>
        <!-- Hier passiert die Magie -->
    </main>

    <footer>
        <!-- Rechtliche Hinweise und Kontakt -->
        <p>&copy; 2023 Firmenname. Alle Rechte vorbehalten.</p>
        <nav>
            <a href="/impressum">Impressum</a> | 
            <a href="/datenschutz">Datenschutz</a>
        </nav>
    </footer>

</body>
</html>
```

#### Die Anatomie des `<main>`-Elements: Die Überzeugungskette

Innerhalb des `<main>`-Tags baust du eine Kette von Argumenten auf, die den Nutzer logisch und emotional durch die Seite führt. Jeder dieser logischen Blöcke sollte in einem eigenen `<section>`-Element untergebracht werden. Dies gliedert nicht nur deinen Code, sondern ermöglicht es auch Screenreadern und Suchmaschinen, die Struktur deiner Seite zu verstehen.

##### 1. Der "Hero"-Bereich: Der erste Eindruck

Der erste Abschnitt, den ein Besucher sieht, wird als "Hero Section" bezeichnet. Er muss in wenigen Sekunden die Aufmerksamkeit fesseln und die Kernbotschaft vermitteln.

*   **Die Hauptüberschrift (`<h1>`):** Dies ist die wichtigste Überschrift deiner Seite. Sie muss das zentrale Nutzenversprechen klar kommunizieren. Es gibt nur eine `<h1>` pro Seite.
*   **Die Unterüberschrift (`<p>`):** Ein kurzer Absatz, der die Hauptüberschrift konkretisiert oder erweitert.
*   **Der Call-to-Action (CTA):** Die Handlungsaufforderung. Meist ein auffälliger Button, der semantisch ein Link (`<a>`) ist, der entweder zu einem anderen Teil der Seite oder zu einem Formular führt.
*   **Visuelle Unterstützung:** Oft ein Bild (`<img>`) oder ein Video, das das Produkt oder das gewünschte Ergebnis zeigt.

```html
<section class="hero">
    <h1>Die einfachste Art, deine Termine zu organisieren</h1>
    <p>Verabschiede dich von Zettelwirtschaft und verpassten Fristen. Gewinne Klarheit und Fokus zurück.</p>
    <a href="#anmeldung" class="cta-button">Jetzt kostenlos starten</a>
    <img src="hero-dashboard.jpg" alt="Screenshot der aufgeräumten Kalender-App">
</section>
```

##### 2. Das Problem und die Lösung (oder Merkmale und Vorteile)

Nachdem du das Interesse geweckt hast, musst du Vertrauen aufbauen und dein Angebot im Detail erklären. In diesem Abschnitt zeigst du dem Nutzer, dass du sein Problem verstehst und die perfekte Lösung dafür hast.

*   **Abschnittsüberschrift (`<h2>`):** Eine klare Überschrift, die den Inhalt des Abschnitts beschreibt, z.B. "Warum du uns lieben wirst".
*   **Feature-/Benefit-Liste:** Oft als Liste (`<ul>`) oder in mehreren Spalten dargestellt. Jedes Element hebt ein Merkmal und den daraus resultierenden Vorteil hervor. Semantisch könntest du hier pro Vorteil ein `<li>` oder sogar einen eigenen `<div>`-Container mit einer `<h3>` und einem `<p>` verwenden.

```html
<section class="features">
    <h2>Alles, was du für perfekte Organisation brauchst</h2>
    <ul>
        <li>
            <h3>Drag & Drop Kalender</h3>
            <p>Plane deine Woche intuitiv und flexibel, ohne dich durch Menüs zu klicken.</p>
        </li>
        <li>
            <h3>Automatische Erinnerungen</h3>
            <p>Verpasse nie wieder einen wichtigen Termin. Wir erinnern dich per E-Mail oder Push-Nachricht.</p>
        </li>
        <li>
            <h3>Team-Kollaboration</h3>
            <p>Teile Kalender mit deinem Team und behaltet gemeinsam den Überblick über Projekte.</p>
        </li>
    </ul>
</section>
```

##### 3. Social Proof: Vertrauen durch andere

Menschen vertrauen den Meinungen anderer Menschen. Deshalb ist "Social Proof" (sozialer Beweis) ein entscheidender Baustein. Das können Kundenstimmen (Testimonials), Logos bekannter Kunden oder positive Bewertungen sein.

*   **Kundenstimmen:** Für Zitate ist das `<blockquote>`-Element die semantisch korrekte Wahl. Der Name der Person oder der Firma wird im `<cite>`-Element platziert.
*   **Logos:** Eine einfache Liste von Bildern in einem `<div>` oder `<ul>` kann hier ausreichen.

```html
<section class="social-proof">
    <h2>Tausende Nutzer sind bereits begeistert</h2>
    <figure>
        <blockquote>
            <p>"Diese App hat mein Arbeitsleben revolutioniert. Endlich habe ich wieder den Kopf frei für die wichtigen Dinge."</p>
        </blockquote>
        <figcaption>
            <cite>Maria Muster, CEO bei TechSolutions</cite>
        </figcaption>
    </figure>
    <figure>
        <blockquote>
            <p>"Einfach, intuitiv und extrem zuverlässig. Ich kann es jedem empfehlen!"</p>
        </blockquote>
        <figcaption>
            <cite>Max Meier, Freiberufler</cite>
        </figcaption>
    </figure>
</section>
```

##### 4. Der finale Call-to-Action (CTA)

Nachdem du alle Argumente präsentiert hast, ist es an der Zeit, den Sack zuzumachen. Am Ende des `<main>`-Bereichs, direkt vor dem Footer, platzierst du oft einen letzten, unmissverständlichen Call-to-Action. Dieser Abschnitt ist meist einfach gehalten und wiederholt das Hauptversprechen und den Button aus dem Hero-Bereich, um dem Nutzer eine letzte, bequeme Möglichkeit zur Konversion zu geben.

```html
<section id="anmeldung" class="final-cta">
    <h2>Bereit, die Kontrolle zurückzugewinnen?</h2>
    <p>Starte noch heute deinen kostenlosen 30-Tage-Test. Keine Kreditkarte erforderlich.</p>
    <a href="/signup" class="cta-button">Jetzt kostenlos testen</a>
</section>
```

#### Der vollständige Plan: Alles zusammengefügt

Wenn wir all diese Teile zusammensetzen, ergibt sich eine klare, logische und semantisch wertvolle Struktur für eine Landingpage. Diese Struktur ist nicht nur für Menschen leicht zu erfassen, sondern auch für Maschinen. Suchmaschinen erkennen die Hierarchie der Informationen durch die `h1`-`h6`-Tags, und assistive Technologien wie Screenreader können Nutzern eine sinnvolle Navigation durch die Abschnitte (`<section>`) anbieten.

Hier ist das vollständige Beispiel in seiner strukturellen Gesamtheit:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Das ultimative Produkt - Landingpage</title>
    <!-- Hier kommen CSS-Links etc. -->
</head>
<body>

    <header>
        <a href="/">
            <img src="logo.svg" alt="Firmenlogo">
        </a>
    </header>

    <main>
        <!-- 1. Hero Section: Aufmerksamkeit erregen -->
        <section class="hero">
            <h1>Die einfachste Art, deine Termine zu organisieren</h1>
            <p>Verabschiede dich von Zettelwirtschaft und verpassten Fristen. Gewinne Klarheit und Fokus zurück.</p>
            <a href="#anmeldung" class="cta-button">Jetzt kostenlos starten</a>
            <img src="hero-dashboard.jpg" alt="Screenshot der aufgeräumten Kalender-App">
        </section>

        <!-- 2. Features/Benefits: Lösung präsentieren -->
        <section class="features">
            <h2>Alles, was du für perfekte Organisation brauchst</h2>
            <ul>
                <li>
                    <h3>Drag & Drop Kalender</h3>
                    <p>Plane deine Woche intuitiv und flexibel, ohne dich durch Menüs zu klicken.</p>
                </li>
                <li>
                    <h3>Automatische Erinnerungen</h3>
                    <p>Verpasse nie wieder einen wichtigen Termin. Wir erinnern dich per E-Mail oder Push-Nachricht.</p>
                </li>
            </ul>
        </section>

        <!-- 3. Social Proof: Vertrauen aufbauen -->
        <section class="social-proof">
            <h2>Tausende Nutzer sind bereits begeistert</h2>
            <figure>
                <blockquote>
                    <p>"Diese App hat mein Arbeitsleben revolutioniert."</p>
                </blockquote>
                <figcaption>
                    <cite>Maria Muster, CEO bei TechSolutions</cite>
                </figcaption>
            </figure>
        </section>

        <!-- 4. Final CTA: Konversion abschließen -->
        <section id="anmeldung" class="final-cta">
            <h2>Bereit, die Kontrolle zurückzugewinnen?</h2>
            <a href="/signup" class="cta-button">Jetzt kostenlos testen</a>
        </section>

    </main>

    <footer>
        <p>&copy; 2023 Firmenname. Alle Rechte vorbehalten.</p>
        <nav>
            <a href="/impressum">Impressum</a> | 
            <a href="/datenschutz">Datenschutz</a>
        </nav>
    </footer>

</body>
</html>
```

Diese Struktur dient als robustes Fundament. Das visuelle Design wird mit CSS umgesetzt, die Interaktivität mit JavaScript – aber die logische, semantische Ordnung, die du mit HTML schaffst, ist die Basis, auf der alles andere aufbaut. Sie ist der Schlüssel zu einer performanten, zugänglichen und erfolgreichen Landingpage.
