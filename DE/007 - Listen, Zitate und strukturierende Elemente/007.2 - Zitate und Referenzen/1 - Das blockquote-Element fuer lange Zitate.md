# Das blockquote-Element für lange Zitate

### Lange Zitate semantisch korrekt auszeichnen: Das `<blockquote>`-Element

Wenn du in deinen Webprojekten auf die Worte anderer verweisen möchtest, stehst du vor der Frage, wie du diese Zitate am besten in deinem HTML-Code darstellst. Für kurze, in einen Satz eingebettete Zitate gibt es das `<q>`-Element. Doch was tust du, wenn du einen ganzen Absatz oder sogar mehrere Absätze aus einer anderen Quelle zitieren möchtest? Genau hier kommt das `<blockquote>`-Element ins Spiel. Es ist das semantisch korrekte Werkzeug für längere, als eigenständiger Block dargestellte Zitate.

#### Was ist ein `<blockquote>` und was tut es?

Das `<blockquote>`-Element umschließt Inhalte, die aus einer anderen Quelle entnommen wurden. Es signalisiert dem Browser, Screenreadern und Suchmaschinen: „Dieser Textabschnitt ist nicht mein eigener Inhalt, sondern ein Zitat.“ Rein semantisch ist dies seine Hauptaufgabe.

Visuell rendern die meisten Browser ein `<blockquote>`-Element standardmäßig mit einem linken und rechten Einzug. Dieser visuelle Hinweis hilft dem Leser, das Zitat sofort vom umgebenden Text zu unterscheiden. Doch hier ist eine der wichtigsten Lektionen, die du über dieses Element lernen musst: **Verwende `<blockquote>` niemals nur, um Text einzurücken!** Es ist ein semantisches Element, kein Styling-Werkzeug. Wenn du Text aus rein gestalterischen Gründen einrücken möchtest, solltest du dafür CSS verwenden, zum Beispiel mit der `margin`- oder `padding`-Eigenschaft. Die missbräuchliche Verwendung von `<blockquote>` für Layoutzwecke verwirrt nicht nur Suchmaschinen, sondern schafft vor allem für Nutzer von Screenreadern eine irreführende Erfahrung, da ihnen ein Zitat vorgelesen wird, wo keines ist.

Ein einfaches `<blockquote>` sieht im Code so aus:

```html
<p>In seinem berühmten Vortrag über die Zukunft des Webs betonte er einen wichtigen Punkt:</p>

<blockquote>
  <p>Das Fundament eines zugänglichen und offenen Internets ist sauberes, semantisches HTML. Ohne diese Grundlage werden fortschrittliche Technologien zu unüberwindbaren Barrieren für viele Menschen.</p>
  <p>Wir tragen als Entwickler die Verantwortung, diese Grundlage zu schützen und zu pflegen.</p>
</blockquote>

<p>Diese Aussage unterstreicht die Bedeutung unserer täglichen Arbeit.</p>
```

Wie du siehst, können innerhalb eines `<blockquote>`-Elements andere Block-Level-Elemente wie Absätze (`<p>`) oder sogar Listen platziert werden. Das Zitat wird dadurch klar vom restlichen Inhalt abgegrenzt.

#### Die Quelle des Zitats angeben: Das `cite`-Attribut

Ein Zitat ist nur halb so viel wert ohne seine Quelle. HTML bietet eine spezielle Möglichkeit, die Herkunft eines Zitats maschinenlesbar anzugeben: das `cite`-Attribut. Dieses Attribut wird direkt im öffnenden `<blockquote>`-Tag platziert und sollte eine gültige URL enthalten, die auf das Quelldokument verweist.

```html
<blockquote cite="https://www.beispiel-quelle.de/artikel/zukunft-des-webs">
  <p>Das Fundament eines zugänglichen und offenen Internets ist sauberes, semantisches HTML. Ohne diese Grundlage werden fortschrittliche Technologien zu unüberwindbaren Barrieren für viele Menschen.</p>
</blockquote>
```

Ein wichtiger Punkt zum `cite`-Attribut ist, dass sein Inhalt **nicht** für den Besucher auf der Webseite sichtbar ist. Es dient als Metadatum für Browser, Suchmaschinen oder andere automatisierte Werkzeuge, um die Quelle des Zitats zu verstehen und zu verknüpfen. Es ist eine Information für die Maschine, nicht primär für den Menschen.

#### Wie macht man die Quelle für den Leser sichtbar?

Da das `cite`-Attribut nicht angezeigt wird, benötigen wir eine Methode, um die Quelle auch für unsere menschlichen Leser sichtbar zu machen. Die reine Lehre und beste Praxis empfiehlt hierfür eine Kombination aus den Elementen `<figure>` und `<figcaption>`.

Das `<figure>`-Element wurde für in sich geschlossene Inhalte wie Bilder, Diagramme oder eben auch Zitate geschaffen, auf die im Haupttext Bezug genommen wird. Das `<figcaption>`-Element stellt die dazugehörige Bild- oder Inhaltsunterschrift dar. Diese Kombination ist semantisch perfekt für ein Zitat mit seiner Quellenangabe.

So sieht die empfohlene Struktur aus:

```html
<figure>
  <blockquote cite="https://www.beispiel-quelle.de/artikel/zukunft-des-webs">
    <p>Das Fundament eines zugänglichen und offenen Internets ist sauberes, semantisches HTML. Ohne diese Grundlage werden fortschrittliche Technologien zu unüberwindbaren Barrieren für viele Menschen.</p>
  </blockquote>
  <figcaption>
    — Tim Berners-Lee, <cite>Weaving the Web</cite>
  </figcaption>
</figure>
```

Analysieren wir diese Struktur genauer:
1.  **`<figure>`**: Umschließt das Zitat und seine Beschreibung als eine logische Einheit.
2.  **`<blockquote>`**: Enthält das eigentliche Zitat. Das `cite`-Attribut verweist weiterhin auf die Online-Quelle.
3.  **`<figcaption>`**: Beinhaltet die für den Benutzer sichtbare Quellenangabe. Hier kannst du den Autor, den Titel des Werks und weitere Informationen unterbringen.
4.  **`<cite>`**: Innerhalb der `<figcaption>` haben wir hier das `<cite>`-Element verwendet. Dieses spezielle Element dient dazu, den Titel eines Werks (wie ein Buch, einen Film, einen Artikel oder eine Website) auszuzeichnen. Browser stellen den Inhalt von `<cite>` typischerweise kursiv dar.

Diese Methode ist nicht nur semantisch am saubersten, sondern auch flexibel und gut für die Zugänglichkeit, da die Beziehung zwischen dem Zitat und seiner Beschreibung klar definiert ist.

#### Das Styling von Blockquotes mit CSS

Wie bereits erwähnt, solltest du dich nicht auf das Standard-Styling des Browsers verlassen. Mit CSS hast du die volle Kontrolle über das Erscheinungsbild deiner Zitate. Hier sind einige gängige Techniken, um `<blockquote>`-Elemente ansprechend zu gestalten.

Angenommen, du hast folgenden HTML-Code:

```html
<figure class="quote-box">
  <blockquote>
    <p>Der einzige Weg, großartige Arbeit zu leisten, ist, zu lieben, was man tut.</p>
  </blockquote>
  <figcaption>— Steve Jobs</figcaption>
</figure>
```

Hier ist ein mögliches CSS, um dieses Zitat hervorzuheben:

```css
.quote-box {
  margin: 2em 0; /* Etwas Abstand zum umgebenden Text */
}

.quote-box blockquote {
  margin: 0; /* Standard-Browser-Einzug zurücksetzen */
  padding: 1em 1.5em;
  background-color: #f9f9f9;
  border-left: 5px solid #ccc;
  font-style: italic;
  color: #333;
}

.quote-box blockquote p {
  margin: 0; /* Standard-Absatz-Margin im Zitat entfernen */
}

.quote-box figcaption {
  margin-top: 0.5em;
  text-align: right;
  font-size: 0.9em;
  color: #666;
}
```

Was passiert hier im Detail?
*   Wir setzen den Standard-`margin` des `<blockquote>` zurück, um volle Kontrolle zu haben.
*   Wir verwenden `padding`, um den inneren Abstand zu schaffen, und einen `border-left`, um die klassische vertikale Linie zu erzeugen, die Zitate oft kennzeichnet.
*   Ein leichter Hintergrund und kursiver Text heben das Zitat weiter ab.
*   Die `<figcaption>` wird rechtsbündig ausgerichtet und etwas kleiner und dezenter gestaltet, um sie klar als Quellenangabe zu kennzeichnen.

Eine weitere beliebte Technik ist die Verwendung von Pseudo-Elementen, um große Anführungszeichen hinzuzufügen:

```css
.quote-box blockquote::before {
  content: "“";
  font-size: 4em;
  color: #e0e0e0;
  position: absolute;
  left: 10px;
  top: -20px;
}

.quote-box blockquote {
  position: relative; /* Notwendig, damit die absolute Positionierung von ::before funktioniert */
  padding-left: 50px; /* Platz für das große Anführungszeichen schaffen */
}
```
Diese CSS-Regeln fügen ein großes, stilisiertes Anführungszeichen vor dem Zitat ein, was einen sehr eleganten visuellen Effekt erzeugt. Die Möglichkeiten sind hier nahezu unbegrenzt und hängen ganz von deinem Design ab.

Die korrekte Verwendung des `<blockquote>`-Elements ist ein Zeichen für hochwertiges, professionelles HTML. Es geht weit über das reine Aussehen hinaus und verleiht deinem Inhalt eine klare, maschinenlesbare Struktur. Indem du die Semantik von `<blockquote>`, `cite`, `<figure>` und `<figcaption>` verstehst und anwendest, verbesserst du nicht nur die Ästhetik deiner Seite durch gezieltes CSS, sondern auch ihre Zugänglichkeit und ihre Auffindbarkeit für Suchmaschinen.
