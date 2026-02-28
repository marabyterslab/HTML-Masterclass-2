# Zugriff via CSS (attr)

### Zugriff via CSS: Die `attr()`-Funktion

Du hast im vorherigen Abschnitt gelernt, wie du mit `data-*`-Attributen benutzerdefinierte Daten direkt in deinem HTML-Markup speichern kannst. Das ist eine saubere und semantisch wertvolle Methode, um Informationen an Elemente zu heften, die über die reinen Standardattribute hinausgehen. Doch was nützt es, Daten zu speichern, wenn man sie nicht nutzen kann? Normalerweise würdest du jetzt vielleicht an JavaScript denken, um diese Daten auszulesen und dynamisch auf der Seite zu verwenden. Es gibt jedoch auch einen direkten Weg, diese Informationen rein mit CSS sichtbar zu machen und für das Styling zu nutzen: die `attr()`-Funktion.

Die `attr()`-Funktion in CSS ist eine Brücke zwischen deinem HTML-Markup und deinem Stylesheet. Sie ermöglicht es dir, den Wert eines beliebigen Attributs eines HTML-Elements auszulesen und ihn als Wert für eine CSS-Eigenschaft zu verwenden. Das klingt unglaublich mächtig – und das ist es potenziell auch. In der Praxis ist ihre Anwendung jedoch derzeit noch auf einen ganz bestimmten Bereich fokussiert.

#### Die Grundlagen: `attr()` in der `content`-Eigenschaft

Der häufigste und von allen Browsern zuverlässig unterstützte Anwendungsfall für `attr()` ist die Verwendung innerhalb der `content`-Eigenschaft. Diese Eigenschaft kommt ausschließlich bei den Pseudo-Elementen `::before` und `::after` zum Einsatz. Mit ihr kannst du zusätzliche Inhalte vor oder nach dem eigentlichen Inhalt eines Elements einfügen.

Stell dir vor, du hast ein Element mit einer wichtigen Zusatzinformation, die du in einem `data`-Attribut gespeichert hast:

```html
<div class="hinweis" data-info="Wichtige Zusatzinformation">
  Dies ist ein Hinweis.
</div>
```

Ohne CSS wäre die "Wichtige Zusatzinformation" für den Besucher unsichtbar. Mit der `attr()`-Funktion kannst du sie nun aber ganz einfach anzeigen lassen.

```css
.hinweis::after {
  content: " (" attr(data-info) ")";
  color: #777;
  font-style: italic;
  margin-left: 8px;
}
```

Was passiert hier?
1.  Wir wählen das Pseudo-Element `::after` des Elements mit der Klasse `.hinweis` aus.
2.  Wir setzen die `content`-Eigenschaft. Der Wert ist eine Kombination aus statischem Text und einem dynamischen Teil.
3.  Die Zeichenketten `" ("` und `")"` werden als fester Text eingefügt.
4.  `attr(data-info)` liest den Wert des `data-info`-Attributs aus dem HTML-Element aus – in diesem Fall "Wichtige Zusatzinformation" – und fügt ihn an dieser Stelle ein.

Das Ergebnis im Browser würde so aussehen:

> Dies ist ein Hinweis. (Wichtige Zusatzinformation)

Diese einfache Technik ist enorm nützlich. Du kannst damit Daten aus deinem HTML direkt in der Darstellung verwenden, ohne auch nur eine Zeile JavaScript schreiben zu müssen. Der Inhalt bleibt im HTML, wo er hingehört, und die Präsentation wird rein über CSS gesteuert.

#### Praktische Anwendungsfälle

Die Kombination aus `data-*`-Attributen, Pseudo-Elementen und `attr()` eröffnet eine Reihe kreativer und praktischer Möglichkeiten.

##### Einfache Tooltips ohne JavaScript

Ein klassisches Beispiel ist die Erstellung von Tooltips, die erscheinen, wenn man mit der Maus über ein Element fährt.

**HTML:**

```html
<p>
  Lerne mehr über <span class="tooltip" data-tooltip="Cascading Style Sheets">CSS</span>,
  um deine Webseiten zu gestalten.
</p>
```

**CSS:**

```css
.tooltip {
  position: relative; /* Wichtig für die Positionierung des Tooltips */
  border-bottom: 1px dotted #007bff;
  cursor: help;
}

/* Der Tooltip-Text (das Pseudo-Element) ist standardmäßig unsichtbar */
.tooltip::after {
  content: attr(data-tooltip);
  position: absolute;
  bottom: 125%; /* Positioniert den Tooltip über dem Element */
  left: 50%;
  transform: translateX(-50%); /* Zentriert den Tooltip horizontal */
  
  /* Styling für die Tooltip-Box */
  background-color: #333;
  color: #fff;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 0.9em;
  white-space: nowrap; /* Verhindert Zeilenumbrüche im Tooltip */
  
  /* Unsichtbar machen und für den Übergang vorbereiten */
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.2s, visibility 0.2s;
  z-index: 10;
}

/* Beim Hovern über das Elternelement wird der Tooltip sichtbar */
.tooltip:hover::after {
  opacity: 1;
  visibility: visible;
}
```

Hier nutzen wir den `:hover`-Zustand, um das `::after`-Pseudo-Element, das den Tooltip enthält, sichtbar zu machen. Der Inhalt des Tooltips wird dabei dynamisch aus dem `data-tooltip`-Attribut des `<span>`-Elements ausgelesen. Das ist eine elegante und performante Lösung für eine häufige UI-Anforderung.

##### Anzeige von Link-Zielen

Besonders für Druck-Stylesheets ist es nützlich, die URLs von Links direkt neben dem Linktext anzuzeigen, da man auf einem Ausdruck nicht auf einen Link klicken kann.

**HTML:**

```html
<a href="https://www.w3.org/TR/html5/">Zur offiziellen HTML5-Spezifikation</a>
```

**CSS (in einem Print-Stylesheet):**

```css
@media print {
  a[href^="http"]::after {
    content: " [" attr(href) "]";
    font-size: 0.8em;
    color: #555;
  }
}
```

Dieser CSS-Code sorgt dafür, dass im Drucklayout hinter jedem externen Link dessen URL in eckigen Klammern erscheint. Der Attribut-Selektor `[href^="http"]` stellt sicher, dass dies nur für absolute Links (die mit `http` beginnen) und nicht für interne Anker-Links geschieht.

##### Kombination von Attributen

Du kannst auch mehrere `attr()`-Aufrufe und Text in einer einzigen `content`-Eigenschaft kombinieren. Stell dir vor, du möchtest die Dimensionen eines Bildes direkt anzeigen, die in den `width`- und `height`-Attributen gespeichert sind.

**HTML:**

```html
<img src="landschaft.jpg" width="800" height="600" alt="Weite Landschaft">
```

**CSS:**

```css
img::after {
  display: block;
  content: "Größe: " attr(width) " x " attr(height) " Pixel";
  text-align: center;
  font-size: 0.9em;
  color: #666;
}
```

Das Ergebnis wäre der Text "Größe: 800 x 600 Pixel", der unter dem Bild angezeigt wird.

#### Ein Blick in die Zukunft: `attr()` außerhalb von `content`

Jetzt kommt der Teil, der die `attr()`-Funktion von "sehr nützlich" zu "revolutionär" machen könnte. Die offizielle CSS-Spezifikation (CSS Values and Units Module Level 5) sieht vor, dass `attr()` in Zukunft für **jede** CSS-Eigenschaft verwendet werden kann, nicht nur für `content`.

Die erweiterte Syntax sieht so aus:

```css
attr( <attribute-name> <type-or-unit>? [ , <fallback> ]? )
```

*   `<type-or-unit>`: Hier könntest du angeben, um welchen Datentyp es sich handelt, z. B. `color`, `px`, `em`, `deg` oder `%`. CSS wüsste dann, wie es den ausgelesenen String-Wert interpretieren muss.
*   `<fallback>`: Ein optionaler Wert, der verwendet wird, wenn das Attribut nicht vorhanden oder ungültig ist.

Stell dir die Möglichkeiten vor. Du könntest Farben, Größen, Positionen und vieles mehr direkt über HTML-Attribute steuern.

**Ein hypothetisches Beispiel (funktioniert heute noch nicht!):**

**HTML:**

```html
<div class="progress-bar" data-progress="75" data-color="#4CAF50"></div>
```

**Zukunfts-CSS:**

```css
.progress-bar {
  height: 20px;
  background-color: #eee;
  border-radius: 10px;
  
  /* Der Balken selbst wird über ein Pseudo-Element realisiert */
}

.progress-bar::before {
  content: '';
  display: block;
  height: 100%;
  border-radius: 10px;

  /* Hier kommt die Magie: */
  width: attr(data-progress %, 0%); /* Lese data-progress und interpretiere es als Prozentwert */
  background-color: attr(data-color color, #ccc); /* Lese data-color und interpretiere es als Farbe */
}
```

In diesem fiktiven Szenario würde der Fortschrittsbalken seine Breite und Farbe direkt aus den `data-*`-Attributen beziehen. Eine Änderung im HTML (`data-progress="90"`) würde sofort die Darstellung anpassen, ganz ohne JavaScript. Man könnte dynamische Komponenten bauen, deren Zustand direkt im DOM sichtbar und manipulierbar ist.

Zum aktuellen Zeitpunkt ist dies jedoch reine Zukunftsmusik. Die Browser-Unterstützung für die Verwendung von `attr()` außerhalb der `content`-Eigenschaft ist praktisch nicht vorhanden. Es ist eine der am sehnlichsten erwarteten CSS-Funktionen, aber es ist unklar, wann sie flächendeckend verfügbar sein wird.

Bis es so weit ist, bleibt `attr()` ein mächtiges, aber spezialisiertes Werkzeug. Es ist die erste Wahl, wenn es darum geht, in HTML gespeicherte Textdaten über CSS sichtbar zu machen. Für alles, was darüber hinausgeht – wie das dynamische Ändern von Farben, Größen oder Layouts basierend auf Attributen – musst du weiterhin auf JavaScript zurückgreifen. Dennoch zeigt `attr()` eindrucksvoll, wie eng HTML und CSS miteinander verwoben sein können und wie die Grenzen zwischen reiner Struktur und reiner Präsentation manchmal auf elegante Weise verschwimmen.
