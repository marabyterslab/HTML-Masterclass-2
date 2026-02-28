# Namespace-Definitionen

### Das `<html>`-Element und die Welt der Namespaces

Nach dem Doctype ist das `<html>`-Element das erste wirkliche Tag in deinem Dokument. Es ist die Wurzel, der Stamm, aus dem alle anderen Äste – also alle anderen HTML-Elemente – wachsen. In seiner einfachsten Form sieht es so aus:

```html
<!DOCTYPE html>
<html lang="de">
  <!-- Hier kommt der Rest deines Dokuments -->
</html>
```

Das `lang`-Attribut hast du bereits kennengelernt; es gibt die primäre Sprache des Dokuments an und ist wichtig für Barrierefreiheit und Suchmaschinen. Doch manchmal siehst du in älteren Beispielen oder in speziellen Anwendungsfällen noch ein weiteres, auf den ersten Blick kryptisch wirkendes Attribut: `xmlns`.

```html
<!-- Ein Beispiel im XHTML-Stil -->
<html xmlns="http://www.w3.org/1999/xhtml" lang="de">
  ...
</html>
```

Was hat es mit diesem `xmlns` auf sich und warum taucht es in den meisten modernen HTML5-Dokumenten nicht mehr auf? Um das zu verstehen, müssen wir einen kleinen Ausflug in die Welt der Namespaces machen.

#### Das Problem der Namensgleichheit

Stell dir vor, du schreibst ein Dokument, in dem du nicht nur reines HTML verwendest, sondern auch andere spezialisierte Auszeichnungssprachen einbettest. Zwei sehr prominente Beispiele dafür sind SVG (Scalable Vector Graphics) zur Darstellung von Vektorgrafiken und MathML (Mathematical Markup Language) zur Darstellung mathematischer Formeln.

Sowohl HTML als auch SVG kennen beispielsweise ein `<title>`-Element. In HTML ist `<title>` das Element im `<head>`, das den Titel der Webseite für den Browser-Tab definiert. In SVG hingegen beschreibt `<title>` den Titel einer Grafik, der oft als Tooltip angezeigt wird, wenn du mit der Maus darüberfährst.

Wenn ein Browser nun auf ein `<title>`-Tag stößt, woher soll er wissen, welche Art von Titel gemeint ist? Der HTML-Titel für den Tab oder der SVG-Titel für die Grafik?

Genau hier kommen Namespaces (auf Deutsch: Namensräume) ins Spiel. Ein Namespace ist wie ein Nachname für Element-Typen. Er schafft einen eindeutigen Kontext und verhindert Kollisionen. Man sagt dem Browser quasi: "Dieses `<title>` hier gehört zur Familie 'HTML', und jenes `<title>` dort drüben gehört zur Familie 'SVG'."

#### Die Lösung: Der `xmlns`-Identifikator

Um einen Namespace zu deklarieren, wird das `xmlns`-Attribut verwendet, was für "XML Namespace" steht. Der Wert dieses Attributs ist eine URL, die als eindeutiger Identifikator (ein sogenannter Uniform Resource Identifier, URI) für die jeweilige Sprache dient.

Ein wichtiger Punkt, der oft für Verwirrung sorgt: **Diese URL ist nur ein Name, kein Link!** Wenn du versuchst, `http://www.w3.org/1999/xhtml` in deinem Browser zu öffnen, landest du zwar auf einer Webseite, aber das ist für die Funktion des Namespaces irrelevant. Der Browser ruft diese Adresse nicht auf. Er nutzt die Zeichenkette lediglich, um die Sprache eindeutig zu identifizieren, so wie eine Personalausweisnummer eine Person eindeutig identifiziert.

In der Ära von XHTML, einem strengeren, auf XML-Regeln basierenden HTML, war es Pflicht, den HTML-Namespace explizit auf dem `<html>`-Wurzelelement anzugeben:

```html
<html xmlns="http://www.w3.org/1999/xhtml">
```

Damit wurde unmissverständlich klargemacht: Alle Elemente in diesem Dokument, die kein anderes Präfix haben, gehören zum Vokabular von XHTML.

#### Und warum fehlt das in modernem HTML5?

Mit der Einführung von HTML5 hat sich der Umgang damit vereinfacht. Der moderne HTML-Parser, den alle Browser heute verwenden, ist nicht mehr strikt auf XML angewiesen. Wenn du dein Dokument mit `<!DOCTYPE html>` beginnst, schaltet der Browser in den Standard-Modus und **weiß automatisch**, dass alle Elemente wie `<html>`, `<body>`, `<p>` oder `<h1>` zum HTML-Namespace gehören. Der Namespace `http://www.w3.org/1999/xhtml` wird also **implizit angenommen**.

Du musst ihn nicht mehr deklarieren. Es ist, als wärst du auf einer Familienfeier der Familie "HTML": Solange niemand explizit sagt, dass er zu einer anderen Familie gehört, gehen alle davon aus, dass jeder Anwesende ein "HTML" ist.

Deshalb ist die `xmlns`-Deklaration auf dem `<html>`-Tag für ein reines HTML5-Dokument überflüssig und wird korrekterweise weggelassen.

#### Inseln in deinem HTML-Ozean: SVG und MathML

Die Sache wird wieder relevant, sobald du tatsächlich andere Sprachen in dein HTML einbettest. Stell dir dein HTML-Dokument als einen großen Ozean vor. Nun möchtest du eine Insel für eine Vektorgrafik (SVG) oder eine für eine mathematische Formel (MathML) erschaffen.

Für diese "Inseln" musst du explizit den richtigen Namespace deklarieren, damit der Browser versteht, wie er die Elemente darin interpretieren soll.

**Beispiel mit SVG:**

```html
<body>
  <h1>Ein einfacher Kreis</h1>
  <svg width="100" height="100" xmlns="http://www.w3.org/2000/svg">
    <circle cx="50" cy="50" r="40" stroke="black" stroke-width="3" fill="red" />
  </svg>
</body>
```

Hier teilt das `xmlns="http://www.w3.org/2000/svg"` auf dem `<svg>`-Tag dem Browser mit: "Achtung, alles innerhalb dieses `<svg>`-Blocks gehört zur Welt der Scalable Vector Graphics. Das `<circle>`-Element ist also kein unbekanntes HTML-Tag, sondern ein SVG-Kreis."

**Beispiel mit MathML:**

```html
<body>
  <p>Die Formel des Pythagoras:</p>
  <math xmlns="http://www.w3.org/1998/Math/MathML">
    <mrow>
      <msup><mi>a</mi><mn>2</mn></msup>
      <mo>+</mo>
      <msup><mi>b</mi><mn>2</mn></msup>
      <mo>=</mo>
      <msup><mi>c</mi><mn>2</mn></msup>
    </mrow>
  </math>
</body>
```

Auch hier signalisiert das `xmlns` auf dem `<math>`-Tag: "Ab hier gelten die Regeln und Elemente von MathML." Der Browser weiß dadurch, wie er die verschachtelten Elemente als Formel rendern muss.

#### Wenn eine Sprache nicht reicht: Namespace-Präfixe

Manchmal möchtest du nicht ganze Blöcke, sondern nur einzelne Attribute aus einer anderen Sprache verwenden. Ein gängiges Beispiel ist die Einbindung von Metadaten für soziale Netzwerke über das Open Graph Protocol (OGP).

Hierfür werden Namespace-Präfixe verwendet. Du deklarierst auf dem `<html>`-Element einen zusätzlichen Namespace, gibst ihm aber einen Kurznamen (ein Präfix).

```html
<html lang="de" prefix="og: http://ogp.me/ns#">
<head>
  <title>Meine tolle Webseite</title>
  <meta property="og:title" content="Meine tolle Webseite" />
  <meta property="og:type" content="website" />
  <meta property="og:url" content="https://www.beispiel.de/" />
  <meta property="og:image" content="https://www.beispiel.de/bild.jpg" />
</head>
<body>
  ...
</body>
</html>
```

In diesem modernen Beispiel wird das `prefix`-Attribut verwendet, das für solche Zwecke in HTML5 vorgesehen ist. Die ältere, XML-basierte Schreibweise würde so aussehen:

```html
<html lang="de" xmlns:og="http://ogp.me/ns#">
```

Beide Varianten erreichen dasselbe: Sie definieren das Präfix `og`. Wenn der Browser nun auf ein Attribut wie `property="og:title"` stößt, weiß er durch das Präfix `og:`, dass `title` hier im Kontext des Open Graph Protocols gemeint ist und nicht mit einem HTML-eigenen Attribut verwechselt werden darf. Das `property`-Attribut selbst wird hier genutzt, um diese Information maschinenlesbar zu machen.

#### Für die Puristen: Polyglottes Markup

Es gibt eine Nische, in der du heute noch `xmlns` auf dem `<html>`-Tag in einem modernen Dokument sehen könntest: bei sogenanntem "polyglotten Markup". Das ist der Versuch, ein Dokument so zu schreiben, dass es sowohl als HTML5 als auch als valides XML (genauer: XHTML5) verarbeitet werden kann. Für eine solche XML-Kompatibilität ist die explizite Deklaration des HTML-Namespaces auf dem Wurzelelement erforderlich.

```html
<!DOCTYPE html>
<html lang="de" xmlns="http://www.w3.org/1999/xhtml">
  ...
</html>
```

Für die allermeisten Webprojekte im Alltag ist dieser Ansatz jedoch nicht notwendig. Die standardmäßige, einfache HTML5-Syntax ohne `xmlns` auf dem `<html>`-Tag ist der etablierte und empfohlene Weg.

Die Welt der Namespaces zeigt eindrücklich, wie HTML nicht in einem Vakuum existiert, sondern als Teil eines größeren Ökosystems von Webtechnologien konzipiert ist. Es stellt sicher, dass verschiedene Sprachen harmonisch im selben Dokument koexistieren können, ohne sich gegenseitig in die Quere zu kommen. Für deine tägliche Arbeit bedeutet das vor allem: Lass das `xmlns` auf dem `<html>`-Tag weg, es sei denn, du bettest explizit Sprachen wie SVG oder MathML ein – dann gehört es aber auf deren jeweiliges Wurzelelement.
