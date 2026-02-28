# Einbindung im Script-Tag

### JSON-LD: Die Einbindung im `<script>`-Tag

Eine der elegantesten und heute am weitesten verbreiteten Methoden, um JSON-LD in eine Webseite zu integrieren, ist die Verwendung des `<script>`-Tags. Auf den ersten Blick mag das etwas seltsam erscheinen. Ein `<script>`-Tag ist doch eigentlich für ausführbaren Code wie JavaScript gedacht, oder? Das ist zwar richtig, aber das HTML-Standard erlaubt es uns, den Typ des Inhalts in einem Script-Tag genau zu spezifizieren. Und genau das machen wir uns für JSON-LD zunutze.

Der entscheidende Trick liegt im `type`-Attribut. Indem du es auf `application/ld+json` setzt, signalisierst du dem Browser und anderen Systemen (wie den Crawlern von Suchmaschinen), dass der Inhalt dieses Tags kein JavaScript ist, sondern JSON-LD-Daten. Du gibst dem Browser quasi einen Zettel mit Metadaten in die Hand und sagst ihm: „Das hier ist nur zum Lesen und Interpretieren, nicht zum Ausführen.“

Diese Methode hat einen riesigen Vorteil gegenüber anderen Formaten wie Microdata oder RDFa: Sie entkoppelt deine strukturierten Daten vollständig von deinem sichtbaren HTML-Markup. Du musst keine speziellen Attribute in deine `<div>`s, `<span>`s oder `<h1>`s einfügen. Stattdessen platzierst du einen sauberen, eigenständigen Block an Daten, meist im `<head>`-Bereich deines Dokuments. Das macht die Pflege und das Management der Daten – insbesondere bei komplexen Seiten oder bei der dynamischen Generierung durch ein Content-Management-System (CMS) – erheblich einfacher.

#### Das Grundgerüst

Schauen wir uns ein einfaches, aber vollständiges Beispiel an. Stell dir vor, du möchtest die grundlegenden Informationen über eine Organisation, zum Beispiel ein Unternehmen oder einen Verein, auf deiner Webseite hinterlegen.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Unsere tolle Firma</title>
    
    <script type="application/ld+json">
    {
      "@context": "https://schema.org",
      "@type": "Organization",
      "name": "Die kreative Web-Manufaktur",
      "url": "https://www.beispiel-firma.de",
      "logo": "https://www.beispiel-firma.de/logo.png",
      "contactPoint": {
        "@type": "ContactPoint",
        "telephone": "+49-123-4567890",
        "contactType": "customer service"
      }
    }
    </script>

</head>
<body>
    <h1>Willkommen bei der kreativen Web-Manufaktur!</h1>
    <p>Wir bauen die besten Webseiten.</p>
</body>
</html>
```

Lass uns diesen JSON-LD-Block Zeile für Zeile aufschlüsseln:

*   **`@context": "https://schema.org"`**: Dies ist die vielleicht wichtigste Zeile. Sie legt das „Vokabular“ fest, das wir verwenden. Indem wir auf `schema.org` verweisen, sagen wir: „Alle Begriffe, die ich hier verwende, wie `Organization`, `name` oder `url`, sind gemäß der Definition auf schema.org zu verstehen.“ Ohne diesen Kontext wären die Begriffe nur bedeutungslose Zeichenketten.
*   **`@type": "Organization"`**: Hier definieren wir den Typ der Entität, die wir beschreiben. In diesem Fall ist es eine Organisation. Suchmaschinen wissen dadurch sofort, dass es sich nicht um eine Person, ein Produkt oder ein Rezept handelt.
*   **`name`, `url`, `logo`**: Das sind Eigenschaften des Typs `Organization`. Sie sind ziemlich selbsterklärend und geben den Namen, die offizielle URL und die URL zum Logo der Organisation an.
*   **`contactPoint`**: Hier wird es interessant. Eine Eigenschaft kann selbst wieder ein Objekt mit eigenem `@type` und eigenen Eigenschaften sein. Wir beschreiben hier einen Kontaktpunkt (`ContactPoint`), der wiederum eine Telefonnummer (`telephone`) und einen Kontakttyp (`contactType`) hat. So lassen sich Daten logisch verschachteln und strukturieren.

Der gesamte Block steht für sich allein und beeinflusst das sichtbare Layout deiner Seite in keiner Weise. Er ist reine Information für Maschinen.

#### Ein komplexeres Beispiel: Ein Rezept

JSON-LD kann weit mehr als nur einfache Kontaktdaten beschreiben. Seine Stärke liegt in der detaillierten Beschreibung komplexer Entitäten. Ein klassisches Beispiel dafür sind Rezepte, die von Suchmaschinen besonders gut verstanden und in den Suchergebnissen prominent dargestellt werden können (z.B. mit Bild, Bewertung und Kochzeit).

Nehmen wir an, du hast einen Food-Blog und veröffentlichst ein Rezept für eine Tomatensuppe.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Rezept: Klassische Tomatensuppe</title>
    
    <script type="application/ld+json">
    {
      "@context": "https://schema.org/",
      "@type": "Recipe",
      "name": "Klassische Tomatensuppe",
      "image": [
        "https://beispiel-foodblog.de/images/tomatensuppe-1x1.jpg",
        "https://beispiel-foodblog.de/images/tomatensuppe-4x3.jpg",
        "https://beispiel-foodblog.de/images/tomatensuppe-16x9.jpg"
       ],
      "author": {
        "@type": "Person",
        "name": "Anna Kocht"
      },
      "datePublished": "2023-10-27",
      "description": "Eine einfache und köstliche Tomatensuppe, perfekt für kalte Tage. Zubereitet aus frischen Tomaten und Kräutern.",
      "prepTime": "PT15M",
      "cookTime": "PT30M",
      "totalTime": "PT45M",
      "recipeYield": "4 Portionen",
      "recipeIngredient": [
        "1 kg reife Tomaten",
        "2 Zwiebeln",
        "2 Knoblauchzehen",
        "1 Liter Gemüsebrühe",
        "Olivenöl",
        "Salz und Pfeffer",
        "Frisches Basilikum"
      ],
      "recipeInstructions": [
        {
          "@type": "HowToStep",
          "text": "Die Zwiebeln und den Knoblauch fein hacken und in Olivenöl glasig dünsten."
        },
        {
          "@type": "HowToStep",
          "text": "Die Tomaten würfeln, hinzufügen und einige Minuten mitkochen lassen."
        },
        {
          "@type": "HowToStep",
          "text": "Mit Gemüsebrühe aufgießen und für ca. 20 Minuten köcheln lassen."
        },
        {
          "@type": "HowToStep",
          "text": "Die Suppe pürieren und mit Salz und Pfeffer abschmecken. Vor dem Servieren mit frischem Basilikum garnieren."
        }
      ],
      "aggregateRating": {
        "@type": "AggregateRating",
        "ratingValue": "4.8",
        "ratingCount": "125"
      },
      "nutrition": {
        "@type": "NutritionInformation",
        "calories": "150 kcal"
      }
    }
    </script>

</head>
<body>
    <!-- Hier steht der sichtbare Inhalt des Rezepts für die Benutzer -->
    <h1>Klassische Tomatensuppe</h1>
    <p>von Anna Kocht</p>
    <!-- ... Restlicher Inhalt wie Zutatenliste, Anweisungen, Bilder etc. -->
</body>
</html>
```

Dieses Beispiel zeigt mehrere wichtige Konzepte:

*   **Arrays**: Eigenschaften wie `image`, `recipeIngredient` und `recipeInstructions` verwenden eckige Klammern `[]`, um eine Liste von Werten aufzunehmen. Du kannst also mehrere Bilder oder eine ganze Liste von Zutaten angeben.
*   **Spezifische Formate**: Zeitangaben wie `prepTime` (Vorbereitungszeit) verwenden das ISO 8601-Format für Zeitdauern. `PT15M` steht für eine Dauer von 15 Minuten (`P` für Period, `T` für Time, `M` für Minutes).
*   **Verschachtelte, typisierte Listen**: Die `recipeInstructions` sind nicht nur eine Liste von Texten, sondern eine Liste von `HowToStep`-Objekten. Jeder Schritt ist also eine eigene kleine Entität, was eine noch präzisere maschinelle Verarbeitung ermöglicht.
*   **Zusammengefasste Daten**: `aggregateRating` fasst Nutzerbewertungen zusammen und gibt den Durchschnittswert (`ratingValue`) sowie die Anzahl der Bewertungen (`ratingCount`) an.

#### Wichtige Hinweise für die Praxis

1.  **Platzierung: `<head>` oder `<body>`?**
    Die gängigste und empfohlene Praxis ist die Platzierung des JSON-LD-Skripts im `<head>`-Bereich deiner HTML-Datei. Das ist logisch, da es sich um Metadaten handelt, die die gesamte Seite beschreiben. Technisch ist es aber auch gültig, das Skript in den `<body>` zu legen. Das kann sinnvoll sein, wenn die Daten sehr spezifisch für einen bestimmten Abschnitt im Body sind und dort dynamisch geladen werden. Für die allgemeine Seitenbeschreibung ist der `<head>` jedoch der richtige Ort.

2.  **Validierung ist entscheidend**
    JSON ist ein sehr strenges Datenformat. Ein einziges fehlendes Komma oder eine vergessene Anführungszeichen können den gesamten Block ungültig machen. Maschinen, die diese Daten lesen, sind nicht fehlertolerant. Wenn die Syntax nicht stimmt, wird der gesamte Block ignoriert. Nutze daher unbedingt einen Validator, um deinen Code zu überprüfen, bevor du ihn veröffentlichst. Der *Schema Markup Validator* (betrieben von schema.org) ist hierfür das offizielle Werkzeug.

3.  **Konsistenz mit dem sichtbaren Inhalt**
    Die Informationen, die du in deinem JSON-LD bereitstellst, sollten mit dem Inhalt übereinstimmen, den deine Nutzer auf der Seite sehen. Es ist ein Verstoß gegen die Richtlinien von Suchmaschinen, im JSON-LD andere Informationen (z. B. eine bessere Bewertung, einen niedrigeren Preis) anzugeben als im sichtbaren Text. Die strukturierten Daten sollen den sichtbaren Inhalt widerspiegeln und für Maschinen verständlich machen, nicht ihn ersetzen oder ihm widersprechen.

Die Einbindung via `<script>`-Tag ist die modernste und flexibelste Art, strukturierte Daten mit JSON-LD in deine Webseite zu bringen. Sie hält deinen HTML-Code sauber und erlaubt dir, selbst komplexe Informationsstrukturen präzise und wartbar abzubilden.
