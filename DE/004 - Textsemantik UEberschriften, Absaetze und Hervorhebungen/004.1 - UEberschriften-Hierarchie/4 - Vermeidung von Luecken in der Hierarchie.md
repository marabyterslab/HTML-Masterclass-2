# Vermeidung von Lücken in der Hierarchie

### Die goldene Regel: Keine Lücken in der Überschriften-Hierarchie

Stell dir vor, du liest ein gut strukturiertes Buch. Es hat einen Haupttitel. Darunter folgen Kapitel. Jedes Kapitel kann in Abschnitte unterteilt sein, und diese Abschnitte vielleicht in noch kleinere Unterabschnitte. Diese Gliederung hilft dir, den roten Faden zu behalten und die Zusammenhänge zu verstehen. Du weißt immer, wo du dich befindest und welche Information zu welchem übergeordneten Thema gehört.

Genau dieses Ordnungsprinzip wendest du mit den HTML-Überschriften `<h1>` bis `<h6>` auf deiner Webseite an. Du schaffst eine klare, logische und nachvollziehbare Struktur für deine Inhalte. Es gibt dabei eine fundamentale Regel, die wichtiger ist als fast jede andere, wenn es um Überschriften geht: **Du überspringst niemals eine Ebene.**

Was bedeutet das konkret? Es bedeutet, dass auf eine `<h1>`-Überschrift immer eine `<h2>` folgen muss, wenn du eine Unterebene einführst. Auf eine `<h2>` folgt eine `<h3>`, auf eine `<h3>` eine `<h4>` und so weiter. Du kannst jederzeit auf einer Ebene bleiben (auf eine `<h2>` kann eine weitere `<h2>` folgen) oder eine Ebene nach oben gehen (auf eine `<h3>` kann eine `<h2>` folgen, wenn ein neuer Abschnitt beginnt). Aber du darfst niemals von einer `<h2>` direkt zu einer `<h4>` springen und die `<h3>`-Ebene auslassen.

#### Warum diese Regel so entscheidend ist

Diese Regel ist kein Selbstzweck oder eine pedantische Spitzfindigkeit für Entwickler. Sie hat handfeste, praktische Gründe, die das Fundament einer guten Webseite ausmachen. Die beiden wichtigsten sind Barrierefreiheit und Suchmaschinenoptimierung (SEO).

**1. Barrierefreiheit (Accessibility)**

Stell dir eine Person vor, die blind ist und eine Webseite mit einem Screenreader besucht. Ein Screenreader ist eine Software, die den Bildschirminhalt vorliest. Für diese Person ist die visuelle Gliederung durch Schriftgrößen und Abstände nicht wahrnehmbar. Stattdessen verlässt sie sich auf die semantische Struktur des HTML-Codes.

Screenreader bieten eine sehr nützliche Funktion: Sie können eine Gliederung der Seite basierend auf den Überschriften-Tags erstellen und dem Nutzer erlauben, direkt von Überschrift zu Überschrift zu springen. Ein Nutzer kann sich also zuerst alle `<h2>`-Überschriften vorlesen lassen, um einen groben Überblick über die Hauptthemen der Seite zu bekommen. Wenn ein Thema interessant klingt, kann er in diesen Abschnitt springen und sich die untergeordneten `<h3>`-Überschriften anhören, um tiefer ins Detail zu gehen.

Wenn du nun eine Ebene überspringst – zum Beispiel von einer `<h2>` direkt zu einer `<h4>` – entsteht eine Lücke in dieser Gliederung. Der Screenreader und sein Nutzer fragen sich: Wo ist die `<h3>`? Habe ich etwas verpasst? Ist die Struktur der Seite fehlerhaft? Diese Verwirrung zerstört das Navigationserlebnis und macht es für den Nutzer unnötig schwer, deine Inhalte zu erfassen. Eine lückenlose Hierarchie ist wie eine verlässliche Landkarte für Menschen, die nicht sehen können. Sie schafft Vertrauen und Orientierung.

**2. Suchmaschinenoptimierung (SEO)**

Auch Suchmaschinen wie Google funktionieren ähnlich wie ein Screenreader: Sie können nicht "sehen", wie eine Seite aussieht. Stattdessen analysieren sie den Code, um die Struktur und die thematische Relevanz der Inhalte zu verstehen. Die Überschriften-Hierarchie ist dabei ein extrem wichtiges Signal.

Eine `<h1>` signalisiert das Hauptthema der gesamten Seite. Die `<h2>`-Tags gliedern dieses Hauptthema in seine wichtigsten Unterthemen. Die `<h3>`-Tags verfeinern diese Unterthemen weiter. Durch eine logische und lückenlose Hierarchie hilfst du der Suchmaschine, den Kontext deiner Inhalte exakt zu verstehen. Sie erkennt, welche Abschnitte zusammengehören und welche Informationen die wichtigsten sind.

Eine fehlerhafte Struktur mit Lücken kann die Suchmaschine verwirren. Sie könnte annehmen, dass deine Seite schlecht strukturiert ist, was sich negativ auf dein Ranking auswirken kann. Eine saubere Hierarchie ist also auch ein klares Signal an Google: "Meine Inhalte sind gut durchdacht, logisch geordnet und nutzerfreundlich."

#### Die häufigste Fehlerquelle: Design über Semantik stellen

Der mit Abstand häufigste Grund, warum Entwickler gegen diese Regel verstoßen, hat mit dem visuellen Design zu tun. Nehmen wir an, deine `<h2>` hat eine Schriftgröße von 32 Pixeln und deine `<h3>` eine von 24 Pixeln. Nun brauchst du für einen bestimmten Bereich eine Überschrift, die optisch etwas kleiner ist als die `<h3>`, vielleicht 20 Pixel groß. Im Standard-Styling deines Browsers entspricht das vielleicht einer `<h4>`.

Der verlockende, aber falsche Gedanke ist nun: "Ich brauche eine 20-Pixel-Überschrift, also nehme ich einfach ein `<h4>`-Tag." Wenn du dich aber gerade in einem von einer `<h2>` eingeleiteten Abschnitt befindest, schaffst du damit genau die Lücke, die wir vermeiden wollen.

**Falscher Ansatz (semantisch inkorrekt):**

```html
<body>
  <h1>Der ultimative Guide für Zimmerpflanzen</h1>
  <p>Alles, was du über die Pflege deiner grünen Freunde wissen musst.</p>
  
  <h2>Die Wahl des richtigen Standorts</h2>
  <p>Licht ist der wichtigste Faktor für das Wachstum von Pflanzen...</p>
  
  <!-- FALSCH! Hier wurde h3 übersprungen, nur weil ein kleinerer Look gewünscht war. -->
  <h4>Schattenliebende Pflanzen</h4>
  <p>Auch für dunkle Ecken gibt es die passenden Gewächse...</p>
</body>
```

Dieser Code ist für sehende Nutzer vielleicht optisch korrekt, aber für Screenreader und Suchmaschinen ist die Struktur kaputt. Die logische Gliederungsebene `<h3>` fehlt.

Die richtige Lösung liegt in der Trennung von Struktur und Design. HTML ist für die Struktur (die Semantik) zuständig, CSS für das Aussehen (das Design). Die semantische Ebene der Überschrift wird ausschließlich durch die Logik deines Inhalts bestimmt, niemals durch ihr gewünschtes Aussehen.

**Richtiger Ansatz (semantisch korrekt):**

Erst definierst du die korrekte, lückenlose HTML-Struktur. Da "Schattenliebende Pflanzen" ein Unterpunkt von "Die Wahl des richtigen Standorts" ist, muss es eine `<h3>` sein.

```html
<body>
  <h1>Der ultimative Guide für Zimmerpflanzen</h1>
  <p>Alles, was du über die Pflege deiner grünen Freunde wissen musst.</p>
  
  <h2>Die Wahl des richtigen Standorts</h2>
  <p>Licht ist der wichtigste Faktor für das Wachstum von Pflanzen...</p>
  
  <!-- RICHTIG! Die logische Ebene h3 wird verwendet. -->
  <h3>Schattenliebende Pflanzen</h3>
  <p>Auch für dunkle Ecken gibt es die passenden Gewächse...</p>

  <h3>Pflanzen für sonnige Fensterbänke</h3>
  <p>Manche Pflanzen können von der Sonne nicht genug bekommen...</p>

  <h2>Die richtige Bewässerung</h2>
  <p>Weniger ist oft mehr. So gießt du deine Pflanzen richtig...</p>
</body>
```

Wenn dir das Aussehen der `<h3>` nun nicht gefällt – weil sie zu groß, zu fett oder in der falschen Farbe ist –, passt du das ganz einfach mit CSS an. Du kannst einer `<h3>` jedes beliebige Aussehen geben, ohne ihre semantische Bedeutung zu verändern.

```css
/* In deiner CSS-Datei */

h3 {
  font-size: 20px; /* Genau die gewünschte Größe */
  font-weight: normal; /* Vielleicht nicht fett? */
  color: #333; /* Eine andere Farbe? */
  margin-top: 30px; /* Mehr Abstand nach oben? */
}
```

Mit diesem Ansatz erreichst du beides: eine perfekte, logische und barrierefreie Dokumentstruktur in deinem HTML und die volle kreative Kontrolle über das Design in deinem CSS.

Denk immer daran: Die Überschriften-Hierarchie ist das Skelett deiner Webseite. Wenn dieses Skelett Knochenbrüche oder fehlende Wirbel hat, kann der Körper nicht richtig funktionieren. Halte die Hierarchie sauber und lückenlos, und du schaffst eine robuste, zugängliche und verständliche Basis für all deine Inhalte.
