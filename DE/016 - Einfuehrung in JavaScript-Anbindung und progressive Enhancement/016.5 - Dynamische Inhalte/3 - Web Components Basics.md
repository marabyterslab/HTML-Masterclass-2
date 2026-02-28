# Web Components Basics

### Web Components: Die Grundlagen wiederverwendbarer Bausteine

Du kennst HTML in- und auswendig. Du weißt, wie du mit `<p>`, `<div>`, `<img>` und vielen anderen Tags eine strukturierte Webseite aufbaust. Aber hast du dir jemals gewünscht, du könntest deine eigenen, maßgeschneiderten HTML-Elemente erfinden? Elemente, die nicht nur eine feste Struktur, sondern auch ihr eigenes Verhalten und Aussehen mitbringen? Genau hier kommen Web Components ins Spiel.

Web Components sind kein Framework oder eine Bibliothek, sondern eine Sammlung von Web-Plattform-APIs, die direkt in modernen Browsern verankert sind. Sie ermöglichen es dir, neue, vollständig gekapselte und wiederverwendbare HTML-Tags zu erstellen. Stell sie dir wie Legosteine für das Web vor: Du baust einmal einen komplexen Stein und kannst ihn dann überall in deinen Projekten wiederverwenden, ohne dir Sorgen über Seiteneffekte oder Konflikte machen zu müssen.

Die Magie der Web Components beruht auf vier Haupttechnologien, die perfekt ineinandergreifen.

#### Die vier Säulen der Web Components

Um zu verstehen, wie du deine eigenen Elemente bauen kannst, müssen wir uns die vier grundlegenden Konzepte ansehen, die Web Components ausmachen.

**1. Custom Elements**

Das Herzstück der Web Components ist die Fähigkeit, eigene HTML-Elemente mit benutzerdefinierten Namen zu definieren. Ein Standard-HTML-Tag wie `<p>` hat einen einfachen Namen. Ein Custom Element muss per Konvention immer einen Bindestrich im Namen enthalten, zum Beispiel `<user-profile>` oder `<fancy-button>`. Dieser Bindestrich sorgt dafür, dass der Browser sofort erkennt, dass es sich um ein benutzerdefiniertes Element handelt und es nicht mit zukünftigen, offiziellen HTML-Tags kollidieren kann.

Um ein Custom Element zu erstellen, definierst du eine JavaScript-Klasse, die von der Basisklasse `HTMLElement` erbt. In dieser Klasse kannst du die Logik und das Verhalten deines Elements festlegen. Anschließend registrierst du dieses Element in der sogenannten `CustomElementRegistry` des Browsers.

```javascript
// Definiere die Logik für unser neues Element
class SimpleGreeting extends HTMLElement {
  constructor() {
    // Rufe immer super() zuerst im Konstruktor auf
    super();

    // Füge einfachen Inhalt hinzu
    this.textContent = 'Hallo, ich bin ein Custom Element!';
  }
}

// Registriere das neue Element beim Browser
customElements.define('simple-greeting', SimpleGreeting);
```

Sobald dieser JavaScript-Code ausgeführt wurde, kannst du dein neues Element direkt in deinem HTML verwenden, als wäre es schon immer da gewesen:

```html
<simple-greeting></simple-greeting>
```

Das Ergebnis im Browser ist ein neues Element, das den Text "Hallo, ich bin ein Custom Element!" anzeigt.

**2. Shadow DOM**

Ein wesentliches Merkmal von Web Components ist die Kapselung. Du möchtest nicht, dass das CSS deiner Hauptseite versehentlich das Aussehen deines Elements zerstört, und umgekehrt soll das interne Styling deines Elements nicht nach außen "durchsickern" und andere Teile der Seite beeinflussen.

Hier kommt der Shadow DOM ins Spiel. Der Shadow DOM ist ein versteckter, gekapselter DOM-Baum, der an ein Element angehängt wird. Dieser "Schattenbaum" ist vom Haupt-DOM der Seite getrennt. Alles, was innerhalb des Shadow DOM passiert – HTML-Struktur, CSS-Regeln, JavaScript-Logik – bleibt darin gefangen.

Du erstellst einen Shadow DOM für ein Element mit der Methode `attachShadow()`.

```javascript
class ScopedElement extends HTMLElement {
  constructor() {
    super();

    // Erstelle einen Shadow DOM für dieses Element
    const shadow = this.attachShadow({ mode: 'open' });

    // Erstelle ein paar interne Elemente
    const wrapper = document.createElement('span');
    wrapper.setAttribute('class', 'wrapper');

    const style = document.createElement('style');
    style.textContent = `
      .wrapper {
        padding: 1rem;
        background-color: lightblue;
        border: 1px solid blue;
      }
    `;

    const text = document.createElement('p');
    text.textContent = 'Dieser Inhalt ist gekapselt.';

    // Füge die erstellten Elemente zum Shadow DOM hinzu
    shadow.appendChild(style);
    shadow.appendChild(wrapper);
    wrapper.appendChild(text);
  }
}

customElements.define('scoped-element', ScopedElement);
```

Wenn du nun `<scoped-element></scoped-element>` in deinem HTML verwendest, siehst du ein Element mit blauem Hintergrund. Die CSS-Regel `.wrapper` gilt nur *innerhalb* dieses Elements. Selbst wenn du auf deiner Hauptseite eine andere Regel für `.wrapper` hättest, kämen sie sich nicht in die Quere.

**3. HTML Templates**

Wenn du eine komplexe Struktur für dein Element hast, wäre es umständlich, jedes einzelne `div`, `span` und `p` in JavaScript mit `document.createElement()` zu erzeugen. Hierfür gibt es eine elegantere Lösung: das `<template>`-Element.

Ein `<template>`-Tag ist ein spezielles HTML-Element, dessen Inhalt vom Browser nicht gerendert wird. Er wird geparst, aber bleibt inert (inaktiv), bis du ihn per JavaScript aktivierst. Es dient als wiederverwendbare Vorlage für die Struktur deines Custom Elements.

```html
<template id="user-card-template">
  <style>
    /* Stile, die nur innerhalb des Shadow DOM gelten */
    .card {
      font-family: sans-serif;
      border: 1px solid #ccc;
      border-radius: 8px;
      padding: 16px;
      width: 250px;
    }
  </style>
  <div class="card">
    <h3 id="name"></h3>
    <p id="email"></p>
  </div>
</template>
```

In deiner Custom-Element-Klasse kannst du auf diese Vorlage zugreifen, ihren Inhalt klonen und in den Shadow DOM deines Elements einfügen.

```javascript
class UserCard extends HTMLElement {
  constructor() {
    super();
    const shadow = this.attachShadow({ mode: 'open' });

    // Finde die Vorlage im DOM
    const template = document.getElementById('user-card-template');
    
    // Klone den Inhalt der Vorlage
    const templateContent = template.content.cloneNode(true);

    // Füge den geklonten Inhalt in den Shadow DOM ein
    shadow.appendChild(templateContent);
  }
}
customElements.define('user-card', UserCard);
```

**4. ES Modules**

Die vierte Säule ist eigentlich keine spezifische Web-Component-API, aber der moderne Standard, um JavaScript-Code zu organisieren und zu teilen. ES Modules erlauben es dir, deine Custom-Element-Definitionen in separate Dateien auszulagern und sie bei Bedarf zu importieren. Dies hält deinen Code sauber und wartbar.

Du würdest deine `UserCard`-Klasse in einer Datei wie `user-card.js` speichern und sie dann in deiner Haupt-HTML-Datei einfach importieren:

```html
<script type="module" src="user-card.js"></script>

<!-- Jetzt kannst du das Element verwenden -->
<user-card></user-card>
```

#### Komponenten mit Leben füllen: Attribute und Lebenszyklus

Bisher sind unsere Komponenten statisch. Wirklich nützlich werden sie aber erst, wenn wir ihnen von außen Daten übergeben können, zum Beispiel über HTML-Attribute.

Custom Elements haben einen Lebenszyklus, der aus mehreren Methoden besteht, die automatisch vom Browser aufgerufen werden, wenn bestimmte Ereignisse eintreten.

*   `connectedCallback()`: Wird aufgerufen, wenn das Element in den DOM eingefügt wird. Perfekt für Initialisierungen oder das Abrufen von Daten.
*   `disconnectedCallback()`: Wird aufgerufen, wenn das Element aus dem DOM entfernt wird. Gut, um Event-Listener zu entfernen oder andere Aufräumarbeiten durchzuführen.
*   `attributeChangedCallback(name, oldValue, newValue)`: Wird aufgerufen, wenn ein beobachtetes Attribut hinzugefügt, entfernt oder geändert wird.

Um `attributeChangedCallback` zu nutzen, musst du dem Element zuerst mitteilen, auf welche Attribute es achten soll. Das geschieht über eine statische `observedAttributes`-Eigenschaft.

Erweitern wir unser `UserCard`-Beispiel, um dynamische Daten über Attribute zu akzeptieren:

```javascript
// In user-card.js

class UserCard extends HTMLElement {
  // 1. Definiere, welche Attribute beobachtet werden sollen
  static get observedAttributes() {
    return ['name', 'email'];
  }

  constructor() {
    super();
    this.attachShadow({ mode: 'open' });
    
    // Wir holen uns die Vorlage wie zuvor
    const template = document.getElementById('user-card-template');
    const content = template.content.cloneNode(true);
    this.shadowRoot.appendChild(content);
  }

  // 2. Reagiere auf Attribut-Änderungen
  attributeChangedCallback(name, oldValue, newValue) {
    if (name === 'name') {
      this.shadowRoot.querySelector('#name').textContent = newValue;
    } else if (name === 'email') {
      this.shadowRoot.querySelector('#email').textContent = newValue;
    }
  }
  
  // 3. Optional: Initialwerte setzen, wenn das Element im DOM ist
  connectedCallback() {
    // Falls Attribute schon beim Parsen gesetzt wurden,
    // können wir hier eine initiale Aktualisierung erzwingen.
    if (this.hasAttribute('name')) {
      this.shadowRoot.querySelector('#name').textContent = this.getAttribute('name');
    }
    if (this.hasAttribute('email')) {
      this.shadowRoot.querySelector('#email').textContent = this.getAttribute('email');
    }
  }
}

customElements.define('user-card', UserCard);
```

Jetzt kannst du deine Komponente in HTML mit Daten füttern:

```html
<!-- Die Vorlage muss weiterhin im HTML vorhanden sein -->
<template id="user-card-template">
  <!-- ... (Inhalt wie oben) ... -->
</template>

<user-card name="Anna Schmidt" email="anna.schmidt@example.com"></user-card>
<user-card name="Ben Weber" email="ben.weber@example.com"></user-card>
```

Du hast nun zwei vollständig funktionierende, wiederverwendbare und gekapselte `user-card`-Komponenten auf deiner Seite. Jede hat ihre eigene interne Struktur und ihre eigenen Daten, verhält sich aber konsistent. Das ist die wahre Stärke von Web Components: Sie bringen Ordnung, Struktur und Wiederverwendbarkeit in deine Frontend-Entwicklung, und das alles mit nativen Bordmitteln des Browsers.
