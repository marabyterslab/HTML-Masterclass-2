# Positionierung

### Positionierung: Elemente gezielt platzieren

Bisher hast du gelernt, wie Elemente im HTML-Dokument auf natürliche Weise angeordnet werden. Block-Elemente wie `div` oder `p` nehmen die volle Breite ein und stapeln sich untereinander. Inline-Elemente wie `span` oder `a` reihen sich wie Wörter in einem Satz aneinander. Dieser natürliche Fluss, der sogenannte *Normal Flow*, ist die Grundlage jedes Web-Layouts.

Doch was, wenn du ein Element an einer ganz bestimmten Stelle platzieren möchtest, unabhängig von seinen Nachbarn? Was, wenn ein Logo eine Bildecke überlappen soll oder eine Navigationsleiste beim Scrollen am oberen Bildschirmrand kleben bleiben muss? An diesem Punkt verlässt du den normalen Dokumentenfluss und betrittst die Welt der CSS-Positionierung. Das zentrale Werkzeug dafür ist die Eigenschaft `position`.

#### Der Normalzustand: `position: static;`

Jedes Element auf deiner Webseite hat standardmäßig den Wert `position: static;`. Das bedeutet nichts anderes, als dass es sich genau an die Regeln des *Normal Flow* hält. Es wird so dargestellt, wie es im HTML-Code erscheint, ohne besondere Eingriffe. Wenn du einem `static`-Element Eigenschaften wie `top`, `left`, `bottom` oder `right` gibst, werden diese einfach ignoriert. `static` ist der Ausgangspunkt, der unberührte Zustand.

```css
.mein-element {
  position: static; /* Das ist der Standardwert, du musst ihn nie explizit setzen. */
}
```

Da dies der Standard ist, wirst du diese Regel in der Praxis so gut wie nie schreiben. Es ist jedoch wichtig zu wissen, dass dies die Basis ist, von der alle anderen Positionierungsarten abweichen.

#### Der sanfte Schubs: `position: relative;`

Stell dir vor, du möchtest ein Element nur ein kleines Stück von seiner ursprünglichen Position verschieben, ohne das restliche Layout durcheinanderzubringen. Hier kommt `position: relative;` ins Spiel.

Ein relativ positioniertes Element verhält sich zunächst wie ein `static`-Element. Der entscheidende Unterschied ist: Es hört nun auf die Koordinaten-Eigenschaften `top`, `right`, `bottom` und `left`. Mit diesen kannst du es von seiner *ursprünglichen Position im Normal Flow* aus verschieben.

Das Wichtigste dabei ist: Der Platz, den das Element ursprünglich eingenommen hat, bleibt für es reserviert. Die anderen Elemente verhalten sich so, als wäre das verschobene Element noch an seinem alten Platz. Es hinterlässt quasi einen leeren "Schatten".

```html
<div class="container">
  <div class="box eins">Box 1</div>
  <div class="box zwei">Box 2 (relativ)</div>
  <div class="box drei">Box 3</div>
</div>
```

```css
.box {
  width: 100px;
  height: 100px;
  border: 1px solid black;
}

.zwei {
  position: relative;
  top: 20px;
  left: 30px;
  background-color: lightblue;
}
```

In diesem Beispiel wird "Box 2" um 20 Pixel nach unten und 30 Pixel nach rechts von ihrer normalen Position verschoben. "Box 3" rückt jedoch nicht auf, sondern bleibt dort, wo sie wäre, wenn "Box 2" nicht verschoben worden wäre.

Doch `position: relative;` hat noch eine zweite, fundamental wichtige Aufgabe: Es erschafft einen neuen **Positionierungskontext** für seine Kind-Elemente. Das wird gleich im nächsten Abschnitt entscheidend.

#### Der Ausbruch aus dem Fluss: `position: absolute;`

Mit `position: absolute;` nimmst du ein Element vollständig aus dem *Normal Flow* heraus. Es ist, als würdest du es aus dem Dokument heben und es schwebt nun darüber. Die anderen Elemente rücken zusammen und füllen den Platz, den das absolute Element zuvor eingenommen hat. Sie ignorieren seine Existenz im Layout komplett.

Wo genau schwebt dieses Element nun? Ein absolut positioniertes Element orientiert sich am nächstgelegenen Vorfahren-Element (Eltern-, Großeltern-Element usw.), das eine andere Position als `static` besitzt. Das ist meistens ein Element mit `position: relative;`. Findet es keinen solchen Vorfahren, orientiert es sich am `<body>`-Element, also quasi am gesamten sichtbaren Bereich der Webseite.

Hier siehst du die Magie der Kombination von `relative` und `absolute`:

```html
<div class="eltern-element">
  Ich bin das Eltern-Element und schaffe den Kontext.
  <div class="kind-element">
    Ich bin absolut positioniert!
  </div>
</div>
```

```css
.eltern-element {
  position: relative; /* Wichtig! Schafft den Positionierungskontext. */
  width: 400px;
  height: 200px;
  background-color: #eee;
  border: 1px solid #ccc;
}

.kind-element {
  position: absolute;
  top: 10px;
  right: 10px;
  width: 150px;
  background-color: salmon;
}
```

Das `.kind-element` wird nun 10 Pixel vom *oberen* und 10 Pixel vom *rechten Rand des `.eltern-element`* platziert. Hättest du `position: relative;` beim `.eltern-element` weggelassen, würde sich das Kind-Element an der oberen rechten Ecke des Browserfensters ausrichten. Diese Technik ist die Grundlage für unzählige Layout-Muster, wie zum Beispiel Icons in Eingabefeldern oder "Neu"-Badges auf Produktbildern.

#### Der Anker im Fenster: `position: fixed;`

`position: fixed;` ist ein naher Verwandter von `position: absolute;`. Auch hier wird das Element komplett aus dem *Normal Flow* entfernt. Der entscheidende Unterschied ist der Bezugspunkt: Ein fixiertes Element orientiert sich **immer** am Viewport, also am sichtbaren Fenster deines Browsers.

Das bedeutet: Wenn du die Seite scrollst, bleibt ein fixiertes Element immer an derselben Stelle im Fenster kleben. Es bewegt sich nicht mit dem Rest des Inhalts.

Der klassische Anwendungsfall dafür sind Navigationsleisten, die oben am Bildschirmrand fixiert sind, Cookie-Banner am unteren Rand oder ein "Nach oben"-Button, der in der Ecke schwebt.

```html
<header class="main-header">
  Meine fixierte Navigation
</header>
<main>
  <!-- Viel Inhalt, damit man scrollen kann -->
</main>
```

```css
.main-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: white;
  padding: 1rem;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}
```

Mit diesem Code bleibt der Header immer am oberen Rand sichtbar, egal wie weit du nach unten scrollst. Beachte, dass der nachfolgende `<main>`-Inhalt unter den Header rutschen würde. Du müsstest dem `<body>` oder dem `<main>`-Element oft einen `padding-top` oder `margin-top` geben, der der Höhe des fixierten Headers entspricht, um diesen Platz wieder freizugeben.

#### Der clevere Hybrid: `position: sticky;`

`position: sticky;` ist eine moderne und sehr nützliche Mischung aus `relative` und `fixed`. Ein "klebriges" Element verhält sich zunächst wie ein relativ positioniertes Element – es bleibt an seinem Platz im *Normal Flow*.

Sobald du jedoch scrollst und das Element einen bestimmten Punkt im Viewport erreicht (definiert durch `top`, `left` etc.), ändert es sein Verhalten und wird *fixiert*. Es "klebt" dann an dieser Position fest, bis du wieder so weit zurückscrollst, dass sein ursprünglicher Platz im Dokument wieder sichtbar wird. Dann löst es sich und wird wieder zu einem `relative`-Element.

Ein perfektes Beispiel ist eine Überschrift in einem langen Artikel, die am oberen Rand kleben bleibt, während du durch den zugehörigen Abschnitt scrollst.

```html
<article>
  <h2>Abschnitt 1</h2>
  <p>Text von Abschnitt 1...</p>
  
  <h2 class="sticky-headline">Abschnitt 2 (Sticky)</h2>
  <p>Dieser Abschnitt hat eine Überschrift, die beim Scrollen oben kleben bleibt.</p>
  <p>Mehr Text...</p>
  <p>Noch mehr Text...</p>

  <h2>Abschnitt 3</h2>
  <p>Text von Abschnitt 3...</p>
</article>
```

```css
.sticky-headline {
  position: sticky;
  top: 0; /* Dies ist der Trigger-Punkt! */
  background-color: white;
  padding: 0.5rem 0;
}
```

Die Überschrift von "Abschnitt 2" scrollt ganz normal mit, bis ihr oberer Rand den oberen Rand des Viewports (`top: 0;`) berührt. Ab diesem Moment bleibt sie dort fixiert. Wenn du weiter nach unten scrollst und "Abschnitt 3" in den Viewport kommt, wird die "klebrige" Überschrift vom nachfolgenden Inhalt quasi nach oben aus dem Bild geschoben.

#### Ebenen steuern mit `z-index`

Sobald du Elemente aus dem normalen Fluss nimmst, können sie sich überlappen. Aber welches Element liegt oben und welches unten? Normalerweise bestimmt die Reihenfolge im HTML-Code die Stapelreihenfolge: Spätere Elemente liegen über früheren.

Um diese Stapelreihenfolge gezielt zu steuern, gibt es die Eigenschaft `z-index`. Sie funktioniert nur für Elemente, deren `position` nicht `static` ist (also `relative`, `absolute`, `fixed` oder `sticky`).

Der `z-index` akzeptiert Ganzzahlen als Wert. Ein Element mit einem höheren `z-index` wird über einem Element mit einem niedrigeren `z-index` dargestellt. Man kann es sich wie Schichten oder Ebenen auf einer dritten Achse, der Z-Achse, vorstellen, die aus dem Bildschirm herausragt.

```css
.rotes-quadrat {
  position: absolute;
  top: 20px;
  left: 20px;
  width: 100px;
  height: 100px;
  background: red;
  z-index: 10; /* Liegt relativ weit oben */
}

.blaues-quadrat {
  position: absolute;
  top: 60px;
  left: 60px;
  width: 100px;
  height: 100px;
  background: blue;
  z-index: 5; /* Liegt unter dem roten Quadrat */
}
```

Obwohl das blaue Quadrat im HTML vielleicht nach dem roten kommt, würde es in diesem Fall hinter dem roten Quadrat liegen, da sein `z-index` kleiner ist. Du kannst auch negative Werte verwenden, um ein Element hinter seinen nicht-positionierten Geschwisterelementen zu platzieren. Der `z-index` ist ein mächtiges Werkzeug, um komplexe, mehrschichtige Layouts zu erstellen.
