# Was ist WAI-ARIA?

### Was ist WAI-ARIA?

Stell dir vor, du baust eine wunderschöne, interaktive Benutzeroberfläche für eine Webanwendung. Du verwendest moderne JavaScript-Frameworks, erstellst dynamische Komponenten wie aufklappbare Menüs, komplexe Formulare mit Validierung in Echtzeit und Drag-and-Drop-Elemente. Für einen sehenden Nutzer, der eine Maus bedient, ist alles klar und intuitiv. Die visuellen Hinweise – Farben, Formen, Animationen – leiten ihn sicher durch die Anwendung.

Doch was passiert, wenn ein Nutzer deine Seite nicht sehen kann? Was, wenn er auf eine Tastaturbedienung oder eine Sprachsteuerung angewiesen ist? Für assistive Technologien wie Screenreader ist deine hochmoderne Oberfläche möglicherweise eine Blackbox. Ein `<div>`, das du mit CSS zu einem schicken Button gestylt und mit JavaScript klickbar gemacht hast, ist für einen Screenreader einfach nur ein `<div>` – ein generischer Container ohne Bedeutung. Er weiß nicht, dass es ein Button ist, was er tut oder in welchem Zustand er sich befindet (z. B. ob er gedrückt ist).

Genau hier kommt WAI-ARIA ins Spiel.

#### Die Brücke zwischen Funktion und Bedeutung

WAI-ARIA steht für „Web Accessibility Initiative – Accessible Rich Internet Applications“. Es ist eine technische Spezifikation des W3C, die eine Brücke schlägt zwischen hochdynamischen Webanwendungen und Nutzern mit assistiven Technologien. Man kann es sich als ein zusätzliches Vokabular für HTML vorstellen, das dir erlaubt, die Semantik von Elementen zu erweitern und zu präzisieren, wo HTML allein an seine Grenzen stößt.

Wichtig ist dabei ein Grundsatz, der oft als die **erste Regel von ARIA** bezeichnet wird: **Verwende ARIA nicht.**

Das klingt paradox, aber der Kern ist einfach: Wenn du ein natives HTML-Element verwenden kannst, das bereits die gewünschte Semantik und Funktionalität mitbringt, dann nutze es. Brauchst du einen Button? Verwende `<button>`. Brauchst du eine Checkbox? Verwende `<input type="checkbox">`. Diese Elemente werden von Browsern und assistiven Technologien von Haus aus verstanden. Sie bringen Tastaturbedienbarkeit und die richtige semantische Rolle gleich mit.

ARIA ist dein Werkzeug für die Fälle, in denen es kein passendes HTML-Element gibt oder du bestehende Elemente für komplexe Interaktionsmuster, sogenannte „Widgets“, anpassen musst. ARIA verändert dabei weder das Aussehen noch die Funktionalität deines Elements. Es ändert nur, wie das Element gegenüber der Accessibility API des Browsers (und damit gegenüber assistiven Technologien) kommuniziert wird. Du bist weiterhin selbst dafür verantwortlich, die erwartete Funktionalität, wie z. B. die Tastaturbedienung, per JavaScript zu implementieren.

#### Die drei Säulen von ARIA

ARIA lässt sich in drei Hauptkategorien von Attributen unterteilen: Rollen, Eigenschaften und Zustände.

**1. Rollen (Roles)**

Rollen definieren, was ein Element ist oder was es tut. Sie geben einem generischen Element wie `<div>` oder `<span>` eine Bedeutung, die es von Natur aus nicht hat. Du teilst dem Screenreader damit mit: „Hey, dieser `<div>` hier ist kein gewöhnlicher Container, sondern er spielt die Rolle einer `tablist` (einer Registerkartenleiste).“

Einige Beispiele für Rollen sind:
*   `role="button"`: Das Element ist ein Button.
*   `role="checkbox"`: Das Element ist eine Checkbox.
*   `role="dialog"`: Das Element ist ein Dialogfenster.
*   `role="navigation"`: Das Element enthält die Hauptnavigation der Seite.
*   `role="search"`: Das Element ist ein Suchfeld-Container.
*   `role="alert"`: Das Element enthält eine wichtige, dynamische Nachricht.

Wenn du also einen Button aus einem `<div>` bauen *musst*, ist das Hinzufügen von `role="button"` der erste Schritt, um ihn barrierefrei zu machen.

```html
<!-- Schlecht: Nur visuell ein Button -->
<div class="custom-button">Speichern</div>

<!-- Besser: Die Rolle wird kommuniziert -->
<div class="custom-button" role="button" tabindex="0">Speichern</div>
```
Das `tabindex="0"` ist hier ebenfalls entscheidend, da es das `<div>` in die Fokus-Reihenfolge der Seite aufnimmt und somit per Tastatur erreichbar macht. Ein natives `<button>`-Element hätte dies bereits von Haus aus.

**2. Eigenschaften (Properties)**

Eigenschaften beschreiben die Charakteristika oder Beziehungen eines Elements zu anderen Elementen. Sie sind in der Regel statischer als Zustände und ändern sich selten während der Interaktion des Nutzers.

Einige wichtige Eigenschaften sind:
*   `aria-label`: Gibt einem Element einen zugänglichen Namen, der den sichtbaren Text überschreibt oder ersetzt. Nützlich für Buttons, die nur ein Icon enthalten.
*   `aria-labelledby`: Verknüpft ein Element mit einem anderen Element auf der Seite, das als dessen Beschriftung dient.
*   `aria-describedby`: Verknüpft ein Element mit einer Beschreibung, die zusätzliche Informationen liefert.
*   `aria-controls`: Gibt an, welches Element von diesem Element gesteuert wird (z. B. ein Button, der ein Menü öffnet).
*   `aria-haspopup`: Informiert den Nutzer, dass das Element ein Popup-Menü, einen Dialog oder eine andere Art von aufklappbarem Inhalt steuert.

Ein klassisches Beispiel ist ein Schließen-Button in einem Modal-Dialog, der nur ein „X“-Icon anzeigt.

```html
<!-- Ohne ARIA würde ein Screenreader nur "mal" oder "X" vorlesen -->
<button>&times;</button>

<!-- Mit aria-label wird der Zweck klar kommuniziert -->
<button aria-label="Dialog schließen">&times;</button>
```

**3. Zustände (States)**

Zustände beschreiben die aktuelle Verfassung eines Elements. Im Gegensatz zu Eigenschaften können und sollen sich Zustände durch Nutzerinteraktion (via JavaScript) dynamisch ändern.

Häufig verwendete Zustände sind:
*   `aria-expanded`: Gibt an, ob ein aufklappbares Element (wie ein Akkordeon-Panel oder ein Dropdown-Menü) gerade geöffnet (`true`) oder geschlossen (`false`) ist.
*   `aria-selected`: Gibt an, ob ein Element in einer Gruppe (wie ein Tab in einer Tab-Leiste) gerade ausgewählt (`true`) ist.
*   `aria-checked`: Gibt den Zustand einer Checkbox, eines Radio-Buttons oder eines anderen Schalters an (`true`, `false` oder `mixed`).
*   `aria-disabled`: Informiert darüber, dass ein Element zwar vorhanden, aber aktuell nicht interaktiv (`true`) ist.
*   `aria-hidden`: Verbirgt ein Element vor assistiven Technologien. Wichtig: Dies hat keinen Einfluss auf die visuelle Darstellung. Ein Element mit `aria-hidden="true"` kann weiterhin sichtbar sein, wird aber von Screenreadern ignoriert.

Ein perfektes Beispiel ist ein Akkordeon-Menü. Der Button, der den Inhalt ein- und ausblendet, sollte seinen `aria-expanded`-Zustand ändern.

```html
<!-- Geschlossener Zustand -->
<button aria-expanded="false" aria-controls="content-1">
  Abschnitt 1
</button>
<div id="content-1" style="display: none;">
  <p>Hier steht der Inhalt von Abschnitt 1.</p>
</div>

<!-- Offener Zustand (nach Klick, durch JS geändert) -->
<button aria-expanded="true" aria-controls="content-1">
  Abschnitt 1
</button>
<div id="content-1" style="display: block;">
  <p>Hier steht der Inhalt von Abschnitt 1.</p>
</div>
```
Ein Screenreader würde nun verkünden: „Abschnitt 1, Button, zugeklappt“ und nach dem Klick „Abschnitt 1, Button, aufgeklappt“. Dieser kleine Unterschied in der Kommunikation ist für den Nutzer entscheidend, um die Funktionsweise der Komponente zu verstehen.

#### Ein praktisches Beispiel: Ein einfaches Tab-Interface

Stell dir vor, du hast ein Tab-Interface, das mit `<div>`-Elementen gebaut wurde. Ohne ARIA ist diese Struktur für einen Screenreader-Nutzer nur eine Ansammlung von Text und klickbaren Bereichen ohne Zusammenhang.

**HTML ohne ARIA:**
```html
<div>
  <div>Tab 1</div>
  <div>Tab 2</div>
</div>
<div>
  <div>Inhalt für Tab 1.</div>
  <div style="display:none;">Inhalt für Tab 2.</div>
</div>
```
Das ist semantisch bedeutungslos. Jetzt reichern wir es mit ARIA an, um die Beziehungen und Rollen klarzumachen.

**HTML mit WAI-ARIA:**
```html
<div role="tablist" aria-label="Beispiel-Tabs">
  <button role="tab" aria-selected="true" aria-controls="panel-1" id="tab-1">
    Tab 1
  </button>
  <button role="tab" aria-selected="false" aria-controls="panel-2" id="tab-2" tabindex="-1">
    Tab 2
  </button>
</div>
<div role="tabpanel" id="panel-1" aria-labelledby="tab-1">
  <p>Inhalt für Tab 1.</p>
</div>
<div role="tabpanel" id="panel-2" aria-labelledby="tab-2" hidden>
  <p>Inhalt für Tab 2.</p>
</div>
```

Analysieren wir, was hier passiert:
1.  `role="tablist"`: Der äußere Container wird als Leiste für die Tabs deklariert.
2.  `role="tab"`: Jeder Button wird als einzelner Tab identifiziert.
3.  `aria-selected`: Zeigt an, welcher Tab gerade aktiv ist. Dieser Zustand muss per JavaScript beim Umschalten geändert werden.
4.  `aria-controls`: Jeder Tab-Button verweist auf das Panel, das er steuert.
5.  `tabindex="-1"`: Sorgt dafür, dass inaktive Tabs nicht über die Tab-Taste erreicht werden können, wie es die Konvention für Tab-Interfaces vorsieht (Navigation zwischen Tabs erfolgt dann per Pfeiltasten).
6.  `role="tabpanel"`: Die Inhaltscontainer werden als Panels identifiziert.
7.  `aria-labelledby`: Jedes Panel verweist zurück auf seinen zugehörigen Tab-Button. Dies stellt die logische Verbindung her.
8.  `hidden`: Das inaktive Panel wird nicht nur visuell, sondern auch für assistive Technologien versteckt.

Durch diese ARIA-Attribute kann ein Screenreader dem Nutzer nun mitteilen: „Du befindest dich in einer Tab-Leiste mit zwei Tabs. Tab 1 ist ausgewählt. Drücke die Pfeiltasten, um zu wechseln.“ Diese Information ist der Schlüssel zu einer nutzbaren Oberfläche.

#### ARIA ist kein Allheilmittel

Bei aller Macht, die dir ARIA verleiht, ist es wichtig, es mit Bedacht einzusetzen. Falsch eingesetztes ARIA kann mehr schaden als nutzen und eine Benutzeroberfläche noch unzugänglicher machen als zuvor. Überschreibst du beispielsweise die Rolle eines nativen Elements fälschlicherweise (`<button role="heading">`), verwirrst du den Nutzer, da das Element nicht mehr die erwartete Funktionalität besitzt.

Denke immer daran: ARIA ist eine Schicht zusätzlicher Information. Es fügt keine Tastaturbedienung, keinen Fokus-Management und keine Funktionalität hinzu. All das musst du weiterhin selbst mit JavaScript implementieren, um die Erwartungen zu erfüllen, die du mit den ARIA-Attributen weckst. ARIA ist das Versprechen, das dein Code einlösen muss.
