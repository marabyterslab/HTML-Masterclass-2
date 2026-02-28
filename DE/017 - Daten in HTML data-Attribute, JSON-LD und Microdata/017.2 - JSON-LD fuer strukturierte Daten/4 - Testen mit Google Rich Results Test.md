# Testen mit Google Rich Results Test

### Testen mit dem Google Rich Results Test

Nachdem du nun weißt, wie du mit JSON-LD strukturierte Daten erstellst und in deine Webseite einbettest, stellt sich eine entscheidende Frage: Woher weißt du, ob du alles richtig gemacht hast? Und noch wichtiger: Woher weißt du, ob Google deine Arbeit versteht und für sogenannte Rich Results in den Suchergebnissen verwenden kann?

Genau hier kommt das "Rich Results Test"-Tool von Google ins Spiel. Es ist dein wichtigster Verbündeter, um die Qualität und Korrektheit deiner strukturierten Daten zu überprüfen. Stell dir das Tool nicht als optionalen letzten Schritt vor, sondern als festen Bestandteil deines Entwicklungsprozesses. Es ist das Äquivalent zur Rechtschreibprüfung für einen Autor – unverzichtbar, um Fehler zu finden, bevor die ganze Welt sie sieht.

#### Was genau macht das Tool?

Im Grunde genommen simuliert das Rich Results Test-Tool, wie der Googlebot deine Webseite analysiert, speziell im Hinblick auf strukturierte Daten. Es erfüllt dabei zwei Hauptaufgaben:

1.  **Validierung der Syntax:** Das Tool prüft, ob dein JSON-LD-Code syntaktisch korrekt ist. Fehlt eine schließende Klammer? Hast du ein Komma an der falschen Stelle gesetzt? Solche grundlegenden Fehler, die deinen gesamten Code unbrauchbar machen können, werden sofort aufgedeckt.
2.  **Prüfung auf Rich-Result-Konformität:** Das ist der entscheidende Teil. Google unterstützt nicht jede Eigenschaft aus dem schema.org-Vokabular für Rich Results. Für jeden unterstützten Typ (wie Rezept, Veranstaltung, Produkt etc.) gibt es eine Liste von erforderlichen und empfohlenen Eigenschaften. Das Tool gleicht deine Daten mit diesen spezifischen Google-Richtlinien ab. Es sagt dir nicht nur, *ob* dein Code gültig ist, sondern auch, *ob er für die Anzeige als Rich Result geeignet ist*.

#### Zwei Wege zum Test: URL oder Code-Snippet

Wenn du das Tool aufrufst, bietet es dir zwei Möglichkeiten, deine Daten zu testen:

*   **URL abrufen:** Hier gibst du die vollständige URL einer bereits veröffentlichten Webseite ein. Das Tool ruft die Seite dann so ab, wie es auch der Googlebot tun würde. Dies ist der beste Weg, um eine Live-Seite zu testen, da es das gesamte gerenderte HTML analysiert, einschließlich strukturierter Daten, die möglicherweise erst durch JavaScript dynamisch hinzugefügt werden.
*   **Code eingeben:** Hier kannst du direkt ein HTML-Snippet oder nur dein `<script type="application/ld+json">` einfügen. Diese Option ist perfekt während der Entwicklungsphase. Du musst deine Seite nicht erst online stellen, um zu sehen, ob dein JSON-LD-Markup korrekt ist. Du kannst Änderungen direkt im Tool testen und iterativ verbessern.

Für unsere Zwecke konzentrieren wir uns zunächst auf die Code-Eingabe, da du damit am schnellsten experimentieren kannst.

#### Ein praktisches Beispiel: Ein Rezept wird getestet

Stellen wir uns vor, du hast das folgende JSON-LD für ein Pfannkuchen-Rezept geschrieben und möchtest es überprüfen.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org/",
  "@type": "Recipe",
  "name": "Einfache Pfannkuchen",
  "author": {
    "@type": "Person",
    "name": "Max Mustermann"
  },
  "datePublished": "2024-10-26",
  "description": "Ein schnelles und leckeres Rezept für klassische Pfannkuchen.",
  "image": [
    "https://example.com/images/pfannkuchen.jpg"
  ],
  "recipeIngredient": [
    "250g Mehl",
    "2 Eier",
    "500ml Milch",
    "1 Prise Salz"
  ],
  "recipeInstructions": [
    {
      "@type": "HowToStep",
      "text": "Mehl und Salz in einer Schüssel mischen."
    },
    {
      "@type": "HowToStep",
      "text": "Eier und Milch hinzufügen und zu einem glatten Teig verrühren."
    },
    {
      "@type": "HowToStep",
      "text": "In einer heißen Pfanne mit etwas Butter goldbraun ausbacken."
    }
  ],
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.5",
    "ratingCount": "117"
  },
  "prepTime": "PT10M",
  "cookTime": "PT15M",
  "totalTime": "PT25M",
  "recipeYield": "4 Portionen",
  "keywords": "Pfannkuchen, Eierkuchen, Frühstück"
}
</script>
```

Du kopierst diesen Code, fügst ihn in das Test-Tool unter "Code" ein und klickst auf "Code testen". Nach einem kurzen Moment der Analyse präsentiert dir das Tool das Ergebnis.

#### Die Ergebnisse richtig interpretieren

Das Ergebnis ist der wertvollste Teil. Es ist nicht nur ein einfaches "bestanden" oder "nicht bestanden". Es gibt dir detailliertes Feedback, das in drei Kategorien unterteilt ist: Fehler, Warnungen und gültige Elemente.

**1. Der Idealfall: Alles ist grün**

Wenn dein Markup perfekt ist, siehst du eine grüne Bestätigung: "Seite ist für Rich-Suchergebnisse geeignet". Darunter listet das Tool alle erkannten strukturierten Datenelemente auf. In unserem Fall würde es "1 erkanntes Element: Rezept" anzeigen.

Wenn du darauf klickst, siehst du eine aufgeschlüsselte Ansicht aller Eigenschaften, die das Tool aus deinem Code extrahiert hat. Dies ist eine hervorragende Möglichkeit, um zu überprüfen, ob Google die Daten genau so interpretiert, wie du es beabsichtigt hast. Du kannst sogar eine Vorschau sehen, die dir eine ungefähre Vorstellung davon gibt, wie dein Rich Result in den Suchergebnissen aussehen könnte.

**2. Der häufige Fall: Warnungen (Gelbes Ausrufezeichen)**

Nehmen wir an, du hättest in unserem Rezept die Eigenschaft `aggregateRating` weggelassen. Das Rezept ist immer noch ein gültiges Rezept, aber ihm fehlt eine Information, die Google als wertvoll für den Nutzer erachtet.

In diesem Fall würde das Tool immer noch anzeigen, dass die Seite für Rich Results geeignet ist, aber es würde eine Warnung ausgeben. Eine typische Warnung lautet: "Das Feld 'aggregateRating' wird empfohlen. Bitte gib einen Wert an, falls verfügbar."

**Was bedeutet eine Warnung?** Eine Warnung ist kein Showstopper. Dein Markup ist immer noch gültig und kann für ein Rich Result qualifiziert sein. Es ist lediglich ein Hinweis von Google, dass du dein Markup durch Hinzufügen empfohlener Felder weiter verbessern könntest. Ein Rezept mit Bewertungen hat eine höhere Chance, in den Suchergebnissen hervorzustechen, als eines ohne. Warnungen solltest du also ernst nehmen und die fehlenden Daten nach Möglichkeit ergänzen, um das volle Potenzial auszuschöpfen.

**3. Der Problemfall: Fehler (Rotes Ausrufezeichen)**

Jetzt wird es ernst. Was passiert, wenn du eine für das Rezept-Rich-Result *erforderliche* Eigenschaft wie `name` vergisst?

```json
{
  "@context": "https://schema.org/",
  "@type": "Recipe",
  // "name": "Einfache Pfannkuchen", <-- absichtlich entfernt
  "image": [
    "https://example.com/images/pfannkuchen.jpg"
  ],
  // ... restlicher Code
}
```

Wenn du diesen Code testest, schlägt die Validierung fehl. Du erhältst eine klare rote Fehlermeldung, die besagt, dass die Seite *nicht* für Rich Results geeignet ist. Das Tool wird dir auch genau sagen, was das Problem ist: "Das Feld 'name' muss angegeben werden."

**Was bedeutet ein Fehler?** Ein Fehler ist kritisch. Solange auch nur ein einziger Fehler vorhanden ist, wird Google deine strukturierten Daten für diesen Rich-Result-Typ ignorieren. Deine Seite ist disqualifiziert. Fehler müssen unbedingt behoben werden. Das Gute daran ist, dass das Tool dir präzise Anweisungen gibt, was zu tun ist. Du musst nicht raten, sondern kannst den Fehler gezielt korrigieren, den Code erneut testen und so lange wiederholen, bis alle roten Markierungen verschwunden sind.

#### Mehr als nur JSON-LD

Obwohl wir uns hier auf JSON-LD konzentrieren, ist es wichtig zu wissen, dass das Rich Results Test-Tool auch andere Formate für strukturierte Daten wie Microdata und RDFa versteht und validiert. Wenn das Tool eine Seite analysiert, sucht es nach allen diesen Formaten und präsentiert dir ein Gesamtergebnis.

#### Ein Werkzeug für den gesamten Lebenszyklus

Verwende das Rich Results Test-Tool nicht nur einmal am Ende. Integriere es in deinen Arbeitsablauf:

*   **Beim Schreiben:** Teste deine JSON-LD-Snippets, während du sie erstellst.
*   **Vor dem Deployment:** Teste die gesamte HTML-Seite in einer Staging-Umgebung.
*   **Nach dem Go-Live:** Überprüfe die Live-URL, um sicherzustellen, dass nichts durch den Server oder andere Skripte beeinträchtigt wird.
*   **Bei Änderungen:** Wenn du Inhalte auf der Seite aktualisierst (z.B. ein neues Bild für ein Rezept), stelle sicher, dass auch deine strukturierten Daten auf dem neuesten Stand sind, und teste erneut.

Indem du das Testen zu einer Routine machst, stellst du sicher, dass deine sorgfältig erstellten strukturierten Daten ihre Aufgabe erfüllen: Suchmaschinen dabei zu helfen, deine Inhalte besser zu verstehen und sie Nutzern in einer ansprechenderen und nützlicheren Form zu präsentieren.
