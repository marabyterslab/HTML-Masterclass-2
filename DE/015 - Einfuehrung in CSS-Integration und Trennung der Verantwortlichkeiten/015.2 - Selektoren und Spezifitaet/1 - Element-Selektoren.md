# Element-Selektoren

### Element-Selektoren: Die einfachste Art, HTML-Elemente anzusprechen

Stell dir vor, du stehst vor einem frisch gebauten Haus, das nur aus grauen Wänden, Fenstern und Türen besteht. Deine Aufgabe ist es, ihm Farbe und Leben zu verleihen. Du würdest nicht einfach einen Eimer Farbe an die Wand werfen und hoffen, dass es gut aussieht. Stattdessen sagst du dir: „Alle Fensterrahmen sollen weiß sein“, „Die Haustür soll blau sein“ und „Alle Wände im Erdgeschoss bekommen einen sanften Beigeton“.

Genau diese Logik wenden wir in CSS an, um unsere HTML-Struktur zu gestalten. Wir müssen dem Browser präzise Anweisungen geben, *welches* Element *welchen* Stil erhalten soll. Das Werkzeug, das uns diese präzise Ansprache ermöglicht, ist der **Selektor**. Und die grundlegendste, direkteste Form eines Selektors ist der **Element-Selektor**.

Ein Element-Selektor ist nichts anderes als der Name eines HTML-Tags. Wenn du alle Absätze (`<p>`) auf deiner Seite ansprechen möchtest, lautet dein Selektor `p`. Wenn du alle Hauptüberschriften (`<h1>`) gestalten willst, ist dein Selektor `h1`. Einfacher geht es kaum.

#### Die grundlegende Syntax

Eine CSS-Regel besteht immer aus zwei Hauptteilen: dem Selektor und dem Deklarationsblock. Der Deklarationsblock wird in geschweifte Klammern `{}` eingeschlossen und enthält eine oder mehrere Deklarationen, die wiederum aus einer Eigenschaft und einem Wert bestehen.

```css
selektor {
  eigenschaft: wert;
  weitere-eigenschaft: anderer-wert;
}
```

Wenn wir diesen Aufbau auf einen Element-Selektor anwenden, sieht das zum Beispiel so aus:

```css
p {
  color: navy;
  font-size: 16px;
}
```

Schauen wir uns das einmal im Kontext eines HTML-Dokuments an. Angenommen, du hast folgenden HTML-Code:

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Ein einfaches Beispiel</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Willkommen auf meiner Seite</h1>
  <p>Dies ist der erste Absatz. Er beschreibt den Inhalt der Seite.</p>
  <p>Hier folgt ein zweiter Absatz mit weiteren Informationen.</p>
  <h2>Ein Unterthema</h2>
  <p>Auch dieser Absatz wird von unserer CSS-Regel erfasst.</p>
</body>
</html>
```

Wenn du nun die oben genannte CSS-Regel in deiner `style.css`-Datei speicherst, passiert Folgendes: Der Browser liest die Regel `p { ... }`. Er durchsucht daraufhin das gesamte HTML-Dokument nach allen `<p>`-Tags – und zwar ausnahmslos jedem einzelnen. Für jedes gefundene `<p>`-Element wendet er die deklarierten Stile an. Das Ergebnis: Alle drei Absätze auf der Seite werden in der Farbe Marineblau (`navy`) und mit einer Schriftgröße von 16 Pixeln dargestellt. Die `<h1>`- und `<h2>`-Überschriften bleiben davon unberührt, da sie nicht vom Selektor `p` angesprochen werden.

#### Die globale Reichweite von Element-Selektoren

Das Besondere am Element-Selektor ist seine globale und undifferenzierte Wirkung. Er ist wie ein Rundruf: „An alle Absätze auf dieser Seite: Ihr seid ab sofort blau!“ Diese Eigenschaft ist sowohl eine Stärke als auch eine Schwäche.

**Die Stärke:** Element-Selektoren sind perfekt geeignet, um grundlegende, seitenweite Stile zu definieren. Sie bilden das Fundament deines Designs. Du kannst damit eine einheitliche Typografie, grundlegende Abstände oder Standardfarben für bestimmte Elemente festlegen.

Ein sehr häufiger Anwendungsfall ist das Styling des `<body>`-Elements. Da fast alle sichtbaren Elemente innerhalb des `<body>` verschachtelt sind, werden viele seiner Stile (insbesondere solche, die die Schrift betreffen) an die Kind-Elemente vererbt.

```css
body {
  font-family: "Helvetica Neue", Arial, sans-serif;
  line-height: 1.6;
  background-color: #f4f4f4;
  color: #333;
}
```

Mit dieser einen Regel hast du bereits das grundlegende Erscheinungsbild deiner gesamten Seite definiert: eine saubere, serifenlose Schriftart, einen angenehmen Zeilenabstand für bessere Lesbarkeit, einen leicht grauen Hintergrund und eine dunkelgraue Schriftfarbe für den Haupttext.

**Die Schwäche:** Was passiert, wenn du nur *einen* bestimmten Absatz hervorheben möchtest? Vielleicht einen Warnhinweis, der rot sein soll. Ein Element-Selektor wie `p { color: red; }` würde *alle* Absätze rot färben, was du nicht willst. Er kann nicht zwischen verschiedenen Absätzen unterscheiden. Für solche spezifischen Aufgaben benötigst du präzisere Werkzeuge wie Klassen- oder ID-Selektoren, die wir in den folgenden Kapiteln kennenlernen werden.

#### Mehrere Element-Selektoren gruppieren

Stell dir vor, du möchtest allen Überschriften auf deiner Seite – also `<h1>`, `<h2>`, `<h3>` und so weiter – die gleiche Schriftart und Farbe geben. Du könntest für jede Überschriftenebene eine eigene Regel schreiben:

```css
/* Die umständliche Methode */
h1 {
  font-family: "Georgia", serif;
  color: #2c3e50;
}

h2 {
  font-family: "Georgia", serif;
  color: #2c3e50;
}

h3 {
  font-family: "Georgia", serif;
  color: #2c3e50;
}
```

Das funktioniert, ist aber sehr umständlich und wiederholt unnötig Code. CSS bietet hierfür eine elegante Lösung: Du kannst mehrere Selektoren durch ein Komma trennen, um ihnen denselben Deklarationsblock zuzuweisen.

```css
/* Die effiziente Methode */
h1, h2, h3 {
  font-family: "Georgia", serif;
  color: #2c3e50;
}
```

Das Komma agiert hier wie ein „und“. Die Regel lässt sich lesen als: „Wähle alle `<h1>`-Elemente **und** alle `<h2>`-Elemente **und** alle `<h3>`-Elemente aus und wende die folgenden Stile auf sie an.“ Das macht deinen Code deutlich kürzer, übersichtlicher und leichter zu warten.

#### Ein besonderer Fall: Der Universal-Selektor `*`

Neben den Selektoren für spezifische HTML-Tags gibt es noch einen besonderen Element-Selektor: den **Universal-Selektor**, dargestellt durch ein Sternchen (`*`).

Dieser Selektor wählt **jedes einzelne Element** im HTML-Dokument aus, ohne Ausnahme. Vom `<html>`-Wurzelelement über `<body>`, `<div>`, `<h1>`, `<p>` bis hin zum kleinsten `<span>` oder `<i>` – alles wird erfasst.

```css
* {
  border: 1px solid red;
}
```

Diese Regel würde um jedes einzelne Element auf deiner Seite einen roten Rahmen zeichnen. Das ist für das Design selten nützlich, aber fantastisch zum Debuggen, um zu sehen, welche Boxen wo genau auf der Seite liegen und wie viel Platz sie einnehmen.

Ein viel praktischerer Anwendungsfall für den Universal-Selektor ist das sogenannte „CSS Reset“. Browser haben standardmäßig voreingestellte Stile für viele Elemente (z. B. haben Absätze einen oberen und unteren Abstand, Überschriften sind fett und unterschiedlich groß). Diese Voreinstellungen können von Browser zu Browser leicht variieren. Um eine konsistentere Ausgangsbasis für das eigene Design zu schaffen, setzen viele Entwickler bestimmte Eigenschaften für alle Elemente auf einen neutralen Wert zurück.

Ein sehr bekanntes Beispiel ist die Anpassung des Box-Modells:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

Diese Regel sorgt dafür, dass die `width`- und `height`-Eigenschaften eines Elements immer die Innenabstände (`padding`) und den Rahmen (`border`) beinhalten, was die Layout-Gestaltung erheblich vereinfacht. Ohne hier zu tief in das Thema Box-Modell einzutauchen, zeigt dieses Beispiel, wie mächtig der Universal-Selektor für grundlegende, globale Anpassungen sein kann.

Du solltest ihn jedoch mit Bedacht einsetzen. Da er wirklich jedes Element anspricht, kann eine übermäßige Nutzung die Verarbeitungsgeschwindigkeit des Browsers (wenn auch heute nur noch marginal) beeinflussen. Für grundlegende Resets ist er aber ein etabliertes und wertvolles Werkzeug.

Element-Selektoren sind dein erster und wichtigster Schritt in die Welt des CSS. Sie bilden die breite Basis, auf der du aufbauen wirst. Sie sind perfekt, um den allgemeinen Ton und das Gefühl deiner Webseite zu definieren. Für die feineren Details und die spezifischen Ausnahmen wirst du bald weitere, schärfere Werkzeuge in deinem Repertoire haben.
