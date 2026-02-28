# Hierarchie der Inhalte

### Hierarchie der Inhalte

Stell dir vor, du schlägst ein Sachbuch auf. Was siehst du als Erstes? Wahrscheinlich einen großen, markanten Titel. Dann folgst du mit den Augen dem Inhaltsverzeichnis, das dir die Kapitelüberschriften zeigt. Innerhalb eines Kapitels findest du Unterüberschriften, die dir helfen, die Abschnitte schnell zu erfassen und zu dem Punkt zu springen, der dich am meisten interessiert. Diese klare, logische Gliederung macht das Buch lesbar und verständlich.

Genau dieses Prinzip überträgst du mit HTML auf deine Webseite. Eine gut durchdachte Inhaltshierarchie ist das Rückgrat jeder erfolgreichen Seite. Sie schafft nicht nur visuelle Ordnung, sondern gibt dem Inhalt eine logische und semantische Struktur. Diese Struktur ist nicht nur für deine menschlichen Besucher entscheidend, sondern auch für die Maschinen, die deine Seite analysieren – allen voran Suchmaschinen und Screenreader für Menschen mit Sehbehinderungen.

#### Die Werkzeuge der Gliederung: Überschriften-Elemente

Dein wichtigstes Werkzeug für die Gliederung von Inhalten sind die Überschriften-Elemente: `<h1>` bis `<h6>`. Jedes dieser Tags repräsentiert eine Ebene in der Hierarchie deiner Seite.

*   `<h1>`: Dies ist die Hauptüberschrift deiner Seite. Sie sollte den übergeordneten Inhalt der gesamten Seite zusammenfassen, vergleichbar mit dem Buchtitel.
*   `<h2>`: Dies sind die Hauptabschnitte deiner Seite, vergleichbar mit den Kapiteln eines Buches.
*   `<h3>`: Dies sind Unterabschnitte innerhalb eines `<h2>`-Blocks.
*   `<h4>`, `<h5>`, `<h6>`: Diese Elemente gliedern den Inhalt noch feiner, für immer spezifischere Unterthemen.

Die Zahl in der Überschrift (`h1`, `h2`, etc.) steht also nicht für die Schriftgröße, sondern für die Wichtigkeit und die Ebene in der Gliederung. `<h1>` ist die höchste und wichtigste Ebene, `<h6>` die niedrigste.

#### Die goldenen Regeln der Überschriften-Hierarchie

Um eine saubere und verständliche Struktur zu schaffen, solltest du zwei fundamentale Regeln befolgen:

**1. Es gibt nur einen Chef: Verwende nur ein `<h1>`-Element pro Seite.**

Deine Seite sollte ein klares, unmissverständliches Hauptthema haben. Das `<h1>`-Element kommuniziert genau dieses Thema. Mehrere `<h1>`-Tags auf einer Seite wären so, als hätte ein Buch mehrere Titel – es stiftet Verwirrung bei Suchmaschinen und Nutzern von assistiven Technologien. Dein `<h1>` sollte prägnant den Inhalt der Seite beschreiben und idealerweise am Anfang deines Hauptinhalts (`<main>`) stehen.

**2. Überspringe keine Ebenen.**

Die Hierarchie muss lückenlos sein. Nach einer `<h2>`-Überschrift kann eine `<h3>` folgen, aber niemals direkt eine `<h4>`. Ein Sprung von `<h2>` auf `<h4>` würde bedeuten, dass du eine logische Gliederungsebene auslässt. Das ist so, als würdest du in einem Buch von Kapitel 2 direkt zu Unter-Unterpunkt 2.1.1 springen, ohne den übergeordneten Abschnitt 2.1 zu benennen.

Schauen wir uns eine korrekte Struktur an:

```html
<body>
  <header>
    <!-- Header-Inhalt wie Logo und Navigation -->
  </header>
  <main>
    <h1>Die Kunst des Brotbackens</h1>
    <p>Eine Einführung in die Grundlagen für Anfänger.</p>

    <h2>1. Die Zutaten: Qualität ist entscheidend</h2>
    <p>Alles beginnt mit den richtigen Rohstoffen...</p>
      <h3>1.1 Das richtige Mehl wählen</h3>
      <p>Weizen, Roggen oder Dinkel? Jedes Mehl hat seine Eigenheiten...</p>
      <h3>1.2 Hefe, Sauerteig und andere Triebmittel</h3>
      <p>Was lässt deinen Teig aufgehen?</p>

    <h2>2. Der Prozess: Vom Kneten zum fertigen Laib</h2>
    <p>Geduld und Technik sind der Schlüssel zum Erfolg.</p>
      <h3>2.1 Der Teig: Richtig kneten und ruhen lassen</h3>
      <p>Hier trennt sich die Spreu vom Weizen...</p>
      <h3>2.2 Das Backen: Temperatur und Timing</h3>
      <p>Der letzte, aber entscheidende Schritt...</p>
  </main>
  <footer>
    <!-- Footer-Inhalt -->
  </footer>
</body>
```

Diese Struktur ist logisch, nachvollziehbar und leicht zu analysieren – sowohl für das menschliche Auge als auch für eine Maschine.

#### Der häufigste Fehler: Überschriften für Styling missbrauchen

Ein weitverbreitetes Missverständnis ist, Überschriften-Tags zu verwenden, um Text optisch hervorzuheben. Du denkst vielleicht: "Dieser Text soll groß und fett sein, also nehme ich ein `<h3>`-Tag." Das ist semantisch falsch und ein fundamentaler Fehler im Verständnis von HTML und CSS.

*   **HTML ist für die Bedeutung (Semantik).**
*   **CSS ist für das Aussehen (Präsentation).**

Wenn du einen Text nur aus visuellen Gründen formatieren möchtest, aber dieser Text keine Überschrift für einen nachfolgenden Abschnitt ist, dann verwende ein neutrales Element wie `<p>` oder `<span>` und weise ihm über CSS eine Klasse zu.

**Falsch:**
```html
<h2>Unsere Angebote</h2>
<p>Wir haben tolle Produkte für dich.</p>
<h3>Nur diese Woche 20% Rabatt!</h3> <!-- Falsch! Das ist keine Unterüberschrift, sondern eine Werbeaussage. -->
```

**Richtig:**
```html
<h2>Unsere Angebote</h2>
<p>Wir haben tolle Produkte für dich.</p>
<p class="angebot-hervorhebung">Nur diese Woche 20% Rabatt!</p>
```
In deiner CSS-Datei könntest du dann die Klasse `.angebot-hervorhebung` nach Belieben gestalten, zum Beispiel mit einer größeren Schriftart und einer anderen Farbe, ohne die semantische Struktur deines Dokuments zu zerstören.

#### Warum die Hierarchie so wichtig ist

Eine saubere Inhaltshierarchie ist kein Selbstzweck. Sie hat handfeste Vorteile in zwei entscheidenden Bereichen: Suchmaschinenoptimierung (SEO) und Barrierefreiheit (Accessibility).

**1. Suchmaschinenoptimierung (SEO)**
Suchmaschinen wie Google durchsuchen deine Webseite nicht wie ein Mensch. Ihre "Crawler" analysieren den Code, um den Inhalt und Kontext zu verstehen. Die Überschriften-Struktur ist dabei wie ein Inhaltsverzeichnis, das dem Crawler sagt: "Das ist das Hauptthema (`<h1>`), das sind die wichtigsten Unterthemen (`<h2>`), und hier geht es weiter ins Detail (`<h3>`)". Eine logische Hierarchie hilft der Suchmaschine, deine Seite besser zu verstehen, zu indizieren und für relevante Suchanfragen als passend einzustufen. Keywords, die in Überschriften platziert sind, haben oft ein höheres Gewicht.

**2. Barrierefreiheit (Accessibility)**
Für Menschen, die auf assistive Technologien wie Screenreader angewiesen sind, ist eine gute Überschriften-Struktur überlebenswichtig. Ein Screenreader-Nutzer "scannt" eine Seite nicht visuell. Stattdessen lässt er sich oft zuerst alle Überschriften vorlesen, um einen schnellen Überblick zu bekommen. Mit einem einfachen Tastaturbefehl kann er dann direkt zu der Überschrift (und dem damit beginnenden Abschnitt) springen, die ihn interessiert.

Wenn du Überschriften-Tags überspringst oder sie für rein visuelle Zwecke missbrauchst, zerstörst du diese Navigationsmöglichkeit. Eine Seite ohne logische Überschriften ist wie ein Buch ohne Kapitel – ein unstrukturierter, langer Textblock, durch den man sich mühsam von Anfang bis Ende durchkämpfen muss.

#### Zusammenspiel mit semantischen Layout-Elementen

Deine Überschriften-Hierarchie existiert nicht im luftleeren Raum. Sie spielt perfekt mit den semantischen Layout-Elementen zusammen, die du bereits kennengelernt hast, wie `<section>`, `<article>` und `<aside>`.

Eine bewährte Praxis ist es, jeden eigenständigen Inhaltsblock, wie zum Beispiel eine `<section>` oder einen `<article>`, mit einer passenden Überschrift beginnen zu lassen. Die Überschrift fungiert dann als Titel für genau diesen Block.

Betrachten wir eine komplexere Seitenstruktur:

```html
<body>
  <header>
    <h1>Mein Blog über Webentwicklung</h1>
    <nav>...</nav>
  </header>

  <main>
    <article>
      <h2>HTML-Struktur: Das Fundament jeder Webseite</h2>
      <p>Einleitung in den Artikel...</p>

      <section>
        <h3>Die Bedeutung der Semantik</h3>
        <p>Text über semantische Elemente...</p>
      </section>

      <section>
        <h3>Die Hierarchie der Inhalte</h3>
        <p>Genau das, was du gerade liest...</p>
      </section>
    </article>

    <aside>
      <h2>Verwandte Artikel</h2>
      <ul>
        <li><a href="#">Einführung in CSS</a></li>
        <li><a href="#">Grundlagen von JavaScript</a></li>
      </ul>
    </aside>
  </main>

  <footer>
    <p>&copy; 2023 Mein Blog</p>
  </footer>
</body>
```

In diesem Beispiel siehst du klar die Gliederung:
*   Das `<h1>` im `<header>` (oder am Anfang von `<main>`) gibt den Titel der gesamten Seite an.
*   Das `<article>` als in sich geschlossener Beitrag hat ein `<h2>` als Titel.
*   Die `<section>`-Elemente innerhalb des Artikels, die thematische Untergruppen bilden, werden jeweils mit einem `<h3>` eingeleitet.
*   Das `<aside>` für den Seiteninhalt hat ebenfalls ein eigenes `<h2>`, da es auf derselben hierarchischen Ebene wie der Hauptartikel steht, aber einen anderen Themenbereich abdeckt.

Indem du deine Inhalte so gewissenhaft strukturierst, baust du nicht nur eine Webseite. Du schaffst eine durchdachte, logische und für alle zugängliche Informationsarchitektur. Diese Sorgfalt ist ein Kennzeichen von professioneller Webentwicklung und die Grundlage für eine positive Nutzererfahrung.
