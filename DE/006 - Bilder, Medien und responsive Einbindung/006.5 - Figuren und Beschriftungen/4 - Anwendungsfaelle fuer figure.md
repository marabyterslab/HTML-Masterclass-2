# Anwendungsfälle für figure

# Anwendungsfälle für figure

Wenn du an das `<figure>`-Element denkst, kommt dir wahrscheinlich sofort ein Bild mit einer Bildunterschrift in den Sinn. Das ist absolut richtig und der häufigste Anwendungsfall. Aber dieses semantische HTML-Element ist weitaus vielseitiger, als es auf den ersten Blick scheint. Lass uns tief in die Welt von `<figure>` und seinem treuen Begleiter, `<figcaption>`, eintauchen und entdecken, wo du sie überall sinnvoll einsetzen kannst.

Die Kernidee hinter `<figure>` ist, eine **eigenständige Inhaltseinheit** zu kapseln. Was bedeutet das? Stell dir vor, du könntest diesen Inhalt – sei es ein Bild, ein Diagramm, ein Code-Beispiel oder ein Zitat – aus dem Haupttext herausnehmen und am Ende des Dokuments in einen Anhang verschieben, ohne dass der Lesefluss des Haupttextes verloren geht. Wenn der Inhalt diese Bedingung erfüllt, ist er ein perfekter Kandidat für `<figure>`. Der Haupttext bezieht sich oft auf diese Figur, zum Beispiel mit einer Formulierung wie „(siehe Abbildung 1)“.

### Der klassische Fall: Ein einzelnes Bild mit Beschriftung

Beginnen wir mit dem bekanntesten Beispiel. Du hast ein Bild, das eine wichtige Information in deinem Artikel illustriert, und du möchtest eine klare, semantisch korrekte Beschriftung hinzufügen. Früher wurden hierfür oft `<div>`-Container mit einem `<img>`- und einem `<p>`-Tag verwendet. Das funktioniert zwar visuell, aber es fehlt die semantische Verbindung. Eine Suchmaschine oder ein Screenreader für sehbehinderte Nutzer weiß nicht, dass der Paragraph die offizielle Beschriftung für das Bild ist.

Hier kommt `<figure>` ins Spiel. Es gruppiert das Bild und seine Beschriftung zu einer logischen Einheit.

```html
<p>Die Golden Gate Bridge in San Francisco ist ein weltberühmtes Wahrzeichen. Ihr Bau begann im Jahr 1933 und war zur damaligen Zeit ein Meisterwerk der Ingenieurskunst. Die charakteristische Farbe "International Orange" wurde gewählt, um die Brücke auch bei dichtem Nebel sichtbar zu machen (siehe Abbildung 1).</p>

<figure>
  <img src="golden-gate-bridge.jpg" alt="Die Golden Gate Bridge im Nebel bei Sonnenuntergang.">
  <figcaption>Abbildung 1: Die Golden Gate Bridge, eingehüllt in den typischen Küstennebel San Franciscos.</figcaption>
</figure>
```

In diesem Beispiel ist klar: Das `<img>`-Element ist der Hauptinhalt der Figur. Das `<figcaption>`-Element (Figure Caption) enthält die offizielle Beschriftung. Diese Struktur ist nicht nur sauber, sondern auch extrem wertvoll für die Barrierefreiheit und die Suchmaschinenoptimierung (SEO). Ein Screenreader würde ansagen: „Abbildung 1: Die Golden Gate Bridge, eingehüllt in den typischen Küstennebel San Franciscos.“ Die Verbindung ist unmissverständlich.

### Mehrere Elemente in einer Figur gruppieren

Die Stärke von `<figure>` geht aber noch weiter. Du bist nicht auf ein einziges Element beschränkt. Stell dir vor, du möchtest eine Serie von Bildern zeigen, die zusammen einen Prozess oder eine Sammlung darstellen. Anstatt für jedes Bild eine eigene Figur zu erstellen, kannst du sie in einer einzigen `<figure>` zusammenfassen und ihnen eine gemeinsame Beschriftung geben.

```html
<p>Der Prozess der Kaffeezubereitung mit einer Siebträgermaschine besteht aus mehreren Schritten, die präzise ausgeführt werden müssen, um ein optimales Ergebnis zu erzielen. Die folgenden Bilder zeigen die Kernschritte von der Bohne bis zum fertigen Espresso.</p>

<figure>
  <img src="schritt1-mahlen.jpg" alt="Kaffeebohnen werden in einer Mühle frisch gemahlen.">
  <img src="schritt2-tampen.jpg" alt="Das gemahlene Kaffeepulver wird im Siebträger festgedrückt (getampt).">
  <img src="schritt3-extraktion.jpg" alt="Der fertige Espresso läuft in die Tasse.">
  <figcaption>Abbildung 2: Die drei Hauptschritte der Espresso-Zubereitung – Mahlen, Tampen und Extrahieren.</figcaption>
</figure>
```

Hier beschreibt die eine `<figcaption>` den gesamten Inhalt der `<figure>`, also alle drei Bilder. Dies ist eine elegante und semantisch korrekte Methode, um zusammengehörige visuelle Elemente zu präsentieren.

### Jenseits von Bildern: Code-Beispiele

Als Webentwickler arbeitest du ständig mit Code. Wenn du in einem Blogbeitrag oder einer Dokumentation ein Code-Snippet zeigst, ist dieses Snippet eine perfekte eigenständige Inhaltseinheit. Es illustriert einen Punkt im Text, könnte aber theoretisch auch in einem Anhang stehen. `<figure>` ist hierfür das ideale Element.

Üblicherweise wird Code in einem `<pre>`-Element (das Leerzeichen und Zeilenumbrüche beibehält) und einem `<code>`-Element (das den Inhalt als Code kennzeichnet) platziert. Diese Kombination kannst du direkt in eine `<figure>` einbetten.

```html
<p>Um eine einfache "Hallo Welt"-Nachricht in der JavaScript-Konsole auszugeben, kannst du die Funktion `console.log()` verwenden. Das folgende Beispiel zeigt die simple Syntax:</p>

<figure>
  <pre><code>console.log("Hallo, Welt!");</code></pre>
  <figcaption>Listing 1: Eine einfache "Hallo Welt"-Ausgabe in JavaScript.</figcaption>
</figure>
```

Durch diese Struktur wird dein Code-Beispiel zu einer referenzierbaren Einheit. Du kannst im Text schreiben „wie in Listing 1 gezeigt“ und die semantische Verknüpfung ist klar. Es ist eine deutliche Aufwertung gegenüber einem einfachen `<pre>`-Tag ohne Kontext.

### Zitate, Diagramme und andere Medien

Die Flexibilität von `<figure>` erlaubt es dir, fast jede Art von referenzierbarem Inhalt damit auszuzeichnen.

**Blockzitate:**
Ein längeres Zitat, das eine wichtige Aussage untermauert, kann ebenfalls in eine Figur gepackt werden. Das `<blockquote>`-Element ist für das Zitat selbst da, während `<figcaption>` den Urheber oder die Quelle nennt.

```html
<p>Bei der Gestaltung von Benutzeroberflächen ist das Prinzip der Einfachheit oft der Schlüssel zum Erfolg. Wie Antoine de Saint-Exupéry treffend bemerkte:</p>

<figure>
  <blockquote>
    <p>Perfektion ist nicht dann erreicht, wenn es nichts mehr hinzuzufügen gibt, sondern wenn man nichts mehr weglassen kann.</p>
  </blockquote>
  <figcaption>
    — Antoine de Saint-Exupéry
  </figcaption>
</figure>
```

**Diagramme und Tabellen:**
Ein komplexes Diagramm (z. B. als SVG oder Bild) oder eine Datentabelle, die deine Argumentation unterstützt, sind ebenfalls perfekte Kandidaten.

```html
<p>Die Verkaufszahlen für das letzte Quartal zeigen ein deutliches Wachstum in allen Produktkategorien, wie die folgende Tabelle verdeutlicht.</p>

<figure>
  <table>
    <caption>Verkaufszahlen Q4</caption>
    <thead>
      <tr>
        <th>Produktkategorie</th>
        <th>Umsatz</th>
        <th>Wachstum</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Widgets</td>
        <td>150.000 €</td>
        <td>+15%</td>
      </tr>
      <tr>
        <td>Gadgets</td>
        <td>220.000 €</td>
        <td>+22%</td>
      </tr>
    </tbody>
  </table>
  <figcaption>Tabelle 1: Umsatzentwicklung im vierten Quartal nach Produktkategorie.</figcaption>
</figure>
```

**Audio und Video:**
Auch mediale Inhalte wie eingebettete Videos oder Audio-Player können von einer `<figure>`-Struktur profitieren. Die Beschriftung kann den Inhalt zusammenfassen, eine Transkription anbieten oder Copyright-Informationen enthalten.

```html
<figure>
  <video controls src="tutorial.mp4">
    Dein Browser unterstützt das Video-Tag nicht.
  </video>
  <figcaption>Video 1: Eine Schritt-für-Schritt-Anleitung zur Verwendung unserer Software.</figcaption>
</figure>
```

### Praktische Hinweise zu Styling und Layout

Standardmäßig fügen die meisten Browser dem `<figure>`-Element einen `margin` (Außenabstand) hinzu. Das führt manchmal zu unerwarteten Layout-Verschiebungen. Es ist eine gängige Praxis, diesen Abstand in deinem CSS zunächst zurückzusetzen und ihn dann nach Bedarf selbst zu definieren:

```css
figure {
  margin: 0;
  /* Füge hier deine eigenen Abstände hinzu, z.B. margin-block: 2rem; */
}
```

Da `<figure>` ein Block-Element ist, kannst du es wie jeden anderen Container stylen. Du kannst ihm einen Rahmen geben, einen Hintergrund hinzufügen oder es im Layout platzieren, zum Beispiel mithilfe von CSS Grid oder Flexbox. Die Tatsache, dass der Inhalt semantisch gekapselt ist, macht das Styling oft einfacher und logischer. Du stylst die gesamte Einheit und nicht nur lose Einzelteile.

### Wann du `<figure>` nicht verwenden solltest

So nützlich `<figure>` auch ist, es ist wichtig zu wissen, wann es *nicht* angebracht ist. Die goldene Regel bleibt: Der Inhalt muss für sich allein stehen können und vom Haupttext referenziert werden.

Verwende `<figure>` nicht für rein dekorative Bilder. Ein Hintergrundbild, ein kleines Icon neben einer Überschrift oder ein schmückendes Element, das keine inhaltliche Relevanz hat und keine Beschriftung benötigt, gehört nicht in eine `<figure>`. Für solche Fälle ist ein einfaches `<img>`-Tag (oft mit einem leeren `alt`-Attribut, `alt=""`, wenn es wirklich rein dekorativ ist) oder noch besser eine CSS `background-image`-Eigenschaft die richtige Wahl.

Wenn ein Bild integraler Bestandteil des Satzes oder des direkten Inhalts ist – zum Beispiel das Logo einer Firma, das direkt im Fließtext erwähnt wird – ist es ebenfalls kein Kandidat für `<figure>`. Es ist dann kein "Anhang", sondern Teil des Hauptinhalts.

Indem du `<figure>` bewusst und korrekt einsetzt, schreibst du nicht nur HTML, das gut aussieht, sondern du schaffst eine reichhaltige, strukturierte und zugängliche Erfahrung für alle Nutzer und Maschinen, die deine Webseite besuchen.
