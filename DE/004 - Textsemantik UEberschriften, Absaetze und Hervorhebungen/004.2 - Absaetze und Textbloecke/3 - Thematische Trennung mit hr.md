# Thematische Trennung mit hr

### Der thematische Bruch: Das `<hr>`-Element

Stell dir vor, du liest eine Geschichte. Die Hauptfigur hat gerade eine anstrengende Reise durch einen düsteren Wald hinter sich gebracht. Der Abschnitt endet, und im nächsten beginnt ein völlig neuer Gedanke: Die Erzählung springt zu einem Gespräch, das zur gleichen Zeit in einem weit entfernten Schloss stattfindet. In Büchern wird ein solcher Szenenwechsel oft durch ein paar leere Zeilen oder ein kleines Symbol, wie drei Sternchen (***), signalisiert. Dieser Bruch teilt dem Leser mit: „Achtung, hier passiert ein thematischer Wechsel.“

In HTML gibt es ein Element, das genau für diesen Zweck geschaffen wurde: das `<hr>`-Element.

Ursprünglich stand `hr` für „Horizontal Rule“, also eine horizontale Linie. In den frühen Tagen des Webs war seine Funktion fast rein präsentationell: Es zeichnete einen Strich über die Seite, um Inhalte visuell voneinander zu trennen. Doch wie viele andere Elemente in HTML hat sich seine Bedeutung mit der Entwicklung von HTML5 grundlegend gewandelt. Heute steht das `<hr>`-Element für einen **thematischen Bruch** auf Absatzebene.

Wichtig ist hierbei das Wort *thematisch*. Das `<hr>`-Element ist kein rein visueller Strich, sondern ein semantisches Signal, das eine Veränderung im Thema oder in der Szenerie anzeigt. Es ist ein sogenanntes „leeres“ oder „void“-Element, was bedeutet, dass es keinen Inhalt umschließt und daher auch kein schließendes Tag benötigt. Man schreibt es einfach als `<hr>`.

#### Wann solltest du ein `<hr>`-Element verwenden?

Die Regel ist einfach: Immer dann, wenn du innerhalb eines fortlaufenden Textes einen klaren thematischen Wechsel signalisieren möchtest, ohne dafür eine neue Überschrift zu benötigen.

Betrachten wir ein paar konkrete Beispiele:

**1. Szenenwechsel in einer Erzählung**

Wie in unserem Eingangsbeispiel kannst du `<hr>` verwenden, um verschiedene Szenen oder Zeitpunkte in einer Geschichte voneinander abzugrenzen.

```html
<article>
  <h1>Das Amulett von Talanor</h1>
  <p>Lyra rannte durch den dichten Nebel des Schattenwaldes. Jeder knackende Ast unter ihren Füßen ließ ihr Herz schneller schlagen. Sie umklammerte das Amulett fester, seine kühle Oberfläche war der einzige Trost in dieser feindseligen Umgebung. Die Bäume schienen nach ihr zu greifen, ihre Äste wie knochige Finger.</p>
  <p>Nach einer gefühlten Ewigkeit lichtete sich der Wald. Vor ihr lag die stille Ebene, und in der Ferne konnte sie die Umrisse der verfluchten Stadt erkennen. Sie hatte es fast geschafft.</p>
  
  <hr>
  
  <p>Zurück im Thronsaal von König Theron herrschte eine angespannte Stille. Der alte Magier Elara starrte in seine Kristallkugel, sein Gesicht war eine Maske der Sorge. "Sie hat den Wald durchquert", flüsterte er, "aber die größte Gefahr liegt noch vor ihr."</p>
</article>
```

Hier signalisiert das `<hr>`, dass der Fokus der Erzählung von Lyra auf den König und den Magier wechselt. Es ist ein klarer Schnitt in der Handlung.

**2. Themenwechsel innerhalb eines Artikels**

Stell dir einen langen Blogbeitrag oder einen informativen Artikel vor. Manchmal möchtest du von einem Aspekt eines Themas zu einem anderen wechseln, der zwar verwandt, aber doch eigenständig ist. Eine neue Überschrift (`<h2>`, `<h3>`) wäre vielleicht zu stark und würde die Sektion als komplett neuen Hauptpunkt ausweisen. Ein `<hr>` kann hier eine sanftere, aber dennoch deutliche Trennung schaffen.

```html
<article>
  <h2>Die Kunst des Kaffeeröstens</h2>
  <p>Der Röstprozess ist entscheidend für das finale Aroma des Kaffees. Während der Röstung durchlaufen die grünen Bohnen komplexe chemische Veränderungen. Zucker karamellisieren, Säuren werden abgebaut und die berühmten Röstaromen entstehen. Ein Röstmeister steuert diesen Prozess präzise über Temperatur und Zeit.</p>
  <p>Man unterscheidet grob zwischen hellen, mittleren und dunklen Röstungen, die jeweils völlig unterschiedliche Geschmacksprofile von fruchtig-säuerlich bis hin zu schokoladig-bitter hervorbringen.</p>
  
  <hr>
  
  <p>Nach dem Rösten ist die richtige Lagerung ebenso wichtig. Kaffee sollte luftdicht, trocken und dunkel aufbewahrt werden, um seine flüchtigen Aromen so lange wie möglich zu bewahren. Gemahlener Kaffee verliert sein Aroma deutlich schneller als ganze Bohnen, weshalb Kenner darauf schwören, die Bohnen erst unmittelbar vor der Zubereitung zu mahlen.</p>
</article>
```

In diesem Beispiel trennt das `<hr>` den Abschnitt über den Röstprozess von den nachfolgenden Tipps zur Lagerung. Beide Themen gehören zum Oberthema „Kaffee“, aber sie behandeln unterschiedliche Phasen.

#### Wann du das `<hr>`-Element *nicht* verwenden solltest

Die moderne, semantische Bedeutung des `<hr>`-Elements zu verstehen, heißt auch zu wissen, wann sein Einsatz falsch ist. Der häufigste Fehler ist, es für rein dekorative Zwecke zu missbrauchen.

**Verwende `<hr>` nicht als visuellen Trenner ohne thematische Bedeutung.**

Wenn du einfach nur eine Linie zur optischen Gliederung deiner Seite möchtest, zum Beispiel zwischen verschiedenen Sektionen einer Visitenkarte oder um eine Überschrift vom Text abzuheben, ist das `<hr>`-Element semantisch falsch. Für solche rein visuellen Aufgaben ist CSS die richtige Wahl.

**Falsch (semantisch):**

```html
<header>
  <h1>Mein Portfolio</h1>
  <hr> <!-- Nur zur Deko, keine thematische Trennung -->
  <nav>...</nav>
</header>
```

**Richtig (mit CSS):**

Du kannst stattdessen einer Sektion oder einer Überschrift einen unteren Rahmen geben.

```html
<header>
  <h1>Mein Portfolio</h1>
  <nav>...</nav>
</header>
```

```css
header h1 {
  border-bottom: 2px solid #333;
  padding-bottom: 0.5em;
  margin-bottom: 1em;
}
```

Diese CSS-Lösung erreicht den gleichen visuellen Effekt, aber ohne die HTML-Struktur mit einem semantisch falschen Element zu belasten. Die Trennung von Struktur (HTML) und Präsentation (CSS) ist eines der fundamentalen Prinzipien moderner Webentwicklung.

#### Die visuelle Gestaltung des Trenners mit CSS

Obwohl die primäre Funktion des `<hr>`-Elements semantisch ist, bedeutet das nicht, dass du sein Aussehen nicht an dein Design anpassen kannst. Im Gegenteil, ein standardmäßiges `<hr>` sieht in den meisten modernen Designs eher altbacken aus. Browser rendern es oft als eine 2 Pixel hohe Linie mit einem 3D-Effekt (Inset-Border).

Glücklicherweise lässt es sich mit CSS sehr einfach und flexibel gestalten. Der übliche Weg ist, zuerst die Standard-Rahmen des Browsers zu entfernen und dann Höhe und Hintergrundfarbe selbst zu definieren.

**Ein einfacher, moderner Trenner:**

```css
hr {
  border: none; /* Entfernt den 3D-Rahmen des Browsers */
  height: 1px; /* Definiert die Dicke der Linie */
  background-color: #ccc; /* Setzt die Farbe der Linie */
  margin: 2em 0; /* Sorgt für vertikalen Abstand */
}
```

Mit diesem einfachen CSS-Snippet wird aus der altbackenen Linie ein feiner, grauer Strich, der sich nahtlos in viele Designs einfügt.

**Kreativere Gestaltungsmöglichkeiten:**

Du kannst aber auch deutlich kreativer werden. Wie wäre es mit einem kürzeren, dickeren Strich, der zentriert ist?

```html
<p>Erster thematischer Block...</p>
<hr class="short-fancy">
<p>Zweiter thematischer Block...</p>
```

```css
hr.short-fancy {
  border: none;
  height: 5px;
  width: 100px; /* Nur 100 Pixel breit */
  background-color: steelblue;
  border-radius: 5px; /* Abgerundete Ecken */
  margin: 3em auto; /* Zentriert die Linie horizontal */
}
```

Du kannst sogar Farbverläufe oder Bilder verwenden, um dein `<hr>`-Element zu einem echten Design-Highlight zu machen, das trotzdem seine semantische Bedeutung beibehält.

#### Zugänglichkeit (Accessibility)

Ein weiterer Vorteil der korrekten Verwendung des `<hr>`-Elements ist die Zugänglichkeit. Standardmäßig hat das `<hr>`-Element die ARIA-Rolle `separator`. Das bedeutet, dass Screenreader, die von Menschen mit Sehbehinderungen genutzt werden, es als „Trennzeichen“ oder „horizontale Trennlinie“ ansagen. Damit wird der thematische Bruch, den du beabsichtigst, auch für Nutzer hörbar gemacht, die die visuelle Linie nicht sehen können.

Wenn du stattdessen ein rein dekoratives `<div>` mit einem CSS-Rahmen verwenden würdest, um eine thematische Trennung zu erzeugen, ginge diese Information für Screenreader-Nutzer verloren, es sei denn, du fügst die ARIA-Rolle manuell hinzu (`<div role="separator">`). Das `<hr>`-Element gibt dir diese semantische Korrektheit und Zugänglichkeit von Haus aus.

Das `<hr>` ist also weit mehr als nur eine Linie. Es ist ein kleines, aber feines Werkzeug, um deine Inhalte sinnvoll zu strukturieren und ihnen eine tiefere Bedeutungsebene zu verleihen. Wenn du es bewusst und an den richtigen Stellen einsetzt, wird es zu einem subtilen, aber mächtigen Werkzeug in deinem semantischen Arsenal.
