# Regressions-Tests

### Regressions-Tests: Dein Sicherheitsnetz beim Refactoring

Stell dir vor, du hast stunden- oder sogar tagelang daran gearbeitet, eine alte, mit Tabellen-Layouts überladene HTML-Seite in eine moderne, semantische Struktur zu überführen. Die alten `<table>`-Elemente sind verschwunden, ersetzt durch saubere `<main>`, `<article>`, `<aside>` und `<nav>`-Tags. Alles sieht auf den ersten Blick wunderbar aus. Du bist stolz auf deine Arbeit. Doch dann schleicht sich ein beunruhigender Gedanke ein: Funktioniert noch alles wie vorher? Was, wenn du durch die Änderung der HTML-Struktur unbemerkt das Styling zerschossen oder eine wichtige JavaScript-Funktion lahmgelegt hast?

Genau hier kommen Regressionstests ins Spiel. Der Begriff „Regression“ bedeutet in der Softwareentwicklung ein Rückfall – ein Fehler, der auftritt, weil eine vormals funktionierende Funktionalität durch eine Änderung plötzlich nicht mehr funktioniert. Ein Regressionstest ist also nichts anderes als ein gezielter Test, um sicherzustellen, dass deine jüngsten Änderungen keine alten, etablierten Funktionen kaputt gemacht haben. Er ist dein Sicherheitsnetz, das dich auffängt, bevor ein Fehler den Endnutzer erreicht.

#### Warum Refactoring ohne Tests einem Blindflug gleicht

Beim Refactoring von Legacy-HTML zu moderner Semantik veränderst du das tiefste Fundament deiner Webseite. Du tauschst das Skelett aus. Selbst wenn du nur HTML-Tags änderst und die Inhalte gleich lässt, sind die potenziellen Bruchstellen vielfältig und oft nicht sofort ersichtlich:

1.  **CSS-Selektoren greifen ins Leere:** Dein altes CSS war möglicherweise stark an die verschachtelte Tabellenstruktur gebunden. Ein Selektor wie `body > table > tr > td.sidebar a` wird nach deinem Refactoring nicht mehr funktionieren, wenn der Link nun in `<aside> <nav> <ul> <li> <a href="...">` liegt. Die Folge: Links sind nicht mehr gestylt, Layouts brechen zusammen und Elemente verschwinden oder überlappen.

2.  **JavaScript verliert den Halt:** Viele ältere JavaScript-Codeschnipsel navigieren durch den DOM (Document Object Model) auf eine sehr starre Weise. Ein Skript, das auf `document.getElementById('main_content_table').rows[3]` zugreift, wird einen Fehler werfen, wenn das Element `main_content_table` nicht mehr existiert. Interaktive Elemente wie aufklappbare Menüs, Formularvalidierungen oder Bildergalerien können dadurch auf einen Schlag unbrauchbar werden.

3.  **Barrierefreiheit leidet:** Obwohl dein Ziel die Verbesserung der Semantik und damit der Barrierefreiheit ist, kannst du versehentlich das Gegenteil erreichen. Vielleicht hast du ein Element entfernt, das ein wichtiges `aria`-Attribut trug, oder die logische Reihenfolge für Screenreader durch eine neue DOM-Struktur durcheinandergebracht.

4.  **SEO-Relevanz geht verloren:** Die Hierarchie von Überschriften (`<h1>` bis `<h6>`) ist ein wichtiger Faktor für Suchmaschinen. Wenn du beim Refactoring die Überschriftenebenen versehentlich änderst oder wichtige Schlüsselwörter in weniger relevanten Tags platzierst, kann dies negative Auswirkungen auf das Ranking deiner Seite haben.

Ohne einen systematischen Testprozess stocherst du im Nebel. Du korrigierst vielleicht einen Fehler, den du siehst, übersiehst aber drei andere, die sich erst unter bestimmten Umständen zeigen. Regressionstests geben dir die Sicherheit, dass das Fundament, auf dem du baust, nach deinen Umbauten immer noch stabil ist.

#### Manuelle vs. Automatisierte Regressionstests

Es gibt grundsätzlich zwei Ansätze, um Regressionen aufzuspüren: den manuellen und den automatisierten Weg. Beide haben ihre Berechtigung und werden in der Praxis oft kombiniert.

##### Der manuelle Ansatz: Die Checkliste

Manuelle Regressionstests sind genau das, wonach sie klingen: Du oder ein Kollege klickt sich systematisch durch die Webseite und überprüft, ob alles noch so aussieht und funktioniert wie erwartet. Der Schlüssel zum Erfolg liegt hier in der Systematik. Anstatt ziellos herumzuklicken, erstellst du einen Testplan – eine einfache Checkliste mit den wichtigsten Funktionen und Ansichten deiner Seite.

Ein solcher Plan für unser Refactoring-Szenario könnte so aussehen:

*   **Visuelle Überprüfung der Startseite:**
    *   [ ] Wird das Logo korrekt angezeigt?
    *   [ ] Ist die Hauptnavigation sichtbar und korrekt formatiert?
    *   [ ] Wird der Hauptinhalt im richtigen Layout dargestellt?
    *   [ ] Ist der Footer am unteren Rand der Seite positioniert?

*   **Funktionale Überprüfung der Navigation:**
    *   [ ] Führt ein Klick auf "Produkte" zur Produktseite?
    *   [ ] Führt ein Klick auf "Kontakt" zur Kontaktseite?
    *   [ ] Funktioniert der "Zurück nach oben"-Button im Footer?

*   **Überprüfung des Kontaktformulars:**
    *   [ ] Werden alle Formularfelder korrekt angezeigt?
    *   [ ] Zeigt die Validierung eine Fehlermeldung bei falscher E-Mail-Eingabe?
    *   [ ] Wird das Formular nach dem Absenden erfolgreich geleert und eine Erfolgsmeldung angezeigt?

**Vorteile:**
*   Keine speziellen Werkzeuge oder Programmierkenntnisse erforderlich.
*   Sehr gut geeignet, um subjektive Aspekte wie das Look-and-Feel und die Benutzerfreundlichkeit zu beurteilen.
*   Flexibel und schnell für kleine Projekte oder einmalige Änderungen.

**Nachteile:**
*   Extrem zeitaufwendig bei größeren Webseiten.
*   Anfällig für menschliche Fehler. Man wird müde, übersieht Kleinigkeiten oder vergisst Testfälle.
*   Nicht skalierbar. Bei jedem Refactoring den gesamten Testplan manuell abzuarbeiten, ist frustrierend und ineffizient.

##### Der automatisierte Ansatz: Der Roboter als Helfer

Automatisierte Tests nutzen Skripte und Werkzeuge, um die gleichen Prüfungen durchzuführen, die du manuell machen würdest – nur eben viel schneller, präziser und beliebig oft wiederholbar. Für das Refactoring von HTML sind vor allem zwei Arten von automatisierten Tests Gold wert.

**1. Visuelle Regressionstests**

Diese Tests sind deine schärfste Waffe gegen zerbrochene Layouts und CSS-Fehler. Das Prinzip ist genial einfach:
1.  Ein Werkzeug macht einen Screenshot von einer Seite *vor* deinen Änderungen. Dies ist dein Referenzbild oder "Baseline".
2.  Nachdem du dein Refactoring durchgeführt hast, macht das Werkzeug einen neuen Screenshot von der exakt gleichen Seite.
3.  Anschließend vergleicht die Software die beiden Bilder Pixel für Pixel.
4.  Gibt es Unterschiede, schlägt der Test fehl und du bekommst einen visuellen Bericht, der dir genau anzeigt, *wo* sich etwas verschoben, verfärbt oder verändert hat.

Werkzeuge wie BackstopJS, Percy oder die visuellen Vergleichsfunktionen moderner Test-Frameworks wie Playwright und Cypress sind hierfür ideal. Du musst nicht mehr mit bloßem Auge zwei Versionen einer Seite vergleichen, sondern bekommst Abweichungen auf dem Silbertablett serviert. Das spart unglaublich viel Zeit und entdeckt auch minimale Verschiebungen von nur einem Pixel, die du manuell niemals finden würdest.

**2. End-to-End (E2E) Tests**

Während visuelle Tests das Aussehen prüfen, stellen E2E-Tests die Funktionalität sicher. Sie simulieren einen echten Benutzer, der mit deiner Webseite interagiert. Ein Test-Framework steuert dabei einen echten Browser und führt Aktionen wie Klicken, Scrollen oder Texteingaben aus.

Ein E2E-Testskript für unser Kontaktformular könnte konzeptionell so aussehen:

```javascript
// Pseudocode für einen E2E-Test mit einem Framework wie Cypress oder Playwright

test('Das Kontaktformular sollte erfolgreich versendet werden können', () => {
  // 1. Seite aufrufen
  browser.visit('/kontakt');

  // 2. Formularfelder ausfüllen
  browser.fill('#name', 'Max Mustermann');
  browser.fill('#email', 'max@beispiel.de');
  browser.fill('#nachricht', 'Dies ist ein Test.');

  // 3. Auf den Senden-Button klicken
  browser.click('#senden-button');

  // 4. Überprüfen, ob die Erfolgsmeldung erscheint
  // Der Test schlägt fehl, wenn das Element nicht gefunden wird.
  browser.expect_element_to_be_visible('#erfolgsmeldung');
});
```

Wenn du nun durch dein Refactoring die ID `#senden-button` zu `#contact-submit` geändert hast, würde dieses Skript sofort fehlschlagen. Du wüsstest augenblicklich, dass deine JavaScript-gesteuerte Formularlogik durch die HTML-Änderung kaputtgegangen ist.

**Vorteile:**
*   **Schnell und zuverlässig:** Hunderte Tests können in Minuten ausgeführt werden.
*   **Wiederholbar:** Die Tests laufen immer unter den exakt gleichen Bedingungen.
*   **Dokumentation:** Die Tests beschreiben, wie die Anwendung funktionieren soll.
*   **Sicherheit:** Du kannst mit viel größerem Vertrauen Änderungen vornehmen, weil dein automatisiertes Sicherheitsnetz dich warnt, wenn etwas schiefgeht.

**Nachteile:**
*   **Einrichtungsaufwand:** Die Implementierung von Test-Frameworks und das Schreiben der Testskripte erfordert Einarbeitungszeit und technisches Wissen.
*   **Wartung:** Wenn sich die Anwendung ändert, müssen auch die Tests angepasst werden.

#### Eine pragmatische Strategie für dein Projekt

Du musst nicht sofort ein vollumfängliches, automatisiertes Test-Monster aufbauen. Für dein Refactoring-Projekt kannst du pragmatisch vorgehen:

1.  **Identifiziere die kritischen Pfade:** Welche 5-10 Seiten oder Funktionen sind für deine Webseite überlebenswichtig? Die Startseite, der Login-Prozess, der Warenkorb, die wichtigste Landingpage. Konzentriere dich auf diese.

2.  **Erstelle einen manuellen Testplan:** Schreibe die Schritte zum Testen dieser kritischen Pfade als Checkliste nieder. Dies ist dein absolutes Minimum an Absicherung.

3.  **Mache "Vorher"-Screenshots:** Bevor du eine einzige Zeile Code änderst, mache manuell Screenshots von den kritischen Seiten. Lege sie in einen "Vorher"-Ordner.

4.  **Refactoring durchführen:** Jetzt modernisierst du dein HTML.

5.  **Teste nach Plan:** Arbeite deine manuelle Checkliste ab. Öffne deine "Vorher"-Screenshots und vergleiche sie visuell mit dem neuen Stand.

Wenn du diesen Prozess mehrmals durchläufst, wirst du den Wunsch nach Automatisierung von selbst entwickeln. Der nächste Schritt wäre dann, für die wichtigsten visuellen Prüfungen ein einfaches visuelles Regressionstool aufzusetzen. Schon mit 3-4 automatisierten Screenshots der wichtigsten Seiten hast du einen riesigen Gewinn an Sicherheit und Geschwindigkeit erzielt.

Regressionstests sind keine Belastung, sondern eine Befähigung. Sie geben dir die Freiheit, mutig zu refactorn, Altes zu verbessern und moderne Techniken anzuwenden, ohne die ständige Angst, das funktionierende System dabei zu zerstören. Sie verwandeln einen riskanten Blindflug in einen kontrollierten und sicheren Modernisierungsprozess.
