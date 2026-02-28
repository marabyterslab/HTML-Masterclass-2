# Traversierung des DOM

### Traversierung des DOM: Von Knoten zu Knoten navigieren

Stell dir deine HTML-Struktur nicht als flachen Text vor, sondern als einen Stammbaum. An der Wurzel steht das `<html>`-Element. Es hat Kinder wie `<head>` und `<body>`. Der `<body>` wiederum kann viele eigene Kinder haben, zum Beispiel eine `<h1>`, mehrere `<p>`-Elemente und ein `<div>`. Jedes dieser Elemente ist ein **Knoten** (Node) in diesem Baum. Das Document Object Model (DOM) ist genau diese Baumstruktur im Speicher deines Browsers.

Wenn du mit JavaScript auf diese Struktur zugreifen möchtest, wählst du oft zuerst ein Element aus – vielleicht über seine ID oder eine Klasse. Aber was dann? Oft möchtest du von diesem Startpunkt aus zu anderen, benachbarten Elementen gelangen: zum Elternelement, zu seinen Geschwistern oder zu seinen Kindern. Diesen Prozess, sich durch den DOM-Baum zu bewegen, nennt man **Traversierung**. Es ist eine fundamentale Fähigkeit, um dynamisch und flexibel auf deine Webseite zu reagieren.

#### Der Weg nach oben: Elternelemente finden

Jeder Knoten im DOM (außer der Wurzel) hat genau ein Elternelement. Stell es dir wie in einer Familie vor: Du hast Eltern, diese haben wiederum Eltern, und so weiter, bis du bei den Urahnen ankommst. Im DOM ist der Urahn das `document`-Objekt.

Um von einem ausgewählten Element aus nach oben zu navigieren, hast du zwei sehr ähnliche Eigenschaften zur Verfügung: `parentNode` und `parentElement`.

*   `parentNode`: Gibt den Elternknoten zurück. Das kann ein Elementknoten, aber auch der Dokumentknoten selbst sein.
*   `parentElement`: Gibt ebenfalls den Elternknoten zurück, aber **nur**, wenn dieser ein HTML-Element ist. Andernfalls gibt es `null` zurück.

In 99 % der Fälle führen beide zum gleichen Ergebnis und du kannst `parentElement` verwenden, da du meistens von Element zu Element navigieren möchtest.

Nehmen wir an, wir haben folgende HTML-Struktur:

```html
<div id="container">
  <p id="mein-absatz">Hallo Welt!</p>
</div>
```

Mit JavaScript können wir nun vom Absatz zum `<div>`-Container navigieren:

```js
// Zuerst wählen wir unser Startelement aus
const absatz = document.getElementById('mein-absatz');

// Jetzt navigieren wir zum Elternelement
const container = absatz.parentElement;

// Um zu beweisen, dass wir den Container haben, ändern wir seinen Stil
container.style.border = '2px solid red';
```

Wenn du diesen Code ausführst, siehst du, dass der `<div>`-Container einen roten Rahmen erhält. Wir haben ihn nicht direkt ausgewählt, sondern sind vom Kind-Element (`<p>`) zum Eltern-Element (`<div>`) "hochgewandert".

#### Der Weg nach unten: Kindelemente entdecken

Von einem Element nach unten zu navigieren ist genauso wichtig. Hier gibt es eine wichtige Unterscheidung, die oft zu Verwirrung führt: der Unterschied zwischen allen Knoten (`nodes`) und reinen Elementknoten (`elements`).

**1. Alle Kinderknoten mit `childNodes`**

Die Eigenschaft `childNodes` gibt dir eine `NodeList` zurück, die *alle* Kindknoten enthält. Das schließt nicht nur HTML-Elemente (`<p>`, `<div>` etc.) ein, sondern auch Textknoten (selbst Leerzeichen und Zeilenumbrüche im HTML-Code!) und Kommentarknoten.

Betrachten wir dieses Beispiel:

```html
<div id="parent">
  <h2>Titel</h2>
  <p>Ein Text.</p>
  <!-- Ein Kommentar -->
</div>
```

Wenn wir die `childNodes` des `div`-Elements ausgeben, erhalten wir ein überraschendes Ergebnis:

```js
const parentDiv = document.getElementById('parent');
console.log(parentDiv.childNodes);
```

Die Konsole zeigt dir wahrscheinlich eine Liste mit 5 Knoten an:
1.  Ein Textknoten (der Zeilenumbruch und die Einrückung nach dem `<div>`-Tag)
2.  Das `<h2>`-Element
3.  Ein Textknoten (Zeilenumbruch/Einrückung zwischen `</h2>` und `<p>`)
4.  Das `<p>`-Element
5.  Ein Textknoten (Zeilenumbruch/Einrückung nach dem `<p>`)
6.  Ein Kommentarknoten
7.  Ein letzter Textknoten (der Zeilenumbruch vor dem schließenden `</div>`-Tag)

Das ist technisch korrekt, aber für die Praxis oft unhandlich. Du willst meistens nur die echten HTML-Elemente.

**2. Nur Element-Kinder mit `children`**

Hier kommt die `children`-Eigenschaft ins Spiel. Sie gibt eine `HTMLCollection` zurück, die ausschließlich die Kind-**Elemente** enthält. Text- und Kommentarknoten werden ignoriert.

```js
const parentDiv = document.getElementById('parent');
console.log(parentDiv.children);
```

Dieses Mal ist das Ergebnis sauber und erwartbar: eine Sammlung, die nur das `<h2>`- und das `<p>`-Element enthält. In den allermeisten Fällen ist `children` die Eigenschaft, die du suchst.

**Erstes und letztes Kind**

Analog dazu gibt es Eigenschaften, um gezielt auf das erste oder letzte Kind zuzugreifen:

*   `firstChild` und `lastChild`: Geben den ersten/letzten Kindknoten zurück (kann auch ein Textknoten sein).
*   `firstElementChild` und `lastElementChild`: Geben das erste/letzte Kind-**Element** zurück.

Auch hier gilt: Wenn du sicher sein willst, dass du ein HTML-Element bekommst, verwende die `...ElementChild`-Variante.

#### Der Weg zur Seite: Geschwisterelemente ansteuern

Geschwisterelemente (Siblings) sind Knoten, die sich auf derselben Hierarchieebene befinden und denselben Elternknoten haben. In einer Liste (`<ul>`) sind zum Beispiel alle Listenelemente (`<li>`) Geschwister.

Die Navigation funktioniert nach dem gleichen Prinzip wie bei den Kindern.

**1. Nächster und vorheriger Knoten mit `nextSibling` und `previousSibling`**

Diese Eigenschaften bewegen dich zum unmittelbar nächsten oder vorherigen Knoten auf derselben Ebene. Und wieder lauert hier die Falle der Textknoten. Ein Zeilenumbruch zwischen zwei `<li>`-Elementen ist aus Sicht des DOM ein valider `nextSibling`.

**2. Nächstes und vorheriges Element mit `nextElementSibling` und `previousElementSibling`**

Diese beiden Eigenschaften sind deine verlässlichen Helfer. Sie springen zum nächsten oder vorherigen **Geschwister-Element** und überspringen dabei alles, was kein Element ist.

Schauen wir uns ein Listen-Beispiel an:

```html
<ul>
  <li>Erstes Item</li>
  <li id="startpunkt">Zweites Item</li>
  <li>Drittes Item</li>
</ul>
```

Wir starten beim zweiten Item und wollen zum dritten navigieren:

```js
const startLi = document.getElementById('startpunkt');

// Navigiere zum nächsten Geschwister-ELEMENT
const naechstesLi = startLi.nextElementSibling;
naechstesLi.style.color = 'green'; // Das dritte Item wird grün

// Navigiere zum vorherigen Geschwister-ELEMENT
const vorherigesLi = startLi.previousElementSibling;
vorherigesLi.style.color = 'orange'; // Das erste Item wird orange
```

Mit `nextElementSibling` und `previousElementSibling` navigierst du sicher und vorhersehbar durch eine Reihe von gleichrangigen Elementen, ohne dir über unsichtbare Textknoten Gedanken machen zu müssen.

#### Alles kombiniert: Eine praktische Traversierungs-Kette

Die wahre Stärke der Traversierung zeigt sich, wenn du diese Eigenschaften kombinierst, um komplexe Beziehungen im DOM abzubilden. Stell dir vor, du hast eine Produktkarte und klickst auf den "In den Warenkorb"-Button. Du möchtest nun den Namen des Produkts aus der Überschrift extrahieren, die sich in derselben Karte befindet.

```html
<article class="produkt-karte">
  <h2 class="produkt-titel">Bequemer Stuhl</h2>
  <p class="preis">99,00 €</p>
  <button class="add-to-cart-btn">In den Warenkorb</button>
</article>
```

Wenn der Button geklickt wird, können wir von ihm aus traversieren:

```js
const button = document.querySelector('.add-to-cart-btn');

button.addEventListener('click', function() {
  // Vom Button zum Elternelement (die <article>-Karte)
  const produktKarte = this.parentElement;
  
  // Von der Karte zum ersten Kind-Element (die <h2>)
  const produktTitelElement = produktKarte.firstElementChild;
  
  // Den Text aus dem Titel-Element auslesen
  const produktName = produktTitelElement.textContent;
  
  console.log(`Produkt "${produktName}" wurde zum Warenkorb hinzugefügt.`);
  // Ausgabe: Produkt "Bequemer Stuhl" wurde zum Warenkorb hinzugefügt.
});
```

In diesem Beispiel haben wir eine Kette gebildet: `button -> parentElement -> firstElementChild`. Wir mussten dem Button oder der Überschrift keine spezifischen IDs geben. Die Logik funktioniert allein durch die relative Position der Elemente zueinander. Das macht deinen Code robuster und wiederverwendbarer, da er nicht von starren IDs abhängt, sondern sich an der semantischen Struktur deines HTML orientiert.

Das Traversieren des DOM ist wie das Navigieren mit einer Landkarte. Wenn du weißt, wo du bist, kannst du dich mithilfe der Beziehungen zwischen den Knoten – Eltern, Kinder, Geschwister – zu jedem beliebigen anderen Punkt auf der Karte bewegen. Während direkte Auswahlmethoden wie `querySelector` oft ein guter Startpunkt sind, ist die Traversierung das Werkzeug, das dir erlaubt, von dort aus dynamisch und kontextbezogen weiterzuarbeiten.
