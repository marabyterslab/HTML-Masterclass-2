# Tags und Attribute

### Tags und Attribute: Die Bausteine des Webs

Stell dir vor, du schreibst einen Text in einem einfachen Editor, so wie du es vielleicht von Notiz-Apps kennst. Es ist reiner Text, ohne Formatierung, ohne Struktur. Wo ist die Überschrift? Wo beginnt ein neuer Absatz? Welcher Teil des Textes ist ein Zitat und welcher ein wichtiger Hinweis? Ohne zusätzliche Informationen kann ein Computer – und damit der Webbrowser – das nicht wissen. Genau hier kommt HTML ins Spiel.

HTML gibt deinem reinen Text eine Bedeutung, eine Struktur. Es sagt dem Browser nicht, wie er etwas aussehen lassen soll (das ist die Aufgabe von CSS), sondern was es *ist*. Diese Anweisungen gibst du mit sogenannten **Tags**.

#### Was genau sind Tags?

Tags sind die fundamentalen Befehle in HTML. Du kannst sie dir wie Etiketten vorstellen, die du an deine Inhalte klebst, um sie zu klassifizieren. Ein Tag wird fast immer durch spitze Klammern (`<` und `>`) gekennzeichnet.

Die meisten HTML-Elemente bestehen aus einem Eröffnungs-Tag (Opening Tag) und einem Schluss-Tag (Closing Tag).

*   **Eröffnungs-Tag:** `<p>` sagt: "Hier beginnt ein Absatz."
*   **Schluss-Tag:** `</p>` sagt: "Hier endet der Absatz."

Der Schrägstrich (`/`) vor dem Tagnamen im Schluss-Tag ist das entscheidende Signal für das Ende des Elements. Alles, was sich zwischen dem Eröffnungs- und dem Schluss-Tag befindet, ist der Inhalt dieses Elements.

Das gesamte Gebilde – Eröffnungs-Tag, Inhalt und Schluss-Tag – wird als **HTML-Element** bezeichnet.

```html
<p>Dies ist der Inhalt eines Absatz-Elements.</p>
```

Hier ist `<p>` der Tag-Name, der für "paragraph" (Absatz) steht. Es gibt Dutzende von vordefinierten Tags in HTML, von denen jedes eine spezifische semantische Bedeutung hat:

*   `<h1>`, `<h2>`, ..., `<h6>` für Überschriften unterschiedlicher Ebenen.
*   `<strong>` für stark betonte, wichtige Inhalte.
*   `<em>` für hervorgehobenen Text (emphasis).
*   `<ul>` für eine unsortierte Liste (unordered list).
*   `<li>` für ein Listenelement (list item).

#### Die Kunst der Verschachtelung

Selten besteht eine Webseite nur aus einer flachen Abfolge von Elementen. Meistens sind Elemente ineinander verschachtelt (genestet), um komplexere Strukturen zu schaffen. Stell dir das wie russische Matrjoschka-Puppen vor: Eine Puppe enthält eine kleinere, die wiederum eine noch kleinere enthält.

In HTML bedeutet das, dass du ein Element vollständig innerhalb eines anderen Elements platzieren kannst. Die wichtigste Regel dabei lautet: Das zuletzt geöffnete Element muss als Erstes wieder geschlossen werden.

**Korrekt:**

```html
<p>In diesem Satz ist ein <strong>sehr wichtiges</strong> Wort enthalten.</p>
```

Hier wird das `<strong>`-Element innerhalb des `<p>`-Elements geöffnet und auch wieder geschlossen, bevor das `<p>`-Element endet. Der Browser versteht diese Hierarchie problemlos.

**Falsch:**

```html
<p>In diesem Satz ist ein <strong>sehr wichtiges Wort enthalten.</p></strong>
```

Diese überkreuzte Verschachtelung ist ungültig. Moderne Browser sind zwar sehr fehlertolerant und versuchen oft, solche Fehler zu korrigieren, aber das Ergebnis ist unvorhersehbar. Eine saubere, korrekte Verschachtelung ist die Grundlage für eine stabile und funktionierende Webseite.

#### Leere Elemente: Tags ohne Inhalt

Nicht alle Tags umschließen Inhalt. Einige Elemente stehen für sich allein und haben daher kein Schluss-Tag. Man nennt sie leere Elemente (void elements) oder auch selbstschließende Tags.

Ein klassisches Beispiel ist der Zeilenumbruch `<br>` (break). Er fügt einfach einen Umbruch ein und hat keinen eigenen Inhalt, den er umschließen könnte.

```html
<p>Diese Zeile ist kurz.<br>Und diese beginnt nach einem Umbruch.</p>
```

Ein weiteres wichtiges leeres Element ist das Bild-Tag `<img>`. Es platziert ein Bild auf der Seite, umschließt aber keinen Text oder andere Elemente.

```html
<img src="pfad/zum/bild.jpg">
```

Du wirst manchmal eine Schreibweise mit einem Schrägstrich am Ende sehen, wie `<br />` oder `<img />`. Dies ist ein Überbleibsel aus XHTML, einem strengeren Vorgänger von HTML5. In modernem HTML5 ist dieser Schrägstrich optional und hat keine funktionale Bedeutung.

#### Attribute: Zusatzinformationen für deine Tags

Bisher wissen wir, *was* ein Element ist (z. B. ein Bild oder ein Link). Aber wir haben noch nicht gesagt, *welches* Bild angezeigt oder *wohin* der Link führen soll. Dafür gibt es **Attribute**.

Attribute sind zusätzliche Informationen, die du einem HTML-Tag mitgibst. Sie werden immer im Eröffnungs-Tag platziert und bestehen aus zwei Teilen: einem Namen und einem Wert.

Die Syntax sieht so aus: `attributname="wert"`.

Nehmen wir das `<a>`-Element, das einen Hyperlink (Anker) definiert. Ohne ein Attribut ist es nutzlos. Es braucht das `href`-Attribut (hypertext reference), um sein Ziel anzugeben:

```html
<a href="https://www.wikipedia.org">Besuche Wikipedia</a>
```

Hier ist:
*   `a` der Tag-Name.
*   `href` der Attribut-Name.
*   `"https://www.wikipedia.org"` der Attribut-Wert.

Der Wert eines Attributs sollte immer in Anführungszeichen stehen. Doppelte Anführungszeichen (`"`) sind die gängige Konvention, aber einfache (`'`) sind ebenfalls gültig.

Ein Element kann auch mehrere Attribute haben. Diese werden einfach durch ein Leerzeichen voneinander getrennt. Die Reihenfolge spielt dabei keine Rolle.

Schauen wir uns das `<img>`-Element genauer an. Es benötigt das `src`-Attribut (source), um die Bildquelle anzugeben. Ein weiteres, extrem wichtiges Attribut ist `alt` (alternative text). Dieser Text wird angezeigt, wenn das Bild nicht geladen werden kann, und ist entscheidend für die Barrierefreiheit, da Screenreader ihn blinden oder sehbehinderten Nutzern vorlesen.

```html
<img src="bilder/katze.png" alt="Eine süße, getigerte Katze, die in einem Korb schläft">
```

Dieses `<img>`-Element hat zwei Attribute: `src` und `alt`, jedes mit seinem eigenen Namen und Wert.

#### Globale Attribute vs. spezifische Attribute

Manche Attribute sind so nützlich, dass sie auf fast jedem HTML-Element verwendet werden können. Man nennt sie **globale Attribute**. Dazu gehören unter anderem:

*   `id`: Verleiht einem Element einen einzigartigen, dokumentweiten Identifikator. Jede `id` darf auf einer Seite nur einmal vorkommen. Sie ist nützlich für Anker-Links innerhalb einer Seite oder um ein ganz bestimmtes Element mit JavaScript anzusprechen.
    ```html
    <h2 id="kapitel2">Das zweite Kapitel</h2>
    ```
*   `class`: Weist einem oder mehreren Elementen eine Klasse (eine Art Gruppierung) zu. Im Gegensatz zur `id` kann derselbe Klassenname beliebig oft auf einer Seite verwendet werden. Klassen sind das primäre Werkzeug, um Elemente mit CSS zu gestalten.
    ```html
    <p class="hinweis">Bitte beachte die neuen Öffnungszeiten.</p>
    <p class="hinweis wichtig">Letzter Einlass ist um 17:00 Uhr.</p>
    ```
    (Ein Element kann auch mehrere Klassen haben, getrennt durch Leerzeichen.)
*   `lang`: Gibt die Sprache des Inhalts eines Elements an, was für Suchmaschinen und Screenreader hilfreich ist.
    ```html
    <p lang="en">This paragraph is in English.</p>
    ```
*   `title`: Fügt eine zusätzliche Information zu einem Element hinzu, die oft als kleiner Tooltip erscheint, wenn du mit der Maus darüberfährst.
    ```html
    <abbr title="Hypertext Markup Language">HTML</abbr>
    ```

Andere Attribute sind **spezifisch** und machen nur bei bestimmten Elementen Sinn. Das `href`-Attribut ergibt nur bei Links einen Sinn, das `src`-Attribut nur bei Elementen, die eine externe Quelle laden (wie Bilder, Videos oder Skripte), und das `type`-Attribut bei `<input>`-Feldern definiert, ob es sich um ein Textfeld, ein Passwortfeld oder eine Checkbox handelt.

Tags und Attribute sind das Herzstück von HTML. Tags definieren die Art und die semantische Rolle deiner Inhalte, während Attribute diese Elemente mit den notwendigen Details und Metadaten anreichern. Wenn du dieses Zusammenspiel verstehst, hast du den grundlegendsten und wichtigsten Schritt getan, um die Sprache des Webs zu beherrschen. Jede Webseite, die du besuchst, ist im Kern nichts anderes als eine clevere und oft sehr komplexe Anordnung dieser beiden Bausteine.
