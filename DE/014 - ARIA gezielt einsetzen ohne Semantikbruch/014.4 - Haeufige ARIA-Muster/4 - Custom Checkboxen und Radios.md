# Custom Checkboxen und Radios

# Custom Checkboxen und Radios

In der Welt des Webdesigns stoßen wir oft an einen Punkt, an dem die Standard-Steuerelemente der Browser einfach nicht zum gewünschten Erscheinungsbild passen. Checkboxen und Radio-Buttons sind hierfür Paradebeispiele. Ihr Aussehen variiert stark zwischen verschiedenen Browsern und Betriebssystemen, und die Möglichkeiten, sie direkt mit CSS zu gestalten, sind extrem begrenzt. Der Wunsch nach einem einheitlichen, markengerechten Design führt uns unweigerlich dazu, eigene, benutzerdefinierte Versionen dieser Elemente zu erstellen.

Doch dieser Weg ist mit Fallstricken gepflastert, insbesondere was die Zugänglichkeit (Accessibility) betrifft. Eine unsichtbare Checkbox ist für einen sehenden Benutzer vielleicht kein Problem, für jemanden, der auf einen Screenreader oder Tastaturnavigation angewiesen ist, kann sie jedoch eine unüberwindbare Hürde darstellen. Die gute Nachricht ist: Mit der richtigen Technik kannst du beides haben – ein ansprechendes Design und eine einwandfreie, semantisch korrekte Funktionalität, ohne dich in komplexen ARIA-Attributen zu verlieren.

### Der Kern des Problems: Styling von `<input>`

Der Grund, warum wir überhaupt über alternative Techniken nachdenken müssen, liegt in der Natur der Formularelemente. Browser rendern `<input type="checkbox">` und `<input type="radio">` oft mithilfe von nativen Steuerelementen des Betriebssystems. Das macht sie schnell und vertraut für die Benutzer, aber zu einer Blackbox für uns Entwickler. Eigenschaften wie `background-color` oder `border` werden oft ignoriert oder nur teilweise angewendet. Ein Häkchen oder einen Punkt durch ein eigenes Icon zu ersetzen, ist auf direktem Wege schlicht nicht möglich.

Die naheliegende Idee, das Original-Input-Element einfach zu verstecken und ein `<span>` oder `<div>` an seiner Stelle zu stylen, ist der richtige Ansatz. Die Umsetzung entscheidet jedoch darüber, ob wir eine elegante Lösung oder eine unzugängliche Barriere schaffen.

### Der richtige Aufbau: Semantik als Fundament

Der Schlüssel zu zugänglichen Custom Controls liegt darin, das native `<input>`-Element nicht komplett zu entfernen, sondern es lediglich visuell zu verbergen. Es bleibt weiterhin im Dokument, kann fokussiert, angeklickt und von assistiven Technologien wie Screenreadern erkannt werden. Es dient als die "Wahrheitsquelle" für den Zustand (aktiviert oder nicht aktiviert).

Unsere HTML-Struktur kombiniert das Beste aus beiden Welten: die robuste Funktionalität des nativen Inputs und die gestalterische Freiheit eines zusätzlichen Elements.

```html
<label class="custom-checkbox">
  <input type="checkbox" class="visually-hidden">
  <span class="checkbox-visual" aria-hidden="true"></span>
  <span class="checkbox-label">Newsletter abonnieren</span>
</label>
```

Schauen wir uns diese Struktur genauer an:

1.  **`<label>` als Container:** Das gesamte Konstrukt wird von einem `<label>`-Element umschlossen. Dies hat zwei entscheidende Vorteile. Erstens ist es semantisch korrekt. Zweitens vergrößert es die Klickfläche: Ein Klick auf den Text oder unser neues visuelles Element aktiviert automatisch das zugehörige Input, ohne dass wir dafür JavaScript benötigen.
2.  **`<input type="checkbox">`:** Das ist unser Original-Element. Es behält die volle Kontrolle über die Logik. Wir geben ihm eine spezielle Klasse, um es visuell zu verbergen.
3.  **`<span class="checkbox-visual">`:** Dieses `<span>` wird unsere gestylte Checkbox. Es ist das Element, dem wir mit CSS die gewünschte Form, Farbe und den Zustand (Häkchen) geben. Das Attribut `aria-hidden="true"` ist hier eine gute Praxis, da die Semantik bereits vom (unsichtbaren) Input-Element an Screenreader übermittelt wird. Das visuelle Element ist rein dekorativ und würde für einen Screenreader-Nutzer nur eine redundante Information darstellen.
4.  **`<span class="checkbox-label">`:** Der sichtbare Text der Beschriftung.

### Die Kunst des Verbergens

Wie verstecken wir das Input-Element, ohne es aus dem Accessibility-Tree zu entfernen? Die häufig genutzte Eigenschaft `display: none;` oder `visibility: hidden;` ist hierfür die falsche Wahl. Beide entfernen das Element komplett, sodass es weder per Tastatur fokussiert noch von Screenreadern wahrgenommen werden kann.

Stattdessen verwenden wir eine bewährte CSS-Technik, die das Element aus dem sichtbaren Bereich verschiebt, es aber für Browser und assistive Technologien intakt lässt.

```css
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
```

Diese Klasse kannst du für jedes Element verwenden, das nur für Screenreader, aber nicht visuell präsent sein soll.

### Styling mit der Macht der Pseudo-Klassen

Jetzt kommt der magische Teil. Wir nutzen CSS, um unser `.checkbox-visual`-Element basierend auf dem Zustand des *unsichtbaren* Inputs zu verändern. Die Pseudo-Klasse `:checked` und der Geschwister-Selektor (`+` oder `~`) sind hier unsere besten Freunde.

Beginnen wir mit dem Grund-Styling für unsere visuelle Checkbox.

```css
.checkbox-visual {
  display: inline-block;
  width: 1.2em;
  height: 1.2em;
  margin-right: 0.5em;
  border: 2px solid #555;
  border-radius: 3px;
  transition: background-color 0.2s, border-color 0.2s;
  vertical-align: middle; /* Sorgt für eine saubere Ausrichtung zum Text */
}
```

Nun definieren wir, was passiert, wenn die originale Checkbox aktiviert wird. Da unser `.checkbox-visual` direkt auf das `<input>` im HTML-Code folgt, können wir den "Adjacent Sibling Selector" (`+`) verwenden.

```css
/* Wenn das unsichtbare Input aktiviert ist ... */
.visually-hidden:checked + .checkbox-visual {
  background-color: #007bff;
  border-color: #007bff;
}
```

Das ist schon mal ein guter Anfang! Die Box füllt sich mit Farbe. Aber wo ist das Häkchen? Hierfür eignen sich Pseudo-Elemente wie `::after` hervorragend. Wir können mit CSS ein Häkchen "zeichnen".

```css
/* Häkchen als Pseudo-Element erstellen */
.checkbox-visual::after {
  content: '';
  display: block;
  width: 0.3em;
  height: 0.6em;
  border: solid white;
  border-width: 0 3px 3px 0;
  transform: rotate(45deg) scale(0); /* Startet unsichtbar und skaliert */
  transition: transform 0.2s;
  margin-left: 0.35em; /* Positionierung des Häkchens */
  margin-top: 0.05em;
}

/* Wenn die Checkbox aktiviert ist, das Häkchen einblenden */
.visually-hidden:checked + .checkbox-visual::after {
  transform: rotate(45deg) scale(1);
}
```

#### Der unverzichtbare Fokus-Stil

Ein fundamentaler Aspekt der Barrierefreiheit ist eine klare visuelle Kennzeichnung des fokussierten Elements. Wer mit der Tastatur navigiert (z. B. durch Drücken der Tab-Taste), muss jederzeit sehen können, wo er sich auf der Seite befindet. Da unser originales Input unsichtbar ist, müssen wir diesen Fokus-Stil an unser visuelles Element weitergeben.

Hierfür eignet sich die Pseudo-Klasse `:focus-visible`. Sie spricht gezielt auf den Fokus an, der durch Tastaturnavigation entsteht, nicht aber durch einen Mausklick, was dem Nutzerverhalten meist entgegenkommt.

```css
/* Wenn das unsichtbare Input den Fokus erhält ... */
.visually-hidden:focus-visible + .checkbox-visual {
  outline: 2px solid #007bff;
  outline-offset: 2px;
}
```

### Das gleiche Spiel für Radio-Buttons

Die gute Nachricht: Die exakt gleiche Technik funktioniert auch für Radio-Buttons. Der einzige Unterschied liegt in der Semantik und im Verhalten, das uns das native `<input type="radio">` schenkt. Radio-Buttons, die denselben `name`-Attributwert haben, bilden eine Gruppe, aus der immer nur eine Option ausgewählt werden kann. Dieses Verhalten bekommen wir durch die Nutzung des nativen Elements geschenkt – ganz ohne JavaScript.

Hier ist ein Beispiel für eine Gruppe von Radio-Buttons:

**HTML:**

```html
<fieldset>
  <legend>Bevorzugte Kontaktmethode</legend>

  <label class="custom-radio">
    <input type="radio" name="contact" value="email" class="visually-hidden" checked>
    <span class="radio-visual" aria-hidden="true"></span>
    <span class="radio-label">E-Mail</span>
  </label>

  <label class="custom-radio">
    <input type="radio" name="contact" value="phone" class="visually-hidden">
    <span class="radio-visual" aria-hidden="true"></span>
    <span class="radio-label">Telefon</span>
  </label>
</fieldset>
```

**CSS:**

Das CSS ist nahezu identisch zu dem der Checkbox, wir passen nur die Form an, um den typischen runden Look zu erzielen.

```css
.radio-visual {
  display: inline-block;
  width: 1.2em;
  height: 1.2em;
  margin-right: 0.5em;
  border: 2px solid #555;
  border-radius: 50%; /* Der einzige Unterschied: ein Kreis! */
  transition: border-color 0.2s;
  vertical-align: middle;
  position: relative;
}

/* Der innere Punkt */
.radio-visual::after {
  content: '';
  display: block;
  width: 0.6em;
  height: 0.6em;
  border-radius: 50%;
  background-color: white;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(0);
  transition: transform 0.2s;
}

/* Wenn das Radio aktiviert ist, den Punkt einblenden und Rand färben */
.visually-hidden:checked + .radio-visual {
  border-color: #007bff;
}

.visually-hidden:checked + .radio-visual::after {
  transform: translate(-50%, -50%) scale(1);
}

/* Und natürlich der Fokus-Stil */
.visually-hidden:focus-visible + .radio-visual {
  outline: 2px solid #007bff;
  outline-offset: 2px;
}
```

### Warum wir hier (fast) kein ARIA brauchen

Dieses Kapitel befindet sich in einem Modul über ARIA, und doch haben wir kaum ein `aria`-Attribut verwendet. Das ist kein Versehen, sondern das Ziel. Die hier gezeigte Methode ist ein perfektes Beispiel für die erste und wichtigste Regel von ARIA:

> **Wenn du ein natives HTML-Element verwenden kannst, das die benötigte Semantik und das Verhalten bereits mitbringt, verwende es.**

Indem wir das native `<input>` beibehalten, erhalten wir kostenlos:
*   Die korrekte Rolle (`role="checkbox"` oder `role="radio"`).
*   Den korrekten Zustand (`aria-checked="true/false"`).
*   Die native Tastaturbedienung (Leertaste für Checkboxen, Pfeiltasten für Radio-Gruppen).
*   Die Integration in den Formular-Versand.

Wir müssen diese Dinge nicht mühsam mit ARIA und JavaScript nachbauen. Unsere Aufgabe beschränkt sich darauf, das visuelle Erscheinungsbild zu synchronisieren und sicherzustellen, dass die Interaktivität des Originals erhalten bleibt. Das ist robust, wartungsfreundlich und von Natur aus zugänglich. Der Einsatz von ARIA wird erst dann notwendig, wenn wir aus zwingenden Gründen kein natives Element verwenden können und ein Steuerelement komplett aus `<div>`s oder `<span>`s nachbauen müssen – ein deutlich komplexerer und fehleranfälligerer Weg.
