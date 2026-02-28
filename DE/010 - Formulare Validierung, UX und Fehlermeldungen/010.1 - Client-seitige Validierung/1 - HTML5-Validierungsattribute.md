# HTML5-Validierungsattribute

### HTML5-Validierungsattribute: Die erste Verteidigungslinie

Stell dir vor, du füllst ein langes Online-Formular aus, klickst auf „Senden“ und erst nach einer spürbaren Ladezeit teilt dir der Server mit, dass du im Feld für die Postleitzahl Buchstaben verwendet hast. Frustrierend, oder? Genau hier setzt die client-seitige Validierung an. Sie ist die erste, unmittelbare Prüfung der Benutzereingaben, die direkt im Browser stattfindet, noch bevor irgendetwas an den Server geschickt wird.

HTML5 hat diesen Prozess revolutioniert, indem es eine Reihe von Attributen eingeführt hat, mit denen du Validierungsregeln direkt in dein HTML einbetten kannst – ganz ohne eine einzige Zeile JavaScript. Diese Attribute sind einfach zu verwenden, verbessern die Benutzererfahrung (User Experience, UX) erheblich und bilden eine solide Grundlage für die Datensicherheit. Lass uns diese nützlichen Helfer im Detail ansehen.

#### Das `required`-Attribut: Die absolute Grundlage

Das wohl einfachste und am häufigsten verwendete Validierungsattribut ist `required`. Wenn du dieses Attribut zu einem Formularfeld hinzufügst, signalisierst du dem Browser, dass dieses Feld nicht leer bleiben darf. Der Benutzer muss einen Wert eingeben, damit das Formular erfolgreich abgeschickt werden kann.

Es handelt sich um ein sogenanntes boolesches Attribut. Das bedeutet, es muss nur vorhanden sein; ein Wert ist nicht notwendig.

```html
<form action="/registrieren" method="post">
  <label for="username">Benutzername:</label>
  <input type="text" id="username" name="username" required>

  <label for="email">E-Mail:</label>
  <input type="email" id="email" name="email" required>
  
  <button type="submit">Account erstellen</button>
</form>
```

Versucht ein Benutzer, dieses Formular mit einem leeren Benutzernamen- oder E-Mail-Feld abzuschicken, wird der Browser den Vorgang blockieren und eine Standard-Fehlermeldung anzeigen, die auf das betreffende Feld hinweist.

#### Längenbeschränkungen: `minlength` und `maxlength`

Oft reicht es nicht aus, nur zu wissen, *dass* etwas eingegeben wurde. Manchmal muss die Eingabe auch eine bestimmte Länge haben. Hierfür gibt es `minlength` und `maxlength`.

*   `minlength`: Legt die minimale Anzahl von Zeichen fest, die ein Feld enthalten muss.
*   `maxlength`: Definiert die maximale Anzahl von Zeichen.

Diese Attribute sind besonders nützlich für Benutzernamen, Passwörter oder Textnachrichten.

```html
<label for="password">Passwort:</label>
<input type="password" id="password" name="password" minlength="8" required>
<small>Dein Passwort muss mindestens 8 Zeichen lang sein.</small>

<label for="bio">Kurzbiografie:</label>
<textarea id="bio" name="bio" maxlength="500"></textarea>
<small>Maximal 500 Zeichen erlaubt.</small>
```

Im Beispiel muss das Passwortfeld nicht nur ausgefüllt sein (`required`), sondern auch mindestens 8 Zeichen enthalten. `maxlength` hat einen zusätzlichen Effekt: Die meisten Browser hindern den Benutzer physisch daran, mehr Zeichen einzugeben, als erlaubt sind.

#### Wertebereiche: `min`, `max` und `step`

Während `minlength` und `maxlength` die Anzahl der Zeichen zählen, beziehen sich `min`, `max` und `step` auf den numerischen Wert der Eingabe. Sie sind daher ideal für `input`-Felder vom Typ `number`, `range`, `date`, `time` und ähnliche.

*   `min`: Gibt den kleinsten erlaubten Wert an.
*   `max`: Gibt den größten erlaubten Wert an.
*   `step`: Definiert die erlaubten Intervalle (z. B. nur gerade Zahlen oder Schritte von 0.5).

```html
<label for="age">Dein Alter:</label>
<input type="number" id="age" name="age" min="18" max="120" required>

<label for="quantity">Anzahl (in 5er-Schritten):</label>
<input type="number" id="quantity" name="quantity" min="5" max="50" step="5">
```

Hier stellt der Browser sicher, dass das Alter zwischen 18 und 120 liegt und die Anzahl ein Vielfaches von 5 innerhalb des angegebenen Bereichs ist. Bei `input type="date"` könntest du `min` und `max` verwenden, um einen gültigen Datumsbereich festzulegen.

#### Typ-basierte Validierung: Mehr als nur ein `type`

Eine der stärksten Formen der HTML5-Validierung ist bereits im `type`-Attribut selbst eingebaut. Indem du einen spezifischen Typ für dein `input`-Feld wählst, aktivierst du automatisch eine eingebaute Prüfung des Formats.

Die wichtigsten Typen mit integrierter Validierung sind:

*   `type="email"`: Der Browser prüft, ob die Eingabe einem grundlegenden E-Mail-Format entspricht (z. B. ob ein `@`-Zeichen und ein Punkt in der Domain vorhanden sind). Dies ist keine Garantie für eine existierende E-Mail-Adresse, aber es fängt offensichtliche Tippfehler wie „maxmustermann“ ab.
*   `type="url"`: Hier wird überprüft, ob die Eingabe wie eine gültige URL aussieht (z. B. ob sie mit `http://`, `https://` oder `ftp://` beginnt).
*   `type="number"`: Erlaubt nur die Eingabe von Zahlen. Auf Mobilgeräten wird oft sogar eine numerische Tastatur angezeigt.

```html
<label for="user-email">Deine E-Mail:</label>
<input type="email" id="user-email" name="user-email" required>

<label for="website">Deine Webseite:</label>
<input type="url" id="website" name="website">
```

Die Verwendung des korrekten `type` ist nicht nur für die Validierung, sondern auch für die Benutzerfreundlichkeit und Barrierefreiheit von enormer Bedeutung.

#### Eigene Regeln mit `pattern`: Der Joker unter den Attributen

Was aber, wenn deine Anforderungen spezifischer sind? Vielleicht möchtest du eine deutsche Postleitzahl (genau 5 Ziffern) oder einen Benutzernamen, der nur Kleinbuchstaben und Zahlen enthalten darf. Hier kommt das `pattern`-Attribut ins Spiel.

Mit `pattern` kannst du eine **Regulären Ausdruck (Regular Expression)** definieren, dem die Eingabe entsprechen muss. Reguläre Ausdrücke sind eine mächtige Mini-Sprache zur Beschreibung von Zeichenmustern.

Wenn du `pattern` verwendest, ist es dringend empfohlen, auch das `title`-Attribut zu setzen. Der Inhalt des `title`-Attributs wird dem Benutzer oft als Teil der Fehlermeldung angezeigt und sollte erklären, welches Format erwartet wird.

```html
<label for="plz">Postleitzahl:</label>
<input type="text" 
       id="plz" 
       name="plz" 
       pattern="[0-9]{5}" 
       title="Bitte gib eine 5-stellige Postleitzahl ein." 
       required>

<label for="custom-username">Benutzername:</label>
<input type="text" 
       id="custom-username" 
       name="custom-username" 
       pattern="[a-z0-9]{4,15}" 
       title="Nur Kleinbuchstaben und Zahlen, 4-15 Zeichen lang." 
       required>
```

Im ersten Beispiel prüft `pattern="[0-9]{5}"`, ob genau fünf Ziffern eingegeben wurden. Im zweiten Beispiel sorgt `pattern="[a-z0-9]{4,15}"` dafür, dass der Benutzername zwischen 4 und 15 Zeichen lang ist und nur aus Kleinbuchstaben und Zahlen besteht.

#### Validierung steuern: `novalidate` und `formnovalidate`

Manchmal möchtest du die Standard-Browser-Validierung gezielt ausschalten. Ein typischer Anwendungsfall ist eine Funktion zum „Speichern als Entwurf“. Hier sollen die Daten an den Server gesendet werden, auch wenn das Formular noch nicht vollständig oder gültig ist.

*   `novalidate`: Dieses boolesche Attribut wird dem `<form>`-Tag hinzugefügt und deaktiviert die HTML5-Validierung für das gesamte Formular.

```html
<form action="/speichern" method="post" novalidate>
  <!-- Alle Felder in diesem Formular werden nicht automatisch validiert -->
  <button type="submit">Formular ohne Validierung senden</button>
</form>
```

*   `formnovalidate`: Dieses Attribut wird einem Senden-Button (`<button type="submit">` oder `<input type="submit">`) hinzugefügt. Es überschreibt die Validierungseinstellung des Formulars nur für diesen einen Klick. Das ist perfekt, um mehrere Aktionen in einem Formular zu ermöglichen.

```html
<form action="/prozess" method="post">
  <label for="titel">Titel:</label>
  <input type="text" id="titel" name="titel" required>

  <!-- Dieser Button löst die normale Validierung aus -->
  <button type="submit">Veröffentlichen</button>

  <!-- Dieser Button umgeht die Validierung -->
  <button type="submit" formnovalidate formaction="/entwurf-speichern">
    Als Entwurf speichern
  </button>
</form>
```

Im obigen Beispiel wird beim Klick auf „Veröffentlichen“ geprüft, ob das Titelfeld ausgefüllt ist. Beim Klick auf „Als Entwurf speichern“ wird das Formular jedoch ohne Prüfung an die alternative URL `/entwurf-speichern` gesendet.

#### Visuelles Feedback: Validierung mit CSS gestalten

Ein großer Vorteil der HTML5-Validierungsattribute ist, dass sie nahtlos mit CSS zusammenspielen. Der Browser vergibt automatisch sogenannte Pseudo-Klassen an Formularfelder, je nachdem, in welchem Zustand sie sich befinden.

*   `:valid`: Das Feld ist gültig gemäß seinen Validierungsregeln.
*   `:invalid`: Das Feld ist ungültig.
*   `:required`: Das Feld hat das `required`-Attribut.
*   `:optional`: Das Feld ist nicht `required`.

Mit diesen Klassen kannst du dem Benutzer sofortiges visuelles Feedback geben.

```css
/* Grundlegende Stile für Input-Felder */
input {
  border: 2px solid #ccc;
  border-radius: 4px;
  padding: 8px;
  transition: border-color 0.3s;
}

/* Stil für ungültige Felder, nachdem der Benutzer damit interagiert hat */
input:invalid {
  border-color: #e74c3c; /* Ein auffälliges Rot */
}

/* Stil für gültige Felder */
input:valid {
  border-color: #2ecc71; /* Ein freundliches Grün */
}

/* Optional: Kein grüner Rahmen für leere, optionale Felder */
input:optional:placeholder-shown {
    border-color: #ccc;
}
```

Dieser CSS-Code sorgt dafür, dass ein Feld eine rote Umrandung erhält, sobald seine Eingabe ungültig ist, und eine grüne, wenn sie gültig wird. Dies ist eine enorme Hilfe für den Benutzer, um Fehler schnell zu erkennen und zu korrigieren.

#### Die Grenzen kennen

HTML5-Validierungsattribute sind ein fantastisches Werkzeug. Sie sind deklarativ, performant und verbessern die UX ohne komplexen Code. Es ist jedoch entscheidend, ihre Grenzen zu verstehen:

1.  **Sicherheit:** Client-seitige Validierung ist reiner Komfort für den Benutzer. Sie kann von einem technisch versierten Angreifer leicht umgangen werden. **Du musst alle Daten ausnahmslos immer auch auf dem Server validieren.** Betrachte die Server-Validierung als die eigentliche Sicherheitskontrolle und die HTML5-Validierung als freundlichen Hinweis für ehrliche Benutzer.
2.  **Browser-Unterschiede:** Das Aussehen der Fehlermeldungen und das exakte Verhalten können sich von Browser zu Browser unterscheiden.
3.  **Komplexität:** Für sehr komplexe, kontextabhängige Regeln (z. B. „Feld B ist nur erforderlich, wenn in Feld A der Wert ‚Ja‘ ausgewählt wurde“) stößt die reine HTML-Validierung an ihre Grenzen. Hierfür benötigst du weiterhin JavaScript.

Trotz dieser Einschränkungen bilden die HTML5-Validierungsattribute das Fundament einer jeden guten Formular-Validierung. Sie sind die erste Verteidigungslinie gegen fehlerhafte Eingaben und ein unverzichtbarer Baustein für moderne, benutzerfreundliche Webanwendungen.
