# Manifest-Dateien für PWA

### Manifest-Dateien: Das Herz deiner Progressive Web App

Nachdem wir uns mit Favicons beschäftigt haben, die deiner Webseite ein kleines, wiedererkennbares Gesicht im Browser-Tab geben, gehen wir nun einen entscheidenden Schritt weiter. Stell dir vor, deine Webseite verhält sich nicht mehr nur wie eine Webseite, sondern fast wie eine native App, die man auf dem Smartphone oder Desktop installieren kann. Genau das ermöglichen Progressive Web Apps (PWAs), und ihr zentrales Steuerungselement ist die sogenannte Manifest-Datei.

#### Was ist eine PWA und was hat das Manifest damit zu tun?

Eine Progressive Web App ist im Grunde eine Webseite, die mit modernen Web-Technologien so aufgerüstet wird, dass sie sich wie eine installierte Anwendung anfühlt und verhält. Sie kann offline funktionieren, Push-Benachrichtigungen senden und – für uns an dieser Stelle am wichtigsten – auf dem Startbildschirm des Nutzers platziert werden, komplett mit eigenem Icon und Startbildschirm (Splash Screen).

Damit der Browser und das Betriebssystem wissen, *wie* sie deine Webseite als App behandeln sollen, benötigen sie eine Art Steckbrief oder Konfigurationsdatei. Und genau das ist die Web App Manifest-Datei. Es ist eine einfache JSON-Datei, in der du Metadaten über deine Anwendung definierst: wie sie heißen soll, welche Icons sie in verschiedenen Größen verwendet, welche Seite beim Start geladen wird und wie sich das Anwendungsfenster verhalten soll.

Diese Datei ist der Schlüssel, um den Sprung von einer Webseite im Browser-Tab zu einer Ikone auf dem Homescreen zu schaffen.

#### Die Manifest-Datei erstellen und einbinden

Die Manifest-Datei ist üblicherweise eine Datei namens `manifest.json` oder `manifest.webmanifest`, die du im Hauptverzeichnis deines Webprojekts ablegst. Der Inhalt ist, wie erwähnt, im JSON-Format (JavaScript Object Notation) geschrieben, also eine Sammlung von Schlüssel-Wert-Paaren.

Um dem Browser mitzuteilen, dass es für deine Seite ein Manifest gibt und wo er es finden kann, verlinkst du es im `<head>`-Bereich deines HTML-Dokuments. Das geschieht mit einem einfachen `<link>`-Tag:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meine PWA</title>
    <link rel="manifest" href="/manifest.json">
    <!-- Weitere Metadaten, CSS-Links etc. -->
</head>
<body>
    <!-- Dein Seiteninhalt -->
</body>
</html>
```

Der entscheidende Teil ist `rel="manifest"`. Daran erkennt der Browser, dass es sich bei der verlinkten Datei um das App-Manifest handelt und beginnt, es zu verarbeiten.

#### Die wichtigsten Eigenschaften im Manifest

Eine Manifest-Datei kann viele verschiedene Eigenschaften enthalten. Schauen wir uns die wichtigsten an, die du für eine solide PWA benötigst.

##### `name` und `short_name`

Diese beiden Eigenschaften definieren den Namen deiner Anwendung.

-   `name`: Der vollständige Name deiner App. Er wird zum Beispiel im Installations-Dialog angezeigt.
-   `short_name`: Ein kürzerer Name, der verwendet wird, wenn der Platz begrenzt ist, wie zum Beispiel unter dem App-Icon auf dem Homescreen eines Smartphones.

```json
{
  "name": "Meine fantastische Wetter-Anwendung",
  "short_name": "Wetter-App"
}
```

##### `icons`

Hier wird es richtig interessant, denn diese Eigenschaft knüpft direkt an unser Wissen über Icons an. Statt nur eines Favicons definierst du hier ein Array von Icons in verschiedenen Größen und Formaten. Das Betriebssystem wählt dann automatisch das am besten passende Icon für den jeweiligen Kontext aus – sei es für den Homescreen, den App-Umschalter, die Benachrichtigungen oder den Startbildschirm.

Jedes Icon wird als Objekt mit den Eigenschaften `src` (der Pfad zur Bilddatei), `sizes` (die Größe in Pixeln) und `type` (der MIME-Typ des Bildes) definiert.

```json
{
  "icons": [
    {
      "src": "/icons/icon-72x72.png",
      "sizes": "72x72",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-96x96.png",
      "sizes": "96x96",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

Es ist eine gute Praxis, mindestens ein Icon in 192x192 Pixeln und eines in 512x512 Pixeln bereitzustellen. Das 192er-Icon wird oft als Standard-Icon verwendet, während das 512er-Icon für den Splash Screen genutzt wird, der beim Start der App kurz angezeigt wird.

Für fortgeschrittene Anwendungsfälle gibt es noch die `purpose`-Eigenschaft. Mit `"purpose": "maskable"` kannst du ein Icon bereitstellen, das von Betriebssystemen wie Android so zugeschnitten werden kann, dass es sich nahtlos in die Form der anderen App-Icons einfügt (rund, quadratisch mit abgerundeten Ecken usw.).

##### `start_url`

Diese Eigenschaft legt fest, welche Seite deiner Web-Anwendung geladen werden soll, wenn der Nutzer die installierte App über das Homescreen-Icon startet. Meistens ist dies einfach das Stammverzeichnis `"/"` oder eine bestimmte Startseite wie `"/index.html"`.

```json
{
  "start_url": "/"
}
```

##### `display`

Mit `display` steuerst du, wie das Fenster deiner App aussehen soll. Hier entscheidest du, wie viel vom typischen Browser-Interface (Adressleiste, Buttons etc.) sichtbar ist. Die gängigsten Werte sind:

-   `browser`: Der Standard. Deine Webseite wird in einem normalen Browser-Tab mit der vollen Benutzeroberfläche geöffnet.
-   `minimal-ui`: Ähnlich wie `standalone`, aber mit einer minimalen Navigationsleiste (z.B. Zurück- und Neu-Laden-Buttons).
-   `standalone`: Dies ist die häufigste Wahl für PWAs. Deine App wird in einem eigenen Fenster ohne Browser-Adressleiste oder andere UI-Elemente geöffnet. Sie fühlt sich dadurch wie eine eigenständige, native App an.
-   `fullscreen`: Die App nimmt den gesamten Bildschirm ein, ohne jegliche System-UI (wie die Statusleiste bei Smartphones). Ideal für Spiele oder immersive Medienanwendungen.

```json
{
  "display": "standalone"
}
```

##### `background_color` und `theme_color`

Diese beiden Eigenschaften helfen dir, das visuelle Erscheinungsbild deiner App zu gestalten, noch bevor die eigentlichen Inhalte geladen sind.

-   `background_color`: Definiert die Hintergrundfarbe des Splash Screens, der kurz angezeigt wird, während deine App startet. Dies verhindert ein unschönes Aufblitzen einer weißen Seite und sorgt für einen weicheren Übergang.
-   `theme_color`: Bestimmt die Farbe von UI-Elementen, die vom Betriebssystem oder Browser um deine App herum angezeigt werden, zum Beispiel die Titelleiste des Fensters auf dem Desktop oder die Statusleiste auf Android.

```json
{
  "background_color": "#ffffff",
  "theme_color": "#3367D6"
}
```

Die `theme_color` im Manifest sollte idealerweise mit dem Meta-Tag `theme-color` in deinem HTML-Header übereinstimmen, um ein konsistentes Erlebnis zu gewährleisten:

```html
<meta name="theme-color" content="#3367D6">
```

##### `scope`

Der `scope` (Geltungsbereich) definiert, welche URLs zur deiner App gehören. Wenn der Nutzer innerhalb der installierten App auf einen Link klickt, der außerhalb des `scope` liegt, wird dieser Link in einem normalen Browser-Fenster geöffnet. Damit stellst du sicher, dass der Nutzer nicht versehentlich in einem fensterlosen App-Modus auf einer fremden Webseite landet. Wenn du den `scope` auf `"/"` setzt, bedeutet das, dass alle Seiten deiner Domain Teil der App sind.

```json
{
  "scope": "/"
}
```

#### Ein vollständiges Beispiel

Fassen wir all diese Eigenschaften zu einer kompletten `manifest.json`-Datei zusammen. So könnte eine solide Basiskonfiguration für eine PWA aussehen:

```json
{
  "name": "HTML Masterclass Notizen",
  "short_name": "HTML Notizen",
  "description": "Eine einfache App zum Verwalten von Notizen aus der HTML-Masterclass.",
  "start_url": "/",
  "scope": "/",
  "display": "standalone",
  "background_color": "#f7f7f7",
  "theme_color": "#0056b3",
  "icons": [
    {
      "src": "/icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png",
      "purpose": "any maskable"
    },
    {
      "src": "/icons/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "any"
    }
  ]
}
```

In diesem Beispiel haben wir zusätzlich eine `description` hinzugefügt, die in manchen Kontexten (wie App-Stores) angezeigt werden kann.

Die Manifest-Datei ist somit weit mehr als nur eine Erweiterung des Favicon-Konzepts. Sie ist die Geburtsurkunde deiner Web-Anwendung und der erste, unerlässliche Schritt, um eine Webseite in eine installierbare, app-ähnliche Erfahrung zu verwandeln, die sich nahtlos in das Ökosystem der Nutzergeräte integriert.
