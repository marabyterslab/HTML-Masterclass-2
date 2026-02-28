# Custom Elements definieren

### Custom Elements definieren

Stell dir vor, du könntest das Vokabular von HTML erweitern. Anstatt dich nur auf die Standard-Tags wie `<div>`, `<p>` oder `<img>` zu beschränken, könntest du deine eigenen, bedeutungsvollen Tags erfinden – zum Beispiel `<user-profile>`, `<product-card>` oder `<countdown-timer>`. Genau das ermöglichen dir Custom Elements. Sie sind das Herzstück der Web Components und geben dir die Freiheit, wiederverwendbare, gekapselte und semantisch reiche HTML-Elemente zu erstellen.

Die Definition eines Custom Elements ist ein zweistufiger Prozess, der vollständig in JavaScript stattfindet:

1.  **Die Klasse definieren:** Du erstellst eine JavaScript-Klasse, die das Verhalten und die Logik deines Elements beschreibt. Diese Klasse erbt von der Basisklasse `HTMLElement`.
2.  **Das Element registrieren:** Du teilst dem Browser mit, unter welchem HTML-Tag-Namen deine Klasse verwendet werden soll.

Lass uns diese beiden Schritte im Detail betrachten.

#### Schritt 1: Die Blaupause – Die JavaScript-Klasse

Jedes Custom Element benötigt eine "Blaupause" oder eine "Bauanleitung", die sein Verhalten definiert. Diese Blaupause ist eine JavaScript-Klasse. Das Wichtigste dabei ist, dass diese Klasse von `HTMLElement` erben muss. Dadurch stellst du sicher, dass dein neues Element alle grundlegenden Eigenschaften und Methoden eines Standard-HTML-Elements besitzt. Es verhält sich also von Natur aus wie ein Teil des DOM – du kannst ihm Attribute geben, Event-Listener hinzufügen, seinen Stil per CSS ändern und vieles mehr.

Die grundlegendste Form einer solchen Klasse sieht so aus:

```js
class MyElement extends HTMLElement {
  constructor() {
    // WICHTIG: super() muss immer zuerst im Konstruktor aufgerufen werden!
    super();
    
    // Hier wird die Logik des Elements initialisiert.
    console.log('Ein <my-element> wurde erstellt!');
  }
}
```

Schauen wir uns das genauer an:

*   **`class MyElement extends HTMLElement`**: Wir definieren eine neue Klasse namens `MyElement`. Mit `extends HTMLElement` sagen wir JavaScript, dass unsere Klasse eine spezialisierte Version eines generischen HTML-Elements ist. Sie erbt also alles, was ein `<div>` oder `<span>` auch kann.
*   **`constructor()`**: Der Konstruktor ist eine spezielle Methode, die automatisch aufgerufen wird, sobald eine Instanz deines Elements erzeugt wird (z.B. wenn der Browser es im HTML-Code findet oder du es per JavaScript erstellst).
*   **`super()`**: Der Aufruf von `super()` ist innerhalb des Konstruktors **zwingend erforderlich** und muss die allererste Anweisung sein. Er ruft den Konstruktor der übergeordneten Klasse (`HTMLElement`) auf und sorgt dafür, dass das Element korrekt im Hintergrund initialisiert wird. Vergisst du `super()`, erhältst du einen Fehler.

Dieser Code allein tut noch nicht viel, außer eine Nachricht auf der Konsole auszugeben. Aber er ist das Fundament, auf dem wir aufbauen.

#### Schritt 2: Ein Name für das Kind – Das Element registrieren

Nachdem du die Klasse als Blaupause erstellt hast, weiß der Browser noch nicht, wie er sie verwenden soll. Du musst ihm mitteilen, welcher HTML-Tag-Name mit dieser Klasse verknüpft ist. Das geschieht über die globale `customElements` Registry und ihre `define()`-Methode.

Die `define()`-Methode erwartet zwei Argumente:

1.  Einen String, der den Namen deines HTML-Tags festlegt.
2.  Die Klasse, die du zuvor definiert hast.

```js
// Registriere die Klasse 'MyElement' unter dem Tag-Namen 'my-element'.
customElements.define('my-element', MyElement);
```

Damit ist der Prozess abgeschlossen! Du hast dem Browser beigebracht, was ein `<my-element>` ist.

**Wichtige Regeln für die Benennung:**

Der Name deines Custom Elements muss einer entscheidenden Regel folgen: Er **muss einen Bindestrich (`-`) enthalten**.

*   **Richtig:** `my-element`, `user-profile`, `app-header`
*   **Falsch:** `myelement`, `profile`, `header`

Diese Regel wurde eingeführt, um Konflikte zwischen deinen eigenen Elementen und potenziellen zukünftigen, offiziellen HTML-Tags zu vermeiden. So wird sichergestellt, dass der HTML-Parser immer eindeutig zwischen einem Standard-Element und einem Custom Element unterscheiden kann.

#### Das Element im HTML verwenden

Sobald die JavaScript-Klasse definiert und beim Browser registriert ist, kannst du dein neues Element direkt im HTML verwenden, als wäre es schon immer da gewesen:

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Mein erstes Custom Element</title>
</head>
<body>

  <h1>Custom Elements in Aktion</h1>
  <my-element></my-element>
  <my-element></my-element>

  <script>
    // Die Definition unseres Elements
    class MyElement extends HTMLElement {
      constructor() {
        super();
        console.log('Ein <my-element> wurde erstellt!');
      }
    }
    
    // Die Registrierung des Elements
    customElements.define('my-element', MyElement);
  </script>

</body>
</html>
```

Wenn du diese HTML-Datei im Browser öffnest und die Entwicklerkonsole einschaltest, siehst du die Nachricht "Ein <my-element> wurde erstellt!" zweimal ausgegeben – einmal für jede Instanz des Tags im HTML.

### Der Lebenszyklus eines Custom Elements

Ein Custom Element ist mehr als nur ein statischer Tag. Es durchläuft einen Lebenszyklus, ähnlich wie eine Komponente in einem modernen JavaScript-Framework. Der Browser ruft zu bestimmten Schlüsselmomenten spezielle Methoden auf deiner Klasse auf, die als "Lifecycle Callbacks" bekannt sind. Diese geben dir die Möglichkeit, auf Veränderungen zu reagieren und die Logik deines Elements zu steuern.

#### `connectedCallback()`: Wenn das Element die Bühne betritt

Diese Methode wird aufgerufen, sobald dein Element in das DOM eingefügt wird. Das ist der perfekte Ort, um initiale Setup-Arbeiten durchzuführen:

*   Inhalte rendern (z.B. via `this.innerHTML`).
*   Event-Listener für interne Elemente hinzufügen.
*   Daten von einem Server abrufen.

Erweitern wir unser Beispiel:

```js
class UserCard extends HTMLElement {
  constructor() {
    super();
    // Der Konstruktor sollte leichtgewichtig bleiben.
    // DOM-Manipulationen gehören eher in den connectedCallback.
  }
  
  connectedCallback() {
    this.innerHTML = `
      <div style="border: 1px solid #ccc; padding: 1rem; border-radius: 8px;">
        <h2>Benutzerkarte</h2>
        <p>Hallo! Ich bin eine Custom Element.</p>
      </div>
    `;
  }
}

customElements.define('user-card', UserCard);
```

Wenn du nun `<user-card></user-card>` in dein HTML einfügst, wird automatisch der Inhalt aus dem `connectedCallback` gerendert.

#### `disconnectedCallback()`: Wenn das Element die Bühne verlässt

Das Gegenstück zum `connectedCallback`. Diese Methode wird aufgerufen, wenn dein Element aus dem DOM entfernt wird. Hier solltest du Aufräumarbeiten erledigen, um Speicherlecks (Memory Leaks) zu verhindern:

*   Event-Listener entfernen, die im `connectedCallback` hinzugefügt wurden.
*   Laufende Timer (z.B. mit `setInterval`) stoppen.
*   Offene Netzwerkverbindungen trennen.

```js
class ClockWidget extends HTMLElement {
  connectedCallback() {
    this.timer = setInterval(() => {
      this.textContent = new Date().toLocaleTimeString();
    }, 1000);
  }
  
  disconnectedCallback() {
    // Wichtig: Den Timer aufräumen, wenn das Element entfernt wird!
    clearInterval(this.timer);
    console.log('Uhr wurde entfernt, Timer gestoppt.');
  }
}

customElements.define('clock-widget', ClockWidget);
```

#### `attributeChangedCallback(name, oldValue, newValue)`: Wenn Attribute sich ändern

Custom Elements können wie normale HTML-Tags Attribute haben (`<my-element data-id="123">`). Diese Methode ermöglicht es dir, auf Änderungen dieser Attribute zu reagieren.

Damit dieser Callback funktioniert, musst du dem Browser explizit mitteilen, welche Attribute er beobachten soll. Das geschieht aus Performance-Gründen über eine statische `observedAttributes`-Getter-Methode in deiner Klasse.

```js
class UserProfile extends HTMLElement {
  // 1. Dem Browser mitteilen, welche Attribute beobachtet werden sollen.
  static get observedAttributes() {
    return ['name', 'avatar'];
  }

  constructor() {
    super();
  }
  
  connectedCallback() {
    this.render();
  }

  // 2. Auf Änderungen reagieren.
  attributeChangedCallback(name, oldValue, newValue) {
    console.log(`Attribut '${name}' geändert von '${oldValue}' zu '${newValue}'`);
    this.render();
  }
  
  render() {
    const name = this.getAttribute('name') || 'Unbekannter Benutzer';
    const avatar = this.getAttribute('avatar') || 'default-avatar.png';
    
    this.innerHTML = `
      <div style="display: flex; align-items: center; gap: 1rem;">
        <img src="${avatar}" alt="Avatar" width="50" height="50" style="border-radius: 50%;">
        <strong>${name}</strong>
      </div>
    `;
  }
}

customElements.define('user-profile', UserProfile);
```

Jetzt kannst du das Element im HTML so verwenden:

```html
<user-profile name="Anna" avatar="anna.png"></user-profile>
```

Und das Beste: Es ist reaktiv! Wenn du das Attribut später mit JavaScript änderst, wird der `attributeChangedCallback` ausgelöst und die `render()`-Methode neu aufgerufen, um die Anzeige zu aktualisieren:

```js
const profile = document.querySelector('user-profile');
// Dies löst attributeChangedCallback aus und aktualisiert die Anzeige.
profile.setAttribute('name', 'Max Mustermann');
```

#### `adoptedCallback()`: Bei einem Umzug in ein anderes Dokument

Dieser Callback ist seltener im Einsatz. Er wird aufgerufen, wenn dein Element in ein neues Dokument verschoben wird, zum Beispiel aus dem Hauptdokument in den DOM eines `<iframe>`. Hier könntest du spezifische Anpassungen vornehmen, die bei einem solchen "Dokumentenwechsel" nötig sind.

Durch die Kombination einer JavaScript-Klasse und der `customElements.define()`-Methode schaffst du eine mächtige Abstraktion. Du baust deine eigenen, wiederverwendbaren und semantisch klaren HTML-Tags, die eine eigene Logik und einen eigenen Lebenszyklus besitzen. Dies ist der erste und wichtigste Schritt auf dem Weg zu einem komponentenbasierten Aufbau deiner Webanwendungen mit den Bordmitteln des Browsers.
