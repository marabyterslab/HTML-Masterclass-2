# Validierung des neuen Codes

### Validierung des neuen Codes

Du hast die harte Arbeit des Refactorings hinter dir. Alte `<table>`-Layouts sind modernen Grid- oder Flexbox-Strukturen gewichen, unzählige `<div>`-Elemente wurden durch semantisch sinnvolle Tags wie `<article>`, `<nav>` und `<aside>` ersetzt und die gesamte HTML-Struktur fühlt sich sauberer, logischer und zukunftssicherer an. Ein gutes Gefühl, oder? Doch bevor du die Sektkorken knallen lässt, kommt der vielleicht wichtigste Schritt im gesamten Prozess: die Validierung.

Refactoring bedeutet, die interne Struktur des Codes zu verbessern, *ohne sein externes Verhalten zu ändern*. Genau das müssen wir jetzt überprüfen. Es geht nicht nur darum, ob die Seite noch „ungefähr so aussieht wie vorher“. Es geht darum, mit methodischer Präzision sicherzustellen, dass wir nichts kaputt gemacht und die beabsichtigten Verbesserungen auch wirklich erreicht haben. Dieser Prozess ist dein Sicherheitsnetz und der finale Qualitätscheck für deine Arbeit.

#### Automatisierte Werkzeuge: Dein erstes Sicherheitsnetz

Der erste und einfachste Schritt der Validierung ist der Einsatz von automatisierten Werkzeugen. Diese Tools sind unbestechlich und finden technische Fehler, die dem menschlichen Auge leicht entgehen.

##### HTML-Validierung mit dem W3C Validator

Der offizielle Validator des World Wide Web Consortiums (W3C) ist dein wichtigster Verbündeter. Er überprüft deine HTML-Datei gegen die offizielle Spezifikation und deckt gnadenlos Syntaxfehler auf. Dazu gehören zum Beispiel:

*   Falsch geschachtelte Elemente.
*   Verwaiste schließende Tags.
*   Veraltete Attribute oder Tags.
*   Fehlende Pflicht-Attribute (wie das `alt`-Attribut bei `<img>`-Tags).

Stell dir vor, du hast im Eifer des Gefechts ein Block-Element wie ein `<div>` in ein `<p>`-Element verschachtelt. Das ist in HTML nicht erlaubt.

**Alter, invalider Code:**

```html
<p>
  Dies ist ein Absatz mit wichtigen Informationen.
  <div>Achtung: Sonderhinweis!</div>
  Der Absatz geht hier weiter.
</p>
```

Der W3C Validator würde hier sofort einen Fehler melden: „Error: Element `div` not allowed as child of element `p` in this context.“

Nach deinem Refactoring sollte der Code semantisch korrekt und valide sein, zum Beispiel so:

**Neuer, valider Code:**

```html
<p>Dies ist ein Absatz mit wichtigen Informationen.</p>
<div class="hinweis">
  <p><strong>Achtung:</strong> Sonderhinweis!</p>
</div>
<p>Der Absatz geht hier weiter.</p>
```

Die Validierung deines Codes über den W3C Validator (oder integrierte Tools in deiner Entwicklungsumgebung) ist keine Option, sondern eine Pflicht. Eine fehlerfreie Validierung ist die Basis für alles Weitere, denn sie garantiert, dass Browser deine Seite auf einer standardkonformen Grundlage interpretieren können.

##### CSS-Validierung und JavaScript-Linting

Auch wenn unser Fokus auf HTML liegt, solltest du nicht vergessen, dass Änderungen an der HTML-Struktur oft Anpassungen in CSS und JavaScript erfordern. Ein Refactoring von Klassen- und ID-Namen kann dazu führen, dass CSS-Selektoren oder JavaScript-DOM-Manipulationen ins Leere laufen.

*   **CSS-Validierung:** Auch hierfür gibt es einen W3C-Validator. Er prüft, ob du gültige Eigenschaften und Werte verwendest. Das ist besonders nützlich, um Tippfehler (`pading` statt `padding`) oder vergessene Semikolons zu finden.
*   **JavaScript-Linting:** Werkzeuge wie ESLint analysieren deinen JavaScript-Code auf potenzielle Fehler, Stilprobleme und logische Inkonsistenzen. Ein Linter würde dich zum Beispiel warnen, wenn du versuchst, auf ein Element mit einer ID zuzugreifen, die du beim Refactoring entfernt oder umbenannt hast.

#### Manuelle Überprüfung: Das menschliche Auge

Automatisierte Tools sind fantastisch für die technische Korrektheit, aber sie können nicht beurteilen, wie eine Seite aussieht, sich anfühlt oder bedienen lässt. Hier kommst du ins Spiel.

##### Visuelles Cross-Browser-Testing

Eine der größten Gefahren beim Refactoring ist, dass die Seite in deinem primären Entwicklungsbrowser (oft Chrome) perfekt aussieht, aber in Firefox, Safari oder Edge völlig anders dargestellt wird. Jede Browser-Engine hat ihre kleinen Eigenheiten bei der Interpretation von HTML und CSS.

Öffne deine refaktorierte Seite in den aktuellsten Versionen der wichtigsten Browser:

*   Google Chrome (Blink-Engine)
*   Mozilla Firefox (Gecko-Engine)
*   Apple Safari (WebKit-Engine)
*   Microsoft Edge (Blink-Engine, aber dennoch wichtig zu testen)

Vergleiche die Darstellung Pixel für Pixel mit einem Screenshot oder der Live-Version der alten Seite. Achte besonders auf Abstände, Schriftgrößen, Zeilenumbrüche und die Positionierung von Elementen. Oft sind es Kleinigkeiten, wie eine leicht unterschiedliche Handhabung von `flex-gap` oder die Interpretation von komplexen Grid-Layouts, die zu Abweichungen führen.

##### Testen des responsiven Verhaltens

Legacy-Code basiert oft auf starren Breiten oder umständlichen `float`-Konstruktionen. Dein modernes, refaktorieretes Layout mit Flexbox oder Grid sollte sich auf verschiedenen Bildschirmgrößen deutlich besser verhalten. Überprüfe das!

Nutze die Entwicklerwerkzeuge deines Browsers (meist über F12 oder Rechtsklick -> Untersuchen erreichbar), um den „Device Mode“ zu aktivieren. Simuliere damit verschiedene Viewports:

*   Ein großes Desktop-Display.
*   Ein typisches Laptop-Display (z. B. 1366px Breite).
*   Ein Tablet im Hoch- und Querformat (z. B. 768px und 1024px).
*   Ein Smartphone im Hoch- und Querformat (z. B. 375px und 667px).

Ziehe die Breite des Browserfensters langsam von groß nach klein und beobachte, wie sich dein Layout anpasst. Funktionieren die von dir definierten Breakpoints? Brechen Texte unschön um? Überlappen sich Elemente? Gerade hier zeigt sich die wahre Stärke deines Refactorings – oder eben dessen Schwächen.

##### Funktionale Tests: Klickt sich alles wie gewohnt?

Eine Webseite ist kein statisches Bild. Sie hat interaktive Elemente. Klicke jeden einzelnen Link, jede Schaltfläche und jedes Menü an. Fülle Testdaten in Formulare ein und schicke sie ab. Öffne und schließe jedes Akkordeon-Element.

Deine Aufgabe ist es, zu bestätigen, dass jede Funktionalität, die vor dem Refactoring vorhanden war, immer noch exakt so funktioniert. Hast du vielleicht eine `id` umbenannt, die von einem JavaScript-Event-Listener verwendet wurde? Oder hast du einen `<button>` durch einen `<a>`-Tag ersetzt und vergessen, das Klick-Event neu zuzuordnen? Solche Fehler sind typische Nebenwirkungen und müssen systematisch aufgespürt werden.

#### Die Königsdisziplin: Semantik und Barrierefreiheit

Du hast den Code nicht nur refaktorieret, damit er technisch valide ist, sondern damit er *besser* wird. Besser bedeutet in diesem Kontext vor allem semantisch korrekter und damit zugänglicher (barrierefrei).

##### Prüfung der Barrierefreiheit (Accessibility, a11y)

Moderne semantische Tags sind der Schlüssel zu einer barrierefreien Webseite. Sie geben assistiven Technologien wie Screenreadern den nötigen Kontext, um den Inhalt korrekt zu interpretieren.

**1. Der Keyboard-Navigationstest:**
Lege deine Maus beiseite. Versuche, die gesamte Seite nur mit der Tastatur zu bedienen. Drücke wiederholt die `Tab`-Taste. Springt der Fokus von einem interaktiven Element (Link, Button, Formularfeld) zum nächsten? Ist die Reihenfolge logisch und nachvollziehbar? Ein sichtbarer Fokus-Indikator (oft ein blauer Rahmen) muss jederzeit klar erkennbar sein. Durch das Refactoring kann sich die DOM-Reihenfolge ändern, was die Tab-Reihenfolge durcheinanderbringen kann.

**2. Überprüfung der Überschriftenstruktur:**
Eine der häufigsten Aufgaben beim Refactoring ist die Korrektur der Überschriftenhierarchie. Es darf nur eine `<h1>` pro Seite geben, und die Hierarchie (`<h2>` folgt auf `<h1>`, `<h3>` auf `<h2>` usw.) muss logisch sein. Es dürfen keine Ebenen übersprungen werden. Nutze die Entwicklerwerkzeuge oder eine Browser-Erweiterung (z. B. "HeadingsMap"), um die Gliederung deiner Seite zu visualisieren. Sie sollte einem logischen Inhaltsverzeichnis entsprechen.

**3. Automatisierte Accessibility-Checks:**
Tools wie Lighthouse (in Chrome DevTools integriert) oder die Axe DevTools (als Browser-Erweiterung) können deine Seite automatisch auf häufige Barrierefreiheitsprobleme scannen. Sie prüfen zum Beispiel:

*   Farbkontraste: Ist der Text gut lesbar?
*   Fehlende `alt`-Texte bei Bildern.
*   Korrekte Beschriftung von Formularfeldern (`<label>`).
*   Verwendung von ARIA-Attributen (falls nötig).

Ein Lighthouse-Score von 100 im Bereich „Accessibility“ ist ein hervorragendes Ziel und ein starkes Indiz für ein erfolgreiches Refactoring.

##### Ein praktischer Workflow für die Validierung

Um den Überblick nicht zu verlieren, kannst du dich an diesem schrittweisen Prozess orientieren:

1.  **Technische Sauberkeit:** Lasse den HTML-Code durch den W3C Validator laufen. Korrigiere alle Fehler.
2.  **Automatisierter Qualitätscheck:** Führe einen Lighthouse-Audit durch. Konzentriere dich vor allem auf die Bereiche „Performance“, „Accessibility“ und „SEO“, da diese direkt von einer sauberen HTML-Struktur beeinflusst werden.
3.  **Visueller Check (Desktop):** Öffne die alte und neue Seite nebeneinander in den wichtigsten Browsern. Suche nach visuellen Abweichungen.
4.  **Responsive Check:** Nutze den Device Mode der DevTools und überprüfe das Layout an allen wichtigen Breakpoints.
5.  **Funktionaler Klick-Test:** Bediene alle interaktiven Elemente auf der Seite.
6.  **Keyboard-Test:** Navigiere die gesamte Seite nur mit der `Tab`-Taste.
7.  **Semantik-Check:** Überprüfe die Überschriftenstruktur und die logische Gliederung des Inhalts.

Dieser gründliche Validierungsprozess mag zeitaufwendig erscheinen, aber er ist der entscheidende Unterschied zwischen einem gut gemeinten und einem wirklich gut gemachten Refactoring. Er gibt dir das Vertrauen, dass dein neuer, moderner Code nicht nur sauberer, sondern in jeder Hinsicht besser ist als der alte.
