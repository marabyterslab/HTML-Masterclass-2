# Einbindung von externen Ressourcen

### Einbindung von externen Ressourcen

Eine HTML-Datei allein macht selten eine moderne Webseite aus. Stell dir dein HTML-Dokument wie das Skelett eines Körpers vor: Es gibt die grundlegende Struktur vor, aber es fehlen die Haut, die Kleidung und die Fähigkeit, sich zu bewegen. Diese zusätzlichen Elemente – das Aussehen (Design) und das Verhalten (Interaktivität) – werden typischerweise in separaten Dateien definiert: CSS für das Styling und JavaScript für die Funktionalität.

Der Grund für diese Trennung ist ein wichtiges Prinzip in der Webentwicklung, das als „Separation of Concerns“ (Trennung der Belange) bekannt ist. Dein HTML-Dokument kümmert sich ausschließlich um die semantische Struktur und den Inhalt. Eine CSS-Datei kümmert sich nur um die Präsentation. Und eine JavaScript-Datei kümmert sich nur um die Interaktivität. Diese Aufteilung macht deinen Code sauberer, leichter zu warten und wiederverwendbar.

Doch wie sagst du deinem HTML-Dokument, dass es diese externen Dateien laden und verwenden soll? Genau das geschieht im `<head>`-Bereich. Hier verknüpfst du dein strukturelles Skelett mit den Muskeln und dem Design, die es zum Leben erwecken.

#### CSS-Stylesheets verknüpfen mit `<link>`

Der häufigste Anwendungsfall für die Einbindung externer Ressourcen ist das Verknüpfen einer CSS-Datei. Ohne CSS würde deine Webseite wie ein schlichtes Textdokument aus den frühen 90er-Jahren aussehen. Um deinem HTML zu sagen, welche Stilregeln es anwenden soll, verwendest du das `<link>`-Element.

Das `<link>`-Element ist ein sogenanntes „leeres“ Element, es hat also keinen schließenden Tag. Es benötigt mindestens zwei Attribute, um sinnvoll zu sein: `rel` und `href`.

*   `rel`: Dieses Attribut beschreibt die **Relation** (Beziehung) zwischen dem aktuellen HTML-Dokument und der verknüpften Ressource. Wenn du ein Stylesheet einbinden möchtest, lautet der Wert `stylesheet`. Damit weiß der Browser: „Ah, diese Datei enthält Stilregeln, die ich auf dieses Dokument anwenden muss.“
*   `href`: Dieses Attribut steht für „Hypertext Reference“ und enthält den Pfad zur externen Datei. Das kann ein relativer Pfad (bezogen auf den Speicherort deiner HTML-Datei) oder ein absoluter Pfad (eine vollständige URL) sein.

Ein typisches Beispiel in deinem `<head>`-Bereich sieht so aus:

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Meine Webseite mit Stil</title>
  
  <!-- Hier wird die externe CSS-Datei eingebunden -->
  <link rel="stylesheet" href="css/main.css">
</head>
<body>
  <h1>Willkommen!</h1>
  <p>Dieser Text wird durch die main.css-Datei formatiert.</p>
</body>
</html>
```

In diesem Beispiel erwartet der Browser, im Unterordner `css` eine Datei namens `main.css` zu finden. Sobald er dieses `<link>`-Element beim Parsen des HTML-Dokuments entdeckt, beginnt er sofort damit, die CSS-Datei herunterzuladen und anzuwenden. Das bedeutet, dass die Webseite bereits beim ersten Rendern mit den korrekten Stilen angezeigt wird, was ein Flackern von ungestyltem Inhalt verhindert.

Früher war es üblich, auch das Attribut `type="text/css"` hinzuzufügen. In HTML5 ist dies für Stylesheets nicht mehr notwendig, da der Browser durch `rel="stylesheet"` bereits weiß, um welche Art von Datei es sich handelt.

Der größte Vorteil dieser Methode liegt auf der Hand: Du kannst eine einzige CSS-Datei für deine gesamte Webseite verwenden. Wenn du das Design ändern möchtest, musst du nur diese eine Datei bearbeiten, und die Änderungen werden auf allen Seiten wirksam, die darauf verweisen. Zudem kann der Browser die CSS-Datei zwischenspeichern (cachen). Besucht ein Nutzer eine zweite Seite deiner Webseite, muss das Stylesheet nicht erneut heruntergeladen werden, was die Ladezeit spürbar verkürzt.

#### JavaScript-Dateien einbinden mit `<script>`

Während CSS für das Aussehen zuständig ist, bringt JavaScript die Interaktivität. Ob es um das Validieren eines Formulars, das Anzeigen einer interaktiven Karte oder das Erstellen komplexer Animationen geht – JavaScript ist die Sprache des Verhaltens im Web.

Um eine externe JavaScript-Datei einzubinden, verwendest du das `<script>`-Element. Anders als `<link>` hat `<script>` einen öffnenden und einen schließenden Tag. Um eine externe Datei zu laden, verwendest du das `src`-Attribut (kurz für „Source“), das den Pfad zur JavaScript-Datei enthält.

```html
<script src="js/app.js"></script>
```

Die große Frage bei JavaScript ist jedoch: **Wo** platziert man diesen Tag? Im `<head>` oder im `<body>`? Die Antwort hat erhebliche Auswirkungen auf die Ladeleistung deiner Seite.

**Option 1: Platzierung im `<head>` (die klassische, aber problematische Methode)**

Wenn du ein `<script>`-Tag ohne weitere Attribute in den `<head>` stellst, passiert Folgendes: Der Browser parst das HTML von oben nach unten. Sobald er auf das `<script>`-Tag stößt, stoppt er das Parsen des restlichen HTML, lädt die JavaScript-Datei herunter und führt sie sofort aus. Erst danach setzt er das Parsen des HTML fort.

Dies wird als „render-blocking“ (das Rendern blockierend) bezeichnet. Wenn deine JavaScript-Datei groß ist oder die Netzwerkverbindung langsam, starrt der Nutzer auf eine weiße Seite, bis das Skript fertig geladen und ausgeführt ist. Das ist eine sehr schlechte Nutzererfahrung.

**Option 2: Die modernen Attribute `async` und `defer`**

Um das blockierende Verhalten zu umgehen, wurden zwei Attribute für das `<script>`-Element eingeführt: `async` und `defer`. Beide sorgen dafür, dass das Skript heruntergeladen wird, ohne das Parsen des HTML zu blockieren.

*   `defer`: Mit dem `defer`-Attribut wird die JavaScript-Datei parallel zum HTML-Parsing heruntergeladen. Die Ausführung des Skripts wird jedoch zurückgestellt (`to defer` = aufschieben), bis das gesamte HTML-Dokument fertig geparst wurde. Wenn du mehrere Skripte mit `defer` einbindest, wird ihre Ausführungsreihenfolge beibehalten. Dies ist die beste Wahl für Skripte, die auf das gesamte HTML-Dokument (das DOM) zugreifen und dessen Struktur manipulieren müssen.

    ```html
    <head>
      <script src="js/main-logic.js" defer></script>
      <script src="js/ui-components.js" defer></script>
    </head>
    ```

*   `async`: Auch mit `async` wird das Skript parallel heruntergeladen. Der entscheidende Unterschied ist, dass es ausgeführt wird, sobald der Download abgeschlossen ist – unabhängig davon, ob das HTML-Parsing bereits beendet ist oder nicht. Dies kann das Parsen kurz unterbrechen. Die Reihenfolge der Ausführung ist bei mehreren `async`-Skripten nicht garantiert. Es wird einfach das Skript zuerst ausgeführt, das zuerst fertig geladen ist. `async` eignet sich daher gut für unabhängige Skripte von Drittanbietern, wie zum Beispiel Analyse-Tools oder Werbebanner, deren Ausführungszeitpunkt und -reihenfolge nicht kritisch sind.

    ```html
    <head>
      <script src="httpsse://stats.example.com/analytics.js" async></script>
    </head>
    ```

**Option 3: Platzierung am Ende des `<body>` (der bewährte Workaround)**

Bevor `async` und `defer` breite Unterstützung fanden, war es die gängigste Praxis, `<script>`-Tags ganz ans Ende des `<body>`-Elements zu setzen, kurz vor dem schließenden `</body>`-Tag.

```html
<body>
  <!-- Der gesamte sichtbare Inhalt der Seite -->
  <h1>Meine interaktive Seite</h1>
  <button id="meinButton">Klick mich!</button>
  
  <script src="js/app.js"></script>
</body>
```

Der Vorteil dieser Methode ist einfach und effektiv: Der Browser parst und rendert zuerst das gesamte sichtbare HTML und CSS. Die Seite wird für den Nutzer also schnell sichtbar und nutzbar. Erst ganz am Ende stößt der Browser auf die `<script>`-Tags und beginnt, sie herunterzuladen und auszuführen. Da der Inhalt bereits da ist, wird kein Rendervorgang blockiert. Diese Methode ist auch heute noch eine absolut valide und oft genutzte Strategie.

**Welche Methode ist die beste?**
Für die meisten Anwendungsfälle ist die Verwendung von `<script defer>` im `<head>` die modernste und sauberste Lösung. Sie hält alle Metadaten und Ressourcen-Links ordentlich im Kopfbereich zusammen und stellt gleichzeitig sicher, dass das Rendern der Seite nicht blockiert wird. Die Platzierung am Ende des `<body>` ist ein ebenso robuster und einfacher Ansatz, der immer noch weit verbreitet ist.

#### Mehr als nur CSS und JavaScript: Fonts und Icons

Das `<link>`-Element ist nicht nur für Stylesheets da. Es ist ein vielseitiges Werkzeug, um verschiedenste Arten von Ressourcen mit deinem Dokument in Beziehung zu setzen.

**Web-Schriftarten (Web Fonts)**
Wenn du spezielle Schriftarten, zum Beispiel von Google Fonts, verwenden möchtest, bindest du diese ebenfalls über `<link>`-Tags im `<head>` ein. Der Service stellt dir dafür die passenden HTML-Zeilen zur Verfügung.

```html
<head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;700&display=swap" rel="stylesheet">
</head>
```

Was hier passiert, ist clever: Das letzte `<link>`-Element verweist auf eine CSS-Datei, die von Google dynamisch generiert wird. In dieser CSS-Datei stehen die `@font-face`-Regeln, die dem Browser sagen, wo er die eigentlichen Schriftdateien (.woff2) finden und wie er sie verwenden soll. Die beiden `preconnect`-Links sind Performance-Optimierungen, die dem Browser signalisieren, frühzeitig eine Verbindung zu den Font-Servern aufzubauen.

**Favicons**
Das kleine Symbol, das du im Browser-Tab neben dem Seitentitel siehst, wird als Favicon bezeichnet. Auch dieses wird über ein `<link>`-Element im `<head>` definiert. Die `rel`-Beziehung lautet hier `icon`.

```html
<head>
  <title>Meine Webseite mit Icon</title>
  <link rel="icon" type="image/png" href="/favicon.png">
</head>
```
Moderne Webseiten stellen oft mehrere Versionen des Icons für unterschiedliche Geräte und Kontexte bereit, zum Beispiel für Lesezeichen auf dem Smartphone-Homescreen (`apple-touch-icon`).

Die Fähigkeit, externe Ressourcen gezielt und performant einzubinden, ist eine Kernkompetenz der Webentwicklung. Sie ermöglicht nicht nur die grundlegende Trennung von Struktur, Design und Verhalten, sondern ist auch entscheidend für die Ladezeit und damit für die Qualität der Nutzererfahrung. Indem du diese Verknüpfungen im `<head>` deines Dokuments definierst, legst du das Fundament für eine moderne, wartbare und schnelle Webseite.
