# Attribut-Selektoren

### Attribut-Selektoren

Bisher hast du gelernt, Elemente anhand ihres Typs (z. B. `p`, `h1`), ihrer Klasse (`.wichtiger-hinweis`) oder ihrer ID (`#hauptnavigation`) auszuwählen. Das ist die Grundlage von CSS und deckt bereits einen Großteil der alltäglichen Anwendungsfälle ab. Aber was, wenn du Elemente nicht aufgrund eines von dir vergebenen Namens, sondern aufgrund ihrer Eigenschaften oder Zustände ansprechen möchtest? Was ist mit all den Attributen, die du in deinem HTML-Code verwendest, wie `href`, `src`, `alt`, `type` oder `disabled`?

Genau hier kommen Attribut-Selektoren ins Spiel. Sie ermöglichen es dir, Elemente basierend auf dem Vorhandensein, dem Wert oder sogar Teilen des Wertes eines Attributes zu stylen. Dies eröffnet eine völlig neue Ebene der Präzision und Flexibilität und erlaubt dir, deinen CSS-Code semantischer und oft auch wartungsärmer zu gestalten.

#### Der einfache Attribut-Selektor: Wenn die Existenz ausreicht

Die einfachste Form eines Attribut-Selektors prüft lediglich, ob ein Element ein bestimmtes Attribut besitzt – der Wert spielt dabei keine Rolle. Die Syntax dafür ist denkbar einfach: Du schreibst den Attributnamen in eckige Klammern.

`[attribut]`

Stell dir vor, du möchtest alle Links auf deiner Seite, die einen `title`-Text für zusätzliche Informationen haben, besonders hervorheben, vielleicht mit einer dezenten gestrichelten Unterstreichung.

```html
<p>
  Besuche unsere <a href="/ueber-uns">Über-uns-Seite</a> für mehr Details.
  Für weitere Informationen kannst du auch die offizielle
  <a href="https://www.w3.org/" title="Website des World Wide Web Consortiums">W3C-Website</a>
  besuchen.
</p>
```

Mit einem einfachen Attribut-Selektor kannst du gezielt nur den zweiten Link ansprechen:

```css
a[title] {
  border-bottom: 1px dotted blue;
  cursor: help;
}
```

In diesem Beispiel erhält nur der Link zum W3C die gestrichelte blaue Linie und den Hilfe-Cursor, weil nur er das `title`-Attribut besitzt. Der erste Link bleibt unberührt. Dies ist unglaublich nützlich, um Elemente mit bestimmten Funktionalitäten (wie Tooltips) oder Zuständen (wie `disabled`) einheitlich zu gestalten, ohne ihnen extra eine Klasse geben zu müssen.

#### Der exakte Wert: `[attribut="wert"]`

Der nächste logische Schritt ist die Auswahl von Elementen, bei denen ein Attribut einen ganz bestimmten Wert hat. Dies ist einer der am häufigsten genutzten Attribut-Selektoren.

`[attribut="wert"]`

Ein klassisches Beispiel sind Formularfelder. Ein `<input>`-Element kann viele verschiedene Typen haben: `text`, `password`, `email`, `submit` und so weiter. Wenn du nur die Text-Eingabefelder gestalten möchtest, ist dieser Selektor perfekt.

```html
<form>
  <label for="username">Benutzername:</label>
  <input type="text" id="username" name="username">

  <label for="password">Passwort:</label>
  <input type="password" id="password" name="password">

  <input type="submit" value="Anmelden">
</form>
```

Mit dem folgenden CSS kannst du ausschließlich die Felder für den Benutzernamen und das Passwort ansprechen, nicht aber den Senden-Button, obwohl es sich bei allen um `<input>`-Elemente handelt.

```css
input[type="text"],
input[type="password"] {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

input[type="submit"] {
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}
```

Dieser Ansatz ist viel sauberer als Klassen wie `.text-input` zu vergeben, da er sich direkt auf die semantische Bedeutung des HTML-Attributs stützt.

#### Flexibler werden: Die Suche nach Teilzeichenketten

Manchmal reicht eine exakte Übereinstimmung nicht aus. Du möchtest vielleicht Elemente auswählen, deren Attributwert ein bestimmtes Wort *enthält*, damit *beginnt* oder darauf *endet*. Für diese Fälle bietet CSS eine Reihe von mächtigen Selektoren.

##### `[attribut~="wert"]` – Enthält ein ganzes Wort

Dieser Selektor mit der Tilde (`~`) findet Elemente, bei denen der Attributwert eine durch Leerzeichen getrennte Liste von Wörtern ist und eines dieser Wörter exakt mit dem angegebenen Wert übereinstimmt. Das klingt kompliziert, ist aber besonders für Attribute wie `class` oder `rel` nützlich.

Stell dir vor, du hast Bilder, die als Icons dienen und zusätzlich andere Klassen haben können.

```html
<img src="profil.png" class="user-icon rounded">
<img src="warnung.png" class="icon-warning">
<img src="info.png" class="info-icon small">
```

Wenn du nun alle Bilder, die ein "icon" in ihrer Klassenliste haben, ansprechen möchtest, könntest du folgendes tun:

```css
img[class~="icon"] {
  /* ... würde nicht funktionieren, da "icon" kein ganzes Wort ist ... */
}

img[class~="user-icon"] {
  /* ... würde das erste Bild finden ... */
  border: 2px solid green;
}
```

Ein besseres Beispiel wäre ein `rel`-Attribut bei Links:

```html
<a href="#" rel="nofollow noopener external">Externer Link</a>
```

Hier könntest du mit `a[rel~="external"]` gezielt diesen Link auswählen, da "external" ein vollständiges, durch Leerzeichen getrenntes Wort im Wert des `rel`-Attributs ist.

##### `[attribut*="wert"]` – Enthält eine Zeichenkette

Der Sternchen-Selektor (`*`) ist vielseitiger. Er wählt jedes Element aus, dessen Attributwert die angegebene Zeichenkette an *irgendeiner* Stelle enthält. Es muss kein ganzes Wort sein.

Dies ist extrem praktisch, um beispielsweise alle Links zu einer bestimmten Domain zu stylen, unabhängig vom Protokoll oder der Unterseite.

```html
<a href="https://beispiel-shop.de/produkte">Zum Shop</a>
<a href="/kontakt">Kontakt</a>
<a href="https://blog.beispiel-shop.de/neues">Unser Blog</a>
```

Mit dem folgenden CSS kannst du alle Links, die auf eine Subdomain oder die Hauptdomain von `beispiel-shop.de` verweisen, mit einem Icon versehen:

```css
a[href*="beispiel-shop.de"]::before {
  content: '🛒 ';
}
```

Beide externen Links würden das Einkaufswagen-Emoji erhalten, der interne Kontaktlink jedoch nicht.

##### `[attribut^="wert"]` – Beginnt mit einer Zeichenkette

Der Zirkumflex-Selektor (`^`) prüft, ob ein Attributwert mit einer bestimmten Zeichenkette *beginnt*. Ein typischer Anwendungsfall ist die Unterscheidung zwischen sicheren (`https://`) und unsicheren (`http://`) externen Links.

```css
/* Style alle sicheren, externen Links */
a[href^="https://"] {
  color: green;
}

/* Style alle internen Links (die relativ sind) */
a[href^="/"] {
  text-decoration: none;
}
```

##### `[attribut$="wert"]` – Endet mit einer Zeichenkette

Das Gegenstück dazu ist der Dollarzeichen-Selektor (`$`), der prüft, ob ein Attributwert mit einer bestimmten Zeichenkette *endet*. Dies wird sehr häufig verwendet, um Links basierend auf dem Dateityp, auf den sie verweisen, zu gestalten.

```html
<ul>
  <li><a href="dokument.pdf">Jahresbericht (PDF)</a></li>
  <li><a href="praesentation.zip">Präsentation (ZIP)</a></li>
  <li><a href="/interne-seite">Interne Seite</a></li>
</ul>
```

Du kannst nun automatisch passende Icons vor die Links setzen, ohne eine einzige Klasse im HTML zu benötigen:

```css
a[href$=".pdf"]::before {
  content: '📄 ';
}

a[href$=".zip"]::before {
  content: '📦 ';
}
```

Das macht deinen Code unglaublich dynamisch. Wenn ein Redakteur einen neuen PDF-Link hinzufügt, erhält dieser automatisch das richtige Icon, ohne dass er etwas über CSS wissen muss.

##### `[attribut|="wert"]` – Beginnt mit einem exakten Wort (oder ist identisch)

Dieser Selektor ist etwas spezieller und wird seltener benötigt. Der senkrechte Strich (`|`) wählt Elemente aus, deren Attributwert entweder exakt `wert` ist oder mit `wert-` beginnt (also `wert` gefolgt von einem Bindestrich). Sein Hauptzweck ist die Arbeit mit Sprachcodes.

```html
<p lang="de">Ein Absatz auf Deutsch.</p>
<p lang="de-CH">Ein Absatz auf Schweizerdeutsch.</p>
<p lang="en-US">A paragraph in American English.</p>
```

Mit `p[lang|="de"]` würdest du die ersten beiden Absätze auswählen (`de` und `de-CH`), aber nicht den dritten. Es ist eine spezialisierte Version von `[attribut^="wert"]`, die den Bindestrich als Trennzeichen voraussetzt.

#### Ein kurzer Hinweis zur Groß- und Kleinschreibung

Standardmäßig sind die Werte in Attribut-Selektoren (außer bei bestimmten HTML-Attributen) in den meisten Browsern case-sensitive, also sie unterscheiden zwischen Groß- und Kleinschreibung. `[type="text"]` würde ein Element mit `type="Text"` nicht finden.

Moderne CSS-Spezifikationen haben hierfür eine Lösung. Du kannst ein `i` vor der schließenden Klammer hinzufügen, um den Vergleich case-insensitive (unabhängig von der Groß- und Kleinschreibung) zu machen.

```css
/* Findet href-Werte, die auf .JPG, .jpg, .Jpg etc. enden */
a[href$=".jpg" i] {
  border: 2px solid gold;
}
```

#### Die Kombination macht's: Attribut-Selektoren und andere Selektoren

Die wahre Stärke von Attribut-Selektoren entfaltet sich, wenn du sie mit anderen Selektoren kombinierst. Du kannst sie an einen Typ-Selektor, eine Klasse oder eine ID anhängen, um deine Auswahl noch weiter zu verfeinern.

```css
/* Style nur externe Links, die auch die Klasse .button haben */
a.button[target="_blank"] {
  background-color: #ffc107;
}

/* Style nur <button>-Elemente, die deaktiviert sind */
button[disabled] {
  opacity: 0.5;
  cursor: not-allowed;
  background-color: #e9ecef;
}

/* Style nur das Bild im Header, das ein alt-Attribut hat */
header img[alt] {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
```

Attribut-Selektoren sind weit mehr als nur ein nettes Extra. Sie sind ein fundamentales Werkzeug, um deinen CSS-Code semantischer, wartbarer und mächtiger zu machen. Sie erlauben dir, direkt auf den Zustand und die Eigenschaften deiner HTML-Elemente zu reagieren, ohne auf zusätzliche Klassen oder IDs angewiesen zu sein. Damit öffnet sich eine Tür zu einem Styling, das intelligenter und kontextbezogener ist.
