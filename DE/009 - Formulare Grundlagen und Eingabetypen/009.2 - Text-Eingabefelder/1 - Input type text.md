# Input type text

### Das universelle Texteingabefeld: `input type="text"`

Wenn du an ein Formular im Web denkst, kommt dir wahrscheinlich als Erstes ein einfaches, leeres Feld in den Sinn, in das du deinen Namen, eine Suchanfrage oder einen Benutzernamen eingibst. Genau dieses Feld ist das Herzstück vieler Interaktionen im Internet und wird in HTML durch `<input type="text">` realisiert. Es ist das vielseitigste und am häufigsten verwendete Eingabeelement – ein echtes Arbeitstier, das du in und auswendig kennen solltest.

Ein Texteingabefeld ist für die Erfassung von einzeiligem, unformatiertem Text konzipiert. Alles, von einem einzelnen Wort bis hin zu einem kurzen Satz, findet hier seinen Platz. In seiner einfachsten Form sieht der Code dafür unscheinbar aus:

```html
<input type="text">
```

Doch hinter dieser schlichten Fassade verbirgt sich eine Fülle von Attributen, die es dir ermöglichen, das Verhalten und die Erscheinung dieses Feldes präzise zu steuern. Lass uns diese Attribute Schritt für Schritt erkunden.

#### Die unverzichtbaren Identifikatoren: `name` und `id`

Zwei der wichtigsten Attribute für jedes Formularfeld sind `name` und `id`. Obwohl sie oft denselben Wert haben, dienen sie völlig unterschiedlichen Zwecken.

Das **`name`**-Attribut ist entscheidend für die serverseitige Verarbeitung. Wenn ein Formular abgeschickt wird, werden die Daten als Schlüssel-Wert-Paare an den Server gesendet. Der Wert des `name`-Attributs wird zum Schlüssel, und die Eingabe des Nutzers wird zum Wert.

Stell dir vor, du hast ein Feld für einen Benutzernamen:

```html
<form action="/registrieren" method="post">
  <label for="username">Benutzername:</label>
  <input type="text" id="username" name="benutzername">
  <button type="submit">Senden</button>
</form>
```

Wenn ein Nutzer "MaxMustermann" eingibt und das Formular abschickt, empfängt der Server die Information `benutzername=MaxMustermann`. Ohne das `name`-Attribut würde die Eingabe des Nutzers einfach im digitalen Nichts verschwinden und den Server nie erreichen.

Das **`id`**-Attribut hingegen ist für die clientseitige Identifikation gedacht. Es vergibt einen einzigartigen Namen für das Element auf der gesamten HTML-Seite. Dieser Name wird hauptsächlich für zwei Dinge gebraucht:
1.  **Verknüpfung mit einem `<label>`:** Das `for`-Attribut eines `<label>`-Elements verweist auf die `id` eines Eingabefeldes. Das hat zwei große Vorteile: Zum einen verbessert es die Barrierefreiheit, da Screenreader nun wissen, welche Beschriftung zu welchem Feld gehört. Zum anderen verbessert es die Benutzerfreundlichkeit, da der Nutzer nun auf die Beschriftung klicken kann, um den Fokus direkt in das zugehörige Eingabefeld zu setzen.
2.  **Manipulation durch CSS und JavaScript:** Mit CSS kannst du das Element gezielt stylen (`#username { border-color: blue; }`), und mit JavaScript kannst du es ansprechen, um seinen Wert zu lesen, zu ändern oder auf Benutzereingaben zu reagieren.

Eine gute Praxis ist es, `name` und `id` fast immer gemeinsam zu verwenden und ihnen oft, aber nicht zwingend, den gleichen Wert zu geben.

#### Starthilfe und Orientierung: `value` und `placeholder`

Manchmal möchtest du einem Feld einen voreingestellten Wert mitgeben. Dafür ist das **`value`**-Attribut zuständig. Der Text, den du hier angibst, steht bereits im Feld, wenn die Seite geladen wird. Der Nutzer kann ihn dann so belassen oder überschreiben. Dies ist besonders nützlich in Formularen zur Bearbeitung von Daten, wo die aktuellen Werte des Nutzers (z.B. sein Name) bereits eingetragen sein sollen.

```html
<label for="vorname">Vorname:</label>
<input type="text" id="vorname" name="vorname" value="Max">
```

Im Gegensatz dazu steht das **`placeholder`**-Attribut. Es zeigt einen kurzen Hinweistext oder ein Beispielformat im Eingabefeld an, solange dieses leer ist und nicht den Fokus hat. Sobald der Nutzer in das Feld klickt oder zu tippen beginnt, verschwindet der Platzhaltertext.

```html
<label for="suche">Suche:</label>
<input type="text" id="suche" name="q" placeholder="z.B. HTML-Formulare">
```

Ein wichtiger Hinweis: Ein `placeholder` ist niemals ein Ersatz für ein `<label>`! Er ist eine rein visuelle Hilfe, die verschwindet. Nutzer von Screenreadern erhalten oft keine Information über den Platzhalter, und wenn der Nutzer erst einmal mit der Eingabe begonnen hat, ist der ursprüngliche Hinweis verschwunden, was zu Verwirrung führen kann. Nutze ihn als ergänzende Hilfe, nicht als primäre Beschriftung.

#### Kontrolle über Größe und Länge: `size`, `minlength` und `maxlength`

Diese drei Attribute helfen dir, die physische und inhaltliche Länge der Eingabe zu steuern.

*   **`size`**: Dieses Attribut bestimmt die sichtbare Breite des Eingabefeldes in Zeichen. `size="20"` bedeutet, dass das Feld ungefähr so breit ist, dass 20 Zeichen hineinpassen. Wichtig ist hierbei zu verstehen, dass dies eine rein visuelle Angabe ist und die Anzahl der Zeichen, die ein Nutzer eingeben kann, nicht begrenzt. In der modernen Webentwicklung wird die Breite von Feldern meist flexibler und präziser über CSS gesteuert.

*   **`maxlength`**: Dieses Attribut setzt eine harte Obergrenze für die Anzahl der Zeichen, die eingegeben werden können. Gibt ein Nutzer mehr Zeichen ein, wird die Eingabe einfach ignoriert. Das ist nützlich für Felder mit einer festen Länge, wie zum Beispiel eine Postleitzahl in manchen Ländern oder eine Identifikationsnummer.

*   **`minlength`**: Dieses Attribut definiert die minimale Anzahl von Zeichen, die das Feld für eine gültige Eingabe enthalten muss. Das Formular kann nicht abgeschickt werden, solange die Eingabe kürzer ist als der hier definierte Wert. Der Browser gibt dem Nutzer in diesem Fall eine entsprechende Fehlermeldung.

Ein Beispiel, das diese Attribute kombiniert:

```html
<label for="plz">Postleitzahl (5 Ziffern):</label>
<input type="text" id="plz" name="postleitzahl" size="5" minlength="5" maxlength="5">
```

#### Interaktion steuern: `readonly` und `disabled`

Es gibt Situationen, in denen ein Feld zwar sichtbar sein, aber vom Nutzer nicht verändert werden soll. Hierfür gibt es zwei Attribute, deren Unterschied entscheidend ist.

*   **`readonly`**: Ein Feld mit diesem Attribut kann nicht bearbeitet werden. Der Nutzer kann den Inhalt markieren und kopieren, aber nichts daran ändern. Der Wert eines `readonly`-Feldes wird jedoch ganz normal mit dem Formular abgeschickt. Das ist ideal, um einen Wert anzuzeigen, der aus einer Berechnung stammt oder vom System vorgegeben ist, wie zum Beispiel ein Benutzername bei der Änderung des Passworts.

*   **`disabled`**: Ein `disabled`-Feld ist vollständig deaktiviert. Es kann weder angeklickt, noch fokussiert, noch bearbeitet werden. Visuell wird es meist ausgegraut dargestellt. Der entscheidende Unterschied: Der Wert eines `disabled`-Feldes wird **nicht** mit dem Formular abgeschickt. Es ist, als wäre das Feld nicht vorhanden. Man nutzt es oft, um Optionen zu deaktivieren, die erst nach einer anderen Auswahl relevant werden.

Beide sind sogenannte boolesche Attribute. Ihre bloße Anwesenheit im Tag aktiviert die Eigenschaft.

```html
<!-- Wert wird mitgesendet, kann aber nicht geändert werden -->
<input type="text" name="benutzer-id" value="12345" readonly>

<!-- Wert wird ignoriert und nicht mitgesendet -->
<input type="text" name="rabattcode" value="nicht verfügbar" disabled>
```

#### Eingaben validieren: `required` und `pattern`

Moderne Browser bieten eingebaute Mechanismen zur Validierung von Formularen, noch bevor die Daten an den Server gesendet werden.

*   **`required`**: Dieses boolesche Attribut ist die einfachste Form der Validierung. Es kennzeichnet ein Feld als Pflichtfeld. Der Browser wird das Absenden des Formulars verhindern, solange dieses Feld leer ist, und dem Nutzer eine entsprechende Meldung anzeigen.

*   **`pattern`**: Für komplexere Validierungsregeln gibt es das `pattern`-Attribut. Es erwartet als Wert einen regulären Ausdruck (Regular Expression). Nur wenn die Eingabe des Nutzers diesem Muster entspricht, gilt das Feld als gültig. Reguläre Ausdrücke sind eine mächtige Mini-Sprache zur Mustererkennung in Texten.

Angenommen, du benötigst eine Kundennummer, die immer mit "KD" beginnt, gefolgt von genau sechs Ziffern:

```html
<label for="kundennummer">Kundennummer:</label>
<input type="text" id="kundennummer" name="kundennummer"
       pattern="KD[0-9]{6}"
       title="Bitte geben Sie eine gültige Kundennummer ein (z.B. KD123456)."
       required>
```

Hier bedeutet `KD[0-9]{6}`:
- `KD`: Die Zeichenkette muss mit "KD" beginnen.
- `[0-9]`: Darauf muss eine Ziffer von 0 bis 9 folgen.
- `{6}`: Davon müssen genau sechs Stück vorhanden sein.

Das `title`-Attribut ist hier besonders nützlich, da viele Browser seinen Inhalt als Teil der Fehlermeldung anzeigen, wenn das Muster nicht passt. So gibst du dem Nutzer einen klaren Hinweis auf das erwartete Format.

#### Nützliche Helfer: `autocomplete` und `spellcheck`

Zuletzt gibt es noch einige Attribute, die die Benutzererfahrung verbessern.

*   **`autocomplete`**: Dieses Attribut gibt dem Browser einen Hinweis, welche Art von Daten in diesem Feld erwartet wird, und erlaubt es ihm, passende Vorschläge aus zuvor gespeicherten Eingaben des Nutzers zu machen (z.B. Namen, Adressen, E-Mail). Du kannst es mit `on` oder `off` global steuern oder spezifische Werte wie `name`, `street-address` oder `username` verwenden, um dem Browser präzisere Anweisungen zu geben.

*   **`spellcheck`**: Dieses Attribut kann auf `true` oder `false` gesetzt werden, um die browserinterne Rechtschreibprüfung für dieses Feld zu aktivieren oder zu deaktivieren. Für Felder wie Benutzernamen oder Codes ist es sinnvoll, sie zu deaktivieren (`spellcheck="false"`), während sie für Freitextfelder wie einen Betreff nützlich sein kann.

Das einfache `<input type="text">` ist also weit mehr als nur ein leeres Kästchen. Mit dem richtigen Einsatz seiner Attribute verwandelst du es in ein intelligentes, benutzerfreundliches und robustes Werkzeug, das präzise die Daten sammelt, die du benötigst.
