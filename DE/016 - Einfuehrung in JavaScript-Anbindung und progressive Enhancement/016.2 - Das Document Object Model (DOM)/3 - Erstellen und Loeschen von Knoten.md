# Erstellen und Löschen von Knoten

# Erstellen und Löschen von Knoten

Bisher hast du das DOM als eine bestehende Struktur kennengelernt, durch die du navigieren und deren Inhalte du auslesen oder verändern kannst. Das ist bereits ein mächtiges Werkzeug. Doch die wahre Magie von JavaScript entfaltet sich, wenn du beginnst, die Struktur der Webseite zur Laufzeit komplett zu verändern – also während ein Nutzer sie verwendet. Du kannst neue Elemente aus dem Nichts erschaffen, sie mit Inhalt füllen und an einer beliebigen Stelle einfügen. Genauso kannst du Elemente, die nicht mehr benötigt werden, spurlos aus dem Dokument entfernen. Diese dynamische Manipulation ist das Herzstück moderner Webanwendungen, von einfachen To-do-Listen bis hin zu komplexen sozialen Netzwerken.

### Elemente im Verborgenen erschaffen

Stell dir vor, du möchtest auf deiner Seite eine neue Benachrichtigung anzeigen, nachdem der Nutzer eine bestimmte Aktion ausgeführt hat. Diese Benachrichtigung existiert nicht im ursprünglichen HTML-Code. Du musst sie mit JavaScript erzeugen. Der erste Schritt dazu ist immer die Methode `document.createElement()`.

Diese Methode nimmt einen einzigen Parameter entgegen: einen String, der den Tag-Namen des gewünschten Elements angibt. Wenn du also einen neuen Paragraphen erstellen möchtest, schreibst du `document.createElement('p')`. Für eine neue Div-Box wäre es `document.createElement('div')`.

```javascript
// Erstellt ein neues <div>-Element
const neueBox = document.createElement('div');

// Erstellt ein neues <h2>-Element
const neueUeberschrift = document.createElement('h2');

// Erstellt ein neues Bild-Element
const neuesBild = document.createElement('img');
```

Was hier passiert, ist entscheidend zu verstehen: Diese Elemente werden zwar erstellt, aber sie existieren zunächst nur im Speicher deines Browsers. Sie sind wie Geister – vorhanden, aber auf der Webseite noch nicht sichtbar. Sie sind noch kein Teil des DOM-Baums. Bevor wir sie sichtbar machen, müssen wir sie meist noch konfigurieren, also mit Inhalt und Attributen versehen.

### Inhalt und Attribute hinzufügen

Ein leeres `<div>` oder ein `<h2>` ohne Text ist selten nützlich. Um einem neu erstellten Knoten Inhalt zu geben, hast du hauptsächlich zwei Möglichkeiten: `textContent` und `innerHTML`.

`textContent` ist die sicherste und direkteste Methode, um reinen Text in ein Element einzufügen. Der zugewiesene String wird als einfacher Text interpretiert, was bedeutet, dass eventuell darin enthaltene HTML-Tags nicht als solche gerendert, sondern als normaler Text angezeigt werden.

```javascript
const neueUeberschrift = document.createElement('h2');
neueUeberschrift.textContent = 'Willkommen auf unserer Seite!';
```

`innerHTML` ist mächtiger, aber auch mit Vorsicht zu genießen. Es erlaubt dir, einen String zu übergeben, der komplettes HTML-Markup enthält. Der Browser parst diesen String und erzeugt daraus die entsprechenden DOM-Knoten als Kinder des Elements.

```javascript
const neueBox = document.createElement('div');
neueBox.innerHTML = '<p>Dies ist ein <strong>wichtiger</strong> Hinweis.</p>';
```

Die Gefahr bei `innerHTML` besteht, wenn du Inhalte einfügst, die von Nutzern stammen. Ein böswilliger Nutzer könnte versuchen, schädlichen Code (z. B. `<script>`-Tags) einzuschleusen. Dies nennt man Cross-Site Scripting (XSS). Wenn du also mit `innerHTML` arbeitest, stelle immer sicher, dass die eingefügten Inhalte aus einer vertrauenswürdigen Quelle stammen oder entsprechend bereinigt (escaped) wurden. Für reinen Text ist `textContent` immer die bessere Wahl.

Neben dem Inhalt benötigen Elemente oft Attribute wie `class`, `id`, `src` oder `href`. Diese kannst du direkt als Eigenschaften des Element-Objekts setzen oder die Methode `setAttribute()` verwenden.

```javascript
// Erstellen und konfigurieren eines Bildes
const neuesBild = document.createElement('img');

// Setzen des src-Attributs über die Eigenschaft
neuesBild.src = 'bilder/logo.png';

// Setzen des alt-Attributs mit setAttribute()
neuesBild.setAttribute('alt', 'Firmenlogo');

// Hinzufügen einer CSS-Klasse
neuesBild.className = 'firmen-logo';
// Oder, moderner und flexibler, über classList
neuesBild.classList.add('rundes-logo');
```

Jetzt haben wir unsere Elemente im Speicher erschaffen und vollständig konfiguriert. Sie sind bereit für ihren großen Auftritt.

### Knoten in den DOM-Baum einhängen

Um ein vorbereitetes Element auf der Seite sichtbar zu machen, musst du es an einer bestimmten Stelle in den DOM-Baum einfügen. Dafür benötigst du zwei Dinge: das Element, das du einfügen möchtest (unseren neuen Knoten), und ein Referenzelement, das bereits im DOM existiert und als Elternteil oder Geschwisterchen dienen soll.

Die klassischste Methode ist `appendChild()`. Sie wird auf einem Elternelement aufgerufen und fügt den neuen Knoten als dessen letztes Kind hinzu.

Angenommen, dein HTML sieht so aus:

```html
<div id="container">
  <h1>Bestehende Überschrift</h1>
</div>
```

Nun möchtest du einen neuen Paragraphen unterhalb der Überschrift einfügen:

```javascript
// 1. Den neuen Knoten erstellen und konfigurieren
const neuerAbsatz = document.createElement('p');
neuerAbsatz.textContent = 'Dies ist ein dynamisch hinzugefügter Text.';

// 2. Das Elternelement im DOM finden
const container = document.getElementById('container');

// 3. Den neuen Knoten als letztes Kind des Containers anhängen
container.appendChild(neuerAbsatz);
```

Nach Ausführung dieses Codes wird der DOM-Baum so aussehen, als hättest du von Anfang an geschrieben:

```html
<div id="container">
  <h1>Bestehende Überschrift</h1>
  <p>Dies ist ein dynamisch hinzugefügter Text.</p>
</div>
```

Die moderne JavaScript-API bietet noch flexiblere Methoden, die oft intuitiver sind:

*   `element.append(knoten1, knoten2, ...)`: Fügt einen oder mehrere Knoten (oder auch nur Text-Strings) am Ende des `element` hinzu. Sehr ähnlich zu `appendChild`, aber flexibler.
*   `element.prepend(knoten1, knoten2, ...)`: Fügt Knoten am Anfang des `element` hinzu (vor dem ersten Kind).
*   `element.before(knoten1, knoten2, ...)`: Fügt Knoten direkt vor dem `element` auf derselben Ebene ein (als vorheriges Geschwisterkind).
*   `element.after(knoten1, knoten2, ...)`: Fügt Knoten direkt nach dem `element` auf derselben Ebene ein (als nächstes Geschwisterkind).

Mit diesen Methoden hast du die volle Kontrolle darüber, wo genau deine neuen Elemente im Dokument landen.

### Knoten aus dem DOM entfernen

Genauso wichtig wie das Erstellen von Elementen ist das Entfernen. Vielleicht möchtest du eine Fehlermeldung ausblenden, nachdem der Nutzer seine Eingabe korrigiert hat, oder einen Artikel aus einer Liste löschen.

Der modernste und einfachste Weg, ein Element zu entfernen, ist die Methode `remove()`. Du rufst sie direkt auf dem Knoten auf, den du löschen möchtest.

```html
<div id="meldung-box">
  <p class="hinweis" id="alter-hinweis">Diese Information ist veraltet.</p>
</div>
```

```javascript
// 1. Das zu löschende Element finden
const alterHinweis = document.getElementById('alter-hinweis');

// 2. Das Element aus dem DOM entfernen
if (alterHinweis) {
  alterHinweis.remove();
}
```

Das ist alles. Die Methode `remove()` entfernt das Element und alle seine Kinder restlos aus dem DOM-Baum. Es ist sauber, direkt und leicht zu lesen.

Für den Fall, dass du auf älteren Code oder in Browsern mit eingeschränkter Unterstützung stößt, ist es gut, die klassische Methode zu kennen: `parentNode.removeChild()`. Hierbei ist der Ansatz etwas umständlicher. Du benötigst eine Referenz auf das Elternelement und rufst darauf `removeChild()` auf, wobei du das zu löschende Kind als Argument übergibst.

```javascript
// 1. Das zu löschende Element finden
const alterHinweis = document.getElementById('alter-hinweis');

if (alterHinweis) {
  // 2. Den Elternknoten des Elements finden
  const elternteil = alterHinweis.parentNode;

  // 3. Das Kind vom Elternteil entfernen lassen
  elternteil.removeChild(alterHinweis);
}
```

Beide Wege führen zum selben Ergebnis. Wann immer möglich, solltest du jedoch `element.remove()` bevorzugen, da der Code damit deutlich selbsterklärender ist.

### Ein praktisches Beispiel: Eine einfache To-do-Liste

Lassen uns das Gelernte in einem kleinen, aber vollständigen Beispiel zusammenführen. Wir erstellen eine To-do-Liste, bei der du neue Aufgaben hinzufügen und bestehende durch einen Klick löschen kannst.

Unser HTML ist minimalistisch:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Dynamische To-do-Liste</title>
</head>
<body>
    <h1>Meine To-do-Liste</h1>
    <input type="text" id="neue-aufgabe-input" placeholder="Neue Aufgabe...">
    <button id="hinzufuegen-btn">Hinzufügen</button>
    <ul id="aufgaben-liste">
        <!-- Hier werden die Aufgaben dynamisch eingefügt -->
    </ul>

    <script src="app.js"></script>
</body>
</html>
```

Und hier ist das zugehörige JavaScript in der Datei `app.js`:

```javascript
// Referenzen auf die wichtigen DOM-Elemente holen
const inputFeld = document.getElementById('neue-aufgabe-input');
const hinzufuegenButton = document.getElementById('hinzufuegen-btn');
const aufgabenListe = document.getElementById('aufgaben-liste');

// Funktion zum Hinzufügen einer neuen Aufgabe
function neueAufgabeHinzufuegen() {
    const aufgabenText = inputFeld.value.trim();

    // Nur fortfahren, wenn der Nutzer etwas eingegeben hat
    if (aufgabenText === '') {
        alert('Bitte gib eine Aufgabe ein.');
        return;
    }

    // --- Erstellen der Knoten ---

    // 1. Ein neues <li>-Element erstellen
    const neuesListenElement = document.createElement('li');

    // 2. Den Textinhalt für das <li> setzen
    neuesListenElement.textContent = aufgabenText;

    // 3. Einen Löschen-Button für diese Aufgabe erstellen
    const loeschenButton = document.createElement('button');
    loeschenButton.textContent = 'Erledigt';
    loeschenButton.style.marginLeft = '10px'; // Ein kleiner Abstand

    // --- Event-Listener für das Löschen hinzufügen ---
    
    // Wenn der "Erledigt"-Button geklickt wird...
    loeschenButton.addEventListener('click', function() {
        // ... entferne das gesamte Listen-Element (<li>), in dem der Button ist.
        neuesListenElement.remove();
    });

    // --- Knoten in den DOM-Baum einhängen ---

    // 4. Den Löschen-Button an das <li>-Element anhängen
    neuesListenElement.append(loeschenButton);

    // 5. Das fertige <li>-Element an die <ul>-Liste anhängen
    aufgabenListe.append(neuesListenElement);

    // 6. Das Eingabefeld für die nächste Aufgabe leeren
    inputFeld.value = '';
    inputFeld.focus(); // Den Cursor zurück ins Feld setzen
}

// Event-Listener auf den Haupt-Button "Hinzufügen" setzen
hinzufuegenButton.addEventListener('click', neueAufgabeHinzufuegen);

// Erlaube auch das Hinzufügen durch Drücken der Enter-Taste im Input-Feld
inputFeld.addEventListener('keypress', function(event) {
    if (event.key === 'Enter') {
        neueAufgabeHinzufuegen();
    }
});
```

In diesem Beispiel siehst du den gesamten Lebenszyklus eines DOM-Knotens in Aktion: Ein `<li>` und ein `<button>` werden auf Knopfdruck erstellt (`createElement`), mit Inhalt versehen (`textContent`), miteinander kombiniert (`append`) und schließlich in den sichtbaren DOM-Baum eingefügt (`append`). Der Löschen-Button erhält eine Funktion, die seinen eigenen Elternknoten (`<li>`) gezielt entfernt (`remove`), sobald er geklickt wird.

Die Fähigkeit, die Struktur deines Dokuments nach Belieben zu formen, ist eine der fundamentalsten und mächtigsten Techniken in der modernen Webentwicklung. Sie ermöglicht es dir, auf jede nur erdenkliche Nutzerinteraktion zu reagieren und Webseiten zu bauen, die sich lebendig und reaktionsschnell anfühlen.
