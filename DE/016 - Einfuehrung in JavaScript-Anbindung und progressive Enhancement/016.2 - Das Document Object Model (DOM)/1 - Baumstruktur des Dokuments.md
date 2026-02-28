# Baumstruktur des Dokuments

### Die Baumstruktur des Dokuments

Wenn du eine HTML-Datei in deinem Editor schreibst, siehst du eine Textdatei. Sie hat eine klare Struktur, die du durch Einrückungen und die Verschachtelung von Tags erzeugst. Für den Browser ist diese Datei jedoch mehr als nur Text. Sobald er sie lädt, passiert etwas Magisches: Er übersetzt deinen Code in ein lebendiges, interaktives Modell, das er in seinem Speicher ablegt. Dieses Modell ist das **Document Object Model**, kurz **DOM**, und seine grundlegende Form ist die einer Baumstruktur.

Stell dir einen Stammbaum vor. Es gibt Großeltern, Eltern, Kinder und Geschwister. Jeder hat seinen festen Platz und eine klare Beziehung zu den anderen. Genau so organisiert der Browser dein HTML-Dokument. Jedes einzelne Element, jedes Stück Text, ja sogar jeder Kommentar in deinem Code wird zu einem Teil dieses Baumes.

#### Alles ist ein Knoten

Der grundlegende Baustein in dieser Baumstruktur ist der **Knoten** (englisch: *Node*). In der Welt des DOM ist fast alles ein Knoten. Diese universelle Bezeichnung erlaubt es, mit den verschiedensten Teilen deines Dokuments auf eine einheitliche Weise zu interagieren. Obwohl es über ein Dutzend verschiedene Knotentypen gibt, wirst du in der Praxis hauptsächlich mit den folgenden vier zu tun haben:

1.  **Das Dokument selbst (Document Node):** An der absoluten Spitze des Baumes steht der Dokumentenknoten. Er ist die Wurzel von allem, der Urahn, von dem alles andere abstammt. In JavaScript greifst du auf ihn über das globale `document`-Objekt zu. Er repräsentiert die gesamte Seite.

2.  **Elementknoten (Element Node):** Dies sind die Knoten, die du am besten kennst. Jedes HTML-Tag in deinem Code – sei es `<html>`, `<head>`, `<body>`, `<h1>`, `<p>`, `<div>` oder `<a>` – wird zu einem Elementknoten im DOM-Baum. Diese Knoten sind die Hauptakteure, denn sie formen die sichtbare und unsichtbare Struktur deiner Seite.

3.  **Textknoten (Text Node):** Der eigentliche Inhalt deiner Seite, der Text, den deine Nutzer lesen, wird ebenfalls zu einem eigenen Knoten. Der Text "Willkommen auf meiner Seite!" innerhalb eines `<h1>`-Tags ist nicht Teil des Elementknotens `<h1>`, sondern ein eigenständiger Textknoten, der ein Kind dieses `<h1>`-Knotens ist. Das ist eine wichtige Unterscheidung, die später bei der Manipulation von Inhalten entscheidend wird.

4.  **Attributknoten (Attribute Node):** Attribute wie `href` in einem `<a>`-Tag oder `class` in einem `<div>`-Tag werden zu Attributknoten. Sie sind nicht direkt Kinder des Elements im herkömmlichen Sinne, sondern gehören untrennbar zu einem Elementknoten und beschreiben dessen Eigenschaften.

#### Die Beziehungen im Baum

Die wahre Stärke der Baumstruktur liegt in den fest definierten Beziehungen zwischen den Knoten. Diese Beziehungen ermöglichen es uns, präzise durch das Dokument zu navigieren, Elemente zu finden und zu verändern. Die Terminologie ist dabei direkt aus dem Bild des Stammbaums entlehnt:

*   **Elternteil (Parent):** Jeder Knoten (außer der Wurzel) hat genau einen Elternteil. Der Elternteil ist der Knoten, in dem der aktuelle Knoten direkt verschachtelt ist. Zum Beispiel ist der `<body>`-Knoten der Elternteil eines `<h1>`-Knotens, der direkt in ihm liegt.

*   **Kinder (Children):** Ein Knoten kann beliebig viele Kinder haben. Dies sind die Knoten, die direkt in ihm verschachtelt sind. Ein `<ul>`-Elementknoten hat zum Beispiel mehrere `<li>`-Elementknoten als Kinder.

*   **Geschwister (Siblings):** Knoten, die denselben Elternteil haben, werden als Geschwister bezeichnet. Ein `<h1>`- und ein direkt folgender `<p>`-Knoten innerhalb des `<body>` sind Geschwister.

*   **Vorfahren (Ancestors):** Das sind alle Knoten auf dem Pfad vom aktuellen Knoten zurück zur Wurzel – also der Elternteil, der Großelternteil und so weiter.

*   **Nachkommen (Descendants):** Dies sind alle Knoten, die innerhalb eines Knotens verschachtelt sind – also seine Kinder, deren Kinder (Enkelkinder) und so weiter, bis hin zu den letzten Blättern des Baumes.

#### Ein praktisches Beispiel

Um diese abstrakten Konzepte greifbar zu machen, schauen wir uns ein einfaches HTML-Dokument an und zeichnen seinen DOM-Baum nach.

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Der DOM-Baum</title>
</head>
<body>
  <h1>Ein wichtiger Titel</h1>
  <p>Dies ist ein Absatz mit <strong>wichtigem</strong> Text.</p>
  <!-- Hier folgt noch mehr Inhalt -->
</body>
</html>
```

Wenn der Browser diesen Code verarbeitet, erstellt er intern die folgende Struktur:

1.  Ganz oben steht der `document`-Knoten.
2.  Sein einziges Kind ist der `<html>`-Elementknoten.
3.  Der `<html>`-Knoten hat zwei Kinder: den `<head>`- und den `<body>`-Elementknoten. Sie sind Geschwister.
4.  Der `<head>`-Knoten hat zwei Kinder: `<meta>` und `<title>`.
5.  Der `<title>`-Knoten hat seinerseits ein Kind: einen Textknoten mit dem Inhalt "Der DOM-Baum".
6.  Der `<body>`-Knoten hat drei Kinder: den `<h1>`-Elementknoten, den `<p>`-Elementknoten und einen Kommentarknoten (`<!-- ... -->`).
7.  Der `<h1>`-Knoten hat ein Kind: einen Textknoten mit dem Inhalt "Ein wichtiger Titel".
8.  Der `<p>`-Knoten ist besonders interessant. Er hat drei Kinder:
    *   Einen Textknoten mit dem Inhalt "Dies ist ein Absatz mit ".
    *   Einen `<strong>`-Elementknoten.
    *   Einen Textknoten mit dem Inhalt " Text.".
9.  Der `<strong>`-Knoten hat wiederum ein eigenes Kind: einen Textknoten mit dem Inhalt "wichtigem".

Du siehst, wie präzise und detailliert dieser Baum ist. Selbst der Text innerhalb des `<p>`-Tags wird durch das `<strong>`-Tag aufgeteilt in separate Textknoten. Diese Granularität ist kein Zufall. Sie ist die Grundlage dafür, dass wir später mit JavaScript jedes noch so kleine Detail unserer Webseite ansprechen und verändern können.

#### Warum diese Struktur so entscheidend ist

Das Verständnis der DOM-Baumstruktur ist nicht nur eine theoretische Übung. Es ist das Fundament für jede dynamische Interaktion auf einer Webseite. Wenn du mit JavaScript ein Element auswählst, um seine Farbe zu ändern, navigierst du durch diesen Baum. Wenn du auf einen Button klickst und ein neues Element auf der Seite erscheint, fügst du dem Baum einen neuen Knoten hinzu. Wenn du eine Fehlermeldung entfernst, löschst du einen Knoten aus dem Baum.

Das DOM ist also die Brücke zwischen deinem statischen HTML-Code und der dynamischen, interaktiven Welt von JavaScript. Es ist die lebendige Repräsentation deiner Seite im Browser, eine strukturierte Karte, die es dir erlaubt, jeden Ort zu finden, zu untersuchen und nach Belieben umzugestalten. Indem du lernst, in dieser Baumstruktur zu denken, legst du den Grundstein, um aus einfachen Dokumenten fesselnde Webanwendungen zu erschaffen.
