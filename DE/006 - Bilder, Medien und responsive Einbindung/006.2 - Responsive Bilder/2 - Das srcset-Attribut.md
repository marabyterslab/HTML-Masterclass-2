# Das srcset-Attribut

### Das srcset-Attribut: Bilder für jede Bildschirmgröße

Stell dir vor, du betrachtest eine Webseite auf einem riesigen 4K-Monitor. Die Bilder sind gestochen scharf und detailreich – perfekt. Jetzt öffnest du dieselbe Seite auf deinem Smartphone, während du im Zug sitzt und nur eine langsame mobile Datenverbindung hast. Die Webseite lädt quälend langsam, weil im Hintergrund genau dasselbe riesige Bild heruntergeladen wird, das für den 4K-Monitor gedacht war. Das verbraucht nicht nur unnötig Datenvolumen, sondern frustriert auch, weil die meiste Detailfülle auf dem kleinen Display ohnehin verloren geht.

Genau hier kommt das `srcset`-Attribut ins Spiel. Es ist die HTML-Lösung für eines der fundamentalsten Probleme des responsiven Webdesigns: wie man das richtige Bild für das richtige Gerät zur richtigen Zeit ausliefert.

#### Das Grundprinzip: Eine Auswahl anbieten

Früher hatten wir nur das `src`-Attribut im `<img>`-Tag. Es war eine simple Anweisung: "Browser, lade genau diese eine Bilddatei."

```html
<img src="mein-bild.jpg" alt="Ein einzelnes Bild für alle.">
```

Das `srcset`-Attribut erweitert diesen Ansatz. Statt nur einer einzigen Bildquelle gibst du dem Browser eine ganze Liste von Bildern zur Auswahl an. Du sagst ihm quasi: "Hier, schau mal, ich habe dieses Bild in verschiedenen Größen. Such dir bitte selbst die Version aus, die für den aktuellen Nutzer am besten passt."

Der Browser ist dabei ziemlich schlau. Er berücksichtigt bei seiner Entscheidung verschiedene Faktoren:

*   **Die Größe des Anzeigebereichs (Viewport):** Wie viel Platz hat das Bild auf dem Bildschirm tatsächlich zur Verfügung?
*   **Die Pixeldichte des Displays:** Handelt es sich um ein Standarddisplay oder ein hochauflösendes "Retina"-Display, das mehr Bildpixel benötigt, um scharf auszusehen?
*   **Die Netzwerkgeschwindigkeit (manchmal):** Einige Browser können sogar die Verbindungsqualität einbeziehen und bei einer langsamen Verbindung bewusst eine kleinere Bildversion wählen.

Du gibst die Kontrolle also an den Browser ab, aber du lieferst ihm alle Informationen, die er für eine kluge Entscheidung braucht. Das `srcset`-Attribut lässt sich auf zwei primäre Weisen nutzen: einmal mit dem `x`-Deskriptor für die Pixeldichte und einmal mit dem `w`-Deskriptor für die Bildbreite.

#### Auflösungswechsel mit dem `x`-Deskriptor

Die einfachste Anwendung von `srcset` ist die Unterscheidung nach Pixeldichte. Moderne Smartphones, Tablets und viele Laptops haben Displays mit einer hohen Pixeldichte. Wo ein älterer Monitor auf einem bestimmten Bereich vielleicht 100x100 Pixel anzeigt (eine Pixeldichte von `1x`), quetscht ein "Retina"-Display auf dieselbe Fläche 200x200 Pixel (`2x`) oder sogar 300x300 Pixel (`3x`).

Um auf diesen hochauflösenden Displays scharf auszusehen, braucht ein Bild, das im Layout 100 Pixel breit ist, bei einem `2x`-Display eine tatsächliche Bilddatei, die 200 Pixel breit ist.

Mit dem `x`-Deskriptor kannst du dem Browser genau diese Varianten anbieten.

```html
<img src="logo-1x.png"
     srcset="logo-2x.png 2x, logo-3x.png 3x"
     alt="Firmenlogo">
```

Schauen wir uns diesen Code genau an:

*   `src="logo-1x.png"`: Dies ist das Fallback. Browser, die `srcset` nicht verstehen (was heute extrem selten ist), laden einfach dieses Bild. Es dient gleichzeitig als die Standardversion für `1x`-Displays.
*   `srcset="logo-2x.png 2x, logo-3x.png 3x"`: Das ist die Liste der Optionen. Jeder Eintrag besteht aus dem Dateipfad und dem `x`-Deskriptor, der die zugehörige Pixeldichte angibt. Ein Browser auf einem `2x`-Display wird also die `logo-2x.png` anfordern, während ein Browser auf einem `3x`-Display die `logo-3x.png` wählt.

Dieser Ansatz eignet sich hervorragend für Bilder mit fester Größe, wie Icons oder Logos, deren Anzeigegröße im CSS fest definiert ist. Für flexible, responsive Bilder, deren Größe sich mit dem Layout ändert, gibt es jedoch eine noch mächtigere Methode.

#### Viewport-abhängige Auswahl mit dem `w`-Deskriptor und dem `sizes`-Attribut

Das eigentliche Potenzial von `srcset` entfaltet sich in Kombination mit dem `w`-Deskriptor und dem `sizes`-Attribut. Diese Kombination ist die Standardlösung für responsive Bilder, die sich an die Breite des Viewports anpassen.

**Der `w`-Deskriptor**

Im Gegensatz zum `x`-Deskriptor, der eine relative Dichte angibt, beschreibt der `w`-Deskriptor die tatsächliche, physische Breite der Bilddatei in Pixeln.

```html
<img srcset="foto-klein-480w.jpg 480w,
             foto-mittel-800w.jpg 800w,
             foto-gross-1200w.jpg 1200w"
     src="foto-mittel-800w.jpg"
     alt="Ein Landschaftsfoto bei Sonnenuntergang.">
```

Hier teilst du dem Browser mit: "Ich habe drei Versionen dieses Fotos. Eine ist 480 Pixel breit, eine 800 und eine 1200." Der Browser kennt nun das Menü der verfügbaren Bilder, aber er weiß noch nicht, wie groß der "Teller" ist, auf dem das Bild serviert werden soll. Er weiß also noch nicht, wie viel Platz das Bild im Layout tatsächlich einnehmen wird.

**Das `sizes`-Attribut: Dem Browser den Kontext geben**

Hier kommt das `sizes`-Attribut ins Spiel. Es ist der unverzichtbare Partner des `w`-Deskriptors. Mit `sizes` beschreibst du, wie breit das Bild in Abhängigkeit von der Viewport-Breite dargestellt wird. Die Syntax mag auf den ersten Blick etwas ungewohnt wirken, aber sie ist unglaublich mächtig.

Das `sizes`-Attribut enthält eine Liste von Medienbedingungen und den dazugehörigen Bildbreiten.

```html
sizes="(max-width: 600px) 100vw, 50vw"
```

Lass uns das übersetzen:

1.  ` (max-width: 600px) 100vw`: "Browser, WENN der Viewport maximal 600px breit ist, DANN wird dieses Bild 100% der Viewport-Breite einnehmen (`100vw`)." `vw` steht für "viewport width".
2.  `50vw`: "In ALLEN ANDEREN Fällen (also wenn der Viewport breiter als 600px ist), wird das Bild 50% der Viewport-Breite einnehmen." Der letzte Wert in der Liste hat keine Medienbedingung und dient als Standardwert.

Der Browser liest diese Liste von links nach rechts und nutzt die erste Bedingung, die zutrifft.

**Das Zusammenspiel von `srcset` und `sizes`**

Jetzt fügen wir alles zusammen. Der Browser hat nun alle Puzzleteile, um die perfekte Wahl zu treffen:

1.  Er prüft die Viewport-Breite. Nehmen wir an, du surfst auf einem Smartphone mit einer Breite von 360px.
2.  Er schaut sich das `sizes`-Attribut an: `(max-width: 600px) 100vw, 50vw`. Die erste Bedingung `(max-width: 600px)` trifft zu.
3.  Er berechnet die Anzeigegröße des Bildes: `100vw` bei einem 360px breiten Viewport ergibt eine Bildbreite von 360px.
4.  Er berücksichtigt die Pixeldichte des Geräts. Nehmen wir an, es ist ein `2x`-Display. Er muss also ein Bild laden, das scharf genug für einen 360px breiten Slot auf einem `2x`-Display ist. Er multipliziert also: 360px * 2 = 720px. Er sucht nach einer Bilddatei, die mindestens 720px breit ist.
5.  Er schaut sich das `srcset`-Attribut an: `foto-klein-480w.jpg 480w`, `foto-mittel-800w.jpg 800w`, `foto-gross-1200w.jpg 1200w`.
6.  Er trifft seine Wahl: Die `480w`-Version ist zu klein. Die `800w`-Version ist die nächstgrößere und damit die perfekte Wahl. Er wird `foto-mittel-800w.jpg` herunterladen.

Ohne `srcset` und `sizes` hätte dieses Smartphone möglicherweise die riesige `1200w`-Datei oder sogar eine noch größere Version geladen – eine pure Verschwendung von Bandbreite und Rechenleistung.

Hier ist ein vollständiges, realistisches Beispiel:

```html
<img srcset="berg-480w.jpg 480w,
             berg-800w.jpg 800w,
             berg-1200w.jpg 1200w,
             berg-1600w.jpg 1600w"
     sizes="(max-width: 500px) 100vw,
            (max-width: 900px) 70vw,
            880px"
     src="berg-800w.jpg"
     alt="Ein majestätischer Berg mit schneebedeckter Spitze.">
```

In diesem Fall haben wir ein komplexeres Layout:
*   Auf sehr kleinen Bildschirmen (bis 500px) ist das Bild bildschirmfüllend (`100vw`).
*   Auf mittelgroßen Bildschirmen (501px bis 900px) nimmt es 70% der Breite ein, vielleicht weil daneben eine Seitenleiste erscheint (`70vw`).
*   Auf allen größeren Bildschirmen hat das Bild eine feste maximale Breite von 880px, weil es sich in einem Inhaltscontainer mit fester Breite befindet.

#### Praktische Tipps und bewährte Methoden

*   **Immer `src` und `alt` angeben:** Das `src`-Attribut ist dein Fallback für sehr alte Browser und das `alt`-Attribut ist für die Barrierefreiheit unerlässlich. Ein `<img>`-Tag ohne `src` und `alt` ist unvollständig.
*   **Wähle sinnvolle Bildgrößen:** Du musst nicht 20 verschiedene Versionen eines Bildes erstellen. Meistens reichen 3 bis 5 gut gewählte Größen (z. B. 480px, 800px, 1200px, 1600px) aus, um die meisten Geräte optimal zu versorgen.
*   **Automatisiere den Prozess:** Das manuelle Erstellen und Verwalten all dieser Bildgrößen ist mühsam. Moderne Entwicklungswerkzeuge (Build-Tools wie Vite oder Webpack) oder Content-Management-Systeme (CMS) können diesen Prozess vollständig automatisieren. Du lädst ein einziges hochauflösendes Bild hoch und das System generiert alle kleineren Versionen und den korrekten HTML-Code für dich.
*   **Benenne deine Dateien logisch:** Eine Konvention wie `bildname-breite_in_pixel.jpg` (z. B. `berg-800w.jpg`) hilft dir, den Überblick zu behalten und macht deinen Code selbsterklärend.

Indem du `srcset` und `sizes` meisterst, machst du einen gewaltigen Schritt nach vorn. Du sorgst nicht nur dafür, dass deine Webseiten auf allen Geräten gut aussehen, sondern auch dafür, dass sie schnell, effizient und ressourcenschonend sind. Du lieferst jedem Nutzer eine maßgeschneiderte Erfahrung und respektierst dabei sein Datenvolumen und seine Zeit.
