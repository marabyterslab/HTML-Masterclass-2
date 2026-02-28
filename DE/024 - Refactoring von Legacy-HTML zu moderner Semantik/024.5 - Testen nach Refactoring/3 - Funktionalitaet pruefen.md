# Funktionalität prüfen

### Funktionalität prüfen

Nachdem du den alten Staub von deinem Legacy-Code geklopft und ihn in glänzendes, semantisches HTML verwandelt hast, steht der wichtigste Schritt bevor: die Überprüfung. Ein Refactoring ist erst dann ein Erfolg, wenn die Webseite danach nicht nur besser strukturiert, sondern auch mindestens genauso gut funktioniert wie vorher. Oftmals ist dies der Moment der Wahrheit, in dem sich zeigt, ob man an alle Abhängigkeiten gedacht hat.

Die reine Umwandlung von `<div>`-Suppen in wohlgeformte `<main>`, `<nav>` und `<article>`-Elemente fühlt sich wie ein reiner Struktureingriff an. Doch diese Annahme ist trügerisch. Dein HTML ist das Skelett, an dem die Muskeln (JavaScript) und die Haut (CSS) befestigt sind. Wenn du die Knochen neu anordnest, verlieren Muskeln und Haut schnell ihren Halt.

Die funktionale Prüfung stellt sicher, dass alle interaktiven Elemente, Skripte und dynamischen Inhalte nach dem Umbau noch wie erwartet arbeiten.

#### Der systematische Ansatz: Eine Checkliste für die Funktionalität

Bevor du blindlings auf deiner frisch refaktorisierten Seite herumklickst, solltest du einen Plan haben. Der beste Weg ist, eine Checkliste aller Funktionalitäten zu erstellen, die die Seite oder die Komponente besitzt. Diese Liste dient dir als Leitfaden und stellt sicher, dass du nichts übersiehst.

Was gehört auf so eine Liste?

*   **Interaktive UI-Elemente:** Buttons, Links, Dropdown-Menüs, Akkordeons, Tabs, Bilderkarussells (Slider).
*   **Formulare:** Absenden, Validierung (sowohl client- als auch serverseitig), Fehlermeldungen, Zurücksetzen-Buttons.
*   **Dynamisch geladene Inhalte:** Inhalte, die per AJAX/Fetch nachgeladen werden (z. B. „Mehr laden“-Buttons).
*   **Links und Navigation:** Funktionieren alle internen und externen Links? Führt die Hauptnavigation zu den richtigen Seiten?
*   **Zustandsänderungen:** Elemente, die ihr Aussehen oder Verhalten ändern, z. B. ein „Gefällt mir“-Button, der nach dem Klick anders aussieht.
*   **Multimedia-Elemente:** Werden Videos und Audio-Dateien korrekt geladen und lassen sie sich steuern?

Mit dieser Liste in der Hand beginnst du die eigentliche Prüfung.

#### Der erste Blick: Manuelles und visuelles Testen

Der erste und einfachste Schritt ist das manuelle Durchklicken. Öffne die Webseite in einem Browser – am besten in mehreren verschiedenen wie Chrome, Firefox und Safari, um Browser-Inkonsistenzen aufzudecken.

Deine beste Freundin hierbei ist die Entwicklerkonsole (meist mit F12 oder `Cmd+Option+I` zu öffnen). Behalte den „Konsole“-Tab immer im Blick. Wenn du auf ein Element klickst und nichts passiert, ist die Konsole oft der erste Ort, der dir verrät, warum. Rote Fehlermeldungen sind ein klares Indiz dafür, dass ein JavaScript-Selektor ins Leere greift oder eine Funktion nicht mehr gefunden wird.

Arbeite deine Checkliste Punkt für Punkt ab:

1.  **Klicke jeden Button und jeden Link.** Passiert das Erwartete? Öffnet sich ein Modal? Führt der Link zum Ziel?
2.  **Bediene jedes Navigationselement.** Klappen die Menüs auf und zu? Funktionieren die Hover-Effekte noch?
3.  **Fülle jedes Formular aus.** Teste es einmal mit korrekten und einmal mit fehlerhaften Daten. Werden die Validierungsmeldungen angezeigt? Lässt sich das Formular erfolgreich absenden?
4.  **Interagiere mit allen Widgets.** Schiebe den Slider weiter, öffne und schließe jedes Akkordeon.

Achte dabei nicht nur auf die Funktion, sondern auch auf das Visuelle. Steht der Button noch an der richtigen Stelle? Hat das aufklappende Menü noch das korrekte Styling? Oft sind funktionale Fehler auch visuell erkennbar.

#### Wenn JavaScript schweigt: Die Jagd nach kaputten Events

Der häufigste Grund für funktionale Fehler nach einem HTML-Refactoring sind JavaScript-Event-Listener, die ihre Zielelemente nicht mehr finden.

Stell dir vor, im alten Code gab es folgenden HTML-Schnipsel für einen Klick-Button:

```html
<!-- Vorher: Ein semantisch schwacher div-Button -->
<div id="main-content">
  <div class="action-button" onclick="doSomething()">Klick mich</div>
</div>
```

Das dazugehörige JavaScript könnte entweder direkt im `onclick`-Attribut liegen oder per Selektor angehängt worden sein:

```javascript
// Alternative 1: Event-Handler über eine Klasse
const button = document.querySelector('.action-button');
if (button) {
  button.addEventListener('click', doSomething);
}
```

Beim Refactoring hast du diesen `div` korrekterweise in ein `<button>`-Element umgewandelt und vielleicht auch die Klassenstruktur bereinigt:

```html
<!-- Nachher: Semantisch korrektes button-Element -->
<main>
  <button type="button" class="button-primary">Klick mich</button>
</main>
```

Was passiert nun?

1.  Das `onclick`-Attribut aus dem ursprünglichen HTML ist verschwunden. Falls die Logik nur dort war, ist sie weg.
2.  Der JavaScript-Selektor `document.querySelector('.action-button')` findet kein Element mehr, da die Klasse `action-button` in `button-primary` umbenannt wurde. Der `addEventListener` wird nie ausgeführt.

Der Klick auf den Button bleibt ohne jede Wirkung. Die Entwicklerkonsole würde in diesem Fall wahrscheinlich keine Fehlermeldung anzeigen, da der Code, der den Event-Listener hinzufügt, dank der `if (button)`-Prüfung einfach stillschweigend übersprungen wird.

Die Lösung besteht darin, das JavaScript an die neue HTML-Struktur anzupassen:

```javascript
// Angepasstes JavaScript
const button = document.querySelector('.button-primary');
if (button) {
  button.addEventListener('click', doSomething);
}
```

Prüfe also gezielt deine JavaScript-Dateien. Suche nach Selektoren (via `querySelector`, `getElementById`, `getElementsByClassName` oder auch jQuery-Selektoren wie `$('.foo')`), die auf die alte Struktur abgezielt haben könnten.

#### Wenn das Layout bricht: CSS-Selektoren im Fokus

Ähnlich wie JavaScript ist auch CSS eng an die HTML-Struktur gekoppelt. Ein Refactoring kann hier verheerende Auswirkungen auf das Layout haben, auch wenn es auf den ersten Blick nicht direkt die „Funktionalität“ betrifft. Aber was nützt ein funktionierender Button, wenn er durch ein anderes Element verdeckt oder gar nicht mehr sichtbar ist?

Ein typisches Beispiel sind übermäßig spezifische oder auf Verschachtelung basierende CSS-Selektoren.

```css
/* Vorher: Ein sehr brüchiger CSS-Selektor */
div#header div.nav-container ul li a {
  padding: 15px;
  color: #333;
  font-weight: bold;
}
```

Dieser Selektor funktioniert nur, solange die exakte Verschachtelung von `div#header`, `div.nav-container`, `ul`, `li` und `a` erhalten bleibt.

Beim Refactoring hast du das HTML modernisiert:

```html
<!-- Nachher: Saubere, semantische Navigation -->
<header>
  <nav class="main-navigation">
    <ul>
      <li><a href="#">Home</a></li>
      <!-- ... -->
    </ul>
  </nav>
</header>
```

Der alte CSS-Selektor greift nicht mehr. Das `div#header` wurde zu `<header>`, und das `div.nav-container` wurde zu `<nav class="main-navigation">`. Als Ergebnis verlieren deine Navigationslinks ihr komplettes Styling. Sie sind vielleicht winzig, unterstrichen und in der Standard-Browserfarbe Blau.

Die Lösung ist, auch das CSS zu refaktorisieren und robustere, weniger spezifische Selektoren zu verwenden:

```css
/* Nachher: Ein robusterer Selektor */
.main-navigation a {
  padding: 15px;
  color: #333;
  font-weight: bold;
}
```

Beim Testen der Funktionalität ist der visuelle Abgleich daher unerlässlich. Vergleiche die Seite nach dem Refactoring mit einem Screenshot oder der Live-Version von vor dem Umbau. Achte auf Abstände, Farben, Schriftgrößen und Positionierungen.

#### Vergessene Ecken: Formulare und Barrierefreiheit

Zwei Bereiche werden beim Testen oft übersehen, sind aber entscheidend für eine gute Nutzererfahrung.

**1. Formular-Interaktion:**
Bei Formularen reicht es nicht, nur den "Senden"-Button zu prüfen. Was ist mit der clientseitigen Validierung? Viele Legacy-Projekte nutzten komplexe JavaScript-Logiken, um zu prüfen, ob eine E-Mail-Adresse gültig ist oder ein Passwort die Mindestlänge hat. Diese Skripte sind oft stark an die `id`- oder `name`-Attribute der `<input>`-Felder sowie an die umgebende HTML-Struktur gekoppelt. Wenn du ein `<input type="text">` zu einem semantisch korrekten `<input type="email">` änderst, könnte das alte Validierungsskript aus dem Takt geraten. Gleichzeitig bietet das neue Attribut aber vielleicht schon eine eingebaute Browser-Validierung. Du musst sicherstellen, dass die Validierung immer noch konsistent und verständlich für den Nutzer funktioniert.

**2. Barrierefreiheit (Accessibility):**
Ein semantisches Refactoring hat oft das Ziel, die Barrierefreiheit zu verbessern. Aber hast du es auch wirklich getan? Die wichtigste manuelle Prüfung hierfür ist die Tastaturbedienung.

*   **Tab-Reihenfolge:** Navigiere mit der `Tab`-Taste durch die Seite. Ist die Reihenfolge logisch und nachvollziehbar? Erreicht der Fokus alle interaktiven Elemente wie Links, Buttons und Formularfelder? Springt der Fokus nicht an unerwartete Stellen?
*   **Fokus-Indikator:** Ist das fokussierte Element immer klar erkennbar (meist durch einen Rahmen, den sogenannten "focus ring")?
*   **Interaktion:** Lassen sich fokussierte Elemente mit der `Enter`- oder `Leertaste` auslösen? Funktionieren Dropdowns auch mit den Pfeiltasten?

Durch die Umstellung von `div`-Elementen mit `onclick`-Handler auf echte `<button>`-Elemente solltest du hier schon viel gewonnen haben, da Browser diese von Haus aus korrekt behandeln. Eine Überprüfung ist dennoch unerlässlich, um sicherzustellen, dass keine CSS-Regel (`outline: none;`) oder ein JavaScript-Eingriff dieses Standardverhalten zerstört hat.

Die Prüfung der Funktionalität ist kein lästiger Anhang, sondern der krönende Abschluss deines Refactorings. Sie ist die Qualitätskontrolle, die aus einer rein technischen Änderung eine echte Verbesserung für den Nutzer macht.
