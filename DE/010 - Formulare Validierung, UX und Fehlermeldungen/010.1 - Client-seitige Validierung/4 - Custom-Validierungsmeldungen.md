# Custom-Validierungsmeldungen

### Custom-Validierungsmeldungen: Wenn Standard nicht genug ist

Die automatische Validierung von Formularen durch den Browser ist eine fantastische Sache. Sie nimmt dir eine Menge Arbeit ab und sorgt mit minimalem Aufwand für eine grundlegende Datenqualität. Du kennst sie sicher: die kleinen Sprechblasen, die erscheinen, wenn du eine E-Mail-Adresse falsch eingibst oder ein Pflichtfeld vergisst. Sie sind praktisch, aber sie haben auch ihre Grenzen. Sie sehen in jedem Browser ein wenig anders aus, ihre Sprache hängt von den Browsereinstellungen des Nutzers ab und vor allem sind sie eines: generisch.

Eine Meldung wie "Geben Sie eine E-Mail-Adresse an." ist korrekt, aber nicht besonders persönlich oder hilfreich. Was, wenn du eine freundlichere, markengerechtere oder präzisere Botschaft vermitteln möchtest? Was, wenn deine Webseite mehrsprachig ist und du die volle Kontrolle über die Texte brauchst? Genau hier kommen Custom-Validierungsmeldungen ins Spiel. Sie erlauben dir, die Standard-Meldungen des Browsers durch deine eigenen, maßgeschneiderten Texte zu ersetzen und die Darstellung von Fehlern vollständig selbst zu gestalten.

#### Die Tür zur Kontrolle: Die Constraint Validation API

Um die Validierung selbst in die Hand zu nehmen, musst du mit dem Browser zusammenarbeiten, nicht gegen ihn. Dein Browser stellt dir dafür eine mächtige Sammlung an Werkzeugen zur Verfügung: die **Constraint Validation API**. Das klingt technisch, ist aber im Grunde ein Satz von Eigenschaften und Methoden, die jedes Formularelement besitzt und die du mit JavaScript abfragen und manipulieren kannst.

Die wichtigsten Werkzeuge in diesem Kasten sind:

*   **`validity`**: Dies ist ein Objekt, das den Validierungsstatus eines Elements beschreibt. Es enthält eine Reihe von `true`/`false`-Eigenschaften, wie zum Beispiel:
    *   `valueMissing`: `true`, wenn ein mit `required` markiertes Feld leer ist.
    *   `typeMismatch`: `true`, wenn der Wert nicht dem erwarteten Typ entspricht (z. B. "abc" in einem Feld vom Typ `email`).
    *   `patternMismatch`: `true`, wenn der Wert nicht dem im `pattern`-Attribut definierten regulären Ausdruck entspricht.
    *   `tooShort` oder `tooLong`: `true`, wenn der Text kürzer oder länger als durch `minlength` oder `maxlength` erlaubt ist.
    *   `valid`: `true`, wenn keine der anderen Fehlerbedingungen zutrifft.
*   **`validationMessage`**: Diese Eigenschaft enthält den Text der Fehlermeldung, den der Browser anzeigen würde.
*   **`setCustomValidity(message)`**: Dies ist die entscheidende Methode. Mit ihr kannst du deine eigene Fehlermeldung setzen.

#### Der einfachste Weg: `setCustomValidity`

Die schnellste Methode, um eine eigene Fehlermeldung zu erzeugen, ist die `setCustomValidity()`-Methode. Die Logik ist simpel: Du prüfst eine Bedingung mit JavaScript und wenn sie nicht erfüllt ist, setzt du eine eigene Meldung. Der Browser erkennt, dass eine Custom-Meldung gesetzt wurde und zeigt diese anstelle seiner Standard-Meldung an, wenn das Formular abgeschickt werden soll.

Schauen wir uns das an einem Beispiel für ein Passwortfeld an, das mindestens 8 Zeichen lang sein muss.

```html
<form>
  <label for="password">Passwort (mind. 8 Zeichen):</label>
  <input type="password" id="password" name="password" required minlength="8">
  <button type="submit">Registrieren</button>
</form>

<script>
  const passwordInput = document.getElementById('password');

  passwordInput.addEventListener('input', () => {
    // Zuerst prüfen, ob das Feld überhaupt einen Fehler hat.
    if (passwordInput.validity.tooShort) {
      // Wenn der Fehler "zu kurz" ist, setzen wir unsere eigene Meldung.
      passwordInput.setCustomValidity('Dein Passwort ist ein bisschen kurz geraten. Gib bitte mindestens 8 Zeichen ein.');
    } else {
      // GANZ WICHTIG: Wenn kein Fehler mehr vorliegt, die Meldung wieder löschen!
      passwordInput.setCustomValidity('');
    }
  });
</script>
```

Der entscheidende Punkt in diesem Skript ist die `else`-Bedingung. Wenn du eine Fehlermeldung mit `setCustomValidity()` setzt, bleibt das Feld so lange als ungültig markiert, bis du die Meldung explizit wieder entfernst. Das tust du, indem du einen leeren String übergibst: `setCustomValidity('')`. Vergisst du das, kann der Nutzer sein Formular niemals abschicken, selbst wenn er den Fehler längst korrigiert hat – ein klassischer Fallstrick.

Diese Methode ist gut, aber wir sind immer noch auf die Standard-Sprechblase des Browsers angewiesen. Für die volle Kontrolle über Aussehen und Verhalten der Fehlermeldungen gehen wir einen Schritt weiter.

#### Die vollständige Kontrolle: Eigene Fehlermeldungs-Elemente

Um das Nutzererlebnis (UX) wirklich zu optimieren, wollen wir die Fehlermeldungen direkt in unser Seitendesign integrieren. Statt einer Pop-up-Blase zeigen wir den Fehlertext in einem von uns gestalteten HTML-Element direkt neben oder unter dem betreffenden Eingabefeld an.

Dazu kombinieren wir HTML, CSS und JavaScript.

**1. Die HTML-Struktur**

Zuerst bereiten wir unser HTML vor. Jedes Eingabefeld, das eine benutzerdefinierte Fehlermeldung erhalten kann, bekommt ein eigenes Element, das als Container für die Nachricht dient. Wichtig für die Barrierefreiheit ist, dass wir das Eingabefeld mit seinem Fehlercontainer über das `aria-describedby`-Attribut verknüpfen. So wissen Screenreader, dass dieser Text zum Eingabefeld gehört und können ihn vorlesen.

```html
<form id="signup-form" novalidate>
  <div>
    <label for="email">E-Mail-Adresse:</label>
    <input type="email" id="email" name="email" required aria-describedby="email-error">
    <span id="email-error" class="error-message" aria-live="polite"></span>
  </div>
  
  <div>
    <label for="password">Passwort:</label>
    <input type="password" id="password" name="password" required minlength="8" aria-describedby="password-error">
    <span id="password-error" class="error-message" aria-live="polite"></span>
  </div>

  <button type="submit">Account erstellen</button>
</form>
```

Beachte zwei wichtige Details:
*   Das `<form>`-Element hat das Attribut `novalidate`. Das ist kein Widerspruch! Es weist den Browser an, seine *automatischen Fehlermeldungs-Pop-ups* beim Absenden zu unterdrücken. Die Constraint Validation API im Hintergrund funktioniert aber weiterhin. Wir können also immer noch mit `input.validity` prüfen, ob ein Feld gültig ist.
*   Das `<span>` für die Fehlermeldung hat `aria-live="polite"`. Das sorgt dafür, dass Screenreader die Fehlermeldung vorlesen, sobald sie erscheint, ohne den Nutzer bei der Eingabe zu unterbrechen.

**2. Das CSS-Styling**

Standardmäßig sollen unsere Fehlercontainer unsichtbar sein. Wir geben ihnen eine Klasse (z.B. `error-message`) und machen sie erst sichtbar, wenn wir eine weitere Klasse (z.B. `active`) per JavaScript hinzufügen.

```css
.error-message {
  display: none; /* Standardmäßig unsichtbar */
  color: #d93025;
  font-size: 0.9em;
  margin-top: 5px;
}

.error-message.active {
  display: block; /* Sichtbar machen, wenn aktiv */
}

input:invalid {
  /* Optional: Felder mit Fehlern hervorheben */
  border-color: #d93025;
}
```

**3. Die JavaScript-Logik**

Jetzt kommt das Herzstück. Wir schreiben ein Skript, das die Validierung bei Bedarf durchführt und unsere Fehler-Container mit den richtigen Nachrichten füllt.

Ein guter Ansatz ist es, eine zentrale Funktion zu haben, die ein einzelnes Feld validiert und die Anzeige aktualisiert. Diese Funktion können wir dann sowohl beim Absenden des Formulars für alle Felder aufrufen als auch während der Eingabe für ein einzelnes Feld.

```javascript
const form = document.getElementById('signup-form');
const emailInput = document.getElementById('email');
const passwordInput = document.getElementById('password');

// Funktion zum Anzeigen von Fehlern
function showError(inputElement, message) {
  const errorElement = document.getElementById(inputElement.id + '-error');
  errorElement.textContent = message;
  errorElement.classList.add('active');
}

// Funktion zum Verstecken von Fehlern
function hideError(inputElement) {
  const errorElement = document.getElementById(inputElement.id + '-error');
  errorElement.textContent = '';
  errorElement.classList.remove('active');
}

// Funktion, die die Validierungslogik für ein Feld enthält
function validateField(inputElement) {
  const validity = inputElement.validity;

  if (validity.valid) {
    hideError(inputElement);
    return true;
  }

  if (validity.valueMissing) {
    showError(inputElement, 'Dieses Feld darf nicht leer sein.');
  } else if (validity.typeMismatch) {
    showError(inputElement, 'Bitte gib eine gültige E-Mail-Adresse ein.');
  } else if (validity.tooShort) {
    showError(inputElement, `Das Passwort muss mindestens ${inputElement.minLength} Zeichen lang sein.`);
  } else {
    // Fallback für andere, nicht spezifizierte Fehler
    showError(inputElement, 'Der eingegebene Wert ist ungültig.');
  }
  return false;
}

// Event Listener für das Absenden des Formulars
form.addEventListener('submit', (event) => {
  // Validierung für alle Felder durchführen
  const isEmailValid = validateField(emailInput);
  const isPasswordValid = validateField(passwordInput);

  // Wenn ein Feld ungültig ist, das Absenden verhindern
  if (!isEmailValid || !isPasswordValid) {
    event.preventDefault();
  }
});

// Optionale: Live-Validierung während der Eingabe für eine bessere UX
emailInput.addEventListener('input', () => validateField(emailInput));
passwordInput.addEventListener('input', () => validateField(passwordInput));
```

Was passiert hier genau?

1.  Wir definieren zwei Hilfsfunktionen, `showError` und `hideError`, die sich nur um die Darstellung kümmern. Das hält den Code sauber.
2.  Die Hauptfunktion `validateField` nimmt ein Eingabeelement entgegen und prüft dessen `validity`-Objekt.
3.  Anhand der `true`-Eigenschaft (`valueMissing`, `typeMismatch` etc.) entscheiden wir, welche Fehlermeldung passend ist und rufen `showError` mit dem entsprechenden Text auf.
4.  Wenn das Feld gültig ist (`validity.valid`), rufen wir `hideError` auf, um eine eventuell zuvor angezeigte Meldung zu entfernen.
5.  Beim `submit`-Event des Formulars rufen wir die Validierung für alle unsere Felder auf. Ist auch nur eines davon ungültig, stoppen wir das Absenden des Formulars mit `event.preventDefault()`.
6.  Für ein noch besseres Nutzererlebnis fügen wir `input`-Event-Listener hinzu. Dadurch erhält der Nutzer sofortiges Feedback, sobald er seine Eingabe korrigiert – nicht erst, wenn er erneut versucht, das Formular abzusenden.

Mit diesem Aufbau hast du die volle Kontrolle. Du kannst die Fehlermeldungen formulieren, wie du möchtest, sie mit CSS gestalten, wie es zu deiner Marke passt, und das Verhalten exakt so steuern, dass es für deine Nutzer am hilfreichsten ist. Du nutzt die leistungsstarke, eingebaute Validierungs-Engine des Browsers, verleihst ihr aber eine eigene, benutzerfreundliche Oberfläche.
