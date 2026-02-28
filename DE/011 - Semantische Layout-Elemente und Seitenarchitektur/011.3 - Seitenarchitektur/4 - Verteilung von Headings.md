# Verteilung von Headings

### Die Hierarchie der Überschriften: Ordnung im Informationschaos

Stell dir vor, du schlägst ein Buch auf und es gäbe keine Kapitelüberschriften. Oder du liest eine Zeitung ohne Schlagzeilen, nur endlose Textblöcke. Es wäre fast unmöglich, dich zu orientieren, die wichtigsten Themen zu erfassen oder gezielt zu dem Abschnitt zu springen, der dich interessiert. Was im analogen Leben gilt, ist im digitalen Raum noch viel wichtiger. Auf einer Webseite sind Überschriften – die HTML-Headings – das Rückgrat deiner Inhalte. Sie sind weit mehr als nur groß und fett formatierter Text; sie sind das entscheidende Werkzeug, um eine logische und verständliche Seitenarchitektur zu schaffen.

#### Das Grundprinzip: Eine klare Hierarchie

HTML stellt dir für Überschriften sechs Ebenen zur Verfügung: `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>` und `<h6>`. Diese Elemente bilden eine strikte Hierarchie, die du unbedingt einhalten musst. Denk an sie wie an die Gliederung eines Dokuments:

*   `<h1>`: Der Haupttitel der gesamten Seite. Er beschreibt das übergeordnete Thema und sollte pro Seite nur **ein einziges Mal** vorkommen. Er ist die wichtigste Überschrift von allen.
*   `<h2>`: Die Hauptabschnitte deiner Seite. Sie gliedern den Inhalt, der unter dem `<h1>`-Titel steht.
*   `<h3>`: Unterabschnitte eines `<h2>`-Blocks. Sie verfeinern und detaillieren das Thema des übergeordneten Abschnitts.
*   `<h4>`, `<h5>`, `<h6>`: Weitere Unterteilungen, die immer seltener gebraucht werden, aber die gleiche logische Abfolge einhalten. Eine `<h4>` kann nur innerhalb eines `<h3>`-Abschnitts vorkommen und so weiter.

Die goldene Regel lautet: **Überspringe niemals eine Ebene.** Du darfst von einer `<h2>` nicht direkt zu einer `<h4>` springen. Eine solche Lücke in der Hierarchie zerstört die logische Struktur deines Dokuments. Es ist, als würdest du in einem Buch von Kapitel 2 direkt zu Unter-Unterpunkt 2.1.1 springen, ohne vorher Abschnitt 2.1 zu definieren.

Schauen wir uns ein korrektes Beispiel für die Struktur einer Blog-Artikelseite an:

```html
<body>
  <header>
    <!-- Navigation und Logo -->
  </header>
  
  <main>
    <article>
      <h1>Die Kunst des Brotbackens für Anfänger</h1>
      
      <p>Einführungstext über die Freude am selbstgebackenen Brot...</p>
      
      <h2>Was du an Ausrüstung wirklich brauchst</h2>
      <p>Liste der grundlegenden Werkzeuge wie Schüssel, Waage, etc.</p>
      
      <h3>Der Unterschied zwischen Trockenhefe und Frischhefe</h3>
      <p>Erklärung der Vor- und Nachteile beider Hefearten...</p>
      
      <h2>Dein erstes Rezept: Ein einfaches Weißbrot</h2>
      <p>Einleitung zum Rezept...</p>
      
      <h3>Zutatenliste</h3>
      <ul>
        <li>500g Mehl</li>
        <li>10g Salz</li>
        <!-- weitere Zutaten -->
      </ul>
      
      <h3>Schritt-für-Schritt-Anleitung</h3>
      <ol>
        <li>Mehl und Salz mischen...</li>
        <li>Hefe im Wasser auflösen...</li>
        <!-- weitere Schritte -->
      </ol>
      
      <h2>Häufige Fehler und wie du sie vermeidest</h2>
      <p>Tipps zu den typischen Stolpersteinen beim Brotbacken...</p>
    </article>
  </main>

  <footer>
    <!-- Fußzeileninformationen -->
  </footer>
</body>
```

Diese Struktur ist logisch und nachvollziehbar. Die `<h1>` definiert das Hauptthema. Die `<h2>`-Elemente gliedern den Artikel in die drei Hauptabschnitte: Ausrüstung, Rezept und Fehlervermeidung. Innerhalb dieser Abschnitte schaffen die `<h3>`-Elemente weitere, feinere Unterteilungen.

Hier ist im Kontrast dazu ein Beispiel, wie du es **nicht** machen solltest:

```html
<!-- FALSCHES BEISPIEL! -->
<body>
  <h1>Die Kunst des Brotbackens</h1>
  
  <h4>Was du an Ausrüstung brauchst</h4> <!-- Falsch! Ebene übersprungen -->
  <p>Text zur Ausrüstung...</p>
  
  <h2>Dein erstes Rezept</h2>
  
  <h1>Ein einfaches Weißbrot</h1> <!-- Falsch! Zweite h1 auf der Seite -->
  
  <h3>Zutatenliste</h3> <!-- Falsch! h3 kann nicht direkt auf h1 folgen, wenn h2 existiert -->
  
  <h5>Schritt-für-Schritt-Anleitung</h5> <!-- Falsch! Ebenen übersprungen -->
</body>
```

Diese Struktur ist chaotisch. Sie ist für Maschinen (wie Suchmaschinen-Crawler und Screenreader) und auch für Menschen, die versuchen, den Code zu verstehen, völlig unlogisch.

#### Warum diese Struktur so entscheidend ist

Eine saubere Überschriftenhierarchie zu pflegen, ist keine akademische Übung. Sie hat drei ganz konkrete und wichtige Vorteile:

**1. Barrierefreiheit (Accessibility)**

Für Menschen, die auf assistierende Technologien wie Screenreader angewiesen sind, sind Überschriften das wichtigste Navigationsinstrument auf einer Webseite. Ein Screenreader-Nutzer liest eine Seite selten von Anfang bis Ende. Stattdessen lässt er sich oft zuerst alle Überschriften vorlesen, um einen Überblick über den Inhalt zu bekommen. Anhand dieser Gliederung kann er dann direkt zu dem Abschnitt springen, der für ihn relevant ist.

Wenn du Ebenen überspringst oder Überschriften nicht-semantisch (also nur wegen ihres Aussehens) verwendest, machst du diese Navigationsfunktion unbrauchbar. Eine korrekte Hierarchie ist die Landkarte, die du diesen Nutzern zur Verfügung stellst. Ohne sie sind sie in deinen Inhalten verloren.

**2. Suchmaschinenoptimierung (SEO)**

Suchmaschinen wie Google analysieren deine Überschriften, um die thematische Relevanz und Struktur deiner Seite zu verstehen. Die `<h1>` signalisiert das Hauptkeyword oder das zentrale Thema der Seite. Die `<h2>`-Überschriften teilen der Suchmaschine mit, welche Unterthemen behandelt werden.

Eine logische Gliederung hilft Google dabei, deine Inhalte besser zu indexieren und zu verstehen. Dies kann sich positiv auf dein Ranking auswirken, da die Suchmaschine deine Seite als gut strukturiert und thematisch fokussiert einstuft. Eine Seite mit einer sauberen Überschriftenstruktur wird tendenziell als qualitativ hochwertiger bewertet als eine ohne.

**3. Wartbarkeit und Lesbarkeit des Codes**

Auch für dich und andere Entwickler ist eine saubere Struktur von unschätzbarem Wert. Wenn du nach Monaten auf deinen Code zurückblickst, erkennst du anhand der Überschriftenhierarchie sofort die Gliederung der Seite, ohne dich durch unzählige `<div>`-Container wühlen zu müssen. Semantischer Code ist selbsterklärend und macht die Zusammenarbeit im Team und die zukünftige Pflege der Webseite wesentlich einfacher.

#### Der häufigste Fehler: Styling mit Headings

Ein Fehler, der besonders bei Anfängern weit verbreitet ist, ist die Auswahl von Überschriften-Tags basierend auf ihrem visuellen Erscheinungsbild im Browser. Du denkst vielleicht: "Ich brauche hier einen etwas kleineren Text als meine `<h2>`, also nehme ich eine `<h4>`." Das ist grundlegend falsch.

Die Semantik (also die Bedeutung) muss immer Vorrang vor dem Aussehen haben. Die Aufgabe von HTML ist es, die Struktur und Bedeutung deines Inhalts zu definieren. Die Aufgabe von CSS ist es, das Aussehen zu gestalten.

Wenn eine Überschrift logisch eine `<h2>` sein sollte, du sie aber kleiner haben möchtest, dann verwende das `<h2>`-Tag und passe seine Größe mit CSS an.

**HTML (Die Struktur):**

```html
<article>
  <h1>Großer Titel</h1>
  <h2>Ein wichtiger Abschnitt</h2>
  <p>Dieser Abschnitt ist von zentraler Bedeutung.</p>
  
  <!-- Dieser Abschnitt ist logisch gleichwertig zum ersten, soll aber anders aussehen. -->
  <h2 class="special-look">Ein weiterer wichtiger Abschnitt</h2>
  <p>Trotz seines anderen Aussehens ist er strukturell eine h2.</p>
</article>
```

**CSS (Das Aussehen):**

```css
h2 {
  font-size: 2em;
  color: #333;
  border-bottom: 2px solid #ccc;
}

/* Wir stylen die spezielle h2 über eine Klasse, ohne die Semantik zu ändern */
h2.special-look {
  font-size: 1.5em; /* Kleiner als die Standard-h2 */
  color: #555;
  border-bottom: none;
  font-style: italic;
}
```

Durch diesen Ansatz trennst du Struktur und Präsentation sauber voneinander. Deine HTML-Datei bleibt logisch korrekt und zugänglich, während du mit CSS die volle gestalterische Freiheit behältst. Denke immer daran: Deine Überschriftenstruktur ist das Fundament deiner Seite. Wenn dieses Fundament wackelig ist, wird das gesamte Gebäude instabil – sowohl für Maschinen als auch für Menschen.
