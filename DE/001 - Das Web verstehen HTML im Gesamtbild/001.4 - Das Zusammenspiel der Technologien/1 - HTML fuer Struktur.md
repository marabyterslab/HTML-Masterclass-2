# HTML für Struktur

### HTML für Struktur: Das Fundament deiner Webseite

Stell dir vor, du baust ein Haus. Bevor du dir Gedanken über die Wandfarbe, die Möbel oder die schicken Lampen machst, brauchst du ein solides Fundament, tragende Wände, ein Dach und eine klare Aufteilung der Räume. Du definierst, wo das Wohnzimmer, die Küche und das Schlafzimmer sein werden. Diese grundlegende Architektur gibt dem Haus seine Form und seinen Zweck. Ohne sie wäre alles nur ein chaotischer Haufen Baumaterial.

Genau diese Rolle übernimmt HTML (HyperText Markup Language) für eine Webseite. HTML ist die Sprache, die du verwendest, um die **Struktur** und die **Bedeutung** deiner Inhalte festzulegen. Es ist das Skelett, das alles zusammenhält.

Es ist entscheidend, diesen Punkt von Anfang an zu verinnerlichen: HTML ist nicht für das Aussehen da. Das ist die alleinige Aufgabe von CSS (Cascading Style Sheets). HTML kümmert sich nicht um Farben, Schriftgrößen oder Abstände. HTML sagt dem Browser nur, *was* etwas ist: Das hier ist eine Überschrift. Das ist ein Absatz. Dies ist eine Liste von Navigationspunkten. Jener Block ist der Hauptinhalt der Seite.

#### Die Magie der Semantik

Wenn wir davon sprechen, dem Inhalt eine Bedeutung zu geben, sprechen wir von **Semantik**. Semantisches HTML bedeutet, die HTML-Tags so zu verwenden, wie sie gedacht sind – entsprechend ihrer Bedeutung.

Warum ist das so unglaublich wichtig? Aus mehreren Gründen:

1.  **Zugänglichkeit (Accessibility):** Stell dir vor, eine Person mit einer Sehbehinderung besucht deine Seite und nutzt einen Screenreader. Diese Software liest den Inhalt der Seite vor. Ein Screenreader versteht keine visuellen Hinweise wie fette Schrift oder große Buchstaben. Aber er versteht HTML-Tags. Wenn er auf ein `<h1>`-Tag stößt, weiß er: „Aha, das ist die Hauptüberschrift der Seite.“ Trifft er auf ein `<nav>`-Tag, kann er dem Nutzer sagen: „Hier beginnt die Navigation.“ Nutzt du hingegen bedeutungslose `<div>`-Elemente für alles und machst sie nur mit CSS groß und fett, hat der Screenreader keine Ahnung, was die logische Struktur ist. Eine semantisch korrekte Seite ist für alle Menschen nutzbar.

2.  **Suchmaschinenoptimierung (SEO):** Suchmaschinen wie Google sind im Grunde genommen blinde, aber sehr schlaue Roboter. Sie durchforsten deine Seite, um zu verstehen, worum es geht und wie die Inhalte gewichtet sind. Ein Begriff in einer `<h1>`-Überschrift hat für Google eine viel höhere Relevanz als derselbe Begriff in einem einfachen `<p>`-Absatz. Durch die Verwendung semantischer Tags hilfst du Suchmaschinen, deine Inhalte korrekt zu indizieren und zu bewerten, was zu einem besseren Ranking führen kann.

3.  **Wartbarkeit und Lesbarkeit:** Wenn du oder jemand aus deinem Team den Code in sechs Monaten wieder öffnet, sorgt semantisches HTML für sofortige Klarheit. Eine Struktur aus `<header>`, `<main>`, `<article>` und `<footer>` ist selbsterklärend. Eine Struktur, die nur aus verschachtelten `<div>`-Elementen besteht (oft als „Div-Suppe“ bezeichnet), ist ein Albtraum zu verstehen und zu pflegen.

#### Der grundlegende Aufbau eines HTML-Dokuments

Jedes HTML-Dokument folgt einer grundlegenden, standardisierten Struktur. Sie sieht immer so aus:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Titel der Seite</title>
</head>
<body>
    <!-- Hier kommt der sichtbare Inhalt deiner Webseite hin -->
</body>
</html>
```

Lass uns das kurz aufschlüsseln:
*   `<!DOCTYPE html>`: Dies ist keine HTML-Tag, sondern eine Anweisung an den Browser. Sie teilt ihm mit: „Achtung, was jetzt kommt, ist modernes HTML nach dem HTML5-Standard.“
*   `<html>`: Das ist das Wurzelelement, das alles andere umschließt. Das Attribut `lang="de"` gibt an, dass die Hauptsprache der Seite Deutsch ist – wichtig für Screenreader und Suchmaschinen.
*   `<head>`: Dieser Bereich enthält Metadaten, also Informationen *über* die Webseite, die nicht direkt auf der Seite sichtbar sind.
    *   `<meta charset="UTF-8">`: Legt die Zeichenkodierung fest, damit Umlaute wie ä, ö, ü und andere Sonderzeichen korrekt dargestellt werden.
    *   `<meta name="viewport" ...>`: Eine entscheidende Zeile für responsives Webdesign, die sicherstellt, dass die Seite auf mobilen Geräten korrekt skaliert wird.
    *   `<title>`: Der Text, der im Browser-Tab angezeigt wird. Extrem wichtig für SEO und die Benutzerfreundlichkeit.
*   `<body>`: Hier passiert die eigentliche Magie. Alles, was du innerhalb des `<body>`-Tags schreibst, ist für den Besucher im Browserfenster sichtbar. Hier baust du deine Inhaltsstruktur auf.

#### Die wichtigsten Bausteine der Struktur

Innerhalb des `<body>` verwendest du verschiedene Tags, um deine Inhalte zu strukturieren. Hier sind die fundamentalen Werkzeuge in deinem Kasten:

**Überschriften und Absätze**
Überschriften gliedern deinen Inhalt hierarchisch. Es gibt sechs Ebenen, von `<h1>` bis `<h6>`.

*   `<h1>`: Die Hauptüberschrift der Seite. Es sollte pro Seite nur eine einzige `<h1>` geben. Sie fasst das zentrale Thema zusammen.
*   `<h2>`: Unterüberschriften, die große Abschnitte gliedern.
*   `<h3>` bis `<h6>`: Weitere Unterteilungen. Wichtig ist, keine Ebenen zu überspringen (also nicht von `<h2>` direkt zu `<h4>`).

Der Fließtext steht in Absätzen, die durch das `<p>`-Tag (Paragraph) definiert werden.

```html
<h1>Der Titel meines fantastischen Blogartikels</h1>
<p>Dies ist der einleitende Absatz, der das Thema kurz umreißt und den Leser neugierig macht.</p>

<h2>Ein wichtiger Unterpunkt</h2>
<p>Hier gehe ich detaillierter auf den ersten Aspekt des Themas ein und erkläre die Zusammenhänge.</p>

<h2>Ein weiterer relevanter Aspekt</h2>
<p>Dieser Absatz behandelt einen zweiten, ebenso wichtigen Punkt.</p>
```

**Listen**
Listen sind perfekt, um zusammengehörige Punkte zu gruppieren. Es gibt zwei Haupttypen:

*   `<ul>` (Unordered List): Eine unsortierte Liste, typischerweise mit Aufzählungszeichen dargestellt.
*   `<ol>` (Ordered List): Eine geordnete, nummerierte Liste.

Beide Listentypen enthalten `<li>`-Elemente (List Item) für die einzelnen Punkte.

```html
<!-- Unsortierte Liste -->
<ul>
    <li>Erster Punkt</li>
    <li>Zweiter Punkt</li>
    <li>Dritter Punkt</li>
</ul>

<!-- Geordnete Liste -->
<ol>
    <li>Schritt 1: Zutat vorbereiten</li>
    <li>Schritt 2: Alles vermischen</li>
    <li>Schritt 3: Backen und genießen</li>
</ol>
```

**Layout-Elemente für die Gesamtstruktur**
Früher wurden Webseiten-Layouts oft mit Tabellen oder unzähligen `<div>`-Elementen gebaut. HTML5 hat eine Reihe von semantischen Tags eingeführt, die speziell dazu dienen, die großen Bereiche einer Seite zu definieren. Sie machen deine Struktur sofort verständlich.

*   `<header>`: Der Kopfbereich einer Seite oder eines Abschnitts. Enthält oft das Logo, den Seitentitel und die Hauptnavigation.
*   `<nav>`: Definiert einen Block mit Navigationslinks.
*   `<main>`: Umschließt den Hauptinhalt der Seite. Der Inhalt hier sollte einzigartig für diese spezifische Seite sein und nicht auf anderen Seiten wiederholt werden (wie z.B. der Header oder Footer).
*   `<article>`: Ein in sich geschlossener, eigenständiger Inhaltsblock, der auch für sich allein Sinn ergeben würde. Beispiele sind ein Blogbeitrag, ein Zeitungsartikel oder ein Forumspost.
*   `<section>`: Ein thematischer Abschnitt innerhalb des Dokuments. Eine Landingpage könnte zum Beispiel Sektionen für "Über uns", "Unsere Produkte" und "Kontakt" haben.
*   `<aside>`: Für Inhalte, die nur lose mit dem Hauptinhalt in Beziehung stehen, wie eine Seitenleiste (Sidebar) mit verwandten Links, Werbung oder einer Autorenbiografie.
*   `<footer>`: Der Fußbereich einer Seite oder eines Abschnitts. Enthält typischerweise Copyright-Informationen, Links zum Impressum oder Kontaktinformationen.

So könnte die grobe Struktur einer typischen Blog-Seite aussehen:

```html
<body>
    <header>
        <h1>Mein Blog</h1>
        <nav>
            <ul>
                <li><a href="/">Startseite</a></li>
                <li><a href="/ueber-mich">Über mich</a></li>
                <li><a href="/kontakt">Kontakt</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <article>
            <h2>Der Titel des Blogbeitrags</h2>
            <p>Der erste Absatz des Inhalts...</p>
            <p>...und noch viel mehr Text.</p>
        </article>
        
        <aside>
            <h3>Verwandte Beiträge</h3>
            <ul>
                <li><a href="#">Ein anderer cooler Beitrag</a></li>
                <li><a href="#">Noch ein Beitrag</a></li>
            </ul>
        </aside>
    </main>

    <footer>
        <p>&copy; 2024 Mein Name. Alle Rechte vorbehalten.</p>
    </footer>
</body>
```

**Die neutralen Container: `<div>` und `<span>`**
Was ist, wenn du Elemente gruppieren musst, aber keines der semantischen Tags passt? Vielleicht brauchst du einen Container nur für Styling-Zwecke, um beispielsweise zwei Absätze zusammen mit einem Bild mit einem Rahmen zu versehen. Hier kommen `<div>` und `<span>` ins Spiel.

*   `<div>`: Ein Block-Level-Container ohne eigene semantische Bedeutung. Er dient als allgemeine "Box", um andere Elemente zu gruppieren.
*   `<span>`: Ein Inline-Container ohne eigene semantische Bedeutung. Er wird verwendet, um einen kleinen Teil innerhalb eines Textes zu umschließen, zum Beispiel um ein einzelnes Wort anders zu färben.

Die goldene Regel lautet: Nutze immer zuerst ein passendes semantisches Element. Nur wenn es absolut kein passendes gibt, greifst du zu `<div>` oder `<span>`. Sie sind deine Werkzeuge für den Notfall, nicht dein Standardbaustein.

Indem du HTML meisterhaft für die Strukturierung deiner Inhalte einsetzt, legst du das bestmögliche Fundament. Deine Webseite wird nicht nur für Menschen mit und ohne Einschränkungen zugänglich, sondern auch für Suchmaschinen verständlich und für dich und dein Team langfristig wartbar. Du schaffst eine robuste Architektur, auf der die visuellen Schichten von CSS und die interaktiven Funktionen von JavaScript perfekt aufbauen können.
