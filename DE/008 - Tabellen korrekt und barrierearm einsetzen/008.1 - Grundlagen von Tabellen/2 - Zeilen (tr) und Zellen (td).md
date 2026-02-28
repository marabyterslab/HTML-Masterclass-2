# Zeilen (tr) und Zellen (td)

### Zeilen (`<tr>`) und Zellen (`<td>`): Das Grundgerüst jeder Tabelle

Stell dir eine Tabelle wie ein leeres Koordinatensystem oder ein einfaches Gitter vor. Bevor du irgendwelche Daten eintragen kannst, musst du zuerst die Struktur festlegen – die horizontalen Reihen und die vertikalen Spalten, die sich kreuzen und die einzelnen Fächer bilden. In HTML übernehmen genau diese Aufgabe die Elemente `<tr>` und `<td>`. Sie sind das absolute Fundament, das Herzstück jeder Tabelle, und ohne sie gäbe es nur ein leeres `<table>`-Tag ohne Inhalt und Form.

Lass uns diese beiden Bausteine Schritt für Schritt kennenlernen.

#### Die Tabellenzeile: `<tr>` (Table Row)

Das `<tr>`-Element ist dein Werkzeug, um eine horizontale Zeile in deiner Tabelle zu definieren. Das Kürzel `tr` steht für **t**able **r**ow, also "Tabellenzeile". Denk an `<tr>` als einen reinen Container. Seine einzige Aufgabe ist es, eine Gruppe von Zellen, die zusammen in einer Reihe stehen, zu bündeln.

Eine `<tr>`-Zeile selbst ist unsichtbar. Sie erzeugt keinen Rahmen, keine Hintergrundfarbe und keinen Inhalt. Sie ist eine reine Strukturanweisung für den Browser, die ihm sagt: "Achtung, hier beginnt eine neue horizontale Gliederungseinheit."

Jede Tabelle besteht aus mindestens einer `<tr>`-Zeile. Jede neue Zeile, die du deiner Tabelle hinzufügen möchtest, benötigt ein eigenes, frisches `<tr>`-Tag-Paar.

Schauen wir uns die grundlegende Verschachtelung an. Ein `<tr>`-Element muss immer ein direktes Kind eines `<table>`-, `<thead>`-, `<tbody>`- oder `<tfoot>`-Elements sein. Für den Moment konzentrieren wir uns auf die einfachste Form, bei der `<tr>` direkt im `<table>`-Element liegt:

```html
<table>
  <tr>
    <!-- Hier kommen die Zellen für die erste Zeile hinein -->
  </tr>
  <tr>
    <!-- Hier kommen die Zellen für die zweite Zeile hinein -->
  </tr>
</table>
```

In diesem Beispiel haben wir eine Tabelle mit zwei Zeilen definiert. Würdest du diesen Code im Browser anzeigen, sähest du … nichts. Das liegt daran, dass die Zeilen zwar strukturell vorhanden sind, aber noch keine Zellen enthalten, die mit Inhalt gefüllt werden könnten. Die Zeilen sind nur die leeren Regalböden; erst die Zellen sind die Bücher, die du hineinstellst.

#### Die Datenzelle: `<td>` (Table Data)

Hier kommt der eigentliche Inhalt ins Spiel. Das `<td>`-Element definiert eine einzelne Zelle in einer Tabellenzeile. Das Kürzel `td` steht für **t**able **d**ata, also "Tabellendaten". Jedes Mal, wenn du ein `<td>`-Element innerhalb eines `<tr>`-Elements platzierst, erzeugst du eine neue Spalte in genau dieser Zeile.

Die `<td>`-Zelle ist der Ort, an dem deine Daten leben. Das kann einfacher Text sein, aber auch so gut wie jedes andere HTML-Element: Bilder (`<img>`), Links (`<a>`), Absätze (`<p>`), Listen (`<ul>`) und vieles mehr.

Die grundlegende Regel lautet: **`<td>`-Elemente leben immer innerhalb von `<tr>`-Elementen.** Du kannst sie niemals direkt in ein `<table>`-Tag schreiben. Die Hierarchie ist streng: Das `<table>`-Element enthält die Zeilen (`<tr>`), und die Zeilen enthalten die Zellen (`<td>`).

Lass uns unser vorheriges Beispiel mit Leben füllen:

```html
<table>
  <tr>
    <td>Zelle 1, Zeile 1</td>
    <td>Zelle 2, Zeile 1</td>
  </tr>
  <tr>
    <td>Zelle 1, Zeile 2</td>
    <td>Zelle 2, Zeile 2</td>
  </tr>
</table>
```

Was passiert hier genau?

1.  Der Browser liest das erste `<tr>` und weiß: "Okay, ich starte eine neue Zeile."
2.  Innerhalb dieser Zeile findet er das erste `<td>`. Er erstellt die erste Zelle in der ersten Spalte und füllt sie mit dem Text "Zelle 1, Zeile 1".
3.  Direkt danach findet er das zweite `<td>`. Er erstellt daneben die zweite Zelle in der zweiten Spalte und füllt sie mit "Zelle 2, Zeile 1".
4.  Das `</tr>` wird geschlossen. Die erste Zeile ist damit komplett und besteht aus zwei Spalten.
5.  Der Browser liest das zweite `<tr>` und beginnt eine neue Zeile unter der ersten.
6.  Der Prozess wiederholt sich: Das erste `<td>` füllt die erste Spalte der zweiten Zeile, das zweite `<td>` füllt die zweite Spalte der zweiten Zeile.

Das Ergebnis ist eine saubere 2x2-Tabelle. Die Anzahl der `<td>`-Elemente in der ersten Zeile legt quasi die Anzahl der Spalten für die gesamte Tabelle fest.

#### Die goldene Regel: Konsistenz der Spaltenanzahl

Ein entscheidender Punkt für eine wohlgeformte und verständliche Tabelle ist die Konsistenz. Im Idealfall sollte jede `<tr>`-Zeile in deiner Tabelle die gleiche Anzahl an `<td>`-Zellen enthalten. Tust du dies nicht, überlässt du dem Browser die Interpretation, wie er die fehlenden oder überzähligen Zellen darstellen soll. Das Ergebnis ist oft unvorhersehbar und visuell unschön.

Betrachte dieses "schlechte" Beispiel:

```html
<!-- NICHT NACHMACHEN: Inkonsistente Spaltenanzahl -->
<table>
  <tr>
    <td>Produkt</td>
    <td>Preis</td>
    <td>Verfügbarkeit</td>
  </tr>
  <tr>
    <td>Apfel</td>
    <td>0,50 €</td>
    <!-- Hier fehlt eine Zelle! -->
  </tr>
  <tr>
    <td>Banane</td>
    <td>0,40 €</td>
    <td>Auf Lager</td>
  </tr>
</table>
```

In diesem Code hat die erste Zeile drei Zellen, die zweite nur zwei und die dritte wieder drei. Der Browser wird versuchen, das Beste daraus zu machen, und vermutlich eine leere Lücke in der zweiten Zeile lassen. Strukturell ist das jedoch unsauber und vor allem für Screenreader, die blinden oder sehbehinderten Nutzern den Inhalt vorlesen, extrem verwirrend. Die logische Verbindung zwischen den Daten geht verloren.

Halte dich also an die Regel: **Gleiche Anzahl von Zellen pro Zeile.** Später wirst du Techniken wie `colspan` und `rowspan` kennenlernen, mit denen du Zellen über mehrere Spalten oder Zeilen verbinden kannst. Aber auch dann folgt die Struktur einer klaren Logik, die du bewusst steuerst. Für den Anfang ist eine konsistente Spaltenzahl der sicherste und sauberste Weg.

#### Mehr als nur Kästchen: Die semantische Bedeutung

Es ist wichtig, sich daran zu erinnern, dass `<td>` für "Table *Data*" steht. Dies unterstreicht die semantische Rolle des Elements: Es enthält die eigentlichen Datenpunkte deiner Tabelle. In späteren Kapiteln wirst du das `<th>`-Element ("Table Header") kennenlernen, das für die Überschriften der Spalten oder Zeilen zuständig ist.

Die Kombination aus `<tr>` und `<td>` bildet das Rückgrat für die Darstellung von tabellarischen Daten – also Informationen, die eine klare Beziehung zwischen Zeilen und Spalten haben. Ein klassisches Beispiel ist eine Preisliste: Jede Zeile (`<tr>`) repräsentiert ein Produkt, und jede Zelle (`<td>`) in dieser Zeile enthält eine spezifische Information dazu, wie den Namen, den Preis oder die Artikelnummer.

Vermeide unbedingt den alten, überholten Ansatz, Tabellen für das Layout einer Webseite zu missbrauchen – also um Menüs, Texte und Bilder in einem bestimmten visuellen Raster anzuordnen. Dafür sind moderne Techniken wie CSS Flexbox oder CSS Grid die weitaus bessere, flexiblere und vor allem barriereärmere Wahl. Tabellen sind für Daten da, und `<tr>` und `<td>` sind deine grundlegenden Werkzeuge, um diese Daten sauber und logisch zu strukturieren.
