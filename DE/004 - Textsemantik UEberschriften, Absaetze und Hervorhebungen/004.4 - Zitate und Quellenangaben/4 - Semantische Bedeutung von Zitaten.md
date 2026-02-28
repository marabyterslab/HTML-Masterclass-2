# Semantische Bedeutung von Zitaten

### Mehr als nur Anführungszeichen: Die semantische Bedeutung von Zitaten

In der Welt des geschriebenen Wortes ist das Zitieren eine alltägliche und essenzielle Praxis. Wir zitieren, um Aussagen zu belegen, um einen Gedanken zu untermauern oder um die Worte eines anderen für sich selbst sprechen zu lassen. Im Web ist das nicht anders. Doch wie du Zitate in HTML auszeichnest, hat weitreichende Konsequenzen, die weit über das bloße Anzeigen von Anführungszeichen hinausgehen. Es geht um Semantik – darum, dem Browser, Suchmaschinen und assistiven Technologien die genaue *Bedeutung* deines Inhalts zu vermitteln.

Vielleicht war dein erster Impuls, einen zitierten Text einfach in Anführungszeichen zu setzen und ihn kursiv zu formatieren. Visuell mag das Ergebnis stimmen, aber semantisch hast du damit eine Chance vertan. Du hast dem Computer nicht gesagt: „Dies ist ein Zitat“, sondern nur: „Stelle diesen Text kursiv dar“. Die eigentliche Bedeutung geht verloren. HTML bietet uns jedoch präzise Werkzeuge, um Zitate und ihre Quellen korrekt und bedeutungsvoll auszuzeichnen.

#### `<blockquote>`: Für die großen, wichtigen Blöcke

Stell dir vor, du schreibst einen Artikel über die Anfänge des Internets und möchtest einen längeren, prägnanten Absatz von einem der Pioniere einfügen. Dieser Absatz steht für sich allein und bildet einen eigenen Block im Textfluss. Genau für diesen Anwendungsfall wurde das `<blockquote>`-Element geschaffen.

Es umschließt Inhalte, die als Block von einer externen Quelle zitiert werden. Browser stellen `<blockquote>`-Elemente standardmäßig mit einem linken und rechten Einzug dar. Aber hier liegt eine der häufigsten Fehlerquellen: Das `<blockquote>`-Element ist kein Werkzeug zur visuellen Einrückung von Text. Es hat eine spezifische semantische Bedeutung. Wenn du Text nur aus gestalterischen Gründen einrücken möchtest, solltest du dafür CSS verwenden, zum Beispiel mit der `margin`-Eigenschaft. Die Verwendung von `<blockquote>` für rein stilistische Zwecke ist semantisch falsch und kann beispielsweise Nutzer von Screenreadern verwirren, die eine Zitatankündigung erwarten, wo keine ist.

Ein korrektes `<blockquote>`-Beispiel sieht so aus:

```html
<p>In seiner Reflexion über die Schaffung des Webs betonte Tim Berners-Lee die Wichtigkeit der Dezentralisierung:</p>

<blockquote>
  <p>The power of a web of human knowledge is in its decentralization. The spirit of the Web is that anyone can publish anything.</p>
  <p>The web is more a social creation than a technical one. I designed it for a social effect — to help people work together — and not as a technical toy.</p>
</blockquote>

<p>Diese Vision prägt bis heute die Diskussionen über die Zukunft des Internets.</p>
```

In diesem Beispiel wird klar, dass der eingerückte Text nicht vom Autor des Artikels stammt, sondern eine direkte Übernahme aus einer anderen Quelle ist.

#### `<q>`: Das Zitat im Satz

Nicht jedes Zitat ist ein langer Block. Oftmals flechten wir kurze Zitate direkt in unsere eigenen Sätze ein. Du könntest zum Beispiel schreiben: „Der berühmte Designer sagte einmal, dass gutes Design ‚nahezu unsichtbar‘ sei.“

Für solche inline-Zitate, die Teil eines Fließtextes sind, gibt es das `<q>`-Element. Es ist das Gegenstück zum `<blockquote>` für kurze, im Satz integrierte Zitate. Der entscheidende Vorteil: Du musst die Anführungszeichen nicht selbst in den HTML-Code schreiben. Der Browser fügt sie automatisch hinzu, und zwar in der für die Dokumentsprache korrekten typografischen Form (z. B. „ “ im Deutschen oder “ ” im Englischen).

```html
<p>In diesem Moment dachte ich an das alte Sprichwort: <q>Wer den Hafen nicht kennt, in den er segeln will, für den ist kein Wind der richtige.</q> Das fasste meine Situation perfekt zusammen.</p>
```

Der Browser rendert dies als:

> In diesem Moment dachte ich an das alte Sprichwort: „Wer den Hafen nicht kennt, in den er segeln will, für den ist kein Wind der richtige.“ Das fasste meine Situation perfekt zusammen.

Durch die Verwendung von `<q>` überlässt du die korrekte Darstellung der Anführungszeichen dem Browser und stellst gleichzeitig sicher, dass die Maschine versteht: Dieser Teil des Satzes ist ein Zitat.

#### Die Quelle angeben: Der Unterschied zwischen dem `cite`-Attribut und dem `<cite>`-Element

Ein Zitat ohne Quellenangabe ist oft nur halb so viel wert. HTML bietet uns zwei verschiedene, aber miteinander verwandte Möglichkeiten, die Herkunft eines Zitats anzugeben. Hier ist es wichtig, genau zu sein, denn sie werden oft verwechselt.

**1. Das `cite`-Attribut: Die maschinenlesbare Quelle**

Sowohl `<blockquote>` als auch `<q>` können ein `cite`-Attribut enthalten. Dieses Attribut ist dazu gedacht, eine URL aufzunehmen, die direkt zur Quelle des Zitats führt. Das kann ein Link zu einem Online-Artikel, einem wissenschaftlichen Paper oder einer digitalen Buchausgabe sein.

Wichtig dabei ist: Der Inhalt des `cite`-Attributs wird für den menschlichen Besucher auf der Webseite *nicht sichtbar* dargestellt. Es ist eine Metainformation für Maschinen – für Browser, Suchmaschinen-Crawler oder andere automatisierte Werkzeuge. Es hilft ihnen, die Herkunft des Inhalts zu validieren und den Kontext deiner Seite besser zu verstehen.

```html
<blockquote cite="https://www.w3.org/History/19921103-hypertext/hypertext/WWW/TheProject.html">
  <p>The WorldWideWeb (W3) is a wide-area hypermedia information retrieval initiative aiming to give universal access to a large universe of documents.</p>
</blockquote>
```

**2. Das `<cite>`-Element: Der sichtbare Titel des Werks**

Im Gegensatz zum Attribut ist das `<cite>`-Element ein normales HTML-Tag, das du im Textfluss verwendest. Seine Aufgabe ist es, den *Titel eines Werks* zu kennzeichnen. Das kann der Titel eines Buches, eines Films, eines Songs, eines Gedichts, eines Artikels oder auch einer Webseite sein. Browser stellen den Inhalt eines `<cite>`-Elements standardmäßig kursiv dar, aber auch hier gilt: Die primäre Funktion ist semantisch, nicht stilistisch.

Ein sehr häufiger Fehler ist die Verwendung von `<cite>` für den Namen einer Person. Das ist semantisch inkorrekt. Der Name des Autors oder Sprechers ist einfach nur Text. Das `<cite>`-Element ist ausschließlich für den Titel des Werks reserviert.

```html
<p>Mein Lieblingsbuch ist <cite>Der Herr der Ringe</cite> von J.R.R. Tolkien.</p>

<p>Hast du den Film <cite>Inception</cite> gesehen?</p>
```

#### Die Königsdisziplin: Alles semantisch korrekt zusammenfügen

Wie kombinierst du nun all diese Elemente, um ein Zitat perfekt auszuzeichnen? Die modernste und semantisch reichhaltigste Methode nutzt die Elemente `<figure>` und `<figcaption>`.

Das `<figure>`-Element ist ein Container für in sich geschlossene Inhalte, die aus dem Haupttextfluss herausgelöst werden könnten, ohne dessen Sinn zu stören. Ein Bild, ein Diagramm oder eben ein prominentes Zitat sind perfekte Kandidaten dafür. Die `<figcaption>` (figure caption) liefert die dazugehörige Beschreibung oder Quellenangabe.

Indem du ein `<blockquote>` in ein `<figure>`-Element einbettest und die Quellenangabe in eine `<figcaption>` schreibst, schaffst du eine klare, logische und für Maschinen wie Menschen verständliche Einheit.

Hier ist das Goldstandard-Beispiel, das alles Gelernte vereint:

```html
<figure>
  <blockquote cite="https://www.goodreads.com/quotes/919-the-man-who-does-not-read-has-no-advantage-over">
    <p>The man who does not read has no advantage over the man who cannot read.</p>
  </blockquote>
  <figcaption>— Mark Twain, zitiert in <cite>The Motivational Speaker's Bible</cite></figcaption>
</figure>
```

Lass uns das auseinandernehmen:
*   **`<figure>`**: Gruppiert das Zitat und seine Quellenangabe zu einer logischen Einheit.
*   **`<blockquote>`**: Kennzeichnet den zitierten Text als Block.
*   **`cite`-Attribut**: Liefert die maschinenlesbare URL der Quelle.
*   **`<figcaption>`**: Stellt die für den Menschen lesbare Quellenangabe bereit.
*   **`— Mark Twain`**: Der Name des Autors wird als einfacher Text geschrieben.
*   **`<cite>`**: Umschließt den Titel des Werks, in dem das Zitat zu finden ist, und stellt ihn korrekt dar.

Diese Struktur ist robust, zugänglich und suchmaschinenfreundlich. Ein Screenreader kann diese Einheit als zusammengehörig erkennen und vorlesen. Eine Suchmaschine versteht, dass du Mark Twain aus einem bestimmten Buch zitierst und kann diese Information verknüpfen. Und für dich als Entwickler ist es eine saubere und wartbare Art, Inhalte zu strukturieren, die sich mit CSS wunderbar gestalten lässt, ohne die Semantik zu verletzen.
