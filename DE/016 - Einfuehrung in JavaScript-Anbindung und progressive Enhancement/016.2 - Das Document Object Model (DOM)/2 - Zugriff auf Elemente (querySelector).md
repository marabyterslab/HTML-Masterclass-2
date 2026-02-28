# Zugriff auf Elemente (querySelector)

### Gezielter Zugriff: `querySelector` und `querySelectorAll`

Nachdem du nun weißt, dass dein HTML-Dokument im Browser als eine Baumstruktur, das DOM, existiert, stellt sich die entscheidende Frage: Wie kannst du mit JavaScript auf ein ganz bestimmtes Element in diesem Baum zugreifen? Wie sagst du dem Code: „Finde mir genau diesen einen Button!“ oder „Gib mir alle Paragrafen innerhalb des Hauptartikels!“?

Früher gab es dafür eine ganze Reihe von Methoden wie `getElementById`, `getElementsByClassName` oder `getElementsByTagName`. Jede hatte ihren eigenen, sehr spezifischen Zweck. Das war funktional, aber auch etwas umständlich. Glücklicherweise gibt es heute einen moderneren, weitaus flexibleren und leistungsfähigeren Ansatz, der dir die ganze Macht eines Werkzeugs an die Hand gibt, das du bereits kennst und schätzt: CSS-Selektoren.

Die beiden Methoden, die dies ermöglichen und die zum Schweizer Taschenmesser für den DOM-Zugriff geworden sind, heißen `querySelector()` und `querySelectorAll()`.

#### Den ersten Treffer landen: `document.querySelector()`

Stell dir vor, du möchtest ein einziges, ganz bestimmtes Element auf deiner Seite ansprechen. Vielleicht ist es der Haupt-Button, ein spezieller Container oder das Logo in der Kopfzeile. Die Methode `document.querySelector()` ist dafür dein perfektes Werkzeug.

Sie durchsucht den gesamten DOM-Baum von oben nach unten und gibt dir das **allererste Element** zurück, das auf den von dir angegebenen CSS-Selektor passt. Findet sie ein passendes Element, stoppt die Suche sofort und liefert es dir. Wenn kein einziges Element dem Selektor entspricht, gibt sie den Wert `null` zurück.

Das Schöne daran ist, dass du jeden gültigen CSS-Selektor verwenden kannst, den du bereits kennst.

**Beispiel: Zugriff über eine ID**
IDs sind einzigartig in einem Dokument. Der Zugriff ist daher besonders eindeutig.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <title>Beispiel</title>
</head>
<body>
    <h1 id="main-headline">Willkommen auf unserer Seite!</h1>
    <p>Dies ist ein Einführungstext.</p>
</body>
</html>
```

Mit JavaScript greifst du auf die Überschrift so zu:

```js
const headline = document.querySelector('#main-headline');

// Jetzt können wir mit dem Element arbeiten
headline.style.color = 'blue';
```

In diesem Beispiel sucht `querySelector()` nach einem Element mit der ID `main-headline`. Es findet die `<h1>`-Überschrift, speichert eine Referenz darauf in der Konstante `headline`, und anschließend ändern wir ihre Textfarbe auf Blau.

**Beispiel: Zugriff über eine Klasse**
Was, wenn mehrere Elemente dieselbe Klasse haben, du aber nur das erste davon brauchst?

```html
<p class="highlight">Dieser Absatz ist wichtig.</p>
<div>
    <p class="highlight">Dieser Absatz ist ebenfalls wichtig.</p>
</div>
```

```js
const firstHighlighted = document.querySelector('.highlight');

// Ändert nur den Hintergrund des ERSTEN Elements mit der Klasse "highlight"
firstHighlighted.style.backgroundColor = 'yellow';
```

Obwohl es zwei Elemente mit der Klasse `highlight` gibt, gibt `querySelector('.highlight')` nur das erste `p`-Element zurück und ignoriert das zweite.

**Beispiel: Komplexere Selektoren**
Hier entfaltet `querySelector()` seine wahre Stärke. Du kannst komplexe Selektoren verketten, genau wie in deinem CSS.

```html
<nav>
    <ul>
        <li><a href="/">Startseite</a></li>
        <li><a href="/produkte">Produkte</a></li>
        <li><a href="/kontakt">Kontakt</a></li>
    </ul>
</nav>
```

```js
// Finde den Link zum Kontakt-Bereich
const contactLink = document.querySelector('nav ul li a[href="/kontakt"]');

// Füge eine visuelle Markierung hinzu
contactLink.style.border = '2px solid red';
```

Da `querySelector()` `null` zurückgibt, wenn nichts gefunden wird, ist es eine gute Praxis, zu überprüfen, ob du tatsächlich ein Element erhalten hast, bevor du versuchst, damit zu arbeiten. Das verhindert Fehler, falls sich dein HTML ändert und der Selektor ins Leere läuft.

```js
const specialElement = document.querySelector('.non-existent-class');

if (specialElement) {
    // Dieser Code wird nie ausgeführt, da specialElement `null` ist.
    specialElement.textContent = 'Ich wurde gefunden!';
} else {
    console.log('Element nicht gefunden.');
}
```

#### Alle passenden Elemente finden: `document.querySelectorAll()`

Oft möchtest du nicht nur ein Element, sondern eine ganze Gruppe von Elementen bearbeiten. Stell dir vor, du willst alle Listeneinträge in einer ungeordneten Liste, alle externen Links auf einer Seite oder alle Bilder in einer Galerie ansprechen.

Hier kommt `document.querySelectorAll()` ins Spiel. Wie der Name schon andeutet, durchsucht diese Methode ebenfalls das DOM, aber sie hört nicht nach dem ersten Treffer auf. Stattdessen sammelt sie **alle** Elemente, die auf den angegebenen CSS-Selektor passen, und gibt sie dir als eine sogenannte `NodeList` zurück.

Eine `NodeList` ist eine sammlung von Elementen, die einem Array sehr ähnlich ist. Du kannst ihre Länge mit `.length` abfragen und – was am wichtigsten ist – du kannst mit einer Schleife, zum Beispiel `forEach`, über jedes einzelne Element in der Liste iterieren.

**Beispiel: Alle Listeneinträge ansprechen**

```html
<ul id="shopping-list">
    <li>Äpfel</li>
    <li>Bananen</li>
    <li>Milch</li>
</ul>
```

Mit `querySelectorAll()` können wir nun auf alle `<li>`-Elemente zugreifen und sie verändern.

```js
const listItems = document.querySelectorAll('#shopping-list li');

// listItems ist jetzt eine NodeList, die drei <li>-Elemente enthält.

listItems.forEach(function(item) {
    // Diese Funktion wird für jedes Element in der Liste ausgeführt
    item.style.fontWeight = 'bold';
    console.log(item.textContent); // Gibt "Äpfel", "Bananen", "Milch" aus
});
```

Jedes `<li>` in der Einkaufsliste wird nun fett dargestellt.

Ein wichtiger Unterschied zu `querySelector()`: Wenn `querySelectorAll()` keine passenden Elemente findet, gibt es nicht `null` zurück, sondern eine **leere `NodeList`**. Das ist sehr praktisch, denn dein Code wird dadurch nicht sofort mit einem Fehler abbrechen. Wenn du versuchst, über eine leere Liste zu iterieren, passiert einfach gar nichts – die Schleife wird null Mal durchlaufen.

```js
const nonExistentItems = document.querySelectorAll('.card');

console.log(nonExistentItems.length); // Gibt 0 aus

nonExistentItems.forEach(function(item) {
    // Dieser Code wird nie ausgeführt. Kein Fehler!
    item.style.display = 'none';
});
```

#### Mehr als nur das `document`: Der Kontext der Suche

Ein extrem nützliches Feature von `querySelector` und `querySelectorAll` ist, dass du sie nicht nur auf dem globalen `document`-Objekt aufrufen musst. Du kannst sie auch auf jedem beliebigen anderen Element-Knoten anwenden.

Wenn du eine Suche auf einem spezifischen Element startest, wird nur der Teilbaum **innerhalb dieses Elements** durchsucht. Das macht deine Selektoren kürzer, präziser und oft auch performanter, da der Browser nicht das gesamte Dokument durchkämmen muss.

Stell dir eine Webseite mit mehreren Artikeln vor. Jeder Artikel hat seine eigene Überschrift und Absätze.

```html
<article id="article-1">
    <h2>Erster Artikel</h2>
    <p>Inhalt des ersten Artikels.</p>
    <a href="#" class="read-more">Weiterlesen</a>
</article>

<article id="article-2">
    <h2>Zweiter Artikel</h2>
    <p>Inhalt des zweiten Artikels.</p>
    <a href="#" class="read-more">Weiterlesen</a>
</article>
```

Angenommen, du hast bereits eine Referenz auf den zweiten Artikel und möchtest nun den „Weiterlesen“-Link *nur in diesem Artikel* finden.

```js
// Zuerst den Kontext (den zweiten Artikel) holen
const secondArticle = document.querySelector('#article-2');

// Jetzt die Suche innerhalb dieses Kontexts durchführen
const readMoreLink = secondArticle.querySelector('.read-more');

// Dies betrifft nur den Link im zweiten Artikel
readMoreLink.textContent = 'Vollständigen Artikel lesen';
```

Hättest du `document.querySelector('.read-more')` verwendet, hättest du den Link aus dem ersten Artikel bekommen. Indem du die Suche auf `secondArticle` beschränkst, stellst du sicher, dass du genau das richtige Element erwischst.

#### Statische vs. Live-Sammlungen: Ein wichtiger Unterschied

Ein technisches Detail, das du im Hinterkopf behalten solltest, ist, dass die `NodeList`, die von `querySelectorAll()` zurückgegeben wird, **statisch** ist. Das bedeutet, sie ist wie eine Momentaufnahme des DOMs zu dem Zeitpunkt, als der Befehl ausgeführt wurde.

Wenn du nach dem Ausführen von `querySelectorAll()` neue Elemente zum DOM hinzufügst, die eigentlich auf den Selektor passen würden, erscheinen diese nicht automatisch in deiner bereits existierenden `NodeList`. Du müsstest `querySelectorAll()` erneut aufrufen, um eine aktualisierte Liste zu erhalten.

Dieses Verhalten ist meistens wünschenswert, da es vorhersehbar ist und unbeabsichtigte Nebeneffekte verhindert. Es steht im Gegensatz zu einigen älteren Methoden wie `getElementsByTagName()`, die „live“ Sammlungen zurückgaben, die sich automatisch aktualisierten – ein Verhalten, das oft zu Verwirrung und schwer zu findenden Fehlern führte.

Mit `querySelector` und `querySelectorAll` hast du ein mächtiges, konsistentes und intuitives Werkzeugset, um mit JavaScript präzise auf jedes Element deines HTML-Dokuments zuzugreifen. Die Fähigkeit, dein gesamtes Wissen über CSS-Selektoren direkt zu nutzen, ist ein unschätzbarer Vorteil, der die Brücke zwischen der Struktur (HTML), dem Stil (CSS) und dem Verhalten (JavaScript) schließt.
