# Rollen, Zustände und Eigenschaften

# Rollen, Zustände und Eigenschaften: Die drei Säulen von ARIA

Wenn du beginnst, mit ARIA zu arbeiten, wirst du schnell feststellen, dass sich alles um drei zentrale Konzepte dreht: Rollen (Roles), Zustände (States) und Eigenschaften (Properties). Man kann sie als die grundlegenden Bausteine betrachten, mit denen du die semantische Lücke zwischen dem, was ein Nutzer sieht, und dem, was eine assistive Technologie versteht, schließt. Stell sie dir wie ein Vokabular vor, das du deinen HTML-Elementen beibringst, damit sie klar und deutlich mit Screenreadern und anderen Werkzeugen kommunizieren können.

In diesem Kapitel schauen wir uns diesen Dreiklang genau an. Du wirst verstehen, was jede dieser Kategorien bedeutet, wie sie zusammenspielen und wann du sie einsetzen solltest, um wirklich barrierefreie Webinhalte zu schaffen.

### Rollen (Roles): "Wer bist du?"

Eine ARIA-Rolle definiert, was ein Element ist oder was es tut. Sie beantwortet die grundlegende Frage: "Welchen Zweck hat dieses Ding auf der Seite?" In nativem HTML haben viele Elemente bereits eine implizite Rolle. Ein `<button>`-Element hat die Rolle `button`, ein `<a>`-Element mit einem `href`-Attribut hat die Rolle `link` und ein `<nav>`-Element hat die Rolle `navigation`.

Du greifst immer dann zu einer ARIA-Rolle, wenn du ein Element verwendest, das von Natur aus keine oder die falsche Semantik für den gewünschten Zweck hat. Das ist oft der Fall, wenn du mit `<div>`- oder `<span>`-Elementen komplexe, interaktive Komponenten baust, für die es kein passendes HTML-Element gibt.

Ein klassisches Beispiel ist ein `<div>`, das durch CSS wie ein Button aussieht und per JavaScript eine Klick-Funktion erhält.

```html
<!-- Visuell ein Button, aber semantisch nur ein Container -->
<div class="custom-button">Speichern</div>
```

Ein sehender Nutzer erkennt hier sofort einen Button. Ein Screenreader jedoch verkündet nur "Speichern, Gruppe" oder etwas Ähnliches. Er hat keine Ahnung, dass es sich um ein interaktives Element handelt, das man aktivieren kann.

Hier kommt die ARIA-Rolle ins Spiel. Indem du `role="button"` hinzufügst, teilst du der assistiven Technologie unmissverständlich mit: "Hey, dieses `<div>` ist ein Button!"

```html
<!-- Semantisch als Button identifiziert -->
<div role="button" tabindex="0" class="custom-button">Speichern</div>
```

Beachte das zusätzliche `tabindex="0"`. Die ARIA-Rolle allein macht ein Element nicht interaktiv. Sie fügt keine Funktionalität hinzu, sondern nur Semantik. Damit dein "Fake-Button" auch per Tastatur erreichbar und bedienbar ist (wie ein echter `<button>`), musst du ihn in die Fokus-Reihenfolge der Seite aufnehmen. JavaScript ist dann weiterhin nötig, um die Klick-Ereignisse und die Aktivierung per `Enter`- oder `Leertaste` zu behandeln.

Die erste Regel von ARIA lautet: Wenn es ein natives HTML-Element gibt, das die gewünschte Semantik und Funktionalität bietet, nutze es! Ein `<button>`-Element ist hier also immer die bessere, robustere und einfachere Wahl. ARIA-Rollen sind für die Fälle reserviert, in denen HTML an seine Grenzen stößt, wie bei komplexen Widgets (z. B. `tablist`, `slider` oder `dialog`).

### Eigenschaften (Properties): "Was kannst du und womit hängst du zusammen?"

Eigenschaften beschreiben Charakteristiken oder Beziehungen eines Elements, die sich in der Regel nicht während der Interaktion mit der Seite ändern. Sie geben Kontext und verbinden Elemente miteinander. Sie beantworten Fragen wie: "Welche Beschriftung gehört zu dir?" (`aria-labelledby`), "Gibt es eine ausführlichere Beschreibung für dich?" (`aria-describedby`) oder "Welches andere Element kontrollierst du?" (`aria-controls`).

Im Gegensatz zu Zuständen (die wir gleich besprechen) sind Eigenschaften eher statischer Natur.

Ein gutes Beispiel ist die Verknüpfung eines Eingabefeldes mit einer externen Beschriftung. Normalerweise nutzt du dafür ein `<label>`-Element mit einem `for`-Attribut. Manchmal ist die Beschriftung aber durch andere Elemente gegeben, etwa eine Überschrift.

```html
<h2 id="search-label">Produktsuche</h2>
<!-- ... anderer Code ... -->
<input type="search" aria-labelledby="search-label">
```

Hier teilt `aria-labelledby` der assistiven Technologie mit, dass der Text innerhalb des Elements mit der ID `search-label` die zugängliche Beschriftung für dieses Eingabefeld ist. Der Screenreader wird also "Produktsuche, Suchfeld" ansagen, obwohl kein direktes `<label>` vorhanden ist.

Eine weitere wichtige Eigenschaft ist `aria-controls`. Sie schafft eine explizite Verbindung zwischen einem steuernden Element und dem Element, das es steuert. Stell dir eine Tab-Navigation vor:

```html
<button role="tab" aria-controls="panel-1">Tab 1</button>
<div role="tabpanel" id="panel-1">
  Inhalt von Tab 1...
</div>
```

Das Attribut `aria-controls="panel-1"` am Button teilt dem Screenreader mit: "Wenn du mich aktivierst, hat das Auswirkungen auf das Element mit der ID `panel-1`." Diese Information hilft Nutzern assistiver Technologien, die Struktur und Funktionsweise der Komponente besser zu verstehen.

### Zustände (States): "Wie geht es dir gerade?"

Zustände beschreiben die aktuelle Verfassung eines Elements und sind – im Gegensatz zu Eigenschaften – dazu gedacht, sich durch Nutzerinteraktion zu ändern. Sie werden fast immer mit JavaScript dynamisch angepasst. Sie beantworten die Frage: "In welchem Zustand befindest du dich im Moment?"

Typische Beispiele für Zustände sind:
*   `aria-expanded`: Ist ein einklappbarer Bereich (wie bei einem Akkordeon) gerade geöffnet (`true`) oder geschlossen (`false`)?
*   `aria-selected`: Ist ein Element in einer Gruppe (wie ein Tab in einer Tab-Leiste) gerade ausgewählt (`true`) oder nicht (`false`)?
*   `aria-hidden`: Ist ein Element aktuell für assistive Technologien versteckt (`true`) oder sichtbar (`false`)?
*   `aria-disabled`: Ist ein interaktives Element derzeit deaktiviert (`true`) oder aktiv (`false`)?
*   `aria-checked`: Ist ein Element, das eine Auswahl repräsentiert (wie eine Checkbox oder ein Radiobutton), markiert (`true`), nicht markiert (`false`) oder in einem gemischten Zustand (`mixed`)?

Schauen wir uns ein Akkordeon an. Der Button, der den Inhalt ein- und ausklappt, ändert seinen Zustand.

**Zugeklappter Zustand:**
```html
<button aria-expanded="false" aria-controls="content-1">
  Kapitel 1 öffnen
</button>
<div id="content-1" style="display: none;">
  Hier steht der Inhalt von Kapitel 1.
</div>
```
Der Screenreader verkündet hier "Kapitel 1 öffnen, Button, zugeklappt". Der Nutzer weiß sofort, dass eine Aktion hier etwas ausklappen wird.

**Aufgeklappter Zustand (nach einem Klick):**
Dein JavaScript würde den HTML-Code nun wie folgt anpassen:
```html
<button aria-expanded="true" aria-controls="content-1">
  Kapitel 1 schließen
</button>
<div id="content-1" style="display: block;">
  Hier steht der Inhalt von Kapitel 1.
</div>
```
Jetzt verkündet der Screenreader "Kapitel 1 schließen, Button, aufgeklappt". Der Zustand hat sich geändert, und diese Änderung wurde klar kommuniziert. Die `aria-expanded`-Information ist für Nutzer assistiver Technologien entscheidend, um die Funktionsweise solcher dynamischen Widgets zu verstehen.

### Das Zusammenspiel: Ein praktisches Beispiel

Die wahre Stärke von ARIA entfaltet sich, wenn Rollen, Eigenschaften und Zustände zusammenarbeiten, um eine komplexe Komponente vollständig zu beschreiben. Eine Tab-Navigation ist das perfekte Beispiel, um diesen Dreiklang in Aktion zu sehen.

Stell dir folgende Struktur vor:

```html
<!-- 1. Die Rolle für den gesamten Container -->
<ul role="tablist" aria-label="Produktinformationen">

  <!-- 2. Der erste Tab (aktiv) -->
  <li role="presentation">
    <a href="#beschreibung" role="tab" aria-controls="beschreibung" aria-selected="true">Beschreibung</a>
  </li>

  <!-- 3. Der zweite Tab (inaktiv) -->
  <li role="presentation">
    <a href="#details" role="tab" aria-controls="details" aria-selected="false" tabindex="-1">Technische Details</a>
  </li>
</ul>

<!-- 4. Der erste Tab-Inhalt (sichtbar) -->
<div id="beschreibung" role="tabpanel" tabindex="0" aria-labelledby="tab-beschreibung">
  <p>Dies ist die ausführliche Produktbeschreibung.</p>
</div>

<!-- 5. Der zweite Tab-Inhalt (versteckt) -->
<div id="details" role="tabpanel" tabindex="0" aria-labelledby="tab-details" style="display:none;">
  <ul>
    <li>Gewicht: 2kg</li>
    <li>Farbe: Schwarz</li>
  </ul>
</div>
```
Lass uns das auseinandernehmen:

*   **Rollen:**
    *   `role="tablist"`: Definiert den `<ul>`-Container als eine Liste von Tabs.
    *   `role="tab"`: Weist jedem Link die Rolle eines einzelnen Tabs zu.
    *   `role="tabpanel"`: Kennzeichnet die `<div>`-Container als die Inhaltsbereiche, die zu den Tabs gehören.
    *   `role="presentation"`: Wird auf den `<li>`-Elementen verwendet, um deren Listen-Semantik zu entfernen, da in diesem Kontext die `tab`- und `tablist`-Rollen die Struktur vorgeben.

*   **Eigenschaften:**
    *   `aria-controls`: Verbindet jeden `tab` mit seinem zugehörigen `tabpanel` über die ID. Dies ist eine stabile Beziehung.
    *   `aria-labelledby`: Verbindet jedes `tabpanel` zurück zu seinem steuernden `tab`. So weiß der Screenreader, wie der aktuell sichtbare Inhaltsbereich benannt ist. (Hinweis: Dafür müssten die `<a>`-Elemente noch IDs bekommen, z.B. `id="tab-beschreibung"`).
    *   `aria-label`: Gibt dem gesamten Widget einen aussagekräftigen Namen ("Produktinformationen").

*   **Zustände:**
    *   `aria-selected`: Dieser Zustand ist der dynamische Teil. Er ist auf `true` für den aktiven Tab und auf `false` für alle inaktiven. Wenn ein Nutzer auf einen anderen Tab klickt, würde dein JavaScript diesen Wert für die entsprechenden Elemente umschalten.
    *   `tabindex="-1"` bei inaktiven Tabs nimmt diese aus der natürlichen Tab-Reihenfolge. Die Navigation zwischen den Tabs erfolgt dann üblicherweise mit den Pfeiltasten, was ebenfalls per JavaScript implementiert werden muss.

Dieses Beispiel zeigt eindrücklich, wie Rollen die grundlegende Identität festlegen, Eigenschaften die statischen Beziehungen definieren und Zustände die dynamischen Veränderungen kommunizieren. Nur durch dieses harmonische Zusammenspiel wird aus einer Sammlung von `<div>`s und Links eine für alle Nutzer verständliche und bedienbare Komponente.
