# Thematische Trennung mit hr

# Thematische Trennung mit hr

Innerhalb deiner textlastigen Inhalte wirst du immer wieder an einen Punkt kommen, an dem du einen gedanklichen Schnitt machen möchtest. Du wechselst das Thema, aber nicht so stark, dass eine komplett neue Überschrift oder ein neues Kapitel gerechtfertigt wäre. Stell dir vor, du schreibst eine Kurzgeschichte: Eine Szene endet, eine neue beginnt an einem anderen Ort oder zu einer anderen Zeit. Genau für solche Fälle gibt es in HTML ein spezielles Element: das `<hr>`-Tag.

### Vom Strich zur Bedeutung: Die Evolution des `<hr>`-Elements

Früher, in den Anfängen des Webs mit älteren HTML-Versionen, stand `hr` schlicht für „horizontal rule“, also „horizontale Linie“. Sein Zweck war rein visueller Natur: Es zeichnete eine Linie quer über die Seite, um Inhalte voneinander zu trennen. Entwickler nutzten es, um Blöcke optisch aufzuteilen, ähnlich wie man mit einem Lineal einen Strich auf ein Blatt Papier zieht.

Mit der Einführung von HTML5 hat sich diese Sichtweise grundlegend geändert. Die Philosophie hinter HTML5 ist, dass Markup (also der HTML-Code) die *Bedeutung* (Semantik) des Inhalts beschreiben soll, nicht sein Aussehen. Das Styling, also wie etwas aussieht, ist die alleinige Aufgabe von CSS.

Das `<hr>`-Element wurde deshalb neu definiert. Es steht heute nicht mehr für eine simple Linie, sondern für einen **thematischen Umbruch auf Absatzebene**. Es signalisiert einen Wechsel des Themas innerhalb eines zusammenhängenden Textblocks. Die horizontale Linie, die Browser standardmäßig immer noch anzeigen, ist nur noch eine visuelle Standarddarstellung dieser semantischen Trennung. Du könntest sie mit CSS komplett entfernen oder anders gestalten, ohne die Bedeutung des Elements zu verändern.

Ein `<hr>`-Tag ist ein sogenanntes „leeres“ oder „selbstschließendes“ Element. Es umschließt keinen Inhalt und benötigt daher keinen schließenden Tag. Du schreibst einfach `<hr>`.

### Wann ein `<hr>` genau richtig ist

Die wichtigste Regel lautet: Nutze `<hr>` immer dann, wenn sich das Thema innerhalb eines Abschnitts ändert, aber der übergeordnete Kontext derselbe bleibt. Es ist ein subtiles Werkzeug, das eine Pause oder einen Übergang im Erzählfluss markiert.

Hier sind einige klassische Anwendungsfälle:

**1. Szenenwechsel in einer Erzählung**
Das ist wohl das anschaulichste Beispiel. Du erzählst eine Geschichte, und der Schauplatz oder die Zeit ändert sich.

```html
<article>
  <h2>Das Abenteuer am nebligen Pass</h2>
  <p>Elara zog ihr Schwert und blickte entschlossen auf die Horde Goblins, die sich ihr in den Weg stellte. Der Regen prasselte auf ihre Rüstung, und der Nebel machte es schwer, Freund von Feind zu unterscheiden. "Für das Königreich!", rief sie und stürmte vorwärts.</p>
  <p>Der Kampf war kurz, aber heftig. Als der letzte Goblin fiel, sank sie erschöpft auf die Knie und blickte in den grauen Himmel.</p>

  <hr>

  <p>Zwei Tage später erreichte sie das Dorf im Tal. Die Sonne schien, Kinder lachten auf der Straße, und der Geruch von frisch gebackenem Brot lag in der Luft. Niemand hier ahnte etwas von dem Kampf, der sich nur wenige Meilen entfernt in den Bergen zugetragen hatte.</p>
</article>
```

In diesem Beispiel markiert das `<hr>` den klaren Schnitt zwischen der Kampfszene am Pass und der Ankunft im friedlichen Dorf. Eine neue Überschrift wie `<h2>Ankunft im Dorf` wäre hier zu viel des Guten, da beides zur selben übergeordneten Geschichte gehört.

**2. Trennung von unterschiedlichen Gedankengängen in einem Artikel**
Stell dir vor, du schreibst einen Blogbeitrag über ein Buch. Zuerst fasst du den Inhalt zusammen und im Anschluss daran gibst du deine persönliche Meinung ab.

```html
<article>
  <h1>Rezension: Der Ozean am Ende der Straße</h1>
  <p>Das Buch erzählt die Geschichte eines Mannes, der in seine Heimatstadt zurückkehrt und sich an die seltsamen und magischen Ereignisse seiner Kindheit erinnert. Es verwebt meisterhaft Realität mit Fantasie...</p>

  <hr>

  <p>Persönlich hat mich dieses Buch tief berührt. Die Art und Weise, wie die Themen Verlust und Erinnerung behandelt werden, ist außergewöhnlich. Ich musste es mehrmals aus der Hand legen, nur um über einen einzigen Satz nachzudenken. Eine klare Leseempfehlung von meiner Seite.</p>
</article>
```
Das `<hr>` trennt hier die objektive Inhaltsangabe von der subjektiven Kritik.

### Die Anti-Muster: Wann du `<hr>` nicht verwenden solltest

Genauso wichtig wie zu wissen, wann man ein Element einsetzt, ist es zu wissen, wann man es *nicht* tun sollte. Da die visuelle Linie immer noch so präsent ist, wird `<hr>` oft fälschlicherweise für rein dekorative Zwecke missbraucht.

**Vermeide `<hr>` für rein visuelle Trennungen.**
Wenn du einfach nur eine Linie unter einer Überschrift oder zwischen verschiedenen `<div>`-Boxen haben möchtest, um dein Layout zu gestalten, ist `<hr>` das falsche Werkzeug. Das ist eine Aufgabe für CSS! Nutze stattdessen Eigenschaften wie `border-bottom` oder `border-top`.

**Falsch:** `<hr>` als visueller Trenner unter einer Überschrift.

```html
<!-- FALSCHE VERWENDUNG! -->
<section>
  <h2>Unsere Produkte</h2>
  <hr>
  <p>Hier finden Sie eine Auswahl unserer besten Produkte...</p>
</section>
```

**Richtig:** Eine Linie mit CSS erzeugen.

```html
<section>
  <h2 class="section-title">Unsere Produkte</h2>
  <p>Hier finden Sie eine Auswahl unserer besten Produkte...</p>
</section>
```

Und der dazugehörige CSS-Code:

```css
.section-title {
  padding-bottom: 10px;
  border-bottom: 2px solid #eeeeee;
}
```
Dieser Ansatz ist flexibler, semantisch korrekt und trennt Inhalt von Design, so wie es sein sollte.

**Vermeide `<hr>` zur Trennung von Hauptabschnitten.**
Wenn du deine Seite in große, eigenständige Bereiche wie „Über uns“, „Dienstleistungen“ und „Kontakt“ gliederst, solltest du dafür keine `<hr>`-Elemente verwenden. Dafür gibt es die strukturellen HTML-Elemente wie `<section>` in Kombination mit Überschriften (`<h2>`, `<h3>` etc.). Ein `<hr>` ist zu schwach, um eine solch grobe Gliederung der Seitenstruktur zu kennzeichnen. Es arbeitet auf einer viel feineren, textinternen Ebene.

### Das Styling der thematischen Trennung

Obwohl die primäre Funktion des `<hr>`-Tags semantisch ist, liefert der Browser eine visuelle Darstellung, die du selbstverständlich an dein Design anpassen kannst und solltest. Die Standardlinie ist oft dick, hat einen unschönen 3D-Effekt und passt selten in ein modernes Webdesign.

Glücklicherweise lässt sich das `<hr>`-Element mit CSS leicht umgestalten. Zuerst musst du die Standard-Stile des Browsers entfernen.

```css
hr {
  border: 0; /* Entfernt den Standard-Rahmen */
  height: 1px; /* Gibt dem Element eine definierte Höhe */
  background-color: #ccc; /* Eine einfache, hellgraue Farbe */
  margin: 40px 0; /* Etwas Abstand nach oben und unten */
}
```
Mit dieser Basis kannst du kreativ werden.

**Beispiel 1: Eine dicke, farbige Linie**

```css
hr.accent {
  height: 4px;
  background-color: #e91e63; /* Eine kräftige Akzentfarbe */
  width: 50%; /* Zentriert und nur 50% breit */
  margin-left: auto;
  margin-right: auto;
}
```

**Beispiel 2: Eine Linie mit Farbverlauf**

```css
hr.gradient {
  height: 3px;
  background-image: linear-gradient(to right, transparent, #333, transparent);
}
```
Diese Linie würde in der Mitte dunkel sein und zu den Seiten hin ausblenden.

**Beispiel 3: Eine Trennung mit einem Symbol**
Du kannst das `<hr>`-Element sogar noch weiter abstrahieren und anstelle einer Linie ein Symbol oder ein kleines Bild verwenden.

```css
hr.symbol {
  height: 30px;
  background-color: transparent;
  background-image: url('symbol.svg');
  background-repeat: no-repeat;
  background-position: center;
  border: 0;
}
```

Die Möglichkeiten sind endlos. Wichtig ist nur, dass das Design die semantische Bedeutung – einen thematischen Übergang – visuell unterstützt und nicht davon ablenkt.

### Barrierefreiheit im Blick

Ein letzter, aber entscheidender Punkt ist die Barrierefreiheit. Was passiert, wenn ein Nutzer mit einem Screenreader auf deine Seite kommt? Ein Screenreader ist eine Software, die den Inhalt einer Webseite vorliest.

Da das `<hr>`-Element eine semantische Bedeutung hat, wird es von den meisten Screenreadern erkannt und entsprechend angekündigt. Oft hört der Nutzer dann etwas wie „Trennstrich“ oder „Separator“. Dies gibt ihm den wichtigen Hinweis, dass nun ein thematischer Wechsel stattfindet.

Hättest du stattdessen ein rein visuelles `<div>` mit einem CSS-Rahmen verwendet, würde der Screenreader dieses Element im schlimmsten Fall komplett ignorieren. Der Nutzer würde den beabsichtigten thematischen Bruch verpassen. Die korrekte Verwendung von `<hr>` trägt also dazu bei, deine Inhalte für alle Menschen zugänglich und verständlich zu machen.

Das `<hr>`-Element ist ein perfektes Beispiel dafür, wie HTML sich von einer reinen Präsentationssprache zu einer Sprache entwickelt hat, die die Bedeutung und Struktur von Inhalten in den Vordergrund stellt. Nutze es mit Bedacht, und es wird die Lesbarkeit und Klarheit deiner Texte subtil, aber wirkungsvoll verbessern.
