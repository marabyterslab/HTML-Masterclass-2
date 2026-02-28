# Syntax-Grundlagen

### Die Bausteine des Webs: Eine Einführung in die HTML-Syntax

Wenn du eine Sprache lernst, beginnst du mit den Grundlagen: Buchstaben, Wörter und Satzbau. Bei HTML ist es ganz ähnlich. Statt Wörtern verwenden wir „Tags“, um dem Browser mitzuteilen, wie er Inhalte strukturieren und darstellen soll. Die Regeln, nach denen diese Tags geschrieben und kombiniert werden, nennen wir Syntax. Das Schöne an HTML ist, dass seine Syntax bemerkenswert einfach und logisch ist. Lass uns diese Grundbausteine Schritt für Schritt erkunden.

#### Tags: Die Befehle für den Browser

Der Kern von HTML sind die Tags. Ein Tag ist im Grunde ein in spitze Klammern (`<` und `>`) eingeschlossener Befehl. Stell dir vor, du möchtest eine Überschrift erster Ordnung erstellen – die wichtigste Überschrift auf deiner Seite. Dafür gibt es den Tag `<h1>`.

Die meisten HTML-Tags treten paarweise auf:

1.  **Ein öffnender Tag (Opening Tag):** Er markiert den Anfang eines Inhaltsbereichs. Zum Beispiel: `<h1>`.
2.  **Ein schließender Tag (Closing Tag):** Er markiert das Ende dieses Bereichs. Er sieht fast genauso aus wie der öffnende Tag, enthält aber einen Schrägstrich (`/`) direkt nach der ersten spitzen Klammer. Zum Beispiel: `</h1>`.

Alles, was zwischen diesen beiden Tags steht, wird vom Browser entsprechend interpretiert.

```html
<h1>Das ist eine Hauptüberschrift</h1>
```

In diesem Beispiel weiß der Browser, dass der Text „Das ist eine Hauptüberschrift“ als wichtigste Überschrift der Seite formatiert werden soll. Das Gleiche gilt für Absätze (`<p>`), Listen (`<ul>`, `<ol>`, `<li>`) und viele andere Elemente.

```html
<p>Dies ist ein ganz normaler Textabsatz.</p>
```

Die Kombination aus öffnendem Tag, Inhalt und schließendem Tag wird als **HTML-Element** bezeichnet. Der Tag ist also nur der Befehlsteil, während das Element das gesamte Konstrukt ist.

#### Verschachtelung: Elemente in Elementen

Selten besteht eine Webseite nur aus einer Aneinanderreihung einzelner Elemente. Meistens sind diese logisch ineinander verschachtelt. Stell dir das wie russische Matrjoschka-Puppen oder Kisten in Kisten vor. Du kannst Elemente in andere Elemente einbetten, um komplexere Strukturen zu schaffen.

Die wichtigste Regel bei der Verschachtelung lautet: **Was du zuletzt öffnest, musst du zuerst schließen.**

Ein korrekt verschachteltes Beispiel:

```html
<div>
  <h2>Eine Unterüberschrift</h2>
  <p>Dieser Absatz gehört zur Unterüberschrift und befindet sich ebenfalls im div-Container.</p>
</div>
```

Hier wird zuerst das `<div>`-Element geöffnet, das als allgemeiner Container dient. Darin werden ein `<h2>`- und ein `<p>`-Element geöffnet und wieder geschlossen. Erst danach wird das äußere `<div>`-Element geschlossen. Die Reihenfolge ist logisch und sauber.

Ein falsches Beispiel würde so aussehen:

```html
<!-- FALSCH! So nicht! -->
<p>Dieser Satz beginnt in einem Absatz, <strong>aber die Verschachtelung ist falsch.</p></strong>
```

Der Browser würde hier versuchen, das Durcheinander zu interpretieren, aber das Ergebnis wäre unvorhersehbar. Die korrekte Reihenfolge wäre, zuerst das `<strong>`-Element zu schließen, da es als letztes geöffnet wurde:

```html
<!-- KORREKT! -->
<p>Dieser Satz beginnt in einem Absatz, <strong>und die Verschachtelung ist richtig.</strong></p>
```

Diese saubere Struktur ist nicht nur für den Browser wichtig, sondern auch für dich, damit du den Überblick über deinen Code behältst.

#### Attribute: Zusatzinformationen für deine Tags

Manchmal reicht ein einfacher Tag nicht aus. Du möchtest einem Element vielleicht zusätzliche Informationen mitgeben. Hier kommen Attribute ins Spiel. Attribute sind kleine Zusatzanweisungen, die immer **im öffnenden Tag** platziert werden.

Sie folgen stets dem gleichen Muster: `attributname="wert"`.

Ein klassisches Beispiel ist der Link (oder Anker-Tag `<a>`). Ein `<a>`-Tag allein weiß nicht, wohin er führen soll. Wir müssen ihm das Ziel über das `href`-Attribut (Hypertext Reference) mitteilen.

```html
<a href="https://www.beispiel.de">Klicke hier, um zur Beispielseite zu gelangen</a>
```

Hier ist `href` der Attributname und `"https://www.beispiel.de"` der Wert. Der Wert wird fast immer in Anführungszeichen gesetzt – entweder doppelte (`"`) oder einfache (`'`). Die Konvention ist, doppelte Anführungszeichen zu verwenden.

Ein weiteres wichtiges Beispiel ist das Bild-Element `<img>`. Es benötigt das `src`-Attribut (Source), um zu wissen, welche Bilddatei angezeigt werden soll, und das `alt`-Attribut (Alternativtext) für Barrierefreiheit.

```html
<img src="bilder/logo.png" alt="Logo der Firma Beispiel AG">
```

Du kannst einem Tag auch mehrere Attribute geben, indem du sie durch Leerzeichen trennst. Die Reihenfolge der Attribute spielt dabei keine Rolle.

```html
<a href="https://www.beispiel.de" target="_blank" title="Besuche die Beispielseite">Ein Link</a>
```

#### Leere Elemente: Tags ohne Inhalt

Während die meisten Elemente Inhalt umschließen und daher einen schließenden Tag benötigen, gibt es einige Ausnahmen. Diese nennt man leere Elemente (Void Elements). Sie stehen für sich allein, da sie keinen textuellen Inhalt umklammern können.

Typische Beispiele sind:
*   `<img>`: Fügt ein Bild ein. Das Bild ist die Information, es gibt keinen Text dazwischen.
*   `<br>`: Erzeugt einen Zeilenumbruch.
*   `<hr>`: Zeichnet eine horizontale Trennlinie.
*   `<input>`: Erstellt ein Eingabefeld in einem Formular.
*   `<meta>`: Definiert Metadaten über das Dokument.

Da diese Elemente keinen Inhalt umschließen, benötigen sie keinen schließenden Tag.

```html
<p>Dies ist die erste Zeile.<br>Und dies ist die zweite Zeile.</p>
<hr>
<img src="bild.jpg" alt="Ein schönes Bild">
```

Früher, zu Zeiten von XHTML, war es üblich, diese leeren Elemente mit einem Schrägstrich am Ende zu kennzeichnen, z. B. `<br />` oder `<img src="..." />`. In modernem HTML5 ist dieser Schrägstrich optional. Du kannst ihn verwenden, wenn es dir hilft, den Code klarer zu finden, aber er ist nicht mehr erforderlich.

#### Kommentare: Notizen für dich und andere

Manchmal möchtest du Notizen in deinem Code hinterlassen – sei es, um einen komplexen Abschnitt zu erklären, eine Erinnerung für später zu hinterlassen oder einen Teil des Codes vorübergehend zu deaktivieren. Dafür gibt es HTML-Kommentare.

Ein Kommentar beginnt mit `<!--` und endet mit `-->`. Alles, was dazwischen steht, wird vom Browser komplett ignoriert und nicht auf der Webseite angezeigt.

```html
<!-- Dies ist ein einzeiliger Kommentar. -->

<p>Dieser Absatz wird ganz normal angezeigt.</p>

<!-- 
  Dies ist ein mehrzeiliger Kommentar.
  Er ist nützlich, um längere Erklärungen 
  oder ganze Code-Blöcke auszukommentieren.

  <div class="alter-bereich">
    <p>Dieser Bereich wird nicht angezeigt.</p>
  </div>
-->
```

Kommentare sind ein unschätzbares Werkzeug für die Zusammenarbeit im Team und für die Wartung deines eigenen Codes.

#### Die Grundstruktur eines jeden HTML-Dokuments

Wenn wir all diese Bausteine zusammensetzen, ergibt sich eine grundlegende Struktur, die jede HTML-Seite haben sollte. Sie gibt dem Browser den Rahmen, den er benötigt, um deine Inhalte korrekt zu interpretieren.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Titel der Webseite</title>
</head>
<body>

    <h1>Meine erste Webseite</h1>
    <p>Hallo Welt! Dies ist mein erster Absatz.</p>

</body>
</html>
```

Lass uns diese Struktur kurz aufschlüsseln:

1.  `<!DOCTYPE html>`: Dies ist keine HTML-Tag, sondern eine Deklaration. Sie steht immer an erster Stelle und teilt dem Browser mit: „Achtung, es folgt ein modernes HTML5-Dokument.“ Ohne diese Zeile könnte der Browser in einen alten Kompatibilitätsmodus verfallen und die Seite seltsam darstellen.

2.  `<html>`: Dies ist das Wurzelelement, das die gesamte Seite umschließt. Das Attribut `lang="de"` gibt an, dass der Hauptinhalt der Seite auf Deutsch ist, was für Suchmaschinen und Screenreader wichtig ist.

3.  `<head>`: Der „Kopf“ des Dokuments. Inhalte im `<head>`-Bereich sind für den Besucher nicht direkt sichtbar (mit Ausnahme des Titels). Hier stehen Metadaten, also Informationen *über* die Seite.
    *   `<meta charset="UTF-8">`: Legt die Zeichenkodierung fest. `UTF-8` ist der universelle Standard, der sicherstellt, dass Umlaute (ä, ö, ü), Sonderzeichen und Emojis korrekt dargestellt werden. Diese Zeile ist unverzichtbar.
    *   `<title>`: Definiert den Titel, der im Browser-Tab oder in den Lesezeichen angezeigt wird.

4.  `<body>`: Der „Körper“ des Dokuments. Alles, was der Besucher auf der Webseite sehen soll – Überschriften, Texte, Bilder, Videos, Links – gehört hier hinein.

Mit dem Verständnis dieser fundamentalen Syntaxregeln – Tags, Elemente, Verschachtelung, Attribute und die grundlegende Dokumentenstruktur – hast du das Rüstzeug, um jedes beliebige HTML-Dokument zu lesen, zu verstehen und selbst zu erstellen. Jede komplexe Webseite, die du im Netz findest, basiert im Kern auf genau diesen einfachen Prinzipien.
