# aria-live für dynamische Updates

### Dynamische Inhalte zugänglich machen mit `aria-live`

Stell dir eine moderne Webanwendung vor: Du fügst einen Artikel zum Warenkorb hinzu und oben rechts erscheint eine kleine Benachrichtigung. Du füllst ein Formular aus und eine Fehlermeldung erscheint direkt unter dem Feld, ohne dass die Seite neu lädt. Ein Live-Ticker auf einer Nachrichtenseite aktualisiert sich mit den neuesten Sportergebnissen.

Für sehende Nutzer sind diese dynamischen Änderungen auf der Benutzeroberfläche sofort ersichtlich. Wir nehmen sie visuell wahr und verstehen den neuen Kontext. Aber was ist mit Nutzern, die auf einen Screenreader angewiesen sind? Für sie spielt sich das Web als linearer Text- und Elementstrom ab. Wenn sich an einer Stelle der Seite, die gerade nicht im Fokus des Screenreaders liegt, etwas ändert, bekommen sie davon nichts mit. Die Benachrichtigung über den vollen Warenkorb, die wichtige Fehlermeldung – all das existiert für sie nicht.

Genau hier kommt das ARIA-Attribut `aria-live` ins Spiel. Es ist das entscheidende Werkzeug, um assistive Technologien (AT) über dynamische Inhaltsänderungen zu informieren. Du verwandelst damit einen normalen Bereich deiner Seite in eine sogenannte "Live-Region".

#### Wie `aria-live` funktioniert

Das Prinzip ist einfach und genial zugleich. Du fügst das Attribut `aria-live` zu einem Container-Element hinzu, dessen Inhalt du potenziell mit JavaScript ändern wirst.

```html
<div id="status-meldung" aria-live="polite">
  <!-- Hier werden später Nachrichten eingefügt -->
</div>
```

Dieses Container-Element muss bereits beim Laden der Seite im DOM vorhanden sein. Wenn du nun später per JavaScript neuen Inhalt in dieses `div` einfügst, passiert Folgendes:

1.  Der Browser erkennt die Änderung innerhalb der als `aria-live` markierten Region.
2.  Er leitet diese Information an die Accessibility-Schnittstelle (Accessibility API) des Betriebssystems weiter.
3.  Der Screenreader empfängt diese Information und liest den neuen oder geänderten Inhalt dem Nutzer vor, egal wo sich dessen Fokus gerade auf der Seite befindet.

Dadurch wird die Lücke zwischen der visuellen Wahrnehmung und der auditiven Erfahrung geschlossen. Der Nutzer wird über wichtige Updates informiert, die er sonst verpasst hätte.

#### Die Dringlichkeitsstufen: `polite` vs. `assertive`

Nicht jede dynamische Änderung ist gleich wichtig. Eine Bestätigung, dass deine Einstellungen gespeichert wurden, ist weniger dringend als eine Fehlermeldung, die dich am Fortfahren hindert. Aus diesem Grund bietet `aria-live` verschiedene Werte, um die Dringlichkeit der Ansage zu steuern.

**`aria-live="polite"`**

Dies ist der am häufigsten verwendete und empfohlene Wert. "Polite" bedeutet "höflich". Der Screenreader wartet einen passenden Moment ab, um die Änderung vorzulesen. Er unterbricht den Nutzer nicht bei seiner aktuellen Tätigkeit (z. B. beim Ausfüllen eines Formularfeldes). Erst wenn der Nutzer eine Pause macht, wird die Nachricht angesagt.

**Anwendungsfälle für `polite`:**

*   **Status-Updates:** "Deine Nachricht wurde gesendet."
*   **Warenkorb-Benachrichtigungen:** "Produkt zum Warenkorb hinzugefügt."
*   **Suchergebnisse:** Eine Mitteilung wie "15 Ergebnisse gefunden", die erscheint, nachdem die Suchergebnisse unterhalb des Suchfeldes geladen wurden.
*   **Live-Ticker:** Neue Sportergebnisse oder Nachrichten-Updates.

Hier ein Beispiel für eine einfache "Toast"-Benachrichtigung:

```html
<!-- Der Container für die Benachrichtigungen -->
<div class="toast-container" aria-live="polite" role="status"></div>
```

```javascript
// Funktion, um eine Benachrichtigung anzuzeigen
function zeigeBenachrichtigung(text) {
  const container = document.querySelector('.toast-container');
  
  // Erstelle ein neues Element für die Nachricht
  const nachricht = document.createElement('p');
  nachricht.textContent = text;
  
  // Füge die Nachricht in den Live-Region-Container ein
  container.appendChild(nachricht);
  
  // Entferne die Nachricht nach einiger Zeit wieder aus dem DOM
  setTimeout(() => {
    container.removeChild(nachricht);
  }, 5000);
}

// Beispielaufruf
// zeigeBenachrichtigung('Deine Einstellungen wurden erfolgreich gespeichert.');
```
In diesem Fall wird der Screenreader, sobald eine passende Pause eintritt, "Deine Einstellungen wurden erfolgreich gespeichert" vorlesen.

**`aria-live="assertive"`**

"Assertive" bedeutet "bestimmt" oder "nachdrücklich". Dieser Wert ist für kritische, dringende Informationen reserviert. Wenn sich der Inhalt einer `assertive`-Region ändert, unterbricht der Screenreader sofort seine aktuelle Ausgabe – egal, was er gerade vorgelesen hat – und gibt die neue Information wieder.

Du solltest diesen Wert mit großer Vorsicht einsetzen, denn er kann für den Nutzer sehr störend sein. Er ist wie ein lauter Alarm, der alles andere übertönt.

**Anwendungsfälle für `assertive`:**

*   **Kritische Formularfehler:** "Fehler: Das Passwort ist erforderlich."
*   **Systemwarnungen:** "Ihre Sitzung läuft in einer Minute ab."
*   **Serverfehler:** "Verbindung zum Server unterbrochen. Ihre Änderungen konnten nicht gespeichert werden."

Ein Beispiel für eine Formularvalidierung:

```html
<form>
  <label for="email">E-Mail-Adresse:</label>
  <input type="email" id="email" required>
  <!-- Der Container für die Fehlermeldung -->
  <div id="email-fehler" class="error-message" aria-live="assertive"></div>
</form>
```

```javascript
const emailInput = document.getElementById('email');
const fehlerContainer = document.getElementById('email-fehler');

emailInput.addEventListener('blur', () => {
  if (!emailInput.value.includes('@')) {
    // Füge die Fehlermeldung in die assertive Live-Region ein
    fehlerContainer.textContent = 'Bitte gib eine gültige E-Mail-Adresse ein.';
  } else {
    // Leere den Container, wenn der Fehler behoben ist
    fehlerContainer.textContent = '';
  }
});
```
Wenn der Nutzer das Feld verlässt und die Eingabe ungültig ist, wird der Screenreader sofort und unmissverständlich die Fehlermeldung vorlesen.

Der dritte mögliche Wert ist `aria-live="off"`, was der Standardwert ist. Er deaktiviert das Live-Region-Verhalten.

#### Feinabstimmung: `aria-atomic` und `aria-relevant`

Neben der Dringlichkeit kannst du auch steuern, *was* und *bei welcher Art von Änderung* der Screenreader vorlesen soll.

**`aria-atomic`**

Dieses Attribut legt fest, ob der Screenreader nur den geänderten Teil oder die gesamte Live-Region vorlesen soll. Es ist ein boolesches Attribut mit den Werten `true` oder `false`.

*   **`aria-atomic="false"` (Standard):** Nur der geänderte oder neu hinzugefügte Knoten (Node) innerhalb der Region wird vorgelesen.
*   **`aria-atomic="true"`:** Die gesamte Region wird als eine atomare Einheit betrachtet. Bei jeder Änderung wird der komplette Inhalt der Region vorgelesen.

Ein klassisches Beispiel ist ein Warenkorb-Zähler:

```html
<p>
  Dein Warenkorb enthält 
  <span id="warenkorb-zaehler" aria-live="polite" aria-atomic="true">3</span> 
  Artikel.
</p>
```

Wenn du jetzt per JavaScript nur die Zahl `3` auf `4` änderst:

```javascript
document.getElementById('warenkorb-zaehler').textContent = '4';
```

*   Ohne `aria-atomic="true"` würde der Screenreader nur "4" vorlesen. Das ist aus dem Kontext gerissen und wenig hilfreich.
*   Mit `aria-atomic="true"` liest der Screenreader den gesamten Inhalt des `span`-Elements vor – also ebenfalls nur "4", was hier nicht das Ziel ist.

Moment, hier müssen wir das Konzept korrigieren. `aria-atomic` bezieht sich auf den *gesamten* Inhalt des Elements, auf dem es deklariert ist. Um den *ganzen Satz* vorgelesen zu bekommen, müsste die Live-Region den gesamten Satz umfassen:

```html
<p id="warenkorb-status" aria-live="polite" aria-atomic="true">
  Dein Warenkorb enthält <span id="warenkorb-zaehler">3</span> Artikel.
</p>
```

```javascript
// Ändere die Zahl im inneren Span
document.getElementById('warenkorb-zaehler').textContent = '4';
```
Jetzt passiert bei der Änderung der Zahl Folgendes: Da sich etwas innerhalb der `p`-Region geändert hat und diese `aria-atomic="true"` besitzt, wird der Screenreader den kompletten Inhalt des Paragrafen neu vorlesen: "Dein Warenkorb enthält 4 Artikel." Das ist eine sinnvolle und kontextbezogene Information.

**`aria-relevant`**

Dieses Attribut gibt dir noch mehr Kontrolle darüber, welche Arten von Änderungen eine Ansage auslösen sollen. Du kannst eine oder mehrere der folgenden Optionen (durch Leerzeichen getrennt) angeben:

*   **`additions`:** Ansage erfolgt, wenn Knoten zur Region hinzugefügt werden.
*   **`removals`:** Ansage erfolgt, wenn Knoten aus der Region entfernt werden.
*   **`text`:** Ansage erfolgt, wenn Textinhalt geändert wird.
*   **`all`:** Alle oben genannten Änderungen lösen eine Ansage aus.

Der Standardwert ist `additions text`. Das bedeutet, dass in den meisten Fällen nur das Hinzufügen von Elementen oder das Ändern von Text eine Ansage auslöst. Das Entfernen von Inhalten wird standardmäßig nicht angesagt. In der Praxis musst du `aria-relevant` nur sehr selten anpassen, da der Standardwert für die meisten Anwendungsfälle passt.

#### Bewährte Methoden und worauf du achten musst

*   **Container im Voraus laden:** Die Live-Region muss Teil des initialen DOM sein. Wenn du den Container und das Attribut `aria-live` dynamisch mit JavaScript hinzufügst, wird es von manchen Screenreadern möglicherweise nicht korrekt als Live-Region registriert. Erstelle also immer leere Platzhalter-Container im HTML.
*   **Sei sparsam mit `assertive`:** Nutze es wirklich nur für dringende Warnungen. Eine zu häufige Verwendung führt zu einer frustrierenden Nutzererfahrung, weil der Nutzer ständig unterbrochen wird. `polite` ist fast immer die bessere Wahl.
*   **Nicht alles muss live sein:** Markiere nur Bereiche, deren dynamische Änderungen für den Nutzer wirklich relevant sind. Eine sich ständig aktualisierende, aber unwichtige Information als Live-Region zu deklarieren, erzeugt nur unnötigen "Lärm".
*   **Klar und prägnant formulieren:** Der Text, den du in eine Live-Region einfügst, sollte kurz, verständlich und eindeutig sein. "Gespeichert" ist besser als eine lange, blumige Erfolgsmeldung.
*   **Teste mit einem echten Screenreader:** Die Theorie ist wichtig, aber nur ein echter Test mit Tools wie NVDA (Windows), VoiceOver (macOS/iOS) oder JAWS (Windows) zeigt dir, wie deine Implementierung in der Praxis klingt und ob die Nutzererfahrung wirklich gut ist.

Durch den gezielten Einsatz von `aria-live` machst du deine dynamischen Webanwendungen für alle Nutzer zugänglich und stellst sicher, dass wichtige Informationen niemanden ausschließen. Es ist ein kleiner, aber entscheidender Schritt hin zu einer inklusiveren digitalen Welt.
