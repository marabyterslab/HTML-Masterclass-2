# Semantische Strukturierung

### Semantische Strukturierung: Die unsichtbare Logik deiner Webseite

Stell dir vor, du schreibst einen Text in einem einfachen Editor. Du möchtest die Hauptüberschrift hervorheben. Was tust du? Wahrscheinlich markierst du den Text und wählst die größte verfügbare Schriftgröße und vielleicht noch Fettdruck. Visuell hast du dein Ziel erreicht: Die Überschrift ist groß, dominant und sticht aus dem Rest des Textes heraus.

Wenn du eine Webseite mit HTML erstellst, könntest du versucht sein, ähnlich vorzugehen. Du könntest einen normalen Absatz-Tag (`<p>`) verwenden und ihm mit CSS eine große Schriftgröße und fette Schrift zuweisen. Das Ergebnis auf dem Bildschirm wäre identisch mit dem einer echten `<h1>`-Überschrift. Doch unter der Haube gibt es einen fundamentalen Unterschied – einen Unterschied, der über Gelingen oder Scheitern deiner Webseite entscheiden kann. Dieser Unterschied heißt Semantik.

#### Was bedeutet „semantisch“ überhaupt?

Semantik ist die Lehre von der Bedeutung. Im Kontext von HTML bedeutet semantische Strukturierung, dass du HTML-Tags nicht danach auswählst, wie sie aussehen, sondern danach, was sie *bedeuten*. Jeder HTML-Tag hat eine ihm zugewiesene, standardisierte Bedeutung.

*   Ein `<p>`-Tag bedeutet: „Dieser Inhalt ist ein Textabsatz.“
*   Ein `<h1>`-Tag bedeutet: „Dieser Inhalt ist die wichtigste Überschrift auf dieser Seite.“
*   Ein `<li>`-Tag bedeutet: „Dieser Inhalt ist ein Element in einer Liste.“

Wenn du also ein `<h1>` verwendest, gibst du dem Browser und anderen Maschinen ein klares Signal über die *Funktion* und *Wichtigkeit* dieses Textstücks. Du sagst nicht nur „Mach diesen Text groß“, sondern du sagst „Dieser Text ist die Kernaussage, der Titel des gesamten folgenden Inhalts.“

Wenn du hingegen einen `<p>`-Tag nimmst und ihn nur visuell aufbläst, ist seine Bedeutung für eine Maschine immer noch „ein einfacher Absatz“. Die visuelle Darstellung und die semantische Bedeutung klaffen auseinander. Dies führt zu Problemen, die auf den ersten Blick nicht sichtbar sind.

#### Warum das Ganze? Die drei Säulen der semantischen Struktur

Eine korrekte semantische Struktur ist kein Selbstzweck für pedantische Entwickler. Sie ist das Fundament einer professionellen, zugänglichen und erfolgreichen Webseite. Die Vorteile lassen sich in drei Hauptbereiche unterteilen.

**1. Für Suchmaschinen (SEO)**

Suchmaschinen wie Google, Bing oder DuckDuckGo sind im Grunde genommen blinde, aber extrem intelligente Leser. Sie können deine Webseite nicht „sehen“, wie ein Mensch es tut. Sie können keine Farben, Layouts oder Schriftgrößen interpretieren, um die Wichtigkeit von Inhalten zu beurteilen. Stattdessen analysieren sie den Code deiner Seite – dein HTML.

Die Überschriften-Hierarchie (`<h1>` bis `<h6>`) ist für eine Suchmaschine wie das Inhaltsverzeichnis eines Buches.
*   Das `<h1>`-Element ist der Buchtitel. Es sagt Google unmissverständlich, was das Hauptthema dieser einen Seite ist.
*   Die `<h2>`-Elemente sind die Kapitelüberschriften. Sie gliedern das Hauptthema in seine wichtigsten Unterbereiche.
*   Die `<h3>`-Elemente sind die Unterkapitel, die die `<h2>`-Themen weiter aufschlüsseln.

Eine saubere, logische Hierarchie erlaubt es der Suchmaschine, den Inhalt deiner Seite blitzschnell zu verstehen, zu kategorisieren und seine Relevanz für eine bestimmte Suchanfrage zu bewerten. Eine Seite mit einer klaren Struktur wird in den Suchergebnissen tendenziell besser platziert als eine Seite, die nur aus einem Brei von `<div>`- und `<p>`-Tags besteht, die irgendwie gestylt wurden.

**2. Für Menschen mit Hilfstechnologien (Barrierefreiheit)**

Dies ist vielleicht der wichtigste und oft am meisten vernachlässigte Aspekt. Nicht alle Menschen surfen im Internet, indem sie eine Maus über einen Bildschirm bewegen. Blinde oder stark sehbehinderte Nutzer verwenden sogenannte Screenreader – eine Software, die den Inhalt einer Webseite vorliest.

Wie navigiert ein Screenreader-Nutzer auf einer langen Seite, um schnell zum gewünschten Abschnitt zu gelangen? Er lässt sich nicht die ganze Seite von oben nach unten vorlesen. Stattdessen nutzen die meisten die Funktion, von Überschrift zu Überschrift zu springen. Der Screenreader listet alle `<h1>`-, `<h2>`-, `<h3>`-Überschriften auf, und der Nutzer kann direkt zu dem Thema springen, das ihn interessiert.

Wenn du deine Überschriften nicht mit den korrekten Tags (`<h1>` bis `<h6>`), sondern mit visuell gestylten `<p>`-Tags umsetzt, ist dieses Inhaltsverzeichnis für den Screenreader leer. Die Seite erscheint als eine unstrukturierte Wand aus Text. Die Navigation wird zur Qual oder ist unmöglich. Eine korrekte semantische Struktur ist daher keine Option, sondern eine grundlegende Anforderung für eine inklusive und barrierefreie Webseite.

**3. Für dich und dein Team (Wartbarkeit)**

Stell dir vor, du kommst nach sechs Monaten zu deinem eigenen Projekt zurück oder übernimmst den Code von jemand anderem. Wenn die HTML-Struktur semantisch korrekt ist, kannst du den Code lesen und sofort die logische Gliederung des Inhalts verstehen, ohne die Seite im Browser überhaupt ansehen zu müssen.

```html
<!-- Leicht verständlich durch Semantik -->
<article>
  <h1>Die Kunst des Kaffeeröstens</h1>
  <p>Eine Einführung in die Grundlagen.</p>
  
  <h2>Die Auswahl der richtigen Bohne</h2>
  <p>Nicht jede Bohne ist gleich...</p>
  
  <h3>Arabica vs. Robusta</h3>
  <p>Die zwei Giganten der Kaffeewelt...</p>
  
  <h2>Der Röstprozess</h2>
  <p>Hier passiert die eigentliche Magie...</p>
</article>
```

Dieser Code ist selbsterklärend. Nun stell dir das Gegenteil vor:

```html
<!-- Schwer verständlich, da rein visuell gedacht -->
<div>
  <p class="main-title">Die Kunst des Kaffeeröstens</p>
  <p class="subtitle">Eine Einführung in die Grundlagen.</p>
  
  <p class="section-heading">Die Auswahl der richtigen Bohne</p>
  <p class="body-text">Nicht jede Bohne ist gleich...</p>
  
  <p class="subsection-heading">Arabica vs. Robusta</p>
  <p class="body-text">Die zwei Giganten der Kaffeewelt...</p>
  
  <p class="section-heading">Der Röstprozess</p>
  <p class="body-text">Hier passiert die eigentliche Magie...</p>
</div>
```

Um diesen zweiten Code zu verstehen, müsstest du erst in der CSS-Datei nachsehen, was `.main-title` oder `.section-heading` eigentlich bedeutet. Die Struktur ist nicht mehr aus dem HTML selbst ersichtlich. Dies macht die Wartung und Weiterentwicklung des Codes unnötig kompliziert und fehleranfällig.

#### Die goldenen Regeln der Überschriften-Hierarchie

Um eine saubere semantische Struktur zu gewährleisten, gibt es zwei einfache, aber unverrückbare Regeln für den Umgang mit Überschriften.

**Regel 1: Es gibt nur eine Nummer eins.**
Auf jeder einzelnen Seite sollte es genau ein `<h1>`-Element geben. Es ist der Haupttitel, die Essenz der Seite. Mehrere `<h1>`-Tags auf einer Seite sind so, als hätte ein Buch mehrere Titel – es stiftet Verwirrung bei Suchmaschinen und Nutzern von Hilfstechnologien.

**Regel 2: Überspringe keine Ebenen.**
Die Hierarchie der Überschriften muss logisch und lückenlos sein. Auf eine `<h1>` folgt eine `<h2>`. Auf eine `<h2>` kann entweder eine weitere `<h2>` (für das nächste Hauptkapitel) oder eine `<h3>` (für ein Unterkapitel) folgen. Du darfst aber niemals direkt von einer `<h2>` zu einer `<h4>` springen.

Stell es dir wieder wie ein Buch vor. Du kannst nicht von Kapitel 2 direkt zu Abschnitt 2.1.1 springen, ohne vorher Abschnitt 2.1 zu haben.

**Korrektes Beispiel:**

```html
<h1>Der ultimative Guide für Zimmerpflanzen</h1>
<p>Alles, was du für einen grünen Daumen wissen musst.</p>

  <h2>Die richtige Pflanze für dein Zuhause</h2>
  <p>Licht, Wasser und deine Lebensgewohnheiten spielen eine Rolle.</p>
  
    <h3>Pflanzen für sonnige Fenster</h3>
    <p>Sukkulenten, Kakteen und mehr...</p>
    
    <h3>Pflanzen für schattige Ecken</h3>
    <p>Farne, Efeututen und die Glücksfeder...</p>

  <h2>Pflege und Düngung</h2>
  <p>So bleiben deine grünen Freunde glücklich und gesund.</p>
  
    <h3>Wie oft sollte man gießen?</h3>
    <p>Ein häufiger Fehler ist das Übergießen...</p>
```

Die Struktur ist klar: 1 -> 2 -> 3 -> 3 -> 2 -> 3. Alles ist logisch und nachvollziehbar.

**Falsches Beispiel (übersprungene Ebene):**

```html
<h1>Der ultimative Guide für Zimmerpflanzen</h1>
<p>Alles, was du für einen grünen Daumen wissen musst.</p>

  <h2>Die richtige Pflanze für dein Zuhause</h2>
  <p>Licht, Wasser und deine Lebensgewohnheiten spielen eine Rolle.</p>
  
    <!-- FEHLER: Von h2 wird direkt auf h4 gesprungen -->
    <h4>Pflanzen für sonnige Fenster</h4>
    <p>Sukkulenten, Kakteen und mehr...</p>

  <h2>Pflege und Düngung</h2>
  <p>So bleiben deine grünen Freunde glücklich und gesund.</p>
```

Dieser Sprung von `<h2>` auf `<h4>` bricht die logische Kette. Ein Screenreader-Nutzer würde sich fragen, wo Ebene 3 geblieben ist. Eine Suchmaschine könnte die Struktur als fehlerhaft interpretieren. Der Grund für einen solchen Fehler ist fast immer, dass der Entwickler die `<h4>` nur wegen ihres Standard-Aussehens (z.B. kleinere Schrift) gewählt hat. Aber denk immer daran: Das Aussehen definierst du ausschließlich mit CSS. Die Bedeutung definierst du mit HTML.

Am Ende geht es bei semantischer Strukturierung um Klarheit und Absicht. Du baust nicht nur eine visuelle Fassade, sondern ein logisches, robustes und für alle verständliches Informationsgerüst. Diese Denkweise ist der Unterschied zwischen jemandem, der HTML-Tags anordnet, und jemandem, der das Web wirklich versteht und gestaltet.
