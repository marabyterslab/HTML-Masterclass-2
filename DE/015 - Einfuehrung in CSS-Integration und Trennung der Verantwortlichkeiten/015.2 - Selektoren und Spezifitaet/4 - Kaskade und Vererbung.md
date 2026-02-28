# Kaskade und Vererbung

### Kaskade und Vererbung: Wer gewinnt im CSS?

Stell dir vor, du schreibst eine Reihe von Anweisungen für deinen Browser. Du sagst ihm: „Alle Absätze sollen blau sein.“ Dann fügst du hinzu: „Nein, warte, alle Absätze mit der Klasse ‚highlight‘ sollen rot sein.“ Und schließlich, für einen ganz bestimmten Absatz, schreibst du direkt in das HTML-Tag: „Dieser eine Absatz soll grün sein.“

Welche Farbe hat der Absatz am Ende?

Dein Browser steht ständig vor solchen Entscheidungen. Er muss aus potenziell Hunderten von CSS-Regeln, die aus verschiedenen Quellen stammen, die eine, gültige Regel für jedes einzelne HTML-Element und jede seiner Eigenschaften finden. Dieser komplexe, aber logische Entscheidungsprozess wird durch drei Kernkonzepte geregelt: die Kaskade, die Spezifität und die Vererbung. Im vorherigen Kapitel hast du bereits die Selektoren und ihre Spezifität kennengelernt. Nun setzen wir diese Puzzleteile zusammen und schauen uns das große Ganze an.

#### Die Kaskade – Der Wasserfall der Stile

Das „C“ in CSS steht für „Cascading“ (kaskadierend). Dieses Wort ist der Schlüssel zum Verständnis, wie CSS-Regeln miteinander konkurrieren. Du kannst es dir wie einen Wasserfall vorstellen: Regeln fließen von oben nach unten, und spätere Regeln können frühere überschreiben.

Die Kaskade berücksichtigt dabei vor allem zwei Dinge: die Herkunft einer Regel und ihre Reihenfolge im Code.

**1. Die Herkunft des Stylesheets**

CSS-Regeln können aus verschiedenen Quellen stammen, die eine klare Hierarchie haben:

1.  **Browser-Standardstile (User Agent Stylesheets):** Jeder Browser hat ein eingebautes Stylesheet, das die Standarddarstellung für alle HTML-Elemente festlegt. Deshalb hat eine `<h1>` ohne jegliches CSS eine große Schriftgröße und einen `<strong>`-Tag macht Text fett. Diese Regeln haben die niedrigste Priorität.
2.  **Benutzer-Stylesheets (User Stylesheets):** Ein Nutzer kann in seinem Browser eigene Stile definieren, um zum Beispiel aus Gründen der Barrierefreiheit die Schriftgröße auf allen Webseiten zu erhöhen. Diese sind heute seltener, aber sie überschreiben die Browser-Standards.
3.  **Autoren-Stylesheets (Author Stylesheets):** Das ist dein Code! Die CSS-Dateien, die du als Webentwickler schreibst und in deine Webseite einbindest. Diese Regeln sind die wichtigsten und überschreiben sowohl die Browser- als auch die Benutzer-Stile.

Innerhalb deiner Autoren-Stile gibt es ebenfalls eine Reihenfolge. CSS, das du direkt im HTML-Dokument in einem `<style>`-Block schreibst, überschreibt Regeln aus einer externen, über `<link>` eingebundenen CSS-Datei, sofern diese davor geladen wird. Und Inline-Stile, die direkt im HTML-Tag über das `style`-Attribut definiert werden, haben eine noch höhere Priorität.

```html
<!-- Externe CSS-Datei -->
<link rel="stylesheet" href="style.css">

<!-- Interne CSS -->
<style>
  p {
    color: orange; /* Diese Regel verliert gegen den Inline-Stil */
  }
</style>

<!-- Inline-CSS (hat hohe Priorität in der Kaskade) -->
<p style="color: green;">Dieser Text wird grün sein.</p>
```

**2. Die Reihenfolge im Code**

Wenn zwei Regeln die gleiche Herkunft und die gleiche Spezifität haben (mehr dazu gleich), gewinnt einfach die Regel, die später im Code definiert wird.

```css
/* style.css */

p {
  color: blue;
}

p {
  color: red; /* Diese Regel gewinnt, da sie später kommt */
}
```

Alle Absätze auf deiner Seite werden rot sein, weil die zweite Regel die erste überschreibt. Die Kaskade fließt nach unten, und die letzte Anweisung setzt sich durch.

**Die Ausnahme: `!important`**

Es gibt eine Möglichkeit, diese natürliche Ordnung zu durchbrechen: die `!important`-Regel. Wenn du sie an eine CSS-Eigenschaft anhängst, erhält diese Deklaration die höchstmögliche Priorität und überschreibt fast alles andere.

```css
p {
  color: red !important; /* Diese Regel gewinnt fast immer */
}

#einzelner-absatz {
  color: blue; /* ...selbst gegen eine spezifischere ID */
}
```

Der Einsatz von `!important` sollte jedoch die absolute Ausnahme bleiben. Es macht deinen Code schwerer zu warten und zu debuggen, da es die logischen Regeln der Kaskade und Spezifität aushebelt. Es ist oft ein Zeichen für einen sogenannten „Spezifitätskrieg“, den man besser durch eine saubere Code-Struktur vermeidet.

#### Spezifität – Die Macht der Selektoren

Was passiert, wenn zwei Regeln aus der gleichen Quelle stammen und auf dasselbe Element abzielen, aber unterschiedliche Selektoren verwenden? Hier kommt die Spezifität ins Spiel, die du bereits kennengelernt hast. Die Kaskade nutzt die Spezifität als entscheidendes Kriterium, um den Gewinner zu ermitteln.

Zur Erinnerung: Spezifität ist ein Maß dafür, wie spezifisch ein Selektor ein Element anspricht. Die Hierarchie ist klar:

1.  **Inline-Stile:** (z.B. `style="color: red;"`) – Höchste Spezifität.
2.  **ID-Selektoren:** (z.B. `#header`)
3.  **Klassen-, Attribut- und Pseudoklassen-Selektoren:** (z.B. `.button`, `[type="text"]`, `:hover`)
4.  **Element- und Pseudoelement-Selektoren:** (z.B. `div`, `::before`)

Schauen wir uns ein praktisches Beispiel an:

```html
<div id="content">
  <p class="intro">Dies ist ein wichtiger Absatz.</p>
</div>
```

```css
/* style.css */

/* Regel 1: Elements-Selektor (niedrigste Spezifität) */
p {
  color: black;
}

/* Regel 2: Klassen-Selektor (mittlere Spezifität) */
.intro {
  color: blue;
}

/* Regel 3: ID-Selektor gefolgt von einem Element-Selektor (hohe Spezifität) */
#content p {
  color: green;
}
```

Obwohl alle drei Regeln auf denselben Absatz abzielen, gewinnt die dritte Regel (`#content p`). Ihr Selektor ist der spezifischste, da er eine ID enthält. Die Reihenfolge im Code spielt hier keine Rolle mehr, weil der Spezifitätsunterschied eindeutig ist. Die Farbe des Absatzes wird grün sein.

#### Vererbung – Das Familienerbe der Stile

Nicht jede CSS-Eigenschaft muss für jedes Element einzeln definiert werden. Wäre das nicht furchtbar mühsam? Stell dir vor, du müsstest für jeden Absatz, jede Überschrift und jeden Listenpunkt einzeln die Schriftart festlegen.

Hier kommt die Vererbung ins Spiel. Das Konzept ist einfach: Wenn für ein Element eine bestimmte Eigenschaft nicht explizit festgelegt wurde, schaut es bei seinem Elternelement nach und „erbt“ den Wert von dort, falls die Eigenschaft vererbbar ist.

**Welche Eigenschaften werden vererbt?**

Typischerweise sind es Eigenschaften, die den Text und seine Darstellung betreffen. Es ergibt Sinn, dass ein `<em>`-Tag innerhalb eines Absatzes dieselbe Schriftart und Farbe haben sollte, wenn nicht anders angegeben.

Einige typische vererbbare Eigenschaften sind:

*   `color`
*   `font-family`, `font-size`, `font-weight`, `font-style`
*   `line-height`
*   `text-align`, `text-indent`
*   `list-style`

**Welche Eigenschaften werden nicht vererbt?**

Andere Eigenschaften werden bewusst nicht vererbt, weil es meist zu unerwünschten Ergebnissen führen würde. Stell dir vor, du gibst einem Container einen Rahmen (`border`) und jedes Kindelement darin würde diesen Rahmen ebenfalls erben – ein optisches Chaos.

Typische nicht vererbbare Eigenschaften sind:

*   `background-color`
*   `border`
*   `padding`, `margin`
*   `width`, `height`
*   `box-shadow`

Schauen wir uns ein Beispiel an:

```html
<body>
  <div>
    <p>Dieser Text erbt die Schriftart und Farbe vom <code>body</code>-Element.</p>
    <em>Dieser Text ebenso.</em>
  </div>
</body>
```

```css
body {
  font-family: 'Helvetica', sans-serif;
  color: #333; /* Dunkelgrau */
}

div {
  border: 1px solid black; /* Border wird nicht an p oder em vererbt */
  background-color: #f0f0f0; /* Hintergrund wird nicht vererbt */
}
```

In diesem Fall werden der `<p>`- und der `<em>`-Tag die Schriftart `Helvetica` und die dunkelgraue Textfarbe vom `<body>`-Element erben. Der Rahmen und die Hintergrundfarbe des `<div>` werden jedoch nicht an die Kinder weitergegeben.

**Die Vererbung steuern**

Manchmal möchtest du dieses Verhalten gezielt beeinflussen. Dafür gibt es spezielle Schlüsselwörter:

*   `inherit`: Dieses Schlüsselwort zwingt eine Eigenschaft zur Vererbung, selbst wenn sie normalerweise nicht vererbbar ist. Du könntest zum Beispiel einem Kindelement sagen, es solle die Rahmenfarbe seines Vaters erben: `border-color: inherit;`.
*   `initial`: Setzt eine Eigenschaft auf ihren ursprünglichen Standardwert zurück, wie er vom Browser definiert ist.
*   `unset`: Ein praktischer Helfer. Bei vererbbaren Eigenschaften verhält es sich wie `inherit`. Bei nicht vererbbaren Eigenschaften verhält es sich wie `initial`. Es ist eine Art intelligenter Reset.

#### Das Zusammenspiel: Die finale Entscheidung des Browsers

Jetzt fügen wir alles zusammen. Um den endgültigen Wert für eine Eigenschaft eines Elements zu bestimmen, folgt der Browser einem klaren Algorithmus:

1.  **Relevanz:** Zuerst sammelt der Browser alle CSS-Deklarationen, deren Selektoren auf das betreffende Element passen.
2.  **Herkunft und Wichtigkeit:** Die Regeln werden nach ihrer Herkunft sortiert. Deine Autoren-Regeln (mit Ausnahme von `!important`-Regeln) haben Vorrang vor Benutzer- und Browser-Regeln.
3.  **Spezifität:** Innerhalb der gleichen Herkunft gewinnt die Regel mit dem spezifischsten Selektor. Alle Regeln mit geringerer Spezifität werden verworfen.
4.  **Reihenfolge:** Wenn nach dem Spezifitäts-Check immer noch mehrere Regeln mit identischer Spezifität übrig sind, gewinnt die Regel, die als letzte im Quellcode definiert wurde.

Wenn nach all diesen Schritten für eine Eigenschaft kein Wert gefunden wurde (weil keine Regel sie direkt anspricht), prüft der Browser:

5.  **Vererbung:** Ist die Eigenschaft vererbbar? Wenn ja, übernimmt das Element den Wert von seinem direkten Elternelement.
6.  **Standardwert:** Ist die Eigenschaft nicht vererbbar oder hat kein Elternelement einen Wert, den es vererben könnte, greift der Browser auf den `initial`-Wert, also den Standardwert für diese Eigenschaft, zurück.

Dieses System mag auf den ersten Blick komplex erscheinen, aber es ist unglaublich mächtig und logisch. Es gibt dir feingranulare Kontrolle über das Aussehen deiner Webseite und sorgt gleichzeitig für Effizienz durch das Prinzip der Vererbung. Wenn du die Regeln der Kaskade, Spezifität und Vererbung verinnerlicht hast, wirst du in der Lage sein, CSS-Konflikte nicht nur zu lösen, sondern sie von vornherein zu vermeiden.
