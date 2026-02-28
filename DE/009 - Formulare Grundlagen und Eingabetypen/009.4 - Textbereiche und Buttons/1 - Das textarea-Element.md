# Das textarea-Element

### Das textarea-Element: Mehrzeilige Texteingaben meistern

Wenn ein einfaches, einzeiliges Textfeld wie `<input type="text">` nicht ausreicht, betritt das `<textarea>`-Element die Bühne. Stell dir vor, du möchtest deinen Nutzern die Möglichkeit geben, einen Kommentar zu schreiben, eine ausführliche Produktbewertung abzugeben oder eine E-Mail in einem Kontaktformular zu verfassen. All diese Anwendungsfälle erfordern mehr Platz als eine einzelne Zeile. Genau hierfür wurde `<textarea>` geschaffen.

Im Gegensatz zum `<input>`-Element ist `<textarea>` ein sogenanntes gepaartes Tag. Das bedeutet, es hat ein öffnendes `<textarea>` und ein schließendes `</textarea>`. Dieser Unterschied ist fundamental, denn er bestimmt, wie du einen Standardwert für das Feld festlegst.

#### Grundlegende Syntax und Standardwerte

Die grundlegendste Form eines Textbereichs sieht so aus:

```html
<textarea name="kommentar"></textarea>
```

Das `name`-Attribut ist, wie bei allen Formularelementen, entscheidend. Es dient als Schlüssel, unter dem die eingegebenen Daten beim Absenden des Formulars an den Server übermittelt werden. Ohne `name` würde der Inhalt des Feldes einfach verloren gehen.

Wenn du einen vordefinierten Text im Feld anzeigen möchtest, schreibst du diesen direkt zwischen die öffnenden und schließenden Tags. Das `value`-Attribut, das du von `<input>`-Elementen kennst, gibt es hier nicht.

```html
<textarea name="feedback">Hier kannst du dein Feedback eintragen...</textarea>
```

**Wichtig:** Achte darauf, dass zwischen den Tags keine unerwünschten Leerzeichen oder Zeilenumbrüche stehen. Alles, was sich zwischen `<textarea>` und `</textarea>` befindet – einschließlich Einrückungen im Code – wird als Teil des Standardwerts interpretiert.

Eine saubere Implementierung mit einem `<label>` für die Barrierefreiheit sieht so aus:

```html
<label for="nachricht">Deine Nachricht an uns:</label>
<textarea id="nachricht" name="nachricht"></textarea>
```

Hier verknüpft das `for`-Attribut des Labels das `id`-Attribut der Textarea. Das hat zwei Vorteile: Ein Klick auf das Label setzt den Fokus direkt in das zugehörige Textfeld, und Screenreader können die Beschriftung korrekt zuordnen, was die Bedienung für Menschen mit Seheinschränkungen massiv erleichtert.

#### Die Größe des Textbereichs festlegen

Standardmäßig ist eine Textarea recht klein. Um ihre anfängliche Größe zu bestimmen, hast du zwei klassische HTML-Attribute zur Verfügung: `rows` und `cols`.

*   **`rows`**: Definiert die sichtbare Höhe des Feldes in Textzeilen.
*   **`cols`**: Definiert die sichtbare Breite des Feldes in durchschnittlichen Zeichenbreiten.

```html
<label for="biografie">Erzähle uns etwas über dich:</label>
<textarea id="biografie" name="biografie" rows="10" cols="50"></textarea>
```

Dieses Beispiel erzeugt ein Textfeld, das 10 Zeilen hoch und etwa 50 Zeichen breit ist. Der Begriff "durchschnittliche Zeichenbreite" ist wichtig, da die meisten Schriftarten keine feste Zeichenbreite haben (ein "i" ist schmaler als ein "W"). `cols` ist also eher ein Richtwert als eine exakte Pixelangabe.

Heutzutage wird die Größe von Formularelementen jedoch vorzugsweise mit CSS gesteuert, da dies mehr Flexibilität und eine präzisere Kontrolle ermöglicht. Mit `width` und `height` kannst du die Dimensionen exakt festlegen.

```css
textarea {
  width: 100%;
  height: 150px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
```

Diese CSS-Regeln würden die Textarea über die volle Breite ihres Elternelements spannen und ihr eine feste Höhe von 150 Pixeln geben.

#### Wichtige Attribute im Detail

Neben `name`, `rows` und `cols` gibt es eine Reihe weiterer Attribute, mit denen du das Verhalten und die Validierung deiner Textarea steuern kannst.

**`placeholder`**
Wie beim `<input>`-Element dient `placeholder` dazu, einen Texthinweis im Feld anzuzeigen, der verschwindet, sobald der Nutzer beginnt zu tippen. Er ist nützlich, um ein kurzes Beispiel oder eine Anweisung zu geben.

```html
<textarea name="tweet" placeholder="Was gibt's Neues?"></textarea>
```

Denke daran, dass der `placeholder` kein Ersatz für ein `<label>` ist. Er ist für die Barrierefreiheit nicht ausreichend, da er verschwindet und von Screenreadern nicht immer zuverlässig als Beschriftung erkannt wird.

**`maxlength` und `minlength`**
Diese Attribute sind extrem nützlich für die clientseitige Validierung.

*   `maxlength`: Limitiert die maximale Anzahl an Zeichen, die der Nutzer eingeben kann.
*   `minlength`: Legt eine minimale Anzahl an Zeichen fest, die eingegeben werden müssen, damit das Formular gültig ist.

```html
<label for="kurzbeschreibung">Produktbeschreibung (100-500 Zeichen):</label>
<textarea 
  id="kurzbeschreibung" 
  name="kurzbeschreibung"
  minlength="100"
  maxlength="500"
  required>
</textarea>
```

Moderne Browser hindern den Nutzer daran, mehr Zeichen als durch `maxlength` erlaubt einzugeben, und zeigen eine Fehlermeldung an, wenn die `minlength` beim Absenden des Formulars nicht erreicht ist (vorausgesetzt, `required` ist ebenfalls gesetzt).

**`required`**
Dieses boolesche Attribut gibt an, dass das Feld ausgefüllt werden muss, bevor das Formular abgesendet werden kann. Der Browser verhindert das Absenden und zeigt eine Standard-Fehlermeldung an, wenn das Feld leer ist.

```html
<textarea name="agb-zustimmung" required></textarea>
```

**`readonly` und `disabled`**
Beide Attribute verhindern, dass der Nutzer den Inhalt der Textarea bearbeitet, aber sie tun dies auf unterschiedliche Weise.

*   **`readonly`**: Der Inhalt kann nicht geändert werden, aber der Nutzer kann den Text markieren und kopieren. Wichtig ist, dass der Wert des Feldes trotzdem mit dem Formular an den Server **gesendet wird**.
*   **`disabled`**: Das Element ist komplett deaktiviert. Es kann nicht fokussiert oder bearbeitet werden, und sein Wert wird **nicht** mit dem Formular an den Server gesendet. Optisch wird es oft ausgegraut dargestellt.

```html
<!-- Nutzer kann den Text lesen und kopieren, Wert wird gesendet -->
<textarea name="lizenztext" readonly>Dies ist der unveränderliche Lizenztext.</textarea>

<!-- Nutzer kann nicht interagieren, Wert wird nicht gesendet -->
<textarea name="veraltetes-feld" disabled>Dieses Feld ist nicht mehr aktiv.</textarea>
```

**`wrap`**
Dieses Attribut steuert, wie der Zeilenumbruch innerhalb der Textarea gehandhabt wird – sowohl bei der Anzeige als auch beim Senden der Daten.

*   **`soft` (Standardwert)**: Der Text wird im Browser für eine bessere Lesbarkeit automatisch umgebrochen, wenn er das Ende einer Zeile erreicht. Beim Absenden werden diese automatischen Umbrüche jedoch ignoriert; der Text wird als eine lange Zeichenkette ohne Zeilenumbrüche (außer den vom Nutzer explizit per Enter-Taste eingefügten) gesendet.
*   **`hard`**: Der Text wird nicht nur im Browser umgebrochen, sondern die Zeilenumbrüche werden auch mit den Formulardaten mitgesendet. Damit dieses Attribut funktioniert, **muss** das `cols`-Attribut ebenfalls gesetzt sein, da es dem Browser sagt, nach wie vielen Zeichen er einen Umbruch einfügen soll.
*   **`off`**: Der Textumbruch ist komplett deaktiviert. Langer Text wird in einer einzigen Zeile dargestellt und erzeugt einen horizontalen Scrollbalken. Dieser Wert wird nur selten verwendet.

```html
<!-- Der Browser fügt beim Senden Zeilenumbrüche nach ca. 60 Zeichen ein -->
<textarea name="gedicht" wrap="hard" cols="60"></textarea>
```

#### Styling und Benutzerfreundlichkeit mit CSS

Die meisten modernen Browser erlauben es dem Nutzer standardmäßig, die Größe einer Textarea durch Ziehen an der unteren rechten Ecke zu verändern. Dieses Verhalten wird durch die CSS-Eigenschaft `resize` gesteuert. Manchmal möchte man dieses Verhalten einschränken.

*   `resize: vertical;` erlaubt nur das Ändern der Höhe.
*   `resize: horizontal;` erlaubt nur das Ändern der Breite.
*   `resize: both;` (Standard) erlaubt beides.
*   `resize: none;` deaktiviert die Größenänderung komplett.

```css
textarea.no-resize {
  resize: none;
}
```

Die Kombination aus durchdachten HTML-Attributen und gezieltem CSS-Styling macht das `<textarea>`-Element zu einem mächtigen Werkzeug für die Erfassung umfangreicherer Texteingaben. Es bildet das Rückgrat für Kommentarfunktionen, Kontaktformulare und unzählige andere interaktive Webanwendungen.
