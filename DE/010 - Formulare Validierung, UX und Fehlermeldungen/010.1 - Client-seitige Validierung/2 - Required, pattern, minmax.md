# Required, pattern, min/max

### Die Wächter deiner Formulare: `required`, `pattern` und `min`/`max`

Stell dir vor, du füllst ein wichtiges Online-Formular aus, klickst auf „Senden“ und … nichts passiert. Oder schlimmer: Die Seite lädt neu und alle deine Eingaben sind weg, nur eine kryptische Fehlermeldung ganz oben sagt dir, dass etwas nicht stimmte. Eine frustrierende Erfahrung, die wir alle schon gemacht haben. Als Entwickler liegt es in deiner Hand, es besser zu machen. Die client-seitige Validierung ist hier dein wichtigstes Werkzeug. Sie ist die erste Verteidigungslinie gegen falsche oder unvollständige Daten und ein fantastischer Service für deine Nutzer. Anstatt sie im Dunkeln tappen zu lassen, gibst du ihnen sofortiges, klares Feedback direkt im Browser – noch bevor irgendwelche Daten an den Server geschickt werden.

In diesem Kapitel schauen wir uns die fundamentalen HTML-Attribute an, die dir diese Macht verleihen. Sie sind einfach zu implementieren und haben eine enorme Wirkung auf die Benutzerfreundlichkeit und die Qualität der Daten, die du erhältst.

#### Das unmissverständliche Muss: `required`

Das wohl einfachste und gleichzeitig eines der nützlichsten Validierungsattribute ist `required`. Es ist ein boolesches Attribut, was bedeutet, dass seine bloße Anwesenheit im Tag ausreicht, um es zu aktivieren. Du teilst dem Browser damit mit: "Dieses Feld darf auf keinen Fall leer sein."

Für ein einfaches Textfeld sieht das so aus:

```html
<label for="username">Benutzername:</label>
<input type="text" id="username" name="username" required>
```

Wenn ein Nutzer nun versucht, das Formular abzusenden, ohne in dieses Feld etwas einzugeben, wird der Browser den Vorgang blockieren. Er zeigt stattdessen eine kleine Sprechblase an, die auf das leere Feld hinweist, oft mit einer Nachricht wie „Füllen Sie dieses Feld aus“. Diese Nachricht ist vom Browser und Betriebssystem abhängig, aber die Funktion ist universell.

Das `required`-Attribut ist aber nicht nur auf Textfelder beschränkt. Es funktioniert intelligent mit verschiedenen `input`-Typen:

*   **Checkboxen (`type="checkbox"`)**: Hier bedeutet `required`, dass die Checkbox angehakt sein muss. Perfekt für die Zustimmung zu den AGB.

    ```html
    <input type="checkbox" id="agb" name="agb" required>
    <label for="agb">Ich akzeptiere die Allgemeinen Geschäftsbedingungen.</label>
    ```

*   **Radio-Buttons (`type="radio"`)**: Bei einer Gruppe von Radio-Buttons (die denselben `name` haben) muss mindestens eine Option ausgewählt sein. Du musst das `required`-Attribut nur bei einem der Radio-Buttons in der Gruppe angeben, es gilt dann aber für die gesamte Gruppe. Üblicherweise setzt man es auf den ersten.

    ```html
    <p>Bevorzugte Kontaktmethode:</p>
    <input type="radio" id="contact_email" name="contact" value="email" required>
    <label for="contact_email">E-Mail</label>

    <input type="radio" id="contact_phone" name="contact" value="phone">
    <label for="contact_phone">Telefon</label>
    ```

*   **Auswahllisten (`<select>`)**: Bei einem Dropdown-Menü stellt `required` sicher, dass der Nutzer eine andere Option als die Platzhalter-Option auswählt. Damit das funktioniert, muss die erste, deaktivierte Option einen leeren `value` haben.

    ```html
    <label for="land">Land:</label>
    <select id="land" name="land" required>
      <option value="">Bitte auswählen</option>
      <option value="de">Deutschland</option>
      <option value="at">Österreich</option>
      <option value="ch">Schweiz</option>
    </select>
    ```
    Der Browser erkennt, dass die Option mit `value=""` keine gültige Auswahl ist und fordert den Nutzer auf, eine der anderen Optionen zu wählen.

#### Grenzen setzen: `minlength`, `maxlength`, `min` und `max`

Manchmal reicht es nicht, nur zu wissen, *dass* ein Feld ausgefüllt ist. Oft müssen die Eingaben auch bestimmten quantitativen Regeln folgen.

##### Zeichenzähler: `minlength` und `maxlength`

Für textbasierte Eingabefelder (`text`, `email`, `password`, `search`, `tel`, `url`) kannst du die erlaubte Zeichenlänge einschränken.

*   `maxlength` ist der ältere der beiden Wächter. Er setzt eine harte Obergrenze. Der Browser verhindert aktiv, dass der Nutzer mehr Zeichen eingibt als erlaubt. Das ist eine sehr direkte Form der Eingabebeschränkung.
*   `minlength` ist sein jüngerer Bruder und ein reines Validierungsattribut. Es legt die Mindestanzahl an Zeichen fest. Der Nutzer kann zwar weniger Zeichen eingeben, aber das Formular kann erst abgeschickt werden, wenn die Mindestlänge erreicht ist.

Ein typisches Anwendungsbeispiel ist die Vergabe eines Passworts:

```html
<label for="password">Passwort:</label>
<input type="password" id="password" name="password" minlength="8" maxlength="64" required>
```

Hier muss der Nutzer ein Passwort eingeben (`required`), das mindestens 8 Zeichen lang ist (`minlength`). Gleichzeitig kann er nicht versehentlich ein extrem langes Passwort eingeben, da bei 64 Zeichen Schluss ist (`maxlength`).

##### Zahlen im Griff: `min`, `max` und `step`

Für numerische Eingabefelder wie `input type="number"` oder auch Datums- und Zeittypen gibt es ein ähnliches Trio: `min`, `max` und `step`.

*   `min` definiert den kleinsten erlaubten Wert.
*   `max` definiert den größten erlaubten Wert.
*   `step` legt die Schrittweite fest, in der sich der Wert ändern darf (z.B. über die kleinen Pfeile im Eingabefeld).

Stell dir vor, du bietest in einem Shop Produkte an, von denen ein Kunde mindestens 1 und höchstens 10 Stück bestellen kann.

```html
<label for="menge">Anzahl:</label>
<input type="number" id="menge" name="menge" min="1" max="10" step="1" value="1">
```

Hier kann der Nutzer nur ganze Zahlen zwischen 1 und 10 eingeben. Der `step="1"` sorgt dafür, dass keine Kommazahlen wie 2,5 eingegeben werden können. Wenn du Kommazahlen erlauben möchtest, könntest du `step="0.1"` für eine Dezimalstelle oder `step="any"` für beliebige Fließkommazahlen verwenden.

Diese Attribute sind auch extrem nützlich für Datumseingaben. Du könntest zum Beispiel ein Geburtsdatum verlangen, das mindestens 18 Jahre in der Vergangenheit liegt, oder ein Lieferdatum, das frühestens morgen sein darf.

```html
<label for="lieferdatum">Lieferdatum:</label>
<!-- Das `min`-Attribut muss im Format YYYY-MM-DD angegeben werden. -->
<!-- Hier würde der Wert dynamisch per JavaScript gesetzt, z.B. auf das morgige Datum. -->
<input type="date" id="lieferdatum" name="lieferdatum" min="2024-01-01" required>
```

#### Das mächtigste Werkzeug: Das `pattern`-Attribut

Was aber, wenn deine Anforderungen komplexer sind als nur Längen- oder Wertebereiche? Was, wenn ein Benutzername nur aus Kleinbuchstaben und Zahlen bestehen darf? Oder eine deutsche Postleitzahl exakt fünf Ziffern haben muss? Hier kommt das `pattern`-Attribut ins Spiel.

Das `pattern`-Attribut erlaubt dir, eine **Regulären Ausdruck (Regular Expression, kurz RegEx)** zu definieren. Ein Regulärer Ausdruck ist eine Mini-Sprache zur Beschreibung von Zeichenkettenmustern. Es ist ein unglaublich mächtiges Werkzeug, aber auch ein Thema für sich. Wir werden hier keine komplette Einführung in RegEx geben, sondern uns auf einige praktische Beispiele konzentrieren, um das Prinzip zu verstehen.

##### Beispiel 1: Deutsche Postleitzahl

Eine deutsche Postleitzahl besteht aus genau fünf Ziffern. Nicht mehr, nicht weniger.

```html
<label for="plz">Postleitzahl:</label>
<input type="text" id="plz" name="plz" pattern="\d{5}" title="Bitte geben Sie eine 5-stellige Postleitzahl ein." required>
```

Schauen wir uns den RegEx `\d{5}` genauer an:
*   `\d` steht für eine beliebige Ziffer (digit) von 0-9.
*   `{5}` ist ein Quantifizierer und bedeutet „exakt fünfmal“.

Zusammengesetzt bedeutet der Ausdruck also: "Erwarte exakt fünf Ziffern."

Beachte das `title`-Attribut! Es ist hier von entscheidender Bedeutung. Wenn die Eingabe des Nutzers nicht dem Muster entspricht, zeigt der Browser eine Standardfehlermeldung wie „Bitte passen Sie das Format an“. Das ist für den Nutzer völlig nutzlos. Der Inhalt des `title`-Attributs wird jedoch in der Fehlermeldung angezeigt und gibt dem Nutzer einen klaren Hinweis darauf, was von ihm erwartet wird. **Ein `pattern` ohne `title` ist schlechte User Experience.**

##### Beispiel 2: Benutzername mit Einschränkungen

Nehmen wir an, ein Benutzername darf nur aus Kleinbuchstaben, Zahlen und dem Unterstrich bestehen und muss zwischen 4 und 16 Zeichen lang sein.

```html
<label for="custom_user">Benutzername:</label>
<input type="text" id="custom_user" name="custom_user" 
       pattern="[a-z0-9_]{4,16}" 
       title="4-16 Zeichen, nur Kleinbuchstaben, Zahlen und Unterstrich." 
       required>
```

Der RegEx `[a-z0-9_]{4,16}` zerlegt sich wie folgt:
*   `[...]` definiert eine Zeichenklasse. Jedes Zeichen in der Eingabe muss einem der hier aufgeführten Zeichen oder Bereiche entsprechen.
*   `a-z` steht für alle Kleinbuchstaben.
*   `0-9` steht für alle Ziffern.
*   `_` steht für den Unterstrich.
*   `{4,16}` bedeutet "mindestens 4, höchstens 16 Mal".

##### Beispiel 3: Einfache Passwort-Richtlinie

Reguläre Ausdrücke können auch komplexere Regeln prüfen, zum Beispiel ob ein Passwort mindestens einen Großbuchstaben, einen Kleinbuchstaben und eine Zahl enthält.

```html
<label for="complex_pass">Neues Passwort:</label>
<input type="password" id="complex_pass" name="complex_pass"
       pattern="(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}"
       title="Mindestens 8 Zeichen, ein Großbuchstabe, ein Kleinbuchstabe und eine Zahl."
       minlength="8" required>
```

Dieser RegEx ist schon fortgeschrittener und nutzt sogenannte "positive lookaheads" `(?=...)`. Jeder dieser Blöcke prüft, ob eine Bedingung erfüllt ist, ohne dabei Zeichen zu "verbrauchen":
*   `(?=.*[a-z])` prüft, ob irgendwo in der Zeichenkette ein Kleinbuchstabe vorkommt.
*   `(?=.*[A-Z])` prüft, ob irgendwo ein Großbuchstabe vorkommt.
*   `(?=.*\d)` prüft, ob irgendwo eine Ziffer vorkommt.
*   `.{8,}` prüft am Ende, ob die gesamte Zeichenkette aus mindestens 8 beliebigen Zeichen (`.`) besteht.

Hier kombinieren wir `pattern` sogar mit `minlength`, was eine gute Praxis ist. `minlength` gibt eine sofort verständliche Längenprüfung, während `pattern` die komplexeren Inhaltsregeln validiert.

Mit diesen Attributen – `required`, `min/maxlength`, `min/max` und `pattern` – hast du bereits ein robustes Set an Werkzeugen, um deine Formulare intelligenter, sicherer und vor allem benutzerfreundlicher zu gestalten. Sie sind die stillen Wächter, die für eine reibungslose Interaktion und saubere Daten sorgen.
