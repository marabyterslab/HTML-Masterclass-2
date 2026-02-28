# Assets vorbereiten

### Assets vorbereiten: Das Rohmaterial für deine Website

Bevor du auch nur eine einzige Zeile HTML-Code schreibst, beginnt jedes Webprojekt mit einer Phase, die oft übersehen wird, aber für den späteren Erfolg entscheidend ist: die Vorbereitung deiner Assets. Stell dir vor, du möchtest ein Gourmet-Menü kochen. Du würdest auch nicht einfach anfangen und hoffen, dass du alle Zutaten findest. Du gehst einkaufen, wäschst das Gemüse, legst das Fleisch bereit und stellst sicher, dass alle Gewürze griffbereit sind. Genau das tun wir jetzt für unsere Website.

Assets sind alle Dateien, die deine Website neben dem reinen Code benötigt, um zum Leben zu erwecken. Dazu gehören Bilder, Videos, Schriftarten (Fonts), Icons und manchmal auch Audiodateien. Eine sorgfältige Vorbereitung dieser digitalen Zutaten sorgt nicht nur für Ordnung und eine leichtere Entwicklung, sondern hat auch einen massiven Einfluss auf die Ladezeit und die Benutzererfahrung deiner fertigen Seite.

#### Die Grundlage: Eine sinnvolle Ordnerstruktur

Ordnung ist das halbe Leben – und in der Webentwicklung vielleicht sogar mehr. Eine klare und konsistente Ordnerstruktur ist der erste und wichtigste Schritt. Sie hilft dir, den Überblick zu behalten, besonders wenn dein Projekt wächst. Eine bewährte und einfache Struktur für den Anfang könnte so aussehen:

```
projekt-ordner/
├── index.html
└── assets/
    ├── css/
    |   └── style.css
    ├── js/
    |   └── script.js
    ├── images/
    |   ├── hero-background.jpg
    |   └── logo.svg
    └── fonts/
        └── open-sans-regular.woff2
```

In diesem Beispiel liegt deine Haupt-HTML-Datei im Wurzelverzeichnis (`projekt-ordner`). Alle unterstützenden Dateien, also unsere Assets, befinden sich in einem eigenen `assets`-Ordner. Innerhalb dieses Ordners schaffen wir weitere Unterordner für jede Art von Asset: `css` für Stylesheets, `js` für JavaScript-Dateien, `images` für Bilder und `fonts` für Schriftarten. Diese Trennung ist Gold wert. Du weißt immer genau, wo du suchen musst, und deine Pfade im Code (`<img src="assets/images/logo.svg">`) sind logisch und leicht nachzuvollziehen.

#### Bilder: Das visuelle Herzstück

Bilder machen oft den größten Teil der Dateigröße einer Website aus. Deshalb ist hier besondere Sorgfalt geboten. Es geht um den perfekten Kompromiss zwischen visueller Qualität und minimaler Dateigröße.

**Das richtige Format wählen**

Nicht jedes Bildformat ist für jeden Zweck geeignet. Die drei wichtigsten Formate, die du kennen musst, sind JPEG, PNG und SVG. Dazu gesellt sich das moderne WebP-Format.

*   **JPEG (.jpg, .jpeg):** Deine erste Wahl für Fotos und komplexe Bilder mit vielen Farbverläufen (wie ein Sonnenuntergang). JPEG verwendet eine "verlustbehaftete" Komprimierung, was bedeutet, dass bei der Verkleinerung der Dateigröße einige Bildinformationen verloren gehen. Für das menschliche Auge ist dieser Verlust bei Fotos jedoch meist kaum wahrnehmbar, während die Dateigröße drastisch reduziert wird. JPEG unterstützt keine Transparenz.

*   **PNG (.png):** Perfekt für Grafiken mit harten Kanten, Logos oder Bilder, die einen transparenten Hintergrund benötigen (z. B. ein freigestelltes Produktbild). PNG nutzt eine "verlustfreie" Komprimierung, was bedeutet, dass die Qualität vollständig erhalten bleibt. Der Preis dafür ist oft eine größere Datei als bei einem vergleichbaren JPEG.

*   **SVG (.svg):** Scalable Vector Graphics sind keine Pixelbilder, sondern basieren auf mathematischen Beschreibungen von Formen und Kurven. Das macht sie ideal für Logos, Icons und einfache Illustrationen. Ihre Superkraft: Sie sind unendlich skalierbar, ohne an Qualität zu verlieren, und die Dateien sind meist winzig klein. Du kannst sie sogar mit CSS gestalten!

*   **WebP (.webp):** Ein modernes Format von Google, das die besten Eigenschaften von JPEG und PNG vereint. Es bietet eine exzellente Kompression (oft besser als JPEG) und unterstützt gleichzeitig Transparenz (wie PNG). Heutzutage wird WebP von allen modernen Browsern unterstützt und sollte oft deine bevorzugte Wahl sein, um die beste Performance zu erzielen.

**Optimierung ist alles**

Ein Bild direkt aus der Kamera oder vom Designer hat oft eine Auflösung von mehreren tausend Pixeln und eine Dateigröße von vielen Megabytes. Das auf eine Website zu laden, wäre eine Katastrophe für die Ladezeit. Die Optimierung besteht aus zwei Schritten:

1.  **Dimensionierung:** Skaliere das Bild auf die maximale Größe, in der es auf deiner Website angezeigt wird. Wenn ein Bild in deinem Design einen Bereich von 800 x 400 Pixeln einnimmt, dann skaliere das Bild auch genau auf diese Größe (oder die doppelte für hochauflösende "Retina"-Displays, also 1600 x 800 Pixel). Es hat keinen Sinn, ein 4000-Pixel-breites Bild zu laden, das der Browser dann mühsam herunterskalieren muss.

2.  **Kompression:** Nachdem das Bild die richtigen Abmessungen hat, jagst du es durch ein Kompressions-Tool. Es gibt fantastische Online-Dienste wie Squoosh.app oder TinyPNG, die die Dateigröße nochmals drastisch reduzieren, ohne die sichtbare Qualität spürbar zu beeinträchtigen.

**Sinnvolle Dateinamen**

Nenne deine Bilddateien niemals `IMG_7432.JPG` oder `bild1.png`. Gib ihnen beschreibende Namen. Das ist nicht nur für deine eigene Orientierung hilfreich, sondern auch für die Suchmaschinenoptimierung (SEO). Verwende Kleinbuchstaben und trenne Wörter mit Bindestrichen.

*   Schlecht: `Header Bild NEU.jpg`
*   Gut: `sonnenuntergang-am-strand-von-santorini.jpg`

#### Schriftarten (Fonts): Die Stimme deines Designs

Web-Schriftarten (Web Fonts) ermöglichen es dir, typografisch einzigartige Erlebnisse zu schaffen, die über die Standard-Systemschriften hinausgehen. Aber auch hier gilt: Performance ist wichtig.

**Das richtige Format: WOFF2**

Früher gab es eine ganze Reihe von Font-Formaten (EOT, TTF, WOFF). Heute ist die Sache einfach: **WOFF2 (.woff2)** ist der moderne Standard. Es bietet die beste Kompression und wird von allen aktuellen Browsern unterstützt. Wenn du eine Schriftart einbindest, benötigst du in der Regel nur noch das WOFF2-Format.

**Selbst hosten oder CDN nutzen?**

Du hast zwei Möglichkeiten, Web Fonts einzubinden:

1.  **Über einen Dienst wie Google Fonts:** Du bindest die Schriftart über einen Link in deinem HTML oder CSS ein. Der Browser des Nutzers lädt die Schriftart dann direkt von den Google-Servern. Das ist einfach und schnell einzurichten.

2.  **Selbst hosten:** Du lädst die Schriftart-Dateien (die .woff2-Dateien) herunter und legst sie in deinen `assets/fonts`-Ordner. Dann bindest du sie mit der `@font-face`-Regel in deinem CSS ein. Dies gibt dir die volle Kontrolle, vermeidet eine Anfrage an einen Drittanbieter-Server (gut für Datenschutz und Performance, da eine DNS-Abfrage entfällt) und ist die professionellere Methode für ein abgeschlossenes Projekt. Für unser Projekt werden wir die Schriftarten herunterladen und lokal einbinden.

#### Icons: Die kleinen, aber mächtigen Helfer

Für Icons gibt es heute eigentlich nur eine wirklich gute Antwort: SVG. Vergiss Icon-Fonts oder PNG-Sprites. Einzelne SVG-Dateien oder ein SVG-Sprite sind die flexibelste, schärfste und performanteste Lösung.

**Einzelne SVG-Dateien**

Du kannst jedes Icon als separate `.svg`-Datei speichern und wie ein normales Bild einfügen:
`<img src="assets/images/icons/menu-icon.svg" alt="Menü öffnen">`
Der Vorteil ist die Einfachheit. Der Nachteil: Für jedes Icon wird eine eigene Anfrage an den Server geschickt.

**SVG-Sprites**

Eine fortgeschrittenere und sehr effiziente Methode ist die Verwendung eines SVG-Sprites. Dabei werden alle Icons in einer einzigen SVG-Datei zusammengefasst. Jedes einzelne Icon wird innerhalb dieser Datei zu einem `<symbol>` mit einer eindeutigen ID.

Ein Sprite könnte vereinfacht so aussehen:

```html
<!-- in einer Datei namens icon-sprite.svg -->
<svg xmlns="http://www.w3.org/2000/svg" style="display: none;">
  <symbol id="icon-home" viewBox="0 0 24 24">
    <!-- Path-Daten für das Home-Icon -->
    <path d="..."/>
  </symbol>
  <symbol id="icon-user" viewBox="0 0 24 24">
    <!-- Path-Daten für das User-Icon -->
    <path d="..."/>
  </symbol>
</svg>
```

In deinem HTML-Code kannst du dann jedes Icon über seine ID referenzieren, ohne eine neue Datei laden zu müssen:

```html
<!-- Home-Icon anzeigen -->
<svg class="icon">
  <use xlink:href="assets/images/icon-sprite.svg#icon-home"></use>
</svg>

<!-- User-Icon anzeigen -->
<svg class="icon">
  <use xlink:href="assets/images/icon-sprite.svg#icon-user"></use>
</svg>
```

Der Browser muss nur eine einzige Sprite-Datei laden, was die Anzahl der Serveranfragen drastisch reduziert – ein enormer Performance-Gewinn, besonders bei vielen Icons.

Wenn du all diese Vorbereitungen getroffen hast – deine Ordnerstruktur steht, deine Bilder sind im richtigen Format, optimiert und sinnvoll benannt, deine Schriftarten liegen bereit und deine Icons sind als SVGs vorbereitet –, dann hast du eine perfekte, saubere und professionelle Basis geschaffen. Du hast deine Küche aufgeräumt und die Zutaten geschnippelt. Jetzt kann das eigentliche Kochen, das Schreiben des Codes, beginnen. Und es wird dir viel leichter von der Hand gehen.
