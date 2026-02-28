# Widget-Roles (tablist, slider, dialog)

### Interaktive Erlebnisse schaffen: Die Widget-Rollen `tablist`, `slider` und `dialog`

Nachdem du nun die grundlegenden ARIA-Rollen kennengelernt hast, die bestehende Strukturen semantisch anreichern, tauchen wir nun tiefer in eine besonders spannende Kategorie ein: die Widget-Rollen. Anders als Landmark- oder Dokumentstruktur-Rollen beschreiben Widgets interaktive Komponenten, die in nativem HTML so oft nicht existieren. Sie sind das Äquivalent zu den Bausteinen, aus denen du komplexe Benutzeroberflächen in Desktop-Anwendungen kennst.

Der entscheidende Punkt bei Widget-Rollen ist: Sie sind ein Versprechen an den Nutzer. Wenn du einem Element eine Widget-Rolle wie `tab` oder `slider` gibst, versprichst du, dass es sich auch wie ein Tab oder ein Slider verhalten wird. Dieses Verhalten musst du vollständig mit JavaScript implementieren. ARIA liefert hier nur den Bauplan und die Semantik, die assistiven Technologien verraten, was du da baust. Ohne das passende Skript bleibt es eine leere Hülle und führt zu einer frustrierenden Erfahrung.

In diesem Kapitel schauen wir uns drei der häufigsten und nützlichsten Widget-Rollen an: `tablist`, `slider` und `dialog`.

#### `role="tablist"`: Strukturierte Inhalte auf Abruf

Stell dir eine Produktseite vor, auf der du zwischen "Beschreibung", "Technische Daten" und "Bewertungen" wechseln kannst. Anstatt alle Inhalte untereinander darzustellen und die Seite unnötig lang zu machen, gruppiert man sie oft in Tabs. Ein Klick auf einen Reiter (Tab) blendet den zugehörigen Inhaltsbereich (Tab-Panel) ein und die anderen aus.

Genau dieses Muster bildet die `tablist`-Rolle ab. Sie erfordert eine klare Struktur aus mehreren zusammenspielenden Rollen und Attributen, um für alle Nutzer, insbesondere für Screenreader-Nutzer, verständlich und bedienbar zu sein.

**Die Kernstruktur eines Tab-Interface:**

1.  **Der Container (`role="tablist"`):** Dies ist das umschließende Element für alle klickbaren Tabs. Es signalisiert: "Hier beginnt eine Gruppe von Reitern." Oft ist dies ein `<ul>`- oder `<div>`-Element.
2.  **Die Reiter (`role="tab"`):** Jedes einzelne Element, das einen Inhaltsbereich steuert, erhält diese Rolle. Es kann ein `<li>`, ein `<button>` oder ein `<a>`-Element sein.
3.  **Die Inhaltsbereiche (`role="tabpanel"`):** Dies sind die Container, die den eigentlichen Inhalt beherbergen, der ein- und ausgeblendet wird.

Damit diese drei Teile miteinander kommunizieren können, sind spezifische ARIA-Attribute unerlässlich:

*   `aria-selected="true"`: Dieses Attribut wird auf dem aktiven `tab` gesetzt. Alle anderen, inaktiven Tabs erhalten `aria-selected="false"`. Dies ist das wichtigste Signal für assistive Technologien, welcher Tab gerade ausgewählt ist.
*   `aria-controls="panel-id"`: Jeder `tab` muss über dieses Attribut mit dem `tabpanel` verbunden werden, das er steuert. Der Wert ist die `id` des entsprechenden Panels.
*   `aria-labelledby="tab-id"`: Umgekehrt sollte jeder `tabpanel` über dieses Attribut auf seinen steuernden `tab` verweisen. Das gibt dem Inhaltsbereich einen zugänglichen Namen, sodass ein Screenreader verkünden kann: "Registerkartenfeld, Beschreibung", wenn der Fokus darauf landet.
*   `tabindex`: Nur der aktive `tab` sollte in der Fokus-Reihenfolge der Seite sein und `tabindex="0"` erhalten. Alle inaktiven Tabs bekommen `tabindex="-1"`, um sie aus der normalen Tab-Navigation (mit der Tab-Taste) zu entfernen. Die Navigation zwischen den Tabs selbst wird dann über die Pfeiltasten gesteuert.

**Tastaturbedienung ist Pflicht!**

Ein `tablist`-Widget muss eine intuitive Tastaturbedienung ermöglichen:

*   **Pfeil nach links/rechts:** Wechselt zwischen den Tabs. Die Aktivierung kann dabei direkt erfolgen oder erst nach Bestätigung mit Enter/Leertaste.
*   **Home/Ende:** Springt zum ersten bzw. letzten Tab in der Liste.
*   **Tab-Taste:** Wenn der Fokus auf einem aktiven Tab liegt, springt der nächste Druck der Tab-Taste in den zugehörigen `tabpanel` (oder zum ersten fokussierbaren Element darin).

Hier ist ein Beispiel für die grundlegende HTML-Struktur. Das JavaScript, das die Attribute und das Verhalten steuert, ist hier bewusst weggelassen, um den Fokus auf die ARIA-Implementierung zu legen.

```html
<!-- Die Tab-Liste -->
<ul role="tablist">
  <li role="presentation">
    <a href="#beschreibung" role="tab" id="tab-beschreibung" aria-selected="true" aria-controls="panel-beschreibung" tabindex="0">
      Beschreibung
    </a>
  </li>
  <li role="presentation">
    <a href="#technische-daten" role="tab" id="tab-tech-daten" aria-selected="false" aria-controls="panel-tech-daten" tabindex="-1">
      Technische Daten
    </a>
  </li>
</ul>

<!-- Die Tab-Inhaltsbereiche -->
<div class="tabpanels">
  <div role="tabpanel" id="panel-beschreibung" aria-labelledby="tab-beschreibung">
    <p>Hier steht die ausführliche Produktbeschreibung...</p>
  </div>
  <div role="tabpanel" id="panel-tech-daten" aria-labelledby="tab-tech-daten" hidden>
    <p>Hier stehen die technischen Daten...</p>
  </div>
</div>
```

Beachte `role="presentation"` auf den `<li>`-Elementen. Da die Semantik hier durch `tablist` und `tab` definiert wird, nehmen wir die Listen-Semantik des `<li>` bewusst zurück, um Verwirrung bei Screenreadern zu vermeiden.

---

#### `role="slider"`: Werte intuitiv auswählen

Ein Slider (Schieberegler) ist ein klassisches Widget, um einen Wert aus einem bestimmten Bereich auszuwählen. Denk an einen Lautstärkeregler, die Einstellung der Helligkeit oder die Auswahl eines Preissegments in einem Online-Shop. Während ein `<input type="range">` diese Funktionalität nativ bereitstellt, gibt es Situationen, in denen du aus gestalterischen Gründen einen eigenen Slider aus `<div>`-Elementen bauen musst. Hier kommt `role="slider"` ins Spiel.

Ein Slider hat keine komplexen Unter-Rollen, aber er lebt von seinen Zustands-Attributen:

*   `aria-valuenow`: Gibt den aktuellen Wert des Sliders an. Dieses Attribut ist das Herzstück und muss von deinem JavaScript bei jeder Änderung aktualisiert werden.
*   `aria-valuemin`: Definiert den minimal möglichen Wert des Sliders (z. B. "0").
*   `aria-valuemax`: Definiert den maximal möglichen Wert (z. B. "100").
*   `aria-label` oder `aria-labelledby`: Jeder Slider braucht eine Beschriftung, damit Nutzer wissen, was sie einstellen. "Lautstärke" wäre ein gutes Beispiel.
*   `aria-valuetext` (optional): Manchmal ist der numerische Wert nicht sehr aussagekräftig. Ein Slider für Kleidergrößen könnte `aria-valuenow="2"` haben, aber mit `aria-valuetext="M"` einen verständlicheren Text liefern.
*   `tabindex="0"`: Damit der Slider mit der Tastatur fokussiert werden kann.

**Tastaturbedienung eines Sliders:**

*   **Pfeil nach links/unten:** Verringert den Wert um einen kleinen Schritt.
*   **Pfeil nach rechts/oben:** Erhöht den Wert um einen kleinen Schritt.
*   **Page Up/Page Down:** Erhöht/verringert den Wert um einen größeren Schritt.
*   **Home:** Setzt den Wert auf das Minimum (`aria-valuemin`).
*   **Ende:** Setzt den Wert auf das Maximum (`aria-valuemax`).

Ein einfacher, mit ARIA ausgezeichneter Slider könnte so aussehen:

```html
<div
  role="slider"
  tabindex="0"
  aria-label="Lautstärke"
  aria-valuemin="0"
  aria-valuemax="100"
  aria-valuenow="75">
  <!-- Visuelle Elemente wie der Griff und die Leiste kommen hier hinein -->
  <div class="slider-rail">
    <div class="slider-thumb" style="left: 75%;"></div>
  </div>
</div>
```

Dein JavaScript würde nun auf Tastatur- und Mausereignisse lauschen, die Position des `slider-thumb` anpassen und vor allem den Wert von `aria-valuenow` synchron halten.

---

#### `role="dialog"`: Fokussierte Interaktionen

Ein Dialog ist ein Fenster, das sich über den restlichen Inhalt der Seite legt, um eine bestimmte Aufgabe zu erledigen oder eine Information anzuzeigen. Beispiele sind Login-Formulare, Cookie-Banner oder Bestätigungsfenster. Wenn ein Dialog aktiv ist, sollte der Nutzer nicht mehr mit dem darunterliegenden Seiteninhalt interagieren können. Dieses Verhalten nennt man "modal".

Während es mittlerweile das native `<dialog>`-Element gibt, das vieles davon automatisch erledigt, ist das Verständnis der ARIA-Rolle `dialog` immer noch essenziell, um ältere Implementierungen zu verstehen oder hochgradig angepasste Dialoge barrierefrei zu gestalten.

Ein barrierefreier Dialog basiert auf drei Säulen, die du per JavaScript sicherstellen musst:

1.  **Fokus-Management:** Sobald der Dialog geöffnet wird, muss der Tastaturfokus aktiv in den Dialog bewegt werden, idealerweise auf das erste interaktive Element (z. B. ein Eingabefeld oder den Schließen-Button). Ein sehender Nutzer orientiert sich visuell, ein Screenreader-Nutzer folgt dem Fokus.
2.  **Fokus-Falle (Focus Trap):** Solange der Dialog geöffnet ist, darf der Nutzer nicht mit der Tab-Taste aus dem Dialog heraus auf die dahinterliegende Seite navigieren können. Der Fokus muss innerhalb des Dialogs "gefangen" bleiben und am Ende wieder zum Anfang des Dialogs springen.
3.  **Fokus-Wiederherstellung:** Wenn der Dialog geschlossen wird, muss der Fokus exakt zu dem Element zurückkehren, das den Dialog ursprünglich geöffnet hat (z. B. der "Login"-Button).

Die ARIA-Attribute für einen Dialog sind überschaubar, aber mächtig:

*   `role="dialog"`: Kennzeichnet den Hauptcontainer des Dialogs.
*   `aria-modal="true"`: Teilt assistiven Technologien mit, dass der Rest der Seite derzeit inaktiv ist. Das ist entscheidend für das modale Verhalten.
*   `aria-labelledby`: Sollte auf die `id` der sichtbaren Überschrift des Dialogs verweisen. Dies gibt dem Dialog seinen zugänglichen Namen, der beim Öffnen angesagt wird (z. B. "Dialog, Anmelden").
*   `aria-describedby` (optional): Kann auf einen Absatz mit einer genaueren Beschreibung oder Anweisung im Dialog verweisen.

**Tastaturbedienung eines Dialogs:**

*   **Escape:** Die Escape-Taste muss den Dialog zuverlässig schließen.

Hier ist das HTML-Grundgerüst eines modalen Dialogs:

```html
<!-- Button zum Öffnen des Dialogs -->
<button id="open-dialog-btn">Anmelden</button>

<!-- Der Dialog selbst, anfangs versteckt -->
<div
  role="dialog"
  id="login-dialog"
  aria-modal="true"
  aria-labelledby="dialog-title"
  hidden>

  <h2 id="dialog-title">Anmelden</h2>
  <form>
    <label for="username">Benutzername:</label>
    <input type="text" id="username">
    <!-- Weitere Formularfelder -->
  </form>
  <button id="close-dialog-btn">Schließen</button>

</div>
```

Die Umsetzung der drei Säulen des Fokus-Managements ist eine reine JavaScript-Aufgabe. Du musst den Fokus beim Öffnen setzen, die Tab-Reihenfolge überwachen und den Fokus beim Schließen wiederherstellen. Widget-Rollen wie diese zeigen eindrücklich, wie eng ARIA, HTML und JavaScript zusammenarbeiten müssen, um eine wirklich barrierefreie und intuitive Benutzererfahrung zu schaffen.
