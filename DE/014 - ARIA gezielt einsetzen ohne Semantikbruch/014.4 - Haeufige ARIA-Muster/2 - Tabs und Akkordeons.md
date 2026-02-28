# Tabs und Akkordeons

### Tabs und Akkordeons: Interaktive Inhalte zugänglich gestalten

In der modernen Webentwicklung stoßen wir oft auf eine Herausforderung: Wie präsentieren wir eine große Menge an Informationen auf begrenztem Raum, ohne die Nutzerin oder den Nutzer zu überfordern? Zwei der elegantesten und am weitesten verbreiteten Lösungen für dieses Problem sind Tabs und Akkordeons. Du hast sie sicher schon unzählige Male gesehen und benutzt. Tabs erlauben es, Inhalte in verschiedene Bereiche zu gliedern, zwischen denen man wie bei einem Aktenordner wechseln kann. Akkordeons hingegen verbergen Inhalte hinter aufklappbaren Überschriften, ähnlich einer Ziehharmonika.

Beide Muster sind fantastisch für die visuelle Aufgeräumtheit. Doch diese Interaktivität, die für sehende Nutzer mit einer Maus selbstverständlich ist, schafft für Menschen, die auf assistierende Technologien wie Screenreader oder eine reine Tastaturbedienung angewiesen sind, eine potenzielle Barriere. Wenn wir solche Komponenten nur mit ein wenig CSS und JavaScript zusammenbauen, fehlt die entscheidende semantische Information. Ein Screenreader weiß dann nicht, dass eine Liste von Links eigentlich eine Tab-Navigation ist oder dass eine Überschrift einen verborgenen Bereich auf- und zuklappen kann.

Hier kommt ARIA ins Spiel. Mit den richtigen ARIA-Attributen können wir diesen dynamischen Komponenten die Semantik verleihen, die sie benötigen, um für alle verständlich und bedienbar zu sein. Wir füllen die Lücke, die reines HTML hier hinterlässt, ohne die grundlegende Semantik zu brechen.

#### Das Tab-Muster: Digitale Reiter für deine Inhalte

Stell dir eine Produktseite vor. Anstatt alle Informationen – Beschreibung, technische Daten, Bewertungen – untereinander aufzulisten und die Seite endlos lang zu machen, gruppiert man sie oft in Tabs. Das ist übersichtlich und nutzerfreundlich. Schauen wir uns an, wie wir eine solche Tab-Komponente barrierefrei umsetzen.

##### Die grundlegende HTML-Struktur

Eine Tab-Komponente besteht immer aus zwei Teilen: der Tab-Liste (die Steuerelemente zum Umschalten) und den Tab-Panels (die dazugehörigen Inhaltsbereiche). Eine gute semantische Grundlage ist eine ungeordnete Liste für die Tabs und eine Reihe von `div`-Containern für die Panels.

```html
<div>
  <!-- Die Tab-Liste -->
  <ul>
    <li><a href="#panel-1">Beschreibung</a></li>
    <li><a href="#panel-2">Technische Daten</a></li>
    <li><a href="#panel-3">Bewertungen</a></li>
  </ul>

  <!-- Die Tab-Panels -->
  <div id="panel-1">
    <p>Inhalt der Beschreibung...</p>
  </div>
  <div id="panel-2">
    <p>Inhalt der technischen Daten...</p>
  </div>
  <div id="panel-3">
    <p>Inhalt der Bewertungen...</p>
  </div>
</div>
```

Diese Struktur ist ein guter Anfang, aber für einen Screenreader ist das nur eine Liste von Links und ein paar divs. Es gibt keine Beziehung zwischen dem Klick auf "Technische Daten" und dem Erscheinen des entsprechenden Inhalts.

##### Die Magie von ARIA: Rollen und Zustände

Um diese Beziehung herzustellen, verwenden wir spezifische ARIA-Rollen.

1.  **`role="tablist"`**: Das `<ul>`-Element, das unsere Tabs umschließt, erhält diese Rolle. Es signalisiert assistierenden Technologien: "Achtung, hier beginnt eine Gruppe von Tabs."
2.  **`role="tab"`**: Jedes Steuerelement, in unserem Fall die `<li>`- oder `<a>`-Elemente darin, bekommt die Rolle `tab`. Damit wird jedes Element als einzelner "Reiter" identifiziert.
3.  **`role="tabpanel"`**: Jeder Inhaltscontainer (`<div>`) erhält diese Rolle. Sie kennzeichnet den Bereich, dessen Inhalt zu einem Tab gehört.

Jetzt müssen wir die Tabs noch mit ihren Panels verknüpfen und ihren Zustand (aktiv oder inaktiv) mitteilen.

*   **`aria-controls`**: Jeder Tab (`role="tab"`) bekommt dieses Attribut. Sein Wert ist die `id` des zugehörigen Panels (`role="tabpanel"`). Damit wird die logische Verbindung hergestellt: "Dieser Tab kontrolliert jenen Inhalt."
*   **`aria-selected`**: Dieses Attribut kommt ebenfalls auf jeden Tab und zeigt an, ob er gerade ausgewählt ist. `aria-selected="true"` für den aktiven Tab, `aria-selected="false"` für alle anderen.
*   **`aria-labelledby`**: Jedes Panel (`role="tabpanel"`) sollte dieses Attribut erhalten. Sein Wert ist die `id` des zugehörigen Tabs. Dies verstärkt die Verbindung und der Screenreader kann ansagen, welcher Tab das gerade sichtbare Panel benennt.

Zusätzlich müssen die inaktiven Panels komplett versteckt werden, auch vor assistierenden Technologien. Das erreichst du am besten mit dem HTML-Attribut `hidden`. Ein `display: none;` in CSS hat denselben Effekt.

So sieht unsere erweiterte Struktur aus:

```html
<div>
  <ul role="tablist">
    <li role="presentation"><a href="#panel-1" id="tab-1" role="tab" aria-controls="panel-1" aria-selected="true">Beschreibung</a></li>
    <li role="presentation"><a href="#panel-2" id="tab-2" role="tab" aria-controls="panel-2" aria-selected="false">Technische Daten</a></li>
    <li role="presentation"><a href="#panel-3" id="tab-3" role="tab" aria-controls="panel-3" aria-selected="false">Bewertungen</a></li>
  </ul>

  <div id="panel-1" role="tabpanel" aria-labelledby="tab-1">
    <p>Inhalt der Beschreibung...</p>
  </div>
  <div id="panel-2" role="tabpanel" aria-labelledby="tab-2" hidden>
    <p>Inhalt der technischen Daten...</p>
  </div>
  <div id="panel-3" role="tabpanel" aria-labelledby="tab-3" hidden>
    <p>Inhalt der Bewertungen...</p>
  </div>
</div>
```
Ein kleiner Hinweis: Das `role="presentation"` auf den `<li>`-Elementen ist nützlich, um deren Listen-Semantik zu entfernen, da die `ul` nun eine `tablist` ist und ihre direkten Kinder `tab` sein sollten. Wenn du die Rolle direkt auf die Links legst, ist das ein gängiger Weg, dies zu lösen.

##### Die Tastaturbedienung ist entscheidend

Eine barrierefreie Komponente muss vollständig per Tastatur bedienbar sein. Für Tabs gibt es ein fest etabliertes Muster:

*   **Tabulator (`Tab`)**: Mit der Tab-Taste springst du *in* die Tab-Liste, und zwar direkt auf den *aktiven* Tab. Ein weiterer Druck auf `Tab` verlässt die gesamte Tab-Komponente und springt zum nächsten fokussierbaren Element auf der Seite. Du navigierst also nicht mit `Tab` *zwischen* den einzelnen Tabs.
*   **Pfeiltasten (`←` / `→` oder `↑` / `↓`)**: Um zwischen den Tabs zu wechseln, benutzt du die Pfeiltasten. Drückst du `→`, wird der nächste Tab aktiviert und sein Inhalt angezeigt. Drückst du `←`, wird der vorherige Tab aktiviert. Für vertikal ausgerichtete Tabs werden entsprechend die Pfeiltasten `↑` und `↓` verwendet.

Dieses Verhalten musst du mit JavaScript umsetzen. Dein Skript wartet auf Tastatureingaben auf der `tablist` und führt dann die entsprechenden Aktionen aus: Es ändert die `aria-selected`-Attribute, setzt oder entfernt das `hidden`-Attribut bei den Panels und verschiebt den Fokus auf den neu aktivierten Tab.

---

#### Das Akkordeon-Muster: Inhalte elegant ein- und ausklappen

Akkordeons sind perfekt für FAQ-Seiten, Glossare oder jede Art von Inhalt, der in Frage-Antwort-Paaren oder Überschrift-Text-Abschnitten organisiert ist. Der Nutzer sieht zuerst nur die Überschriften und kann bei Interesse den zugehörigen Inhalt aufklappen.

Im Gegensatz zu Tabs, bei denen immer ein Panel sichtbar ist, können bei einem Akkordeon alle Abschnitte geschlossen sein. Es ist auch üblich, dass mehrere Abschnitte gleichzeitig geöffnet sein können.

##### Die HTML-Struktur eines Akkordeons

Ein Akkordeon besteht typischerweise aus einer Reihe von Kopfzeilen (Headings), die als Schalter dienen, und den dazugehörigen Inhaltsbereichen.

```html
<h2>Häufig gestellte Fragen</h2>

<div>
  <h3>
    <button>Frage 1: Wie funktioniert die Lieferung?</button>
  </h3>
  <div>
    <p>Antwort auf Frage 1...</p>
  </div>
</div>

<div>
  <h3>
    <button>Frage 2: Welche Zahlungsmethoden gibt es?</button>
  </h3>
  <div>
    <p>Antwort auf Frage 2...</p>
  </div>
</div>
```
Die Verwendung eines echten `<button>`-Elements innerhalb der Überschrift ist hier bereits ein großer semantischer Gewinn. Ein Button ist von Natur aus fokussierbar und per `Enter` und `Leertaste` aktivierbar. Wir können diese Struktur mit ARIA aber noch präziser machen.

##### ARIA für aufklappbare Bereiche

Für Akkordeons ist das wichtigste ARIA-Attribut `aria-expanded`.

1.  **Der Auslöser (Trigger)**: Der Button, der den Inhalt ein- und ausblendet, ist unser zentrales Steuerelement. Er bekommt das Attribut `aria-expanded`.
    *   `aria-expanded="true"`: Der zugehörige Inhaltsbereich ist sichtbar.
    *   `aria-expanded="false"`: Der zugehörige Inhaltsbereich ist verborgen.
2.  **Die Verknüpfung**: Genau wie bei den Tabs verknüpfen wir den Button mit seinem Inhaltsbereich.
    *   **`aria-controls`**: Der Button bekommt dieses Attribut, das auf die `id` des Inhaltsbereichs verweist.
3.  **Der Inhalt (Panel)**: Der Inhaltsbereich selbst kann optional eine `role="region"` erhalten und mit `aria-labelledby` zurück auf den Button verweisen, um die Assoziation zu stärken.

Auch hier müssen die verborgenen Inhalte wieder mit dem `hidden`-Attribut versehen werden.

Unsere verbesserte, barrierefreie Struktur sieht so aus:

```html
<h2>Häufig gestellte Fragen</h2>

<div>
  <h3>
    <button id="accordion-btn-1" aria-expanded="false" aria-controls="accordion-panel-1">
      Frage 1: Wie funktioniert die Lieferung?
    </button>
  </h3>
  <div id="accordion-panel-1" role="region" aria-labelledby="accordion-btn-1" hidden>
    <p>Antwort auf Frage 1...</p>
  </div>
</div>

<div>
  <h3>
    <button id="accordion-btn-2" aria-expanded="false" aria-controls="accordion-panel-2">
      Frage 2: Welche Zahlungsmethoden gibt es?
    </button>
  </h3>
  <div id="accordion-panel-2" role="region" aria-labelledby="accordion-btn-2" hidden>
    <p>Antwort auf Frage 2...</p>
  </div>
</div>
```

##### Die erwartete Tastaturbedienung

Die Tastaturinteraktion für ein Akkordeon ist einfacher als bei Tabs:

*   **Tabulator (`Tab`)**: Mit `Tab` springst du von einer Akkordeon-Überschrift (dem Button) zur nächsten.
*   **Enter / Leertaste**: Wenn ein Button den Fokus hat, öffnet oder schließt ein Druck auf `Enter` oder die `Leertaste` den zugehörigen Inhaltsbereich. Dein JavaScript ist hier dafür verantwortlich, den Wert von `aria-expanded` umzuschalten und das `hidden`-Attribut zu setzen oder zu entfernen.
*   **Pfeiltasten (`↑` / `↓`) (Optional, aber empfohlen)**: Um die Navigation zu beschleunigen, kannst du es Nutzern ermöglichen, mit den Pfeiltasten zwischen den Akkordeon-Buttons zu springen.

Die Umsetzung dieser Muster erfordert ein Zusammenspiel von semantischem HTML, präzisem ARIA und ereignisgesteuertem JavaScript. Doch der Aufwand lohnt sich. Du verwandelst eine potenziell frustrierende Hürde in eine intuitive und zugängliche Erfahrung für alle Menschen, unabhängig davon, wie sie auf deine Inhalte zugreifen.
