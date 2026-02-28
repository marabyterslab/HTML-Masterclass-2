# Itemscope, itemtype, itemprop

### Itemscope, Itemtype, Itemprop: Das Trio für strukturierte Daten

Stell dir vor, eine Suchmaschine wie Google besucht deine Webseite. Sie ist ein extrem schneller, aber im Grunde blinder Leser. Sie kann den Text auf deiner Seite zwar erfassen – die Wörter, die Überschriften, die Absätze –, aber sie versteht nicht unbedingt die *Bedeutung* oder den *Zusammenhang* dahinter. Sie sieht vielleicht den Text "Avatar", "James Cameron" und "2009", kann aber nicht mit Sicherheit sagen, dass es sich hier um einen Film mit einem bestimmten Regisseur und einem Erscheinungsjahr handelt.

Genau hier kommt Microdata ins Spiel. Es ist eine Methode, um direkt in deinem HTML-Code zusätzliche Informationen einzubetten, die diese Zusammenhänge für Maschinen glasklar machen. Du gibst dem blinden Leser quasi eine Brille auf, mit der er die Struktur und Bedeutung deiner Inhalte erkennen kann. Das Herzstück von Microdata sind drei simple, aber mächtige HTML-Attribute: `itemscope`, `itemtype` und `itemprop`. Lass uns dieses Trio einmal genauer unter die Lupe nehmen.

#### Das Grundprinzip: Ein Item definieren

Bevor wir über die Details sprechen können, müssen wir verstehen, was ein "Item" ist. Ein Item ist einfach ausgedrückt eine Sache, eine Entität. Das kann eine Person sein, ein Produkt, ein Unternehmen, ein Rezept, ein Event – im Grunde alles, was du auf einer Webseite beschreiben könntest.

Microdata funktioniert, indem du im HTML-Code Blöcke definierst, die genau solch ein Item beschreiben. Und dafür nutzen wir unser erstes Attribut.

**`itemscope`**: Dieses Attribut ist ein reines Signalwort (ein boolean attribute) und hat keinen Wert. Wenn du es einem HTML-Tag hinzufügst, sagst du damit: "Achtung, alles innerhalb dieses Tags gehört zusammen und beschreibt genau ein Item." Es schafft also einen Geltungsbereich, einen Rahmen für die Beschreibung deiner Sache.

Schauen wir uns ein einfaches Beispiel an, noch ohne Microdata:

```html
<div>
  <h1>Max Mustermann</h1>
  <p>Softwareentwickler bei der WebDev GmbH.</p>
  <p>Absolvent der Technischen Universität Beispielstadt.</p>
</div>
```

Für einen Menschen ist das klar. Für eine Maschine ist es nur eine Überschrift und zwei Absätze. Fügen wir `itemscope` hinzu:

```html
<div itemscope>
  <h1>Max Mustermann</h1>
  <p>Softwareentwickler bei der WebDev GmbH.</p>
  <p>Absolvent der Technischen Universität Beispielstadt.</p>
</div>
```

Damit haben wir dem Browser und den Suchmaschinen mitgeteilt: Der Inhalt dieses `<div>` beschreibt eine Einheit. Aber welche Art von Einheit? Das weiß die Maschine immer noch nicht.

#### Der Bauplan: Den Typ des Items festlegen

Hier kommt das zweite Attribut ins Spiel: `itemtype`. Es beantwortet die Frage: "Um was für eine Art von Item handelt es sich hier?"

**`itemtype`**: Dieses Attribut benötigt einen Wert, und zwar eine URL, die auf eine Definition dieses Item-Typs verweist. Du denkst dir diese Definitionen aber nicht selbst aus. Stattdessen greifen wir auf ein gemeinsames, standardisiertes Vokabular zurück. Das mit Abstand wichtigste und am weitesten verbreitete Vokabular ist **Schema.org**, eine gemeinsame Initiative von Google, Microsoft, Yahoo! und Yandex.

Auf schema.org findest du Hunderte von vordefinierten Typen für fast alles, was du dir vorstellen kannst: `Person`, `Product`, `Recipe`, `Movie`, `LocalBusiness` und viele mehr. Jeder dieser Typen hat eine eigene Seite (und damit eine URL) und eine Liste von Eigenschaften, die du verwenden kannst.

Ergänzen wir unser Beispiel mit `itemtype`, um zu definieren, dass es sich um eine Person handelt:

```html
<div itemscope itemtype="https://schema.org/Person">
  <h1>Max Mustermann</h1>
  <p>Softwareentwickler bei der WebDev GmbH.</p>
  <p>Absolvent der Technischen Universität Beispielstadt.</p>
</div>
```

Jetzt weiß die Maschine: "Aha! In diesem `<div>` wird eine Person beschrieben, die dem Schema von schema.org/Person folgt." Der erste große Schritt zur Verständlichkeit ist getan. Aber welche Information gehört zu welcher Eigenschaft der Person?

#### Die Etiketten: Eigenschaften zuweisen

Wir haben den Rahmen (`itemscope`) und den Bauplan (`itemtype`). Jetzt brauchen wir die Etiketten für die einzelnen Bauteile. Dafür ist das dritte Attribut zuständig: `itemprop` (kurz für "item property").

**`itemprop`**: Mit diesem Attribut markierst du einzelne HTML-Tags innerhalb eines `itemscope` und weist ihnen eine bestimmte Eigenschaft aus dem Vokabular von `itemtype` zu. Der Wert von `itemprop` ist der Name der Eigenschaft, wie er auf schema.org definiert ist.

Für unseren `Person`-Typ gibt es zum Beispiel Eigenschaften wie `name` (Name), `jobTitle` (Berufsbezeichnung) oder `alumniOf` (Absolvent von). Wenden wir das auf unser Beispiel an:

```html
<div itemscope itemtype="https://schema.org/Person">
  <h1 itemprop="name">Max Mustermann</h1>
  <p><span itemprop="jobTitle">Softwareentwickler</span> bei der WebDev GmbH.</p>
  <p>Absolvent der <span itemprop="alumniOf">Technischen Universität Beispielstadt</span>.</p>
</div>
```

Jetzt ist das Bild für die Maschine komplett:
1.  `itemscope`: Hier beginnt die Beschreibung einer Sache.
2.  `itemtype="https://schema.org/Person"`: Diese Sache ist eine Person.
3.  `itemprop="name"`: Der Text "Max Mustermann" ist der Name dieser Person.
4.  `itemprop="jobTitle"`: Der Text "Softwareentwickler" ist die Berufsbezeichnung.
5.  `itemprop="alumniOf"`: Der Text "Technischen Universität Beispielstadt" ist die Bildungseinrichtung, deren Absolvent diese Person ist.

Beachte, dass wir `<span>`-Tags verwendet haben, um die `itemprop`-Attribute gezielt auf die relevanten Textteile anzuwenden, ohne das visuelle Layout zu verändern.

#### Verschachtelte Items: Beziehungen herstellen

Die wahre Stärke von Microdata zeigt sich, wenn du Items ineinander verschachtelst. Eine Person arbeitet vielleicht für ein Unternehmen. Ein Produkt hat ein Angebot von einem Verkäufer. Ein Unternehmen ist ebenfalls ein Item. Wir können also ein Item als Eigenschaft eines anderen Items definieren.

Nehmen wir an, wir wollen die "WebDev GmbH" nicht nur als reinen Text, sondern als eigenständiges Unternehmen (Typ `Organization`) auszeichnen. Das geht so:

```html
<div itemscope itemtype="https://schema.org/Person">
  <h1 itemprop="name">Max Mustermann</h1>
  <p>
    <span itemprop="jobTitle">Softwareentwickler</span> bei 
    <span itemprop="worksFor" itemscope itemtype="https://schema.org/Organization">
      <span itemprop="name">WebDev GmbH</span>
    </span>.
  </p>
</div>
```

Was ist hier passiert?
- Wir haben eine neue Eigenschaft für die Person verwendet: `worksFor` (arbeitet für).
- Der Wert dieser Eigenschaft ist kein einfacher Text, sondern ein komplett neues Item.
- Deshalb hat das innere `<span>` wieder sein eigenes `itemscope` und ein passendes `itemtype` (`Organization`).
- Innerhalb dieses neuen Items definieren wir wiederum eine Eigenschaft, nämlich den Namen der Organisation mit `itemprop="name"`.

Der Clou an der Sache ist das `itemprop="worksFor"` am äußeren `<span>` des verschachtelten Items. Es stellt die Verbindung her und sagt: "Das `Organization`-Item, das hier beginnt, ist der Wert der `worksFor`-Eigenschaft der übergeordneten `Person`."

#### Spezielle Inhalte mit `itemprop` auszeichnen

Bisher haben wir `itemprop` immer auf Tags angewendet, deren Textinhalt direkt ausgelesen wurde. Aber was ist mit Bildern, Links oder Daten, die nicht direkt sichtbar sein sollen? Microdata hat für alles eine Lösung.

**Für Links und URLs:** Wenn eine Eigenschaft eine URL ist (z.B. die Webseite eines Unternehmens), wird das `itemprop` auf ein `<a>`- oder `<link>`-Tag gesetzt. Die Maschine liest dann automatisch den Wert des `href`-Attributs aus.

```html
<div itemprop="brand" itemscope itemtype="https://schema.org/Brand">
  <a itemprop="url" href="https://www.beispielmarke.de">
    <span itemprop="name">Beispielmarke</span>
  </a>
</div>
```

**Für Bilder:** Ähnlich verhält es sich mit Bildern. Das `itemprop` kommt auf das `<img>`-Tag, und der Wert des `src`-Attributs wird als URL des Bildes interpretiert.

```html
<img itemprop="image" src="/bilder/produkt-xyz.jpg" alt="Ein tolles Produkt">
```

**Für Datum und Uhrzeit:** Der semantisch korrekte Weg ist die Verwendung des `<time>`-Elements. Das `itemprop` wird auf das Tag gesetzt, und die Maschine liest den maschinenlesbaren Wert aus dem `datetime`-Attribut.

```html
<time itemprop="datePublished" datetime="2023-10-27">27. Oktober 2023</time>
```

**Für nicht sichtbare Daten:** Manchmal gibt es Informationen, die für Maschinen wichtig, aber für den Nutzer irrelevant sind (z.B. eine Produkt-ID oder eine ISBN-Nummer). Hierfür kannst du das `<meta>`-Tag innerhalb deines `itemscope` verwenden. Der Wert wird dann aus dem `content`-Attribut gelesen.

```html
<div itemscope itemtype="https://schema.org/Product">
  <h1 itemprop="name">Das ultimative Widget</h1>
  <meta itemprop="productID" content="UW-12345">
  ...
</div>
```

#### Warum der ganze Aufwand?

Das Einpflegen von Microdata ist zugegebenermaßen ein kleiner Mehraufwand. Der Nutzen rechtfertigt ihn jedoch bei Weitem. Wenn Suchmaschinen deine Inhalte nicht nur lesen, sondern auch *verstehen*, können sie diese in den Suchergebnissen viel besser präsentieren.

Das Ergebnis sind sogenannte **Rich Snippets**. Du kennst sie garantiert:
- **Bewertungssterne** und die Anzahl der Stimmen direkt unter einem Produkt.
- **Preise** und die Verfügbarkeit bei einem Online-Shop-Artikel.
- **Kochzeit** und Kalorienangaben bei einem Rezept.
- **Datum, Uhrzeit und Ort** bei einer Veranstaltung.

Diese angereicherten Suchergebnisse fallen auf, erzeugen Vertrauen und führen zu deutlich höheren Klickraten. Du lieferst den Suchmaschinen die Daten auf dem Silbertablett, und sie belohnen dich mit einer besseren Darstellung.

Indem du `itemscope`, `itemtype` und `itemprop` meisterst, verwandelst du dein HTML von einer reinen Ansammlung von Text und Bildern in eine strukturierte, semantische und maschinenlesbare Wissensdatenbank. Du machst deine Inhalte nicht nur für Menschen, sondern auch für die Algorithmen wertvoller, die heute das Tor zum Internet sind.
