# Fallbacks für ältere Browser

### Fallbacks für ältere Browser: Wenn die Zukunft auf die Vergangenheit trifft

Stell dir das Web als eine riesige, bunte Stadt vor. Es gibt hochmoderne Wolkenkratzer mit der neuesten Technologie, aber auch alte, charmante Backsteingebäude, die immer noch bewohnt und genutzt werden. Deine Website ist ein Besucher in dieser Stadt, und sie sollte in der Lage sein, mit beiden Architekturen zu interagieren. Ältere Browser sind wie diese Backsteingebäude: Sie haben nicht die neuesten Annehmlichkeiten, aber sie sind immer noch Teil des Ökosystems. Ein Fallback ist im Grunde der Plan B deiner Website – eine alternative Lösung, die greift, wenn eine moderne Funktion in einer älteren Umgebung nicht unterstützt wird.

Das Ziel ist nicht, dass deine Website in einem zehn Jahre alten Browser exakt genauso aussieht und funktioniert wie in der neuesten Chrome-Version. Das wäre ein Kampf gegen Windmühlen. Das Ziel ist, dass die Kernfunktionalität erhalten bleibt und der Inhalt zugänglich ist. Dieses Prinzip nennt man oft "Progressive Enhancement" (progressive Verbesserung): Du baust eine solide, funktionale Basis, die überall läuft, und fügst dann moderne Features als zusätzliche Schicht hinzu, die neuere Browser nutzen können.

#### HTML-Fallbacks: Das Fundament sichern

Schon auf der Ebene von HTML kannst du Vorkehrungen treffen. Viele neuere HTML-Elemente und -Attribute haben eingebaute Fallback-Mechanismen oder degradieren auf eine Weise, die meist unproblematisch ist ("graceful degradation").

##### Das `<picture>`-Element für responsive Bilder

Das `<picture>`-Element ist ein fantastisches Werkzeug, um je nach Bildschirmgröße oder Browser-Fähigkeiten unterschiedliche Bildquellen zu laden. Was aber passiert, wenn ein Browser dieses Element gar nicht kennt? Er ignoriert es einfach, ebenso wie die darin enthaltenen `<source>`-Tags. Deshalb ist es entscheidend, immer ein "normales" `<img>`-Element als letztes Kind innerhalb des `<picture>`-Elements zu platzieren. Dieses `<img>`-Element dient als universeller Fallback.

```html
<picture>
  <!-- Für moderne Browser, die das WebP-Format unterstützen -->
  <source srcset="bild-gross.webp" media="(min-width: 800px)">
  <source srcset="bild-klein.webp">
  
  <!-- Der Fallback für alle älteren Browser -->
  <img src="bild-gross.jpg" alt="Eine aussagekräftige Bildbeschreibung.">
</picture>
```

Ein alter Browser sieht nur das `<img>`-Tag und zeigt `bild-gross.jpg` an. Ein moderner Browser interpretiert das `<picture>`-Element und wählt die am besten passende Quelle aus. Der Inhalt bleibt für alle zugänglich.

##### Fallback-Inhalte für `<video>` und `<audio>`

Ähnlich verhält es sich mit den Medien-Elementen. Alles, was du zwischen die öffnenden und schließenden Tags von `<video>` oder `<audio>` schreibst, wird von Browsern ignoriert, die diese Elemente unterstützen. Ältere Browser, die damit nichts anfangen können, rendern jedoch genau diesen Inhalt. Das ist der perfekte Ort für einen Fallback.

```html
<video controls poster="vorschaubild.jpg">
  <source src="mein-film.mp4" type="video/mp4">
  <source src="mein-film.webm" type="video/webm">
  
  <!-- Fallback-Inhalt für ältere Browser -->
  <p>
    Dein Browser unterstützt das Video-Element leider nicht.
    Du kannst das Video aber <a href="mein-film.mp4">hier herunterladen</a>.
  </p>
</video>
```

So stellst du sicher, dass niemand vom Inhalt ausgeschlossen wird, nur weil sein Browser keine modernen HTML5-Medien abspielen kann.

##### Semantische Input-Typen

HTML5 hat viele nützliche `type`-Attribute für `<input>`-Elemente eingeführt, wie `date`, `color`, `range` oder `email`. Ältere Browser, die diese spezifischen Typen nicht kennen, machen etwas sehr Praktisches: Sie fallen auf `type="text"` zurück.

```html
<form>
  <label for="geburtsdatum">Geburtsdatum:</label>
  <input type="date" id="geburtsdatum" name="geburtsdatum">
</form>
```

In einem modernen Browser erscheint ein schicker Datumswähler. In einem älteren Browser wird ein einfaches Textfeld angezeigt. Der Nutzer kann das Datum immer noch von Hand eingeben. Die Funktionalität ist nicht perfekt, aber die grundlegende Dateneingabe ist weiterhin möglich, ohne dass die Seite kaputtgeht.

#### CSS-Fallbacks: Die Kunst der Kaskade nutzen

Im CSS ist das Fallback-Prinzip tief in seiner Funktionsweise verankert: der Kaskade. Eine grundlegende Regel des CSS besagt: Wenn ein Browser eine Eigenschaft oder einen Wert nicht versteht, ignoriert er die gesamte Deklaration und geht zur nächsten über. Das können wir uns zunutze machen.

##### Einfache Eigenschafts-Fallbacks

Der einfachste CSS-Fallback besteht darin, eine allgemein unterstützte Eigenschaft vor einer neueren, spezifischeren Eigenschaft zu deklarieren.

```css
.box {
  /* Fallback für Browser, die keine Farbverläufe kennen */
  background-color: #337ab7; 
  
  /* Moderne Deklaration, die den Fallback überschreibt, wenn sie verstanden wird */
  background-image: linear-gradient(to bottom, #5691c8, #337ab7);
}
```

Ein älterer Browser liest `background-color: #337ab7;` und wendet es an. Die nächste Zeile mit `linear-gradient` versteht er nicht, also ignoriert er sie. Das Ergebnis ist eine Box mit einer soliden blauen Farbe. Ein moderner Browser liest ebenfalls zuerst die `background-color`, aber direkt danach liest er die `background-image`-Deklaration, versteht sie und überschreibt damit die vorherige Hintergrundfarbe. Das Ergebnis ist eine Box mit einem schönen Farbverlauf.

##### Feature Queries mit `@supports`

Manchmal reicht das einfache Überschreiben nicht aus, besonders bei komplexen Layout-Techniken wie CSS Grid oder Flexbox. Hier kommen "Feature Queries" ins Spiel. Mit der `@supports`-Regel kannst du den Browser direkt fragen, ob er eine bestimmte CSS-Eigenschaft-Wert-Kombination unterstützt.

Stell dir vor, du möchtest ein Grid-Layout verwenden, aber auch einen Fallback für Browser bereitstellen, die CSS Grid nicht kennen. Dein Fallback könnte ein älteres, aber weit verbreitetes System wie Floats sein.

```css
.container {
  /* Fallback-Layout mit Floats für ältere Browser */
  overflow: hidden; /* Clearfix für Floats */
}

.container > .item {
  float: left;
  width: 30%;
  margin-right: 5%;
}

.container > .item:last-child {
  margin-right: 0;
}

/* Jetzt kommt die Magie: Das moderne Layout für unterstützende Browser */
@supports (display: grid) {
  .container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 20px;
    overflow: visible; /* Float-Clearfix zurücksetzen */
  }

  /* Die Float-Eigenschaften der Items zurücksetzen */
  .container > .item {
    float: none;
    width: auto;
    margin-right: 0;
  }
}
```

Hier definierst du zuerst das komplette Float-basierte Layout. Es funktioniert überall dort, wo Grid nicht unterstützt wird. Danach prüft der `@supports`-Block, ob `display: grid` verfügbar ist. Wenn ja, werden die Regeln innerhalb des Blocks angewendet. Diese überschreiben die Float-Regeln und etablieren das Grid-Layout. So erhältst du das Beste aus beiden Welten: ein funktionierendes Layout für alle und ein modernes, besseres Layout für die Mehrheit.

#### JavaScript-Fallbacks: Fehlende Funktionen nachrüsten

Bei JavaScript wird es etwas komplexer, da eine fehlende Funktion oft zu einem Script-Abbruch und damit zu einer kaputten Seite führt. Der häufigste Ansatz hierfür sind sogenannte "Polyfills".

Ein Polyfill ist ein Stück Code, das eine moderne Funktionalität, die dem Browser fehlt, in JavaScript nachbildet. Du prüfst, ob eine bestimmte Methode oder ein Objekt existiert, und wenn nicht, definierst du es selbst.

Nehmen wir als Beispiel die Methode `String.prototype.startsWith()`, die prüft, ob ein String mit einer bestimmten Zeichenkette beginnt. Diese wurde erst in ECMAScript 2015 (ES6) eingeführt und fehlt in älteren Browsern wie dem Internet Explorer.

```javascript
// Ein einfacher Polyfill für startsWith

// Zuerst prüfen, ob die Funktion bereits existiert
if (!String.prototype.startsWith) {
  // Wenn nicht, definieren wir sie selbst
  String.prototype.startsWith = function(searchString, position) {
    position = position || 0;
    return this.substr(position, searchString.length) === searchString;
  };
}

// Jetzt können wir den Code sicher verwenden
const text = "Hallo Welt";
if (text.startsWith("Hallo")) {
  console.log("Der Text beginnt mit 'Hallo'.");
}
```

Du musst diese Polyfills nicht alle selbst schreiben. Es gibt Bibliotheken und Dienste (wie `core-js` oder `polyfill.io`), die diese Aufgabe für dich übernehmen. Werkzeuge wie Babel können deinen modernen JavaScript-Code automatisch in eine ältere, kompatiblere Version umwandeln (Transpilation) und dabei die notwendigen Polyfills einbinden.

Der Kerngedanke bleibt derselbe: Stelle sicher, dass dein Code nicht ins Leere läuft. Prüfe auf die Existenz von Features, bevor du sie nutzt, und biete eine Alternative an, wenn sie nicht vorhanden sind. Diese Alternative kann ein Polyfill sein, der die Funktion nachbaut, oder eine einfachere Implementierung, die die Kernaufgabe erfüllt, ohne auf die moderne API angewiesen zu sein.
