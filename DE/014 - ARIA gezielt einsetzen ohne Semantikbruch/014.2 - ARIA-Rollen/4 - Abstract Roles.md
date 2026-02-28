# Abstract Roles

### Abstrakte Rollen: Die Baupläne im ARIA-Universum

Stell dir vor, du arbeitest mit einem Baukastensystem. Du hast viele spezifische Teile: rote Steine, blaue Räder, gelbe Fenster. Aber all diese Teile basieren auf übergeordneten Konzepten. Ein Rad ist eine Art von "beweglichem Teil", ein Fenster ist eine Art von "transparentem Bauelement". Diese übergeordneten Konzepte würdest du aber nie direkt verbauen. Du greifst immer zum konkreten Rad oder zum konkreten Fenster.

Genau so funktionieren abstrakte Rollen in ARIA. Sie sind die konzeptionellen Vorlagen oder Baupläne im Hintergrund, die eine Familie von verwandten, konkreten Rollen definieren. Die wichtigste Regel, die du dir von Anfang an merken musst, lautet: **Du darfst abstrakte Rollen niemals direkt in deinem HTML-Code verwenden.**

#### Warum gibt es sie dann überhaupt?

Abstrakte Rollen sind für die Spezifikation selbst da, nicht für dich als Entwickler im täglichen Einsatz. Sie dienen dazu, die ARIA-Spezifikation sauber, logisch und wiederholungsfrei (nach dem DRY-Prinzip: Don't Repeat Yourself) zu strukturieren. Sie gruppieren Eigenschaften, Zustände und Verhaltensweisen, die für eine ganze Gruppe von Elementen gelten.

Denk an sie wie an abstrakte Klassen in der objektorientierten Programmierung. Du kannst keine Instanz einer abstrakten Klasse erstellen, aber sie dient als Vorlage, von der andere, konkrete Klassen erben können. Diese konkreten Klassen bekommen dann alle Eigenschaften der abstrakten Klasse und fügen ihre eigenen, spezifischen Merkmale hinzu.

Wenn du versuchst, eine abstrakte Rolle wie `role="widget"` zu verwenden, wird ein HTML-Validator einen Fehler melden. Noch wichtiger ist, dass assistierende Technologien wie Screenreader mit dieser Information nichts anfangen können. Sie erwarten eine konkrete Rolle, um dem Nutzer eine sinnvolle Interaktion zu ermöglichen. Die Verwendung einer abstrakten Rolle führt also direkt zu einem Bruch in der Barrierefreiheit.

Schauen wir uns einige dieser unsichtbaren Vorfahren genauer an, damit du ein Gefühl dafür bekommst, wie das ARIA-System unter der Haube organisiert ist.

#### `command`

Eine `command`-Rolle repräsentiert eine Aktion, die ein Nutzer auslösen kann. Sie ist die Urmutter aller interaktiven Elemente, die eine Funktion starten oder einen Prozess in Gang setzen.

Konkrete Rollen, die von `command` erben:
*   `button`
*   `link`
*   `menuitem`

Alle diese Elemente haben etwas gemeinsam: Der Nutzer erwartet, dass eine Aktivierung (ein Klick, ein Tastendruck) eine Aktion auslöst. Diese gemeinsame Erwartungshaltung ist im abstrakten `command`-Konzept verankert.

**Falsch:**
```html
<!-- FALSCH: 'command' ist eine abstrakte Rolle und darf nicht verwendet werden. -->
<div role="command" tabindex="0">Aktion ausführen</div>
```

**Richtig:**
```html
<!-- RICHTIG: 'button' ist eine konkrete Rolle, die von 'command' erbt. -->
<div role="button" tabindex="0">Aktion ausführen</div>

<!-- Noch besser: Das native HTML-Element verwenden! -->
<button>Aktion ausführen</button>
```

#### `widget`

Die Rolle `widget` ist eine der grundlegendsten abstrakten Rollen. Sie ist der Oberbegriff für so ziemlich jedes interaktive Element einer grafischen Benutzeroberfläche (GUI). Wenn ein Element nicht primär dazu dient, die Seitenstruktur zu organisieren (wie eine Überschrift oder ein Absatz), sondern eine Form der Interaktion ermöglicht, dann ist sein Urahn wahrscheinlich die `widget`-Rolle.

Konkrete Rollen, die von `widget` erben (eine kleine Auswahl):
*   `button`
*   `checkbox`
*   `grid`
*   `link`
*   `menu`
*   `progressbar`
*   `radio`
*   `slider`
*   `tab`
*   `textbox`

Diese Liste zeigt, wie breit das Konzept von `widget` ist. Es fasst einfach alle Bausteine zusammen, aus denen du eine interaktive Anwendung oder ein komplexes Formular zusammenbaust.

#### `structure`

Die Rolle `structure` ist das Gegenstück zu `widget`. Sie ist die Basis für alle Elemente, die die Struktur einer Seite beschreiben und organisieren, aber in der Regel nicht interaktiv sind. Sie helfen assistierenden Technologien dabei, den Inhalt zu gliedern und Nutzern eine schnelle Navigation zu ermöglichen.

Konkrete Rollen, die von `structure` erben:
*   `article`
*   `figure`
*   `heading`
*   `list`
*   `note`
*   `table`
*   `toolbar`

Wenn du eine dieser Rollen verwendest, signalisierst du: "Dieser Teil der Seite dient der Organisation und dem Verständnis des Inhalts, erwarte hier keine komplexe Interaktion."

#### `section`

Die abstrakte Rolle `section` ist eine Spezialisierung von `structure`. Sie dient als Basis für größere, oft zusammenhängende Bereiche einer Seite. Ein Nutzer kann mithilfe dieser Bereiche schneller navigieren.

Konkrete Rollen, die von `section` erben:
*   `alert`
*   `article`
*   `log`
*   `status`
*   `tabpanel`

Wie du siehst, ist `article` ein Kind von `section`, was wiederum ein Kind von `structure` ist. Diese Vererbungshierarchie zeigt, wie die Konzepte immer spezifischer werden.

#### `range`

Diese abstrakte Rolle ist ein perfektes Beispiel, um die Vererbung von Eigenschaften zu demonstrieren. `range` ist die Vorlage für UI-Elemente, die einen Wert innerhalb eines bestimmten Bereichs (Minimum und Maximum) repräsentieren.

Alle Rollen, die von `range` erben, können die folgenden ARIA-Attribute nutzen:
*   `aria-valuemax`
*   `aria-valuemin`
*   `aria-valuenow`
*   `aria-valuetext`

Konkrete Rollen, die von `range` erben:
*   `progressbar`
*   `scrollbar`
*   `slider`
*   `spinbutton`

Durch die abstrakte `range`-Rolle ist sichergestellt, dass all diese Widgets ein konsistentes Set an Attributen zur Verfügung haben, um ihren Zustand zu beschreiben.

**Falsch:**
```html
<!-- FALSCH: 'range' ist abstrakt. -->
<div role="range" aria-valuemin="0" aria-valuemax="100" aria-valuenow="50"></div>
```

**Richtig:**
```html
<!-- RICHTIG: 'slider' ist eine konkrete Rolle, die von 'range' erbt. -->
<div role="slider" tabindex="0" aria-valuemin="0" aria-valuemax="100" aria-valuenow="50"></div>
```

#### `select`

Die abstrakte Rolle `select` dient als Basis für Rollen, bei denen der Nutzer eine oder mehrere Optionen aus einer Sammlung auswählen kann.

Konkrete Rollen, die von `select` erben:
*   `gridcell`
*   `option`
*   `row`
*   `tab`

All diese Rollen repräsentieren ein auswählbares Element innerhalb eines größeren Ganzen (wie einem `grid`, einer `listbox` oder einer `tablist`). Das Konzept des "Ausgewähltseins" wird durch das `aria-selected`-Attribut umgesetzt, das für diese Rollen typisch ist.

#### Warum du das wissen solltest

Du wirst abstrakte Rollen zwar nie selbst in deinem Code schreiben, aber ihr Verständnis ist entscheidend, um ein tieferes Gespür für ARIA zu entwickeln. Wenn du die Familien und Hierarchien kennst, fällt es dir leichter:

1.  **Die richtige Rolle zu wählen:** Wenn du weißt, dass `button`, `link` und `menuitem` alle von `command` abstammen, verstehst du ihre gemeinsame DNA als "Aktionsauslöser". Das hilft dir, die semantisch passendste Rolle für deinen Anwendungsfall zu finden.
2.  **Zusammenhänge zu verstehen:** Wenn du weißt, dass `slider` und `progressbar` beide von `range` erben, ist es keine Überraschung mehr, dass sie dieselben `aria-valu*`-Attribute verwenden. Du siehst das System hinter den Regeln.
3.  **Fehler zu vermeiden:** Das Wissen, dass eine Rolle abstrakt ist, schützt dich davor, sie versehentlich zu verwenden und damit die Barrierefreiheit deiner Anwendung zu beeinträchtigen.

Betrachte die abstrakten Rollen also als einen Blick hinter die Kulissen. Sie sind das Fundament, auf dem die konkreten, nutzbaren ARIA-Rollen aufgebaut sind. Indem du dieses Fundament verstehst, wirst du zu einem sichereren und kompetenteren Architekten für barrierefreie Weberlebnisse.
