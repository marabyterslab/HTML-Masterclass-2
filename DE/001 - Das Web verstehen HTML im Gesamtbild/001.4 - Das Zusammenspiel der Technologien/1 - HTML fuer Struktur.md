# HTML für Struktur

### Kapitel 2: HTML als das Skelett des Webs – Die Kunst der Struktur

Stell dir vor, du baust ein Haus. Bevor du über Wandfarben, Möbel oder die Beleuchtung nachdenkst, brauchst du ein solides Fundament, tragende Wände, ein Dach und eine klare Raumaufteilung. Ohne diese Grundstruktur wäre alles, was du darauf aufbaust, instabil und chaotisch. Im Web ist HTML genau das: das Fundament, das Skelett, die unsichtbare, aber absolut entscheidende Struktur, die einer Webseite Halt und Sinn gibt.

Wenn wir über das Zusammenspiel der Web-Technologien sprechen, ist die Rollenverteilung klar:
*   **HTML (HyperText Markup Language)** ist für die **Struktur und Bedeutung** des Inhalts zuständig.
*   **CSS (Cascading Style Sheets)** kümmert sich um die **Präsentation und das Design** – die Wandfarben, Schriftarten und das Layout.
*   **JavaScript** ist für die **Interaktivität und Funktionalität** verantwortlich – die elektrischen Leitungen, der Aufzug, die smarte Türklingel.

In diesem Kapitel konzentrieren wir uns ausschließlich auf die erste und wichtigste Säule: HTML und seine Aufgabe, Ordnung ins Chaos der Informationen zu bringen.

#### Die grundlegende Anatomie einer HTML-Seite

Jede einzelne Webseite, die du jemals besucht hast, folgt im Kern einem identischen, einfachen Bauplan. Dieser Bauplan stellt sicher, dass der Browser versteht, was er vor sich hat und wie er den Inhalt interpretieren soll.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Titel der Webseite</title>
</head>
<body>
    <!-- Hier kommt der sichtbare Inhalt der Seite hin -->
</body>
</html>
```

Lass uns diese fundamentalen Bausteine kurz zerlegen:

*   **`<!DOCTYPE html>`**: Dies ist keine HTML-Markierung (Tag) im eigentlichen Sinne, sondern eine Anweisung an den Browser. Sie teilt ihm mit: "Achtung, was jetzt kommt, ist ein HTML5-Dokument. Bitte interpretiere es nach den modernen Regeln." Diese Zeile sollte immer am Anfang jedes HTML-Dokuments stehen.
*   **`<html>`**: Dies ist das Wurzelelement. Es umschließt alles andere auf der Seite. Das Attribut `lang="de"` ist eine wichtige Angabe für Barrierefreiheit und Suchmaschinen, da es die Hauptsprache des Dokuments als Deutsch deklariert.
*   **`<head>`**: Der "Kopf"-Bereich enthält Metadaten und Informationen *über* die Webseite, die nicht direkt im Browserfenster angezeigt werden. Dazu gehören der Titel, der im Browser-Tab erscheint (`<title>`), die Zeichenkodierung (`<meta charset="UTF-8">`), die für die korrekte Darstellung von Umlauten und Sonderzeichen sorgt, sowie Verknüpfungen zu externen Dateien wie CSS-Stylesheets oder Skripten.
*   **`<body>`**: Hier spielt die Musik. Alles, was du innerhalb des `<body>`-Tags platzierst – Texte, Bilder, Videos, Links – wird im Hauptfenster des Browsers sichtbar sein. Es ist der Bereich, in dem du die eigentliche Struktur deines Inhalts aufbaust.

#### Inhalte mit Bedeutung versehen: Semantisches HTML

In den Anfängen des Webs war HTML recht simpel. Man nutzte Tabellen für das Layout und generische Container-Elemente wie `<div>`, um alles Mögliche zu gruppieren. Das Problem dabei: Ein `<div>` sagt nichts über den Inhalt aus, den es umschließt. Es ist einfach nur eine Box.

Modernes HTML legt daher einen riesigen Wert auf **Semantik**. Das bedeutet, dass du Markierungen verwendest, die die Bedeutung und die Rolle des Inhalts beschreiben. Du sagst dem Browser (und damit auch Suchmaschinen und Screenreadern für Menschen mit Sehbehinderung) nicht nur, *wie* etwas aussehen soll, sondern vor allem, *was* es ist.

Ein gutes Beispiel ist die Gliederung von Textinhalten. Stell dir einen Zeitungsartikel vor. Er hat eine Hauptüberschrift, mehrere Zwischenüberschriften und Absätze. In HTML bildest du diese Struktur logisch ab:

```html
<body>
    <h1>Die geheime Welt der Tiefseequallen</h1>
    
    <p>Die Tiefsee ist einer der letzten unerforschten Orte unseres Planeten. In ihren dunklen Weiten verbergen sich Kreaturen, die wie aus einer anderen Welt wirken. Eine der faszinierendsten Gruppen sind die Tiefseequallen.</p>
    
    <h2>Leuchtende Jäger der Dunkelheit</h2>
    
    <p>Viele dieser Quallen haben die Fähigkeit zur Biolumineszenz entwickelt. Sie erzeugen ihr eigenes Licht, um Beute anzulocken oder Fressfeinde abzuschrecken. Dieses Leuchten ist oft das einzige Licht in tausenden Metern Tiefe.</p>
    
    <h2>Anpassung an extremen Druck</h2>
    
    <p>Der Druck in der Tiefsee ist immens. Die Körper dieser Tiere bestehen zu über 95 % aus Wasser, was ihnen hilft, dem Druck standzuhalten, ohne zerquetscht zu werden.</p>
</body>
```

Hier siehst du die wichtigsten Strukturelemente für Text:

*   **`<h1>` bis `<h6>`**: Dies sind die Überschriftenebenen. `<h1>` ist die wichtigste Hauptüberschrift der Seite und sollte nur einmal vorkommen. `<h2>` ist eine Unterüberschrift, `<h3>` eine weitere Unterebene davon und so weiter. Du nutzt sie, um eine klare, logische Hierarchie zu schaffen, genau wie in einem Buchkapitel. Du wählst sie nicht aufgrund ihrer Größe aus – das ist Aufgabe von CSS –, sondern aufgrund ihrer strukturellen Bedeutung.
*   **`<p>`**: Das `p` steht für "paragraph" (Absatz). Es umschließt einen zusammenhängenden Textblock. Jeder neue Gedanke oder thematische Abschnitt bekommt sein eigenes `<p>`-Tag.

#### Die grobe Seitengliederung: Wo gehört was hin?

Über die reine Textstruktur hinaus bietet HTML5 eine Reihe von semantischen Elementen, um die großen Bereiche einer Webseite zu definieren. Diese helfen dabei, eine Seite wie eine Landkarte lesbar zu machen.

Stell dir eine typische Blog-Seite vor. Sie hat oben eine Kopfzeile mit Logo und Navigation, in der Mitte den Hauptinhalt und unten eine Fußzeile mit Copyright-Informationen. Statt alles in `<div>`-Boxen zu packen, verwenden wir dafür sprechende Tags:

```html
<body>
    <header>
        <!-- Kopfbereich der Seite -->
        <img src="logo.png" alt="Mein Blog Logo">
        <nav>
            <!-- Hauptnavigation -->
            <ul>
                <li><a href="/">Startseite</a></li>
                <li><a href="/ueber-mich">Über mich</a></li>
                <li><a href="/kontakt">Kontakt</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <!-- Der einzigartige Hauptinhalt der Seite -->
        <article>
            <h1>Der Titel meines Blogartikels</h1>
            <p>Hier steht der erste Absatz des Artikels...</p>
            <p>Und hier ein weiterer Absatz...</p>
        </article>
    </main>

    <aside>
        <!-- Seitenleiste mit Zusatzinformationen -->
        <h2>Ähnliche Artikel</h2>
        <ul>
            <li><a href="/artikel-2">Ein anderer spannender Artikel</a></li>
            <li><a href="/artikel-3">Noch mehr Lesestoff</a></li>
        </ul>
    </aside>

    <footer>
        <!-- Fußbereich der Seite -->
        <p>&copy; 2023 Mein Name</p>
    </footer>
</body>
```

Analysieren wir diese neuen Strukturelemente:

*   **`<header>`**: Definiert den Kopfbereich einer Seite oder eines Abschnitts. Hier finden sich oft das Logo, der Seitentitel und die Hauptnavigation.
*   **`<nav>`**: Ist speziell für Navigationsblöcke vorgesehen. Ob Hauptnavigation, eine Brotkrümelnavigation oder ein Inhaltsverzeichnis – wenn es eine Sammlung von Links zur Orientierung ist, gehört sie in ein `<nav>`-Tag.
*   **`<main>`**: Umschließt den zentralen, einzigartigen Inhalt der Seite. Pro Seite sollte es nur ein `<main>`-Element geben. Alles, was nicht wiederkehrender Inhalt wie Header, Footer oder Sidebar ist, gehört hier hinein.
*   **`<article>`**: Repräsentiert einen in sich geschlossenen, eigenständigen Inhalt, der potenziell auch an anderer Stelle (z.B. in einem RSS-Feed) Sinn ergeben würde. Ein Blogbeitrag, ein Forenpost oder ein Zeitungsartikel sind perfekte Kandidaten für `<article>`.
*   **`<section>`**: Gruppiert thematisch zusammengehörige Inhalte. Ein `<article>` könnte zum Beispiel in mehrere `<section>`-Elemente unterteilt sein, etwa "Einleitung", "Hauptteil" und "Fazit".
*   **`<aside>`**: Beinhaltet Inhalte, die nur lose mit dem Hauptinhalt zu tun haben. Die klassische Seitenleiste (Sidebar) mit Werbung, weiterführenden Links oder einer Autorenbiografie ist ein typischer Anwendungsfall.
*   **`<footer>`**: Kennzeichnet den Fußbereich einer Seite oder eines Abschnitts. Hier stehen üblicherweise Copyright-Hinweise, Links zum Impressum, Datenschutz oder Social-Media-Profile.

Die Verwendung dieser Tags ist keine bloße Formsache. Eine Maschine, wie der Google-Bot, kann eine mit `<nav>` ausgezeichnete Navigation sofort als solche erkennen. Ein Screenreader kann einem blinden Nutzer anbieten: "Möchtest du direkt zum Hauptinhalt springen?" – und überspringt dann `<header>` und `<nav>`, um direkt bei `<main>` zu landen. Du schaffst damit eine robustere, zugänglichere und besser verständliche Webseite, ohne auch nur eine Zeile CSS oder JavaScript geschrieben zu haben.

#### Block vs. Inline: Ein kleiner, aber feiner Unterschied

Zum Abschluss der Strukturbetrachtung ist es wichtig, den Unterschied zwischen zwei fundamentalen Element-Typen in HTML zu verstehen: Block-Level-Elemente und Inline-Elemente.

*   **Block-Level-Elemente** nehmen standardmäßig die gesamte verfügbare Breite ein und erzeugen vor und nach sich einen Zeilenumbruch. Sie bilden die groben Blöcke deiner Struktur. Beispiele sind `<h1>`, `<p>`, `<div>`, `<header>`, `<footer>`, `<li>`.
*   **Inline-Elemente** nehmen nur so viel Platz ein, wie ihr Inhalt benötigt, und fügen sich in den Textfluss ein, ohne einen Zeilenumbruch zu erzeugen. Sie werden verwendet, um kleine Teile innerhalb eines Blocks auszuzeichnen. Beispiele sind `<a>` (für Links), `<strong>` (für stark betonte Texte), `<em>` (für hervorgehobene Texte) oder `<span>` (ein generischer Inline-Container ohne semantische Bedeutung).

Wenn du schreibst `<p>Das ist ein <strong>wichtiger</strong> Punkt.</p>`, dann bleibt das Wort "wichtiger" in derselben Zeile wie der Rest des Satzes, weil `<strong>` ein Inline-Element ist. Es formatiert nur diesen Teil des Textes, ohne den Fluss zu unterbrechen. Ein `<p>`-Tag hingegen würde immer in einer neuen Zeile beginnen.

Das Verständnis dieser grundlegenden Unterscheidung ist der Schlüssel, um später nachzuvollziehen, warum sich Elemente beim Styling mit CSS auf eine bestimmte Weise verhalten.

HTML für die Struktur zu nutzen, bedeutet also, wie ein Architekt zu denken. Du definierst Räume, gibst ihnen einen Zweck und baust eine logische, stabile und für jeden verständliche Hierarchie auf. Diese saubere Struktur ist die Leinwand, auf der du mit CSS malen und mit JavaScript Leben einhauchen wirst. Ohne sie ist alles nur ein Haufen Farbe auf dem Boden.
