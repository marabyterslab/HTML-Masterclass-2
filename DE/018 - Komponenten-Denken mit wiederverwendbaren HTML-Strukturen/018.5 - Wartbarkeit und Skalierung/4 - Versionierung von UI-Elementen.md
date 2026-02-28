# Versionierung von UI-Elementen

### Versionierung von UI-Elementen: Komponenten zukunftssicher gestalten

Stell dir vor, du arbeitest an einem großen Webprojekt. Über Monate und Jahre hinweg habt ihr eine solide Bibliothek an wiederverwendbaren HTML-Komponenten aufgebaut: Buttons, Karten, Formularfelder, Modals. Alles funktioniert wunderbar. Das Projekt wächst, neue Anforderungen kommen hinzu und das Design entwickelt sich weiter. Plötzlich stehst du vor einer Herausforderung: Eine deiner zentralen Komponenten, zum Beispiel die `card`-Komponente, muss grundlegend geändert werden. Vielleicht soll sie statt `div`-Elementen semantisch korrekte `article`-, `header`- und `footer`-Tags verwenden. Oder die CSS-Klassen sollen umbenannt werden, um einem neuen Namensschema wie BEM (Block, Element, Modifier) zu folgen.

Was tust du jetzt? Wenn du einfach die bestehende Komponente anpasst, läufst du Gefahr, dutzende oder gar hunderte Stellen im gesamten Projekt zu zerschießen, an denen die alte Version verwendet wird. Jede einzelne Implementierung müsste gefunden und manuell angepasst werden – ein Albtraum für die Wartbarkeit und eine garantierte Quelle für neue Fehler.

Genau hier kommt die Versionierung von UI-Elementen ins Spiel. Sie ist kein kompliziertes, abstraktes Konzept, sondern eine sehr praktische Strategie, um Veränderungen an Komponenten kontrolliert, sicher und nachvollziehbar zu gestalten. Versionierung ist ein Grundpfeiler für skalierbare und wartbare Frontends.

#### Der Vertrag einer Komponente

Bevor wir über Strategien sprechen, müssen wir verstehen, was wir eigentlich versionieren. Jede HTML-Komponente hat eine Art "öffentlichen Vertrag" oder eine Schnittstelle (API), an die sich jeder Entwickler hält, der sie verwendet. Dieser Vertrag besteht aus mehreren Teilen:

1.  **Die HTML-Struktur:** Die erwartete Verschachtelung von Tags. Wenn deine Komponente zum Beispiel einen `.card__header` innerhalb eines `.card`-Containers erwartet, ist das Teil des Vertrags.
2.  **Die CSS-Klassen:** Die Namen der Klassen, die für das Styling und als JavaScript-Hooks dienen, sind der wichtigste Teil der Schnittstelle. Eine Änderung von `.button` zu `.btn` ist eine Vertragsverletzung.
3.  **Die JavaScript-API:** Dazu gehören `data-*`-Attribute, die für die Initialisierung von Skripten verwendet werden, oder bestimmte Ereignisse, die von der Komponente ausgelöst werden.

Jede Änderung, die diesen Vertrag bricht und dazu führt, dass eine bestehende Implementierung der Komponente nicht mehr wie erwartet funktioniert, wird als **Breaking Change** (brechende Änderung) bezeichnet. Eine Änderung, die den Vertrag erweitert, ohne Bestehendes zu beeinträchtigen (z. B. das Hinzufügen einer neuen, optionalen CSS-Klasse für eine Farbvariante), ist hingegen ein **Non-Breaking Change**.

Das Ziel der Versionierung ist es, klar zu kommunizieren, wann solche Breaking Changes auftreten, und einen Migrationspfad anzubieten, anstatt das gesamte System auf einmal umstellen zu müssen.

#### Strategien zur Versionierung im Code

Die bekannteste Methode zur Versionierung von Software ist die **Semantische Versionierung (SemVer)** mit ihrem `MAJOR.MINOR.PATCH`-Schema.

*   **MAJOR (z.B. 2.0.0):** Wird erhöht, wenn du einen Breaking Change einführst.
*   **MINOR (z.B. 1.1.0):** Wird erhöht, wenn du neue Funktionalität hinzufügst, die abwärtskompatibel ist.
*   **PATCH (z.B. 1.0.1):** Wird erhöht, wenn du abwärtskompatible Fehlerbehebungen vornimmst.

Dieses Prinzip ist ein hervorragendes mentales Modell, um über Änderungen an UI-Komponenten nachzudenken. Aber wie übersetzen wir das in konkreten HTML- und CSS-Code?

##### 1. Versionierung über CSS-Klassen

Der direkteste Weg, eine neue Version einer Komponente einzuführen, ist über eine neue, versionierte CSS-Klasse. Dies ermöglicht es, die alte und die neue Version der Komponente für eine Übergangszeit parallel im Projekt zu betreiben.

Nehmen wir unsere `card`-Komponente. Die ursprüngliche Version (v1) könnte so aussehen:

```html
<!-- v1.0.0 der Card-Komponente -->
<div class="card">
  <img class="card-image" src="bild.jpg" alt="...">
  <div class="card-content">
    <h3>Ein Titel</h3>
    <p>Ein bisschen Text zur Beschreibung.</p>
  </div>
</div>
```

```css
/* v1.0.0 CSS */
.card {
  border: 1px solid #ccc;
  border-radius: 4px;
}
.card-image {
  width: 100%;
}
.card-content {
  padding: 16px;
}
```

Nun kommt die Anforderung, die Struktur zu verbessern und BEM zu verwenden. Das ist ein klarer Breaking Change. Wir erstellen also eine Version 2. Anstatt den alten Code zu überschreiben, führen wir eine neue Hauptklasse ein, z.B. `card--v2`.

```html
<!-- v2.0.0 der Card-Komponente -->
<article class="card card--v2">
  <header class="card__header">
    <h3 class="card__title">Ein Titel</h3>
  </header>
  <div class="card__body">
    <p>Ein bisschen Text zur Beschreibung.</p>
  </div>
  <img class="card__image" src="bild.jpg" alt="...">
</article>
```

```css
/* v2.0.0 CSS */
.card--v2 {
  display: flex;
  flex-direction: column;
  border: 1px solid #aaa;
  border-radius: 8px;
  background: #f9f9f9;
}

.card--v2 .card__header {
  padding: 16px;
  border-bottom: 1px solid #eee;
}

.card--v2 .card__title {
  margin: 0;
}

/* ... weitere v2-spezifische Stile */
```

Der entscheidende Vorteil: Beide Versionen können koexistieren. Neue Features werden mit der `v2`-Komponente gebaut. Alte Bereiche der Webseite, die noch `v1` nutzen, funktionieren weiterhin tadellos. Das Team kann die Migration schrittweise durchführen, Seite für Seite, ohne den Druck einer "Big Bang"-Umstellung. Sobald alle Instanzen von `v1` migriert sind, kann der alte Code sicher entfernt werden.

##### 2. Versionierung über die Dateistruktur

In einem gut organisierten Projekt, das vielleicht einen Präprozessor wie Sass oder ein Build-System verwendet, ist die Organisation über Ordner eine saubere Alternative oder Ergänzung.

Stell dir folgende Ordnerstruktur vor:

```
/components
  /button
    - _button.scss
    - button.js
  /card
    /v1
      - _card.scss
      - card.html
    /v2
      - _card.scss
      - card.html
```

In diesem Fall sind die Versionen physisch voneinander getrennt. In deinen Haupt-Stylesheets oder JavaScript-Dateien importierst du dann explizit die Version, die du benötigst.

Für ein neues Projekt könntest du direkt `v2` importieren:
`@import 'components/card/v2/card';`

In einem Legacy-Bereich, der noch nicht umgestellt wurde, bleibt der alte Import bestehen:
`@import 'components/card/v1/card';`

Diese Methode hält den Code für jede Version isoliert und sauber. Sie verhindert, dass Stile der alten Version versehentlich die neue beeinflussen oder umgekehrt. Die Klarheit in der Dateistruktur macht auf den ersten Blick ersichtlich, welche Versionen einer Komponente existieren und aktiv genutzt werden.

#### Der sanfte Übergang: Deprecation

Wenn du eine neue Version einer Komponente einführst, ist es wichtig, den Nutzern der alten Version (also deinen Teamkollegen) einen klaren Pfad aufzuzeigen. Das Konzept der "Deprecation" (Missbilligung, Veralten) ist hierbei zentral.

Eine "deprecated" Komponente funktioniert zwar noch, aber sie ist für die zukünftige Verwendung nicht mehr empfohlen. Ihr baldiges Ende ist angekündigt. Dies kann auf verschiedene Weisen kommuniziert werden:

*   **Dokumentation:** Der offensichtlichste Ort. Im Design System oder der Komponenten-Dokumentation wird die `v1` der Karte als "veraltet" markiert, mit einem Link zur `v2` und einer Migrationsanleitung.
*   **Code-Kommentare:** Ein Kommentar direkt im CSS/Sass-Code kann Wunder wirken:
    ```scss
    // =================================================================
    // CARD v1 (DEPRECATED - wird in Q4 entfernt. Bitte card--v2 nutzen)
    // =================================================================
    .card { ... }
    ```
*   **Build-Warnungen:** Fortgeschrittene Build-Prozesse können so konfiguriert werden, dass sie eine Warnung in der Konsole ausgeben, wenn eine veraltete Sass-Datei importiert wird.
*   **Laufzeit-Warnungen:** Ein kleines JavaScript, das an die alte Komponente gebunden ist, kann eine Nachricht in der Entwicklerkonsole des Browsers ausgeben: `console.warn('Die Komponente ".card" ist veraltet. Bitte auf die neue Card-Struktur (v2) migrieren.')`.

Durch Deprecation schaffst du Transparenz und gibst dem Team die Zeit, die es für eine geordnete Umstellung braucht. Du verhinderst, dass aus Unwissenheit weiterhin neue Instanzen der alten Komponente verbaut werden.

Versionierung ist also mehr als nur das Anhängen einer Zahl an einen Dateinamen. Es ist eine Denkweise, die Wartbarkeit und Skalierbarkeit in den Vordergrund stellt. Sie zwingt dich dazu, bewusst über die Schnittstellen deiner Komponenten nachzudenken und Änderungen so zu planen, dass sie ein wachsendes Projekt nicht lähmen, sondern es evolutionär und stabil weiterentwickeln. In einem Team, das gemeinsam an einer großen Codebasis arbeitet, ist diese Disziplin unverzichtbar.
