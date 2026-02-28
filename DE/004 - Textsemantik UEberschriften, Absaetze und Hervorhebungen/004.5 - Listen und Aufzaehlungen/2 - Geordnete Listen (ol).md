# Geordnete Listen (ol)

### Geordnete Listen: Wenn die Reihenfolge zählt

Stell dir vor, du schreibst eine Anleitung, wie man einen Kuchen backt, eine Top-10-Liste deiner Lieblingsfilme oder eine Wegbeschreibung zum Haus eines Freundes. In all diesen Fällen ist die Reihenfolge der einzelnen Punkte nicht nur wichtig, sondern entscheidend. Die Zutaten für den Kuchen müssen in einer bestimmten Abfolge hinzugefügt werden, und Platz 1 deiner Filmliste ist nun einmal nicht Platz 7. Genau für solche Szenarien, in denen die Sequenz eine Bedeutung hat, gibt es in HTML die geordnete Liste.

Das Kürzel dafür lautet `<ol>`, was für „ordered list“ steht. Wie bei ihrem Gegenstück, der ungeordneten Liste (`<ul>`), umschließt das `<ol>`-Tag die gesamte Liste. Die einzelnen Einträge innerhalb der Liste werden – ebenfalls genau wie bei der ungeordneten Liste – mit dem `<li>`-Tag (list item) ausgezeichnet.

Der entscheidende Unterschied liegt in der Darstellung im Browser: Statt einfacher Aufzählungspunkte (wie Kreise oder Quadrate) verwendet der Browser standardmäßig Zahlen, die automatisch hochzählen.

Sieh dir dieses grundlegende Beispiel an, eine einfache Morgenroutine:

```html
<ol>
  <li>Aufwachen und den Wecker ausschalten</li>
  <li>Kaffee kochen</li>
  <li>Frühstücken</li>
  <li>Zähne putzen</li>
</ol>
```

Im Browser wird dies folgendermaßen dargestellt, wobei die Nummerierung automatisch erfolgt:

1.  Aufwachen und den Wecker ausschalten
2.  Kaffee kochen
3.  Frühstücken
4.  Zähne putzen

Würdest du die Reihenfolge der `<li>`-Elemente im Code ändern, würde sich auch die Nummerierung anpassen. Die Zahl repräsentiert die Position des Elements in der Liste, nicht einen festen Wert, den du selbst eintippst. Das ist die semantische Kraft des `<ol>`-Elements: Du teilst dem Browser (und damit auch Suchmaschinen und Screenreadern) mit, dass diese Punkte in einer spezifischen, bedeutungsvollen Reihenfolge stehen.

#### Die Darstellung anpassen: Die Attribute des `<ol>`-Tags

Obwohl die Standardnummerierung mit arabischen Ziffern (1, 2, 3, ...) für die meisten Fälle ausreicht, bietet HTML dir einige Attribute, um das Aussehen und Verhalten deiner geordneten Liste zu steuern.

##### Das `type`-Attribut: Zahlen, Buchstaben oder römische Ziffern

Mit dem `type`-Attribut kannst du festlegen, welche Art von Zählzeichen verwendet werden soll. Das ist besonders nützlich für Gliederungen oder juristische Texte, in denen oft unterschiedliche Nummerierungsstile gemischt werden.

Folgende Werte stehen dir zur Verfügung:

*   `"1"`: Standardmäßige arabische Ziffern (1, 2, 3, …) – das ist der Defaultwert.
*   `"a"`: Kleinbuchstaben (a, b, c, …)
*   `"A"`: Großbuchstaben (A, B, C, …)
*   `"i"`: Kleine römische Ziffern (i, ii, iii, …)
*   `"I"`: Große römische Ziffern (I, II, III, …)

Hier siehst du alle Varianten im direkten Vergleich:

```html
<p>Nummerierung mit Großbuchstaben:</p>
<ol type="A">
  <li>Erster Punkt</li>
  <li>Zweiter Punkt</li>
</ol>

<p>Nummerierung mit kleinen römischen Ziffern:</p>
<ol type="i">
  <li>Erster Punkt</li>
  <li>Zweiter Punkt</li>
</ol>
```

Die semantische Bedeutung – eine geordnete Abfolge – bleibt erhalten. Du änderst lediglich die visuelle Repräsentation der Zählmarken. Es sei jedoch angemerkt, dass heutzutage viele Entwickler solche rein stilistischen Anpassungen bevorzugt mit CSS (über die Eigenschaft `list-style-type`) vornehmen, um Struktur (HTML) und Design (CSS) sauber zu trennen. Für schnelle und einfache Anpassungen ist das `type`-Attribut aber nach wie vor ein gültiges und nützliches Werkzeug.

##### Das `start`-Attribut: Die Zählung mittendrin beginnen

Manchmal möchtest du eine Liste nicht bei 1 (oder a, oder i) beginnen lassen. Stell dir vor, du hast eine lange Anleitung, die du durch einen erklärenden Absatz unterbrechen musst. Danach soll die Nummerierung aber genau dort fortgesetzt werden, wo sie aufgehört hat. Hier kommt das `start`-Attribut ins Spiel.

Du kannst damit einen numerischen Startwert für die Liste festlegen. Der Browser zählt von diesem Wert aus weiter.

```html
<p>Die ersten beiden Schritte:</p>
<ol>
  <li>Projekt initialisieren</li>
  <li>Abhängigkeiten installieren</li>
</ol>

<p>Nachdem diese Schritte erledigt sind, folgt die Konfiguration der Datenbank. Erst danach geht es mit den eigentlichen Entwicklungsschritten weiter.</p>

<p>Die weiteren Schritte:</p>
<ol start="3">
  <li>Die erste Komponente erstellen</li>
  <li>Styling hinzufügen</li>
  <li>Tests schreiben</li>
</ol>
```

Das Ergebnis im Browser ist eine nahtlos fortgeführte Zählung:

Die ersten beiden Schritte:
1.  Projekt initialisieren
2.  Abhängigkeiten installieren

Nachdem diese Schritte erledigt sind, folgt die Konfiguration der Datenbank. Erst danach geht es mit den eigentlichen Entwicklungsschritten weiter.

Die weiteren Schritte:
3.  Die erste Komponente erstellen
4.  Styling hinzufügen
5.  Tests schreiben

Das `start`-Attribut funktioniert auch in Kombination mit dem `type`-Attribut. Wichtig ist dabei zu verstehen, dass `start` immer einen numerischen Wert erwartet, auch wenn der `type` auf Buchstaben oder römische Ziffern gesetzt ist. `start="3"` bedeutet also immer „starte mit dem dritten Element der Sequenz“.

*   Bei `type="a"` und `start="3"` beginnt die Liste mit „c“.
*   Bei `type="I"` und `start="4"` beginnt die Liste mit „IV“.

##### Das `reversed`-Attribut: Der Countdown

Seltener gebraucht, aber für bestimmte Anwendungsfälle sehr elegant, ist das `reversed`-Attribut. Es ist ein sogenanntes boolesches Attribut, was bedeutet, dass seine bloße Anwesenheit ausreicht, um seine Funktion zu aktivieren. Es kehrt die Zählreihenfolge um.

Das ist perfekt für einen Countdown oder eine Top-Liste, die du vom höchsten zum niedrigsten Rang präsentieren möchtest.

```html
<p>Countdown zum Start:</p>
<ol reversed>
  <li>Triebwerke zünden</li>
  <li>Hauptstufe aktivieren</li>
  <li>Start!</li>
</ol>
```

Der Browser wird dies als absteigende Liste darstellen:

3.  Triebwerke zünden
2.  Hauptstufe aktivieren
1.  Start!

Du kannst `reversed` auch mit `start` kombinieren. Wenn du beispielsweise eine Top-5-Liste hast, die absteigend gezählt werden soll, würdest du schreiben: `<ol reversed start="5">`. Die Zählung würde dann bei 5 beginnen und bis 1 herunterzählen.

#### Verschachtelte geordnete Listen

Genau wie ungeordnete Listen kannst du auch geordnete Listen ineinander verschachteln. Das ist unerlässlich für die Erstellung komplexer Gliederungen, bei denen Unterpunkte ebenfalls eine klare Reihenfolge haben.

Die Regel für die Verschachtelung ist einfach und strikt: Eine neue Liste (egal ob `<ol>` oder `<ul>`) darf nur innerhalb eines `<li>`-Elements platziert werden. Sie wird damit zum Kind-Element des Listeneintrags, nicht der übergeordneten Liste.

Hier ist ein Beispiel für eine Rezeptanleitung mit Vorbereitungs- und Zubereitungsschritten:

```html
<ol>
  <li>Vorbereitung
    <ol type="a">
      <li>Gemüse waschen und schneiden</li>
      <li>Ofen auf 180°C vorheizen</li>
      <li>Auflaufform einfetten</li>
    </ol>
  </li>
  <li>Zubereitung
    <ol type="a">
      <li>Gemüse in der Pfanne andünsten</li>
      <li>Mit Gewürzen abschmecken</li>
      <li>Alles in die Auflaufform geben</li>
      <li>30 Minuten backen</li>
    </ol>
  </li>
  <li>Servieren</li>
</ol>
```

Die meisten Browser sind so intelligent, für verschachtelte Listen automatisch einen anderen Zählstil zu verwenden, um die Hierarchie visuell klarer zu machen. Die äußere Liste könnte mit Zahlen (1, 2, 3), die erste innere Ebene mit Kleinbuchstaben (a, b, c) und eine weitere Ebene mit kleinen römischen Ziffern (i, ii, iii) dargestellt werden. Dieses Verhalten kannst du natürlich mit dem `type`-Attribut für jede Liste individuell überschreiben.

Die geordnete Liste ist ein fundamentaler Baustein für die semantische Auszeichnung von Inhalten. Immer wenn du eine Abfolge, einen Prozess, eine Rangliste oder eine schrittweise Anleitung präsentierst, ist `<ol>` die richtige Wahl. Es verleiht deinem Inhalt nicht nur eine klare visuelle Struktur, sondern auch eine logische Bedeutung, die von Maschinen verstanden werden kann.
