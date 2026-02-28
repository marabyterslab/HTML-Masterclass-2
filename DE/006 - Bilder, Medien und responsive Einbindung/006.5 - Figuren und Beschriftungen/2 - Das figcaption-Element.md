# Das figcaption-Element

### Das figcaption-Element: Mehr als nur eine Bildunterschrift

Wenn du eine Abbildung, ein Diagramm oder ein Foto in deinen Text einfügst, möchtest du oft eine Beschreibung hinzufügen. Diese Beschreibung gibt Kontext, nennt die Quelle oder erklärt, was zu sehen ist. Viele Jahre lang behalfen sich Entwickler mit Notlösungen, wie einem einfachen Absatz-Element (`<p>`) direkt unter dem Bild. Das funktioniert zwar visuell, aber es fehlt eine entscheidende Eigenschaft: eine semantische, also bedeutungsvolle, Verbindung zwischen dem Bild und seinem beschreibenden Text. Für eine Maschine, wie eine Suchmaschine oder einen Screenreader, sind Bild und Text zwei voneinander getrennte Elemente.

Genau hier kommt das `figure`-Element ins Spiel, und untrennbar damit verbunden ist sein treuer Begleiter: das `<figcaption>`-Element.

#### Die unzertrennliche Einheit: `<figure>` und `<figcaption>`

Um das `<figcaption>`-Element zu verstehen, musst du zuerst das Konzept der „Figur“ in HTML verinnerlichen. Eine Figur, umschlossen vom `<figure>`-Tag, ist eine in sich geschlossene Inhaltseinheit. Stell sie dir wie einen Exponat in einem Museum vor, das für sich allein stehen kann, aber im Kontext der Ausstellung eine tiefere Bedeutung erhält. Eine solche Figur wird oft im Haupttext referenziert (z. B. „siehe Abbildung 1“), könnte aber theoretisch auch an eine andere Stelle im Dokument oder sogar in einen Anhang verschoben werden, ohne den Lesefluss des Haupttextes zu zerstören.

Der Inhalt einer Figur kann vielfältig sein:
*   Ein oder mehrere Bilder (`<img>`)
*   Ein Code-Beispiel (`<pre><code>...</code></pre>`)
*   Ein Zitat (`<blockquote>`)
*   Ein Video (`<video>`) oder eine Audiodatei (`<audio>`)
*   Eine Tabelle (`<table>`)
*   Ein Diagramm (oft als `<img>` oder `<svg>`)

Und nun zum Kern der Sache: Das `<figcaption>`-Element dient dazu, dieser Figur eine Beschriftung zu geben. Es ist das kleine Schild neben dem Exponat, das alles erklärt. `<figcaption>` steht für „Figure Caption“ (Figurenbeschriftung) und darf ausschließlich innerhalb eines `<figure>`-Elements verwendet werden.

Der klassische Anwendungsfall ist ein Bild mit einer Unterschrift:

```html
<figure>
  <img src="bilder/eibsee-bayern.jpg" alt="Ein klarer Bergsee bei Sonnenaufgang, umgeben von Nadelwäldern und den Gipfeln der Alpen.">
  <figcaption>Der Eibsee in den bayerischen Alpen, kurz nach Sonnenaufgang.</figcaption>
</figure>
```

In diesem Beispiel bilden das Bild und die Beschriftung eine unmissverständliche Einheit. Ein Screenreader für blinde oder sehbehinderte Nutzer kann nun verkünden: „Figur: Der Eibsee in den bayerischen Alpen, kurz nach Sonnenaufgang.“ Anschließend liest er den Alternativtext des Bildes vor. Die semantische Verbindung ist hergestellt und schafft echten Mehrwert für die Barrierefreiheit.

#### Positionierung der Beschriftung

Die HTML-Spezifikation ist hierbei recht flexibel. Du kannst das `<figcaption>`-Element entweder als **erstes** oder als **letztes** Kindelement innerhalb des `<figure>`-Tags platzieren. Pro `<figure>`-Element ist nur ein einziges `<figcaption>` erlaubt.

**Beschriftung nach dem Inhalt (der gängige Fall):**

Dies ist die intuitivste und am häufigsten verwendete Variante, die einer klassischen Bildunterschrift entspricht.

```html
<figure>
  <img src="bilder/apollo-11-fussabdruck.jpg" alt="Ein einzelner Stiefelabdruck im feinen, grauen Mondstaub.">
  <figcaption>Abbildung 1: Einer der ersten menschlichen Fußabdrücke auf dem Mond, hinterlassen während der Apollo-11-Mission im Jahr 1969.</figcaption>
</figure>
```

**Beschriftung vor dem Inhalt:**

Manchmal ergibt es Sinn, die Beschriftung als eine Art Überschrift für die Figur zu verwenden. Das ist besonders bei Code-Beispielen oder Tabellen üblich.

```html
<figure>
  <figcaption>Beispiel 6.1: Eine einfache JavaScript-Funktion zur Addition zweier Zahlen.</figcaption>
  <pre><code>function addiere(a, b) {
  // Gibt die Summe der beiden Parameter zurück
  return a + b;
}</code></pre>
</figure>
```

Hier fungiert die Beschriftung als Titel, der dem Betrachter sofort verrät, worum es in dem folgenden Codeblock geht.

#### Mehr als nur Bilder: Die Vielseitigkeit von `<figcaption>`

Die wahre Stärke dieses Elements zeigt sich, wenn du es für andere Inhaltstypen als nur einzelne Bilder einsetzt.

**Mehrere Bilder in einer Figur:**

Du kannst mehrere zusammengehörige Bilder gruppieren und ihnen eine gemeinsame Beschriftung geben. Das ist ideal für Vergleiche, Galerien oder schrittweise Anleitungen.

```html
<figure>
  <img src="bilder/vorher.jpg" alt="Ein unaufgeräumtes Zimmer mit Kleidung auf dem Boden.">
  <img src="bilder/nachher.jpg" alt="Dasselbe Zimmer, aber jetzt sauber und ordentlich.">
  <figcaption>Vorher-Nachher-Vergleich: Die Wirkung von 15 Minuten Aufräumen.</figcaption>
</figure>
```

**Zitate mit Quellenangabe:**

Auch ein Zitat kann eine Figur sein. Das `<figcaption>`-Element eignet sich perfekt, um den Urheber des Zitats zu nennen.

```html
<figure>
  <blockquote>
    <p>Der Weg ist das Ziel.</p>
  </blockquote>
  <figcaption>— Konfuzius</figcaption>
</figure>
```

**Videos und andere Medien:**

Eingebettete Medien profitieren ebenfalls von einer klaren Beschriftung, die Kontext liefert oder den Inhalt kurz beschreibt.

```html
<figure>
  <video controls src="videos/start-rakete.mp4">
    Dein Browser unterstützt das Video-Tag nicht.
  </video>
  <figcaption>Videoclip: Start der Saturn-V-Rakete während der Apollo-Missionen.</figcaption>
</figure>
```

#### Der semantische Unterschied: `<figcaption>` vs. `alt`-Attribut

Ein häufiges Missverständnis betrifft den Unterschied zwischen dem `alt`-Attribut eines `<img>`-Tags und einer `<figcaption>`. Beide beschreiben ein Bild, aber sie tun es mit unterschiedlichen Zielen:

*   **`alt`-Attribut (Alternativtext):** Beschreibt, **was das Bild darstellt**. Es ist ein direkter Ersatz für das Bild, falls es nicht geladen werden kann oder von einem Screenreader vorgelesen wird. Der Text sollte kurz und prägnant sein. Beispiel: „Ein roter Sportwagen fährt auf einer Küstenstraße.“
*   **`<figcaption>`-Element (Beschriftung):** Stellt das Bild in einen **größeren Kontext**. Es erklärt die Bedeutung des Bildes für den umgebenden Artikel. Beispiel: „Der Ferrari F8 Tributo auf dem Pacific Coast Highway, ein Paradebeispiel für italienisches Automobildesign.“

Beide sind wichtig und ergänzen sich. Der `alt`-Text sorgt für die grundlegende Zugänglichkeit des Bildinhalts, während die `<figcaption>` die Interpretation und Einordnung im Textkontext liefert.

#### Gestaltung mit CSS

Wie die meisten HTML-Elemente sind auch `<figure>` und `<figcaption>` vollständig mit CSS gestaltbar. Du bist nicht an eine bestimmte Darstellung gebunden. Du kannst Ränder hinzufügen, die Typografie anpassen oder die Positionierung verändern.

Ein einfaches Styling könnte so aussehen:

```css
figure {
  margin: 2em 1em; /* Außenabstand oben/unten und seitlich */
  padding: 1em; /* Innenabstand */
  border: 1px solid #e0e0e0;
  background-color: #f9f9f9;
  max-width: 100%; /* Sorgt für responsives Verhalten */
}

figure img {
  max-width: 100%; /* Bilder skalieren mit der Figur */
  height: auto;
  display: block; /* Verhindert unerwünschten Leerraum unter dem Bild */
}

figcaption {
  margin-top: 1em; /* Abstand zum Inhalt der Figur */
  font-size: 0.9em;
  font-style: italic;
  color: #333;
  text-align: center;
}
```

Mit diesem CSS-Code erhält jede Figur einen dezenten Rahmen und einen leichten Hintergrund, was sie visuell vom Fließtext abhebt. Die Beschriftung wird zentriert, kursiv und in einer etwas kleineren Schriftgröße dargestellt.

Indem du `<figure>` und `<figcaption>` korrekt einsetzt, schreibst du nicht nur sauberen und logischen HTML-Code. Du verbesserst die Struktur deiner Dokumente, machst deine Inhalte für Suchmaschinen verständlicher und schaffst eine zugänglichere und reichhaltigere Erfahrung für alle Nutzer, insbesondere für jene, die auf assistierende Technologien angewiesen sind. Es ist ein kleines, aber mächtiges Werkzeug in deinem HTML-Repertoire.
