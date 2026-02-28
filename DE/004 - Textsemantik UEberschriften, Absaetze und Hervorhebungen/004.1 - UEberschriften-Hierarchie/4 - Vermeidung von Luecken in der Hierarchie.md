# Vermeidung von Lücken in der Hierarchie

### Vermeidung von Lücken in der Hierarchie

Stell dir die Überschriften-Hierarchie deiner Webseite wie das Inhaltsverzeichnis eines Buches vor. Das `<h1>`-Element ist der Buchtitel. Die `<h2>`-Elemente sind die großen Kapitel. Die `<h3>`-Elemente sind die Unterkapitel innerhalb eines Kapitels und so weiter. Ein gut strukturiertes Buch springt nicht von Kapitel 1 direkt zu Unter-Unterkapitel 1.3.1. Das würde jeden Leser verwirren. Genau dieselbe Logik gilt für deine HTML-Dokumente.

Die goldene Regel der Überschriften-Hierarchie lautet: Du darfst keine Ebenen überspringen.

Das bedeutet, auf eine `<h1>` folgt immer eine `<h2>`. Auf eine `<h2>` kann entweder eine weitere `<h2>` (ein neues "Kapitel") oder eine `<h3>` (ein "Unterkapitel") folgen. Auf eine `<h3>` folgt entsprechend eine weitere `<h3>` oder eine `<h4>`. Was du niemals tun solltest, ist zum Beispiel von einer `<h2>` direkt zu einer `<h4>` zu springen.

#### Warum ist diese Regel so wichtig?

Man könnte meinen, dies sei eine rein akademische Spitzfindigkeit. Doch das Gegenteil ist der Fall. Die Einhaltung einer lückenlosen Hierarchie hat tiefgreifende Auswirkungen auf drei entscheidende Bereiche: Barrierefreiheit, Suchmaschinenoptimierung und die Wartbarkeit deines Codes.

**1. Barrierefreiheit (Accessibility)**

Dies ist der wichtigste Grund. Menschen mit Sehbehinderungen nutzen oft Screenreader, um sich im Web zu bewegen. Diese Software liest den Inhalt einer Webseite vor. Um sich schnell einen Überblick zu verschaffen, springen Nutzer von Screenreadern nicht von Wort zu Wort, sondern navigieren oft von Überschrift zu Überschrift. Sie können sich eine Liste aller Überschriften ansagen lassen oder mit einer Tastenkombination zur nächsten Überschrift einer bestimmten Ebene springen.

Stell dir nun vor, ein Nutzer hört: "Überschrift Ebene 1: Die Geschichte des Kaffees". Er erwartet nun als nächstes eine Überschrift der Ebene 2, zum Beispiel "Die Entdeckung in Äthiopien". Stattdessen hört er aber: "Überschrift Ebene 3: Die Legende von Kaldi".

Für den Nutzer entsteht sofort Verwirrung. Er wird sich fragen: "Habe ich etwas übersehen? Wo ist Überschrift Ebene 2? Gehört die Legende von Kaldi zu einem übergeordneten Thema, das mir entgangen ist?" Die logische Struktur der Seite bricht zusammen. Die Navigation wird unvorhersehbar und frustrierend. Eine lückenlose Hierarchie hingegen bietet eine klare, verlässliche Gliederung, die es jedem ermöglicht, den Inhalt und seine Zusammenhänge mühelos zu erfassen.

**2. Suchmaschinenoptimierung (SEO)**

Suchmaschinen wie Google sind im Grunde nichts anderes als extrem schnelle, automatisierte Nutzer. Ihre "Crawler" analysieren den Aufbau deiner Webseite, um deren Inhalt und Relevanz zu verstehen. Die Überschriften-Hierarchie ist dabei eines der stärksten Signale, das du ihnen senden kannst.

Eine saubere, logische Struktur von `<h1>` über `<h2>` zu `<h3>` teilt der Suchmaschine unmissverständlich mit: "Dieses Dokument ist gut organisiert. Das Hauptthema ist X (`<h1>`), es gliedert sich in die wichtigen Unterthemen Y und Z (`<h2>`), und Thema Y hat wiederum die spezifischen Aspekte A und B (`<h3>`)."

Eine Lücke in dieser Hierarchie sendet ein unklares Signal. Der Crawler könnte Schwierigkeiten haben, die genaue Beziehung zwischen den Inhaltsblöcken zu interpretieren. Auch wenn Google dich nicht aktiv dafür "bestraft", wenn du eine Ebene überspringst, so bevorzugt der Algorithmus doch klar strukturierte, qualitativ hochwertige und nutzerfreundliche Inhalte. Eine korrekte Hierarchie ist ein starkes Indiz für genau das und kann sich positiv auf die Bewertung deiner Seite auswirken.

**3. Logik und Wartbarkeit**

Nicht zuletzt hilfst du dir selbst und jedem, der nach dir an dem Code arbeitet. Ein HTML-Dokument mit einer sauberen Überschriften-Hierarchie ist selbsterklärend. Du kannst den Code überfliegen und verstehst sofort die Gliederung des Inhalts, ohne auch nur eine Zeile Text gelesen zu haben.

Wenn du später Inhalte hinzufügen, entfernen oder umstrukturieren musst, macht eine logische Gliederung diesen Prozess unendlich viel einfacher. Du weißt genau, wo ein neuer Abschnitt als `<h3>` hingehört oder ob ein ganzer `<h2>`-Block verschoben werden muss. Bei einer chaotischen Struktur wird jede Änderung zu einem Ratespiel.

#### Die häufigste Falle: Stil vor Semantik

Der häufigste Grund für Lücken in der Hierarchie ist ein Missverständnis der Rollen von HTML und CSS. Ein Entwickler benötigt vielleicht eine Überschrift, die optisch klein ist, ähnlich der Standarddarstellung einer `<h4>`. Inhaltlich handelt es sich aber um ein Hauptkapitel der Seite, das semantisch eine `<h2>` sein müsste. Aus reiner Bequemlichkeit wird dann zum `<h4>`-Tag gegriffen, weil es "richtig aussieht".

Das ist der falsche Ansatz. **HTML strukturiert den Inhalt, CSS gestaltet ihn.**

**Falscher Ansatz (aus stilistischen Gründen):**

```html
<!-- FALSCH: Ebene 2 wurde übersprungen, nur weil h3 "besser aussah" -->
<h1>Willkommen auf unserer Bäckerei-Webseite</h1>

<h3>Unsere Brotsorten</h3>
<p>Hier finden Sie eine Auswahl unserer handgemachten Brote...</p>

<h3>Unsere Kuchen</h3>
<p>Entdecken Sie unsere süßen Verführungen...</p>
```

In diesem Beispiel fehlt die `<h2>`-Ebene komplett. Sowohl für Screenreader als auch für Suchmaschinen ist unklar, ob "Unsere Brotsorten" und "Unsere Kuchen" nun sehr spezifische Unterpunkte des Willkommensgrußes sind oder eigenständige, gleichrangige Hauptbereiche der Seite.

**Korrekter, semantischer Ansatz:**

```html
<!-- RICHTIG: Korrekte semantische Hierarchie -->
<h1>Willkommen auf unserer Bäckerei-Webseite</h1>

<h2>Unsere Brotsorten</h2>
<p>Hier finden Sie eine Auswahl unserer handgemachten Brote...</p>

<h2>Unsere Kuchen</h2>
<p>Entdecken Sie unsere süßen Verführungen...</p>
```

"Aber jetzt ist die Überschrift zu groß!", könntest du einwenden. Das ist der Punkt, an dem CSS ins Spiel kommt. Deine Aufgabe ist es, die semantisch korrekte Überschrift (`<h2>`) zu verwenden und sie dann mit CSS genau so zu gestalten, wie du es benötigst.

```css
/* In deiner CSS-Datei */
h2 {
  font-size: 1.1em; /* Macht die Schrift kleiner */
  color: #663300;  /* Ändert die Farbe */
  font-weight: normal; /* Macht die Schrift nicht fett */
  border-bottom: 1px solid #ccc; /* Fügt eine feine Linie hinzu */
  margin-top: 40px; /* Fügt Abstand nach oben hinzu */
}
```

Mit diesem CSS-Code hast du die volle Kontrolle über das Aussehen, ohne die logische Struktur deines Dokuments zu zerstören. Du trennst sauber zwischen Inhalt (HTML) und Präsentation (CSS), was das Fundament professioneller Webentwicklung ist.

#### Ein vollständiges, korrektes Beispiel

Sehen wir uns eine logische Struktur für einen fiktiven Blogartikel an.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Die Kunst des perfekten Espressos</title>
</head>
<body>

    <h1>Die Kunst des perfekten Espressos</h1>
    <p>Ein Leitfaden für Einsteiger und Fortgeschrittene.</p>

    <h2>Die Wahl der richtigen Bohne</h2>
    <p>Alles beginnt mit der Qualität des Rohmaterials. Arabica, Robusta oder eine Mischung?</p>

        <h3>Herkunft und Röstung</h3>
        <p>Informationen über den Einfluss von Anbaugebiet und Röstgrad.</p>

        <h3>Frische ist entscheidend</h3>
        <p>Warum das Röstdatum wichtiger ist als das Mindesthaltbarkeitsdatum.</p>
    
    <h2>Die richtige Mahlung</h2>
    <p>Der Mahlgrad ist eine Wissenschaft für sich. Zu fein, zu grob – beides ruiniert den Espresso.</p>

    <h2>Der Brühvorgang: Druck und Temperatur</h2>
    <p>Die finalen 25 Sekunden, in denen Magie passiert.</p>

        <h3>Die goldene Regel: 9 Bar Druck</h3>
        <p>Warum dieser Wert als Industriestandard gilt.</p>

        <h3>Die ideale Wassertemperatur</h3>
        <p>Ein paar Grad zu viel oder zu wenig können den Unterschied machen.</p>

    <h2>Fazit: Übung macht den Meister</h2>
    <p>Zusammenfassende Gedanken und Ermutigung zum Experimentieren.</p>

</body>
</html>
```

Diese Struktur ist glasklar. Es gibt einen Haupttitel (`<h1>`). Die vier Hauptabschnitte des Artikels ("Bohne", "Mahlung", "Brühvorgang", "Fazit") sind logisch als `<h2>` ausgezeichnet. Spezifische Unterthemen innerhalb der Hauptabschnitte ("Herkunft", "Frische", "Druck", "Temperatur") sind korrekt als `<h3>` verschachtelt. Ein Nutzer mit einem Screenreader kann problemlos von `<h2>` zu `<h2>` springen, um die Hauptthemen zu erfassen, und bei Interesse in die `<h3>`-Ebene eintauchen.

Halte dich an diese einfache Regel – überspringe niemals eine Überschriften-Ebene – und du legst ein robustes, zugängliches und suchmaschinenfreundliches Fundament für jede Webseite, die du erstellst.
