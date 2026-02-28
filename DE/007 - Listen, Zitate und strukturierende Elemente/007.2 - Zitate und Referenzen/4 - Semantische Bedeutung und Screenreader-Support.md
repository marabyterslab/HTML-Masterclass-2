# Semantische Bedeutung und Screenreader-Support

### Semantische Bedeutung und Screenreader-Support: Warum das richtige Tag den Unterschied macht

Wenn du eine Webseite gestaltest, denkst du wahrscheinlich zuerst an das Visuelle: Farben, Schriftarten, Layouts. Du nutzt CSS, um einem Text kursiv zu machen, ihm einen linken Rand zu geben und ihn vielleicht in einem eleganten Grau darzustellen, damit er wie ein Zitat aussieht. Für sehende Benutzer ist die Absicht klar. Aber was passiert, wenn jemand deine Seite nicht sehen kann?

Hier kommt die semantische Bedeutung von HTML ins Spiel, und sie ist untrennbar mit der Barrierefreiheit, insbesondere mit der Unterstützung durch Screenreader, verbunden. Ein Screenreader ist eine Software, die den Bildschirminhalt für Menschen mit Sehbehinderungen in Sprache oder Brailleschrift umwandelt. Diese Software sieht nicht deine schönen CSS-Stile. Sie liest die zugrunde liegende HTML-Struktur, den sogenannten Document Object Model (DOM), und interpretiert ihn. Genauer gesagt, verlässt sie sich auf den sogenannten **Accessibility Tree** (Baum der Barrierefreiheit), eine abgeleitete Version des DOM, die speziell für assistive Technologien aufbereitet ist.

Wenn du also nur visuelle Hinweise verwendest, um Bedeutung zu vermitteln, gehen diese Informationen für einen Screenreader-Nutzer komplett verloren. Deine Webseite wird zu einer Aneinanderreihung von Textabschnitten ohne Kontext und ohne Struktur.

#### Das Problem: Ein Zitat, das keines ist

Stell dir vor, du möchtest ein inspirierendes Zitat von Albert Einstein auf deiner Seite einfügen. Dein erster Impuls könnte sein, einfach ein `<div>` zu verwenden und es mit CSS zu gestalten.

```html
<div class="zitat">
  <p>Phantasie ist wichtiger als Wissen, denn Wissen ist begrenzt.</p>
  <p>- Albert Einstein</p>
</div>
```

```css
.zitat {
  font-style: italic;
  border-left: 4px solid #ccc;
  padding-left: 16px;
  margin: 20px 0;
  color: #555;
}
```

Visuell erreicht dies das Ziel. Du siehst einen eingerückten, kursiven Text, der klar als Zitat erkennbar ist.

Ein Screenreader sieht jedoch etwas ganz anderes. Er sieht einfach ein `<div>`-Element, das semantisch keinerlei Bedeutung hat – es ist eine generische Box. Danach liest er zwei separate Absätze (`<p>`). Der Nutzer hört also:

> "Phantasie ist wichtiger als Wissen, denn Wissen ist begrenzt."
> "Minus Albert Einstein."

Der gesamte Kontext – die Tatsache, dass es sich um ein Zitat handelt, das von allem anderen auf der Seite abgegrenzt ist – geht verloren. Die visuelle Gestaltung ist eine Barriere, keine Hilfe.

#### Die Lösung: Semantik, die spricht

HTML bietet uns genau für diesen Zweck die richtigen Werkzeuge. Anstatt eines nichtssagenden `<div>` verwenden wir das `<blockquote>`-Element. Sein Name sagt bereits alles aus: Es ist für einen Block von zitiertem Inhalt.

Lass uns das vorherige Beispiel korrekt umsetzen:

```html
<blockquote>
  <p>Phantasie ist wichtiger als Wissen, denn Wissen ist begrenzt.</p>
</blockquote>
<p>- Albert Einstein</p>
```

Was passiert nun, wenn ein Screenreader auf diesen Code trifft? Die Software erkennt das `<blockquote>`-Tag und versteht seine semantische Rolle. Je nach Screenreader und Benutzereinstellungen könnte die Ausgabe wie folgt klingen:

> **"Blockzitat Anfang."** "Phantasie ist wichtiger als Wissen, denn Wissen ist begrenzt." **"Blockzitat Ende."**
> "Minus Albert Einstein."

Plötzlich ist der Kontext da! Der Nutzer weiß sofort, dass der folgende Text nicht vom Autor der Seite stammt, sondern eine zitierte Passage ist. Du hast mit einer einfachen Änderung des HTML-Tags eine entscheidende Information vermittelt, ohne auch nur eine Zeile CSS zu ändern. Die Standardformatierung von `<blockquote>` (meist ein Einzug) kannst du natürlich weiterhin nach Belieben anpassen.

Um das Ganze noch besser zu machen, hat das `<blockquote>`-Element ein `cite`-Attribut. In diesem Attribut kannst du eine URL angeben, die zur Quelle des Zitats führt.

```html
<blockquote cite="https://www.einstein-website.de/zitate/wissenschaft">
  <p>Phantasie ist wichtiger als Wissen, denn Wissen ist begrenzt.</p>
</blockquote>
```

Wichtig zu wissen ist, dass Screenreader das `cite`-Attribut in der Regel nicht von sich aus vorlesen. Es dient jedoch als maschinenlesbare Metainformation, die für Suchmaschinen, Browser-Plugins oder andere Werkzeuge von großem Wert ist. Es ist eine bewährte Praxis, es hinzuzufügen, um die Herkunft des Zitats sauber zu dokumentieren.

#### Kurze Zitate im Fließtext: `<q>`

Nicht jedes Zitat ist ein ganzer Block. Manchmal möchtest du nur ein paar Worte innerhalb eines Satzes zitieren. Auch hierfür gibt es eine semantische Lösung: das `<q>`-Tag (für "quote").

Betrachte diesen Satz ohne semantisches Markup:

```html
<p>Wie der Entwickler sagte, "Code ist Poesie".</p>
```

Ein Screenreader liest dies einfach als einen Satz vor. Die Anführungszeichen werden zwar vorgelesen, aber die besondere Kennzeichnung als Zitat fehlt.

Mit dem `<q>`-Tag wird es besser:

```html
<p>Wie der Entwickler sagte, <q>Code ist Poesie</q>.</p>
```

Der Browser fügt hier automatisch die korrekten, sprachspezifischen Anführungszeichen hinzu (z. B. „“ im Deutschen oder “” im Englischen). Für einen Screenreader-Nutzer ist der Unterschied subtil, aber wichtig. Das `<q>`-Tag kennzeichnet den eingeschlossenen Text explizit als Zitat. Einige Screenreader ändern möglicherweise die Tonlage der Stimme oder kündigen die Anführungszeichen deutlicher an, was dem Hörer hilft, die Struktur des Satzes besser zu verstehen.

#### Die Quelle benennen: `<cite>`

Jetzt, da wir wissen, wie wir Zitate auszeichnen, müssen wir noch die Quelle korrekt referenzieren. Hierfür gibt es das `<cite>`-Element. Es ist eines der am häufigsten missverstandenen Tags in HTML.

**`<cite>` wird verwendet, um den Titel eines Werkes zu kennzeichnen.**

Das kann ein Buch, ein Film, ein Song, ein Gedicht, ein Theaterstück, ein wissenschaftlicher Aufsatz oder eine Webseite sein. Es wird **nicht** für den Namen einer Person verwendet.

**Falsch:**

```html
<p>- <cite>Albert Einstein</cite></p>
```

**Richtig:**

```html
<footer>
  <p>— Albert Einstein, aus einem Interview im <cite>Saturday Evening Post</cite> (1929)</p>
</footer>
```

In diesem korrekten Beispiel wird der Name des Autors als normaler Text belassen, während der Titel der Zeitschrift, aus der das Zitat stammt, mit `<cite>` ausgezeichnet wird. Ein Screenreader erkennt dies und kann dem Nutzer mitteilen, dass es sich um den Titel eines Werkes handelt. Dies hilft, zwischen dem Urheber (einer Person) und der Quelle (einem Werk) zu unterscheiden – eine Nuance, die für das Verständnis entscheidend sein kann.

Eine sehr elegante Methode, ein Zitat und seine Quelle zu gruppieren, ist die Verwendung der Elemente `<figure>` und `<figcaption>`:

```html
<figure>
  <blockquote cite="https://www.einstein-website.de/zitate/wissenschaft">
    <p>Phantasie ist wichtiger als Wissen, denn Wissen ist begrenzt.</p>
  </blockquote>
  <figcaption>— Albert Einstein, <cite>Saturday Evening Post</cite></figcaption>
</figure>
```

Diese Struktur ist semantisch brillant. `<figure>` gruppiert den Inhalt als eine in sich geschlossene Einheit. `<blockquote>` kennzeichnet das Zitat. Und `<figcaption>` stellt eine Bild- oder Inhaltsunterschrift bereit, die direkt mit der Figur verbunden ist. Für einen Screenreader ist diese Verbindung glasklar. Er versteht, dass die `figcaption` die Beschreibung oder Quelle für das `blockquote` ist. Das ist weit mehr als nur Text – das ist eine strukturierte, logische Beziehung.

#### Mehr als nur Zitate

Das Prinzip der semantischen Bedeutung geht weit über Zitate hinaus. Jedes Mal, wenn du ein HTML-Element wählst, triffst du eine Entscheidung darüber, wie deine Inhalte von Maschinen und assistiven Technologien interpretiert werden.

-   Verwendest du `<address>`, um Kontaktinformationen für den Autor des Dokuments bereitzustellen? Ein Screenreader-Nutzer kann gezielt zu diesen Informationen springen.
-   Zeichnest du ein Datum mit `<time datetime="2023-10-27">27. Oktober 2023</time>` aus? Ein Screenreader kann das Datum eindeutig und im vom Nutzer bevorzugten Format vorlesen, während die maschinenlesbare Version für Kalender-Apps oder Suchmaschinen verfügbar ist.
-   Strukturierst du deine Navigation mit `<nav>`, deine Kopfzeile mit `<header>` und deinen Hauptinhalt mit `<main>`? Damit schaffst du sogenannte "Landmarks", die es Nutzern von assistiven Technologien ermöglichen, mit einem einzigen Tastendruck von einem Hauptbereich der Seite zum nächsten zu springen, anstatt sich durch Dutzende von Links und Textabschnitten kämpfen zu müssen.

Dein HTML-Code ist nicht nur eine Anweisung für den Browser, wie er etwas darstellen soll. Er ist die universelle Sprache, die die Bedeutung und Struktur deiner Inhalte beschreibt. Indem du die semantisch korrekten Elemente für Zitate, Referenzen und alle anderen Inhaltsarten verwendest, baust du nicht nur eine Webseite. Du baust eine robuste, zugängliche und verständliche Informationsarchitektur, die für Menschen und Maschinen gleichermaßen funktioniert. Du sorgst dafür, dass deine Botschaft nicht nur gesehen, sondern auch wirklich verstanden wird – von jedem.
