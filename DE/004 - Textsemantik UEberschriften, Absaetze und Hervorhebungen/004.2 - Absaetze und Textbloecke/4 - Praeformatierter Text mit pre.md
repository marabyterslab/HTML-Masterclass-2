# Präformatierter Text mit pre

### Präformatierter Text mit dem `<pre>`-Element

In den bisherigen Kapiteln hast du gesehen, wie HTML-Elemente wie Absätze (`<p>`) oder Überschriften (`<h1>`) den Text strukturieren. Dabei ist dir vielleicht aufgefallen, dass der Browser eine ganz eigene Vorstellung davon hat, wie er Leerzeichen und Zeilenumbrüche behandelt. Gibst du in deinem HTML-Code mehrere Leerzeichen hintereinander ein, fasst der Browser sie zu einem einzigen zusammen. Drückst du die Enter-Taste für einen Zeilenumbruch im Code-Editor, ignoriert der Browser das im gerenderten Ergebnis komplett. Dieses Verhalten wird als „Whitespace Collapsing“ bezeichnet und ist in den meisten Fällen extrem nützlich, da es dir erlaubt, deinen HTML-Code für eine bessere Lesbarkeit zu formatieren, ohne die Darstellung auf der Webseite zu beeinflussen.

Doch was, wenn genau diese Leerzeichen und Zeilenumbrüche eine entscheidende Bedeutung haben? Was, wenn du die Formatierung deines Textes exakt so beibehalten möchtest, wie du sie im Quelltext angelegt hast?

Stell dir folgenden Text in einem `<p>`-Element vor:

```html
<p>
  Es war einmal ein Programmierer,
  der schrieb ein kleines Gedicht.

    Die Syntax war korrekt,
    die Logik     perfekt,
  nur der Browser verstand es nicht.
</p>
```

Der Browser würde diesen liebevoll formatierten Text nehmen und ihn ohne die zusätzlichen Leerzeichen und Umbrüche als einen einzigen, durchgehenden Fließtext darstellen:

> Es war einmal ein Programmierer, der schrieb ein kleines Gedicht. Die Syntax war korrekt, die Logik perfekt, nur der Browser verstand es nicht.

Die gesamte beabsichtigte Struktur geht verloren. Genau für solche Fälle gibt es das `<pre>`-Element. Der Name steht für „preformatted“, also „vorformatiert“. Umschließt du einen Textblock mit `<pre>`, gibst du dem Browser die Anweisung: „Fass diesen Inhalt nicht an! Zeige jedes Leerzeichen, jeden Tabulator und jeden Zeilenumbruch exakt so an, wie er im Quellcode steht.“

Wenden wir das `<pre>`-Element auf unser Beispiel an:

```html
<pre>
  Es war einmal ein Programmierer,
  der schrieb ein kleines Gedicht.

    Die Syntax war korrekt,
    die Logik     perfekt,
  nur der Browser verstand es nicht.
</pre>
```

Das Ergebnis im Browser sieht nun exakt so aus, wie wir es beabsichtigt haben, inklusive der Einrückungen, der doppelten Leerzeile und der zusätzlichen Leerzeichen in der vierten Zeile.

#### Die Darstellung und der häufigste Anwendungsfall: Code

Dir wird sofort eine weitere Besonderheit auffallen, wenn du das `<pre>`-Element verwendest: Der Text wird standardmäßig in einer nichtproportionalen Schriftart (Monospace-Schriftart) wie `Courier` oder `Consolas` dargestellt. Bei einer solchen Schriftart nimmt jedes Zeichen, egal ob ein „i“ oder ein „W“, exakt denselben horizontalen Platz ein.

Dieser Umstand macht das `<pre>`-Element zum perfekten Werkzeug für die Darstellung von Computercode. In Programmiersprachen ist die exakte Einrückung oft nicht nur eine Frage der Lesbarkeit, sondern ein fundamentaler Teil der Syntax (wie zum Beispiel in Python). Die Monospace-Schriftart sorgt dafür, dass sauber untereinander ausgerichteter Code auch im Browser exakt so ausgerichtet bleibt.

Für die semantisch korrekte Auszeichnung von Code gibt es jedoch noch ein weiteres Element: `<code>`. Während `<pre>` ein Block-Element ist, das für die *Darstellung* eines vorformatierten Textblocks zuständig ist, ist `<code>` ein Inline-Element, das einen Textabschnitt als *Computercode* kennzeichnet. In der Praxis werden sie fast immer kombiniert, um einen ganzen Codeblock semantisch korrekt und mit erhaltener Formatierung darzustellen.

Die korrekte und gängigste Methode, einen mehrzeiligen Code-Schnipsel auf einer Webseite anzuzeigen, sieht also so aus:

```html
<pre><code class="language-js">
function gruss(name) {
  // Überprüft, ob ein Name angegeben wurde
  if (name) {
    console.log(`Hallo, ${name}!`);
  } else {
    console.log("Hallo, Welt!");
  }
}

gruss("Leser");
</code></pre>
```

Hier sagen wir dem Browser: „Hier beginnt ein Block mit vorformatiertem Text (`<pre>`), und der Inhalt dieses Blocks ist Computercode (`<code>`).“ Diese Kombination ist der Goldstandard. Viele Werkzeuge für Syntax-Highlighting (die den Code farblich hervorheben) erwarten genau diese Struktur und nutzen Klassen wie `language-js`, um die Programmiersprache zu identifizieren.

#### Die Falle: HTML-Sonderzeichen

Eine wichtige Sache musst du beachten, wenn du HTML-Code innerhalb eines `<pre>`-Blocks darstellen möchtest. Der Browser interpretiert HTML-Tags innerhalb von `<pre>` weiterhin als solche. Wenn du also versuchst, ein HTML-Beispiel direkt anzuzeigen, wird es nicht wie erwartet funktionieren:

```html
<!-- FALSCH! Das wird nicht wie gewünscht dargestellt. -->
<pre><code>
  <h1>Eine wichtige Überschrift</h1>
  <p>Ein Absatz mit Text.</p>
</code></pre>
```

Der Browser wird hier tatsächlich eine `<h1>`-Überschrift und ein `<p>`-Element rendern, anstatt den Code selbst anzuzeigen. Um das zu verhindern, musst du spezielle Zeichen, die in HTML eine Bedeutung haben, durch ihre sogenannten HTML-Entitäten ersetzen. Die wichtigsten sind:

*   `<` wird zu `&lt;` (less than)
*   `>` wird zu `&gt;` (greater than)
*   `&` wird zu `&amp;` (ampersand)

Der korrekte Weg, das obige HTML-Beispiel darzustellen, wäre also:

```html
<!-- KORREKT! So wird der Code als Text angezeigt. -->
<pre><code>
  &lt;h1&gt;Eine wichtige Überschrift&lt;/h1&gt;
  &lt;p&gt;Ein Absatz mit Text.&lt;/p&gt;
</code></pre>

Das mag anfangs umständlich wirken, ist aber essenziell, um die Integrität deiner Seite zu wahren und Code korrekt als reinen Text darzustellen.

#### Mehr als nur Code: ASCII-Art und strukturierte Daten

Obwohl die Darstellung von Code der mit Abstand häufigste Anwendungsfall ist, eignet sich `<pre>` für alles, bei dem die exakte textuelle Anordnung zählt. Ein klassisches und unterhaltsames Beispiel ist ASCII-Art:

```html
<pre>
   /\_/\
  ( o.o )
  > ^ <
</pre>
```

Auch zur einfachen Darstellung von Log-Dateien, Konfigurationsdateien oder tabellarischen Daten, bei denen eine richtige HTML-Tabelle (`<table>`) übertrieben wäre, leistet das `<pre>`-Element hervorragende Dienste.

#### Umgang mit langen Zeilen

Das strikte Festhalten an der Vorformatierung hat eine Konsequenz, die zum Problem werden kann: Lange Zeilen werden standardmäßig nicht umgebrochen. Wenn du eine sehr lange Zeile Code oder Text in ein `<pre>`-Element einfügst, wird diese Zeile aus dem Container herausragen und potenziell das Layout deiner gesamten Seite zerstören, indem sie einen horizontalen Scrollbalken für die ganze Seite erzwingt.

Glücklicherweise gibt es hierfür elegante Lösungen mit CSS. Du hast hauptsächlich zwei Optionen:

1.  **Zeilenumbruch erlauben:** Mit der CSS-Eigenschaft `white-space: pre-wrap;` kannst du dem Browser sagen, dass er die Leerzeichen und Zeilenumbrüche aus dem Quellcode zwar beibehalten, aber bei Bedarf zusätzliche Umbrüche bei langen Zeilen einfügen soll.

    ```css
    pre {
      white-space: pre-wrap;
    }
    ```

2.  **Scrollbalken für den Block:** Oft ist es bei Codeblöcken erwünscht, die langen Zeilen intakt zu lassen, damit man sie nicht versehentlich falsch kopiert. Statt die Seite zu zersprengen, kann man dem `<pre>`-Block selbst einen horizontalen Scrollbalken geben.

    ```css
    pre {
      overflow-x: auto;
    }
    ```

Diese zweite Methode ist bei der Darstellung von Code meist die bevorzugte, da sie die Originalformatierung zu 100 % bewahrt und gleichzeitig das Seitenlayout schützt.

Das `<pre>`-Element ist also ein spezialisiertes, aber mächtiges Werkzeug in deinem HTML-Repertoire. Immer wenn du die Kontrolle über Leerzeichen und Zeilenumbrüche behalten musst und die textbasierte Struktur deines Inhalts von Bedeutung ist, ist es die richtige Wahl.
