# Barrieren im Web erkennen

### Die unsichtbaren Hürden: Barrieren im Web erkennen

Stell dir vor, du stehst vor einem imposanten Gebäude mit einer breiten Treppe, die zum Eingang führt. Für dich ist das kein Problem, du nimmst die Stufen und bist drin. Doch für eine Person im Rollstuhl, jemanden mit einer Gehhilfe oder Eltern mit einem Kinderwagen ist diese Treppe eine unüberwindbare Barriere. Eine Rampe neben der Treppe würde das Problem lösen. Sie schließt niemanden aus.

Im digitalen Raum ist es ganz ähnlich. Als Entwicklerinnen und Entwickler bauen wir oft unbewusst Treppen, wo wir eigentlich Rampen bräuchten. Diese digitalen Barrieren sind für uns, die die Website mit Maus, Tastatur und vollem Seh- und Hörvermögen nutzen, meist unsichtbar. Unsere Aufgabe ist es, zu lernen, diese Hürden zu erkennen, damit wir sie abbauen können. Es geht darum, eine neue Perspektive einzunehmen und das Web mit den Augen und Werkzeugen anderer Menschen zu sehen.

#### Visuelle Barrieren

Visuelle Einschränkungen sind vielfältig. Sie reichen von vollständiger Blindheit über starke Sehschwächen bis hin zu Farbenblindheit. Jede dieser Gruppen stößt auf unterschiedliche Arten von Hindernissen.

##### Für blinde Menschen: Wenn die Struktur fehlt

Blinde Menschen navigieren das Web nicht mit den Augen, sondern meist mit einem Screenreader. Das ist eine Software, die den Bildschirminhalt vorliest. Ein Screenreader ist auf eine klare, logische Struktur der Webseite angewiesen, um sie verständlich "übersetzen" zu können. Hier lauern die häufigsten Barrieren:

**1. Nichtssagende Bilder:** Ein Bild sagt mehr als tausend Worte – aber nur, wenn man es sehen kann. Für einen Screenreader ist ein Bild ohne beschreibenden Alternativtext (das `alt`-Attribut) einfach nur eine leere Stelle oder er liest den Dateinamen vor, was selten hilfreich ist.

*   **Schlecht:**
    ```html
    <img src="hund-im-park.jpg">
    ```
    Der Screenreader sagt vielleicht: "Grafik, hund-im-park.jpg". Das ist nutzlos.

*   **Gut:**
    ```html
    <img src="hund-im-park.jpg" alt="Ein Golden Retriever fängt einen roten Ball auf einer grünen Wiese.">
    ```
    Jetzt kann sich die Person eine genaue Vorstellung von der Szene machen.

Ist ein Bild rein dekorativ und trägt keine wichtige Information, solltest du ein leeres `alt`-Attribut setzen (`alt=""`). Dadurch wird es vom Screenreader ignoriert und stört den Lesefluss nicht.

**2. Nicht-semantische HTML-Struktur:** Stell dir vor, du bekommst ein Buch, in dem es keine Überschriften, Absätze oder Kapitel gibt – nur einen einzigen, langen Textblock. Du wüsstest nicht, wo ein neues Thema beginnt oder was die Kernaussagen sind. Genau so fühlt sich eine Webseite ohne semantisches HTML für einen Screenreader-Nutzer an.

Wenn du alles mit `<div>`-Elementen baust, ist die Seite eine strukturelle Wüste. Semantisches HTML gibt dem Inhalt eine Bedeutung:

*   `<main>` für den Hauptinhalt
*   `<nav>` für die Navigation
*   `<h1>`, `<h2>`, `<h3>` für eine logische Überschriftenhierarchie
*   `<ul>` und `<ol>` für Listen
*   `<button>` für Aktionen

Ein Screenreader-Nutzer kann gezielt von Überschrift zu Überschrift springen oder sich alle Links auf einer Seite vorlesen lassen. Wenn ein Link nur "Hier klicken" heißt, ist das im Kontext einer Liste von Links völlig nichtssagend. Beschreibender Linktext wie "Mehr über unsere HTML-Kurse erfahren" ist hingegen eindeutig.

##### Für Menschen mit Sehschwäche: Wenn der Kontrast fehlt

Menschen mit Sehschwäche können den Bildschirm oft noch erkennen, benötigen aber starke Vergrößerungen oder hohe Kontraste, um Inhalte zu entziffern.

**1. Geringer Farbkontrast:** Hellgrauer Text auf weißem Hintergrund mag minimalistisch und modern aussehen, ist für viele Menschen aber unlesbar. Das World Wide Web Consortium (W3C) hat in den Web Content Accessibility Guidelines (WCAG) klare Regeln für das Kontrastverhältnis zwischen Text- und Hintergrundfarbe definiert. Es gibt zahlreiche Online-Tools, mit denen du die Kontraste deiner Farbpalette überprüfen kannst.

**2. Nicht skalierbarer Text:** Viele Nutzer vergrößern den Text im Browser, um ihn besser lesen zu können. Wenn du Schriftgrößen in absoluten Einheiten wie Pixeln (`px`) festlegst, kann das zu Problemen führen. Besser sind relative Einheiten wie `rem` oder `em`. Sie passen sich an die vom Nutzer gewählte Basisschriftgröße an und sorgen dafür, dass das Layout beim Zoomen nicht bricht.

##### Für farbenblinde Menschen: Wenn Farbe die einzige Information ist

Etwa jeder zwölfte Mann und jede zweihundertste Frau hat eine Form der Rot-Grün-Sehschwäche. Eine häufige Barriere entsteht, wenn Information ausschließlich durch Farbe vermittelt wird.

Ein klassisches Beispiel ist ein Formular, das fehlerhafte Eingabefelder nur durch einen roten Rahmen markiert. Eine farbenblinde Person erkennt den roten Rahmen möglicherweise nicht. Die Lösung ist einfach: Ergänze die Farbinformation durch Text oder ein Icon.

*   **Schlecht (nur Farbe):**
    ```css
    .input-error {
      border: 2px solid red;
    }
    ```

*   **Gut (Farbe + Text):**
    ```html
    <label for="email">E-Mail:</label>
    <input type="email" id="email" class="input-error" aria-describedby="email-error">
    <span id="email-error" class="error-message">Bitte gib eine gültige E-Mail-Adresse ein.</span>
    ```
    Hier wird der Fehler nicht nur visuell durch Farbe, sondern auch durch eine klare Textbotschaft kommuniziert.

#### Auditive Barrieren

Diese Barrieren betreffen gehörlose oder schwerhörige Menschen, die auf Audio- und Videoinhalte ohne textliche Alternativen stoßen.

**1. Fehlende Untertitel und Transkripte:** Ein Podcast ohne ein Transkript (eine verschriftlichte Version des Gesprochenen) ist für gehörlose Menschen komplett unzugänglich. Ein Video-Tutorial ohne Untertitel schließt sie ebenfalls aus.

Automatisch generierte Untertitel sind ein guter Anfang, aber oft fehlerhaft. Eine manuelle Überprüfung und Korrektur ist unerlässlich, um sicherzustellen, dass der Inhalt korrekt und verständlich wiedergegeben wird.

#### Motorische Barrieren

Menschen mit motorischen Einschränkungen können möglicherweise keine Maus benutzen. Sie sind auf alternative Eingabemethoden angewiesen, allen voran die Tastaturbedienung.

**1. Fehlende Tastaturbedienbarkeit:** Jede interaktive Komponente deiner Webseite – jeder Link, jeder Button, jedes Formularfeld – muss allein mit der Tastatur erreichbar und bedienbar sein. Mit der `Tab`-Taste springt man von einem Element zum nächsten, mit `Shift + Tab` zurück. `Enter` löst in der Regel eine Aktion aus (wie ein Klick) oder sendet ein Formular ab, und die Leertaste aktiviert Checkboxen oder Buttons.

Eine häufige Barriere entsteht durch selbstgebaute Widgets mit JavaScript, die nicht auf die Tastatur reagieren. Ein mit einem `<div>` und einem Klick-Event erstellter "Button" ist für die Tastatur unsichtbar. Nutze stattdessen immer das native `<button>`-Element, das diese Funktionalität von Haus aus mitbringt.

**2. Unsichtbarer Fokus:** Wenn du mit der Tab-Taste durch eine Seite navigierst, hebt der Browser das aktuell fokussierte Element hervor, meist mit einem blauen Rahmen (dem "Fokus-Indikator"). Manche Designer finden diesen Rahmen unschön und entfernen ihn mit CSS (`outline: none;`). Das ist fatal für die Barrierefreiheit. Es ist, als würde man versuchen, mit verbundenen Augen mit der Maus zu navigieren – man weiß nie, wo der Cursor gerade ist. Der Fokus-Indikator muss immer sichtbar sein.

**3. Hover-Fallen:** Inhalte oder Menüs, die ausschließlich bei einem Mouse-Hover-Effekt erscheinen, sind für Tastaturnutzer unerreichbar. Jede Information, die über Hover zugänglich ist, muss auch über den Tastaturfokus erreichbar sein.

#### Kognitive Barrieren

Dies ist vielleicht der komplexeste Bereich, da er Menschen mit sehr unterschiedlichen Bedürfnissen betrifft, zum Beispiel Menschen mit Lernschwierigkeiten, ADHS oder Konzentrationsstörungen.

**1. Komplexe Sprache und unklare Navigation:** Lange, verschachtelte Sätze, Fachjargon und eine unlogische Seitenstruktur können eine enorme Hürde darstellen. Klare, einfache Sprache und eine konsistente, vorhersehbare Navigation helfen allen, sind aber für Menschen mit kognitiven Einschränkungen essenziell.

**2. Ablenkungen und Zeitdruck:** Sich schnell bewegende Karussells, automatisch startende Videos oder blinkende Werbebanner können extrem ablenkend und überfordernd sein. Gib deinen Nutzern die Kontrolle und lass sie selbst entscheiden, wann sie eine Animation starten oder ein Video abspielen.

Ähnliches gilt für Zeitlimits. Wenn ein Formular nach fünf Minuten Inaktivität automatisch zurückgesetzt wird, kann das für Menschen, die mehr Zeit zum Lesen und Verstehen benötigen, sehr frustrierend sein. Wenn ein Zeitlimit unumgänglich ist, sollte es eine Möglichkeit geben, es zu verlängern.

Barrieren zu erkennen, ist der erste und wichtigste Schritt auf dem Weg zu einem inklusiveren Web. Es erfordert einen bewussten Perspektivwechsel – weg von der Annahme, dass alle Nutzer so sind wie wir, und hin zu dem Verständnis, dass das Web für eine immense Vielfalt von Menschen funktionieren muss. Jede Barriere, die du findest und abbaust, ist wie das Anbringen einer weiteren Rampe, die mehr Menschen den Zugang zu deiner digitalen Welt ermöglicht.
