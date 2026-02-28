# Das figure-Element

### Das `figure`-Element: Wenn Inhalt und Kontext eine Einheit bilden

Stell dir vor, du schreibst einen Blogartikel über die Architektur des Kolosseums. Mitten im Text möchtest du ein Bild des Amphitheaters einfügen, um deine Ausführungen zu untermauern. Du könntest einfach ein `<img>`-Element verwenden. Aber was ist mit der Bildunterschrift? „Abbildung 1: Das Kolosseum bei Sonnenuntergang.“ Und was ist, wenn dieses Bild so wichtig ist, dass es als eigenständige Informationseinheit betrachtet werden sollte, die man theoretisch auch an das Ende des Artikels oder in einen Anhang verschieben könnte, ohne den Lesefluss des Haupttextes zu zerstören?

Genau für solche Fälle wurde in HTML5 das `<figure>`-Element eingeführt. Es ist weit mehr als nur ein weiterer `<div>`-Container für Bilder. Es ist ein semantisches Element, das dem Browser, Suchmaschinen und assistiven Technologien eine klare Botschaft sendet: „Dieser Block hier – sei es ein Bild, ein Diagramm, ein Code-Beispiel oder eine Gruppe davon – ist eine in sich geschlossene Einheit, die sich auf den Hauptinhalt bezieht, aber davon unabhängig ist.“

#### Die Anatomie von `<figure>` und `<figcaption>`

Das `<figure>`-Element tritt selten allein auf. Sein engster Verbündeter ist das `<figcaption>`-Element (Figure Caption). Zusammen bilden sie ein unschlagbares Team für die semantisch korrekte Auszeichnung von referenziertem Inhalt.

Schauen wir uns ein grundlegendes Beispiel an:

```html
<p>Die römischen Ingenieure nutzten ein ausgeklügeltes System aus Bögen und Gewölben, um die massive Struktur des Kolosseums zu tragen (siehe Abbildung 1). Dies ermöglichte nicht nur eine immense Stabilität, sondern auch eine effiziente Verteilung der Zuschauer.</p>

<figure>
  <img src="kolosseum.jpg" alt="Das Kolosseum in Rom, beleuchtet von der Abendsonne.">
  <figcaption>Abbildung 1: Die beeindruckende Bogenkonstruktion des Kolosseums.</figcaption>
</figure>

<p>Jeder Bogen im Erdgeschoss diente als Eingang für verschiedene Sektoren des Amphitheaters, was ein schnelles Betreten und Verlassen ermöglichte.</p>
```

Analysieren wir diesen Code:

1.  **`<figure>`**: Der Container, der die Einheit als Ganzes umschließt. Er signalisiert: Alles hier drin gehört zusammen.
2.  **`<img>`**: Das eigentliche Bildelement. Wichtig ist hier, wie immer, das `alt`-Attribut. Es beschreibt, *was* auf dem Bild zu sehen ist, für den Fall, dass es nicht geladen werden kann oder ein Screenreader es vorliest.
3.  **`<figcaption>`**: Die Beschriftung der Figur. Sie liefert Kontext, eine Erklärung oder eine Quellenangabe. Das Besondere ist die direkte semantische Verknüpfung zum `<figure>`-Element. Ein Screenreader weiß, dass diese Beschriftung zum Bild gehört, und liest sie entsprechend vor, zum Beispiel: „Figur, Abbildung 1: Die beeindruckende Bogenkonstruktion des Kolosseums. Bild: Das Kolosseum in Rom, beleuchtet von der Abendsonne.“

Es gibt eine wichtige Regel: Ein `<figure>`-Element darf höchstens ein `<figcaption>`-Element enthalten. Dieses kann entweder als erstes oder als letztes Kind-Element platziert werden. Die gängigste und meist auch logischste Position ist am Ende.

#### Mehr als nur Bilder

Die wahre Stärke des `<figure>`-Elements zeigt sich darin, dass es nicht auf Bilder beschränkt ist. Jede Art von selbsterklärendem, referenziertem Inhalt kann in eine Figur gepackt werden.

**Code-Beispiele:**

```html
<figure>
  <pre><code>function halloWelt() {
  console.log("Hallo, Welt!");
}</code></pre>
  <figcaption>Listing 2.1: Eine einfache JavaScript-Funktion zur Ausgabe von Text.</figcaption>
</figure>
```
Hier wird ein Code-Block, oft in `<pre>`- und `<code>`-Tags eingeschlossen, mit einer Beschriftung versehen. Das ist sauber, semantisch korrekt und viel aussagekräftiger als ein einfacher `<div>`.

**Zitate (Blockquotes):**

```html
<figure>
  <blockquote>
    <p>Der Weg ist das Ziel.</p>
  </blockquote>
  <figcaption>— Konfuzius</figcaption>
</figure>
```
Auch Zitate können als Figur ausgezeichnet werden, insbesondere wenn die Urheberschaft klar als Beschriftung und nicht als Teil des eigentlichen Zitats dargestellt werden soll.

**Mehrere Elemente in einer Figur:**

Du kannst sogar mehrere inhaltliche Elemente innerhalb einer einzigen `<figure>` gruppieren, wenn sie eine konzeptionelle Einheit bilden. Stell dir vor, du möchtest einen Vorher-Nachher-Vergleich zeigen:

```html
<figure>
  <img src="garten-vorher.jpg" alt="Ein verwilderter Garten mit hohem Unkraut.">
  <img src="garten-nachher.jpg" alt="Derselbe Garten, jetzt gepflegt mit gemähtem Rasen und blühenden Blumen.">
  <figcaption>Abbildung 3: Die Transformation des Gartens nach einem Wochenende Arbeit.</figcaption>
</figure>
```
Beide Bilder gehören untrennbar zur selben Aussage und werden durch eine einzige, gemeinsame Beschriftung erklärt. Semantisch ist das eine perfekte Lösung.

#### Wann solltest du `<figure>` nicht verwenden?

Die wichtigste Eigenschaft einer Figur ist ihre Unabhängigkeit vom Fließtext. Der beste Test ist die „Anhang-Frage“: Könnte ich diesen Inhalt nehmen und ihn in einen Anhang am Ende der Seite verschieben, ohne dass der Haupttext seinen Sinn verliert? Wenn die Antwort „Ja“ lautet, ist `<figure>` wahrscheinlich die richtige Wahl.

Verwende `<figure>` also **nicht** für:

*   **Rein dekorative Bilder:** Bilder, die nur der Zierde dienen und keinen inhaltlichen Wert haben. Diese gehören ins CSS, meist als `background-image`.
*   **Bilder, die Teil des Satzes sind:** Zum Beispiel ein kleines Logo oder Icon, das direkt im Textfluss steht. Ein Satz wie „Besuche uns auf <img src="twitter-logo.png" alt="Twitter">“ benötigt kein `<figure>`. Das Bild ist hier ein integraler Bestandteil des Satzes, so wie ein Wort.
*   **Jedes einzelne Bild auf deiner Seite:** Nur weil es ein Bild ist, muss es nicht automatisch in ein `<figure>`-Element. Wenn es keine Beschriftung braucht und seine Position im Fließtext entscheidend ist, reicht ein einfaches `<img>`-Element völlig aus.

#### Die wichtige Unterscheidung: `alt` vs. `figcaption`

Ein häufiges Missverständnis betrifft den Unterschied zwischen dem `alt`-Attribut eines Bildes und dem `<figcaption>`-Element. Sie dienen unterschiedlichen, aber gleichermaßen wichtigen Zwecken.

*   **`alt`-Text (Alternativtext):** Beschreibt den **visuellen Inhalt** des Bildes. Er ist eine Alternative für das Bild selbst. Er beantwortet die Frage: „Was ist auf diesem Bild zu sehen?“ Der `alt`-Text ist entscheidend für die Barrierefreiheit.
*   **`<figcaption>` (Bildunterschrift):** Beschreibt den **kontextuellen Zweck** des Bildes innerhalb des Dokuments. Sie beantwortet die Frage: „Warum ist dieses Bild hier und was soll es illustrieren?“

Denk an ein Museum: Der `alt`-Text ist das, was du einem Freund am Telefon beschreiben würdest, damit er sich das Gemälde vorstellen kann („Eine Frau mit einem geheimnisvollen Lächeln vor einer Fantasielandschaft“). Die `<figcaption>` ist das kleine Schild neben dem Gemälde im Museum („Mona Lisa, Leonardo da Vinci, ca. 1503–1506“). Beides ist wichtig, aber beides beschreibt etwas anderes.

#### Styling von `<figure>`-Elementen mit CSS

Standardmäßig fügen die meisten Browser dem `<figure>`-Element einen Außenabstand (margin) hinzu. Dies führt oft dazu, dass die Figur etwas vom restlichen Text eingerückt wird. Das kannst du mit CSS natürlich nach Belieben anpassen.

Ein typisches CSS-Setup könnte so aussehen:

```css
figure {
  margin: 2em 0; /* Vertikalen Abstand schaffen, seitlichen Standard-Abstand entfernen */
  padding: 1em;
  border: 1px solid #e0e0e0;
  background-color: #f9f9f9;
  max-width: 100%; /* Verhindert, dass die Figur aus dem Elternelement herausragt */
}

/* Sorgt dafür, dass Bilder innerhalb der Figur responsiv sind */
figure img {
  display: block; /* Verhindert unerwünschte Leerräume unter dem Bild */
  max-width: 100%;
  height: auto;
  margin-left: auto;
  margin-right: auto;
}

figcaption {
  margin-top: 1em;
  text-align: center;
  font-style: italic;
  color: #555;
}
```
Mit diesem CSS-Code entfernst du die Standard-Einrückung, fügst einen dezenten Rahmen und Hintergrund hinzu und zentrierst die Beschriftung. Die Regeln für das `img`-Element sind besonders wichtig für ein responsives Design, da sie sicherstellen, dass das Bild niemals breiter wird als sein Container.

Durch die bewusste Verwendung von `<figure>` und `<figcaption>` hebst du deine HTML-Struktur auf ein höheres professionelles Niveau. Du zeichnest deine Inhalte nicht nur so aus, dass sie gut aussehen, sondern so, dass ihre Bedeutung und ihre Beziehung zueinander für Maschinen und Menschen gleichermaßen klar und verständlich sind. Das ist die Essenz von semantischem HTML.
