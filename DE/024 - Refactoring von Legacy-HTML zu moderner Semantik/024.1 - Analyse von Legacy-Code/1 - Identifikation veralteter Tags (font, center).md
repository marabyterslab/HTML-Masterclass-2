# Identifikation veralteter Tags (font, center)

### Relikte der Vergangenheit: Identifikation veralteter Tags wie `<font>` und `<center>`

Wenn du dich durch den Quellcode älterer Webseiten bewegst, wirst du unweigerlich auf seltsame Artefakte stoßen – HTML-Tags, die heute kaum noch jemand verwendet. Sie sind wie Fossilien aus einer früheren Ära des Webs, als die Trennung von Inhalt und Design noch in den Kinderschuhen steckte. Zwei der prominentesten Vertreter dieser ausgestorbenen Spezies sind die Tags `<font>` und `<center>`. Sie zu erkennen und ihre Rolle zu verstehen, ist der erste entscheidende Schritt, um Legacy-Code in ein modernes, wartbares und semantisches Gewand zu kleiden.

Diese Tags sind nicht einfach nur "alt". Sie sind offiziell als "veraltet" (deprecated) eingestuft. Das bedeutet, dass sie aus dem aktuellen HTML-Standard entfernt wurden. Moderne Browser zeigen sie aus Gründen der Abwärtskompatibilität zwar meist noch korrekt an, doch ihre Verwendung gilt als schlechter Stil und ist mit erheblichen Nachteilen verbunden. Das Kernproblem liegt darin, dass sie Präsentationslogik – also Anweisungen, wie etwas aussehen soll – direkt in die HTML-Struktur einbetten. Genau das wollen wir im modernen Webdesign unter allen Umständen vermeiden.

#### Der `<font>`-Tag: Ein Dinosaurier der Webtypografie

In den späten 90er-Jahren, lange bevor CSS zur dominierenden Kraft für das Webdesign wurde, war der `<font>`-Tag das Mittel der Wahl, um das Aussehen von Text zu verändern. Mit ihm konntest du Schriftart, Größe und Farbe direkt im HTML-Dokument festlegen.

Ein typisches Beispiel aus dieser Zeit könnte so aussehen:

```html
<p>Willkommen auf meiner Homepage! Hier findest du Informationen über meine Hobbys. 
Besonders interessant ist der Bereich über <font face="Comic Sans MS" color="blue" size="4">seltene Briefmarken</font>. 
Vergiss nicht, dich ins <font color="red">Gästebuch</font> einzutragen!</p>
```

Auf den ersten Blick mag das harmlos erscheinen. Der Code tut, was er soll: Er hebt bestimmte Textteile farblich oder durch eine andere Schriftart hervor. Doch bei genauerer Betrachtung offenbaren sich die gravierenden Nachteile dieses Ansatzes:

1.  **Vermischung von Struktur und Präsentation:** Das HTML-Dokument sollte ausschließlich die Struktur und die Bedeutung deines Inhalts beschreiben. Ob ein Text blau, rot oder in "Comic Sans MS" dargestellt wird, ist eine reine Design-Entscheidung. Indem du diese Information direkt ins HTML schreibst, blähst du den Code unnötig auf und machst ihn schwer lesbar. Die eigentliche Struktur – ein Absatz mit Text – wird von Stil-Anweisungen durchsetzt.

2.  **Katastrophale Wartbarkeit:** Stell dir vor, du hast eine Webseite mit 100 Unterseiten, auf der alle wichtigen Hinweise mit `<font color="red">` markiert sind. Nun entscheidest du, dass diese Hinweise besser in einem dunklen Orange dargestellt werden sollten, um besser zum neuen Logo zu passen. Die Konsequenz? Du musst 100 HTML-Dateien manuell öffnen und jede einzelne Instanz des `<font>`-Tags ändern. Ein Albtraum für jeden Entwickler.

3.  **Mangelnde Flexibilität und Skalierbarkeit:** Die Attribute des `<font>`-Tags sind starr. `size="4"` ist ein absoluter Wert, der auf verschiedenen Geräten und bei unterschiedlichen Benutzereinstellungen zu inkonsistenten Ergebnissen führt. Modernes Webdesign setzt auf relative Einheiten (wie `em` oder `rem`), die sich an die Umgebung anpassen und so für ein responsives und zugängliches Design sorgen.

4.  **Fehlende semantische Bedeutung:** Der `<font>`-Tag sagt nichts darüber aus, *warum* ein Text anders aussieht. Ist der rote Text eine Warnung? Eine wichtige Hervorhebung? Oder einfach nur eine dekorative Spielerei? Suchmaschinen und assistiven Technologien wie Screenreadern fehlen diese Informationen. Sie sehen nur Text, der irgendwie anders aussieht, können aber keine Bedeutung daraus ableiten.

**Die moderne Lösung: CSS**

Die korrekte Herangehensweise besteht darin, die Stil-Anweisungen vollständig in eine separate CSS-Datei auszulagern. Im HTML-Code markierst du den entsprechenden Textabschnitt mit einem semantisch neutralen Element wie `<span>` und gibst ihm eine aussagekräftige Klasse.

Das obige Beispiel würde in modernem HTML und CSS so aussehen:

**HTML:**
```html
<p>Willkommen auf meiner Homepage! Hier findest du Informationen über meine Hobbys. 
Besonders interessant ist der Bereich über <span class="thema-highlight">seltene Briefmarken</span>. 
Vergiss nicht, dich ins <span class="call-to-action">Gästebuch</span> einzutragen!</p>
```

**CSS:**
```css
.thema-highlight {
  font-family: "Comic Sans MS", cursive; /* Fallback-Schriftart nicht vergessen */
  color: blue;
  font-size: 1.2em; /* Relative Größe für bessere Skalierbarkeit */
}

.call-to-action {
  color: red;
  font-weight: bold;
}
```

Die Vorteile sind offensichtlich: Das HTML ist sauber und beschreibt nur noch die Struktur. Die Klassennamen `thema-highlight` und `call-to-action` geben dem Inhalt eine Bedeutung. Und wenn du das Design ändern möchtest, musst du nur eine einzige Zeile in deiner CSS-Datei anpassen, und die Änderung wird auf der gesamten Webseite wirksam.

#### Der `<center>`-Tag: Starre Ausrichtung in einer flexiblen Welt

Ein weiteres häufig anzutreffendes Relikt ist der `<center>`-Tag. Sein Name ist Programm: Alles, was du zwischen `<center>` und `</center>` packst, wird vom Browser horizontal zentriert.

Ein klassisches Anwendungsbeispiel:

```html
<center>
  <img src="logo.gif" alt="Mein cooles Logo">
  <h1>Die beste Webseite des Internets</h1>
  <p>Erstellt im Jahr 1998</p>
</center>
```

Auch hier gilt dasselbe Grundproblem wie beim `<font>`-Tag: Die Ausrichtung eines Elements ist eine reine Präsentationsangelegenheit und hat im HTML-Markup nichts zu suchen. Die Nachteile sind praktisch identisch:

1.  **Präsentationslogik im HTML:** Der `<center>`-Tag ist ein reiner Styling-Befehl. Er sagt dem Browser, *wie* etwas aussehen soll, nicht, *was* es ist.

2.  **Mangelnde Kontrolle:** Der Tag ist ein grobes Werkzeug. Er zentriert gnadenlos alles, was sich in ihm befindet. Was aber, wenn du nur die Überschrift `<h1>` zentrieren möchtest, der Absatz darunter aber linksbündig bleiben soll? Mit dem `<center>`-Tag ist das nicht ohne umständliche Verschachtelungen möglich.

3.  **Konflikt mit modernen Layout-Methoden:** In einer Welt von Flexbox und CSS Grid, die uns eine präzise und flexible Kontrolle über das Layout auf zwei Achsen geben, wirkt der `<center>`-Tag wie ein Werkzeug aus der Steinzeit. Er lässt sich schlecht mit diesen modernen Techniken kombinieren und führt oft zu unerwartetem Verhalten.

**Die moderne Lösung: CSS**

Für das Zentrieren von Inhalten bietet CSS eine Fülle von Möglichkeiten, die weitaus mächtiger und präziser sind.

Um Text innerhalb eines Block-Elements zu zentrieren, verwendest du die Eigenschaft `text-align`:

**HTML:**
```html
<div class="header-bereich">
  <img src="logo.gif" alt="Mein cooles Logo">
  <h1>Die beste Webseite des Internets</h1>
  <p class="copyright">Erstellt im Jahr 1998</p>
</div>
```

**CSS:**
```css
.header-bereich {
  text-align: center;
}

/* Falls der Absatz doch linksbündig sein soll: */
.copyright {
  text-align: left;
}
```

Möchtest du ein Block-Element selbst (wie z. B. den gesamten `.header-bereich`-Container) innerhalb seines Elternelements zentrieren, gibt es ebenfalls elegante CSS-Lösungen. Ein klassischer Weg ist `margin: auto;` für Elemente mit fester Breite, während Flexbox die modernste und flexibelste Methode darstellt:

**CSS mit Flexbox:**
```css
body {
  display: flex;
  justify-content: center; /* Zentriert das Kind-Element horizontal */
}

.header-bereich {
  width: 80%; /* Beispielhafte Breite */
}
```
Diese CSS-Methoden geben dir die volle Kontrolle und halten dein HTML sauber und semantisch korrekt.

#### Weitere veraltete Präsentations-Attribute

Neben ganzen Tags wirst du in Legacy-Code auch eine Vielzahl veralteter Attribute finden, die direktes Styling im HTML ermöglichen. Halte Ausschau nach folgenden Übeltätern:

*   `bgcolor`: Legt die Hintergrundfarbe fest. ` <body bgcolor="yellow">`
*   `align`: Richtet Inhalte aus. `<p align="right">`
*   `width`, `height`, `border`: Werden oft bei Bildern (`<img>`) oder Tabellen (`<table>`) verwendet, um deren Dimensionen und Rahmen festzulegen.

All diese Aufgaben werden heute ausnahmslos mit CSS erledigt:

| Veraltetes HTML-Attribut             | Moderne CSS-Entsprechung                    |
| ------------------------------------ | ------------------------------------------- |
| `<body bgcolor="#f0f0f0">`           | `body { background-color: #f0f0f0; }`       |
| `<p align="center">`                 | `p { text-align: center; }`                 |
| `<hr color="blue" width="50%">`      | `hr { border-color: blue; width: 50%; }`    |
| `<img src="bild.jpg" border="2">`    | `img { border: 2px solid black; }`          |

Die Identifikation dieser veralteten Tags und Attribute ist der erste und wichtigste Schritt im Refactoring-Prozess. Jedes Mal, wenn du auf ein `<font>`, `<center>` oder ein `bgcolor`-Attribut stößt, sollten bei dir die Alarmglocken läuten. Sie sind klare Indikatoren für Code, der die fundamentalen Prinzipien der Trennung von Inhalt und Präsentation verletzt. Indem du sie aufspürst und durch moderne, CSS-basierte Lösungen ersetzt, machst du deinen Code nicht nur sauberer und professioneller, sondern auch unendlich viel einfacher zu warten und für die Zukunft zu rüsten.
