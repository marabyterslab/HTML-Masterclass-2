# Bedeutung von h1 bis h6

### Die Hierarchie der Überschriften: Die Bedeutung von `<h1>` bis `<h6>`

Stell dir vor, du schlägst ein dickes Sachbuch auf, um eine bestimmte Information zu finden. Was tust du als Erstes? Wahrscheinlich überfliegst du das Inhaltsverzeichnis. Du schaust auf die großen Kapitelüberschriften, dann auf die Unterkapitel und vielleicht sogar auf die noch kleineren Abschnittsüberschriften, bis du den relevanten Teil gefunden hast. Dieses System aus Haupt- und Unterpunkten hilft dir, die Struktur des Buches in Sekunden zu erfassen und direkt dorthin zu navigieren, wo du hinwillst.

Genau dieselbe Funktion erfüllen Überschriften-Tags in HTML. Die Elemente `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>` und `<h6>` sind nicht einfach nur Werkzeuge, um Text in verschiedenen Größen darzustellen. Sie sind das strukturelle Rückgrat deiner Webseite. Sie erzeugen eine logische Hierarchie und Gliederung, die sowohl für Menschen als auch für Maschinen von entscheidender Bedeutung ist.

#### Mehr als nur große Buchstaben: Semantik ist alles

Ein häufiger Fehler von Anfängern ist es, Überschriften-Tags nach ihrem Aussehen auszuwählen. Man braucht einen großen Titel, also nimmt man `<h1>`. Ein kleinerer Zwischentext wird dann vielleicht mit `<h4>` umgesetzt, weil es von der Größe her gerade passt. Dieser Ansatz ist grundlegend falsch und ignoriert das wichtigste Prinzip von HTML: die Semantik, also die Bedeutung der Elemente.

Ein `<h1>`-Tag sagt dem Browser nicht „mach mich groß und fett“, sondern „ich bin die wichtigste Überschrift auf dieser Seite“. Die visuelle Darstellung (groß und fett) ist lediglich eine Standardeinstellung des Browsers, um diese Wichtigkeit visuell zu unterstreichen. Das Aussehen kannst und solltest du später vollständig mit CSS kontrollieren. Die strukturelle Bedeutung hingegen ist fest im HTML verankert und unveränderlich.

Denke an die Überschriften-Tags als eine Rangordnung:

*   `<h1>`: Die Hauptüberschrift des gesamten Dokuments. Der Titel des „Buches“.
*   `<h2>`: Eine Hauptabschnittsüberschrift. Ein „Kapitel“.
*   `<h3>`: Eine Unterabschnittsüberschrift. Ein „Unterkapitel“.
*   `<h4>`: Eine weitere Unterteilung. Ein Abschnitt innerhalb eines Unterkapitels.
*   `<h5>` und `<h6>`: Noch feinere Gliederungsebenen.

Deine Aufgabe ist es, diese Ränge korrekt zu verwenden, um die logische Struktur deines Inhalts abzubilden, völlig unabhängig davon, wie sie am Ende aussehen sollen.

#### Die Regeln der Hierarchie

Um eine saubere und verständliche Struktur zu gewährleisten, gibt es zwei goldene Regeln bei der Verwendung von Überschriften:

**1. Es gibt nur eine Nummer eins: Der `<h1>`-Tag**

Jede einzelne HTML-Seite sollte genau einen `<h1>`-Tag haben. Er repräsentiert den übergeordneten Titel des gesamten Seiteninhalts, ähnlich dem Titel auf einem Buchcover. Wenn ein Nutzer auf deiner Seite landet, sollte der `<h1>`-Inhalt ihm sofort verraten, worum es hier im Kern geht. Mehrere `<h1>`-Tags auf einer Seite würden Verwirrung stiften, so als hätte ein Buch mehrere gleichrangige Titel. Suchmaschinen und Hilfstechnologien würden nicht mehr eindeutig erkennen, was das Hauptthema der Seite ist.

**2. Überspringe keine Ebenen**

Die Hierarchie der Überschriften muss logisch und lückenlos sein. Das bedeutet, auf eine `<h1>` folgt eine `<h2>`. Auf eine `<h2>` kann entweder eine weitere `<h2>` (für den nächsten Hauptabschnitt) oder eine `<h3>` (für einen Unterabschnitt) folgen.

Was du niemals tun solltest, ist, eine Ebene zu überspringen. Ein `<h1>`-Tag sollte niemals direkt von einem `<h3>`-Tag gefolgt werden. Das wäre so, als würdest du in einem Buch von der Kapitelüberschrift direkt zu einem kleinen Unter-Unterabschnitt springen, ohne das dazugehörige Unterkapitel zu benennen. Die logische Gliederung wäre durchbrochen.

Eine korrekte Struktur sieht so aus:

```html
<!-- KORREKT -->
<h1>Der Haupttitel der Seite</h1>
<p>Ein einleitender Absatz...</p>

<h2>Erster Hauptabschnitt</h2>
<p>Text zum ersten Hauptabschnitt.</p>
  <h3>Unterabschnitt 1.1</h3>
  <p>Details zu Unterabschnitt 1.1.</p>
  <h3>Unterabschnitt 1.2</h3>
  <p>Details zu Unterabschnitt 1.2.</p>

<h2>Zweiter Hauptabschnitt</h2>
<p>Text zum zweiten Hauptabschnitt.</p>
```

Eine falsche, lückenhafte Struktur würde so aussehen:

```html
<!-- FALSCH -->
<h1>Der Haupttitel der Seite</h1>
<p>Ein einleitender Absatz...</p>

<h3>Ein falsch platzierter Unterabschnitt</h3>
<p>Dieser Abschnitt hat keine übergeordnete <h2>. Die Hierarchie ist kaputt.</p>

<h2>Ein Hauptabschnitt</h2>
<p>Text zum Hauptabschnitt.</p>
```

#### Warum eine saubere Hierarchie entscheidend ist

Eine semantisch korrekte Überschriftenstruktur ist kein Selbstzweck, sondern hat handfeste Vorteile in drei zentralen Bereichen: Suchmaschinenoptimierung (SEO), Barrierefreiheit (Accessibility) und Wartbarkeit des Codes.

**1. Für Suchmaschinen (SEO)**

Suchmaschinen wie Google analysieren deine Webseite nicht mit menschlichen Augen. Sie lesen den Code. Die Überschriften-Tags sind für sie wie ein Inhaltsverzeichnis, das ihnen hilft, den Inhalt und die Struktur deiner Seite blitzschnell zu verstehen. Der Inhalt eines `<h1>`-Tags hat für Google das höchste Gewicht. Er signalisiert das Hauptkeyword oder Thema der Seite. Die `<h2>`-Tags definieren die wichtigsten unterstützenden Unterthemen.

Eine saubere Hierarchie hilft der Suchmaschine, die Relevanz deiner Seite für bestimmte Suchanfragen besser einzuschätzen. Das kann sich positiv auf dein Ranking auswirken. Eine chaotische oder fehlende Überschriftenstruktur hingegen macht es der Suchmaschine schwer, den Kontext zu verstehen.

**2. Für die Barrierefreiheit (Accessibility)**

Dies ist vielleicht der wichtigste Grund für eine korrekte Überschriftenhierarchie. Für blinde oder stark sehbehinderte Menschen, die einen Screenreader nutzen, sind Überschriften das primäre Navigationsinstrument auf einer Webseite. Ein Screenreader ist eine Software, die den Bildschirminhalt vorliest.

Statt eine Seite von oben nach unten linear durchzuhören, können Nutzer eines Screenreaders eine Liste aller Überschriften auf der Seite aufrufen. Sie können dann direkt von einer `<h2>` zur nächsten springen, um schnell den für sie relevanten Abschnitt zu finden – genau wie sehende Nutzer den Text visuell überfliegen.

Wenn du Ebenen überspringst oder Überschriften nur für visuelle Effekte einsetzt, zerstörst du diese Navigationsmöglichkeit. Die Seite wird zu einer unüberwindbaren „Wand aus Text“ und ist für diese Nutzergruppe quasi unbenutzbar.

**3. Für dich und dein CSS (Wartbarkeit)**

Eine logische HTML-Struktur macht auch dein Leben als Entwickler einfacher. Wenn du später das Aussehen deiner Seite mit CSS gestaltest, kannst du dich auf die semantische Struktur verlassen. Du kannst zum Beispiel mit einer einzigen CSS-Regel das Aussehen aller Hauptabschnittsüberschriften (`<h2>`) auf deiner gesamten Webseite einheitlich definieren.

```css
/* Eine einfache CSS-Regel für alle h2-Elemente */
h2 {
  font-size: 2em;
  color: #333;
  border-bottom: 2px solid #f0f0f0;
  padding-bottom: 10px;
  margin-top: 40px;
}
```

Wenn deine HTML-Struktur sauber ist, ist auch dein CSS klarer, kürzer und leichter zu warten. Du musst nicht für jeden Einzelfall separate Klassen erfinden, nur weil du an einer Stelle eine `<h4>` wie eine `<h2>` aussehen lassen wolltest.

#### Die unteren Ränge: `<h4>`, `<h5>` und `<h6>`

Die Überschriften `<h4>` bis `<h6>` kommen in der Praxis seltener vor. Sie sind für sehr tief verschachtelte und detaillierte Inhalte gedacht, wie zum Beispiel in langen wissenschaftlichen Artikeln, juristischen Texten oder sehr komplexen Dokumentationen.

Bevor du eine `<h4>` oder gar eine `<h5>` einsetzt, frage dich, ob dein Inhalt noch gut strukturiert ist. Manchmal ist die Notwendigkeit einer so tiefen Gliederung ein Zeichen dafür, dass ein Thema zu komplex für eine einzelne Seite ist und besser auf mehrere Unterseiten aufgeteilt werden sollte. Dennoch gibt es legitime Anwendungsfälle, und es ist wichtig zu wissen, dass dir diese Werkzeuge zur Verfügung stehen, um auch die feinsten Verästelungen deines Inhalts semantisch korrekt abzubilden.
