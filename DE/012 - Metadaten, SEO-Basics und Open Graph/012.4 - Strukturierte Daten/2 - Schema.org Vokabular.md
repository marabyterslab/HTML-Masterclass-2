# Schema.org Vokabular

### Das Schema.org Vokabular: Die gemeinsame Sprache für strukturierte Daten

Nachdem du das Konzept der strukturierten Daten verstanden hast – also die Idee, Suchmaschinen und anderen Programmen präzise Informationen über den Inhalt deiner Seite zu liefern – stellt sich die nächste logische Frage: In welcher Sprache kommunizieren wir diese Informationen? Wenn jeder Webentwickler seine eigenen Begriffe für ein „Rezept“, ein „Produkt“ oder ein „Event“ erfinden würde, hätten wir ein heilloses Durcheinander. Die Maschinen wüssten nicht, ob „Hersteller“, „Marke“ oder „Produzent“ dasselbe bedeuten.

Genau hier kommt Schema.org ins Spiel. Stell dir Schema.org wie ein riesiges, gemeinsames Wörterbuch vor, das von den größten Akteuren der Suchmaschinenwelt – Google, Microsoft (Bing), Yahoo! und Yandex – gemeinsam entwickelt und gepflegt wird. Es ist ein standardisiertes Vokabular, das eine Hierarchie von Typen und Eigenschaften definiert, um Entitäten, Aktionen und Beziehungen im Web zu beschreiben. Indem du dieses Vokabular nutzt, sprichst du eine Sprache, die Suchmaschinen garantiert verstehen.

#### Die grundlegende Struktur: Typen und Eigenschaften

Das gesamte Schema.org-Vokabular basiert auf einem einfachen, aber mächtigen Prinzip: Alles ist ein `Thing`. Das ist der grundlegendste Typ, von dem alle anderen, spezifischeren Typen abgeleitet sind. Ein `Thing` hat einige grundlegende Eigenschaften wie `name` (Name), `description` (Beschreibung) oder `url` (URL).

Von diesem universellen `Thing` zweigen sich spezifischere Kategorien ab. Einige der wichtigsten Oberkategorien sind:

*   **`CreativeWork`**: Für alles, was erschaffen wurde, wie ein `Article`, ein `Book`, ein `Movie` oder ein `Recipe`.
*   **`Event`**: Für zeitlich begrenzte Ereignisse, wie ein `Concert`, ein `Festival` oder ein `BusinessEvent`.
*   **`Organization`**: Für Organisationen, wie ein `Corporation` (Unternehmen), eine `NGO` (Nichtregierungsorganisation) oder ein `LocalBusiness` (lokales Geschäft).
*   **`Person`**: Für eine einzelne Person.
*   **`Place`**: Für einen geografischen Ort oder ein Gebäude.
*   **`Product`**: Für ein Produkt, das verkauft werden kann.

Diese Hierarchie ermöglicht es dir, so spezifisch wie nötig zu sein. Ein Blogbeitrag ist nicht nur ein `Thing`, er ist ein `CreativeWork`, genauer gesagt ein `Article` und vielleicht sogar noch spezifischer ein `BlogPosting`. Je genauer du den Typ definierst, desto besser können Suchmaschinen den Inhalt einordnen.

Jeder dieser Typen hat eine Reihe von zugehörigen **Eigenschaften (Properties)**. Ein `Movie` hat zum Beispiel Eigenschaften wie `director` (Regisseur), `actor` (Schauspieler) und `duration` (Dauer). Eine Eigenschaft wie `director` erwartet dabei nicht einfach nur einen beliebigen Text, sondern idealerweise einen weiteren Schema-Typ, nämlich eine `Person`. So entstehen logische Verknüpfungen: Dieser `Movie` (Film) hat einen `director` (Regisseur), der eine `Person` ist, die wiederum einen `name` (Namen) hat.

#### Die Implementierung mit JSON-LD

Während es historisch mehrere Formate gab, um Schema.org in HTML einzubetten (wie Microdata und RDFa), hat sich **JSON-LD (JavaScript Object Notation for Linked Data)** als der empfohlene Standard durchgesetzt. Der große Vorteil von JSON-LD ist, dass du die strukturierten Daten sauber vom sichtbaren HTML-Inhalt trennen kannst. Du fügst einfach ein `<script>`-Tag in den `<head>` oder `<body>` deiner HTML-Datei ein und definierst dort alle Metadaten in einem klar lesbaren JSON-Format. Das macht den Code übersichtlicher und einfacher zu warten.

Schauen wir uns ein konkretes Beispiel an. Stell dir vor, du hast eine Webseite mit einem einfachen Rezept für Pfannkuchen. Ohne strukturierte Daten sehen Suchmaschinen nur eine Ansammlung von Text. Mit Schema.org und JSON-LD kannst du ihnen exakt mitteilen: „Das hier ist ein Rezept, es hat diesen Namen, diese Zutaten und diese Zubereitungszeit.“

So könnte der JSON-LD-Code dafür aussehen:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Recipe",
  "name": "Klassische Eierpfannkuchen",
  "author": {
    "@type": "Person",
    "name": "Max Mustermann"
  },
  "datePublished": "2023-10-27",
  "description": "Ein einfaches und schnelles Rezept für leckere, fluffige Pfannkuchen.",
  "prepTime": "PT10M",
  "cookTime": "PT15M",
  "totalTime": "PT25M",
  "recipeYield": "4 Portionen",
  "recipeIngredient": [
    "250g Mehl",
    "500ml Milch",
    "3 Eier",
    "1 Prise Salz"
  ],
  "recipeInstructions": [
    {
      "@type": "HowToStep",
      "text": "Mehl, Milch, Eier und Salz in einer Schüssel zu einem glatten Teig verrühren."
    },
    {
      "@type": "HowToStep",
      "text": "Etwas Öl in einer Pfanne erhitzen."
    },
    {
      "@type": "HowToStep",
      "text": "Eine Kelle Teig in die heiße Pfanne geben und von beiden Seiten goldbraun backen."
    }
  ],
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.8",
    "reviewCount": "125"
  }
}
</script>
```

Lass uns diesen Code kurz aufschlüsseln:
*   `@context`: Definiert das Vokabular, das wir verwenden – in diesem Fall Schema.org.
*   `@type`: Gibt den Haupttyp des Elements an, das wir beschreiben. Hier ist es ein `Recipe`.
*   `name`, `description`, `datePublished`: Das sind einfache Eigenschaften mit Text- oder Datumswerten.
*   `author`: Hier siehst du ein verschachteltes Objekt. Der Autor ist nicht nur ein Name, sondern eine eigene Entität vom Typ `Person`.
*   `prepTime`, `cookTime`: Die Zeitangaben folgen dem ISO 8601 Format für Zeitdauern. `PT10M` steht für "Period of Time, 10 Minutes".
*   `recipeIngredient`: Eine Eigenschaft, die eine Liste (ein Array) von Werten erwartet – in diesem Fall die Zutaten als einfache Textzeilen.
*   `recipeInstructions`: Eine Liste von Schritten. Jeder Schritt ist selbst wieder ein Schema-Typ (`HowToStep`) mit einer `text`-Eigenschaft.
*   `aggregateRating`: Ein weiteres verschachteltes Objekt, das eine zusammengefasste Bewertung darstellt. Genau diese Informationen nutzt Google, um die bekannten Bewertungssterne in den Suchergebnissen anzuzeigen.

#### Gängige Anwendungsfälle und ihre Typen

Das Vokabular von Schema.org ist riesig und deckt unzählige Nischen ab. Für den Anfang sind jedoch einige Typen besonders relevant, da sie häufig zu sogenannten **Rich Results** (früher Rich Snippets) in den Suchergebnissen führen – also den optisch angereicherten Ergebnissen mit Sternen, Bildern oder Zusatzinformationen.

*   **`Article` / `BlogPosting`**: Unverzichtbar für Blogs und Nachrichtenseiten. Wichtige Eigenschaften sind `headline`, `image`, `author` und `datePublished`. Suchmaschinen können diese Informationen nutzen, um den Artikel prominenter in News-Karussells oder Top-Stories anzuzeigen.

*   **`Product`**: Das A und O für jeden Onlineshop. Mit Eigenschaften wie `name`, `image`, `description`, `sku` und vor allem `offers` kannst du Produktdaten präzise übermitteln. Die `offers`-Eigenschaft enthält den Preis (`price`), die Währung (`priceCurrency`) und die Verfügbarkeit (`availability`). Dies ist die Grundlage für Produktanzeigen in der Suche, inklusive Preis und Lagerstatus.

*   **`LocalBusiness`**: Für jedes Unternehmen mit einem physischen Standort. Hier kannst du Adresse (`address`), Telefonnummer (`telephone`), Öffnungszeiten (`openingHours`) und die Art des Geschäfts (z.B. `Restaurant` oder `HairSalon`) angeben. Diese Daten fließen direkt in Dienste wie Google Maps und die lokale Suche ein.

*   **`Event`**: Für Konzerte, Webinare, Konferenzen oder Feste. Mit `name`, `startDate`, `endDate`, `location` und `performer` lieferst du alle relevanten Informationen, die Suchmaschinen benötigen, um dein Event prominent in den Suchergebnissen für Veranstaltungen aufzulisten.

#### Der Weg zur richtigen Auszeichnung

Du musst dieses riesige Vokabular nicht auswendig lernen. Deine wichtigste Ressource ist die offizielle Webseite **schema.org**. Dort kannst du die gesamte Hierarchie der Typen durchsuchen. Jede Seite für einen Typ (z.B. [schema.org/Movie](https://schema.org/Movie)) listet alle spezifischen Eigenschaften für diesen Typ sowie die Eigenschaften, die er von seinen übergeordneten Typen (wie `CreativeWork` und `Thing`) erbt.

Die Nutzung von Schema.org ist ein entscheidender Schritt, um deine Webseite von einer reinen Ansammlung von HTML-Tags und Text in eine semantisch reiche und maschinenlesbare Datenquelle zu verwandeln. Du gibst den Such-Crawlern nicht nur Futter, sondern ein wohl zubereitetes Festmahl. Du hilfst ihnen, den Kontext und die Bedeutung deines Inhalts tiefgreifend zu verstehen, was sich nicht nur in besseren Rankings, sondern vor allem in einer besseren und nützlicheren Darstellung deiner Seite in den Suchergebnissen niederschlagen kann.
