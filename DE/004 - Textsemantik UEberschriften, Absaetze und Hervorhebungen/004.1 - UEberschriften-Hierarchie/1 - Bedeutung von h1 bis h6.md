# Bedeutung von h1 bis h6

### Die Bedeutung von h1 bis h6: Mehr als nur große Buchstaben

Wenn du deine ersten Schritte in HTML machst, gehören die Überschriften-Tags – also `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>` und `<h6>` – zu den ersten Elementen, die du kennenlernst. Auf den ersten Blick scheint ihre Funktion offensichtlich: Sie machen Text größer und fetter. Die `<h1>` ist riesig, die `<h2>` etwas kleiner und so weiter, bis zur winzigen `<h6>`. Es ist eine der häufigsten Fehlannahmen, zu glauben, dass dies ihr einziger Zweck ist. In Wahrheit ist die visuelle Darstellung nur ein Nebeneffekt ihrer eigentlichen, viel wichtigeren Aufgabe: die Strukturierung deines Dokuments.

Die Überschriften-Tags sind das Fundament für die semantische Gliederung deiner Webseite. Semantik bedeutet hier, dass die Tags dem Inhalt eine Bedeutung geben. Sie sagen dem Browser, den Suchmaschinen und assistiven Technologien nicht nur, *wie* etwas aussehen soll, sondern *was* es ist. Eine `<h1>` ist nicht einfach nur "großer Text", sondern "die Hauptüberschrift dieser Seite".

#### Die Hierarchie – Das Inhaltsverzeichnis deiner Webseite

Stell dir vor, du schreibst kein HTML-Dokument, sondern ein Buch. Ein Buch hat einen Haupttitel, der das gesamte Werk beschreibt. Darunter gibt es Kapitel, die große Themenbereiche abdecken. Innerhalb dieser Kapitel findest du vielleicht Abschnitte und Unterabschnitte, die immer spezifischere Details behandeln.

Genau diese logische Gliederung bilden die HTML-Überschriften-Tags nach:

*   **`<h1>`**: Der Buchtitel. Dies ist die wichtigste Überschrift und sollte den gesamten Inhalt der Seite zusammenfassen. Auf einer einzelnen Seite sollte es idealerweise nur eine einzige `<h1>` geben.
*   **`<h2>`**: Die Kapitelüberschriften. Sie gliedern die Seite in ihre Hauptthemenbereiche.
*   **`<h3>`**: Die Unterkapitel oder Abschnitte innerhalb eines Kapitels. Sie unterteilen ein `<h2>`-Thema weiter.
*   **`<h4>`, `<h5>`, `<h6>`**: Noch feinere Untergliederungen. Sie folgen demselben Prinzip und schaffen immer tiefere Strukturebenen.

Diese Hierarchie ist nicht optional, sondern der Kern des Konzepts. Die Zahl in `h1` bis `h6` repräsentiert den Rang oder die Ebene der Überschrift, nicht ihre Schriftgröße. Eine `<h3>` ist immer eine Unterüberschrift einer `<h2>`, die wiederum eine Unterüberschrift einer `<h1>` ist. Diese Struktur bildet ein unsichtbares Inhaltsverzeichnis für deine Seite.

#### Warum eine korrekte Struktur entscheidend ist

Die Einhaltung dieser Hierarchie ist kein Selbstzweck. Sie hat handfeste, praktische Vorteile, die weit über eine ordentliche Codebasis hinausgehen. Drei Bereiche profitieren massiv von einer sauberen Überschriftenstruktur: Suchmaschinenoptimierung (SEO), Barrierefreiheit (Accessibility) und die Wartbarkeit deines Codes.

**1. Für Suchmaschinen (SEO)**

Suchmaschinen wie Google schicken kleine Programme, sogenannte Crawler oder Bots, durch das Internet, um den Inhalt von Webseiten zu analysieren und zu indexieren. Diese Crawler können keine Webseiten „sehen“, wie wir es tun. Stattdessen lesen sie den HTML-Code, um zu verstehen, worum es auf einer Seite geht.

Die Überschriften-Tags sind für sie wie Wegweiser. Die `<h1>` verrät dem Crawler: "Das ist das Hauptthema dieser Seite." Die `<h2>`-Tags geben ihm einen Überblick über die wichtigsten Unterthemen. Eine logische Struktur hilft der Suchmaschine, den Kontext und die Relevanz deiner Inhalte präzise zu erfassen. Eine gut strukturierte Seite hat oft bessere Chancen, für relevante Suchanfragen gut platziert zu werden, als eine Seite, die ihre Inhalte ohne klare Gliederung präsentiert.

**2. Für die Barrierefreiheit (Accessibility)**

Stell dir vor, du könntest eine Webseite nicht sehen und wärst auf ein Programm angewiesen, das dir den Inhalt vorliest – einen sogenannten Screenreader. Wie würdest du schnell herausfinden, welche Informationen die Seite enthält, ohne dir Wort für Wort alles vorlesen lassen zu müssen?

Hier kommt die Überschriften-Hierarchie ins Spiel. Screenreader bieten Nutzern die Möglichkeit, von Überschrift zu Überschrift zu springen. Ein Nutzer kann sich zuerst alle `<h2>`-Überschriften vorlesen lassen, um einen schnellen Überblick über die Hauptabschnitte der Seite zu bekommen. Hat er einen interessanten Abschnitt gefunden, kann er dorthin springen und sich nur diesen Teil im Detail vorlesen lassen.

Wenn du Überschriften nur aufgrund ihres Aussehens verwendest – zum Beispiel eine `<h4>` direkt nach einer `<h1>`, weil dir die Schriftgröße gefällt – zerstörst du diese Navigationsmöglichkeit. Für einen sehenden Benutzer mag das kaum auffallen, aber für jemanden, der auf einen Screenreader angewiesen ist, wird die Seite unübersichtlich und frustrierend. Eine korrekte semantische Struktur ist daher ein Grundpfeiler des barrierefreien Webdesigns.

**3. Für dich und dein CSS**

Eines der wichtigsten Prinzipien der modernen Webentwicklung ist die Trennung von Inhalt (HTML) und Darstellung (CSS). Indem du Überschriften semantisch korrekt verwendest, stärkst du diese Trennung.

Dein HTML-Code definiert die Struktur: "Dies ist eine Hauptüberschrift, dies sind Unterüberschriften." Dein CSS-Code definiert das Aussehen: "Alle Hauptüberschriften sollen blau und 48 Pixel groß sein, alle Unterüberschriften schwarz und 32 Pixel groß."

Wenn du später das Design deiner Seite ändern möchtest, musst du nur eine einzige Zeile in deiner CSS-Datei anpassen. Hättest du stattdessen `<p>`-Tags mit manuellen Stil-Anweisungen verwendet, um eine Überschrift zu simulieren, müsstest du jede einzelne Stelle in deinem HTML-Code finden und ändern. Eine saubere Struktur in HTML macht dein CSS einfacher, deinen Code wartbarer und deine Arbeit als Entwickler deutlich effizienter.

#### Die goldenen Regeln im Umgang mit Überschriften

Um sicherzustellen, dass du die Macht der Überschriften-Tags richtig nutzt, gibt es ein paar einfache, aber entscheidende Regeln.

**Regel 1: Es kann nur eine geben – Die `<h1>`**

Die `<h1>` ist der Titel deiner Seite. So wie ein Buch nur einen Haupttitel hat, sollte eine Webseite nur eine `<h1>` haben. Sie sollte den Inhalt der gesamten Seite prägnant zusammenfassen und ganz am Anfang deines Hauptinhalts stehen. Mehrere `<h1>`-Tags auf einer Seite können Suchmaschinen und Screenreader verwirren, da unklar wird, was das eigentliche Hauptthema ist.

**Regel 2: Überspringe keine Ebenen**

Die Hierarchie muss lückenlos sein. Springe niemals von einer `<h2>` direkt zu einer `<h4>`. Wenn du einen Abschnitt, der mit einer `<h2>` eingeleitet wird, weiter unterteilen möchtest, musst du eine `<h3>` verwenden. Erst wenn du einen `<h3>`-Abschnitt weiter unterteilst, kommt die `<h4>` zum Einsatz.

Falsch ist also eine Struktur wie `<h1>` → `<h2>` → `<h4>`.
Korrekt ist `<h1>` → `<h2>` → `<h3>` → `<h4>`.

Denk immer an das Buch-Beispiel: Du würdest auch kein Unter-Unterkapitel erstellen, ohne vorher ein Unterkapitel zu haben.

**Regel 3: Benutze Überschriften nur für Überschriften**

Es mag verlockend sein, ein `<h3>` oder `<h4>` zu verwenden, um einen kurzen Text hervorzuheben, weil die Standardformatierung zufällig passt. Widerstehe dieser Versuchung! Überschriften leiten einen neuen Inhaltsabschnitt ein. Wenn du nur ein Wort oder einen Satz betonen möchtest, ohne einen neuen Abschnitt zu beginnen, nutze dafür vorgesehene Tags wie `<strong>` für starke Wichtigkeit, `<em>` für Betonung oder ein `<span>`-Element, das du mit CSS gezielt formatierst.

#### Ein Blick auf die Praxis: Gut vs. Schlecht

Schauen wir uns zum Abschluss ein konkretes Beispiel an. Stell dir eine einfache Seite über die Zubereitung von Kaffee vor.

**Ein schlechtes Beispiel (semantisch falsch):**

Hier werden Überschriften für das Aussehen missbraucht, Ebenen übersprungen und es gibt keine klare Struktur.

```html
<!-- FALSCH: Semantisch nicht korrekt -->
<body>
  <p style="font-size: 32px; font-weight: bold;">Der perfekte Kaffee</p>
  <!-- Simuliert eine h1 mit einem Paragrafen -->
  
  <h3>Die Bohnen</h3>
  <!-- Springt direkt zu h3 -->
  <p>Die Wahl der richtigen Kaffeebohnen ist der erste Schritt...</p>
  
  <h3>Die Zubereitung</h3>
  <p>Es gibt viele Wege, Kaffee zuzubereiten...</p>
  
  <h6>Espresso</h6>
  <!-- Springt zu h6 für kleine Schrift -->
  <p>Der Espresso ist eine konzentrierte Form des Kaffees...</p>

  <h4>Filterkaffee</h4>
  <!-- Unlogische Reihenfolge (h6, dann h4) -->
  <p>Der klassische Filterkaffee ist weltweit beliebt...</p>
</body>
```

Diese Struktur ist für Maschinen und assistive Technologien ein reines Chaos. Es gibt keine `<h1>`, die Hierarchie ist lückenhaft und die Reihenfolge willkürlich.

**Ein gutes Beispiel (semantisch korrekt):**

Hier wird die Hierarchie sauber eingehalten. Die Tags beschreiben die Bedeutung des Inhalts, nicht sein Aussehen.

```html
<!-- RICHTIG: Semantisch korrekt und logisch strukturiert -->
<body>
  <h1>Die Kunst der Kaffeezubereitung</h1>
  <!-- Eine klare Hauptüberschrift für die ganze Seite -->
  
  <h2>Die Wahl der richtigen Bohne</h2>
  <!-- Ein Hauptkapitel -->
  <p>Die Grundlage für jeden guten Kaffee ist eine hochwertige Bohne. Achte auf Herkunft und Röstdatum...</p>
  
  <h2>Methoden der Zubereitung</h2>
  <!-- Das zweite Hauptkapitel -->
  <p>Je nach Methode entfaltet der Kaffee unterschiedliche Aromen. Hier sind die beliebtesten Varianten:</p>
  
  <h3>Espresso</h3>
  <!-- Ein Unterpunkt von "Methoden der Zubereitung" -->
  <p>Für einen Espresso wird heißes Wasser mit hohem Druck durch sehr fein gemahlenes Kaffeemehl gepresst...</p>
  
  <h3>Filterkaffee</h3>
  <!-- Ein weiterer, gleichrangiger Unterpunkt -->
  <p>Beim Filterkaffee wird heißes Wasser langsam über das Kaffeemehl gegossen und durch einen Filter extrahiert...</p>
  
  <h4>Der Handfilter</h4>
  <!-- Eine Unter-Unterrubrik, die zu Filterkaffee gehört -->
  <p>Eine besonders aromatische Variante ist die Zubereitung mit einem Handfilter aus Porzellan...</p>
</body>
```

Dieser zweite Code-Block ist ein Paradebeispiel für sauberes, semantisches HTML. Er ist für Menschen, Suchmaschinen und Screenreader gleichermaßen verständlich. Das Aussehen all dieser Überschriften kannst du nun zentral und flexibel in deinem CSS steuern. Du hast die Struktur von der Präsentation getrennt und damit den Grundstein für eine professionelle, zugängliche und wartbare Webseite gelegt.
