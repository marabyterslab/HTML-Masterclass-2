# Syntax-Grundlagen

### Syntax-Grundlagen: Die Bausteine von HTML

Um eine Sprache zu lernen, musst du zuerst ihr Alphabet und ihre Grammatik verstehen. Bei HTML ist das nicht anders. Statt Buchstaben und Satzzeichen verwenden wir hier jedoch sogenannte Tags, Elemente und Attribute. Diese Bausteine bilden die grundlegende Syntax, also die Regeln, nach denen ein gültiges HTML-Dokument aufgebaut ist. Wenn du diese Regeln einmal verinnerlicht hast, wird dir das Schreiben von HTML ganz natürlich von der Hand gehen. Es ist wie das Erlernen eines einfachen Baukastensystems: Du hast verschiedene Steine und klare Regeln, wie du sie zusammensetzen darfst.

#### Tags: Die Befehle für den Browser

Das Herzstück von HTML sind die **Tags**. Ein Tag ist im Grunde ein Befehl, den du in spitze Klammern (`<` und `>`) einschließt. Dieser Befehl sagt dem Webbrowser, wie er einen bestimmten Inhalt interpretieren und darstellen soll. Soll ein Text ein Absatz sein? Eine Überschrift? Ein Link? All das definierst du mit Tags.

Die meisten Tags treten als Paar auf: ein **öffnender Tag** (Opening Tag) und ein **schließender Tag** (Closing Tag).

Der öffnende Tag leitet einen Inhaltsbereich ein. Er besteht aus dem Namen des Tags in spitzen Klammern. Ein Absatz wird zum Beispiel mit `<p>` eingeleitet (das „p“ steht für „paragraph“, englisch für Absatz).

```html
<p>
```

Der schließende Tag beendet diesen Bereich. Er sieht fast genauso aus wie der öffnende Tag, enthält aber direkt nach der ersten spitzen Klammer einen Schrägstrich (`/`).

```html
</p>
```

Alles, was zwischen dem öffnenden und dem schließenden Tag steht, ist der Inhalt, auf den sich der Befehl bezieht. Der Browser weiß also: Alles zwischen `<p>` und `</p>` gehört zu diesem einen Absatz.

#### Elemente: Das Gesamtpaket

Wenn wir von einem **HTML-Element** sprechen, meinen wir die gesamte Konstruktion: den öffnenden Tag, den Inhalt und den schließenden Tag.

```html
<p>Dies ist der Inhalt eines Absatzes.</p>
```

In diesem Beispiel ist `<p>Dies ist der Inhalt eines Absatzes.</p>` ein komplettes `p`-Element. `<p>` ist der öffnende Tag, `</p>` ist der schließende Tag, und „Dies ist der Inhalt eines Absatzes.“ ist der Inhalt des Elements.

Diese Unterscheidung zwischen „Tag“ und „Element“ ist wichtig für das fachliche Verständnis. Ein Tag ist nur die Markierung am Anfang oder Ende, während das Element die gesamte Einheit darstellt.

#### Attribute: Zusatzinformationen für Elemente

Manchmal reicht ein einfacher Befehl wie „Sei ein Absatz!“ nicht aus. Wir müssen einem Element zusätzliche Informationen oder Eigenschaften mit auf den Weg geben. Dafür gibt es **Attribute**.

Ein Attribut ist eine Zusatzinformation, die immer im öffnenden Tag eines Elements platziert wird. Es besteht aus zwei Teilen: einem **Attributnamen** und einem **Attributwert**, der in Anführungszeichen (entweder doppelte `"` oder einfache `'`) gesetzt wird. Die allgemeine Form lautet: `name="wert"`.

Ein klassisches Beispiel ist der Link. Ein Link wird mit dem `<a>`-Tag erstellt (das „a“ steht für „anchor“, also Anker). Damit der Browser weiß, wohin der Link führen soll, braucht er eine Zieladresse. Diese geben wir ihm mit dem `href`-Attribut („hypertext reference“).

```html
<a href="https://www.wikipedia.org">Besuche Wikipedia</a>
```

Hier ist `<a>` der öffnende Tag, der den Inhalt „Besuche Wikipedia“ zu einem Link macht. Das Attribut `href` mit dem Wert `"https://www.wikipedia.org"` teilt dem Browser das genaue Ziel mit.

Ein weiteres häufiges Beispiel ist das Bild-Element `<img>`. Um ein Bild anzuzeigen, musst du dem Browser sagen, wo er die Bilddatei findet. Das geschieht über das `src`-Attribut („source“, Quelle).

```html
<img src="bilder/sonnenuntergang.jpg">
```

Ein Element kann auch mehrere Attribute haben. Diese werden einfach durch Leerzeichen voneinander getrennt im öffnenden Tag notiert. Die Reihenfolge der Attribute spielt dabei keine Rolle.

```html
<a href="https://example.com" title="Besuche die Beispiel-Webseite" target="_blank">Ein Link</a>
```

#### Verschachtelung: Elemente in Elementen

Eine Webseite besteht selten nur aus einer flachen Liste von Elementen. Stattdessen bauen wir komplexe Strukturen, indem wir Elemente ineinander **verschachteln** (Nesting). Das bedeutet, ein komplettes Element befindet sich innerhalb des Inhaltsbereichs eines anderen Elements.

Stell dir das wie russische Matrjoschka-Puppen oder ineinander gestapelte Kisten vor. Du öffnest eine große Kiste, und darin befindet sich eine kleinere Kiste.

Ein gängiges Beispiel ist eine Liste. Eine ungeordnete Liste wird mit dem `<ul>`-Element erstellt („unordered list“). Jeder einzelne Listenpunkt innerhalb dieser Liste ist ein `<li>`-Element („list item“). Die `<li>`-Elemente sind also in das `<ul>`-Element verschachtelt:

```html
<ul>
  <li>Erster Listenpunkt</li>
  <li>Zweiter Listenpunkt</li>
  <li>Dritter Listenpunkt</li>
</ul>
```

Die Einrückung im Code ist hierbei nur für uns Menschen gedacht, um die Struktur besser lesen zu können. Dem Browser ist sie egal. Wichtig ist jedoch die korrekte Reihenfolge der schließenden Tags. Das zuletzt geöffnete Element muss immer als Erstes wieder geschlossen werden.

**Korrekt:**
```html
<p>Dieser Text ist <strong>wichtig</strong>.</p>
```
Hier wird `<strong>` innerhalb von `<p>` geöffnet und auch wieder innerhalb von `<p>` geschlossen.

**Falsch:**
```html
<p>Dieser Text ist <strong>wichtig.</p></strong>
```
Hier werden die Tags überkreuz geschlossen. Das führt zu unvorhersehbarem Verhalten und ist invalides HTML.

#### Leere Elemente: Die Ausnahmen

Während die meisten Elemente Inhalt umschließen und daher ein öffnendes und ein schließendes Tag benötigen, gibt es einige Ausnahmen: die **leeren Elemente** (Empty Elements oder Void Elements).

Diese Elemente haben keinen Inhalt und bestehen daher nur aus einem einzigen Tag. Sie fügen etwas an einer bestimmten Stelle in das Dokument ein, umschließen aber nichts.

Die bekanntesten Beispiele sind:
*   `<img>`: Fügt ein Bild ein.
*   `<br>`: Erzeugt einen Zeilenumbruch („break“).
*   `<hr>`: Zeichnet eine thematische Trennlinie („horizontal rule“).
*   `<input>`: Erstellt ein Eingabefeld in einem Formular.

Ein leeres Element hat also keinen schließenden Tag.

```html
<p>Dies ist die erste Zeile.<br>Und dies die zweite.</p>

<hr>

<img src="logo.png" alt="Firmenlogo">
```
Du wirst manchmal eine Schreibweise mit einem Schrägstrich am Ende sehen, wie `<br />` oder `<hr />`. Diese Schreibweise stammt aus XHTML, einem strengeren Verwandten von HTML. In modernem HTML5 ist dieser Schrägstrich optional und hat keine technische Funktion. Er schadet aber auch nicht.

#### Die grundlegende Dokumentenstruktur

Jedes HTML-Dokument folgt einer grundlegenden, standardisierten Struktur. Diese Struktur stellt sicher, dass Browser auf der ganzen Welt deine Seite korrekt interpretieren können. Ein minimales HTML-Dokument sieht so aus:

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Titel der Seite</title>
</head>
<body>
  <h1>Meine erste Überschrift</h1>
  <p>Mein erster Absatz.</p>
</body>
</html>
```

Lass uns das kurz aufschlüsseln:

1.  **`<!DOCTYPE html>`**: Dies ist die Dokumenttyp-Deklaration. Sie ist kein HTML-Tag, sondern eine Anweisung an den Browser, die ganz am Anfang stehen muss. Sie sagt ihm: „Achtung, was jetzt kommt, ist ein modernes HTML5-Dokument.“

2.  **`<html>`**: Dies ist das Wurzelelement (Root Element). Alle anderen Elemente auf der Seite müssen innerhalb dieses Elements verschachtelt sein. Das Attribut `lang="de"` gibt an, dass die Hauptsprache der Seite Deutsch ist.

3.  **`<head>`**: Der „Kopf“-Bereich. Die Inhalte hier sind für den Besucher der Webseite nicht direkt sichtbar (mit Ausnahme des Titels). Hier stehen Metadaten, also Informationen *über* die Webseite.
    *   **`<meta charset="UTF-8">`**: Legt die Zeichenkodierung fest. UTF-8 ist der universelle Standard, der sicherstellt, dass Umlaute (ä, ö, ü) und Sonderzeichen korrekt dargestellt werden.
    *   **`<title>`**: Definiert den Titel der Seite, der im Browser-Tab oder in den Lesezeichen angezeigt wird.

4.  **`<body>`**: Der „Körper“-Bereich. Alles, was du hier hineinschreibst – Überschriften, Texte, Bilder, Links –, ist der sichtbare Inhalt deiner Webseite.

#### Kommentare: Notizen für dich und andere

Manchmal möchtest du dir Notizen direkt im Code machen. Vielleicht, um einen komplexen Abschnitt zu erklären oder um ein Stück Code vorübergehend zu deaktivieren, ohne es zu löschen. Dafür gibt es HTML-Kommentare.

Ein Kommentar beginnt mit `<!--` und endet mit `-->`. Alles, was dazwischen steht, wird vom Browser komplett ignoriert und nicht auf der Webseite angezeigt.

```html
<!-- Dies ist ein einzeiliger Kommentar. -->

<p>Dieser Absatz wird ganz normal angezeigt.</p>

<!-- 
  Hier beginnt ein Bereich, den wir später noch bearbeiten müssen.
  Aktuell ist die Navigation noch nicht fertig.
  <nav>
    ...
  </nav>
-->
```

Kommentare sind ein wertvolles Werkzeug, um deinen Code für dich selbst und für andere Entwickler verständlich und wartbar zu halten.

Mit diesen Grundlagen – Tags, Elemente, Attribute, Verschachtelung und der grundlegenden Dokumentenstruktur – hast du das Rüstzeug, um die Sprache von HTML zu verstehen und deine ersten eigenen Webseiten zu strukturieren. Jedes komplexe Web-Layout, das du siehst, basiert auf genau diesen einfachen Bausteinen.
