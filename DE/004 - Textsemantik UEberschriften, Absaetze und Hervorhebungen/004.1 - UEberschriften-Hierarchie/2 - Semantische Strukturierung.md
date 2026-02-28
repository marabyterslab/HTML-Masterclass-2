# Semantische Strukturierung

### Die verborgene Ordnung: Semantische Strukturierung mit Überschriften

Stell dir vor, du schlägst ein Buch auf und siehst nur eine endlose Wand aus Text. Keine Kapitelüberschriften, keine Absätze, keine Zwischenüberschriften. Es wäre eine Qual, den Inhalt zu erfassen, die Struktur zu verstehen oder eine bestimmte Information wiederzufinden. Was dieses Buch unlesbar macht, ist das Fehlen einer klaren Struktur – einer Ordnung, die dem Inhalt eine Bedeutung gibt.

Genau diese Aufgabe übernimmt HTML für eine Webseite. Deine erste und wichtigste Aufgabe als Webentwickler ist es nicht, festzulegen, wie etwas *aussieht*, sondern zu definieren, was etwas *ist*. Das ist der Kern der Semantik: die Lehre von der Bedeutung. Semantisches HTML bedeutet, dass du Elemente so verwendest, dass sie die Bedeutung und die Struktur deines Inhalts exakt beschreiben. Du sagst dem Browser, dem Suchmaschinen-Crawler und dem Screenreader: „Dieser Text hier ist die Hauptüberschrift der Seite“, „Das ist ein wichtiger Absatz“ oder „Hier beginnt ein neuer, eigenständiger Themenblock“.

Das visuelle Erscheinungsbild, also Schriftgrößen, Farben und Abstände, ist dabei zunächst zweitrangig. Das ist die Aufgabe von CSS, die wir später behandeln. In HTML schaffen wir das reine, logische Gerüst. Und das Fundament dieses Gerüsts ist die Hierarchie der Überschriften.

#### Die Hierarchie der Überschriften: Das Inhaltsverzeichnis deiner Seite

HTML stellt dir sechs Ebenen von Überschriften zur Verfügung: `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>` und `<h6>`. Diese Elemente sind nicht einfach nur dazu da, Text in sechs verschiedenen Größen darzustellen. Sie sind dazu da, eine logische Gliederung für dein Dokument zu erstellen, ganz ähnlich dem Inhaltsverzeichnis in einem Buch.

**`<h1>`: Der Titel deines Dokuments**

Die `<h1>`-Überschrift ist die wichtigste Überschrift auf deiner Seite. Sie sollte den Haupttitel des gesamten Dokuments enthalten und den Inhalt der Seite prägnant zusammenfassen. Betrachte sie als den Buchtitel. Aus diesem Grund sollte es in der Regel nur eine einzige `<h1>`-Überschrift pro Seite geben. Sie ist der Ankerpunkt, um den sich die gesamte restliche Struktur aufbaut.

**`<h2>` bis `<h6>`: Die Gliederung der Inhalte**

Alle weiteren Überschriften dienen dazu, den Inhalt hierarchisch zu untergliedern. Eine `<h2>`-Überschrift markiert einen Hauptabschnitt, der ein Unterthema der `<h1>`-Überschrift ist. Eine `<h3>`-Überschrift wiederum unterteilt einen `<h2>`-Abschnitt weiter, und so weiter.

Die goldene Regel lautet: Überspringe niemals eine Ebene. Du würdest in einem Buch auch kein Unter-Unterkapitel (1.1.1) direkt nach einem Hauptkapitel (1) beginnen, ohne ein Unterkapitel (1.1) dazwischen. Ein Sprung von einer `<h2>` direkt zu einer `<h4>` ist semantisch falsch, weil er die logische Gliederung durchbricht. Es ist, als würdest du in deinem Inhaltsverzeichnis einen Punkt auslassen – die Struktur wird unlogisch und schwer zu verfolgen.

Schauen wir uns ein korrektes Beispiel für die Gliederung eines Blogartikels an:

```html
<article>
  <h1>Die Kunst des Brotbackens zu Hause</h1>

  <p>Brotbacken ist eine meditative und lohnende Tätigkeit. In diesem Artikel lernst du die Grundlagen kennen.</p>

  <h2>1. Die Zutaten: Das Fundament des Geschmacks</h2>
  <p>Gutes Brot braucht nicht viel, aber die Qualität der Zutaten ist entscheidend.</p>
  
  <h3>Mehl: Die Seele des Brotes</h3>
  <p>Wir vergleichen Weizenmehl, Dinkelmehl und Roggenmehl...</p>

  <h3>Wasser: Mehr als nur Flüssigkeit</h3>
  <p>Die Temperatur und Qualität des Wassers beeinflussen die Gärung...</p>
  
  <h3>Hefe und Sauerteig: Die Triebkräfte</h3>
  <p>Hier erklären wir den Unterschied zwischen frischer Hefe, Trockenhefe und einem lebendigen Sauerteig-Starter.</p>

  <h2>2. Der Prozess: Schritt für Schritt zum perfekten Brot</h2>
  <p>Vom Kneten bis zum Backen – hier ist die genaue Anleitung.</p>

  <h3>Der Teig: Kneten und Ruhen</h3>
  <p>Wie lange und wie intensiv du kneten solltest, hängt vom Teig ab...</p>
  
  <h3>Das Formen: Laibe und Brötchen</h3>
  <p>Wir zeigen dir Techniken, wie du deinen Teig in die gewünschte Form bringst.</p>
  
  <h2>3. Häufige Fehler und wie du sie vermeidest</h2>
  <p>Dein Brot ist zu flach oder die Kruste zu hart? Hier sind die Lösungen.</p>
</article>
```

In diesem Beispiel siehst du eine perfekte Gliederung. Die `<h1>` gibt das Hauptthema vor. Die drei `<h2>`-Überschriften teilen den Artikel in logische Hauptabschnitte: Zutaten, Prozess und Fehlerbehebung. Innerhalb des ersten Abschnitts verfeinern die `<h3>`-Überschriften das Thema weiter. Die Struktur ist klar, logisch und für jeden – ob Mensch oder Maschine – sofort verständlich.

#### Warum ist diese semantische Ordnung so wichtig?

Du könntest argumentieren: „Aber ich kann doch mit CSS jeden Text groß und fett machen, warum brauche ich dann `<h2>` oder `<h3>`?“ Die Antwort liegt darin, wer oder was deine Webseite noch „liest“, außer den sehenden Benutzern.

**1. Barrierefreiheit und Screenreader**

Für Menschen mit Sehbehinderungen, die einen Screenreader nutzen, ist die Überschriften-Hierarchie das wichtigste Navigationsinstrument auf einer Webseite. Ein Screenreader ist eine Software, die den Bildschirminhalt vorliest. Anstatt sich linear durch hunderte von Wörtern zu kämpfen, können Nutzer von einer Überschrift zur nächsten springen, um sich einen schnellen Überblick über den Inhalt der Seite zu verschaffen. Sie können sich eine Liste aller `<h2>`-Überschriften ausgeben lassen, um direkt zu dem Abschnitt zu springen, der sie interessiert.

Wenn du Überschriften nur für visuelle Effekte missbrauchst – zum Beispiel eine `<h4>` verwendest, weil dir die Schriftgröße gefällt, obwohl eine `<h2>` logisch korrekt wäre –, zerstörst du diese Navigationsmöglichkeit. Die Seite wird zu einem unstrukturierten Chaos, das für diese Nutzergruppe praktisch unbenutzbar ist. Eine korrekte semantische Struktur ist kein „Nice-to-have“, sie ist eine grundlegende Voraussetzung für ein inklusives Web.

**2. Suchmaschinenoptimierung (SEO)**

Suchmaschinen wie Google sind im Grunde „blinde Roboter“. Sie sehen nicht die Farben und das Layout deiner Seite. Stattdessen analysieren sie den HTML-Code, um die Struktur und die Relevanz deines Inhalts zu verstehen. Die Überschriften-Hierarchie ist für sie ein unglaublich starkes Signal.

Die `<h1>`-Überschrift teilt Google unmissverständlich mit: „Das ist das Hauptthema dieser Seite.“ Die `<h2>`-Überschriften signalisieren wichtige Unterthemen. Eine saubere, logische Gliederung hilft der Suchmaschine, deinen Inhalt besser zu verstehen, zu indizieren und ihn bei relevanten Suchanfragen höher zu platzieren. Wenn du die semantische Struktur ignorierst, machst du es den Suchmaschinen unnötig schwer, den Wert deines Inhalts zu erkennen.

**3. Wartbarkeit und Styling**

Auch für dich als Entwickler hat eine saubere semantische Struktur enorme Vorteile. Stell dir vor, du möchtest das Aussehen aller Hauptabschnitts-Überschriften auf deiner gesamten Webseite ändern. Wenn du konsequent `<h2>` dafür verwendet hast, brauchst du nur eine einzige CSS-Regel:

```css
h2 {
  font-family: 'Merriweather', serif;
  color: #333;
  border-bottom: 2px solid #eee;
}
```

Wenn du stattdessen eine Mischung aus `<p>`-Tags mit Klassen wie `.gross-und-fett` und `<h4>`-Tags nur aus optischen Gründen verwendet hast, wird dein CSS-Code schnell unübersichtlich und schwer zu pflegen. Semantische HTML-Elemente sind die perfekten Haken, an denen du deine CSS-Stile aufhängen kannst – sauber, logisch und zukunftssicher.

#### Der häufigste Fehler: Styling mit HTML

Der mit Abstand häufigste Fehler von Anfängern ist, HTML-Elemente basierend auf ihrem Standard-Aussehen im Browser auszuwählen. Man braucht einen großen Text, also nimmt man eine `<h1>`. Man braucht einen etwas kleineren, fetten Text, also greift man zu einer `<h3>`.

Dieser Ansatz ist grundlegend falsch. Vergiss für einen Moment, wie die Elemente aussehen. Frage dich stattdessen: **Was ist die Bedeutung dieses Inhalts?** Ist es die Überschrift für die gesamte Seite? Dann ist es eine `<h1>`. Ist es die Überschrift für einen Hauptabschnitt? Dann ist es eine `<h2>`. Ist es einfach nur ein normaler Text, der hervorgehoben werden soll? Dann ist es vielleicht ein `<p>`-Tag in Kombination mit einem `<strong>`-Tag, aber niemals eine Überschrift.

Denke immer in Strukturen, nicht in Stilen. Die Struktur ist die Domäne von HTML. Der Stil ist die Domäne von CSS. Wenn du diese beiden Konzepte von Anfang an sauber trennst, legst du das Fundament für qualitativ hochwertigen, professionellen und nachhaltigen Code. Deine Überschriften-Hierarchie ist der erste und wichtigste Schritt auf diesem Weg. Sie ist die verborgene Ordnung, die deiner Webseite Sinn und Verstand verleiht.
