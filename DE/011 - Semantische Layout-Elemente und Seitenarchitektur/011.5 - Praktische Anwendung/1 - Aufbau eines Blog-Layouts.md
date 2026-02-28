# Aufbau eines Blog-Layouts

### Aufbau eines Blog-Layouts

Wenn du an eine Webseite denkst, ist die Struktur eines Blogs eines der klassischsten und verständlichsten Beispiele. Es gibt einen Kopfbereich, einen Hauptinhalt, oft eine Seitenleiste und einen Fußbereich. Diese klare Gliederung findet sich millionenfach im Web und ist ein perfektes Übungsfeld, um die semantischen Layout-Elemente von HTML in der Praxis zu sehen. Sie geben deiner Seite nicht nur eine sichtbare Struktur, sondern auch eine maschinenlesbare Bedeutung, was für Suchmaschinen und Barrierefreiheit von unschätzbarem Wert ist.

Lass uns gemeinsam eine solche Blog-Struktur von Grund auf mit den passenden HTML-Elementen nachbauen. Wir konzentrieren uns dabei ausschließlich auf das HTML-Grundgerüst, das später mit CSS gestaltet werden kann.

#### Die grobe Aufteilung: Die Hauptbereiche der Seite

Jede gute Architektur beginnt mit einem Plan der großen Bereiche. Bei einem Blog sind das typischerweise:

1.  **Der Kopfbereich (`<header>`):** Hier finden sich meist das Logo, der Name des Blogs und die Hauptnavigation, mit der du zu den wichtigsten Seiten wie "Home", "Über mich" oder "Kontakt" gelangst.
2.  **Der Hauptinhaltsbereich (`<main>`):** Das ist das Herzstück der Seite. Hier stehen die Blogartikel. Auf der Startseite sind es vielleicht mehrere Teaser, auf einer Artikelseite ist es der vollständige Beitrag.
3.  **Die Seitenleiste (`<aside>`):** Sie enthält ergänzende, aber nicht essenzielle Informationen. Das können Links zu den neuesten Beiträgen, eine Kategorienliste, ein Archiv oder auch Werbung sein.
4.  **Der Fußbereich (`<footer>`):** Ganz unten auf der Seite stehen oft Copyright-Hinweise, Links zum Impressum, zur Datenschutzerklärung oder zu sozialen Netzwerken.

Diese vier Bereiche bilden das Skelett unserer Seite. HTML5 bietet uns für jeden dieser Bereiche ein passendes, "sprechendes" Element.

#### Vom Plan zum Code: Die semantischen Elemente im Einsatz

Sehen wir uns an, wie wir diese Struktur in HTML-Code umsetzen. Die Basis ist ein leeres HTML-Dokument. Innerhalb des `<body>`-Tags bauen wir unser Layout auf.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mein fantastischer Blog</title>
</head>
<body>

    <!-- Der Kopfbereich der gesamten Seite -->
    <header>
        <h1>Mein fantastischer Blog</h1>
        <nav>
            <ul>
                <li><a href="/">Home</a></li>
                <li><a href="/ueber-mich">Über mich</a></li>
                <li><a href="/kontakt">Kontakt</a></li>
            </ul>
        </nav>
    </header>

    <!-- Ein Wrapper-Div für das zweispaltige Layout (Hauptinhalt + Seitenleiste) -->
    <div class="container">

        <!-- Der Hauptinhalt der Seite -->
        <main>
            <!-- Hier kommen die Blogartikel -->
        </main>

        <!-- Die Seitenleiste -->
        <aside>
            <!-- Hier kommen die zusätzlichen Informationen -->
        </aside>

    </div>

    <!-- Der Fußbereich der gesamten Seite -->
    <footer>
        <p>&copy; 2023 Mein fantastischer Blog. Alle Rechte vorbehalten.</p>
        <p>
            <a href="/impressum">Impressum</a> | 
            <a href="/datenschutz">Datenschutz</a>
        </p>
    </footer>

</body>
</html>
```

In diesem ersten Gerüst siehst du bereits die Hauptelemente in Aktion: `<header>`, `<main>`, `<aside>` und `<footer>`. Der `<h1>`-Tag im Header ist für den Haupttitel der Seite reserviert – ideal für den Namen deines Blogs. Die Navigation (`<nav>`) umschließt die Liste der Hauptlinks und signalisiert damit klar ihre Funktion.

Du bemerkst vielleicht das `div` mit der Klasse `container`. Obwohl wir semantische Elemente nutzen, haben `div`-Elemente immer noch ihre Berechtigung. In diesem Fall dient es als reiner Styling-Container, um `<main>` und `<aside>` später per CSS nebeneinander anordnen zu können. Es hat keine eigene inhaltliche Bedeutung, sondern ist ein reines Hilfsmittel für das Layout.

#### Das Herzstück füllen: Der Blogartikel (`<article>`)

Der `<main>`-Bereich ist noch leer. Füllen wir ihn mit dem, was einen Blog ausmacht: Artikeln. Für in sich geschlossene, eigenständige Inhalte wie einen Blogbeitrag, einen Forenpost oder eine Produktkarte gibt es das `<article>`-Element. Es ist so konzipiert, dass sein Inhalt auch losgelöst vom Rest der Seite Sinn ergibt und theoretisch an anderer Stelle (z. B. in einem RSS-Feed) wiederverwendet werden könnte.

Ein einzelner Blogartikel hat oft selbst wieder eine innere Struktur: eine Überschrift, Metadaten (Autor, Datum), den eigentlichen Text und vielleicht einen kleinen Fußbereich mit Tags oder Social-Media-Links.

```html
<main>
    <article>
        <header>
            <h2>Die Kunst der semantischen HTML-Struktur</h2>
            <p>Veröffentlicht am <time datetime="2023-10-27">27. Oktober 2023</time> von Alex Mustermann</p>
        </header>

        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur vitae felis eget sapien placerat cursus. Sed eu nisl nec nisl aliquet fringilla.</p>
        <p>Integer nec odio. Praesent libero. Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at nibh elementum imperdiet.</p>
        
        <section>
            <h3>Kommentare</h3>
            <p>Hier könnten die Kommentare zum Artikel stehen.</p>
        </section>

        <footer>
            <p>Tags: <a href="/tags/html">HTML</a>, <a href="/tags/semantik">Semantik</a>, <a href="/tags/webdev">WebDev</a></p>
        </footer>
    </article>

    <article>
        <header>
            <h2>CSS-Grid: Ein Einstieg in moderne Layouts</h2>
            <p>Veröffentlicht am <time datetime="2023-10-20">20. Oktober 2023</time> von Alex Mustermann</p>
        </header>

        <p>Duis sagittis ipsum. Praesent mauris. Fusce nec tellus sed augue semper porta. Mauris massa. Vestibulum lacinia arcu eget nulla.</p>
        
        <footer>
            <p>Tags: <a href="/tags/css">CSS</a>, <a href="/tags/layout">Layout</a></p>
        </footer>
    </article>
</main>
```

Schau dir den Aufbau des ersten Artikels genau an:

*   **`<article>`:** Umschließt den gesamten Beitrag als eine logische Einheit.
*   **`<header>` innerhalb von `<article>`:** Ja, `<header>` kann mehrfach auf einer Seite vorkommen! Während das äußere `<header>`-Element den Kopf der *gesamten Seite* darstellt, markiert dieses hier den Kopf des *Artikels*. Es enthält die Überschrift (`<h2>`, da `<h1>` bereits für den Blogtitel vergeben ist) und Metainformationen.
*   **`<time>`:** Ein wunderbares semantisches Element, um ein Datum oder eine Uhrzeit anzugeben. Das `datetime`-Attribut enthält das maschinenlesbare Format, während der Inhalt für den Menschen lesbar ist.
*   **`<section>`:** Innerhalb des Artikels haben wir einen Kommentarbereich. Dieser Bereich ist thematisch klar vom Haupttext getrennt, gehört aber untrennbar zum Artikel. Dafür ist `<section>` ideal. Es gruppiert zusammengehörige Inhalte und sollte fast immer eine eigene Überschrift haben (hier `<h3>`).
*   **`<footer>` innerhalb von `<article>`:** Ähnlich wie beim `<header>` kann auch der `<footer>` für einen untergeordneten Bereich genutzt werden. Hier enthält er Informationen, die den Artikel abschließen, wie zum Beispiel die zugehörigen Tags.

#### Die Seitenleiste gestalten (`<aside>` und `<section>`)

Die Seitenleiste (`<aside>`) ist der perfekte Ort für verwandte, aber sekundäre Inhalte. Wir können sie ebenfalls mit `<section>`-Elementen unterteilen, um verschiedene Blöcke wie "Neueste Beiträge" oder "Kategorien" zu erstellen.

```html
<aside>
    <section>
        <h3>Neueste Beiträge</h3>
        <nav>
            <ul>
                <li><a href="#">Die Kunst der semantischen HTML-Struktur</a></li>
                <li><a href="#">CSS-Grid: Ein Einstieg</a></li>
                <li><a href="#">JavaScript-Events verstehen</a></li>
            </ul>
        </nav>
    </section>

    <section>
        <h3>Kategorien</h3>
        <nav>
            <ul>
                <li><a href="#">HTML & CSS</a></li>
                <li><a href="#">JavaScript</a></li>
                <li><a href="#">Tools</a></li>
            </ul>
        </nav>
    </section>
</aside>
```

Auch hier verwenden wir `<section>`, um thematische Gruppen zu bilden, jeweils mit einer eigenen Überschrift (`<h3>`). Da es sich bei den Listen um eine Form der Navigation handelt (du navigierst zu anderen Beiträgen oder Kategorieseiten), ist die Verwendung eines `<nav>`-Elements semantisch korrekt und sinnvoll.

#### Das fertige Gesamtbild

Wenn wir alle Teile zusammensetzen, erhalten wir ein robustes, semantisch reiches und logisch aufgebautes HTML-Dokument. Es ist nicht nur für den Browser, sondern auch für Suchmaschinen-Crawler und Screenreader für Menschen mit Sehbehinderung perfekt verständlich. Ein Screenreader kann nun beispielsweise ansagen: "Hauptnavigation", "Hauptinhalt mit zwei Artikeln" oder "Seitenleiste mit einem Bereich für neueste Beiträge".

Diese Art der Strukturierung ist die Grundlage jeder modernen und professionellen Webseite. Sie trennt die Bedeutung des Inhalts (HTML) von seiner Darstellung (CSS) und schafft ein solides Fundament, auf dem du komplexe und zugängliche Web-Erlebnisse aufbauen kannst.
