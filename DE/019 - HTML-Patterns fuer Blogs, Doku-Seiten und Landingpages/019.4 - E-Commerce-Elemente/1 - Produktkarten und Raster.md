# Produktkarten und Raster

### Produktkarten und Raster

Wenn du einen Online-Shop oder eine Produktübersicht baust, sind Produktkarten und das Raster, in dem sie angeordnet sind, das Herzstück deiner Präsentation. Stell sie dir als das digitale Äquivalent zu den Regalen in einem Laden vor. Jede Karte ist ein einzelnes Produkt, das die Aufmerksamkeit auf sich ziehen und die wichtigsten Informationen auf einen Blick vermitteln muss. Das Raster ist das Regalsystem, das für Ordnung und eine ansprechende Darstellung sorgt.

#### Die Anatomie einer Produktkarte

Eine gute Produktkarte ist wie ein Mini-Verkaufsgespräch. Sie muss informativ, ansprechend und funktional sein. Bevor wir sie in ein Raster packen, zerlegen wir eine einzelne Karte in ihre wesentlichen Bestandteile.

1.  **Der Container:** Jede Karte braucht eine Hülle, die alle ihre Elemente zusammenhält. Semantisch gesehen ist ein `<article>`-Element hierfür die beste Wahl. Ein Produkt ist eine in sich geschlossene, eigenständige Informationseinheit, die auch für sich allein stehen könnte – die genaue Definition eines `<article>`. Ein `<div>` würde zwar auch funktionieren, aber `<article>` gibt dem Browser und Suchmaschinen einen klareren Hinweis auf die Bedeutung des Inhalts.

2.  **Das Produktbild:** Das ist oft das Erste, was ein Nutzer wahrnimmt. Ein `<img>`-Tag ist hierfür die logische Wahl. Entscheidend ist, immer ein aussagekräftiges `alt`-Attribut zu verwenden. Es beschreibt das Bild für Screenreader und wird angezeigt, falls das Bild nicht geladen werden kann. Für ein Produktbild könnte das zum Beispiel `alt="Weißer Sneaker aus Leder mit roten Streifen"` sein.

3.  **Der Produkttitel:** Der Name des Produkts sollte klar und deutlich erkennbar sein. Dafür eignet sich eine Überschrift, zum Beispiel ein `<h3>`. Warum nicht `<h1>`? Weil die `<h1>` in der Regel für den Haupttitel der gesamten Seite reserviert ist (z.B. "Unsere Sneaker-Kollektion"). Die Produkttitel sind untergeordnete Überschriften. Die Wahl zwischen `<h2>`, `<h3>` oder `<h4>` hängt von der Gesamtstruktur deiner Seite ab. Wichtig ist, die Hierarchie logisch zu halten.

4.  **Der Preis:** Eine der wichtigsten Informationen. Ein einfacher `<p>`-Tag, oft mit einer spezifischen Klasse für das Styling, ist hier ausreichend. Manchmal wird der Preis auch in einem `<span>` oder `<strong>`-Tag platziert, um ihn besonders hervorzuheben.

5.  **Die Kurzbeschreibung (optional):** Ein oder zwei Sätze, die das Produkt anpreisen oder seine wichtigsten Merkmale zusammenfassen. Auch hier ist ein `<p>`-Tag die richtige Wahl.

6.  **Der Call-to-Action (CTA):** Der Button, der den Nutzer zur nächsten Aktion auffordert, meist "In den Warenkorb" oder "Details ansehen". Dies kann ein `<a>`-Tag sein, der zur Produktdetailseite führt, oder ein `<button>`, der eine Aktion per JavaScript auslöst. Für eine reine Produktübersicht ist der Link zur Detailseite der gängigste Weg.

#### Der HTML-Aufbau einer einzelnen Karte

Lass uns diese Bausteine nun zu einem sauberen HTML-Konstrukt zusammensetzen. Wir verwenden BEM-ähnliche Klassennamen (`block__element`), um die Struktur klar und für CSS leicht ansprechbar zu machen.

```html
<article class="product-card">
  <a href="/produkt/sneaker-modell-x" class="product-card__image-link">
    <img src="sneaker-x.jpg" alt="Weißer Sneaker aus Leder mit roten Streifen" class="product-card__image">
  </a>
  <div class="product-card__content">
    <h3 class="product-card__title">
      <a href="/produkt/sneaker-modell-x">Sneaker Modell X</a>
    </h3>
    <p class="product-card__price">99,95 €</p>
    <p class="product-card__description">
      Ein bequemer und stylischer Begleiter für den Alltag aus nachhaltigen Materialien.
    </p>
    <a href="/warenkorb?add=123" class="product-card__cta">In den Warenkorb</a>
  </div>
</article>
```

In diesem Beispiel haben wir ein paar bewährte Praktiken umgesetzt:
*   Sowohl das Bild als auch der Titel sind klickbar und führen zur selben Produktseite. Das verbessert die Benutzerfreundlichkeit, da Nutzer instinktiv auf beides klicken.
*   Der Container für den textlichen Inhalt (`.product-card__content`) hilft bei der Strukturierung und dem Styling mit CSS.
*   Der CTA-Button ist ein Link, der direkt zum Warenkorb führen oder eine "In den Warenkorb"-Aktion auslösen könnte.

#### Vom Einzelstück zum geordneten Raster

Eine einzelne Karte macht noch keinen Shop. Die wahre Stärke entfaltet sich, wenn du mehrere Karten in einem sauberen, responsiven Raster anordnest. Früher war das mit HTML und CSS eine komplizierte Angelegenheit, die oft auf Tricks wie `float` oder `inline-block` zurückgriff. Heute haben wir dafür zwei mächtige Werkzeuge: **Flexbox** und **CSS Grid**.

Für Produktgitter ist CSS Grid meist die überlegene Wahl. Es wurde speziell für zweidimensionale Layouts (Zeilen und Spalten) entwickelt und macht die Erstellung eines flexiblen Rasters unglaublich einfach.

Zuerst brauchen wir einen Container, der alle unsere Produktkarten umschließt. Ein `<section>`-Element ist hierfür semantisch passend, da es eine thematische Gruppierung von Inhalten darstellt.

```html
<section class="product-grid">
  <article class="product-card">
    <!-- Inhalt der ersten Karte -->
  </article>
  <article class="product-card">
    <!-- Inhalt der zweiten Karte -->
  </article>
  <article class="product-card">
    <!-- Inhalt der dritten Karte -->
  </article>
  <!-- ... und so weiter -->
</section>
```

Jetzt kommt die Magie mit CSS. Wir weisen dem `.product-grid`-Container die Eigenschaft `display: grid;` zu und definieren dann, wie die Spalten aussehen sollen.

```css
.product-grid {
  display: grid;
  gap: 2rem; /* Abstand zwischen den Karten */
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}
```

Lass uns diese eine Zeile `grid-template-columns` genauer ansehen, denn sie ist extrem leistungsfähig:

*   `repeat()`: Diese Funktion sagt dem Browser, dass er ein Muster wiederholen soll, anstatt dass wir jede Spalte manuell definieren müssen.
*   `auto-fit`: Das ist der Schlüssel zur Responsivität. Der Browser wird automatisch so viele Spalten erstellen, wie in den verfügbaren Platz passen. Wenn der Bildschirm schmaler wird, reduziert er die Anzahl der Spalten von selbst.
*   `minmax(250px, 1fr)`: Dies definiert die Größe jeder einzelnen Spalte.
    *   `250px` ist die minimale Breite. Keine Karte wird schmaler als 250 Pixel. Das verhindert, dass der Inhalt bei sehr schmalen Spalten unleserlich wird.
    *   `1fr` (ein "fractional unit" oder Bruchteil) ist die maximale Breite. Es bedeutet: "Nimm einen Anteil des verfügbaren freien Platzes". Wenn alle Spalten `1fr` haben, teilen sie sich den Platz gleichmäßig auf. Das sorgt dafür, dass die Karten den Bildschirm ausfüllen und keine unschönen Lücken am Rand entstehen.

Das Ergebnis ist ein perfektes, responsives Raster, das sich ohne eine einzige Media Query an jede Bildschirmgröße anpasst. Auf einem großen Desktop-Monitor siehst du vielleicht vier oder fünf Karten nebeneinander, auf einem Tablet zwei oder drei und auf einem Smartphone nur eine pro Zeile.

#### Feinschliff und Konsistenz

Damit das Raster harmonisch wirkt, ist es wichtig, dass alle Karten eine konsistente Höhe haben. Wenn Produktbeschreibungen unterschiedlich lang sind, kann dies zu ungleichen Kartenhöhen führen, was unordentlich aussieht.

Mit Flexbox oder Grid lässt sich dieses Problem leicht lösen. Wenn du CSS Grid verwendest (wie in unserem Beispiel), werden die Karten in einer Zeile standardmäßig bereits die gleiche Höhe haben. Falls du jedoch Flexbox für den Inhalt *innerhalb* einer Karte verwendest, kannst du sicherstellen, dass zum Beispiel der CTA-Button immer am unteren Rand der Karte ausgerichtet ist, egal wie lang der Beschreibungstext ist.

Ein einfaches Beispiel für das Styling der Karte selbst:

```css
.product-card {
  border: 1px solid #eee;
  border-radius: 8px;
  overflow: hidden; /* Stellt sicher, dass z.B. abgerundete Ecken beim Bild funktionieren */
  display: flex;
  flex-direction: column; /* Ordnet die Elemente in der Karte untereinander an */
  box-shadow: 0 4px 8px rgba(0,0,0,0.05);
  transition: box-shadow 0.3s ease;
}

.product-card:hover {
  box-shadow: 0 6px 12px rgba(0,0,0,0.1);
}

.product-card__image {
  width: 100%;
  height: auto;
  aspect-ratio: 1 / 1; /* Sorgt für quadratische Bilder, passt sich der Breite an */
  object-fit: cover; /* Verhindert, dass Bilder verzerrt werden */
}

.product-card__content {
  padding: 1.5rem;
  flex-grow: 1; /* Wichtiger Teil für gleiche Höhe! */
  display: flex;
  flex-direction: column;
}

.product-card__title {
  font-size: 1.25rem;
  margin: 0 0 0.5rem 0;
}

.product-card__price {
  font-size: 1.1rem;
  font-weight: bold;
  color: #333;
  margin: 0 0 1rem 0;
}

.product-card__description {
  flex-grow: 1; /* Schiebt den Button nach unten */
  margin: 0 0 1.5rem 0;
  color: #666;
  line-height: 1.5;
}

.product-card__cta {
  display: inline-block;
  background-color: #007bff;
  color: white;
  text-decoration: none;
  padding: 0.75rem 1.5rem;
  border-radius: 4px;
  text-align: center;
  margin-top: auto; /* Klebt den Button am unteren Rand, wenn flex-grow genutzt wird */
  transition: background-color 0.3s ease;
}

.product-card__cta:hover {
  background-color: #0056b3;
}
```
In diesem CSS-Beispiel sorgt die Kombination aus `display: flex` auf `.product-card` und `.product-card__content` sowie `flex-grow: 1` auf den textlichen Elementen dafür, dass sich der Inhalt ausdehnt und der CTA-Button immer bündig am unteren Ende der Karte positioniert ist. Das schafft ein sauberes und professionelles Erscheinungsbild für dein gesamtes Produktraster.
