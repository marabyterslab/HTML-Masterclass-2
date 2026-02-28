# Vergessene Zustandsänderungen

### Vergessene Zustandsänderungen: Wenn die Oberfläche schweigt

Stell dir vor, du betätigst einen Lichtschalter in einem dunklen Raum. Du drückst ihn, aber es gibt kein Klicken. Kein Geräusch, kein haptisches Feedback. Das Licht geht zwar an, aber für einen kurzen, verwirrenden Moment bist du unsicher, ob deine Aktion erfolgreich war. Du musst auf das visuelle Ergebnis – das Licht selbst – warten, um sicherzugehen.

Im Webdesign passiert genau das ständig, nur dass die Konsequenzen für manche Menschen weitaus gravierender sind. Ein interaktives Element, zum Beispiel ein Menü-Button, wird geklickt. Visuell klappt ein Menü auf. Für einen sehenden Nutzer ist die Sache klar. Für eine Person, die einen Screenreader verwendet, passiert jedoch … nichts. Stille. Der Button hat seinen Zustand von „geschlossen“ zu „geöffnet“ geändert, aber er hat es niemandem mitgeteilt.

Dieses Schweigen der Benutzeroberfläche ist eine der häufigsten und frustrierendsten Barrieren im Web. Du als Entwickler hast die visuelle Zustandsänderung implementiert, oft mit CSS-Klassen, aber vergessen, diese Änderung auch auf der semantischen Ebene für assistierende Technologien (AT) nachzuvollziehen. Das ist ein klassischer ARIA-Fehler: Die visuelle Realität und die semantische Realität driften auseinander.

Die Brücke zwischen diesen beiden Welten schlagen die ARIA-Zustandsattribute. Sie sind das „Klicken“ des Lichtschalters. Sie ändern nichts am Aussehen oder an der Funktionalität deines Codes, aber sie geben assistierenden Technologien das entscheidende Feedback, das sie benötigen, um den aktuellen Zustand eines Elements korrekt zu vermitteln. Die Pflege dieser Attribute ist keine Magie, sondern eine simple, aber unverzichtbare Aufgabe, die fast immer mit JavaScript erledigt wird.

#### Aufgeklappt oder zugeklappt? `aria-expanded`

Der häufigste Anwendungsfall für vergessene Zustandsänderungen sind auf- und zuklappbare Elemente, wie Akkordeons, mobile Navigationsmenüs oder Dropdown-Listen. Visuell ist sofort klar, ob ein Bereich sichtbar oder verborgen ist. Ein Screenreader weiß davon aber nichts, es sei denn, du sagst es ihm.

Betrachten wir ein typisches Akkordeon-Element. Es besteht aus einem Button, der einen Inhaltsbereich steuert.

**Der Ausgangspunkt (fehlerhaft):**

```html
<button class="accordion-trigger">
  Kapitel 1: Die Grundlagen
</button>
<div class="accordion-panel">
  <p>Hier steht der Inhalt von Kapitel 1...</p>
</div>
```

Dein JavaScript könnte so aussehen:

```javascript
const trigger = document.querySelector('.accordion-trigger');
const panel = document.querySelector('.accordion-panel');

trigger.addEventListener('click', () => {
  // Ändert nur die visuelle Darstellung
  panel.classList.toggle('is-open'); 
});
```

Ein sehender Nutzer klickt den Button, die Klasse `is-open` wird hinzugefügt, und per CSS wird `.accordion-panel.is-open` sichtbar gemacht. Für einen Screenreader-Nutzer ist der Button aber immer noch einfach nur ein Button mit dem Namen „Kapitel 1: Die Grundlagen“. Ob das Panel nun offen oder geschlossen ist, bleibt ein Geheimnis.

**Die korrekte Implementierung mit `aria-expanded`:**

Um diesen Zustand zu kommunizieren, fügst du dem steuernden Element – dem Button – das Attribut `aria-expanded` hinzu.

```html
<button class="accordion-trigger" 
        aria-expanded="false" 
        aria-controls="panel-1">
  Kapitel 1: Die Grundlagen
</button>
<div id="panel-1" class="accordion-panel" hidden>
  <p>Hier steht der Inhalt von Kapitel 1...</p>
</div>
```

Beachte die zwei wichtigen Ergänzungen:
1.  `aria-expanded="false"` signalisiert den Anfangszustand: Das Panel ist geschlossen.
2.  `aria-controls="panel-1"` verknüpft den Button explizit mit dem Panel, das er steuert. Das ist nicht zwingend für die Zustandsmitteilung, aber eine wichtige Verbesserung der Semantik.
3.  Das Panel selbst hat anfangs das `hidden`-Attribut, was es sowohl visuell als auch für AT versteckt.

Jetzt muss dein JavaScript nicht nur die Klasse, sondern auch das ARIA-Attribut aktualisieren.

```javascript
const trigger = document.querySelector('.accordion-trigger');
const panel = document.querySelector('#panel-1');

trigger.addEventListener('click', () => {
  const isExpanded = trigger.getAttribute('aria-expanded') === 'true';

  // Wechsle den ARIA-Zustand
  trigger.setAttribute('aria-expanded', !isExpanded);
  
  // Wechsle die Sichtbarkeit des Panels
  panel.hidden = !panel.hidden;
});
```
*Anmerkung: Die visuelle Darstellung (z. B. durch Entfernen des `hidden`-Attributs und CSS-Transitions) kannst du weiterhin über Klassen steuern. Wichtig ist die Synchronisation von visueller Darstellung und ARIA-Zustand.*

Was hört der Screenreader nun?
*   Vor dem Klick: „Kapitel 1: Die Grundlagen, Button, eingeklappt.“
*   Nach dem Klick: „Kapitel 1: Die Grundlagen, Button, ausgeklappt.“

Der Nutzer weiß jetzt jederzeit, was Sache ist. Er kann bewusst entscheiden, ob er das Panel schließen oder den Inhalt erkunden möchte. Du hast das Schweigen gebrochen.

#### An oder aus? `aria-checked` und `aria-pressed`

Native HTML-Elemente wie `<input type="checkbox">` oder `<input type="radio">` bringen ihre Zustandsverwaltung von Haus aus mit. Screenreader wissen, wie sie damit umgehen müssen. Sobald du aber beginnst, eigene, komplexe Bedienelemente zu bauen – zum Beispiel einen schicken Toggle-Schalter anstelle einer drögen Checkbox –, übernimmst du auch die volle Verantwortung für die Kommunikation seiner Zustände.

Ein häufiges Beispiel ist ein Schalter, der aus einem `<div>` oder `<button>` gebaut wird.

**Der Ausgangspunkt (fehlerhaft):**

```html
<div class="toggle-switch" role="button" tabindex="0">
  <span class="toggle-handle"></span>
</div>
```

Dein JavaScript fügt vielleicht eine Klasse `.is-active` hinzu, die den Griff nach rechts schiebt und die Hintergrundfarbe ändert. Der Screenreader weiß davon aber nichts. Für ihn ist es nur ein klickbares `div` oder ein einfacher Button.

**Die korrekte Implementierung mit `role="switch"` und `aria-checked`:**

Wir geben dem Element zuerst eine passende Rolle und dann den dazugehörigen Zustand.

```html
<button class="toggle-switch" 
        role="switch" 
        aria-checked="false">
  Benachrichtigungen aktivieren
</button>
```

Die `role="switch"` teilt dem Screenreader mit: „Hey, dieses Ding hier funktioniert wie ein An/Aus-Schalter.“ Das Attribut `aria-checked` übernimmt dann die Kommunikation des Zustands. `false` bedeutet „aus“, `true` bedeutet „an“.

Dein JavaScript muss diesen Zustand bei jeder Interaktion aktualisieren.

```javascript
const aSwitch = document.querySelector('[role="switch"]');

aSwitch.addEventListener('click', () => {
  let isChecked = aSwitch.getAttribute('aria-checked') === 'true';
  
  // Wechsle den Zustand
  aSwitch.setAttribute('aria-checked', !isChecked);

  // Hier kommt deine Logik zum visuellen Umschalten hinzu,
  // z.B. das Togglen einer CSS-Klasse.
  aSwitch.classList.toggle('is-on', !isChecked);
});
```

Jetzt kündigt der Screenreader an: „Benachrichtigungen aktivieren, Schalter, aus.“ Nach dem Klick hört der Nutzer: „Benachrichtigungen aktivieren, Schalter, an.“

Ein enger Verwandter ist `aria-pressed`. Dieses Attribut wird für Toggle-Buttons verwendet, die einen Zustand „gedrückt“ oder „nicht gedrückt“ haben können, wie zum Beispiel ein „Fett“-Button in einem Texteditor. Die Logik ist identisch: `aria-pressed="false"` für den Normalzustand, `aria-pressed="true"` für den aktiven/gedrückten Zustand.

#### Ausgewählt oder nicht? `aria-selected`

Ein weiteres klassisches Beispiel sind Tab-Navigationen. Visuell ist immer klar, welcher Tab gerade aktiv ist – er ist oft hervorgehoben und sein Inhaltsbereich ist sichtbar. Diese Information muss aber auch an den Screenreader weitergegeben werden.

Eine semantisch korrekte Tab-Struktur sieht so aus:

```html
<div role="tablist" aria-label="Inhaltsbereiche">
  <button role="tab" aria-selected="true" aria-controls="panel-a" id="tab-a">Tab 1</button>
  <button role="tab" aria-selected="false" aria-controls="panel-b" id="tab-b">Tab 2</button>
  <button role="tab" aria-selected="false" aria-controls="panel-c" id="tab-c">Tab 3</button>
</div>

<div role="tabpanel" aria-labelledby="tab-a" id="panel-a">
  <p>Inhalt von Tab 1...</p>
</div>
<div role="tabpanel" aria-labelledby="tab-b" id="panel-b" hidden>
  <p>Inhalt von Tab 2...</p>
</div>
<div role="tabpanel" aria-labelledby="tab-c" id="panel-c" hidden>
  <p>Inhalt von Tab 3...</p>
</div>
```

Der entscheidende Teil ist das Attribut `aria-selected`. Nur der aktive Tab hat den Wert `true`, alle anderen haben `false`. Wenn der Nutzer nun auf einen anderen Tab klickt, reicht es nicht, nur den sichtbaren `tabpanel` auszutauschen. Dein JavaScript muss die `aria-selected`-Zustände für *alle* Tabs in der `tablist` neu verwalten.

Ein typischer Ablauf im JavaScript wäre:
1.  Ein Klick-Event wird auf einen Tab registriert.
2.  Finde alle Tabs innerhalb der `tablist`.
3.  Setze bei allen Tabs `aria-selected` auf `false`.
4.  Setze nur beim geklickten Tab `aria-selected` auf `true`.
5.  Verstecke alle `tabpanel`-Elemente.
6.  Zeige nur das `tabpanel`-Element an, das zum geklickten Tab gehört.

Damit wird dem Screenreader-Nutzer eine klare Information gegeben: „Tab 2, Tab, 2 von 3.“ Wenn er ihn aktiviert, hört er: „Tab 2, ausgewählt, Tab, 2 von 3.“ So kann er sich mühelos durch die Tabs navigieren, weil er stets über den Status informiert ist.

#### Das Unvermeidliche: JavaScript ist der Hausmeister

Wie du an allen Beispielen siehst: Zustands-ARIA ist keine „Set-it-and-forget-it“-Angelegenheit. Das initiale HTML legt nur den Startzustand fest. Ab der ersten Nutzerinteraktion ist es die alleinige Aufgabe von JavaScript, die ARIA-Attribute synchron zur visuellen Darstellung zu halten.

Wenn du eine Klasse hinzufügst, um etwas aufzuklappen, musst du auch `aria-expanded` auf `true` setzen.
Wenn du eine Klasse entfernst, um etwas zu schließen, musst du auch `aria-expanded` auf `false` setzen.

Dieser Gleichklang ist entscheidend. Jeder visuelle Zustand muss ein semantisches Äquivalent haben. Betrachte ARIA-Zustände als eine Art Kommentar im Code, der nicht für dich, sondern für Maschinen lesbar ist. Und diese Kommentare müssen, genau wie der Code selbst, bei jeder Änderung gepflegt und aktualisiert werden. Geschieht dies nicht, lügt deine Benutzeroberfläche die Nutzer an, die auf sie am meisten angewiesen sind.
