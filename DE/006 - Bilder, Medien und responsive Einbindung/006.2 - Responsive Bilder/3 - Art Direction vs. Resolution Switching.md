# Art Direction vs. Resolution Switching

### Art Direction vs. Resolution Switching: Zwei Ansätze für ein Ziel

Wenn wir über responsive Bilder sprechen, geht es im Kern darum, dem Browser die nötigen Informationen zu geben, damit er für den jeweiligen Nutzer das bestmögliche Bild ausliefern kann. „Bestmöglich“ kann dabei aber zwei völlig unterschiedliche Dinge bedeuten: Entweder geht es um die technische Performance oder um die gestalterische Wirkung. Genau hier liegt der Unterschied zwischen den beiden fundamentalen Strategien: Resolution Switching und Art Direction.

Auch wenn sie oft in einem Atemzug genannt werden, lösen sie zwei verschiedene Probleme. Stell sie dir als zwei spezialisierte Werkzeuge in deinem Werkzeugkasten vor. Du würdest ja auch keinen Hammer benutzen, um eine Schraube einzudrehen. Lass uns diese beiden Werkzeuge genauer unter die Lupe nehmen.

#### Resolution Switching: Das Effizienz-Problem lösen

Stell dir ein großes, detailreiches Foto vor. Auf einem 27-Zoll-Desktop-Monitor sieht es fantastisch aus. Die Datei ist vielleicht 2 Megabyte groß und hat eine Auflösung von 3000 Pixeln in der Breite. Lädst du exakt dieselbe Datei auf einem Smartphone, dessen Bildschirm nur 400 Pixel breit ist, passiert Folgendes:

1.  Der Nutzer lädt unnötigerweise eine riesige Datei herunter, was Ladezeit und Datenvolumen kostet.
2.  Der Browser muss das riesige Bild auf eine winzige Größe herunterskalieren, was Rechenleistung erfordert.

Das Ergebnis ist eine schlechte User Experience. Das Bild sieht am Ende vielleicht genauso aus wie eine optimierte, kleinere Version, aber der Weg dorthin war ineffizient und langsam.

Genau hier kommt **Resolution Switching** (auf Deutsch etwa „Auflösungswahl“) ins Spiel. Das Ziel ist, dem Browser eine Auswahl desselben Bildes in verschiedenen Auflösungen anzubieten. Der Browser kann dann, basierend auf der Bildschirmgröße, der Pixeldichte (z. B. bei Retina-Displays) und der im CSS definierten Anzeigegröße des Bildes, die passendste Version auswählen.

Das Bildmotiv selbst bleibt dabei immer identisch. Wir tauschen lediglich eine niedrig aufgelöste Version gegen eine hoch aufgelöste aus.

Die technische Umsetzung erfolgt in der Regel mit dem `<img>`-Element und den Attributen `srcset` und `sizes`.

```html
<img 
  src="blume-800w.jpg" 
  srcset="blume-400w.jpg 400w,
          blume-800w.jpg 800w,
          blume-1200w.jpg 1200w,
          blume-1600w.jpg 1600w"
  sizes="(max-width: 600px) 100vw, 50vw"
  alt="Eine Nahaufnahme einer leuchtend roten Mohnblume.">
```

Schauen wir uns das genauer an:

*   **`src`**: Dies ist das Fallback. Browser, die `srcset` nicht verstehen, laden einfach dieses Bild. Es ist oft eine mittelgroße Version.
*   **`srcset`**: Hier listest du alle verfügbaren Bildversionen auf. Hinter jedem Dateinamen steht die tatsächliche, intrinsische Breite des Bildes, gefolgt von einem `w` (für Width). Das ist keine Pixelangabe, sondern eine Information für den Browser über die Quelldatei. Du sagst ihm: „Ich habe diese Datei, und sie ist in Wirklichkeit 1200 Pixel breit.“
*   **`sizes`**: Das ist der entscheidende Hinweis für den Browser. Hier beschreibst du, wie viel Platz das Bild im Layout einnehmen wird. Die Angabe `(max-width: 600px) 100vw, 50vw` bedeutet:
    *   „Wenn der Viewport **maximal 600 Pixel** breit ist, wird dieses Bild **100% der Viewport-Breite** (`100vw`) einnehmen.“
    *   „In allen anderen Fällen (also bei über 600 Pixel breiten Viewports) wird es **50% der Viewport-Breite** (`50vw`) einnehmen.“

Mit diesen Informationen – der Liste der verfügbaren Bilder (`srcset`) und der Angabe zur Layout-Größe (`sizes`) – kann der Browser eine intelligente Entscheidung treffen. Auf einem kleinen Smartphone mit 375px Breite wird er wahrscheinlich `blume-400w.jpg` oder `blume-800w.jpg` (für hochauflösende Displays) wählen. Auf einem großen Desktop, wo das Bild 50% des Viewports einnimmt (z.B. 800px), wird er eher zu `blume-1600w.jpg` greifen, um eine gestochen scharfe Darstellung zu gewährleisten.

**Die Kernaussage von Resolution Switching ist:** Du überlässt dem Browser die Kontrolle. Du gibst ihm die Optionen und die Regeln, und er sucht sich das Beste für die aktuelle Situation aus. Das Ziel ist reine Performance-Optimierung.

#### Art Direction: Das Gestaltungs-Problem lösen

Jetzt wechseln wir das Szenario. Stell dir ein breites Bannerbild vor, das eine fünfköpfige Band auf einer großen Bühne zeigt. Auf einem Desktop-Bildschirm ist das ein tolles Panorama. Du siehst die Musiker, das Publikum, die Lichter – die ganze Atmosphäre.

Wenn du dieses Bild nun auf einem Smartphone-Display im Hochformat anzeigst, passiert eine Katastrophe. Das breite Panorama wird so stark verkleinert, dass die Musiker nur noch winzige Strichmännchen sind. Die emotionale Wirkung ist komplett verloren. Die Komposition funktioniert nicht mehr.

Hier hilft uns Resolution Switching nicht weiter, denn eine höher aufgelöste Version der winzigen Strichmännchen ist immer noch eine Version mit winzigen Strichmännchen.

Was wir brauchen, ist ein völlig anderes Bild. Ein Bild, das speziell für den schmalen Bildschirm gestaltet wurde. Vielleicht eine Nahaufnahme des Sängers oder ein Hochformat-Ausschnitt, der nur den Gitarristen und den Schlagzeuger zeigt.

Das ist **Art Direction** (künstlerische Leitung). Hier geht es nicht um die Auflösung, sondern um den Bildinhalt selbst. Du triffst eine bewusste gestalterische Entscheidung, auf bestimmten Bildschirmgrößen ein anderes Motiv zu zeigen, um die bestmögliche visuelle und emotionale Wirkung zu erzielen.

Die technische Umsetzung dafür ist das `<picture>`-Element. Es fungiert als Wrapper für verschiedene Bildquellen (`<source>`) und ein finales `<img>`-Fallback.

```html
<picture>
  <!-- Für Bildschirme, die schmaler als 600px sind -->
  <source media="(max-width: 599px)" srcset="band-portrait.jpg">
  
  <!-- Für Bildschirme, die 600px oder breiter sind -->
  <source media="(min-width: 600px)" srcset="band-panorama.jpg">
  
  <!-- Fallback für ältere Browser -->
  <img src="band-panorama.jpg" alt="Die Band 'The Pixels' live auf der Bühne.">
</picture>
```

So funktioniert das `<picture>`-Element:

1.  Der Browser liest die `<source>`-Elemente von oben nach unten.
2.  Er prüft bei jedem `<source>` die Bedingung im `media`-Attribut. Dieses Attribut enthält eine ganz normale Media Query, wie du sie aus CSS kennst.
3.  Das **erste** `<source>`-Element, dessen Media Query zutrifft, wird ausgewählt. Sein `srcset` wird verwendet, um das Bild zu laden. Alle weiteren `<source>`-Elemente werden ignoriert.
4.  Wenn keine der Media Queries zutrifft, oder wenn der Browser das `<picture>`-Element gar nicht kennt, wird das `<img>`-Element am Ende verwendet. Dieses ist obligatorisch und dient sowohl als Fallback als auch als das Element, das das Bild tatsächlich anzeigt (inklusive `alt`-Text).

**Die Kernaussage von Art Direction ist:** Du behältst die volle Kontrolle. Du schreibst dem Browser exakt vor, welches Bild er unter welcher Bedingung laden soll. Das Ziel ist die Optimierung der visuellen Kommunikation und des Designs.

#### Die Kernunterschiede auf einen Blick

| Kriterium | Resolution Switching | Art Direction |
| :--- | :--- | :--- |
| **Problem** | Ineffiziente Dateigrößen, langsame Ladezeiten. | Unpassende Bildkomposition, Verlust der visuellen Wirkung. |
| **Ziel** | Performance und Bandbreite sparen. | Design, User Experience und visuelle Botschaft optimieren. |
| **Bildinhalt** | Immer derselbe, nur in anderer Auflösung. | Unterschiedliche Motive, Ausschnitte oder Kompositionen. |
| **Kontrolle** | Der **Browser** entscheidet basierend auf den von dir gelieferten Daten. | **Du** entscheidest durch feste Regeln (Media Queries). |
| **HTML-Umsetzung** | `<img>` mit `srcset` und `sizes`. | `<picture>` mit `<source>`-Elementen und einem `<img>`-Fallback. |

#### Das Beste aus beiden Welten: Eine Kombination

Was, wenn du beides brauchst? Stell dir unser Band-Beispiel vor. Du hast dich entschieden, auf schmalen Bildschirmen das Porträt des Sängers zu zeigen (Art Direction). Aber auch dieses Porträt möchtest du für normale und hochauflösende Displays in unterschiedlichen Auflösungen anbieten (Resolution Switching).

Genau das ist möglich! Du kannst die beiden Techniken kombinieren. Das `<source>`-Element im `<picture>`-Tag kann nämlich ebenfalls ein `srcset`-Attribut mit mehreren `w`-Deskriptoren enthalten.

```html
<picture>
  <!-- Art Direction für schmale Bildschirme -->
  <source 
    media="(max-width: 599px)" 
    srcset="saenger-portrait-400w.jpg 400w, 
            saenger-portrait-800w.jpg 800w">
  
  <!-- Art Direction für breite Bildschirme -->
  <source 
    media="(min-width: 600px)" 
    srcset="band-panorama-1200w.jpg 1200w, 
            band-panorama-2400w.jpg 2400w">
  
  <!-- Fallback -->
  <img src="band-panorama-1200w.jpg" alt="Die Band 'The Pixels' live auf der Bühne.">
</picture>
```

In diesem Code passiert Folgendes:
*   Auf einem schmalen Bildschirm (unter 600px) wählt der Browser das erste `<source>`-Element. Nun hat er die Wahl zwischen `saenger-portrait-400w.jpg` und `saenger-portrait-800w.jpg` und kann je nach Pixeldichte die passende Version laden.
*   Auf einem breiten Bildschirm wird das zweite `<source>`-Element aktiv, und der Browser wählt je nach Bedarf zwischen den beiden Panorama-Versionen.

Hier nutzt du also zuerst Art Direction, um den fundamentalen Bildtyp zu bestimmen, und innerhalb dieser Entscheidung dann Resolution Switching, um die Performance weiter zu optimieren.

Beide Techniken sind keine Konkurrenten, sondern Partner. Resolution Switching ist dein Alltags-Werkzeug für fast jedes Bild auf deiner Webseite. Art Direction ist der Spezialist, den du für die gestalterisch wichtigen Bilder wie Header, Banner oder Teaser heranziehst, bei denen ein einfacher Skalierungsprozess nicht ausreicht. Deine Aufgabe ist es, für jedes Bild zu entscheiden, welches Werkzeug – oder welche Kombination – das richtige für den Job ist.
