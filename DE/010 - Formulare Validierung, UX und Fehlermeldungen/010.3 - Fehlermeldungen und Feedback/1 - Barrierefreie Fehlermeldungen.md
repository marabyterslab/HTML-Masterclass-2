# Barrierefreie Fehlermeldungen

### Barrierefreie Fehlermeldungen

Stell dir vor, du füllst ein wichtiges Online-Formular aus. Du gibst dir Mühe, alles korrekt einzutragen, klickst auf „Senden“ und … nichts passiert. Oder schlimmer: Irgendwo auf der Seite leuchtet ein Feld rot auf, aber du weißt nicht, welches oder warum. Frustrierend, oder? Für Menschen mit Behinderungen kann eine solche Situation nicht nur frustrierend, sondern eine unüberwindbare Hürde sein. Eine schlecht gestaltete Fehlermeldung kann deine Webseite für sie unbenutzbar machen.

Gute, barrierefreie Fehlermeldungen sind daher kein Luxus, sondern eine Notwendigkeit. Sie sind ein zentraler Bestandteil einer guten User Experience (UX) und stellen sicher, dass alle Nutzer, unabhängig von ihren Fähigkeiten, ein Formular erfolgreich ausfüllen und absenden können.

#### Das Problem mit der reinen Optik

Ein häufiger Fehler bei der Gestaltung von Fehlermeldungen ist der alleinige Fokus auf visuelle Hinweise. Ein klassisches Beispiel ist das Ändern der Rahmenfarbe eines Eingabefeldes auf Rot.

```css
input:invalid {
  border-color: red;
}
```

Dieser Ansatz hat gleich mehrere schwerwiegende Mängel:

1.  **Für farbenblinde Nutzer:** Etwa 8 % der Männer haben eine Rot-Grün-Sehschwäche. Für sie ist ein roter Rahmen kaum von einem grünen oder grauen zu unterscheiden. Die Information geht verloren.
2.  **Für blinde Nutzer:** Ein Screenreader, der blinden oder sehbehinderten Nutzern den Bildschirminhalt vorliest, hat keine Ahnung von Farben. Die Änderung der `border-color` ist für ihn unsichtbar. Er wird den Fehler nicht ankündigen.
3.  **Für alle Nutzer:** Selbst für sehende Nutzer ohne Einschränkungen ist ein roter Rahmen oft nicht genug. Was genau ist der Fehler? Ist das Feld leer? Ist das Format falsch? Die reine Farbänderung ist nicht aussagekräftig.

Barrierefreiheit verlangt, dass Informationen auf mehreren Wegen vermittelt werden. Eine Fehlermeldung muss **wahrnehmbar**, **verständlich** und **bedienbar** sein.

#### Die drei Säulen einer barrierefreien Fehlermeldung

Um eine robuste und für alle zugängliche Fehlerbehandlung zu schaffen, stützen wir uns auf drei wesentliche Säulen.

##### 1. Wahrnehmbarkeit: Den Fehler unmissverständlich signalisieren

Der Nutzer muss überhaupt erst einmal mitbekommen, *dass* ein Fehler aufgetreten ist. Das erreichen wir durch eine Kombination aus visuellen und nicht-visuellen Techniken.

**Textliche Fehlermeldung:** Das ist die Grundlage. Jeder Fehler muss durch eine klare Textnachricht beschrieben werden. Diese Nachricht muss in der Nähe des fehlerhaften Feldes platziert werden, damit der visuelle Zusammenhang sofort klar ist.

**Visuelle Hervorhebung (jenseits von Farbe):** Verstärke die rote Farbe durch zusätzliche visuelle Indikatoren. Das kann ein Icon (z. B. ein Ausrufezeichen), eine dickere Rahmenlinie oder eine Änderung des Hintergrunds sein. So stellst du sicher, in Anlehnung an die WCAG-Richtlinien (Web Content Accessibility Guidelines), dass Farbe nicht das *einzige* Mittel zur Informationsvermittlung ist.

**Ankündigung für Screenreader:** Das ist der entscheidende technische Schritt. Wenn ein Fehler auftritt, muss ein Screenreader dies aktiv ankündigen. Hierfür gibt es sogenannte „ARIA Live Regions“. Das sind Bereiche auf deiner Seite, deren Inhalte von Screenreadern automatisch vorgelesen werden, wenn sie sich ändern.

Ein Container für Fehlermeldungen könnte so aussehen:

```html
<div id="error-summary" role="alert" aria-live="assertive">
  <!-- Fehlermeldungen werden hier dynamisch per JavaScript eingefügt -->
</div>
```

-   `role="alert"`: Dieses ARIA-Attribut kennzeichnet den Bereich als wichtige, zeitkritische Information. Es ist eine Abkürzung für `aria-live="assertive"`.
-   `aria-live="assertive"`: Sorgt dafür, dass ein Screenreader seine aktuelle Ausgabe sofort unterbricht und den neuen Inhalt dieses Bereichs vorliest. Dies ist nützlich für kritische Fehler nach dem Absenden des Formulars.
-   `aria-live="polite"`: Eine sanftere Alternative. Der Screenreader wartet, bis der Nutzer seine aktuelle Tätigkeit beendet hat (z. B. einen Satz zu Ende gelesen hat), und liest dann die neue Information vor. Dies eignet sich gut für eine Validierung, die bereits während der Eingabe stattfindet.

##### 2. Verständlichkeit: Sagen, was los ist – und wie man es behebt

Eine Fehlermeldung wie „Ungültige Eingabe“ ist nutzlos. Sie erzeugt nur Ratlosigkeit. Eine gute Fehlermeldung ist präzise, konstruktiv und frei von technischem Jargon.

-   **Sei spezifisch:** Statt „Falsches Format“, schreibe: „Bitte gib eine gültige E-Mail-Adresse ein (z. B. name@beispiel.de).“
-   **Sei hilfreich:** Statt „Passwort zu kurz“, schreibe: „Dein Passwort muss mindestens 8 Zeichen lang sein.“
-   **Vermeide Schuldzuweisungen:** Formuliere neutral oder positiv. Statt „Du hast das Feld nicht ausgefüllt“, schreibe: „Dieses Feld ist ein Pflichtfeld.“

Eine klare, menschliche Sprache baut Frust ab und gibt dem Nutzer das Gefühl, die Kontrolle zu haben.

##### 3. Bedienbarkeit: Der direkte Weg zur Korrektur

Der Nutzer weiß nun, dass ein Fehler da ist und was er bedeutet. Jetzt musst du ihm helfen, den Fehler schnell zu finden und zu beheben.

**Programmatische Verknüpfung:**
Das ist das Herzstück der barrierefreien Fehlerbehandlung. Du musst das Eingabefeld und seine zugehörige Fehlermeldung semantisch miteinander verbinden. Dies geschieht mit ARIA-Attributen.

-   `aria-invalid="true"`: Dieses Attribut wird am `<input>`-Element gesetzt, wenn dessen Inhalt ungültig ist. Es signalisiert assistiven Technologien, dass hier ein Problem vorliegt.
-   `aria-describedby`: Dieses Attribut am `<input>`-Element verweist auf die `id` des Elements, das die Fehlermeldung enthält.

Wenn ein Nutzer nun mit einem Screenreader auf das Feld navigiert, liest dieser nicht nur das Label des Feldes vor, sondern auch die direkt damit verknüpfte Fehlermeldung. Der Kontext ist sofort klar.

Schauen wir uns ein vollständiges, barrierefreies Beispiel für ein E-Mail-Feld an:

```html
<div>
  <label for="email">E-Mail-Adresse</label>
  <input
    type="email"
    id="email"
    name="email"
    aria-invalid="true"
    aria-describedby="email-error"
  >
  <span id="email-error" class="error-message">
    Bitte gib eine gültige E-Mail-Adresse ein. Das Format sollte name@domain.de sein.
  </span>
</div>
```

**Was hier passiert:**

1.  Das `<label>` ist korrekt mit dem `<input>` über `for` und `id` verbunden. Das ist die Grundlage jeder guten Formularstruktur.
2.  Das `<input>` hat `aria-invalid="true"`, weil ein Fehler vorliegt.
3.  Die Fehlermeldung in unserem `<span>` hat eine eindeutige `id`, nämlich `email-error`.
4.  Das `<input>`-Element verweist mit `aria-describedby="email-error"` genau auf diese `id`.

Ein Screenreader würde beim Fokussieren dieses Feldes nun etwas Ähnliches wie dieses vorlesen: „E-Mail-Adresse, Eingabefeld, ungültige Eingabe. Bitte gib eine gültige E-Mail-Adresse ein. Das Format sollte name@domain.de sein.“ Besser geht es kaum.

**Fokusmanagement:**
Wenn ein Nutzer ein langes Formular abschickt und Fehler auftreten, sollte er nicht gezwungen sein, die ganze Seite abzusuchen. Die beste Praxis ist es, den Fokus des Browsers programmatisch auf das erste fehlerhafte Feld zu setzen.

Mit JavaScript kannst du das einfach erreichen:

```javascript
// Nach dem fehlgeschlagenen Absenden des Formulars:
const firstInvalidField = document.querySelector('[aria-invalid="true"]');

if (firstInvalidField) {
  firstInvalidField.focus();
}
```

Dieser kleine Code-Schnipsel findet das erste Element mit dem Attribut `aria-invalid="true"` und setzt den Cursor direkt hinein. Der Nutzer kann sofort mit der Korrektur beginnen.

**Fehlerzusammenfassung am Seitenanfang:**
Bei längeren oder komplexeren Formularen ist es zusätzlich hilfreich, eine Zusammenfassung aller Fehler am Anfang des Formulars anzuzeigen. Diese Zusammenfassung sollte in einem `<div>` mit `role="alert"` platziert werden, damit sie nach dem Absenden sofort vorgelesen wird.

Das Besondere an dieser Zusammenfassung: Jeder aufgelistete Fehler ist ein Link, der den Nutzer direkt zum entsprechenden Eingabefeld springen lässt.

```html
<div id="error-summary" role="alert" tabindex="-1">
  <h2>Deine Eingaben konnten nicht verarbeitet werden</h2>
  <p>Bitte korrigiere die folgenden 2 Fehler:</p>
  <ul>
    <li><a href="#email">Die E-Mail-Adresse hat ein ungültiges Format.</a></li>
    <li><a href="#password">Das Passwort ist zu kurz.</a></li>
  </ul>
</div>

<!-- ... weiter unten im Formular ... -->

<div>
  <label for="email">E-Mail-Adresse</label>
  <input type="email" id="email" aria-invalid="true" aria-describedby="email-error">
  <span id="email-error">...</span>
</div>

<div>
  <label for="password">Passwort</label>
  <input type="password" id="password" aria-invalid="true" aria-describedby="password-error">
  <span id="password-error">...</span>
</div>
```

Nach dem Absenden setzt du den Fokus per JavaScript auf den `error-summary`-Container (`document.getElementById('error-summary').focus()`). Durch `tabindex="-1"` wird das `<div>` fokussierbar. Der Nutzer hört zuerst die Zusammenfassung und kann dann bequem über die Links zu den einzelnen Fehlern navigieren.

Barrierefreie Fehlermeldungen sind ein perfektes Beispiel dafür, wie gutes technisches Handwerk und Empathie für den Nutzer Hand in Hand gehen. Indem du sicherstellst, dass deine Fehler klar kommuniziert, verständlich formuliert und einfach zu beheben sind, baust du nicht nur Barrieren ab, sondern schaffst eine insgesamt bessere und erfolgreichere Erfahrung für jeden einzelnen Nutzer deiner Webseite.
