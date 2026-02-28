# Button-Typen (submit, reset, button)

### Die drei Musketiere der Formulare: `submit`, `reset` und `button`

Nachdem du nun weißt, wie du mit `<textarea>` größere Textmengen von deinen Nutzern entgegennehmen kannst, kommen wir zu den interaktiven Elementen, die einem Formular erst Leben einhauchen: den Buttons. Ohne sie wäre jedes Formular nur eine Datensammlung ohne Ziel. Ein Button ist der Auslöser, der entscheidende Klick, der eine Aktion startet. In HTML gibt es drei grundlegende Typen von Buttons, die du innerhalb eines Formulars verwenden kannst, jeder mit einer ganz spezifischen Aufgabe. Wir schauen uns `submit`, `reset` und `button` jetzt ganz genau an.

Diese Typen kannst du sowohl mit dem `<input>`-Element als auch mit dem flexibleren `<button>`-Element umsetzen. Wir werden beide Varianten beleuchten.

#### Der `submit`-Button: Das Tor zur Datenverarbeitung

Der `submit`-Button ist der wahrscheinlich wichtigste und am häufigsten verwendete Button in jedem Formular. Seine einzige Aufgabe ist es, die vom Nutzer eingegebenen Formulardaten zu nehmen und sie an die Adresse zu senden, die im `action`-Attribut des umschließenden `<form>`-Elements definiert ist. Er ist der "Senden"-Knopf, der den gesamten Prozess in Gang setzt.

Wenn ein Nutzer auf einen `submit`-Button klickt, tut der Browser Folgendes:
1.  Er sammelt die Daten aus allen Formularfeldern (wie `input`, `textarea`, `select`) innerhalb desselben `<form>`-Tags.
2.  Er verpackt diese Daten gemäß der im `method`-Attribut des Formulars festgelegten Methode (typischerweise `GET` oder `POST`).
3.  Er sendet dieses Datenpaket an die im `action`-Attribut angegebene URL.
4.  Der Browser erwartet eine Antwort vom Server und lädt in der Regel eine neue Seite – entweder die im `action`-Attribut angegebene oder die, die der Server als Antwort schickt.

**Umsetzung mit `<input>`**

Die klassische und einfachste Art, einen Submit-Button zu erstellen, ist mit dem `<input>`-Element:

```html
<form action="/registrierung-verarbeiten" method="post">
  <label for="username">Benutzername:</label>
  <input type="text" id="username" name="username">

  <label for="password">Passwort:</label>
  <input type="password" id="password" name="password">

  <input type="submit" value="Konto erstellen">
</form>
```

Hier ist das Entscheidende `type="submit"`. Der Text auf dem Button wird durch das `value`-Attribut bestimmt. Lässt du `value` weg, zeigt der Browser einen Standardtext an, der je nach Browsersprache variiert (z. B. "Senden" oder "Submit").

**Umsetzung mit `<button>`**

Eine modernere und flexiblere Methode ist die Verwendung des `<button>`-Elements. Der entscheidende Vorteil: Zwischen dem öffnenden `<button>`- und dem schließenden `</button>`-Tag kannst du fast beliebigen HTML-Inhalt platzieren. Das ermöglicht eine viel reichhaltigere Gestaltung.

```html
<form action="/login-verarbeiten" method="post">
  <label for="email">E-Mail:</label>
  <input type="email" id="email" name="email">

  <!-- Ein Button mit fettgedrucktem Text und einem Icon (z.B. als SVG oder Bild) -->
  <button type="submit">
    <strong>Jetzt Einloggen</strong>
    <img src="icon-login.svg" alt="" width="16" height="16">
  </button>
</form>
```

Hier siehst du, dass wir nicht nur Text, sondern auch andere HTML-Elemente wie `<strong>` oder `<img>` innerhalb des Buttons verwenden können. Das gibt dir unendlich viele Möglichkeiten für das Design. Wichtig ist auch hier, dass du `type="submit"` setzt, damit der Button weiß, dass er das Formular absenden soll.

#### Der `reset`-Button: Ein Relikt mit Risiken

Der `reset`-Button hat eine sehr simple Funktion: Er setzt alle Eingabefelder innerhalb des Formulars auf ihren ursprünglichen Zustand zurück. Wenn ein Feld einen vordefinierten Wert im `value`-Attribut hatte, wird dieser wiederhergestellt. Ansonsten werden die Felder einfach geleert.

**Umsetzung mit `<input>` und `<button>`**

```html
<form action="/feedback" method="post">
  <label for="feedback-text">Dein Feedback:</label>
  <textarea id="feedback-text" name="feedback-text" rows="5"></textarea>

  <!-- Umsetzung mit input -->
  <input type="reset" value="Eingaben löschen">

  <!-- Umsetzung mit button -->
  <button type="reset">Formular zurücksetzen</button>
</form>
```

Auch hier gilt: `value` bestimmt den Text bei `<input>`, während der Inhalt zwischen den Tags den Text für `<button>` festlegt.

**Eine wichtige Warnung:** Der `reset`-Button ist heutzutage mit großer Vorsicht zu genießen. In der modernen Webentwicklung wird er kaum noch eingesetzt. Der Grund dafür ist das hohe Frustrationspotenzial für den Nutzer. Stell dir vor, du hast ein langes Formular sorgfältig ausgefüllt und klickst versehentlich auf "Zurücksetzen" statt auf "Senden". All deine Eingaben sind unwiderruflich verloren. Es gibt keine "Bist du sicher?"-Abfrage. Aus Usability-Sicht ist dieser Button daher oft eine schlechte Wahl. Wenn du eine solche Funktion wirklich benötigst, ist es meist besser, sie mit JavaScript und einer zusätzlichen Bestätigungsabfrage umzusetzen.

#### Der `button`-Button: Dein programmierbarer Helfer

Jetzt wird es spannend. Was macht ein Button mit `type="button"`? Die Antwort ist einfach: Nichts. Zumindest nichts von sich aus. Er sendet kein Formular ab und er setzt auch keines zurück. Er ist ein neutraler, programmierbarer Button, der auf eine Anweisung wartet.

Seine wahre Stärke entfaltet er erst im Zusammenspiel mit JavaScript. Du gibst ihm eine Aufgabe, die er ausführen soll, wenn jemand auf ihn klickt. Das macht ihn unglaublich vielseitig für Aktionen, die direkt auf der Seite stattfinden sollen, ohne dass Daten an einen Server gesendet werden müssen.

Mögliche Anwendungsfälle sind:
*   Ein Dialogfenster (Modal) öffnen oder schließen.
*   Zusätzliche Formularfelder ein- oder ausblenden.
*   Eine Berechnung auf der Seite durchführen (z. B. in einem Preisrechner).
*   Daten über JavaScript an einen Server senden, ohne die Seite neu zu laden (sogenannte AJAX- oder Fetch-Requests).
*   Eine clientseitige Validierung der Formulareingaben anstoßen.

**Umsetzung und Beispiel mit JavaScript**

```html
<form>
  <label for="zahl1">Zahl 1:</label>
  <input type="number" id="zahl1">

  <label for="zahl2">Zahl 2:</label>
  <input type="number" id="zahl2">

  <p>Ergebnis: <span id="ergebnis"></span></p>

  <!-- Ein neutraler Button, der eine JavaScript-Funktion aufruft -->
  <button type="button" id="berechnen-btn">Berechnen</button>
</form>

<script>
  // Wir holen uns den Button und das Ergebnis-Element
  const berechnenButton = document.querySelector('#berechnen-btn');
  const ergebnisSpan = document.querySelector('#ergebnis');

  // Wir fügen ein Klick-Event hinzu
  berechnenButton.addEventListener('click', function() {
    // Werte aus den Input-Feldern auslesen
    const zahl1 = parseFloat(document.querySelector('#zahl1').value) || 0;
    const zahl2 = parseFloat(document.querySelector('#zahl2').value) || 0;

    // Berechnung durchführen und Ergebnis anzeigen
    const summe = zahl1 + zahl2;
    ergebnisSpan.textContent = summe;
  });
</script>
```

In diesem Beispiel passiert alles direkt im Browser. Der `button` mit `type="button"` ist der Auslöser für unser JavaScript, aber er würde niemals das Formular absenden.

#### Eine wichtige Regel: Der `type` bei `<button>`

Du hast gesehen, dass das `<button>`-Element sehr flexibel ist. Aber es birgt eine kleine Falle, über die viele Anfänger stolpern. Wenn du bei einem `<button>`-Element innerhalb eines `<form>`-Tags das `type`-Attribut komplett weglässt, was passiert dann?

```html
<!-- Achtung: Was macht dieser Button? -->
<form action="/suche" method="get">
  <input type="search" name="q">
  <button>Suchen</button>
</form>
```

Die Antwort ist: In den meisten Browsern verhält sich dieser Button wie ein `<button type="submit">`. Er wird also das Formular absenden. Das kann zu unerwartetem Verhalten führen, wenn du eigentlich einen neutralen JavaScript-Button erstellen wolltest. Du klickst auf einen Button, der eine JavaScript-Aktion ausführen soll, und plötzlich lädt die Seite neu, weil das Formular abgesendet wird.

**Daher die goldene Regel:** Setze bei einem `<button>`-Element *immer* explizit das `type`-Attribut (`type="submit"`, `type="reset"` oder `type="button"`). So machst du deinen Code eindeutig, verhinderst Fehler und sorgst dafür, dass der Button genau das tut, was du von ihm erwartest.

#### Ein kurzer Blick auf das Styling

Unabhängig vom Typ (`submit`, `reset` oder `button`) und vom Element (`<input>` oder `<button>`) kannst du das Aussehen deiner Buttons vollständig mit CSS steuern. Browser geben Buttons ein Standard-Styling, das oft altbacken und von System zu System unterschiedlich aussieht. Mit ein paar CSS-Regeln kannst du sie an das Design deiner Webseite anpassen.

```css
/* Ein einfaches Beispiel für das Styling eines Buttons */
button,
input[type="submit"],
input[type="reset"],
input[type="button"] {
  background-color: #007bff; /* Ein schönes Blau */
  color: white; /* Weißer Text */
  border: none; /* Kein Rand */
  padding: 10px 20px; /* Innenabstand */
  border-radius: 5px; /* Abgerundete Ecken */
  font-size: 16px;
  cursor: pointer; /* Mauszeiger wird zur Hand */
  transition: background-color 0.2s; /* Sanfter Übergang für den Hover-Effekt */
}

/* Stil für den Button, wenn die Maus darüber schwebt */
button:hover,
input[type="submit"]:hover,
input[type="reset"]:hover,
input[type="button"]:hover {
  background-color: #0056b3; /* Etwas dunkleres Blau */
}
```

Mit diesem Wissen über die drei Button-Typen bist du nun in der Lage, deinen Formularen die nötige Interaktivität zu verleihen – sei es, um Daten zu versenden, Eingaben zurückzusetzen oder benutzerdefinierte Aktionen mit JavaScript auszulösen.
