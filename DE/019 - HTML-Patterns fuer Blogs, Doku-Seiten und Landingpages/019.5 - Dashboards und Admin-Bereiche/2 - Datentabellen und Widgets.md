# Datentabellen und Widgets

### Datentabellen und Widgets: Das Herzstück jedes Dashboards

Wenn du einen Admin-Bereich oder ein Dashboard gestaltest, dreht sich fast alles um Daten. Du möchtest Zahlen, Fakten und Zusammenhänge auf einen Blick erfassen, um fundierte Entscheidungen zu treffen. Im Webdesign gibt es zwei fundamentale Werkzeuge, um diese Datenflut zu bändigen und verständlich darzustellen: klassische Datentabellen und moderne Widgets. Beide haben ihre Berechtigung und ihren festen Platz, doch sie dienen unterschiedlichen Zwecken. Die Tabelle liefert dir die granulare, detaillierte Ansicht, während das Widget dir den schnellen, zusammengefassten Überblick verschafft.

Lass uns eintauchen, wie du beide Elemente mit sauberem, semantischem HTML aufbaust und damit die Grundlage für ein leistungsstarkes und benutzerfreundliches Dashboard legst.

#### Die Kunst der Datentabelle: Mehr als nur Zeilen und Spalten

Tabellen haben im Web eine bewegte Geschichte. Früher wurden sie missbraucht, um komplexe Seitenlayouts zu erstellen – eine Praxis, die heute glücklicherweise der Vergangenheit angehört. Die wahre Stärke von HTML-Tabellen liegt in ihrer ursprünglichen Bestimmung: der Darstellung von tabellarischen Daten. Das sind Informationen, die eine klare Beziehung zwischen Zeilen und Spalten haben, wie zum Beispiel eine Benutzerliste, eine Produktübersicht oder Finanzdaten.

Ein Dashboard ohne eine gut strukturierte Tabelle ist kaum vorstellbar. Hier siehst du nicht nur die Daten, sondern kannst sie oft auch sortieren, filtern und durchsuchen. Die Basis für all diese Interaktionen ist eine solide HTML-Struktur.

##### Der semantische Aufbau einer Tabelle

Eine korrekte Tabelle besteht aus mehr als nur `<table>`, `<tr>` und `<td>`. Für maximale Lesbarkeit, Barrierefreiheit und Styling-Möglichkeiten solltest du die semantischen Strukturelemente nutzen.

-   `<table>`: Der Container für die gesamte Tabelle.
-   `<caption>`: Eine sichtbare Überschrift, die den Inhalt der Tabelle beschreibt. Sie ist essenziell für die Barrierefreiheit, da Screenreader sie vorlesen, um Nutzern Kontext zu geben.
-   `<thead>`: Der Tabellenkopf. Hier platzierst du die Zeile (`<tr>`) mit den Spaltenüberschriften (`<th>`).
-   `<tbody>`: Der Tabellenkörper. Er enthält die eigentlichen Datenzeilen (`<tr>`) mit den Datenzellen (`<td>`).
-   `<tfoot>`: Der Tabellenfuß. Er ist optional und kann für Zusammenfassungen oder Endergebnisse genutzt werden.

Schauen wir uns das an einem Beispiel für eine einfache Benutzerliste an:

```html
<table>
  <caption>Aktive Benutzer im System</caption>
  <thead>
    <tr>
      <th scope="col">Benutzer-ID</th>
      <th scope="col">Name</th>
      <th scope="col">E-Mail-Adresse</th>
      <th scope="col">Rolle</th>
      <th scope="col">Letzter Login</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>101</td>
      <td>Anna Schmidt</td>
      <td>anna.schmidt@example.com</td>
      <td>Admin</td>
      <td>2023-10-26 14:30</td>
    </tr>
    <tr>
      <td>102</td>
      <td>Ben Müller</td>
      <td>ben.mueller@example.com</td>
      <td>Editor</td>
      <td>2023-10-26 11:15</td>
    </tr>
    <tr>
      <td>103</td>
      <td>Carla Huber</td>
      <td>carla.huber@example.com</td>
      <td>Viewer</td>
      <td>2023-10-25 09:00</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="5">Insgesamt 3 aktive Benutzer</td>
    </tr>
  </tfoot>
</table>
```

Dir fallen vielleicht die `scope`-Attribute in den `<th>`-Elementen auf. `scope="col"` teilt dem Browser (und assistiven Technologien) explizit mit, dass diese Zelle eine Überschrift für die gesamte Spalte ist. Dies verbessert die Zugänglichkeit erheblich, da ein Screenreader die Verbindung zwischen einer Datenzelle und ihrer zugehörigen Überschrift herstellen kann.

Das `colspan="5"` im `<tfoot>` sorgt dafür, dass sich die eine Zelle über alle fünf Spalten erstreckt – perfekt für eine zusammenfassende Zeile.

##### Tabellen für die moderne Welt: Styling und Responsivität

Eine nackte HTML-Tabelle sieht selten ansprechend aus. Mit CSS kannst du sie jedoch schnell in eine übersichtliche und gut lesbare Komponente verwandeln. Ein gängiges Muster ist das "Zebra-Stripping", bei dem jede zweite Zeile eine andere Hintergrundfarbe erhält, um die Lesbarkeit zu verbessern.

```css
table {
  width: 100%;
  border-collapse: collapse; /* Entfernt doppelte Ränder */
  font-family: sans-serif;
}

caption {
  font-size: 1.2em;
  margin-bottom: 10px;
  font-weight: bold;
  text-align: left;
}

th, td {
  padding: 12px 15px;
  border: 1px solid #ddd;
  text-align: left;
}

thead th {
  background-color: #f2f2f2;
}

tbody tr:nth-of-type(even) {
  background-color: #f9f9f9;
}

tbody tr:hover {
  background-color: #f1f1f1;
}

tfoot td {
  font-weight: bold;
  background-color: #f2f2f2;
}
```

Die größte Herausforderung bei Tabellen ist die Darstellung auf kleinen Bildschirmen. Breite Tabellen mit vielen Spalten sprengen schnell das Layout eines Smartphones. Die einfachste und robusteste Lösung ist, die Tabelle horizontal scrollbar zu machen, wenn sie nicht mehr auf den Bildschirm passt. Dazu packst du die Tabelle in ein `<div>` und gibst diesem Container die entsprechende CSS-Eigenschaft.

HTML-Struktur:
```html
<div class="table-wrapper">
  <table>
    <!-- Der gesamte Tabelleninhalt von oben -->
  </table>
</div>
```

CSS:
```css
.table-wrapper {
  overflow-x: auto;
}
```
Diese simple Technik stellt sicher, dass deine Seite auf dem Handy nicht unbrauchbar wird, nur weil eine Tabelle zu breit ist. Der Nutzer kann einfach nach links und rechts wischen, um alle Daten zu sehen.

#### Widgets: Visuelle Informationshäppchen

Während Tabellen ins Detail gehen, dienen Widgets dazu, die wichtigsten Kennzahlen (Key Performance Indicators, KPIs) auf einen Blick zu präsentieren. Stell sie dir wie die Anzeigen auf dem Armaturenbrett deines Autos vor: Du siehst sofort deine Geschwindigkeit, den Tankfüllstand und die Motortemperatur, ohne ein Handbuch studieren zu müssen.

In einem Admin-Dashboard könnten das Widgets für "Neue Anmeldungen heute", "Aktuelle Serverauslastung" oder "Umsatz des letzten Monats" sein. Im Gegensatz zur `<table>` gibt es kein spezifisches `<widget>`-Element in HTML. Stattdessen baust du Widgets aus einer Kombination von Standardelementen, die du semantisch passend zusammensetzt.

##### Die Anatomie eines typischen Widgets

Ein Widget ist im Grunde eine kleine, in sich geschlossene Box – eine Karte. Die Struktur ist meistens ähnlich:
1.  **Ein Container:** Oft ein `<div>` oder, wenn der Inhalt für sich allein stehen könnte, ein `<section>`- oder `<article>`-Element.
2.  **Eine Überschrift:** Eine `<h2>` oder `<h3>`, die klar benennt, was das Widget anzeigt.
3.  **Der Hauptinhalt:** Das kann eine große Zahl, ein kleines Diagramm (oft als `<img>`, `<svg>` oder mit einem `<canvas>`-Element realisiert) oder eine kurze Liste sein.
4.  **(Optional) Ein Footer:** Häufig mit einem Link wie "Details anzeigen", der zur entsprechenden detaillierten Tabellenansicht führt.

Schauen wir uns den HTML-Aufbau für ein typisches "Statistik-Widget" an:

```html
<div class="widget-card">
  <h3 class="widget-title">Neue Bestellungen</h3>
  <div class="widget-content">
    <p class="widget-value">42</p>
    <p class="widget-change increase">+5% seit gestern</p>
  </div>
  <div class="widget-footer">
    <a href="/orders/all">Alle Bestellungen ansehen</a>
  </div>
</div>
```

Dieses HTML ist einfach, aber aussagekräftig. Wir verwenden Klassen, um die einzelnen Teile des Widgets zu identifizieren, was das Styling mit CSS enorm erleichtert.

##### Widgets zum Leben erwecken mit CSS

Die Magie der Widgets entfaltet sich erst durch das CSS. Hier definierst du das kartenähnliche Aussehen und sorgst für eine klare visuelle Hierarchie.

```css
.widget-card {
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 20px;
  display: flex;
  flex-direction: column;
}

.widget-title {
  margin: 0 0 15px 0;
  font-size: 1em;
  color: #666;
  font-weight: normal;
}

.widget-content {
  flex-grow: 1; /* Sorgt dafür, dass der Inhalt den Platz füllt */
}

.widget-value {
  margin: 0;
  font-size: 2.5em;
  font-weight: bold;
  color: #333;
}

.widget-change {
  margin: 5px 0 0 0;
  font-size: 0.9em;
}

.widget-change.increase {
  color: #28a745; /* Grün für positive Veränderung */
}

.widget-change.decrease {
  color: #dc3545; /* Rot für negative Veränderung */
}

.widget-footer {
  margin-top: 20px;
  font-size: 0.9em;
}

.widget-footer a {
  color: #007bff;
  text-decoration: none;
}

.widget-footer a:hover {
  text-decoration: underline;
}
```

Mit diesem CSS erhältst du eine saubere, moderne Karte, die Informationen effektiv kommuniziert. In einem Dashboard würdest du typischerweise mehrere solcher Widgets in einem Grid- oder Flexbox-Layout anordnen, um eine übersichtliche Startseite zu schaffen.

#### Das Zusammenspiel von Tabellen und Widgets

Die wahre Stärke eines Dashboards liegt in der Kombination beider Elemente. Die Widgets auf der Startseite geben dir den schnellen Überblick. Du siehst sofort: "Ah, 42 neue Bestellungen, das sind 5 % mehr als gestern." Wenn dich diese Zahl neugierig macht, klickst du auf den Link "Alle Bestellungen ansehen". Dieser Link führt dich dann zu einer Seite mit einer detaillierten Datentabelle, in der du jede einzelne der 42 Bestellungen mit allen relevanten Informationen (Bestellnummer, Kunde, Wert, Status) sehen, sortieren und filtern kannst.

Die Widgets sind das "Was", die Tabellen sind das "Warum" und "Wer". Dein Fundament für beides ist und bleibt sauberes, semantisches HTML. Es sorgt nicht nur dafür, dass deine Seite zugänglich und wartbar ist, sondern bietet auch die perfekte Leinwand für das CSS, das die Optik bestimmt, und das JavaScript, das später für dynamische Daten und Interaktivität sorgt.
