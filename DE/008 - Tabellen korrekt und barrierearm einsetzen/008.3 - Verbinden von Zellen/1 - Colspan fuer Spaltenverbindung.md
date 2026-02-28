# colspan für Spaltenverbindung

# Zellen über Spalten verbinden: Das `colspan`-Attribut

Manchmal reicht eine einfache, gitterartige Tabelle nicht aus, um Daten sinnvoll darzustellen. Stell dir einen Stundenplan vor: Vielleicht gibt es einen großen Block am Vormittag für ein Projekt, das sich über mehrere Stunden erstreckt. Oder denk an eine Preisliste, bei der eine Überschrift wie „Sonderangebote“ für mehrere Produkte gleichzeitig gilt. In solchen Fällen möchtest du, dass eine einzelne Zelle den Platz von mehreren Spalten einnimmt.

Genau hierfür wurde in HTML das `colspan`-Attribut geschaffen. Es ist ein einfaches, aber mächtiges Werkzeug, mit dem du die Struktur deiner Tabellen an die logische Gliederung deiner Daten anpassen kannst. Der Name selbst ist eine Abkürzung für „column span“, also „Spalten-Spannweite“. Du weist damit eine einzelne Tabellenzelle (`<td>` oder `<th>`) an, sich horizontal über eine bestimmte Anzahl von Spalten auszudehnen.

### Die grundlegende Funktionsweise von `colspan`

Die Anwendung des Attributs ist denkbar einfach. Du fügst es direkt in den öffnenden Tag einer Header- (`<th>`) oder Datenzelle (`<td>`) ein und gibst ihm einen numerischen Wert. Dieser Wert entspricht der Anzahl der Spalten, die diese Zelle überspannen soll.

Ein Beispiel: `colspan="3"` bedeutet, dass die Zelle den Platz von drei regulären Spalten einnehmen wird.

Schauen wir uns das an einem simplen Beispiel an. Wir beginnen mit einer normalen 2x3-Tabelle (zwei Zeilen, drei Spalten):

```html
<table>
  <caption>Einfacher Monatsplan</caption>
  <thead>
    <tr>
      <th>Monat</th>
      <th>Einnahmen</th>
      <th>Ausgaben</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Januar</td>
      <td>3.000 €</td>
      <td>2.500 €</td>
    </tr>
  </tbody>
</table>
```

Diese Tabelle ist klar strukturiert. Was aber, wenn wir eine übergeordnete Überschrift für die Finanzdaten „Einnahmen“ und „Ausgaben“ erstellen wollen? Wir könnten eine neue Zeile hinzufügen und dort `colspan` einsetzen.

```html
<table>
  <caption>Monatsplan mit gruppierter Überschrift</caption>
  <thead>
    <tr>
      <th rowspan="2">Monat</th>
      <th colspan="2">Finanzübersicht</th>
    </tr>
    <tr>
      <th>Einnahmen</th>
      <th>Ausgaben</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Januar</td>
      <td>3.000 €</td>
      <td>2.500 €</td>
    </tr>
  </tbody>
</table>
```

Analysieren wir, was hier passiert ist:

1.  **Die erste Header-Zeile (`<tr>`):**
    *   Die Zelle „Monat“ hat das Attribut `rowspan="2"` bekommen, damit sie sich über zwei Zeilen erstreckt (mehr dazu im nächsten Kapitel). Für den Moment ist nur wichtig, dass sie ihren Platz in beiden Header-Zeilen einnimmt.
    *   Die entscheidende Zelle ist `<th colspan="2">Finanzübersicht</th>`. Sie erhält die Anweisung, sich über zwei Spalten auszudehnen. Sie nimmt also den Platz ein, der normalerweise für die Spalten „Einnahmen“ und „Ausgaben“ vorgesehen wäre.

2.  **Die zweite Header-Zeile (`<tr>`):**
    *   Da die Zelle „Monat“ aus der ersten Zeile bereits den Platz in der ersten Spalte dieser zweiten Zeile belegt (dank `rowspan`), müssen wir hier nur noch die Zellen für die übrigen Spalten definieren.
    *   Das sind `<th>Einnahmen</th>` und `<th>Ausgaben</th>`. Diese beiden Zellen füllen nun den Raum unterhalb der von „Finanzübersicht“ überspannten Fläche.

### Das wichtigste Prinzip: Zellen müssen weichen

Der häufigste Fehler bei der Verwendung von `colspan` ist das Vergessen, die „überflüssigen“ Zellen zu entfernen. HTML-Tabellen basieren auf einem strengen Raster. Jede Zeile muss grundsätzlich die gleiche Anzahl von Spalten haben, um korrekt dargestellt zu werden. Wenn du eine Zelle mit `colspan="2"` versiehst, teilst du dem Browser mit: „Diese Zelle belegt ihren eigenen Platz UND den Platz der nächsten Zelle in dieser Zeile.“

Das bedeutet im Umkehrschluss, dass du die nächste Zelle in deinem HTML-Code für diese Zeile weglassen musst. Wenn du es nicht tust, entsteht ein Überschuss. Die überschüssige Zelle wird dann aus dem Raster geschoben, was die gesamte Tabellenstruktur zerstört.

Stell dir vor, wir hätten im obigen Beispiel den Code fälschlicherweise so geschrieben:

```html
<!-- FALSCHES BEISPIEL: Zu viele Zellen in der ersten Header-Zeile -->
<thead>
  <tr>
    <th rowspan="2">Monat</th>
    <th colspan="2">Finanzübersicht</th>
    <th>Einnahmen</th> <!-- DIESE ZELLE IST ZU VIEL! -->
  </tr>
  <tr>
    <!-- ... -->
  </tr>
</thead>
```

Der Browser würde versuchen, eine Zelle für „Monat“, eine Zelle für „Finanzübersicht“ (die zwei Spalten breit ist) *und* eine weitere Zelle für „Einnahmen“ in die erste Zeile zu setzen. Das ergibt insgesamt vier Spalteneinheiten in einer Zeile, die eigentlich nur für drei Spalten konzipiert ist. Das Layout bricht zusammen.

Die Regel lautet also: **Für jede Einheit, die `colspan` über 1 liegt, musst du eine `<td>`- oder `<th>`-Zelle aus derselben Zeile entfernen.**

*   `colspan="2"`: Entferne eine nachfolgende Zelle.
*   `colspan="3"`: Entferne zwei nachfolgende Zellen.
*   `colspan="4"`: Entferne drei nachfolgende Zellen.
*   ... und so weiter.

### Ein praktisches Anwendungsbeispiel: Ein Wochenplan

Lass uns einen etwas komplexeren Wochenplan erstellen, um die Nützlichkeit von `colspan` zu verdeutlichen. Wir wollen den Tag in „Vormittag“ und „Nachmittag“ unterteilen, wobei jeder dieser Blöcke mehrere konkrete Zeitfenster umfasst.

Unsere Tabelle soll folgende Struktur haben:
*   Eine oberste Header-Zeile mit den Blöcken „Vormittag“ und „Nachmittag“.
*   Eine zweite Header-Zeile mit den spezifischen Uhrzeiten.
*   Datenzeilen für die Wochentage.

```html
<table>
  <caption>Wochenplan für Projekt X</caption>
  <thead>
    <tr>
      <!-- Leere Zelle oben links für die Wochentage -->
      <th></th> 
      <!-- "Vormittag" soll 3 Spalten überspannen (9, 10, 11 Uhr) -->
      <th colspan="3">Vormittag</th>
      <!-- "Nachmittag" soll 3 Spalten überspannen (13, 14, 15 Uhr) -->
      <th colspan="3">Nachmittag</th>
    </tr>
    <tr>
      <th>Wochentag</th>
      <th>9:00</th>
      <th>10:00</th>
      <th>11:00</th>
      <th>13:00</th>
      <th>14:00</th>
      <th>15:00</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Montag</th>
      <td colspan="2">Konzept-Meeting</td>
      <td>Brainstorming</td>
      <td>Umsetzung</td>
      <td colspan="2">Code-Review</td>
    </tr>
    <tr>
      <th>Dienstag</th>
      <td>Design-Phase</td>
      <td colspan="2">Prototyping</td>
      <td colspan="3">User-Testing</td>
    </tr>
  </tbody>
</table>
```

In diesem Beispiel siehst du `colspan` gleich mehrfach im Einsatz:

1.  **Im Tabellenkopf (`<thead>`):**
    *   Die erste Zeile enthält nur vier `<th>`-Elemente. Die erste Zelle ist leer und dient als Platzhalter. Die zweite Zelle (`Vormittag`) überspannt mit `colspan="3"` die drei Spalten für die Uhrzeiten darunter. Die dritte Zelle (`Nachmittag`) tut dasselbe. Ohne `colspan` hätten wir hier eine unlogische Struktur.
    *   Die zweite Zeile definiert dann die insgesamt sieben Spalten der Tabelle: Eine für den Wochentag und sechs für die Uhrzeiten.

2.  **Im Tabellenkörper (`<tbody>`):**
    *   Am Montag findet ein „Konzept-Meeting“ statt, das von 9:00 bis 11:00 Uhr dauert. Anstatt die Zelle zu wiederholen, verbinden wir die beiden Zellen für 9:00 und 10:00 Uhr mit `colspan="2"`. Dadurch wird der Eintrag für „Brainstorming“ in die nächste freie Spalte (11:00 Uhr) verschoben.
    *   Am Dienstag erstreckt sich das „User-Testing“ über den gesamten Nachmittag. Mit `colspan="3"` belegt diese eine Zelle den gesamten Platz von 13:00 bis 16:00 Uhr. Die Zeile für Dienstag enthält daher nur drei `<td>`-Elemente nach dem `<th>` für den Wochentag, obwohl die Tabelle insgesamt sieben Spalten hat.

### `colspan` und Barrierefreiheit: Das `scope`-Attribut

Wenn du Zellen verbindest, kann das für Nutzer von Screenreadern verwirrend werden. Ein Screenreader liest eine Tabelle normalerweise Zelle für Zelle vor und nennt dabei die zugehörige Spalten- und Zeilenüberschrift. Bei einer verbundenen Zelle ist diese Zuordnung nicht mehr eindeutig.

Um diese Verbindung für assistive Technologien verständlich zu machen, solltest du das `scope`-Attribut verwenden. Wenn eine Header-Zelle (`<th>`) mehrere Spalten überspannt, ist sie nicht mehr der Header für eine einzelne Spalte, sondern für eine ganze Spaltengruppe.

Dafür gibt es den Wert `scope="colgroup"`.

Nehmen wir unser Wochenplan-Beispiel und machen es barriereärmer:

```html
<table>
  <caption>Wochenplan für Projekt X (barrierearm)</caption>
  <thead>
    <tr>
      <th></th> 
      <th colspan="3" scope="colgroup">Vormittag</th>
      <th colspan="3" scope="colgroup">Nachmittag</th>
    </tr>
    <tr>
      <th scope="col">Wochentag</th>
      <th scope="col">9:00</th>
      <th scope="col">10:00</th>
      <!-- ... und so weiter für die restlichen Header ... -->
    </tr>
  </thead>
  <!-- ... -->
</table>
```

Durch `scope="colgroup"` auf den `<th>`-Elementen „Vormittag“ und „Nachmittag“ weiß ein Screenreader nun: „Aha, diese Zelle ist die Überschrift für die folgende Gruppe von Spalten.“ Wenn der Screenreader dann eine Datenzelle im Vormittagsbereich vorliest, kann er die Information „Vormittag, 9:00, Konzept-Meeting“ ausgeben. Diese zusätzliche semantische Information ist ein kleiner Aufwand im Code, aber ein riesiger Gewinn für die Zugänglichkeit.

`colspan` ist also weit mehr als nur ein Werkzeug für das visuelle Design. Es ist ein fundamentaler Baustein, um die logische Struktur von tabellarischen Daten in HTML abzubilden. Wenn du das Prinzip des Zellenentfernens verinnerlicht hast und an die semantische Auszeichnung mit `scope` denkst, kannst du auch komplexe, aber dennoch verständliche und barrierearme Tabellen erstellen.
