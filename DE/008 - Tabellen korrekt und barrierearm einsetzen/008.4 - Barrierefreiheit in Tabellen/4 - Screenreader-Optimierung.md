# Screenreader-Optimierung

### Screenreader-Optimierung: Tabellen zum Sprechen bringen

Stell dir vor, du siehst eine Tabelle mit Umsatzzahlen. Dein Gehirn verarbeitet die visuellen Informationen sofort. Du erkennst auf einen Blick, welche Zahl zum Monat Januar und zum Produkt A gehört, weil sie sich im Schnittpunkt der entsprechenden Spalte und Zeile befindet. Die visuelle Gitterstruktur gibt dir den gesamten Kontext.

Für einen Menschen, der einen Screenreader benutzt, existiert diese visuelle Gitterstruktur nicht. Ein Screenreader liest eine Webseite linear vor, von oben links nach unten rechts, Element für Element. Eine schlecht ausgezeichnete Tabelle wird zu einer langen, verwirrenden Kette von Zahlen und Wörtern ohne Zusammenhang. Der Nutzer hört vielleicht "Januar", "Februar", "März", "Produkt A", "100", "150", "120", aber die entscheidende Information – dass 150 der Wert für Februar und Produkt A ist – geht verloren.

Deine Aufgabe ist es, HTML so zu schreiben, dass der Screenreader diese Beziehungen versteht und sie dem Nutzer vorlesen kann. Du musst der Tabelle eine programmatische Bedeutung geben, die den visuellen Kontext für nicht-sehende Nutzer übersetzt.

#### Die Grundlagen: `<th>` ist dein Fundament

Das absolut grundlegendste Element für barrierefreie Tabellen ist das Tabellenkopf-Element `<th>` (`table head`). Viele Entwickler verwenden fälschlicherweise `<td>` (`table data`) für Kopfzeilen und formatieren den Text dann mit CSS, damit er fett gedruckt wird. Das ist ein schwerwiegender Fehler für die Barrierefreiheit.

Ein `<td>` ist eine reine Datenzelle. Ein `<th>` hingegen sagt dem Browser und assistiven Technologien: „Dieser Inhalt ist die Überschrift für eine Gruppe von Zellen.“

Ein Screenreader nutzt diese Information. Wenn der Nutzer durch die Tabelle navigiert und auf eine `<td>`-Zelle stößt, kann der Screenreader die zugehörige `<th>`-Zelle automatisch vorlesen.

Schau dir diese einfache Tabelle an:

```html
<table>
  <caption>Monatliche Verkaufszahlen</caption>
  <thead>
    <tr>
      <th>Monat</th>
      <th>Umsatz</th>
      <th>Gewinn</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Januar</td>
      <td>10.000 €</td>
      <td>2.000 €</td>
    </tr>
    <tr>
      <td>Februar</td>
      <td>12.000 €</td>
      <td>2.500 €</td>
    </tr>
  </tbody>
</table>
```

Wenn ein Screenreader-Nutzer auf die Zelle "12.000 €" navigiert, wird der Screenreader nicht nur "12.000 €" vorlesen, sondern so etwas wie: "Zeile 3, Spalte Umsatz, 12.000 €". Der Kontext wird automatisch hergestellt, weil wir `<th>` für die Überschriften "Monat", "Umsatz" und "Gewinn" verwendet haben. Die Verwendung von `<thead>` und `<tbody>` hilft zusätzlich, die Struktur der Tabelle zu verdeutlichen, was sowohl für Screenreader als auch für die Browser-Darstellung von Vorteil ist.

#### Klarheit schaffen mit dem `scope`-Attribut

Bei einfachen Tabellen wie der obigen kann der Browser oft selbst erraten, worauf sich eine `<th>`-Zelle bezieht. Aber Verlass ist darauf nicht. Sobald Tabellen etwas komplexer werden, zum Beispiel mit Überschriften für Zeilen *und* Spalten, musst du dem Screenreader explizit sagen, wofür eine Überschrift zuständig ist.

Dafür gibt es das `scope`-Attribut. Es kann zwei wesentliche Werte annehmen:
*   `scope="col"`: Die Überschrift (`<th>`) gilt für alle Zellen in derselben Spalte (column).
*   `scope="row"`: Die Überschrift (`<th>`) gilt für alle Zellen in derselben Zeile (row).

Nehmen wir unser Beispiel und fügen Zeilenüberschriften hinzu:

```html
<table>
  <caption>Verkaufszahlen Q1 nach Produkt</caption>
  <thead>
    <tr>
      <th></th> <!-- Leere Zelle oben links -->
      <th scope="col">Januar</th>
      <th scope="col">Februar</th>
      <th scope="col">März</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Produkt A</th>
      <td>1.200</td>
      <td>1.300</td>
      <td>1.500</td>
    </tr>
    <tr>
      <th scope="row">Produkt B</th>
      <td>800</td>
      <td>950</td>
      <td>1.100</td>
    </tr>
  </tbody>
</table>
```

Hier passiert etwas Wichtiges:
1.  Die Monatsnamen in der Kopfzeile (`<thead>`) bekommen `scope="col"`. Damit ist klar, dass "Januar" die Überschrift für die gesamte erste Datenspalte ist.
2.  Die Produktnamen in der ersten Spalte jeder Zeile bekommen `scope="row"`. "Produkt A" ist also die Überschrift für alle Daten in dieser Zeile.

Wenn ein Screenreader-Nutzer nun auf die Zelle mit dem Wert "950" navigiert, kann der Screenreader dank des `scope`-Attributs eine eindeutige Ansage machen: "Produkt B, Februar, 950". Der Kontext ist perfekt, die Information ist vollständig und ohne Raten zugänglich. Das `scope`-Attribut ist dein wichtigstes Werkzeug für die meisten gängigen Datentabellen.

#### Für Fortgeschrittene: Komplexe Tabellen mit `id` und `headers`

Manchmal reicht `scope` nicht aus. Stell dir eine Tabelle vor, bei der sich Überschriften über mehrere Spalten oder Zeilen erstrecken (mit `colspan` oder `rowspan`) oder es mehrere Ebenen von Überschriften gibt. In solchen Fällen brauchst du eine noch präzisere Methode, um Zellen und ihre Überschriften zu verbinden: die Attribute `id` und `headers`.

Das Prinzip funktioniert so:
1.  Jede Überschriftenzelle (`<th>`), die du referenzieren möchtest, erhält eine eindeutige `id`.
2.  Jede Datenzelle (`<td>`), die auf diese Überschriften verweisen soll, erhält ein `headers`-Attribut. Der Wert dieses Attributs ist eine durch Leerzeichen getrennte Liste der `id`s der zugehörigen Überschriften.

Das klingt komplizierter, als es ist. Schauen wir uns ein Beispiel an:

```html
<table>
  <caption>Bevölkerungsstatistik</caption>
  <thead>
    <tr>
      <th id="land">Land</th>
      <th colspan="2" id="gruppe_maennlich">Männlich</th>
      <th colspan="2" id="gruppe_weiblich">Weiblich</th>
    </tr>
    <tr>
      <th></th> <!-- Leere Zelle -->
      <th id="alter_m_jung">0-50</th>
      <th id="alter_m_alt">51+</th>
      <th id="alter_w_jung">0-50</th>
      <th id="alter_w_alt">51+</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="land_de" scope="row">Deutschland</th>
      <td headers="land_de gruppe_maennlich alter_m_jung">40 Mio.</td>
      <td headers="land_de gruppe_maennlich alter_m_alt">22 Mio.</td>
      <td headers="land_de gruppe_weiblich alter_w_jung">41 Mio.</td>
      <td headers="land_de gruppe_weiblich alter_w_alt">25 Mio.</td>
    </tr>
  </tbody>
</table>
```
Analysieren wir die erste Datenzelle mit dem Inhalt "40 Mio.":
`<td headers="land_de gruppe_maennlich alter_m_jung">40 Mio.</td>`

Das `headers`-Attribut listet drei `id`s auf:
*   `land_de`: verweist auf die Zeilenüberschrift "Deutschland".
*   `gruppe_maennlich`: verweist auf die übergeordnete Spaltenüberschrift "Männlich".
*   `alter_m_jung`: verweist auf die untergeordnete Spaltenüberschrift "0-50".

Ein Screenreader kann diese Verbindungen nun exakt auslesen und würde für diese Zelle ansagen: "Deutschland, Männlich, 0-50, 40 Mio.". Jede einzelne Information, die ein sehender Nutzer aus der Tabellenstruktur ableiten würde, wird hier explizit für den Screenreader bereitgestellt. Die `id`/`headers`-Methode ist zwar aufwendiger, aber für komplexe Datenstrukturen der einzige Weg, um eine vollständige Barrierefreiheit zu gewährleisten.

#### Der Titel des Ganzen: Das `<caption>`-Element

Ein oft übersehenes, aber entscheidendes Element ist `<caption>`. Es dient dazu, einer Tabelle einen Titel oder eine Beschreibung zu geben. Dieses Element muss das erste Kind-Element direkt innerhalb des `<table>`-Tags sein.

Warum ist `<caption>` so wichtig?
Es ist das Erste, was ein Screenreader vorliest, wenn er auf eine Tabelle trifft. Es gibt dem Nutzer sofortigen Kontext und hilft ihm zu entscheiden, ob der Inhalt der Tabelle für ihn relevant ist. Ohne `<caption>` muss der Nutzer erst in die Tabelle hineinnavigieren, um herauszufinden, worum es überhaupt geht.

Eine Überschrift wie `<h2>Unsere Verkaufszahlen</h2>` vor der Tabelle ist für sehende Nutzer hilfreich, aber sie ist nicht programmatisch mit der Tabelle verknüpft. `<caption>` hingegen ist untrennbar mit seiner `<table>` verbunden.

Ein gutes `<caption>` ist kurz und prägnant:
*   Gut: `<caption>Jahresumsatz 2023 nach Quartal</caption>`
*   Schlecht: `<caption>Tabelle 1</caption>` (sagt nichts über den Inhalt aus)

Die Kombination aus einem klaren `<caption>` und korrekt ausgezeichneten Kopfzeilen (`<th>` mit `scope` oder `id`/`headers`) macht deine Tabellen von einem undurchdringlichen Datensalat zu einer verständlichen und navigierbaren Informationsquelle für alle.

#### Ein Wort der Warnung: Tabellen sind nicht für das Layout

Früher, in den Anfängen des Webs, war es üblich, Tabellen zu verwenden, um das Layout einer Webseite zu gestalten – also um Spalten, Sidebars und Positionierungen zu erzeugen. Diese Praxis ist heute ein absolutes No-Go und ein Desaster für die Barrierefreiheit.

Ein Screenreader ist darauf ausgelegt, Tabellen als Datentabellen zu interpretieren. Wenn du eine Layout-Tabelle verwendest, wird er versuchen, Zeilen- und Spaltenüberschriften zu finden, wo keine sind. Die Lesereihenfolge wird unlogisch und der Inhalt völlig aus dem Zusammenhang gerissen. Für die visuelle Gestaltung von Webseiten gibt es moderne, flexible und barrierefreie CSS-Technologien wie Flexbox und Grid. Verwende Tabellen ausschließlich für das, wofür sie gedacht sind: die Darstellung von tabellarischen Daten.
