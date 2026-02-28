# Best Practices für mobile Darstellung

### Best Practices für mobile Darstellung

Tabellen sind fantastische Werkzeuge, um strukturierte Daten darzustellen. Sie bringen Ordnung in komplexe Informationen und machen Vergleiche auf einen Blick möglich. Auf einem großen Desktop-Monitor ist das eine wahre Freude. Doch was passiert, wenn sich der verfügbare Platz drastisch reduziert, wie auf dem Bildschirm eines Smartphones? Hier wird die klassische Tabelle schnell zu einem Problemkind des Webdesigns.

Die Herausforderung ist offensichtlich: Tabellen sind von Natur aus breit. Wenn eine Tabelle mehr Spalten hat, als auf einen schmalen Bildschirm passen, bricht das Layout. Der Browser versucht, das Beste daraus zu machen, aber das Ergebnis ist selten optimal. Entweder werden die Inhalte in den Zellen unleserlich klein gequetscht, oder die Tabelle sprengt die Grenzen der Seite und erzwingt unschönes horizontales Scrollen. Beides führt zu einer schlechten Benutzererfahrung. Dein Ziel ist es, Tabellen so zu gestalten, dass sie auf jedem Gerät gut aussehen und benutzbar bleiben. Schauen wir uns die gängigsten und effektivsten Lösungsansätze an.

#### Die pragmatische Lösung: Kontrolliertes horizontales Scrollen

Manchmal ist der einfachste Weg auch ein vollkommen legitimer. Anstatt die Tabellenstruktur aufzulösen, kannst du der Tabelle erlauben, horizontal zu scrollen, aber innerhalb eines definierten Bereichs. So bleibt das restliche Seitenlayout intakt und der Nutzer kann gezielt durch die Tabellendaten wischen.

Der Trick besteht darin, die Tabelle in ein `div`-Element zu packen und diesem Container die Eigenschaft `overflow-x: auto;` zu geben.

**HTML-Struktur:**

```html
<div class="table-wrapper">
  <table>
    <!-- Dein Tabelleninhalt hier -->
    <thead>
      <tr>
        <th>Produkt-ID</th>
        <th>Name</th>
        <th>Kategorie</th>
        <th>Preis</th>
        <th>Lagerbestand</th>
        <th>Bewertung</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>1024</td>
        <td>Ergonomische Maus</td>
        <td>Computerzubehör</td>
        <td>79,99 €</td>
        <td>150</td>
        <td>4.8 / 5.0</td>
      </tr>
      <!-- weitere Zeilen -->
    </tbody>
  </table>
</div>
```

**CSS-Styling:**

```css
.table-wrapper {
  overflow-x: auto;
  -webkit-overflow-scrolling: touch; /* Sorgt für flüssiges Scrollen auf iOS */
}

table {
  width: 100%;
  border-collapse: collapse;
}

/* Optional: Ein visueller Hinweis, dass gescrollt werden kann */
@media (max-width: 768px) {
  .table-wrapper {
    border-right: 1px solid #ccc; /* Ein dezenter Rand rechts */
  }
}
```

Diese Methode ist besonders nützlich, wenn der tabellarische Zusammenhang der Daten entscheidend ist – also wenn der Nutzer Zeilen und Spalten direkt miteinander vergleichen muss. Der große Vorteil ist die Einfachheit in der Umsetzung. Der Nachteil: Nutzer müssen aktiv scrollen und können nicht alle Informationen auf einen Blick erfassen. Es ist ein guter Kompromiss, aber nicht immer die eleganteste Lösung.

#### Die selektive Lösung: Spalten priorisieren und ausblenden

Nicht alle Informationen in einer Tabelle sind gleich wichtig. Auf einem kleinen Bildschirm kannst du dich auf das Wesentliche konzentrieren und weniger wichtige Spalten einfach ausblenden. Dieser Ansatz erfordert eine inhaltliche Entscheidung: Welche Daten sind für den Nutzer auf dem Smartphone unverzichtbar und welche sind nur "nice to have"?

Du setzt dies mit Media Queries um. Für mobile Ansichten definierst du, welche Spalten mit `display: none;` ausgeblendet werden.

**HTML (bleibt unverändert):**

```html
<table>
  <thead>
    <tr>
      <th>Produkt-ID</th>
      <th class="priority-1">Name</th>
      <th class="priority-3">Kategorie</th>
      <th class="priority-1">Preis</th>
      <th class="priority-2">Lagerbestand</th>
      <th class="priority-3">Bewertung</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1024</td>
      <td class="priority-1">Ergonomische Maus</td>
      <td class="priority-3">Computerzubehör</td>
      <td class="priority-1">79,99 €</td>
      <td class="priority-2">150</td>
      <td class="priority-3">4.8 / 5.0</td>
    </tr>
    <!-- weitere Zeilen -->
  </tbody>
</table>
```

Hier haben wir den Spalten mit Klassen Prioritäten zugewiesen. `priority-1` ist am wichtigsten, `priority-3` am unwichtigsten.

**CSS-Styling:**

```css
/* Standard-Styling für alle Spalten */
th, td {
  padding: 8px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

/* Tablet-Größe: Spalten mit niedrigster Priorität ausblenden */
@media (max-width: 768px) {
  .priority-3 {
    display: none;
  }
}

/* Smartphone-Größe: Auch Spalten mit mittlerer Priorität ausblenden */
@media (max-width: 480px) {
  .priority-2 {
    display: none;
  }
}
```

Dieser Ansatz ist sehr effektiv, um die Tabelle übersichtlich zu halten. Bedenke aber, dass mit `display: none;` ausgeblendete Inhalte auch für Screenreader nicht mehr verfügbar sind. Stelle also sicher, dass du keine für das Verständnis absolut kritischen Informationen entfernst.

#### Die transformative Lösung: Die Tabelle "stapeln" (Stacking)

Der vielleicht eleganteste und benutzerfreundlichste Ansatz für komplexe Tabellen ist die Umwandlung des Layouts auf kleinen Bildschirmen. Statt einer horizontalen Anordnung von Zellen in einer Zeile, stapelst du die Zellen jeder Zeile vertikal untereinander. Jede Zeile der ursprünglichen Tabelle wird so zu einer Art "Karteikarte".

Damit der Kontext nicht verloren geht, musst du die Spaltenüberschrift für jede Zelle erneut einblenden. Dies gelingt wunderbar mit CSS-Pseudo-Elementen (`::before`) und `data-`Attributen im HTML.

**HTML-Struktur mit `data-`Attributen:**

Die `data-`Attribute sind hier der Schlüssel. Sie spiegeln den Inhalt der Kopfzeile wider und machen ihn für unser CSS zugänglich.

```html
<table>
  <thead>
    <tr>
      <th>Produkt-ID</th>
      <th>Name</th>
      <th>Kategorie</th>
      <th>Preis</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-label="Produkt-ID">1024</td>
      <td data-label="Name">Ergonomische Maus</td>
      <td data-label="Kategorie">Computerzubehör</td>
      <td data-label="Preis">79,99 €</td>
    </tr>
    <tr>
      <td data-label="Produkt-ID">1025</td>
      <td data-label="Name">Mechanische Tastatur</td>
      <td data-label="Kategorie">Computerzubehör</td>
      <td data-label="Preis">129,00 €</td>
    </tr>
  </tbody>
</table>
```

**CSS-Styling für den Stacking-Effekt:**

```css
@media (max-width: 600px) {
  /* Zuerst die ursprünglichen Kopfzeilen ausblenden */
  table thead {
    display: none;
  }

  /* Die Tabellen-Elemente auf Block-Layout umstellen */
  table, table tbody, table tr, table td {
    display: block;
    width: 100%;
  }

  /* Jede Zeile wird zu einer Karte */
  table tr {
    margin-bottom: 15px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }

  /* Jede Zelle bekommt etwas Platz */
  table td {
    padding: 10px;
    text-align: right; /* Den Dateninhalt rechts ausrichten */
    position: relative; /* Wichtig für die Positionierung des Labels */
    border-bottom: 1px solid #eee;
  }

  table td:last-child {
    border-bottom: 0;
  }

  /* Das ist die Magie: Das Label aus dem data-Attribut einfügen */
  table td::before {
    content: attr(data-label); /* Holt den Text aus dem data-label Attribut */
    position: absolute;
    left: 10px;
    font-weight: bold;
    text-align: left;
  }
}
```

Mit diesem CSS passiert auf Bildschirmen unter 600px Breite Folgendes:

1.  Die `<thead>` wird versteckt, da wir sie nicht mehr benötigen.
2.  `<tr>` und `<td>` werden zu Block-Elementen, sodass sie die volle Breite einnehmen und sich untereinander anordnen.
3.  Jede `<tr>` wird optisch zu einer eigenen Karte.
4.  Das `::before`-Pseudo-Element fügt vor dem Inhalt jeder Zelle (`<td>`) den Text aus dem `data-label`-Attribut ein.
5.  Durch die Ausrichtung (Label links, Dateninhalt rechts) entsteht eine klare, lesbare Schlüssel-Wert-Paar-Struktur.

Dieser Ansatz erfordert etwas mehr Vorbereitung im HTML, belohnt dich aber mit einer extrem übersichtlichen und nativ anfühlenden mobilen Darstellung. Ein wichtiger Hinweis zur Barrierefreiheit: Inhalte, die über CSS `content` eingefügt werden, werden von den meisten Screenreadern ignoriert. Da die ursprüngliche, semantisch korrekte Tabellenstruktur aber weiterhin im DOM vorhanden ist (lediglich visuell anders dargestellt), können assistive Technologien die Tabelle in der Regel trotzdem korrekt interpretieren. Das ist ein großer Vorteil gegenüber dem reinen Ausblenden von Spalten.

#### Welche Methode ist die richtige für dich?

Es gibt keine universelle Antwort. Die Wahl der richtigen Technik hängt immer vom Kontext ab:

*   **Für einfache Datentabellen, bei denen der Zeilenvergleich im Vordergrund steht,** kann kontrolliertes **horizontales Scrollen** eine schnelle und ausreichende Lösung sein.
*   **Wenn du Tabellen mit vielen "Bonus-Informationen" hast,** ist das **Priorisieren und Ausblenden von Spalten** eine sehr effektive Methode, um die mobile Ansicht aufzuräumen.
*   **Für komplexe Tabellen mit vielen Spalten, bei denen die Details jeder einzelnen Zeile wichtig sind,** ist der **Stacking-Ansatz** fast immer die beste Wahl für eine optimale User Experience.

Du kannst diese Techniken auch kombinieren. Blende beispielsweise auf Tablets nur die unwichtigsten Spalten aus und wechsle erst auf Smartphones zum Stacking-Layout. Experimentiere und teste deine Tabellen immer auf echten Geräten. So stellst du sicher, dass deine Daten nicht nur gut strukturiert, sondern auch auf jedem Bildschirm elegant und zugänglich präsentiert werden.
