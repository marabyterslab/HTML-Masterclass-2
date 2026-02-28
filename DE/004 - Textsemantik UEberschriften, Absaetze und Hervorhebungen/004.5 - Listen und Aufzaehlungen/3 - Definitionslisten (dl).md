# Definitionslisten (dl)

### Definitionslisten: Wenn Begriffe eine Erklärung brauchen

Neben den ungeordneten (`<ul>`) und geordneten Listen (`<ol>`), die du bereits kennengelernt hast, bietet HTML eine dritte, spezialisierte Listenart: die Definitionsliste (`<dl>`). Auf den ersten Blick mag sie weniger gebräuchlich erscheinen, doch sie ist ein unglaublich mächtiges Werkzeug für die semantische Auszeichnung von Inhalten, die aus Begriffen und den dazugehörigen Erklärungen bestehen. Stell sie dir wie ein Glossar, ein Lexikon oder die FAQ-Sektion einer Webseite vor. Überall dort, wo du ein Wort oder einen Ausdruck hast und diesem eine Beschreibung zuordnen möchtest, ist die Definitionsliste die semantisch korrekte Wahl.

#### Die Anatomie einer Definitionsliste

Eine Definitionsliste besteht immer aus drei Kernelementen, die untrennbar zusammengehören:

*   **`<dl>` (Definition List):** Dies ist das umschließende Element, das die gesamte Liste als Definitionsliste kennzeichnet. Es ist der Container für alle Begriffe und ihre Beschreibungen.
*   **`<dt>` (Definition Term):** Dieses Element enthält den Begriff, das Wort oder den Ausdruck, der definiert werden soll. Es ist quasi das Stichwort in deinem Lexikon.
*   **`<dd>` (Definition Description):** Dieses Element enthält die Beschreibung, Definition oder Erklärung, die sich auf den unmittelbar vorangehenden Begriff (`<dt>`) bezieht.

Die Grundstruktur ist also immer ein `<dl>`, das eine oder mehrere Gruppen von `<dt>`- und `<dd>`-Elementen enthält.

Schauen wir uns ein einfaches, klassisches Beispiel an, das den Aufbau verdeutlicht:

```html
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language. Die Standardsprache zur Erstellung von Webseiten und Webanwendungen. Sie strukturiert den Inhalt und gibt ihm eine semantische Bedeutung.</dd>

  <dt>CSS</dt>
  <dd>Cascading Style Sheets. Eine Stylesheet-Sprache, die verwendet wird, um das Aussehen und die Formatierung von in HTML geschriebenen Dokumenten zu beschreiben.</dd>

  <dt>JavaScript</dt>
  <dd>Eine Programmiersprache, die es ermöglicht, interaktive Elemente auf Webseiten zu implementieren und das Verhalten von Webseiten dynamisch zu steuern.</dd>
</dl>
```

Standardmäßig rendern die meisten Browser diesen Code, indem sie die `<dd>`-Elemente leicht einrücken, um die Zuordnung zum jeweiligen `<dt>` visuell hervorzuheben. Aber vergiss nie: Diese Standarddarstellung ist nur eine Konvention. Die wahre Stärke liegt in der semantischen Bedeutung, nicht im Aussehen. Mit CSS kannst du das Erscheinungsbild einer Definitionsliste vollständig nach deinen Wünschen gestalten.

#### Flexible Strukturen: Mehr als nur eins zu eins

Die wahre Flexibilität von Definitionslisten zeigt sich darin, dass die Beziehung zwischen Begriffen und Beschreibungen nicht starr auf eins zu eins festgelegt ist. Du kannst die Struktur an deine inhaltlichen Bedürfnisse anpassen.

**Ein Begriff, mehrere Beschreibungen**

Manchmal hat ein Begriff mehrere Bedeutungen oder Aspekte, die du getrennt voneinander erklären möchtest. In diesem Fall kannst du einem `<dt>` einfach mehrere `<dd>`-Elemente folgen lassen.

```html
<dl>
  <dt>Cookie</dt>
  <dd>Im Webkontext: Eine kleine Textdatei, die von einer Webseite auf dem Computer des Benutzers gespeichert wird, um Informationen wie Sitzungs-IDs oder Präferenzen zu speichern.</dd>
  <dd>Im kulinarischen Kontext: Ein kleines, flaches und süßes Gebäck, das im Deutschen oft als Keks bezeichnet wird.</dd>
</dl>
```

Jedes `<dd>` wird als separate Beschreibung für das vorhergehende `<dt>` interpretiert. Das ist semantisch sauber und für Maschinen wie Screenreader oder Suchmaschinen klar verständlich.

**Mehrere Begriffe, eine Beschreibung**

Genauso ist der umgekehrte Fall möglich. Wenn mehrere Begriffe oder Synonyme dieselbe Erklärung teilen, kannst du mehrere `<dt>`-Elemente gruppieren und ihnen eine einzige, gemeinsame `<dd>` folgen lassen.

```html
<dl>
  <dt>HTTP</dt>
  <dt>Hypertext Transfer Protocol</dt>
  <dd>Ein Protokoll zur Übertragung von Daten im World Wide Web. Es ist die Grundlage der Kommunikation zwischen Webbrowsern und Webservern.</dd>
</dl>
```

Diese Struktur macht unmissverständlich klar, dass sowohl „HTTP“ als auch „Hypertext Transfer Protocol“ durch denselben Text beschrieben werden. Du vermeidest so unnötige Wiederholungen und hältst deinen Code schlank und logisch.

**Komplexe Inhalte in Beschreibungen**

Ein `<dd>`-Element ist nicht auf reinen Text beschränkt. Es kann fast jedes andere HTML-Element enthalten, einschließlich Absätze (`<p>`), weiterer Listen (`<ul>`, `<ol>`), Bilder (`<img>`) oder sogar anderer Definitionslisten. Das macht es extrem vielseitig.

```html
<dl>
  <dt>Webseite</dt>
  <dd>
    <p>Ein Dokument, das typischerweise in HTML geschrieben ist und über das World Wide Web zugänglich ist. Eine Webseite kann eine Vielzahl von Elementen enthalten, zum Beispiel:</p>
    <ul>
      <li>Texte und Überschriften</li>
      <li>Bilder und Videos</li>
      <li>Links zu anderen Seiten</li>
      <li>Interaktive Formulare</li>
    </ul>
    <p>Die Gestaltung wird durch CSS und die Interaktivität durch JavaScript realisiert.</p>
  </dd>
</dl>
```

#### Die goldene Regel: Semantik vor Präsentation

Eine der häufigsten Fehlerquellen im Umgang mit Definitionslisten ist ihr Missbrauch für rein visuelle Zwecke. Weil der Browser die `<dd>`-Elemente standardmäßig einrückt, kamen Entwickler früher oft auf die Idee, `<dl>` zu verwenden, um beliebige Texteinrückungen zu erzeugen, zum Beispiel für Dialoge in einem Skript.

**Ein semantisch falsches Beispiel (so bitte nicht!):**

```html
<!-- Falsche Verwendung für reines Layout! -->
<dl>
  <dt>Anna:</dt>
  <dd>Hallo, wie geht es dir?</dd>
  <dt>Ben:</dt>
  <dd>Danke, gut. Und dir?</dd>
</dl>
```

Obwohl das Ergebnis optisch vielleicht dem gewünschten Layout entspricht, ist die Semantik völlig falsch. „Anna:“ ist kein Begriff, der durch „Hallo, wie geht es dir?“ definiert wird. Diese Struktur verwirrt assistierende Technologien wie Screenreader, die versuchen, die logische Beziehung zwischen den Elementen zu interpretieren. Für solche Fälle wären Absätze (`<p>`) mit `<span>`-Elementen oder anderen geeigneten Tags und entsprechender CSS-Formatierung die richtige Wahl.

Nutze eine Definitionsliste also immer nur dann, wenn eine klare Beziehung zwischen einem Begriff (oder einer Gruppe von Begriffen) und einer zugehörigen Beschreibung besteht.

#### Praktische Anwendungsfälle

Abseits von klassischen Glossaren gibt es viele hervorragende Einsatzmöglichkeiten für Definitionslisten im modernen Webdesign:

**1. FAQ-Seiten (Frequently Asked Questions)**
FAQs sind ein Paradebeispiel. Die Frage ist der Begriff (`<dt>`), und die Antwort ist die Beschreibung (`<dd>`).

```html
<dl>
  <dt>Wie lange dauert der Versand?</dt>
  <dd>Der Standardversand innerhalb Deutschlands dauert in der Regel 2-3 Werktage.</dd>

  <dt>Kann ich meine Bestellung zurücksenden?</dt>
  <dd>Ja, du hast ein 30-tägiges Rückgaberecht auf alle unbenutzten Artikel.</dd>
</dl>
```

**2. Metadaten und Schlüssel-Wert-Paare**
Definitionslisten eignen sich perfekt zur Darstellung von Metadaten zu einem Objekt, wie zum Beispiel in einem Produktsteckbrief, einem Rezept oder einer Biografie.

```html
<!-- Beispiel: Metadaten für ein Rezept -->
<dl>
  <dt>Autor:</dt>
  <dd>Max Mustermann</dd>
  <dt>Schwierigkeitsgrad:</dt>
  <dd>Leicht</dd>
  <dt>Zubereitungszeit:</dt>
  <dd>ca. 45 Minuten</dd>
  <dt>Portionen:</dt>
  <dd>4 Personen</dd>
</dl>
```

**3. Dialoge und Skripte (mit Bedacht)**
Obwohl der Missbrauch für reines Layout falsch ist, kann eine Definitionsliste für ein Drehbuch oder einen Dialog semantisch korrekt sein, wenn man den Namen der sprechenden Person als den zu „definierenden“ Begriff und ihre Aussage als „Beschreibung“ ihres Beitrags zur Szene interpretiert. Dies ist jedoch ein Grenzfall, der sorgfältig abgewogen werden sollte.

#### Ein kleiner Ausblick auf das Styling mit CSS

Wie bereits erwähnt, bist du nicht an die Standarddarstellung gebunden. Mit CSS kannst du eine Definitionsliste in fast jede erdenkliche Form bringen. Ein gängiges Muster ist eine zweispaltige Ansicht, bei der die Begriffe in der linken und die Beschreibungen in der rechten Spalte stehen.

Hier ein kurzes Beispiel, wie du das mit modernem CSS (z. B. Grid) erreichen könntest:

```html
<dl class="meta-data">
  <dt>Produkt-ID:</dt>
  <dd>12345-ABC</dd>
  <dt>Material:</dt>
  <dd>Recyceltes Aluminium</dd>
  <dt>Verfügbarkeit:</dt>
  <dd>Auf Lager</dd>
</dl>
```

```css
.meta-data {
  display: grid;
  grid-template-columns: max-content 1fr; /* Spalte 1 so breit wie nötig, Spalte 2 füllt den Rest */
  gap: 10px 20px; /* 10px vertikaler, 20px horizontaler Abstand */
}

.meta-data dt {
  grid-column: 1;
  font-weight: bold;
}

.meta-data dd {
  grid-column: 2;
  margin: 0; /* Standard-Einrückung des Browsers zurücksetzen */
}
```

Dieses CSS verwandelt die einfache, untereinander stehende Liste in ein sauberes, zweispaltiges Layout, ohne die semantische HTML-Struktur zu verändern.

Die Definitionsliste ist somit weit mehr als nur eine Nischenlösung. Sie ist ein präzises und flexibles Werkzeug, um die Beziehung zwischen Namen und Werten, Begriffen und Erklärungen oder Fragen und Antworten klar und maschinenlesbar auszudrücken. Wenn du das nächste Mal auf eine solche Datenstruktur stößt, weißt du, dass `<dl>` die richtige Wahl für eine saubere und semantisch wertvolle Auszeichnung ist.
