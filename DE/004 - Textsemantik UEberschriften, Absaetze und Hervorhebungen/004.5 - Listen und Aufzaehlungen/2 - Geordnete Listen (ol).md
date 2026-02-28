# Geordnete Listen (ol)

### Geordnete Listen: Wenn die Reihenfolge zählt

Neben den unsortierten Listen, die du bereits kennengelernt hast, gibt es eine weitere, ebenso wichtige Art von Listen in HTML: die geordneten Listen. Wie der Name schon vermuten lässt, kommen sie immer dann zum Einsatz, wenn die Reihenfolge der einzelnen Punkte eine entscheidende Rolle spielt. Stell dir eine Backanleitung, eine Schritt-für-Schritt-Anleitung zur Montage eines Möbelstücks oder eine Top-10-Rangliste vor. In all diesen Fällen ist die Abfolge der Elemente nicht willkürlich, sondern folgt einer klaren Logik. Würdest du die Schritte vertauschen, wäre das Ergebnis unbrauchbar oder schlichtweg falsch.

Genau für solche Szenarien wurde das `<ol>`-Element geschaffen. Das Kürzel steht für "ordered list", also "geordnete Liste". Es fungiert als Container für eine Reihe von Listeneinträgen, deren Abfolge eine semantische Bedeutung hat.

#### Der grundlegende Aufbau

Der Aufbau einer geordneten Liste ist dem einer ungeordneten Liste sehr ähnlich. Du verwendest das `<ol>`-Tag, um die Liste zu beginnen und zu beenden. Jeder einzelne Punkt innerhalb dieser Liste wird, genau wie bei der ungeordneten Liste, mit dem `<li>`-Tag (list item) umschlossen.

Betrachten wir ein einfaches Beispiel: die drei Erstplatzierten eines Rennens.

```html
<ol>
  <li>Michael</li>
  <li>Sabine</li>
  <li>Peter</li>
</ol>
```

Wenn du diesen Code im Browser anzeigst, passiert etwas Interessantes. Der Browser fügt nicht einfach nur Aufzählungszeichen hinzu, sondern nummeriert die Einträge automatisch durch. Das Ergebnis sieht so aus:

1.  Michael
2.  Sabine
3.  Peter

Hier zeigt sich die wahre Stärke der semantischen Auszeichnung. Du musst die Zahlen nicht selbst in deinen HTML-Code schreiben. Du teilst dem Browser lediglich mit, dass es sich um eine geordnete Liste handelt, und er kümmert sich um die korrekte Nummerierung. Das hat einen riesigen Vorteil: Wenn du später einen Punkt hinzufügst, entfernst oder die Reihenfolge änderst, passt der Browser die Nummerierung automatisch an. Du musst dich um nichts kümmern.

Stell dir vor, es stellt sich heraus, dass eine weitere Person, Anna, eigentlich den zweiten Platz belegt hat. Du musst nur den Code anpassen:

```html
<ol>
  <li>Michael</li>
  <li>Anna</li>
  <li>Sabine</li>
  <li>Peter</li>
</ol>
```

Der Browser rendert dies ohne weiteres Zutun deinerseits korrekt als:

1.  Michael
2.  Anna
3.  Sabine
4.  Peter

Die Zahlen haben sich automatisch aktualisiert. Diese dynamische Natur macht `<ol>`-Listen extrem praktisch und wartungsfreundlich.

#### Die Nummerierung anpassen: Das `type`-Attribut

Standardmäßig verwenden Browser arabische Ziffern (1, 2, 3, ...). Manchmal möchtest du jedoch eine andere Art der Nummerierung verwenden, zum Beispiel Buchstaben oder römische Ziffern. Dafür gibt es das `type`-Attribut, das du direkt dem `<ol>`-Tag hinzufügst.

Folgende Werte sind für das `type`-Attribut möglich:

*   `"1"`: Arabische Ziffern (Standardwert)
*   `"a"`: Kleinbuchstaben (a, b, c, ...)
*   `"A"`: Großbuchstaben (A, B, C, ...)
*   `"i"`: Kleine römische Ziffern (i, ii, iii, ...)
*   `"I"`: Große römische Ziffern (I, II, III, ...)

Hier sind einige Beispiele in der Anwendung:

```html
<!-- Nummerierung mit Kleinbuchstaben -->
<ol type="a">
  <li>Erster Punkt</li>
  <li>Zweiter Punkt</li>
  <li>Dritter Punkt</li>
</ol>

<!-- Nummerierung mit großen römischen Ziffern -->
<ol type="I">
  <li>Einleitung</li>
  <li>Hauptteil</li>
  <li>Schlussfolgerung</li>
</ol>
```

Es ist wichtig zu erwähnen, dass das `type`-Attribut zwar voll funktionsfähig ist, in der modernen Webentwicklung die visuelle Gestaltung von Elementen – und dazu gehört auch die Art der Aufzählungszeichen – jedoch primär über CSS gesteuert wird. Mit der CSS-Eigenschaft `list-style-type` hast du noch weitaus mehr Möglichkeiten zur Gestaltung. Für das grundlegende semantische Verständnis von HTML ist die Kenntnis des `type`-Attributs aber nach wie vor wertvoll.

#### Den Startpunkt festlegen: Das `start`-Attribut

Manchmal möchtest du eine Liste nicht bei 1 (oder a, oder I) beginnen lassen. Stell dir vor, du hast eine lange Anleitung, die durch erklärende Absätze oder Bilder unterbrochen wird. Du könntest eine erste `<ol>`-Liste mit den Schritten 1 bis 3 haben, gefolgt von einem Bild, und dann soll die nächste `<ol>`-Liste nahtlos mit Schritt 4 weitermachen.

Genau dafür gibt es das `start`-Attribut. Du gibst ihm als Wert die Zahl, mit der die Liste beginnen soll.

```html
<p>Hier sind die ersten Schritte:</p>
<ol>
  <li>Zutaten vorbereiten.</li>
  <li>Ofen vorheizen.</li>
  <li>Teig anrühren.</li>
</ol>

<p>Nachdem der Teig 30 Minuten geruht hat, fahre mit den folgenden Schritten fort:</p>

<ol start="4">
  <li>Teig ausrollen.</li>
  <li>In den Ofen schieben.</li>
  <li>Goldbraun backen.</li>
</ol>
```

Das Ergebnis im Browser wird eine nahtlos wirkende Nummerierung sein, obwohl es sich um zwei separate HTML-Listen handelt.

Ein interessantes Detail: Der Wert des `start`-Attributs muss immer eine Zahl sein, auch wenn du mit `type` einen anderen Nummerierungsstil gewählt hast. Der Browser rechnet den Wert automatisch um. Wenn du also eine Liste mit `type="a"` und `start="3"` erstellst, beginnt die Liste nicht mit "3", sondern mit "c", dem dritten Buchstaben im Alphabet.

```html
<ol type="a" start="3">
  <li>Punkt C</li>
  <li>Punkt D</li>
  <li>Punkt E</li>
</ol>
```

#### Rückwärts zählen: Das `reversed`-Attribut

Eine weitere nützliche Funktion ist die Möglichkeit, eine Liste rückwärts zählen zu lassen. Dies ist besonders praktisch für Ranglisten, bei denen der wichtigste Eintrag am Ende steht, oder für einen Countdown. Dafür verwendest du das boolesche Attribut `reversed`. Boolesche Attribute benötigen keinen Wert; ihre reine Anwesenheit im Tag aktiviert die Funktion.

```html
<p>Countdown zum Start:</p>
<ol reversed>
  <li>Drei</li>
  <li>Zwei</li>
  <li>Eins</li>
  <li>Start!</li>
</ol>
```

Im Browser wird dies so dargestellt:

4.  Drei
3.  Zwei
2.  Eins
1.  Start!

Du kannst `reversed` auch mit dem `start`-Attribut kombinieren, um den Startpunkt des Countdowns festzulegen. Zum Beispiel würde `<ol reversed start="10">` eine Liste von 10 bis 1 absteigend erstellen.

#### Verschachtelte Listen

Genau wie ungeordnete Listen können auch geordnete Listen ineinander verschachtelt werden. Dies ist nützlich, um Unterpunkte oder detailliertere Schritte innerhalb eines Hauptschrittes zu strukturieren. Die Regel für die Verschachtelung ist dabei immer dieselbe: Eine neue Liste (`<ol>` oder `<ul>`) muss immer innerhalb eines `<li>`-Elements der übergeordneten Liste platziert werden.

Ein gutes Beispiel ist ein Rezept, bei dem ein Hauptschritt mehrere kleinere Aktionen umfasst:

```html
<ol>
  <li>Zutaten vorbereiten
    <ol type="a">
      <li>Mehl und Zucker vermischen.</li>
      <li>Butter schmelzen.</li>
      <li>Eier aufschlagen.</li>
    </ol>
  </li>
  <li>Teig verrühren</li>
  <li>Backen</li>
</ol>
```

Der Browser kümmert sich automatisch um die Einrückung und ändert oft auch den Nummerierungsstil für die innere Liste, um die Hierarchie visuell klarzumachen. Das gerenderte Ergebnis könnte so aussehen:

1.  Zutaten vorbereiten
    a.  Mehl und Zucker vermischen.
    b.  Butter schmelzen.
    c.  Eier aufschlagen.
2.  Teig verrühren
3.  Backen

Du kannst natürlich auch geordnete und ungeordnete Listen mischen, je nachdem, was semantisch am meisten Sinn ergibt.

#### Semantik ist der Schlüssel

Der wichtigste Gedanke, den du bei der Verwendung von `<ol>` mitnehmen solltest, ist die Semantik. Du verwendest dieses Element nicht, weil du nummerierte Punkte auf deiner Seite haben möchtest – das könntest du auch mit simplen Absätzen und manuell getippten Zahlen erreichen. Du verwendest `<ol>`, weil du dem Browser, den Suchmaschinen und assistiven Technologien (wie Screenreadern für sehbehinderte Menschen) mitteilen möchtest: "Die Reihenfolge dieser Elemente ist von Bedeutung."

Ein Screenreader wird eine `<ol>`-Liste zum Beispiel ansagen als "Liste mit 5 Einträgen" und dann jeden Punkt mit seiner Nummer vorlesen ("Eins: ...", "Zwei: ..."). Diese zusätzliche Information ist für Nutzer dieser Technologien von unschätzbarem Wert und macht deine Webseite zugänglicher und verständlicher.

Wähle also immer bewusst zwischen `<ol>` und `<ul>`. Frage dich: Würde sich die Bedeutung ändern, wenn ich die Reihenfolge der Punkte vertausche? Wenn die Antwort "Ja" lautet, ist `<ol>` die richtige Wahl. Wenn die Antwort "Nein" ist, greifst du zu `<ul>`.
