# Tags und Attribute

### Tags und Attribute: Die Bausteine des Webs

Stell dir vor, du schreibst einen Text in einem einfachen Texteditor. Es sind nur Buchstaben, Zahlen und Satzzeichen. Nun möchtest du eine Überschrift hervorheben, einen Satz fett drucken oder einen Absatz definieren. Wie teilst du dem Computer mit, was ein normaler Satz und was eine wichtige Überschrift ist? Genau hier kommt HTML ins Spiel. HTML gibt deinem reinen Text eine Struktur und eine Bedeutung, indem es ihn in „Container“ verpackt. Diese Container nennst du **Tags**.

#### Was genau sind Tags?

Ein Tag ist im Grunde eine Anweisung an den Browser, die in spitzen Klammern (`<` und `>`) eingeschlossen ist. Du verwendest sie, um den Inhalt zu markieren – oder auf Englisch: „to mark up“. Daher kommt auch der Name: Hypertext **Markup** Language.

Die meisten HTML-Elemente bestehen aus zwei Teilen: einem öffnenden Tag (Start-Tag) und einem schließenden Tag (End-Tag). Dazwischen befindet sich der eigentliche Inhalt, den du auszeichnen möchtest.

Nehmen wir ein ganz einfaches Beispiel, den Absatz. In HTML wird ein Absatz mit dem `<p>`-Tag markiert. Das „p“ steht dabei für „paragraph“.

```html
<p>Dies ist ein ganz normaler Absatz.</p>
```

Lass uns das auseinandernehmen:

*   `<p>`: Das ist der **Start-Tag**. Er sagt dem Browser: „Achtung, hier beginnt ein Absatz.“
*   `Dies ist ein ganz normaler Absatz.`: Das ist der **Inhalt**, also der Text, der im Absatz stehen soll.
*   `</p>`: Das ist der **End-Tag**. Er unterscheidet sich vom Start-Tag durch den Schrägstrich (`/`) direkt nach der öffnenden spitzen Klammer. Er signalisiert dem Browser: „Hier endet der Absatz.“

Das gesamte Gebilde – Start-Tag, Inhalt und End-Tag – bezeichnen wir als **HTML-Element**.

Es gibt viele verschiedene Tags für unterschiedliche Zwecke. Überschriften zum Beispiel werden mit `<h1>`, `<h2>`, `<h3>` und so weiter bis `<h6>` ausgezeichnet. `<h1>` steht dabei für die wichtigste Überschrift der Seite, `<h6>` für die unwichtigste.

```html
<h1>Das ist die Hauptüberschrift</h1>
<p>Hier folgt ein Absatz, der das Thema einleitet.</p>
<h2>Ein Unterthema</h2>
<p>Und hier ein weiterer Absatz, der Details zum Unterthema liefert.</p>
```

Der Browser weiß nun genau, wie er diesen Inhalt interpretieren muss. Er wird die `<h1>`-Überschrift standardmäßig größer und fetter darstellen als die `<h2>`-Überschrift und diese wiederum anders als den normalen Absatztext. Du gibst deinem Inhalt also eine semantische, also eine bedeutungsvolle, Struktur.

**Leere Elemente: Tags ohne Inhalt**

Nicht alle Elemente folgen diesem Muster aus Öffnen, Inhalt und Schließen. Einige Elemente haben keinen eigenen Inhalt, den sie umschließen könnten. Man nennt sie leere oder selbstschließende Elemente. Ein klassisches Beispiel ist der Zeilenumbruch, `<br>` (für „break“). Er zwingt den Text, in die nächste Zeile zu springen, umschließt aber nichts.

```html
<p>Diese Zeile ist kurz.<br>Und diese Zeile beginnt direkt darunter.</p>
```

Ein weiteres wichtiges leeres Element ist das Bild-Tag `<img>` (für „image“). Es platziert ein Bild auf der Seite, hat aber selbst keinen textuellen Inhalt zwischen einem Start- und einem End-Tag. Wie das Bild-Tag weiß, welches Bild es anzeigen soll, klären wir im nächsten Abschnitt.

#### Attribute: Zusätzliche Informationen für deine Tags

Ein Tag allein sagt oft nicht alles. Ein `<a>`-Tag zum Beispiel definiert einen Link (das „a“ steht für „anchor“, also Anker), aber wohin soll der Link führen? Ein `<img>`-Tag sagt, dass hier ein Bild hinkommt, aber welches Bild?

Hier kommen die **Attribute** ins Spiel. Attribute sind zusätzliche Informationen, die du einem HTML-Tag mitgibst, um sein Verhalten oder seine Eigenschaften genauer zu definieren. Sie werden immer im Start-Tag platziert und folgen einem einfachen Muster:

`attributname="wert"`

Ein Attribut besteht immer aus einem Namen und einem Wert, der in Anführungszeichen gesetzt wird.

Schauen wir uns das am Beispiel des Link-Tags `<a>` an. Um dem Browser das Ziel des Links mitzuteilen, verwenden wir das `href`-Attribut (Hypertext Reference).

```html
<a href="https://www.beispiel.de">Besuche diese Webseite!</a>
```

Hier ist `<a` der Tag-Name, `href` ist der Attributname und `"https://www.beispiel.de"` ist der Wert des Attributs. Der Browser weiß nun: Wenn jemand auf den Text „Besuche diese Webseite!“ klickt, soll er zur angegebenen URL navigieren.

Oder kehren wir zum Bild-Tag `<img>` zurück. Es braucht zwingend das `src`-Attribut (Source, also Quelle), um die URL der Bilddatei anzugeben.

```html
<img src="bilder/sonnenuntergang.jpg">
```

Dieses Bild-Tag ist jedoch noch nicht vollständig. Was passiert, wenn das Bild nicht geladen werden kann oder wenn ein Nutzer mit einer Sehbehinderung deine Seite besucht und einen Screenreader verwendet? Dafür gibt es das `alt`-Attribut (Alternativtext). Es beschreibt den Inhalt des Bildes.

```html
<img src="bilder/sonnenuntergang.jpg" alt="Ein farbenprächtiger Sonnenuntergang über dem Meer">
```

Ein Element kann mehrere Attribute haben. Du schreibst sie einfach nacheinander, getrennt durch ein Leerzeichen, in den Start-Tag. Die Reihenfolge der Attribute spielt dabei keine Rolle.

#### Die Kunst der Verschachtelung

HTML-Dokumente sind hierarchisch aufgebaut. Das bedeutet, du kannst Elemente in andere Elemente hineinlegen. Diesen Vorgang nennt man Verschachtelung (Nesting). Stell es dir wie russische Matrjoschka-Puppen vor: eine Puppe in einer Puppe in einer Puppe.

Du könntest zum Beispiel innerhalb eines Absatzes ein Wort besonders betonen wollen. Dafür gibt es das `<strong>`-Tag, das dem Inhalt eine starke Wichtigkeit verleiht (und standardmäßig fett dargestellt wird).

```html
<p>Das ist ein <strong>sehr wichtiger</strong> Hinweis.</p>
```

Hier ist das `<strong>`-Element vollständig innerhalb des `<p>`-Elements verschachtelt. Wichtig ist die richtige Reihenfolge beim Schließen der Tags: Das innere Element muss immer vor dem äußeren Element geschlossen werden. Man spricht vom LIFO-Prinzip (Last In, First Out). Das zuletzt geöffnete Tag wird zuerst geschlossen.

**Falsch wäre:**

```html
<p>Das ist ein <strong>sehr wichtiger Hinweis.</p></strong>
```

Diese überlappende Struktur ist ungültig und kann zu unvorhersehbarem Verhalten im Browser führen. Halte dich immer an die saubere Verschachtelung, als würdest du Klammern in der Mathematik setzen.

#### Globale Attribute: Deine universellen Helfer

Es gibt eine Reihe von Attributen, die du auf fast jedem HTML-Element verwenden kannst. Man nennt sie globale Attribute. Sie sind extrem nützlich, um deine Elemente für Styling mit CSS oder Interaktivität mit JavaScript zugänglich zu machen. Hier sind einige der wichtigsten:

*   **`id`**: Dieses Attribut gibt einem Element einen **einzigartigen** Bezeichner. Eine ID darf auf einer gesamten HTML-Seite nur ein einziges Mal vergeben werden. Sie ist wie der Personalausweis eines Elements. Du kannst sie verwenden, um direkt zu einem bestimmten Seitenelement zu verlinken oder es gezielt mit JavaScript anzusprechen.

    ```html
    <h2 id="kapitel2">Das zweite Kapitel</h2>
    ```

*   **`class`**: Mit dem `class`-Attribut kannst du einem oder mehreren Elementen eine oder mehrere Klassen zuweisen. Klassen dienen dazu, Elemente zu gruppieren, die sich ähnlich verhalten oder gleich aussehen sollen. Im Gegensatz zur `id` kann dieselbe Klasse beliebig oft auf einer Seite verwendet werden, und ein Element kann auch mehrere Klassen haben (getrennt durch Leerzeichen).

    ```html
    <p class="hinweis">Dies ist ein allgemeiner Hinweis.</p>
    <p class="hinweis alarm">Dies ist ein besonders wichtiger Hinweis.</p>
    ```

*   **`style`**: Mit diesem Attribut kannst du einem Element direkte Stil-Anweisungen in Form von CSS mitgeben. Es ist nützlich für schnelle Tests, aber in größeren Projekten solltest du die Gestaltung lieber in separate CSS-Dateien auslagern, um Struktur und Stil sauber zu trennen.

    ```html
    <p style="color: blue; font-size: 18px;">Dieser Text ist blau und etwas größer.</p>
    ```

*   **`lang`**: Dieses Attribut gibt die Sprache des Inhalts eines Elements an. Es ist wichtig für Suchmaschinen und Hilfstechnologien wie Screenreader, um den Inhalt korrekt zu interpretieren und auszusprechen.

    ```html
    <p lang="en">This is a paragraph in English.</p>
    ```

Tags und Attribute sind das absolute Fundament von HTML. Mit Tags gibst du deinem Inhalt eine Struktur und eine Bedeutung. Mit Attributen reicherst du diese Tags um zusätzliche Informationen und Funktionalitäten an. Wenn du dieses Zusammenspiel verstanden hast, hast du den entscheidenden Schritt getan, um das Vokabular und die Grammatik des Webs zu beherrschen.
