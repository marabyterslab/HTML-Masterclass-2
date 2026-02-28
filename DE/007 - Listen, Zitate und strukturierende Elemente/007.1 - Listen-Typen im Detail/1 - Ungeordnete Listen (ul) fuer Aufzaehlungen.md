# Ungeordnete Listen (ul) für Aufzählungen

### Ungeordnete Listen (`<ul>`) für Aufzählungen

Stell dir vor, du schreibst eine Einkaufsliste. Du notierst schnell, was du brauchst: Milch, Eier, Brot, Butter. Spielt es eine Rolle, in welcher Reihenfolge du diese Dinge aufschreibst? Nein, überhaupt nicht. Du könntest zuerst die Eier aufschreiben oder das Brot. Das Ziel bleibt dasselbe: am Ende alles im Einkaufswagen zu haben.

Genau für solche Fälle, in denen die Reihenfolge der Elemente keine Rolle spielt, wurde in HTML die ungeordnete Liste geschaffen. Das `<ul>`-Tag, eine Abkürzung für „Unordered List“, ist das perfekte Werkzeug, um eine Sammlung von zusammengehörigen Punkten zu gruppieren, deren Abfolge willkürlich ist.

#### Die grundlegende Struktur

Eine ungeordnete Liste besteht immer aus zwei Arten von Tags, die untrennbar zusammengehören:

1.  **Das `<ul>`-Element:** Dies ist der Container, der die gesamte Liste umschließt. Es signalisiert dem Browser und anderen Systemen wie Screenreadern: „Achtung, hier beginnt eine Liste von Punkten, deren Reihenfolge nicht von Bedeutung ist.“
2.  **Das `<li>`-Element:** Jedes einzelne Element innerhalb der Liste wird von einem `<li>`-Tag (für „List Item“) umschlossen. Du kannst so viele `<li>`-Elemente in ein `<ul>`-Element packen, wie du benötigst.

Sehen wir uns die Einkaufsliste von vorhin als HTML-Code an:

```html
<ul>
  <li>Milch</li>
  <li>Eier</li>
  <li>Brot</li>
  <li>Butter</li>
</ul>
```

Das ist schon alles. Die Struktur ist logisch und einfach nachzuvollziehen. Das `<ul>`-Tag bildet den Rahmen, und jedes `<li>` ist ein klar definierter Punkt innerhalb dieses Rahmens. Wenn du diese Liste in einem Webbrowser anzeigst, wird er sie standardmäßig mit Aufzählungspunkten (meist ausgefüllten Kreisen) darstellen, um die Zusammengehörigkeit der Elemente visuell zu unterstreichen.

Es ist wichtig zu verstehen, dass diese Aufzählungspunkte eine reine Stilentscheidung des Browsers sind. Die eigentliche Magie von HTML liegt in der *semantischen* Bedeutung. Du teilst der Maschine mit, dass es sich hier um eine Gruppe von gleichwertigen Elementen handelt. Wie diese Gruppe am Ende aussieht, ist eine Frage des Designs, die später mit CSS geklärt wird.

#### Listen verschachteln für mehr Struktur

Manchmal sind Listen komplexer. Vielleicht möchtest du deine Einkaufsliste nach Kategorien organisieren, zum Beispiel in „Milchprodukte“ und „Backwaren“. Auch das ist mit ungeordneten Listen problemlos möglich. Du kannst Listen ineinander verschachteln.

Dabei gibt es eine entscheidende Regel, die du unbedingt beachten musst: **Eine neue Liste (`<ul>`) darf niemals direkt innerhalb einer anderen Liste (`<ul>`) stehen. Stattdessen muss sie immer innerhalb eines Listenelements (`<li>`) platziert werden.**

Warum ist das so? Denk logisch darüber nach: Die Unterliste gehört konzeptionell zu einem bestimmten Punkt der übergeordneten Liste. Die Kategorie „Milchprodukte“ ist ein Punkt auf deiner Haupteinkaufsliste, und die spezifischen Produkte wie Milch und Butter sind Teil dieser Kategorie.

Hier ist das korrekte Beispiel für eine verschachtelte Liste:

```html
<ul>
  <li>Milchprodukte
    <ul>
      <li>Milch</li>
      <li>Butter</li>
      <li>Joghurt</li>
    </ul>
  </li>
  <li>Backwaren
    <ul>
      <li>Brot</li>
      <li>Brötchen</li>
    </ul>
  </li>
  <li>Obst</li>
</ul>
```

In diesem Code siehst du, dass die inneren `<ul>`-Elemente Kinder der `<li>`-Elemente „Milchprodukte“ und „Backwaren“ sind. Das ist valider und semantisch korrekter HTML. Der Browser spiegelt diese Hierarchie auch visuell wider. Standardmäßig ändert er oft das Symbol für die Aufzählungspunkte mit jeder Verschachtelungsebene – zum Beispiel von einem ausgefüllten Kreis (disc) zu einem nicht ausgefüllten Kreis (circle) und dann zu einem Quadrat (square). Auch hier gilt: Das ist nur eine visuelle Voreinstellung, die du mit CSS vollständig kontrollieren kannst.

Ein häufiger Fehler wäre, den Code so zu schreiben:

```html
<!-- FALSCHES BEISPIEL! NICHT NACHMACHEN! -->
<ul>
  <li>Milchprodukte</li>
  <ul>
    <li>Milch</li>
    <li>Butter</li>
  </ul>
  <li>Backwaren</li>
</ul>
```

Dieser Code ist ungültig, da ein `<ul>` nur `<li>`-Elemente als direkte Kinder enthalten darf.

#### Semantik und Barrierefreiheit: Warum `<ul>` so wichtig ist

Du könntest versucht sein, eine Liste einfach mit Absätzen (`<p>`) und einem Bindestrich oder Sternchen am Anfang jeder Zeile zu simulieren. Visuell mag das Ergebnis ähnlich aussehen, aber semantisch und für die Barrierefreiheit wäre es eine Katastrophe.

Wenn ein Screenreader – eine Software, die blinden oder sehbehinderten Menschen Webinhalte vorliest – auf ein `<ul>`-Element trifft, kündigt er dies an. Der Nutzer erfährt: „Liste mit 3 Einträgen“. Er erhält sofort den Kontext, dass eine Gruppe von zusammengehörigen Informationen folgt. Bei der Navigation durch die Liste weiß er immer, bei welchem Punkt von wie vielen er sich befindet („Eintrag 2 von 3“).

Würdest du stattdessen nur Textzeilen mit Bindestrichen verwenden, würde der Screenreader diese einfach als separate Textabschnitte ohne jeglichen Zusammenhang vorlesen. Der wichtige Kontext der Gruppierung ginge vollständig verloren. Die korrekte Verwendung von `<ul>` ist also kein optionales Extra, sondern ein fundamentaler Baustein für ein zugängliches und maschinenlesbares Web.

#### Der häufigste Anwendungsfall: Navigationsmenüs

Einer der verbreitetsten und wichtigsten Anwendungsfälle für ungeordnete Listen hat auf den ersten Blick gar nichts mit klassischen Aufzählungen zu tun: Navigationsmenüs.

Denk an die Hauptnavigation einer Webseite. Sie besteht aus einer Sammlung von Links: „Startseite“, „Über uns“, „Produkte“, „Kontakt“. Gibt es eine zwingend logische Reihenfolge? Nicht wirklich. Es ist eine Sammlung von Navigationspunkten. Daher ist eine ungeordnete Liste die semantisch perfekte Wahl, um ein solches Menü zu strukturieren.

Ein typisches Navigationsmenü im HTML-Code sieht so aus:

```html
<nav>
  <ul>
    <li><a href="/">Startseite</a></li>
    <li><a href="/produkte/">Produkte</a></li>
    <li><a href="/ueber-uns/">Über uns</a></li>
    <li><a href="/kontakt/">Kontakt</a></li>
  </ul>
</nav>
```

„Aber Moment mal“, sagst du jetzt vielleicht, „eine Navigation sieht doch ganz anders aus! Die Links stehen nebeneinander, haben keine Aufzählungspunkte und verändern ihre Farbe, wenn man mit der Maus darüberfährt.“

Das ist absolut richtig. Und hier zeigt sich die ganze Stärke der Trennung von Inhalt (HTML) und Präsentation (CSS). Mit HTML gibst du dem Menü seine logische, semantische Struktur: eine Liste von Links. Mit CSS nimmst du diese Liste und gestaltest sie nach Belieben. Du kannst die Aufzählungspunkte entfernen (`list-style-type: none;`), die Listenelemente nebeneinander anordnen (`display: flex;`) und ihnen jedes erdenkliche Aussehen verleihen.

Die Grundlage bleibt aber immer eine saubere, semantische HTML-Struktur. Diese Vorgehensweise stellt sicher, dass deine Navigation nicht nur für sehende Benutzer mit einer Maus funktioniert, sondern auch für Suchmaschinen, Screenreader und andere Systeme, die auf die logische Struktur deiner Seite angewiesen sind.

Ob für eine einfache Liste von Features, eine Sammlung von Blog-Tags oder das Hauptmenü deiner Webseite – die ungeordnete Liste ist ein flexibles, semantisch reiches und unverzichtbares Werkzeug in deinem HTML-Baukasten.
