# Das picture-Element

### Das `<picture>`-Element: Die Kunst der Bildauswahl

Stell dir vor, du hast ein fantastisches, breites Landschaftsfoto für deine Webseite. Auf einem großen Desktop-Monitor sieht es umwerfend aus. Auf einem Smartphone im Hochformat wird es jedoch zu einem winzigen, unkenntlichen Streifen, bei dem alle wichtigen Details verloren gehen. Wäre es nicht großartig, wenn du dem Browser sagen könntest: „Hey, auf großen Bildschirmen nimm bitte dieses breite Bild, aber auf kleinen, schmalen Geräten zeige stattdessen diese speziell zugeschnittene Hochformat-Version an“? Genau hier kommt das `<picture>`-Element ins Spiel.

Während das `<img>`-Element mit den Attributen `srcset` und `sizes` bereits eine brillante Lösung für das Anbieten desselben Bildes in verschiedenen Auflösungen bietet (Resolution Switching), geht das `<picture>`-Element einen entscheidenden Schritt weiter. Es erlaubt dir, dem Browser komplett unterschiedliche Bildquellen unter bestimmten Bedingungen anzubieten. Diesen Anwendungsfall nennt man „Art Direction“ – du übernimmst also die künstlerische Regie darüber, welches Bild wann angezeigt wird.

#### Die Anatomie des `<picture>`-Elements

Das `<picture>`-Element an sich ist unsichtbar. Es funktioniert wie ein Container oder ein Rahmen, der dem Browser eine Auswahl an Bildquellen zur Verfügung stellt. Die eigentliche Arbeit erledigen die Kind-Elemente: eines oder mehrere `<source>`-Elemente und genau ein `<img>`-Element.

Ein typischer Aufbau sieht so aus:

```html
<picture>
  <source media="(min-width: 992px)" srcset="bild-gross.jpg">
  <source media="(min-width: 600px)" srcset="bild-mittel.jpg">
  <img src="bild-klein.jpg" alt="Eine aussagekräftige Beschreibung des Bildes.">
</picture>
```

Lass uns das Stück für Stück aufschlüsseln:

1.  **`<picture>`:** Das umschließende Element. Es signalisiert dem Browser, dass eine Auswahl an Bildern folgt.
2.  **`<source>`:** Jedes `<source>`-Element definiert eine alternative Bildquelle. Es ist ein leeres Element, genau wie `<img>`. Die entscheidenden Attribute sind hier `media` und `srcset`.
    *   Das `media`-Attribut enthält eine Media Query, genau wie du sie aus CSS kennst. Der Browser prüft diese Bedingung. Wenn sie zutrifft, wird die in `srcset` angegebene Bildquelle ausgewählt.
    *   Das `srcset`-Attribut gibt den Pfad zum Bild an.
3.  **`<img>`:** Dieses Element ist **zwingend erforderlich** und muss immer das letzte Kind-Element innerhalb von `<picture>` sein. Es erfüllt zwei entscheidende Funktionen:
    *   **Fallback:** Wenn keine der Bedingungen der `<source>`-Elemente zutrifft oder der Browser das `<picture>`-Element gar nicht unterstützt, wird das im `src`-Attribut des `<img>`-Elements angegebene Bild angezeigt. Das sorgt für maximale Kompatibilität.
    *   **Beschreibung und Darstellung:** Das `<img>`-Element ist das, was letztendlich auf der Seite gerendert wird. Es trägt daher auch das `alt`-Attribut für die Barrierefreiheit sowie alle anderen Attribute, die du auf einem Bild anwenden möchtest (wie `class`, `id`, `loading`, `decoding` usw.). Der `alt`-Text gilt für das gesamte `<picture>`-Konstrukt, egal welche Quelle am Ende ausgewählt wird.

Der Browser arbeitet die `<source>`-Elemente von oben nach unten ab. Das erste `<source>`-Element, dessen `media`-Bedingung erfüllt ist, gewinnt. Sein `srcset`-Wert wird für das `<img>`-Element übernommen, und alle weiteren `<source>`-Elemente werden ignoriert.

#### Anwendungsfall 1: Art Direction

Der klassische Anwendungsfall ist die bereits erwähnte „künstlerische Regie“. Du möchtest sicherstellen, dass dein Bild auf jedem Gerät optimal zur Geltung kommt.

Nehmen wir unser Beispiel mit dem Landschaftsfoto. Für große Bildschirme haben wir ein breites Panorama, das die Weite der Landschaft zeigt. Für mobile Geräte haben wir eine zugeschnittene Version, die sich auf ein zentrales Motiv konzentriert, zum Beispiel einen markanten Berg.

```html
<picture>
  <!-- Für Bildschirme, die 800px oder breiter sind -->
  <source media="(min-width: 800px)" srcset="landschaft-panorama.jpg">
  
  <!-- Für alle anderen (kleineren) Bildschirme -->
  <img src="landschaft-detail-hochkant.jpg" alt="Eine weite Berglandschaft mit einem See im Vordergrund.">
</picture>
```

**Was passiert hier?**

*   Ein Nutzer mit einem Desktop-Computer, dessen Browserfenster 1200 Pixel breit ist, erfüllt die Bedingung `(min-width: 800px)`. Der Browser lädt und zeigt `landschaft-panorama.jpg`.
*   Ein Nutzer auf einem Smartphone mit einer Breite von 400 Pixeln erfüllt die Bedingung nicht. Der Browser überspringt das `<source>`-Element und greift auf das `<img>`-Element zurück. Er lädt und zeigt `landschaft-detail-hochkant.jpg`.

Damit hast du nicht nur für eine bessere visuelle Darstellung gesorgt, sondern auch die Performance verbessert. Das zugeschnittene Hochformat-Bild ist wahrscheinlich deutlich kleiner in der Dateigröße als das riesige Panorama, was auf mobilen Geräten mit oft langsameren Verbindungen einen großen Unterschied macht.

#### Anwendungsfall 2: Moderne Bildformate anbieten

Ein weiterer extrem nützlicher Anwendungsfall ist das Anbieten moderner Bildformate wie WebP oder AVIF. Diese Formate bieten eine exzellente Kompression bei hoher Qualität, werden aber nicht von allen, insbesondere älteren Browsern, unterstützt. Mit `<picture>` kannst du dem Browser eine Auswahl an Formaten servieren und er sucht sich das beste aus, das er versteht.

Hierfür verwenden wir das `type`-Attribut im `<source>`-Element.

```html
<picture>
  <!-- Biete zuerst das modernste Format AVIF an -->
  <source srcset="blume.avif" type="image/avif">
  
  <!-- Wenn der Browser AVIF nicht kann, biete WebP an -->
  <source srcset="blume.webp" type="image/webp">
  
  <!-- Als Fallback das universell unterstützte JPEG -->
  <img src="blume.jpg" alt="Nahaufnahme einer roten Mohnblume.">
</picture>
```

**Die Logik dahinter:**

Der Browser liest wieder von oben nach unten.
1.  Er prüft das erste `<source>`-Element. Er fragt sich: „Kann ich Bilder vom Typ `image/avif` darstellen?“ Wenn ja, lädt er `blume.avif` und ist fertig.
2.  Wenn nein, geht er zum nächsten `<source>`-Element. Er fragt: „Okay, wie sieht es mit `image/webp` aus?“ Wenn ja, lädt er `blume.webp` und ist fertig.
3.  Wenn er auch WebP nicht unterstützt, ignoriert er auch dieses `<source>`-Element und greift auf das `<img>`-Fallback zurück. Er lädt das sichere `blume.jpg`, das praktisch jeder Browser seit Jahrzehnten versteht.

Mit dieser Methode stellst du sicher, dass deine Nutzer von der bestmöglichen Performance profitieren, ohne dass Nutzer mit älterer Software ausgeschlossen werden.

#### Alles kombiniert: Die wahre Stärke von `<picture>`

Jetzt wird es richtig spannend. Du kannst Art Direction und die Auswahl von Bildformaten miteinander kombinieren, um die ultimative Kontrolle über deine Bilder zu erlangen.

Stellen wir uns vor, wir wollen unser Landschaftsbild nicht nur zuschneiden, sondern auch in modernen Formaten ausliefern.

```html
<picture>
  <!-- Breite Ansicht für große Bildschirme -->
  <source media="(min-width: 800px)" srcset="landschaft-panorama.avif" type="image/avif">
  <source media="(min-width: 800px)" srcset="landschaft-panorama.webp" type="image/webp">
  <source media="(min-width: 800px)" srcset="landschaft-panorama.jpg" type="image/jpeg">
  
  <!-- Schmale Ansicht für kleinere Bildschirme -->
  <source srcset="landschaft-detail-hochkant.avif" type="image/avif">
  <source srcset="landschaft-detail-hochkant.webp" type="image/webp">
  
  <!-- Universeller Fallback -->
  <img src="landschaft-detail-hochkant.jpg" alt="Eine weite Berglandschaft mit einem See im Vordergrund.">
</picture>
```

Hier ist die Reihenfolge entscheidend. Der Browser prüft zuerst die Media Query. Ist der Bildschirm breiter als 800 Pixel?
*   **Ja:** Er bleibt bei den ersten drei `<source>`-Elementen. Nun prüft er den `type`: Kann er AVIF? Ja? Super, `landschaft-panorama.avif` wird geladen. Nein? Kann er WebP? Ja? `landschaft-panorama.webp` wird geladen. Nein? Dann muss es `landschaft-panorama.jpg` sein.
*   **Nein:** Der Bildschirm ist schmaler. Der Browser überspringt die ersten drei `<source>`-Elemente, da deren `media`-Bedingung nicht zutrifft. Er geht zu den nächsten `<source>`-Elementen. Kann er AVIF? Ja? `landschaft-detail-hochkant.avif` wird geladen. Nein? Kann er WebP? Ja? `landschaft-detail-hochkant.webp` wird geladen. Wenn auch das fehlschlägt, bleibt nur noch das Fallback-`<img>` mit `landschaft-detail-hochkant.jpg`.

Du siehst, das `<picture>`-Element gibt dir ein unglaublich mächtiges Werkzeug an die Hand. Es ermöglicht dir, die Bildauslieferung auf deiner Webseite präzise zu steuern, die User Experience auf verschiedenen Geräten drastisch zu verbessern und gleichzeitig die Ladezeiten durch den Einsatz moderner, effizienter Formate zu optimieren. Es ist die Verkörperung des responsiven Webdesigns, angewandt auf das wichtigste visuelle Medium im Web: das Bild.
