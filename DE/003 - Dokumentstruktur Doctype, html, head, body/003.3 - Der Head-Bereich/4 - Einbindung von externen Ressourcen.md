# Einbindung von externen Ressourcen

### Einbindung von externen Ressourcen

Eine HTML-Datei ist selten eine einsame Insel. Sie ist vielmehr das Fundament eines Hauses, das erst durch Strom, Wasser und Einrichtung wirklich bewohnbar wird. In der Welt des Webs sind diese "Versorgungsleitungen" und "Einrichtungsgegenstände" externe Ressourcen wie Stylesheets, Skripte, Schriftarten oder Icons. Der `<head>`-Bereich deines HTML-Dokuments ist die zentrale Schaltstelle, in der du dem Browser mitteilst, welche externen Dateien er laden und wie er sie verwenden soll.

#### CSS-Stylesheets: Das Design deiner Webseite

Die wohl häufigste externe Ressource, die du einbinden wirst, ist eine CSS-Datei (Cascading Style Sheet). Sie enthält alle Regeln, die das Aussehen deines HTML-Dokuments bestimmen – von Farben und Schriftgrößen bis hin zu komplexen Layouts. Die Trennung von Struktur (HTML) und Präsentation (CSS) ist ein Grundpfeiler moderner Webentwicklung. Sie macht deinen Code sauberer, wartbarer und ermöglicht es dir, das Design einer ganzen Website durch die Änderung einer einzigen Datei anzupassen.

Die Einbindung erfolgt über das `<link>`-Element. Dieses Element ist leer, das heißt, es hat keinen schließenden Tag. Für ein Stylesheet benötigst du zwei wesentliche Attribute: `rel` und `href`.

*   `rel` (relationship): Dieses Attribut beschreibt die Beziehung zwischen dem aktuellen Dokument und der verlinkten Ressource. Für ein Stylesheet lautet der Wert immer `stylesheet`.
*   `href` (hypertext reference): Hier gibst du den Pfad zur CSS-Datei an. Dieser Pfad kann relativ (im selben Projektordner) oder absolut (eine vollständige URL) sein.

Ein klassisches Beispiel sieht so aus:

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Meine Webseite</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <h1>Hallo Welt!</h1>
</body>
</html>
```

In diesem Fall erwartet der Browser, im Unterordner `css` eine Datei namens `style.css` zu finden. Der Browser liest diesen Link, lädt die CSS-Datei und wendet die darin definierten Stile auf die HTML-Elemente an. Früher war auch das `type`-Attribut (`type="text/css"`) üblich, aber bei `rel="stylesheet"` ist dies der Standard und wird von modernen Browsern nicht mehr benötigt. Du kannst es der Vollständigkeit halber hinzufügen, es ist aber optional.

#### JavaScript-Dateien: Die Interaktivität deiner Seite

Während CSS für das Aussehen zuständig ist, bringt JavaScript Leben und Interaktivität auf deine Seite. Ob es sich um aufklappende Menüs, die Validierung von Formularen oder komplexe Webanwendungen handelt – JavaScript ist die Sprache dafür.

Ähnlich wie bei CSS ist es bewährte Praxis, JavaScript-Code in separate `.js`-Dateien auszulagern. Die Einbindung erfolgt über das `<script>`-Element mit dem `src`-Attribut (source).

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Interaktive Webseite</title>
  <link rel="stylesheet" href="css/style.css">
  <script src="js/main.js"></script>
</head>
<body>
  <!-- ... Inhalt ... -->
</body>
</html>
```

Hier wird eine Datei `main.js` aus dem Unterordner `js` geladen.

**Ein wichtiger Hinweis zum Ladeverhalten:** Wenn ein Browser beim Parsen des HTML-Codes auf ein `<script>`-Tag ohne weitere Attribute stößt, hält er inne. Er stoppt das Rendern der Seite, lädt die JavaScript-Datei herunter und führt sie sofort aus. Erst danach setzt er das Parsen des restlichen HTML fort. Das nennt man "render-blocking". Wenn deine JavaScript-Datei groß ist oder von einem langsamen Server geladen wird, kann dies die wahrgenommene Ladezeit deiner Seite erheblich verlangsamen. Der Nutzer starrt auf eine weiße Seite, obwohl der restliche Inhalt vielleicht schon längst hätte angezeigt werden können.

Aus diesem Grund gibt es zwei wichtige Attribute, die du kennen solltest: `defer` and `async`.

*   **`defer`**: Mit `defer` wiesest du den Browser an, die Skriptdatei parallel zum Parsen des HTML herunterzuladen. Die Ausführung des Skripts wird jedoch zurückgestellt (`to defer`), bis das gesamte HTML-Dokument geparst wurde. Die Skripte werden zudem in der Reihenfolge ausgeführt, in der sie im HTML stehen. Dies ist die sicherste und meist empfohlene Methode, wenn dein Skript auf Elemente des DOM (Document Object Model) zugreifen muss und die Reihenfolge der Skripte wichtig ist.

    ```html
    <script src="js/library.js" defer></script>
    <script src="js/main.js" defer></script> 
    <!-- library.js wird garantiert vor main.js ausgeführt -->
    ```

*   **`async`**: Das `async`-Attribut (asynchronous) weist den Browser ebenfalls an, das Skript parallel herunterzuladen. Der entscheidende Unterschied ist, dass das Skript ausgeführt wird, sobald der Download abgeschlossen ist – unabhängig davon, ob das HTML-Parsing beendet ist oder nicht. Dies kann das Parsen unterbrechen. Die Reihenfolge der Ausführung ist bei mehreren `async`-Skripten nicht garantiert. `async` eignet sich gut für unabhängige Skripte, wie zum Beispiel Tracking-Codes oder Werbeanzeigen, die nicht vom Rest der Seite abhängen.

    ```html
    <script src="js/analytics.js" async></script>
    <script src="js/ads.js" async></script>
    <!-- Es ist nicht garantiert, welches Skript zuerst ausgeführt wird -->
    ```

Wegen des Render-Blockings ist es eine gängige Praxis, `<script>`-Tags ganz an das Ende des `<body>`-Elements zu setzen, kurz vor dem schließenden `</body>`-Tag. Dies hat einen ähnlichen Effekt wie `defer`, da das HTML bereits vollständig geparst ist, wenn der Browser auf die Skripte stößt. Mit `defer` im `<head>` erreichst du jedoch, dass der Download des Skripts früher beginnt, was die Gesamtladezeit weiter optimieren kann.

#### Webfonts und Icons

Um deiner Seite eine individuelle Typografie zu verleihen, nutzt du oft Webfonts, die nicht auf dem System des Nutzers vorinstalliert sind. Dienste wie Google Fonts machen die Einbindung sehr einfach. Meistens bekommst du von diesen Diensten ein `<link>`-Element, das du in deinen `<head>` einfügst.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
```

Hier siehst du gleich drei `<link>`-Tags. Die ersten beiden mit `rel="preconnect"` sind eine Performance-Optimierung. Sie weisen den Browser an, frühzeitig eine Verbindung zu den Font-Servern aufzubauen, was den späteren Download beschleunigt. Das dritte `<link>`-Tag lädt eine spezielle CSS-Datei von Google, die wiederum die eigentlichen Schriftdateien über `@font-face`-Regeln einbindet.

#### Favicons: Das Symbol deiner Seite

Das kleine Symbol, das im Browser-Tab, in Lesezeichen oder auf dem Homescreen von Mobilgeräten angezeigt wird, nennt man Favicon. Es ist ein wichtiges Element für den Wiedererkennungswert deiner Marke. Auch Favicons werden über das `<link>`-Element im `<head>` eingebunden.

Traditionell war dies eine einzelne `.ico`-Datei:

```html
<link rel="shortcut icon" href="favicon.ico" type="image/x-icon">
```

Heute ist es üblich, mehrere Versionen für verschiedene Geräte und Auflösungen bereitzustellen. Moderne Browser bevorzugen oft Vektorgrafiken (`.svg`) oder hochauflösende `.png`-Dateien.

Ein umfassenderes Favicon-Setup könnte so aussehen:

```html
<!-- Klassisches Favicon für ältere Browser -->
<link rel="icon" href="/favicon.ico" sizes="any">

<!-- Modernes, skalierbares SVG-Favicon -->
<link rel="icon" href="/favicon.svg" type="image/svg+xml">

<!-- Icon für Apple-Geräte (Homescreen) -->
<link rel="apple-touch-icon" href="/apple-touch-icon.png">

<!-- Web App Manifest für Android und andere -->
<link rel="manifest" href="/site.webmanifest">
```

Jedes `<link>`-Element bedient einen anderen Anwendungsfall. Der Browser wählt automatisch das am besten geeignete Icon aus.

#### Performance-Hinweise: Ressourcen vorladen

Neben dem bereits erwähnten `preconnect` gibt es weitere `rel`-Werte, mit denen du dem Browser Hinweise zur Optimierung des Ladevorgangs geben kannst.

*   `rel="preload"`: Wenn du weißt, dass eine bestimmte Ressource (z. B. ein wichtiges Hintergrundbild, eine Schriftart oder ein Skript) später auf der Seite dringend benötigt wird, kannst du den Browser anweisen, sie frühzeitig mit hoher Priorität zu laden. Das `as`-Attribut ist hierbei entscheidend, da es dem Browser den Typ der Ressource mitteilt.

    ```html
    <!-- Eine wichtige Schriftart vorladen, die im CSS verwendet wird -->
    <link rel="preload" href="/fonts/meine-schrift.woff2" as="font" type="font/woff2" crossorigin>

    <!-- Ein JavaScript vorladen, das später im Body geladen wird -->
    <link rel="preload" href="js/critical-script.js" as="script">
    ```

*   `rel="dns-prefetch"`: Eine noch schlankere Version von `preconnect`. Der Browser löst hier nur die DNS-Adresse einer Domain im Voraus auf, ohne eine vollständige Verbindung aufzubauen. Das ist nützlich für Ressourcen von Drittanbietern, von denen du weißt, dass sie später geladen werden.

    ```html
    <link rel="dns-prefetch" href="https://api.example.com">
    ```

Die Einbindung externer Ressourcen im `<head>` ist also weit mehr als nur das Verlinken einer CSS-Datei. Es ist die Kommandozentrale, in der du das Laden, die Darstellung und die Performance deiner Webseite maßgeblich steuerst. Ein gut strukturierter `<head>`-Bereich ist das Kennzeichen eines professionellen Webentwicklers, der nicht nur die Funktionalität, sondern auch das Nutzererlebnis im Blick hat.
