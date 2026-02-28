# Wiederverwendbarkeit planen

### Wiederverwendbarkeit planen: Vom Atom zum Organismus

Stell dir vor, du baust ein Haus aus Legosteinen. Du würdest nicht für jede Wand einen riesigen, einzigartigen Klotz gießen. Stattdessen hast du eine Sammlung von Standardsteinen – kleine Einer, längliche Vierer, flache Platten –, die du auf unzählige Weisen kombinieren kannst. Wenn du eine Wand ändern möchtest, tauschst du einfach ein paar Steine aus, anstatt die ganze Wand einzureißen.

Genau diese Denkweise ist der Schlüssel zu modernem, effizientem und wartbarem Webdesign. Anstatt jede Seite als ein monolithisches, einzigartiges Kunstwerk zu betrachten, lernen wir, sie als ein System aus wiederverwendbaren Komponenten zu sehen. Dieses "Komponenten-Denken" ist keine komplizierte Technik, sondern eine grundlegende Haltungsänderung. Du hörst auf, Seiten zu bauen, und fängst an, Systeme zu entwerfen.

Ein fantastisches mentales Modell, um diese Herangehensweise zu strukturieren, ist das **Atomic Design**, ein Konzept, das von Brad Frost populär gemacht wurde. Es teilt eine Benutzeroberfläche in fünf verschiedene, aufeinander aufbauende Ebenen auf, genau wie die Chemie die Welt in Atome, Moleküle und Organismen unterteilt. Indem wir diese Ebenen verstehen und für unsere HTML-Strukturen planen, schaffen wir ein robustes Fundament für jedes Webprojekt.

#### Die erste Ebene: Atome

Atome sind die kleinsten, nicht weiter teilbaren Bausteine deiner Benutzeroberfläche. Sie sind die fundamentalen HTML-Tags, die für sich allein genommen abstrakt sind, aber die Grundlage für alles Weitere bilden.

Denk an Elemente wie:

*   Ein `<label>`
*   Ein `<input>`-Feld
*   Ein `<button>`
*   Eine Überschrift wie `<h1>` oder `<h2>`
*   Ein einfacher Textabsatz `<p>`
*   Ein Bild `<img>`

Ein einzelnes `<input>`-Feld hat für sich genommen noch keine große Funktion. Es ist einfach nur da. Aber es ist ein universeller, wiederverwendbarer Baustein. Die Kunst auf dieser Ebene besteht darin, diese grundlegenden Elemente zu definieren und ihnen ein einheitliches, grundlegendes Styling zu geben (was später mit CSS geschieht). Für unsere HTML-Planung bedeutet das, zu erkennen, welche dieser grundlegenden "Atome" wir in unserem Projekt benötigen.

```html
<!-- Ein Atom: Ein einfacher Button -->
<button class="btn">Klick mich</button>

<!-- Ein weiteres Atom: Ein Texteingabefeld -->
<input class="form-input" type="text" placeholder="Dein Name...">
```

Diese Atome sind die Grundelemente in deinem Werkzeugkasten. Sie sind kontextlos und universell einsetzbar.

#### Die zweite Ebene: Moleküle

Wenn sich Atome verbinden, bilden sie Moleküle. In der Welt des Webdesigns sind Moleküle kleine, funktionale Einheiten, die aus einer Gruppe von Atomen bestehen. Sie haben eine klare Aufgabe und bilden zusammen eine sinnvolle Einheit.

Ein klassisches Beispiel ist ein Suchformular. Es besteht aus mehreren Atomen:

*   Ein `<label>` (Atom)
*   Ein `<input>`-Feld (Atom)
*   Ein `<button>` (Atom)

Einzeln sind sie nur Elemente. Zusammen bilden sie das "Suchformular"-Molekül – eine kleine, wiederverwendbare Komponente mit einer einzigen, klaren Funktion: dem Benutzer die Möglichkeit zu geben, eine Suche zu starten.

```html
<!-- Ein Molekül: Ein Suchformular -->
<div class="search-form">
  <label class="search-form-label" for="search-input">Suche</label>
  <input class="form-input" id="search-input" type="search" placeholder="Website durchsuchen...">
  <button class="btn btn-primary">Suchen</button>
</div>
```

Das Schöne an diesem Molekül ist, dass du es nun überall auf deiner Website einsetzen kannst, wo eine Suchfunktion benötigt wird – im Header, in der Seitenleiste, auf einer 404-Seite. Du musst die Struktur nicht jedes Mal neu erfinden. Du hast ein verlässliches, wiederverwendbares Muster geschaffen. Andere Beispiele für Moleküle sind eine einzelne Navigationsverknüpfung mit Icon und Text oder ein Bild-Upload-Feld mit Vorschau.

#### Die dritte Ebene: Organismen

Organismen sind die nächste Stufe der Komplexität. Sie sind Baugruppen aus Molekülen und/oder Atomen, die zusammen einen größeren, eigenständigen Teil einer Benutzeroberfläche bilden. Organismen sind oft die Hauptbestandteile einer Seite.

Ein gutes Beispiel für einen Organismus ist der Kopfbereich (Header) einer Website. Ein Header besteht typischerweise aus mehreren Molekülen und Atomen:

*   Ein Logo (ein `<img>`-Atom, vielleicht in einem `<a>`-Tag)
*   Das Hauptnavigationsmenü (ein Molekül, das aus mehreren Link-Atomen in einer Liste besteht)
*   Das Suchformular (unser Molekül von oben)

```html
<!-- Ein Organismus: Der Seitenkopf (Header) -->
<header class="site-header">
  <a href="/" class="site-logo">
    <img src="logo.svg" alt="Firmenlogo">
  </a>
  
  <nav class="main-navigation">
    <ul>
      <li><a href="/produkte">Produkte</a></li>
      <li><a href="/ueber-uns">Über uns</a></li>
      <li><a href="/kontakt">Kontakt</a></li>
    </ul>
  </nav>
  
  <div class="search-form">
    <!-- Hier wird unser Suchformular-Molekül wiederverwendet -->
    <label class="search-form-label" for="search-input-header">Suche</label>
    <input class="form-input" id="search-input-header" type="search" placeholder="Website durchsuchen...">
    <button class="btn btn-primary">Suchen</button>
  </div>
</header>
```

Dieser Header-Organismus ist eine relativ komplexe, aber in sich geschlossene und wiederverwendbare Einheit. Du kannst ihn auf jeder einzelnen Seite deiner Website platzieren und sicher sein, dass er immer gleich strukturiert ist und die gleichen Kernkomponenten enthält. Andere Organismen könnten ein Produktkarten-Raster, ein Blogpost-Teaser oder ein komplexer Footer sein.

#### Die vierte Ebene: Templates

Templates sind der Punkt, an dem wir unsere Komponenten zu einem Seitenlayout zusammenfügen. Ein Template ist im Wesentlichen der Bauplan einer Seite, aber noch ohne den spezifischen, finalen Inhalt. Es definiert die Struktur und die Anordnung der Organismen. Man könnte es als eine High-Fidelity-Version eines Wireframes bezeichnen.

Ein Template für eine Blog-Artikelseite könnte beispielsweise so aussehen:

*   Oben: Der "Header"-Organismus.
*   Darunter im Hauptbereich: Ein Platzhalter für den "Artikel-Inhalt"-Organismus (Überschrift, Metadaten, Fließtext).
*   Rechts daneben: Ein Platzhalter für den "Seitenleisten"-Organismus (der vielleicht aus einem "Autorenprofil"-Molekül und einer "Kategorienliste"-Molekül besteht).
*   Unten: Der "Footer"-Organismus.

Die HTML-Struktur eines Templates konzentriert sich auf das Layout und die Platzierung der Komponenten.

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <title>Seitentitel-Platzhalter</title>
  <!-- Metadaten, CSS-Verknüpfungen etc. -->
</head>
<body>

  <!-- Header-Organismus hier einfügen -->
  <header class="site-header">
    ...
  </header>

  <main class="content-area">
    <article class="blog-post">
      <h1>Platzhalter für Artikelüberschrift</h1>
      <p class="meta-data">Veröffentlicht am [Datum] von [Autor]</p>
      <div class="post-content">
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
        <p>Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
      </div>
    </article>
  </main>

  <aside class="sidebar">
    <!-- Autorenprofil-Molekül hier einfügen -->
    <!-- Kategorienliste-Molekül hier einfügen -->
  </aside>

  <!-- Footer-Organismus hier einfügen -->
  <footer class="site-footer">
    ...
  </footer>

</body>
</html>
```
Der entscheidende Punkt bei Templates ist, dass sie sich auf die zugrundeliegende Inhaltsstruktur konzentrieren, nicht auf den tatsächlichen Inhalt. Sie helfen dir, die Beziehung zwischen deinen Organismen und Molekülen in einem realistischen Kontext zu sehen und sicherzustellen, dass dein Designsystem flexibel genug ist.

#### Die fünfte Ebene: Seiten

Die letzte Ebene ist die konkreteste: die Seite. Eine Seite ist eine spezifische Instanz eines Templates, die mit echtem, realem Inhalt gefüllt ist. Hier ersetzt du die Platzhaltertexte und -bilder durch finale Inhalte.

Auf dieser Ebene wird dein System auf die Probe gestellt. Was passiert, wenn eine Artikelüberschrift extrem lang ist? Wie sieht die Produktkarte aus, wenn der Produktname nur aus einem Wort besteht? Was geschieht, wenn ein Benutzer kein Profilbild hochgeladen hat?

Die Seitenebene ist der Realitätscheck für dein Komponentensystem. Sie zeigt dir, ob die Atome, Moleküle und Organismen, die du so sorgfältig geplant hast, auch in der unvorhersehbaren Welt echten Contents robust und flexibel sind. Es gibt hier keine neue HTML-Struktur zu schreiben; es ist die Anwendung deines Templates mit echten Daten.

#### Warum diese Planung Gold wert ist

Wenn du beginnst, in diesen Ebenen zu denken, verändert sich deine Herangehensweise an die HTML-Strukturierung fundamental.

1.  **Konsistenz:** Da du immer wieder dieselben Bausteine (Atome, Moleküle) verwendest, um größere Einheiten (Organismen) zu bauen, wird deine Benutzeroberfläche von Natur aus konsistent. Ein Button sieht überall wie ein Button aus und verhält sich auch so.
2.  **Effizienz und Geschwindigkeit:** Du musst das Rad nicht ständig neu erfinden. Sobald du ein "Suchformular"-Molekül definiert hast, kannst du es in Sekunden überall einfügen, anstatt es jedes Mal von Grund auf neu zu schreiben. Das beschleunigt die Entwicklung enorm.
3.  **Einfache Wartung:** Stell dir vor, du musst das Design aller primären Buttons auf deiner Website ändern. In einem traditionellen Projekt müsstest du Dutzende von CSS-Regeln anpassen oder jede Seite durchsuchen. Im Atomic Design gehst du zu deinem Button-Atom, änderst es an einer einzigen Stelle, und die Änderung wird automatisch überall dort wirksam, wo dieses Atom verwendet wird.
4.  **Klarheit und Kommunikation:** Dieses System schafft eine gemeinsame Sprache für Designer und Entwickler. Wenn ein Designer von einem "Produktkarten-Organismus" spricht, weiß der Entwickler genau, welche HTML-Struktur und welche Unterkomponenten gemeint sind.

Das Planen von Wiederverwendbarkeit ist keine zusätzliche Arbeit, die du dir machst. Es ist eine Investition, die sich über den gesamten Lebenszyklus eines Projekts auszahlt. Es zwingt dich, von Anfang an über Struktur, Hierarchie und Systematik nachzudenken. Dein HTML wird dadurch nicht nur sauberer und semantischer, sondern du schaffst ein flexibles, skalierbares und zukunftssicheres Fundament für jede Weboberfläche, die du baust.
