# Semantische Strukturierung

### Semantische Strukturierung: Mehr als nur Aussehen

Stell dir vor, du baust ein Haus. Du könntest einfach einen riesigen, leeren Raum errichten und dann Möbel hineinstellen, um Bereiche wie „Küche“ oder „Schlafzimmer“ anzudeuten. Es würde vielleicht funktionieren, aber es wäre chaotisch. Ein Architekt würde das nie so machen. Er plant Wände, Türen und Stockwerke, um dem Haus eine klare, logische Struktur zu geben. Jeder weiß sofort, was der Zweck eines Raumes ist, noch bevor ein einziges Möbelstück darin steht.

Genau dieses Prinzip wenden wir mit semantischer Strukturierung auf unsere HTML-Dokumente an. Früher, in den wilden Anfangstagen des Webs, ging es oft nur darum, wie eine Webseite aussah. Entwickler nutzten Tabellen für das Layout und wählten Überschriften-Tags (`<h1>`, `<h2>` usw.) danach aus, welche Schriftgröße sie erzeugten. Das Ergebnis war ein visuelles, aber strukturelles Chaos – wie das Haus ohne Wände.

Heute wissen wir es besser. Die goldene Regel lautet: HTML ist für die Bedeutung (Semantik), CSS ist für das Aussehen (Präsentation). Dein HTML-Code sollte die Struktur und den Sinn deines Inhalts beschreiben, völlig unabhängig davon, wie er später dargestellt wird. Du sagst dem Browser nicht „Mach diesen Text groß und fett“, sondern „Dieser Text ist die wichtigste Überschrift der Seite“. Wie groß und fett er dann wird, entscheidest du später in deinem CSS.

Warum ist dieser Mehraufwand so entscheidend? Aus mehreren, sehr wichtigen Gründen:

1.  **Suchmaschinen (SEO):** Suchmaschinen wie Google oder DuckDuckGo sind die wichtigsten Besucher deiner Webseite. Sie haben aber keine Augen. Sie lesen deinen Code, um zu verstehen, worum es auf deiner Seite geht. Wenn sie ein `<h1>`-Tag finden, wissen sie: „Aha, das ist das Hauptthema dieses Dokuments.“ Ein `<h2>` signalisiert ein wichtiges Unterthema. Eine gut strukturierte Seite ist für eine Suchmaschine wie ein gut geschriebenes Inhaltsverzeichnis. Sie kann den Inhalt besser verstehen, indexieren und Suchenden als relevantes Ergebnis präsentieren. Semantisch sauberes HTML ist die Grundlage für jede gute Suchmaschinenoptimierung.

2.  **Barrierefreiheit (Accessibility):** Stell dir vor, du könntest nicht sehen und wärst auf einen Screenreader angewiesen – eine Software, die dir Webseiten vorliest. Auf einer schlecht strukturierten Seite, auf der Überschriften nur fett formatierter Text sind, hört der Nutzer einen endlosen Monolog aus Text. Es ist unmöglich, schnell zu einem bestimmten Abschnitt zu springen. Auf einer semantisch korrekten Seite hingegen kann der Nutzer den Screenreader anweisen: „Lies mir alle Überschriften der zweiten Ebene vor.“ Er kann dann wie in einem Inhaltsverzeichnis von `<h2>` zu `<h2>` springen, um schnell den für ihn relevanten Abschnitt zu finden. Semantik ist kein „Nice-to-have“, sondern eine fundamentale Voraussetzung, um das Web für alle Menschen zugänglich zu machen.

3.  **Wartbarkeit und Teamarbeit:** Dein Code wird öfter gelesen als geschrieben – von dir in der Zukunft oder von deinen Kollegen. Semantischer Code ist quasi selbsterklärend. Wenn du in deinem Code ein `<nav>`-Element siehst, weißt du sofort, dass hier die Navigation untergebracht ist. Ein `<main>`-Element umschließt den Hauptinhalt der Seite. Das ist unendlich viel klarer als nichtssagende `<div>`-Container mit kryptischen IDs wie `<div id="main_content_wrapper">`.

#### Die Hierarchie der Überschriften

Das Herzstück der semantischen Textstrukturierung ist die korrekte Verwendung von Überschriften-Tags, von `<h1>` bis `<h6>`. Diese Tags sind nicht dazu da, sechs verschiedene Schriftgrößen zur Auswahl zu haben. Sie repräsentieren eine strenge, logische Hierarchie, ganz wie in einem Buch oder einem wissenschaftlichen Aufsatz.

**Die `<h1>`-Überschrift: Der Titel der Seite**

Jedes HTML-Dokument sollte genau eine `<h1>`-Überschrift haben. Sie ist der Titel deiner Seite, die wichtigste Aussage. Sie beschreibt das Gesamtthema des Dokuments. Stell sie dir wie den Titel auf dem Buchcover vor. Es gibt nur einen.

**`<h2>` bis `<h6>`: Kapitel und Unterkapitel**

Alle weiteren Überschriften gliedern den Inhalt unterhalb der `<h1>`. Dabei musst du die Hierarchie strikt einhalten. Du darfst keine Ebenen überspringen.

*   Auf eine `<h1>` folgt eine `<h2>`.
*   Auf eine `<h2>` kann entweder eine weitere `<h2>` (ein neues „Kapitel“) oder eine `<h3>` (ein „Unterkapitel“) folgen.
*   Du würdest niemals direkt von einer `<h2>` zu einer `<h4>` springen. Das wäre so, als ob du in einem Buch von Kapitel 2 direkt zu Abschnitt 2.1.1 springst, ohne dass es einen Abschnitt 2.1 gibt.

Lass uns das an einem konkreten Beispiel für einen Blogartikel über die Zubereitung von Kaffee verdeutlichen.

**Ein gutes, semantisch korrektes Beispiel:**

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Der perfekte Kaffee</title>
</head>
<body>

    <h1>Die Kunst der perfekten Kaffeezubereitung</h1>
    <p>Kaffee ist mehr als nur ein Getränk. In diesem Artikel erkunden wir verschiedene Methoden, um das Beste aus jeder Bohne herauszuholen.</p>

    <h2>Die Wahl der richtigen Bohne</h2>
    <p>Alles beginnt mit der Qualität der Kaffeebohnen. Arabica und Robusta sind die bekanntesten Sorten.</p>
    
    <h3>Arabica: Das feine Aroma</h3>
    <p>Arabica-Bohnen sind für ihre komplexen Aromen und ihre angenehme Säure bekannt.</p>

    <h3>Robusta: Der kräftige Wachmacher</h3>
    <p>Robusta enthält mehr Koffein und hat einen kräftigeren, oft erdigeren Geschmack.</p>

    <h2>Die Zubereitungsmethoden</h2>
    <p>Es gibt unzählige Wege, Kaffee zuzubereiten. Hier sind drei beliebte Methoden.</p>

    <h3>Die French Press</h3>
    <p>Bei dieser Methode wird das Kaffeepulver direkt im Wasser aufgebrüht und dann durch ein Metallsieb nach unten gedrückt.</p>

    <h3>Der Handfilter (Pour-Over)</h3>
    <p>Eine klassische Methode, die viel Kontrolle über den Brühvorgang erlaubt und einen sehr klaren Kaffee erzeugt.</p>

    <h3>Die Espressomaschine</h3>
    <p>Für einen konzentrierten, intensiven Kaffee unter hohem Druck. Die Basis für viele Kaffeespezialitäten.</p>

    <h2>Fazit: Übung macht den Meister</h2>
    <p>Egal welche Methode du wählst, das Wichtigste ist die Freude am Experimentieren.</p>

</body>
</html>
```

Diese Struktur ist logisch und für Mensch und Maschine sofort verständlich. Die `<h1>` gibt das Hauptthema vor. Die `<h2>`-Tags teilen den Artikel in große Abschnitte („Bohnenwahl“, „Zubereitungsmethoden“, „Fazit“). Die `<h3>`-Tags unterteilen den Abschnitt „Bohnenwahl“ und „Zubereitungsmethoden“ weiter in spezifische Unterpunkte. Ein Screenreader-Nutzer könnte direkt zu „Die Zubereitungsmethoden“ springen und sich dann die einzelnen Methoden (`<h3>`) vorlesen lassen.

**Ein schlechtes, rein visuell gedachtes Beispiel:**

Hier ist ein Beispiel, wie man es **nicht** machen sollte. Der Autor hat die Überschriften-Tags gewählt, weil ihm die Standard-Schriftgröße gefiel, nicht wegen ihrer hierarchischen Bedeutung.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Der perfekte Kaffee</title>
</head>
<body>

    <h1>Die Kunst der perfekten Kaffeezubereitung</h1>
    <p>Kaffee ist mehr als nur ein Getränk...</p>

    <h2>Die Wahl der richtigen Bohne</h2>
    <p>Alles beginnt mit der Qualität...</p>
    
    <h4>Arabica: Das feine Aroma</h4> <!-- FALSCH: Ebene <h3> übersprungen -->
    <p>Arabica-Bohnen sind für ihre komplexen Aromen bekannt.</p>

    <h4>Robusta: Der kräftige Wachmacher</h4> <!-- FALSCH: Ebene <h3> übersprungen -->
    <p>Robusta enthält mehr Koffein...</p>

    <h2>Die Zubereitungsmethoden</h2>
    <p>Es gibt unzählige Wege...</p>

    <h3>Die French Press</h3>
    <p>Bei dieser Methode wird das Kaffeepulver...</p>

    <h6>Der Handfilter (Pour-Over)</h6> <!-- FALSCH: Hier müsste eine <h3> stehen, nicht <h6>, nur weil es "weniger wichtig" aussieht -->
    <p>Eine klassische Methode...</p>

    <h2>Fazit: Übung macht den Meister</h2> <!-- FALSCH: Dies ist kein neues Hauptkapitel. Es sollte eher eine <h3> oder eine eigene Sektion sein, aber die Logik ist hier gebrochen. -->
    <p>Egal welche Methode du wählst...</p>

</body>
</html>
```

Dieser zweite Code mag im Browser auf den ersten Blick vielleicht ähnlich aussehen, aber seine innere Struktur ist kaputt. Für eine Suchmaschine ist die Hierarchie unklar. Für einen Screenreader-Nutzer ist die Navigation verwirrend und unlogisch. Der Sprung von `<h2>` zu `<h4>` bricht die Gliederung. Die willkürliche Nutzung von `<h6>` für den Handfilter macht überhaupt keinen Sinn.

Denke also immer daran: Die Struktur deines Dokuments wird allein durch HTML definiert. Das Aussehen kommt später mit CSS. Wenn du eine Überschrift der dritten Ebene (`<h3>`) kleiner darstellen möchtest als eine Überschrift der vierten Ebene (`<h4>`), dann ist das vollkommen in Ordnung – aber du erreichst das mit CSS. Die HTML-Struktur bleibt logisch und korrekt.

Semantische Strukturierung ist eine Denkweise. Es geht darum, deinem Inhalt eine klare Bedeutung zu geben und die Werkzeuge, die HTML dir bietet, für ihren vorgesehenen Zweck zu verwenden. Eine saubere Überschriften-Hierarchie ist der erste und wichtigste Schritt auf dem Weg zu professionellem, zugänglichem und zukunftssicherem HTML-Code.
