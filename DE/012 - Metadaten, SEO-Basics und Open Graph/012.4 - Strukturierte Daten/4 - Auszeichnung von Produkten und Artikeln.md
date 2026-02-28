# Auszeichnung von Produkten und Artikeln

### Auszeichnung von Produkten und Artikeln

Stell dir das Internet als eine riesige, unendlich große Bibliothek vor. Deine Website ist ein Buch in dieser Bibliothek. Damit die Bibliothekarinnen – in unserem Fall die Suchmaschinen wie Google oder Bing – dein Buch nicht nur finden, sondern auch seinen Inhalt auf den ersten Blick verstehen, brauchst du mehr als nur gut geschriebenen Text. Du brauchst eine Art Inhaltsverzeichnis für Maschinen. Genau hier kommen strukturierte Daten ins Spiel.

Im Kern geht es darum, den reinen Text deiner Webseite mit einem unsichtbaren Vokabular zu versehen, das Maschinen eindeutig verstehen. Du sagst einer Suchmaschine nicht nur: „Hier steht ‚99,95 €‘“, sondern: „Das hier ist der Preis für dieses spezifische Produkt, und die Währung ist Euro.“ Dieser feine, aber entscheidende Unterschied ermöglicht es Suchmaschinen, sogenannte „Rich Snippets“ (reichhaltige Suchergebnisse) zu erzeugen. Das sind die Suchergebnisse, die mit Sternchenbewertungen, Preisen, Verfügbarkeiten oder dem Bild des Autors hervorstechen und die Klickrate massiv erhöhen können.

Die gemeinsame Sprache, auf die sich die großen Suchmaschinen geeinigt haben, heißt **Schema.org**. Es ist eine gewaltige Sammlung von Schemata (also vordefinierten Strukturen) für so ziemlich alles, was man im Web beschreiben kann: Personen, Organisationen, Rezepte, Veranstaltungen und eben auch Produkte und Artikel.

Wir werden uns hier auf die Implementierung mit **JSON-LD (JavaScript Object Notation for Linked Data)** konzentrieren. Warum? Weil es die von Google empfohlene Methode ist. Anstatt die Auszeichnungen mühsam direkt in deine HTML-Tags zu flechten (wie bei Microdata), schreibst du ein sauberes, separates Skript, das du in den `<head>` oder `<body>` deiner Seite einfügst. Das hält deinen HTML-Code sauber und die Daten an einem gut lesbaren Ort.

#### Die Welt der Produkte – `schema.org/Product`

Wenn du einen Onlineshop betreibst oder Produkte auf deiner Seite vorstellst, ist die Auszeichnung mit dem `Product`-Schema fast schon Pflicht. Es ist der direkteste Weg, Google alle relevanten Informationen zu liefern, damit dein Produkt in den Suchergebnissen optimal präsentiert wird.

Stell dir vor, du verkaufst eine innovative Smart-Wasserflasche. Dein HTML könnte einfach eine Überschrift, einen Absatz und einen Preis enthalten. Für eine Suchmaschine sind das nur Text und Zahlen. Mit strukturierten Daten gibst du diesen Elementen eine Bedeutung.

Die wichtigsten Eigenschaften für ein `Product`-Schema sind:

*   `@context`: Gibt an, welches Vokabular wir verwenden (fast immer `https://schema.org`).
*   `@type`: Definiert den Typ des Objekts, hier also `Product`.
*   `name`: Der Name des Produkts.
*   `image`: Die URL zu einem repräsentativen Produktbild.
*   `description`: Eine kurze, prägnante Beschreibung des Produkts.
*   `sku`: Die „Stock Keeping Unit“, also deine interne Artikelnummer. Sie ist für die eindeutige Identifikation wichtig.
*   `mpn`: Die „Manufacturer Part Number“, also die Herstellernummer.
*   `brand`: Die Marke des Produkts, oft als eigenes `Brand`-Objekt verschachtelt.
*   `offers`: Hier wird es interessant. Diese Eigenschaft enthält ein weiteres Objekt vom Typ `Offer`, das alle kommerziellen Informationen bündelt.
*   `aggregateRating`: Wenn dein Produkt Bewertungen hat, kannst du sie hier zusammenfassen.

Schauen wir uns das `Offer`-Objekt genauer an. Es enthält die eigentlichen Verkaufsdetails:

*   `@type`: `Offer`
*   `priceCurrency`: Der ISO-Code der Währung (z. B. `EUR` oder `USD`).
*   `price`: Der Preis des Produkts (ohne Währungssymbol).
*   `availability`: Der Lagerstatus, z. B. `https://schema.org/InStock` (Auf Lager) oder `https://schema.org/OutOfStock` (Nicht vorrätig).
*   `itemCondition`: Der Zustand des Produkts, z. B. `https://schema.org/NewCondition`.
*   `url`: Die direkte URL zur Produktseite.

Ein vollständiges JSON-LD-Skript für unsere Smart-Wasserflasche könnte so aussehen. Du platzierst diesen Code-Block idealerweise im `<head>` deiner HTML-Seite.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org/",
  "@type": "Product",
  "name": "HydroSmart Pro Wasserflasche",
  "image": [
    "https://deine-seite.de/images/hydrosmart-pro-1.jpg",
    "https://deine-seite.de/images/hydrosmart-pro-2.jpg"
   ],
  "description": "Die HydroSmart Pro ist eine intelligente Wasserflasche, die deine Flüssigkeitszufuhr trackt und dich daran erinnert, regelmäßig zu trinken. Aus BPA-freiem Edelstahl.",
  "sku": "HSP-BLU-500",
  "mpn": "98765-43210",
  "brand": {
    "@type": "Brand",
    "name": "AquaTech"
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.8",
    "reviewCount": "215"
  },
  "offers": {
    "@type": "Offer",
    "url": "https://deine-seite.de/produkte/hydrosmart-pro",
    "priceCurrency": "EUR",
    "price": "49.99",
    "priceValidUntil": "2024-12-31",
    "itemCondition": "https://schema.org/NewCondition",
    "availability": "https://schema.org/InStock"
  }
}
</script>
```

Mit diesem einzigen Code-Block hast du der Suchmaschine alles mitgeteilt, was sie wissen muss: den Namen, die Bilder, die Beschreibung, die Marke, die hervorragende Durchschnittsbewertung und natürlich den Preis und die Verfügbarkeit. Die Chance, dass dein Produkt nun mit Sternchen und Preis in den Suchergebnissen erscheint, ist drastisch gestiegen.

#### Inhalte zum Leben erwecken – `schema.org/Article`

Nicht jeder betreibt einen Onlineshop. Wenn du einen Blog, ein Nachrichtenmagazin oder eine Wissensdatenbank pflegst, ist das `Article`-Schema dein wichtigstes Werkzeug. Es hilft Suchmaschinen, den Kontext deiner Inhalte zu verstehen: Wer hat es geschrieben? Wann wurde es veröffentlicht? Worum geht es?

Besonders für Nachrichten ist dies relevant, da Google solche Artikel prominent in den „Top Stories“ oder im „News“-Tab platzieren kann. Aber auch für jeden normalen Blogbeitrag ist es wertvoll, da es Autorität und Vertrauen signalisiert.

Schema.org unterscheidet verschiedene Arten von Artikeln, wie `Article`, `NewsArticle` oder `BlogPosting`. Für die meisten Zwecke ist `Article` ein guter und sicherer Startpunkt.

Die wichtigsten Eigenschaften für ein `Article`-Schema sind:

*   `@type`: `Article` (oder eine spezifischere Variante).
*   `headline`: Die Überschrift des Artikels (sollte mit deinem `<h1>` übereinstimmen).
*   `image`: Die URL eines repräsentativen Beitragsbildes.
*   `datePublished`: Das Datum, an dem der Artikel veröffentlicht wurde (im ISO 8601 Format, z. B. `2023-10-26`).
*   `dateModified`: Das Datum der letzten wesentlichen Änderung. Das ist wichtig, um Aktualität zu signalisieren.
*   `author`: Der Autor des Artikels, idealerweise als `Person`-Objekt verschachtelt.
*   `publisher`: Der Herausgeber des Inhalts, meist eine Firma oder Organisation, als `Organization`-Objekt verschachtelt.

Gerade `author` und `publisher` sind entscheidend für das, was Google unter E-E-A-T (Experience, Expertise, Authoritativeness, Trustworthiness) versteht. Indem du klar definierst, wer für den Inhalt verantwortlich ist, baust du Vertrauen auf. Der `publisher` sollte dabei unbedingt ein Logo (`logo`) beinhalten.

Hier ist ein Beispiel für einen Blogbeitrag über moderne CSS-Techniken:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Moderne CSS-Layouts: Ein tiefer Einblick in Grid und Flexbox",
  "description": "Lerne, wie du mit CSS Grid und Flexbox komplexe, responsive Web-Layouts erstellst, ohne auf veraltete Techniken zurückgreifen zu müssen.",
  "image": "https://dein-blog.de/images/css-layouts-header.jpg",
  "datePublished": "2023-09-15T08:00:00+02:00",
  "dateModified": "2023-10-20T12:30:00+02:00",
  "author": {
    "@type": "Person",
    "name": "Anna Schmidt",
    "url": "https://dein-blog.de/autoren/anna-schmidt"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Web-Entwickler Magazin",
    "logo": {
      "@type": "ImageObject",
      "url": "https://dein-blog.de/images/logo.png"
    }
  }
}
</script>
```

Durch diese Auszeichnung weiß eine Suchmaschine sofort:
1.  Dies ist ein Artikel.
2.  Die Überschrift lautet „Moderne CSS-Layouts...“.
3.  Er wurde von Anna Schmidt geschrieben.
4.  Veröffentlicht wurde er vom „Web-Entwickler Magazin“.
5.  Er ist aktuell, da er kürzlich überarbeitet wurde.

Diese Informationen können dazu führen, dass dein Artikel in den Suchergebnissen mit einem Vorschaubild und dem Veröffentlichungsdatum erscheint, was ihn deutlich attraktiver macht als einen reinen Textlink.

#### Validierung ist der Schlüssel

Nachdem du strukturierte Daten zu deiner Seite hinzugefügt hast, solltest du sie unbedingt testen. Der bloße Einbau garantiert noch keine korrekte Funktion. Kleine Tippfehler bei Eigenschaftsnamen oder ein falsches Format können die gesamte Struktur unbrauchbar machen.

Das wichtigste Werkzeug hierfür ist der **Rich-Suchergebnis-Test** von Google (Google Rich Results Test). Du gibst dort entweder die URL deiner Seite oder direkt den Code-Schnipsel ein. Das Tool analysiert den Code und sagt dir sofort, ob die strukturierten Daten gültig sind und für welche Rich Snippets deine Seite qualifiziert ist. Es zeigt dir Warnungen und Fehler an, sodass du sie gezielt beheben kannst. Dieser Schritt ist unverzichtbar und sollte nach jeder Implementierung oder Änderung durchgeführt werden.

Durch die gezielte Auszeichnung deiner Produkte und Artikel gibst du den Suchmaschinen also genau das Futter, das sie brauchen, um deine Inhalte optimal zu verstehen und zu präsentieren. Du hebst dich von der Konkurrenz ab, verbesserst deine Sichtbarkeit und schaffst eine bessere Nutzererfahrung, noch bevor jemand deine Seite überhaupt betreten hat.
