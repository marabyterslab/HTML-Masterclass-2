# Best Practices für HTML-Projekte

### Best Practices für HTML-Projekte: Von der Struktur bis zum Commit

Wenn du ein neues HTML-Projekt startest, ist es verlockend, einfach eine `index.html`-Datei anzulegen und loszulegen. Doch ein solides Fundament ist entscheidend, nicht nur für dich selbst, sondern auch für alle, die später mit deinem Code arbeiten – und ganz besonders für die Zusammenarbeit mit Versionskontrollsystemen wie Git. Best Practices sind keine starren Regeln, die deine Kreativität einschränken sollen. Sie sind vielmehr bewährte Methoden, die dir helfen, sauberen, wartbaren und professionellen Code zu schreiben. Betrachte sie als das Handwerkszeug eines erfahrenen Entwicklers.

#### Die Verzeichnisstruktur – Dein digitales Fundament

Noch bevor du die erste Zeile HTML schreibst, solltest du deinem Projekt eine klare Struktur geben. Eine unorganisierte Ansammlung von Dateien im Hauptverzeichnis wird schnell unübersichtlich und schwer zu verwalten. Eine bewährte und einfache Struktur für die meisten Webprojekte sieht so aus:

```
mein-projekt/
├── index.html
├── css/
│   └── style.css
├── js/
│   └── script.js
└── assets/
    ├── images/
    │   ├── logo.svg
    │   └── hero-banner.jpg
    └── fonts/
        └── meine-schrift.woff2
```

Lass uns das kurz aufschlüsseln:

*   **`index.html`**: Dies ist die Einstiegsseite deiner Website. Browser und Webserver suchen standardmäßig nach dieser Datei, wenn jemand die Haupt-URL deiner Domain aufruft.
*   **`css/`**: In diesem Ordner sammelst du alle deine Stylesheet-Dateien. Selbst wenn du anfangs nur eine `style.css` hast, hilft dir diese Struktur, den Überblick zu behalten, wenn das Projekt wächst.
*   **`js/`**: Alle deine JavaScript-Dateien gehören hier hinein. Die Trennung von Struktur (HTML), Präsentation (CSS) und Verhalten (JS) ist eines der fundamentalsten Prinzipien der Webentwicklung.
*   **`assets/`** (oder `img/`, `media/`): Dieser Ordner dient als Sammelstelle für alle Mediendateien. Eine weitere Unterteilung in `images`, `fonts`, `videos` etc. ist sehr zu empfehlen.

Warum ist das wichtig? Eine logische Ordnerstruktur macht dein Projekt sofort verständlich. Neue Teammitglieder finden sich schneller zurecht, und wenn du nach Monaten zu deinem Projekt zurückkehrst, weißt du sofort, wo du was findest. Für Git bedeutet das, dass Commits oft auf bestimmte Bereiche (z. B. nur Änderungen im `css/`-Ordner) beschränkt sind, was die Nachverfolgung von Änderungen erheblich erleichtert.

#### Sinnvolle Namenskonventionen – Sprich Klartext

Die Benennung von Dateien und Ordnern ist wie die Beschriftung von Umzugskartons. Gute Namen sparen dir stundenlanges Suchen. Halte dich an folgende einfache Regeln:

1.  **Nur Kleinbuchstaben**: Webserver unterscheiden oft zwischen Groß- und Kleinschreibung (`About.html` ist nicht dasselbe wie `about.html`). Um Fehler zu vermeiden, verwende konsequent Kleinbuchstaben.
2.  **Keine Leerzeichen oder Sonderzeichen**: Leerzeichen werden in URLs unschön kodiert (z. B. zu `%20`). Verwende stattdessen Bindestriche (`-`), auch Kebab-Case genannt.
3.  **Sei beschreibend**: `kontaktformular.html` ist unendlich viel besser als `seite2.html`. Benenne Dateien nach ihrem Inhalt oder ihrer Funktion.

Gute Beispiele:
*   `ueber-uns.html`
*   `kunden-feedback.css`
*   `navigation-mobil.js`
*   `brandenburger-tor-bei-nacht.jpg`

Diese Konvention gilt auch für deine CSS-Klassen und IDs. Eine weit verbreitete Methode ist **BEM (Block, Element, Modifier)**. Sie schafft klare, selbsterklärende Klassennamen.

```html
<!-- BEM-Beispiel für eine Produktkarte -->
<div class="card">
  <h2 class="card__title">Produktname</h2>
  <p class="card__description">Eine kurze Beschreibung.</p>
  <button class="card__button card__button--primary">Kaufen</button>
</div>
```

Hier ist `card` der Block, `card__title` ein Element innerhalb des Blocks und `card__button--primary` eine Modifikation des Button-Elements. Das sieht anfangs vielleicht etwas sperrig aus, aber in großen Projekten verhindert es zuverlässig Stilkonflikte.

#### Das HTML-Grundgerüst – Ein guter Start ist alles

Jede deiner HTML-Dateien sollte mit einer soliden und standardkonformen Grundstruktur beginnen. Diese "Boilerplate" stellt sicher, dass Browser deine Seite korrekt interpretieren.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ein aussagekräftiger Seitentitel</title>
    <meta name="description" content="Eine kurze, prägnante Beschreibung des Seiteninhalts.">
    
    <link rel="stylesheet" href="css/style.css">
</head>
<body>

    <!-- Hier kommt dein sichtbarer Inhalt hin -->

    <script src="js/script.js"></script>
</body>
</html>
```

Analysieren wir die wichtigsten Teile:

*   **`<!DOCTYPE html>`**: Dies ist keine HTML-Marke, sondern eine Anweisung für den Browser. Sie teilt ihm mit: "Achtung, hier folgt ein HTML5-Dokument." Ohne diese Zeile schalten Browser in den sogenannten "Quirks Mode", der zu unvorhersehbarem Darstellungsverhalten führen kann.
*   **`<html lang="de">`**: Das `lang`-Attribut ist entscheidend für Barrierefreiheit und Suchmaschinenoptimierung (SEO). Es teilt Screenreadern mit, in welcher Sprache der Inhalt vorgelesen werden soll, und hilft Suchmaschinen, deine Seite korrekt zu kategorisieren.
*   **`<meta charset="UTF-8">`**: Diese Zeile stellt sicher, dass der Browser die Zeichenkodierung richtig interpretiert. UTF-8 ist der universelle Standard, der alle denkbaren Zeichen, Umlaute und Emojis abdeckt. Ohne diese Angabe könnten Umlaute wie `ä`, `ö`, `ü` falsch dargestellt werden.
*   **`<meta name="viewport" ...>`**: Dies ist der Grundpfeiler des responsiven Webdesigns. Er weist mobile Browser an, die Seite nicht einfach zu verkleinern, sondern sie in der tatsächlichen Gerätebreite darzustellen.
*   **`<title>`**: Der Inhalt dieses Tags erscheint im Browser-Tab, in Lesezeichen und als Überschrift in den Suchergebnissen. Er ist extrem wichtig für Benutzerfreundlichkeit und SEO.
*   **`<script>` am Ende des `<body>`**: JavaScript-Dateien werden traditionell vor dem schließenden `</body>`-Tag platziert. Der Grund dafür ist die Performance. Der Browser parst das HTML von oben nach unten. Trifft er auf ein Skript, hält er das Rendern der Seite an, lädt das Skript herunter und führt es aus. Platzierst du es am Ende, ist die sichtbare Seite bereits geladen, bevor das Skript die Darstellung blockieren kann.

#### Semantisches HTML – Gib deinem Inhalt eine Bedeutung

In den Anfängen des Webs wurden Layouts oft mit Tabellen oder unzähligen verschachtelten `<div>`-Elementen gebaut. Modernes HTML bietet uns eine Fülle von semantischen Tags, die dem Inhalt eine Bedeutung geben. Verwende sie!

Anstatt so etwas zu schreiben:
```html
<!-- Schlecht: "Div-Suppe" -->
<div id="header">...</div>
<div id="nav">...</div>
<div class="main-content">...</div>
<div id="footer">...</div>
```

Solltest du die dafür vorgesehenen HTML5-Elemente verwenden:
```html
<!-- Gut: Semantisch korrekt -->
<header>...</header>
<nav>...</nav>
<main>
    <article>
        <h1>Titel des Artikels</h1>
        <p>Inhalt...</p>
    </article>
</main>
<footer>...</footer>
```

Warum ist das so wichtig?

1.  **Barrierefreiheit (Accessibility)**: Screenreader für sehbehinderte Menschen können eine Seite mit semantischen Tags viel besser interpretieren. Sie können direkt zur Hauptnavigation (`<nav>`) oder zum Hauptinhalt (`<main>`) springen, anstatt sich durch bedeutungslose `<div>`s kämpfen zu müssen.
2.  **SEO**: Suchmaschinen wie Google verstehen die Struktur deiner Seite besser. Ein Inhalt in einem `<header>` wird anders gewichtet als einer in einem `<footer>`.
3.  **Wartbarkeit**: Dein Code wird selbsterklärend. Du und deine Kollegen erkennen auf den ersten Blick, welcher Teil der Seite welche Funktion hat.

Einige der wichtigsten semantischen Elemente sind: `<header>`, `<footer>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>` und `<figure>`. Nutze sie, um deine Inhalte logisch zu gliedern.

#### Lesbarkeit und Kommentare – Schreibe für Menschen

Dein Code wird weitaus häufiger von Menschen gelesen als vom Computer ausgeführt. Sorge dafür, dass er lesbar ist.

*   **Einrückung**: Halte dich konsequent an eine saubere Einrückung. Jede neue Verschachtelungsebene wird um eine Stufe (meist 2 oder 4 Leerzeichen) eingerückt. Moderne Code-Editoren haben dafür automatische Formatierungsfunktionen (z. B. Prettier). Nutze sie!
*   **Kommentare**: Gute Kommentare erklären nicht, *was* der Code tut (das sollte der Code selbst tun), sondern *warum* er es tut. Ein schlechter Kommentar wäre `<!-- Ein Navigationslink -->`. Ein guter Kommentar wäre `<!-- Dropdown-Navigation für mobile Ansicht, wird per JS eingeblendet -->`.

#### Die Brücke zur Versionskontrolle mit Git

All diese Best Practices entfalten ihre volle Wirkung, wenn du sie im Kontext von Git betrachtest. Eine saubere Arbeitsweise macht deine Versionsgeschichte unendlich viel wertvoller.

*   **Klare Struktur**: Wenn du einen Fehler im Styling behebst, zeigt dein `git diff` nur Änderungen in einer Datei im `css/`-Ordner. Der Commit ist klein, fokussiert und leicht verständlich. Hättest du alles in einer riesigen Datei, wären Änderungen schwerer zu isolieren.
*   **Sinnvolle Namen**: Wenn du eine Datei von `p2.html` in `kontakt.html` umbenennst, erzeugt das in Git eine Lösch- und eine Hinzufüge-Operation. Wenn du von Anfang an `kontakt.html` verwendest, bleibt die Historie dieser Datei sauber und nachvollziehbar.
*   **Semantik und Kommentare**: Deine Commit-Nachricht beschreibt die Änderung auf einer Meta-Ebene (z. B. "Feat: Kontaktformular hinzugefügt"). Der semantische Code und die Kommentare im Code selbst erklären die Implementierungsdetails. Zusammen ergeben sie ein vollständiges Bild, das es jedem ermöglicht, deine Arbeit nachzuvollziehen.
*   **Konsistenz**: Ein konsistenter Code-Stil, der durch Tools wie einen Formatter erzwungen wird, vermeidet "Rauschen" in deinen Commits. Es gibt keine Änderungen, die nur aus der Korrektur von Einrückungen bestehen. Jeder `diff` zeigt eine echte, inhaltliche Änderung.

Indem du diese Best Practices von Beginn eines Projekts an anwendest, schreibst du nicht nur besseres HTML. Du baust ein robustes, wartbares und professionelles Projekt auf, das sich nahtlos in moderne Entwicklungsworkflows mit Tools wie Git einfügt.
