# Number und range

### Zahlen und Bereiche: Die Eingabetypen `number` und `range`

Wenn du möchtest, dass Benutzer in deinen Formularen Zahlen eingeben, ist ein allgemeines Textfeld (`<input type="text">`) oft nicht die beste Wahl. Es erlaubt die Eingabe beliebiger Zeichen, was zu Fehleingaben führen kann und die anschließende Validierung auf dem Server erschwert. Viel wichtiger noch: Es bietet dem Benutzer keine optimale Erfahrung, insbesondere auf mobilen Geräten.

HTML5 hat für diesen Zweck spezialisierte Eingabetypen eingeführt, die genau auf numerische Daten zugeschnitten sind. Die beiden wichtigsten sind `type="number"` für die exakte Eingabe von Zahlen und `type="range"` für die Auswahl eines Wertes aus einem vordefinierten Bereich. Schauen wir uns beide genauer an.

#### Präzise Werte mit `<input type="number">`

Der Eingabetyp `number` ist deine erste Wahl, wenn du eine exakte numerische Eingabe benötigst. Denk an Anwendungsfälle wie die Angabe eines Alters, einer Bestellmenge oder eines Preises.

Ein einfaches `number`-Feld sieht so aus:

```html
<label for="menge">Anzahl:</label>
<input type="number" id="menge" name="artikel_menge">
```

Schon in dieser Grundform bietet es enorme Vorteile gegenüber einem Textfeld. Die meisten Desktop-Browser rendern dieses Feld mit kleinen Pfeiltasten (sogenannten "Steppers" oder "Spin Buttons"), mit denen der Benutzer den Wert schrittweise erhöhen oder verringern kann. Auf mobilen Geräten passiert etwas noch Besseres: Beim Antippen des Feldes wird automatisch die numerische Tastatur eingeblendet, was die Eingabe von Zahlen deutlich erleichtert und die Wahrscheinlichkeit von Tippfehlern (wie der Eingabe von Buchstaben) reduziert.

Die wahre Stärke des `number`-Typs liegt jedoch in seinen Attributen, mit denen du die erlaubten Eingaben präzise steuern kannst.

*   **`min` und `max`**: Mit diesen beiden Attributen legst du den zulässigen Wertebereich fest. Möchtest du zum Beispiel die Anzahl der zu bestellenden Produkte auf 1 bis 10 begrenzen, kannst du das so umsetzen:

    ```html
    <label for="menge">Anzahl (1-10):</label>
    <input type="number" id="menge" name="artikel_menge" min="1" max="10">
    ```
    Der Browser wird nun automatisch verhindern, dass der Benutzer einen Wert außerhalb dieses Bereichs über die Pfeiltasten auswählt. Bei einer manuellen Eingabe und anschließendem Absenden des Formulars wird der Browser eine eingebaute Validierungsfehlermeldung anzeigen, falls der Wert ungültig ist.

*   **`step`**: Dieses Attribut definiert die Schrittweite, mit der sich der Wert ändert, wenn die Pfeiltasten verwendet werden. Der Standardwert ist `1`. Wenn du aber zum Beispiel nur gerade Zahlen zulassen möchtest, kannst du `step="2"` verwenden.

    ```html
    <label for="gerade-zahl">Gerade Zahl:</label>
    <input type="number" id="gerade-zahl" name="gerade_zahl" step="2" min="0">
    ```

*   **Dezimalzahlen**: Standardmäßig erwartet das `number`-Feld ganze Zahlen. Wenn du Dezimalzahlen (Gleitkommazahlen) erlauben möchtest, musst du das `step`-Attribut entsprechend anpassen. Um beispielsweise Preise mit zwei Nachkommastellen zu ermöglichen, setzt du `step="0.01"`.

    ```html
    <label for="preis">Preis in €:</label>
    <input type="number" id="preis" name="produkt_preis" min="0" step="0.01" placeholder="z.B. 19.99">
    ```
    Wenn du beliebige Dezimalzahlen zulassen möchtest, kannst du den speziellen Wert `step="any"` verwenden.

*   **`value`**: Mit diesem Attribut kannst du einen voreingestellten Wert festlegen, der beim Laden der Seite bereits im Feld steht.

Zusammengenommen ergibt sich ein sehr mächtiges Werkzeug. Hier ist ein Beispiel, das mehrere Attribute kombiniert, um die Körpergröße in Metern zu erfassen:

```html
<label for="groesse">Deine Körpergröße (in m):</label>
<input
  type="number"
  id="groesse"
  name="koerpergroesse"
  min="0.5"
  max="2.5"
  step="0.01"
  value="1.75">
```

Dieses Feld startet mit dem Wert 1.75, erlaubt Werte zwischen 0.50 und 2.50 und lässt sich in Schritten von einem Zentimeter (0.01 Meter) verändern. Das ist eine deutliche Verbesserung der Benutzerführung und Datenqualität im Vergleich zu einem einfachen Textfeld.

#### Ungefähre Werte mit `<input type="range">`

Manchmal ist die exakte numerische Eingabe gar nicht das Ziel. Stell dir vor, du möchtest die Lautstärke in einer Web-Anwendung einstellen oder die Helligkeit eines Bildes anpassen. Hier ist die genaue Zahl (z.B. 73 von 100) weniger wichtig als die relative Position auf einer Skala. Für solche Fälle ist der Eingabetyp `range` perfekt geeignet.

Browser stellen ein `<input type="range">` typischerweise als Schieberegler (Slider) dar. Der Benutzer kann einen "Anfasser" (Thumb) entlang einer Leiste ziehen, um einen Wert auszuwählen.

```html
<label for="lautstaerke">Lautstärke:</label>
<input type="range" id="lautstaerke" name="volume">
```

Auch der `range`-Typ verwendet die Attribute `min`, `max`, `step` und `value`, um sein Verhalten zu definieren. Die Standardwerte sind oft `min="0"`, `max="100"` und `step="1"`.

```html
<label for="helligkeit">Helligkeit:</label>
<input
  type="range"
  id="helligkeit"
  name="brightness"
  min="0"
  max="100"
  step="1"
  value="50">
```

Dieses Beispiel erzeugt einen Schieberegler, der von 0 bis 100 reicht und standardmäßig in der Mitte (bei 50) positioniert ist.

Ein wesentlicher Unterschied zum `number`-Feld ist, dass der `range`-Slider dem Benutzer den aktuell ausgewählten Wert *nicht* standardmäßig anzeigt. Man sieht nur die Position des Reglers. Das ist oft ein Nachteil, da der Benutzer kein genaues Feedback über seine Auswahl erhält.

Glücklicherweise lässt sich das sehr einfach mit einer Prise JavaScript und einem `<output>`-Element beheben. Das `<output>`-Element ist semantisch dafür gedacht, das Ergebnis einer Berechnung oder einer Benutzeraktion anzuzeigen.

So kannst du den Wert des Sliders in Echtzeit sichtbar machen:

```html
<label for="zufriedenheit">Wie zufrieden bist du? (0-10)</label>
<input
  type="range"
  id="zufriedenheit"
  name="rating"
  min="0"
  max="10"
  value="5"
  oninput="this.nextElementSibling.value = this.value">
<output>5</output>
```

Was passiert hier?
1.  Wir haben ein `<output>`-Element direkt nach dem `<input>` platziert. Es zeigt den initialen Wert `5` an.
2.  Das `oninput`-Attribut im `<input>`-Tag enthält ein kurzes JavaScript-Snippet. Das `input`-Event wird jedes Mal ausgelöst, wenn sich der Wert des Reglers ändert (also während des Ziehens).
3.  `this.value` bezieht sich auf den aktuellen Wert des Sliders.
4.  `this.nextElementSibling` greift auf das nächste Geschwisterelement zu – in unserem Fall das `<output>`-Tag.
5.  `this.nextElementSibling.value = this.value` weist dem `<output>`-Element den aktuellen Wert des Sliders zu.

Das Ergebnis ist eine interaktive Komponente, bei der der Benutzer sofortiges visuelles Feedback über seine Auswahl erhält.

Eine weitere nützliche Funktion ist die Möglichkeit, mit dem `<datalist>`-Element Markierungen (Tick Marks) am Schieberegler anzubringen. Dies gibt dem Benutzer visuelle Anhaltspunkte für bestimmte Werte.

```html
<label for="temperatur">Gewünschte Raumtemperatur:</label>
<input type="range" id="temperatur" name="temp" min="16" max="28" step="1" list="temp-werte">

<datalist id="temp-werte">
  <option value="16" label="Kalt"></option>
  <option value="22" label="Ideal"></option>
  <option value="28" label="Warm"></option>
</datalist>
```

Hierbei verknüpfen wir den Slider über das `list`-Attribut mit der `<datalist>`, die die gleiche `id` hat. Die Browser, die dies unterstützen, zeigen nun kleine Striche an den Positionen 16, 22 und 28. Das `label`-Attribut in den `<option>`-Tags kann von manchen Browsern als Beschriftung für die Markierungen verwendet werden.

#### `number` vs. `range`: Wann verwendest du was?

Die Entscheidung zwischen `number` und `range` hängt ganz vom Anwendungsfall und der erwarteten Benutzerinteraktion ab.

*   **Verwende `type="number"`**, wenn der Benutzer einen **präzisen, bekannten Wert** eingeben muss. Die genaue Zahl ist wichtig. Beispiele: Alter, Postleitzahl, Stückzahl, Preis. Die Eingabe erfolgt meist über die Tastatur oder die Stepper-Pfeile.

*   **Verwende `type="range"`**, wenn der Benutzer einen Wert aus einem Bereich auswählen soll, bei dem die **relative Position wichtiger ist als die exakte Zahl**. Die Eingabe ist eher subjektiv oder schätzungsweise. Beispiele: Lautstärke, Helligkeit, Zoom-Stufe, Zufriedenheitsbewertung. Die Interaktion ist visuell und explorativ.

In manchen Fällen kann es sogar sinnvoll sein, beide Elemente zu kombinieren. Stell dir vor, du bietest einen Schieberegler für eine grobe Auswahl und daneben ein `number`-Feld, das den Wert des Reglers anzeigt und gleichzeitig eine feingranulare, manuelle Korrektur erlaubt. Durch eine Verknüpfung via JavaScript können sich beide Elemente gegenseitig aktualisieren und bieten so das Beste aus beiden Welten: eine intuitive, visuelle Auswahl und die Möglichkeit zur präzisen Eingabe.
