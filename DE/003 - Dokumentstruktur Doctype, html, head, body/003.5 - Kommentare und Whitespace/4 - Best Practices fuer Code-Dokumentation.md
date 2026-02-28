# Best Practices für Code-Dokumentation

### Die Kunst der guten Dokumentation: Kommentare als Wegweiser im Code

Code zu schreiben ist eine Sache. Ihn Monate oder Jahre später noch zu verstehen, eine ganz andere. Hier kommen Kommentare ins Spiel – die kleinen Notizen, die du direkt in deinem Quellcode hinterlässt. Sie sind Wegweiser für andere Entwickler und, was oft noch wichtiger ist, für dein zukünftiges Ich. Doch wie bei jedem Werkzeug kommt es darauf an, wie man es einsetzt. Ein schlecht platzierter oder veralteter Kommentar kann mehr Verwirrung stiften als Klarheit schaffen. In diesem Kapitel erkunden wir die Kunst, deinen HTML-Code so zu dokumentieren, dass er nicht nur heute funktioniert, sondern auch morgen noch verständlich ist.

#### Die goldene Regel: Kommentiere das „Warum“, nicht das „Was“

Die wichtigste Regel für gute Kommentare ist einfach, aber fundamental: Dein Code erklärt bereits, *was* er tut. Deine Aufgabe als Kommentarschreiber ist es, zu erklären, *warum* er es tut. Ein Kommentar, der nur den Code nacherzählt, ist überflüssig und bläht die Datei unnötig auf.

Betrachten wir ein schlechtes Beispiel:

```html
<!-- Ein Absatz mit Text -->
<p>Dies ist ein wichtiger Hinweis für unsere Nutzer.</p>
```

Jeder, der auch nur die Grundlagen von HTML kennt, sieht, dass `<p>` ein Absatz ist. Dieser Kommentar bietet keinerlei Mehrwert. Er ist reines Rauschen.

Ein guter Kommentar hingegen liefert Kontext, den der Code allein nicht vermitteln kann. Er erklärt die Absicht hinter einer Entscheidung oder weist auf eine Besonderheit hin.

Hier ist eine deutlich bessere Variante:

```html
<!-- Dieser Hinweis muss aus rechtlichen Gründen auf jeder Seite sichtbar sein,
     die Produkte aus der Kategorie XY anzeigt. Er darf nicht entfernt werden. -->
<p>Dies ist ein wichtiger Hinweis für unsere Nutzer.</p>
```

Dieser Kommentar ist Gold wert. Er erklärt nicht, *was* ein `<p>`-Tag ist, sondern *warum* dieser spezielle Absatz an dieser Stelle existiert und warum er wichtig ist. Ein neuer Entwickler im Team weiß sofort, dass dieser Code eine besondere Bedeutung hat und nicht leichtfertig geändert werden sollte.

#### Wann und wo solltest du kommentieren?

Nicht jede Zeile Code benötigt einen Kommentar. Ständige Unterbrechungen durch Kommentare können den Lesefluss genauso stören wie gar keine. Es geht darum, die richtigen Stellen zu finden, an denen eine Anmerkung echten Nutzen bringt.

**1. Komplexe oder nicht-intuitive Abschnitte**

Manchmal musst du HTML auf eine Weise schreiben, die nicht sofort offensichtlich ist. Vielleicht ist es ein Workaround für einen Browser-Bug, eine komplexe Verschachtelung für ein bestimmtes CSS-Layout oder eine Struktur, die für Barrierefreiheit optimiert ist. Das sind perfekte Kandidaten für einen Kommentar.

```html
<!-- HINWEIS: Die leeren <span>-Elemente hier sind kein Fehler.
     Sie werden von der CSS-Datei `animations.css` genutzt, um einen
     visuellen "Glitch"-Effekt auf den Buttons zu erzeugen. -->
<button class="glitch-button">
  <span></span>
  Start
  <span></span>
</button>
```

Ohne diesen Kommentar könnte jemand dein „sauberes“ HTML aufräumen und dabei unbeabsichtigt die visuelle Gestaltung zerstören. Der Kommentar schützt den Code vor gut gemeinten, aber falschen Korrekturen.

**2. Temporäre Anmerkungen und TODOs**

Entwicklung ist ein Prozess. Selten ist alles von Anfang an perfekt. Kommentare sind ein hervorragendes Werkzeug, um Platzhalter, offene Aufgaben oder bekannte Probleme zu markieren. Eine gängige Konvention ist die Verwendung von Schlüsselwörtern wie `TODO`, `FIXME` oder `NOTE`, oft gefolgt von deinem Namen oder Kürzel und dem Datum.

```html
<!-- TODO: Die Verlinkung zum Impressum muss noch durch die finale URL ersetzt werden. (Max M. - 2023-10-26) -->
<a href="#">Impressum</a>

<!-- FIXME: Dieser Abschnitt verursacht im Internet Explorer 11 ein Layout-Problem.
     Muss vor dem Livegang untersucht werden. -->
<div class="special-grid-container">
  ...
</div>
```

Solche Kommentare dienen als internes Ticketsystem direkt im Code. Viele Code-Editoren und Entwicklungsumgebungen können diese Schlüsselwörter sogar farblich hervorheben oder eine Liste aller TODOs im Projekt erstellen, was die Organisation enorm erleichtert.

**3. Strukturierung von großen Dokumenten**

Bei sehr langen und komplexen HTML-Dateien können Kommentare helfen, die Struktur visuell zu gliedern. Du kannst sie verwenden, um Anfang und Ende großer, logischer Blöcke zu markieren, wie zum Beispiel den Header, den Hauptinhalt oder den Footer.

```html
<!-- =================================================================== -->
<!-- HEADER START -->
<!-- =================================================================== -->
<header>
  ... (viele Zeilen Code für Navigation, Logo, etc.) ...
</header>
<!-- =================================================================== -->
<!-- HEADER END -->
<!-- =================================================================== -->


<!-- =================================================================== -->
<!-- MAIN CONTENT START -->
<!-- =================================================================== -->
<main>
  ...
</main>
<!-- =================================================================== -->
<!-- MAIN CONTENT END -->
<!-- =================================================================== -->
```

Diese Art der Kommentierung macht es viel einfacher, sich in einer riesigen Datei zurechtzufinden und schnell zum gewünschten Abschnitt zu springen. Es ist wie das Inhaltsverzeichnis eines Buches, direkt in den Code eingebettet.

**4. Auskommentieren von Code**

Eine der häufigsten Anwendungen von Kommentaren ist das temporäre Deaktivieren von Codeblöcken, ohne sie zu löschen. Das ist extrem nützlich beim Testen oder bei der Fehlersuche.

```html
<section class="user-profile">
  <h2>Dein Profil</h2>
  <p>Name: Max Mustermann</p>

  <!-- Das Feature für die Profilbilder ist noch nicht fertig.
       Wird vorübergehend deaktiviert, bis das Backend bereit ist. -->
  <!--
  <div class="profile-picture-uploader">
    <label for="avatar">Profilbild hochladen:</label>
    <input type="file" id="avatar" name="avatar">
  </div>
  -->
</section>
```

Hier wird ein ganzes `div`-Element mitsamt Inhalt auskommentiert. Der Browser ignoriert diesen Block vollständig, aber der Code bleibt für die spätere Reaktivierung erhalten. Ein kurzer Kommentar, der erklärt, warum der Code auskommentiert wurde, ist hier ebenfalls eine gute Praxis.

#### Die Anatomie eines guten Kommentars

Neben dem *Was* und *Wo* ist auch das *Wie* entscheidend. Ein guter Kommentar ist:

*   **Klar und präzise:** Vermeide lange, umständliche Sätze. Komm direkt auf den Punkt. Ein guter Kommentar sollte in wenigen Sekunden lesbar und verständlich sein.
*   **Konsistent:** Entscheide dich für einen Stil und bleibe dabei. Schreibst du Kommentare auf Deutsch oder Englisch? Beginnt jeder Satz mit einem Großbuchstaben? Setzt du am Ende einen Punkt? Einheitlichkeit im gesamten Projekt erleichtert das Lesen erheblich.
*   **Gepflegt und aktuell:** Der vielleicht größte Fehler bei der Code-Dokumentation ist, sie veralten zu lassen. Ein Kommentar, der eine nicht mehr existierende Logik beschreibt, ist schlimmer als gar kein Kommentar. Er führt Entwickler auf die falsche Fährte und untergräbt das Vertrauen in die gesamte Dokumentation. Wenn du Code änderst, überprüfe immer, ob die dazugehörigen Kommentare noch zutreffen, und passe sie bei Bedarf an. Behandle Kommentare wie einen integralen Bestandteil deines Codes.

#### Kommentare in HTML, CSS und JavaScript

Während die Prinzipien guter Dokumentation universell sind, unterscheidet sich die Syntax von Sprache zu Sprache. Im Kontext der Webentwicklung wirst du hauptsächlich mit diesen drei zu tun haben:

**HTML:**
Kommentare beginnen mit `<!--` und enden mit `-->`. Sie können sich über mehrere Zeilen erstrecken.

```html
<!-- Dies ist ein mehrzeiliger
     HTML-Kommentar. -->
```

**CSS:**
In CSS werden Kommentare mit `/*` eingeleitet und mit `*/` beendet. Auch sie können mehrzeilig sein.

```css
/*
  Dieser CSS-Block definiert das grundlegende
  Aussehen aller Buttons auf der Website.
*/
.button {
  background-color: #007bff;
  color: white; /* Textfarbe auf Weiß setzen */
}
```

**JavaScript:**
JavaScript bietet zwei Arten von Kommentaren:
1.  Einzeilige Kommentare, die mit `//` beginnen.
2.  Mehrzeilige Kommentare, die wie in CSS mit `/*` und `*/` umschlossen werden.

```javascript
// Berechnet die Summe von zwei Zahlen.
function add(a, b) {
  /*
    Diese Funktion ist ein zentraler Bestandteil
    unserer Berechnungslogik. Bitte mit Vorsicht ändern.
  */
  return a + b;
}
```

Code-Dokumentation ist kein lästiges Übel, sondern ein Zeichen von Professionalität und Voraussicht. Sie ist eine Investition in die Zukunft deines Projekts. Gut kommentierter Code ist leichter zu warten, einfacher zu erweitern und macht die Zusammenarbeit im Team deutlich angenehmer. Betrachte jeden Kommentar als eine freundliche Nachricht an die Person, die diesen Code als Nächstes bearbeiten wird – und sei dir bewusst, dass diese Person sehr wahrscheinlich du selbst sein wirst.
