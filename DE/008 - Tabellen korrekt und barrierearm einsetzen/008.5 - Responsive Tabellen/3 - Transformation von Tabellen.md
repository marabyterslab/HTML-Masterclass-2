# Transformation von Tabellen

### Transformation von Tabellen: Wenn Spalten zu Zeilen werden

Tabellen sind fantastische Werkzeuge, um strukturierte Daten darzustellen. Ob es sich um eine Liste von Benutzern, Produktspezifikationen oder Finanzberichte handelt – das Zeilen- und Spaltenformat ist für das menschliche Auge auf einem ausreichend großen Bildschirm schnell und logisch erfassbar. Doch was passiert, wenn dieser große Bildschirm nicht vorhanden ist? Auf einem Smartphone wird selbst eine Tabelle mit nur vier oder fünf Spalten schnell zu einem unleserlichen, gequetschten Etwas oder erzwingt unschönes horizontales Scrollen.

Genau hier kommt das Konzept der responsiven Tabellen ins Spiel. Es geht nicht nur darum, die Tabelle irgendwie auf den kleinen Bildschirm zu bekommen. Es geht darum, ihre Lesbarkeit und Nutzbarkeit zu erhalten, indem wir ihre Darstellungsform radikal an den verfügbaren Platz anpassen. Eine der elegantesten und effektivsten Methoden hierfür ist die Transformation der Tabelle. Anstatt einer horizontalen Anordnung von Daten verwandeln wir jede Tabellenzeile in eine Art „Karte“ oder einen Block, in dem die Daten untereinander dargestellt werden.

#### Das Ausgangsmaterial: Eine klassische Tabelle

Stell dir eine einfache Tabelle vor, die eine Liste von Teammitgliedern anzeigt. Im HTML sieht sie semantisch korrekt so aus:

```html
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Position</th>
      <th>Abteilung</th>
      <th>Beitrittsdatum</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Anna Müller</td>
      <td>Lead Developer</td>
      <td>Technik</td>
      <td>15.03.2020</td>
    </tr>
    <tr>
      <td>Ben Schmidt</td>
      <td>UX/UI Designer</td>
      <td>Design</td>
      <td>01.08.2021</td>
    </tr>
    <tr>
      <td>Carla Weber</td>
      <td>Projektmanagerin</td>
      <td>Management</td>
      <td>10.01.2019</td>
    </tr>
  </tbody>
</table>
```

Auf einem Desktop-Computer sieht das sauber und übersichtlich aus. Auf einem Smartphone hingegen bricht das Layout. Die Spalten werden schmal, der Text umbricht unschön, und die gesamte Struktur wird schwer lesbar.

#### Die einfachste Lösung: Horizontales Scrollen

Bevor wir zur eigentlichen Transformation kommen, sei die einfachste Notlösung erwähnt: das horizontale Scrollen. Du kannst die Tabelle in ein `div`-Element einbetten und diesem per CSS anweisen, bei Bedarf eine Scrollleiste anzuzeigen.

```html
<div class="table-wrapper">
  <table>
    <!-- ... dein Tabelleninhalt ... -->
  </table>
</div>
```

Das dazugehörige CSS ist denkbar simpel:

```css
.table-wrapper {
  overflow-x: auto;
  width: 100%;
}
```

Diese Methode bewahrt die ursprüngliche Tabellenstruktur, was in manchen Fällen, etwa bei sehr breiten Finanztabellen, sogar erwünscht sein kann. Der Nachteil ist jedoch die Benutzerfreundlichkeit. Der Nutzer muss seitwärts scrollen, um alle Informationen einer Zeile zu sehen, was den Vergleich verschiedener Zeilen erschwert. Es ist eine pragmatische, aber keine elegante Lösung.

#### Die Transformation: Von der Tabelle zum Kartenstapel

Die weitaus benutzerfreundlichere Methode ist die vollständige Transformation der Darstellung auf kleinen Bildschirmen. Wir nutzen CSS, um die tabellarische Anzeige komplett aufzuheben und jede `<tr>`-Zeile als einen eigenen, vertikalen Block darzustellen.

Der Schlüssel zu dieser Technik liegt in zwei Dingen:
1.  Wir brechen das visuelle Tabellenmodell mit der `display`-Eigenschaft von CSS.
2.  Wir nutzen `data`-Attribute im HTML, um die Spaltenüberschriften zu speichern und sie dann mit CSS-Pseudo-Elementen wieder sichtbar zu machen.

**Schritt 1: Das HTML mit `data`-Attributen vorbereiten**

Damit wir später in unserem CSS wissen, welche Beschriftung zu welcher Zelle gehört, müssen wir diese Information direkt in die `<td>`-Elemente schreiben. `data`-Attribute sind dafür perfekt geeignet, da sie für genau solche Zwecke gedacht sind: benutzerdefinierte Daten zu speichern, die von Skripten oder CSS genutzt werden können, ohne die Semantik zu stören.

Wir erweitern unser HTML also wie folgt:

```html
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Position</th>
      <th>Abteilung</th>
      <th>Beitrittsdatum</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-label="Name">Anna Müller</td>
      <td data-label="Position">Lead Developer</td>
      <td data-label="Abteilung">Technik</td>
      <td data-label="Beitrittsdatum">15.03.2020</td>
    </tr>
    <tr>
      <td data-label="Name">Ben Schmidt</td>
      <td data-label="Position">UX/UI Designer</td>
      <td data-label="Abteilung">Design</td>
      <td data-label="Beitrittsdatum">01.08.2021</td>
    </tr>
    <tr>
      <td data-label="Name">Carla Weber</td>
      <td data-label="Position">Projektmanagerin</td>
      <td data-label="Abteilung">Management</td>
      <td data-label="Beitrittsdatum">10.01.2019</td>
    </tr>
  </tbody>
</table>
```
Jede Zelle im `<tbody>` hat nun ein `data-label`-Attribut, das den Text ihrer zugehörigen Spaltenüberschrift enthält. Das ist die entscheidende Vorbereitung.

**Schritt 2: Die CSS-Transformation per Media Query**

Nun kommt die Magie mit CSS. Wir wollen diese Transformation nur auf schmalen Bildschirmen anwenden, also packen wir alle unsere Regeln in eine `@media`-Query. Ein typischer Breakpoint für Smartphones liegt bei etwa 768 Pixeln oder weniger.

```css
/* Grundlegende Stile für die Tabelle (optional, aber empfohlen) */
table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 20px;
}

th, td {
  padding: 10px 15px;
  text-align: left;
  border: 1px solid #ddd;
}

th {
  background-color: #f2f2f2;
}

/* Die Transformation für kleine Bildschirme */
@media (max-width: 768px) {
  /* 1. Die ursprünglichen Tabellen-Header ausblenden */
  thead {
    display: none;
  }

  /* 2. Das Tabellenlayout aufbrechen */
  table, tbody, tr, td {
    display: block;
    width: 100%;
  }

  /* 3. Jede Zeile wie eine Karte behandeln */
  tr {
    margin-bottom: 15px;
  }

  td {
    text-align: right; /* Den Zellinhalt rechts ausrichten */
    padding-left: 50%; /* Platz für das Label schaffen */
    position: relative; /* Wichtig für die Positionierung des Pseudo-Elements */
    border-bottom: none; /* Ästhetische Anpassung */
  }

  /* Letzte Zelle einer "Karte" bekommt wieder einen unteren Rand */
  tr td:last-child {
    border-bottom: 1px solid #ddd;
  }

  /* 4. Das Label mit dem ::before-Pseudo-Element einfügen */
  td::before {
    content: attr(data-label); /* Holt den Text aus dem data-label Attribut */
    position: absolute;
    left: 15px;
    width: calc(50% - 30px); /* Breite des Labels anpassen */
    text-align: left;
    font-weight: bold;
  }
}
```

Lass uns diese CSS-Regeln Schritt für Schritt durchgehen:

1.  `thead { display: none; }`: Da wir die Beschriftungen nun in jeder Zelle anzeigen, wird der ursprüngliche Tabellenkopf (`<thead>`) überflüssig. Wir blenden ihn komplett aus.

2.  `table, tbody, tr, td { display: block; }`: Dies ist der entscheidende Punkt. Wir heben das Standardverhalten von Tabellenelementen auf. Statt `display: table`, `display: table-row` usw. behandeln wir jedes Element als einfachen Block. Das bewirkt, dass sie sich untereinander anordnen, wie es `div`-Elemente standardmäßig tun.

3.  `tr { margin-bottom: 15px; }`: Jede ursprüngliche Zeile (`<tr>`) wird nun zu einem visuellen Block, einer „Karte“. Mit einem Außenabstand sorgen wir für eine klare Trennung zwischen den einzelnen Datensätzen.

4.  `td { ... }`: Die Zellen (`<td>`) werden ebenfalls zu Blöcken. Wir richten den Text rechtsbündig aus, um eine klare Trennlinie zwischen Label und Wert zu schaffen. Der `padding-left: 50%` schafft auf der linken Seite Platz, wo wir gleich die Beschriftung einfügen werden. `position: relative` ist notwendig, damit wir das `::before`-Pseudo-Element absolut innerhalb der Zelle positionieren können.

5.  `td::before { ... }`: Hier geschieht die eigentliche Magie.
    *   `content: attr(data-label);`: Diese CSS-Funktion liest den Wert des `data-label`-Attributs aus unserem HTML und fügt ihn als Inhalt des Pseudo-Elements ein.
    *   `position: absolute; left: 15px;`: Wir positionieren die Beschriftung absolut am linken Rand der Zelle.
    *   Die weiteren Eigenschaften (`width`, `text-align`, `font-weight`) dienen der sauberen Formatierung, sodass die Beschriftung linksbündig, fett und klar vom rechtsbündigen Wert getrennt ist.

Das Ergebnis ist eine perfekt lesbare, vertikale Liste auf dem Smartphone. Jeder Datensatz ist als eine in sich geschlossene Karte erkennbar. Der Kontext (also welche Information welcher Wert ist) geht nie verloren, da die Beschriftung immer direkt neben dem Wert steht.

#### Verfeinerung mit Flexbox

Die obige Methode ist robust und funktioniert hervorragend. Du kannst die Ausrichtung innerhalb der Zellen noch moderner und flexibler gestalten, indem du auf Flexbox setzt, anstatt mit `padding` und `position: absolute` zu arbeiten.

Eine alternative CSS-Regel für die `<td>`-Zelle könnte so aussehen:

```css
@media (max-width: 768px) {
  /* ... andere Regeln bleiben gleich ... */

  td {
    display: flex;
    justify-content: space-between; /* Label links, Inhalt rechts */
    align-items: center;
    border-bottom: 1px solid #eee;
    padding: 10px 15px;
  }

  td::before {
    content: attr(data-label);
    font-weight: bold;
    padding-right: 10px; /* Ein wenig Abstand zum Wert */
  }

  tr {
    border: 1px solid #ddd;
    margin-bottom: 15px;
  }
}
```

In diesem Ansatz verwandeln wir jede `<td>`-Zelle in einen Flex-Container. `justify-content: space-between` sorgt dafür, dass sich das `::before`-Element (das Label) an den linken Rand und der eigentliche Zellinhalt an den rechten Rand schiebt. Das macht die Positionierung oft einfacher und das Layout widerstandsfähiger gegenüber unterschiedlichen Inhaltslängen.

Welche Methode du wählst, hängt von deinen Vorlieben ab. Beide führen zu einem ähnlichen, exzellenten Ergebnis: einer Tabelle, die auf jedem Gerät nicht nur funktioniert, sondern auch elegant und benutzerfreundlich bleibt. Du hast die starre Struktur der Tabelle für kleine Ansichten transformiert, ohne dabei die semantische Bedeutung deines HTML-Markups zu verlieren.
