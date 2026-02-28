# Das article-Element

### Das `<article>`-Element: In sich geschlossene Inhalte kapseln

Stell dir vor, du liest eine Online-Zeitung. Du scrollst durch die Startseite, die verschiedene Schlagzeilen aus den Ressorts Sport, Politik und Kultur anzeigt. Jeder dieser Teaser ist ein eigenständiger Inhalt. Wenn du einen davon anklickst, landest du auf einer Seite, die nur diesen einen Artikel darstellt. Du könntest diesen Artikel auch ausdrucken, per E-Mail versenden oder in einem RSS-Reader lesen – und er würde immer noch vollständig und verständlich sein.

Genau für solche Fälle wurde das `<article>`-Element in HTML5 eingeführt. Es ist ein semantisches Element, das einen in sich geschlossenen, unabhängigen Inhaltsblock auf einer Webseite auszeichnet. Der entscheidende Gedanke dahinter ist die **Wiederverwendbarkeit und Verteilbarkeit**. Ein Inhalt, der mit `<article>` umschlossen ist, sollte theoretisch aus dem Kontext der ursprünglichen Seite herausgelöst werden können und trotzdem noch einen Sinn ergeben.

#### Was genau ist ein "in sich geschlossener Inhalt"?

Die offizielle Definition beschreibt ein `<article>` als eine „vollständige oder in sich geschlossene Komposition in einem Dokument, einer Seite, einer Anwendung oder einer Website, die für eine unabhängige Verteilung oder Wiederverwendung bestimmt ist“. Das klingt zunächst etwas abstrakt, lässt sich aber an praktischen Beispielen sehr gut verdeutlichen. Typische Kandidaten für das `<article>`-Element sind:

*   **Ein Blogbeitrag:** Der klassische Anwendungsfall. Jeder einzelne Post ist eine eigenständige Einheit.
*   **Ein Nachrichtenartikel:** Ähnlich wie ein Blogbeitrag ist jeder Artikel ein für sich stehendes Werk.
*   **Ein Forenbeitrag:** Der ursprüngliche Beitrag in einem Thread ist ein `<article>`, und oft ist auch jede einzelne Antwort darauf ein eigenständiges `<article>`.
*   **Ein Produkt auf einer Kategorieseite:** In einem Onlineshop ist jedes Produkt in der Listenansicht eine eigenständige Einheit mit Bild, Namen, Preis und Beschreibung. Du könntest dieses eine Produkt teilen, ohne den Rest der Kategorieseite zu benötigen.
*   **Ein einzelner Kommentar in einem Kommentarbereich:** Jeder Nutzerkommentar ist eine unabhängige Aussage.
*   **Ein interaktives Widget:** Ein Wetter-Widget oder ein Börsenticker auf einer Portalseite kann als `<article>` betrachtet werden, da es eine in sich geschlossene Informationseinheit darstellt.

Wichtig ist dabei nicht die Länge des Inhalts. Ein `<article>` kann aus einem einzigen Satz bestehen, wie ein kurzer Tweet, oder Tausende von Wörtern umfassen, wie ein ausführlicher Fachartikel. Die entscheidende Frage ist immer: Ergibt dieser Inhalt auch dann noch Sinn, wenn ich ihn von der umgebenden Seite isoliere?

```html
<!-- Beispiel für eine Blog-Übersichtsseite -->
<main>
  <h1>Mein Tech-Blog</h1>

  <article>
    <h2>Die Macht der semantischen HTML-Elemente</h2>
    <p>Semantisches HTML ist mehr als nur eine gute Praxis. Es verbessert die Zugänglichkeit, SEO und die Wartbarkeit deines Codes...</p>
    <a href="/blog/semantisches-html">Weiterlesen</a>
  </article>

  <article>
    <h2>Ein tiefer Einblick in CSS Grid</h2>
    <p>Vergiss Floats und Tabellenlayouts. CSS Grid bietet eine zweidimensionale Layout-Kontrolle, die das Webdesign revolutioniert...</p>
    <a href="/blog/css-grid-einfuehrung">Weiterlesen</a>
  </article>

</main>
```

In diesem Beispiel ist jeder Blog-Teaser ein `<article>`. Du könntest jeden dieser Blöcke nehmen und in einen RSS-Feed einfügen, und der Inhalt wäre immer noch klar verständlich.

#### Die wichtige Unterscheidung: `<article>` vs. `<section>`

Eines der häufigsten Missverständnisse in der semantischen Auszeichnung ist die Abgrenzung zwischen `<article>` und `<section>`. Beide Elemente dienen dazu, Inhalte zu gruppieren, aber ihre Absicht ist grundverschieden.

*   Ein **`<article>`** ist für **eigenständige, verteilbare Inhalte**. Wie oben beschrieben, muss der Inhalt für sich alleine stehen können.
*   Ein **`<section>`** ist für die **thematische Gruppierung von Inhalten** innerhalb eines Dokuments. Der Inhalt einer `<section>` ergibt oft nur im Kontext der umgebenden Seite einen Sinn.

Stellen wir uns wieder die Online-Zeitung vor. Die Seite ist in die Bereiche "Sport", "Politik" und "Wirtschaft" unterteilt. Jeder dieser Bereiche wäre eine perfekte `<section>`.

*   `<section>`: Der Sportteil.
*   `<section>`: Der Politikteil.

Innerhalb der Sport-`<section>` findest du dann mehrere einzelne Nachrichtenmeldungen. Jede dieser Meldungen ist ein `<article>`.

*   `<section id="sport">`
    *   `<h1>Sport</h1>`
    *   `<article>`: Spielbericht zum Fußballspiel vom Wochenende.
    *   `<article>`: Interview mit einer Tennisspielerin.
    *   `<article>`: Kurzmeldung zu Transfergerüchten.
*   `</section>`

Die Faustregel lautet: Frage dich, ob der Inhalt eine eigene Überschrift in einer Inhaltsübersicht oder einem RSS-Feed rechtfertigen würde. Wenn ja, ist es wahrscheinlich ein `<article>`. Wenn es nur ein thematischer Abschnitt der aktuellen Seite ist (z. B. "Einleitung", "Unsere Dienstleistungen", "Kontaktinformationen"), dann ist `<section>` die bessere Wahl.

Es ist auch möglich und oft sinnvoll, `<section>`-Elemente innerhalb eines `<article>` zu verwenden. Ein langer wissenschaftlicher Artikel könnte beispielsweise in Abschnitte wie "Einleitung", "Methodik" und "Ergebnisse" unterteilt sein.

```html
<article>
  <h1>Die Auswirkungen des Klimawandels auf alpine Ökosysteme</h1>
  
  <section>
    <h2>Einleitung</h2>
    <p>Die globale Erwärmung stellt eine signifikante Bedrohung für empfindliche Ökosysteme dar...</p>
  </section>
  
  <section>
    <h2>Beobachtete Veränderungen</h2>
    <p>Studien der letzten Jahrzehnte zeigen einen deutlichen Rückgang der Gletscher...</p>
  </section>
  
  <section>
    <h2>Zukünftige Prognosen</h2>
    <p>Modellierungen deuten darauf hin, dass ohne drastische Maßnahmen...</p>
  </section>

</article>
```
Hier ist der gesamte wissenschaftliche Aufsatz der eigenständige Inhalt (`<article>`), während die Kapitel darin thematische Gruppierungen (`<section>`) sind.

#### Verschachtelung von `<article>`-Elementen

Ein weiteres interessantes Merkmal ist, dass `<article>`-Elemente ineinander verschachtelt werden können. Das klassische Beispiel hierfür ist ein Blogbeitrag mit Kommentaren. Der Blogbeitrag selbst ist ein `<article>`. Jeder Kommentar, der zu diesem Beitrag abgegeben wird, ist ebenfalls ein eigenständiger, in sich geschlossener Beitrag und sollte daher ebenfalls als `<article>` ausgezeichnet werden.

```html
<article>
  <header>
    <h1>Wie man den perfekten Kaffee kocht</h1>
    <p>Veröffentlicht am <time datetime="2023-10-27">27. Oktober 2023</time> von Alex</p>
  </header>
  
  <p>Die Zubereitung von Kaffee ist eine Kunst. Hier sind meine Top-5-Tipps...</p>
  
  <footer>
    <p>Tags: Kaffee, Barista, Tipps</p>
  </footer>

  <!-- Beginn des Kommentarbereichs -->
  <section id="kommentare">
    <h2>Kommentare</h2>

    <article>
      <header>
        <p><strong>Bettina</strong> schrieb:</p>
      </header>
      <p>Toller Artikel! Ich habe Tipp 3 ausprobiert und der Kaffee war fantastisch.</p>
      <footer>
        <p>Gepostet am <time datetime="2023-10-27T14:30:00Z">27. Oktober 2023 um 14:30</time></p>
      </footer>
    </article>

    <article>
      <header>
        <p><strong>Carlos</strong> schrieb:</p>
      </header>
      <p>Ich würde noch hinzufügen, dass die Wasserqualität entscheidend ist.</p>
      <footer>
        <p>Gepostet am <time datetime="2023-10-27T15:10:00Z">27. Oktober 2023 um 15:10</time></p>
      </footer>
    </article>

  </section>
</article>
```
In diesem Aufbau ist der Haupt-Blogbeitrag das übergeordnete `<article>`. Der Kommentarbereich ist eine thematische `<section>` innerhalb dieses Artikels. Und jeder einzelne Kommentar ist wiederum ein verschachteltes `<article>`, da er eine eigenständige Meinungsäußerung darstellt.

#### Struktur innerhalb eines `<article>`

Ein `<article>` ist wie ein Mini-Dokument innerhalb deiner Webseite. Daher ist es eine gute Praxis, ihm auch eine eigene, sinnvolle Struktur zu geben. Typischerweise enthält ein `<article>`:

*   **Eine Überschrift:** Meist ein `<h1>` oder `<h2>`. Welche Ebene du wählst, hängt von der Gesamtstruktur deiner Seite ab. Wichtig ist, dass jedes `<article>` eine eigene, beschreibende Überschrift hat.
*   **Ein `<header>`-Element:** Optional, aber oft nützlich, um Metadaten wie den Autor, das Veröffentlichungsdatum oder Kategorien zu bündeln.
*   **Ein `<footer>`-Element:** Ebenfalls optional, aber gut geeignet für verwandte Informationen wie Tags, Share-Buttons oder Quellenangaben.

#### Warum ist das alles wichtig? Die Vorteile der Semantik

Du könntest all diese Layouts natürlich auch mit `<div>`-Elementen und CSS-Klassen bauen. Warum also der Aufwand mit `<article>`? Die Antwort liegt in den Vorteilen, die über die reine visuelle Darstellung hinausgehen.

1.  **Barrierefreiheit (Accessibility):** Screenreader und andere assistierende Technologien erkennen das `<article>`-Element. Sie können einem Nutzer beispielsweise die Möglichkeit bieten, direkt von Artikel zu Artikel auf einer Seite zu springen und irrelevante Teile wie Navigation oder Werbung zu überspringen. Das verbessert die Benutzererfahrung für Menschen mit Behinderungen erheblich.

2.  **Suchmaschinenoptimierung (SEO):** Suchmaschinen wie Google verstehen semantische Tags. Wenn sie ein `<article>`-Tag sehen, wissen sie, dass es sich hier um einen primären, eigenständigen Inhalt handelt. Dies kann helfen, deine Inhalte besser zu indizieren und sie für relevante Suchanfragen in den Vordergrund zu rücken, beispielsweise in News-Feeds oder speziellen Suchergebnis-Blöcken.

3.  **Wartbarkeit und Lesbarkeit des Codes:** Für dich und andere Entwickler wird der Code sofort verständlicher. Ein `<div class="blog-post-wrapper">` sagt weniger aus als ein klares `<article>`. Semantischer Code ist selbsterklärend und macht die Struktur deiner Seite auf den ersten Blick nachvollziehbar.

Das `<article>`-Element ist also weit mehr als nur ein Container. Es ist ein starkes semantisches Werkzeug, das deinem Inhalt eine klare Bedeutung verleiht. Indem du es bewusst und korrekt einsetzt, schaffst du nicht nur eine logische und gut strukturierte Webseite, sondern machst sie auch zugänglicher, maschinenlesbarer und zukunftssicherer.
