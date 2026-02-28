# Richtige Formate und Kompression

### Richtige Formate und Kompression

Bilder sind oft die schwersten Komponenten einer Webseite. Sie können die Ladezeit dramatisch beeinflussen und damit direkt über das Nutzererlebnis entscheiden. Eine langsam ladende Seite frustriert Besucher und kann dazu führen, dass sie deine Seite verlassen, bevor sie überhaupt den Inhalt gesehen haben. Deshalb ist es unerlässlich, dass du dich intensiv mit der Optimierung deiner Bilder beschäftigst. Der erste und wichtigste Schritt dabei ist die Wahl des richtigen Dateiformats und der passenden Kompressionsstrategie.

#### Raster- vs. Vektorgrafiken: Ein fundamentaler Unterschied

Bevor wir in die Details der einzelnen Formate eintauchen, musst du den grundlegenden Unterschied zwischen zwei Arten von Grafiken verstehen: Raster- und Vektorgrafiken.

**Rastergrafiken** bestehen aus einem Gitter von einzelnen Bildpunkten, den sogenannten Pixeln. Jedes Pixel hat eine definierte Farbe. Fotografien sind das klassische Beispiel für Rastergrafiken. Formate wie JPEG, PNG, GIF, WebP und AVIF gehören in diese Kategorie. Ihre große Stärke liegt in der Darstellung komplexer Farbübergänge und Details, wie sie in Fotos vorkommen. Ihr Nachteil: Sie sind auflösungsabhängig. Wenn du ein Rasterbild stark vergrößerst, werden die einzelnen Pixel sichtbar, und das Bild wirkt „pixelig“ oder unscharf. Die Dateigröße wächst zudem mit der Anzahl der Pixel (also der Auflösung).

**Vektorgrafiken**, deren bekanntestes Web-Format SVG (Scalable Vector Graphics) ist, funktionieren komplett anders. Sie basieren nicht auf Pixeln, sondern auf mathematischen Formeln, die Formen, Linien und Kurven beschreiben. Ein Kreis wird beispielsweise durch seinen Mittelpunkt, seinen Radius und seine Farbe definiert. Der große Vorteil: Vektorgrafiken sind auflösungsunabhängig. Du kannst sie ohne Qualitätsverlust beliebig vergrößern oder verkleinern. Sie eignen sich perfekt für Logos, Icons, Diagramme und Illustrationen mit klaren Linien und flächigen Farben. Oftmals sind ihre Dateigrößen dabei erstaunlich klein. Für komplexe, fotorealistische Darstellungen sind sie jedoch ungeeignet.

Die erste Entscheidung, die du also triffst, ist: Handelt es sich bei meiner Grafik um ein Foto oder eine komplexe Illustration (dann wähle ein Rasterformat) oder um ein Logo, ein Icon oder eine einfache Grafik (dann ist SVG fast immer die bessere Wahl)? Da sich dieses Kapitel auf die Optimierung von komplexeren Bildern konzentriert, fokussieren wir uns im Folgenden auf die Rasterformate.

#### Die Kompression: Verlustfrei vs. Verlustbehaftet

Die Dateigröße von Rasterbildern wird durch Kompression reduziert. Hier gibt es zwei grundlegend verschiedene Ansätze:

**Verlustfreie Kompression (Lossless):**
Stell dir vor, du packst eine Textdatei in ein ZIP-Archiv. Die Datei wird kleiner, aber wenn du sie wieder entpackst, ist der Inhalt exakt derselbe wie zuvor – kein einziges Zeichen geht verloren. Genau so funktioniert die verlustfreie Kompression bei Bildern. Algorithmen finden Muster und wiederkehrende Informationen im Bild und speichern diese effizienter ab, ohne die Bildqualität zu beeinträchtigen. Das Originalbild kann zu 100 % wiederhergestellt werden. PNG ist ein klassisches Format, das verlustfrei komprimiert.

**Verlustbehaftete Kompression (Lossy):**
Bei diesem Ansatz werden Bildinformationen, die für das menschliche Auge als weniger wichtig erachtet werden, gezielt und unwiderruflich entfernt. Der Algorithmus analysiert das Bild und verwirft feine Details oder Farbnuancen, deren Fehlen kaum auffällt. Stell es dir wie eine sehr gute Zusammenfassung eines Buches vor: Du verstehst die komplette Geschichte, aber einige beschreibende Adjektive oder Nebensätze fehlen. Der Vorteil ist eine drastische Reduzierung der Dateigröße, die mit verlustfreier Kompression nicht erreichbar wäre. Der Nachteil: Die entfernten Daten sind für immer verloren. Wenn du die Kompression zu stark einstellst, leidet die Bildqualität sichtbar, und es entstehen unschöne Artefakte (z. B. blockartige Muster oder unscharfe Kanten). JPEG ist das prominenteste Beispiel für ein verlustbehaftetes Format.

Die Kunst besteht darin, den perfekten Kompromiss zwischen Dateigröße und sichtbarer Qualität zu finden.

#### Die klassischen Bildformate im Überblick

**JPEG (Joint Photographic Experts Group)**
*   **Kompression:** Verlustbehaftet.
*   **Ideal für:** Fotografien und Bilder mit vielen Farben und komplexen Verläufen.
*   **Besonderheiten:** JPEG unterstützt keine Transparenz. Du kannst die Kompressionsstärke über einen Qualitätsregler (meist von 0 bis 100) sehr fein einstellen. Ein Wert zwischen 75 und 85 ist oft ein guter Ausgangspunkt für das Web. Eine Variante ist das „Progressive JPEG“, das beim Laden erst eine unscharfe Vorschau anzeigt, die dann schrittweise schärfer wird. Dies verbessert die wahrgenommene Ladezeit.

**PNG (Portable Network Graphics)**
*   **Kompression:** Verlustfrei.
*   **Ideal für:** Grafiken mit scharfen Kanten, Text, Logos und Bilder, die Transparenz benötigen (z. B. ein freigestelltes Produkt).
*   **Besonderheiten:** Die große Stärke von PNG ist der Alpha-Kanal, der eine feinstufige Transparenz (von komplett durchsichtig bis komplett undurchsichtig) ermöglicht. PNG gibt es in zwei Hauptvarianten: PNG-8 (mit einer begrenzten Palette von 256 Farben, ähnlich wie GIF) und PNG-24 (das Millionen von Farben unterstützt). Für Fotos ist PNG aufgrund der verlustfreien Kompression meist ungeeignet, da die Dateien im Vergleich zu einem gut komprimierten JPEG riesig werden.

**GIF (Graphics Interchange Format)**
*   **Kompression:** Verlustfrei (aber mit stark reduzierter Farbpalette).
*   **Ideal für:** Sehr einfache, kurze Animationen.
*   **Besonderheiten:** GIF unterstützt nur maximal 256 Farben, was es für Fotos völlig unbrauchbar macht. Es unterstützt zudem nur eine binäre Transparenz (ein Pixel ist entweder voll sichtbar oder voll transparent, keine weichen Übergänge). Seine einzige verbleibende Daseinsberechtigung im modernen Web sind simple Animationen, obwohl es dafür heute oft bessere Alternativen wie animierte WebPs oder Videoformate gibt.

#### Moderne Formate: WebP und AVIF

Die Entwicklung bleibt nicht stehen. Um den ständig steigenden Anforderungen an Performance gerecht zu werden, wurden modernere Formate entwickelt, die die besten Eigenschaften der Klassiker vereinen und übertreffen.

**WebP**
*   **Entwickler:** Google.
*   **Kompression:** Unterstützt sowohl verlustbehaftete als auch verlustfreie Kompression sowie Transparenz und Animationen.
*   **Vorteile:** WebP ist ein wahres Multitalent. In seiner verlustbehafteten Form erzeugt es bei gleicher visueller Qualität deutlich kleinere Dateien als JPEG (ca. 25-35 % kleiner). In seiner verlustfreien Form ist es effizienter als PNG und unterstützt ebenfalls Transparenz. Der Browser-Support ist mittlerweile exzellent.

**AVIF (AV1 Image File Format)**
*   **Entwickler:** Alliance for Open Media (ein Konsortium aus Firmen wie Google, Apple, Mozilla, Microsoft).
*   **Kompression:** Basiert auf dem modernen AV1-Video-Codec und bietet eine nochmals überlegene verlustbehaftete und verlustfreie Kompression.
*   **Vorteile:** AVIF kann bei vergleichbarer Qualität noch kleinere Dateigrößen als WebP erreichen (oftmals bis zu 50 % kleiner als ein JPEG). Es unterstützt ebenfalls Transparenz und weitere moderne Features. Der Browser-Support wächst rasant und ist in allen modernen Browsern bereits gegeben.

#### Die richtige Strategie in der Praxis mit dem `<picture>`-Element

Du fragst dich jetzt vielleicht: "Soll ich also alles in AVIF speichern?" Die Antwort ist: "Ja, aber mit einem Plan B." Nicht jeder Nutzer hat den allerneuesten Browser. Damit deine Bilder überall sichtbar sind, musst du eine Fallback-Lösung bereitstellen. Genau hierfür wurde das HTML-Element `<picture>` geschaffen.

Mit dem `<picture>`-Element kannst du dem Browser mehrere Bildquellen in verschiedenen Formaten anbieten. Der Browser wählt dann selbstständig das erste Format aus der Liste aus, das er versteht und darstellen kann. Das ist ein perfektes Beispiel für *Progressive Enhancement*: Moderne Browser bekommen das beste und kleinste Format (AVIF), ältere Browser bekommen eine gut funktionierende Alternative (WebP oder JPEG).

So sieht eine robuste Implementierung aus:

```html
<picture>
  <!-- Biete zuerst das modernste und effizienteste Format an: AVIF -->
  <source srcset="blumen.avif" type="image/avif">
  
  <!-- Als nächstes das sehr gut unterstützte und effiziente WebP -->
  <source srcset="blumen.webp" type="image/webp">
  
  <!-- Das <img>-Element ist der universelle Fallback für alle anderen Browser -->
  <!-- Es ist zwingend erforderlich und wird auch für die eigentliche Bilddarstellung genutzt -->
  <img src="blumen.jpg" alt="Ein Strauß bunter Tulpen in einer Vase." width="800" height="600">
</picture>
```

Die Reihenfolge innerhalb des `<picture>`-Elements ist entscheidend. Der Browser prüft die `<source>`-Tags von oben nach unten. Sobald er ein `type`-Attribut findet, das er unterstützt, lädt er das in `srcset` angegebene Bild und ignoriert alle folgenden `<source>`-Tags. Das `<img>`-Element am Ende ist nicht nur der Fallback für Browser, die `<picture>` gar nicht kennen, sondern es ist auch das Element, das letztendlich das Bild rendert und Attribute wie `alt`, `width` und `height` trägt.

Deine Strategie zur Bildoptimierung sollte also immer so aussehen:
1.  **Analysiere die Grafik:** Ist es eine Vektorgrafik (Logo, Icon)? Dann nutze SVG.
2.  **Wenn es eine Rastergrafik ist:** Erstelle Versionen in mehreren Formaten. Eine gute Kette ist AVIF -> WebP -> JPEG (für Fotos) oder PNG (für Grafiken mit Transparenz).
3.  **Implementiere mit `<picture>`:** Binde die Bilder mit dem `<picture>`-Element ein, um jedem Browser das bestmögliche Format anzubieten.

Die Wahl des richtigen Formats und die intelligente Nutzung moderner HTML-Elemente sind keine Nebensächlichkeiten. Sie sind das Fundament einer performanten Webseite und ein Zeichen von professioneller, nutzerzentrierter Entwicklung.
