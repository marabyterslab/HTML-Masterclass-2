# aria-expanded und aria-hidden

### Dynamische Zustände meistern: `aria-expanded` und `aria-hidden`

Im modernen Webdesign sind statische Seiten eher die Ausnahme als die Regel. Inhalte werden dynamisch ein- und ausgeblendet, Menüs klappen auf, Akkordeons öffnen sich und Dialogfenster erscheinen über dem restlichen Inhalt. Für sehende Nutzer sind diese Zustandsänderungen meist selbsterklärend – eine visuelle Bewegung oder das Erscheinen neuer Elemente signalisiert klar, was passiert.

Doch wie vermittelst du diese Dynamik an Nutzer, die auf assistierende Technologien wie Screenreader angewiesen sind? Genau hier kommen zwei zentrale ARIA-Attribute ins Spiel: `aria-expanded` und `aria-hidden`. Sie sind deine Werkzeuge, um die Lücke zwischen der visuellen Darstellung und der maschinenlesbaren Semantik zu schließen. Sie machen deine dynamischen Komponenten verständlich und bedienbar für alle.

#### `aria-expanded`: Den Zustand eines Bedienelements kommunizieren

Stell dir eine klassische Akkordeon-Komponente vor. Du hast eine Reihe von Überschriften, und bei einem Klick auf eine davon klappt der zugehörige Inhaltsbereich auf. Für einen Screenreader-Nutzer ist ohne zusätzliche Informationen nicht ersichtlich, dass die Überschrift ein interaktives Element ist, das etwas steuert. Und selbst wenn, weiß der Nutzer nicht, ob der Bereich darunter gerade geöffnet oder geschlossen ist.

Das `aria-expanded`-Attribut löst genau dieses Problem. Es ist ein Zustandsattribut, das du auf ein interaktives Element setzt, welches einen anderen Bereich ein- oder ausblendet. Es teilt der assistierenden Technologie unmissverständlich mit, in welchem Zustand sich das von ihm gesteuerte Element befindet.

`aria-expanded` hat drei mögliche Werte:

*   `"true"`: Das Element, das von diesem Bedienelement gesteuert wird, ist aktuell sichtbar oder „aufgeklappt“.
*   `"false"`: Das gesteuerte Element ist aktuell verborgen oder „zugeklappt“.
*   `undefined` (das Attribut fehlt): Das Bedienelement steuert keinen aufklappbaren Bereich.

**Wichtig:** Das `aria-expanded`-Attribut gehört immer auf das **auslösende Element** (den Trigger), also den Button oder den Link, der geklickt wird – nicht auf den Inhaltsbereich, der ein- oder ausgeblendet wird.

Schauen wir uns ein einfaches Akkordeon-Beispiel an. Die Grundstruktur könnte so aussehen:

```html
<h3>
  <button aria-expanded="false" aria-controls="section1">
    Kapitel 1: Die Grundlagen
  </button>
</h3>
<div id="section1" class="accordion-panel-hidden">
  <p>Hier steht der Inhalt von Kapitel 1...</p>
</div>
```

Analysieren wir diesen Code:

1.  Der `button` ist der Trigger. Er ist semantisch korrekt, da er eine Aktion auslöst.
2.  `aria-expanded="false"` signalisiert, dass der zugehörige Inhaltsbereich (`section1`) initial geschlossen ist. Ein Screenreader würde etwa ansagen: „Kapitel 1: Die Grundlagen, Schalter, eingeklappt“.
3.  `aria-controls="section1"` stellt eine programmatische Verbindung zwischen dem Button und dem Inhaltsbereich her. Das ist eine Best Practice, die die Benutzererfahrung weiter verbessert, da die assistierende Technologie nun genau weiß, *welches* Element gesteuert wird.
4.  Der Inhalts-`div` mit der `id="section1"` ist initial verborgen, zum Beispiel durch eine CSS-Klasse.

Wenn der Nutzer nun den Button aktiviert, ist es die Aufgabe deines JavaScript-Codes, sowohl die visuelle Darstellung als auch den ARIA-Zustand zu aktualisieren:

```javascript
const trigger = document.querySelector('button[aria-controls="section1"]');
const panel = document.getElementById('section1');

trigger.addEventListener('click', () => {
  const isExpanded = trigger.getAttribute('aria-expanded') === 'true';

  // Den ARIA-Zustand umschalten
  trigger.setAttribute('aria-expanded', !isExpanded);

  // Die visuelle Darstellung umschalten
  if (isExpanded) {
    panel.classList.add('accordion-panel-hidden');
  } else {
    panel.classList.remove('accordion-panel-hidden');
  }
});
```

Nach dem Klick würde der Screenreader den neuen Zustand ansagen: „Kapitel 1: Die Grundlagen, Schalter, ausgeklappt“. Der Nutzer weiß nun genau, dass der Inhalt sichtbar ist und er mit der Navigation fortfahren kann, um ihn zu lesen.

Andere typische Anwendungsfälle für `aria-expanded` sind Dropdown-Menüs, Navigationsmenüs auf Mobilgeräten (der „Burger-Button“) oder Baumansichten (Tree Views).

#### `aria-hidden`: Elemente aus der Wahrnehmung entfernen

Während `aria-expanded` den Zustand eines Triggers beschreibt, hat `aria-hidden` eine viel direktere und radikalere Funktion: Es entfernt ein Element und all seine untergeordneten Elemente komplett aus dem Accessibility Tree. Für einen Screenreader existiert ein mit `aria-hidden="true"` markiertes Element schlichtweg nicht. Es kann nicht erreicht, fokussiert oder vorgelesen werden.

Du denkst jetzt vielleicht: „Das Gleiche erreiche ich doch mit `display: none;` oder `visibility: hidden;` in CSS?“ Das ist korrekt. In den meisten Fällen, in denen du etwas visuell ausblendest, entfernen diese CSS-Eigenschaften das Element ebenfalls aus dem Accessibility Tree. `aria-hidden` wird dann überflüssig.

Der entscheidende Anwendungsfall für `aria-hidden="true"` tritt dann auf, wenn ein Element **visuell sichtbar**, aber für assistierende Technologien **irrelevant oder störend** ist.

Betrachten wir einige Szenarien:

**1. Dekorative oder redundante Inhalte**

Stell dir einen Button mit einem Icon und einem sichtbaren Textlabel vor:

```html
<button>
  <span class="icon-search" aria-hidden="true"></span>
  Suchen
</button>
```

Das `<span>` mit der Klasse `icon-search` stellt vielleicht ein Lupen-Icon dar. Für sehende Nutzer ist es eine nützliche visuelle Hilfe. Ein Screenreader würde jedoch möglicherweise den Unicode-Charakter des Icons oder einen leeren Span vorlesen, was zu Verwirrung führt. Da der Text „Suchen“ bereits die volle Bedeutung des Buttons transportiert, ist das Icon für den Screenreader redundant. Mit `aria-hidden="true"` stellen wir sicher, dass nur der relevante Text „Suchen, Schalter“ vorgelesen wird.

**2. Off-Screen-Navigationen**

Eine sehr verbreitete Technik für mobile Menüs ist es, die Navigation außerhalb des sichtbaren Viewports zu positionieren, zum Beispiel mit `transform: translateX(-100%)`. Visuell ist das Menü weg, aber es ist immer noch Teil des DOMs und damit für einen Screenreader potenziell erreichbar. Ein Nutzer könnte durch die Seite tabben und plötzlich den Fokus auf einem Link in einem unsichtbaren Menü landen – eine extrem verwirrende Erfahrung.

Hier ist `aria-hidden="true"` die perfekte Lösung. Solange das Menü außerhalb des Bildschirms ist, gibst du dem Container das Attribut:

```html
<nav id="main-nav" class="is-offscreen" aria-hidden="true">
  <!-- Navigationslinks -->
</nav>
```

Wenn der Nutzer den Burger-Button klickt, um das Menü einzublenden, entfernt dein JavaScript nicht nur die CSS-Klasse, die es versteckt, sondern auch das `aria-hidden`-Attribut (oder setzt es auf `false`):

```javascript
// Beim Öffnen des Menüs
nav.classList.remove('is-offscreen');
nav.setAttribute('aria-hidden', 'false'); // Oder nav.removeAttribute('aria-hidden');
```

So stellst du sicher, dass das Menü nur dann für Screenreader wahrnehmbar und bedienbar ist, wenn es auch visuell präsent ist.

**3. Modale Dialogfenster**

Wenn ein modales Fenster (ein Pop-up) geöffnet wird, sollte der Fokus des Nutzers auf dieses Fenster beschränkt sein. Der restliche Seiteninhalt im Hintergrund ist zwar oft noch schwach sichtbar, aber er sollte nicht interaktiv sein. Um zu verhindern, dass ein Screenreader-Nutzer versehentlich aus dem Modal „heraustabbt“ und mit den Elementen im Hintergrund interagiert, wird der Hauptinhalt der Seite (z.B. alles innerhalb von `<main>` und `<header>`) mit `aria-hidden="true"` versehen, solange das Modal aktiv ist.

```html
<body>
  <header id="page-header">...</header>
  <main id="page-main">...</main>
  
  <div role="dialog" aria-modal="true" class="modal-is-open">
    <!-- Inhalt des Modals -->
  </div>
</body>
```

Wenn das Modal geöffnet wird, setzt dein JavaScript:

```javascript
document.getElementById('page-header').setAttribute('aria-hidden', 'true');
document.getElementById('page-main').setAttribute('aria-hidden', 'true');
```

Wenn das Modal geschlossen wird, müssen diese Attribute unbedingt wieder entfernt werden.

**Eine wichtige Warnung:** Setze `aria-hidden="true"` niemals auf ein Element, das fokussierbar ist oder fokussierbare Kinderelemente enthält. Dies führt zu einer sogenannten „Geisterfalle“: Ein Nutzer kann per Tab-Taste auf ein Element springen, das für den Screenreader nicht existiert. Der Fokus ist dann im Nichts, und der Nutzer ist desorientiert. Moderne Accessibility-Checker warnen dich in der Regel vor solchen Fehlern.

#### Das Zusammenspiel in der Praxis

`aria-expanded` und `aria-hidden` wirken oft Hand in Hand, bedienen aber unterschiedliche Zwecke. `aria-expanded` beschreibt den **Zustand eines Controllers**, während `aria-hidden` die **Sichtbarkeit eines Bereichs** für assistierende Technologien steuert.

In unserem Akkordeon-Beispiel könntest du beides verwenden:

```html
<h3>
  <button aria-expanded="false" aria-controls="section1">
    Kapitel 1: Die Grundlagen
  </button>
</h3>
<div id="section1" aria-hidden="true">
  <p>Hier steht der Inhalt von Kapitel 1...</p>
</div>
```

Beim Klick würdest du dann `aria-expanded` auf `"true"` und `aria-hidden` auf `"false"` setzen. Dieser Ansatz ist absolut valide. Oft ist es jedoch einfacher und robuster, sich auf eine Methode zur Steuerung der Sichtbarkeit zu verlassen. Die Verwendung des `hidden`-HTML-Attributs ist hier oft die beste Wahl, da es ein Element sowohl visuell als auch für den Accessibility Tree versteckt und es nicht fokussierbar macht:

```html
<!-- Initialer Zustand -->
<button aria-expanded="false" ...>Titel</button>
<div id="content" hidden>...</div>

<!-- Zustand nach Klick -->
<button aria-expanded="true" ...>Titel</button>
<div id="content">...</div>
```

Dein JavaScript würde hier einfach das `hidden`-Attribut hinzufügen oder entfernen, was sauberer und weniger fehleranfällig ist als das manuelle Jonglieren von CSS-Klassen und `aria-hidden`.

Die bewusste und korrekte Anwendung von `aria-expanded` und `aria-hidden` ist ein entscheidender Schritt, um komplexe und dynamische Webanwendungen für alle Nutzer zugänglich zu machen. Sie sind keine komplizierte Magie, sondern präzise Kommunikationsmittel, die Klarheit und Kontrolle in die Interaktion bringen.
