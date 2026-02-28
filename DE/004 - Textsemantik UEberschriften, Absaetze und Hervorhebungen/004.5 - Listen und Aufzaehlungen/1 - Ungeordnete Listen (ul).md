# Ungeordnete Listen (ul)

### Kapitel 4.2: Ungeordnete Listen – Wenn die Reihenfolge keine Rolle spielt

Stell dir eine einfache Einkaufsliste vor: Milch, Eier, Brot, Butter. Spielt es eine Rolle, in welcher Reihenfolge du diese Dinge in deinen Korb legst? In den meisten Fällen nicht. Hauptsache, am Ende ist alles da. Genau für solche Szenarien, in denen die Reihenfolge der Elemente keine Rolle spielt, wurde in HTML die ungeordnete Liste geschaffen.

Eine ungeordnete Liste, im Englischen "unordered list", ist ein semantisches Element, das eine Sammlung von zusammengehörigen, aber nicht sequenziell geordneten Einträgen darstellt. Du signalisierst damit dem Browser und assistiven Technologien wie Screenreadern: "Hier kommt eine Gruppe von Dingen, die zusammengehören, aber ihre interne Anordnung ist nicht von entscheidender Bedeutung."

#### Die grundlegende Struktur: `<ul>` und `<li>`

Um eine ungeordnete Liste zu erstellen, benötigst du zwei wesentliche HTML-Tags:

1.  **`<ul>`**: Dieses Tag steht für "unordered list" und umschließt die gesamte Liste. Es ist der Container, der dem Browser sagt: "Alles, was jetzt kommt, ist Teil einer ungeordneten Aufzählung."
2.  **`<li>`**: Dieses Tag steht für "list item" (Listenelement) und umschließt jeden einzelnen Eintrag innerhalb der Liste. Jedes `<li>`-Element repräsentiert einen Aufzählungspunkt.

Schauen wir uns unsere Einkaufsliste als HTML-Code an. Die Struktur ist denkbar einfach und logisch.

```html
<ul>
  <li>Milch</li>
  <li>Eier</li>
  <li>Brot</li>
  <li>Butter</li>
</ul>
```

Wenn ein Browser diesen Code interpretiert, rendert er standardmäßig eine Liste, bei der jeder Eintrag mit einem Aufzählungspunkt (meist einem ausgefüllten Kreis, dem "disc") versehen ist:

*   Milch
*   Eier
*   Brot
*   Butter

Das Wichtigste, was du dir hier merken musst, ist die Hierarchie: Die `<li>`-Elemente sind immer direkte Kinder des `<ul>`-Elements. Du solltest niemals Text oder andere Elemente direkt zwischen `<ul>` und `<li>` platzieren.

#### Semantik vor Aussehen

Ein häufiges Missverständnis bei Anfängern ist, dass `<ul>` gewählt wird, *weil* man Punkte vor den Einträgen haben möchte. Das ist zwar der visuelle Standardeffekt, aber nicht der primäre Zweck des Tags. Der eigentliche Zweck ist die **semantische Bedeutung**.

Du teilst der Maschine mit, dass es sich um eine Liste von gleichwertigen Elementen handelt. Ein Screenreader wird einem sehbehinderten Nutzer beispielsweise vorlesen: "Liste mit vier Einträgen: Milch, Eier, Brot, Butter." Diese Information ist weitaus wertvoller als die reine visuelle Darstellung.

Das Aussehen der Liste kannst du jederzeit und vollständig mit CSS (Cascading Style Sheets) anpassen. Die Standard-Aufzählungszeichen sind nur ein Vorschlag des Browsers. Du könntest sie in Quadrate, Kreise oder sogar eigene Bilder ändern – oder sie komplett entfernen.

Hier ein kleines Beispiel, wie du mit CSS die Aufzählungszeichen verändern könntest:

```css
/* Ändert die Punkte in Quadrate */
ul {
  list-style-type: square;
}

/* Entfernt die Aufzählungszeichen komplett */
ul.navigation {
  list-style-type: none;
}
```

Die HTML-Struktur bleibt dabei unangetastet und semantisch korrekt. Diese Trennung von Inhalt (HTML) und Präsentation (CSS) ist eines der fundamentalen Prinzipien der Webentwicklung.

#### Verschachtelte Listen: Struktur innerhalb der Struktur

Was ist, wenn deine Liste komplexer wird? Angenommen, du möchtest nicht nur Brot kaufen, sondern hast die Wahl zwischen Vollkornbrot und Roggenbrot. Solche Unterpunkte kannst du durch Verschachtelung abbilden. Das bedeutet, du platzierst eine komplette `<ul>`-Liste *innerhalb* eines `<li>`-Elements der übergeordneten Liste.

Die Regel ist einfach und strikt: Eine neue Liste muss immer innerhalb eines `<li>`-Elements beginnen.

Schauen wir uns das an einem erweiterten Beispiel an:

```html
<ul>
  <li>Milch</li>
  <li>Eier</li>
  <li>
    Brot
    <ul>
      <li>Vollkornbrot</li>
      <li>Roggenbrot</li>
    </ul>
  </li>
  <li>Butter</li>
</ul>
```

Visuell wird der Browser diese Verschachtelung typischerweise durch Einrückung und oft auch durch ein anderes Aufzählungszeichen (z. B. einen unausgefüllten Kreis, "circle") darstellen:

*   Milch
*   Eier
*   Brot
    *   Vollkornbrot
    *   Roggenbrot
*   Butter

Diese Fähigkeit zur Verschachtelung macht Listen extrem mächtig, um hierarchische Informationen klar und strukturiert darzustellen, ohne dabei die semantische Bedeutung zu verlieren.

#### Praktische Anwendungsfälle für `<ul>`

Ungeordnete Listen sind eines der am häufigsten verwendeten Elemente im Web. Ihre Einsatzmöglichkeiten gehen weit über einfache Aufzählungen hinaus.

**Website-Navigation**
Der wohl wichtigste und häufigste Anwendungsfall für `<ul>` ist die Navigation einer Webseite. Eine Sammlung von Navigationslinks ("Home", "Über uns", "Produkte", "Kontakt") ist semantisch nichts anderes als eine Liste von Zielen, deren Reihenfolge in der Regel nicht streng sequenziell ist.

```html
<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about.html">Über uns</a></li>
    <li><a href="/products.html">Produkte</a></li>
    <li><a href="/contact.html">Kontakt</a></li>
  </ul>
</nav>
```

Mit CSS wird diese Liste dann so gestaltet, dass sie wie eine horizontale Menüleiste, ein vertikales Menü oder eine Burger-Navigation auf Mobilgeräten aussieht. Die zugrundeliegende HTML-Struktur bleibt aber eine saubere, semantische Liste.

**Feature-Listen**
Wenn du die Merkmale eines Produkts oder einer Dienstleistung aufzählst, ist eine `<ul>` die perfekte Wahl.

```html
<h3>Unsere Premium-Mitgliedschaft bietet:</h3>
<ul>
  <li>Unbegrenzten Zugriff auf alle Inhalte</li>
  <li>Werbefreies Erlebnis</li>
  <li>Exklusive Community-Events</li>
  <li>Monatlich kündbar</li>
</ul>
```

**Tag- oder Kategorie-Listen**
In einem Blog werden Artikeln oft Schlagwörter (Tags) oder Kategorien zugeordnet. Auch diese lassen sich hervorragend als ungeordnete Liste auszeichnen.

```html
<div class="tags">
  <h4>Schlagwörter:</h4>
  <ul>
    <li>HTML</li>
    <li>Semantik</li>
    <li>Webentwicklung</li>
  </ul>
</div>
```

#### Was du vermeiden solltest

Bei der Arbeit mit `<ul>` gibt es ein paar klassische Fehler, die du kennen und vermeiden solltest.

1.  **Missbrauch für Einrückungen:** Benutze niemals eine `<ul>`-Liste, nur um Text einzurücken. Einrückung ist eine rein visuelle Eigenschaft und sollte ausschließlich mit CSS (z. B. durch `padding` oder `margin`) gesteuert werden. Die Verwendung von HTML für gestalterische Zwecke ist semantisch falsch und schadet der Zugänglichkeit deiner Seite.

2.  **Inhalt außerhalb von `<li>`:** Wie bereits erwähnt, dürfen direkte Kinder eines `<ul>`-Elements nur `<li>`-Elemente sein. Dieser Code ist ungültig:

    ```html
    <!-- FALSCH! -->
    <ul>
      Ich bin ein verwaister Text.
      <li>Listeneintrag 1</li>
      <div>Ich bin ein Div und hier falsch.</div>
      <li>Listeneintrag 2</li>
    </ul>
    ```

    Jeder Inhalt, der zur Liste gehört, muss in sein eigenes `<li>`-Tag eingeschlossen werden.

Die ungeordnete Liste ist ein einfaches, aber unglaublich vielseitiges Werkzeug in deinem HTML-Repertoire. Indem du sie korrekt und für ihren semantischen Zweck einsetzt, schaffst du nicht nur visuell ansprechende, sondern auch gut strukturierte, zugängliche und maschinenlesbare Webseiten.
