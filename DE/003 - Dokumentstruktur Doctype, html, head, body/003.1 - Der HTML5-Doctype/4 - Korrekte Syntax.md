# Korrekte Syntax

### Korrekte Syntax: Die Grammatik des Webs

Stell dir vor, du lernst eine neue Sprache. Du beginnst mit dem Alphabet, lernst Wörter und fügst sie schließlich nach bestimmten Regeln – der Grammatik – zu Sätzen zusammen. HTML ist die Sprache des Webs, und seine Grammatik nennen wir Syntax. Wenn du die Syntax beherrschst, kannst du fehlerfreie und verständliche Anweisungen für den Browser schreiben.

Das Schöne und manchmal auch Tückische an Webbrowsern ist, dass sie unglaublich fehlertolerant sind. Sie versuchen fast immer, das Beste aus dem Code zu machen, den du ihnen gibst, selbst wenn er syntaktische Fehler enthält. Doch auf diese Nachsicht solltest du dich niemals verlassen. Ein syntaktisch korrekter Code ist die Grundlage für eine stabile, vorhersagbare und professionelle Webseite. Er sorgt dafür, dass deine Seite heute, morgen und in jedem Browser so funktioniert, wie du es erwartest.

#### Das Fundament: Der Doctype

Jedes einzelne HTML-Dokument, ohne Ausnahme, muss mit einer ganz bestimmten Zeile beginnen: der Dokumenttyp-Deklaration, kurz Doctype. Sie ist gewissermaßen der erste Gruß an den Browser.

```html
<!DOCTYPE html>
```

Diese Zeile sieht vielleicht wie ein HTML-Tag aus, ist es aber technisch gesehen nicht. Sie ist eine Anweisung. Sie teilt dem Browser mit: "Achtung, was jetzt folgt, ist ein HTML5-Dokument. Bitte interpretiere es nach den modernsten Webstandards."

Früher, in den Zeiten von XHTML und älteren HTML-Versionen, waren diese Deklarationen lang, kryptisch und schwer zu merken. Die Einfachheit von `<!DOCTYPE html>` ist ein Geschenk von HTML5. Mit dieser einen, klaren Zeile versetzt du den Browser in den sogenannten "Standards Mode". In diesem Modus rendert er die Seite nach den offiziellen Spezifikationen des World Wide Web Consortiums (W3C), was zu einer konsistenteren Darstellung über verschiedene Browser hinweg führt.

Lässt du den Doctype weg oder schreibst ihn falsch, schaltet der Browser aus Kompatibilitätsgründen in den "Quirks Mode". Das ist ein Relikt aus der Vergangenheit, in dem der Browser versucht, das Verhalten alter, fehlerhafter Browser aus den späten 90er-Jahren zu imitieren. Das führt zu unvorhersehbarem Verhalten und seltsamen Darstellungsfehlern, die du unbedingt vermeiden willst. Die erste Regel der korrekten Syntax lautet also: Jedes Dokument beginnt mit `<!DOCTYPE html>`.

#### Die Grundstruktur: Das Wurzelelement und seine Kinder

Nach dem Doctype folgt die eigentliche Struktur deines Dokuments. Jedes HTML-Dokument hat ein einziges Wurzelelement (Root Element), das alle anderen Elemente umschließt: das `<html>`-Element.

```html
<!DOCTYPE html>
<html>
  <!-- Alle weiteren Inhalte kommen hier hinein -->
</html>
```

Es ist eine gute Praxis, dem `<html>`-Tag die Sprache des Dokuments mitzuteilen. Dies geschieht über das `lang`-Attribut und ist wichtig für Suchmaschinen und assistierende Technologien wie Screenreader. Für ein deutsches Dokument sieht das so aus:

```html
<html lang="de">
```

Innerhalb des `<html>`-Elements gibt es genau zwei direkte Kind-Elemente: `<head>` und `<body>`. Kein anderes Element darf direkt innerhalb von `<html>` stehen.

1.  **Der `<head>`-Bereich:** Hier platzierst du Metadaten – also Daten über dein HTML-Dokument. Diese Informationen sind für den Besucher der Webseite in der Regel nicht direkt sichtbar, aber für den Browser und andere Maschinen (wie Suchmaschinen-Crawler) von entscheidender Bedeutung.
2.  **Der `<body>`-Bereich:** Hier kommt alles hinein, was der Benutzer im Browserfenster sehen soll: Texte, Bilder, Videos, Überschriften, Listen und so weiter.

Eine korrekte Grundstruktur sieht also immer so aus:

```html
<!DOCTYPE html>
<html lang="de">
  <head>
    <!-- Metadaten für den Browser -->
  </head>
  <body>
    <!-- Sichtbarer Inhalt für den Benutzer -->
  </body>
</html>
```

#### Die unsichtbaren Helfer im `<head>`

Der `<head>`-Bereich ist das Gehirn deiner Webseite. Zwei Elemente sind hier praktisch unverzichtbar.

Das erste ist die Zeichenkodierung. Sie teilt dem Browser mit, wie er die Nullen und Einsen deines Dokuments in lesbare Buchstaben und Symbole umwandeln soll. Ohne diese Angabe kann es passieren, dass Umlaute (ä, ö, ü) oder Sonderzeichen falsch dargestellt werden. Der weltweite Standard ist UTF-8, da er so gut wie jedes Zeichen aus jeder Sprache der Welt abbilden kann. Du deklarierst ihn so:

```html
<meta charset="UTF-8">
```

Diese Zeile sollte eine der ersten innerhalb deines `<head>`-Tags sein, damit der Browser von Anfang an weiß, wie er den Text interpretieren muss.

Das zweite essenzielle Element ist der Titel des Dokuments. Dieser wird im Tab des Browsers angezeigt und ist auch der Standard-Titel, wenn jemand deine Seite als Lesezeichen speichert. Suchmaschinen gewichten den Inhalt des `<title>`-Tags ebenfalls sehr hoch.

```html
<title>Meine erste Webseite: Korrekte Syntax</title>
```

#### Die Anatomie eines HTML-Elements

Wenn wir uns die bisherigen Beispiele ansehen, erkennen wir ein klares Muster. Die meisten HTML-Elemente bestehen aus drei Teilen:

1.  **Einem öffnenden Tag (Opening Tag):** Er besteht aus einer spitzen Klammer auf (`<`), dem Namen des Elements (z. B. `p` für einen Paragraphen) und einer spitzen Klammer zu (`>`). Beispiel: `<p>`.
2.  **Dem Inhalt:** Das ist der Text oder die weiteren HTML-Elemente, die sich zwischen dem öffnenden und dem schließenden Tag befinden.
3.  **Einem schließenden Tag (Closing Tag):** Er sieht fast genauso aus wie der öffnende Tag, enthält aber einen Schrägstrich (Slash) vor dem Elementnamen. Beispiel: `</p>`.

Zusammengesetzt ergibt das ein vollständiges Element:

```html
<p>Dies ist ein einfacher Textabsatz.</p>
```

Manche Elemente, wie das `<img>`-Tag für Bilder oder das `<br>`-Tag für einen Zeilenumbruch, haben keinen Inhalt. Man nennt sie "leere Elemente" oder "Void Elements". Sie bestehen nur aus einem einzigen Tag. In HTML5 schreibst du sie einfach so:

```html
<img src="bild.jpg" alt="Beschreibung des Bildes">
<br>
```

Du wirst manchmal eine Schreibweise mit einem Schrägstrich am Ende sehen (`<br />`). Dies ist ein Überbleibsel aus XHTML, einer strengeren Variante von HTML. In modernem HTML5 ist dieser Schrägstrich optional und wird üblicherweise weggelassen.

Elemente können auch **Attribute** haben. Das sind zusätzliche Informationen, die das Verhalten oder die Bedeutung eines Elements steuern. Wir haben sie bereits beim `lang`-Attribut im `<html>`-Tag und beim `charset`-Attribut im `<meta>`-Tag gesehen. Attribute werden immer im öffnenden Tag platziert und folgen dem Muster `name="wert"`.

```html
<a href="https://beispiel.de">Dies ist ein Link</a>
```

Hier ist `href` der Name des Attributs und `"https://beispiel.de"` ist sein Wert.

#### Die Kunst der korrekten Verschachtelung

HTML-Elemente können ineinander verschachtelt werden, um komplexere Strukturen zu schaffen. Zum Beispiel kannst du innerhalb eines Textabsatzes ein Wort besonders betonen:

```html
<p>Dies ist ein <strong>wichtiger</strong> Punkt.</p>
```

Hier ist das `<strong>`-Element innerhalb des `<p>`-Elements verschachtelt. Die entscheidende Regel bei der Verschachtelung lautet: **Das zuletzt geöffnete Element muss als Erstes wieder geschlossen werden.**

**Korrekt:**

```html
<p>Dies ist <strong>wichtig</strong>.</p>
```

**Falsch:**

```html
<p>Dies ist <strong>wichtig.</p></strong>
```

Im falschen Beispiel wird das `<p>`-Tag geschlossen, bevor das `<strong>`-Tag geschlossen wurde. Das ist ein Syntaxfehler, der den Browser verwirrt und zu unerwarteten Ergebnissen in der Darstellung führen kann. Stell es dir wie russische Matroschka-Puppen vor: Du musst immer die innerste Puppe schließen, bevor du die äußere schließen kannst.

#### Kommentare und Groß-/Kleinschreibung

Manchmal möchtest du Notizen in deinem Code hinterlassen, die der Browser ignorieren soll. Dafür gibt es HTML-Kommentare. Sie sind nützlich, um Codeabschnitte zu erklären oder Teile vorübergehend zu deaktivieren.

```html
<!-- Dies ist ein Kommentar und wird im Browser nicht angezeigt. -->
<p>Dieser Text ist sichtbar.</p>
<!--
<p>Dieser Absatz ist auskommentiert und daher unsichtbar.</p>
-->
```

Eine letzte wichtige Anmerkung zur Syntax: HTML-Tag- und Attributnamen sind nicht case-sensitive, das heißt, `<p>` ist für den Browser dasselbe wie `<P>`. Dennoch hat sich als Konvention und für eine bessere Lesbarkeit durchgesetzt, **alles in Kleinbuchstaben zu schreiben**. Werte von Attributen, wie zum Beispiel Dateinamen in einem `href`-Attribut, können jedoch sehr wohl case-sensitive sein, je nachdem, wie der Webserver konfiguriert ist. Bleibe bei Kleinbuchstaben, und du bist auf der sicheren Seite.

#### Das syntaktisch perfekte Minimaldokument

Fassen wir all diese Regeln zusammen, erhalten wir das Grundgerüst eines jeden perfekten HTML5-Dokuments. Es ist die Vorlage, mit der du jedes neue Projekt beginnen solltest.

```html
<!DOCTYPE html>
<html lang="de">
  <head>
    <meta charset="UTF-8">
    <title>Titel der Seite</title>
  </head>
  <body>
    <h1>Meine erste Überschrift</h1>
    <p>Ein Absatz mit etwas Text.</p>
  </body>
</html>
```

Diese Struktur ist sauber, logisch und für jeden Browser unmissverständlich. Wenn du diese grundlegende Grammatik verinnerlichst, legst du das Fundament, auf dem du komplexe, robuste und funktionale Webseiten aufbauen kannst. Korrekte Syntax ist kein Selbstzweck; sie ist ein Zeichen von Professionalität und der Schlüssel zu einem vorhersehbaren und wartbaren Web.
