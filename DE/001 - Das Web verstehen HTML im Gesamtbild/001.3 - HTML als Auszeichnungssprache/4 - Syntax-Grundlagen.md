# Syntax-Grundlagen

### Syntax-Grundlagen: Die Grammatik des Webs

Stell dir vor, du lernst eine neue Sprache. Bevor du Romane schreiben kannst, musst du die Grundlagen verstehen: Buchstaben, Wörter, Satzbau und Grammatik. HTML ist da ganz ähnlich. Es ist die Sprache, mit der du dem Webbrowser sagst, wie deine Inhalte strukturiert sind. Diese Sprache hat ihre eigene Grammatik, die wir Syntax nennen. Wenn du diese Syntax beherrschst, kannst du dem Browser präzise Anweisungen geben. Glücklicherweise ist die Grammatik von HTML viel einfacher als die der deutschen Sprache.

Im Kern besteht HTML aus drei fundamentalen Bausteinen, die untrennbar miteinander verbunden sind: Tags, Elemente und Attribute. Lass uns diese Bausteine Schritt für Schritt auseinandernehmen.

#### Das Herzstück: HTML-Tags

Der grundlegendste Baustein in HTML ist der **Tag**. Ein Tag ist ein Befehl, den du in spitze Klammern (`<` und `>`) einschließt. Diese Tags sind wie Etiketten, mit denen du deine Inhalte versiehst. Du sagst dem Browser zum Beispiel: „Dieser Text hier ist eine Überschrift erster Ordnung“ oder „Dieser Block ist ein Absatz“.

Die meisten Tags treten paarweise auf: Es gibt einen **öffnenden Tag** (Opening Tag) und einen **schließenden Tag** (Closing Tag). Sie umschließen den Inhalt, den sie beschreiben.

Ein öffnender Tag sieht so aus: `<p>` (das `p` steht für „paragraph“, also Absatz).
Der dazugehörige schließende Tag sieht fast identisch aus, hat aber einen Schrägstrich (Slash) vor dem Namen des Tags: `</p>`.

Alles, was zwischen diesen beiden Tags steht, wird vom Browser als Absatz interpretiert.

```html
<p>Dies ist der Inhalt eines Absatzes.</p>
```

Ein anderes klassisches Beispiel ist die Hauptüberschrift einer Seite, die mit dem `<h1>`-Tag ausgezeichnet wird (`h` steht für „heading“, also Überschrift).

```html
<h1>Das ist eine Hauptüberschrift</h1>
```

Der Schrägstrich im schließenden Tag ist das entscheidende Signal für den Browser, dass die Auszeichnung an dieser Stelle endet. Ohne ihn wüsste der Browser nicht, wo der Absatz oder die Überschrift aufhört.

#### Vom Tag zum Element

Jetzt, wo du Tags kennst, können wir über **Elemente** sprechen. Oft werden die Begriffe „Tag“ und „Element“ synonym verwendet, aber es gibt einen feinen, wichtigen Unterschied. Ein Tag ist nur die Markierung selbst, also z. B. `<p>` oder `</h1>`. Ein Element hingegen ist das große Ganze: Es besteht aus dem öffnenden Tag, dem Inhalt und dem schließenden Tag.

Man kann es sich so vorstellen:

`Öffnender Tag` + `Inhalt` + `Schließender Tag` = **Element**

Schauen wir uns das am Beispiel des Absatzes noch einmal genau an:

```html
<p>Dieser Text ist der Inhalt.</p>
```

*   `<p>` ist der öffnende Tag.
*   `Dieser Text ist der Inhalt.` ist der Inhalt (Content).
*   `</p>` ist der schließende Tag.
*   Das gesamte Konstrukt von Anfang bis Ende ist das **p-Element**.

Das Verständnis dieses Unterschieds ist entscheidend, denn wenn wir später über die Gestaltung (mit CSS) oder das Verhalten (mit JavaScript) von Webseiten sprechen, beziehen wir uns fast immer auf Elemente, nicht auf einzelne Tags. Du wählst ein Element aus, um es zu verändern.

#### Die Ausnahme von der Regel: Leere Elemente

Wie in jeder guten Grammatik gibt es auch in HTML Ausnahmen. Nicht alle Elemente umschließen Inhalt und benötigen daher auch keinen schließenden Tag. Diese nennt man **leere Elemente** (Empty Elements oder Void Elements). Sie stehen für sich allein und fügen etwas in das Dokument ein, das keinen separaten Textinhalt hat.

Ein perfektes Beispiel ist der Zeilenumbruch. Wenn du innerhalb eines Absatzes eine neue Zeile erzwingen möchtest, ohne einen neuen Absatz zu beginnen, verwendest du das `<br>`-Element (`br` steht für „break“).

```html
<p>Die erste Zeile des Gedichts.<br>Und hier beginnt die zweite Zeile.</p>
```

Das `<br>`-Element hat keinen Inhalt, den es umschließen könnte. Es ist einfach nur eine Anweisung: „Browser, füge hier einen Zeilenumbruch ein.“ Deshalb hat es auch keinen schließenden Tag wie `</br>`.

Ein weiteres sehr wichtiges leeres Element ist das Bild-Element `<img>` (`img` steht für „image“). Ein Bild umschließt keinen Text; es wird an einer bestimmten Stelle im Dokument platziert. Woher das Bild kommt, definieren wir später mit Attributen.

```html
<img src="mein-foto.jpg">
```

Andere Beispiele für leere Elemente sind `<hr>` für eine horizontale Trennlinie oder `<input>` für ein Formularfeld.

#### Elemente verschachteln: Die Baumstruktur von HTML

Eine Webseite besteht selten nur aus einer Liste von Elementen, die brav untereinander stehen. Die wahre Stärke von HTML liegt in der Möglichkeit, Elemente ineinander zu **verschachteln** (Nesting). Du kannst dir das wie russische Matrjoschka-Puppen oder Kisten in Kisten vorstellen.

Ein Element, das innerhalb eines anderen Elements platziert wird, ist ein Kind-Element des äußeren Eltern-Elements. Diese Verschachtelung erzeugt eine hierarchische Baumstruktur, die für den Browser (und für dich) entscheidend ist, um den Aufbau der Seite zu verstehen.

Dabei gibt es eine goldene Regel: **Ein inneres Element muss immer geschlossen werden, bevor das äußere Element geschlossen wird.**

Schau dir dieses korrekte Beispiel an:

```html
<div>
    <h1>Eine wichtige Überschrift</h1>
    <p>In diesem Absatz gibt es einen <strong>besonders hervorgehobenen</strong> Text.</p>
</div>
```

Hier ist das `<strong>`-Element korrekt innerhalb des `<p>`-Elements verschachtelt. Das `<strong>`-Element wird geöffnet und geschlossen, bevor das `<p>`-Element geschlossen wird. Ebenso sind das `<h1>`- und das `<p>`-Element Kinder des `<div>`-Elements und werden geschlossen, bevor das `<div>`-Element geschlossen wird.

Eine falsche Verschachtelung würde den Browser verwirren und zu unvorhersehbaren Ergebnissen führen:

```html
<p>Dieser Text ist <strong>fett und wichtig.</p></strong> <!-- FALSCH! -->
```

Hier wird versucht, das `<p>`-Element zu schließen, bevor das darin enthaltene `<strong>`-Element geschlossen wurde. Das ist ein Syntaxfehler.

#### Mehr Details mit Attributen

Bisher können unsere Elemente nur die Art des Inhalts beschreiben (Überschrift, Absatz, etc.). Aber was ist, wenn wir zusätzliche Informationen bereitstellen wollen? Was, wenn wir einem Link sagen wollen, wohin er führen soll? Oder einem Bild, welche Datei es anzeigen soll?

Hier kommen die **Attribute** ins Spiel. Attribute sind zusätzliche Konfigurationswerte, die einem Element mehr Kontext oder Funktionalität verleihen. Sie werden **immer** im öffnenden Tag platziert und folgen einem einfachen Muster:

`attributname="wert"`

*   **Attributname:** Der Name der Eigenschaft, die du setzen möchtest (z. B. `href` für einen Link oder `src` für eine Bildquelle).
*   **Gleichheitszeichen:** Verbindet den Namen mit dem Wert.
*   **Wert:** Die eigentliche Information, immer in Anführungszeichen (doppelte `"..."` sind der gängige Standard, einfache `'...'` sind aber auch erlaubt).

Das klassische Beispiel ist der Anker-Tag `<a>` (`a` steht für „anchor“), der einen Hyperlink erzeugt. Ohne Attribut ist er nutzlos. Erst das `href`-Attribut (`href` steht für „hypertext reference“) macht ihn zu einem funktionierenden Link:

```html
<a href="https://www.wikipedia.org">Besuche Wikipedia</a>
```

Hier ist `href` der Attributname und `"https://www.wikipedia.org"` der Wert.

Ein anderes Beispiel ist das bereits erwähnte `<img>`-Element. Es benötigt mindestens das `src`-Attribut (`src` steht für „source“), um dem Browser mitzuteilen, welche Bilddatei geladen werden soll. Ein weiteres, extrem wichtiges Attribut ist `alt` (für „alternative text“). Dieser Text wird angezeigt, wenn das Bild nicht geladen werden kann, und ist für Bildschirmlesegeräte (Screenreader) für blinde oder sehbehinderte Menschen unerlässlich.

```html
<img src="bilder/logo.png" alt="Firmenlogo der HTML-Masterclass">
```

Ein Element kann mehrere Attribute haben. Sie werden einfach durch Leerzeichen voneinander getrennt. Die Reihenfolge spielt dabei keine Rolle.

#### Kommentare: Notizen für dich und andere

Manchmal möchtest du Notizen in deinem Code hinterlassen – für dich selbst, um dich später an etwas zu erinnern, oder für Kollegen, die mit deinem Code arbeiten. Dafür gibt es in HTML Kommentare.

Ein Kommentar wird vom Browser komplett ignoriert und ist auf der Webseite nicht sichtbar. Er dient allein der Dokumentation im Quellcode. Die Syntax ist etwas anders als bei normalen Tags:

`<!-- Hier steht dein Kommentar. -->`

Ein Kommentar beginnt mit `<!--` und endet mit `-->`. Alles dazwischen ist der Kommentartext.

```html
<!-- Dieser Abschnitt enthält die Hauptnavigation der Webseite -->
<nav>
    ... Navigationslinks ...
</nav>
```

#### Das Grundgerüst einer HTML-Datei

Wenn wir all diese Bausteine zusammensetzen, können wir das grundlegende Skelett jeder HTML-Seite erstellen. Jede standardkonforme HTML-Datei hat eine bestimmte Grundstruktur, die dem Browser wichtige Informationen über das Dokument gibt.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Titel der Webseite</title>
</head>
<body>
    <h1>Meine erste Webseite</h1>
    <p>Hallo Welt!</p>
</body>
</html>
```

Lass uns dieses Gerüst Zeile für Zeile durchgehen:

1.  `<!DOCTYPE html>`: Dies ist die **Dokumenttyp-Deklaration** (kurz Doctype). Sie ist kein HTML-Tag, sondern eine Anweisung an den Browser. Sie teilt ihm mit: „Achtung, was jetzt kommt, ist ein modernes HTML5-Dokument.“ Diese Zeile muss immer ganz am Anfang stehen.

2.  `<html lang="de">...</html>`: Das ist das **Wurzelelement** (Root Element). Alle anderen Elemente auf der Seite sind darin verschachtelt. Das Attribut `lang="de"` ist eine wichtige Angabe, die dem Browser (und Suchmaschinen) mitteilt, dass der Hauptinhalt der Seite auf Deutsch ist.

3.  `<head>...</head>`: Der „Kopf“ des Dokuments. Der Inhalt des `<head>`-Elements ist für den Besucher nicht direkt auf der Seite sichtbar (mit Ausnahme des Titels). Hier stehen **Metadaten**, also Informationen *über* das Dokument.
    *   `<meta charset="UTF-8">`: Dies ist eine der wichtigsten Zeilen. Sie legt die Zeichenkodierung fest und sorgt dafür, dass Umlaute (ä, ö, ü) und Sonderzeichen korrekt dargestellt werden.
    *   `<title>...</title>`: Der Titel des Dokuments. Dieser Text erscheint im Tab des Browsers und ist auch für Suchmaschinen extrem wichtig.

4.  `<body>...</body>`: Der „Körper“ des Dokuments. Hier kommt alles hinein, was der Benutzer im Browserfenster sehen soll: Überschriften, Texte, Bilder, Videos, Links – einfach der gesamte sichtbare Inhalt.

Mit diesem Wissen über Tags, Elemente, Attribute und die Grundstruktur hast du die Grammatik von HTML verstanden. Du bist jetzt in der Lage, jedes HTML-Dokument zu lesen, seine Struktur zu verstehen und selbst einfache, aber syntaktisch korrekte Webseiten zu erstellen.
