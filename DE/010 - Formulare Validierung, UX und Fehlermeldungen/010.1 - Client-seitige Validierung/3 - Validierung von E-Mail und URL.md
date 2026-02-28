# Validierung von E-Mail und URL

### Validierung von E-Mail und URL

In der Welt der Formulare gibt es einige Eingabefelder, die fast allgegenwärtig sind: E-Mail-Adressen und Web-Adressen (URLs). Anders als ein einfacher Name oder eine Freitext-Nachricht folgen diese Eingaben einem ganz bestimmten Muster. Eine E-Mail-Adresse ohne ein `@`-Zeichen ist keine E-Mail-Adresse. Eine URL ohne einen Domain-Namen ist keine URL. Deine Aufgabe als Entwickler ist es, dem Nutzer dabei zu helfen, diese Daten korrekt einzugeben. Die client-seitige Validierung ist hierfür dein erstes und wichtigstes Werkzeug, denn sie gibt sofortiges Feedback, lange bevor die Daten überhaupt zum Server geschickt werden.

#### E-Mail-Adressen: Mehr als nur ein @-Zeichen

Fast jedes Registrierungs- oder Kontaktformular fragt nach einer E-Mail-Adresse. Die Validierung dieser Eingabe ist entscheidend, denn eine falsch eingegebene Adresse bedeutet, dass du den Nutzer nicht kontaktieren kannst.

##### Die einfache HTML5-Lösung: `type="email"`

HTML5 macht uns das Leben leicht und bietet einen speziellen `input`-Typ nur für E-Mail-Adressen. Wenn du ihn verwendest, übernimmt der Browser einen Teil der Validierungsarbeit für dich.

```html
<form>
  <label for="email">Deine E-Mail-Adresse:</label>
  <input type="email" id="email" name="user_email" required>
  <button type="submit">Senden</button>
</form>
```

Das Tolle daran ist, dass du fast nichts tun musst. Wenn ein Nutzer versucht, das Formular mit einer Eingabe wie "mein-name" abzusenden, wird der Browser den Versand blockieren und eine Standard-Fehlermeldung anzeigen, die etwa lautet: "Bitte geben Sie eine E-Â­Mail-Â­Adresse ein."

Was genau prüft der Browser hier? Er führt eine relativ einfache Musterprüfung durch. Im Grunde schaut er, ob die Eingabe dem groben Schema `etwas@etwas.etwas` entspricht. Er prüft also, ob ein `@`-Zeichen vorhanden ist, das nicht am Anfang oder Ende steht, und ob nach dem `@` mindestens ein Punkt folgt.

**Vorteile von `type="email"`:**

1.  **Einfachheit:** Es ist nur ein Attribut, kein JavaScript erforderlich.
2.  **Gute User Experience (UX):** Auf mobilen Geräten wird oft eine spezielle Tastatur angezeigt, die das `@`- und das `.`-Zeichen prominent platziert.
3.  **Barrierefreiheit:** Screenreader erkennen das Feld als E-Mail-Eingabefeld.

**Die Grenzen der HTML5-Validierung:**

Die browser-eigene Prüfung ist zwar praktisch, aber nicht narrensicher. Eine Eingabe wie `a@b.c` würde sie als gültig akzeptieren, obwohl eine solche Adresse in der Praxis kaum existiert. Sie prüft nur das Format, nicht, ob die Domain tatsächlich existiert oder ob das Postfach erreichbar ist. Das ist aber auch nicht ihre Aufgabe. Die client-seitige Validierung soll offensichtliche Tippfehler abfangen, nicht die Existenz einer E-Mail-Adresse verifizieren. Für Letzteres wäre ohnehin ein serverseitiger Prozess nötig (z. B. das Versenden einer Bestätigungs-E-Mail).

##### Feinere Kontrolle mit JavaScript und Regulären Ausdrücken

Manchmal reichen die Bordmittel von HTML5 nicht aus oder du möchtest eine eigene, spezifischere Fehlermeldung anzeigen. In diesem Fall greifst du zu JavaScript. Das mächtigste Werkzeug zur Mustererkennung in Zeichenketten sind **Reguläre Ausdrücke** (oft als "Regex" abgekürzt).

Ein Regulärer Ausdruck ist eine Mini-Sprache, mit der du komplexe Suchmuster definieren kannst. Die perfekte Regex für E-Mail-Adressen, die alle theoretischen Fälle abdeckt, ist ein berüchtigt komplexes Ungetüm. Für die Praxis genügt jedoch meist ein pragmatischer Ansatz, der 99,9 % aller gängigen Adressen korrekt erkennt.

Hier ist ein gängiges und solides Regex-Muster für E-Mail-Adressen:

```javascript
const emailRegex = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
```

Lassen wir uns davon nicht einschüchtern. Das bedeutet im Klartext:
*   `^`: Der Anfang der Zeichenkette.
*   `[a-zA-Z0-9._%+-]+`: Der Teil vor dem `@`. Er darf Buchstaben, Zahlen und die Sonderzeichen `._%+-` enthalten. Das `+` bedeutet "ein oder mehrere Male".
*   `@`: Das literale `@`-Zeichen.
*   `[a-zA-Z0-9.-]+`: Der Domain-Name. Er darf Buchstaben, Zahlen, Punkte und Bindestriche enthalten.
*   `\.`: Ein literaler Punkt. Der Backslash ist nötig, da der Punkt in Regex eine Sonderbedeutung hat.
*   `[a-zA-Z]{2,}`: Die Top-Level-Domain (wie `.com`, `.de`). Sie muss aus mindestens zwei Buchstaben bestehen.
*   `$`: Das Ende der Zeichenkette.

Die Überprüfung in JavaScript könnte dann so aussehen:

```html
<form id="contact-form">
  <label for="email-js">Deine E-Mail-Adresse:</label>
  <input type="email" id="email-js" name="user_email">
  <p id="email-error" style="color: red; display: none;">Bitte gib eine gültige E-Mail-Adresse ein.</p>
  <button type="submit">Senden</button>
</form>

<script>
  const form = document.getElementById('contact-form');
  const emailInput = document.getElementById('email-js');
  const emailError = document.getElementById('email-error');

  // Ein pragmatisches Regex-Muster für die E-Mail-Validierung
  const emailRegex = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;

  form.addEventListener('submit', function(event) {
    // Standardverhalten des Formulars (Seite neu laden) verhindern
    event.preventDefault();

    const emailValue = emailInput.value;
    
    if (emailRegex.test(emailValue)) {
      // E-Mail ist gültig
      emailError.style.display = 'none';
      console.log('Formular wird gesendet...');
      // Hier würde die Logik zum Absenden des Formulars folgen
      // form.submit();
    } else {
      // E-Mail ist ungültig
      emailError.style.display = 'block';
    }
  });
</script>
```

In diesem Beispiel fangen wir das `submit`-Event des Formulars ab. Anstatt den Browser die Arbeit machen zu lassen, prüfen wir mit `emailRegex.test(emailValue)` selbst, ob der Wert im Eingabefeld unserem Muster entspricht. Ist das nicht der Fall, zeigen wir unsere eigene Fehlermeldung an und verhindern den Versand.

#### URL-Validierung: Die Tücken des Protokolls

Ähnlich wie bei E-Mails haben auch URLs ein festes Format. Eine typische URL besteht aus einem Protokoll (`http://`, `https://`), einer Domain (`beispiel.de`) und optional einem Pfad, Parametern und mehr.

##### Die HTML5-Lösung: `type="url"`

Auch für URLs gibt es einen dedizierten `input`-Typen, der eine grundlegende Validierung durch den Browser ermöglicht.

```html
<form>
  <label for="website">Deine Webseite:</label>
  <input type="url" id="website" name="user_website" placeholder="https://deine-seite.de">
  <button type="submit">Senden</button>
</form>
```

Wenn ein Nutzer hier `meine-seite.de` eingibt und das Formular absendet, wird der Browser dies als Fehler markieren. Warum? Weil das Protokoll (z.B. `https://`) fehlt. Die Browser-Validierung für `type="url"` ist oft streng und verlangt eine vollständige URL inklusive Protokoll.

Der Haken an der Sache ist die User Experience. Viele Nutzer sind es gewohnt, Adressen ohne `http://` einzugeben. Sie als ungültig zu markieren, kann frustrierend sein. Es ist also eine Abwägungssache: Willst du strikte, vollständige URLs erzwingen oder dem Nutzer mehr Flexibilität bieten?

##### Flexiblere URL-Prüfung mit JavaScript

Wenn du nutzerfreundlicher sein willst, ist JavaScript die bessere Wahl. Du kannst entweder eine flexiblere Regex verwenden oder, noch besser, auf moderne JavaScript-APIs zurückgreifen.

**Ansatz 1: Eine flexiblere Regex**

Eine Regex für URLs kann noch komplexer werden als die für E-Mails. Ein Muster, das gängige Web-Adressen (mit optionalem Protokoll) erkennt, könnte so aussehen:

```javascript
const urlRegex = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/;
```
Diese Regex ist schon toleranter und würde auch `beispiel.com` ohne Protokoll akzeptieren.

**Ansatz 2: Der moderne Weg mit dem `URL`-Konstruktor**

Eine robustere und oft einfachere Methode als komplexe Reguläre Ausdrücke ist die Verwendung des eingebauten `URL`-Konstruktors in JavaScript. Dieser versucht, aus einer Zeichenkette ein URL-Objekt zu erstellen. Schlägt dies fehl, wirft er einen Fehler. Diesen Fehler können wir gezielt abfangen.

```javascript
function isValidUrl(string) {
  try {
    new URL(string);
    return true;
  } catch (error) {
    return false;
  }
}

// Beispiele für die Nutzung:
console.log(isValidUrl('https://www.google.com'));       // true
console.log(isValidUrl('http://beispiel.de/pfad'));     // true
console.log(isValidUrl('google.com'));                  // false -> Wirft Fehler, da kein Protokoll
console.log(isValidUrl('nur Text'));                    // false
```

Der Nachteil ist hier derselbe wie bei `type="url"`: Der `URL`-Konstruktor benötigt ein Protokoll. Wir können ihn aber clever einsetzen, um nutzerfreundlicher zu sein. Eine gängige Strategie ist, zu prüfen, ob die Eingabe bereits mit `http://` oder `https://` beginnt. Wenn nicht, fügen wir es für die Validierung temporär hinzu.

Hier ist ein komplettes Beispiel, das diesen nutzerfreundlichen Ansatz umsetzt:

```html
<form id="website-form">
  <label for="website-js">Deine Webseite:</label>
  <input type="text" id="website-js" name="user_website" placeholder="deine-seite.de">
  <p id="website-error" style="color: red; display: none;">Bitte gib eine gültige Web-Adresse ein.</p>
  <button type="submit">Senden</button>
</form>

<script>
  const websiteForm = document.getElementById('website-form');
  const websiteInput = document.getElementById('website-js');
  const websiteError = document.getElementById('website-error');

  function validateAndNormalizeUrl(string) {
    let urlString = string.trim();
    if (urlString === '') return null; // Leere Eingabe ist nicht gültig

    // Füge https:// hinzu, wenn kein Protokoll vorhanden ist
    if (!urlString.startsWith('http://') && !urlString.startsWith('https://')) {
      urlString = 'https://' + urlString;
    }

    try {
      new URL(urlString);
      return urlString; // Gib die normalisierte, gültige URL zurück
    } catch (error) {
      return null; // Ungültige URL
    }
  }

  websiteForm.addEventListener('submit', function(event) {
    event.preventDefault();
    
    const validatedUrl = validateAndNormalizeUrl(websiteInput.value);

    if (validatedUrl) {
      websiteError.style.display = 'none';
      console.log(`Gültige URL gefunden: ${validatedUrl}`);
      // Du könntest den Wert im Input-Feld sogar aktualisieren:
      // websiteInput.value = validatedUrl;
      // ...und dann das Formular senden.
    } else {
      websiteError.style.display = 'block';
    }
  });
</script>
```

In dieser Implementierung wird eine Eingabe wie `beispiel.de` intern zu `https://beispiel.de` erweitert und dann validiert. Dies schlägt zwei Fliegen mit einer Klappe: Die Eingabe für den Nutzer ist einfach und flexibel, und die Daten, die du am Ende verarbeitest, haben ein konsistentes, gültiges Format.

Ob du nun die einfachen HTML5-Typen oder die flexiblen JavaScript-Methoden wählst, hängt immer vom Kontext und der gewünschten User Experience ab. Die wichtigste Regel bleibt jedoch bestehen: Client-seitige Validierung ist ein Komfort für den Nutzer, kein Sicherheitsmerkmal. Eine serverseitige Überprüfung aller eingehenden Daten ist und bleibt unerlässlich.
