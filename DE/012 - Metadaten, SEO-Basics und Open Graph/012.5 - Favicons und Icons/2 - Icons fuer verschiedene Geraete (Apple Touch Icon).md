# Icons für verschiedene Geräte (Apple Touch Icon)

### Icons für verschiedene Geräte: Das Apple Touch Icon

Während das klassische Favicon primär für den Browser-Tab und die Lesezeichenleiste gedacht ist, hat die mobile Revolution ganz neue Anforderungen an Web-Icons gestellt. In einer Welt, in der das Smartphone für viele Menschen das primäre Tor zum Internet ist, speichern Nutzer Webseiten oft direkt auf ihrem Homescreen, um schnell darauf zugreifen zu können – fast so, als wären es native Apps.

Genau hier kommt das Apple Touch Icon ins Spiel. Es ist ein hochwertiges Icon, das speziell dafür entwickelt wurde, deine Webseite auf dem Homescreen von iPhones, iPads und auch vielen Android-Geräten ansprechend zu repräsentieren. Ohne dieses spezielle Icon würde das Gerät versuchen, einen Screenshot der Seite zu erstellen und diesen als unschönes, oft unleserliches Symbol zu verwenden. Ein definiertes Apple Touch Icon hingegen verleiht deiner Webseite einen professionellen, app-ähnlichen Charakter und stärkt deine Markenpräsenz direkt auf dem Gerät des Nutzers.

#### Die grundlegende Implementierung

Die Einbindung eines Apple Touch Icons ist erfreulich unkompliziert. Ähnlich wie beim Favicon nutzt du dafür ein `<link>`-Element im `<head>`-Bereich deines HTML-Dokuments. Die einfachste Form sieht so aus:

```html
<head>
  <title>Meine Webseite</title>
  <link rel="apple-touch-icon" href="/apple-touch-icon.png">
</head>
```

Lass uns diesen Code kurz aufschlüsseln:
*   `rel="apple-touch-icon"`: Dieses Attribut ist der entscheidende Hinweis für Apple-Geräte (und andere, die es unterstützen). Es signalisiert: „Hier findest du das Icon, das für den Homescreen verwendet werden soll.“
*   `href="/apple-touch-icon.png"`: Hier gibst du den Pfad zu deiner Icon-Datei an. Es ist eine bewährte Praxis, das Icon im Stammverzeichnis (Root) deiner Webseite abzulegen und ihm den Standardnamen `apple-touch-icon.png` zu geben. Früher haben iOS-Geräte sogar automatisch nach einer Datei mit diesem Namen im Root-Verzeichnis gesucht, auch ohne expliziten `<link>`-Tag. Heute solltest du dich aber immer auf die explizite Deklaration im HTML verlassen, da sie zuverlässiger ist.

Das Icon selbst sollte im PNG-Format vorliegen und – ganz wichtig – quadratisch sein.

#### Die richtige Größe für jedes Display

Die Welt der mobilen Geräte ist von einer Vielfalt an Bildschirmgrößen und Pixeldichten geprägt. Ein altes iPhone ohne Retina-Display hat ganz andere Anforderungen als ein modernes iPad Pro. Um auf jedem Gerät eine gestochen scharfe Darstellung zu gewährleisten, kannst du Icons in verschiedenen Auflösungen bereitstellen. Das Gerät wählt dann automatisch die am besten passende Größe aus.

Hierfür wird das `<link>`-Element um das `sizes`-Attribut erweitert:

```html
<head>
  <title>Meine Webseite</title>
  
  <!-- Für ältere iPhones ohne Retina-Display (veraltet, aber zur Vollständigkeit) -->
  <link rel="apple-touch-icon" sizes="57x57" href="/apple-touch-icon-57x57.png">
  
  <!-- Für iPads der 1. und 2. Generation -->
  <link rel="apple-touch-icon" sizes="72x72" href="/apple-touch-icon-72x72.png">
  
  <!-- Für iPhones mit Retina-Display (z.B. iPhone 4 bis iPhone 6) -->
  <link rel="apple-touch-icon" sizes="120x120" href="/apple-touch-icon-120x120.png">
  
  <!-- Für iPads mit Retina-Display -->
  <link rel="apple-touch-icon" sizes="152x152" href="/apple-touch-icon-152x152.png">
  
  <!-- Für iPhones mit höherer Auflösung (z.B. iPhone 6 Plus, iPhone X und neuer) -->
  <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon-180x180.png">
</head>
```

Das Gerät sucht sich aus dieser Liste das Icon heraus, dessen Größe am nächsten an der optimalen Auflösung für sein Display liegt, ohne kleiner zu sein. Wenn also ein Gerät ein 120x120 Pixel großes Icon benötigt, aber nur ein 152x152 Pixel großes Icon findet, wird es dieses nehmen und herunterskalieren. Das Ergebnis ist immer noch scharf. Findet es jedoch nur ein 72x72 Pixel großes Icon, müsste es dieses hochskalieren, was zu Unschärfe und Pixelbrei führen würde.

**Die moderne Strategie:**
In der Praxis musst du nicht mehr jede einzelne Größe bereitstellen. Die meisten modernen Geräte haben hochauflösende Displays. Eine sehr gute und einfache Strategie ist es daher, nur eine einzige, hochauflösende Version des Icons bereitzustellen. Eine Größe von **180x180 Pixeln** ist heute ein exzellenter Standard, der die meisten aktuellen Apple-Geräte optimal abdeckt. Kleinere Geräte skalieren das Icon dann einfach herunter.

Eine minimalistische, aber zukunftssichere Implementierung sieht also oft so aus:

```html
<head>
  <title>Meine Webseite</title>
  <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">
</head>
```
Du kannst die Größe sogar weglassen, wenn du nur ein Icon bereitstellst. Das Gerät wird es dann als Standard für alle Auflösungen verwenden. Die Angabe der Größe ist jedoch sauberer.

#### Design-Hinweise: Glanz und runde Ecken

Wenn du dein Icon gestaltest, gibt es zwei wichtige Dinge zu beachten, die iOS automatisch mit deinem Icon macht:

1.  **Runde Ecken:** iOS wendet auf alle Homescreen-Icons eine Maske an, um die charakteristischen abgerundeten Ecken zu erzeugen. Du solltest dein Icon also immer als **perfektes Quadrat** erstellen und die Ecken nicht selbst abrunden. Überlasse das dem Betriebssystem, damit es auf allen Geräten einheitlich aussieht.
2.  **Glanz-Effekt (historisch):** Ältere iOS-Versionen (vor iOS 7) haben standardmäßig einen leichten Glanz-Effekt auf das Icon gelegt, um ihm einen plastischeren Look zu verleihen. Wenn du das nicht wolltest, konntest du ein alternatives `rel`-Attribut verwenden: `apple-touch-icon-precomposed`. Das Suffix `-precomposed` signalisierte dem System: „Fasse mein Icon nicht an, es ist bereits fertig gestaltet.“

```html
<!-- Historisches Beispiel, heute kaum noch relevant -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon.png">
```

Seit der Einführung des Flat Designs mit iOS 7 wird dieser Glanz-Effekt nicht mehr angewendet. Das `precomposed`-Attribut ist damit praktisch überflüssig geworden. Du solltest dich heute an das Standardattribut `rel="apple-touch-icon"` halten.

Ein weiterer wichtiger Design-Hinweis betrifft die Transparenz. Anders als bei Favicons solltest du bei Apple Touch Icons **keine transparenten Bereiche** verwenden. iOS interpretiert Transparenz als Schwarz und füllt den Hintergrund deines Icons mit einer schwarzen Fläche auf. Gestalte dein Icon also immer mit einer vollflächigen, undurchsichtigen Hintergrundfarbe.

#### Mehr als nur Apple

Obwohl der Name „Apple Touch Icon“ auf den Ursprung hindeutet, hat sich dieser Standard weit über das Apple-Ökosystem hinaus verbreitet. Auch Android-Geräte suchen nach diesem Icon, wenn ein Nutzer eine Webseite zum Startbildschirm hinzufügt und keine spezifischeren Android-Icons (über eine `manifest.json`-Datei) definiert sind. Damit hat das `apple-touch-icon` eine Art universellen Status als hochwertiges Homescreen-Icon für Webseiten erlangt. Die Bereitstellung ist also nicht nur für die Nutzer von iPhones und iPads eine wertvolle Optimierung, sondern verbessert das Erlebnis für eine viel breitere Nutzerbasis.

Indem du ein durchdachtes und gut gestaltetes Apple Touch Icon bereitstellst, machst du einen entscheidenden Schritt, um deiner Webseite den letzten Schliff zu geben. Du schaffst eine Brücke zwischen der flüchtigen Welt des Browsers und dem personalisierten, persistenten Homescreen des Nutzers und sorgst dafür, dass deine Webseite auch dort einen professionellen und einprägsamen Eindruck hinterlässt.
