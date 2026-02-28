# Validierung vs. Sanitization

### Validierung vs. Sanitization: Zwei Seiten einer Medaille

Wenn du eine Webseite entwickelst, die auf irgendeine Weise mit Nutzereingaben interagiert – sei es ein Kontaktformular, ein Kommentarbereich oder ein Nutzerprofil –, betrittst du ein Minenfeld. Jedes einzelne Datenstück, das von einem Nutzer kommt, ist potenziell gefährlich. Es ist eine grundlegende Regel der Websicherheit: Vertraue niemals den Eingaben deiner Nutzer. Um diese Gefahr zu bändigen, stehen dir zwei mächtige, aber grundlegend verschiedene Werkzeuge zur Verfügung: Validierung und Sanitization.

Obwohl die Begriffe oft synonym verwendet werden, beschreiben sie zwei unterschiedliche Prozesse mit unterschiedlichen Zielen. Sie sind nicht austauschbar, sondern ergänzen sich und bilden zusammen eine robuste Verteidigungslinie. Lass uns tief in beide Konzepte eintauchen, um ihre Unterschiede, ihre Stärken und ihr Zusammenspiel zu verstehen.

#### Validierung: Der strenge Türsteher

Stell dir Validierung als einen Türsteher vor einem exklusiven Club vor. Der Türsteher hat eine klare Liste von Regeln: Nur Personen über 21, nur mit passender Kleidung, nur mit einer gültigen Einladung. Er schaut sich jede Person an und trifft eine klare Ja/Nein-Entscheidung. Entweder du erfüllst alle Kriterien und darfst rein, oder du wirst abgewiesen. Der Türsteher versucht nicht, deine Kleidung zu ändern oder dich älter zu machen. Er prüft nur, ob du den Regeln entsprichst.

Genau das tut die Validierung mit Daten. Sie ist der Prozess, bei dem du überprüfst, ob eine Eingabe einem erwarteten Format, Typ oder Wertebereich entspricht. Das Ergebnis der Validierung ist immer binär: Die Daten sind entweder gültig oder ungültig.

**Was prüft die Validierung?**

*   **Format:** Ist die E-Mail-Adresse im Format `name@domain.tld`? Ist das Datum im Format `TT.MM.JJJJ`?
*   **Typ:** Ist die Eingabe für das Alter eine Zahl? Ist die Eingabe für einen Namen ein String?
*   **Länge:** Hat das Passwort mindestens 12 Zeichen? Ist der Kommentar nicht länger als 5000 Zeichen?
*   **Wertebereich:** Liegt das eingegebene Alter zwischen 18 und 120?
*   **Anwesenheit:** Wurde ein Pflichtfeld (z. B. der Nutzername) überhaupt ausgefüllt?

Wenn eine Eingabe die Validierung nicht besteht, ist die übliche Reaktion, sie abzulehnen und dem Nutzer eine klare Fehlermeldung zu geben. „Bitte gib eine gültige E-Mail-Adresse ein.“ oder „Das Passwort muss mindestens 12 Zeichen lang sein.“

Schauen wir uns ein einfaches JavaScript-Beispiel für die Validierung einer Postleitzahl an. In Deutschland muss eine PLZ genau fünf Ziffern haben.

```javascript
function validierePLZ(plz) {
  // Die Regel: genau 5 Ziffern von Anfang (^) bis Ende ($)
  const plzRegex = /^\d{5}$/; 
  
  if (plzRegex.test(plz)) {
    console.log(`Die PLZ "${plz}" ist gültig.`);
    return true; // Gültig
  } else {
    console.log(`Die PLZ "${plz}" ist ungültig.`);
    return false; // Ungültig
  }
}

validierePLZ("12345");   // Output: Die PLZ "12345" ist gültig.
validierePLZ("1234");    // Output: Die PLZ "1234" ist ungültig.
validierePLZ("abcde");   // Output: Die PLZ "abcde" ist ungültig.
validierePLZ("123456");  // Output: Die PLZ "123456" ist ungültig.
```

In diesem Code wird die Eingabe nicht verändert. Es wird lediglich eine Entscheidung getroffen: akzeptieren oder ablehnen. Das ist die Essenz der Validierung. Sie schützt dein System, indem sie nur Daten hereinlässt, die der erwarteten Struktur entsprechen. Falsch formatierte Daten, die später zu Fehlern in deiner Anwendung führen könnten, werden so von vornherein abgeblockt.

#### Sanitization: Die chemische Reinigung

Bleiben wir bei der Club-Analogie. Stell dir nun vor, der Türsteher hat dich reingelassen, aber deine Jacke ist voller Schlamm. Bevor du den Club betrittst, wirst du zu einer Garderobe geschickt, wo der Schlamm von deiner Jacke entfernt wird. Deine Jacke wird nicht weggeworfen (abgelehnt), sondern sie wird so verändert (gesäubert), dass sie den Club nicht verschmutzt.

Genau das ist Sanitization (zu Deutsch auch „Säuberung“). Anstatt eine Eingabe abzulehnen, geht die Sanitization davon aus, dass sie potenziell schädliche Teile enthalten könnte, und versucht, diese zu entfernen oder zu neutralisieren. Das Ziel ist es, die Eingabe so zu modifizieren, dass sie sicher für die Weiterverarbeitung ist – sei es für die Speicherung in einer Datenbank oder die Anzeige auf einer Webseite.

Sanitization ist deine wichtigste Verteidigungslinie gegen Angriffe wie Cross-Site Scripting (XSS). Bei einem XSS-Angriff versucht ein Angreifer, schädlichen Code (meist JavaScript) in deine Webseite einzuschleusen, der dann im Browser anderer Nutzer ausgeführt wird.

Ein klassisches Beispiel ist ein Kommentarfeld. Ein Angreifer könnte statt eines netten Kommentars Folgendes eingeben:

```html
Netter Artikel! <script>alert('Du wurdest gehackt!');</script>
```

Wenn du diesen Kommentar einfach so in deine HTML-Seite einfügst, wird der Browser das `<script>`-Tag ausführen und jeder Besucher deiner Seite sieht ein alarmierendes Pop-up.

Hier kommt Sanitization ins Spiel. Ein Sanitizer würde diesen String durchgehen und das gefährliche `<script>`-Tag entfernen oder unschädlich machen.

**Methoden der Sanitization:**

1.  **Escaping/Encoding:** Dies ist die häufigste Methode. Potenziell gefährliche Zeichen werden durch ihre harmlosen HTML-Entitäten ersetzt. Der Browser interpretiert diese Entitäten dann als Text, nicht als Code.
    *   `<` wird zu `&lt;`
    *   `>` wird zu `&gt;`
    *   `"` wird zu `&quot;`
    *   `'` wird zu `&#39;`
    *   `&` wird zu `&amp;`

    Der bösartige Kommentar von oben würde nach dem Escaping so aussehen:

    ```html
    Netter Artikel! &lt;script&gt;alert('Du wurdest gehackt!');&lt;/script&gt;
    ```

    Wenn der Browser diesen Code liest, zeigt er den Text `<script>alert('Du wurdest gehackt!');</script>` auf der Seite an, anstatt ihn auszuführen. Das ist sicher.

2.  **Entfernen von schädlichem Code (Filtering):** Manchmal möchtest du Nutzern erlauben, eine begrenzte Auswahl an HTML zu verwenden (z. B. `<b>` für Fettdruck oder `<i>` für Kursivschrift). In diesem Fall verwendest du eine Whitelist erlaubter Tags und Attribute. Alles, was nicht auf dieser Liste steht, wird rigoros entfernt. Ein Sanitizer würde das `<script>`-Tag komplett entfernen, aber ein `<b>`-Tag stehen lassen.

Sehen wir uns ein sehr vereinfachtes PHP-Beispiel für das Escaping an, bevor Daten auf einer Webseite ausgegeben werden:

```php
// Unsichere Nutzereingabe aus einem Formular
$kommentar = "Ein harmloser Kommentar. <script>alert('XSS');</script>";

// Sanitization durch HTML-Escaping
$sicherer_kommentar = htmlspecialchars($kommentar, ENT_QUOTES, 'UTF-8');

// Ausgabe im HTML-Dokument
echo "<p>" . $sicherer_kommentar . "</p>";

// Der Browser erhält folgenden HTML-Code:
// <p>Ein harmloser Kommentar. &lt;script&gt;alert('XSS');&lt;/script&gt;</p>
// Der schädliche Code wird als Text angezeigt, nicht ausgeführt.
```

Sanitization verändert also die Eingabe, um sie sicher zu machen. Sie ist der entscheidende Schritt, um zu verhindern, dass die Eingaben eines Nutzers zu ausführbarem Code im Kontext eines anderen Nutzers werden.

#### Das Zusammenspiel: Verteidigung in der Tiefe

Jetzt wird klar, warum die Frage nicht "Validierung ODER Sanitization?" lauten darf. Die richtige Strategie lautet immer: **Validierung UND Sanitization**. Sie bilden ein mehrstufiges Sicherheitssystem, das als "Defense in Depth" (tiefengestaffelte Verteidigung) bekannt ist.

Stellen wir uns den Prozess für ein Kommentarformular vor:

1.  **Client-seitige Validierung (im Browser):** Du beginnst mit einer schnellen Validierung im Browser des Nutzers. Du prüfst, ob das Kommentarfeld nicht leer ist und die maximale Zeichenlänge nicht überschreitet. Dies dient hauptsächlich der Benutzerfreundlichkeit (UX), da der Nutzer sofort Feedback erhält, ohne die Seite neu laden zu müssen. **Achtung: Dies ist keine Sicherheitsmaßnahme!** Client-seitige Prüfungen können von einem Angreifer leicht umgangen werden.

2.  **Server-seitige Validierung (auf dem Server):** Die Eingabe kommt auf deinem Server an. Jetzt findet die *echte* Validierung statt. Du wiederholst die Prüfungen von Schritt 1 (Länge, Anwesenheit etc.), weil du dem Client niemals vertrauen kannst. Wenn der Kommentar beispielsweise länger als die erlaubten 5000 Zeichen ist, lehnst du die Anfrage hier rigoros ab und sendest eine Fehlermeldung zurück. Die Daten sind ungültig und werden gar nicht erst weiterverarbeitet.

3.  **Server-seitige Sanitization (auf dem Server):** Die Daten haben die Validierung bestanden. Du weißt jetzt, dass der Kommentar eine angemessene Länge hat. Du weißt aber immer noch nicht, ob er *sicher* ist. Bevor du den Kommentar in deiner Datenbank speicherst oder auf der Seite anzeigst, führst du die Sanitization durch. Du wendest `htmlspecialchars` oder eine robustere Filterbibliothek an, um potenziellen XSS-Code zu entschärfen.

Dieses Vorgehen ist extrem robust:
*   Die **Validierung** sorgt dafür, dass die Daten die richtige Form haben. Das verhindert eine ganze Klasse von Fehlern und unerwartetem Verhalten in deiner Anwendung.
*   Die **Sanitization** sorgt dafür, dass die Daten, selbst wenn sie formal korrekt sind, keinen schädlichen Inhalt haben. Das schützt deine Nutzer vor Angriffen.

Validierung ist die erste, grobe Hürde. Sanitization ist die zweite, feine Reinigung für alles, was die erste Hürde genommen hat. Beide sind unverzichtbar. Wenn du nur validierst, könnte ein Kommentar mit korrekter Länge immer noch bösartigen Code enthalten. Wenn du nur säuberst, könntest du am Ende riesige Mengen an gesäuberten, aber nutzlosen Daten in deiner Datenbank speichern, die deine Anwendung verlangsamen oder sprengen. Setze immer beides ein – immer auf dem Server.
