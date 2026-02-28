# Performance-Review

### Performance-Review: Mehr als nur korrekter Code

Ein Code-Review stellt sicher, dass dein Code funktioniert, lesbar ist und den Team-Standards entspricht. Aber funktioniert er auch *schnell*? Lädt die Seite zügig, auch auf einem älteren Smartphone mit einer wackeligen 3G-Verbindung? Reagiert die Benutzeroberfläche flüssig, wenn der Nutzer damit interagiert? Genau diese Fragen beantwortet ein Performance-Review.

Es ist eine spezielle Form des Code-Reviews, die sich ausschließlich darauf konzentriert, wie sich deine Änderungen auf die Lade- und Ausführungsgeschwindigkeit der Webseite auswirken. Während ein normaler Review nach logischen Fehlern oder Stil-Verstößen sucht, jagt der Performance-Review Millisekunden. Er betrachtet deinen Code nicht als isolierte Anweisungen, sondern als Teil eines komplexen Systems, das Ressourcen verbraucht: Netzwerkbandbreite, CPU-Zyklen und Arbeitsspeicher.

In der heutigen, von Ungeduld geprägten Web-Welt ist Performance kein "Nice-to-have" mehr, sondern ein entscheidendes Feature. Eine langsame Seite frustriert Nutzer, schadet deinem Ranking in Suchmaschinen und kann sich direkt auf den Geschäftserfolg auswirken. Ein Performance-Review ist also eine essenzielle Praktik der Qualitätssicherung, um sicherzustellen, dass dein Code nicht nur *richtig*, sondern auch *effizient* ist.

#### Die drei Säulen der Web-Performance

Um einen Performance-Review strukturiert anzugehen, kannst du dich an drei Hauptbereichen orientieren, die den größten Einfluss auf die gefühlte Geschwindigkeit einer Webseite haben: das Netzwerk, das Rendering und die JavaScript-Ausführung.

##### 1. Das Netzwerk – Der Flaschenhals des Webs

Jede Ressource, die deine Webseite benötigt – HTML, CSS, JavaScript, Bilder, Schriftarten – muss über das Netzwerk vom Server zum Browser des Nutzers transportiert werden. Jede einzelne Anfrage kostet Zeit. Daher lauten die obersten Gebote: Reduziere die Anzahl der Anfragen und minimiere die Größe jeder einzelnen Anfrage.

**Bilder: Die größten Datensünder**

Bilder sind oft für den größten Teil des heruntergeladenen Datenvolumens verantwortlich. Hier gibt es enormes Optimierungspotenzial.

*   **Moderne Formate:** Verwendest du noch JPEGs und PNGs, wo du moderne Formate wie WebP oder sogar AVIF einsetzen könntest? Diese bieten bei gleicher visueller Qualität eine deutlich geringere Dateigröße. Der `<picture>`-Tag ist dein Freund, um verschiedene Formate als Fallback anzubieten.
*   **Responsive Bilder:** Liefert dein Code ein riesiges 4K-Desktop-Hintergrundbild an ein kleines Smartphone aus? Das ist pure Verschwendung von Daten und Zeit. Mit dem `srcset`-Attribut im `<img>`-Tag kann der Browser die am besten passende Bildgröße für das jeweilige Gerät auswählen.

    ```html
    <img src="small.jpg"
         srcset="medium.jpg 1000w, large.jpg 2000w"
         sizes="(min-width: 900px) 800px, 100vw"
         alt="Eine Beschreibung des Bildes.">
    ```

*   **Lazy Loading:** Müssen alle Bilder sofort geladen werden, auch die, die sich weit unten auf der Seite befinden ("below the fold")? Das `loading="lazy"`-Attribut ist eine einfache, native HTML-Lösung, die dem Browser sagt, er soll Bilder erst dann laden, wenn sie in den sichtbaren Bereich des Nutzers scrollen.

    ```html
    <img src="hero-image.jpg" loading="lazy" alt="Ein Bild, das erst später geladen wird.">
    ```

**CSS und JavaScript: Weniger ist mehr**

Auch bei Text-basierten Assets wie CSS und JavaScript kannst du ansetzen.

*   **Minimierung:** Sind deine CSS- und JS-Dateien "minifiziert"? Das bedeutet, dass alle unnötigen Zeichen wie Leerzeichen, Zeilenumbrüche und Kommentare entfernt wurden, um die Dateigröße zu reduzieren. Dies ist heutzutage ein Standardprozess in jedem modernen Build-Tool.
*   **Code-Splitting:** Lädst du eine riesige `app.js`-Datei, die den Code für die gesamte Anwendung enthält, obwohl der Nutzer auf der Startseite nur 10 % davon benötigt? Moderne Frameworks und Bundler ermöglichen "Code-Splitting", bei dem der Code in kleinere Chunks aufgeteilt wird, die nur bei Bedarf nachgeladen werden.

##### 2. Rendering – Wie der Browser die Seite zeichnet

Sobald die Ressourcen beim Browser ankommen, beginnt dieser, die Seite zu "zeichnen". Dieser Prozess, der sogenannte "Critical Rendering Path", kann durch unachtsamen Code blockiert werden, was zu einer leeren, weißen Seite führt, obwohl die Daten längst da sind.

**Render-blockierende Ressourcen entschärfen**

Der Browser liest dein HTML von oben nach unten. Trifft er auf bestimmte Tags, hält er inne und wartet, bis die verlinkte Ressource heruntergeladen und verarbeitet wurde.

*   **CSS:** CSS im `<head>` ist per Definition render-blockierend. Das ist auch gut so, denn der Browser soll nicht anfangen, ungestylten Inhalt darzustellen, nur um ihn kurz darauf neu zu formatieren ("Flash of Unstyled Content"). Deine Aufgabe im Review ist es sicherzustellen, dass nur das *absolut notwendige* CSS für den ersten sichtbaren Bereich ("Above the Fold") im `<head>` blockierend geladen wird. Zusätzliches CSS für andere Seitenbereiche oder Interaktionen kann asynchron nachgeladen werden.
*   **JavaScript:** Traditionell platzierte `<script>`-Tags im `<head>` sind die schlimmsten Performance-Killer. Der Browser stoppt das Parsen des HTML komplett, lädt das Skript herunter und führt es aus, bevor er auch nur eine Zeile weiter liest. Die Lösung liegt in zwei Attributen: `defer` und `async`.

    *   `defer`: Das Skript wird parallel zum HTML-Parsing heruntergeladen und erst dann ausgeführt, wenn das gesamte HTML-Dokument fertig geparst ist, aber noch vor dem `DOMContentLoaded`-Event. Die Reihenfolge der Skripte bleibt erhalten. Dies ist die beste Wahl für die meisten Skripte, die das DOM manipulieren.

        ```html
        <script src="mein-skript.js" defer></script>
        ```

    *   `async`: Das Skript wird ebenfalls parallel heruntergeladen, aber sofort ausgeführt, sobald es verfügbar ist. Dabei wird das HTML-Parsing unterbrochen. Die Reihenfolge der Ausführung ist nicht garantiert. Dies eignet sich für unabhängige Skripte, wie zum Beispiel Tracking- oder Werbe-Skripte.

        ```html
        <script src="tracking.js" async></script>
        ```

Ein guter Performance-Review prüft, ob Skripte ohne `async` oder `defer` im `<head>` wirklich zwingend notwendig sind. In 99 % der Fälle lautet die Antwort: Nein.

**Effiziente CSS-Selektoren**

Dies ist oft eine Mikro-Optimierung, aber in komplexen Anwendungen relevant. Der Browser wertet CSS-Selektoren von rechts nach links aus. Ein übermäßig spezifischer Selektor wie `div#main section.news article.featured > h2` ist für den Browser aufwendiger zu verarbeiten als ein einfacher Klassen-Selektor wie `.featured-headline`. Achte im Review auf unnötig verschachtelte oder überqualifizierte Selektoren.

##### 3. JavaScript-Ausführung – Die Last auf der CPU

Nach dem Laden und Rendern kommt die Interaktion. Hier spielt die Effizienz deines JavaScript-Codes eine entscheidende Rolle. Der Browser hat für die meisten Aufgaben, inklusive Rendering und der Reaktion auf Nutzereingaben, nur einen einzigen Thread, den "Main Thread". Wenn dein JavaScript diesen Thread für längere Zeit blockiert, friert die gesamte Seite ein.

**Teure Operationen identifizieren**

Achte im Review auf Code-Muster, die den Main Thread stark belasten können.

*   **DOM-Manipulation in Schleifen:** Jeder Zugriff auf das DOM (z. B. das Ändern eines Styles oder das Hinzufügen eines Elements) kann den Browser zu einem teuren Neu-Berechnen des Layouts ("Reflow") und Neu-Zeichnen ("Repaint") zwingen. Wenn du dies in einer langen Schleife tust, kann die Seite ruckeln. Besser ist es, Änderungen zu bündeln oder außerhalb des sichtbaren DOMs in einem DocumentFragment vorzunehmen und erst am Ende gesammelt einzufügen.
*   **Event-Handler für häufige Events:** Events wie `scroll`, `resize` oder `mousemove` können dutzende Male pro Sekunde ausgelöst werden. Wenn der zugehörige Event-Handler eine aufwendige Berechnung durchführt, wird der Browser überlastet. Techniken wie "Debouncing" (eine Funktion erst ausführen, nachdem eine bestimmte Zeit lang kein Event mehr ausgelöst wurde) oder "Throttling" (eine Funktion nur alle x Millisekunden ausführen) sind hier essenziell.

**Der menschliche Faktor im Performance-Review**

Ein Performance-Review ist keine rein mechanische Checkliste. Es geht auch um eine Haltung und eine Kultur im Team.

*   **Performance als Feature verstehen:** Behandle Performance nicht als nachträgliche Optimierung, sondern als grundlegende Anforderung an jede neue Funktion. Frage bei jeder Änderung: "Was sind die Performance-Implikationen davon?"
*   **Empathie für den Nutzer:** Denke nicht nur an deine schnelle Entwicklermaschine mit Glasfaseranschluss. Versetze dich in die Lage eines Nutzers mit einem Mittelklasse-Handy in einem Gebiet mit schlechtem Empfang. Tools wie die Entwicklertools im Browser erlauben dir, Netzwerk- und CPU-Geschwindigkeiten zu drosseln, um diese Bedingungen zu simulieren.
*   **Pragmatismus statt Dogma:** Nicht jede Millisekunde ist es wert, gejagt zu werden. Es ist immer ein Kompromiss zwischen Entwicklungsaufwand, Code-Komplexität und dem tatsächlichen Nutzen für den Nutzer. Ein Performance-Review sollte pragmatische Lösungen finden, nicht theoretisch perfekte, aber unpraktikable.

Indem du diese Aspekte in deine regulären Code-Reviews integrierst, schaffst du nicht nur Code, der funktioniert, sondern Erlebnisse, die deine Nutzer begeistern. Du baust Webseiten, die sich schnell, reaktionsschnell und einfach gut anfühlen – und das ist ein Qualitätsmerkmal, das man nicht hoch genug einschätzen kann.
