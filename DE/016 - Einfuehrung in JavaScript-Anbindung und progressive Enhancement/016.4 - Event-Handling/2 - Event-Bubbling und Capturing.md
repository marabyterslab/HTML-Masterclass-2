# Event-Bubbling und Capturing

### Event-Bubbling und Capturing: Die Reise eines Ereignisses durch den DOM

Stell dir vor, du klickst auf einen Button auf einer Webseite. Für dich ist das eine einzige, simple Aktion. Für den Browser ist es der Beginn einer kleinen Reise. Das Klick-Ereignis (oder „Event“) entsteht nicht nur isoliert auf dem Button, sondern es wandert durch die Struktur deiner HTML-Seite, den sogenannten Document Object Model (DOM). Dieses Wandern, auch Event-Propagation genannt, ist ein fundamentales Konzept im Event-Handling und findet in zwei Phasen statt: dem Capturing und dem Bubbling.

Das Verständnis dieser beiden Phasen ist entscheidend, denn es gibt dir die volle Kontrolle darüber, wann und wo du auf ein Ereignis reagierst.

#### Event-Bubbling – Der Weg nach oben

Beginnen wir mit der Phase, die du im Alltag am häufigsten antreffen und nutzen wirst: das Event-Bubbling. Der Name beschreibt den Prozess perfekt. Wie eine Luftblase, die im Wasser nach oben steigt, wandert das Event vom auslösenden Element (dem „Target“) die Hierarchie des DOM-Baums hinauf.

Schauen wir uns eine einfache HTML-Struktur an:

```html
<div id="aussen">
  <div id="mitte">
    <button id="innen">Klick mich!</button>
  </div>
</div>
```

Hier haben wir einen Button, der in zwei `div`-Elemente verschachtelt ist. Wenn du nun auf den Button klickst, passiert Folgendes:

1.  Zuerst wird das Klick-Ereignis auf dem `<button>` selbst ausgelöst.
2.  Danach „blubbert“ das Ereignis nach oben zum nächsten Elternelement, dem `div` mit der ID `mitte`. Dort wird ebenfalls ein Klick-Ereignis ausgelöst.
3.  Anschließend geht die Reise weiter zum `div` mit der ID `aussen`.
4.  Danach geht es weiter zum `<body>`, zum `<html>` und schließlich zum `document` und zum `window`-Objekt.

Dieses Verhalten ist der Standard in allen modernen Browsern. Wenn du einen Event-Listener mit `addEventListener()` hinzufügst, ohne spezielle Optionen anzugeben, wird er immer in der Bubbling-Phase ausgeführt.

Lass uns das mit etwas JavaScript sichtbar machen:

```javascript
const aussen = document.getElementById('aussen');
const mitte = document.getElementById('mitte');
const innen = document.getElementById('innen');

aussen.addEventListener('click', () => {
  console.log('Klick auf AUSSEN (Bubbling)');
});

mitte.addEventListener('click', () => {
  console.log('Klick auf MITTE (Bubbling)');
});

innen.addEventListener('click', () => {
  console.log('Klick auf INNEN (Bubbling)');
});
```

Wenn du jetzt auf den Button (`#innen`) klickst, siehst du in der Konsole folgende Ausgabe:

```
Klick auf INNEN (Bubbling)
Klick auf MITTE (Bubbling)
Klick auf AUSSEN (Bubbling)
```

Die Reihenfolge bestätigt es: Das Event startet beim innersten Element und wandert nach oben.

**Wofür ist das nützlich?**
Dieses Verhalten ist die Grundlage für ein unglaublich mächtiges Muster namens **Event-Delegation**. Anstatt jedem einzelnen Kind-Element einen eigenen Event-Listener zu geben (was bei hunderten Elementen ineffizient wäre), kannst du einen einzigen Listener am Elternelement anbringen. Dank des Bubblings fängst du dort alle Klicks auf, die von den Kindern nach oben steigen. Innerhalb des Listeners kannst du dann über das `event.target`-Objekt herausfinden, welches Kind-Element ursprünglich geklickt wurde.

#### Event-Capturing – Die selten genutzte Abwärtsbewegung

Bevor das Bubbling überhaupt beginnt, findet eine andere Phase statt: die Capturing-Phase. Sie ist das genaue Gegenteil des Bubblings. Hier wandert das Ereignis den DOM-Baum von oben nach unten, vom `window`-Objekt bis hin zum Elternelement des Ziels.

1.  Das Klick-Ereignis startet beim `window`-Objekt.
2.  Es wandert hinunter zum `document`, zum `<html>`, zum `<body>`.
3.  Dann erreicht es das `div` mit der ID `aussen`.
4.  Danach das `div` mit der ID `mitte`.
5.  Die Capturing-Phase endet beim direkten Elternelement des Ziels. Das Ziel selbst wird in der nächsten Phase behandelt.

Standardmäßig werden Event-Listener nicht in der Capturing-Phase ausgeführt. Sie ignorieren diese Abwärtsbewegung komplett. Du musst dem Browser explizit sagen, dass ein Listener auf dieser Reise nach unten lauschen soll. Das tust du, indem du dem `addEventListener()` als dritten Parameter ein `true` mitgibst.

```javascript
element.addEventListener('click', meineFunktion, true); // Aktiviert Capturing
```

Passen wir unser Beispiel von oben an, um die Listener für die Capturing-Phase zu registrieren:

```javascript
const aussen = document.getElementById('aussen');
const mitte = document.getElementById('mitte');
const innen = document.getElementById('innen');

aussen.addEventListener('click', () => {
  console.log('Klick auf AUSSEN (Capturing)');
}, true); // Dritter Parameter ist true

mitte.addEventListener('click', () => {
  console.log('Klick auf MITTE (Capturing)');
}, true); // Dritter Parameter ist true

innen.addEventListener('click', () => {
  console.log('Klick auf INNEN (Capturing)');
}, true); // Dritter Parameter ist true
```

Wenn du jetzt wieder auf den Button klickst, ist die Ausgabe in der Konsole genau umgekehrt:

```
Klick auf AUSSEN (Capturing)
Klick auf MITTE (Capturing)
Klick auf INNEN (Capturing)
```

Das Event wird zuerst vom äußersten Element „gefangen“ und wandert dann nach innen.

**Wofür ist das nützlich?**
Die Capturing-Phase wird in der Praxis selten verwendet. Sie ist jedoch nützlich in speziellen Szenarien, in denen du sicherstellen musst, ein Ereignis abzufangen, bevor es sein eigentliches Ziel erreicht. Stell dir vor, du möchtest eine bestimmte Aktion unterbinden, egal, welches Kind-Element geklickt wird. Mit einem Capturing-Listener auf einem äußeren Container kannst du das Event frühzeitig abfangen und seine weitere Ausbreitung stoppen.

#### Die drei Phasen des Event-Flusses

Jetzt fügen wir alles zusammen. Der vollständige Event-Fluss, wie er vom W3C-Standard definiert ist, besteht aus drei Phasen:

1.  **Capturing-Phase:** Das Event wandert vom `window`-Objekt den DOM-Baum hinab bis zum Elternelement des Ziels. Event-Listener, die mit `useCapture: true` registriert wurden, werden in dieser Phase ausgeführt.
2.  **Target-Phase:** Das Event erreicht das Ziel-Element (`event.target`), also das Element, das die Aktion direkt ausgelöst hat (z. B. der geklickte Button). In dieser Phase werden alle Listener auf dem Ziel-Element ausgeführt, unabhängig davon, ob sie für Capturing oder Bubbling registriert wurden. Die Reihenfolge ihrer Ausführung entspricht der Reihenfolge, in der sie hinzugefügt wurden.
3.  **Bubbling-Phase:** Das Event wandert vom Elternelement des Ziels wieder den DOM-Baum hinauf bis zum `window`-Objekt. Event-Listener, die standardmäßig (oder mit `useCapture: false`) registriert wurden, werden in dieser Phase ausgeführt.

Wenn du also Listener für beide Phasen auf denselben Elementen registrierst, siehst du den kompletten Zyklus.

#### Die Reise anhalten – `event.stopPropagation()`

Manchmal möchtest du nicht, dass ein Event seine Reise fortsetzt. Wenn ein Klick auf den inneren Button stattfindet, soll vielleicht der äußere Container davon nichts mitbekommen. Genau dafür gibt es die Methode `event.stopPropagation()`.

Wenn du diese Methode innerhalb eines Event-Listeners aufrufst, wird die weitere Propagation des Events sofort gestoppt. Befindet sich das Event gerade in der Capturing-Phase, wird die Target- und Bubbling-Phase nie erreicht. Befindet es sich in der Bubbling-Phase, wandert es nicht weiter nach oben.

```javascript
mitte.addEventListener('click', (event) => {
  console.log('Klick auf MITTE (Bubbling)');
  event.stopPropagation(); // Stoppt die weitere Reise nach oben
});

// Der Listener auf 'aussen' wird nun nicht mehr ausgelöst,
// wenn auf 'mitte' oder 'innen' geklickt wird.
```

Klickst du jetzt auf den Button `#innen`, bekommst du folgende Ausgabe:

```
Klick auf INNEN (Bubbling)
Klick auf MITTE (Bubbling)
```

Der Listener auf `#aussen` wird nie erreicht, weil das Event bei `#mitte` gestoppt wurde.

Eine noch stärkere Variante ist `event.stopImmediatePropagation()`. Diese Methode tut alles, was `stopPropagation()` tut, und verhindert zusätzlich, dass weitere Event-Listener auf *demselben Element* für dasselbe Ereignis ausgeführt werden.

#### Die Standardaktion verhindern – `event.preventDefault()`

Eine weitere wichtige Methode im Event-Handling ist `event.preventDefault()`. Sie wird oft mit `stopPropagation()` verwechselt, hat aber eine völlig andere Aufgabe.

Viele HTML-Elemente haben ein Standardverhalten im Browser. Ein Klick auf einen Link (`<a>`) lädt eine neue Seite. Ein Klick auf einen Submit-Button in einem Formular (`<form>`) sendet das Formular ab und lädt die Seite neu. Mit `event.preventDefault()` kannst du genau dieses Standardverhalten unterbinden.

```html
<a id="meinLink" href="https://example.com">Dieser Link wird nicht navigieren</a>
```

```javascript
const meinLink = document.getElementById('meinLink');

meinLink.addEventListener('click', (event) => {
  console.log('Link geklickt, aber Navigation verhindert.');
  event.preventDefault(); // Verhindert das Standardverhalten des Links
});
```

Wenn du auf diesen Link klickst, wird die Nachricht in der Konsole erscheinen, aber der Browser wird nicht zur `example.com`-Seite navigieren.

**Der entscheidende Unterschied:** `preventDefault()` stoppt das **Standardverhalten** des Browsers. `stopPropagation()` stoppt die **Weiterleitung des Events** im DOM. Ein Event kann seine Reise durch den DOM fortsetzen (bubbling), auch wenn seine Standardaktion verhindert wurde, und umgekehrt. Es sind zwei voneinander unabhängige Kontrollmechanismen, die dir die volle Macht über die Interaktionen auf deiner Webseite geben.
