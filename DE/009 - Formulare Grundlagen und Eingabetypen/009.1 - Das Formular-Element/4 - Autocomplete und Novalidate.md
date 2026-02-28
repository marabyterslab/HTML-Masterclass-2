# Autocomplete und Novalidate

### Autocomplete und Novalidate: Intelligente Helfer und bewusste Kontrolle

Wenn du ein Formular erstellst, interagierst du nicht nur mit dem Code, den du schreibst, sondern auch mit der Intelligenz des Webbrowsers. Moderne Browser sind darauf ausgelegt, dem Nutzer das Leben so einfach wie möglich zu machen. Sie merken sich Eingaben, validieren Daten und versuchen, Fehler zu verhindern. Doch manchmal möchtest du als Entwickler die volle Kontrolle darüber haben, was passiert. Genau hier kommen die Attribute `autocomplete` und `novalidate` ins Spiel. Sie sind wie Schalter, mit denen du das Standardverhalten des Browsers für deine Formulare feinjustieren kannst.

#### Das `autocomplete`-Attribut: Der hilfsbereite Assistent

Bestimmt kennst du das: Du fängst an, deinen Namen in ein Formularfeld zu tippen, und der Browser schlägt dir sofort deinen vollen Namen, deine E-Mail-Adresse oder sogar deine komplette Anschrift vor. Das ist die `autocomplete`-Funktion in Aktion. Sie ist ein Segen für die Benutzerfreundlichkeit, denn sie spart Zeit, reduziert Tippfehler und senkt die Hürde, ein Formular auszufüllen – besonders auf mobilen Geräten.

Standardmäßig ist diese Funktion für die meisten Formulare aktiviert (`autocomplete="on"`). Der Browser versucht, anhand von Attributen wie `name`, `id` und `label` zu erraten, welche Art von Information in ein Feld gehört, und bietet dann passende, zuvor gespeicherte Daten an.

Manchmal möchtest du dieses Verhalten jedoch unterbinden. Vielleicht handelt es sich um ein Formular mit sehr sensiblen Daten, wie einem Einmal-Passwort oder einer Transaktionsnummer, bei dem eine automatische Vervollständigung ein Sicherheitsrisiko darstellen könnte. Oder du hast eine eigene, JavaScript-basierte Autocomplete-Lösung implementiert, die mit der des Browsers in Konflikt geraten würde.

In solchen Fällen kannst du die Autocomplete-Funktion für das gesamte Formular deaktivieren:

```html
<form action="/login" method="post" autocomplete="off">
  <label for="username">Benutzername:</label>
  <input type="text" id="username" name="username">

  <label for="pass">Passwort:</label>
  <input type="password" id="pass" name="password">

  <button type="submit">Anmelden</button>
</form>
```

Mit `autocomplete="off"` im öffnenden `<form>`-Tag teilst du dem Browser mit, dass er für kein einziges Feld in diesem Formular Vorschläge machen soll.

Ein wichtiger Hinweis aus der Praxis: Moderne Browser nehmen sich manchmal die Freiheit, `autocomplete="off"` zu ignorieren, insbesondere bei Anmeldeformularen (Benutzername und Passwort). Sie tun dies im Interesse des Nutzers, der seine Anmeldedaten oft bequem über den integrierten Passwort-Manager verwalten möchte. Vollständige Kontrolle ist hier also nicht immer garantiert.

##### Feingranulare Steuerung auf Feldebene

Die wahre Stärke von `autocomplete` zeigt sich, wenn du dem Browser präzise Anweisungen gibst, welche Daten in welches Feld gehören. Anstatt die Funktion nur an- oder auszuschalten, kannst du für jedes `<input>`-Element ein spezifisches "Token" (eine Art Stichwort) angeben, das die erwartete Information beschreibt. Dadurch wird die automatische Vervollständigung nicht nur aktiviert, sondern auch extrem treffsicher.

Stell dir ein Registrierungs- oder Bestellformular vor. Hier kannst du dem Browser genau sagen, wo der Vorname, die Straße oder die Kreditkartennummer hingehört.

Hier ist eine Liste der gängigsten und nützlichsten `autocomplete`-Werte:

*   **`name`**: Der vollständige Name.
*   **`given-name`**: Der Vorname.
*   **`family-name`**: Der Nachname.
*   **`email`**: Eine E-Mail-Adresse.
*   **`username`**: Ein Benutzername oder Account-Name.
*   **`new-password`**: Ein neues Passwort. Ideal für Registrierungen oder "Passwort ändern"-Formulare, um zu verhindern, dass der Browser das *alte* Passwort einfügt.
*   **`current-password`**: Das aktuelle Passwort des Nutzers. Nützlich für Anmeldeformulare oder zur Bestätigung von Änderungen.
*   **`tel`**: Eine vollständige Telefonnummer.
*   **`street-address`**: Die vollständige Straße mit Hausnummer.
*   **`address-line1`**, **`address-line2`**: Einzelne Adresszeilen.
*   **`postal-code`**: Die Postleitzahl.
*   **`city`**: Der Ort oder die Stadt.
*   **`country`**: Das Land.
*   **`cc-name`**: Der Name auf der Kreditkarte.
*   **`cc-number`**: Die Kreditkartennummer.
*   **`cc-exp-month`**, **`cc-exp-year`**: Ablaufmonat und -jahr der Kreditkarte.
*   **`cc-csc`**: Der Sicherheitscode der Karte (CVC/CVV).

Lass uns das in einem komplexeren Beispiel ansehen. Dieses Formular für eine Lieferadresse gibt dem Browser perfekte Hinweise:

```html
<form action="/bestellen" method="post" autocomplete="on">
  <fieldset>
    <legend>Lieferadresse</legend>

    <label for="vorname">Vorname:</label>
    <input type="text" id="vorname" name="vorname" autocomplete="given-name">

    <label for="nachname">Nachname:</label>
    <input type="text" id="nachname" name="nachname" autocomplete="family-name">

    <label for="strasse">Straße & Hausnummer:</label>
    <input type="text" id="strasse" name="strasse" autocomplete="street-address">

    <label for="plz">PLZ:</label>
    <input type="text" id="plz" name="plz" autocomplete="postal-code">

    <label for="ort">Ort:</label>
    <input type="text" id="ort" name="ort" autocomplete="city">

    <label for="land">Land:</label>
    <input type="text" id="land" name="land" autocomplete="country">
  </fieldset>

  <button type="submit">Bestellung abschließen</button>
</form>
```

Durch die Verwendung dieser spezifischen Werte hilfst du dem Browser, die im Nutzerprofil gespeicherten Daten exakt zuzuordnen. Das Ergebnis ist ein Formular, das sich für den Nutzer fast wie von selbst ausfüllt – ein enormer Gewinn für die Konversionsrate und die Zufriedenheit.

#### Das `novalidate`-Attribut: Wenn du die Regeln selbst machst

HTML5 hat eine eingebaute Formularvalidierung eingeführt. Attribute wie `required`, `minlength`, `pattern` oder Typen wie `type="email"` ermöglichen es dem Browser, die Eingaben eines Nutzers zu überprüfen, *bevor* das Formular überhaupt an den Server gesendet wird. Wenn ein Nutzer versucht, ein Formular mit einem leeren Pflichtfeld abzusenden, blockiert der Browser den Vorgang und zeigt eine standardisierte Fehlermeldung an.

Das ist fantastisch für einfache Anwendungsfälle und sorgt für eine grundlegende Datenqualität, ohne dass du eine einzige Zeile JavaScript schreiben musst.

Aber was ist, wenn dir das Standardverhalten nicht ausreicht? Vielleicht möchtest du:
*   Fehlermeldungen, die perfekt zum Design deiner Webseite passen.
*   Eine Validierung, die schon während der Eingabe stattfindet (Live-Validierung).
*   Komplexere Validierungsregeln, die von den Werten in anderen Feldern abhängen.

In all diesen Fällen wirst du die Validierung wahrscheinlich selbst mit JavaScript implementieren wollen. Und genau hier stört die eingebaute Browser-Validierung, denn sie würde deiner eigenen Logik zuvorkommen.

Um die Browser-Validierung für ein komplettes Formular zu deaktivieren, fügst du dem `<form>`-Element das `novalidate`-Attribut hinzu. Es handelt sich um ein sogenanntes boolesches Attribut, seine reine Anwesenheit schaltet die Funktion aus.

```html
<form action="/registrieren" method="post" novalidate>
  <label for="mail">E-Mail (erforderlich):</label>
  <input type="email" id="mail" name="user_email" required>

  <label for="pw">Passwort (min. 8 Zeichen):</label>
  <input type="password" id="pw" name="user_password" required minlength="8">

  <button type="submit">Konto erstellen</button>
</form>
```

In diesem Beispiel sind die Felder mit `required` und `minlength` deklariert. Ohne `novalidate` würde der Browser das Absenden mit einer ungültigen E-Mail-Adresse oder einem zu kurzen Passwort verhindern. Mit `novalidate` wird das Formular jedoch ohne Prüfung an den Server geschickt. Dies gibt dir die Freiheit, mit JavaScript auf das `submit`-Ereignis zu hören, deine eigene Validierungslogik auszuführen und benutzerdefinierte Fehlermeldungen anzuzeigen, falls die Daten nicht korrekt sind.

##### Gezielte Deaktivierung mit `formnovalidate`

Es gibt auch Situationen, in denen du die Validierung nur für eine bestimmte Aktion innerhalb des Formulars umgehen möchtest. Ein klassisches Beispiel ist eine "Als Entwurf speichern"-Funktion. Der Nutzer soll seinen Fortschritt speichern können, auch wenn noch nicht alle Pflichtfelder ausgefüllt sind. Die endgültige "Absenden"-Aktion soll jedoch weiterhin validiert werden.

Dafür gibt es das `formnovalidate`-Attribut, das du direkt auf einen Senden-Button (`<button type="submit">` oder `<input type="submit">`) anwenden kannst.

```html
<form action="/artikel" method="post">
  <label for="titel">Titel:</label>
  <input type="text" id="titel" name="titel" required>

  <label for="inhalt">Inhalt:</label>
  <textarea id="inhalt" name="inhalt" required rows="10"></textarea>

  <!-- Dieser Button umgeht die Validierung -->
  <button type="submit" name="aktion" value="speichern" formnovalidate>
    Als Entwurf speichern
  </button>

  <!-- Dieser Button löst die normale Validierung aus -->
  <button type="submit" name="aktion" value="veroeffentlichen">
    Veröffentlichen
  </button>
</form>
```

Wenn der Nutzer auf "Als Entwurf speichern" klickt, wird das Formular gesendet, selbst wenn Titel und Inhalt leer sind. Klickt er hingegen auf "Veröffentlichen", greift die `required`-Prüfung des Browsers, und das Formular wird nur bei korrekter Befüllung abgeschickt.

Zusammenfassend lässt sich sagen, dass `autocomplete` und `novalidate` zwei mächtige Werkzeuge sind, um das Zusammenspiel zwischen Nutzer, Browser und deinem Formular zu steuern. Mit `autocomplete` gibst du dem Browser gezielte Hinweise, um dem Nutzer bestmöglich zu assistieren. Mit `novalidate` nimmst du dem Browser die Kontrolle über die Datenprüfung ab, um sie nach deinen eigenen, präzisen Vorstellungen umzusetzen.
