# Vermeidung von Lücken in der Hierarchie

### Vermeidung von Lücken in der Hierarchie

Stell dir die Überschriften-Hierarchie deines Dokuments wie das Inhaltsverzeichnis eines Buches vor. Das `<h1>`-Element ist der Buchtitel. Die `<h2>`-Elemente sind die großen Kapitelüberschriften. Die `<h2>`-Elemente gliedern sich weiter in `<h3>`-Abschnitte, diese wiederum in `<h4>`-Unterabschnitte und so weiter. Diese Struktur ist nicht nur eine optische Konvention, sondern das logische Rückgrat deiner Webseite. Eine der wichtigsten Regeln für den Aufbau dieses Rückgrats lautet: Überspringe niemals eine Überschriftenebene.

Diese Regel ist keine willkürliche Schikane für Entwickler. Sie hat tiefgreifende, praktische Gründe, die sich auf drei wesentliche Bereiche auswirken: Barrierefreiheit (Accessibility), Suchmaschinenoptimierung (SEO) und die Wartbarkeit deines Codes.

#### Für Menschen und Maschinen: Die Bedeutung der Struktur

Der wohl wichtigste Grund, die Hierarchie lückenlos zu halten, ist die Barrierefreiheit. Nicht alle Nutzer erleben das Web auf die gleiche Weise. Insbesondere Menschen mit Sehbehinderungen, die auf Screenreader angewiesen sind, navigieren eine Webseite nicht primär visuell, sondern anhand ihrer strukturellen Gliederung.

Ein Screenreader ist eine Software, die den Bildschirminhalt vorliest. Für Nutzer dieser Software sind Überschriften die zentralen Wegweiser auf einer Seite. Sie können sich eine Gliederung aller Überschriften ansagen lassen, um schnell einen Überblick über den Inhalt zu bekommen – ganz ähnlich, wie sehende Nutzer eine Seite überfliegen (scannen), um interessante Abschnitte zu finden. Außerdem bieten die meisten Screenreader Tastaturkürzel an, um direkt von einer Überschrift zur nächsten zu springen (z. B. von `<h2>` zu `<h2>`) oder um eine Ebene tiefer zu navigieren (von `<h2>` zur nächsten `<h3>`).

Wenn du nun eine Ebene überspringst – also zum Beispiel von einer `<h1>` direkt zu einer `<h3>` springst –, zerreißt du dieses Navigationsnetz. Der Nutzer des Screenreaders fragt sich: Wo ist das `<h2>`-Kapitel, zu dem dieser `<h3>`-Abschnitt gehört? Ist es ein Fehler auf der Seite oder habe ich etwas übersehen? Die logische Struktur bricht zusammen und die Seite wird unübersichtlich und schwer zu navigieren. Eine korrekte, lückenlose Hierarchie ist also ein Akt der Inklusion und des Respekts gegenüber allen deinen Nutzern.

Auch Suchmaschinen wie Google verlassen sich stark auf die Überschriften-Hierarchie, um den Inhalt und die thematische Struktur deiner Seite zu verstehen. Der Crawler einer Suchmaschine analysiert dein HTML und interpretiert die Überschriften als Gliederungspunkte. Das `<h1>`-Element signalisiert das Hauptthema der Seite. Die `<h2>`-Elemente definieren die wichtigsten Unterthemen. Die `<h3>`-Elemente verfeinern diese Unterthemen weiter. Eine saubere, logische Abstufung hilft der Suchmaschine, die Relevanz deines Inhalts für bestimmte Suchanfragen präzise zu bewerten. Lücken in dieser Hierarchie können den Crawler verwirren und zu einer schlechteren Einschätzung der Inhaltsstruktur führen, was sich negativ auf dein Ranking auswirken kann.

#### Ein typischer Fehler: Der Sprung von `<h1>` zu `<h3>`

Lass uns ein konkretes Beispiel betrachten. Angenommen, du erstellst eine Seite über Zimmerpflanzen. Du beginnst korrekt mit einer Hauptüberschrift `<h1>`. Danach möchtest du verschiedene Pflanzenarten vorstellen, die für Anfänger geeignet sind. Aus rein gestalterischen Gründen findest du die Standardformatierung einer `<h2>`-Überschrift zu groß und entscheidest dich stattdessen für eine `<h3>`, weil sie kleiner und dezenter aussieht.

Dein Code könnte dann so aussehen:

```html
<!-- FALSCH: Die Hierarchie-Ebene <h2> wird übersprungen -->

<h1>Der ultimative Guide für Zimmerpflanzen</h1>

<p>Willkommen zu unserem Guide. Hier findest du alles, was du über die Pflege von Pflanzen in deinem Zuhause wissen musst.</p>

<h3>Die besten Pflanzen für Anfänger</h3>
<p>Monstera, Grünlilie und Bogenhanf sind besonders pflegeleicht und daher ideal für den Einstieg...</p>

<h3>Pflege von Sukkulenten</h3>
<p>Sukkulenten benötigen wenig Wasser, aber viel Licht. Hier sind die wichtigsten Tipps...</p>
```

Auf den ersten Blick mag das Layout im Browser vielleicht genau so aussehen, wie du es dir vorgestellt hast. Strukturell ist es jedoch fehlerhaft. Es fehlt die übergeordnete Kategorie, zu der "Pflanzen für Anfänger" und "Pflege von Sukkulenten" gehören.

#### So geht es richtig: Eine lückenlose Hierarchie

Die korrekte Herangehensweise wäre, eine `<h2>`-Überschrift als logisches "Kapitel" einzuführen. Auch wenn du vielleicht keinen einleitenden Text für dieses Kapitel hast, ist die Überschrift selbst für die Struktur unerlässlich.

Der semantisch korrekte Code würde so aussehen:

```html
<!-- RICHTIG: Die Hierarchie ist lückenlos und logisch -->

<h1>Der ultimative Guide für Zimmerpflanzen</h1>

<p>Willkommen zu unserem Guide. Hier findest du alles, was du über die Pflege von Pflanzen in deinem Zuhause wissen musst.</p>

<h2>Arten und ihre Pflege</h2>

<h3>Die besten Pflanzen für Anfänger</h3>
<p>Monstera, Grünlilie und Bogenhanf sind besonders pflegeleicht und daher ideal für den Einstieg...</p>

<h3>Pflege von Sukkulenten</h3>
<p>Sukkulenten benötigen wenig Wasser, aber viel Licht. Hier sind die wichtigsten Tipps...</p>
```

In dieser Version ist die Struktur glasklar: Die Seite handelt vom "Guide für Zimmerpflanzen" (`<h1>`). Ein Hauptkapitel darin ist "Arten und ihre Pflege" (`<h2>`). Dieses Kapitel enthält die Unterabschnitte "Pflanzen für Anfänger" (`<h3>`) und "Pflege von Sukkulenten" (`<h3>`). Jede Überschrift ist eine logische Unterordnung der vorhergehenden Ebene. Sowohl für einen Screenreader-Nutzer als auch für eine Suchmaschine ist diese Gliederung jetzt perfekt nachvollziehbar.

#### "Aber es soll doch anders aussehen!" – HTML für Struktur, CSS für Stil

Das häufigste Argument für das Überspringen von Überschriftenebenen ist ein rein visuelles: "Ich brauche an dieser Stelle eine kleinere Überschrift." Dies ist ein klassischer Denkfehler, der aus der Vermischung von Struktur und Präsentation resultiert.

Die wichtigste Lektion, die du hier mitnehmen musst, ist die strikte Trennung von Inhalt und Struktur (definiert durch HTML) und der visuellen Darstellung (definiert durch CSS).

Die Größe, die Farbe oder der Schriftschnitt einer Überschrift sind nicht in Stein gemeißelt. Was du im Browser siehst, sind lediglich die Standardstile, die der Browser auf `<h1>`-, `<h2>`-, `<h3>`-Elemente usw. anwendet. Du hast die volle Kontrolle darüber, das Aussehen jedes Elements mit CSS anzupassen.

Wenn du also in unserem korrekten Beispiel möchtest, dass die `<h2>`-Überschrift "Arten und ihre Pflege" kleiner erscheint – vielleicht so klein wie eine standardmäßige `<h3>` –, dann erreichst du das nicht, indem du das HTML-Tag änderst. Stattdessen behältst du das semantisch korrekte `<h2>`-Tag bei und passt sein Aussehen mit CSS an.

Du könntest deinem `<h2>`-Element eine Klasse geben, um es gezielt zu stylen:

```html
<!-- Semantisch korrektes HTML -->
<h2 class="unterkapitel-klein">Arten und ihre Pflege</h2>
```

Und in deiner CSS-Datei definierst du dann das gewünschte Aussehen für diese Klasse:

```css
/* In deiner CSS-Datei */
.unterkapitel-klein {
  font-size: 1.2em; /* Eine kleinere Schriftgröße */
  font-weight: normal; /* Vielleicht nicht fettgedruckt */
  color: #555;      /* Eine dezentere Farbe */
  margin-top: 40px;  /* Mehr Abstand nach oben */
}
```

Mit diesem Ansatz erreichst du das Beste aus beiden Welten:
1.  **Semantisch perfektes HTML:** Deine Dokumentenstruktur bleibt logisch, korrekt und für alle zugänglich.
2.  **Volle gestalterische Freiheit:** Du kannst jedes Element exakt so aussehen lassen, wie es dein Design erfordert.

Indem du diese Regel konsequent befolgst, schreibst du nicht nur sauberen und professionellen Code, sondern schaffst ein besseres, faireres und verständlicheres Web für alle. Die Hierarchie der Überschriften ist das Fundament deiner Inhalte – baue es stabil und ohne Lücken.
