# Wichtige Plugins und Erweiterungen

### 2.3 Wichtige Plugins und Erweiterungen

Ein moderner Code-Editor wie Visual Studio Code ist von Haus aus bereits ein mächtiges Werkzeug. Seine wahre Stärke entfaltet er aber erst durch die schier unendliche Vielfalt an Erweiterungen, auch Plugins oder Extensions genannt. Stell dir deinen Editor wie eine gut ausgestattete Werkstatt vor. Die Grundausstattung ist da, aber für spezielle Aufgaben brauchst du spezielle Werkzeuge. Diese Erweiterungen sind genau das: Spezialwerkzeuge, die deinen Arbeitsablauf beschleunigen, Fehler reduzieren und dir letztlich das Leben als Entwickler einfacher machen.

Die Installation ist denkbar einfach: In der Aktivitätsleiste deines Editors (meist am linken Rand) findest du ein Symbol für Erweiterungen (oft vier Quadrate, eines davon abgesetzt). Dort kannst du nach den hier vorgestellten Namen suchen und sie mit einem Klick installieren. Die folgenden Vorschläge sind eine Auswahl der beliebtesten und nützlichsten Erweiterungen für die Webentwicklung, insbesondere wenn du mit HTML, CSS und JavaScript arbeitest.

#### Code-Qualität und konsistente Formatierung

Eines der ersten Dinge, die du dir angewöhnen solltest, ist, sauberen und konsistent formatierten Code zu schreiben. Das hilft nicht nur dir, den Überblick zu behalten, sondern ist auch unerlässlich, wenn du später einmal mit anderen im Team arbeitest.

**Prettier - Code formatter**

Prettier ist der De-facto-Standard, wenn es um Code-Formatierung geht. Es ist ein sogenannter "opinionated" Code-Formatter. Das bedeutet, es nimmt dir die meisten Entscheidungen über das Aussehen deines Codes ab und wendet ein einheitliches Regelwerk an. Soll ein Einzug mit zwei oder vier Leerzeichen erfolgen? Kommt das schließende `>` einer langen Tag-Zeile in eine neue Zeile? Solche Fragen musst du dir nicht mehr stellen.

Sobald Prettier installiert und konfiguriert ist (du kannst es zum Beispiel so einstellen, dass es bei jedem Speichern automatisch ausgeführt wird), formatiert es deinen Code.

Ein unformatierter HTML-Schnipsel könnte so aussehen:

```html
<div class="container"  id="main"  ><p>Dies ist ein sehr langer Satz in einem schlecht formatierten Absatz, der schwer zu lesen ist.</p><ul><li>Punkt 1</li><li   >Punkt 2</li></ul></div>
```

Nachdem Prettier seine Arbeit getan hat, sieht derselbe Code so aus:

```html
<div class="container" id="main">
  <p>
    Dies ist ein sehr langer Satz in einem schlecht formatierten Absatz, der
    schwer zu lesen ist.
  </p>
  <ul>
    <li>Punkt 1</li>
    <li>Punkt 2</li>
  </ul>
</div>
```

Der Unterschied ist wie Tag und Nacht. Der Code ist sofort lesbar und strukturiert. Das erspart dir manuelle Arbeit und beugt langen Diskussionen im Team über den "richtigen" Formatierungsstil vor.

#### Produktivität und schnellere Code-Erstellung

Diese Erweiterungen sind darauf ausgelegt, dir Tipparbeit abzunehmen und häufig wiederkehrende Aufgaben zu automatisieren.

**Auto Rename Tag**

Eine kleine, aber unglaublich nützliche Erweiterung. Wenn du ein öffnendes HTML-Tag änderst, zum Beispiel von `<div>` zu `<section>`, ändert diese Erweiterung automatisch das zugehörige schließende Tag `</div>` zu `</section>`. Das klingt nach einer Kleinigkeit, aber es spart im Alltag eine Menge Zeit und verhindert Flüchtigkeitsfehler, bei denen die Tags nicht mehr zusammenpassen, was zu schwer auffindbaren Anzeigefehlern im Browser führen kann.

**Path Intellisense**

In HTML musst du ständig auf andere Dateien verweisen: auf CSS-Dateien, Bilder, JavaScript-Dateien oder andere HTML-Seiten. Dabei den richtigen Pfad zu tippen, kann fehleranfällig sein. Ein Punkt zu viel (`../`) oder ein Schrägstrich vergessen, und schon wird die Ressource nicht gefunden. Path Intellisense hilft dir, indem es die Pfade automatisch vervollständigt, während du tippst. Sobald du `src="` oder `href="` schreibst, schlägt es dir die verfügbaren Dateien und Ordner vor.

```html
<!-- Ohne Erweiterung musst du den Pfad manuell und fehlerfrei tippen -->
<img src="assets/images/header-logo.png" alt="Logo">

<!-- Mit Path Intellisense bekommst du Vorschläge, sobald du "assets/" tippst -->
<img src="assets/images/header-logo.png" alt="Logo">
```

**HTML CSS Support**

Diese Erweiterung ist eine große Hilfe, wenn du mit CSS-Klassen arbeitest. Sie scannt dein Projekt nach CSS-Dateien und bietet dir dann eine Autovervollständigung für Klassennamen und IDs direkt in deinen HTML-Dateien an. Wenn du `class="` in ein Tag schreibst, schlägt sie dir alle in deinem Projekt definierten CSS-Klassen vor. Das verhindert Tippfehler bei Klassennamen – ein sehr häufiger Grund, warum CSS-Regeln nicht wie erwartet angewendet werden.

#### Live-Vorschau und Entwicklungsserver

Früher war der Arbeitsablauf oft so: Du schreibst Code, speicherst die Datei, wechselst zum Browser und drückst die F5-Taste, um die Seite neu zu laden und deine Änderungen zu sehen. Das ist umständlich und unterbricht den kreativen Fluss.

**Live Server**

Live Server revolutioniert diesen Prozess. Nach der Installation kannst du mit einem Rechtsklick auf deine HTML-Datei einen lokalen Entwicklungsserver starten. Dein Browser öffnet sich und zeigt die Seite an. Das Besondere daran: Jedes Mal, wenn du nun deine HTML-, CSS- oder JavaScript-Datei speicherst, lädt die Erweiterung die Seite im Browser automatisch neu. Du siehst deine Änderungen also sofort, ohne den Editor verlassen oder manuell aktualisieren zu müssen. Das beschleunigt die Entwicklung enorm und fühlt sich an, als würdest du direkt im Browser gestalten.

#### Integration mit Versionskontrolle

Auch wenn du gerade erst anfängst, ist es eine gute Idee, dich früh mit Versionskontrolle, insbesondere mit Git, vertraut zu machen.

**GitLens — Git supercharged**

Dein Editor hat bereits eine grundlegende Git-Integration, aber GitLens hebt diese auf ein neues Level. Es blendet direkt im Code nützliche Informationen ein. Du kannst zum Beispiel an jeder einzelnen Zeile sehen, wer sie wann zuletzt geändert hat (die sogenannte "Git Blame"-Information). Du kannst dir die Historie einer Datei ansehen, Änderungen zwischen verschiedenen Versionen vergleichen und vieles mehr – alles, ohne den Editor verlassen zu müssen. Für die Zusammenarbeit im Team ist das unverzichtbar, aber auch für eigene Projekte ist es extrem hilfreich, um Änderungen nachvollziehen zu können.

#### Visuelle Helfer und Personalisierung

Nicht alle Erweiterungen dienen direkt der Code-Erstellung. Einige verbessern einfach die visuelle Darstellung und die Organisation, was sich aber ebenfalls positiv auf deine Produktivität auswirkt.

**Material Icon Theme**

Diese Erweiterung ersetzt die Standard-Dateisymbole im Datei-Explorer deines Editors durch spezifische, gut unterscheidbare Icons für verschiedene Dateitypen. Eine `.html`-Datei bekommt ein HTML5-Logo, eine `.css`-Datei ein CSS3-Logo, ein Ordner namens `js` ein JavaScript-Logo und so weiter. Das macht die Navigation in deiner Projektstruktur auf einen Blick deutlich übersichtlicher und angenehmer für die Augen.

**TODO Highlight**

Als Entwickler hinterlässt du dir oft Notizen direkt im Code, zum Beispiel mit `// TODO: Hier muss noch der Text angepasst werden`. Diese Kommentare können im Code leicht untergehen. TODO Highlight hebt solche Schlüsselwörter (`TODO`, `FIXME` etc.) farblich hervor, sodass sie sofort ins Auge springen. Es kann dir sogar eine Liste aller offenen To-dos in deinem Projekt anzeigen.

Diese Liste ist nur der Anfang. Das Ökosystem der Erweiterungen ist riesig. Der beste Weg, neue nützliche Helfer zu finden, ist, deinen eigenen Arbeitsablauf zu beobachten. Immer wenn du merkst, dass du eine bestimmte Aufgabe ständig wiederholst oder dich über einen umständlichen Prozess ärgerst, ist die Wahrscheinlichkeit hoch, dass jemand bereits eine Erweiterung dafür entwickelt hat. Experimentiere, probiere verschiedene Plugins aus und stelle dir so nach und nach deinen perfekt auf dich zugeschnittenen Werkzeugkasten zusammen.
