# Das table-Element

### Kapitel 8.1: Das `<table>`-Element: Struktur für tabellarische Daten

Tabellen sind ein grundlegender Baustein des Webs, dessen eigentlicher Zweck oft missverstanden wird. In den frühen Tagen des Internets wurden sie missbraucht, um komplexe visuelle Layouts für ganze Webseiten zu erstellen. Diese Zeit ist zum Glück vorbei. Heute besinnen wir uns auf ihre wahre Stärke: die semantisch korrekte und barrierearme Darstellung von tabellarischen Daten.

Stell dir eine Excel-Tabelle oder ein einfaches Raster aus Spalten und Zeilen vor. Genau das ist der Anwendungsfall für das `<table>`-Element in HTML. Es dient dazu, Daten in eine zweidimensionale Beziehung zueinander zu setzen. Typische Beispiele sind Preislisten, Terminkalender, Vergleichsstatistiken oder Finanzberichte – also alles, was eine klare Zuordnung von Datenpunkten in einem Gitternetz erfordert.

#### Die grundlegende Anatomie einer Tabelle

Eine HTML-Tabelle besteht aus einem Set von ineinander verschachtelten Elementen, die zusammen eine logische Struktur ergeben. Jedes Element hat dabei eine ganz bestimmte Aufgabe. Die drei unverzichtbaren Grundbausteine sind:

*   `<table>`: Das Wurzelelement, das die gesamte Tabelle umschließt. Es signalisiert dem Browser und assistiven Technologien: „Achtung, hier beginnen tabellarische Daten.“
*   `<tr>`: Steht für „table row“ (Tabellenzeile). Dieses Element definiert eine horizontale Zeile innerhalb der Tabelle.
*   `<td>`: Steht für „table data“ (Tabellendaten). Dieses Element definiert eine einzelne Zelle innerhalb einer Zeile. Es enthält den eigentlichen Datenpunkt.

Lass uns eine ganz einfache Tabelle erstellen, die eine kleine Liste von Früchten und deren Farben zeigt:

```html
<table>
  <tr>
    <td>Apfel</td>
    <td>Rot</td>
  </tr>
  <tr>
    <td>Banane</td>
    <td>Gelb</td>
  </tr>
  <tr>
    <td>Kiwi</td>
    <td>Grün</td>
  </tr>
</table>
```

Auch ohne CSS-Styling rendert der Browser hier bereits eine simple tabellarische Struktur. Wir haben eine Tabelle (`<table>`) mit drei Zeilen (`<tr>`). Jede Zeile enthält wiederum zwei Datenzellen (`<td>`), eine für den Fruchtnamen und eine für die Farbe.

#### Überschriften für den Kontext: Das `<th>`-Element

Unsere einfache Tabelle ist zwar funktional, aber ihr fehlt etwas Entscheidendes: Kontext. Woher wissen wir, was in der ersten und zweiten Spalte steht? Sind es Namen, Farben, Herkunftsländer? Um diese Mehrdeutigkeit zu beseitigen, führen wir Kopfzellen ein.

*   `<th>`: Steht für „table header“ (Tabellenkopf). Dieses Element wird anstelle von `<td>` für Zellen verwendet, die als Überschrift für eine Spalte oder eine Zeile dienen.

Browser stellen `<th>`-Elemente standardmäßig fett und zentriert dar. Viel wichtiger ist jedoch ihre semantische Bedeutung. Für einen Screenreader ist ein `<th>`-Element der Ankerpunkt, um Daten korrekt vorzulesen. Er kann dann sagen: „Spalte Frucht, Zeile 1: Apfel. Spalte Farbe, Zeile 1: Rot.“ Ohne `<th>` wäre die Ausgabe nur ein unzusammenhängendes „Apfel, Rot“.

Ergänzen wir unsere Tabelle um eine Kopfzeile:

```html
<table>
  <tr>
    <th>Frucht</th>
    <th>Farbe</th>
  </tr>
  <tr>
    <td>Apfel</td>
    <td>Rot</td>
  </tr>
  <tr>
    <td>Banane</td>
    <td>Gelb</td>
  </tr>
  <tr>
    <td>Kiwi</td>
    <td>Grün</td>
  </tr>
</table>
```

Jetzt ist die Struktur sofort klarer. Die erste Zeile (`<tr>`) enthält nun zwei `<th>`-Elemente, die die Spalten „Frucht“ und „Farbe“ definieren.

#### Mehr Struktur für komplexe Tabellen: `<thead>`, `<tbody>` und `<tfoot>`

Für sehr einfache Tabellen mag die bisherige Struktur ausreichen. Sobald Tabellen jedoch länger und komplexer werden, hilft es, sie weiter logisch zu unterteilen. Dafür stellt HTML drei spezielle Elemente zur Verfügung, die direkt innerhalb des `<table>`-Elements platziert werden:

*   `<thead>`: Gruppiert den Kopfbereich der Tabelle. Hier gehören die Zeilen (`<tr>`) hinein, die die Spaltenüberschriften (`<th>`) enthalten.
*   `<tbody>`: Gruppiert den Hauptinhalt, also den Körper der Tabelle. Die meisten deiner Datenzeilen werden hier platziert.
*   `<tfoot>`: Gruppiert den Fußbereich der Tabelle. Er kann Zusammenfassungen, Summen oder andere Abschlussinformationen enthalten.

Diese Elemente verbessern nicht nur die Lesbarkeit deines HTML-Codes, sondern bieten auch praktische Vorteile. Beispielsweise können Browser beim Drucken langer Tabellen den `<thead>`-Inhalt auf jeder neuen Seite wiederholen. Außerdem erleichtern sie das gezielte Styling mit CSS.

Unsere Fruchttabelle in der voll strukturierten Form sieht so aus:

```html
<table>
  <thead>
    <tr>
      <th>Frucht</th>
      <th>Farbe</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Apfel</td>
      <td>Rot</td>
    </tr>
    <tr>
      <td>Banane</td>
      <td>Gelb</td>
    </tr>
    <tr>
      <td>Kiwi</td>
      <td>Grün</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Anzahl Früchte</td>
      <td>3</td>
    </tr>
  </tfoot>
</table>
```

Beachte, dass `<thead>`, `<tbody>` und `<tfoot>` keine visuellen Änderungen an der Standarddarstellung der Tabelle bewirken. Ihr Wert liegt rein in der semantischen Strukturierung.

#### Barrierefreiheit explizit machen: Das `scope`-Attribut

Obwohl wir mit `<th>` bereits Kopfzellen definiert haben, können wir die Beziehung zwischen Überschrift und Datenzelle für assistive Technologien noch expliziter machen. Das `scope`-Attribut (Geltungsbereich) auf einem `<th>`-Element teilt unmissverständlich mit, worauf sich die Überschrift bezieht.

Es gibt zwei primäre Werte:

*   `scope="col"`: Die Kopfzelle ist eine Überschrift für die gesamte Spalte (column).
*   `scope="row"`: Die Kopfzelle ist eine Überschrift für die gesamte Zeile (row).

Für die meisten Tabellen, bei denen die Überschriften oben stehen, ist `scope="col"` die richtige Wahl. Wenn du eine Tabelle hast, bei der die erste Zelle jeder Zeile eine Überschrift ist (z. B. eine Feature-Vergleichstabelle), würdest du `scope="row"` verwenden.

Unsere verbesserte Tabelle mit `scope`:

```html
<table>
  <thead>
    <tr>
      <th scope="col">Frucht</th>
      <th scope="col">Farbe</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Apfel</td>
      <td>Rot</td>
    </tr>
    <!-- ... weitere Zeilen ... -->
  </tbody>
</table>
```

Diese kleine Ergänzung ist ein großer Gewinn für die Barrierefreiheit und sollte zur Standardpraxis bei jeder Tabellenerstellung gehören.

#### Der Titel der Tabelle: Das `<caption>`-Element

Jede gute Tabelle verdient eine Überschrift, die ihren Inhalt beschreibt. Dafür gibt es das `<caption>`-Element. Es wird als erstes Kindelement direkt in das `<table>`-Tag geschrieben, noch vor `<thead>`.

Der Inhalt von `<caption>` wird typischerweise über oder unter der Tabelle angezeigt (je nach Browser und CSS) und dient als offizielle Beschriftung. Screenreader lesen diesen Titel vor, bevor sie mit dem Inhalt der Tabelle beginnen. Das gibt Nutzern einen sofortigen Kontext und hilft ihnen zu entscheiden, ob die Tabelle für sie relevant ist.

```html
<table>
  <caption>Übersicht verfügbarer Früchte und ihrer Farben</caption>
  <thead>
    <tr>
      <th scope="col">Frucht</th>
      <th scope="col">Farbe</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Apfel</td>
      <td>Rot</td>
    </tr>
    <tr>
      <td>Banane</td>
      <td>Gelb</td>
    </tr>
  </tbody>
</table>
```

Die Verwendung von `<caption>` ist weitaus besser als eine separate Überschrift wie `<h3>` vor der Tabelle, da die `<caption>` semantisch fest mit ihrer Tabelle verbunden ist.

#### Zellen verbinden: `colspan` und `rowspan`

Manchmal reicht ein starres Raster nicht aus. Daten müssen sich über mehrere Spalten oder Zeilen erstrecken. Hierfür gibt es zwei Attribute, die du auf `<td>`- oder `<th>`-Elemente anwenden kannst:

*   `colspan`: Verbindet eine Zelle horizontal über eine angegebene Anzahl von Spalten (column span).
*   `rowspan`: Verbindet eine Zelle vertikal über eine angegebene Anzahl von Zeilen (row span).

Stell dir einen einfachen Stundenplan vor. Die Mittagspause könnte sich über mehrere Spalten erstrecken.

```html
<table>
  <caption>Stundenplan</caption>
  <thead>
    <tr>
      <th scope="col">Zeit</th>
      <th scope="col">Montag</th>
      <th scope="col">Dienstag</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">09:00 - 10:00</th>
      <td>Mathe</td>
      <td>Deutsch</td>
    </tr>
    <tr>
      <th scope="row">10:00 - 11:00</th>
      <td colspan="2">Mittagspause</td>
    </tr>
    <tr>
      <th scope="row">11:00 - 12:00</th>
      <td>Sport</td>
      <td>Kunst</td>
    </tr>
  </tbody>
</table>
```

In diesem Beispiel erstreckt sich die Zelle „Mittagspause“ (`<td colspan="2">`) über zwei Spalten. Wichtig ist hierbei: Da diese eine Zelle den Platz von zweien einnimmt, darf in dieser Zeile (`<tr>`) nur noch die `<th>`-Zelle für die Zeit und diese eine `<td>`-Zelle stehen. Die "fehlende" zweite `<td>`-Zelle für den Dienstag wird weggelassen, da ihr Platz bereits belegt ist.

Ähnlich funktioniert `rowspan`. Wenn der Mathe-Unterricht zwei Stunden dauern würde, könnten wir ihn über zwei Zeilen verbinden:

```html
<tbody>
  <tr>
    <th scope="row">09:00 - 11:00</th>
    <td rowspan="2">Mathe</td>
    <td>Deutsch</td>
  </tr>
  <tr>
    <!-- Die Zelle für Montag wird hier weggelassen -->
    <td>Englisch</td>
  </tr>
</tbody>
```

Hier erstreckt sich die „Mathe“-Zelle über zwei Zeilen. In der darauffolgenden Zeile (`<tr>`) wird die Zelle für den Montag weggelassen, da sie bereits von der Zelle darüber abgedeckt wird.

Die Verwendung von `colspan` und `rowspan` kann die Komplexität und die kognitive Last für Nutzer von Screenreadern erhöhen. Setze sie daher sparsam und nur dann ein, wenn es für die logische Darstellung der Daten absolut notwendig ist.
