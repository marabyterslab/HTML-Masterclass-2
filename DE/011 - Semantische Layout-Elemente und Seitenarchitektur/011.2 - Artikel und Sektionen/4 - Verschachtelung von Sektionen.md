# Verschachtelung von Sektionen

### Die Hierarchie der Inhalte: Verschachtelung von Sektionen

Du hast gelernt, dass das `<section>`-Element dazu dient, thematisch zusammengehörige Inhalte auf einer Webseite zu gruppieren. Eine Webseite ist aber selten nur eine flache Liste von Themen. Oft gibt es Hauptthemen, die sich wiederum in Unterthemen gliedern. Denk an ein Buch: Es hat Kapitel, und jedes Kapitel kann mehrere Unterkapitel haben. Genau diese logische Gliederung kannst du in HTML abbilden, indem du Sektionen ineinander verschachtelst.

#### Das Prinzip der Dokument-Gliederung (Document Outline)

Bevor wir in die Praxis eintauchen, ist es wichtig, ein zentrales Konzept zu verstehen: die Dokument-Gliederung (im Englischen "Document Outline"). Jedes Mal, wenn du ein semantisches Sektionierungselement wie `<section>`, `<article>`, `<nav>` oder `<aside>` verwendest, erzeugst du einen neuen, eigenständigen Bereich in der logischen Struktur deines Dokuments.

Der entscheidende Punkt dabei ist: Die erste Überschrift (`<h1>` bis `<h6>`), die innerhalb eines solchen Elements platziert wird, wird zur Überschrift dieses Gliederungsabschnitts. Alle weiteren Überschriften innerhalb desselben Abschnitts werden als untergeordnet betrachtet. Wenn du nun eine `<section>` in eine andere `<section>` einbettest, erstellst du einen Unterpunkt in dieser Gliederung.

Stell es dir wie eine Baumstruktur vor. Die Hauptsektion ist ein Ast, und eine verschachtelte Sektion ist ein kleinerer Ast, der von diesem abzweigt. Suchmaschinen und insbesondere assistierende Technologien wie Screenreader nutzen diese Gliederung, um die Struktur deiner Seite zu verstehen und dem Benutzer eine schnelle Navigation zwischen den Themenbereichen zu ermöglichen. Eine saubere, logische Verschachtelung ist also nicht nur für dich als Entwickler eine Hilfe, sondern ein entscheidender Faktor für Barrierefreiheit und SEO.

#### Einfache Verschachtelung: Haupt- und Unterthemen

Beginnen wir mit einem einfachen, greifbaren Beispiel. Stell dir vor, du schreibst einen langen Artikel über die Entwicklung des Internets. Der Artikel selbst ist ein `<article>`. Innerhalb dieses Artikels möchtest du die Geschichte in zwei große Abschnitte unterteilen: "Die Anfänge" und "Das moderne Web". Das ist ein perfekter Anwendungsfall für verschachtelte Sektionen.

```html
<article>
  <h1>Die Entwicklung des Internets</h1>
  <p>Eine kurze Reise durch die Zeit, von den ersten Netzwerken bis heute.</p>

  <section>
    <h2>Die Anfänge (1960er - 1990er)</h2>
    <p>In dieser Ära wurde der Grundstein gelegt. Es begann mit dem ARPANET, einem Projekt des US-Verteidigungsministeriums...</p>
    <p>Weitere Details zu den frühen Protokollen und der akademischen Nutzung.</p>
  </section>

  <section>
    <h2>Das moderne Web (ab 1990)</h2>
    <p>Mit der Erfindung des World Wide Web durch Tim Berners-Lee änderte sich alles. Der erste Browser, die erste Webseite...</p>
    <p>Hier geht es um die Kommerzialisierung, soziale Medien und die mobile Revolution.</p>
  </section>

</article>
```

In diesem Beispiel ist der `<article>` der Hauptcontainer für einen in sich geschlossenen Inhalt. Die beiden `<section>`-Elemente gliedern diesen Inhalt weiter. Beachte die Überschriftenebenen: Das `<h1>` ist die Überschrift des gesamten Artikels. Die `<h2>`-Überschriften definieren die Titel der beiden Hauptabschnitte *innerhalb* des Artikels. Die Gliederung sieht logisch so aus:

1.  Die Entwicklung des Internets (`<h1>`)
    1.  Die Anfänge (1960er - 1990er) (`<h2>` in der ersten `<section>`)
    2.  Das moderne Web (ab 1990) (`<h2>` in der zweiten `<section>`)

#### Tiefere Verschachtelung für komplexe Strukturen

Manchmal reichen zwei Ebenen nicht aus. Nehmen wir an, du möchtest den Abschnitt "Das moderne Web" noch feiner untergliedern, zum Beispiel in "Das Web 2.0" und "Das mobile Zeitalter". Dafür verschachtelst du einfach weitere `<section>`-Elemente:

```html
<article>
  <h1>Die Entwicklung des Internets</h1>
  <p>Eine kurze Reise durch die Zeit...</p>

  <section>
    <h2>Die Anfänge (1960er - 1990er)</h2>
    <p>...</p>
  </section>

  <section>
    <h2>Das moderne Web (ab 1990)</h2>
    <p>Mit der Erfindung des World Wide Web...</p>

    <section>
      <h3>Das Web 2.0 und die sozialen Medien</h3>
      <p>Der Aufstieg von nutzergenerierten Inhalten, Blogs, Wikis und sozialen Netzwerken wie Facebook und Twitter...</p>
    </section>

    <section>
      <h3>Das mobile Zeitalter</h3>
      <p>Smartphones veränderten die Art und Weise, wie wir das Internet nutzen. Responsive Design wurde zur Notwendigkeit...</p>
    </section>

  </section>

</article>
```

Die Struktur wird nun noch detaillierter. Die `<section>` mit der `<h2>`-Überschrift "Das moderne Web" enthält nun zwei weitere, untergeordnete `<section>`-Elemente. Deren Überschriften sind folgerichtig `<h3>`s. Sie sind semantisch Kinder von "Das moderne Web".

Die logische Gliederung erweitert sich wie folgt:

1.  Die Entwicklung des Internets (`<h1>`)
    1.  Die Anfänge (1960er - 1990er) (`<h2>`)
    2.  Das moderne Web (ab 1990) (`<h2>`)
        1.  Das Web 2.0 und die sozialen Medien (`<h3>`)
        2.  Das mobile Zeitalter (`<h3>`)

Durch diese saubere Strukturierung weiß jeder Browser und jeder Screenreader genau, wie deine Inhalte zusammenhängen.

#### Ein `<h1>` für jede Sektion? Theorie und Praxis

Jetzt wird es ein wenig theoretisch, aber es ist ein wichtiges Detail für dein tiefes Verständnis von HTML. Laut der offiziellen HTML-Spezifikation ist es vollkommen korrekt – und sogar vorgesehen –, dass *jedes* Sektionierungselement (`<section>`, `<article>` etc.) eine eigene `<h1>`-Überschrift haben kann. Der Gedanke dahinter ist, dass jeder dieser Abschnitte ein eigenständiges "Mini-Dokument" innerhalb der Seite darstellt. Die Browser sollen dann aus der Verschachtelungsebene die korrekte Überschriftenhierarchie selbst ableiten.

Ein theoretisch korrektes Beispiel sähe also so aus:

```html
<!-- THEORETISCH KORREKT laut Spezifikation -->
<article>
  <h1>Die Entwicklung des Internets</h1>
  
  <section>
    <h1>Die Anfänge</h1>
    <p>...</p>
  </section>

  <section>
    <h1>Das moderne Web</h1>
    <p>...</p>
    <section>
      <h1>Das Web 2.0</h1>
      <p>...</p>
    </section>
  </section>
</article>
```

In der Praxis hat sich dieser Ansatz jedoch nicht durchgesetzt. Der Grund dafür ist zweigeteilt:
1.  **Browser-Implementierung:** Die automatische Berechnung der Gliederungstiefe durch die Browser (der "Document Outline Algorithm") wurde nie vollständig und konsistent umgesetzt.
2.  **SEO und Barrierefreiheit:** Viele Tools, insbesondere Screenreader und Suchmaschinen-Crawler, verlassen sich nach wie vor stark auf die explizite Hierarchie der `<h1>` bis `<h6>`-Tags. Eine Seite mit mehreren `<h1>`-Tags wird oft als unstrukturiert oder verwirrend interpretiert.

**Daher gilt als bewährte Praxis (Best Practice):** Verwende pro HTML-Seite nur ein einziges `<h1>`-Element für die Hauptüberschrift der gesamten Seite. Strukturiere deine Inhalte danach mit `<h2>`, `<h3>` und so weiter, genau wie in den ersten Beispielen gezeigt. Diese Methode ist robust, wird von allen Systemen verstanden und sorgt für eine klare und zugängliche Seitenarchitektur. Es ist aber gut zu wissen, was die Spezifikation ursprünglich vorsah, um die Logik hinter Sektionierungselementen vollständig zu verstehen.

#### `section` vs. `div`: Wann verschachteln und wann nicht?

Mit dem Wissen über die Verschachtelung von Sektionen stellt sich oft die Frage: Wann nehme ich eine `<section>` und wann ein `<div>` für eine Gruppierung?

Die Regel ist einfach und leitet sich direkt aus dem Konzept der Dokument-Gliederung ab:
**Verwende eine `<section>`, wenn die Inhaltsgruppe eine eigene, sinnvolle Überschrift in der Gliederung deiner Seite rechtfertigt.**

Wenn du Inhalte nur aus rein visuellen Gründen oder zur Anwendung von JavaScript-Logik gruppieren möchtest, ohne dass diese Gruppe einen semantischen Stellenwert in der Dokumentstruktur hat, dann ist ein `<div>` die richtige Wahl. Ein `<div>` hat keine semantische Bedeutung und taucht in der Dokument-Gliederung nicht auf.

Schau dir dieses Beispiel an:

```html
<section>
  <h2>Unsere Produkt-Highlights</h2>
  <p>Hier finden Sie eine Auswahl unserer beliebtesten Produkte.</p>
  
  <!-- Diese Gruppierung ist nur für das Layout (z.B. Flexbox/Grid) -->
  <div class="product-wrapper">
    <article>
      <h3>Produkt A</h3>
      <p>Beschreibung...</p>
    </article>
    <article>
      <h3>Produkt B</h3>
      <p>Beschreibung...</p>
    </article>
  </div>
</section>
```

Hier ist die `<section>` goldrichtig, denn "Unsere Produkt-Highlights" ist ein klar definierter Themenbereich der Seite. Der `<div class="product-wrapper">` hingegen dient nur als gestalterischer Container für die Produkte. Er hat keine eigene thematische Überschrift und trägt nichts zur logischen Gliederung bei. Es wäre falsch, hier eine weitere `<section>` zu verwenden, da du keine passende Überschrift für diesen "Wrapper" finden würdest.

Die bewusste Entscheidung zwischen `<section>` und `<div>` bei der Verschachtelung ist ein Zeichen für hochwertigen, semantischen HTML-Code. Sie zeigt, dass du nicht nur das Aussehen, sondern auch die Struktur und Bedeutung deiner Inhalte im Blick hast.
