# Semantische Gliederung komplexer Daten

### Semantische Gliederung komplexer Daten

Wenn du an eine HTML-Tabelle denkst, kommt dir wahrscheinlich ein einfaches Gitter aus Zeilen und Spalten in den Sinn. Für simple Datensätze mag das ausreichen. Doch sobald die Daten komplexer werden – mit Zwischenüberschriften, zusammengefassten Spalten oder speziellen Zeilen für Summen – reicht ein einfaches `<table>`-Gitter nicht mehr aus. An diesem Punkt kommt die semantische Gliederung ins Spiel. Es geht darum, deiner Tabelle eine klare, logische und maschinenlesbare Struktur zu geben. Das hilft nicht nur Suchmaschinen, den Inhalt zu verstehen, sondern ist vor allem für die Barrierefreiheit, insbesondere für Screenreader-Nutzer, unerlässlich.

#### Die große Dreiteilung: `<thead>`, `<tbody>` und `<tfoot>`

Eine der grundlegendsten Methoden zur Strukturierung einer Tabelle ist die Aufteilung in einen Kopf-, einen Körper- und einen Fußbereich. HTML stellt dafür drei spezielle Elemente zur Verfügung, die direkt innerhalb des `<table>`-Elements platziert werden:

*   **`<thead>` (Table Head):** Dieser Container umschließt die Kopfzeile(n) deiner Tabelle. Hier stehen typischerweise die `<th>`-Elemente (Table Header), die die Spalten beschriften. Auch wenn eine Tabelle nur eine Kopfzeile hat, ist es gute Praxis, sie in ein `<thead>` zu packen. Der Browser weiß dann eindeutig: Das hier sind die Überschriften.
*   **`<tbody>` (Table Body):** Hier gehört der eigentliche Inhalt deiner Tabelle hinein, also die Datenzeilen. Jede Zeile (`<tr>`) mit ihren Datenzellen (`<td>`) wird innerhalb des `<tbody>`-Elements platziert. Eine Tabelle kann sogar mehrere `<tbody>`-Elemente enthalten, um logisch zusammengehörige Datengruppen zu bündeln, zum Beispiel Verkaufszahlen nach Regionen getrennt.
*   **`<tfoot>` (Table Foot):** Dieser Bereich ist für die Fußzeile(n) reserviert. Oft werden hier Zusammenfassungen, Summen oder Endergebnisse dargestellt.

Die Verwendung dieser drei Elemente schafft eine robuste Grundstruktur. Ein Browser kann diese Information nutzen, um beispielsweise bei langen Tabellen den Tabellenkopf beim Scrollen fixiert anzuzeigen. Für assistive Technologien wird die Tabelle vorhersagbarer und leichter zu navigieren.

Schauen wir uns ein einfaches Beispiel für eine Rechnung an:

```html
<table>
  <caption>Rechnungsdetails für Bestellung #12345</caption>
  
  <thead>
    <tr>
      <th>Produkt</th>
      <th>Anzahl</th>
      <th>Einzelpreis</th>
      <th>Gesamtpreis</th>
    </tr>
  </thead>
  
  <tbody>
    <tr>
      <td>HTML-Masterclass-Buch</td>
      <td>1</td>
      <td>49,90 €</td>
      <td>49,90 €</td>
    </tr>
    <tr>
      <td>CSS-Design-Poster</td>
      <td>2</td>
      <td>12,50 €</td>
      <td>25,00 €</td>
    </tr>
  </tbody>
  
  <tfoot>
    <tr>
      <td colspan="3">Zwischensumme</td>
      <td>74,90 €</td>
    </tr>
    <tr>
      <td colspan="3">Mehrwertsteuer (19%)</td>
      <td>14,23 €</td>
    </tr>
    <tr>
      <td colspan="3"><strong>Gesamtsumme</strong></td>
      <td><strong>89,13 €</strong></td>
    </tr>
  </tfoot>
</table>
```

In diesem Code ist die Trennung klar: Der Kopf definiert die Spalten, der Körper enthält die einzelnen Posten und der Fuß fasst alles zusammen.

#### Das Herzstück der Semantik: `<th>` und das `scope`-Attribut

Das `<th>`-Element ist mehr als nur eine fettgedruckte Zelle. Es signalisiert, dass der Inhalt eine Überschrift für andere Zellen ist. Aber für welche? In einfachen Tabellen ist das oft selbsterklärend. In komplexeren Strukturen müssen wir jedoch eine explizite Verbindung herstellen. Genau hierfür gibt es das `scope`-Attribut.

Das `scope`-Attribut wird direkt im `<th>`-Tag platziert und teilt dem Browser und assistiven Technologien mit, auf welchen Bereich sich die Überschrift bezieht. Die wichtigsten Werte sind:

*   **`scope="col"`:** Die Überschrift gilt für alle Zellen in derselben Spalte (Column) unterhalb der Überschrift. Das ist der häufigste Anwendungsfall.
*   **`scope="row"`:** Die Überschrift gilt für alle Zellen in derselben Zeile (Row) rechts von der Überschrift.

Stell dir einen einfachen Kursplan vor:

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
      <th scope="row">09:00 - 10:30</th>
      <td>HTML Grundlagen</td>
      <td>CSS Flexbox</td>
      <td>HTML Formulare</td>
    </tr>
    <tr>
      <th scope="row">11:00 - 12:30</th>
      <td>Barrierefreiheit</td>
      <td>JavaScript Intro</td>
      <td>CSS Grid</td>
    </tr>
  </tbody>
</table>
```

Ein Screenreader, der die Zelle "CSS Flexbox" vorliest, kann dank `scope` nun den Kontext präzise wiedergeben: "Dienstag, 09:00 - 10:30: CSS Flexbox". Ohne `scope` wüsste das Programm nicht sicher, ob "Dienstag" oder "09:00 - 10:30" (oder beides) die relevante Überschrift ist. Durch diese einfache Ergänzung wird die Tabelle navigierbar und verständlich.

#### Wenn Zellen wachsen: `colspan` und `rowspan` meistern

Komplexität entsteht oft durch Zellen, die sich über mehrere Spalten (`colspan`) oder Zeilen (`rowspan`) erstrecken. Diese verbundenen Zellen können die Zuordnung von Daten zu Überschriften schnell verkomplizieren.

Nehmen wir an, wir haben eine Tabelle, die Verkaufszahlen für verschiedene Quartale und Monate anzeigt. Das Quartal ist eine übergeordnete Überschrift für die Monate.

```html
<table>
  <caption>Verkaufszahlen 2023</caption>
  <thead>
    <tr>
      <th scope="col">Produkt</th>
      <th scope="colgroup" colspan="3">Quartal 1</th>
      <th scope="colgroup" colspan="3">Quartal 2</th>
    </tr>
    <tr>
      <th></th> <!-- Leere Zelle unter "Produkt" -->
      <th scope="col">Januar</th>
      <th scope="col">Februar</th>
      <th scope="col">März</th>
      <th scope="col">April</th>
      <th scope="col">Mai</th>
      <th scope="col">Juni</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Widget A</th>
      <td>150</td>
      <td>180</td>
      <td>210</td>
      <td>190</td>
      <td>220</td>
      <td>250</td>
    </tr>
    <tr>
      <th scope="row">Widget B</th>
      <td>120</td>
      <td>130</td>
      <td>145</td>
      <td>160</td>
      <td>155</td>
      <td>170</td>
    </tr>
  </tbody>
</table>
```

Hier gibt es ein paar wichtige Details zu beachten:

1.  **`colspan="3"`:** Die Zellen für "Quartal 1" und "Quartal 2" erstrecken sich über jeweils drei Spalten.
2.  **`scope="colgroup"`:** Dies ist ein weiterer Wert für das `scope`-Attribut. Er bedeutet, dass die Überschrift für die gesamte Spaltengruppe gilt, die durch `colspan` definiert wird. Ein Screenreader versteht so, dass "Januar", "Februar" und "März" alle zum "Quartal 1" gehören.
3.  **Zweite Kopfzeile:** Die zweite `<tr>` im `<thead>` enthält die Monatsüberschriften. Wir nutzen hier wieder `scope="col"`, da jede dieser Überschriften für ihre jeweilige Spalte zuständig ist.
4.  **Leere Zellen:** Die leeren `<th>`-Zellen sind Platzhalter, um die Gitterstruktur der Tabelle aufrechtzuerhalten. Sie sind notwendig, damit die Spalten korrekt ausgerichtet sind.

Analog zu `scope="colgroup"` existiert auch `scope="rowgroup"`, das in Verbindung mit `rowspan` verwendet wird, um eine Überschrift für eine Gruppe von Zeilen zu deklarieren.

#### Der Titel des Werks: `<caption>` für den Kontext

Eine Tabelle sollte niemals ohne Kontext im Raum stehen. Du könntest eine normale Überschrift wie `<h3>` vor die Tabelle setzen, aber HTML bietet eine semantisch viel bessere Lösung: das `<caption>`-Element.

Das `<caption>`-Element muss das erste Kindelement einer `<table>` sein. Sein Inhalt beschreibt, was die Tabelle darstellt. Für assistive Technologien ist dies der offizielle Titel der Tabelle. Wenn ein Screenreader-Nutzer auf eine Tabelle stößt, wird der Inhalt des `<caption>`-Elements als Erstes vorgelesen. Das gibt sofort den nötigen Kontext, um zu entscheiden, ob der Inhalt der Tabelle relevant ist.

```html
<table>
  <caption>Bevölkerungsentwicklung der größten Städte Deutschlands (2010-2020)</caption>
  <!-- Der Rest der Tabelle hier -->
</table>
```

Die `<caption>` ist die Beschriftung, die untrennbar mit der Tabelle verbunden ist. Sie ist der semantische Anker, der den gesamten Datenblock erklärt.

#### Spalten gruppieren mit `<colgroup>` und `<col>`

Manchmal möchtest du vielleicht ganze Spalten formatieren oder ihnen eine bestimmte Bedeutung geben, ohne jede einzelne Zelle mit einer Klasse zu versehen. Hierfür gibt es die Elemente `<colgroup>` und `<col>`.

*   **`<colgroup>`:** Gruppiert eine oder mehrere Spalten.
*   **`<col>`:** Repräsentiert eine einzelne Spalte innerhalb einer `<colgroup>`.

Diese Elemente werden direkt nach dem `<caption>` und vor dem `<thead>` platziert. Ihre Hauptanwendung liegt im Styling, da du ihnen direkt CSS-Regeln zuweisen kannst, die für die gesamte Spalte gelten (allerdings nur für eine begrenzte Anzahl von Eigenschaften wie `background-color`, `border`, `width` und `visibility`).

Obwohl ihr semantischer Wert geringer ist als der von `<thead>` oder `scope`, helfen sie dabei, die Struktur deines Codes zu organisieren und machen deine Absichten klarer.

```html
<table>
  <caption>Monatsbudget</caption>
  <colgroup>
    <col style="background-color: #f2f2f2;"> <!-- Spalte für Kategorien -->
    <col span="2"> <!-- Spalten für "Geplant" und "Tatsächlich" -->
    <col style="background-color: #eaf7e9;"> <!-- Spalte für "Differenz" -->
  </colgroup>
  <thead>
    <tr>
      <th scope="col">Kategorie</th>
      <th scope="col">Geplant</th>
      <th scope="col">Tatsächlich</th>
      <th scope="col">Differenz</th>
    </tr>
  </thead>
  <tbody>
    <!-- ... Datenzeilen ... -->
  </tbody>
</table>
```

Im Beispiel oben formatiert das erste `<col>` die Kategoriespalte, das `span="2"` im zweiten `<col>` sorgt dafür, dass die nächsten beiden Spalten gleich behandelt werden, und das dritte `<col>` hebt die Differenzspalte farblich hervor. Es ist eine saubere Methode, um spaltenbasierte Logik direkt im HTML abzubilden.

Indem du diese Techniken – `<thead>`/`<tbody>`/`<tfoot>`, `scope`, `colspan`/`rowspan` in Kombination mit `scope="colgroup"`/`rowgroup"` und `<caption>` – bewusst einsetzt, verwandelst du ein einfaches Datengitter in eine aussagekräftige, zugängliche und professionell strukturierte Datentabelle. Du schaffst eine Struktur, die nicht nur für das menschliche Auge, sondern auch für Maschinen eindeutig und verständlich ist.
