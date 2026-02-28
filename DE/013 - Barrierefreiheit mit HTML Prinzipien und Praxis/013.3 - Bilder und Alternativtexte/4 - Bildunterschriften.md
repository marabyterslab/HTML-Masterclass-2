# Bildunterschriften

### Bildunterschriften: Mehr als nur Text unter dem Bild

Wenn du an eine Bildunterschrift denkst, hast du wahrscheinlich das klassische Bild vor Augen: ein Foto in einer Zeitung oder einem Magazin und darunter eine kurze Zeile, die erklärt, was zu sehen ist. Im Web ist das Prinzip dasselbe, aber die Umsetzung und die Gründe dafür sind noch vielschichtiger und wichtiger, besonders im Hinblick auf die Barrierefreiheit.

Eine Bildunterschrift ist nicht dasselbe wie ein Alternativtext. Diese Unterscheidung ist fundamental und einer der häufigsten Stolpersteine für Entwickler. Lass uns das ein für alle Mal klären:

*   **Der Alternativtext (`alt`-Attribut):** Er ist ein *Ersatz* für das Bild. Er beschreibt den visuellen Inhalt für Nutzer, die das Bild nicht sehen können, sei es aufgrund einer Sehbehinderung, einer langsamen Internetverbindung oder weil Bilder im Browser deaktiviert sind. Er ist für Sehende unsichtbar.
*   **Die Bildunterschrift (`<figcaption>`):** Sie ist eine *Ergänzung* zum Bild. Sie liefert zusätzlichen Kontext, eine Erklärung, einen Fotonachweis oder eine Interpretation, die für *alle* Nutzer sichtbar und relevant ist.

Stell dir vor, du hast ein Foto von einer Person, die durch ein Mikroskop schaut.
Der `alt`-Text könnte lauten: `alt="Eine Wissenschaftlerin in einem weißen Laborkittel blickt konzentriert durch ein Mikroskop."`
Die Bildunterschrift könnte lauten: `Dr. Anja Weber bei der Untersuchung von Proben im Rahmen ihrer preisgekrönten Krebsforschung.`

Siehst du den Unterschied? Der `alt`-Text beschreibt, was man sieht. Die Bildunterschrift gibt die Information, die man nicht sehen kann, die aber für das Verständnis des Gesamtkontextes entscheidend ist.

#### Die semantische Umsetzung mit `<figure>` und `<figcaption>`

Früher behalf man sich oft mit Notlösungen, um Bilder und ihre Beschriftungen zu verbinden. Man packte ein `<img>`-Element und einen `<p>`-Tag in einen gemeinsamen `<div>`-Container. Das funktioniert zwar visuell, aber es fehlt die semantische Verbindung. Ein Screenreader oder eine Suchmaschine weiß nicht, dass dieser spezifische Paragraph zu genau diesem Bild gehört. Sie sind einfach nur zwei aufeinanderfolgende Elemente im Dokumentenfluss.

HTML5 hat für dieses Problem eine elegante und semantisch korrekte Lösung eingeführt: die Elemente `<figure>` und `<figcaption>`.

*   **`<figure>`:** Dieses Element ist ein Container für in sich geschlossene Inhalte, die im Haupttext referenziert werden, aber deren genaue Position im Fließtext nicht entscheidend ist. Man könnte sie an den Anfang, das Ende oder in eine Seitenleiste verschieben, ohne den Haupttext unverständlich zu machen. Das können Bilder, Diagramme, Code-Beispiele, Zitate oder Videos sein.
*   **`<figcaption>`:** Dieses Element repräsentiert die Beschriftung oder Legende für den Inhalt des übergeordneten `<figure>`-Elements. Es gibt nur ein `<figcaption>` pro `<figure>` und es kann entweder als erstes oder als letztes Kindelement platziert werden.

Ein klassisches Beispiel sieht so aus:

```html
<figure>
  <img src="matterhorn.jpg" alt="Das Matterhorn bei Sonnenuntergang, dessen schneebedeckter Gipfel in goldenem Licht erstrahlt.">
  <figcaption>Das Matterhorn, einer der bekanntesten Berge der Alpen, an der Grenze zwischen der Schweiz und Italien.</figcaption>
</figure>
```

In diesem Code-Schnipsel passiert etwas Wichtiges:
1.  Das `<figure>`-Element signalisiert dem Browser und assistiven Technologien: "Achtung, hier kommt eine in sich geschlossene Einheit aus Inhalt und Beschreibung."
2.  Das `<img>`-Element mit seinem beschreibenden `alt`-Text ist der primäre Inhalt der Figur.
3.  Das `<figcaption>`-Element ist untrennbar und programmatisch mit dem `<img>`-Element verknüpft.

#### Der Gewinn für die Barrierefreiheit

Diese semantische Verknüpfung ist ein riesiger Gewinn. Wenn ein Screenreader auf diese Struktur trifft, kann er sie als zusammengehörige Einheit ansagen. Ein Nutzer könnte beispielsweise hören: "Abbildung: Das Matterhorn bei Sonnenuntergang, dessen schneebedeckter Gipfel in goldenem Licht erstrahlt. Beschriftung: Das Matterhorn, einer der bekanntesten Berge der Alpen, an der Grenze zwischen der Schweiz und Italien."

Der Nutzer versteht sofort die Beziehung zwischen Bild und Text. Bei der alten `<div>`-und-`<p>`-Methode würde der Screenreader einfach nur "Grafik, Das Matterhorn..." und danach "Text, Das Matterhorn..." vorlesen. Die logische Verbindung ginge verloren.

Aber die Vorteile gehen über Screenreader hinaus. Bildunterschriften unterstützen auch Menschen mit kognitiven Einschränkungen oder Lernschwierigkeiten. Ein komplexes Diagramm oder ein abstraktes Bild kann durch eine klare, prägnante Beschriftung verständlich gemacht werden. Sie bieten einen schnellen Ankerpunkt zum Verständnis, ohne dass der gesamte umgebende Text gelesen werden muss.

Auch für sehende Nutzer sind sie von unschätzbarem Wert. Wer von uns scannt nicht Webseiten, anstatt sie Wort für Wort zu lesen? Bilder ziehen unsere Aufmerksamkeit auf sich, und eine gute Bildunterschrift liefert uns den schnellen Kontext, den wir suchen.

#### Wann solltest du eine Bildunterschrift verwenden?

Nicht jedes Bild benötigt eine `<figcaption>`. Ein rein dekoratives Bild, das keine inhaltliche Information transportiert (und daher ein leeres `alt`-Attribut haben sollte: `alt=""`), braucht erst recht keine Bildunterschrift.

Eine Bildunterschrift ist dann sinnvoll, wenn:

*   **Kontext erforderlich ist:** Das Bild zeigt Personen, Orte oder Ereignisse, deren Namen oder Bedeutung nicht offensichtlich sind.
*   **Daten visualisiert werden:** Diagramme, Grafiken und Tabellen sind ohne eine Legende oder Erklärung oft nutzlos. Die `<figcaption>` ist der perfekte Ort dafür.
*   **Quellenangaben nötig sind:** Du musst den Urheber eines Fotos nennen oder auf die Quelle einer Statistik verweisen.
*   **Eine bestimmte Interpretation gelenkt werden soll:** Du möchtest die Aufmerksamkeit des Betrachters auf ein bestimmtes Detail im Bild lenken oder eine übertragene Bedeutung hervorheben.

#### Styling von `<figure>` und `<figcaption>`

Ein weiterer Vorteil der semantischen Struktur ist, dass sie sich leicht mit CSS gestalten lässt. Standardmäßig rendern Browser `<figure>` oft mit einem seitlichen Einzug (`margin`). Das kannst du aber leicht anpassen.

Hier ist ein einfaches CSS-Beispiel, um eine Abbildung und ihre Beschriftung zu gestalten:

```css
figure {
  margin: 1.5em 0; /* Standard-Margin des Browsers überschreiben und vertikalen Abstand schaffen */
  padding: 10px;
  border: 1px solid #e0e0e0;
  background-color: #f9f9f9;
  max-width: 100%; /* Stellt sicher, dass die Figure nicht über ihren Container hinausragt */
}

figure img {
  display: block; /* Verhindert unerwünschte Leerräume unter dem Bild */
  max-width: 100%;
  height: auto; /* Sorgt für responsives Verhalten des Bildes */
  margin: 0 auto; /* Zentriert das Bild, falls es schmaler als die Figure ist */
}

figcaption {
  margin-top: 10px;
  padding: 5px;
  text-align: center;
  font-size: 0.9em;
  font-style: italic;
  color: #333;
}
```

Mit diesem CSS wird die gesamte Figure-Einheit klar vom restlichen Text abgehoben, das Bild verhält sich responsiv und die Beschriftung ist sauber formatiert und zentriert. Du hast die volle Kontrolle über die visuelle Präsentation, während die semantische Struktur und damit die Barrierefreiheit unangetastet bleiben.

Die Verwendung von `<figure>` und `<figcaption>` ist also keine bloße Formsache oder eine "fortgeschrittene" Technik. Es ist die grundlegend richtige, robusteste und zugänglichste Methode, um Bilder und ihre zugehörigen Beschreibungen im Web darzustellen. Es ist ein kleines Detail, das einen großen Unterschied für die Qualität und Professionalität deiner Webseite macht – und vor allem für die Erfahrung all deiner Nutzer.
