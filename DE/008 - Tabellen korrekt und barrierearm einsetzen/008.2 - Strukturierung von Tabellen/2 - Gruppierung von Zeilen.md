# Gruppierung von Zeilen

### Gruppierung von Zeilen: Mehr als nur Optik

Wenn du beginnst, Tabellen in HTML zu erstellen, konzentrierst du dich wahrscheinlich zuerst auf die grundlegenden Bausteine: `<table>`, `<tr>`, `<th>` und `<td>`. Das ist völlig ausreichend für einfache, kleine Datensammlungen. Doch was passiert, wenn deine Tabellen komplexer werden? Wenn sie Dutzende oder Hunderte von Zeilen umfassen und vielleicht sogar eine Zusammenfassung am Ende benötigen?

Hier kommt die semantische Gruppierung von Zeilen ins Spiel. Anstatt alle deine `<tr>`-Elemente einfach hintereinander in den `<table>`-Tag zu werfen, gibt dir HTML mächtige Werkzeuge an die Hand, um deine Tabelle in logische Abschnitte zu unterteilen: einen Kopf, einen Körper und einen Fuß. Diese Werkzeuge sind die Elemente `<thead>`, `<tbody>` und `<tfoot>`.

Auf den ersten Blick mag das wie unnötiger Mehraufwand erscheinen. Schließlich sieht die Tabelle im Browser oft erst einmal gleich aus. Aber die wahre Stärke dieser Elemente liegt unter der Haube. Sie verleihen deiner Tabelle eine klare, maschinenlesbare Struktur, die sowohl für die Barrierefreiheit, das Styling mit CSS als auch für die Manipulation mit JavaScript von unschätzbarem Wert ist.

#### Die drei Musketiere der Tabellenstruktur

Stell dir eine Tabelle wie ein Dokument oder einen Brief vor. Sie hat einen Briefkopf (Header), den eigentlichen Inhalt (Body) und oft eine Fußzeile mit einer Zusammenfassung oder einem Gruß (Footer). Genau dieses Prinzip bilden `<thead>`, `<tbody>` und `<tfoot>` in HTML ab.

*   **`<thead>` (Table Head):** Dieses Element umschließt den Kopfbereich deiner Tabelle. Hier gehören die Zeilen (`<tr>`) hin, die die Spaltenüberschriften (`<th>`) enthalten. Auch wenn es oft nur eine einzige Zeile ist, sorgt die Kapselung in `<thead>` für eine eindeutige semantische Abgrenzung.
*   **`<tbody>` (Table Body):** Hier spielt die Musik. Der Tabellenkörper umschließt alle Zeilen (`<tr>`), die die eigentlichen Daten (`<td>`) enthalten. Dies ist in der Regel der längste Abschnitt deiner Tabelle.
*   **`<tfoot>` (Table Foot):** Dieses Element ist für den Fußbereich der Tabelle reserviert. Es enthält Zeilen mit zusammenfassenden Informationen, wie Summen, Durchschnitte oder andere Endergebnisse.

#### Ein praktisches Beispiel: Vom Chaos zur Ordnung

Nehmen wir an, du möchtest eine einfache Abrechnung für ein Projekt darstellen. Ohne semantische Gruppierung könnte dein Code so aussehen:

```html
<table>
  <caption>Projekt-Abrechnung Q3</caption>
  <tr>
    <th>Leistung</th>
    <th>Stunden</th>
    <th>Stundensatz</th>
    <th>Summe</th>
  </tr>
  <tr>
    <td>Konzeption & Design</td>
    <td>20</td>
    <td>90 €</td>
    <td>1800 €</td>
  </tr>
  <tr>
    <td>Frontend-Entwicklung</td>
    <td>45</td>
    <td>110 €</td>
    <td>4950 €</td>
  </tr>
  <tr>
    <td>Backend-Anbindung</td>
    <td>30</td>
    <td>120 €</td>
    <td>3600 €</td>
  </tr>
  <tr>
    <td><strong>Gesamtsumme</strong></td>
    <td colspan="2"></td>
    <td><strong>10350 €</strong></td>
  </tr>
</table>
```

Diese Tabelle funktioniert und wird korrekt angezeigt. Aber für eine Maschine (wie einen Screenreader oder eine Suchmaschine) ist die letzte Zeile einfach nur eine weitere Zeile. Sie hat keine besondere Bedeutung als "Fußzeile" oder "Zusammenfassung".

Jetzt strukturieren wir dieselbe Tabelle mit `<thead>`, `<tbody>` und `<tfoot>`.

```html
<table>
  <caption>Projekt-Abrechnung Q3</caption>
  <thead>
    <tr>
      <th>Leistung</th>
      <th>Stunden</th>
      <th>Stundensatz</th>
      <th>Summe</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Konzeption & Design</td>
      <td>20</td>
      <td>90 €</td>
      <td>1800 €</td>
    </tr>
    <tr>
      <td>Frontend-Entwicklung</td>
      <td>45</td>
      <td>110 €</td>
      <td>4950 €</td>
    </tr>
    <tr>
      <td>Backend-Anbindung</td>
      <td>30</td>
      <td>120 €</td>
      <td>3600 €</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td><strong>Gesamtsumme</strong></td>
      <td colspan="2"></td>
      <td><strong>10350 €</strong></td>
    </tr>
  </tfoot>
</table>
```

Der Code ist nun sauberer, lesbarer und vor allem semantisch korrekt. Jede Zeile ist nun klar einem logischen Bereich der Tabelle zugeordnet.

#### Die Superkräfte der semantischen Struktur

Warum solltest du dir diese Mühe machen? Die Vorteile sind erheblich und gehen weit über reine Code-Ästhetik hinaus.

**1. Barrierefreiheit (Accessibility)**

Für Menschen, die auf assistierende Technologien wie Screenreader angewiesen sind, ist diese Struktur ein Segen. Wenn sie durch eine lange Tabelle navigieren, kann der Screenreader die Kopfzeilen aus dem `<thead>` wiederholen, wenn eine neue Zeile betreten wird. So weiß der Nutzer immer, welche Spalte er gerade hört, ohne ständig nach oben scrollen oder sich die Reihenfolge merken zu müssen. Der `<tfoot>` signalisiert zudem klar, dass hier zusammenfassende Informationen folgen.

**2. Intelligentes Drucken und Anzeigen**

Browser sind clever. Wenn eine lange Tabelle über mehrere Seiten gedruckt wird, wiederholen viele Browser automatisch den Inhalt des `<thead>` am Anfang jeder neuen Seite und den Inhalt des `<tfoot>` am Ende jeder Seite. Das sorgt für perfekt lesbare und kontextbezogene Ausdrucke, ohne dass du dafür extra Code schreiben musst.

Ein interessanter Fakt zur Reihenfolge: Laut HTML-Spezifikation kannst du den `<tfoot>` im Quellcode sogar *vor* dem `<tbody>` platzieren. Der Browser wird ihn trotzdem immer am Ende der Tabelle rendern. Das war früher nützlich, damit der Browser den Fuß der Tabelle schon anzeigen konnte, bevor alle (potenziell tausenden) Zeilen des `<tbody>` geladen waren.

```html
<table>
  <thead>
    <!-- Kopfzeilen -->
  </thead>
  <tfoot>
    <!-- Fußzeilen -->
  </tfoot>
  <tbody>
    <!-- Hunderte von Datenzeilen -->
  </tbody>
</table>
```
Auch wenn diese Technik heute seltener benötigt wird, zeigt sie eindrucksvoll, wie die semantische Bedeutung die visuelle Darstellung steuert.

**3. Einfacheres Styling mit CSS**

Mit den Gruppierungs-Tags wird das Stylen deiner Tabellen zum Kinderspiel. Du kannst jedem Abschnitt ein komplett eigenes Aussehen geben, ohne auf komplexe Klassen oder IDs zurückgreifen zu müssen.

Stell dir vor, du möchtest dem Tabellenkopf einen dunklen Hintergrund geben, die Datenzeilen abwechselnd einfärben ("Zebra-Striping") und die Fußzeile fett und mit einer oberen Trennlinie hervorheben. Mit CSS ist das dank der semantischen Struktur trivial:

```css
/* Stil für den gesamten Tabellenkopf */
thead {
  background-color: #333;
  color: white;
  font-weight: bold;
}

/* Zebra-Striping nur für die Datenzeilen im Body */
tbody tr:nth-child(even) {
  background-color: #f2f2f2;
}

/* Spezieller Stil für die Fußzeile */
tfoot {
  font-weight: bold;
  border-top: 2px solid #333;
}
```

Dieser CSS-Code ist sauber, selbsterklärend und zielt präzise auf die logischen Teile der Tabelle ab. Ohne `<thead>`, `<tbody>` und `<tfoot>` müsstest du mit komplizierteren Selektoren wie `:first-child` und `:last-child` arbeiten, was schnell unübersichtlich und fehleranfällig wird, besonders bei komplexeren Tabellen.

**4. Mächtige Steuerung mit JavaScript**

Wenn du Tabellen dynamisch machen möchtest – zum Beispiel Daten sortieren, filtern oder einen feststehenden Kopf beim Scrollen realisieren willst – sind diese Gruppierungselemente Gold wert. Du kannst den gesamten `<tbody>` ansprechen, um ihn zu sortieren, ohne versehentlich den Kopf oder Fuß mitzusortieren.

Ein klassisches Anwendungsbeispiel ist eine Tabelle, deren Kopf (`<thead>`) sichtbar bleibt, während der Inhalt (`<tbody>`) scrollbar ist. Dies lässt sich mit CSS realisieren, indem man dem `<tbody>` eine feste Höhe und `overflow-y: scroll;` zuweist. Diese saubere Trennung von Kopf und Körper macht solche modernen UI-Muster erst möglich.

#### Fortgeschrittene Gruppierung: Mehrere `<tbody>`-Elemente

Eine oft übersehene, aber extrem nützliche Eigenschaft ist, dass eine Tabelle **mehrere `<tbody>`-Elemente** enthalten kann. Das erlaubt dir, Datenzeilen innerhalb einer einzigen Tabelle in weitere logische Blöcke zu unterteilen.

Das ist ideal, wenn du zum Beispiel eine Liste von Spielern nach Teams oder Verkaufsdaten nach Regionen gruppieren möchtest. Jede Gruppe bekommt ihren eigenen `<tbody>`.

Hier ein Beispiel für eine Mitarbeiterliste, gruppiert nach Abteilungen:

```html
<table>
  <caption>Mitarbeiterliste nach Abteilung</caption>
  <thead>
    <tr>
      <th>Name</th>
      <th>Position</th>
      <th>E-Mail</th>
    </tr>
  </thead>
  <tbody>
    <!-- Erste Gruppe: Marketing -->
    <tr>
      <th colspan="3">Marketing</th>
    </tr>
    <tr>
      <td>Anna Meier</td>
      <td>Leitung</td>
      <td>a.meier@firma.de</td>
    </tr>
    <tr>
      <td>Ben Huber</td>
      <td>Social Media Manager</td>
      <td>b.huber@firma.de</td>
    </tr>
  </tbody>
  <tbody>
    <!-- Zweite Gruppe: Entwicklung -->
    <tr>
      <th colspan="3">Entwicklung</th>
    </tr>
    <tr>
      <td>Clara Schmidt</td>
      <td>Senior Developer</td>
      <td>c.schmidt@firma.de</td>
    </tr>
    <tr>
      <td>David Wolf</td>
      <td>Junior Developer</td>
      <td>d.wolf@firma.de</td>
    </tr>
  </tbody>
</table>
```

In diesem Beispiel hat jede Abteilung ihren eigenen `<tbody>`. Das eröffnet fantastische Möglichkeiten für das Styling. Du könntest zum Beispiel jeder zweiten Gruppe eine andere Hintergrundfarbe geben, um die Blöcke visuell voneinander abzuheben.

```css
/* Gibt jeder zweiten Datengruppe einen leicht grauen Hintergrund */
tbody:nth-of-type(even) {
  background-color: #fafafa;
  border-top: 1px solid #ccc;
  border-bottom: 1px solid #ccc;
}
```

Die Gruppierung von Zeilen mit `<thead>`, `<tbody>` und `<tfoot>` ist also weit mehr als eine formale Übung. Es ist ein fundamentaler Schritt hin zu professionellen, wartbaren und barrierearmen HTML-Tabellen. Du schaffst eine robuste Struktur, die dir und den Maschinen, die deinen Code verarbeiten, das Leben leichter macht. Nimm dir also die Zeit, deine Tabellen von Anfang an richtig zu gliedern – es zahlt sich auf lange Sicht immer aus.
