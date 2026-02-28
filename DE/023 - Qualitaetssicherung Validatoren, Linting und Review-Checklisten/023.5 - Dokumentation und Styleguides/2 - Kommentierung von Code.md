# Kommentierung von Code

### Die Kunst des Kommentierens: Mehr als nur Notizen im Code

Code ist selten für die Ewigkeit geschrieben und noch seltener nur für eine einzige Person – dich selbst. Stell dir vor, du öffnest ein Projekt, an dem du vor sechs Monaten gearbeitet hast. Kannst du dich sofort an jeden Gedankengang, jede Entscheidung und jede clevere Lösung erinnern? Wahrscheinlich nicht. Oder stell dir vor, eine Kollegin muss eine von dir geschriebene Funktion erweitern. Ohne Wegweiser wird sie wertvolle Zeit damit verbringen, deine Logik zu entschlüsseln, anstatt produktiv zu arbeiten.

Hier kommen Kommentare ins Spiel. Sie sind das Schmiermittel für die Zusammenarbeit und ein unschätzbares Werkzeug für dein zukünftiges Ich. Ein gut kommentierter Code ist ein Zeichen von Professionalität und Voraussicht. Er ist Teil der Dokumentation deines Projekts und ein entscheidender Aspekt der Qualitätssicherung. Doch wie bei jedem Werkzeug kommt es darauf an, wie man es benutzt. Zu viele oder falsche Kommentare können mehr schaden als nutzen.

#### Die Syntax: Wie man in verschiedenen Sprachen kommentiert

Bevor wir in die Philosophie des Kommentierens eintauchen, klären wir die Grundlagen. In den Kernsprachen des Webs – HTML, CSS und JavaScript – gibt es unterschiedliche Wege, um Code zu kommentieren.

**HTML-Kommentare**

In HTML schließt du einen Kommentar mit `<!--` und `-->` ein. Alles, was dazwischen steht, wird vom Browser nicht gerendert, also nicht auf der Webseite angezeigt. Es ist jedoch im Quelltext der Seite sichtbar.

```html
<!-- Dies ist ein einzeiliger Kommentar. -->

<header>
  <h1>Willkommen auf meiner Seite</h1>
  <!-- 
    Dieser Navigationsbereich wird vorübergehend ausgeblendet,
    bis die Unterseiten fertiggestellt sind.
    TODO: Wieder aktivieren, sobald /ueber-uns und /kontakt existieren.
  -->
  <!--
  <nav>
    <ul>
      <li><a href="/">Start</a></li>
      <li><a href="/ueber-uns">Über uns</a></li>
      <li><a href="/kontakt">Kontakt</a></li>
    </ul>
  </nav>
  -->
</header>
```

HTML-Kommentare sind ideal, um ganze Code-Blöcke vorübergehend zu „deaktivieren“ oder um Erklärungen zu komplexen DOM-Strukturen zu hinterlassen.

**CSS-Kommentare**

In CSS gibt es nur eine Art von Kommentar, die mit `/*` beginnt und mit `*/` endet. Sie kann sich über eine oder mehrere Zeilen erstrecken.

```css
/* Dies ist ein einzeiliger CSS-Kommentar */

body {
  font-family: 'Helvetica', sans-serif;
  line-height: 1.6; /* Ein guter Standard für die Lesbarkeit */
}

/* 
   ================================
   Hauptnavigations-Stile
   ================================
   Dieser Abschnitt definiert das Aussehen
   der primären Navigation im Header.
*/
.main-nav {
  background-color: #333;
}

/* Ein kleiner Hack für einen älteren Browser-Bug. */
.special-container {
  display: inline-block; /* Verhindert das Kollabieren des Elternelements */
  width: 100%;
}
```

CSS-Kommentare eignen sich hervorragend, um Stylesheets zu strukturieren und Abschnitte klar voneinander zu trennen.

**JavaScript-Kommentare**

JavaScript bietet dir zwei Möglichkeiten: einzeilige und mehrzeilige Kommentare.

Einzeilige Kommentare beginnen mit `//`. Alles vom `//` bis zum Ende der Zeile wird vom Interpreter ignoriert.

Mehrzeilige Kommentare funktionieren genau wie in CSS mit `/*` und `*/`.

```javascript
// Variable für die aktuelle Benutzer-ID
let currentUserId = 123;

function calculateTotal(price, quantity) {
  // Prüfen, ob die Menge eine positive Zahl ist.
  if (quantity <= 0) {
    return 0; // Bei ungültiger Menge 0 zurückgeben.
  }

  /* 
    Hier wird eine komplexe Steuerberechnung durchgeführt.
    Der Steuersatz wird von einer externen API bezogen,
    was in einer späteren Version implementiert wird.
    FIXME: Feste 19% durch API-Aufruf ersetzen.
  */
  const taxRate = 0.19; 
  return (price * quantity) * (1 + taxRate);
}
```

#### Die goldene Regel: Kommentiere das „Warum“, nicht das „Was“

Der häufigste Fehler beim Kommentieren ist, das Offensichtliche zu erklären. Dein Code sollte so sauber und verständlich geschrieben sein, dass er für sich selbst spricht. Er erklärt, *was* er tut. Deine Kommentare sollten erklären, *warum* er es tut.

Betrachte dieses schlechte Beispiel:

```javascript
// Erhöhe i um 1
i++; 
```

Dieser Kommentar ist vollkommen überflüssig. Jeder, der auch nur die Grundlagen von JavaScript kennt, weiß, was `i++` bedeutet. Der Kommentar erzeugt nur visuellen Lärm und lenkt vom Wesentlichen ab.

Vergleiche das mit einem guten Kommentar, der Kontext liefert:

```javascript
// Wir überspringen das erste Element, da es die Überschrift der CSV-Datei ist.
i++; 
```

Plötzlich hat dieselbe Codezeile eine tiefere Bedeutung. Der Kommentar erklärt die Absicht, die Geschäftslogik hinter dieser Anweisung. Er beantwortet die Frage „Warum beginnt die Verarbeitung nicht bei Null?“.

Gute Kommentare konzentrieren sich auf:
*   **Geschäftslogik:** Warum wird ein Rabatt nur für Kunden aus einem bestimmten Land gewährt?
*   **Designentscheidungen:** Warum wurde hier eine `div`-Struktur anstelle einer semantischen HTML5-Tabelle verwendet? (Vielleicht wegen eines speziellen Layout-Frameworks.)
*   **Workarounds:** Warum wird dieser seltsame CSS-Präfix oder JavaScript-Polyfill benötigt? (Meistens, um einen Bug in einem bestimmten Browser zu umgehen.)
*   **Konsequenzen:** Welche Auswirkungen hat die Änderung dieser Funktion auf andere Teile der Anwendung?

#### Sinnvolle Anwendungsfälle für Kommentare

Neben der goldenen Regel gibt es einige etablierte Muster, bei denen Kommentare besonders wertvoll sind.

**1. Strukturierung von Code**

In langen Dateien, insbesondere in CSS-Stylesheets, helfen Kommentare dabei, den Überblick zu behalten. Sie dienen als Überschriften für logische Blöcke.

```css
/* ==========================================================================
   #HEADER
   ========================================================================== */

.site-header {
  /* ... */
}

/* ==========================================================================
   #FOOTER
   ========================================================================== */

.site-footer {
  /* ... */
}
```

**2. Absicht und Kontext erklären**

Manchmal ist Code nicht selbsterklärend, egal wie gut du deine Variablen und Funktionen benennst. Eine kurze Erklärung der Absicht kann Wunder wirken.

```javascript
// Diese Funktion nutzt den "Fisher-Yates-Shuffle"-Algorithmus, um eine
// performante und statistisch unvoreingenommene Durchmischung des Arrays zu gewährleisten.
function shuffleArray(arr) {
  // ... komplexe Implementierung ...
}
```

**3. TODOs und FIXMEs**

Kommentare sind ein praktisches Werkzeug, um dich oder dein Team an ausstehende Aufgaben oder bekannte Probleme direkt im Code zu erinnern. Viele Entwicklungsumgebungen und Tools heben diese Schlüsselwörter sogar farblich hervor.

*   `// TODO:` Markiert eine geplante Funktion oder eine unvollständige Implementierung, die noch erledigt werden muss.
*   `// FIXME:` Weist auf einen bekannten Fehler hin, der behoben werden muss.

```javascript
function sendEmail(address, subject, body) {
  // TODO: Fügen Sie eine Validierung für die E-Mail-Adresse hinzu.
  // ...
}
```

**4. Formale Dokumentationskommentare (z. B. JSDoc)**

Für komplexere Projekte, insbesondere in JavaScript, gibt es standardisierte Formate wie JSDoc. Diese speziell formatierten Kommentare können von Tools gelesen werden, um automatisch eine vollständige technische Dokumentation zu erstellen.

```javascript
/**
 * Berechnet den Gesamtpreis inklusive Mehrwertsteuer.
 *
 * @param {number} price - Der Nettopreis des Produkts.
 * @param {number} quantity - Die Anzahl der Produkte.
 * @returns {number} Der Bruttogesamtpreis.
 */
function calculateTotal(price, quantity) {
  const taxRate = 0.19;
  return (price * quantity) * (1 + taxRate);
}
```
Auch wenn dies über einfaches Kommentieren hinausgeht, ist es wichtig zu wissen, dass Kommentare die Grundlage für eine professionelle Dokumentation bilden können.

#### Die Anti-Muster: Was du unbedingt vermeiden solltest

So wie es gute Praktiken gibt, gibt es auch schlechte Angewohnheiten, die du dir abgewöhnen solltest.

**1. Auskommentierter Code**

Es ist verlockend, alten Code nicht zu löschen, sondern ihn einfach auszukommentieren – für den Fall, dass man ihn später noch braucht. Widerstehe diesem Drang! Auskommentierter Code ist „toter Code“. Er macht Dateien unübersichtlich und verwirrt andere Entwickler, die nicht wissen, ob er wichtig ist, fehlerhaft war oder einfach vergessen wurde.

Für die Verwaltung von Code-Versionen gibt es Versionskontrollsysteme wie Git. Wenn du alten Code wiederherstellen musst, kannst du das jederzeit aus der Git-Historie tun. Lösche ihn also ohne Reue.

**2. Irreführende oder veraltete Kommentare**

Ein falscher Kommentar ist weitaus schlimmer als gar kein Kommentar. Wenn du den Code änderst, musst du auch den dazugehörigen Kommentar aktualisieren. Ein Kommentar, der eine Logik beschreibt, die nicht mehr existiert, führt Entwickler auf eine falsche Fährte und kostet wertvolle Debugging-Zeit. Pflege deine Kommentare wie deinen Code.

**3. Witze und unprofessionelle Bemerkungen**

Auch wenn ein witziger Kommentar im Moment harmlos erscheint, hat er in professionellem Code nichts zu suchen. Er kann missverstanden werden, wirkt unprofessionell und lenkt vom eigentlichen Zweck des Kommentars ab: Klarheit zu schaffen.

Kommentare sind ein fester Bestandteil deines Handwerks als Webentwickler. Sie sind eine Form der Kommunikation mit deinem Team und mit dir selbst in der Zukunft. Setze sie bewusst und gezielt ein, um das „Warum“ hinter deinem Code zu beleuchten, und du wirst nicht nur die Qualität deiner Projekte steigern, sondern auch die Zusammenarbeit im Team erheblich erleichtern.
