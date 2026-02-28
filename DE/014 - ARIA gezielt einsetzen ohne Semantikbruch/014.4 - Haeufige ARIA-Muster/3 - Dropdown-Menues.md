# Dropdown-Menüs

### Dropdown-Menüs

Dropdown-Menüs gehören zu den am häufigsten anzutreffenden interaktiven Elementen im Web. Du kennst sie: Ein Klick auf einen Button oder einen Link öffnet ein darunter oder daneben liegendes Panel mit weiteren Optionen, Links oder Aktionen. So praktisch sie für sehende Nutzer sind, die mit einer Maus navigieren, so problematisch können sie für Menschen sein, die auf Tastaturbedienung oder Screenreader angewiesen sind – zumindest, wenn sie nicht sorgfältig und mit Bedacht auf Barrierefreiheit umgesetzt werden.

Ein typisches, aber leider oft unzugängliches Dropdown-Menü wird häufig aus einfachen `<div>`-Elementen zusammengebaut, deren Sichtbarkeit mit JavaScript umgeschaltet wird. Das Problem dabei ist, dass ein `<div>` keine semantische Bedeutung hat. Es ist nur ein neutraler Container. Für eine assistierende Technologie (AT) wie einen Screenreader ist ein klickbares `<div>` nicht von einem normalen Textabschnitt zu unterscheiden. Es wird nicht als interaktives Element angekündigt, sein Zustand (offen oder geschlossen) ist unbekannt, und die Beziehung zwischen dem Auslöser und dem Menü, das erscheint, ist unklar.

Hier kommt ARIA ins Spiel. Mit den richtigen ARIA-Attributen kannst du diese semantische Lücke schließen und einem Screenreader genau die Informationen geben, die er benötigt, um das Dropdown-Menü korrekt zu interpretieren und bedienbar zu machen.

#### Die semantische Basis: Ein Button und eine Liste

Bevor wir uns ARIA zuwenden, erinnern wir uns an das oberste Gebot: Brich die Semantik nicht, sondern erweitere sie. Die beste Grundlage für einen Dropdown-Auslöser ist ein natives HTML-`<button>`-Element. Warum?

1.  **Fokus:** Ein `<button>` ist von Natur aus per Tastatur (mit der Tab-Taste) erreichbar.
2.  **Interaktion:** Er reagiert standardmäßig auf Klicks sowie auf die `Enter`- und `Leertaste`. Diese Funktionalität musst du nicht selbst programmieren.
3.  **Semantik:** Screenreader kündigen ein `<button>`-Element als „Schaltfläche“ an, was dem Nutzer sofort signalisiert: „Hier kann ich etwas auslösen.“

Für das Menü selbst eignet sich eine ungeordnete Liste (`<ul>`) mit Listenelementen (`<li>`), die wiederum Links (`<a>`) oder andere interaktive Elemente enthalten. Diese Struktur ist semantisch sinnvoll, da sie eine Sammlung von zusammengehörigen Optionen darstellt.

Unsere Grundstruktur sieht also so aus:

```html
<div>
  <button id="menu-button">Menü öffnen</button>
  <ul id="menu-content">
    <li><a href="/profil">Mein Profil</a></li>
    <li><a href="/einstellungen">Einstellungen</a></li>
    <li><a href="/logout">Abmelden</a></li>
  </ul>
</div>
```

Dieses Grundgerüst ist ein guter Anfang, aber es fehlt die entscheidende Verbindung zwischen dem Button und der Liste. Der Screenreader weiß immer noch nicht, dass der Button diese spezifische Liste steuert oder ob die Liste gerade sichtbar ist oder nicht.

#### Die ARIA-Attribute für die Verbindung und den Zustand

Um diese Lücke zu schließen, benötigen wir ein paar zentrale ARIA-Attribute am Auslöser, also unserem `<button>`:

1.  **`aria-haspopup="true"`**: Dieses Attribut teilt der assistierenden Technologie mit, dass das Element ein Menü oder ein anderes "Popup"-Element (wie ein Dialogfeld) öffnet. Für ein typisches Dropdown-Menü ist der Wert `"true"` oder, noch spezifischer, `"menu"` angemessen. Dadurch wird der Button beispielsweise als „Menü-Schaltfläche“ angekündigt.

2.  **`aria-controls="[ID des Menüs]"`**: Hier schaffst du die programmatische Verbindung. Du gibst dem Attribut als Wert die `id` des Elements, das gesteuert wird – in unserem Fall die `id` der `<ul>`. Damit weiß der Screenreader genau, welcher Inhalt zu diesem Button gehört. Das ermöglicht es Nutzern von Screenreadern, direkt vom Button zum geöffneten Menü zu springen.

3.  **`aria-expanded="false"` / `"true"`**: Dies ist das wohl wichtigste Attribut für dynamische Inhalte. Es beschreibt den Zustand des Menüs: Ist es gerade sichtbar oder nicht? `"false"` bedeutet „eingeklappt“ oder „versteckt“, `"true"` bedeutet „ausgeklappt“ oder „sichtbar“. Dieser Wert muss dynamisch mit JavaScript geändert werden, immer dann, wenn du das Menü ein- oder ausblendest.

Mit diesen Attributen erweitern wir unseren Button:

```html
<button
  id="menu-button"
  aria-haspopup="true"
  aria-controls="menu-content"
  aria-expanded="false">
  Menü öffnen
</button>
```

#### Die ARIA-Rollen für das Menü selbst

Nun müssen wir dem Menü und seinen Einträgen ebenfalls eine klare semantische Rolle zuweisen. Dies hilft dem Screenreader, in einen speziellen „Menü-Modus“ zu wechseln, der eine intuitive Navigation mit den Pfeiltasten ermöglicht.

1.  **`role="menu"`**: Diese Rolle wird der `<ul>` zugewiesen. Sie signalisiert, dass es sich hierbei um eine Liste von Menüoptionen handelt.

2.  **`role="menuitem"`**: Jedes klickbare Element innerhalb des Menüs, also die `<a>`-Tags in den `<li>`, sollte diese Rolle erhalten. Damit wird jeder Eintrag als eigenständiger Menüpunkt identifiziert.

Unser komplettes, barrierefreies HTML-Grundgerüst sieht damit so aus:

```html
<div>
  <button
    id="menu-button"
    aria-haspopup="true"
    aria-controls="menu-content"
    aria-expanded="false">
    Menü öffnen
  </button>
  <ul id="menu-content" role="menu" hidden>
    <li role="none"><a href="/profil" role="menuitem">Mein Profil</a></li>
    <li role="none"><a href="/einstellungen" role="menuitem">Einstellungen</a></li>
    <li role="none"><a href="/logout" role="menuitem">Abmelden</a></li>
  </ul>
</div>
```

Du siehst hier zwei zusätzliche Details:
*   Das `hidden`-Attribut auf der `<ul>`: Dies ist eine semantisch saubere Methode, das Menü standardmäßig zu verstecken. Es wird von CSS (`display: none;`) und Screenreadern gleichermaßen verstanden.
*   `role="none"` oder `role="presentation"` auf den `<li>`-Elementen: In einem `role="menu"` erwarten Screenreader direkt `role="menuitem"` als Kinder. Die `<li>`-Elemente sind semantisch "im Weg". Mit `role="none"` nehmen wir dem `<li>` seine Listenelement-Semantik und machen es für die assistierende Technologie quasi unsichtbar, sodass die Struktur `menu -> menuitem` korrekt abgebildet wird.

#### Die Magie des JavaScripts: ARIA zum Leben erwecken

ARIA-Attribute sind ein Versprechen. Du versprichst dem Nutzer, dass sich ein Element auf eine bestimmte Weise verhält. Dieses Versprechen musst du mit JavaScript einlösen. Ohne JavaScript ist `aria-expanded` nur ein statisches Attribut ohne Funktion.

Dein JavaScript muss folgende Aufgaben übernehmen:

1.  **Zustand umschalten:** Bei einem Klick auf den Button musst du den Wert von `aria-expanded` zwischen `"true"` und `"false"` wechseln und gleichzeitig das `hidden`-Attribut des Menüs entfernen oder hinzufügen.

2.  **Tastaturbedienung sicherstellen:** Ein barrierefreies Menü muss vollständig per Tastatur bedienbar sein.
    *   **Schließen mit `Escape`:** Wenn das Menü geöffnet ist, sollte ein Druck auf die `Escape`-Taste es schließen und den Fokus zurück auf den Button setzen.
    *   **Navigation mit Pfeiltasten:** Die Pfeiltasten (hoch/runter) sollten den Fokus zwischen den Menüeinträgen (`role="menuitem"`) bewegen.
    *   **Schließen bei Klick außerhalb:** Ein Klick außerhalb des Menüs sollte es ebenfalls schließen.

Hier ist ein einfaches Beispiel, wie die Logik zum Öffnen und Schließen aussehen könnte:

```javascript
const menuButton = document.getElementById('menu-button');
const menuContent = document.getElementById('menu-content');

menuButton.addEventListener('click', () => {
  const isExpanded = menuButton.getAttribute('aria-expanded') === 'true';

  if (isExpanded) {
    // Menü schließen
    menuButton.setAttribute('aria-expanded', 'false');
    menuContent.hidden = true;
  } else {
    // Menü öffnen
    menuButton.setAttribute('aria-expanded', 'true');
    menuContent.hidden = false;
  }
});
```

Dieses Skript kümmert sich nur um das grundlegende Umschalten. Eine vollständige Implementierung würde auch die Keyboard-Events (Pfeiltasten, Escape) und das Fokusmanagement behandeln.

#### Styling mit CSS

Du kannst die ARIA-Zustände auch direkt für dein Styling nutzen. Anstatt eine Klasse wie `.is-open` zu verwenden, kannst du direkt auf das `aria-expanded`-Attribut zugreifen. Das hält deinen Code sauber und konsistent.

```css
/* Das Menü ist standardmäßig versteckt, wenn es nicht das `hidden`-Attribut hat */
#menu-content {
  display: none;
  /* Weitere Styles für Position, Aussehen etc. */
}

/* Wenn `hidden` entfernt wird, wird es sichtbar */
#menu-content:not([hidden]) {
  display: block;
}

/* Alternativer Ansatz mit dem Attribut-Selektor */
button[aria-expanded="true"] + ul {
  display: block;
}
```
Der Ansatz mit dem `hidden`-Attribut ist oft robuster, da es sowohl das visuelle Aussehen (via Browser-Stylesheet `[hidden] { display: none; }`) als auch die Zugänglichkeit (Element wird aus dem Accessibility Tree entfernt) steuert.

Indem du diese Prinzipien befolgst – eine solide semantische HTML-Basis, die gezielte Erweiterung mit ARIA-Rollen und -Attributen und die Erfüllung des interaktiven Versprechens durch JavaScript –, verwandelst du ein potenziell frustrierendes Element in ein vollständig zugängliches und benutzerfreundliches Dropdown-Menü.
