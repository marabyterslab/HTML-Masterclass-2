# Wann ARIA notwendig ist

### Wann du ARIA wirklich brauchst

Wenn du dich mit der Entwicklung von barrierefreien Webseiten beschäftigst, stößt du unweigerlich auf ARIA – die „Accessible Rich Internet Applications“ Suite. Die Versuchung kann groß sein, ARIA-Attribute großzügig über dein HTML zu streuen, in der Hoffnung, die Zugänglichkeit quasi magisch zu verbessern. Doch das ist ein Trugschluss. Der gezielte und korrekte Einsatz von ARIA ist eine Kunst, die auf einem grundlegenden Prinzip beruht: Weniger ist oft mehr.

Die allererste und wichtigste Regel im Umgang mit ARIA lautet: **Verwende, wann immer es möglich ist, native HTML-Elemente.** Ein `<button>`-Element ist von Natur aus barrierefrei. Browser und assistive Technologien (AT), wie Screenreader, wissen genau, was es ist und wie man damit interagiert. Es ist fokussierbar, per Tastatur (Enter und Leertaste) aktivierbar und teilt seine Rolle als „Schaltfläche“ unmissverständlich mit. Wenn du stattdessen ein `<div>` mit einem `role="button"` versiehst, musst du all diese Funktionalitäten – Fokussierbarkeit, Keyboard-Events, Zustandsmanagement – selbst per JavaScript nachbauen. Du lädst dir also zusätzliche Arbeit und potenzielle Fehlerquellen auf, nur um etwas zu erreichen, was HTML dir von Haus aus schenkt.

ARIA ist kein Ersatz für gutes, semantisches HTML. Es ist eine Brücke. Eine Erweiterung für jene Fälle, in denen die HTML-Spezifikation an ihre Grenzen stößt. Deine Aufgabe ist es, zu erkennen, wann du diese Brücke bauen musst. Im Grunde gibt es drei Hauptszenarien, in denen ARIA nicht nur nützlich, sondern absolut notwendig ist.

#### 1. Dynamische Inhalte und Statusänderungen mitteilen

Das moderne Web ist dynamisch. Inhalte laden nach, Formulare zeigen Fehlermeldungen an und Benachrichtigungen ploppen auf – oft alles, ohne dass die Seite neu geladen wird. Für sehende Nutzer ist das meist kein Problem; sie sehen die Veränderung auf dem Bildschirm. Ein Screenreader-Nutzer bekommt davon jedoch nichts mit, es sei denn, du teilst es ihm explizit mit.

Hier kommt das ARIA-Attribut `aria-live` ins Spiel. Es verwandelt ein gewöhnliches Element in eine „Live Region“. Jede Änderung innerhalb dieses Elements wird dem Nutzer von seiner assistiven Technologie vorgelesen.

Stell dir eine simple Benachrichtigung vor, die nach einer erfolgreichen Aktion erscheint:

```html
<div id="notification" class="toast" role="status" aria-live="polite">
  <!-- Hier wird die Nachricht per JavaScript eingefügt -->
</div>

<script>
  function showNotification(message) {
    const notificationArea = document.getElementById('notification');
    notificationArea.textContent = message;
    
    // Optional: Nachricht nach einiger Zeit wieder ausblenden
    setTimeout(() => {
      notificationArea.textContent = '';
    }, 5000);
  }

  // Beispielaufruf
  // showNotification('Deine Einstellungen wurden erfolgreich gespeichert.');
</script>
```

In diesem Beispiel sorgt `aria-live="polite"` dafür, dass der Screenreader seine aktuelle Tätigkeit (z. B. das Vorlesen eines Textabschnitts) beendet und *danach* den neuen Inhalt der Benachrichtigung vorliest. Das ist die höfliche, nicht unterbrechende Variante.

Für sehr wichtige, dringende Meldungen, wie eine kritische Fehlermeldung, gibt es `aria-live="assertive"`. Diese Einstellung unterbricht den Screenreader sofort und liest die neue Information vor.

Ein weiteres nützliches Attribut in diesem Kontext ist `aria-busy="true"`. Wenn du einen Bereich deiner Seite aktualisierst und die Daten erst vom Server geladen werden müssen, kannst du dem Container dieses Attribut geben. Damit teilst du assistiven Technologien mit: „Moment, hier wird gerade gearbeitet. Bitte warte, bevor du den Inhalt auswertest.“ Sobald der Inhalt geladen ist, setzt du es wieder auf `false`.

#### 2. Komplexe, interaktive Komponenten (Widgets)

HTML bietet uns Bausteine für Formulare, Links, Listen und Schaltflächen. Aber was ist mit Dingen wie einem Tab-Panel, einem Akkordeon, einem Schieberegler (Slider) oder einer Autocomplete-Eingabebox? Für solche komplexen UI-Komponenten, die oft als „Widgets“ bezeichnet werden, gibt es keine nativen HTML-Elemente.

Wenn du so eine Komponente mit `<div>`s und `<span>`s baust, erschaffst du aus semantischer Sicht eine Blackbox. Ein Screenreader sieht nur eine Ansammlung von generischen Containern und weiß nicht, dass sie zusammen ein interaktives Tab-System bilden.

Das ist der zweite große Anwendungsfall für ARIA: Du verleihst deinen selbstgebauten Widgets eine Bedeutung, indem du ihnen Rollen, Zustände und Eigenschaften zuweist.

**Beispiel: Ein einfaches Akkordeon**

Ein Akkordeon besteht aus mehreren ausklappbaren Abschnitten. Jeder Abschnitt hat einen klickbaren Kopfbereich (Header), der den zugehörigen Inhaltsbereich (Panel) ein- oder ausblendet.

Ohne ARIA wäre der HTML-Code vielleicht so:

```html
<!-- NICHT barrierefrei -->
<div>
  <h3>Abschnitt 1</h3>
  <div>
    Inhalt von Abschnitt 1...
  </div>
  <h3>Abschnitt 2</h3>
  <div style="display: none;">
    Inhalt von Abschnitt 2...
  </div>
</div>
```

Ein Screenreader weiß hier nicht, dass `<h3>` und `<div>` zusammengehören, dass der erste Abschnitt offen und der zweite geschlossen ist, oder dass man auf die Überschrift klicken kann, um etwas zu ändern.

Mit ARIA wird daraus eine verständliche Struktur:

```html
<div>
  <h3>
    <button aria-expanded="true" aria-controls="panel-1" id="header-1">
      Abschnitt 1
    </button>
  </h3>
  <div id="panel-1" role="region" aria-labelledby="header-1">
    Inhalt von Abschnitt 1...
  </div>
  <h3>
    <button aria-expanded="false" aria-controls="panel-2" id="header-2">
      Abschnitt 2
    </button>
  </h3>
  <div id="panel-2" role="region" aria-labelledby="header-2" hidden>
    Inhalt von Abschnitt 2...
  </div>
</div>
```

Schauen wir uns die ARIA-Attribute genauer an:

*   **`<button>`:** Wir verwenden einen echten Button für den klickbaren Bereich. Das gibt uns die native Tastaturbedienung und die korrekte Rolle gratis dazu.
*   **`aria-expanded="true/false"`:** Dieses Attribut teilt dem Screenreader den Zustand mit. "true" bedeutet „aufgeklappt“, "false" bedeutet „zugeklappt“. Dein JavaScript muss diesen Wert bei jedem Klick umschalten.
*   **`aria-controls="panel-1"`:** Hiermit stellst du eine programmatische Verbindung zwischen dem Button und dem Inhaltsbereich her, den er steuert.
*   **`role="region"`:** Verleiht dem Inhaltscontainer eine semantische Bedeutung als zusammengehöriger Bereich.
*   **`aria-labelledby="header-1"`:** Verbindet den Inhaltsbereich zurück mit seiner Überschrift. Das hilft dem Nutzer bei der Orientierung.

Durch diese Handvoll ARIA-Attribute wird aus einer nichtssagenden `div`-Struktur ein voll funktionsfähiges und verständliches Akkordeon für Nutzer assistiver Technologien. Ähnliche Prinzipien gelten für Tabs (`role="tablist"`, `role="tab"`, `role="tabpanel"`, `aria-selected`), Menüs (`role="menu"`, `role="menuitem"`) und viele andere Widgets.

#### 3. Semantische Lücken im HTML füllen

Manchmal ist die Struktur deiner Seite visuell klar, aber die programmatische Beziehung zwischen Elementen fehlt. Das klassische `<label for="...">` ist ein gutes Beispiel, wie HTML Beziehungen herstellt. Aber was, wenn eine einfache Beschriftung nicht ausreicht?

**Zusätzliche Beschreibungen bereitstellen**

Stell dir ein Passwort-Eingabefeld vor. Direkt darunter steht ein kleiner Text mit den Passwortanforderungen (z. B. „Mindestens 8 Zeichen, ein Großbuchstabe und eine Zahl.“).

```html
<label for="password">Passwort</label>
<input type="password" id="password" aria-describedby="password-hint">
<p id="password-hint">
  Mindestens 8 Zeichen, ein Großbuchstabe und eine Zahl.
</p>
```

Das Attribut `aria-describedby` ist hier die Lösung. Es verknüpft das Eingabefeld mit dem beschreibenden Text. Ein Screenreader liest zuerst das Label („Passwort“) vor, gibt den Typ des Feldes an und liest dann den zusätzlichen Hinweis aus dem Absatz vor. Ohne `aria-describedby` müsste der Nutzer diesen wichtigen Kontext auf der Seite selbst suchen.

**Beziehungen zwischen nicht verwandten Elementen herstellen**

Ein weiteres starkes Attribut ist `aria-labelledby`. Im Gegensatz zum `label`-Element kann `aria-labelledby` auf mehrere Elemente verweisen, um eine kombinierte Beschriftung zu erzeugen. Das ist nützlich in komplexen Tabellen oder Formularen, wo die Beschriftung eines Elements aus verschiedenen Teilen der Seite zusammengesetzt wird.

### Wann du ARIA *nicht* verwenden solltest

Genauso wichtig wie das Wissen, wann ARIA notwendig ist, ist das Wissen, wann man es vermeiden sollte.

1.  **Wenn es ein natives HTML-Element gibt.** Das ist die goldene Regel, die wir schon besprochen haben. Verwende keinen `<div role="checkbox">`, wenn du ein `<input type="checkbox">` verwenden kannst.
2.  **Um die native Semantik zu überschreiben.** Du solltest niemals `role` verwenden, um die grundlegende Bedeutung eines Elements zu ändern. Ein `<h2 role="button">` ist ein absolutes Antipattern. Du nimmst der Überschrift ihre wichtige strukturelle Bedeutung und schaffst eine verwirrende, nicht funktionierende Schaltfläche.
3.  **Wenn du die Interaktivität nicht selbst implementierst.** ARIA ist nur eine semantische Schicht. `role="button"` auf einem `<div>` sorgt nicht dafür, dass es auf die Leertaste reagiert. Das musst du selbst mit JavaScript umsetzen. Wenn du das nicht tust, erschaffst du ein „Fake-Widget“, das für Tastaturnutzer unbenutzbar ist.

ARIA ist ein mächtiges Werkzeug, aber kein Allheilmittel. Betrachte es als Präzisionsinstrument, nicht als Hammer. Nutze es gezielt, um die Lücken zu schließen, die semantisches HTML hinterlässt, um dynamische Änderungen zu kommunizieren und um komplexe Widgets verständlich zu machen. Wenn du diesem Leitfaden folgst, bist du auf dem besten Weg, ARIA effektiv und ohne Semantikbruch einzusetzen.
