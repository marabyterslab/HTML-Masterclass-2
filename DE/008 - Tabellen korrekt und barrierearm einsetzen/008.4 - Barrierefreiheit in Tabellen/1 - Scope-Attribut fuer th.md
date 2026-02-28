# scope-Attribut für th

### Das `scope`-Attribut: Eindeutige Beziehungen in Tabellen schaffen

Wenn du eine Tabelle betrachtest, ist die Beziehung zwischen den Kopfzellen und den Datenzellen für dein Auge meistens sofort klar. Du siehst eine Spaltenüberschrift und weißt instinktiv, dass sich alle Zellen darunter auf diese Überschrift beziehen. Dasselbe gilt für Zeilenüberschriften. Diese visuelle Logik ist für sehende Benutzer selbstverständlich.

Für assistive Technologien wie Screenreader, die Webinhalte für blinde oder sehbehinderte Nutzer vorlesen, existiert diese visuelle Logik jedoch nicht. Ein Screenreader bewegt sich linear durch den HTML-Code und benötigt explizite Anweisungen, um die komplexen zweidimensionalen Beziehungen einer Tabelle zu verstehen. Ohne diese Hilfe liest er die Zellen oft einfach nacheinander vor, ohne den wichtigen Kontext zu liefern. Eine Zelle mit dem Inhalt "42" ist bedeutungslos, wenn der Nutzer nicht weiß, ob es sich um "Alter", "Anzahl Produkte" oder "Hausnummer" handelt.

Genau hier kommt das `scope`-Attribut ins Spiel. Es ist ein einfaches, aber extrem wirkungsvolles Werkzeug, um die semantische Verbindung zwischen einer Kopfzelle (`<th>`) und den dazugehörigen Datenzellen (`<td>`) programmatisch herzustellen. Du teilst dem Browser und somit auch den assistiven Technologien unmissverständlich mit, für welchen Bereich (engl. "scope") eine bestimmte Kopfzelle zuständig ist.

#### Die grundlegenden Werte: `col` und `row`

Das `scope`-Attribut wird ausschließlich auf `<th>`-Elementen verwendet und kann verschiedene Werte annehmen. Die beiden wichtigsten und am häufigsten verwendeten sind `col` (für Spalten) und `row` (für Zeilen).

##### `scope="col"` für Spaltenüberschriften

Stell dir eine einfache Tabelle vor, in der die erste Zeile die Überschriften für die folgenden Spalten enthält. Das ist der klassische Anwendungsfall für `scope="col"`.

Nehmen wir eine Tabelle mit den Namen, E-Mail-Adressen und dem Anmeldedatum von Benutzern.

```html
<table>
  <caption>Benutzerdaten</caption>
  <thead>
    <tr>
      <th>Name</th>
      <th>E-Mail</th>
      <th>Angemeldet seit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Maria Musterfrau</td>
      <td>maria@beispiel.de</td>
      <td>15.03.2023</td>
    </tr>
    <tr>
      <td>Max Mustermann</td>
      <td>max@beispiel.de</td>
      <td>21.06.2022</td>
    </tr>
  </tbody>
</table>
```

Visuell ist alles klar. Technisch fehlt jedoch die explizite Zuweisung. Mit dem `scope`-Attribut machen wir diese Beziehung eindeutig:

```html
<table>
  <caption>Benutzerdaten</caption>
  <thead>
    <tr>
      <th scope="col">Name</th>
      <th scope="col">E-Mail</th>
      <th scope="col">Angemeldet seit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Maria Musterfrau</td>
      <td>maria@beispiel.de</td>
      <td>15.03.2023</td>
    </tr>
    <tr>
      <td>Max Mustermann</td>
      <td>max@beispiel.de</td>
      <td>21.06.2022</td>
    </tr>
  </tbody>
</table>
```

Durch das Hinzufügen von `scope="col"` zu jeder `<th>`-Zelle in der Kopfzeile weiß ein Screenreader nun genau: "Die Kopfzelle 'Name' ist für alle Zellen in dieser Spalte zuständig." Wenn ein Nutzer nun die Zelle mit "maria@beispiel.de" ansteuert, kann der Screenreader den Kontext mitliefern und zum Beispiel ansagen: "E-Mail: maria@beispiel.de". Ohne `scope` würde er möglicherweise nur den Zellinhalt vorlesen, was den Nutzer zwingt, sich die Spaltenposition zu merken und geistig zuzuordnen.

##### `scope="row"` für Zeilenüberschriften

Manche Tabellen sind so aufgebaut, dass die erste Zelle jeder Zeile als Überschrift für die restlichen Zellen dieser Zeile dient. Das ist typisch für Vergleichstabellen oder Tabellen, die Merkmale eines einzelnen Objekts auflisten.

Betrachten wir die Spezifikationen eines Laptops:

```html
<table>
  <caption>Laptop-Spezifikationen: Modell XPS-15</caption>
  <tbody>
    <tr>
      <th scope="row">CPU</th>
      <td>Intel Core i7-13700H</td>
    </tr>
    <tr>
      <th scope="row">Arbeitsspeicher</th>
      <td>32 GB DDR5</td>
    </tr>
    <tr>
      <th scope="row">Festplatte</th>
      <td>1 TB NVMe SSD</td>
    </tr>
  </tbody>
</table>
```

Hier macht `scope="col"` keinen Sinn. Stattdessen verwenden wir `scope="row"`. Damit definieren wir, dass "CPU" die Überschrift für "Intel Core i7-13700H" ist und "Arbeitsspeicher" die Überschrift für "32 GB DDR5". Navigiert ein Nutzer mit einem Screenreader zur Zelle mit dem Inhalt "1 TB NVMe SSD", erhält er die klare Ansage: "Festplatte: 1 TB NVMe SSD".

#### Die Kombination macht's: Komplexe Tabellen mit `scope`

Die wahre Stärke des `scope`-Attributs zeigt sich in Tabellen, die sowohl Spalten- als auch Zeilenüberschriften haben. Das ist bei den meisten Datentabellen der Fall, zum Beispiel bei Preislisten, Zeitplänen oder Verkaufsstatistiken.

Schauen wir uns einen einfachen Stundenplan an:

```html
<table>
  <caption>Wochenplan</caption>
  <thead>
    <tr>
      <th></th> <!-- Leere Zelle oben links -->
      <th scope="col">Montag</th>
      <th scope="col">Dienstag</th>
      <th scope="col">Mittwoch</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">09:00 - 10:00</th>
      <td>Mathematik</td>
      <td>Deutsch</td>
      <td>Mathematik</td>
    </tr>
    <tr>
      <th scope="row">10:00 - 11:00</th>
      <td>Sport</td>
      <td>Englisch</td>
      <td>Kunst</td>
    </tr>
  </tbody>
</table>
```

In diesem Beispiel haben wir beide `scope`-Typen im Einsatz:
1.  Die Tage ("Montag", "Dienstag", ...) sind mit `scope="col"` ausgezeichnet. Sie sind die Kopfzeilen für ihre jeweiligen Spalten.
2.  Die Uhrzeiten ("09:00 - 10:00", ...) sind mit `scope="row"` ausgezeichnet. Sie sind die Kopfzeilen für ihre jeweiligen Zeilen.

Dank dieser Kombination kann eine assistive Technologie nun für jede einzelne Datenzelle einen präzisen Kontext liefern. Wenn der Fokus auf der Zelle mit dem Inhalt "Englisch" liegt, kann der Screenreader die Information aus beiden Kopfzeilen kombinieren und etwa so etwas ansagen: "Dienstag, 10:00 - 11:00: Englisch". Diese Information ist vollständig und erlaubt es dem Nutzer, die Datenstruktur sofort zu erfassen, ohne sich mühsam durch die Tabelle navigieren zu müssen, um die zugehörigen Überschriften zu finden.

Die leere `<th>`-Zelle in der oberen linken Ecke ist übrigens wichtig, da sie den strukturellen Platzhalter für die Zeilenüberschriften darstellt. Sie selbst benötigt kein `scope`-Attribut, da sie keine Daten beschreibt.

#### Für fortgeschrittene Strukturen: `colgroup` und `rowgroup`

Neben `col` und `row` gibt es zwei weitere, seltener genutzte Werte: `colgroup` und `rowgroup`. Diese kommen dann zum Einsatz, wenn eine Kopfzelle nicht nur für eine einzelne Spalte oder Zeile, sondern für eine ganze Gruppe davon zuständig ist.

##### `scope="colgroup"`

Dieser Wert wird verwendet, wenn eine Überschrift für eine Gruppe von Spalten gilt. Diese Spaltengruppen werden mit dem `<colgroup>`-Element definiert.

Ein Beispiel wäre eine Tabelle, die Verkaufszahlen für verschiedene Jahre aufschlüsselt, wobei jedes Jahr in Quartale unterteilt ist.

```html
<table>
  <caption>Verkaufszahlen nach Quartal</caption>
  <colgroup span="1"></colgroup>
  <colgroup span="2"></colgroup>
  <colgroup span="2"></colgroup>
  <thead>
    <tr>
      <th scope="col" rowspan="2">Produkt</th>
      <th scope="colgroup" colspan="2">2022</th>
      <th scope="colgroup" colspan="2">2023</th>
    </tr>
    <tr>
      <th scope="col">Q1</th>
      <th scope="col">Q2</th>
      <th scope="col">Q1</th>
      <th scope="col">Q2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Widget A</th>
      <td>150</td>
      <td>200</td>
      <td>180</td>
      <td>220</td>
    </tr>
    <tr>
      <th scope="row">Widget B</th>
      <td>300</td>
      <td>310</td>
      <td>350</td>
      <td>340</td>
    </tr>
  </tbody>
</table>
```

Hier ist die Zelle "2022" eine Überschrift für die Spalten "Q1" und "Q2" dieses Jahres. Durch `scope="colgroup"` in Verbindung mit `colspan="2"` wird diese übergeordnete Beziehung programmatisch hergestellt. Ein Screenreader versteht nun die Hierarchie: Die Zelle mit "200" gehört zu "Q2", und "Q2" wiederum gehört zu "2022".

##### `scope="rowgroup"`

Analog zu `colgroup` bezieht sich `rowgroup` auf eine Gruppe von Zeilen, die typischerweise durch `<thead>`, `<tbody>` oder `<tfoot>` definiert werden. Eine Kopfzelle innerhalb eines `<tbody>` könnte beispielsweise für alle Zeilen in diesem Body gelten. Dieser Anwendungsfall ist in der Praxis jedoch sehr selten. In den allermeisten Fällen sind `col` und `row` die Werkzeuge deiner Wahl.

#### Warum `scope` und nicht `id`/`headers`?

Für sehr komplexe Tabellen, die keine klare Gitterstruktur mehr haben (z. B. mit verschachtelten oder unregelmäßig verbundenen Zellen), gibt es eine alternative Methode: die Verwendung von `id`-Attributen auf den `<th>`-Zellen und einem `headers`-Attribut auf den `<td>`-Zellen. Im `headers`-Attribut werden dann die IDs der zugehörigen Kopfzellen aufgelistet.

Diese Methode ist extrem mächtig, aber auch sehr aufwendig und fehleranfällig in der Pflege. Für 99 % aller Datentabellen, die eine logische Zeilen- und Spaltenstruktur aufweisen, ist das `scope`-Attribut die deutlich einfachere, sauberere und empfohlene Lösung. Es hält deinen Code schlank und deine Absicht klar.

Halte dich also an eine einfache Regel: Solange deine Tabelle eine Gitterstruktur hat, nutze `scope`. Nur wenn die Beziehungen so komplex werden, dass `scope` nicht mehr ausreicht, solltest du die `id`/`headers`-Technik in Betracht ziehen.

Durch die konsequente Anwendung des `scope`-Attributs leistest du einen entscheidenden Beitrag zur Barrierefreiheit deiner Webseiten. Du wandelst eine rein visuelle Struktur in eine logische, maschinenlesbare Struktur um und ermöglichst es damit allen Nutzern, deine Daten schnell und fehlerfrei zu erfassen.
