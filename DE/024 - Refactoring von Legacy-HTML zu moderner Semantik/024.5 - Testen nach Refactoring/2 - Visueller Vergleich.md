# Visueller Vergleich

### Visueller Vergleich: Das Auge testet mit

Stell dir vor, du hast stundenlang daran gearbeitet, eine alte, mit `<div>`-Elementen überladene Webseite in eine saubere, semantische HTML-Struktur zu überführen. Die `<div>`s sind jetzt `<main>`, `<article>`, `<section>` und `<aside>`. Alles ist logisch, zugänglich und für Suchmaschinen optimiert. Du bist stolz auf deine Arbeit. Aber als du die neue Version im Browser lädst, stockt dir der Atem: Das Layout ist komplett zerschossen. Überschriften haben die falsche Größe, Bilder kleben am falschen Rand und die Navigation ist nicht mehr wiederzuerkennen.

Was ist passiert? Dein Refactoring war technisch korrekt, aber du hast die enge, oft zerbrechliche Verbindung zwischen der alten HTML-Struktur und dem CSS, das auf sie abzielte, unterschätzt. Ein CSS-Selektor wie `div.main-content > div.article-header > div.title` funktioniert eben nicht mehr, wenn die Struktur jetzt `<main><article><header><h1>` lautet.

Genau hier kommt der visuelle Vergleich ins Spiel. Er ist dein Sicherheitsnetz beim Refactoring. Das Ziel eines semantischen Refactorings ist es meistens, die Struktur unter der Haube zu verbessern, *ohne das visuelle Erscheinungsbild zu verändern*. Der visuelle Vergleich ist die Methode, mit der du genau das überprüfst. Er stellt sicher, dass für den Endbenutzer alles genau so aussieht wie vor deiner Änderung.

#### Die manuelle Methode: Zwei Fenster und scharfe Augen

Die einfachste und direkteste Form des visuellen Vergleichs ist der manuelle Abgleich. Der Ablauf ist denkbar simpel:

1.  Öffne die ursprüngliche Version der Webseite (die "Legacy"-Version) in einem Browserfenster.
2.  Öffne deine refaktorierte Version in einem zweiten Browserfenster direkt daneben.
3.  Passe die Fenstergrößen so an, dass sie identisch sind.
4.  Scrolle auf beiden Seiten zu denselben Stellen und vergleiche mit bloßem Auge, ob alles gleich aussieht.

Achte dabei auf typische Fehlerquellen:
*   **Layout und Abstände:** Sind Elemente verrutscht? Haben sich `margin` oder `padding` verändert?
*   **Typografie:** Stimmen Schriftart, Schriftgröße, Zeilenhöhe und Farbe noch?
*   **Farben:** Haben Hintergründe, Texte oder Rahmen die korrekten Farbwerte?
*   **Bilder und Medien:** Werden alle Bilder korrekt geladen und skaliert?
*   **Interaktive Elemente:** Sehen Buttons, Formularfelder und Links noch so aus wie vorher?

Diese Methode ist schnell und erfordert keinerlei Werkzeuge. Für eine einzelne, einfache Seite mag das ausreichen. Doch sie hat gravierende Nachteile: Sie ist extrem fehleranfällig. Das menschliche Auge übersieht leicht winzige Abweichungen von ein paar Pixeln, einen leicht veränderten Farbton oder eine minimale Anpassung der Schriftstärke. Außerdem ist dieser Prozess mühsam und skaliert überhaupt nicht. Wenn du eine Webseite mit Dutzenden oder gar Hunderten von Unterseiten refaktorierst, ist ein manueller Vergleich schlichtweg unmöglich.

Ganz wichtig ist hierbei auch das responsive Design. Du müsstest diesen Vergleich für verschiedene Viewport-Größen wiederholen – für ein typisches Smartphone, ein Tablet und einen Desktop-Monitor. Was auf dem Desktop perfekt aussieht, kann auf dem Handy komplett zerbrochen sein.

#### Screenshot-basiertes Testen: Der erste Schritt zur Automatisierung

Eine Verbesserung gegenüber dem reinen Augenvergleich ist das Anfertigen von Screenshots. Du erstellst einen Screenshot der alten Version und einen der neuen Version und legst sie in einem Bildbearbeitungsprogramm übereinander. Indem du die obere Ebene transparent schaltest oder zwischen den Ebenen hin- und herschaltest, werden Unterschiede viel deutlicher sichtbar.

Browser-Entwicklertools bieten oft eine Funktion, um Screenshots von der gesamten Seite ("Full Page Screenshot") zu machen, nicht nur vom sichtbaren Bereich. Das ist besonders nützlich für lange Seiten.

Auch hier bleibt das Problem der Skalierbarkeit und des manuellen Aufwands. Aber du hast zumindest eine reproduzierbare Grundlage, die du auch Kollegen zeigen kannst. Dieser Ansatz ist ein guter Mittelweg, wenn du keine komplexen Werkzeuge einrichten möchtest, aber dennoch eine höhere Genauigkeit als beim reinen Blickvergleich anstrebst.

#### Professionelle Werkzeuge: Die visuelle Regressionstestung

Wenn du Refactoring ernsthaft und in größerem Stil betreibst, kommst du um automatisierte Werkzeuge nicht herum. In der Fachwelt spricht man hier von **visueller Regressionstestung** (Visual Regression Testing) oder **Snapshot Testing**.

Die Grundidee dieser Werkzeuge ist immer dieselbe:

1.  **Baseline erstellen:** Das Werkzeug erstellt einen "Golden Master" oder eine "Baseline". Das ist ein Satz von Referenz-Screenshots der ursprünglichen, funktionierenden Webseite in verschiedenen Viewports. Dieser Zustand wird als korrekt und erwünscht definiert.
2.  **Änderungen durchführen:** Du nimmst dein Refactoring vor.
3.  **Vergleichs-Screenshots erstellen:** Nach deinen Änderungen führst du das Test-Tool erneut aus. Es erstellt nun einen neuen Satz von Screenshots von der refaktorieren Seite unter exakt denselben Bedingungen (gleiche Browser-Engine, gleiche Viewport-Größe).
4.  **Differenzanalyse:** Das Herzstück des Tools ist der Pixel-für-Pixel-Vergleich zwischen den Baseline-Screenshots und den neuen Screenshots. Findet es Unterschiede, generiert es ein "Diff"-Bild. Dieses Bild hebt alle abweichenden Pixel farblich hervor, sodass du auf einen Blick siehst, wo genau sich etwas verändert hat.
5.  **Bewertung:** Du siehst dir die Diff-Bilder an.
    *   Handelt es sich um einen **unerwünschten Fehler** (eine Regression), gehst du zurück in deinen Code und behebst das Problem.
    *   Handelt es sich um eine **erwünschte Änderung** (z.B. weil du im Zuge des Refactorings auch ein kleines Design-Update vorgenommen hast), akzeptierst du den neuen Screenshot. Er wird damit zur neuen Baseline für zukünftige Tests.

Ein konkretes Beispiel macht das klarer. Nehmen wir an, dein alter HTML-Code sah so aus:

```html
<!-- Vorher: Legacy-HTML -->
<div class="product-card">
  <div class="product-image-wrapper">
    <img src="schuhe.jpg" alt="Bequeme Laufschuhe">
  </div>
  <div class="product-title">Tolle Laufschuhe</div>
  <div class="product-description">
    Diese Schuhe sind super.
  </div>
</div>
```

Dein refaktorierter Code nutzt semantische Tags:

```html
<!-- Nachher: Modernes, semantisches HTML -->
<figure class="product-card">
  <img src="schuhe.jpg" alt="Bequeme Laufschuhe">
  <figcaption>
    <h2>Tolle Laufschuhe</h2>
    <p>Diese Schuhe sind super.</p>
  </figcaption>
</figure>
```

Dein altes CSS hatte vielleicht eine Regel wie `div.product-title { font-size: 1.5rem; }`. Diese Regel greift bei der neuen `<h2>` nicht mehr. Ein visuelles Regressionstest-Tool würde sofort einen Unterschied in der Schriftgröße des Titels feststellen und ihn dir als Diff anzeigen. Du wüsstest sofort, dass du deine CSS-Selektoren an die neue HTML-Struktur anpassen musst, zum Beispiel zu `figure.product-card h2 { font-size: 1.5rem; }`.

Beliebte Werkzeuge in diesem Bereich sind **BackstopJS**, **Percy**, oder die Snapshot-Testing-Funktionen, die in modernen Test-Frameworks wie **Playwright** oder **Cypress** (oft über Plugins) integriert sind. Die Einrichtung erfordert zwar etwas Einarbeit, aber der Gewinn an Sicherheit und Geschwindigkeit ist bei größeren Projekten enorm.

#### Typische Herausforderungen und wie du sie meisterst

Automatisierte visuelle Tests sind mächtig, aber nicht frei von Tücken. Es gibt einige klassische Probleme, auf die du stoßen wirst:

*   **Dynamische Inhalte:** Was passiert, wenn deine Seite Inhalte anzeigt, die sich bei jedem Aufruf ändern? Eine News-Seite mit den "neuesten Artikeln", eine Werbeanzeige oder ein einfacher Zeitstempel ("Stand: 14:32 Uhr") würden bei jedem Testlauf zu einem Fehler führen. Die Lösung der Tools ist hier das "Maskieren". Du kannst bestimmte Bereiche der Seite definieren, die beim Pixelvergleich ignoriert werden sollen.

*   **Font-Rendering und Anti-Aliasing:** Wie Schriften auf dem Bildschirm geglättet werden (Anti-Aliasing), kann sich minimal zwischen verschiedenen Betriebssystemen oder sogar Browser-Versionen unterscheiden. Das kann zu Fehlalarmen führen, weil ein paar Pixel an den Rändern von Buchstaben abweichen. Gute Tools bieten einen "Threshold" (Toleranzwert), mit dem du festlegen kannst, wie viele Pixel abweichen dürfen, bevor ein Test als fehlgeschlagen gilt. Oft ist es auch am besten, die Tests immer in einer kontrollierten Umgebung laufen zu lassen, zum Beispiel in einem Docker-Container, um die Konsistenz zu gewährleisten.

*   **Animationen und Übergänge:** Wenn ein Element beim Laden der Seite eine Animation ausführt (z.B. ein "Fade-in"), hängt das Ergebnis des Screenshots vom exakten Zeitpunkt der Aufnahme ab. Das führt fast garantiert zu inkonsistenten Ergebnissen. Die gängige Praxis ist, alle CSS-Animationen und -Transitions für die Dauer des Testlaufs global zu deaktivieren. Das geht oft mit einer einfachen CSS-Regel:

    ```css
    /* Dieses CSS nur während des visuellen Tests laden */
    *, *::before, *::after {
       animation-delay: -1ms !important;
       animation-duration: 1ms !important;
       animation-iteration-count: 1 !important;
       transition-duration: 1ms !important;
       transition-delay: -1ms !important;
       scroll-behavior: auto !important;
    }
    ```

Der visuelle Vergleich, von der einfachen manuellen Methode bis hin zur vollautomatisierten Regressionstestung, ist ein unverzichtbarer Teil des Refactoring-Prozesses. Er gibt dir das Vertrauen, mutige strukturelle Änderungen vorzunehmen, in dem Wissen, dass du die Benutzeroberfläche, das, was der Nutzer tatsächlich sieht und erlebt, nicht versehentlich zerstörst. Er ist die Brücke zwischen technisch sauberem Code und einem visuell perfekten Ergebnis.
