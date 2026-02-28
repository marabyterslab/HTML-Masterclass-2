# JSON-LD Einführung

### JSON-LD: Daten für Maschinen verständlich machen

Stell dir vor, du schreibst einen Artikel über deinen Lieblingsfilm auf deiner Webseite. Du fügst den Titel, den Regisseur, das Erscheinungsjahr und eine kurze Inhaltsangabe hinzu. Für einen menschlichen Besucher ist alles klar und verständlich. Er liest den Text und erkennt sofort die Zusammenhänge: "Avatar" ist der Titel, "James Cameron" ist der Regisseur und "2009" ist das Jahr der Veröffentlichung.

Eine Suchmaschine wie Google oder Bing sieht das jedoch anders. Für sie ist das zunächst nur eine Ansammlung von Zeichenketten. Sie ist unglaublich gut darin, Muster zu erkennen und Zusammenhänge zu erraten, aber es bleibt ein Raten. Woher soll die Maschine mit hundertprozentiger Sicherheit wissen, dass "James Cameron" der Regisseur und nicht etwa der Hauptdarsteller oder der Produzent ist?

Hier kommen strukturierte Daten ins Spiel, und JSON-LD ist eine der elegantesten und modernsten Methoden, sie umzusetzen. Es ist eine Brücke zwischen dem für Menschen lesbaren Inhalt deiner Seite und dem maschinellen Verständnis von Suchmaschinen und anderen Programmen.

#### Was bedeutet JSON-LD?

Die Abkürzung steht für **J**ava**S**cript **O**bject **N**otation for **L**inked **D**ata. Lass uns das kurz aufschlüsseln, denn der Name verrät schon fast alles:

*   **JSON (JavaScript Object Notation):** Wenn du bereits ein wenig mit JavaScript zu tun hattest, kennst du dieses Format. Es ist eine sehr einfache und für Menschen gut lesbare Art, Daten in Schlüssel-Wert-Paaren zu organisieren. Ein Schlüssel ist eine Eigenschaft (z. B. `"name"`), und der Wert ist die zugehörige Information (z. B. `"Avatar"`). Genau dieses simple, aber mächtige Format nutzt JSON-LD als Grundlage.

*   **LD (Linked Data):** Das ist der entscheidende Teil. "Linked Data" bedeutet "verknüpfte Daten". Die Idee ist, nicht nur isolierte Informationen bereitzustellen, sondern sie in einen größeren Kontext zu stellen und miteinander zu verknüpfen. JSON-LD ermöglicht es dir zu sagen: "Die Information, die ich hier als `name` bezeichne, ist nicht irgendein Name, sondern der offizielle Titel eines Films, wie er in einem universellen Wörterbuch für Webdaten definiert ist."

Zusammengefasst: JSON-LD verwendet die einfache Syntax von JSON, um klar definierte und verknüpfte Daten direkt in dein HTML-Dokument einzubetten, sodass Maschinen den Inhalt deiner Seite nicht mehr nur lesen, sondern wirklich *verstehen* können.

#### Wie sieht JSON-LD in der Praxis aus?

Im Gegensatz zu anderen Formaten für strukturierte Daten wie Microdata oder RDFa, bei denen du spezielle Attribute direkt in deine HTML-Tags einfügen musst, wird JSON-LD als ein einzelner, sauberer Block in einem `<script>`-Tag platziert. Dieser Block kann entweder im `<head>` oder im `<body>` deines HTML-Dokuments stehen. Für die Darstellung deiner Seite hat er keinerlei Auswirkungen, er ist für das menschliche Auge unsichtbar.

Das Besondere an diesem `<script>`-Tag ist sein `type`-Attribut: `type="application/ld+json"`. Dadurch weiß der Browser (und jede andere Maschine, die die Seite verarbeitet), dass es sich hier nicht um ausführbares JavaScript, sondern um einen Block mit verknüpften Daten im JSON-Format handelt.

Schauen wir uns ein konkretes Beispiel an. Nehmen wir an, du hast folgenden einfachen HTML-Abschnitt auf deiner Seite:

```html
<div>
  <h1>Avatar - Aufbruch nach Pandora</h1>
  <p>Regie: James Cameron</p>
  <p>Erschienen: 2009</p>
  <p>Ein fantastisches Science-Fiction-Abenteuer auf dem Mond Pandora.</p>
</div>
```

Um diese Informationen für Maschinen verständlich zu machen, könntest du folgenden JSON-LD-Block hinzufügen:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Movie",
  "name": "Avatar - Aufbruch nach Pandora",
  "director": {
    "@type": "Person",
    "name": "James Cameron"
  },
  "datePublished": "2009-12-18",
  "description": "Ein fantastisches Science-Fiction-Abenteuer auf dem Mond Pandora."
}
</script>
```

Lass uns diesen Block Zeile für Zeile analysieren:

1.  **`"@context": "https://schema.org"`**: Dies ist vielleicht der wichtigste Teil. Das `@context`-Feld legt das Vokabular fest – sozusagen das Wörterbuch, das wir verwenden. Es sagt der Maschine: "Alle Begriffe, die ich hier benutze, wie `Movie`, `name` oder `director`, beziehen sich auf die Definitionen, die du unter `https://schema.org` findest." Schema.org ist ein gemeinsames Projekt von Google, Microsoft, Yahoo und Yandex und bietet ein riesiges, standardisiertes Vokabular für alle möglichen Dinge, von Filmen über Rezepte bis hin zu Organisationen und Personen.

2.  **`"@type": "Movie"`**: Hier legen wir fest, welche Art von "Ding" (Entität) wir beschreiben. In diesem Fall ist es ein `Movie` (ein Film). Laut dem Wörterbuch von Schema.org wissen Maschinen nun, dass sie Eigenschaften wie einen Regisseur, Schauspieler oder eine Dauer erwarten können.

3.  **`"name": "Avatar - Aufbruch nach Pandora"`**: Dies ist eine einfache Eigenschaft. Wir weisen dem Schlüssel `name` den Wert `"Avatar - Aufbruch nach Pandora"` zu. Dank `@context` und `@type` weiß die Maschine, dass dies der Name eines Films ist.

4.  **`"director": { ... }`**: Hier wird es interessant. Der Regisseur ist ja keine einfache Zeichenkette, sondern selbst eine Entität – eine Person. Deshalb weisen wir dem Schlüssel `director` nicht nur einen Namen zu, sondern ein weiteres, verschachteltes Objekt. Dieses Objekt hat seinen eigenen `@type`, nämlich `Person`, und seine eigene `name`-Eigenschaft. So schaffen wir eine klare Beziehung: Der `director` dieses `Movie` ist eine `Person` mit dem Namen "James Cameron". Das ist die "Verknüpfung" in Linked Data.

5.  **`"datePublished": "2009-12-18"`**: Eine weitere einfache Eigenschaft, die das Veröffentlichungsdatum im standardisierten Format (JJJJ-MM-TT) angibt.

6.  **`"description": "..."`**: Hier wird die Kurzbeschreibung des Films hinterlegt.

#### Warum solltest du JSON-LD verwenden?

Die offensichtlichste Antwort ist **Suchmaschinenoptimierung (SEO)**. Suchmaschinen nutzen diese strukturierten Daten, um sogenannte **Rich Results** (früher Rich Snippets) zu erzeugen. Das sind die erweiterten, optisch ansprechenderen Suchergebnisse, die du sicher schon oft gesehen hast:

*   **Bewertungssterne** direkt unter einem Produkt oder Rezept.
*   **Kochzeit und Kalorienangaben** bei einem Rezept-Suchergebnis.
*   **Daten und Orte** bei einer Veranstaltung.
*   **Fragen und Antworten** in einem FAQ-Bereich, die direkt in den Suchergebnissen aufklappbar sind.

Diese Rich Results erhöhen die Sichtbarkeit deiner Seite in den Suchergebnissen erheblich. Sie nehmen mehr Platz ein, ziehen die Aufmerksamkeit auf sich und können die Klickrate (Click-Through Rate) deutlich steigern, da der Nutzer bereits vor dem Klick relevante Zusatzinformationen erhält.

Darüber hinaus gibt es weitere, ebenso wichtige Vorteile:

*   **Eindeutigkeit:** Du eliminierst jegliche Zweideutigkeit. Eine Maschine muss nicht mehr raten, was "James Cameron" ist, sondern weiß es.
*   **Wartbarkeit:** Da der gesamte Block mit den strukturierten Daten an einer Stelle steht, ist er sehr einfach zu finden, zu bearbeiten und zu verwalten. Du musst nicht durch deinen gesamten HTML-Code navigieren, um einzelne Attribute zu ändern. Dies ist besonders in modernen Web-Anwendungen und Content-Management-Systemen ein riesiger Vorteil, wo diese Blöcke oft automatisch generiert werden.
*   **Flexibilität:** JSON-LD ist extrem flexibel. Du kannst komplexe, verschachtelte Strukturen abbilden und mehrere Entitäten auf einer Seite beschreiben (z. B. einen Artikel (`Article`) und den Autor des Artikels (`Person`) in separaten Blöcken).

JSON-LD ist somit mehr als nur ein SEO-Trick. Es ist ein wichtiger Schritt hin zu einem semantischen Web – einem Web, in dem Informationen nicht nur für Menschen dargestellt, sondern auch für Maschinen universell verständlich und verarbeitbar gemacht werden. Indem du JSON-LD auf deiner Webseite einsetzt, machst du deine Inhalte zu einem vollwertigen, verständlichen Teil dieses intelligenten Netzes.
