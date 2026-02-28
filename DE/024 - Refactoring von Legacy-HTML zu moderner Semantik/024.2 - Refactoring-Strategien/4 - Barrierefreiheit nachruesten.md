# Barrierefreiheit nachrüsten

### Barrierefreiheit nachrüsten: Mehr als nur ein `alt`-Attribut

Wenn du ein bestehendes Projekt übernimmst oder alten Code modernisieren sollst, ist „Legacy-Code“ oft das erste Wort, das dir in den Sinn kommt. Du siehst vielleicht veraltete Strukturen, unzählige `<div>`-Container und Inline-Styles. Inmitten dieses Refactoring-Prozesses liegt eine riesige Chance, die oft übersehen wird: die Barrierefreiheit nachzurüsten.

Barrierefreiheit, oft auch als Accessibility (a11y) bezeichnet, ist kein optionales Extra, sondern ein fundamentaler Aspekt moderner Webentwicklung. Es geht darum, deine Webseite für wirklich *alle* Menschen nutzbar zu machen, unabhängig von ihren körperlichen oder kognitiven Fähigkeiten oder den technischen Hilfsmitteln, die sie verwenden. Beim Refactoring von Legacy-Code hast du die perfekte Gelegenheit, Barrieren abzubauen und eine inklusivere Erfahrung zu schaffen. Oft sind die notwendigen Änderungen eng mit der Umstellung auf semantisches HTML verknüpft, was die Arbeit doppelt lohnenswert macht.

#### Die niedrig hängenden Früchte: Schnelle Erfolge mit großer Wirkung

Nicht jede Verbesserung muss ein riesiger Kraftakt sein. Es gibt einige grundlegende Dinge, die du oft mit minimalem Aufwand korrigieren kannst, deren positive Auswirkung für Nutzer von Screenreadern oder anderen assistiven Technologien jedoch enorm ist.

**1. Aussagekräftige Alternativtexte für Bilder**

Das `alt`-Attribut ist der Klassiker, wird aber in älterem Code oft falsch oder gar nicht verwendet. Ein Screenreader liest diesen Text vor, um blinden oder sehbehinderten Nutzern den Inhalt des Bildes zu vermitteln.

*   **Schlecht (fehlend):** `<img src="grafik-q3-umsatz.png">`
*   **Schlecht (nichtssagend):** `<img src="grafik-q3-umsatz.png" alt="Grafik">`
*   **Gut (deskriptiv):** `<img src="grafik-q3-umsatz.png" alt="Balkendiagramm, das den Umsatz im dritten Quartal mit einem Anstieg von 15% zeigt.">`

Eine wichtige Ausnahme sind rein dekorative Bilder. Wenn ein Bild keinen inhaltlichen Mehrwert bietet (z. B. eine schmückende Hintergrundtextur), solltest du ein leeres `alt`-Attribut setzen: `alt=""`. Dadurch signalisierst du dem Screenreader, das Bild zu ignorieren. Lässt du das Attribut komplett weg, lesen manche Screenreader stattdessen den Dateinamen vor, was sehr störend sein kann.

**2. Verständliche Link-Texte**

Nutzer von Screenreadern können sich oft eine Liste aller Links auf einer Seite ausgeben lassen, um schnell zu navigieren. Eine Liste, die aus zehnmal „Hier klicken“ und fünfmal „Mehr lesen“ besteht, ist absolut nutzlos. Der Link-Text muss für sich allein stehend verständlich machen, wohin der Link führt.

*   **Schlecht:** `Für weitere Informationen zum Produkt, <a href="/details.html">klicke hier</a>.`
*   **Gut:** `<a href="/details.html">Erfahre mehr über die Produktdetails</a>.`

Beim Refactoring kannst du solche vagen Formulierungen leicht durch aussagekräftige ersetzen.

**3. Die richtige Sprache deklarieren**

Eine winzige Änderung mit großer Wirkung: Gib im `<html>`-Tag die Hauptsprache deines Dokuments an. Das hilft Screenreadern, den Text mit der korrekten Aussprache und dem richtigen Akzent vorzulesen.

```html
<!DOCTYPE html>
<html lang="de">
  <head>
    <!-- ... -->
  </head>
  <body>
    <!-- ... -->
  </body>
</html>
```

#### Semantik heilt viele Wunden: Von `<div>`-Suppen zu klarer Struktur

Legacy-HTML-Seiten sind oft ein Labyrinth aus verschachtelten `<div>`-Elementen, die durch Klassen oder IDs eine vermeintliche Bedeutung erhalten. Dieses Phänomen wird oft als „Divitis“ bezeichnet.

**Vorher: Eine typische `<div>`-Struktur**
```html
<div id="header">
  <img src="logo.png" alt="Firmenlogo">
  <div id="navigation">
    <ul>
      <li><a href="/">Start</a></li>
      <li><a href="/produkte">Produkte</a></li>
    </ul>
  </div>
</div>

<div id="main-content">
  <h1>Willkommen!</h1>
  <p>Das ist der Hauptinhalt der Seite.</p>
</div>

<div id="footer">
  <p>&copy; 2023 Meine Firma</p>
</div>
```

Diese Struktur ist für einen sehenden Menschen durch das Layout verständlich. Für eine Maschine oder einen Screenreader ist es jedoch nur eine Ansammlung von Boxen. Assistive Technologien können die einzelnen Bereiche („Header“, „Navigation“, „Hauptinhalt“) nicht als solche erkennen und dem Nutzer keine Orientierungshilfen bieten.

Hier kommt modernes, semantisches HTML ins Spiel. Durch den Austausch der generischen `<div>`s durch bedeutungsvolle Tags schaffst du eine klare, maschinenlesbare Struktur.

**Nachher: Die gleiche Struktur mit semantischem HTML**
```html
<header>
  <img src="logo.png" alt="Firmenlogo">
  <nav>
    <ul>
      <li><a href="/">Start</a></li>
      <li><a href="/produkte">Produkte</a></li>
    </ul>
  </nav>
</header>

<main>
  <h1>Willkommen!</h1>
  <p>Das ist der Hauptinhalt der Seite.</p>
</main>

<footer>
  <p>&copy; 2023 Meine Firma</p>
</footer>
```
Was haben wir erreicht?
*   `<header>`, `<main>` und `<footer>` definieren die Hauptbereiche der Seite (sogenannte Landmark-Regions). Ein Screenreader kann nun ansagen: „Navigation“, „Hauptinhalt“ oder „Fußzeile“, und der Nutzer kann direkt zu diesen Bereichen springen.
*   `<nav>` kennzeichnet den Hauptnavigationsbereich explizit.
*   Der Code ist lesbarer und selbsterklärender geworden.

Weitere wichtige semantische Elemente, die du beim Refactoring einsetzen solltest, sind `<section>`, `<article>` und `<aside>`.

#### Formulare und interaktive Elemente entminen

Interaktive Elemente sind eine häufige Fehlerquelle in altem Code. Hier lauern oft Barrieren, die die Nutzung für Menschen, die auf Tastaturbedienung oder Screenreader angewiesen sind, unmöglich machen.

**1. Labels für Formularfelder**

Jedes Eingabefeld (`<input>`, `<textarea>`, `<select>`) benötigt ein zugehöriges `<label>`. Ein Label beschreibt, welche Information erwartet wird. Die Verknüpfung erfolgt über das `for`-Attribut des Labels, das auf die `id` des Formularfeldes verweist.

*   **Schlecht:**
    ```html
    E-Mail: <input type="email" id="email_input">
    ```
*   **Gut:**
    ```html
    <label for="email_input">E-Mail-Adresse</label>
    <input type="email" id="email_input">
    ```

Diese Verknüpfung hat zwei entscheidende Vorteile:
1.  Ein Klick auf das Label setzt den Fokus direkt in das zugehörige Eingabefeld. Das vergrößert die Klickfläche und ist eine enorme Hilfe für Nutzer mit motorischen Einschränkungen.
2.  Screenreader lesen das Label vor, wenn das Eingabefeld den Fokus erhält. Ohne Label wüsste ein blinder Nutzer nicht, was er eingeben soll.

**2. Buttons sind Buttons, Links sind Links**

In der Ära vor modernem JavaScript und CSS war es üblich, interaktive Elemente aus `<div>`s oder `<span>`s zu bauen und ihnen per JavaScript eine `onclick`-Funktion zuzuweisen.

*   **Legacy-Beispiel:**
    ```html
    <div class="button" onclick="saveData()">Speichern</div>
    ```

Das ist aus Sicht der Barrierefreiheit eine Katastrophe:
*   Ein `<div>` ist nicht per Tastatur (Tab-Taste) erreichbar.
*   Es kann nicht mit der Enter- oder Leertaste ausgelöst werden.
*   Ein Screenreader erkennt es nicht als interaktives Element, sondern liest nur „Speichern“ vor.

Die Lösung ist einfach: Nutze das richtige HTML-Element für den Job.
*   Ein Link (`<a>`) wird verwendet, um zu einer anderen Seite oder einem anderen Bereich zu navigieren.
*   Ein Button (`<button>`) wird verwendet, um eine Aktion auf der aktuellen Seite auszulösen (z. B. ein Formular senden, ein Modal öffnen, Daten speichern).

*   **Refactored-Beispiel:**
    ```html
    <button type="button" onclick="saveData()">Speichern</button>
    ```

Dieser Button ist standardmäßig per Tastatur fokussierbar und bedienbar. Ein Screenreader kündigt ihn korrekt als „Schaltfläche, Speichern“ an.

#### ARIA als Rettungsanker, wenn HTML nicht ausreicht

Manchmal stößt reines HTML an seine Grenzen, besonders bei komplexen, dynamischen Widgets wie Tabs, Akkordeons oder benutzerdefinierten Dropdown-Menüs. Hier kommt ARIA (Accessible Rich Internet Applications) ins Spiel. ARIA ist eine Sammlung von Attributen, die du zu HTML-Elementen hinzufügen kannst, um ihre Rolle, ihren Zustand und ihre Eigenschaften für assistive Technologien zu beschreiben.

Die erste Regel von ARIA lautet: **Verwende ARIA nicht, wenn es ein natives HTML-Element gibt, das die Aufgabe erfüllt.** Nutze einen `<button>` anstelle eines `<div role="button">`.

Wenn du aber ein komplexes Widget nachrüsten musst, das aus `<div>`s gebaut ist, kann ARIA helfen. Stell dir ein Akkordeon vor, bei dem Inhalte ein- und ausgeklappt werden können.

```html
<!-- Vereinfachtes Beispiel eines Akkordeon-Headers -->
<h3 id="section1-header">
  <button aria-expanded="false" aria-controls="section1-content">
    Abschnitt 1
  </button>
</h3>
<div id="section1-content" role="region" aria-labelledby="section1-header" hidden>
  <p>Dies ist der Inhalt von Abschnitt 1.</p>
</div>
```

Hier bewirken die ARIA-Attribute Folgendes:
*   `aria-expanded="false"` teilt dem Screenreader mit, dass der Bereich aktuell eingeklappt ist. JavaScript muss diesen Wert auf `"true"` ändern, wenn der Bereich geöffnet wird.
*   `aria-controls="section1-content"` stellt eine programmatische Verbindung zwischen dem Button und dem Inhaltsbereich her, den er steuert.
*   `role="region"` und `aria-labelledby` machen den Inhaltscontainer zu einer benannten Region.

ARIA schließt die Lücke zwischen statischem HTML und dynamischen Webanwendungen. Setze es mit Bedacht ein, um die Semantik dort zu ergänzen, wo HTML allein nicht ausreicht.

#### Visuelle Aspekte nicht vergessen: Kontraste und Fokus

Barrierefreiheit ist nicht nur für Screenreader-Nutzer da. Auch Menschen mit Sehschwächen oder motorischen Einschränkungen profitieren von einem durchdachten Design.

**1. Farbkontraste**

Stelle sicher, dass der Kontrast zwischen Text- und Hintergrundfarbe ausreichend hoch ist. Geringe Kontraste machen Texte für viele Menschen schwer oder unmöglich lesbar. Die Web Content Accessibility Guidelines (WCAG) geben hier klare Mindestverhältnisse vor. Du kannst diese Kontraste einfach mit den Entwicklertools deines Browsers oder Online-Tools überprüfen.

**2. Sichtbarer Fokus-Indikator**

Wer eine Webseite mit der Tastatur bedient, ist darauf angewiesen, jederzeit zu sehen, welches Element gerade den Fokus hat. Standardmäßig zeigen Browser dafür einen Rahmen (meist blau oder schwarz) um das aktive Element. In vielen älteren CSS-Dateien findet sich jedoch die unheilvolle Zeile:

```css
:focus {
  outline: none;
}
```

Das entfernt den Fokus-Indikator komplett und macht die Seite für Tastaturnutzer unbedienbar. Wenn du diesen Code beim Refactoring findest, entferne ihn. Falls der Standard-Fokusring optisch nicht zum Design passt, ersetze ihn durch eine eigene, klar sichtbare Hervorhebung.

```css
/* Eine bessere Alternative */
:focus-visible {
  outline: 2px solid #005fcc;
  outline-offset: 2px;
  box-shadow: 0 0 0 4px rgba(0, 95, 204, 0.4);
}
```
Die `:focus-visible`-Pseudoklasse sorgt dafür, dass der Stil nur bei Tastaturfokus und nicht bei einem Mausklick angewendet wird, was oft als ästhetisch ansprechender empfunden wird.

Barrierefreiheit in Legacy-Projekte zu integrieren, mag auf den ersten Blick wie eine zusätzliche Last erscheinen. Doch in Wahrheit ist es ein integraler Bestandteil eines jeden ernsthaften Refactorings. Es verbessert nicht nur die Qualität deines Codes durch saubere Semantik, sondern macht dein Produkt auch für ein viel breiteres Publikum zugänglich und nutzbar. Jeder `<div>`-Tag, den du durch ein `<nav>` ersetzt, und jedes Label, das du hinzufügst, ist ein Schritt zu einem besseren und faireren Web.
