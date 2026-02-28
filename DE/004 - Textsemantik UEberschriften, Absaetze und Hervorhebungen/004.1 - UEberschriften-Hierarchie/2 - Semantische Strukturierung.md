# Semantische Strukturierung

### Die Ordnung der Dinge: Semantische Strukturierung mit Überschriften

Stell dir vor, du betrittst eine riesige Bibliothek ohne jegliche Beschilderung. Es gibt keine Schilder für Sachbücher, Romane oder Zeitschriften. Die Bücher selbst haben keine Titel auf dem Buchrücken, und im Inneren gibt es keine Kapitelüberschriften oder Seitenzahlen. Du suchst eine ganz bestimmte Information. Wie lange würdest du brauchen, um sie zu finden? Wahrscheinlich eine Ewigkeit. Du müsstest jedes Buch von vorne bis hinten durchlesen.

Eine Webseite ohne semantische Struktur ist genau wie diese chaotische Bibliothek. Für das bloße Auge mag sie vielleicht ansprechend aussehen – die Texte haben unterschiedliche Größen, sind fett gedruckt oder kursiv. Aber unter der Haube, im HTML-Code, herrscht pures Chaos.

Hier kommt die Semantik ins Spiel. Das Wort „Semantik“ bedeutet so viel wie „die Lehre von der Bedeutung“. Im Kontext von HTML bedeutet es, dass du den Elementen deines Dokuments eine klare Bedeutung gibst. Du sagst dem Browser und anderen Maschinen (wie den Suchmaschinen-Crawlern) nicht nur, *wie* etwas aussehen soll, sondern vor allem, *was* es ist. Ein `<p>`-Tag sagt: „Dies ist ein Absatz.“ Ein `<strong>`-Tag sagt: „Dieser Text hat eine hohe Wichtigkeit.“ Und ein `<h1>`-Tag sagt: „Dies ist die Hauptüberschrift der gesamten Seite.“

Dieser Ansatz ist das genaue Gegenteil davon, HTML-Tags nur für ihr Aussehen zu missbrauchen. Früher war es üblich, Text einfach in einen `<h1>`-Tag zu packen, weil er standardmäßig groß und fett dargestellt wird. Das ist, als würdest du ein „Achtung, Hochspannung!“-Schild verwenden, um auf den kostenlosen Kaffee im Pausenraum hinzuweisen, nur weil das Schild eine auffällige Farbe hat. Es mag funktionieren, aber die Bedeutung ist komplett falsch und potenziell irreführend.

In diesem Kapitel konzentrieren wir uns auf das Rückgrat jeder gut strukturierten Webseite: die Überschriften-Hierarchie. Sie ist das Inhaltsverzeichnis deines Dokuments und der erste und wichtigste Schritt zu sauberem, semantischem HTML.

#### Das Gesetz der Hierarchie: `<h1>` bis `<h6>`

HTML stellt dir sechs Ebenen von Überschriften zur Verfügung: `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>` und `<h6>`. Man könnte meinen, diese Tags seien einfach dazu da, sechs verschiedene Schriftgrößen zu erzeugen. Das ist der häufigste und zugleich schwerwiegendste Trugschluss in der Webentwicklung.

Denk an diese Tags nicht als Stilwerkzeuge, sondern als Gliederungsebenen, genau wie in einem Buch oder einem wissenschaftlichen Aufsatz:

*   **`<h1>`: Der Buchtitel.** Dies ist die wichtigste Überschrift deines Dokuments. Sie beschreibt das übergeordnete Thema der gesamten Seite. Auf einer ganzen HTML-Seite sollte es **genau eine** `<h1>`-Überschrift geben. Sie ist der Ankerpunkt, an dem sich alles andere ausrichtet.
*   **`<h2>`: Die Kapitelüberschriften.** Diese Überschriften gliedern den Inhalt, der unter der `<h1>` steht, in seine Hauptabschnitte. Du kannst so viele `<h2>`-Tags haben, wie du logische Hauptabschnitte hast.
*   **`<h3>`: Die Unterkapitel.** Wenn ein Hauptabschnitt (eingeleitet durch eine `<h2>`) weiter unterteilt werden muss, kommen `<h3>`-Tags ins Spiel. Sie schaffen eine Gliederung innerhalb eines Kapitels.
*   **`<h4>`, `<h5>`, `<h6>`: Die weiteren Detailebenen.** Diese Tags dienen dazu, die Struktur noch feiner zu granulieren. In der Praxis wirst du `<h5>` und `<h6>` eher selten benötigen, aber es ist gut zu wissen, dass sie für sehr komplexe und tief verschachtelte Dokumente existieren.

Die goldene Regel der Überschriften-Hierarchie lautet: **Du darfst keine Ebene überspringen.**

Du beginnst immer mit einer `<h1>`. Die nächste Überschrift in der Gliederung muss eine `<h2>` sein (oder eine weitere `<h1>`, falls ein komplett neues Dokument beginnt, was auf einer einzelnen Webseite nie der Fall ist). Unter einer `<h2>` kann entweder eine weitere `<h2>` folgen (für den nächsten Hauptabschnitt) oder eine `<h3>`, um den aktuellen Abschnitt zu unterteilen. Es ist jedoch ein logischer Bruch und damit ein semantischer Fehler, direkt von einer `<h2>` zu einer `<h4>` zu springen, nur weil dir die Standard-Schriftgröße der `<h4>` besser gefällt. Das Styling ist alleinige Aufgabe von CSS. Im HTML geht es ausschließlich um Struktur und Bedeutung.

Schauen wir uns ein schlechtes und ein gutes Beispiel an. Stell dir eine einfache Rezept-Seite für Apfelkuchen vor.

**So machst du es NICHT:**

```html
<!-- FALSCH: Die Hierarchie wird für visuelle Zwecke missbraucht. -->

<h1>Omas Apfelkuchen</h1>
<!-- Soweit so gut, die Hauptüberschrift stimmt. -->

<h4>Ein Klassiker, der immer gelingt</h4>
<!-- FEHLER: Sprung von h1 zu h4. Dies ist nur ein Untertitel, keine Überschrift der 4. Ebene. -->

<h2>Zutaten</h2>
<!-- OK, ein neuer Hauptabschnitt beginnt. -->

<h2>Zubereitung</h2>
<!-- OK, der nächste Hauptabschnitt. -->

<h4>Schritt 1: Teig vorbereiten</h4>
<!-- FEHLER: Dies ist ein Unterpunkt von "Zubereitung". Es müsste eine h3 sein. -->

<h4>Schritt 2: Äpfel schneiden</h4>
<!-- FEHLER: Ebenfalls ein Unterpunkt, der eine h3 sein sollte. -->

<h1>Noch mehr tolle Rezepte</h1>
<!-- GROSSER FEHLER: Es gibt eine zweite h1 auf der Seite. -->
```

Dieser Code ist ein semantisches Durcheinander. Eine Maschine, die diesen Code liest, ist verwirrt. Warum folgt auf die Hauptüberschrift eine Überschrift der vierten Ebene? Warum gibt es zwei Hauptüberschriften?

**So ist es richtig:**

```html
<!-- KORREKT: Eine logische und klare Hierarchie. -->

<h1>Omas Apfelkuchen</h1>
<p>Ein Klassiker, der immer gelingt. Dieser Untertitel ist ein einfacher Absatz, keine Überschrift.</p>

<h2>Zutaten</h2>
<ul>
  <li>Mehl</li>
  <li>Zucker</li>
  <li>Äpfel</li>
  <!-- ... weitere Zutaten ... -->
</ul>

<h2>Zubereitung</h2>
<p>Folge diesen einfachen Schritten für den perfekten Kuchen.</p>

<h3>Schritt 1: Teig vorbereiten</h3>
<p>Mische Mehl, Zucker und Butter zu einem glatten Teig...</p>

<h3>Schritt 2: Äpfel schneiden</h3>
<p>Schäle die Äpfel, entferne das Kerngehäuse und schneide sie in Spalten...</p>

<h2>Nährwertangaben</h2>
<p>Pro Stück enthält der Kuchen ca. 300 Kalorien...</p>
```

In der korrekten Version ist die Struktur sofort glasklar. Es gibt eine Hauptüberschrift (`<h1>`). Darauf folgen logische Hauptabschnitte (`<h2>` für Zutaten, Zubereitung, Nährwertangaben). Der Abschnitt „Zubereitung“ wird durch `<h3>`-Überschriften sinnvoll unterteilt. Der Untertitel ist ein einfacher `<p>`-Absatz, denn er leitet keinen eigenen Inhaltsblock ein, sondern ergänzt nur die Hauptüberschrift. Diese Struktur ist logisch, vorhersehbar und maschinenlesbar.

#### Warum der ganze Aufwand?

Vielleicht fragst du dich jetzt: „Warum ist das so wichtig? Visuell kann ich doch mit CSS alles genauso aussehen lassen.“ Das stimmt, aber das Aussehen ist nur die Oberfläche. Die wahre Stärke einer semantischen Struktur liegt tiefer und zahlt sich in drei entscheidenden Bereichen aus:

**1. Zugänglichkeit (Accessibility)**

Stell dir vor, du bist blind und nutzt einen Screenreader, um im Internet zu surfen. Ein Screenreader ist eine Software, die den Inhalt einer Webseite vorliest. Du würdest nicht wollen, dass dir die gesamte Seite von oben bis unten vorgelesen wird, nur um herauszufinden, ob die Informationen relevant sind. Stattdessen nutzt du eine spezielle Funktion deines Screenreaders, die dir eine Liste aller Überschriften auf der Seite anzeigt.

Bei unserem korrekten Apfelkuchen-Beispiel würde der Screenreader dir eine Gliederung präsentieren:

*   Überschrift Ebene 1: Omas Apfelkuchen
*   Überschrift Ebene 2: Zutaten
*   Überschrift Ebene 2: Zubereitung
    *   Überschrift Ebene 3: Schritt 1: Teig vorbereiten
    *   Überschrift Ebene 3: Schritt 2: Äpfel schneiden
*   Überschrift Ebene 2: Nährwertangaben

Du kannst nun direkt zu dem Abschnitt springen, der dich interessiert. Wenn du nur die Zubereitung wissen willst, navigierst du direkt dorthin. Bei der falschen, kaputten Struktur wäre diese Navigation unmöglich oder extrem verwirrend. Eine korrekte Überschriften-Hierarchie ist keine nette Dreingabe für die Barrierefreiheit – sie ist eine absolute Notwendigkeit.

**2. Suchmaschinenoptimierung (SEO)**

Suchmaschinen wie Google sind im Grunde blinde, aber extrem schnelle Nutzer. Sie können das visuelle Design deiner Seite nicht „sehen“. Stattdessen analysieren sie den Code, um den Inhalt zu verstehen. Die Überschriften-Hierarchie ist für sie ein entscheidender Hinweis darauf, worum es auf deiner Seite geht und welche Themenbereiche besonders wichtig sind.

Die `<h1>` signalisiert Google das Hauptkeyword oder das zentrale Thema der Seite. Die `<h2>`-Tags teilen die wichtigsten Unterthemen mit. Eine saubere, logische Struktur hilft der Suchmaschine, deine Inhalte besser zu katalogisieren und als relevant für bestimmte Suchanfragen einzustufen. Eine Seite mit einer klaren semantischen Gliederung hat oft einen Vorteil gegenüber einer unstrukturierten Seite, weil die Suchmaschine den Inhalt einfach besser versteht.

**3. Wartbarkeit und Styling**

Auch für dich als Entwickler ist eine saubere Struktur ein Segen. Wenn du zu deinem Code zurückkehrst, erkennst du auf einen Blick die Gliederung des Dokuments, ohne auch nur eine Zeile CSS oder die gerenderte Seite sehen zu müssen. Der Code wird selbsterklärend.

Zudem vereinfacht es das Styling mit CSS ungemein. Anstatt komplizierte Klassen wie `.grosser-titel`, `.mittlerer-titel` oder `.ganz-kleiner-untertitel` zu vergeben, kannst du deine Stile direkt und logisch an die semantischen Elemente knüpfen:

```css
/* Gib allen Hauptabschnitten einen oberen Abstand */
h2 {
  margin-top: 40px;
}

/* Formatiere alle Unterpunkte innerhalb der Zubereitung anders */
h2 + h3 {
  color: #555;
  font-style: italic;
}
```

Diese CSS-Regeln sind robust, verständlich und basieren auf der logischen Struktur deines Dokuments, nicht auf zufälligen Klassennamen. Ändert sich die Struktur, passt du einfach das HTML an, und die CSS-Regeln greifen weiterhin logisch.

Die semantische Strukturierung mit Überschriften ist also weit mehr als eine formale Übung. Sie ist die Grundlage für ein zugängliches, suchmaschinenfreundliches und wartbares Web. Bevor du also das nächste Mal einen Tag nur wegen seines Aussehens wählst, halte kurz inne und frage dich: „Was *ist* dieser Inhalt?“ Die Antwort auf diese Frage führt dich fast immer zum richtigen HTML-Tag.
