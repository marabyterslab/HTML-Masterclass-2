# Struktur (HTML) vs. Präsentation (CSS)

### Die Kunst der Trennung: Struktur (HTML) vs. Präsentation (CSS)

Stell dir vor, du baust ein Haus. Das Erste, was du brauchst, ist ein solider Bauplan und ein stabiles Fundament. Du errichtest Wände, ziehst Decken ein und definierst die Räume: hier das Wohnzimmer, dort die Küche, oben die Schlafzimmer. Diese grundlegende Architektur, das Skelett des Hauses, ist unverzichtbar. Sie gibt allem seinen Platz und seine Funktion. Das ist die Welt von HTML.

Wenn das Gerüst steht, beginnst du mit der Einrichtung. Du entscheidest, welche Wandfarbe das Wohnzimmer bekommt, ob der Boden aus Parkett oder Fliesen sein soll, welche Vorhänge an die Fenster kommen und wo die stylishe Stehlampe platziert wird. Du kümmerst dich um das Aussehen, das Ambiente, die Ästhetik. Das ist die Welt von CSS.

Diese Analogie trifft den Kern der Sache perfekt. Im Webdesign ist die Trennung von Struktur und Präsentation nicht nur eine gute Idee, sondern ein fundamentales Prinzip, das die Grundlage für saubere, wartbare und zugängliche Websites bildet. Lass uns diese beiden Welten genauer betrachten.

#### HTML: Der Architekt des Inhalts

HTML (Hypertext Markup Language) hat nur eine einzige, aber immens wichtige Aufgabe: Es beschreibt die semantische Struktur deines Inhalts. „Semantisch“ bedeutet hier „die Bedeutung betreffend“. Du sagst dem Browser und anderen Maschinen (wie Suchmaschinen oder Screenreadern) nicht, wie etwas aussehen soll, sondern was es *ist*.

- `<h1>` sagt: „Dies ist die wichtigste Überschrift auf dieser Seite.“
- `<p>` sagt: „Dies ist ein Textabsatz.“
- `<ul>` in Kombination mit `<li>` sagt: „Dies ist eine unsortierte Liste von Elementen.“
- `<nav>` sagt: „Hier befindet sich die Hauptnavigation der Seite.“
- `<article>` sagt: „Dieser in sich geschlossene Inhalt könnte auch für sich allein stehen, wie ein Blogbeitrag oder ein Zeitungsartikel.“

Betrachte folgendes, sehr einfaches HTML-Dokument:

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Mein Lieblingsrezept</title>
</head>
<body>

  <article>
    <h1>Der perfekte Käsekuchen</h1>
    <p>Dieses Rezept ist einfach und gelingt immer. Es ist das Ergebnis jahrelanger Verfeinerung und unzähliger Testläufe in meiner Küche.</p>
    
    <h2>Zutaten</h2>
    <ul>
      <li>1 kg Quark</li>
      <li>250g Zucker</li>
      <li>4 Eier</li>
      <li>1 Päckchen Vanillepuddingpulver</li>
      <li>Saft einer Zitrone</li>
    </ul>
    
    <h2>Zubereitung</h2>
    <p>Alle Zutaten in einer großen Schüssel gut verrühren, bis eine glatte Masse entsteht. Die Masse in eine gefettete Springform füllen und bei 160°C ca. 60 Minuten backen.</p>
  </article>

</body>
</html>
```

Wenn du diese Datei in einem Browser ohne jegliches Styling öffnest, siehst du reinen, unformatierten Inhalt. Es ist vielleicht nicht schön, aber es ist perfekt strukturiert und verständlich. Die Überschriften sind hierarchisch geordnet, die Absätze sind klar als solche erkennbar und die Zutatenliste ist eine semantisch korrekte Liste. Eine Suchmaschine weiß genau, was die Hauptüberschrift ist, und ein Screenreader kann einem sehbehinderten Nutzer die Zutaten als eine Liste mit fünf Punkten vorlesen. Die Struktur ist logisch und intakt. Das ist die ganze Magie von HTML.

#### CSS: Der Innenarchitekt des Webs

CSS (Cascading Style Sheets) kommt ins Spiel, um dem strukturierten Inhalt Leben einzuhauchen. CSS ist ausschließlich für die Präsentation zuständig. Es beantwortet Fragen wie:

- Welche Schriftart soll verwendet werden?
- Welche Farbe hat der Hintergrund?
- Wie groß soll der Abstand zwischen den Absätzen sein?
- Soll der Inhaltsbereich zentriert und auf eine maximale Breite begrenzt werden?
- Wie soll sich das Layout auf einem kleinen Smartphone-Bildschirm im Vergleich zu einem großen Desktop-Monitor verändern?

Nehmen wir unser Käsekuchen-Rezept von oben. Das HTML-Dokument bleibt exakt dasselbe. Wir ändern keinen einzigen Buchstaben daran. Stattdessen erstellen wir eine separate Datei, zum Beispiel `style.css`, und füllen sie mit Stilregeln.

```css
body {
  font-family: 'Helvetica', sans-serif;
  line-height: 1.6;
  background-color: #fdfaf4;
  color: #333;
}

article {
  max-width: 800px;
  margin: 40px auto;
  padding: 20px;
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

h1 {
  color: #c23b22;
  text-align: center;
}

h2 {
  color: #5a5a5a;
  border-bottom: 2px solid #f0e5d8;
  padding-bottom: 5px;
}

ul {
  list-style-type: square;
  padding-left: 20px;
}
```

Wenn wir diese CSS-Datei nun mit unserem HTML-Dokument verknüpfen (normalerweise über ein `<link>`-Element im `<head>` des HTML), verwandelt sich unser schlichtes Rezept augenblicklich. Plötzlich hat es eine angenehme Schriftart, ansprechende Farben, Abstände und sogar einen leichten Schatten, der den Inhaltsbereich vom Hintergrund abhebt. Die Struktur ist dieselbe, aber die Präsentation ist eine völlig andere.

#### Warum diese Trennung so entscheidend ist

Auf den ersten Blick mag diese Trennung wie unnötiger Mehraufwand erscheinen. Warum nicht einfach die Farbe direkt im HTML-Tag festlegen? Die Antwort liegt in den enormen Vorteilen, die diese „Separation of Concerns“ (Trennung der Verantwortlichkeiten) mit sich bringt.

**1. Wartbarkeit und Effizienz**
Stell dir vor, du hast eine Website mit hundert Seiten, und auf jeder Seite sind die Überschriften blau. Wenn du die Farbe nun in Grün ändern möchtest, müsstest du ohne die Trennung jede einzelne der hundert HTML-Dateien öffnen und jede einzelne Überschrift manuell anpassen. Ein Albtraum.

Mit einer zentralen CSS-Datei änderst du an einer einzigen Stelle die Eigenschaft `color` für deine Überschriften von `blue` auf `green`. Du speicherst die Datei, und die Änderung wird sofort auf allen hundert Seiten wirksam. Das spart nicht nur unglaublich viel Zeit, sondern reduziert auch die Fehleranfälligkeit drastisch.

**2. Zugänglichkeit (Accessibility)**
Wie bereits erwähnt, verlassen sich assistive Technologien wie Screenreader auf die saubere, semantische Struktur von HTML. Wenn du beginnst, HTML-Elemente für visuelle Zwecke zu missbrauchen (z.B. eine Überschrift nur deshalb zu verwenden, weil der Text groß und fett sein soll, obwohl er inhaltlich keine Überschrift ist), zerstörst du diese logische Struktur. Für einen sehenden Benutzer mag das egal sein, aber für einen blinden Benutzer wird die Seite unlogisch und schwer zu navigieren. Eine saubere Trennung stellt sicher, dass dein HTML die Bedeutung des Inhalts bewahrt.

**3. SEO (Suchmaschinenoptimierung)**
Suchmaschinen wie Google sind im Grunde genommen blinde, aber sehr intelligente Nutzer. Sie analysieren die HTML-Struktur, um den Inhalt deiner Seite zu verstehen und zu indexieren. Eine klare Hierarchie mit `<h1>`, `<h2>`, `<p>`, Listen und anderen semantischen Tags hilft der Suchmaschine, die Relevanz deines Inhalts für bestimmte Suchanfragen zu bewerten. Sauberes HTML ist die Grundlage für gutes SEO.

**4. Flexibilität und Responsive Design**
Heute greifen Nutzer mit den unterschiedlichsten Geräten auf Websites zu – vom riesigen 4K-Monitor bis zum winzigen Smartphone-Display. Die Trennung von Struktur und Präsentation ist die Voraussetzung für Responsive Webdesign. Der HTML-Inhalt bleibt auf allen Geräten identisch. Lediglich das CSS passt sich an die jeweilige Bildschirmgröße an und ordnet die Elemente anders an, verändert Schriftgrößen oder blendet weniger wichtige Informationen aus. Dies geschieht mithilfe von sogenannten Media Queries in CSS. Du kannst also ein und dasselbe Haus (HTML) für verschiedene Anlässe (Geräte) völlig unterschiedlich dekorieren (CSS).

#### Die Sünden der Vergangenheit

Um zu verstehen, wie wertvoll diese Trennung ist, hilft ein kurzer Blick in die Vergangenheit des Webs. In den frühen Tagen waren HTML und Präsentation wild miteinander vermischt. Es gab HTML-Tags, deren einziger Zweck die visuelle Gestaltung war.

Ein Beispiel für diesen schlechten Stil könnte so aussehen:

```html
<!-- BITTE NICHT NACHMACHEN! DIES IST EIN NEGATIVBEISPIEL. -->
<body bgcolor="#fdfaf4">

  <center>
    <h1><font color="#c23b22" face="Helvetica">Der perfekte Käsekuchen</font></h1>
  </center>
  
  <p><font face="Helvetica" color="#333333">Dieses Rezept ist einfach und gelingt immer...</font></p>
  
  <table width="800" align="center" border="0" cellpadding="20">
    <tr>
      <td>
        <!-- Hier weiterer Inhalt... -->
      </td>
    </tr>
  </table>
  
</body>
```

Du siehst hier Elemente wie `<center>` zum Zentrieren, das `<font>`-Tag zum Festlegen von Schriftart und Farbe sowie Attribute wie `bgcolor` für die Hintergrundfarbe. Schlimmer noch: Oft wurden `<table>`-Elemente für das gesamte Seitenlayout missbraucht. Dieser Code ist nicht nur schwer zu lesen und zu warten, er ist auch für Barrierefreiheit und SEO eine Katastrophe. Glücklicherweise sind diese Tags und Attribute heute veraltet (deprecated) und sollten unter keinen Umständen mehr verwendet werden.

Die moderne Webentwicklung basiert auf dem klaren Prinzip: HTML ist für das *Was* (Inhalt und Struktur) zuständig, CSS ist für das *Wie* (Aussehen und Layout). Wenn du diese Regel verinnerlichst, bist du auf dem besten Weg, professionelle, flexible und zukunftssichere Websites zu erstellen. Sie sind das Fundament und der Anstrich deines digitalen Hauses – zwei Spezialisten, die perfekt zusammenarbeiten, aber ihre Aufgabenbereiche klar voneinander trennen.
