# aria-label und aria-labelledby

### Accessible Namen vergeben: `aria-label` und `aria-labelledby`

Stell dir vor, du gestaltest eine moderne, minimalistische Benutzeroberfläche. Ein zentrales Element ist ein Schließen-Button für ein Modal-Fenster, der nur aus einem „X“-Symbol besteht. Für sehende Nutzer ist die Funktion sofort klar. Doch was hört ein Screenreader-Nutzer? Im besten Fall hört er „X“ oder „Multiplikationszeichen“. Das ist nicht hilfreich. Dem Element fehlt ein zugänglicher Name (Accessible Name), der seine Funktion unmissverständlich beschreibt.

Genau hier kommen zwei der wichtigsten ARIA-Properties ins Spiel: `aria-label` und `aria-labelledby`. Beide haben das gleiche Ziel: einem Element einen zugänglichen Namen zu geben, der von assistiven Technologien (wie Screenreadern) ausgelesen werden kann. Ihre Funktionsweise ist jedoch grundlegend verschieden, und die Entscheidung, welches Attribut du wann einsetzt, ist entscheidend für eine saubere und semantisch korrekte Umsetzung.

#### `aria-label`: Der direkte Weg zum zugänglichen Namen

Das `aria-label`-Attribut ist der direkteste Weg, einem Element einen Namen zu geben. Du schreibst den gewünschten Text einfach als Wert direkt in das Attribut.

Schauen wir uns unseren „X“-Button an:

```html
<!-- Schlecht: Kein zugänglicher Name -->
<button>×</button>

<!-- Gut: Mit aria-label einen klaren Namen vergeben -->
<button aria-label="Fenster schließen">×</button>
```

In diesem Beispiel wird ein Screenreader den Inhalt des Buttons – das „×“ – komplett ignorieren und stattdessen den Wert von `aria-label` vorlesen: „Fenster schließen, Button“. Das Problem ist gelöst. Der zugängliche Name überschreibt den sichtbaren Inhalt des Elements vollständig für assistive Technologien.

**Wann ist `aria-label` die richtige Wahl?**

`aria-label` ist ideal für Fälle, in denen ein Element *keinen sichtbaren Text* hat, der als Beschriftung dienen könnte. Typische Anwendungsfälle sind:

*   **Icon-Buttons:** Wie im Beispiel oben, bei Buttons, die nur ein Icon (SVG, Icon-Font oder Bild) enthalten.
*   **Grafische Bedienelemente:** Ein als Link fungierendes Logo, das zum Start zurückführt, könnte `aria-label="Zurück zur Startseite"` erhalten.
*   **Einzigartige Navigations-Landmarks:** Ein `<nav>`-Element für die Hauptnavigation könnte `aria-label="Hauptnavigation"` bekommen, um es von einer Fußzeilennavigation (`<nav aria-label="Fußzeilennavigation">`) zu unterscheiden.

**Die wichtigste Regel bei `aria-label`**

Der entscheidende Punkt, den du dir merken musst, ist: `aria-label` **überschreibt** jeglichen Textinhalt, den ein Element und seine Kind-Elemente haben.

Betrachte dieses Beispiel:

```html
<!-- FEHLER: Der sichtbare und der zugängliche Name stimmen nicht überein -->
<button aria-label="In den Warenkorb legen">Jetzt kaufen</button>
```

Ein sehender Nutzer liest „Jetzt kaufen“, während ein Screenreader-Nutzer „In den Warenkorb legen“ hört. Diese Diskrepanz ist verwirrend und ein Verstoß gegen die Barrierefreiheitsrichtlinien (WCAG 2.5.3 Label in Name). Nutze `aria-label` also niemals, um einen bereits vorhandenen, sichtbaren Text zu korrigieren oder zu ersetzen. Wenn ein Element bereits eine gute, sichtbare Beschriftung hat, brauchst du `aria-label` nicht.

#### `aria-labelledby`: Der referenzierende Ansatz

Während `aria-label` einen neuen Namen als einfachen Textstring definiert, verfolgt `aria-labelledby` einen anderen Ansatz: Es **referenziert** ein oder mehrere andere Elemente auf der Seite, deren Textinhalt dann als zugänglicher Name verwendet wird.

Die Verbindung wird über die `id` der referenzierten Elemente hergestellt. Du übergibst dem `aria-labelledby`-Attribut die `id` des Elements, das als Beschriftung dienen soll.

Ein klassisches Beispiel ist ein Modal-Dialog. Ein solcher Dialog hat typischerweise eine sichtbare Überschrift, die seinen Zweck perfekt beschreibt.

```html
<div role="dialog" aria-labelledby="dialog-title">
  <h1 id="dialog-title">Anmeldung erforderlich</h1>
  
  <!-- ... Inhalt des Dialogs, Formular etc. ... -->
  
  <button>Anmelden</button>
  <button>Abbrechen</button>
</div>
```

Wenn ein Screenreader-Nutzer den Fokus auf diesen Dialog setzt, wird er durch `aria-labelledby="dialog-title"` die Überschrift „Anmeldung erforderlich“ als Namen für den gesamten Dialog hören. Das ist extrem nützlich, da es dem Nutzer sofort den Kontext des neuen Fensters vermittelt.

Der große Vorteil hierbei ist, dass du vorhandenen, sichtbaren Text wiederverwendest. Du musst keine redundanten Beschriftungen pflegen und stellst sicher, dass sehende und nicht-sehende Nutzer dieselbe Information erhalten.

**Mehrere Referenzen für komplexere Namen**

Die wahre Stärke von `aria-labelledby` zeigt sich darin, dass du mehrere `id`-Werte, getrennt durch Leerzeichen, übergeben kannst. Die assistiven Technologien verketten dann die Textinhalte der referenzierten Elemente in der angegebenen Reihenfolge zu einem einzigen zugänglichen Namen.

Stell dir eine Einstellungsseite mit mehreren Schaltern vor, die alle gleich aussehen, sich aber in unterschiedlichen Sektionen befinden:

```html
<h2 id="notifications">Benachrichtigungen</h2>
<div>
  <span id="email-label">E-Mail</span>
  <div role="switch" aria-checked="true" aria-labelledby="notifications email-label"></div>
</div>

<h2 id="privacy">Privatsphäre</h2>
<div>
  <span id="profile-label">Profil öffentlich sichtbar</span>
  <div role="switch" aria-checked="false" aria-labelledby="privacy profile-label"></div>
</div>
```

Für den ersten Schalter wird der zugängliche Name aus den Inhalten von `h2#notifications` und `span#email-label` zusammengesetzt. Ein Screenreader würde also etwas wie „Benachrichtigungen E-Mail, Schalter, an“ ausgeben. So wird ein ansonsten mehrdeutiger Schalter durch den Kontext der Überschrift eindeutig identifizierbar.

#### `aria-label` vs. `aria-labelledby`: Ein direkter Vergleich

Um die Entscheidung zu erleichtern, hier die Kernunterschiede auf einen Blick:

*   **Quelle des Namens:**
    *   `aria-label`: Der Name ist ein Text-String, der direkt im Attributwert steht. Er ist für sehende Nutzer nicht sichtbar.
    *   `aria-labelledby`: Der Name stammt aus dem Textinhalt eines oder mehrerer anderer, sichtbarer Elemente auf der Seite, die über ihre `id` referenziert werden.

*   **Anwendungsfall:**
    *   `aria-label`: Ideal, wenn es **keinen sichtbaren Text** gibt, der als Beschriftung dienen kann (z. B. Icon-Buttons).
    *   `aria-labelledby`: Ideal, wenn eine **passende Beschriftung bereits sichtbar** auf der Seite existiert und du sie nur noch programmatisch mit dem Element verknüpfen musst.

*   **Vorrang:**
    *   Solltest du versehentlich beide Attribute auf demselben Element verwenden, hat `aria-labelledby` immer Vorrang vor `aria-label`. Das liegt daran, dass die Verknüpfung mit sichtbarem Text als stärker und zuverlässiger angesehen wird.

#### Die erste Regel von ARIA: Nutze kein ARIA (wenn es eine HTML-Lösung gibt)

So mächtig diese Attribute auch sind, sie sollten immer deine zweite Wahl sein. Die robusteste, einfachste und wartungsfreundlichste Methode ist fast immer die Verwendung von nativem, semantischem HTML. Bevor du zu `aria-label` oder `aria-labelledby` greifst, frage dich immer: Gibt es dafür ein Standard-HTML-Element?

*   **Formular-Elemente:** Ein `<input>` sollte immer mit einem `<label for="...">`-Element verknüpft werden. Das ist der semantische Standard und funktioniert für alle Nutzergruppen perfekt. Du brauchst hier kein ARIA.

    ```html
    <!-- Perfekt: Nativer HTML-Standard -->
    <label for="username">Benutzername</label>
    <input type="text" id="username">
    
    <!-- Unnötig und schlechter Stil: ARIA als Ersatz für <label> -->
    <input type="text" aria-label="Benutzername">
    ```

*   **Buttons mit Text:** Wenn dein Button Text enthalten kann, dann schreib den Text einfach direkt in das `<button>`-Element.

    ```html
    <!-- Perfekt: Einfach und semantisch -->
    <button>Einstellungen speichern</button>
    
    <!-- Unnötig: aria-label für sichtbaren Text -->
    <button aria-label="Einstellungen speichern">Speichern</button> 
    ```

*   **Icon-Buttons mit verstecktem Text:** Eine sehr robuste Alternative zu `aria-label` für Icon-Buttons ist es, den beschreibenden Text in einem `<span>` zu platzieren und dieses visuell zu verstecken (z.B. mit einer CSS-Klasse wie `.visually-hidden`).

    ```html
    <button>
      <span class="visually-hidden">Fenster schließen</span>
      <svg aria-hidden="true" ...>
        <!-- Icon-Grafik -->
      </svg>
    </button>
    ```
    Der Vorteil dieser Methode ist, dass der Text im DOM bleibt und beispielsweise bei fehlerhaftem CSS sichtbar werden kann, während `aria-label`-Inhalte immer unsichtbar sind.

`aria-label` und `aria-labelledby` sind unverzichtbare Werkzeuge, um Lücken in der Barrierefreiheit zu schließen, die semantisches HTML allein nicht abdecken kann. Setze sie gezielt und bewusst dort ein, wo sie wirklich gebraucht werden: um visuellen Kontext in eine für assistive Technologien verständliche Form zu übersetzen. Indem du den Unterschied und die jeweiligen Stärken verstehst, schaffst du Oberflächen, die nicht nur gut aussehen, sondern für absolut jeden bedienbar sind.
