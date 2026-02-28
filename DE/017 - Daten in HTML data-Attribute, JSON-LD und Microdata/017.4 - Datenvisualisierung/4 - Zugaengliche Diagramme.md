# Zugängliche Diagramme

### Zugängliche Diagramme: Mehr als nur bunte Bilder

Diagramme und Grafiken sind mächtige Werkzeuge. Sie können komplexe Daten auf einen Blick verständlich machen und trockene Zahlen in eine fesselnde Geschichte verwandeln. Ein gut gestaltetes Balkendiagramm zeigt einen Trend oft deutlicher als eine lange Tabelle. Eine anschauliche Infografik kann einen komplizierten Prozess in leicht verdauliche Schritte zerlegen. Für viele von uns ist diese visuelle Aufbereitung von Informationen eine enorme Hilfe.

Doch was passiert, wenn jemand deine Webseite besucht, der diese visuellen Informationen nicht oder nur eingeschränkt wahrnehmen kann? Für Menschen, die blind sind und einen Screenreader nutzen, ist ein Diagramm ohne textliche Entsprechung nur eine leere Stelle auf der Seite, oft angekündigt mit einem nichtssagenden "Bild". Für Personen mit Farbsehschwäche kann ein Tortendiagramm, das Informationen ausschließlich über Farben vermittelt, zu einem unentzifferbaren bunten Kreis werden. Und selbst für Nutzer mit einer langsamen Internetverbindung, bei denen Bilder nicht laden, geht die gesamte Information verloren.

Dein Ziel ist es daher, nicht einfach nur ein Diagramm zu erstellen, sondern die darin enthaltene *Information* für alle zugänglich zu machen. Die gute Nachricht ist: Du musst nicht auf visuell ansprechende Datenvisualisierungen verzichten. Du musst sie nur mit Bedacht und Empathie erstellen.

#### Die Grundlage: Textliche Alternativen

Der absolut grundlegendste Schritt, um ein Diagramm zugänglich zu machen, ist die Bereitstellung einer textlichen Alternative. Jedes visuelle Element, das Informationen transportiert, benötigt eine solche Entsprechung.

##### Für einfache Diagramme: Das `alt`-Attribut

Wenn dein Diagramm sehr einfach ist und seine Aussage in einem kurzen Satz zusammengefasst werden kann, ist das `alt`-Attribut deines `<img>`-Tags oft ausreichend.

Stell dir ein simples Tortendiagramm vor, das das Ergebnis einer Umfrage zeigt.

```html
<img src="umfrage-ergebnis.png" 
     alt="Tortendiagramm: 82% der Befragten stimmten mit Ja, 18% mit Nein.">
```

Ein Screenreader wird genau diesen Text vorlesen. Die Information ist vollständig übermittelt. Die visuelle Darstellung ist für sehende Nutzer da, die textliche für alle anderen.

##### Für komplexe Diagramme: Die Langbeschreibung

Die meisten Diagramme sind jedoch zu komplex für einen einzigen Satz. Ein Liniendiagramm, das die Umsatzentwicklung über zwölf Monate zeigt, oder ein Balkendiagramm, das die Bevölkerungszahlen von fünf Städten vergleicht, enthält zu viele Datenpunkte für ein kurzes `alt`-Attribut. Hier brauchst du eine ausführlichere Alternative.

Eine bewährte Methode ist die Kombination aus dem `<figure>`-Element und einer direkt sichtbaren Beschreibung oder einer Datentabelle.

Das `<figure>`-Element gruppiert das Diagramm semantisch mit seiner Beschriftung (`<figcaption>`). Die Beschriftung gibt einen kurzen Überblick, während die eigentlichen Daten in einer nachfolgenden, korrekt ausgezeichneten Tabelle bereitgestellt werden.

```html
<figure role="group" aria-labelledby="traffic-caption">
  <figcaption id="traffic-caption">
    Besucherzahlen der Webseite von Januar bis April 2023.
  </figcaption>
  
  <img src="traffic-chart.svg" alt="Ein Balkendiagramm, das die steigenden Besucherzahlen über vier Monate anzeigt. Die genauen Daten sind in der nachfolgenden Tabelle aufgeführt.">
  
  <table>
    <caption>Detaillierte Besucherzahlen von Januar bis April 2023</caption>
    <thead>
      <tr>
        <th scope="col">Monat</th>
        <th scope="col">Besucher</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Januar</td>
        <td>1.200</td>
      </tr>
      <tr>
        <td>Februar</td>
        <td>1.850</td>
      </tr>
      <tr>
        <td>März</td>
        <td>2.500</td>
      </tr>
      <tr>
        <td>April</td>
        <td>3.100</td>
      </tr>
    </tbody>
  </table>
</figure>
```

Analysieren wir diesen Aufbau:
1.  **`<figure>`:** Gruppiert alles zu einer logischen Einheit. Das `role="group"` und `aria-labelledby` helfen Screenreadern, die Beziehung zwischen der Überschrift und dem Inhalt zu verstehen.
2.  **`<figcaption>`:** Gibt der gesamten Figur einen Titel, der für alle sichtbar ist.
3.  **`<img>`:** Das `alt`-Attribut beschreibt nun nicht mehr jeden einzelnen Datenpunkt, sondern die Art des Diagramms und den allgemeinen Trend. Es verweist explizit auf die Tabelle für die Details. Das ist entscheidend, um Redundanz zu vermeiden.
4.  **`<table>`:** Dies ist die zugängliche Langbeschreibung. Eine semantisch korrekte Tabelle ist für Screenreader-Nutzer perfekt navigierbar. Sie können sich Zeilen, Spalten und Kopfzeilen vorlesen lassen und so die Daten in ihrem eigenen Tempo erfassen.

Dieser Ansatz ist robust, weil er allen Nutzern dient. Sehende Nutzer können das Diagramm schnell scannen und bei Bedarf die exakten Werte in der Tabelle nachlesen. Blinde Nutzer erhalten über die Tabelle den vollen Zugang zu allen Informationen.

#### Farbe allein ist nicht genug

Eine der häufigsten Barrieren bei Diagrammen ist die alleinige Verwendung von Farbe zur Unterscheidung von Datenreihen. Rund 8 % der Männer und 0,5 % der Frauen haben eine Rot-Grün-Sehschwäche. Für sie können rote und grüne Balken in einem Diagramm identisch aussehen.

Um dieses Problem zu lösen, musst du zusätzliche visuelle Unterscheidungsmerkmale einbauen:

*   **Muster und Texturen:** Statt nur auf Farben zu setzen, kannst du unterschiedliche Muster verwenden. Ein Balken kann schraffiert, einer gepunktet und ein dritter kariert sein.
*   **Direkte Beschriftungen:** Beschrifte Datenpunkte oder Segmente eines Tortendiagramms direkt, anstatt dich auf eine separate Legende zu verlassen. Das reduziert die kognitive Last für alle Nutzer, da sie nicht ständig zwischen Legende und Diagramm hin- und herspringen müssen.
*   **Formen und Symbole:** Verwende in Liniendiagrammen unterschiedliche Symbole (Kreise, Quadrate, Dreiecke) für die Datenpunkte der verschiedenen Linien.
*   **Hoher Kontrast:** Achte immer darauf, dass die Farben, die du verwendest, ausreichende Kontrastverhältnisse zueinander und zum Hintergrund haben. Die WCAG (Web Content Accessibility Guidelines) geben hier klare Mindestanforderungen vor.

#### SVG: Die flexible und zugängliche Wahl

Für Diagramme im Web sind Vektorgrafiken (SVG) oft die bessere Wahl als Rastergrafiken (PNG, JPG). SVGs bestehen aus XML-Code, nicht aus Pixeln. Das bringt enorme Vorteile für die Barrierefreiheit.

Da ein SVG-Diagramm aus Code besteht, kannst du seine einzelnen Elemente direkt im DOM ansprechen und mit Informationen anreichern.

Innerhalb eines `<svg>`-Elements gibt es zwei spezielle Tags für Barrierefreiheit:
*   **`<title>`:** Ein kurzer, aussagekräftiger Titel, vergleichbar mit dem `alt`-Attribut eines Bildes.
*   **`<desc>`:** Eine längere Beschreibung, die mehr Details liefert.

```html
<svg role="img" aria-labelledby="chart-title chart-desc">
  <title id="chart-title">Umsatzentwicklung Q1</title>
  <desc id="chart-desc">
    Ein Liniendiagramm zeigt den Umsatzanstieg. Januar: 10.000€, Februar: 15.000€, März: 22.000€.
  </desc>
  
  <!-- Hier folgt der eigentliche SVG-Code für die Linien, Achsen etc. -->
  <g>
    <path d="..." />
    <text x="10" y="50">Januar</text>
    <!-- ... -->
  </g>
</svg>
```

In diesem Beispiel wird die SVG-Grafik durch `role="img"` als Bild für assistive Technologien gekennzeichnet. Mit `aria-labelledby` wird die Grafik mit dem Inhalt des `<title>`- und `<desc>`-Elements verknüpft. Ein Screenreader kann diese Informationen auslesen und dem Nutzer präsentieren.

Der große Vorteil von SVGs liegt darin, dass du sogar einzelne Teile des Diagramms (wie einen bestimmten Balken) interaktiv und zugänglich machen kannst. Du könntest einem Balken ein `tabindex="0"` geben, um ihn per Tastatur fokussierbar zu machen, und ihm via ARIA-Attribute eine genaue Beschreibung mitgeben (z.B. `aria-label="März: 2.500 Besucher"`).

#### Progressive Enhancement: Vom besten zum guten Fall

Der vielleicht eleganteste Ansatz für zugängliche Diagramme ist das Prinzip des "Progressive Enhancement". Die Idee ist, mit einer soliden, semantischen und für jeden zugänglichen Basis zu starten und diese dann für Nutzer, deren Browser es unterstützen, visuell zu verbessern.

Im Fall von Diagrammen ist die Basis eine gut strukturierte Datentabelle.

```html
<div class="chart-container">
  <table class="data-for-chart">
    <caption>Besucherzahlen der Webseite von Januar bis April 2023</caption>
    <thead>
      <tr>
        <th scope="col">Monat</th>
        <th scope="col">Besucher</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Januar</td>
        <td>1.200</td>
      </tr>
      <!-- ... weitere Monate -->
    </tbody>
  </table>
</div>
```

Diese Tabelle ist die "Wahrheit". Sie enthält alle Daten und ist von Natur aus zugänglich. Nun kommt JavaScript ins Spiel. Ein Skript kann diese Tabelle auslesen und dynamisch ein visuelles Diagramm (z.B. mit SVG oder HTML Canvas) erstellen und es auf der Seite einfügen. Oft wird die Tabelle selbst dann visuell versteckt (aber nicht aus dem DOM entfernt, damit Screenreader sie weiterhin finden können).

Der Vorteil dieser Methode ist enorm:
*   **Ausfallsicherheit:** Wenn JavaScript deaktiviert ist oder fehlschlägt, sehen die Nutzer immer noch die rohen Daten in der Tabelle. Die Information geht nie verloren.
*   **Single Source of Truth:** Du musst deine Daten nur an einer Stelle pflegen – in der HTML-Tabelle. Das Diagramm generiert sich daraus automatisch.
*   **Barrierefreiheit im Kern:** Die zugänglichste Form der Daten ist die Grundlage, nicht ein nachträglicher Gedanke.

Es gibt zahlreiche JavaScript-Bibliotheken (wie Chart.js, D3.js oder Highcharts), die diesen Ansatz unterstützen und dir helfen, aus einfachen Tabellen beeindruckende und gleichzeitig zugängliche Diagramme zu erstellen.

Die Erstellung zugänglicher Diagramme ist kein obskures Nischenthema, sondern ein zentraler Aspekt professioneller Webentwicklung. Es geht darum, respektvoll mit allen deinen Nutzern umzugehen und sicherzustellen, dass die Geschichten, die du mit deinen Daten erzählst, von jedem gehört und verstanden werden können – unabhängig davon, wie er oder sie auf deine Inhalte zugreift.
