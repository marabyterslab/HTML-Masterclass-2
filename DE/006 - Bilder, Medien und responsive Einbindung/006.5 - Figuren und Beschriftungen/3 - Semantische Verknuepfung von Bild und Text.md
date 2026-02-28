# Semantische Verknüpfung von Bild und Text

### Semantische Verknüpfung von Bild und Text: Die Elemente `<figure>` und `<figcaption>`

In der Welt des Webdesigns ist es eine alltägliche Aufgabe, ein Bild auf einer Seite zu platzieren und es mit einer kurzen Beschreibung oder einem Titel zu versehen. Vielleicht hast du das schon oft getan, indem du ein `<img>`-Element verwendet und direkt darunter einen `<p>`-Tag mit dem Beschreibungstext gesetzt hast.

```html
<img src="weg-im-wald.jpg" alt="Ein sonniger Pfad, der durch einen dichten Laubwald führt.">
<p>Abbildung 1: Wanderweg im Teutoburger Wald im Herbst.</p>
```

Auf den ersten Blick sieht das Ergebnis im Browser völlig in Ordnung aus. Das Bild wird angezeigt, und der Text steht darunter. Problem gelöst, oder? Nicht ganz. Obwohl es visuell funktioniert, fehlt hier eine entscheidende Komponente: die semantische Verbindung. Für den Browser, für Suchmaschinen und vor allem für Hilfstechnologien wie Screenreader sind das Bild und der Absatz zwei völlig getrennte, unabhängige Inhaltselemente. Sie stehen nur zufällig nebeneinander. Der Browser weiß nicht, dass der Text eine Bildunterschrift *ist*. Er weiß nur, dass nach einem Bild ein Absatz folgt.

Genau für dieses Problem hat HTML eine elegante und semantisch korrekte Lösung parat: die Elemente `<figure>` und `<figcaption>`.

#### Was ist eine `<figure>`?

Stell dir das `<figure>`-Element wie einen schützenden Rahmen vor. Es ist ein Container für in sich geschlossene Inhalte, die oft als Einheit referenziert werden und aus dem Haupttextfluss herausgenommen werden könnten, ohne dessen Verständlichkeit zu beeinträchtigen. Das klingt vielleicht etwas abstrakt, aber die Idee ist einfach: Wenn du einen Inhalt hast – sei es ein Bild, ein Diagramm, ein Code-Beispiel oder eine Grafik –, der für sich allein stehen kann und im Text vielleicht mit "siehe Abbildung 1" oder "wie im folgenden Beispiel" erwähnt wird, dann ist `<figure>` der perfekte Container dafür.

#### Die Rolle von `<figcaption>`

Innerhalb dieses `<figure>`-Rahmens spielt `<figcaption>` (Figure Caption) eine spezielle Rolle. Es ist das offizielle Etikett, die Beschriftung für den Inhalt der Figur. Indem du deinen Beschreibungstext in ein `<figcaption>`-Element packst und dieses zusammen mit dem Bild in ein `<figure>`-Element einschließt, schaffst du eine unmissverständliche, semantische Verbindung.

Schauen wir uns unser ursprüngliches Beispiel in der korrekten Schreibweise an:

```html
<figure>
  <img src="weg-im-wald.jpg" alt="Ein sonniger Pfad, der durch einen dichten Laubwald führt.">
  <figcaption>Abbildung 1: Wanderweg im Teutoburger Wald im Herbst.</figcaption>
</figure>
```

Der Unterschied ist subtil, aber wirkungsvoll. Jetzt ist für jede Maschine, die deinen Code liest, klar: Das `<img>`-Element und das `<figcaption>`-Element gehören untrennbar zusammen. Die Bildunterschrift ist nicht mehr nur irgendein Absatz, sondern explizit die Beschriftung für dieses Bild. Die Position der `<figcaption>` innerhalb der `<figure>` ist übrigens flexibel; sie kann vor oder nach dem Bildelement stehen, je nachdem, was für dein Design sinnvoller ist.

#### Der wichtige Unterschied: `alt` vs. `<figcaption>`

Ein häufiger Punkt der Verwirrung ist der Unterschied zwischen dem `alt`-Attribut eines Bildes und der `<figcaption>`. Die Unterscheidung ist jedoch klar und wichtig:

*   **Das `alt`-Attribut (Alternativtext):** Seine Aufgabe ist es, den *Inhalt des Bildes* zu beschreiben. Es ist für den Fall da, dass das Bild nicht geladen werden kann, und vor allem wird es von Screenreadern für sehbehinderte Nutzer vorgelesen. Der `alt`-Text ist ein direkter Ersatz für das Bild. Er sollte präzise beschreiben, was auf dem Bild zu sehen ist. Im Beispiel oben: `"Ein sonniger Pfad, der durch einen dichten Laubwald führt."`
*   **Das `<figcaption>`-Element (Bildunterschrift):** Es liefert *Kontext*, eine *Interpretation* oder einen *Titel* für das Bild. Es ergänzt das Bild, anstatt es zu ersetzen. Oft enthält es Informationen, die man nicht allein durch das Betrachten des Bildes ableiten kann, wie den Ort, den Namen des Fotografen, das Datum oder eine numerische Referenz wie "Abbildung 1". Im Beispiel: `"Abbildung 1: Wanderweg im Teutoburger Wald im Herbst."`

Beide sind für eine gute und barrierefreie Website unerlässlich und erfüllen unterschiedliche Zwecke.

#### Warum der semantische Aufwand sich lohnt

Du fragst dich vielleicht, warum diese semantische Korrektheit so wichtig ist, wenn das Ergebnis visuell doch fast identisch aussieht. Die Vorteile liegen unter der Haube und sind entscheidend für eine professionelle Webentwicklung.

**1. Barrierefreiheit (Accessibility):**
Dies ist der wichtigste Grund. Ein Screenreader, der auf eine `<figure>` mit einer `<figcaption>` trifft, kann diese als zusammengehörige Einheit ansagen. Er könnte zum Beispiel sagen: "Abbildung, mit Beschriftung: Abbildung 1: Wanderweg im Teutoburger Wald im Herbst. Bild: Ein sonniger Pfad, der durch einen dichten Laubwald führt." Diese klare Struktur gibt Nutzern, die auf Hilfstechnologien angewiesen sind, den vollen Kontext und macht deine Inhalte verständlicher und zugänglicher. Bei der getrennten `<img>`- und `<p>`-Variante würde der Nutzer nur zwei unverbundene Inhaltsteile hören.

**2. Suchmaschinenoptimierung (SEO):**
Suchmaschinen wie Google werden immer besser darin, den Inhalt und die Struktur einer Webseite zu verstehen. Eine klare semantische Auszeichnung hilft ihnen dabei. Wenn du ein Bild mit einer relevanten `<figcaption>` versiehst, gibst du der Suchmaschine wertvolle Informationen darüber, worum es in dem Bild geht und in welchem Kontext es steht. Dies kann die Sichtbarkeit deiner Bilder in der Bildersuche und das allgemeine Ranking deiner Seite positiv beeinflussen.

**3. Styling mit CSS:**
Da `<figure>` ein Container ist, kannst du das Bild und seine Beschriftung ganz einfach als eine visuelle Einheit gestalten. Du kannst dem `<figure>`-Element einen Rahmen, einen Schatten, eine Hintergrundfarbe oder bestimmte Abstände geben, und diese Stile werden auf das gesamte Paket angewendet.

```css
figure {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 20px 0; /* Etwas Abstand nach oben und unten */
  background-color: #f9f9f9;
  max-width: 100%; /* Sorgt dafür, dass die Figur nicht über den Container hinausragt */
}

figure img {
  max-width: 100%;
  height: auto; /* Wichtig für responsives Verhalten */
  display: block; /* Verhindert unerwünschte Leerräume unter dem Bild */
}

figure figcaption {
  text-align: center;
  font-style: italic;
  font-size: 0.9em;
  color: #555;
  margin-top: 8px;
}
```

Mit diesem CSS-Code wird jede Figur auf deiner Seite einheitlich mit einem dezenten Rahmen und einer zentrierten, kursiven Beschriftung versehen. Das wäre mit einer losen Kombination aus `<img>` und `<p>` deutlich umständlicher zu erreichen.

#### Mehr als nur Bilder: Die Vielseitigkeit von `<figure>`

Obwohl die häufigste Anwendung die Kombination mit Bildern ist, ist das `<figure>`-Element weitaus vielseitiger. Du kannst es für jede Art von in sich geschlossenem Inhalt verwenden, der eine Beschriftung benötigt.

**Beispiel mit einem Code-Block:**

```html
<figure>
  <figcaption>Beispiel 2: Eine einfache "Hallo Welt"-Funktion in JavaScript.</figcaption>
  <pre><code>function sagHallo(name) {
  console.log(`Hallo, ${name}!`);
}

sagHallo("Welt");</code></pre>
</figure>
```
Hier wird ein Code-Beispiel semantisch korrekt mit seiner Erklärung verknüpft.

**Beispiel mit mehreren Bildern:**

Du kannst sogar mehrere Bilder in einer einzigen `<figure>` gruppieren, die sich eine gemeinsame Beschriftung teilen.

```html
<figure>
  <img src="schritt1.jpg" alt="Zutaten auf einem Tisch.">
  <img src="schritt2.jpg" alt="Teig wird geknetet.">
  <img src="schritt3.jpg" alt="Brot im Ofen.">
  <figcaption>Abbildung 3: Die drei Hauptschritte beim Brotbacken.</figcaption>
</figure>
```

Die Verwendung von `<figure>` und `<figcaption>` ist ein Paradebeispiel dafür, wie man in HTML über die reine visuelle Darstellung hinausdenkt. Es ist eine Praxis, die deine Webseiten robuster, zugänglicher und professioneller macht. Es ist der Unterschied zwischen dem reinen Platzieren von Elementen und dem bewussten Strukturieren von Bedeutung.
