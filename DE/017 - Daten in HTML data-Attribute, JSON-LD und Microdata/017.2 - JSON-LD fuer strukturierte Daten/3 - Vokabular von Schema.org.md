# Vokabular von Schema.org

### Das Vokabular von Schema.org: Die gemeinsame Sprache des Webs

Du weißt jetzt, wie du mit JSON-LD strukturierte Daten in deine Webseite einbetten kannst. Das ist die Grammatik. Aber welche Wörter sollst du verwenden, um einer Suchmaschine zu sagen: „Dies hier ist ein Rezept, das ist die Kochzeit und hier sind die Zutaten“? Genau hier kommt Schema.org ins Spiel. Es ist das gemeinsame Vokabular – das Wörterbuch –, auf das sich die großen Suchmaschinen wie Google, Bing, Yahoo! und Yandex geeinigt haben.

Stell es dir wie eine universelle Sprache vor, die Maschinen verstehen. Wenn du diese Sprache sprichst, können Suchmaschinen den Inhalt deiner Seite nicht nur indizieren, sondern wirklich verstehen. Das Ergebnis sind die Rich Snippets in den Suchergebnissen: Bewertungssterne, Kochzeiten, Veranstaltungsdaten und vieles mehr. Schema.org ist also kein Konkurrenzformat zu JSON-LD oder Microdata, sondern der Inhalt, den du in diese Formate einfüllst.

#### Die Grundbausteine: Typen und Eigenschaften

Das gesamte Vokabular von Schema.org basiert auf zwei einfachen Konzepten: **Typen** (Types) und **Eigenschaften** (Properties).

1.  **Typen (Types):** Ein Typ ist eine Definition für eine bestimmte Art von „Ding“. Das kann etwas Abstraktes wie ein `Event` (Veranstaltung) oder etwas sehr Konkretes wie ein `Restaurant` oder ein `Product` (Produkt) sein. Typen sind wie die Substantive in unserer Sprache. Sie sagen, *was* etwas ist.

2.  **Eigenschaften (Properties):** Jede Sache hat Merkmale. Ein `Product` hat einen `name` (Namen), einen `price` (Preis) und eine `description` (Beschreibung). Diese Merkmale sind die Eigenschaften. Sie beschreiben den Typ genauer und sind wie die Adjektive oder Attribute einer Sache.

Die wahre Stärke von Schema.org liegt in der hierarchischen Organisation dieser Typen.

#### Der Stammbaum der Dinge: Die Hierarchie von Schema.org

An der Spitze des gesamten Vokabulars steht der allgemeinste Typ, den es gibt: `Thing`. Jedes einzelne Konzept in Schema.org ist eine Unterart von `Thing`. Man könnte sagen, `Thing` ist der Urahn aller Typen.

Von `Thing` zweigen spezifischere Typen ab, zum Beispiel:

*   `CreativeWork`: Für alles, was kreativ erschaffen wurde (Bücher, Filme, Artikel, Rezepte).
*   `Event`: Für Veranstaltungen (Konzerte, Festivals, Konferenzen).
*   `Organization`: Für Organisationen (Firmen, Vereine, Schulen).
*   `Person`: Für eine Person.
*   `Place`: Für einen Ort (Städte, Restaurants, Sehenswürdigkeiten).
*   `Product`: Für ein Produkt, das verkauft wird.

Diese Hierarchie geht noch viel tiefer. Ein `CreativeWork` kann zum Beispiel weiter spezifiziert werden als:

*   `Article` (Artikel)
    *   `NewsArticle` (Nachrichtenartikel)
    *   `BlogPosting` (Blogbeitrag)
*   `Book` (Buch)
*   `Movie` (Film)
*   `Recipe` (Rezept)

Warum ist das wichtig? Weil ein spezifischerer Typ alle Eigenschaften seines „Eltern-Typs“ erbt. Ein `Recipe` ist auch ein `CreativeWork` und somit auch ein `Thing`. Es erbt also Eigenschaften wie `name` und `description` von `Thing` und `CreativeWork`, hat aber zusätzlich noch eigene, spezifische Eigenschaften wie `cookTime` (Kochzeit) oder `recipeIngredient` (Zutat).

Dein Ziel sollte immer sein, den spezifischsten Typ zu verwenden, der auf deinen Inhalt zutrifft. Beschreibst du ein Restaurant, verwende `Restaurant`, nicht das allgemeinere `LocalBusiness` oder das noch allgemeinere `Organization`. Je genauer du bist, desto mehr wertvolle Informationen lieferst du den Suchmaschinen.

#### Ein praktisches Beispiel: Ein Blogartikel

Schauen wir uns an, wie wir einen einfachen Blogartikel mit dem Vokabular von Schema.org beschreiben würden. Der spezifischste Typ dafür wäre `BlogPosting`. Ein `BlogPosting` ist eine Art von `Article`, das wiederum ein `CreativeWork` ist.

Ein `BlogPosting` hat nützliche Eigenschaften wie:

*   `headline`: Die Überschrift des Artikels.
*   `author`: Der Autor des Artikels.
*   `datePublished`: Das Veröffentlichungsdatum.
*   `image`: Ein repräsentatives Bild.
*   `articleBody`: Der eigentliche Textinhalt.

Jetzt kommt der interessante Teil: Der Wert einer Eigenschaft muss nicht immer ein einfacher Text oder eine Zahl sein. Es kann auch ein anderer Schema.org-Typ sein!

Die Eigenschaft `author` erwartet zum Beispiel den Typ `Person` oder `Organization`. Anstatt also nur den Namen des Autors als Text anzugeben, können wir ein ganzes `Person`-Objekt erstellen, das wiederum eigene Eigenschaften wie `name` und `url` (z. B. zu einem Autorenprofil) hat.

So könnte das komplette JSON-LD-Skript für einen Blogartikel aussehen:

```json
{
  "@context": "https://schema.org",
  "@type": "BlogPosting",
  "headline": "Die Kunst der perfekten Pizza: Ein Leitfaden für Anfänger",
  "datePublished": "2023-10-27",
  "image": "https://example.com/images/pizza.jpg",
  "author": {
    "@type": "Person",
    "name": "Alex Schmidt",
    "url": "https://example.com/autoren/alex-schmidt"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Food-Blog Deluxe",
    "logo": {
      "@type": "ImageObject",
      "url": "https://example.com/images/logo.png"
    }
  },
  "description": "Lerne Schritt für Schritt, wie du zu Hause eine Pizza backst, die so gut schmeckt wie in deiner Lieblingspizzeria."
}
```

Du siehst hier die Verschachtelung:
*   Der Haupttyp ist `BlogPosting`.
*   Die Eigenschaft `author` enthält ein Objekt vom Typ `Person`.
*   Die Eigenschaft `publisher` (Herausgeber) enthält ein Objekt vom Typ `Organization`.
*   Das Logo des Herausgebers ist wiederum ein eigenes Objekt vom Typ `ImageObject`, das die `url` zum Bild enthält.

Diese Verschachtelung erlaubt es dir, extrem detaillierte und maschinenlesbare Beziehungen zwischen den Dingen auf deiner Seite herzustellen.

#### Noch ein Beispiel: Ein Produkt

Ein weiteres extrem häufiges Anwendungsfeld ist die Auszeichnung von Produkten in einem Onlineshop. Der Typ hierfür ist `Product`.

Wichtige Eigenschaften eines `Product` sind:

*   `name`: Der Name des Produkts.
*   `image`: Produktbilder.
*   `description`: Die Produktbeschreibung.
*   `sku`: Die Artikelnummer (Stock Keeping Unit).
*   `brand`: Die Marke, oft als Typ `Brand` oder `Organization` ausgezeichnet.
*   `offers`: Einer der wichtigsten Punkte – die Angebotsinformationen.

Die Eigenschaft `offers` erwartet einen Typ `Offer`. Hier werden Preis, Währung, Verfügbarkeit und Zustand des Produkts definiert. Warum ist das ein eigener Typ? Weil ein Produkt theoretisch mehrere Angebote haben könnte (z. B. von verschiedenen Händlern auf einem Marktplatz oder in verschiedenen Zuständen wie „neu“ und „gebraucht“).

Ein JSON-LD-Beispiel für ein Produkt könnte so aussehen:

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Professioneller Barista-Kaffeevollautomat",
  "image": "https://example.com/images/kaffeemaschine.jpg",
  "description": "Dieser Kaffeevollautomat bringt das Café-Erlebnis direkt in deine Küche. Mit integriertem Mahlwerk und Milchschaumsystem.",
  "sku": "KB-4815162342",
  "brand": {
    "@type": "Brand",
    "name": "Kaffee-König"
  },
  "offers": {
    "@type": "Offer",
    "priceCurrency": "EUR",
    "price": "799.99",
    "availability": "https://schema.org/InStock",
    "priceValidUntil": "2024-12-31"
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.8",
    "reviewCount": "256"
  }
}
```

Beachte hier ein paar Details:
*   Die `availability` (Verfügbarkeit) ist kein freier Text, sondern eine URL, die auf eine vordefinierte Konstante von Schema.org verweist (`https://schema.org/InStock`). Andere Optionen wären `OutOfStock`, `PreOrder` etc. Das sorgt für Eindeutigkeit.
*   Wir haben auch eine `aggregateRating` (zusammengefasste Bewertung) hinzugefügt, was wiederum ein eigener Typ ist. Hier gibst du den Durchschnittswert (`ratingValue`) und die Anzahl der Bewertungen (`reviewCount`) an. Genau diese Information nutzt Google, um die Bewertungssterne in den Suchergebnissen anzuzeigen.

#### Wie du die richtigen Typen und Eigenschaften findest

Du musst dieses riesige Vokabular natürlich nicht auswendig lernen. Dein wichtigstes Werkzeug ist die offizielle Webseite: **schema.org**.

Dort kannst du die Hierarchie durchsuchen oder direkt nach dem suchen, was du beschreiben möchtest. Wenn du zum Beispiel ein Rezept hast, suche einfach nach „recipe“. Du landest auf der Seite für den Typ `Recipe`.

Dort findest du:
1.  Eine kurze Beschreibung, was ein `Recipe` ist.
2.  Eine Liste aller spezifischen Eigenschaften für diesen Typ (z. B. `cookTime`, `recipeInstructions`).
3.  Eine Liste der geerbten Eigenschaften von `CreativeWork` und `Thing`.
4.  Für jede Eigenschaft wird der „erwartete Typ“ (Expected Type) angegeben. Das sagt dir, ob die Eigenschaft einen Text (`Text`), eine Zahl (`Number`), ein Datum (`Date`) oder einen anderen Schema.org-Typ (z. B. `Person`) als Wert erwartet.

Die Webseite ist dein Nachschlagewerk. Nutze sie, um die passenden Begriffe für deinen Inhalt zu finden und sicherzustellen, dass du die Eigenschaften korrekt verwendest.

Schema.org ist kein starres Regelwerk, sondern ein mächtiges Werkzeug. Es entwickelt sich ständig weiter, um neue Arten von Informationen im Web beschreiben zu können. Indem du dieses Vokabular nutzt, machst du deine Webseite zu einem wertvolleren und verständlicheren Teil des semantischen Webs – ein Web, in dem Maschinen nicht nur lesen, sondern verstehen.
