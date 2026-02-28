# Blockquotes für lange Zitate

### Das `<blockquote>`-Element für lange Zitate

Wenn du in deinen Texten auf andere Werke, Artikel oder Aussagen verweisen möchtest, die länger als ein kurzer Satz sind, stößt du schnell an die Grenzen des `<q>`-Elements. Für ganze Absätze oder längere Textpassagen, die du aus einer anderen Quelle zitierst, hat HTML ein spezielles, semantisch überaus wichtiges Element vorgesehen: das `<blockquote>`-Element.

#### Semantik vor Aussehen: Der wahre Zweck von `<blockquote>`

Stell dir vor, du schreibst einen Blogartikel über Webdesign und möchtest einen inspirierenden Absatz aus einem bekannten Buch zitieren. Deine erste Intuition könnte sein, den Text einfach einzurücken, um ihn visuell vom Rest deines Inhalts abzuheben. Viele Anfänger greifen hierfür fälschlicherweise zum `<blockquote>`-Element, weil Browser es standardmäßig mit einem linken und rechten Einzug versehen.

Das ist jedoch ein grundlegendes Missverständnis seiner Funktion. `<blockquote>` ist kein Werkzeug zur visuellen Gestaltung. Es ist ein semantisches Element, das dem Browser, Suchmaschinen und assistiven Technologien eine klare Botschaft sendet: „Der Inhalt, der hier umschlossen ist, stammt nicht von mir, dem Autor dieser Seite, sondern ist ein Zitat aus einer anderen Quelle.“

Die visuelle Einrückung ist lediglich eine Konvention der Browser-Standardstile. Du könntest diese Darstellung mit CSS komplett verändern – zum Beispiel könntest du den Einzug entfernen und stattdessen eine vertikale Linie links neben dem Zitat platzieren oder den Hintergrund leicht einfärben. Die semantische Bedeutung des Zitats bleibt davon unberührt. Der Missbrauch von `<blockquote>` nur für Einrückungen ist daher genauso falsch wie die Verwendung einer Überschrift (`<h1>` bis `<h6>`), nur um Text größer darzustellen.

Ein einfaches Beispiel für die korrekte Anwendung sieht so aus:

```html
<p>In seinem wegweisenden Buch über die Benutzerfreundlichkeit im Web betont Steve Krug einen zentralen Punkt immer wieder:</p>

<blockquote>
  <p>Dein Ziel sollte es sein, dass jede Seite selbsterklärend ist oder zumindest selbsterläuternd. Wenn der Nutzer auf einer Seite landet, sollte er in der Lage sein, mit einem Blick zu erkennen – oder zumindest schnell herauszufinden –, worum es auf der Seite geht und warum er hier sein sollte.</p>
</blockquote>

<p>Dieser Gedanke ist heute relevanter denn je.</p>
```

Wie du siehst, umschließt `<blockquote>` den gesamten zitierten Absatz. Da der zitierte Text selbst ein Absatz ist, befindet er sich innerhalb des `<blockquote>`-Elements wiederum in einem `<p>`-Tag. Das ist gängige Praxis und sorgt für eine saubere, strukturierte Gliederung deines Dokuments. Ein Blockquote kann mehrere Absätze, Listen oder sogar andere Block-Elemente enthalten.

#### Die Quelle angeben: Der `cite`-Attribut

Ein Zitat ohne Quellenangabe ist oft nur halb so viel wert. HTML bietet eine maschinenlesbare Möglichkeit, die Quelle eines Blockquotes direkt mit dem Element zu verknüpfen: das `cite`-Attribut. In dieses Attribut fügst du eine URL ein, die direkt zum zitierten Dokument oder der Quelle führt.

Wichtig zu verstehen ist, dass der Inhalt des `cite`-Attributs für den menschlichen Besucher auf der Webseite standardmäßig **nicht sichtbar** ist. Er dient als Metainformation für Browser, Suchmaschinen oder andere Tools, die deine Seite verarbeiten.

Erweitern wir unser vorheriges Beispiel um das `cite`-Attribut:

```html
<blockquote cite="https://www.example.com/quelle-des-zitats.html">
  <p>Dein Ziel sollte es sein, dass jede Seite selbsterklärend ist oder zumindest selbsterläuternd. Wenn der Nutzer auf einer Seite landet, sollte er in der Lage sein, mit einem Blick zu erkennen – oder zumindest schnell herauszufinden –, worum es auf der Seite geht und warum er hier sein sollte.</p>
</blockquote>
```

Diese Information ist nun fest mit dem Zitat verknüpft, auch wenn sie nicht direkt angezeigt wird.

#### Sichtbare Quellenangaben mit `<cite>` und `<footer>`

Da das `cite`-Attribut für deine Leser unsichtbar ist, benötigst du eine zusätzliche, sichtbare Quellenangabe. Hierfür gibt es eine etablierte und semantisch korrekte Vorgehensweise. Oft wird die Quellenangabe direkt unterhalb des Zitattextes platziert.

Eine elegante Methode ist die Verwendung des `<footer>`-Elements innerhalb des `<blockquote>`. Das `<footer>`-Element ist nicht nur für den Fußbereich einer ganzen Seite gedacht, sondern kann auch den Abschluss eines in sich geschlossenen Inhaltsbereichs – wie eben eines Blockquotes – markieren.

Innerhalb dieses Footers kannst du dann den Namen des Autors oder den Titel des Werks angeben. Für den Titel eines Werks (Buch, Artikel, Film etc.) solltest du das `<cite>`-Element verwenden, das wir bereits im Kontext von kurzen Zitaten kennengelernt haben.

Eine vollständige, semantisch saubere Umsetzung sieht so aus:

```html
<blockquote cite="https://www.sensible.com/dont-make-me-think/">
  <p>Dein Ziel sollte es sein, dass jede Seite selbsterklärend ist oder zumindest selbsterläuternd. Wenn der Nutzer auf einer Seite landet, sollte er in der Lage sein, mit einem Blick zu erkennen – oder zumindest schnell herauszufinden –, worum es auf der Seite geht und warum er hier sein sollte.</p>
  <footer>— Steve Krug, in <cite>Don't Make Me Think</cite></footer>
</blockquote>
```

In diesem Beispiel haben wir alles vereint:
1.  Das `<blockquote>`-Element kennzeichnet den Text als langes Zitat.
2.  Das `cite`-Attribut liefert die maschinenlesbare URL der Quelle.
3.  Das `<footer>`-Element gruppiert die sichtbare Quellenangabe.
4.  Der Name des Autors wird als normaler Text und der Titel des Buches mit dem `<cite>`-Element semantisch korrekt ausgezeichnet.

#### Gestaltung von Blockquotes mit CSS

Jetzt, wo die semantische Struktur steht, können wir uns der visuellen Gestaltung zuwenden. Wie bereits erwähnt, bist du nicht an die Standarddarstellung des Browsers gebunden. Mit CSS hast du die volle Kontrolle über das Aussehen deines Zitats.

Ein beliebter und stilvoller Ansatz ist es, die standardmäßige Einrückung zu entfernen und stattdessen eine dekorative linke Leiste und vielleicht ein anderes Schriftbild zu verwenden.

Hier ist ein Beispiel, wie du das umsetzen könntest:

**HTML:**
```html
<blockquote class="styled-quote" cite="https://www.sensible.com/dont-make-me-think/">
  <p>Dein Ziel sollte es sein, dass jede Seite selbsterklärend ist oder zumindest selbsterläuternd. Wenn der Nutzer auf einer Seite landet, sollte er in der Lage sein, mit einem Blick zu erkennen – oder zumindest schnell herauszufinden –, worum es auf der Seite geht und warum er hier sein sollte.</p>
  <footer>— Steve Krug, in <cite>Don't Make Me Think</cite></footer>
</blockquote>
```

**CSS:**
```css
.styled-quote {
  /* Standard-Einrückung des Browsers entfernen */
  margin: 1.5em 0;
  padding: 1em 1.5em;
  
  /* Eigene Gestaltung hinzufügen */
  border-left: 5px solid #007bff; /* Eine markante linke Leiste */
  background-color: #f8f9fa; /* Ein dezenter Hintergrund */
  font-style: italic; /* Text kursiv setzen */
  color: #333;
}

.styled-quote p {
  margin-bottom: 1em; /* Abstand zwischen Zitattext und Quelle */
}

/* Den Footer innerhalb des Zitats gestalten */
.styled-quote footer {
  text-align: right;
  font-style: normal; /* Den Stil für den Footer zurücksetzen */
  font-size: 0.9em;
  color: #555;
}

/* Das <cite>-Element innerhalb des Footers hervorheben */
.styled-quote footer cite {
  font-weight: bold;
}
```

Mit diesem CSS-Code wird das Zitat nicht mehr nur eingerückt, sondern als ein klar abgegrenzter, stilvoller Block präsentiert. Dies zeigt eindrucksvoll die Trennung von Struktur (HTML) und Präsentation (CSS). Du hast die semantische Bedeutung beibehalten und gleichzeitig eine ansprechende visuelle Darstellung geschaffen, die zu deinem Seitendesign passt.

#### Barrierefreiheit und `<blockquote>`

Die korrekte Verwendung von `<blockquote>` hat auch positive Auswirkungen auf die Barrierefreiheit (Accessibility). Screenreader, die von Menschen mit Sehbehinderungen genutzt werden, erkennen das `<blockquote>`-Element und können dem Nutzer signalisieren, dass nun ein Zitat beginnt und endet. Dies gibt dem Hörer den notwendigen Kontext, um zu verstehen, dass dieser Textabschnitt eine andere Stimme oder Quelle repräsentiert. Der Missbrauch für rein visuelle Effekte würde diese Nutzer verwirren, da sie eine Zitatankündigung ohne tatsächliches Zitat hören würden.

Durch die Verwendung von `<blockquote>` für seine eigentliche Bestimmung trägst du also dazu bei, dass deine Inhalte für ein breiteres Publikum zugänglich und verständlich sind.
