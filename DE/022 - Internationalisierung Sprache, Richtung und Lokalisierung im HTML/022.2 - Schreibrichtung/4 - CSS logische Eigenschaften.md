# CSS logische Eigenschaften

### CSS Logische Eigenschaften: Dein Layout für die ganze Welt

Stell dir vor, du gestaltest eine schicke Komponente, zum Beispiel eine Infokarte mit einem kleinen Icon auf der linken Seite und einem Text daneben. Du möchtest einen Abstand zwischen dem Icon und dem Text. Intuitiv greifst du wahrscheinlich zu `margin-right` für das Icon oder `margin-left` für den Text. Für ein deutsches oder englisches Layout funktioniert das tadellos. Der Text fließt von links nach rechts (Left-to-Right, LTR), und dein Abstand ist genau da, wo er sein soll.

Doch was passiert, wenn deine Webseite ins Arabische, Hebräische oder Persische übersetzt wird? In diesen Sprachen verläuft die Schrift von rechts nach links (Right-to-Left, RTL). Dein `margin-left`, das den Text vom linken Rand wegschieben sollte, drückt ihn nun in die falsche Richtung. Der Text klebt am Icon, und der Abstand befindet sich auf der falschen Seite, am äußeren rechten Rand. Dein Design ist kaputt.

Dieses Problem entsteht, weil Eigenschaften wie `margin-left`, `padding-right`, `border-top` oder `width` **physikalisch** sind. Sie beziehen sich auf die festen, visuellen Kanten des Bildschirms: links, rechts, oben, unten. Sie ignorieren den Kontext der Sprache und der Schreibrichtung vollständig.

Hier kommen die **logischen Eigenschaften** ins Spiel. Sie sind die moderne und flexiblere Antwort auf dieses Problem. Anstatt in festen, physischen Richtungen zu denken, denken wir mit ihnen in logischen, fluss-relativen Richtungen.

#### Die zwei Achsen: Inline und Block

Um logische Eigenschaften zu verstehen, müssen wir unser mentales Modell von einem Webseiten-Layout ein wenig anpassen. Vergiss für einen Moment "horizontal" und "vertikal". Denke stattdessen in zwei Achsen, die sich nach der Schreibrichtung des Dokuments richten:

1.  **Die Inline-Achse:** Das ist die Achse, auf der der Text fließt. In einer deutschen oder englischen Webseite verläuft sie horizontal von links nach rechts. In einer arabischen Webseite verläuft sie horizontal von rechts nach links. In einer traditionellen japanischen Webseite könnte sie sogar vertikal von oben nach unten verlaufen.
2.  **Die Block-Achse:** Das ist die Achse, auf der neue Inhaltsblöcke (wie Absätze, Überschriften oder `div`-Elemente) untereinander angeordnet werden. In den meisten Sprachen verläuft sie von oben nach unten.

Anstelle von `left`/`right` und `top`/`bottom` verwenden logische Eigenschaften die Begriffe `start`/`end` und beziehen diese auf die beiden Achsen:

*   **`inline-start`**: Der Anfang auf der Inline-Achse. Bei LTR-Schrift ist das `left`, bei RTL-Schrift ist das `right`.
*   **`inline-end`**: Das Ende auf der Inline-Achse. Bei LTR-Schrift ist das `right`, bei RTL-Schrift ist das `left`.
*   **`block-start`**: Der Anfang auf der Block-Achse. In einer von oben nach unten verlaufenden Schrift ist das `top`.
*   **`block-end`**: Das Ende auf der Block-Achse. In einer von oben nach unten verlaufenden Schrift ist das `bottom`.

Dieses Konzept ist der Schlüssel. Du beschreibst nicht mehr, wo etwas physisch auf dem Bildschirm ist, sondern wo es in Relation zum Inhaltsfluss sein soll.

#### Abstände, Innenabstände und Rahmen im logischen Modell

Schauen wir uns an, wie die bekannten CSS-Eigenschaften in ihre logischen Pendants übersetzt werden.

##### Margin und Padding

Die Umstellung bei `margin` und `padding` ist am einfachsten und hat den größten Effekt.

| Physikalische Eigenschaft | Logische Eigenschaft        | Beschreibung                                           |
| ------------------------- | --------------------------- | ------------------------------------------------------ |
| `margin-left`             | `margin-inline-start`       | Abstand am Anfang der Inline-Achse.                    |
| `margin-right`            | `margin-inline-end`         | Abstand am Ende der Inline-Achse.                      |
| `margin-top`              | `margin-block-start`        | Abstand am Anfang der Block-Achse.                     |
| `margin-bottom`           | `margin-block-end`          | Abstand am Ende der Block-Achse.                       |
| `padding-left`            | `padding-inline-start`      | Innenabstand am Anfang der Inline-Achse.               |
| `padding-right`           | `padding-inline-end`        | Innenabstand am Ende der Inline-Achse.                 |
| `padding-top`             | `padding-block-start`       | Innenabstand am Anfang der Block-Achse.                |
| `padding-bottom`          | `padding-block-end`         | Innenabstand am Ende der Block-Achse.                  |

Es gibt auch praktische Kurzschreibweisen:

*   **`margin-inline: <start> <end>`**: Setzt `margin-inline-start` und `margin-inline-end`. Wenn nur ein Wert angegeben wird, gilt er für beide Seiten.
*   **`margin-block: <start> <end>`**: Setzt `margin-block-start` und `margin-block-end`. Wenn nur ein Wert angegeben wird, gilt er für beide Seiten.
*   **`padding-inline: <start> <end>`**: Dasselbe für `padding` auf der Inline-Achse.
*   **`padding-block: <start> <end>`**: Dasselbe für `padding` auf der Block-Achse.

**Beispiel:**

Anstatt dies zu schreiben:

```css
.card {
  margin-left: 10px;
  margin-right: 10px;
  padding-top: 20px;
  padding-bottom: 20px;
}
```

Schreibst du dies:

```css
.card {
  margin-inline: 10px;
  padding-block: 20px;
}
```

Dieser Code ist nicht nur kürzer, er funktioniert auch automatisch korrekt in LTR- und RTL-Kontexten.

##### Rahmen (Border)

Das gleiche Prinzip gilt für Rahmen. Du ersetzt die physische Richtung durch die logische.

| Physikalische Eigenschaft | Logische Eigenschaft         |
| ------------------------- | ---------------------------- |
| `border-left`             | `border-inline-start`        |
| `border-right`            | `border-inline-end`          |
| `border-top`              | `border-block-start`         |
| `border-bottom`           | `border-block-end`           |

Auch für die detaillierten Eigenschaften wie `border-left-width` oder `border-right-color` gibt es logische Äquivalente:

*   `border-inline-start-width`
*   `border-inline-end-style`
*   `border-block-start-color`
*   usw.

#### Größe und Positionierung

Die Revolution der logischen Eigenschaften geht aber noch weiter. Sie betrifft auch die grundlegendsten Layout-Eigenschaften: Größe und Position.

##### Logische Größe: `inline-size` und `block-size`

Traditionell verwenden wir `width` und `height`. Aber was ist die "Breite" in einem vertikalen Schriftsystem? Plötzlich ist die "Breite" die vertikale Dimension und die "Höhe" die horizontale. Das ist verwirrend.

Logische Eigenschaften lösen das elegant:

*   **`width`** wird zu **`inline-size`**: die Größe eines Elements entlang der Inline-Achse.
*   **`height`** wird zu **`block-size`**: die Größe eines Elements entlang der Block-Achse.

Die dazugehörigen `min-` und `max-` Eigenschaften gibt es ebenfalls:

*   `min-inline-size`, `max-inline-size`
*   `min-block-size`, `max-block-size`

Für ein horizontales LTR-Layout verhält sich `inline-size` wie `width` und `block-size` wie `height`. Der entscheidende Vorteil zeigt sich, wenn du die Schreibrichtung änderst.

##### Logische Positionierung

Wenn du mit `position: absolute` arbeitest, nutzt du normalerweise `top`, `right`, `bottom` und `left`, um ein Element zu platzieren. Auch hierfür gibt es logische Alternativen, die sich unter dem Namen `inset` zusammenfassen lassen.

| Physikalische Eigenschaft | Logische Eigenschaft  |
| ------------------------- | --------------------- |
| `top`                     | `inset-block-start`   |
| `bottom`                  | `inset-block-end`     |
| `left`                    | `inset-inline-start`  |
| `right`                   | `inset-inline-end`    |

Es gibt eine sehr mächtige Kurzschreibweise `inset`, die `inset-block-start`, `inset-inline-end`, `inset-block-end` und `inset-inline-start` (in dieser Reihenfolge) setzt – ähnlich wie `margin` oder `padding`.

```css
.modal {
  position: absolute;
  /* Statt: top: 0; right: 0; bottom: 0; left: 0; */
  inset: 0;
}
```

#### Ein praktisches Beispiel: Die Infokarte

Erinnern wir uns an unsere Infokarte vom Anfang. Hier ist der Code, einmal auf die alte, physische Weise und einmal auf die neue, logische Weise.

**Der HTML-Code (für beide Beispiele gleich):**

```html
<article class="info-card">
  <span class="icon">💡</span>
  <p class="text">Dies ist eine wichtige Information, die flexibel auf verschiedene Schreibrichtungen reagieren soll.</p>
</article>
```

**CSS – Der alte, physische Weg:**

```css
.info-card {
  display: flex;
  align-items: center;
  border-left: 5px solid steelblue;
  padding: 16px;
  width: 300px;
}

.icon {
  margin-right: 12px;
}
```

Wenn du nun dem `<html>`-Tag das Attribut `dir="rtl"` hinzufügst (`<html lang="ar" dir="rtl">`), siehst du das Problem: Der blaue `border-left` bleibt links, obwohl der Text nun rechtsbündig ist. Der `margin-right` des Icons schiebt den Text weg, aber in die falsche Richtung, sodass der Abstand zwischen Icon und rechtem Rand entsteht, anstatt zwischen Icon und Text.

**CSS – Der neue, logische Weg:**

```css
.info-card {
  display: flex;
  align-items: center;
  border-inline-start: 5px solid steelblue;
  padding: 16px;
  inline-size: 300px;
}

.icon {
  margin-inline-end: 12px;
}
```

Wenn du jetzt `dir="rtl"` hinzufügst, passiert die Magie:

*   `border-inline-start` wird automatisch zu `border-right`.
*   `margin-inline-end` wird automatisch zu `margin-left`.

Das Layout passt sich perfekt und ohne eine einzige zusätzliche Zeile CSS an die neue Schreibrichtung an. Es funktioniert einfach.

#### Über den Tellerrand: Vertikale Schreibmodi

Die wahre Stärke logischer Eigenschaften zeigt sich, wenn wir die Block-Achse verändern. Mit der CSS-Eigenschaft `writing-mode` können wir den Textfluss komplett umstellen, zum Beispiel für traditionelle ostasiatische Schriften.

```css
.vertical-text {
  writing-mode: vertical-rl; /* Text fließt von oben nach unten, Zeilen von rechts nach links */
  
  /* Jetzt wird's interessant: */
  inline-size: 300px; /* Das ist jetzt die HÖHE */
  block-size: 200px; /* Das ist jetzt die BREITE */
  
  padding-inline-start: 20px; /* Innenabstand OBEN */
  padding-block-start: 10px; /* Innenabstand RECHTS */
}
```

In einem vertikalen Schreibmodus kippen die Achsen um 90 Grad. Die Inline-Achse verläuft nun vertikal und die Block-Achse horizontal. Dank der logischen Eigenschaften passen sich deine Größen- und Abstandsdefinitionen automatisch an. `inline-size` steuert die Größe in Textflussrichtung (jetzt die Höhe), und `block-size` steuert die Größe, in der Blöcke nebeneinander gestapelt werden (jetzt die Breite).

Dieser Perspektivwechsel ist unglaublich mächtig. Du definierst dein Design nicht mehr für einen Bildschirm, sondern für den Inhalt selbst.

#### Ein Wandel in der Denkweise

Der Umstieg auf logische Eigenschaften ist mehr als nur das Erlernen neuer CSS-Namen. Es ist ein fundamentaler Wandel in der Art und Weise, wie du über Layouts nachdenkst. Du entkoppelst dein Design von der physischen Darstellung und bindest es an die logische Struktur deines Inhalts.

In einer globalisierten Welt, in der deine Webseite potenziell von jedem Menschen in jeder Sprache gelesen werden kann, ist dieser Ansatz nicht nur "nice to have" – er ist die Grundlage für robustes, zukunftssicheres und inklusives Webdesign. Indem du von Anfang an in `inline-start` und `block-end` denkst, baust du Webseiten, die von Natur aus flexibler und für ein globales Publikum besser vorbereitet sind.
