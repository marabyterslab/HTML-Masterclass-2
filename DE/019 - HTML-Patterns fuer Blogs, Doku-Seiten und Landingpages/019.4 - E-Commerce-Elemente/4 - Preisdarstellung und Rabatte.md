# Preisdarstellung und Rabatte

### Preisdarstellung und Rabatte

In jedem E-Commerce-Projekt ist die Darstellung von Preisen ein zentraler und sensibler Punkt. Es geht nicht nur darum, eine Zahl auf den Bildschirm zu bringen. Eine gute Preisdarstellung ist klar, ehrlich und aus technischer Sicht semantisch korrekt und barrierefrei. Sie beeinflusst die Kaufentscheidung und das Vertrauen deiner Nutzer maßgeblich. Besonders bei Rabattaktionen kommt es darauf an, die Preisreduzierung so darzustellen, dass sie sowohl für Menschen als auch für Maschinen (wie Suchmaschinen-Crawler) verständlich ist.

#### Die einfache Preisdarstellung

Beginnen wir mit dem einfachsten Fall: einem einzelnen Preis ohne Rabatt. Man könnte versucht sein, den Preis einfach als Text in einen Paragrafen zu schreiben:

```html
<p>19,99 €</p>
```

Das funktioniert, ist aber nicht ideal. Du gibst dem Preis keine spezifische semantische Bedeutung und machst es dir schwerer, ihn gezielt mit CSS zu gestalten oder mit JavaScript darauf zuzugreifen. Eine bessere Praxis ist es, den Preis in ein `<span>`-Element zu verpacken. Das `<span>` ist ein generisches Inline-Element, das keine eigene semantische Bedeutung hat, sich aber hervorragend als Haken für Styling und Skripte eignet.

```html
<div class="product-price">
  <span>19,99 €</span>
</div>
```

Mit einer CSS-Klasse wie `.product-price` kannst du nun den gesamten Preisbereich gestalten, zum Beispiel die Schriftgröße oder Farbe anpassen.

#### Die Kunst der Rabattdarstellung: `<del>` und `<ins>`

Jetzt wird es interessant. Wie stellst du einen Rabatt dar? Üblicherweise siehst du einen durchgestrichenen alten Preis neben einem neuen, hervorgehobenen Preis. Ein häufiger, aber semantisch ungenauer Ansatz wäre die Verwendung von `<s>` (strikethrough) und `<b>` (bold).

```html
<!-- Semantisch nicht optimal -->
<p>
  <s>29,99 €</s> <b>19,99 €</b>
</p>
```

Warum ist das nicht optimal? Das `<s>`-Element bedeutet laut HTML-Spezifikation lediglich, dass etwas nicht mehr relevant oder akkurat ist. Das `<b>`-Element dient nur der visuellen Hervorhebung, ohne dem Inhalt eine besondere Wichtigkeit zu verleihen. Das passt zwar oberflächlich, aber HTML bietet uns präzisere Werkzeuge.

Die semantisch korrekte Methode zur Darstellung von Preisänderungen sind die Elemente `<del>` (delete) und `<ins>` (insert).

*   `<del>`: Markiert Inhalt, der aus dem Dokument entfernt wurde.
*   `<ins>`: Markiert Inhalt, der dem Dokument hinzugefügt wurde.

Bezogen auf einen Preis bedeutet das: Der alte Preis wurde „entfernt“ und der neue Preis wurde „eingefügt“. Das beschreibt exakt den Vorgang einer Preissenkung.

```html
<div class="product-price">
  <del>29,99 €</del>
  <ins>19,99 €</ins>
</div>
```

Standardmäßig rendern Browser `<del>`-Text durchgestrichen und `<ins>`-Text unterstrichen. Das ist ein guter Ausgangspunkt, aber für eine ansprechende Optik im E-Commerce passen wir das Styling meist mit CSS an.

```css
.product-price del {
  color: #888; /* Ein dezentes Grau für den alten Preis */
  text-decoration: line-through;
  font-size: 0.9em; /* Etwas kleiner, um ihn weniger dominant zu machen */
  margin-right: 8px; /* Ein kleiner Abstand zum neuen Preis */
}

.product-price ins {
  color: #e44d26; /* Eine auffällige Farbe für den neuen Preis */
  font-weight: bold;
  text-decoration: none; /* Die standardmäßige Unterstreichung entfernen wir */
  font-size: 1.2em; /* Größer, um die Aufmerksamkeit zu lenken */
}
```

Mit diesem HTML und CSS hast du eine Darstellung, die nicht nur visuell klar ist, sondern auch die Bedeutung der Preisänderung im Code selbst transportiert.

#### Preise für Suchmaschinen: Strukturierte Daten mit Schema.org

Damit nicht nur Menschen, sondern auch Suchmaschinen wie Google deine Preise verstehen, solltest du strukturierte Daten verwenden. Dies ermöglicht es Google, Rich Snippets in den Suchergebnissen anzuzeigen, also Preise, Verfügbarkeit und Bewertungen direkt unter deinem Link. Der gängigste Standard hierfür ist Schema.org.

Du integrierst Schema.org-Vokabular über Mikrodaten direkt in dein HTML. Dazu verwendest du Attribute wie `itemscope`, `itemtype` und `itemprop`.

Ein Produkt wird als `Product` definiert, und sein Preis ist Teil eines `Offer` (Angebot).

Schauen wir uns ein vollständiges Beispiel an, das Semantik, Zugänglichkeit und strukturierte Daten kombiniert:

```html
<div class="product-card" itemscope itemtype="http://schema.org/Product">
  <h2 itemprop="name">Der ultimative HTML-Kaffebecher</h2>
  
  <div class="product-price" itemprop="offers" itemscope itemtype="http://schema.org/Offer">
    <!-- Preisinformationen für Suchmaschinen -->
    <meta itemprop="priceCurrency" content="EUR" />
    <meta itemprop="price" content="19.99" />
    
    <!-- Visuelle Preisdarstellung für Menschen -->
    <del>29,99 €</del>
    <ins>19,99 €</ins>
  </div>
</div>
```

Lass uns das aufschlüsseln:

1.  **`itemscope`**: Definiert den Geltungsbereich eines Elements als ein „Item“. Alles innerhalb dieses `<div>` gehört zum selben Datenelement.
2.  **`itemtype="http://schema.org/Product"`**: Gibt an, dass es sich bei diesem Item um ein Produkt handelt.
3.  **`itemprop="name"`**: Weist den Inhalt des `<h2>`-Elements der Eigenschaft „name“ des Produkts zu.
4.  **`itemprop="offers"`**: Innerhalb des Produkts definieren wir ein Angebot. Auch dieses bekommt ein `itemscope` und ein `itemtype="http://schema.org/Offer"`.
5.  **`meta itemprop="priceCurrency" content="EUR"`**: Hier geben wir die Währung im maschinenlesbaren ISO-4217-Format an. Das `<meta>`-Tag ist für den Nutzer unsichtbar.
6.  **`meta itemprop="price" content="19.99"`**: Ebenso geben wir hier den Preis in einem reinen Zahlenformat an (mit Punkt als Dezimaltrennzeichen), das Maschinen leicht verarbeiten können.

Die Elemente `<del>` und `<ins>` bleiben für die visuelle Darstellung erhalten. Sie sind für den Menschen gedacht. Die `<meta>`-Tags liefern dieselbe Information in einer sauberen, strukturierten Form für Maschinen. Schema.org hat keine dedizierte Eigenschaft für den "alten Preis", da Suchmaschinen primär am aktuellen, gültigen Angebot interessiert sind. Der durchgestrichene Preis ist also in erster Linie eine Information für deine menschlichen Besucher.

#### Barrierefreiheit nicht vergessen

Die Verwendung von `<del>` und `<ins>` ist auch ein Gewinn für die Barrierefreiheit. Screenreader, die von Menschen mit Sehbehinderungen genutzt werden, kündigen diese Elemente korrekt an. Ein Screenreader könnte den Preis vorlesen als: „durchgestrichen 29,99 Euro, eingefügt 19,99 Euro“. Dies vermittelt die Preisreduktion viel klarer als eine rein visuelle Formatierung, die für den Screenreader unsichtbar wäre.

Zusätzlich kannst du den Rabatt explizit für Screenreader-Nutzer angeben. Oft wird der prozentuale Rabatt visuell als kleines Badge dargestellt. Du kannst diese Information auch in einem für sehende Nutzer verborgenen `<span>` bereitstellen.

```html
<div class="product-price" itemprop="offers" itemscope itemtype="http://schema.org/Offer">
  <!-- ... Meta-Tags für Schema.org ... -->
  
  <del>29,99 €</del>
  <ins>19,99 €</ins>
  <span class="visually-hidden">Sie sparen 33 Prozent.</span>
</div>
```

Die CSS-Klasse `.visually-hidden` versteckt das Element visuell, hält es aber für Screenreader zugänglich:

```css
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border-width: 0;
}
```

Diese Technik stellt sicher, dass alle Nutzer, unabhängig von ihren Fähigkeiten, die volle Information über den Preis und den damit verbundenen Vorteil erhalten. Eine durchdachte Preisdarstellung ist also eine Kombination aus korrekter HTML-Semantik, ansprechendem CSS-Styling, maschinenlesbaren strukturierten Daten und einem Bewusstsein für Barrierefreiheit.
