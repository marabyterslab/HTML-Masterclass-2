# Tabellen als Datenbasis

### Tabellen als Datenbasis

Wenn du an HTML-Tabellen denkst, kommt dir wahrscheinlich zuerst die klassische, zeilen- und spaltenbasierte Darstellung von Informationen in den Sinn. Eine Preisliste, Kontaktdaten, Öffnungszeiten – die typischen Anwendungsfälle. Doch unter dieser einfachen Oberfläche verbirgt sich ein mächtiges Konzept, das oft übersehen wird: Eine gut strukturierte HTML-Tabelle ist nicht nur eine visuelle Darstellung, sondern eine vollwertige, semantische Datenquelle, die direkt in deinem Dokument lebt.

Stell dir eine Tabelle nicht nur als etwas vor, das du ansiehst, sondern als eine Mini-Datenbank, die im Browser wartet, ausgelesen und weiterverarbeitet zu werden. Dieser Ansatz ist besonders elegant, wenn die Daten, die du visualisieren oder interaktiv gestalten möchtest, bereits aus inhaltlichen Gründen auf der Seite vorhanden sein müssen. Anstatt dieselben Daten zusätzlich als JSON-Objekt in ein Skript einzubetten oder per API nachzuladen, nutzt du einfach das, was schon da ist. Das ist effizient, reduziert Redundanz und ist oft eine hervorragende Lösung für progressive Verbesserungen (Progressive Enhancement).

#### Die semantische Grundlage: Mehr als nur Zeilen und Spalten

Damit dieser Ansatz funktioniert, ist eine saubere, semantische HTML-Struktur unerlässlich. Eine Tabelle, die nur aus `<table>`, `<tr>` und `<td>` besteht, ist zwar visuell eine Tabelle, aber für eine Maschine schwer zu interpretieren. Die entscheidenden Bausteine für eine maschinenlesbare Datenstruktur sind `<thead>`, `<tbody>` und `<th>`.

-   `<thead>` (Table Head): Dieser Bereich umschließt die Kopfzeile(n) der Tabelle.
-   `<th>` (Table Header): Diese Zellen innerhalb des `<thead>` definieren die Überschriften für jede Spalte. Sie sind die "Schlüssel" oder "Properties" unserer zukünftigen Datenobjekte.
-   `<tbody>` (Table Body): Hier befinden sich die eigentlichen Datenzeilen, die die "Datensätze" darstellen.
-   `<tr>` (Table Row): Jede Zeile im `<tbody>` entspricht einem einzelnen Datensatz oder Objekt.
-   `<td>` (Table Data): Jede Zelle in einer Zeile enthält einen "Wert" für den entsprechenden Schlüssel aus dem Tabellenkopf.

Betrachten wir ein konkretes Beispiel. Angenommen, wir haben eine einfache Tabelle mit Verkaufsdaten:

```html
<table id="verkaufsdaten">
  <thead>
    <tr>
      <th>Monat</th>
      <th>Umsatz</th>
      <th>Einheiten</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Januar</td>
      <td>45.000 €</td>
      <td>230</td>
    </tr>
    <tr>
      <td>Februar</td>
      <td>52.000 €</td>
      <td>280</td>
    </tr>
    <tr>
      <td>März</td>
      <td>61.000 €</td>
      <td>310</td>
    </tr>
  </tbody>
</table>
```

Diese Struktur ist nicht nur für Menschen und Screenreader klar verständlich, sondern auch perfekt für ein Skript vorbereitet. Der `<thead>` gibt uns die Schlüssel (`Monat`, `Umsatz`, `Einheiten`), und jeder `<tr>` im `<tbody>` ist ein kompletter Datensatz, den wir nun extrahieren können.

#### Der Zugriff per JavaScript: Vom DOM zum Datenobjekt

Jetzt kommt der spannende Teil: Wie verwandeln wir diese HTML-Struktur in ein nutzbares JavaScript-Datenformat, zum Beispiel in ein Array von Objekten? Der Prozess lässt sich in wenige, logische Schritte unterteilen.

**1. Die Kopfzeilen (Schlüssel) auslesen**

Zuerst müssen wir die Spaltenüberschriften aus dem `<thead>` extrahieren. Sie werden die Eigenschaftsnamen für unsere Objekte sein.

```javascript
const tabelle = document.querySelector('#verkaufsdaten');
const kopfZellen = tabelle.querySelectorAll('thead th');

const schluessel = [];
kopfZellen.forEach(kopfZelle => {
  // Wir wandeln den Text in Kleinbuchstaben um und entfernen Sonderzeichen,
  // um saubere und konsistente Schlüssel zu erhalten.
  schluessel.push(kopfZelle.textContent.toLowerCase().trim());
});

// Ergebnis: schluessel ist jetzt ['monat', 'umsatz', 'einheiten']
```

Wir haben nun ein Array mit den Namen unserer zukünftigen Objekteigenschaften. Dieser Schritt ist entscheidend, denn er macht unseren Code flexibel. Wenn du später eine Spalte hinzufügst oder umbenennst, passt sich das Skript automatisch an, ohne dass du den Code ändern musst.

**2. Die Datenzeilen (Werte) verarbeiten**

Als Nächstes durchlaufen wir jede Zeile (`<tr>`) im `<tbody>`, um die einzelnen Datensätze zu erfassen. Für jede Zeile erstellen wir ein neues Objekt.

```javascript
const datenZeilen = tabelle.querySelectorAll('tbody tr');
const datenArray = [];

datenZeilen.forEach(zeile => {
  const datensatz = {};
  const zellen = zeile.querySelectorAll('td');

  zellen.forEach((zelle, index) => {
    // Wir verwenden den Index der Zelle, um den passenden Schlüssel
    // aus unserem zuvor erstellten 'schluessel'-Array zu finden.
    const aktuellerSchluessel = schluessel[index];
    datensatz[aktuellerSchluessel] = zelle.textContent.trim();
  });

  datenArray.push(datensatz);
});

// Das finale Ergebnis in der Konsole ausgeben
console.log(datenArray);
```

Wenn du diesen Code ausführst, erhältst du in der Browser-Konsole eine saubere JavaScript-Datenstruktur:

```json
[
  {
    "monat": "Januar",
    "umsatz": "45.000 €",
    "einheiten": "230"
  },
  {
    "monat": "Februar",
    "umsatz": "52.000 €",
    "einheiten": "280"
  },
  {
    "monat": "März",
    "umsatz": "61.000 €",
    "einheiten": "310"
  }
]
```

Herzlichen Glückwunsch! Du hast soeben eine HTML-Tabelle in ein strukturiertes, nutzbares Datenformat umgewandelt. Diese Datenbasis ist nun bereit für den nächsten Schritt: die Visualisierung.

#### Vom Datenobjekt zur Visualisierung

Mit diesem `datenArray` stehen dir nun alle Türen offen. Du kannst diese Daten an eine Chart-Bibliothek wie Chart.js oder D3.js übergeben, um dynamische Diagramme zu erzeugen. Du könntest die Daten nutzen, um eine interaktive Filter- oder Sortierfunktion für die Tabelle zu bauen, ohne die Seite neu laden zu müssen. Oder du könntest eine völlig andere Darstellung der Daten generieren, wie zum Beispiel eine Reihe von "Karten"-Elementen.

Ein einfaches Beispiel: Erstellen wir aus den Daten eine simple, unformatierte Liste, nur um das Prinzip zu verdeutlichen.

```javascript
// Annahme: datenArray existiert bereits aus dem vorherigen Schritt

const container = document.createElement('div');
document.body.appendChild(container); // Fügt den Container zum Dokument hinzu

datenArray.forEach(eintrag => {
  const infoElement = document.createElement('p');
  infoElement.textContent = `Im ${eintrag.monat} wurden ${eintrag.einheiten} Einheiten verkauft, was einem Umsatz von ${eintrag.umsatz} entspricht.`;
  container.appendChild(infoElement);
});
```
Dieses simple Beispiel zeigt die grundlegende Macht dieses Konzepts: Die Originaltabelle bleibt als semantische und für Screenreader zugängliche Basis bestehen, während du mit JavaScript eine völlig neue, dynamische Repräsentation der darin enthaltenen Daten erschaffst.

#### Fortgeschrittene Technik: `data-`Attribute für rohe Daten

Ein kleines Problem bleibt in unserem Beispiel bestehen: Der Umsatz (`"45.000 €"`) und die Einheiten (`"230"`) sind als Strings extrahiert worden. Mit dem Währungssymbol und dem Tausenderpunkt ist der Umsatz für Berechnungen unbrauchbar. Die Einheiten könnten zwar mit `parseInt()` umgewandelt werden, aber es geht eleganter.

Hier kommen `data-`Attribute ins Spiel. Sie erlauben es uns, maschinenlesbare Rohdaten direkt an unsere HTML-Elemente zu hängen, ohne die für den Menschen lesbare Darstellung zu beeinträchtigen.

Passen wir unsere Tabelle an:

```html
<table id="verkaufsdaten-optimiert">
  <thead>
    <tr>
      <th>Monat</th>
      <th>Umsatz</th>
      <th>Einheiten</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Januar</td>
      <td data-wert="45000">45.000 €</td>
      <td data-wert="230">230</td>
    </tr>
    <tr>
      <td>Februar</td>
      <td data-wert="52000">52.000 €</td>
      <td data-wert="280">280</td>
    </tr>
    <tr>
      <td>März</td>
      <td data-wert="61000">61.000 €</td>
      <td data-wert="310">310</td>
    </tr>
  </tbody>
</table>
```

Der sichtbare Inhalt bleibt gleich, aber wir haben nun einen sauberen, numerischen Wert im `data-wert`-Attribut. Unser JavaScript-Code kann nun darauf zugreifen und die Datenqualität erheblich verbessern.

Wir modifizieren die innere Schleife unseres Skripts:

```javascript
// ... (der äußere Teil des Skripts bleibt gleich)

zellen.forEach((zelle, index) => {
  const aktuellerSchluessel = schluessel[index];
  
  // Prüfen, ob ein data-wert-Attribut vorhanden ist
  if (zelle.dataset.wert) {
    // Wandle den Wert in eine Zahl um
    datensatz[aktuellerSchluessel] = parseFloat(zelle.dataset.wert);
  } else {
    // Ansonsten nimm den sichtbaren Text
    datensatz[aktuellerSchluessel] = zelle.textContent.trim();
  }
});

// ...
```

Das Ergebnis ist nun ein Array mit echten Zahlen, bereit für mathematische Operationen, Sortierungen oder die Achsen eines Diagramms:

```json
[
  {
    "monat": "Januar",
    "umsatz": 45000,
    "einheiten": 230
  },
  {
    "monat": "Februar",
    "umsatz": 52000,
    "einheiten": 280
  },
  {
    "monat": "März",
    "umsatz": 61000,
    "einheiten": 310
  }
]
```

Diese Methode, semantische HTML-Tabellen als stille Datenlieferanten zu nutzen, ist ein Paradebeispiel für die Trennung von Inhalt (HTML), Präsentation (CSS) und Verhalten (JavaScript). Du erhältst eine barrierefreie, suchmaschinenfreundliche und bei deaktiviertem JavaScript immer noch funktionale Webseite, die du mit wenigen Zeilen Code in eine interaktive Datenanwendung verwandeln kannst.
