# Bildformate (JPG, PNG, WebP, SVG)

# Die Welt der Bildformate: JPG, PNG, WebP und SVG im Detail

Wenn du eine Webseite erstellst, sind Bilder nicht nur Dekoration – sie sind entscheidender Inhalt. Sie transportieren Emotionen, erklären komplexe Sachverhalte und machen deine Seite lebendig. Doch ein Bild ist nicht gleich ein Bild. Die Wahl des richtigen Dateiformats ist eine der wichtigsten technischen Entscheidungen, die du für die Performance und die visuelle Qualität deiner Webseite treffen wirst. Jedes Format hat seine eigenen Stärken und Schwächen, und zu wissen, wann du welches einsetzt, ist ein entscheidender Schritt auf dem Weg zum Web-Profi.

Bevor wir uns die einzelnen Formate ansehen, müssen wir eine grundlegende Unterscheidung verstehen: den Unterschied zwischen Raster- und Vektorgrafiken.

*   **Rastergrafiken** (auch Bitmap-Grafiken genannt) bestehen aus einem festen Gitter von einzelnen Bildpunkten, den sogenannten Pixeln. Stell es dir wie ein Mosaik vor, bei dem jedes Steinchen eine bestimmte Farbe hat. Fotografien sind das klassische Beispiel für Rastergrafiken. Ihr großer Nachteil: Wenn du sie vergrößerst, werden die einzelnen Pixel sichtbar, und das Bild wirkt unscharf oder "pixelig". JPG, PNG und WebP sind Rasterformate.
*   **Vektorgrafiken** bestehen nicht aus Pixeln, sondern aus mathematischen Anweisungen. Sie beschreiben Formen, Linien und Kurven anhand von geometrischen Formeln. Stell es dir wie eine Bauanleitung vor: "Zeichne einen Kreis mit diesem Radius an dieser Position und fülle ihn mit dieser Farbe." Der große Vorteil: Vektorgrafiken sind unendlich und ohne Qualitätsverlust skalierbar. Egal, ob du sie auf einer Smartwatch oder einer riesigen Plakatwand anzeigst, sie bleiben immer gestochen scharf. SVG ist das dominierende Vektorformat im Web.

Mit diesem Wissen im Hinterkopf tauchen wir nun in die Details der gängigsten Formate ein.

### JPG (oder JPEG): Der Alleskönner für Fotos

Das Kürzel JPG steht für **Joint Photographic Experts Group**, die Gruppe, die diesen Standard entwickelt hat. JPG ist seit Jahrzehnten das Arbeitspferd des Internets, wenn es um die Darstellung von Fotos und komplexen, farbenreichen Bildern geht.

Sein entscheidendes Merkmal ist die **verlustbehaftete Komprimierung (lossy compression)**. Das klingt zunächst negativ, ist aber seine größte Stärke. Um die Dateigröße drastisch zu reduzieren, analysiert der JPG-Algorithmus das Bild und wirft Informationen weg, die für das menschliche Auge kaum oder gar nicht wahrnehmbar sind. Wenn du ein Foto als JPG speicherst, kannst du in der Regel einen Qualitätsregler (meist von 0 bis 100) einstellen. Ein Wert von 100 bedeutet minimale Komprimierung und hohe Qualität, während ein niedrigerer Wert zu einer kleineren Datei, aber auch zu sichtbaren Qualitätsverlusten, sogenannten "Kompressionsartefakten", führt.

**Wann solltest du JPG verwenden?**

*   **Fotografien:** Hier glänzt JPG. Die sanften Farbverläufe und die Detailvielfalt eines Fotos lassen sich hervorragend komprimieren, ohne dass die Qualität für den Betrachter leidet.
*   **Bilder mit vielen Farben und komplexen Verläufen:** Jedes Bild, das keine scharfen Kanten oder Textelemente hat, ist ein guter Kandidat für JPG.

**Wann solltest du JPG vermeiden?**

*   **Grafiken mit scharfen Kanten und Text:** Logos, Icons oder Diagramme werden im JPG-Format oft unscharf und bekommen unschöne "Schlieren" an den Kanten.
*   **Bilder, die Transparenz benötigen:** JPG unterstützt keine transparenten Hintergründe. Jeder Pixel im Bild hat eine Farbe, auch wenn er weiß ist.
*   **Bilder, die oft neu gespeichert werden müssen:** Jedes erneute Speichern eines JPGs führt zu einer weiteren Komprimierungsrunde und damit zu einem weiteren Qualitätsverlust.

### PNG: Der Champion für Transparenz und scharfe Kanten

PNG steht für **Portable Network Graphics** und wurde als modernerer und vielseitigerer Nachfolger des alten GIF-Formats entwickelt. Sein wichtigstes Merkmal ist die **verlustfreie Komprimierung (lossless compression)**.

Das bedeutet, dass beim Speichern eines PNGs keine Bildinformationen verloren gehen. Der Algorithmus reduziert die Dateigröße, indem er Muster in den Daten findet und sie effizienter speichert – ähnlich wie ein ZIP-Programm eine Textdatei komprimiert. Wenn du das Bild wieder öffnest, wird es exakt so wiederhergestellt, wie es ursprünglich war.

Die größte Stärke von PNG im Web ist seine exzellente Unterstützung für **Transparenz**. Im Gegensatz zu JPG kann PNG einen sogenannten Alpha-Kanal speichern. Dieser Kanal definiert für jeden Pixel nicht nur die Farbe, sondern auch seine Deckkraft (von 0 % bis 100 %). Das ermöglicht weiche, durchscheinende Ränder und komplexe Freisteller, die sich nahtlos in jeden Webseitenhintergrund einfügen.

Es gibt zwei Hauptvarianten:

*   **PNG-8:** Verwendet eine begrenzte Farbpalette von maximal 256 Farben und erzeugt sehr kleine Dateien. Ideal für einfache Logos oder Icons.
*   **PNG-24:** Unterstützt Millionen von Farben (True Color) und volle Alpha-Transparenz, was allerdings zu deutlich größeren Dateien führt als bei einem vergleichbaren JPG.

**Wann solltest du PNG verwenden?**

*   **Logos, Icons, Illustrationen:** Überall dort, wo du gestochen scharfe Linien und klare Farben benötigst.
*   **Bilder mit transparentem Hintergrund:** Wenn ein Teil deines Bildes durchsichtig sein soll, ist PNG die klassische Wahl.
*   **Screenshots von Benutzeroberflächen oder Diagramme:** Hier ist die exakte, pixelgenaue Darstellung von Text und Linien entscheidend.

**Wann solltest du PNG vermeiden?**

*   **Fotografien:** Ein Foto als PNG-24 zu speichern, führt zu einer riesigen Datei im Vergleich zu einem qualitativ gleichwertigen JPG. Das verlangsamt deine Webseite erheblich.

### WebP: Der moderne Herausforderer von Google

WebP ist ein relativ neues Bildformat, das von Google mit dem Ziel entwickelt wurde, das Web schneller zu machen. Es ist ein echtes Multitalent, denn es kombiniert die besten Eigenschaften von JPG und PNG und verbessert sie sogar.

WebP unterstützt:

*   **Verlustbehaftete Komprimierung:** Ähnlich wie JPG, aber die Algorithmen sind moderner. Bei gleicher visueller Qualität sind WebP-Dateien oft 25-35 % kleiner als ihre JPG-Pendants.
*   **Verlustfreie Komprimierung:** Ähnlich wie PNG, aber auch hier sind die Dateien im Schnitt rund 25 % kleiner.
*   **Transparenz (Alpha-Kanal):** WebP unterstützt Transparenz, und das sogar in Kombination mit verlustbehafteter Komprimierung – etwas, das weder JPG noch PNG kann.
*   **Animation:** WebP kann auch animierte Bilder erstellen und ist damit ein moderner Ersatz für animierte GIFs.

Früher war die Browser-Unterstützung ein Problem, aber heute wird WebP von allen modernen Browsern (Chrome, Firefox, Edge, Safari) unterstützt. Es ist also eine sichere und sehr empfehlenswerte Wahl für fast jeden Anwendungsfall.

Um die Kompatibilität mit sehr alten Browsern sicherzustellen, kannst du das `<picture>`-Element in HTML verwenden. Es erlaubt dir, mehrere Bildquellen anzugeben, aus denen der Browser die erste wählt, die er versteht.

```html
<picture>
  <!-- Der Browser versucht zuerst, das moderne WebP-Format zu laden. -->
  <source srcset="bild.webp" type="image/webp">
  
  <!-- Wenn er WebP nicht versteht, greift er auf dieses PNG als Fallback zurück. -->
  <source srcset="bild.png" type="image/png"> 
  
  <!-- Das ist das finale Fallback für alle Browser und für die Barrierefreiheit. -->
  <img src="bild.png" alt="Eine aussagekräftige Beschreibung des Bildes.">
</picture>
```

In diesem Beispiel versucht der Browser, die `bild.webp`-Datei zu laden. Nur wenn er das Format nicht kennt, springt er zur nächsten `source` und lädt `bild.png`.

### SVG: Die Magie der Vektoren

SVG steht für **Scalable Vector Graphics** und ist das einzige Vektorformat in dieser Liste. Wie anfangs erklärt, basiert es nicht auf Pixeln, sondern auf XML-Code, der Formen und Pfade beschreibt.

```xml
<svg width="100" height="100" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" stroke="black" stroke-width="3" fill="red" />
</svg>
```

Dieser Code beschreibt einen Kreis mit einem Mittelpunkt bei (50,50), einem Radius von 40, einem schwarzen Rand und einer roten Füllung. Du könntest diesen Code direkt in deine HTML-Datei einfügen, und der Browser würde den Kreis zeichnen.

Die Vorteile sind gewaltig:

*   **Unendliche Skalierbarkeit:** Ein SVG sieht auf jedem Display gestochen scharf aus, egal wie groß oder klein es dargestellt wird. Das ist perfekt für responsive Designs.
*   **Kleine Dateigrößen:** Für einfache bis mittelkomplexe Grafiken (Logos, Icons) sind SVGs oft winzig im Vergleich zu ihren Raster-Pendants.
*   **Manipulierbarkeit mit CSS und JavaScript:** Da SVGs Teil des DOM (Document Object Model) sind, kannst du sie mit CSS gestalten (z. B. die Füllfarbe bei einem `:hover`-Effekt ändern) oder mit JavaScript animieren.
*   **Barrierefreiheit:** Da es sich um Text handelt, können Screenreader den Inhalt eines SVGs lesen (wenn er entsprechend aufbereitet ist), und Suchmaschinen können ihn indizieren.

**Wann solltest du SVG verwenden?**

*   **Logos und Marken-Icons:** Das ist der ideale Anwendungsfall. Dein Logo muss auf allen Geräten perfekt aussehen.
*   **Benutzeroberflächen-Elemente:** Icons für Menüs, Buttons oder andere interaktive Elemente.
*   **Einfache Illustrationen und Infografiken:** Alles, was aus geometrischen Formen, Linien und Kurven aufgebaut ist.

**Wann solltest du SVG vermeiden?**

*   **Fotografien:** Der Versuch, ein Foto als Vektorgrafik darzustellen, ist technisch möglich, würde aber eine absurd komplexe Datei mit Millionen von Pfaden erzeugen, die um ein Vielfaches größer wäre als ein JPG und den Browser lahmlegen würde.

### Die strategische Entscheidung: Eine Faustregel

Die Wahl des richtigen Formats ist keine Frage des Geschmacks, sondern eine technische Abwägung zwischen Qualität, Funktionalität und Ladezeit.

*   Für **Fotos**: Beginne mit **WebP** (verlustbehaftet). Wenn du eine Fallback-Option benötigst, nimm **JPG**.
*   Für **Grafiken mit Transparenz oder scharfen Linien** (wie Logos oder Icons): Beginne mit **WebP** (verlustfrei). Als Fallback-Option wähle **PNG**.
*   Für **Logos, Icons und Illustrationen**, die auf jeder Bildschirmgröße perfekt aussehen und vielleicht sogar interaktiv sein sollen: Wähle immer **SVG**.

Indem du diese Regeln befolgst, stellst du sicher, dass deine Bilder immer großartig aussehen, ohne die Ladezeit deiner Webseite unnötig zu belasten – ein Gewinn für die Ästhetik und die Benutzererfahrung zugleich.
