# DOM-Manipulation

### DOM-Manipulation: Wie JavaScript deine Webseite lebendig macht

Stell dir dein HTML-Dokument wie den Bauplan eines Hauses vor. Es legt fest, wo die Wände, Türen und Fenster sind – also die Struktur. CSS ist der Innenarchitekt, der alles anmalt, dekoriert und möbliert. Bisher war dieses Haus aber statisch. Ein Museum, in dem man nichts anfassen darf. JavaScript ändert das. Es ist die Magie, die es dir erlaubt, Wände zu versetzen, Lichter ein- und auszuschalten und Möbel zu verrücken, *nachdem* das Haus bereits gebaut wurde.

Diese „Magie“ hat einen technischen Namen: DOM-Manipulation. Und um sie zu verstehen, müssen wir zuerst klären, was das „DOM“ überhaupt ist.

#### Das Document Object Model (DOM)

Wenn ein Browser deine HTML-Datei lädt, liest er nicht einfach nur den Text. Er tut etwas viel Klügeres: Er übersetzt deinen HTML-Code in eine lebendige, baumartige Struktur im Arbeitsspeicher. Diese Struktur wird als **Document Object Model**, kurz DOM, bezeichnet.

Jedes einzelne Element in deinem HTML-Code – jeder Absatz (`<p>`), jede Überschrift (`<h1>`), jeder Link (`<a>`) – wird zu einem **Knoten** (Node) in diesem Baum. Das `<html>`-Element ist die Wurzel des Baums. Es hat zwei direkte Kinder: `<head>` und `<body>`. Der `<body>`-Knoten wiederum kann Kinder haben, wie zum Beispiel eine `<div>` und eine `<ul>`. Die `<ul>` hat dann vielleicht mehrere `<li>`-Kinder.

Dieser Baum ist nicht nur eine passive Darstellung. Er ist eine Schnittstelle (ein sogenanntes API – Application Programming Interface), die es Sprachen wie JavaScript erlaubt, auf die Dokumentstruktur zuzugreifen und sie zu verändern. Wenn du mit JavaScript eine Überschrift änderst, bearbeitest du nicht die ursprüngliche `.html`-Datei auf dem Server. Du veränderst den DOM-Knoten für diese Überschrift direkt im Browser des Nutzers. Der Browser reagiert sofort und zeichnet die Webseite neu, um die Änderung widerzuspiegeln. Das ist das Herzstück aller interaktiven Webseiten.

#### Der erste Schritt: Elemente gezielt auswählen

Bevor du etwas verändern kannst, musst du JavaScript erst einmal sagen, *was* du verändern möchtest. Du brauchst einen Weg, um einen oder mehrere Knoten im DOM-Baum zu „greifen“. Dafür gibt es verschiedene Methoden, die alle am globalen `document`-Objekt hängen.

##### Auswahl über eine eindeutige ID

Der präziseste Weg, ein Element zu finden, ist über seine ID. Da eine ID pro Dokument einzigartig sein sollte, ist dies wie die Sozialversicherungsnummer für ein HTML-Element.

```html
<div id="welcome-banner">
  <h1>Hallo Welt!</h1>
</div>
```

Mit JavaScript kannst du dieses `div`-Element nun sehr einfach schnappen:

```js
const banner = document.getElementById('welcome-banner');
```

Die Variable `banner` enthält jetzt eine Referenz auf das DOM-Objekt, das unser `div`-Element repräsentiert. Ab jetzt kannst du mit diesem Objekt arbeiten. Wenn kein Element mit dieser ID gefunden wird, gibt die Methode `null` zurück.

##### Auswahl über CSS-Selektoren

Ein modernerer und oft flexiblerer Weg ist die Verwendung von CSS-Selektoren. Du kennst sie bereits aus dem Styling deiner Seiten. JavaScript kann dieselben Selektoren nutzen, um Elemente zu finden.

**`querySelector()` – Das erste passende Element finden**

Diese Methode durchsucht das DOM und gibt das *erste* Element zurück, das auf den angegebenen CSS-Selektor passt.

```html
<p class="info-text">Dies ist eine wichtige Information.</p>
<p class="info-text">Dies ist eine weitere Information.</p>
```

```js
// Wählt nur den ERSTEN Absatz mit der Klasse "info-text"
const firstInfo = document.querySelector('.info-text');
```

Du kannst jeden gültigen CSS-Selektor verwenden, egal wie komplex: `querySelector('#main-content .list-item a')`. Das macht diese Methode unglaublich mächtig.

**`querySelectorAll()` – Alle passenden Elemente finden**

Was aber, wenn du alle Elemente mit der Klasse `info-text` verändern willst? Hierfür gibt es `querySelectorAll()`.

```js
// Wählt ALLE Absätze mit der Klasse "info-text"
const allInfos = document.querySelectorAll('.info-text');
```

Diese Methode gibt keine einzelne Referenz zurück, sondern eine sogenannte **NodeList**. Eine NodeList ist eine sammlung von Knoten, die sehr ähnlich wie ein Array funktioniert. Du kannst sie zum Beispiel mit einer Schleife durchlaufen, um auf jedes Element einzeln zuzugreifen.

```js
allInfos.forEach(infoElement => {
  console.log(infoElement); // Gibt jedes <p>-Element in der Konsole aus
});
```

#### Die Macht der Veränderung: Elemente manipulieren

Sobald du ein Element ausgewählt und in einer Variable gespeichert hast, beginnt der eigentliche Spaß. Du kannst nun fast alles an diesem Element ändern.

##### Inhalte ändern: `textContent` und `innerHTML`

Der häufigste Anwendungsfall ist das Ändern des Inhalts eines Elements.

**`textContent`** ändert nur den reinen Text innerhalb eines Elements. Alle HTML-Tags werden dabei ignoriert bzw. als normaler Text dargestellt. Das ist sicher und schnell.

```html
<h1 id="main-heading">Alter Titel</h1>
```

```js
const heading = document.getElementById('main-heading');
heading.textContent = 'Ein brandneuer, dynamischer Titel!';
```

**`innerHTML`** hingegen interpretiert die Zeichenkette, die du ihm gibst, als HTML. Du kannst damit also komplette neue HTML-Strukturen in ein Element einfügen.

```html
<div id="user-profile"></div>
```

```js
const profile = document.getElementById('user-profile');
profile.innerHTML = '<h2>Max Mustermann</h2><p>Web-Entwickler</p>';
```

Sei vorsichtig mit `innerHTML`, wenn du Inhalte von Nutzern einfügst. Ein bösartiger Nutzer könnte schädlichen Code (z.B. `<script>`-Tags) einfügen, was zu Sicherheitslücken (Cross-Site Scripting, XSS) führen kann. Für reinen Text ist `textContent` immer die bessere Wahl.

##### Attribute verändern

Du kannst auch die Attribute eines Elements lesen und verändern. Stell dir vor, du möchtest das Bild auf deiner Seite austauschen.

```html
<img id="product-image" src="bild1.jpg" alt="Produktansicht 1">
```

```js
const image = document.getElementById('product-image');

// Ändert das src-Attribut, um ein anderes Bild zu laden
image.src = 'bild2.jpg';

// Ändert auch den Alternativtext
image.alt = 'Produktansicht 2';
```

Für Standardattribute wie `src`, `href`, `id` oder `alt` kannst du direkt auf die Eigenschaften des DOM-Objekts zugreifen. Für alle anderen oder für eine allgemeinere Methode gibt es `setAttribute()` und `getAttribute()`.

```js
image.setAttribute('data-product-id', 'p-4711');
const productId = image.getAttribute('data-product-id'); // Ergibt "p-4711"
```

##### Styles und Klassen manipulieren

Obwohl die grundlegende Gestaltung deiner Seite im CSS-File liegen sollte, gibt es oft den Bedarf, Styles dynamisch zu ändern – zum Beispiel um einen Fehlerzustand zu signalisieren oder ein Element hervorzuheben.

**Der direkte Weg: Das `style`-Objekt**

Jedes DOM-Element hat eine `style`-Eigenschaft, die dir direkten Zugriff auf die Inline-Styles des Elements gibt.

```js
const warningBox = document.querySelector('.warning');
warningBox.style.backgroundColor = '#ffdddd';
warningBox.style.border = '1px solid red';
warningBox.style.color = 'black';
```

Beachte, dass CSS-Eigenschaften mit Bindestrich (wie `background-color`) in JavaScript in CamelCase-Schreibweise (wie `backgroundColor`) umgewandelt werden. Dieser Weg ist gut für kleine, dynamische Anpassungen, aber er vermischt Styling-Logik mit deinem JavaScript-Code.

**Der bessere Weg: Klassen togglen mit `classList`**

Ein saubererer Ansatz ist es, die benötigten Styles in deinem CSS in Klassen zu definieren und diese Klassen dann mit JavaScript bei Bedarf hinzuzufügen oder zu entfernen.

Dein CSS könnte so aussehen:

```css
.is-active {
  background-color: lightblue;
  font-weight: bold;
}

.has-error {
  border: 2px solid red;
}
```

Mit der `classList`-Eigenschaft kannst du diese Klassen nun kinderleicht verwalten.

```js
const navItem = document.querySelector('#nav-home');

// Fügt eine Klasse hinzu
navItem.classList.add('is-active');

// Entfernt eine Klasse
navItem.classList.remove('is-active');

// Fügt die Klasse hinzu, wenn sie nicht da ist, und entfernt sie, wenn sie da ist.
// Perfekt für Klick-Events!
navItem.classList.toggle('is-active');
```

Dieser Ansatz hält deine Verantwortlichkeiten getrennt: CSS kümmert sich um das Aussehen, JavaScript kümmert sich um die Logik, wann dieses Aussehen angewendet wird. Dies ist ein Kernprinzip von gut strukturierter Webentwicklung.

#### Dynamische Erstellung: Neue Elemente erschaffen

DOM-Manipulation beschränkt sich nicht nur auf das Verändern bestehender Elemente. Du kannst auch komplett neue Elemente aus dem Nichts erschaffen und sie in dein Dokument einfügen.

Stell dir eine To-Do-Liste vor, zu der du neue Aufgaben hinzufügen möchtest.

```html
<ul id="todo-list">
  <li>Alte Aufgabe</li>
</ul>
<button id="add-task-btn">Neue Aufgabe hinzufügen</button>
```

Der JavaScript-Code, um einen neuen Listeneintrag zu erstellen und hinzuzufügen, könnte so aussehen:

```js
// 1. Die existierenden Elemente auswählen
const list = document.getElementById('todo-list');
const addButton = document.getElementById('add-task-btn');

// Wenn der Button geklickt wird...
addButton.addEventListener('click', () => {
  // 2. Ein neues Element im Speicher erstellen
  const newListItem = document.createElement('li');

  // 3. Dem neuen Element Inhalt und Attribute geben
  newListItem.textContent = 'Eine brandneue Aufgabe';
  newListItem.classList.add('task');

  // 4. Das neue Element in das DOM einhängen
  // appendChild fügt es als letztes Kind hinzu
  list.appendChild(newListItem);
});
```

Jeder Klick auf den Button führt diesen Code aus, erstellt ein neues `<li>`-Element, konfiguriert es und hängt es an das Ende der `<ul>`-Liste an. Deine Seite wird interaktiv.

#### Aufräumen: Elemente entfernen

Genauso wie du Elemente hinzufügen kannst, kannst du sie auch wieder entfernen. Die modernste und einfachste Methode dafür ist `remove()`.

```js
const elementToRemove = document.getElementById('obsolete-banner');
if (elementToRemove) {
  elementToRemove.remove();
}
```

Zuerst wählst du das Element aus, das du entfernen möchtest, und rufst dann direkt auf diesem Element die `remove()`-Methode auf. Das Element verschwindet mitsamt all seinen Kind-Elementen aus dem DOM und somit von der Webseite.

Die Manipulation des DOM ist eine der fundamentalsten Fähigkeiten in der Frontend-Entwicklung. Sie ist die Brücke, die dein strukturiertes HTML-Dokument in eine dynamische, reaktionsfähige und nützliche Web-Anwendung verwandelt.
