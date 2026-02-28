# Modale Dialoge und Fokus-Trapping

### Modale Dialoge und Fokus-Trapping

Stell dir vor, du bittest einen Nutzer um eine wichtige Bestätigung, bevor eine kritische Aktion ausgeführt wird – zum Beispiel das endgültige Löschen seines Accounts. Du möchtest sicherstellen, dass er diese Entscheidung bewusst trifft und nicht versehentlich auf etwas anderes auf der Seite klickt. Genau hier kommen modale Dialoge ins Spiel.

Ein modaler Dialog ist ein Fenster, das sich über den Hauptinhalt einer Webseite legt. Solange dieser Dialog aktiv ist, wird der Rest der Seite visuell abgedunkelt und ist – und das ist der entscheidende Punkt – nicht mehr interaktiv. Der Nutzer wird gezwungen, sich ausschließlich mit dem Inhalt des Dialogs zu beschäftigen. Er muss eine Aktion im Dialog ausführen (z.B. auf "Bestätigen" oder "Abbrechen" klicken), um wieder mit dem Rest der Seite interagieren zu können.

Für sehende Nutzer, die eine Maus verwenden, ist das Konzept meist intuitiv. Sie sehen das Dialogfenster im Vordergrund, der Hintergrund ist inaktiv, und sie klicken auf die Schaltflächen im Dialog. Für Nutzer, die auf eine Tastaturbedienung oder einen Screenreader angewiesen sind, entsteht hier jedoch eine der größten Hürden für die Barrierefreiheit, wenn sie nicht korrekt umgesetzt wird: das Fokus-Problem.

#### Die unsichtbare Falle: Wenn der Fokus entweicht

Wenn ein modaler Dialog erscheint, muss der Fokus der Tastatur sofort in den Dialog verschoben werden. Passiert das nicht, bleibt der Fokus auf dem Element, das den Dialog ausgelöst hat (z.B. der "Löschen"-Button). Wenn der Nutzer nun die `Tab`-Taste drückt, um zum nächsten Element zu springen, bewegt sich der Fokus im Hintergrund weiter, auf der deaktivierten Hauptseite. Der Nutzer navigiert also "blind" hinter dem Vorhang des Dialogs, ohne es zu merken. Für einen Screenreader-Nutzer ist der Dialog quasi nicht existent, da er nie den Fokus erhält.

Noch schlimmer ist es, wenn der Fokus zwar in den Dialog gesetzt wird, aber nicht darin "gefangen" wird. Der Nutzer drückt vielleicht einige Male die `Tab`-Taste, navigiert durch die Elemente im Dialog und landet dann – zack – wieder auf der Hauptseite dahinter. Der Kontext ist verloren, die Bedienung wird frustrierend und oft unmöglich.

Die Lösung für dieses Problem besteht aus zwei Teilen: der korrekten semantischen Auszeichnung mit ARIA und einer Technik namens **Fokus-Trapping** (Fokus-Falle), die per JavaScript umgesetzt wird.

#### ARIA-Rollen für klare Kommunikation

Um assistiven Technologien verständlich zu machen, dass es sich um einen modalen Dialog handelt, benötigen wir einige spezifische ARIA-Attribute.

1.  **`role="dialog"`**: Dieses Attribut weist den Container des Dialogs als Dialogfenster aus. Screenreader erkennen dies und geben dem Nutzer entsprechenden Kontext, etwa "Dialog, Bestätigung".

2.  **`aria-modal="true"`**: Das ist das entscheidende Signal. Es teilt der assistiven Technologie mit, dass der Inhalt außerhalb dieses Dialogs vorübergehend nicht verfügbar ist. Moderne Screenreader nutzen diese Information, um die Navigation auf den Inhalt des Dialogs zu beschränken, was eine große Hilfe ist.

3.  **`aria-labelledby` und `aria-describedby`**: Ein Dialog ohne Titel ist wie ein Raum ohne Türschild – man weiß nicht, worum es geht.
    *   `aria-labelledby` verknüpft den Dialog mit seinem Titel. Der Wert dieses Attributs ist die `id` des Elements, das den Titel enthält (z.B. eine `<h2>`). Dies ist das Erste, was ein Screenreader vorliest, wenn der Dialog den Fokus erhält.
    *   `aria-describedby` verknüpft den Dialog mit einer optionalen, aber oft nützlichen Beschreibung. Dies könnte ein Absatz sein, der den Zweck des Dialogs genauer erklärt.

Hier ist ein Beispiel für die grundlegende HTML-Struktur:

```html
<!-- Button, der den Dialog öffnet -->
<button id="open-dialog-btn">Account löschen</button>

<!-- Der modale Dialog (anfangs per CSS versteckt) -->
<div id="delete-dialog"
     role="dialog"
     aria-modal="true"
     aria-labelledby="dialog-title"
     aria-describedby="dialog-desc"
     class="modal-hidden">

  <h2 id="dialog-title">Account wirklich löschen?</h2>
  <p id="dialog-desc">Diese Aktion kann nicht rückgängig gemacht werden. Alle deine Daten gehen verloren.</p>
  
  <div class="dialog-buttons">
    <button id="confirm-btn">Ja, löschen</button>
    <button id="cancel-btn">Abbrechen</button>
  </div>
</div>

<!-- Der Overlay für den Hintergrund -->
<div id="overlay" class="modal-hidden"></div>
```

Diese Struktur allein reicht aber nicht. Ohne JavaScript bleibt der Dialog versteckt und der Fokus wird nicht gesteuert.

#### Fokus-Trapping mit JavaScript implementieren

Das eigentliche "Fangen" des Fokus ist eine Aufgabe für JavaScript. Das Skript muss drei Kernaufgaben erfüllen:

1.  **Beim Öffnen des Dialogs:**
    *   Den Dialog und den Overlay sichtbar machen.
    *   Das Element speichern, das den Fokus *vor* dem Öffnen hatte (den Trigger-Button).
    *   Den Fokus auf das erste fokussierbare Element *innerhalb* des Dialogs setzen (z.B. den "Abbrechen"-Button oder den Dialog-Container selbst mit `tabindex="-1"`).

2.  **Während der Dialog geöffnet ist:**
    *   Eine "Fokus-Falle" einrichten. Das bedeutet, wir müssen Tastendrücke abfangen.
    *   Wenn der Nutzer die `Tab`-Taste auf dem *letzten* fokussierbaren Element im Dialog drückt, müssen wir den Fokus manuell auf das *erste* fokussierbare Element im Dialog setzen.
    *   Wenn der Nutzer `Shift + Tab` auf dem *ersten* fokussierbaren Element drückt, müssen wir den Fokus manuell auf das *letzte* fokussierbare Element setzen.
    *   Das Schließen des Dialogs über die `Escape`-Taste ermöglichen.

3.  **Beim Schließen des Dialogs:**
    *   Den Dialog und den Overlay wieder verstecken.
    *   Den Fokus auf das Element zurücksetzen, das wir uns beim Öffnen gemerkt haben. Dies ist ein entscheidender Schritt für eine nahtlose Nutzererfahrung.

Hier ist ein vereinfachtes Beispielskript, das diese Logik veranschaulicht:

```javascript
const openDialogBtn = document.getElementById('open-dialog-btn');
const dialog = document.getElementById('delete-dialog');
const overlay = document.getElementById('overlay');
const confirmBtn = document.getElementById('confirm-btn');
const cancelBtn = document.getElementById('cancel-btn');

let previouslyFocusedElement;

// Funktion zum Öffnen des Dialogs
function openDialog() {
  previouslyFocusedElement = document.activeElement; // Fokus speichern
  
  dialog.classList.remove('modal-hidden');
  overlay.classList.remove('modal-hidden');
  
  // Alle fokussierbaren Elemente im Dialog finden
  const focusableElements = dialog.querySelectorAll('button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])');
  const firstFocusableElement = focusableElements[0];
  const lastFocusableElement = focusableElements[focusableElements.length - 1];

  // Fokus auf das erste Element im Dialog setzen
  firstFocusableElement.focus();

  // Event Listener für das Fokus-Trapping
  dialog.addEventListener('keydown', function(e) {
    const isTabPressed = e.key === 'Tab' || e.keyCode === 9;

    if (!isTabPressed) { 
      return; 
    }

    if (e.shiftKey) { // Shift + Tab
      if (document.activeElement === firstFocusableElement) {
        lastFocusableElement.focus();
        e.preventDefault();
      }
    } else { // Nur Tab
      if (document.activeElement === lastFocusableElement) {
        firstFocusableElement.focus();
        e.preventDefault();
      }
    }
  });

  // Schließen mit Escape-Taste
  document.addEventListener('keydown', closeOnEscape);
}

// Funktion zum Schließen des Dialogs
function closeDialog() {
  dialog.classList.add('modal-hidden');
  overlay.classList.add('modal-hidden');
  document.removeEventListener('keydown', closeOnEscape);
  
  // Fokus zurückgeben
  if (previouslyFocusedElement) {
    previouslyFocusedElement.focus();
  }
}

function closeOnEscape(e) {
  if (e.key === 'Escape') {
    closeDialog();
  }
}

openDialogBtn.addEventListener('click', openDialog);
cancelBtn.addEventListener('click', closeDialog);
confirmBtn.addEventListener('click', () => {
  // Logik für die Bestätigung...
  console.log('Account wird gelöscht!');
  closeDialog();
});
```

Diese Kombination aus semantischem HTML mit ARIA und präziser Fokussteuerung per JavaScript verwandelt einen potenziell frustrierenden Dialog in ein barrierefreies und robustes UI-Pattern.

#### Der moderne Weg: Das `<dialog>`-Element

Die gute Nachricht ist, dass HTML selbst eine modernere, einfachere Lösung für dieses Problem bietet: das `<dialog>`-Element. Es wurde speziell für solche Anwendungsfälle entwickelt und bringt viele der besprochenen Funktionalitäten von Haus aus mit.

Ein `<dialog>`-Element:
*   implementiert **natives Fokus-Trapping**. Du musst dich nicht mehr selbst um die `Tab`-Logik kümmern.
*   hat eine einfache JavaScript-API mit `dialog.showModal()` und `dialog.close()`.
*   wird standardmäßig über die `Escape`-Taste geschlossen.
*   bringt ein `::backdrop`-Pseudo-Element mit, das du einfach per CSS gestalten kannst, um den Hintergrund abzudunkeln.

So sieht die Implementierung mit dem `<dialog>`-Element aus:

**HTML:**

```html
<button id="open-dialog-btn-native">Dialog öffnen</button>

<dialog id="native-dialog">
  <h2>Das ist ein nativer Dialog</h2>
  <p>Fokus-Trapping und Schließen per Escape-Taste funktionieren automatisch.</p>
  <form method="dialog">
    <button>OK</button>
  </form>
</dialog>
```
Beachte den `method="dialog"`-Button. Ein Button innerhalb eines `<form>`-Elements mit dieser Methode schließt den Dialog automatisch, wenn er geklickt wird.

**JavaScript:**

```javascript
const openNativeBtn = document.getElementById('open-dialog-btn-native');
const nativeDialog = document.getElementById('native-dialog');

openNativeBtn.addEventListener('click', () => {
  nativeDialog.showModal(); // Öffnet den Dialog modal
});
```

Das ist alles! Der Browser übernimmt den Rest. Das `<dialog>`-Element ist der semantisch korrekte und technisch überlegene Weg. Auch wenn die Browser-Unterstützung heute sehr gut ist, ist es dennoch wichtig, die manuelle ARIA- und JavaScript-Methode zu verstehen. Du wirst sie in älteren Projekten finden oder sie als Fallback benötigen, wenn du Browser unterstützen musst, die `<dialog>` noch nicht vollständig implementiert haben.

Ob manuell gebaut oder nativ verwendet: Ein korrekter modaler Dialog respektiert den Nutzer, indem er den Kontext klar definiert und die Steuerung nicht aus der Hand gibt. Das Fokus-Trapping ist dabei kein nettes Extra, sondern der Kern einer barrierefreien und für alle nutzbaren Implementierung.
