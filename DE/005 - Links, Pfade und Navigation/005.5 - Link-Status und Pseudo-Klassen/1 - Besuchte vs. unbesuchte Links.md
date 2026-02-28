# Besuchte vs. unbesuchte Links

### Besuchte und unbesuchte Links: Visuelles Feedback für den Nutzer

Stell dir vor, du recherchierst ein komplexes Thema auf einer riesigen Website wie Wikipedia. Du klickst dich von einem Artikel zum nächsten, folgst Querverweisen und tauchst immer tiefer in die Materie ein. Wie behältst du den Überblick, welche der unzähligen Links du bereits angeklickt hast? Die Antwort ist eine der grundlegendsten und gleichzeitig genialsten Funktionen des Webs: die visuelle Unterscheidung zwischen besuchten und unbesuhten Links.

Diese Unterscheidung ist kein Zufall, sondern ein bewusstes Designmerkmal, das die Benutzerfreundlichkeit (Usability) einer Webseite massiv verbessert. Sie dient als eine Art visuelles Gedächtnis, das dir hilft, dich im Hypertext zu orientieren, Redundanzen zu vermeiden und deinen Weg nachzuvollziehen. Dein Browser merkt sich, welchen URLs du bereits gefolgt bist, und gibt diese Information an die Webseite weiter, damit sie entsprechend gestaltet werden kann.

Die technische Umsetzung dieser Unterscheidung geschieht in CSS mithilfe sogenannter **Pseudo-Klassen**. Eine Pseudo-Klasse ist ein Schlüsselwort, das du an einen Selektor anhängst, um ein Element in einem bestimmten Zustand zu gestalten. Sie beschreibt also nicht, *was* ein Element ist (wie ein `p` oder `div`), sondern in welchem *Zustand* es sich gerade befindet.

Für die Zustände von Links sind vor allem zwei Pseudo-Klassen von zentraler Bedeutung:

*   `:link`: Diese Pseudo-Klasse zielt auf alle `<a>`-Elemente mit einem `href`-Attribut ab, deren Zieladresse sich **nicht** im Browserverlauf des Nutzers befindet. Es ist der Standardzustand eines Links, den du noch nicht besucht hast.
*   `:visited`: Diese Pseudo-Klasse zielt auf alle `<a>`-Elemente ab, deren Zieladresse sich bereits im Browserverlauf befindet. Es ist der Zustand eines Links, den du bereits angeklickt hast.

#### Die grundlegende Gestaltung

Die wohl bekannteste Konvention im Web ist, unbesuchte Links blau und besuchte Links lila darzustellen. Diese Farbgebung hat sich über Jahrzehnte etabliert und ist für viele Nutzer eine tief verankerte Erwartungshaltung. Auch wenn du gestalterisch völlig frei bist, ist es oft ratsam, sich an diese oder ähnliche, leicht unterscheidbare Muster zu halten.

Schauen wir uns ein einfaches Beispiel an. Gegeben sei folgender HTML-Code:

```html
<p>
  Willkommen in der Welt der Hyperlinks. Hier ist ein Link zur
  <a href="https://de.wikipedia.org/wiki/Hypertext_Markup_Language">HTML-Spezifikation auf Wikipedia</a>,
  den du wahrscheinlich schon einmal besucht hast. Und hier ist ein Link zu einer
  <a href="https://www.beispiel-einer-unbesuchten-seite.xyz/">noch nicht existierenden Seite</a>,
  den du sicher noch nicht kennst.
</p>
```

Ohne spezifisches CSS würde der Browser seine Standardfarben verwenden – meistens genau das erwähnte Blau und Lila. Wenn du diese Farben jedoch an dein eigenes Design anpassen möchtest, kannst du das mit CSS sehr einfach tun:

```css
/* Stil für unbesuchte Links */
a:link {
  color: #007bff; /* Ein leuchtendes Blau */
  text-decoration: underline;
}

/* Stil für besuchte Links */
a:visited {
  color: #6a0dad; /* Ein klassisches Lila */
  text-decoration: none; /* Nehmen wir zur Abwechslung den Unterstrich weg */
}
```

Mit diesem CSS wird jeder Link, den du noch nicht angeklickt hast, in einem leuchtenden Blau mit Unterstrich dargestellt. Sobald du einen Link anklickst und zur Zielseite navigierst, wird der Browser diese URL in seinem Verlauf speichern. Kehrst du danach zur ursprünglichen Seite zurück, wird derselbe Link nun lila und ohne Unterstrich angezeigt. Du hast sofortiges visuelles Feedback darüber, wo du schon warst.

#### Eine wichtige Einschränkung: Der Schutz der Privatsphäre

Früher war es möglich, mit der `:visited`-Pseudo-Klasse fast jede beliebige CSS-Eigenschaft zu verändern. Kreative, aber leider auch böswillige Entwickler erkannten darin eine Sicherheitslücke. Sie konnten eine unsichtbare Liste mit Tausenden von Links zu populären (oder auch heiklen) Webseiten erstellen und dann per JavaScript überprüfen, welche dieser Links die `:visited`-Stile angenommen hatten (z.B. eine andere Farbe oder Größe). So konnten sie Rückschlüsse auf deinen Browserverlauf ziehen und ein detailliertes Profil deiner Interessen erstellen. Dieser Angriff wurde als "History Sniffing" bekannt.

Um diese massive Verletzung der Privatsphäre zu unterbinden, haben moderne Browser die Möglichkeiten der `:visited`-Pseudo-Klasse stark eingeschränkt. Die Regel lautet heute: **Du kannst nur solche CSS-Eigenschaften für besuchte Links ändern, deren Wert nicht über JavaScript ausgelesen werden kann.**

In der Praxis bedeutet das, dass du hauptsächlich die Farbe von Elementen ändern kannst. Folgende Eigenschaften sind für `:visited` in der Regel sicher und funktionieren in allen modernen Browsern:

*   `color`
*   `background-color`
*   `border-color` (und seine spezifischen Varianten wie `border-top-color`)
*   `outline-color`
*   `column-rule-color`
*   Die Farbattribute von SVG-Elementen (`fill` und `stroke`)

Eigenschaften, die das Layout, die Dimensionen oder die Schriftart eines Elements beeinflussen, werden vom Browser für `:visited`-Links ignoriert. Du kannst also **nicht** Folgendes tun:

*   Die Schriftgröße ändern (`font-size`).
*   Den Link fett oder kursiv machen (`font-weight`, `font-style`).
*   Ein Hintergrundbild hinzufügen (`background-image`).
*   Den Link verschieben oder seine Größe ändern (`margin`, `padding`, `width`, `height`).
*   Ihn ausblenden (`display: none`).

Wenn du versuchst, eine dieser "verbotenen" Eigenschaften auf einen `:visited`-Link anzuwenden, wird der Browser stattdessen den Wert der `:link`-Regel (oder der allgemeinen `a`-Regel) verwenden. Dies stellt sicher, dass eine Webseite nicht durch Messung von Box-Dimensionen oder Auslesen von Schriftarten auf deinen Browserverlauf schließen kann. Die einzige Information, die visuell preisgegeben wird, ist die Farbe – und diese kann per `getComputedStyle()` in JavaScript nicht mehr unterschieden werden.

#### Die richtige Reihenfolge: Link-Zustände kombinieren

Neben `:link` und `:visited` gibt es noch zwei weitere wichtige Pseudo-Klassen für Links, die Interaktionen beschreiben:

*   `:hover`: Der Zustand, wenn du mit dem Mauszeiger über dem Link schwebst.
*   `:active`: Der Zustand, während du den Link aktiv anklickst (Maustaste gedrückt hältst).

Wenn du alle vier Zustände definieren möchtest, ist die Reihenfolge in deiner CSS-Datei entscheidend. Aufgrund der Art und Weise, wie CSS-Regeln bei gleicher Spezifität angewendet werden (die letzte Regel gewinnt), hat sich eine feste Reihenfolge als Best Practice etabliert. Man kann sie sich mit der Eselsbrücke **L-V-H-A** merken:

1.  **L**ink
2.  **V**isited
3.  **H**over
4.  **A**ctive

Ein vollständiges und robustes Styling für Links könnte also so aussehen:

```css
/* 1. Standard für unbesuchte Links */
a:link {
  color: #005a9c;
  text-decoration: none; /* Kein Unterstrich im Ruhezustand */
}

/* 2. Standard für besuchte Links */
a:visited {
  color: #5a3a73;
}

/* 3. Stil, wenn der Mauszeiger darüber schwebt (gilt für besuchte UND unbesuchte) */
a:hover {
  color: #007bff;
  text-decoration: underline; /* Unterstrich als visuelles Feedback für die Interaktion */
}

/* 4. Stil, während der Link geklickt wird (gilt für besuchte UND unbesuchte) */
a:active {
  color: #ff4136; /* Eine auffällige "Klick"-Farbe */
}
```

Warum ist diese Reihenfolge so wichtig? Lass es uns durchspielen:

*   Ein unbesuchter Link ist zunächst nur `:link`. Wenn du mit der Maus darüberfährst, ist er gleichzeitig `:link` und `:hover`. Da die `:hover`-Regel nach der `:link`-Regel kommt, überschreibt sie die Farbe und fügt den Unterstrich hinzu. Perfekt.
*   Ein besuchter Link ist `:visited`. Fährst du mit der Maus darüber, ist er gleichzeitig `:visited` und `:hover`. Auch hier kommt die `:hover`-Regel nach `:visited` und gewinnt, sodass der Hover-Effekt wie erwartet funktioniert. Würde `:hover` vor `:visited` stehen, würde ein besuchter Link beim Darüberfahren lila bleiben, was den interaktiven Effekt zunichtemachen würde.
*   Die `:active`-Regel steht ganz am Ende, weil der Klick-Zustand der kurzlebigste und spezifischste ist. Er soll alle anderen Zustände überschreiben, solange die Maustaste gedrückt ist.

Die bewusste Gestaltung von besuchten und unbesuchten Links ist ein kleines Detail mit großer Wirkung. Sie ist ein Eckpfeiler guter Web-Usability und zeigt, wie eng technisches Verständnis (CSS Pseudo-Klassen, Privatsphäre-Implikationen) und nutzerzentriertes Design miteinander verwoben sind.
