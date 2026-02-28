# Funktion und Inhalt des head

### Funktion und Inhalt des head

Stell dir eine HTML-Seite wie eine Theaterbühne vor. Der `<body>`-Bereich ist die eigentliche Bühne, auf der die Schauspieler (deine Inhalte wie Texte, Bilder und Videos) für das Publikum sichtbar agieren. Der `<head>`-Bereich hingegen ist der Backstage-Bereich. Das Publikum sieht ihn nie direkt, aber hier geschieht all die Magie, die die Vorstellung erst möglich macht: Hier liegen die Skripte, die Anweisungen für die Beleuchtung, die Requisitenlisten und die Informationen für das Programmheft.

Der `<head>` ist also der unsichtbare, aber unverzichtbare Kontrollraum deines HTML-Dokuments. Er enthält Metadaten – also Daten über die Daten –, die dem Browser, den Suchmaschinen und anderen Web-Diensten wichtige Anweisungen und Informationen über deine Seite geben. Nichts, was du in den `<head>` schreibst, wird direkt auf der Webseite dargestellt, mit einer wichtigen Ausnahme, die wir gleich kennenlernen werden.

Werfen wir einen genauen Blick auf die wichtigsten Elemente, die du im `<head>`-Bereich findest.

#### Das `<title>`-Element: Der Name deiner Seite

Das `<title>`-Element ist das einzige Kind des `<head>`, dessen Inhalt für den Benutzer direkt sichtbar wird, wenn auch nicht auf der Seite selbst. Der Text, den du hier platzierst, erscheint an drei prominenten Stellen:

1.  **Im Tab des Browsers:** Es ist der Titel, der oben im Browser-Tab oder -Fenster angezeigt wird und dem Nutzer hilft, deine Seite unter vielen offenen Tabs wiederzufinden.
2.  **In den Lesezeichen:** Wenn ein Nutzer deine Seite als Lesezeichen speichert, wird der Inhalt des `<title>`-Tags als Standardname für dieses Lesezeichen verwendet.
3.  **In den Suchergebnissen:** Für Suchmaschinen wie Google ist der Titel einer der wichtigsten Faktoren. Er wird als klickbare Überschrift in der Ergebnisliste angezeigt.

Ein guter Titel ist kurz, prägnant und beschreibt den Inhalt der Seite treffend. Jede einzelne Seite deiner Website sollte einen einzigartigen Titel haben.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Über Uns - Die Geschichte unseres Unternehmens</title>
  </head>
  <body>
    <!-- Seiteninhalt kommt hier hin -->
  </body>
</html>
```

Ein fehlender oder leerer `<title>` ist nicht nur schlecht für die Benutzerfreundlichkeit und die Suchmaschinenoptimierung (SEO), sondern macht dein HTML auch formal ungültig.

#### Das `<meta>`-Element: Der Alleskönner für Metadaten

Das `<meta>`-Element ist ein wahres Chamäleon. Es dient dazu, Metadaten zu definieren, für die es kein eigenes, spezifisches HTML-Element gibt. Es ist ein leeres Element, das heißt, es hat kein schließendes Tag, und seine Informationen werden über Attribute übermittelt. Die wichtigsten Anwendungsfälle schauen wir uns jetzt an.

##### Zeichenkodierung: `<meta charset="UTF-8">`

Dies ist wahrscheinlich die wichtigste Zeile in deinem gesamten `<head>`. Sie teilt dem Browser mit, welchen Zeichensatz er zur Darstellung der Seite verwenden soll. Stell es dir wie ein Alphabet vor. Wenn du dem Browser nicht sagst, welches Alphabet er nutzen soll, kann er Buchstaben, Sonderzeichen und Emojis falsch interpretieren. Das Ergebnis sind unschöne Hieroglyphen wie "f�r" anstelle von "für".

`UTF-8` ist der universelle Standard für das Web, da er praktisch alle Zeichen und Symbole aller Sprachen der Welt abdeckt. Diese Angabe sollte immer als allererstes Element innerhalb des `<head>` stehen, damit der Browser von Anfang an weiß, wie er die Zeichen interpretieren muss.

```html
<head>
  <meta charset="UTF-8">
  <title>Meine Webseite</title>
</head>
```

##### Der Viewport für mobile Geräte

In den Anfängen des mobilen Internets versuchten Smartphone-Browser, komplette Desktop-Webseiten auf ihren winzigen Bildschirmen darzustellen. Das Ergebnis war eine winzige, unlesbare Miniaturansicht, in die man mühsam hineinzoomen musste. Das `viewport`-Meta-Tag löst dieses Problem.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Diese Zeile ist heute für jede Webseite unerlässlich. Sie gibt dem Browser zwei Anweisungen:

*   `width=device-width`: Setze die Breite des Anzeigebereichs (des Viewports) auf die tatsächliche Breite des Geräts. Ein iPhone wird also nicht mehr so tun, als wäre es ein 980 Pixel breiter Desktop-Monitor.
*   `initial-scale=1.0`: Stelle die Seite beim ersten Laden ohne Zoom dar, also in einem 1:1-Verhältnis.

Ohne dieses Meta-Tag wird deine Webseite auf mobilen Geräten nicht korrekt dargestellt, selbst wenn du mit CSS responsive Designtechniken anwendest.

##### Beschreibung und Schlüsselwörter für Suchmaschinen

Obwohl ihre Bedeutung für das Ranking bei Google stark nachgelassen hat, sind diese Meta-Tags immer noch nützlich:

*   **`description`**: Der Text, den du hier angibst, wird von Suchmaschinen oft als Beschreibungstext unter dem Titel in den Suchergebnissen angezeigt. Eine gute Beschreibung ist eine kurze, verlockende Zusammenfassung des Seiteninhalts, die Nutzer zum Klicken anregt.

    ```html
    <meta name="description" content="Erfahre alles über die Geschichte unseres Unternehmens, von der Gründung in einer Garage bis zum heutigen Erfolg.">
    ```

*   **`keywords`**: Früher war dieses Tag entscheidend für SEO. Webmaster listeten hier die wichtigsten Schlüsselwörter auf, unter denen sie gefunden werden wollten. Heute ignorieren große Suchmaschinen wie Google dieses Tag weitgehend, da es zu oft für Spam missbraucht wurde. Es schadet nicht, es hinzuzufügen, aber erwarte keine Wunder davon.

    ```html
    <meta name="keywords" content="Unternehmensgeschichte, Firmengründung, Über Uns">
    ```

Es gibt noch viele weitere `meta`-Angaben, zum Beispiel für den Autor (`<meta name="author" content="Max Mustermann">`) oder zur Steuerung des Caching-Verhaltens von Browsern.

#### Das `<link>`-Element: Die Verbindung zur Außenwelt

Mit dem `<link>`-Element stellst du eine Beziehung zwischen deinem HTML-Dokument und einer externen Ressource her. Der häufigste und wichtigste Anwendungsfall ist das Einbinden von externen CSS-Dateien, die das Aussehen und Design deiner Seite definieren.

```html
<head>
  <link rel="stylesheet" href="css/style.css">
</head>
```

Schauen wir uns die Attribute genauer an:

*   `rel="stylesheet"`: Das `rel`-Attribut (von engl. *relationship*) beschreibt die Beziehung zwischen dem aktuellen Dokument und der verlinkten Ressource. In diesem Fall sagen wir: "Dieses verlinkte Dokument ist ein Stylesheet."
*   `href="css/style.css"`: Das `href`-Attribut (*hypertext reference*) enthält den Pfad zur Datei, die geladen werden soll.

Ein weiterer sehr verbreiteter Einsatz des `<link>`-Tags ist das Einbinden eines Favicons – des kleinen Symbols, das im Browser-Tab neben dem Titel angezeigt wird.

```html
<link rel="icon" href="favicon.ico" type="image/x-icon">
<link rel="apple-touch-icon" href="apple-icon.png"> <!-- Für Apple-Geräte -->
```

#### Das `<script>`-Element: Interaktivität und Logik

Während HTML die Struktur und CSS das Aussehen bestimmt, bringt JavaScript die Interaktivität auf deine Seite. Mit dem `<script>`-Element kannst du JavaScript-Code entweder direkt in dein HTML-Dokument einbetten oder – was die deutlich bessere Praxis ist – eine externe JavaScript-Datei laden.

**Externe Skripte (bevorzugt):**
Das ist der saubere und empfohlene Weg. Du hältst deine Logik getrennt von deiner Struktur, und der Browser kann die `.js`-Datei zwischenspeichern, was die Ladezeiten bei wiederholten Besuchen verbessert.

```html
<script src="js/main.js" defer></script>
```

Das `src`-Attribut gibt den Pfad zur JavaScript-Datei an. Das Attribut `defer` ist eine moderne und sehr nützliche Ergänzung. Es weist den Browser an, das HTML-Dokument erst vollständig zu parsen und darzustellen, bevor er das Skript ausführt. Das verhindert, dass ein großes JavaScript das Laden deiner Seite blockiert und der Nutzer auf einen weißen Bildschirm starrt.

**Interne Skripte:**
Für sehr kleine, seitenspezifische Skripte kannst du den Code auch direkt in den `<head>` schreiben. Dies wird jedoch schnell unübersichtlich.

```html
<script>
  console.log("Diese Nachricht erscheint in der Entwicklerkonsole des Browsers.");
</script>
```

Obwohl du `<script>`-Tags auch im `<body>` platzieren kannst (oft direkt vor dem schließenden `</body>`-Tag), ist der `<head>` in Kombination mit dem `defer`-Attribut eine gängige und performante Methode.

#### Das `<style>`-Element: Internes CSS

Ähnlich wie bei JavaScript kannst du auch CSS-Regeln direkt in dein HTML-Dokument schreiben, anstatt sie aus einer externen Datei zu laden. Dazu dient das `<style>`-Element.

```html
<head>
  <style>
    body {
      font-family: sans-serif;
      background-color: #f0f0f0;
    }
    h1 {
      color: #333;
    }
  </style>
</head>
```

Dies kann nützlich sein, um sehr spezifische Stile anzuwenden, die nur auf dieser einen Seite gelten und nirgendwo anders wiederverwendet werden. In 99 % der Fälle ist es jedoch besser, CSS in einer separaten `.css`-Datei zu organisieren und diese mit dem `<link>`-Element einzubinden. Das macht deinen Code wartbarer und ermöglicht Caching.

#### Das `<base>`-Element: Der Ausgangspunkt für alle Pfade

Das `<base>`-Element ist ein seltener genutztes, aber mächtiges Werkzeug. Es erlaubt dir, eine Basis-URL für alle relativen Pfade im Dokument festzulegen. Wenn du beispielsweise viele Bilder aus einem bestimmten Ordner lädst, kannst du den Pfad zu diesem Ordner als Basis definieren.

```html
<head>
  <base href="https://www.meine-domain.de/bilder/">
</head>
<body>
  <!-- Dieses Bild wird von https://www.meine-domain.de/bilder/logo.png geladen -->
  <img src="logo.png" alt="Firmenlogo">

  <!-- Dieser Link führt zu https://www.meine-domain.de/produkte/ -->
  <a href="../produkte/">Unsere Produkte</a>
</body>
```

Achtung: Du darfst nur ein einziges `<base>`-Element pro Dokument verwenden, und es muss vor allen Elementen stehen, die eine URL enthalten (wie `<img>`, `<a>` oder `<link>`).

Der `<head>` ist also weit mehr als nur ein Container. Er ist die Kommandozentrale, die deinem Dokument eine Identität gibt, es mit der Außenwelt verbindet und dem Browser sagt, wie er sich verhalten soll. Ein gut strukturierter und durchdachter `<head>`-Bereich ist die Grundlage für eine funktionale, benutzerfreundliche und suchmaschinenoptimierte Webseite.
