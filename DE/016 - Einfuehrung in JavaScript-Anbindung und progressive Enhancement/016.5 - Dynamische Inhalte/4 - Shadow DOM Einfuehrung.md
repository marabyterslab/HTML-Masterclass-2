# Shadow DOM Einführung

### Shadow DOM: Dein eigener, gekapselter Kosmos im Web

Stell dir vor, du baust eine komplexe Webseite. Du integrierst vielleicht ein Widget von einem Drittanbieter, schreibst eine eigene, wiederverwendbare Komponente wie einen aufwendigen Video-Player oder eine interaktive Karte. Schnell stößt du auf ein klassisches Problem des Webs: Alles lebt im selben globalen Raum. Dein CSS für den Hauptinhalt kann versehentlich das Aussehen deines Widgets zerschießen. Umgekehrt könnten die Styles des Widgets dein Seitenlayout beeinflussen. JavaScript-Variablen können in Konflikt geraten, und IDs müssen auf der gesamten Seite einzigartig sein. Es ist ein bisschen wie eine WG, in der jeder den Kühlschrank und das Wohnzimmer mitbenutzt – Chaos ist vorprogrammiert.

Genau hier kommt das Shadow DOM ins Spiel. Es ist eine der fundamentalen Technologien hinter den Web Components und löst dieses Problem der globalen Einmischung durch ein mächtiges Konzept: Kapselung (Encapsulation).

Das Shadow DOM erlaubt es dir, einen versteckten, separaten DOM-Baum an ein Element im normalen DOM (wir nennen es ab jetzt **Light DOM**) anzuhängen. Dieser neue Baum ist der **Shadow Tree**, und er ist von der Außenwelt fast vollständig isoliert.

Die wichtigsten Begriffe, die du kennen solltest:

*   **Shadow Host:** Das ist das ganz normale HTML-Element im Light DOM, an dem der Shadow DOM "befestigt" ist.
*   **Shadow Root:** Der Wurzelknoten des verborgenen DOM-Baums. Er ist der Einstiegspunkt in die "Schattenwelt".
*   **Shadow Tree:** Der gesamte Baum aus Elementen, der innerhalb des Shadow Root lebt.

Das Geniale daran ist: CSS-Regeln, die du innerhalb des Shadow DOM definierst, gelten *nur* dort und sickern nicht nach außen. Umgekehrt dringen die meisten CSS-Regeln von der Hauptseite nicht in den Shadow DOM ein. Das Gleiche gilt für JavaScript: Ein `querySelector` auf dem Hauptdokument findet keine Elemente im Shadow DOM, und Ereignisse verhalten sich anders. Du erschaffst eine sichere, abgeschirmte Blase für deine Komponente.

#### Wie erstellt man ein Shadow DOM?

Ein Shadow DOM wird nicht mit HTML deklariert, sondern dynamisch mit JavaScript erzeugt. Das passt perfekt in unser Thema der dynamischen Inhalte. Schauen wir uns ein einfaches Beispiel an.

Nehmen wir an, wir haben ein einfaches `<div>` in unserem HTML, das als Host dienen soll:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Shadow DOM Demo</title>
</head>
<body>

    <h1>Willkommen im Light DOM</h1>
    
    <div id="host-element"></div>

    <script src="main.js"></script>
</body>
</html>
```

Nun erzeugen wir in unserer `main.js`-Datei einen Shadow DOM für dieses `<div>`:

```javascript
// 1. Das Host-Element im Light DOM auswählen
const host = document.querySelector('#host-element');

// 2. Einen Shadow Root an das Host-Element anhängen
// Der Modus 'open' bedeutet, dass wir von außen per JavaScript auf den Shadow DOM zugreifen können (z.B. über element.shadowRoot).
// 'closed' würde den Zugriff verwehren, wird aber selten empfohlen.
const shadowRoot = host.attachShadow({ mode: 'open' });

// 3. Den Shadow DOM mit Inhalt füllen
shadowRoot.innerHTML = `
    <style>
        /* Diese Styles gelten NUR hier drinnen! */
        p {
            color: rebeccapurple;
            font-family: sans-serif;
            border: 2px solid rebeccapurple;
            padding: 1rem;
        }
    </style>
    <p>Hallo aus dem Shadow DOM! Ich bin gekapselt und sicher.</p>
`;
```

Wenn du diese Seite im Browser öffnest, siehst du den lila-farbenen Absatz. Das Besondere daran: Wenn du die Entwickler-Tools öffnest, siehst du unter dem `<div id="host-element">` einen Eintrag `#shadow-root`. Klappst du diesen auf, findest du deinen `<style>`-Tag und den `<p>`-Tag. Sie sind da, aber sie sind nicht Teil des Haupt-DOM-Baums.

Wenn du jetzt eine weitere Regel in deinem globalen Stylesheet (oder in einem `<style>`-Tag im `<head>`) hinzufügst, die alle Absätze anspricht, wirst du sehen, dass sie keine Wirkung hat:

```css
/* Diese Regel in einer globalen CSS-Datei oder im <head>... */
p {
    color: red; /* ...wird den Absatz im Shadow DOM NICHT rot färben! */
}
```

Die Kapselung funktioniert!

#### Styling zwischen den Welten

Die totale Isolation ist stark, aber manchmal möchtest du deiner Komponente von außen ein bestimmtes Aussehen geben oder ihr erlauben, sich an das Design der Seite anzupassen. Das Shadow DOM bietet dafür elegante Mechanismen, ohne die Kapselung aufzubrechen.

##### 1. Das Host-Element von außen stylen

Der Shadow Host selbst ist ein ganz normales Element im Light DOM. Du kannst es also wie gewohnt mit CSS ansprechen.

```css
/* In deinem globalen Stylesheet */
#host-element {
    display: block; /* Wichtig für Layout-Eigenschaften */
    margin-top: 2rem;
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}
```

Diese Regel wirkt auf den "Container" deiner Komponente, aber nicht auf die Elemente *innerhalb* des Shadow DOM.

##### 2. Das Host-Element von innen stylen mit `:host`

Was aber, wenn die Komponente selbst entscheiden soll, wie sie sich im Layout verhält? Dafür gibt es die `:host` Pseudo-Klasse. Sie funktioniert *nur innerhalb* eines Shadow DOM und wählt den Shadow Host aus.

```javascript
shadowRoot.innerHTML = `
    <style>
        :host {
            display: block; /* Die Komponente sorgt selbst für korrektes Block-Verhalten */
            padding: 1rem;
            background-color: #f0f0f0;
            border-radius: 8px;
        }
        
        p {
            margin: 0;
            color: #333;
        }
    </style>
    <p>Ich style meinen eigenen Host von innen!</p>
`;
```

Mit `:host` kann eine Komponente grundlegende Styling-Regeln für sich selbst definieren, ohne dass der Nutzer der Komponente daran denken muss. Es gibt auch funktionale Varianten wie `:host(:hover)` oder `:host(.active)`, um auf Zustände des Host-Elements zu reagieren.

##### 3. Die Brücke bauen: CSS Custom Properties

Die mächtigste Methode, um eine anpassbare Komponente zu schaffen, sind CSS Custom Properties (auch als CSS-Variablen bekannt). Sie haben die besondere Eigenschaft, die Grenze des Shadow DOM zu "durchdringen". Das macht sie zum perfekten Werkzeug, um eine öffentliche Styling-API für deine Komponente zu erstellen.

Stell dir vor, du möchtest, dass der Nutzer die Akzentfarbe deiner Komponente festlegen kann.

Im Shadow DOM verwendest du die Variable mit einem Standardwert (Fallback):

```javascript
shadowRoot.innerHTML = `
    <style>
        :host {
            display: block;
            border-left: 5px solid var(--accent-color, orange); /* Fallback auf 'orange' */
            padding: 1rem;
        }
    </style>
    <p>Die Akzentfarbe kann von außen gesteuert werden.</p>
`;
```

Im globalen CSS kann der Nutzer diese Variable nun einfach definieren:

```css
/* In deinem globalen Stylesheet */
#host-element {
    --accent-color: steelblue;
}
```

Das Ergebnis: Der linke Rand der Komponente ist jetzt `steelblue`. Wenn die Variable nicht gesetzt wäre, würde sie auf `orange` zurückfallen. Auf diese Weise gibst du gezielte Kontrollpunkte frei, ohne die internen Styling-Details preiszugeben.

#### Inhalte von außen einfügen: Slots

Eine weitere Herausforderung ist, wie man eigenen, dynamischen Inhalt *in* eine gekapselte Komponente bekommt. Was, wenn du eine schicke Panel-Komponente mit einem Header und Footer baust, aber der Inhalt in der Mitte vom Nutzer bereitgestellt werden soll? Dafür gibt es das `<slot>`-Element.

Ein `<slot>` ist ein Platzhalter im Shadow DOM. HTML, das du innerhalb des Host-Elements im Light DOM schreibst, wird an der Stelle dieses Platzhalters gerendert.

Ändern wir unseren Shadow DOM, um einen Slot zu verwenden:

```javascript
shadowRoot.innerHTML = `
    <style>
        .wrapper { border: 1px solid #ccc; padding: 1em; }
        h3 { margin-top: 0; color: #555; }
    </style>
    <div class="wrapper">
        <h3>Titel der Komponente</h3>
        <slot></slot> <!-- Hier wird der Inhalt aus dem Light DOM eingefügt -->
    </div>
`;
```

Und jetzt passen wir unser HTML an, um Inhalt bereitzustellen:

```html
<div id="host-element">
    <!-- Dieser Inhalt wird in den Slot projiziert -->
    <p>Dies ist mein eigener Inhalt aus dem Light DOM.</p>
    <p>Er wird innerhalb der gekapselten Komponente angezeigt!</p>
</div>
```

Das Ergebnis ist magisch: Du siehst den Titel aus dem Shadow DOM, gefolgt von den beiden Absätzen aus dem Light DOM, alles verpackt in dem gestylten Wrapper aus dem Shadow DOM. Das Beste daran: Die Absätze behalten ihre globalen Styles (z.B. wenn `p` global auf `color: red` gesetzt ist), da sie technisch gesehen immer noch Teil des Light DOM sind. Sie werden nur visuell an einer anderen Stelle dargestellt.

Du kannst sogar mehrere, benannte Slots verwenden (`<slot name="header">`), um eine präzise Struktur für die von außen kommenden Inhalte vorzugeben.

Das Shadow DOM ist eine unglaublich leistungsfähige Technologie. Es ist das Herzstück wiederverwendbarer, robuster und wartbarer Web Components. Es befreit dich von den Fesseln des globalen Scopes und gibt dir die Werkzeuge an die Hand, um wirklich unabhängige, modulare Bausteine für das Web zu erstellen – jeder mit seiner eigenen kleinen, geschützten Welt.
