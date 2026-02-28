# Validität und Konformität

### Validität und Konformität: Das Regelwerk des Webs

Stell dir vor, du baust ein Haus. Du würdest nicht einfach anfangen, Ziegel aufeinanderzuschichten und hoffen, dass am Ende etwas Stabiles dabei herauskommt. Du würdest einen Bauplan verwenden – eine detaillierte Anleitung, die genau vorschreibt, wo jede Wand, jede Tür und jedes Fenster hingehört. Dieser Bauplan sorgt dafür, dass das Haus nicht nur stabil ist, sondern auch von jedem Handwerker verstanden wird, der daran arbeitet.

Im Web ist es ganz ähnlich. Dein HTML-Dokument ist das Haus und die Webstandards, die vom World Wide Web Consortium (W3C) und der Web Hypertext Application Technology Working Group (WHATWG) festgelegt werden, sind der Bauplan. Die Begriffe "Validität" und "Konformität" beschreiben, wie genau du dich an diesen Plan hältst. Sie sind keine Schikane für Entwickler, sondern das Fundament für ein funktionierendes, zugängliches und zukunftssicheres Internet.

#### Was bedeutet Validität?

Im Kern ist Validität eine Frage der Grammatik und Syntax. Ein valides HTML-Dokument ist ein Dokument, das die Regeln der spezifischen HTML-Version, die du verwendest, zu 100 % einhält. Jedes Tag ist korrekt geöffnet und geschlossen, Attribute sind richtig geschrieben und Elemente sind nicht an Stellen verschachtelt, wo sie nicht hingehören.

Die erste und wichtigste Regel zur Sicherstellung der Validität ist die Angabe des Dokumententyps, der sogenannte **DOCTYPE**. Diese eine Zeile Code, die ganz am Anfang deines HTML-Dokuments stehen muss, ist wie die Titelseite deines Bauplans. Sie teilt dem Browser mit: "Achtung, was jetzt kommt, ist ein HTML-Dokument und es folgt den Regeln von HTML5."

Für modernes HTML sieht das so aus:

```html
<!DOCTYPE html>
```

Das war's schon. Diese einfache Deklaration versetzt den Browser in den "Standards-Modus", in dem er versucht, den Code so exakt wie möglich nach den aktuellen Webstandards zu interpretieren. Ohne diesen DOCTYPE würde der Browser in den sogenannten "Quirks-Modus" verfallen, einen Kompatibilitätsmodus, der versucht, auch alten, fehlerhaften Code irgendwie darzustellen. Das führt oft zu unvorhersehbarem und inkonsistentem Verhalten – ein Albtraum für jeden Entwickler.

Ein valides HTML-Dokument folgt also konsequent den definierten Regeln. Warum ist das so wichtig?

1.  **Vorhersehbarkeit und Konsistenz:** Wenn dein Code valide ist, weißt du, dass alle modernen Browser ihn auf die gleiche, vorhersagbare Weise interpretieren werden. Du reduzierst das Risiko von seltsamen Darstellungsfehlern, die nur in einem bestimmten Browser auftreten.
2.  **Fehlervermeidung:** Der Prozess der Validierung deckt Tippfehler und einfache logische Fehler auf, bevor sie zu einem größeren Problem werden. Ein vergessener schließender Tag kann das Layout einer ganzen Seite zerstören. Ein Validator findet diesen Fehler in Sekunden.
3.  **Zukunftssicherheit:** Code, der sich an Standards hält, hat eine viel höhere Wahrscheinlichkeit, auch in zukünftigen Browser-Versionen und auf neuen Geräten korrekt zu funktionieren. Du baust auf einem soliden Fundament.
4.  **Professionalität:** Das Liefern von validem Code ist ein Zeichen von handwerklicher Sorgfalt. Es zeigt, dass du dein Handwerk verstehst und Wert auf Qualität legst.

#### Der Validator: Dein digitaler Bauinspektor

Um zu überprüfen, ob dein HTML-Code valide ist, musst du ihn nicht Zeile für Zeile mit der offiziellen Spezifikation vergleichen. Dafür gibt es automatisierte Werkzeuge: die Validatoren. Der bekannteste und offizielle ist der **W3C Markup Validation Service**.

Du kannst ihm entweder eine URL zu deiner Webseite geben, eine Datei hochladen oder deinen Code direkt in ein Textfeld kopieren. Der Validator agiert dann wie ein unbestechlicher Bauinspektor: Er geht deinen Code Zeile für Zeile durch und vergleicht ihn mit den Regeln, die durch deinen DOCTYPE festgelegt wurden.

Am Ende bekommst du einen Bericht. Im Idealfall siehst du eine grüne Erfolgsmeldung. Viel häufiger, besonders am Anfang, siehst du eine Liste von Fehlern und Warnungen. Aber keine Sorge, das ist kein Scheitern, sondern ein extrem nützliches Werkzeug zum Lernen und Verbessern. Jeder Fehler wird mit einer Zeilennummer und einer Beschreibung gemeldet, was genau das Problem ist und oft auch, wie du es beheben kannst.

Schauen wir uns ein kleines, fehlerhaftes Beispiel an:

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Ein fehlerhaftes Dokument</title>
</head>
<body>
  <h1>Meine Überschrift
  <p>Hier ist ein <b>fett gedruckter Text und ein <div>Block-Element</div></b>.</p>
  <img src="bild.jpg">
</body>
</html>
```

Ein Validator würde hier mehrere Probleme finden:

*   **Fehler:** Das `<h1>`-Element wurde nicht mit `</h1>` geschlossen.
*   **Fehler:** Ein `<div>`-Element, das ein Block-Element ist, darf nicht innerhalb eines `<b>`-Elements stehen, das primär für Textformatierung (Phrasing Content) gedacht ist.
*   **Warnung/Fehler:** Dem `<img>`-Element fehlt das `alt`-Attribut, das für die Barrierefreiheit unerlässlich ist, um eine Textalternative für das Bild bereitzustellen.

Indem du diese Fehler behebst, machst du deinen Code nicht nur valide, sondern auch robuster und zugänglicher.

#### Konformität: Mehr als nur gültige Syntax

Wenn Validität die Einhaltung der Grammatik ist, dann ist Konformität die Einhaltung der Semantik – der Bedeutung. Ein HTML-Dokument kann technisch valide sein, aber dennoch nicht konform, wenn die Elemente nicht ihrem eigentlichen Zweck entsprechend verwendet werden.

Denk an einen grammatikalisch korrekten Satz, der aber keinen Sinn ergibt, wie: "Die grüne Idee schläft wütend." Alle Wörter sind korrekt geschrieben und die Satzstruktur stimmt, aber die Bedeutung ist Unsinn.

In HTML wäre ein Beispiel dafür die Verwendung eines `<blockquote>`-Elements, nur um einen Text einzurücken, weil es standardmäßig einen visuellen Einzug hat.

```html
<!-- Valide, aber nicht konform -->
<blockquote>
  <p>Ich bin kein Zitat, ich wollte nur eingerückt werden.</p>
</blockquote>
```

Technisch gesehen ist dieser Code valide. Es gibt keinen Syntaxfehler. Aber er ist nicht konform, weil `<blockquote>` semantisch für die Auszeichnung eines längeren, zitierten Abschnitts aus einer anderen Quelle vorgesehen ist. Für einen rein visuellen Einzug solltest du CSS verwenden.

Warum ist diese Unterscheidung so wichtig?

1.  **Barrierefreiheit (Accessibility):** Das ist der wichtigste Grund. Assistive Technologien wie Screenreader, die von Menschen mit Sehbehinderungen genutzt werden, verlassen sich auf die semantische Bedeutung von HTML-Elementen, um den Inhalt einer Seite zu interpretieren und vorzulesen. Ein Screenreader kündigt ein `<blockquote>` als Zitat an. Wenn du es missbrauchst, verwirrst du den Nutzer. Eine Überschrift, die nur mit `<div>` und CSS groß gemacht wurde, wird nicht als Überschrift erkannt, was die Navigation auf der Seite unmöglich machen kann.
2.  **Suchmaschinenoptimierung (SEO):** Suchmaschinen wie Google sind deine wichtigsten "blinden" Nutzer. Sie analysieren die semantische Struktur deiner Seite, um den Inhalt zu verstehen und zu bewerten. Eine korrekte Verwendung von Überschriften (`<h1>` bis `<h6>`), Listen (`<ul>`, `<ol>`) und anderen semantischen Elementen hilft Suchmaschinen, die Relevanz und Hierarchie deiner Inhalte zu erfassen, was sich positiv auf dein Ranking auswirken kann.
3.  **Wartbarkeit:** Code, der semantisch korrekt ist, ist selbsterklärend. Wenn du oder ein Kollege in sechs Monaten auf den Code schauen, wisst ihr sofort, was ein `<nav>`-Block oder ein `<article>`-Element bedeutet, ohne euch durch CSS-Klassen wühlen zu müssen.

Ein konformes Dokument ist also nicht nur syntaktisch korrekt (valide), sondern nutzt auch jedes HTML-Element für den Zweck, für den es geschaffen wurde.

#### Pragmatismus in der Praxis

Muss jede einzelne Webseite auf der Welt zu jeder Zeit zu 100 % valide sein? In der realen Welt gibt es Grauzonen. Moderne Browser sind extrem fehlertolerant. Sie versuchen ihr Bestes, auch kaputten Code sinnvoll darzustellen. Diese "Fehlerkorrektur" ist ein Segen und ein Fluch zugleich. Sie sorgt dafür, dass das Web nicht zusammenbricht, verleitet aber auch zu Nachlässigkeit.

Das Ziel sollte nicht sein, "grüne Haken" im Validator zu sammeln, nur um der Sache willen. Das Ziel ist es, eine robuste, zugängliche und wartbare Webseite zu erstellen. Validierung ist eines der besten Werkzeuge auf dem Weg dorthin.

Verstehe die Regeln, damit du weißt, wann du sie bewusst und mit gutem Grund vielleicht einmal leicht biegst (was selten vorkommen sollte). Nutze den Validator als deinen Assistenten, der dich auf Flüchtigkeitsfehler und echte Probleme aufmerksam macht. Strebe immer nach Konformität, denn semantisch korrekter Code ist die Grundlage für ein offenes und für alle zugängliches Web. Ein Haus, das nach einem soliden Plan gebaut wurde, übersteht nicht nur den nächsten Sturm, sondern ist auch für zukünftige Generationen ein angenehmer und sicherer Ort. Dasselbe gilt für deinen Code.
