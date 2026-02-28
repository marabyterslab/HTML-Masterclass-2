# Syntax und Aufbau

### JSON-LD: Syntax und Aufbau

Wenn du dich mit strukturierten Daten beschäftigst, stößt du unweigerlich auf JSON-LD. Der Name steht für "JavaScript Object Notation for Linked Data" und beschreibt bereits perfekt, worum es geht: Wir nutzen das bekannte und weitverbreitete JSON-Format, um Daten so zu strukturieren, dass Maschinen sie nicht nur lesen, sondern auch verstehen können. Anders als bei Microdata oder RDFa, die direkt in die sichtbaren HTML-Tags eingewoben werden, hat JSON-LD einen entscheidenden Vorteil: Es lebt in seinem eigenen, abgeschlossenen Bereich und hält dein HTML sauber und übersichtlich.

#### Das Grundgerüst: Der `<script>`-Tag

Der Ort, an dem du deine JSON-LD-Daten in ein HTML-Dokument einfügst, ist ein spezieller `<script>`-Tag. Dieser Tag wird üblicherweise im `<head>`-Bereich deines Dokuments platziert, kann aber auch im `<body>` stehen, oft kurz vor dem schließenden `</body>`-Tag.

Das Entscheidende ist das `type`-Attribut. Es lautet nicht `text/javascript`, wie du es von ausführbarem JavaScript kennst, sondern `application/ld+json`. Damit signalisierst du dem Browser und vor allem den Suchmaschinen-Crawlern: "Achtung, der Inhalt hier ist kein Programmcode, sondern ein Block strukturierter, verknüpfter Daten."

Ein leeres Grundgerüst sieht also so aus:

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Beispielseite mit JSON-LD</title>
  
  <script type="application/ld+json">
  {
    // Hier fügen wir unsere strukturierten Daten ein.
  }
  </script>
  
</head>
<body>
  <h1>Unsere Firma</h1>
  <p>Willkommen auf unserer Webseite.</p>
</body>
</html>
```

Innerhalb dieses Skript-Tags befindet sich ein einzelnes JSON-Objekt, das durch geschweifte Klammern `{}` definiert wird.

#### Die Kernkomponenten: `@context` und `@type`

Jedes JSON-LD-Objekt stützt sich auf zwei fundamentale Schlüssel, die mit einem `@`-Zeichen beginnen. Diese Schlüssel sind das Herzstück der Syntax und geben den Daten ihre Bedeutung.

**1. `@context` (Der Kontext): Das Vokabular**

Stell dir `@context` als das Wörterbuch vor, das du verwendest. Es teilt den Maschinen mit, welche Bedeutung die von dir verwendeten Begriffe (wie "name", "address" oder "openingHours") haben. Ohne diesen Kontext wären diese Begriffe nur bedeutungslose Zeichenketten.

In den allermeisten Fällen wirst du für Webseiten das Vokabular von Schema.org verwenden. Es ist der De-facto-Standard, den große Suchmaschinen wie Google, Bing und Yandex gemeinsam entwickelt haben und verstehen. Der Wert für `@context` ist daher meistens:

```json
{
  "@context": "https://schema.org"
}
```

Mit dieser einen Zeile legst du fest, dass alle weiteren Eigenschaften in deinem JSON-LD-Objekt auf den Definitionen von Schema.org basieren. Du sagst quasi: "Wenn ich 'name' schreibe, meine ich das, was Schema.org unter einem Namen versteht."

**2. `@type` (Der Typ): Die Art der Entität**

Nachdem du das Vokabular festgelegt hast, musst du definieren, *was* du eigentlich beschreibst. Handelt es sich um eine Person, ein Produkt, ein Rezept, eine Organisation oder ein Event? Genau das legt der Schlüssel `@type` fest. Der Wert, den du hier angibst, muss ein gültiger Typ aus dem Vokabular sein, das du im `@context` definiert hast.

Wenn du also eine Organisation beschreiben möchtest, sieht dein grundlegendes JSON-LD-Objekt so aus:

```json
{
  "@context": "https://schema.org",
  "@type": "Organization"
}
```

Damit ist die Basis geschaffen. Jede Maschine, die dieses Objekt liest, weiß nun: "Aha, hier folgt die Beschreibung einer Organisation nach den Regeln von Schema.org."

#### Daten hinzufügen: Eigenschaften und Werte

Nun geht es ans Eingemachte: das Füllen deines Objekts mit konkreten Informationen. Dies geschieht über einfache Schlüssel-Wert-Paare, genau wie im Standard-JSON. Der Schlüssel ist dabei immer eine Eigenschaft (ein "Property") aus dem Schema.org-Vokabular, das zum gewählten `@type` passt. Der Wert ist die eigentliche Information.

Erweitern wir unser Beispiel für eine Organisation um grundlegende Daten:

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Die Web-Werkstatt",
  "url": "https://www.web-werkstatt.example.com",
  "logo": "https://www.web-werkstatt.example.com/logo.png",
  "telephone": "+49 30 12345678"
}
```

Die Syntax ist einfach:
*   Der Schlüssel (z. B. `"name"`) steht in doppelten Anführungszeichen.
*   Darauf folgt ein Doppelpunkt `:`.
*   Danach kommt der Wert. Handelt es sich um eine Zeichenkette (Text), muss auch dieser in doppelten Anführungszeichen stehen. Bei Zahlen oder booleschen Werten (`true`/`false`) entfallen die Anführungszeichen.

#### Komplexe Datenstrukturen: Verschachtelte Objekte

Selten sind alle Informationen einfache Textbausteine. Eine Adresse zum Beispiel besteht selbst wieder aus mehreren Teilen: Straße, Postleitzahl, Stadt und Land. Für solche Fälle erlaubt JSON-LD die Verschachtelung von Objekten. Der Wert einer Eigenschaft ist dann nicht mehr nur ein einfacher Text, sondern ein komplettes weiteres JSON-Objekt.

Dieses untergeordnete Objekt braucht ebenfalls einen `@type`, um klar zu definieren, was es ist. Im Fall einer Adresse ist das der Typ `PostalAddress`.

Schauen wir uns an, wie wir eine Adresse zu unserer Organisation hinzufügen:

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Die Web-Werkstatt",
  "url": "https://www.web-werkstatt.example.com",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Musterstraße 1",
    "addressLocality": "Berlin",
    "postalCode": "10115",
    "addressCountry": "DE"
  }
}
```

Die Eigenschaft `address` hat nun als Wert ein ganzes Objekt, das die Adresse detailliert beschreibt. Diese Verschachtelung sorgt für eine klare und logische Struktur deiner Daten. Du kannst Objekte beliebig tief ineinander verschachteln, um auch sehr komplexe Beziehungen abzubilden.

#### Mehrere Werte: Die Verwendung von Arrays

Was tust du, wenn eine Eigenschaft mehrere Werte haben kann? Eine Firma hat vielleicht mehrere Telefonnummern, oder du möchtest für ein Produkt mehrere Bilder angeben. Hierfür verwendet JSON das Array-Format, das durch eckige Klammern `[]` gekennzeichnet wird. Innerhalb der Klammern listest du die einzelnen Werte auf, getrennt durch Kommas.

Nehmen wir an, unsere Web-Werkstatt ist unter zwei Telefonnummern erreichbar und hat auch einen Social-Media-Link, den wir angeben wollen. Die Eigenschaft `sameAs` wird oft genutzt, um auf Profile in sozialen Netzwerken oder Einträge in anderen Datenbanken (wie Wikidata) zu verweisen.

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Die Web-Werkstatt",
  "url": "https://www.web-werkstatt.example.com",
  "telephone": [
    "+49 30 12345678",
    "+49 30 87654321"
  ],
  "sameAs": [
    "https://www.facebook.com/webwerkstatt",
    "https://www.linkedin.com/company/webwerkstatt"
  ],
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Musterstraße 1",
    "addressLocality": "Berlin",
    "postalCode": "10115",
    "addressCountry": "DE"
  }
}
```

Jedes Element im Array folgt den gleichen Regeln wie einzelne Werte. Wenn es sich um Zeichenketten handelt, stehen sie in Anführungszeichen. Du könntest hier auch komplexe Objekte in einem Array auflisten, zum Beispiel wenn du mehrere Standorte (also mehrere `PostalAddress`-Objekte) angeben möchtest.

#### Eindeutige Identifikatoren: `@id`

Ein Kernkonzept von "Linked Data" ist die Idee, dass jede Entität (jede "Sache", die du beschreibst) eine eindeutige, globale Kennung haben sollte – typischerweise eine URL. Dafür gibt es den Schlüssel `@id`.

Mit `@id` gibst du einer Entität einen eindeutigen Namen im Web. Für eine Firma ist das oft einfach die URL ihrer "Über uns"-Seite oder ihrer Homepage.

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "@id": "https://www.web-werkstatt.example.com/#organization",
  "name": "Die Web-Werkstatt"
}
```

Der Teil `#organization` am Ende der URL ist eine gängige Konvention, um auf ein bestimmtes Fragment auf der Seite zu verweisen, das diese Entität repräsentiert. Dies ist besonders nützlich, wenn du auf einer Seite mehrere Entitäten beschreibst und sie miteinander verknüpfen möchtest. So kannst du eine Entität an einer Stelle vollständig definieren und an anderer Stelle nur noch über ihre `@id` darauf verweisen.

Der saubere, von deinem visuellen HTML getrennte Aufbau macht JSON-LD zu einer mächtigen und flexiblen Methode, um deine Inhalte für Maschinen verständlich zu machen. Die Syntax folgt den klaren Regeln von JSON, ergänzt um wenige, aber wirkungsvolle Schlüssel wie `@context`, `@type` und `@id`, die deinen Daten eine semantische Tiefe verleihen.
