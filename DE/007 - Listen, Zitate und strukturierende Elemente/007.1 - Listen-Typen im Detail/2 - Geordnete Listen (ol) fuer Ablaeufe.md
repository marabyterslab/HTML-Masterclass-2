# Geordnete Listen (ol) für Abläufe

### Geordnete Listen (`<ol>`): Wenn die Reihenfolge zählt

Stell dir vor, du schreibst eine Anleitung, ein Rezept oder eine Top-10-Liste. In all diesen Fällen ist die Reihenfolge der einzelnen Punkte nicht nur wichtig, sie ist entscheidend. Ein Kuchenrezept funktioniert nicht, wenn du die Eier verquirlst, nachdem der Teig schon im Ofen ist. Eine Wegbeschreibung ist nutzlos, wenn die Abbiegehinweise durcheinander geraten. Genau für solche Szenarien, in denen eine schrittweise Abfolge oder eine Rangordnung im Mittelpunkt steht, wurde in HTML die geordnete Liste geschaffen.

Das Element, das diese Art von Liste definiert, ist `<ol>`, eine Abkürzung für "ordered list". Im Gegensatz zur ungeordneten Liste (`<ul>`), bei der die Punkte austauschbar sind, signalisiert eine `<ol>` dem Browser – und damit auch deinen Nutzern und Suchmaschinen –, dass die hier enthaltenen Elemente eine ganz bestimmte, sinnvolle Sequenz bilden.

#### Der grundlegende Aufbau

Die Struktur einer geordneten Liste ist denkbar einfach und folgt demselben Prinzip wie bei ihrem ungeordneten Gegenstück. Das `<ol>`-Element dient als Container, der die gesamte Liste umschließt. Jeder einzelne Punkt innerhalb dieser Liste wird dann durch ein `<li>`-Element (list item) ausgezeichnet.

Betrachten wir ein einfaches Beispiel für die Zubereitung von Filterkaffee:

```html
<p>So bereitest du einen perfekten Filterkaffee zu:</p>
<ol>
  <li>Wasser im Wasserkocher zum Kochen bringen.</li>
  <li>Kaffeefilter in den Handfilter einsetzen und mit heißem Wasser befeuchten.</li>
  <li>Frisch gemahlenes Kaffeepulver in den Filter geben.</li>
  <li>Eine kleine Menge Wasser aufgießen und den Kaffee 30 Sekunden aufquellen lassen.</li>
  <li>Das restliche Wasser langsam und in kreisenden Bewegungen nachgießen.</li>
  <li>Den Kaffee vollständig durchlaufen lassen und genießen.</li>
</ol>
```

Wenn du diesen Code in einem Browser anzeigst, passiert etwas sehr Praktisches: Der Browser kümmert sich automatisch um die Nummerierung. Er stellt jedem `<li>`-Element eine Ziffer voran, beginnend bei 1. Das Ergebnis sieht dann so aus:

1.  Wasser im Wasserkocher zum Kochen bringen.
2.  Kaffeefilter in den Handfilter einsetzen und mit heißem Wasser befeuchten.
3.  Frisch gemahlenes Kaffeepulver in den Filter geben.
4.  Eine kleine Menge Wasser aufgießen und den Kaffee 30 Sekunden aufquellen lassen.
5.  Das restliche Wasser langsam und in kreisenden Bewegungen nachgießen.
6.  Den Kaffee vollständig durchlaufen lassen und genießen.

Der große Vorteil ist, dass du dich nicht selbst um die Zahlen kümmern musst. Wenn du später einen Schritt hinzufügen, entfernen oder die Reihenfolge ändern möchtest, passt der Browser die Nummerierung automatisch an. Das macht deinen Code nicht nur wartbarer, sondern auch semantisch korrekt. Du teilst der Maschine mit: "Dies ist eine Abfolge von Schritten", und die Maschine übernimmt die visuelle Darstellung dieser Abfolge.

#### Die Nummerierung anpassen: Die Attribute `type`, `start` und `reversed`

Standardmäßig verwendet der Browser für die Nummerierung arabische Ziffern (1, 2, 3, ...). Doch HTML bietet dir die Möglichkeit, dieses Verhalten über Attribute direkt am `<ol>`-Tag zu steuern.

**Das `type`-Attribut**

Mit dem `type`-Attribut kannst du die Art der Nummerierungszeichen festlegen. Folgende Werte stehen dir zur Verfügung:

*   `"1"`: Arabische Ziffern (Standardwert)
*   `"a"`: Kleinbuchstaben (a, b, c, ...)
*   `"A"`: Großbuchstaben (A, B, C, ...)
*   `"i"`: Kleine römische Zahlen (i, ii, iii, ...)
*   `"I"`: Große römische Zahlen (I, II, III, ...)

Ein Beispiel für eine Gliederung mit Großbuchstaben könnte so aussehen:

```html
<ol type="A">
  <li>Einleitung</li>
  <li>Hauptteil</li>
  <li>Schlussfolgerung</li>
</ol>
```

Obwohl das `type`-Attribut voll funktionsfähig ist, gilt es heute als bewährte Praxis, rein visuelle Anpassungen wie diese über CSS mit der Eigenschaft `list-style-type` vorzunehmen. Dennoch ist es gut, das HTML-Attribut zu kennen, da du ihm in bestehendem Code begegnen wirst.

**Das `start`-Attribut**

Manchmal möchtest du eine Liste nicht bei 1 (oder a, A, i, I) beginnen lassen. Stell dir vor, du unterbrichst eine Anleitung durch einen längeren Textabschnitt oder ein Bild und möchtest die Nummerierung danach fortsetzen. Hierfür gibt es das `start`-Attribut. Es erwartet als Wert eine Zahl, die den Startpunkt der Liste definiert.

```html
<h4>Phase 1: Vorbereitung</h4>
<ol>
  <li>Projektziele definieren.</li>
  <li>Team zusammenstellen.</li>
</ol>

<p>Nachdem die Vorbereitungsphase abgeschlossen ist, folgt die detaillierte Planung der einzelnen Meilensteine in Phase 2.</p>

<h4>Phase 2: Planung</h4>
<ol start="3">
  <li>Zeitplan erstellen.</li>
  <li>Ressourcen zuweisen.</li>
  <li>Risikoanalyse durchführen.</li>
</ol>
```

Im zweiten Listenblock wird die Zählung dank `start="3"` nicht wieder bei 1, sondern bei 3 begonnen. Dies erzeugt eine logische Kontinuität für den Leser. Das `start`-Attribut funktioniert auch in Kombination mit dem `type`-Attribut. ` <ol type="a" start="4">` würde die Liste beispielsweise mit dem Buchstaben "d" beginnen.

**Das `reversed`-Attribut**

Eine besonders interessante Möglichkeit bietet das `reversed`-Attribut. Es ist ein sogenanntes boolesches Attribut, was bedeutet, dass allein seine Anwesenheit ausreicht, um es zu aktivieren. Es kehrt die Zählrichtung um. Dies ist perfekt für Countdowns oder absteigende Ranglisten.

```html
<h3>Top 3 der meistbesuchten Städte</h3>
<ol reversed>
  <li>Paris</li>
  <li>Bangkok</li>
  <li>London</li>
</ol>
```

Der Browser wird diese Liste wie folgt darstellen:

3.  Paris
2.  Bangkok
1.  London

In Kombination mit `start` kannst du auch den Startpunkt des Countdowns festlegen. Zum Beispiel würde `<ol reversed start="10">` eine Liste erzeugen, die von 10 abwärts bis zum Ende der Listenelemente zählt.

#### Verschachtelte Listen: Abläufe mit Unterpunkten

Komplexe Abläufe haben oft Hauptschritte, die wiederum aus mehreren Unterschritten bestehen. HTML erlaubt es dir, Listen ineinander zu verschachteln, um solche Hierarchien abzubilden. Die Regel dabei ist einfach, aber strikt: Eine neue Liste (egal ob `<ol>` oder `<ul>`) darf nur *innerhalb* eines `<li>`-Elements platziert werden.

Erweitern wir unser Kaffee-Beispiel um Unterschritte:

```html
<ol>
  <li>Wasser im Wasserkocher zum Kochen bringen.</li>
  <li>
    Den Filter vorbereiten:
    <ol type="a">
      <li>Kaffeefilter in den Handfilter einsetzen.</li>
      <li>Filter mit heißem Wasser befeuchten, um Papiergeschmack zu entfernen.</li>
      <li>Das Wasser aus der Kanne wieder ausgießen.</li>
    </ol>
  </li>
  <li>Frisch gemahlenes Kaffeepulver in den Filter geben.</li>
  <li>
    Den Brühvorgang starten:
    <ol type="a">
      <li>Eine kleine Menge Wasser aufgießen (ca. 50 ml).</li>
      <li>Den Kaffee 30 Sekunden aufquellen lassen ("Blooming").</li>
      <li>Das restliche Wasser langsam nachgießen.</li>
    </ol>
  </li>
  <li>Den Kaffee vollständig durchlaufen lassen und genießen.</li>
</ol>
```

Hier siehst du, dass die Unterschritte in einem neuen `<ol>`-Element innerhalb der `<li>`-Elemente von Schritt 2 und 4 liegen. Die Browser sind intelligent genug, um für verschachtelte Listen automatisch einen anderen Nummerierungsstil (z.B. Buchstaben statt Zahlen) und eine Einrückung zu verwenden, was die Struktur visuell sehr übersichtlich macht.

#### Einzelne Listenelemente steuern: Das `value`-Attribut

Während `start` die gesamte Liste beeinflusst, gibt es mit dem `value`-Attribut auch eine Möglichkeit, die Nummerierung eines *einzelnen* Listenelements zu manipulieren. Dieses Attribut wird direkt an einem `<li>`-Tag platziert. Es setzt den Zähler für genau dieses Element auf den angegebenen Wert. Alle nachfolgenden `<li>`-Elemente zählen von diesem neuen Wert aus weiter.

Dies kann nützlich sein, wenn in einer technischen Dokumentation bestimmte Schritte übersprungen werden sollen, die Nummerierung aber konsistent zu einem Handbuch bleiben muss.

```html
<h3>Fehlerbehebungsschritte</h3>
<ol>
  <li>Gerät vom Stromnetz trennen.</li>
  <li value="3">Sicherungen im Hauptverteiler überprüfen.</li>
  <li>Fünf Minuten warten.</li>
  <li>Gerät wieder an das Stromnetz anschließen.</li>
</ol>
```

Die resultierende Liste wird wie folgt nummeriert: 1, 3, 4, 5. Schritt 2 wurde ausgelassen, und die Zählung wurde bei Schritt 3 mit `value="3"` manuell neu gesetzt. Das nachfolgende Element zählt korrekt mit 4 weiter. Setze dieses Attribut mit Bedacht ein, da es die natürliche Abfolge durchbricht und bei unsachgemäßer Verwendung zu Verwirrung führen kann.

Die geordnete Liste ist somit weit mehr als nur eine nummerierte Aufzählung. Sie ist ein starkes semantisches Werkzeug, um Prozesse, Anleitungen, Rangfolgen und jegliche Form von sequenziellen Informationen klar und logisch zu strukturieren – sowohl für den Menschen als auch für die Maschine.
