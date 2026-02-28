# Inline-Auszeichnung von Daten

### Inline-Auszeichnung von Daten: Mehr Bedeutung für deine Inhalte

Stell dir vor, du schreibst eine Webseite über dein Lieblingsrezept. Du verwendest HTML-Tags, um die Überschrift (`<h1>`), die Zutatenliste (`<ul>`, `<li>`) und die Zubereitungsschritte (`<ol>`, `<li>`) zu strukturieren. Ein Mensch, der deine Seite besucht, versteht sofort, worum es geht. Er erkennt den Titel, die Zutaten und die Anleitung.

Doch was ist mit Maschinen? Eine Suchmaschine wie Google oder ein Screenreader sieht zunächst nur eine Ansammlung von Tags und Text. Sie weiß, dass `<h1>` eine Überschrift ist, aber sie weiß nicht, dass "Spaghetti Carbonara" der *Name* eines Rezepts ist. Sie sieht eine Liste von Zutaten, aber sie versteht nicht, dass "200g Pancetta" eine *Zutat* ist.

Genau hier kommt die Inline-Auszeichnung von Daten ins Spiel. Mit Techniken wie Microdata und RDFa kannst du deinen bestehenden HTML-Inhalten eine zusätzliche, für Maschinen lesbare Bedeutungsebene hinzufügen. Du sagst dem Browser, der Suchmaschine oder jedem anderen Computerprogramm ganz explizit: "Hey, dieser Text hier ist nicht nur irgendein Text, er ist der Name einer Person" oder "Diese Zahl ist eine Kalorienangabe". Du reicherst deine sichtbaren Inhalte mit unsichtbaren, aber wertvollen Metadaten an.

#### Microdata: Einfach und direkt

Microdata ist eine Spezifikation, die entwickelt wurde, um genau dieses Problem zu lösen. Die Idee ist, mit einfachen HTML-Attributen die Semantik deiner Inhalte zu beschreiben. Das Schöne daran ist, dass du dein vorhandenes HTML kaum verändern musst. Du fügst lediglich ein paar Attribute zu den Tags hinzu, die du ohnehin schon verwendest.

Die drei zentralen Attribute von Microdata sind:

1.  **`itemscope`**: Dieses boolesche Attribut (es braucht keinen Wert) markiert den Beginn eines neuen "Items" oder Objekts. Du setzt es auf das Container-Element, das alle Informationen über eine bestimmte Sache enthält – sei es eine Person, ein Produkt oder ein Event.
2.  **`itemtype`**: Dieses Attribut wird immer zusammen mit `itemscope` verwendet. Es gibt an, *welche Art* von Objekt du beschreibst. Der Wert ist eine URL, die auf eine Definition dieses Objekttyps verweist. In der Praxis stammt diese URL fast immer aus dem Vokabular von **schema.org**. Schema.org ist eine gemeinschaftliche Initiative von Suchmaschinenbetreibern, die ein riesiges, standardisiertes Vokabular für alle möglichen Dinge bereitstellt. Für eine Person würdest du zum Beispiel `https://schema.org/Person` verwenden.
3.  **`itemprop`**: Dieses Attribut wird innerhalb eines `itemscope`-Containers verwendet, um die einzelnen Eigenschaften (Properties) des Objekts zu kennzeichnen. Wenn du eine Person beschreibst (`itemtype=".../Person"`), wären mögliche Eigenschaften `name`, `jobTitle` oder `email`.

Schauen wir uns das an einem einfachen Beispiel an. Hier ist ein HTML-Schnipsel ohne Microdata:

```html
<div>
  <h3>Anna Schmidt</h3>
  <span>Softwareentwicklerin bei WebWorks GmbH</span>
  <a href="mailto:anna.schmidt@webworks.de">Kontakt aufnehmen</a>
</div>
```

Für einen Menschen ist das klar. Für eine Maschine ist es nur eine Überschrift, ein Text und ein Link. Jetzt reichern wir es mit Microdata an:

```html
<div itemscope itemtype="https://schema.org/Person">
  <h3 itemprop="name">Anna Schmidt</h3>
  <span itemprop="jobTitle">Softwareentwicklerin bei WebWorks GmbH</span>
  <a href="mailto:anna.schmidt@webworks.de" itemprop="email">Kontakt aufnehmen</a>
</div>
```

Was ist passiert?

*   Mit `<div itemscope itemtype="https://schema.org/Person">` sagen wir: "Alles innerhalb dieses `<div>` beschreibt ein Objekt vom Typ 'Person' gemäß der Definition von schema.org."
*   Mit `itemprop="name"` markieren wir "Anna Schmidt" als den Namen der Person.
*   Mit `itemprop="jobTitle"` kennzeichnen wir den Text als ihre Berufsbezeichnung.
*   Mit `itemprop="email"` weisen wir den Link ihrer E-Mail-Adresse zu.

Die Maschine versteht nun den Kontext. Sie weiß, dass "Anna Schmidt" ein Name ist und nicht etwa der Name eines Produkts. Dieser kleine Zusatzaufwand hat eine enorme Wirkung, insbesondere für die Suchmaschinenoptimierung (SEO).

#### RDFa: Flexibel und ausdrucksstark

RDFa (Resource Description Framework in Attributes) ist ein älterer und etwas mächtigerer Standard des W3C, der ein ähnliches Ziel verfolgt wie Microdata. Er ist Teil einer größeren Familie von Technologien rund um das "Semantic Web". Auch RDFa verwendet HTML-Attribute, um Daten zu strukturieren, aber die Namen der Attribute sind anders und die Syntax ist etwas flexibler.

Die wichtigsten Attribute in RDFa sind:

1.  **`vocab`**: Dieses Attribut wird auf einem übergeordneten Element platziert und definiert das Standardvokabular für alle darunterliegenden Elemente. Statt bei jeder Eigenschaft die volle URL anzugeben, legst du einmal fest: "Wir verwenden hier schema.org". Das macht den Code oft etwas sauberer.
2.  **`typeof`**: Dies ist das Äquivalent zu `itemtype` in Microdata. Es gibt den Typ des Objekts an, oft in Verbindung mit dem unter `vocab` definierten Vokabular.
3.  **`property`**: Dies entspricht `itemprop` in Microdata und kennzeichnet eine Eigenschaft des Objekts.

Lass uns unser Beispiel von Anna Schmidt nun mit RDFa umsetzen:

```html
<div vocab="https://schema.org/" typeof="Person">
  <h3 property="name">Anna Schmidt</h3>
  <span property="jobTitle">Softwareentwicklerin bei WebWorks GmbH</span>
  <a href="mailto:anna.schmidt@webworks.de" property="email">Kontakt aufnehmen</a>
</div>
```

Du siehst die Ähnlichkeiten sofort.

*   Mit `vocab="https://schema.org/"` legen wir das Vokabular für den gesamten `<div>`-Block fest.
*   Mit `typeof="Person"` deklarieren wir, dass es sich um eine Person handelt. Da wir das Vokabular schon definiert haben, reicht der Typenname allein.
*   `property="name"`, `property="jobTitle"` und `property="email"` funktionieren fast identisch zu `itemprop`.

Ob du Microdata oder RDFa verwendest, ist oft eine Frage der persönlichen Vorliebe oder der Projektanforderungen. Microdata gilt als etwas einfacher und einsteigerfreundlicher, während RDFa in komplexeren Szenarien mehr Flexibilität bieten kann. Beide werden von den großen Suchmaschinen verstanden und verarbeitet.

#### Der Lohn der Mühe: Warum das alles?

Du fragst dich vielleicht, warum du dir diese zusätzliche Arbeit machen solltest. Der größte unmittelbare Vorteil liegt in der Art und Weise, wie Suchmaschinen deine Inhalte verstehen und darstellen können. Wenn Google, Bing & Co. die strukturierten Daten auf deiner Seite erkennen, können sie sogenannte **Rich Snippets** (oder "Rich Results") in den Suchergebnissen anzeigen.

Du kennst das garantiert:

*   Du suchst nach einem Rezept und siehst direkt in den Suchergebnissen ein Bild, eine Bewertung mit Sternen, die Kochzeit und die Kalorienangabe.
*   Du suchst nach einem Produkt und bekommst den Preis, die Verfügbarkeit und Kundenbewertungen angezeigt.
*   Du suchst nach einem Event und siehst Datum, Uhrzeit und Veranstaltungsort.

All diese zusätzlichen Informationen stammen aus strukturierten Daten, die mit Microdata, RDFa oder JSON-LD (einer weiteren Methode, die Daten in einem `<script>`-Tag bündelt) ausgezeichnet wurden. Eine Seite mit Rich Snippets sticht aus der Masse heraus, hat eine höhere Klickrate und wird von Nutzern oft als vertrauenswürdiger wahrgenommen. Du gibst der Suchmaschine nicht nur Text, sondern Wissen – und sie belohnt dich dafür mit einer besseren Präsentation.

#### Verschachtelte Daten: Objekte in Objekten

Die Realität ist oft komplexer als ein einfaches Personenprofil. Ein Blogbeitrag hat einen Autor, der wiederum eine Person ist. Ein Rezept kann Nährwertangaben enthalten, die ein eigenes kleines Objekt darstellen. Sowohl Microdata als auch RDFa erlauben es dir, Objekte ineinander zu verschachteln.

Schauen wir uns ein etwas komplexeres Beispiel mit Microdata an: ein einfaches Rezept.

```html
<div itemscope itemtype="https://schema.org/Recipe">
  <h2 itemprop="name">Klassische Tomatensuppe</h2>

  <p itemprop="description">Eine einfache und schnelle Tomatensuppe, perfekt für kalte Tage.</p>
  
  <div itemprop="author" itemscope itemtype="https://schema.org/Person">
    <p>Rezept von: <span itemprop="name">Max Koch</span></p>
  </div>

  <h3>Zutaten:</h3>
  <ul>
    <li itemprop="recipeIngredient">1 kg reife Tomaten</li>
    <li itemprop="recipeIngredient">1 Zwiebel</li>
    <li itemprop="recipeIngredient">2 Knoblauchzehen</li>
    <li itemprop="recipeIngredient">500 ml Gemüsebrühe</li>
  </ul>

  <h3>Nährwertangaben:</h3>
  <div itemprop="nutrition" itemscope itemtype="https://schema.org/NutritionInformation">
    <p>
      Kalorien: <span itemprop="calories">120 kcal</span>
    </p>
  </div>
</div>
```

In diesem Beispiel siehst du deutlich, wie die Verschachtelung funktioniert:

1.  Das äußere `<div>` definiert das Hauptobjekt: ein `Recipe`.
2.  Innerhalb dieses Rezepts gibt es eine Eigenschaft `author` (`itemprop="author"`). Der Wert dieser Eigenschaft ist aber kein einfacher Text, sondern ein weiteres, eigenständiges Objekt. Deshalb fügen wir hier erneut `itemscope` und `itemtype="https://schema.org/Person"` hinzu, um den Autor als Person zu definieren. Diese Person hat wiederum ihre eigene Eigenschaft `name`.
3.  Ähnlich verfahren wir mit den Nährwertangaben (`nutrition`). Wir definieren ein neues Objekt vom Typ `NutritionInformation` und geben darin die Eigenschaft `calories` an.

Durch diese Verschachtelung kannst du komplexe Beziehungen und Datenstrukturen direkt in deinem HTML abbilden. Du baust eine maschinenlesbare Wissensdatenbank direkt in deine Webseite ein, ohne die für den Menschen sichtbare Darstellung zu beeinträchtigen. Das ist die wahre Stärke der Inline-Daten-Auszeichnung.
