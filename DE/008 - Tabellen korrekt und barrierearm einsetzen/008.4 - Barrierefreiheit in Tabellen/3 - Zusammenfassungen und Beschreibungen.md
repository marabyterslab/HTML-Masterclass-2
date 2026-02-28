# Zusammenfassungen und Beschreibungen

### Zusammenfassungen und Beschreibungen: Gib deinen Tabellen Kontext

Stell dir vor, du betrittst einen Raum, in dem ein großes, komplexes Diagramm an der Wand hängt. Ohne eine Überschrift oder eine erklärende Legende wüsstest du kaum, was du siehst. Sind es Börsenkurse, Wetterdaten oder die Verkaufszahlen des letzten Quartals? Erst der Titel gibt dir den entscheidenden ersten Hinweis.

Ganz ähnlich ergeht es Nutzern, die auf deiner Webseite auf eine Datentabelle stoßen. Insbesondere für Menschen, die auf assistierende Technologien wie Screenreader angewiesen sind, ist eine Tabelle ohne Kontext nur eine Ansammlung von Zellen. Sie hören vielleicht: „Tabelle mit 5 Spalten und 10 Zeilen“, aber was diese Daten bedeuten, bleibt ein Rätsel. Genau hier kommen Zusammenfassungen und Beschreibungen ins Spiel. Sie sind die Wegweiser, die sicherstellen, dass jeder – wirklich jeder – den Inhalt und den Zweck deiner Tabellen verstehen kann.

#### Das `<caption>`-Element: Die sichtbare Überschrift für alle

Das wichtigste und grundlegendste Element, um einer Tabelle Kontext zu geben, ist das `<caption>`-Element. Es fungiert als offizielle, semantisch korrekte Überschrift deiner Tabelle.

Das `<caption>`-Element muss das erste Kind-Element direkt innerhalb deines `<table>`-Tags sein. Es ist für alle Nutzer sichtbar und wird von Screenreadern in der Regel als Erstes vorgelesen, noch bevor die eigentlichen Tabellendaten folgen. Das gibt dem Nutzer sofort die entscheidende Information, worum es in der Tabelle geht, und er kann entscheiden, ob die enthaltenen Daten für ihn relevant sind oder ob er die Tabelle überspringen möchte.

Schauen wir uns ein einfaches Beispiel an: eine Tabelle mit den Öffnungszeiten eines Geschäfts.

```html
<table>
  <caption>Öffnungszeiten unserer Filiale in Berlin</caption>
  <thead>
    <tr>
      <th scope="col">Tag</th>
      <th scope="col">Vormittag</th>
      <th scope="col">Nachmittag</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Montag - Freitag</th>
      <td>09:00 - 13:00 Uhr</td>
      <td>14:00 - 18:00 Uhr</td>
    </tr>
    <tr>
      <th scope="row">Samstag</th>
      <td>10:00 - 14:00 Uhr</td>
      <td>Geschlossen</td>
    </tr>
    <tr>
      <th scope="row">Sonntag</th>
      <td colspan="2">Geschlossen</td>
    </tr>
  </tbody>
</table>
```

Ohne das `<caption>`-Element wäre diese Tabelle nur eine Ansammlung von Tagen und Uhrzeiten. Mit `<caption>Öffnungszeiten unserer Filiale in Berlin</caption>` ist der Zweck sofort glasklar.

**Warum nicht einfach eine `<h2>`-Überschrift?**

Du könntest versucht sein, einfach eine normale Überschrift wie `<h2>` vor die Tabelle zu setzen. Das ist visuell vielleicht ähnlich, aber semantisch ein großer Unterschied. Eine `<h2>`-Überschrift steht für sich allein und ist nicht programmatisch mit der Tabelle verknüpft. Das `<caption>`-Element hingegen ist ein untrennbarer Teil der Tabellenstruktur. Ein Screenreader weiß: „Aha, dieser Text gehört exakt zu dieser Tabelle.“ Diese direkte Verknüpfung ist für die Barrierefreiheit entscheidend. Visuell kannst du ein `<caption>` mit CSS übrigens genauso gestalten wie jede andere Überschrift, du hast also keine gestalterischen Nachteile.

#### Die `summary`-Falle: Ein Blick in die Vergangenheit

Wenn du dich mit älterem HTML-Code oder älteren Tutorials beschäftigst, wirst du vielleicht auf das `summary`-Attribut stoßen, das direkt im `<table>`-Tag platziert wurde:

```html
<!-- VERALTET UND FALSCH! NICHT VERWENDEN! -->
<table summary="Diese Tabelle zeigt die Öffnungszeiten an Wochentagen und am Wochenende.">
  <!-- ... Tabelleninhalt ... -->
</table>
```

Die ursprüngliche Idee des `summary`-Attributs war es, Screenreadern eine nicht-sichtbare Zusammenfassung der Tabellenstruktur zu geben. Es sollte erklären, wie die Tabelle aufgebaut ist, um die Navigation zu erleichtern.

**Wichtig: Das `summary`-Attribut ist in HTML5 als veraltet (obsolete) eingestuft und du solltest es auf keinen Fall mehr verwenden.**

Warum wurde es entfernt? Aus mehreren guten Gründen:
1.  **Versteckte Informationen:** Inhalte, die nur für eine Nutzergruppe (Screenreader-Nutzer) verfügbar sind, aber für sehende Nutzer verborgen bleiben, verstoßen gegen das Prinzip der Inklusion. Wichtige Informationen sollten für alle zugänglich sein.
2.  **Häufiger Missbrauch:** Das Attribut wurde oft falsch verwendet, um den Inhalt des `<caption>`-Elements zu wiederholen oder um Informationen zu liefern, die besser in einem sichtbaren Textabsatz aufgehoben wären.
3.  **Bessere Alternativen:** Es gibt heute modernere und bessere Techniken, um komplexe Tabellen zu beschreiben, die für alle Nutzer zugänglich sind.

Wenn du also auf das `summary`-Attribut stößt, weißt du, dass es ein Relikt aus der Vergangenheit ist. Entferne es und nutze stattdessen die modernen Ansätze.

#### Komplexe Tabellen und die moderne Beschreibung mit `aria-describedby`

Ein `<caption>` ist fantastisch für einen Titel. Aber was ist, wenn eine Tabelle so komplex ist, dass ein einfacher Titel nicht ausreicht, um sie zu verstehen? Stell dir eine Tabelle vor, die Finanzdaten über mehrere Jahre vergleicht, mit verschachtelten Spaltenüberschriften und Fußnoten, die bestimmte Werte erklären.

Hier braucht der Nutzer möglicherweise eine kurze Anleitung, wie die Tabelle zu lesen ist, oder eine Erläuterung der Besonderheiten. Diese Beschreibung sollte, dem modernen Verständnis von Barrierefreiheit folgend, für alle sichtbar sein.

Die beste Methode hierfür ist, einen normalen Absatz (`<p>`) oder ein anderes passendes Element in die Nähe der Tabelle zu setzen, der die notwendigen Informationen enthält. Um diesen Beschreibungstext nun programmatisch mit der Tabelle zu verknüpfen, verwenden wir das ARIA-Attribut `aria-describedby`.

So funktioniert es:
1.  Du schreibst deine Beschreibung in ein beliebiges HTML-Element, zum Beispiel in einen `<p>`-Tag.
2.  Diesem Element gibst du eine eindeutige `id`.
3.  Im `<table>`-Tag fügst du das Attribut `aria-describedby` hinzu und weist ihm als Wert die `id` deines Beschreibungselements zu.

Ein Screenreader, der auf diese Tabelle trifft, wird nun zuerst das `<caption>` vorlesen und anschließend den Inhalt des Elements, auf das `aria-describedby` verweist. Der Nutzer erhält also Titel und Beschreibung, bevor er sich in die Daten stürzt.

Schauen wir uns ein Beispiel an. Wir haben eine Tabelle, die das Wachstum von Nutzerzahlen darstellt, aber ein Wert ist nur eine Schätzung.

```html
<p id="user-growth-description">
  Diese Tabelle vergleicht die aktiven Nutzerzahlen pro Quartal für die Jahre 2022 und 2023.
  Alle Zahlen sind in Tausend angegeben. Der Wert für Q4 2023 ist eine vorläufige Schätzung.
</p>

<table aria-describedby="user-growth-description">
  <caption>Wachstum der aktiven Nutzer (in Tsd.)</caption>
  <thead>
    <tr>
      <th scope="col">Quartal</th>
      <th scope="col">2022</th>
      <th scope="col">2023</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Q1</th>
      <td>120</td>
      <td>150</td>
    </tr>
    <tr>
      <th scope="row">Q2</th>
      <td>135</td>
      <td>165</td>
    </tr>
    <tr>
      <th scope="row">Q3</th>
      <td>140</td>
      <td>180</td>
    </tr>
    <tr>
      <th scope="row">Q4</th>
      <td>145</td>
      <td>195*</td>
    </tr>
  </tbody>
</table>
```

In diesem Beispiel haben wir beides perfekt kombiniert:
*   Das `<caption>` gibt den klaren und prägnanten Titel: „Wachstum der aktiven Nutzer (in Tsd.)“.
*   Der Absatz mit der `id="user-growth-description"` liefert den notwendigen Kontext: Die Einheit der Zahlen und die wichtige Information, dass ein Wert eine Schätzung ist. Da dieser Absatz ein ganz normales Element ist, ist er für sehende Nutzer ebenfalls sichtbar und hilfreich. Das `aria-describedby`-Attribut an der Tabelle stellt die Brücke für assistierende Technologien her.

#### Wann verwendest du was? Eine klare Abgrenzung

Um es auf den Punkt zu bringen, hier ist die Faustregel für den Einsatz dieser Elemente:

1.  **`<caption>` (Die Überschrift):**
    *   **Was es ist:** Der Titel der Tabelle.
    *   **Wann verwenden:** **Immer.** Jede Datentabelle braucht einen Titel, der beschreibt, was sie enthält. Das `<caption>` ist dafür das semantisch korrekte Element. Es ist nicht optional.
    *   **Beispiel:** "Kontaktliste des Marketing-Teams", "Nährwertangaben pro 100g", "Vergleich der Produkt-Features".

2.  **Textabsatz mit `aria-describedby` (Die Beschreibung):**
    *   **Was es ist:** Eine weiterführende Erklärung oder Anleitung zum Lesen der Tabelle.
    *   **Wann verwenden:** **Bei Bedarf** für komplexe Tabellen. Wenn der Aufbau oder die Daten der Tabelle nicht selbsterklärend sind und zusätzlicher Kontext für das Verständnis notwendig ist.
    *   **Beispiel:** "Die in der Spalte 'Anpassung' genannten Werte basieren auf internen Schätzungen.", "Um die Tabelle korrekt zu interpretieren, beachte, dass alle Umsatzzahlen ohne Mehrwertsteuer ausgewiesen sind.", "Diese Tabelle verwendet verschachtelte Spalten. Die obere Zeile gibt die Region an, die untere Zeile das jeweilige Produkt."

Indem du diese beiden Werkzeuge – `<caption>` als Pflicht und `aria-describedby` als Kür für komplexe Fälle – korrekt einsetzt, machst du einen riesigen Schritt nach vorn. Du wandelst eine potenziell verwirrende Datenwüste in eine klar strukturierte und für jeden verständliche Informationsquelle um. Deine Tabellen werden dadurch nicht nur barrierefrei, sondern schlicht und ergreifend besser.
