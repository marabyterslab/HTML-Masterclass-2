# Automatisierte Tests

### Automatisierte Tests: Dein unermüdlicher Helfer bei der Qualitätssicherung

Nachdem wir uns mit manuellen Validatoren, Linting und Checklisten beschäftigt haben, kommen wir nun zu einem der wirkungsvollsten Werkzeuge in der modernen Webentwicklung: den automatisierten Tests. Stell dir vor, du hättest einen unendlich geduldigen und extrem genauen Assistenten, der nach jeder einzelnen Code-Änderung deine gesamte Website oder Anwendung durchklickt, um sicherzustellen, dass alles noch funktioniert. Genau das leisten automatisierte Tests für dich.

Manuelle Überprüfungen sind wichtig, aber sie haben ihre Grenzen. Sie sind zeitaufwendig, anfällig für menschliche Fehler und werden bei wachsendem Projektumfang schnell unpraktikabel. Wer hat schon die Zeit, vor jeder Veröffentlichung 50 verschiedene Unterseiten und Formulare von Hand zu testen? Hier kommt die Automatisierung ins Spiel. Du schreibst einmalig Anweisungen in Form von Code – sogenannte Testskripte –, und ein Programm führt diese immer wieder exakt gleich aus.

#### Warum du automatisierte Tests lieben wirst

Die Vorteile gehen weit über die reine Zeitersparnis hinaus. Automatisierte Tests schaffen ein Sicherheitsnetz, das dir erlaubt, mutiger und schneller zu entwickeln.

*   **Sicherheit bei Änderungen (Regressionstests):** Das ist der vielleicht größte Gewinn. Du fügst eine neue Funktion hinzu oder optimierst ein CSS-Styling. Woher weißt du, dass du nicht versehentlich das Login-Formular auf einer ganz anderen Seite unbrauchbar gemacht hast? Ein automatisierter Test, der den Login-Prozess prüft, wird dich sofort warnen. Das Verhindern solcher unbeabsichtigten Fehler, sogenannter Regressionen, gibt dir enormes Vertrauen in deinen Code.
*   **Schnelles Feedback:** Statt einen Fehler erst Tage später in der Produktion durch einen verärgerten Nutzer zu entdecken, findest du ihn Minuten nach der Code-Änderung auf deinem eigenen Rechner oder in der Continuous-Integration-Pipeline. Je früher ein Fehler entdeckt wird, desto einfacher und günstiger ist er zu beheben.
*   **Lebende Dokumentation:** Ein gut geschriebener Test beschreibt, wie eine Komponente oder eine Funktion verwendet werden soll. Er ist eine exakte, stets aktuelle Dokumentation des erwarteten Verhaltens. Ein neuer Kollege kann sich die Tests ansehen und versteht sofort, wie ein bestimmter Teil der Anwendung funktionieren soll.
*   **Verbessertes Code-Design:** Wenn du von Anfang an bedenkst, wie du deinen Code testen kannst, schreibst du oft automatisch besseren, modulareren und leichter wartbaren Code. Schwer testbarer Code ist häufig ein Anzeichen für ein schlechtes Softwaredesign.

#### Die verschiedenen Ebenen des Testens

Nicht alle Tests sind gleich. In der Frontend-Entwicklung hat sich eine Gliederung in verschiedene Testarten etabliert, die oft als „Testpyramide“ visualisiert wird. Die Idee ist, viele schnelle und einfache Tests an der Basis und wenige langsame, komplexe Tests an der Spitze zu haben.

**1. Unit-Tests (Einheitentests)**

Unit-Tests bilden die Basis der Pyramide. Hier testest du die kleinste logische Einheit deines Codes isoliert von allem anderen. Im JavaScript-Kontext ist das meist eine einzelne Funktion oder eine Komponente (z. B. ein Custom Element oder eine React/Vue-Komponente). Du prüfst: Wenn ich dieser Funktion einen bestimmten Input gebe, erhalte ich dann den erwarteten Output?

Angenommen, du hast eine kleine Hilfsfunktion in JavaScript, die prüft, ob eine E-Mail-Adresse ein `@`-Zeichen enthält:

```javascript
// datei: validators.js
export function isValidEmail(email) {
  if (typeof email !== 'string') {
    return false;
  }
  return email.includes('@');
}
```

Ein Unit-Test dafür würde die Funktion mit verschiedenen Werten aufrufen und das Ergebnis überprüfen:

```javascript
// datei: validators.test.js
import { isValidEmail } from './validators.js';

test('sollte true zurückgeben für eine E-Mail mit @', () => {
  expect(isValidEmail('test@example.com')).toBe(true);
});

test('sollte false zurückgeben für eine E-Mail ohne @', () => {
  expect(isValidEmail('testexample.com')).toBe(false);
});

test('sollte false zurückgeben für einen Nicht-String', () => {
  expect(isValidEmail(123)).toBe(false);
});
```

Solche Tests sind extrem schnell und geben dir präzises Feedback über die Kernlogik deiner Anwendung.

**2. Integrationstests**

Eine Stufe höher stehen die Integrationstests. Hier testest du das Zusammenspiel mehrerer Einheiten. Funktionieren zwei oder mehr Komponenten korrekt zusammen? Wenn du auf einen Button klickst, wird dann auch wirklich das zugehörige Formular abgeschickt?

Stell dir eine simple Newsletter-Anmeldung vor, die aus einem Eingabefeld und einem Sende-Button besteht. Ein Integrationstest würde nicht nur die Komponenten einzeln prüfen, sondern auch simulieren, wie ein Nutzer eine E-Mail eingibt, auf den Button klickt und dann überprüft, ob eine Erfolgsmeldung im HTML erscheint. Hier geht es darum, die Verbindungen und Schnittstellen zwischen den Modulen zu validieren.

**3. End-to-End-Tests (E2E-Tests)**

An der Spitze der Pyramide stehen die E2E-Tests. Sie sind die umfassendsten und simulieren eine komplette Nutzerreise durch deine Anwendung. Ein E2E-Testskript steuert einen echten Browser, öffnet deine Webseite, navigiert durch die Menüs, füllt Formulare aus, klickt auf Links und überprüft, ob die sichtbaren Ergebnisse im Browser korrekt sind.

Diese Tests sind am nächsten an der realen Nutzererfahrung. Sie prüfen nicht nur deine HTML-, CSS- und JavaScript-Logik, sondern das gesamte System, inklusive der Server-Antworten. Sie sind langsamer und aufwendiger zu schreiben und zu warten, aber unverzichtbar, um kritische Nutzerpfade wie den Registrierungs- oder den Bezahlvorgang abzusichern.

#### Werkzeuge für den Frontend-Test-Alltag

Für jede Testebene gibt es spezialisierte Werkzeuge. Die Landschaft der Tools entwickelt sich ständig weiter, aber einige haben sich als Quasi-Standards etabliert.

*   **Für Unit- und Integrationstests:** Frameworks wie **Jest** oder **Vitest** sind hier sehr beliebt. Sie bieten eine Testumgebung (einen "Test-Runner"), Funktionen zum Formulieren von Erwartungen (Assertions, wie `expect(...).toBe(...)`) und Werkzeuge, um Teile deiner Anwendung zu simulieren ("Mocking").
*   **Für E2E-Tests:** Hier dominieren Tools, die einen echten Browser fernsteuern können. **Cypress** ist bekannt für seine einfache Einrichtung und seine exzellente Benutzeroberfläche, die dir bei der Fehlersuche hilft. **Playwright** von Microsoft ist eine weitere extrem leistungsfähige Alternative, die verschiedene Browser-Engines (Chromium, Firefox, WebKit) ansteuern kann und so echtes Cross-Browser-Testing ermöglicht.

#### Ein praktisches Beispiel: Ein E2E-Test mit Cypress

Um das Ganze greifbarer zu machen, schauen wir uns ein einfaches Cypress-Testskript an. Angenommen, wir haben eine Kontaktseite (`kontakt.html`) mit einem simplen Formular.

Unser HTML könnte so aussehen:

```html
<!-- datei: kontakt.html -->
<!DOCTYPE html>
<html lang="de">
<head>
    <title>Kontakt</title>
</head>
<body>
    <h1>Kontaktformular</h1>
    <form id="contact-form">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required>
        
        <label for="email">E-Mail:</label>
        <input type="email" id="email" name="email" required>
        
        <button type="submit">Senden</button>
    </form>
    <div id="success-message" style="display: none;">
        Vielen Dank für deine Nachricht!
    </div>

    <script>
        document.getElementById('contact-form').addEventListener('submit', function(event) {
            event.preventDefault();
            document.getElementById('success-message').style.display = 'block';
        });
    </script>
</body>
</html>
```

Ein Cypress-Test, der das Ausfüllen und Absenden dieses Formulars überprüft, könnte so aussehen:

```javascript
// datei: cypress/integration/kontakt.spec.js
describe('Kontaktformular', () => {
  it('sollte nach dem Absenden eine Erfolgsmeldung anzeigen', () => {
    // 1. Die Seite besuchen
    cy.visit('kontakt.html');

    // 2. Das Namensfeld finden und Text eingeben
    cy.get('#name').type('Max Mustermann');

    // 3. Das E-Mail-Feld finden und Text eingeben
    cy.get('#email').type('max@example.com');

    // 4. Den Sende-Button finden und klicken
    cy.get('button[type="submit"]').click();

    // 5. Überprüfen, ob die Erfolgsmeldung sichtbar ist
    cy.get('#success-message').should('be.visible');
    cy.contains('Vielen Dank für deine Nachricht!');
  });
});
```

Dieses Skript ist fast wie eine menschliche Anweisung zu lesen. Cypress öffnet einen Browser, führt diese Schritte aus und meldet Erfolg oder Misserfolg. Wenn du jetzt am HTML-Formular etwas änderst, das die `id` der Felder oder den Text des Buttons betrifft, wird dieser Test fehlschlagen und dich sofort warnen.

#### Automatisierung in den Arbeitsablauf integrieren

Der wahre Nutzen entfaltet sich, wenn diese Tests automatisch bei jeder Code-Änderung laufen. Dies geschieht in der Regel in einer sogenannten **Continuous Integration (CI)**-Umgebung (z. B. mit GitHub Actions, GitLab CI/CD oder Jenkins).

Der Prozess sieht typischerweise so aus:
1.  Du schreibst neuen Code und lädst ihn in euer Code-Repository (z. B. auf GitHub) hoch.
2.  Dieser Push löst automatisch den CI-Prozess aus.
3.  Ein Server checkt den neuen Code aus.
4.  Er führt alle vordefinierten Schritte aus: zuerst die Linter und Validatoren, dann die schnellen Unit-Tests, dann die Integrationstests und schließlich die E2E-Tests.
5.  Nur wenn alle Schritte erfolgreich durchlaufen wurden, wird der Code als "grün" markiert und kann sicher in den Hauptzweig der Entwicklung integriert oder sogar direkt auf einem Testserver veröffentlicht werden.

Automatisierte Tests sind kein Ersatz für manuelles, exploratives Testen oder für das Denken als Entwickler. Aber sie sind eine unverzichtbare Ergänzung. Sie nehmen dir die monotone, fehleranfällige Routinearbeit ab und geben dir die Freiheit und das Vertrauen, qualitativ hochwertige Webanwendungen zu erstellen und diese kontinuierlich zu verbessern, ohne Angst vor unbeabsichtigten Fehlern haben zu müssen.
