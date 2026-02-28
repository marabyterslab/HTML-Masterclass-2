# Optimierung von Dateigrößen

### Optimierung von Dateigrößen: Weniger ist mehr

Stell dir vor, du betrittst ein Geschäft und musst fünf Minuten warten, bis sich die Tür öffnet. Unwahrscheinlich, dass du lange bleibst, oder? Im Web ist es ganz ähnlich. Die Ladezeit einer Webseite ist einer der entscheidendsten Faktoren für den Erfolg. Und der größte Feind schneller Ladezeiten sind oft unoptimierte Bilder. Jedes Kilobyte, das du einsparst, ist ein direkter Gewinn für die Benutzererfahrung, schont das mobile Datenvolumen deiner Besucher und wird sogar von Suchmaschinen wie Google positiv bewertet.

In diesem Kapitel tauchen wir tief in die Kunst der Bildoptimierung ein. Es geht nicht darum, die Qualität deiner Bilder zu ruinieren, sondern darum, den perfekten Kompromiss zwischen visueller Brillanz und minimaler Dateigröße zu finden.

#### Die drei Säulen der Bildoptimierung

Die Größe einer Bilddatei wird im Wesentlichen von drei Faktoren bestimmt: den Pixel-Dimensionen, dem Dateiformat und dem Grad der Komprimierung. Wenn du diese drei Säulen meisterst, hast du die Kontrolle über die Performance deiner Webseite.

##### 1. Die richtigen Dimensionen wählen

Der häufigste Fehler ist, ein riesiges Bild hochzuladen und es dann per CSS auf die gewünschte Größe zu verkleinern. Wenn du zum Beispiel ein Foto mit 4000 x 3000 Pixeln in einen Bereich einfügst, der nur 800 x 600 Pixel groß ist, muss der Browser trotzdem das riesige Originalbild herunterladen. Das ist pure Verschwendung von Bandbreite.

Die Regel lautet: **Skaliere deine Bilder vor dem Upload auf die maximal benötigte Anzeigegröße.**

Wenn ein Bild auf deiner Webseite nie breiter als 900 Pixel angezeigt wird, dann sollte die Bilddatei auch nicht breiter als 900 Pixel sein.

**Sonderfall: Hochauflösende Displays (Retina)**

Moderne Geräte haben oft Displays mit einer sehr hohen Pixeldichte. Um auf diesen "Retina"-Displays scharf auszusehen, benötigen Bilder mehr Pixel. Eine gängige Praxis ist es, Bilder in doppelter Auflösung bereitzustellen. Für einen 900-Pixel-Container würdest du also ein 1800 Pixel breites Bild verwenden. Der Browser skaliert es dann herunter, was zu einer gestochen scharfen Darstellung führt. Wie du dem Browser diese verschiedenen Größen anbietest, sehen wir uns später im Abschnitt zur HTML-Einbindung an.

##### 2. Das passende Dateiformat finden

Nicht jedes Format ist für jeden Zweck geeignet. Die Wahl des richtigen Formats kann die Dateigröße drastisch reduzieren, ohne dass du an sichtbarer Qualität verlierst.

*   **JPEG (Joint Photographic Experts Group)**
    *   **Ideal für:** Fotos und Bilder mit vielen Farben und komplexen Verläufen.
    *   **Merkmale:** Nutzt eine verlustbehaftete Komprimierung (mehr dazu gleich), was zu sehr kleinen Dateigrößen führen kann. Unterstützt keine Transparenz.
    *   **Faustregel:** Dein Standardformat für alle fotografischen Inhalte.

*   **PNG (Portable Network Graphics)**
    *   **Ideal für:** Grafiken mit harten Kanten, Logos, Icons und Bilder, die Transparenz benötigen (z. B. ein freigestelltes Logo).
    *   **Merkmale:** Nutzt eine verlustfreie Komprimierung. Die Dateigrößen sind bei Fotos oft deutlich größer als bei JPEGs, aber bei Grafiken mit wenigen Farben ist PNG oft effizienter. Es gibt PNG-8 (bis 256 Farben) und PNG-24 (Millionen Farben), wobei PNG-8 kleinere Dateien erzeugt.
    *   **Faustregel:** Immer dann, wenn du Transparenz brauchst oder scharfe Linien (wie in einem Diagramm) erhalten müssen.

*   **GIF (Graphics Interchange Format)**
    *   **Ideal für:** Kurze, einfache Animationen.
    *   **Merkmale:** Auf 256 Farben beschränkt, was es für Fotos ungeeignet macht. Die Komprimierung ist für simple Animationen gut, aber moderne Videoformate sind oft überlegen.
    *   **Faustregel:** Nur für simple, loopende Animationen verwenden, bei denen ein Video übertrieben wäre.

*   **SVG (Scalable Vector Graphics)**
    *   **Ideal für:** Logos, Icons und einfache Illustrationen.
    *   **Merkmale:** SVG ist kein Pixelbild, sondern eine XML-basierte Beschreibung von Formen und Pfaden. Dadurch sind SVGs unendlich skalierbar, ohne an Qualität zu verlieren, und haben oft eine winzige Dateigröße.
    *   **Faustregel:** Wenn eine Grafik aus Linien, Kurven und Farbflächen besteht, ist SVG fast immer die beste Wahl.

*   **Moderne Formate: WebP und AVIF**
    *   **Ideal für:** Alles – sie können JPEG, PNG und GIF ersetzen.
    *   **Merkmale:** WebP und das noch neuere AVIF sind moderne Bildformate, die eine deutlich bessere Komprimierung als ihre Vorgänger bieten – oft bei gleicher oder sogar besserer visueller Qualität. Sie unterstützen sowohl verlustbehaftete als auch verlustfreie Komprimierung sowie Transparenz und Animationen.
    *   **Herausforderung:** Nicht alle älteren Browser unterstützen sie. Du musst also immer eine Fallback-Lösung (z. B. ein JPEG) bereitstellen. Wie das geht, zeige ich dir gleich.

##### 3. Die Kunst der Komprimierung

Nachdem du die richtigen Dimensionen und das richtige Format gewählt hast, kommt der letzte, entscheidende Schritt: die Komprimierung. Hier unterscheiden wir zwei grundlegende Arten:

*   **Verlustfreie Komprimierung (Lossless):**
    Diese Methode reduziert die Dateigröße, indem sie Bilddaten effizienter speichert, ohne dabei Informationen zu verwerfen. Stell es dir vor wie das Packen einer ZIP-Datei: Beim Entpacken ist alles wieder exakt so wie vorher. PNG und GIF nutzen diese Methode. Die Einsparungen sind moderat.

*   **Verlustbehaftete Komprimierung (Lossy):**
    Diese Methode analysiert das Bild und entfernt gezielt Informationen, die für das menschliche Auge kaum oder gar nicht wahrnehmbar sind. Einmal entfernt, sind diese Daten für immer verloren. JPEG und die modernen Formate WebP/AVIF nutzen diese Technik. Der Vorteil ist eine enorme Reduzierung der Dateigröße. Du kannst den Grad der Komprimierung selbst steuern (z. B. über einen Qualitätsregler von 0 bis 100). Bei einer Qualität von 70-80 % ist der Unterschied zum Original für die meisten Menschen nicht sichtbar, die Dateigröße aber oft um über 50 % reduziert.

**Werkzeuge für die Optimierung**

Du musst das nicht manuell machen. Es gibt fantastische Werkzeuge, die dir diese Arbeit abnehmen:

*   **Bildbearbeitungsprogramme:** Adobe Photoshop ("Für Web speichern"), Affinity Photo oder das kostenlose GIMP bieten exzellente Export-Dialoge, in denen du Format, Qualität und Dimensionen präzise einstellen kannst.
*   **Online-Tools:** Dienste wie [Squoosh.app](https://squoosh.app) (von Google) oder [TinyPNG](https://tinypng.com) sind unglaublich einfach zu bedienen. Du ziehst dein Bild hinein, wählst die Einstellungen und kannst live den Unterschied in Qualität und Dateigröße vergleichen.
*   **Automatisierte Werkzeuge:** In professionellen Web-Projekten werden Bilder oft automatisch während des Entwicklungsprozesses optimiert. Tools wie `imagemin` erledigen das für dich, sobald du neue Bilder zum Projekt hinzufügst.

#### Intelligente Einbindung in HTML

Jetzt, wo deine Bilder perfekt vorbereitet sind, müssen wir dem Browser noch auf die bestmögliche Weise mitteilen, welches Bild er wann laden soll. Modernes HTML bietet uns dafür mächtige Werkzeuge.

##### Responsive Bilder mit `srcset` und `sizes`

Erinnerst du dich an die Retina-Displays? Wir wollen nicht jedem Besucher das riesige 2x-Bild schicken, vor allem nicht auf einem Mobilgerät mit langsamer Verbindung. Mit dem `srcset`-Attribut können wir dem Browser eine Auswahl an Bildversionen zur Verfügung stellen.

```html
<img src="blume-mittel.jpg"
     srcset="blume-klein.jpg 400w,
             blume-mittel.jpg 800w,
             blume-gross.jpg 1600w"
     sizes="(max-width: 600px) 100vw, 50vw"
     alt="Eine Nahaufnahme einer leuchtend roten Mohnblume.">
```

Lass uns das aufschlüsseln:
*   `src`: Dies ist das Fallback für sehr alte Browser, die `srcset` nicht verstehen.
*   `srcset`: Hier listest du deine Bildversionen auf. Hinter jeden Dateinamen schreibst du die tatsächliche Breite des Bildes in Pixeln, gefolgt von einem `w` (für Width-Descriptor).
*   `sizes`: Das ist der knifflige, aber wichtigste Teil. Hier gibst du dem Browser einen Hinweis, wie viel Platz das Bild im Layout einnehmen wird.
    *   `(max-width: 600px) 100vw`: "Wenn der Bildschirm (Viewport) maximal 600px breit ist, wird dieses Bild 100% der Bildschirmbreite einnehmen (`100vw`)."
    *   `50vw`: "In allen anderen Fällen (also bei Bildschirmen breiter als 600px) wird das Bild 50% der Bildschirmbreite einnehmen."

Mit diesen Informationen kann der Browser eine intelligente Entscheidung treffen. Er kennt die Bildschirmbreite, die Pixeldichte des Geräts und die verfügbaren Bildgrößen. So kann er das kleinstmögliche Bild wählen, das in der gegebenen Situation noch scharf aussieht.

##### Moderne Formate mit dem `<picture>`-Element

Um moderne Formate wie AVIF oder WebP zu nutzen und gleichzeitig ältere Browser zu unterstützen, verwenden wir das `<picture>`-Element. Es funktioniert wie ein Wrapper um dein `<img>`-Tag.

```html
<picture>
  <!-- Biete dem Browser zuerst das modernste Format an (AVIF) -->
  <source srcset="blume.avif" type="image/avif">

  <!-- Wenn der Browser AVIF nicht kann, versucht er es mit WebP -->
  <source srcset="blume.webp" type="image/webp">

  <!-- Das <img>-Tag ist das letzte Fallback für alle Browser -->
  <!-- Es muss immer vorhanden sein! -->
  <img src="blume.jpg" alt="Eine Nahaufnahme einer leuchtend roten Mohnblume.">
</picture>
```

Der Browser geht die `<source>`-Elemente von oben nach unten durch. Das erste Format, das er versteht, wird geladen. Die anderen ignoriert er. Versteht er keines der `<source>`-Formate, fällt er auf das gute alte `<img>`-Tag zurück. So stellst du sicher, dass deine Seite für alle schnell ist, aber moderne Browser von den besten Technologien profitieren.

##### Lazy Loading für Bilder "below the fold"

Nicht jedes Bild muss sofort geladen werden. Bilder, die erst beim Scrollen sichtbar werden ("below the fold"), können nachgeladen werden. Früher brauchte man dafür JavaScript, heute gibt es eine native HTML-Lösung: das `loading`-Attribut.

```html
<img src="grosses-bild.jpg" loading="lazy" alt="Ein Bild, das weiter unten auf der Seite ist.">
```

Mit `loading="lazy"` weist du den Browser an, mit dem Laden dieses Bildes zu warten, bis es sich dem sichtbaren Bereich nähert. Das verbessert die anfängliche Ladezeit der Seite enorm, da nur die sofort sichtbaren Inhalte geladen werden müssen. Für Bilder im sofort sichtbaren Bereich (z.B. ein Logo oder ein Hauptbanner) solltest du dieses Attribut weglassen, damit sie sofort geladen werden.
