# Best Practices für Code-Dokumentation

### Die Kunst der guten Dokumentation: Kommentare und Whitespace als deine Verbündeten

Stell dir vor, du findest ein altes Notizbuch von dir wieder. Die Schrift ist krakelig, die Sätze sind wirr aneinandergereiht und es gibt keinerlei Absätze. Obwohl du es selbst geschrieben hast, fällt es dir schwer, den Gedankengängen von damals zu folgen. Ganz ähnlich kann es dir mit deinem eigenen Code ergehen. Was heute glasklar erscheint, kann in sechs Monaten ein undurchdringliches Rätsel sein.

Genau hier kommt die Code-Dokumentation ins Spiel. Und damit ist nicht nur ein separates Word-Dokument gemeint, das niemand liest. Die beste und direkteste Form der Dokumentation lebt direkt in deinem Code: in Form von Kommentaren und der bewussten Nutzung von Leerraum (Whitespace). Sie sind die Notizen an dein zukünftiges Ich und an deine Teamkollegen. Sie schaffen Klarheit, wo sonst Verwirrung herrschen würde, und verwandeln eine reine Ansammlung von Tags in eine verständliche, wartbare Struktur.

#### Kommentare – Deine Notizen für die Zukunft

In HTML schreibst du einen Kommentar, indem du ihn mit `<!--` beginnst und mit `-->` beendest. Alles, was dazwischen steht, wird vom Browser komplett ignoriert. Es ist unsichtbar für den Endnutzer, aber von unschätzbarem Wert für dich und andere Entwickler. Doch wie bei jedem Werkzeug kommt es darauf an, wie du es einsetzt.

##### Best Practice 1: Erkläre das „Warum“, nicht das „Was“

Ein häufiger Fehler von Anfängern ist es, das Offensichtliche zu kommentieren. Dein Code sollte so lesbar wie möglich sein und für sich selbst sprechen.

**Ein schlechtes Beispiel:**

```html
<!-- Dies ist eine Navigationsleiste -->
<nav>
  <ul>
    <!-- Ein Listeneintrag für die Startseite -->
    <li><a href="/">Startseite</a></li>
  </ul>
</nav>
```

Jeder, der HTML-Grundlagen kennt, sieht, dass `<nav>` eine Navigation ist und `<li>` ein Listeneintrag. Dieser Kommentar fügt keinen Wert hinzu, er ist nur Rauschen.

Ein guter Kommentar hingegen erklärt, warum eine bestimmte Entscheidung getroffen wurde, insbesondere wenn sie unkonventionell oder komplex ist. Er liefert den Kontext, den der Code allein nicht transportieren kann.

**Ein gutes Beispiel:**

```html
<!-- 
  Wir verwenden hier ein div anstelle eines button-Elements,
  da ein externes Styling-Framework das Styling von echten Buttons überschreibt.
  Die Button-Funktionalität wird per JavaScript hinzugefügt.
  Aria-Rollen stellen die Barrierefreiheit sicher.
-->
<div class="custom-button" role="button" tabindex="0">
  Klick mich
</div>
```

Dieser Kommentar ist Gold wert. Er verhindert, dass ein Kollege (oder du selbst in einem Jahr) diesen Code sieht und denkt: „Warum zum Teufel wurde hier kein `<button>` verwendet?“ Er bewahrt andere davor, den Code voreilig zu „korrigieren“ und dabei unbeabsichtigt etwas kaputtzumachen.

##### Best Practice 2: Markiere komplexe Abschnitte

Bei sehr langen oder verschachtelten HTML-Dokumenten kann es hilfreich sein, größere logische Blöcke zu markieren. Dies erleichtert das schnelle Scannen und Zurechtfinden in der Datei. Es ist, als würdest du Lesezeichen in ein dickes Buch legen.

```html
<!-- ========== Start: Haupt-Header Sektion ========== -->
<header class="site-header">
  <!-- ... hier folgt viel Code für Logo, Navigation, Suchfeld etc. ... -->
</header>
<!-- ========== Ende: Haupt-Header Sektion ========== -->

<main>
  <!-- ... -->
</main>
```

Diese Art von Kommentaren hilft, die grobe Struktur einer Seite auf einen Blick zu erfassen, ohne sich in den Details der einzelnen Tags zu verlieren.

##### Best Practice 3: Nutze TODOs und FIXMEs

Manchmal schreibst du Code, von dem du bereits weißt, dass er noch nicht fertig oder nicht perfekt ist. Anstatt diese Gedanken auf einem Zettel zu notieren, der verloren geht, kannst du sie direkt im Code hinterlassen. Dafür haben sich bestimmte Schlüsselwörter etabliert:

*   **`<!-- TODO: ... -->`**: Für eine Funktion, die noch implementiert werden muss.
*   **`<!-- FIXME: ... -->`**: Für ein bekanntes Problem, das behoben werden muss.

**Beispiel:**

```html
<div class="user-profile">
  <img src="placeholder.jpg" alt="Benutzerprofilbild">
  <!-- TODO: Dynamische Profilbilder aus der API laden, sobald der Endpunkt fertig ist. -->
</div>

<!-- FIXME: Das Layout bricht auf sehr kleinen Bildschirmen (< 320px). Braucht eine zusätzliche Media Query. -->
<section class="image-gallery">
  <!-- ... -->
</section>
```

Viele Code-Editoren und Entwicklungsumgebungen erkennen diese Schlüsselwörter und können dir eine Liste aller offenen TODOs und FIXMEs im gesamten Projekt anzeigen. So wird dein Code selbst zu einer Art Aufgabenliste.

##### Best Practice 4: Vermeide auskommentierten Code

Es ist verlockend: Du bist dir nicht sicher, ob du einen Code-Block noch brauchst, also kommentierst du ihn einfach aus, „für alle Fälle“. Widerstehe dieser Versuchung! Auskommentierter Code ist digitaler Müll. Er macht Dateien unübersichtlich und wirft Fragen auf:

*   Ist das veraltet?
*   Wird das noch gebraucht?
*   Warum wurde das auskommentiert?

Wenn du Code entfernst, aber die Möglichkeit haben möchtest, ihn wiederherzustellen, ist ein Versionskontrollsystem wie Git das richtige Werkzeug. Es ist wie eine Zeitmaschine für deinen Code – sauber, nachvollziehbar und es belastet nicht deine aktuellen Dateien. Lösche den Code also mutig. Git vergisst nichts.

#### Whitespace – Die stille Dokumentation

Mindestens genauso wichtig wie das, was du schreibst, ist das, was du *nicht* schreibst. Leerraum – also Einrückungen, Leerzeilen und Abstände – ist ein unglaublich mächtiges Werkzeug, um Struktur und Lesbarkeit zu schaffen. Der Browser ignoriert überflüssigen Whitespace im HTML-Code größtenteils, aber für das menschliche Auge ist er entscheidend.

##### Best Practice 1: Einrückung ist nicht optional

Einrückung ist die visuelle Darstellung der Hierarchie deines Dokuments. Jedes Mal, wenn ein Element in einem anderen verschachtelt wird, solltest du es eine Stufe weiter einrücken. Das macht die Eltern-Kind-Beziehungen sofort ersichtlich.

**Ein schlecht lesbares Beispiel ohne Einrückung:**

```html
<body>
<header>
<h1>Meine Webseite</h1>
<nav>
<ul>
<li><a href="#">Home</a></li>
<li><a href="#">Über uns</a></li>
</ul>
</nav>
</header>
<main>
<h2>Willkommen!</h2>
<p>Dies ist ein Text.</p>
</main>
</body>
```

Es ist fast unmöglich, hier auf den ersten Blick zu erkennen, was wozu gehört.

**Ein gut lesbares Beispiel mit korrekter Einrückung:**

```html
<body>
  <header>
    <h1>Meine Webseite</h1>
    <nav>
      <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">Über uns</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <h2>Willkommen!</h2>
    <p>Dies ist ein Text.</p>
  </main>
</body>
```

Hier siehst du sofort, dass `h1` und `nav` Kinder von `header` sind und `ul` ein Kind von `nav` ist. Die Struktur springt dir förmlich ins Auge.

##### Best Practice 2: Trenne logische Blöcke mit Leerzeilen

Genauso wie du Absätze in einem Text verwendest, um Gedankengänge zu trennen, solltest du Leerzeilen in deinem HTML-Code nutzen, um logische Blöcke voneinander abzugrenzen. Dies lockert den Code auf und verbessert die Lesbarkeit enorm.

Verwende eine Leerzeile, um große, eigenständige Komponenten wie den Header, den Hauptinhalt und den Footer voneinander zu trennen. Innerhalb dieser Komponenten kannst du ebenfalls kleinere, zusammengehörige Gruppen (wie ein Formular oder eine Artikelvorschau) durch eine Leerzeile vom Rest abheben.

**Ein Beispiel für gute vertikale Abstände:**

```html
<body>
  <header class="main-header">
    <a href="/" class="logo">MeinLogo</a>

    <nav class="main-nav">
      <ul>
        <li><a href="/produkte">Produkte</a></li>
        <li><a href="/kontakt">Kontakt</a></li>
      </ul>
    </nav>
  </header>

  <main class="content">
    <section class="hero-section">
      <h1>Das beste Produkt aller Zeiten</h1>
      <p>Kaufen Sie es jetzt und seien Sie glücklich.</p>
    </section>

    <section class="features">
      <h2>Unsere Features</h2>
      <!-- ... -->
    </section>
  </main>

  <footer class="main-footer">
    <p>&copy; 2023 Meine Firma</p>
  </footer>
</body>
```

Beachte, wie die Leerzeilen zwischen `header`, `main` und `footer` eine klare Trennung schaffen. Auch innerhalb des Headers trennt die Leerzeile das Logo von der Navigation, was ihre Zusammengehörigkeit, aber auch ihre Eigenständigkeit verdeutlicht.

##### Best Practice 3: Sei konsistent

Die wichtigste Regel bei der Verwendung von Whitespace ist Konsistenz. Entscheide dich (oder dein Team) für einen Stil und halte dich daran.

*   **Einrückung:** Verwendest du Tabs oder Spaces? Wenn Spaces, wie viele? (Zwei oder vier sind am gebräuchlichsten).
*   **Leerzeilen:** Wo genau setzt du Leerzeilen? Immer vor einem neuen großen Abschnitt?

Die genaue Wahl ist oft weniger wichtig als die Tatsache, dass sie im gesamten Projekt konsequent durchgehalten wird. Moderne Code-Editoren und Tools wie Prettier können dir dabei helfen, diese Regeln automatisch durchzusetzen, sodass du nicht ständig darüber nachdenken musst.

Indem du Kommentare und Whitespace bewusst und sorgfältig einsetzt, erhebst du deinen Code von einer reinen Anweisung für den Computer zu einem lesbaren, verständlichen und wartbaren Dokument für Menschen. Das ist keine lästige Pflicht, sondern ein Zeichen von Professionalität und Respekt – gegenüber deinen Kollegen und deinem zukünftigen Ich.
