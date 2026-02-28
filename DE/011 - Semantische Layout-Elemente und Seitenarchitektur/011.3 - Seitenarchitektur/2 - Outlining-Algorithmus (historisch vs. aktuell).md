# Outlining-Algorithmus (historisch vs. aktuell)

### Die Anatomie einer Webseite: Der Outlining-Algorithmus gestern und heute

Wenn du eine Webseite baust, erschaffst du nicht nur ein visuelles Design, sondern auch eine unsichtbare Struktur. Diese Struktur, die Gliederung deines Dokuments, ist für Maschinen wie Suchmaschinen-Crawler und insbesondere für assistierende Technologien wie Screenreader von entscheidender Bedeutung. Sie ist wie das Inhaltsverzeichnis eines Buches: Sie verrät auf einen Blick, worum es geht und wie die Inhalte zueinander in Beziehung stehen. Der Mechanismus, der diese Gliederung aus deinem HTML-Code ableitet, wird als Outlining-Algorithmus (oder Gliederungsalgorithmus) bezeichnet. Und die Geschichte dieses Algorithmus ist eine faszinierende Erzählung von einer großen Vision und einer pragmatischen Realität.

#### Der historische Traum: HTML5 und der kontextbasierte Gliederungsalgorithmus

Mit der Einführung von HTML5 kam eine revolutionäre Idee auf, die die Art und Weise, wie wir über Dokumentenstruktur nachdenken, für immer verändern sollte. Die Vision war elegant und bestechend einfach: Die Hierarchieebene einer Überschrift (`<h1>` bis `<h6>`) sollte nicht mehr absolut sein, sondern sich aus dem Kontext ergeben, in dem sie steht.

Konkret bedeutete das: Jedes sogenannte „Sectioning Content Element“ – also `<article>`, `<section>`, `<nav>` und `<aside>` – sollte seinen eigenen, in sich geschlossenen Gliederungskontext schaffen. Innerhalb eines solchen Elements würde eine `<h1>`-Überschrift immer die ranghöchste Überschrift für genau diesen Abschnitt darstellen. Die tatsächliche Ebene in der Gesamtgliederung des Dokuments würde der Browser dann automatisch berechnen, basierend darauf, wie tief das Sectioning Element verschachtelt ist.

Klingt kompliziert? Lass uns das an einem Beispiel betrachten. Nach dieser ursprünglichen HTML5-Spezifikation wäre der folgende Code vollkommen korrekt und semantisch ideal gewesen:

```html
<body>
  <h1>Meine fantastische Webseite</h1>
  <section>
    <h1>Kapitel 1: Die Grundlagen</h1>
    <p>Hier steht der Einführungstext.</p>
    <article>
      <h1>Unterkapitel 1.1: Ein wichtiges Detail</h1>
      <p>Details, Details, Details...</p>
    </article>
  </section>
  <section>
    <h1>Kapitel 2: Für Fortgeschrittene</h1>
    <p>Jetzt wird es spannend.</p>
  </section>
</body>
```

Die Vision dahinter war, dass der Browser diesen Code interpretiert und daraus folgende Gliederung ableitet:

1.  Meine fantastische Webseite (`<h1>`)
    1.  Kapitel 1: Die Grundlagen (interpretiert als `<h2>`)
        1.  Unterkapitel 1.1: Ein wichtiges Detail (interpretiert als `<h3>`)
    2.  Kapitel 2: Für Fortgeschrittene (interpretiert als `<h2>`)

Das große Versprechen dieser Methode war die Modularität. Du könntest einen kompletten `<article>`-Block, inklusive seiner eigenen `<h1>`, als eine in sich geschlossene Komponente entwickeln. Diese Komponente könntest du dann beliebig auf deiner Seite verschieben – vom Hauptinhalt in eine Seitenleiste, von einer Seite auf eine andere –, ohne auch nur eine einzige Überschriften-Ebene im Code anpassen zu müssen. Der Algorithmus sollte sich um alles kümmern. Es war der Traum eines jeden komponentenbasierten Webdesigns: wirklich unabhängige, wiederverwendbare Bausteine.

#### Die ernüchternde Realität: Fehlende Implementierung und die Folgen

Die Idee war brillant. Die Umsetzung durch die Browser-Hersteller... fand jedoch nie statt.

Bis heute hat kein einziger großer Browser den HTML5-Outlining-Algorithmus in einer Weise implementiert, die für die wichtigsten Nutzer – nämlich die von assistierenden Technologien – zugänglich wäre. Screenreader und andere Werkzeuge haben sich nie auf diese automatische Berechnung der Überschriftenebenen verlassen. Sie lesen einfach das, was im Code steht: ein `<h1>`, ein weiteres `<h1>`, und noch ein `<h1>`.

Das Ergebnis war ein gefährliches Auseinanderklaffen von Theorie und Praxis. Entwickler, die sich an die Spezifikation hielten, produzierten Webseiten, die in der Theorie eine perfekte Gliederung hatten. In der Praxis präsentierten sie Screenreader-Nutzern jedoch eine flache, verwirrende Struktur, die aus mehreren gleichrangigen `<h1>`-Überschriften bestand. Eine Gliederung, die von den wichtigsten Werkzeugen ignoriert wird, ist für die Barrierefreiheit nutzlos und sogar schädlich.

Diese Diskrepanz führte zu jahrelanger Verwirrung. Validierungstools zeigten vielleicht eine „korrekte“ Gliederung nach der HTML5-Theorie an, während die realen Erfahrungen der Nutzer eine ganz andere Sprache sprachen. Die Web-Community erkannte schließlich, dass der Traum von einem vollautomatischen Gliederungsalgorithmus – zumindest vorerst – gescheitert war.

#### Die heutige Praxis: Zurück zur klaren, manuellen Hierarchie

Angesichts der fehlenden Browser-Unterstützung hat sich die bewährte, klassische Methode als der einzig verlässliche Weg durchgesetzt. Die aktuelle Best Practice ist einfach, robust und wird von allen Werkzeugen und Browsern universell verstanden.

**Die Regeln sind klar und unmissverständlich:**

1.  **Verwende genau eine `<h1>`-Überschrift pro Seite.** Diese `<h1>` repräsentiert den Haupttitel des gesamten Dokuments, quasi den Titel des Buches. Sie sollte kurz und prägnant den Inhalt der gesamten Seite beschreiben.
2.  **Strukturiere deine Inhalte mit `<h2>` bis `<h6>` in einer logischen, absteigenden Reihenfolge.** Beginne mit `<h2>` für die Hauptabschnitte deiner Seite. Wenn ein `<h2>`-Abschnitt weitere Unterabschnitte benötigt, verwende `<h3>` und so weiter.
3.  **Überspringe keine Überschriftenebenen.** Gehe niemals direkt von einer `<h2>` zu einer `<h4>`. Eine solche Lücke in der Hierarchie kann Screenreader-Nutzer verwirren, da sie annehmen könnten, dass Inhalte fehlen.

Lass uns unser vorheriges Beispiel nehmen und es nach den heutigen Best Practices korrekt strukturieren:

```html
<body>
  <h1>Meine fantastische Webseite</h1>
  <section>
    <h2>Kapitel 1: Die Grundlagen</h2>
    <p>Hier steht der Einführungstext.</p>
    <article>
      <h3>Unterkapitel 1.1: Ein wichtiges Detail</h3>
      <p>Details, Details, Details...</p>
    </article>
  </section>
  <section>
    <h2>Kapitel 2: Für Fortgeschrittene</h2>
    <p>Jetzt wird es spannend.</p>
  </section>
</body>
```

Dieser Code erzeugt eine Gliederung, die für jeden – Mensch und Maschine – sofort verständlich ist:

1.  Meine fantastische Webseite (`<h1>`)
    1.  Kapitel 1: Die Grundlagen (`<h2>`)
        1.  Unterkapitel 1.1: Ein wichtiges Detail (`<h3>`)
    2.  Kapitel 2: Für Fortgeschrittene (`<h2>`)

Diese Methode erfordert zwar, dass du beim Verschieben von Inhalten die Überschriftenebenen manuell anpassen musst, aber sie hat einen unschätzbaren Vorteil: Sie funktioniert. Immer. Überall. Klarheit und Kompatibilität schlagen hier die theoretische Eleganz des alten Algorithmus um Längen.

#### Die Rolle von `<section>` & Co. in der modernen Welt

Jetzt fragst du dich vielleicht: Wenn `<section>` und `<article>` die Überschriftenebene nicht mehr beeinflussen, wozu brauche ich sie dann überhaupt noch?

Ihre Bedeutung hat sich nicht verringert, sondern nur verlagert. Diese Elemente sind nach wie vor essenziell für die semantische Auszeichnung deines Dokuments. Ihre Aufgabe ist es nicht, die Überschriftenhierarchie zu *berechnen*, sondern thematisch zusammengehörige Inhalte zu *gruppieren* und ihnen eine Bedeutung zu geben.

*   **`<section>`:** Gruppiert einen thematischen Block von Inhalten. Stell es dir als ein Kapitel in deinem Dokument vor. Jede `<section>` sollte idealerweise mit einer Überschrift (`<h2>`-`<h6>`) beginnen, die ihren Inhalt beschreibt.
*   **`<article>`:** Definiert einen in sich geschlossenen, eigenständigen Inhalt, der potenziell unabhängig vom Rest der Seite existieren und weiterverteilt werden könnte (z.B. ein Blogbeitrag, ein Forenpost, ein Nachrichtenartikel).
*   **`<nav>`:** Bezeichnet einen Block mit Navigationslinks.
*   **`<aside>`:** Enthält Inhalte, die nur am Rande mit dem Hauptinhalt zu tun haben, wie eine Seitenleiste mit weiterführenden Links oder eine Werbeanzeige.

Für Screenreader sind diese Elemente sogenannte „Landmarks“. Sie ermöglichen es Nutzern, schnell und effizient durch eine Seite zu navigieren, indem sie direkt zum Hauptinhalt, zur Navigation oder zu einem bestimmten Abschnitt springen. In Kombination mit einer sauberen Überschriftenhierarchie schaffst du so eine robuste und zugängliche Seitenarchitektur, die für alle funktioniert. Der Outlining-Algorithmus ist heute also das, was du explizit durch die Ränge deiner Überschriften definierst – eine direkte und unmissverständliche Anweisung an die Maschinen, wie deine Seite zu verstehen ist.
