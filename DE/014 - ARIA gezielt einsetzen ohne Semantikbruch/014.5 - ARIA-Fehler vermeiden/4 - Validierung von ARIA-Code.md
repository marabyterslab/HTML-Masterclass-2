# Validierung von ARIA-Code

### Die Validierung von ARIA-Code

Du hast gelernt, wie man mit ARIA die semantische Lücke zwischen dem, was ein sehender Benutzer wahrnimmt, und dem, was eine assistierende Technologie (AT) versteht, schließen kann. Du hast Rollen, Zustände und Eigenschaften gezielt eingesetzt, um komplexe Widgets und dynamische Inhalte zugänglich zu machen. Doch woher weißt du, dass dein ARIA-Code nicht nur gut gemeint, sondern auch gut gemacht ist?

Die Antwort liegt in der Validierung. ARIA ist unglaublich mächtig, aber auch empfindlich. Ein kleiner Tippfehler, eine falsche Eigenschaft oder eine widersprüchliche Rolle kann mehr schaden als nutzen. Statt Klarheit schaffst du Verwirrung. Statt einer Brücke baust du eine Barriere. Die Validierung deines ARIA-Codes ist daher kein optionaler letzter Schritt, sondern ein integraler Bestandteil des Entwicklungsprozesses. Es ist deine Qualitätssicherung für Barrierefreiheit.

Stell dir vor, du schreibst einen wichtigen Text. Du würdest ihn Korrektur lesen, um Rechtschreib- und Grammatikfehler zu finden. Genau das tun wir auch mit ARIA, nur dass unsere Werkzeuge nicht nur nach Tippfehlern suchen, sondern auch nach logischen Brüchen in der semantischen Struktur.

#### Der mehrstufige Ansatz der Validierung

Eine einzelne Methode reicht selten aus, um alle potenziellen ARIA-Fehler aufzudecken. Ein robuster Validierungsprozess kombiniert daher automatisierte Werkzeuge mit manueller Prüfung. Jede Stufe hat ihre eigenen Stärken und deckt unterschiedliche Arten von Fehlern ab.

**1. Statische Code-Analyse: Die erste Verteidigungslinie**

Die einfachsten Fehler sind oft die ärgerlichsten: Tippfehler. Ein `aria-lbel` statt `aria-label` oder ein `aria-expended` statt `aria-expanded` wird von assistiven Technologien einfach ignoriert. Dein sorgfältig implementiertes Feature bleibt stumm.

Hier kommt die statische Code-Analyse, auch „Linting“ genannt, ins Spiel. Moderne Code-Editoren wie Visual Studio Code bieten Erweiterungen, die deinen HTML-Code schon während des Schreibens auf die Einhaltung von ARIA-Spezifikationen überprüfen. Werkzeuge wie `ESLint` mit Plugins wie `eslint-plugin-jsx-a11y` (für React-Entwickler) oder `axe-linter` tun genau das.

Diese Tools erkennen sofort:
*   **Tippfehler in ARIA-Attributen:** Sie markieren unbekannte Attribute wie `aria-describdby`.
*   **Ungültige Werte für Attribute:** Ein `aria-hidden="maybe"` wird sofort als Fehler erkannt, da nur `"true"` oder `"false"` erlaubt sind.
*   **Fehlende, aber erforderliche Attribute:** Wenn du `role="checkbox"` verwendest, aber das notwendige Attribut `aria-checked` vergisst, wird dich ein guter Linter darauf hinweisen.
*   **Verbotene Kombinationen:** Das Anwenden einer ARIA-Rolle auf ein Element, das bereits eine starke implizite Semantik hat (z. B. `role="button"` auf einem nativen `<button>`-Element), wird als redundant oder fehlerhaft markiert.

```html
<!-- Fehler: Tippfehler im Attributnamen -->
<button aria-lbel="Einstellungen öffnen">...</button>

<!-- Fehler: Ungültiger Wert für aria-expanded -->
<button aria-expanded="open" aria-controls="menu">Menü</button>

<!-- Fehler: role="heading" auf einem <h1> ist redundant -->
<h1 role="heading" aria-level="1">Willkommen</h1>
```

Linting ist deine erste und schnellste Feedbackschleife. Es fängt die offensichtlichen Syntaxfehler ab, bevor der Code überhaupt im Browser ausgeführt wird.

**2. Automatisierte Browser-Validierung: Der Blick auf das gerenderte Ergebnis**

Dein Code existiert selten statisch. JavaScript verändert das DOM, fügt Klassen hinzu, blendet Elemente ein und aus und manipuliert ARIA-Zustände. Ein Linter, der nur den Quellcode liest, kann diese dynamischen Änderungen nicht bewerten.

Hierfür benötigst du automatisierte Werkzeuge, die direkt im Browser auf der gerenderten Seite laufen. Sie analysieren den aktuellen Zustand des DOM und prüfen die ARIA-Implementierung im Kontext der gesamten Seite.

Beliebte und äußerst nützliche Werkzeuge sind:
*   **Axe DevTools:** Eine Browser-Erweiterung für Chrome, Firefox und Edge. Sie ist der Industriestandard für automatisierte Accessibility-Tests und liefert detaillierte, verständliche Berichte über gefundene Probleme, inklusive Links zu den relevanten WCAG-Richtlinien.
*   **WAVE (Web Accessibility Evaluation Tool):** Ebenfalls eine Browser-Erweiterung, die deine Seite visuell überlagert und Fehler, Warnungen und strukturelle Informationen direkt im Kontext anzeigt.
*   **Googles Lighthouse:** In den Chrome DevTools integriert, bietet Lighthouse einen Accessibility-Audit, der viele gängige ARIA-Probleme aufdeckt.

Diese Tools sind besonders gut darin, beziehungsbezogene Fehler zu finden:
*   **Verwaiste Referenzen:** Du hast ein `aria-labelledby="title"`, aber es gibt kein Element mit `id="title"`. Die Verbindung ist gebrochen, und das Label bleibt stumm.
*   **Falsch platzierte Rollen:** Eine `role="listitem"` außerhalb einer `role="list"` ist semantischer Unsinn. Automatisierte Tools erkennen solche ungültigen Verschachtelungen.
*   **Kontrast- und Sichtbarkeitsprobleme:** Obwohl nicht direkt ein ARIA-Fehler, prüfen diese Tools oft auch, ob ein mit `aria-hidden="false"` sichtbares Element tatsächlich für sehende Benutzer sichtbar ist und ausreichenden Farbkontrast hat.

Ein typischer Fehler, den diese Tools aufdecken:

```html
<!-- Fehler: Die ID "popup-beschreibung" existiert nicht im DOM -->
<button aria-describedby="popup-beschreibung">Hilfe</button>

<!-- ... irgendwo anders auf der Seite fehlt das entsprechende Element -->
<!-- <p id="popup-beschreibung">Öffnet ein Dialogfenster mit weiteren Informationen.</p> -->
```

Automatisierte Browser-Validierung ist dein zweiter, unverzichtbarer Schritt. Sie prüft, was der Benutzer – und damit auch die assistiven Technologien – tatsächlich vorgesetzt bekommt.

**3. Manuelle Prüfung: Der menschliche Faktor**

Automatisierte Tools sind fantastisch, aber sie haben eine entscheidende Schwäche: Sie haben kein Verständnis für den Kontext oder die Benutzererfahrung. Sie können prüfen, *ob* ein ARIA-Attribut syntaktisch korrekt ist, aber nicht, *ob es die richtige Geschichte erzählt*. Man schätzt, dass automatisierte Tests nur etwa 30-50 % aller Barrierefreiheitsprobleme aufdecken.

Die manuelle Prüfung ist daher unersetzlich. Hier schlüpfst du in die Rolle des Nutzers und testest die Funktionalität mit den gleichen Werkzeugen, die Menschen mit Einschränkungen verwenden.

**a) Die Tastatur-Navigation**

Der einfachste manuelle Test, den du durchführen kannst. Lege die Maus beiseite und navigiere nur mit der Tastatur durch deine Seite.
*   **Tab-Taste:** Kannst du jedes interaktive Element (Links, Buttons, Formularfelder, benutzerdefinierte Widgets) mit der Tab-Taste erreichen?
*   **Shift + Tab:** Funktioniert die Navigation auch rückwärts?
*   **Logische Reihenfolge:** Ist die Fokus-Reihenfolge sinnvoll und nachvollziehbar, oder springt der Fokus willkürlich über die Seite?
*   **Interaktion:** Kannst du benutzerdefinierte Steuerelemente, denen du eine ARIA-Rolle wie `button` oder `menuitem` gegeben hast, mit `Enter` oder der `Leertaste` auslösen? Funktioniert die Pfeiltastennavigation in einem `role="tablist"` oder `role="radiogroup"` wie erwartet?

Ein `div` mit `role="button"` ist für einen Screenreader ein Button. Wenn dieses Element aber nicht per Tastatur fokussierbar und bedienbar ist, hast du ein Versprechen gegeben, das die Funktionalität nicht hält.

```html
<!-- Falsch: Nicht per Tastatur erreichbar oder bedienbar -->
<div role="button" onclick="doSomething()">Aktion ausführen</div>

<!-- Richtig: Fokussierbar und mit JavaScript für Tasten-Events versehen -->
<div role="button" tabindex="0" onclick="doSomething()" onkeydown="handleKeyPress(event)">
  Aktion ausführen
</div>
```

**b) Der Screenreader-Test**

Dies ist der ultimative Realitätscheck. Du hörst dir deine Webseite so an, wie es ein blinder oder sehbehinderter Nutzer tun würde. Installiere und aktiviere einen Screenreader und navigiere durch deine Implementierung. Die gängigsten sind:
*   **NVDA** (Windows, kostenlos und Open Source)
*   **JAWS** (Windows, kommerziell, aber weit verbreitet)
*   **VoiceOver** (in macOS und iOS integriert)

Schließe die Augen oder schau vom Bildschirm weg und achte darauf, was du hörst:
*   **Rolle, Name, Zustand:** Wird dein benutzerdefiniertes Widget korrekt angesagt? Hörst du bei einem Akkordeon-Element etwas wie „Bereich XY, zugeklappt, Button“, und ändert sich der Zustand zu „aufgeklappt“, wenn du es aktivierst?
*   **Dynamische Änderungen:** Wenn ein `aria-live`-Bereich aktualisiert wird (z. B. eine Fehlermeldung erscheint), wird diese Änderung vom Screenreader vorgelesen, ohne dass der Nutzer den Fokus dorthin bewegen muss?
*   **Klarheit und Prägnanz:** Ist die Ausgabe verständlich, oder ist sie zu „geschwätzig“? Manchmal kann übermäßiges ARIA zu einer Flut von Informationen führen, die mehr verwirrt als hilft.
*   **Kontext:** Verstehst du, was ein Element tut und in welchem Zusammenhang es steht, nur anhand der akustischen Ausgabe?

Die manuelle Prüfung mit Tastatur und Screenreader deckt die logischen und kontextuellen Fehler auf, die keine Maschine finden kann. Sie stellt sicher, dass deine ARIA-Implementierung nicht nur technisch korrekt ist, sondern auch eine genuinely nutzbare und verständliche Erfahrung schafft.
