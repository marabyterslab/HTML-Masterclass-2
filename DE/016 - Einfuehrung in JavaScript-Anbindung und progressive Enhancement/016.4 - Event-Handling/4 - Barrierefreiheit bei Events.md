# Barrierefreiheit bei Events

### Barrierefreiheit bei Events: Wenn der Klick nicht alles ist

Wenn du beginnst, mit JavaScript-Events zu arbeiten, ist der `click`-Event oft der erste und naheliegendste Begleiter. Ein Klick hier, eine Aktion da – es fühlt sich intuitiv an. Doch die digitale Welt ist weitaus vielfältiger als der Zeiger einer Maus. Was ist mit Nutzern, die ausschließlich mit der Tastatur navigieren? Was ist mit Menschen, die auf Screenreader angewiesen sind, um den Inhalt einer Seite zu verstehen?

Hier kommt die Barrierefreiheit, oft als "a11y" (11 Buchstaben zwischen A und Y) abgekürzt, ins Spiel. Bei der Event-Behandlung bedeutet Barrierefreiheit, interaktive Elemente so zu gestalten, dass sie für *jeden* bedienbar sind, unabhängig vom verwendeten Eingabegerät oder individuellen Fähigkeiten. Es geht darum, deine Webanwendungen robust und inklusiv zu machen.

#### Das Fundament: Semantisches HTML ist nicht verhandelbar

Bevor du auch nur eine Zeile JavaScript schreibst, beginnt die Arbeit an barrierefreien Events im HTML. Die goldene Regel lautet: Nutze das richtige HTML-Element für den richtigen Zweck.

Stell dir vor, du möchtest einen Button erstellen, der eine Nachricht anzeigt. Ein gängiger Fehler ist, dafür ein `<div>`- oder `<span>`-Element zu verwenden und ihm einen `click`-Event-Listener anzuhängen.

**Negativbeispiel:**

```html
<div class="custom-button">Zeige Nachricht</div>
```

```javascript
const customButton = document.querySelector('.custom-button');

customButton.addEventListener('click', () => {
  alert('Hallo Welt!');
});
```

Warum ist das ein Problem?

1.  **Nicht per Tastatur erreichbar:** Ein `<div>` ist standardmäßig nicht im Fokus-Flow der Seite. Das bedeutet, du kannst es nicht mit der Tab-Taste ansteuern. Ein Nutzer, der keine Maus benutzt, kann diesen "Button" niemals auslösen.
2.  **Keine semantische Bedeutung:** Ein Screenreader liest dieses Element als "Gruppe" oder einfach nur als Text vor, aber nicht als "Schaltfläche". Der Nutzer weiß nicht, dass er damit interagieren kann.
3.  **Keine eingebaute Funktionalität:** Echte Buttons können nicht nur mit der Maus geklickt, sondern auch mit der `Enter`- oder `Leertaste` auf der Tastatur aktiviert werden. Diese Funktionalität müsstest du für dein `<div>` mühsam selbst nachbauen.

Die korrekte Lösung ist verblüffend einfach: Nutze ein `<button>`-Element.

**Positivbeispiel:**

```html
<button id="messageButton">Zeige Nachricht</button>
```

```javascript
const messageButton = document.getElementById('messageButton');

messageButton.addEventListener('click', () => {
  alert('Hallo Welt!');
});
```

Dieser Button ist von Haus aus:
*   **Fokussierbar:** Er kann mit der Tab-Taste erreicht werden.
*   **Aktivierbar:** Er reagiert auf Klicks, Taps und die `Enter`- sowie `Leertaste`.
*   **Semantisch korrekt:** Ein Screenreader kündigt ihn als "Schaltfläche, Zeige Nachricht" an. Der Nutzer weiß sofort, was zu tun ist.

Du hast dieselbe Funktionalität erreicht, aber durch die Wahl des richtigen HTML-Elements eine riesige Hürde für viele Nutzer entfernt.

#### Die Tastatur ist dein Freund: Fokus und Keyboard-Events

Viele Web-Interaktionen gehen über einfache Klicks hinaus. Denk an Dropdown-Menüs, Modals oder benutzerdefinierte Slider. Hier ist eine durchdachte Tastaturbedienung unerlässlich.

**Fokusmanagement**

Der Fokus ist der "aktive" Punkt auf einer Webseite, der Tastatureingaben empfängt. Du erkennst ihn meist an einem visuellen Rahmen (dem `outline`). Nur fokussierbare Elemente können Tastatur-Events empfangen.

Mit dem `tabindex`-Attribut kannst du das Fokusverhalten steuern:

*   `tabindex="0"`: Macht ein Element, das normalerweise nicht fokussierbar ist (wie ein `<div>`), Teil der natürlichen Tab-Reihenfolge. Nutze dies sparsam und nur, wenn du ein interaktives Widget baust, für das es kein natives HTML-Element gibt.
*   `tabindex="-1"`: Macht ein Element programmatisch fokussierbar (über `element.focus()` in JavaScript), nimmt es aber aus der natürlichen Tab-Reihenfolge heraus. Das ist nützlich, um den Fokus gezielt zu setzen, z.B. wenn sich ein Modal-Fenster öffnet.
*   `tabindex` mit Werten größer als 0 (`tabindex="1"`, `tabindex="2"`, ...): **Vermeide dies!** Es zerstört die natürliche und logische Navigationsreihenfolge der Seite und führt zu einer verwirrenden Benutzererfahrung.

**Keyboard-Events lauschen**

Wenn du eine benutzerdefinierte Komponente baust, musst du oft auf `keydown`-Events lauschen, um auf Tastendrücke zu reagieren. Das `event`-Objekt, das an deinen Listener übergeben wird, enthält eine `key`-Eigenschaft, mit der du die gedrückte Taste identifizieren kannst.

Schauen wir uns ein einfaches Beispiel für ein Akkordeon-Element an, das sich per Klick und auch per Tastatur öffnen und schließen lässt.

```html
<div class="accordion">
  <h3>
    <button aria-expanded="false" aria-controls="panel1">
      Abschnitt 1
    </button>
  </h3>
  <div id="panel1" role="region" hidden>
    <p>Inhalt von Abschnitt 1...</p>
  </div>
</div>
```

```javascript
const button = document.querySelector('.accordion button');
const panel = document.getElementById('panel1');

button.addEventListener('click', () => {
  const isExpanded = button.getAttribute('aria-expanded') === 'true';
  button.setAttribute('aria-expanded', !isExpanded);
  panel.hidden = isExpanded;
});
```

Dieser Code funktioniert per Maus. Um die Tastaturbedienung zu vervollständigen, ist hier nichts weiter nötig, da der `<button>` bereits auf `Enter` und `Leertaste` reagiert. Bei komplexeren Widgets, wie einem Dropdown, müsstest du jedoch auf Pfeiltasten oder die `Escape`-Taste hören.

```javascript
// Beispiel für ein Dropdown
dropdown.addEventListener('keydown', (event) => {
  if (event.key === 'Escape') {
    // Schließe das Dropdown
    closeDropdown();
  } else if (event.key === 'ArrowDown') {
    // Bewege den Fokus zum nächsten Element in der Liste
    focusNextItem();
  }
});
```

#### Mehr als nur Klicks: Geräteunabhängige Events

Ein häufiger Fehler ist die Verwendung von Events, die an ein bestimmtes Eingabegerät gebunden sind. `mouseover` und `mouseout` sind die klassischen Kandidaten. Sie funktionieren wunderbar mit einer Maus, aber was passiert auf einem Touchscreen? Nichts. Was passiert, wenn ein Nutzer per Tastatur navigiert? Auch nichts.

Wenn du Inhalte einblenden möchtest, sobald ein Element aktiv wird (z. B. ein Tooltip), nutze stattdessen die `focus`- und `blur`-Events. Diese werden ausgelöst, wenn ein Element den Fokus erhält oder verliert, egal ob per Maus, Tastatur oder Touch.

**Beispiel für einen barrierefreien Tooltip:**

```html
<button id="infoButton" aria-describedby="tooltip">Mehr Infos</button>
<div id="tooltip" role="tooltip" class="tooltip-hidden">
  Dies ist eine wichtige Information.
</div>
```

```css
.tooltip-hidden {
  display: none;
}
```

```javascript
const button = document.getElementById('infoButton');
const tooltip = document.getElementById('tooltip');

function showTooltip() {
  tooltip.classList.remove('tooltip-hidden');
}

function hideTooltip() {
  tooltip.classList.add('tooltip-hidden');
}

// Kombination für Maus- und Tastaturnutzer
button.addEventListener('mouseover', showTooltip);
button.addEventListener('focus', showTooltip);

button.addEventListener('mouseout', hideTooltip);
button.addEventListener('blur', hideTooltip);
```

Indem du sowohl `mouseover`/`mouseout` als auch `focus`/`blur` verwendest, stellst du sicher, dass der Tooltip für Maus- *und* Tastaturnutzer sichtbar wird.

Noch moderner sind die **Pointer Events** (`pointerdown`, `pointerup`, `pointerover` etc.). Sie fassen Maus-, Touch- und Stift-Ereignisse unter einer einheitlichen API zusammen und sind eine hervorragende Wahl für geräteunabhängige Interaktionen.

#### Klarheit schaffen: Wenn Events die Seite verändern

Oft führt ein Event dazu, dass sich der Inhalt der Seite dynamisch ändert. Eine neue Liste mit Suchergebnissen wird geladen, eine Erfolgsmeldung erscheint oder ein Fehler wird angezeigt. Für sehende Nutzer sind diese Änderungen offensichtlich. Für Nutzer von Screenreadern sind sie unsichtbar, wenn du nicht explizit darauf hinweist.

**Fokus auf das Wesentliche lenken**

Wenn ein Nutzer eine Aktion auslöst, die ein neues Element auf der Seite erzeugt (z.B. ein Modal-Fenster öffnet), sollte der Fokus programmatisch auf dieses neue Element verschoben werden. Andernfalls bleibt der Fokus auf dem ursprünglichen Button "hinter" dem Modal. Der Nutzer ist visuell und funktional gefangen.

```javascript
function openModal() {
  const modal = document.getElementById('myModal');
  modal.style.display = 'block';

  // Finde das erste fokussierbare Element im Modal und setze den Fokus
  const closeButton = modal.querySelector('button');
  closeButton.focus(); 
}
```
Durch den Aufruf von `closeButton.focus()` springt der Screenreader und die Tastaturnavigation direkt in das Modal.

**Screenreader über Änderungen informieren mit ARIA-Live**

Für Änderungen, die keinen Fokuswechsel erfordern (wie eine Statusmeldung), kannst du ARIA-Live-Regionen verwenden. Ein Element mit dem Attribut `aria-live` wird von Screenreadern "beobachtet". Jede textliche Änderung innerhalb dieses Elements wird dem Nutzer vorgelesen.

*   `aria-live="polite"`: Der Screenreader wartet, bis der Nutzer eine Pause macht, und liest die Änderung dann vor. Dies ist die häufigste und empfohlene Einstellung.
*   `aria-live="assertive"`: Der Screenreader unterbricht die aktuelle Ausgabe sofort und liest die Änderung vor. Nutze dies nur für sehr wichtige, zeitkritische Warnungen (z.B. "Ihre Sitzung läuft in einer Minute ab").

**Beispiel für eine Statusmeldung:**

```html
<button id="addItemButton">Zum Warenkorb hinzufügen</button>
<div id="statusMessage" aria-live="polite" role="status"></div>
```

```javascript
const addButton = document.getElementById('addItemButton');
const statusMessage = document.getElementById('statusMessage');

addButton.addEventListener('click', () => {
  // Simuliert das Hinzufügen eines Artikels
  statusMessage.textContent = "Artikel wurde erfolgreich zum Warenkorb hinzugefügt.";

  // Optional: Nachricht nach einiger Zeit wieder ausblenden
  setTimeout(() => {
    statusMessage.textContent = "";
  }, 5000);
});
```

Wenn der Nutzer nun auf den Button klickt, verändert sich der Text im `div`. Dank `aria-live="polite"` liest der Screenreader vor: "Artikel wurde erfolgreich zum Warenkorb hinzugefügt", ohne dass der Nutzer seinen aktuellen Fokus verliert.

Barrierefreiheit bei Events ist kein optionales Extra, sondern ein Kernbestandteil professioneller Webentwicklung. Indem du von Anfang an über den Maus-Klick hinausdenkst und semantisches HTML, durchdachte Tastaturbedienung und ARIA-Attribute einsetzt, schaffst du Erlebnisse, die für alle Menschen zugänglich und angenehm zu bedienen sind.
