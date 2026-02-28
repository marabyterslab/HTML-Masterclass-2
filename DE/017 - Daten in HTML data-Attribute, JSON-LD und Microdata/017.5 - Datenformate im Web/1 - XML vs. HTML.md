# XML vs. HTML

### XML vs. HTML: Zwei Sprachen, zwei Welten

Auf den ersten Blick sehen sich XML und HTML zum Verwechseln ähnlich. Beide verwenden spitze Klammern (`<` und `>`), um sogenannte Tags zu definieren, und beide strukturieren damit Informationen. Diese Ähnlichkeit ist kein Zufall, denn sie haben einen gemeinsamen Vorfahren: SGML (Standard Generalized Markup Language), eine Art Meta-Sprache zur Definition von Auszeichnungssprachen aus den 1980er Jahren. Doch trotz dieser familiären Bande sind HTML und XML für grundlegend unterschiedliche Aufgaben konzipiert. Sie sind keine Konkurrenten, sondern Werkzeuge mit verschiedenen Zielen. Ihre Unterschiede zu verstehen ist essenziell, um zu begreifen, wie Daten im Web strukturiert und transportiert werden.

#### Der grundlegende Unterschied: Was vs. Wie

Der Kernunterschied liegt im Zweck der jeweiligen Sprache. Stell dir die Frage: „Was soll diese Sprache erreichen?“

**HTML (HyperText Markup Language)** wurde mit einem klaren Ziel entwickelt: Inhalte für die Darstellung in einem Webbrowser zu strukturieren und zu beschreiben. Die Tags in HTML haben eine vordefinierte, semantische Bedeutung, die der Browser interpretiert, um eine Webseite visuell zu rendern. Wenn du `<h1>` schreibst, sagst du dem Browser: „Dies ist die wichtigste Überschrift auf dieser Seite.“ Der Browser weiß daraufhin, dass er diesen Text standardmäßig groß und fett darstellen soll. Wenn du `<p>` verwendest, weiß der Browser, dass es sich um einen Textabsatz handelt und fügt entsprechende Abstände ein.

HTML beantwortet also die Frage: „Wie soll dieser Inhalt aussehen und strukturiert sein?“ Es ist eine *Präsentationssprache*. Die Namen der Tags – `<body>`, `<header>`, `<img>`, `<a>` – sind fest im HTML-Standard verankert. Du kannst dir keine neuen Tags ausdenken; du musst mit dem Vokabular arbeiten, das dir die Sprache vorgibt.

**XML (eXtensible Markup Language)** hat ein völlig anderes Ziel. Der Name selbst verrät es: „eXtensible“ bedeutet „erweiterbar“. XML wurde nicht entwickelt, um Daten darzustellen, sondern um Daten zu *beschreiben* und zu *transportieren*. Bei XML gibt es keine vordefinierten Tags. Du als Entwickler erfindest die Tags selbst, um deine Daten so zu strukturieren, wie es für deine Anwendung am sinnvollsten ist.

XML beantwortet die Frage: „Was bedeuten diese Daten?“ Es ist eine *Datenbeschreibungssprache*. Der Fokus liegt einzig und allein auf der Struktur und der semantischen Bedeutung der Information, völlig losgelöst davon, wie sie später einmal aussehen mag. Eine XML-Datei ist im Grunde eine selbsterklärende, strukturierte Datensammlung.

#### Ein praktisches Beispiel: Ein Buch beschreiben

Stellen wir uns vor, wir möchten die Informationen über ein Buch strukturieren: Titel, Autor und ISBN-Nummer.

So könntest du es in **HTML** tun:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Buchinformation</title>
</head>
<body>
  <h1>Der Prozess</h1>
  <h2>von Franz Kafka</h2>
  <p>ISBN: 978-3-596-90373-1</p>
</body>
</html>
```

Hier verwendest du HTML-Tags, die für die visuelle Hierarchie einer Webseite gedacht sind. `<h1>` für den Titel, weil er am größten erscheinen soll, `<h2>` für den Autor und `<p>` für die ISBN. Ein Browser würde dies korrekt darstellen, aber die Tags beschreiben nicht die *Art* der Daten, sondern ihre *Anzeigepriorität*. Für eine Maschine ist nicht sofort ersichtlich, dass "Franz Kafka" ein Autor ist; es ist einfach nur eine Überschrift zweiter Ordnung.

Nun dieselbe Information in **XML**:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<buch>
  <titel>Der Prozess</titel>
  <autor>Franz Kafka</autor>
  <isbn>978-3-596-90373-1</isbn>
</buch>
```

Der Unterschied ist sofort ersichtlich. Die Tags `<buch>`, `<titel>`, `<autor>` und `<isbn>` habe ich frei erfunden. Sie existieren nicht als Standard, aber sie beschreiben perfekt, was die Daten zwischen ihnen bedeuten. Jede Anwendung, die diese XML-Datei liest, versteht sofort die Struktur: Es gibt ein Objekt vom Typ `buch`, das einen `titel`, einen `autor` und eine `isbn` hat. Wie diese Information später dargestellt wird – ob in einer großen Überschrift, in einer Tabellenzeile oder gar nicht –, ist für die XML-Datei selbst völlig irrelevant. Ihr einziger Job ist es, die Daten sauber zu strukturieren.

#### Freiheit vs. Strenge: Die Regeln des Spiels

Ein weiterer fundamentaler Unterschied liegt in der Syntax. HTML ist bekanntermaßen sehr fehlertolerant. Moderne Webbrowser sind darauf ausgelegt, auch mit schlecht geschriebenem HTML-Code, oft als „Tag-Suppe“ bezeichnet, bestmöglich umzugehen. Wenn du ein schließendes Tag vergisst oder Tags falsch verschachtelst, wird der Browser in den meisten Fällen versuchen, das Problem zu „erraten“ und die Seite trotzdem so gut wie möglich darzustellen. Das ist praktisch für Webdesigner, aber eine Katastrophe für den zuverlässigen Datenaustausch.

XML hingegen ist extrem streng und unnachgiebig. Eine XML-Datei muss „wohlgeformt“ (well-formed) sein, was bedeutet, dass sie sich an ein paar eiserne Regeln halten muss:

1.  **Es muss ein einziges Wurzelelement geben:** Die gesamte Struktur muss von einem einzigen, äußersten Tag umschlossen sein (im Beispiel oben war es `<buch>`).
2.  **Jedes Tag muss geschlossen werden:** Ein Tag wie `<autor>` muss immer ein entsprechendes `</autor>` haben. Leere Tags können sich selbst schließen, z. B. `<bild/>`.
3.  **Tags müssen korrekt verschachtelt sein:** Eine Struktur wie `<a_tag><b_tag>text</a_tag></b_tag>` ist verboten. Es muss immer heißen: `<a_tag><b_tag>text</b_tag></a_tag>`.
4.  **Bei Attributwerten müssen Anführungszeichen verwendet werden:** `<element id="123">` ist korrekt, `<element id=123>` ist falsch.
5.  **Groß- und Kleinschreibung wird unterschieden:** `<Titel>` und `<titel>` sind zwei verschiedene Tags.

Wenn auch nur eine dieser Regeln verletzt wird, ist die gesamte XML-Datei ungültig. Ein Programm (ein sogenannter XML-Parser), das versucht, diese Datei zu lesen, wird sofort mit einer Fehlermeldung abbrechen. Diese Strenge ist kein Nachteil, sondern ein zentrales Merkmal. Sie garantiert, dass Daten, die in XML ausgetauscht werden, immer eine eindeutige und verlässliche Struktur haben, was für die maschinelle Verarbeitung unerlässlich ist.

#### Wo du ihnen heute begegnest

**HTML** ist die unangefochtene Sprache des World Wide Web. Jede einzelne Webseite, die du in deinem Browser aufrufst, ist im Kern ein HTML-Dokument. Es bildet das Skelett, das von CSS gestaltet und von JavaScript zum Leben erweckt wird.

**XML** arbeitet heute oft im Hintergrund, ist aber keineswegs verschwunden. Du findest es in vielen Bereichen:

*   **Konfigurationsdateien:** Viele Anwendungen, insbesondere im Java-Umfeld, nutzen XML-Dateien zur Konfiguration (z. B. `pom.xml` für Maven).
*   **Vektorgrafiken:** Das SVG-Format (Scalable Vector Graphics), mit dem du verlustfrei skalierbare Grafiken für das Web erstellen kannst, ist eine XML-Anwendung.
*   **Daten-Feeds:** RSS-Feeds, mit denen du Blog-Artikel abonnieren kannst, sind in XML strukturiert.
*   **Office-Dokumente:** Moderne Formate wie `.docx` (Word) oder `.xlsx` (Excel) sind im Grunde ZIP-Archive, die eine Sammlung von XML-Dateien enthalten, welche die Inhalte, Formatierungen und Strukturen des Dokuments beschreiben.
*   **Sitemaps:** Suchmaschinen wie Google verwenden `sitemap.xml`-Dateien, um die Struktur einer Webseite besser zu verstehen und effizienter zu crawlen.

Während für viele Web-APIs (Schnittstellen zum Datenaustausch) heute das schlankere JSON-Format die Oberhand gewonnen hat, bleibt XML ein robustes und bewährtes Format für komplexe, stark strukturierte Daten, bei denen Validierung und ein festes Schema (mittels DTD oder XSD) von Bedeutung sind.

Zusammenfassend lässt sich sagen: HTML ist die Sprache für das, was Menschen sehen, und XML ist eine Sprache für das, was Maschinen verstehen. Beide sind auf ihre Weise mächtig und haben ihren festen Platz im digitalen Ökosystem. Als Webentwickler wirst du täglich mit HTML arbeiten, aber das Wissen um XML hilft dir zu verstehen, wie Daten hinter den Kulissen strukturiert, ausgetauscht und verarbeitet werden können.
