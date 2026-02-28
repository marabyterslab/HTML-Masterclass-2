# rowspan für Zeilenverbindung

### Zellen über mehrere Zeilen verbinden: Das `rowspan`-Attribut

Manchmal stößt du bei der Erstellung von Tabellen auf eine besondere Anforderung: Eine einzelne Zelle soll sich nicht nur über eine Zeile erstrecken, sondern über mehrere. Stell dir einen Stundenplan vor, in dem ein zweistündiger Workshop stattfindet. In der Tabelle würde dieser Workshop zwei Zeilen (zwei Zeitblöcke) einnehmen. Oder denk an eine Liste von Teammitgliedern und ihren Projekten, bei der ein Team für mehrere aufeinanderfolgende Projekte zuständig ist. Anstatt den Teamnamen in jeder Zeile zu wiederholen, wäre es optisch ansprechender und logisch klarer, eine einzige Zelle für den Teamnamen zu haben, die sich über alle zugehörigen Projektzeilen erstreckt.

Genau für diesen Zweck gibt es in HTML das `rowspan`-Attribut. Es erlaubt dir, eine Tabellenzelle (`<td>`) oder eine Kopfzelle (`<th>`) vertikal über eine von dir definierte Anzahl von Zeilen auszudehnen.

#### Die Grundlagen von `rowspan`

Das `rowspan`-Attribut wird direkt in das `<td>`- oder `<th>`-Tag geschrieben, das du erweitern möchtest. Der Wert, den du dem Attribut zuweist, ist eine ganze Zahl. Diese Zahl gibt an, über wie viele Zeilen sich die Zelle erstrecken soll.

Ein einfaches Beispiel: `rowspan="2"` bedeutet, dass die Zelle ihre eigene Zeile plus die darunterliegende Zeile einnimmt. `rowspan="3"` erstreckt sich über drei Zeilen und so weiter.

Schauen wir uns das an einem ganz grundlegenden Beispiel an. Hier ist eine einfache 2x2-Tabelle ohne Zellverbindung:

```html
<table>
  <caption>Einfache 2x2-Tabelle</caption>
  <tr>
    <td>Zelle 1, Spalte 1</td>
    <td>Zelle 1, Spalte 2</td>
  </tr>
  <tr>
    <td>Zelle 2, Spalte 1</td>
    <td>Zelle 2, Spalte 2</td>
  </tr>
</table>
```

Visuell ergibt das ein sauberes Raster mit vier Zellen. Was passiert nun, wenn wir möchten, dass die erste Zelle in der ersten Spalte beide Zeilen einnimmt? Wir fügen der ersten Zelle das Attribut `rowspan="2"` hinzu.

Doch hier kommt der entscheidende Punkt, den du unbedingt verstehen musst: Wenn eine Zelle den Platz einer anderen Zelle einnimmt, darf diese andere Zelle nicht mehr im HTML-Code existieren. Du musst sie buchstäblich aus deinem Code entfernen.

In unserem Beispiel erstreckt sich "Zelle 1, Spalte 1" nach unten und besetzt den Platz von "Zelle 2, Spalte 1". Also müssen wir das `<td>`-Element für "Zelle 2, Spalte 1" aus der zweiten Zeile (`<tr>`) löschen.

Der korrekte Code sieht dann so aus:

```html
<table>
  <caption>Tabelle mit rowspan</caption>
  <tr>
    <td rowspan="2">Diese Zelle erstreckt sich über zwei Zeilen</td>
    <td>Zelle 1, Spalte 2</td>
  </tr>
  <tr>
    <!-- Diese Zeile hat jetzt nur noch eine Zelle! -->
    <!-- Die erste Zelle wird von der Zelle darüber eingenommen. -->
    <td>Zelle 2, Spalte 2</td>
  </tr>
</table>
```

Wenn du dieses "Löschen" der verdrängten Zelle vergisst, wird dein Tabellenlayout zerstört. Der Browser würde versuchen, die zusätzliche Zelle trotzdem zu rendern, was dazu führt, dass sie am Ende der Zeile angehängt wird und die Spaltenstruktur durcheinanderbringt. Merk dir also als goldene Regel: Für jede Zelle, die durch `rowspan` nach unten erweitert wird, musst du in den folgenden Zeilen die entsprechende Anzahl von Zellen am Anfang entfernen.

#### Ein praktisches Anwendungsbeispiel: Der Terminplan

Lass uns das Gelernte an einem realistischeren Beispiel anwenden. Wir erstellen einen kleinen Ausschnitt aus einem Tagesplan. Der Plan hat zwei Spalten: "Uhrzeit" und "Aktivität". Ein Termin, das "Team-Meeting", dauert von 9:00 bis 11:00 Uhr, also über zwei einstündige Zeitblöcke.

```html
<table>
  <caption>Tagesplan für Montag</caption>
  <thead>
    <tr>
      <th>Uhrzeit</th>
      <th>Aktivität</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>08:00 - 09:00</td>
      <td>E-Mails bearbeiten</td>
    </tr>
    <tr>
      <td>09:00 - 10:00</td>
      <td rowspan="2">Team-Meeting</td>
    </tr>
    <tr>
      <td>10:00 - 11:00</td>
      <!-- Die Zelle für die Aktivität wird hier weggelassen, -->
      <!-- da sie von der Zelle "Team-Meeting" darüber abgedeckt wird. -->
    </tr>
    <tr>
      <td>11:00 - 12:00</td>
      <td>Projektarbeit</td>
    </tr>
  </tbody>
</table>
```

Analysieren wir den Code Schritt für Schritt:
1.  Die Zeile für 08:00 Uhr ist normal und enthält zwei Zellen (`<td>`).
2.  Die Zeile für 09:00 Uhr enthält ebenfalls zwei Zellen. Die zweite Zelle, "Team-Meeting", erhält jedoch `rowspan="2"`. Damit geben wir dem Browser die Anweisung: "Diese Zelle soll sich über diese und die nächste Zeile erstrecken."
3.  Jetzt kommt der entscheidende Teil: die Zeile für 10:00 Uhr. Da die Zelle für die Aktivität bereits von der Zelle "Team-Meeting" von oben besetzt wird, definieren wir in diesem `<tr>` nur noch *eine* Zelle – die für die Uhrzeit. Die zweite Zelle wird komplett weggelassen.
4.  Die Zeile für 11:00 Uhr ist wieder eine normale Zeile mit zwei Zellen.

Das Ergebnis ist eine saubere, logisch strukturierte Tabelle, in der sofort ersichtlich ist, dass sich ein Termin über zwei Stunden erstreckt.

#### `rowspan` und Barrierefreiheit: Das `scope`-Attribut

Wenn du Zellen verbindest, insbesondere Kopfzellen (`<th>`), kann die logische Verbindung zwischen Kopf- und Datenzellen für assistierende Technologien wie Screenreader unklar werden. Ein Screenreader liest eine Tabelle Zeile für Zeile oder Spalte für Spalte vor und ordnet dabei die Datenzellen den entsprechenden Kopfzellen zu. `rowspan` kann diese Zuordnung erschweren.

Glücklicherweise gibt es eine einfache Möglichkeit, diese Beziehungen klar zu definieren: das `scope`-Attribut. Wenn du `rowspan` auf eine Kopfzelle anwendest, die als Überschrift für eine Gruppe von Zeilen dient, solltest du das Attribut `scope="rowgroup"` verwenden.

Stell dir eine Tabelle vor, die Aufgaben verschiedener Teams auflistet. Jedes Team ist für mehrere Aufgaben zuständig.

```html
<table>
  <caption>Team-Aufgabenübersicht</caption>
  <thead>
    <tr>
      <th>Team</th>
      <th>Aufgabe</th>
      <th>Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" scope="rowgroup">Team Alpha</th>
      <td>Design-Entwurf</td>
      <td>In Arbeit</td>
    </tr>
    <tr>
      <td>Prototyping</td>
      <td>Abgeschlossen</td>
    </tr>
    <tr>
      <th rowspan="2" scope="rowgroup">Team Beta</th>
      <td>Backend-Entwicklung</td>
      <td>In Arbeit</td>
    </tr>
    <tr>
      <td>Datenbank-Schema</td>
      <td>Geplant</td>
    </tr>
  </tbody>
</table>
```

In diesem Beispiel haben wir zwei Kopfzellen (`<th>`) mit `rowspan="2"`: "Team Alpha" und "Team Beta". Durch das Hinzufügen von `scope="rowgroup"` teilen wir einem Screenreader explizit mit: "Diese Kopfzelle ('Team Alpha') ist die Überschrift für die Gruppe von zwei Zeilen, die sie überspannt." Ein Nutzer, der auf diese Technologie angewiesen ist, würde dann für die Zelle "Prototyping" die korrekte Information erhalten, nämlich dass sie zum "Team Alpha" gehört. Ohne `scope` wäre diese Zuordnung möglicherweise nicht eindeutig.

#### Worauf du achten solltest

Die Verwendung von `rowspan` ist mächtig, birgt aber auch einige Fallstricke.
*   **Die vergessene Zell-Löschung:** Der häufigste Fehler ist, wie bereits erwähnt, das Vergessen, die überschriebenen Zellen aus den nachfolgenden Zeilen im HTML-Code zu entfernen. Dies führt unweigerlich zu einem kaputten Layout. Kontrolliere deinen Code also immer doppelt.
*   **Komplexität:** Vermeide es, exzessiv komplexe Tabellen mit unzähligen `rowspan`- und `colspan`-Kombinationen zu erstellen. Solche Tabellen werden sehr schnell unübersichtlich, sind schwer zu warten und stellen eine große Herausforderung für die Barrierefreiheit dar. Tabellen sind primär für die Darstellung von tabellarischen Daten gedacht, nicht für das allgemeine Seitenlayout. Wenn deine Struktur zu kompliziert wird, ist sie vielleicht gar keine Tabelle mehr, sondern sollte mit anderen HTML-Elementen und CSS umgesetzt werden.
*   **`rowspan="0"` ist veraltet:** Früher hatte der Wert `0` eine besondere Bedeutung und sorgte dafür, dass sich die Zelle bis zum Ende des Tabellenabschnitts (`<thead>`, `<tbody>` oder `<tfoot>`) erstreckte. Diese Funktionalität wird von modernen Browsern nicht mehr unterstützt und sollte nicht verwendet werden. Nutze immer eine positive ganze Zahl, die exakt der Anzahl der zu verbindenden Zeilen entspricht.

`rowspan` ist ein wertvolles Werkzeug in deinem HTML-Repertoire. Richtig eingesetzt, hilft es dir, Daten klarer und logischer zu strukturieren, indem es zusammengehörige Inhalte visuell und semantisch gruppiert. Behalte stets die Struktur deines Codes und die Auswirkungen auf die Barrierefreiheit im Blick, dann wirst du damit saubere und verständliche Tabellen erstellen.
