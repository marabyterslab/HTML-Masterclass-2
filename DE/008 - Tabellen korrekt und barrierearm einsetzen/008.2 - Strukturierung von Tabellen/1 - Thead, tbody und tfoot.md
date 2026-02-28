# thead, tbody und tfoot

### Struktur schaffen mit thead, tbody und tfoot

Wenn du anfängst, mit HTML-Tabellen zu arbeiten, lernst du schnell die grundlegenden Bausteine kennen: `<table>`, `<tr>` für die Zeilen und `<td>` für die Datenzellen. Für eine kleine, übersichtliche Tabelle mit wenigen Einträgen ist das auch völlig ausreichend. Aber was passiert, wenn deine Tabellen wachsen? Wenn sie dutzende oder gar hunderte von Zeilen umfassen, mit Spaltenüberschriften und vielleicht sogar einer Zeile für die Gesamtsumme am Ende? Dann wird es Zeit, deiner Tabelle eine klare, semantische Struktur zu geben. Genau hier kommen die Elemente `<thead>`, `<tbody>` und `<tfoot>` ins Spiel.

Stell dir eine Tabelle wie einen menschlichen Körper vor. Sie hat einen Kopf, einen Rumpf und Füße. Diese einfache Analogie hilft dir, die Rolle der drei Elemente zu verstehen:

*   **`<thead>` (Table Head):** Der Kopfbereich der Tabelle. Hier platzierst du die Zeile(n) mit den Spaltenüberschriften (`<th>`).
*   **`<tbody>` (Table Body):** Der Rumpf oder Körper der Tabelle. Er enthält die eigentlichen Datenzeilen (`<tr>` mit `<td>`).
*   **`<tfoot>` (Table Foot):** Der Fußbereich der Tabelle. Er ist für zusammenfassende Informationen wie Summen, Durchschnitte oder Anmerkungen gedacht.

Diese Elemente sind mehr als nur organisatorische Helferlein. Sie verleihen deiner Tabelle eine semantische Bedeutung, die sowohl für Browser als auch für Hilfstechnologien wie Screenreader von unschätzbarem Wert ist.

#### Warum diese Gliederung so wichtig ist

Bevor wir uns die Elemente im Detail ansehen, lass uns kurz die entscheidenden Vorteile dieser Strukturierung beleuchten:

1.  **Semantik und Lesbarkeit:** Der Code wird selbsterklärend. Wenn du oder ein anderer Entwickler den Quellcode einer Tabelle sehen, ist sofort klar, welcher Teil der Kopf, der Körper und der Fuß ist. Das verbessert die Wartbarkeit des Codes erheblich.
2.  **Styling mit CSS:** Du erhältst mächtige "Haken" für dein CSS. Du kannst den gesamten Kopfbereich anders gestalten als den Körper oder den Fuß, ohne komplexe Klassen oder IDs vergeben zu müssen. Ein dunkler Kopf, hellgrau gestreifte Datenzeilen und ein fettgedruckter Fußbereich werden so zum Kinderspiel.
3.  **Barrierefreiheit (Accessibility):** Für Nutzer von Screenreadern ist diese Struktur ein Segen. Ein Screenreader kann erkennen, was die Kopfzeile ist, und diese bei Bedarf wiederholen, während der Nutzer durch eine lange Datentabelle navigiert. So geht der Kontext der Spalten niemals verloren. Außerdem kann der Screenreader ankündigen, dass die Tabelle einen Kopf- und Fußbereich besitzt, was dem Nutzer eine bessere Orientierung gibt.
4.  **Funktionalität mit JavaScript:** Wenn du Tabelleninhalte dynamisch manipulieren möchtest, kannst du gezielt auf den `<tbody>` zugreifen, um Zeilen hinzuzufügen oder zu entfernen, ohne den `<thead>` oder `<tfoot>` zu beeinflussen. Ein klassisches Anwendungsbeispiel ist auch das Scrollen durch einen langen Tabellenkörper, während der Tabellenkopf und -fuß sichtbar bleiben – eine häufige Anforderung bei Dashboards oder Datenanalysen.

#### Der Tabellenkopf: `<thead>`

Der `<thead>`-Tag umschließt den Kopfbereich deiner Tabelle. In der Regel enthält er eine einzige Tabellenzeile (`<tr>`), in der die Spaltenüberschriften mit dem `<th>`-Tag (Table Header) definiert sind. Das `<th>`-Element signalisiert sowohl dem Browser als auch assistiven Technologien, dass es sich hierbei um eine Überschrift und nicht um eine normale Datenzelle handelt. Browser heben `<th>`-Zellen standardmäßig optisch hervor (meist fett und zentriert).

Ein einfaches Beispiel für den Tabellenkopf sieht so aus:

```html
<table>
  <thead>
    <tr>
      <th>Produktname</th>
      <th>Kategorie</th>
      <th>Preis</th>
    </tr>
  </thead>
  <!-- Hier folgen tbody und tfoot -->
</table>
```

Innerhalb einer Tabelle darf es nur ein einziges `<thead>`-Element geben. Es muss nach dem `<table>`-Tag und eventuellen `<caption>`- oder `<colgroup>`-Elementen stehen.

#### Der Tabellenkörper: `<tbody>`

Der `<tbody>`-Tag ist das Arbeitstier deiner Tabelle. Er umschließt alle Zeilen, die die eigentlichen Daten enthalten. Jede Zeile (`<tr>`) innerhalb des `<tbody>` besteht typischerweise aus `<td>`-Zellen (Table Data).

Ergänzen wir unser vorheriges Beispiel um den Körper:

```html
<table>
  <thead>
    <tr>
      <th>Produktname</th>
      <th>Kategorie</th>
      <th>Preis</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Fair-Trade Kaffee</td>
      <td>Getränke</td>
      <td>7,99 €</td>
    </tr>
    <tr>
      <td>Bio-Haferflocken</td>
      <td>Müsli & Cerealien</td>
      <td>2,49 €</td>
    </tr>
    <tr>
      <td>Vollkornbrot</td>
      <td>Backwaren</td>
      <td>3,29 €</td>
    </tr>
  </tbody>
  <!-- Hier folgt tfoot -->
</table>
```

Eine besonders nützliche Eigenschaft des `<tbody>`-Elements ist, dass du **mehrere `<tbody>`-Elemente** in einer einzigen Tabelle verwenden kannst. Das ist extrem praktisch, um Datenzeilen logisch zu gruppieren. Stell dir vor, du möchtest die Produkte nach Kategorien unterteilen. Jeder `<tbody>` kann dann eine Kategorie repräsentieren.

```html
<table>
  <thead>
    <tr>
      <th>Produktname</th>
      <th>Preis</th>
    </tr>
  </thead>
  <tbody> <!-- Erste Gruppe: Getränke -->
    <tr>
      <th colspan="2">Getränke</th>
    </tr>
    <tr>
      <td>Fair-Trade Kaffee</td>
      <td>7,99 €</td>
    </tr>
    <tr>
      <td>Bio-Apfelsaft</td>
      <td>1,99 €</td>
    </tr>
  </tbody>
  <tbody> <!-- Zweite Gruppe: Backwaren -->
    <tr>
      <th colspan="2">Backwaren</th>
    </tr>
    <tr>
      <td>Vollkornbrot</td>
      <td>3,29 €</td>
    </tr>
    <tr>
      <td>Dinkelbrötchen</td>
      <td>0,89 €</td>
    </tr>
  </tbody>
</table>
```

Durch die Verwendung mehrerer `<tbody>`-Elemente kannst du diese Gruppen separat mit CSS ansprechen (z. B. um einen feinen Rand zwischen den Gruppen zu ziehen) und die semantische Struktur deiner Daten weiter verfeinern.

#### Der Tabellenfuß: `<tfoot>`

Der `<tfoot>`-Tag umschließt den Fußbereich der Tabelle. Hier werden oft zusammenfassende Informationen platziert. Das können Summen, Endergebnisse oder allgemeine Anmerkungen zur Tabelle sein. Ähnlich wie der `<thead>` darf auch der `<tfoot>` nur einmal pro Tabelle vorkommen.

Vervollständigen wir unser erstes Beispiel mit einem Fußbereich, der die Gesamtsumme anzeigt:

```html
<table>
  <thead>
    <tr>
      <th>Produktname</th>
      <th>Kategorie</th>
      <th>Preis</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Fair-Trade Kaffee</td>
      <td>Getränke</td>
      <td>7,99 €</td>
    </tr>
    <tr>
      <td>Bio-Haferflocken</td>
      <td>Müsli & Cerealien</td>
      <td>2,49 €</td>
    </tr>
    <tr>
      <td>Vollkornbrot</td>
      <td>Backwaren</td>
      <td>3,29 €</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="2">Gesamtsumme</td>
      <td>13,77 €</td>
    </tr>
  </tfoot>
</table>
```

Hier nutzen wir das `colspan`-Attribut, um die ersten beiden Zellen der Fußzeile zu einer einzigen Zelle zu verbinden, was für solche Zusammenfassungen typisch ist.

Ein interessanter historischer Hinweis zur Reihenfolge: In älteren HTML-Spezifikationen wurde empfohlen, den `<tfoot>` im Quellcode *vor* dem `<tbody>` zu platzieren. Die Idee dahinter war, dass ein Browser den Kopf- und Fußbereich bereits rendern konnte, während die potenziell sehr große Datenmenge im `<tbody>` noch geladen wurde. Moderne Browser haben damit keine Probleme mehr. Die visuelle Darstellung im Browser ist immer korrekt: Kopf oben, Körper in der Mitte, Fuß unten, unabhängig von der Reihenfolge im Quellcode. Heutzutage gilt die logische Reihenfolge `<thead>`, `<tbody>`, `<tfoot>` als Best Practice, da sie die Lesbarkeit des Codes verbessert.

#### Das Zusammenspiel in der Praxis

Wenn du alle drei Elemente korrekt einsetzt, entsteht eine robuste und flexible Tabellenstruktur. Schauen wir uns an, wie wir die Vorteile nun konkret nutzen können.

##### Styling mit CSS

Mit den semantischen Containern wird das Styling elegant und einfach. Du kannst die Elemente direkt ansprechen, ohne auf Klassen angewiesen zu sein.

```css
/* Grundlegende Tabellenformatierung */
table {
  width: 100%;
  border-collapse: collapse; /* Entfernt doppelte Ränder */
  font-family: sans-serif;
}

/* Styling für den Tabellenkopf */
thead {
  background-color: #333;
  color: white;
  text-align: left;
}

/* Abstand für Kopf- und Datenzellen */
th, td {
  padding: 12px 15px;
  border: 1px solid #ddd;
}

/* Gestreifte Zeilen im Tabellenkörper für bessere Lesbarkeit */
tbody tr:nth-child(even) {
  background-color: #f2f2f2;
}

/* Hover-Effekt für Datenzeilen */
tbody tr:hover {
  background-color: #e0e0e0;
}

/* Styling für den Tabellenfuß */
tfoot {
  background-color: #f8f8f8;
  font-weight: bold;
  border-top: 2px solid #333;
}
```

Mit diesem CSS-Code erhältst du eine professionell aussehende, gut lesbare Tabelle, deren Stilregeln klar von der semantischen HTML-Struktur abgeleitet sind.

##### Ein Gewinn für die Barrierefreiheit

Stell dir einen Nutzer vor, der einen Screenreader verwendet, um sich die Inhalte unserer Produkttabelle vorlesen zu lassen. Ohne die `<thead>`-Struktur müsste er sich bei jeder Zelle merken: "War die erste Spalte der Name oder der Preis?". Mit `<thead>` und `<th>` kann der Screenreader den Kontext herstellen. Wenn der Nutzer zur Zelle "7,99 €" navigiert, kann das Programm ansagen: "Zeile 2, Spalte Preis: 7,99 €". Dieser kleine, aber feine Unterschied macht deine Tabelle für Menschen mit Sehbehinderungen von einer unüberwindbaren Datenwüste zu einer zugänglichen Informationsquelle.

Die Gliederung in `<thead>`, `<tbody>` und `<tfoot>` ist also kein optionaler Luxus, sondern ein grundlegender Baustein für professionelle, barrierearme und wartbare Webentwicklung. Sobald deine Tabellen über eine Handvoll Zeilen hinauswachsen, solltest du dir diese Strukturierung zur Gewohnheit machen.
