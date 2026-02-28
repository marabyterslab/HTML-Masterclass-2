# Quellenangabe mit cite

### Quellenangabe mit `<cite>`: Dem Original die Ehre erweisen

Wenn du im Internet auf Inhalte stößt, die du zitieren oder auf die du dich beziehen möchtest, ist es nicht nur guter Stil, die Quelle anzugeben – es ist oft auch rechtlich und moralisch geboten. Im akademischen oder journalistischen Schreiben sind Zitate und Quellenverweise eine Selbstverständlichkeit. Im Web ist es genauso wichtig, denn es schafft Vertrauen, gibt deinen Aussagen Gewicht und zollt den ursprünglichen Schöpfern den verdienten Respekt.

HTML bietet uns für genau diesen Zweck ein spezielles, semantisches Element: das `<cite>`-Tag. Doch seine Verwendung ist präziser definiert, als viele zunächst annehmen. Lass uns gemeinsam erkunden, wie du es korrekt einsetzt, um deine Inhalte professionell und semantisch sauber auszuzeichnen.

#### Was genau ist ein `<cite>`-Element?

Das `<cite>`-Element wird verwendet, um den Titel eines kreativen Werks zu markieren. Das ist der Kern seiner Bedeutung. Es geht nicht darum, eine Person zu zitieren oder einen beliebigen Verweis zu kennzeichnen, sondern ausschließlich um den Titel des Werks, aus dem ein Zitat stammt oder auf das du dich beziehst.

Was zählt als "kreatives Werk"? Die Definition ist recht breit und umfasst unter anderem:

*   **Bücher:** *Der Herr der Ringe*
*   **Filme:** *Inception*
*   **Songs oder Musikalben:** *Bohemian Rhapsody*
*   **Theaterstücke:** *Hamlet*
*   **Gedichte:** *Der Erlkönig*
*   **Gemälde oder Skulpturen:** *Die Mona Lisa*
*   **Fernsehserien:** *Game of Thrones*
*   **Wissenschaftliche Arbeiten oder Aufsätze:** *Zur Elektrodynamik bewegter Körper*
*   **Websites oder Blog-Titel:** *Smashing Magazine*
*   **Computerspiele:** *The Legend of Zelda: Breath of the Wild*

Die entscheidende Regel, die du dir merken solltest, lautet: `<cite>` umschließt den **Titel des Werks**, nicht den Namen des Autors oder der Autorin. Dies ist einer der häufigsten Fehler bei der Verwendung dieses Tags.

**Falsch:**
```html
<p><cite>Vincent van Gogh</cite> malte die Sternennacht.</p>
```

**Richtig:**
```html
<p>Vincent van Gogh malte <cite>Die Sternennacht</cite>.</p>
```

Warum ist dieser Unterschied so wichtig? Weil semantisches HTML darauf abzielt, die *Bedeutung* von Inhalten für Maschinen – wie Suchmaschinen oder Screenreader – verständlich zu machen. Eine Maschine versteht, dass `<cite>Die Sternennacht</cite>` der Titel eines Werks ist. `<cite>Vincent van Gogh</cite>` hingegen wäre irreführend, da es eine Person als Werkstitel deklarieren würde.

#### Die Kombination macht's: `<cite>` im Zusammenspiel mit `<blockquote>` und `<q>`

Am häufigsten wirst du das `<cite>`-Element in Verbindung mit einem Zitat finden. Hierfür haben wir bereits die Elemente `<blockquote>` für längere, blockförmige Zitate und `<q>` für kurze, inline-Zitate kennengelernt. Das `<cite>`-Tag ergänzt diese perfekt, indem es die Quelle des Zitats angibt.

Stell dir vor, du möchtest einen berühmten Satz aus George Orwells Roman *1984* zitieren. Eine semantisch korrekte Umsetzung würde so aussehen:

```html
<figure>
  <blockquote>
    <p>Big Brother is watching you.</p>
  </blockquote>
  <figcaption>— George Orwell, <cite>1984</cite></figcaption>
</figure>
```

Schauen wir uns diesen Code genauer an:
1.  **`<figure>`:** Dieses Element wird verwendet, um in sich geschlossene Inhalte wie Diagramme, Bilder, Code-Snippets oder eben auch Zitate zu gruppieren. Es ist hier eine gute Wahl, da das Zitat und seine Quelle eine logische Einheit bilden.
2.  **`<blockquote>`:** Es umschließt das eigentliche Zitat als Block.
3.  **`<figcaption>`:** Dieses Tag liefert eine Bildunterschrift oder eine Beschreibung für den Inhalt der `<figure>`. Es ist der perfekte Ort für die Quellenangabe.
4.  **`<cite>`:** Hier kommt unser Star zum Einsatz. Es umschließt ausschließlich den Titel des Buches, *1984*.

Diese Struktur ist nicht nur semantisch brillant, sondern auch für Screenreader-Nutzer sehr gut verständlich. Der Screenreader kann die Beziehung zwischen dem Zitat und der Quellenangabe klar erkennen.

Für ein kurzes Zitat innerhalb eines Satzes könntest du `<q>` verwenden:

```html
<p>In seinem Roman <cite>Per Anhalter durch die Galaxis</cite> hinterließ uns Douglas Adams den weisen Rat: <q>Don't Panic</q>.</p>
```

Auch hier ist die Regel dieselbe: `<cite>` markiert den Buchtitel, während `<q>` das direkte Zitat umschließt.

#### Das `cite`-Attribut: Der unsichtbare Helfer

Jetzt wird es ein wenig knifflig, aber es ist eine wichtige Unterscheidung: Es gibt nicht nur das **`<cite>`-Element**, sondern auch ein **`cite`-Attribut**. Dieses Attribut kann in den Tags `<blockquote>` und `<q>` verwendet werden, um eine URL anzugeben, die direkt zur Online-Quelle des Zitats führt.

*   Das **`<cite>`-Element** ist für Menschen lesbar. Es zeigt den Titel des Werks im Browser an.
*   Das **`cite`-Attribut** ist für Maschinen lesbar. Es enthält einen Link zur Quelle und ist für den normalen Besucher der Webseite nicht sichtbar.

Eine vollumfängliche, mustergültige Zitation kombiniert beides:

```html
<blockquote cite="https://www.gutenberg.org/files/11/11-h/11-h.htm">
  <p>It is a truth universally acknowledged, that a single man in possession of a good fortune, must be in want of a wife.</p>
</blockquote>
<p>— Jane Austen, <cite>Pride and Prejudice</cite></p>
```

In diesem Beispiel liefert das `cite`-Attribut im `<blockquote>`-Tag den maschinenlesbaren Link zum Online-Text von *Pride and Prejudice*. Der für Menschen lesbare Text darunter verwendet das `<cite>`-Element, um den Buchtitel semantisch korrekt hervorzuheben. Suchmaschinen können diese Information nutzen, um deine Seite besser zu kontextualisieren, und Browser-Plugins könnten sie theoretisch verwenden, um einen direkten Link zur Quelle anzubieten.

#### Darstellung im Browser und Anpassung mit CSS

Standardmäßig rendern die meisten Webbrowser den Inhalt eines `<cite>`-Elements kursiv. Das kennst du vielleicht vom `<i>`- oder `<em>`-Tag. Aber hier liegt ein entscheidender Unterschied, der das Herz von semantischem HTML trifft:

*   `<i>` (Idiomatic Text) ist rein präsentationsbezogen. Es sagt dem Browser: "Stelle diesen Text kursiv dar", ohne eine tiefere Bedeutung zu vermitteln.
*   `<em>` (Emphasis) hat eine semantische Bedeutung: "Betone diesen Text." Die Standarddarstellung ist ebenfalls kursiv, aber die Bedeutung ist eine andere.
*   `<cite>` hat ebenfalls eine semantische Bedeutung: "Dies ist der Titel eines kreativen Werks." Die kursive Darstellung ist nur eine Konvention, ein visueller Standard.

Du solltest dich niemals auf die Standarddarstellung verlassen. Wenn dir das kursive Aussehen nicht gefällt, kannst du es jederzeit mit CSS ändern. Die semantische Bedeutung bleibt erhalten, egal wie der Text aussieht.

Angenommen, du möchtest Werktitel nicht kursiv, sondern in einer etwas dunkleren Schriftfarbe und normaler Schriftart darstellen:

```css
cite {
  font-style: normal; /* Hebt die standardmäßige Kursivschrift auf */
  color: #333333;
  font-weight: 500; /* Etwas dicker als normaler Text */
}
```

Mit dieser CSS-Regel hast du das Aussehen vollständig von der Bedeutung getrennt. Dein HTML-Code bleibt sauber und semantisch, während dein CSS sich um die Präsentation kümmert. Das ist das Prinzip der "Separation of Concerns" (Trennung der Belange) in seiner schönsten Form.

Indem du das `<cite>`-Element bewusst und korrekt einsetzt, machst du mehr, als nur Text zu formatieren. Du strukturierst dein Wissen, gibst Quellen die gebührende Ehre und machst deine Webseite für Menschen und Maschinen gleichermaßen verständlicher und wertvoller. Es ist ein kleines Detail, das den Unterschied zwischen einer einfachen Ansammlung von Text und einem professionell strukturierten, semantischen Dokument ausmacht.
