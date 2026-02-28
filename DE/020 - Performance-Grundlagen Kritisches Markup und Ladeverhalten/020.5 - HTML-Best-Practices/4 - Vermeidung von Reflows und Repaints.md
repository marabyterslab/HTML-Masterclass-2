# Vermeidung von Reflows und Repaints

### Vermeidung von Reflows und Repaints

Stell dir vor, dein Browser ist ein unglaublich fleißiger, aber auch sehr gewissenhafter Architekt und Innenarchitekt in einer Person. Wenn er deine HTML- und CSS-Dateien erhält, liest er nicht nur die Baupläne, sondern errichtet sofort ein komplettes Gebäude – deine Webseite. Dieser Prozess, vom leeren Bildschirm zur fertigen Seite, folgt einer klaren Abfolge von Schritten, die als Rendering-Pipeline bezeichnet wird.

Zwei der wichtigsten und rechenintensivsten Schritte in dieser Pipeline sind der **Reflow** (auch Layout genannt) und der **Repaint** (auch Paint genannt). Wenn du verstehst, was sie sind und wie du sie minimieren kannst, hältst du einen mächtigen Schlüssel zur Web-Performance in den Händen. Eine flüssige, reaktionsschnelle Seite ist oft das Ergebnis einer bewussten Vermeidung unnötiger Arbeit für den Browser.

#### Was sind Reflow und Repaint?

Um das zu verstehen, lass uns bei unserer Architekten-Metapher bleiben.

**Reflow (Layout): Das neue Vermessen**

Ein Reflow ist der Prozess, bei dem der Browser die Position und die Geometrie aller Elemente auf der Seite neu berechnet. Stell dir vor, du sagst deinem Architekten: „Diese tragende Wand im Wohnzimmer soll bitte einen Meter weiter nach links.“

Was passiert? Der Architekt kann nicht einfach nur diese eine Wand verschieben. Er muss alles neu berechnen:
*   Die Größe des Wohnzimmers ändert sich.
*   Das Nebenzimmer wird dadurch größer oder kleiner.
*   Die Position der Fenster und Türen in diesen Wänden muss eventuell angepasst werden.
*   Die darüber liegende Etage muss neu gestützt werden.
*   Möglicherweise verschieben sich sogar Elemente in ganz anderen Teilen des Hauses.

Im Browser ist es genauso. Wenn du die Breite eines `div`-Containers änderst, startet ein Reflow. Der Browser muss berechnen, wie sich diese Änderung auf alle nachfolgenden und umschließenden Elemente auswirkt. Passt der Text noch hinein? Muss er umgebrochen werden? Verschieben sich die Elemente darunter? All diese Berechnungen sind teuer und kosten wertvolle Millisekunden.

Typische Auslöser für einen Reflow sind:
*   Änderungen an der Fenstergröße des Browsers.
*   Änderungen an der Schriftgröße.
*   Hinzufügen oder Entfernen von Elementen im DOM.
*   Änderung von CSS-Eigenschaften, die die Geometrie beeinflussen, wie `width`, `height`, `margin`, `padding`, `border`, `position`, `top`, `left` oder `font-size`.
*   Das Abfragen bestimmter berechneter Werte in JavaScript, wie `element.offsetWidth` oder `element.offsetHeight`.

Ein Reflow ist fast immer der kostspieligste Vorgang, den du im Rendering-Prozess auslösen kannst, denn er zieht oft einen Rattenschwanz an Neuberechnungen nach sich.

**Repaint (Paint): Der neue Anstrich**

Nachdem der Architekt alles neu vermessen hat (Reflow), kommt der Maler und streicht die Wände neu an. Das ist der Repaint. Der Browser zeichnet die Pixel der Elemente neu auf den Bildschirm. Das betrifft alles Visuelle: Farben, Hintergründe, Schatten, Umrandungen.

Stell dir vor, du sagst deinem Architekten: „Die Wohnzimmerwand soll nicht mehr weiß, sondern blau sein.“ In diesem Fall müssen keine Wände verschoben werden. Die Raumaufteilung bleibt exakt gleich. Der Maler muss lediglich die betroffene Fläche neu streichen.

Ein Repaint ist weniger aufwändig als ein Reflow, weil die Geometrie der Seite unverändert bleibt. Trotzdem kostet auch dieser Vorgang Zeit und Rechenleistung.

Typische Auslöser für einen Repaint (ohne vorherigen Reflow) sind Änderungen an visuellen CSS-Eigenschaften wie:
*   `background-color`
*   `color`
*   `visibility`
*   `outline`
*   `box-shadow`

Jeder Reflow löst zwangsläufig auch einen Repaint aus, denn wenn sich die Geometrie eines Elements ändert, müssen seine Pixel natürlich neu gezeichnet werden. Ein Repaint kann aber auch für sich allein stattfinden.

#### Strategien zur Vermeidung unnötiger Arbeit

Dein Ziel als Entwickler ist es, den Browser so wenig wie möglich zu zwingen, die Seite neu zu vermessen und zu streichen. Hier sind die effektivsten Techniken, um das zu erreichen.

##### 1. DOM-Änderungen intelligent bündeln

Eine der häufigsten Ursachen für Performance-Probleme ist die wiederholte Manipulation des DOM in einer Schleife. Jedes Mal, wenn du ein Element zum sichtbaren DOM hinzufügst, kann das einen Reflow auslösen.

**Schlechter Ansatz:** Hinzufügen von Elementen in einer Schleife.

```javascript
const list = document.getElementById('my-list');
const data = ['Eintrag 1', 'Eintrag 2', 'Eintrag 3', 'Eintrag 4', 'Eintrag 5'];

for (let i = 0; i < data.length; i++) {
  const listItem = document.createElement('li');
  listItem.textContent = data[i];
  list.appendChild(listItem); // Löst potenziell 5 Reflows/Repaints aus
}
```

In diesem Beispiel wird bei jedem Schleifendurchlauf das `ul`-Element verändert, was den Browser jedes Mal zu einer Neuberechnung zwingen kann.

**Besserer Ansatz:** Ein `DocumentFragment` verwenden.

Ein `DocumentFragment` ist wie ein leichtgewichtiger Container, der im Speicher existiert, aber nicht Teil des sichtbaren DOM ist. Du kannst alle deine Änderungen in diesem Fragment vornehmen und es dann in einem einzigen Schritt in das DOM einfügen.

```javascript
const list = document.getElementById('my-list');
const data = ['Eintrag 1', 'Eintrag 2', 'Eintrag 3', 'Eintrag 4', 'Eintrag 5'];

// Erstelle ein DocumentFragment
const fragment = document.createDocumentFragment();

for (let i = 0; i < data.length; i++) {
  const listItem = document.createElement('li');
  listItem.textContent = data[i];
  fragment.appendChild(listItem); // Änderungen passieren im Speicher
}

// Füge das Fragment in einem einzigen Schritt zum DOM hinzu
list.appendChild(fragment); // Löst nur einen einzigen Reflow/Repaint aus
```

Dieser Ansatz reduziert fünf potenzielle Reflows auf einen einzigen – ein gewaltiger Performance-Gewinn bei großen Datenmengen.

##### 2. CSS-Änderungen über Klassen statt Inline-Styles vornehmen

Wenn du mehrere CSS-Eigenschaften eines Elements mit JavaScript ändern musst, vermeide es, jede Eigenschaft einzeln zu setzen.

**Schlechter Ansatz:** Mehrere Inline-Styles setzen.

```javascript
const box = document.getElementById('my-box');

// Jede Zuweisung kann den Browser zur Neuberechnung zwingen
box.style.width = '200px';
box.style.height = '200px';
box.style.border = '1px solid black';
```

**Besserer Ansatz:** Eine CSS-Klasse umschalten.

Definiere die gewünschten Stile in einer CSS-Klasse und füge diese Klasse dann mit JavaScript hinzu. Der Browser ist darauf optimiert, die Änderungen, die durch das Hinzufügen einer Klasse entstehen, in einem Rutsch zu berechnen.

```css
.box-active {
  width: 200px;
  height: 200px;
  border: 1px solid black;
}
```

```javascript
const box = document.getElementById('my-box');

// Füge die Klasse hinzu. Der Browser bündelt die Änderungen.
box.classList.add('box-active');
```

##### 3. Layout-Thrashing vermeiden

Layout-Thrashing (manchmal auch "Forced Synchronous Layout" genannt) ist ein besonders heimtückischer Performance-Fresser. Er tritt auf, wenn du in deinem JavaScript-Code abwechselnd DOM-Eigenschaften liest und schreibst.

Wenn du eine Geometrie-Eigenschaft wie `element.offsetWidth` abfragst, muss der Browser sicherstellen, dass er dir den aktuellsten Wert zurückgibt. Falls du kurz zuvor eine Stiländerung vorgenommen hast, die das Layout beeinflusst, muss der Browser den anstehenden Reflow *sofort* und *synchron* ausführen, um deine Frage zu beantworten.

**Schlechter Ansatz (Layout-Thrashing):** Lesen und Schreiben in einer Schleife.

```javascript
const elements = document.querySelectorAll('.my-element');

for (let i = 0; i < elements.length; i++) {
  // 1. Lesen: Fordert einen sofortigen Reflow an, um die Breite zu ermitteln
  const currentWidth = elements[i].offsetWidth; 
  
  // 2. Schreiben: Ändert das Layout
  elements[i].style.width = (currentWidth + 10) + 'px'; 
}
```

In diesem Code wird in jeder Iteration zuerst ein Layout-Wert gelesen (`offsetWidth`), was einen Reflow erzwingt. Direkt danach wird ein Wert geschrieben (`style.width`), der das Layout ungültig macht. In der nächsten Iteration wiederholt sich das Spiel. Das ist extrem ineffizient.

**Besserer Ansatz:** Lesen und Schreiben trennen.

Die Lösung ist einfach: Führe zuerst alle Leseoperationen durch und danach alle Schreiboperationen.

```javascript
const elements = document.querySelectorAll('.my-element');
const widths = [];

// 1. Phase: Nur lesen
for (let i = 0; i < elements.length; i++) {
  widths.push(elements[i].offsetWidth);
}

// 2. Phase: Nur schreiben
for (let i = 0; i < elements.length; i++) {
  elements[i].style.width = (widths[i] + 10) + 'px';
}
```

Hier wird der Browser nur einen einzigen Reflow am Anfang der Lese-Phase durchführen (falls nötig) und dann alle Schreibvorgänge bündeln, was zu einem weiteren, einzelnen Reflow führt. Das "Thrashing" wird komplett vermieden.

##### 4. Animationen mit `transform` und `opacity`

Moderne Browser sind clever. Sie können bestimmte Elemente auf separate Ebenen (sogenannte Compositor Layers) auslagern, die von der Grafikkarte (GPU) direkt verwaltet werden. Änderungen an diesen Ebenen sind unglaublich schnell, weil sie weder einen Reflow noch einen Repaint der restlichen Seite auslösen. Es ist, als würdest du eine Folie über ein gemaltes Bild legen und nur die Folie bewegen.

Die beiden CSS-Eigenschaften, die fast immer auf einer solchen separaten Ebene ausgeführt werden können, sind `transform` und `opacity`.

Wenn du ein Element animieren möchtest, zum Beispiel um es zu verschieben:

**Schlechter Ansatz:** Positionseigenschaften wie `left` oder `top` animieren.

```css
.box-animation {
  position: relative;
  animation: move-right 3s infinite;
}

@keyframes move-right {
  from { left: 0; }
  to { left: 300px; }
}
```

Die Animation von `left` löst bei jedem Frame einen Reflow aus, weil der Browser die Position des Elements im Layout-Fluss der Seite neu berechnen muss. Das Ergebnis sind oft ruckelnde Animationen.

**Besserer Ansatz:** `transform` verwenden.

```css
.box-animation {
  animation: move-right-transform 3s infinite;
}

@keyframes move-right-transform {
  from { transform: translateX(0); }
  to { transform: translateX(300px); }
}
```

Die Animation mit `transform: translateX()` verschiebt das Element visuell, ohne seine Position im Layout der Seite zu verändern. Der Browser kann das Element auf eine eigene Ebene legen und die Verschiebung komplett der GPU überlassen. Das Ergebnis ist eine butterweiche Animation, selbst auf leistungsschwächeren Geräten.

Die gleiche Regel gilt für das Ein- und Ausblenden von Elementen. Animiere `opacity` statt `display` oder `visibility`, wenn du eine weiche Überblendung wünschst.

Als Faustregel gilt: Wenn du etwas visuell bewegen, skalieren, drehen oder seine Deckkraft ändern willst, greife immer zuerst zu `transform` und `opacity`. Spare dir die layout-intensiven Eigenschaften für statische Zustände. Mit der CSS-Eigenschaft `will-change: transform, opacity;` kannst du dem Browser zusätzlich einen Hinweis geben, dass du vorhast, diese Eigenschaften zu animieren, sodass er sich frühzeitig darauf vorbereiten kann. Setze diese Eigenschaft jedoch sparsam ein, da sie auch Speicherressourcen verbraucht.
