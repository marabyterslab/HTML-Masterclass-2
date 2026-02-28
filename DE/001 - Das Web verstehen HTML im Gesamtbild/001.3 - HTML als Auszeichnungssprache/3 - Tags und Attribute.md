# Tags und Attribute

### Tags und Attribute: Die Bausteine von HTML

Stell dir vor, du möchtest ein Haus bauen. Du brauchst Ziegel, Fenster, Türen und ein Dach. Jedes dieser Elemente hat eine klare Funktion. In der Welt von HTML sind **Tags** diese grundlegenden Bausteine. Sie sind die Ziegel, die Fenster und die Türen deiner Webseite. Sie geben dem Inhalt, der auf deiner Seite erscheint, eine Struktur und eine Bedeutung.

Ein Tag ist im Grunde eine Anweisung an den Webbrowser, die in spitzen Klammern (`<` und `>`) eingeschlossen ist. Du sagst dem Browser: „Achtung, was jetzt kommt, ist eine Überschrift“ oder „Dieser Textabschnitt ist ein normaler Absatz.“

#### Öffnende und schließende Tags

Die meisten HTML-Tags treten paarweise auf: Es gibt einen **öffnenden Tag** und einen **schließenden Tag**. Der öffnende Tag markiert den Anfang eines Elements, der schließende Tag sein Ende. Alles, was dazwischen steht, ist der Inhalt dieses Elements.

Nehmen wir das Tag für einen Textabsatz, das `<p>`-Tag (von englisch *paragraph*). Es sieht so aus:

```html
<p>Dies ist ein einfacher Textabsatz.</p>
```

Der öffnende Tag ist `<p>`. Der schließende Tag ist fast identisch, hat aber einen Schrägstrich (Slash) direkt nach der öffnenden Klammer: `</p>`. Der Browser weiß nun, dass der Text „Dies ist ein einfacher Textabsatz.“ als ein zusammenhängender Absatz behandelt werden soll.

Das Gleiche gilt für Überschriften. HTML bietet sechs Ebenen von Überschriften, von `<h1>` (die wichtigste) bis `<h6>` (die unwichtigste).

```html
<h1>Das ist die Hauptüberschrift der Seite</h1>
<h2>Dies ist eine Unterüberschrift</h2>
<p>Und hier folgt ein Absatz, der sich auf die Unterüberschrift bezieht.</p>
```

Indem du diese Tags verwendest, schreibst du nicht nur Text. Du gibst ihm eine **semantische Bedeutung**. Ein `<h1>`-Tag sagt nicht „mach diesen Text groß und fett“, sondern „dies ist die thematisch wichtigste Überschrift auf dieser Seite“. Das *Aussehen* wird später mit CSS gesteuert, aber die *Struktur* und die *Bedeutung* legst du hier mit HTML fest. Das ist ein fundamentaler Unterschied und der Kern dessen, was eine Auszeichnungssprache ausmacht.

#### Die Verschachtelung von Elementen

Selten besteht eine Webseite nur aus einer losen Abfolge von Absätzen und Überschriften. Normalerweise sind Elemente ineinander verschachtelt, um komplexere Strukturen zu schaffen. Stell dir russische Matrjoschka-Puppen vor: Eine Puppe enthält die nächste, kleinere Puppe.

In HTML funktioniert das genauso. Du kannst ein Element vollständig in ein anderes einbetten. Wichtig ist dabei nur die Reihenfolge des Schließens: Das zuletzt geöffnete Tag muss als Erstes wieder geschlossen werden.

Ein einfaches Beispiel: Du möchtest ein Wort in einem Absatz besonders betonen. Dafür gibt es das `<em>`-Tag (von englisch *emphasis*).

```html
<p>HTML zu lernen ist <em>wirklich</em> einfach.</p>
```

Hier wird das `<em>`-Tag innerhalb des `<p>`-Tags geöffnet und auch wieder geschlossen. Die Reihenfolge ist korrekt: `<p>` öffnet, dann `<em>` öffnet, dann `<em>` schließt, dann `<p>` schließt.

Eine falsche Verschachtelung würde so aussehen und zu Fehlern in der Darstellung führen:

```html
<!-- FALSCH! So nicht machen. -->
<p>HTML zu lernen ist <em>wirklich einfach.</p></em>
```

Die Struktur deiner gesamten HTML-Seite basiert auf diesem Prinzip. Das `<body>`-Tag enthält alle sichtbaren Inhalte, und darin sind wiederum Überschriften, Absätze, Listen, Bilder und vieles mehr verschachtelt.

#### Leere Elemente: Tags ohne Inhalt

Es gibt einige wenige Ausnahmen von der Regel des öffnenden und schließenden Tags. Manche Elemente haben oder brauchen keinen Inhalt, weil sie für sich allein stehen. Man nennt sie **leere Elemente** oder **selbstschließende Tags**.

Ein klassisches Beispiel ist der Zeilenumbruch, das `<br>`-Tag (von englisch *break*). Es fügt einfach einen Zeilenumbruch ein. Es gibt keinen Text, den man „in einen Zeilenumbruch einschließen“ könnte.

```html
<p>Diese Zeile ist kurz.<br>Und diese hier auch.</p>
```

Ein weiteres wichtiges leeres Element ist das Bild-Tag `<img>`. Es platziert ein Bild auf der Seite, aber es umschließt keinen Inhalt. Woher das Bild kommt, definieren wir gleich mit Attributen.

```html
<img src="logo.png">
```

Früher, in der XHTML-Ära, war es üblich, diese Tags mit einem Schrägstrich am Ende zu schreiben, um ihre Selbstschließung zu verdeutlichen (`<br />` oder `<img />`). In modernem HTML5 ist das nicht mehr notwendig, aber du wirst es in älterem Code noch oft sehen. Beide Schreibweisen sind für heutige Browser in der Regel kein Problem.

---

### Attribute: Die Feinabstimmung der Bausteine

Wenn Tags die grundlegenden Bausteine sind, dann sind **Attribute** die Eigenschaften und Anweisungen, die du diesen Bausteinen mitgibst. Sie liefern zusätzliche Informationen über ein Element und erlauben es dir, sein Verhalten oder seine Beziehung zu anderen Dateien zu konfigurieren.

Ein Attribut wird immer im **öffnenden Tag** platziert und besteht aus zwei Teilen:
1.  Dem **Attributnamen** (z. B. `href`, `src`, `class`).
2.  Dem **Attributwert**, der in Anführungszeichen (`"`) steht (z. B. `"https://www.beispiel.de"`).

Die allgemeine Syntax lautet: `<tagname attributname="wert">Inhalt</tagname>`

#### Attribute in der Praxis

Schauen wir uns einige der wichtigsten Attribute an, um ihr Konzept zu verstehen.

**1. Das `href`-Attribut für Links**

Das `<a>`-Tag (von englisch *anchor*) erzeugt einen Hyperlink. Aber ein `<a>`-Tag allein weiß nicht, wohin es verlinken soll. Es braucht das `href`-Attribut (von englisch *hypertext reference*), um das Link-Ziel anzugeben.

```html
<a href="https://www.wikipedia.org">Besuche Wikipedia</a>
```

Ohne das `href`-Attribut wäre das `<a>`-Tag nutzlos. Es ist ein sogenanntes **erforderliches Attribut** für dieses Tag.

**2. Die `src`- und `alt`-Attribute für Bilder**

Wir haben das `<img>`-Tag bereits kennengelernt. Damit der Browser weiß, *welches* Bild er anzeigen soll, benötigt er das `src`-Attribut (von englisch *source*). Der Wert ist der Pfad zur Bilddatei.

```html
<img src="bilder/katze.jpg">
```

Doch was passiert, wenn das Bild nicht geladen werden kann? Oder wenn ein Nutzer mit einer Sehbehinderung deine Seite mit einem Screenreader besucht, der ihm den Inhalt vorliest? Dafür gibt es das `alt`-Attribut (von englisch *alternative text*). Es liefert eine textliche Beschreibung des Bildes.

```html
<img src="bilder/katze.jpg" alt="Eine orange getigerte Katze, die auf einem Sofa schläft.">
```

Guter Alternativtext ist entscheidend für die **Barrierefreiheit (Accessibility)** und ein Zeichen von professionellem HTML. Das `alt`-Attribut ist für `<img>`-Tags praktisch unverzichtbar.

**3. Die globalen Attribute: `id` und `class`**

Einige Attribute sind so nützlich, dass sie auf fast jedem HTML-Tag verwendet werden können. Man nennt sie **globale Attribute**. Die zwei wichtigsten sind `id` und `class`.

*   Die **`id`** ist wie ein Personalausweis für ein Element. Jede `id` auf einer HTML-Seite muss **einzigartig** sein. Du kannst sie verwenden, um ein ganz bestimmtes Element anzusprechen, zum Beispiel für einen Ankerlink innerhalb der Seite oder um es mit JavaScript zu manipulieren.

    ```html
    <h2 id="kapitel-3">Das dritte Kapitel</h2>
    ...
    <a href="#kapitel-3">Springe zu Kapitel 3</a>
    ```

*   Die **`class`** ist eher wie ein Gruppenschild. Du kannst dieselbe Klasse an viele verschiedene Elemente vergeben, um sie zu kategorisieren. Das Hauptanwendungsgebiet für Klassen ist das Styling mit CSS. Du könntest zum Beispiel allen wichtigen Warnhinweisen auf deiner Seite die gleiche Klasse geben, um sie einheitlich rot darzustellen.

    ```html
    <p class="warnung">Achtung: Dieser Vorgang kann nicht rückgängig gemacht werden.</p>
    <div class="warnung">
      <h4>Wichtiger Hinweis</h4>
      <p>Bitte lies die Bedingungen sorgfältig durch.</p>
    </div>
    ```

Hier haben sowohl der Absatz als auch der `<div>`-Container die Klasse `warnung` und können somit über eine einzige CSS-Regel gleichzeitig gestaltet werden. Ein Element kann auch mehrere Klassen haben, die durch Leerzeichen getrennt werden: `class="warnung dringend"`.

**4. Boolean-Attribute**

Eine besondere Art von Attributen sind die sogenannten **Boolean-Attribute**. Sie benötigen keinen Wert. Ihre bloße Anwesenheit im Tag schaltet eine bestimmte Eigenschaft ein (setzt sie auf „wahr“).

Ein gutes Beispiel ist das `disabled`-Attribut für einen Button. Wenn du es hinzufügst, wird der Button ausgegraut und ist nicht mehr klickbar.

```html
<button disabled>Diesen Button kann man nicht klicken</button>
```

Es gibt keine Form wie `disabled="false"`. Um die Eigenschaft wieder zu deaktivieren, entfernst du einfach das gesamte Attribut.

Tags und Attribute sind das dynamische Duo von HTML. Während Tags die grundlegende Struktur und semantische Bedeutung deines Inhalts definieren, erlauben dir Attribute, diese Elemente zu konfigurieren, zu verbinden und zu verfeinern. Das Verständnis, wie diese beiden Konzepte zusammenarbeiten, ist der erste und wichtigste Schritt auf dem Weg, das Web und seine Sprache zu meistern.
