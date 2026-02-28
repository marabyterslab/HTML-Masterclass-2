# Semantik-Check

### Der Semantik-Check: Die Bedeutung hinter den Tags

Wenn du einen Code-Review durchführst, ist einer der ersten und einfachsten Schritte, den Code durch einen Validator zu jagen. Ein Validator prüft, ob dein HTML syntaktisch korrekt ist – also ob alle Tags geschlossen sind, Attribute richtig geschrieben sind und die Dokumentenstruktur den formalen Regeln des W3C entspricht. Das ist wichtig, aber es ist nur die halbe Miete.

Ein Validator ist eine Maschine. Er kann dir nicht sagen, ob du das *richtige* Tag für den *richtigen Zweck* verwendet hast. Er kann nicht beurteilen, ob deine Webseite für einen Screenreader-Nutzer verständlich oder für eine Suchmaschine logisch aufgebaut ist. Genau hier kommst du als menschlicher Reviewer ins Spiel: beim Semantik-Check. Semantik ist die Lehre von der Bedeutung. In HTML bedeutet das, Elemente so zu verwenden, wie es ihre Spezifikation vorsieht, um dem Inhalt eine Struktur und einen Sinn zu geben.

Ein semantischer Check fragt nicht: „Ist dieser Code gültig?“, sondern: „Ist dieser Code sinnvoll?“. Es geht darum, die Intention hinter dem Code zu verstehen und sicherzustellen, dass das gewählte HTML diese Intention bestmöglich transportiert.

#### Die Hierarchie der Überschriften

Einer der häufigsten semantischen Fehler betrifft Überschriften (`<h1>` bis `<h6>`). Viele Entwickler wählen Überschriften basierend auf ihrem Aussehen aus – `<h3>` sieht vielleicht passender aus als `<h2>` – und passen das Styling dann per CSS an. Das ist ein fundamentaler Fehler.

Überschriften definieren die Gliederung deines Dokuments, ähnlich wie ein Inhaltsverzeichnis in einem Buch. Sie sind entscheidend für die Navigation, sowohl für Suchmaschinen als auch für Nutzer von assistiven Technologien wie Screenreadern, die oft von Überschrift zu Überschrift springen, um sich einen Überblick zu verschaffen.

Bei einem Review solltest du folgende Regeln prüfen:

1.  **Es gibt nur eine `<h1>` pro Seite.** Die `<h1>` ist der Haupttitel des Dokuments. Sie sollte den Inhalt der gesamten Seite zusammenfassen. Mehrere `<h1>`-Tags verwirren sowohl Maschinen als auch Menschen.
2.  **Die Hierarchie wird eingehalten.** Auf eine `<h2>` folgt entweder eine weitere `<h2>` auf derselben Ebene oder eine `<h3>` auf der nächsttieferen Ebene. Überspringe niemals Ebenen, zum Beispiel von einer `<h2>` direkt zu einer `<h4>`.

Schau dir dieses Beispiel an:

```html
<!-- Schlecht: Überschriften werden für das Styling missbraucht -->
<h1>Mein fantastischer Online-Shop</h1>
<h3>Bestseller</h3>
<p>Hier sind unsere Top-Produkte...</p>
<h3>Neuheiten</h3>
<p>Gerade frisch eingetroffen...</p>
```

Der Code ist zwar valide, aber semantisch falsch. Die Hierarchie wird von `<h1>` zu `<h3>` übersprungen. Ein Screenreader-Nutzer würde sich fragen, wo die `<h2>`-Ebene geblieben ist.

So wäre es richtig:

```html
<!-- Gut: Logische und korrekte Überschriftenhierarchie -->
<h1>Mein fantastischer Online-Shop</h1>
<h2>Bestseller</h2>
<p>Hier sind unsere Top-Produkte...</p>
<h2>Neuheiten</h2>
<p>Gerade frisch eingetroffen...</p>
```

#### Landmarks: Die Gliederung deiner Seite

Mit HTML5 wurden sogenannte Landmark-Elemente eingeführt, die den großen Bereichen einer Webseite eine klare semantische Bedeutung geben. Vorher bestand eine Seite oft aus einem Meer von `<div>`-Elementen mit IDs wie `id="header"`, `id="main-content"` oder `id="footer"`.

```html
<!-- Veraltet: Die sogenannte "div-itis" -->
<div id="header">...</div>
<div id="nav">...</div>
<div id="main">
  <div class="content">...</div>
  <div class="sidebar">...</div>
</div>
<div id="footer">...</div>
```

Moderne, semantische HTML-Strukturen nutzen dafür die vorgesehenen Tags. Sie machen den Code nicht nur lesbarer, sondern ermöglichen es Browsern und assistiven Technologien, direkt zu wichtigen Abschnitten zu springen.

Prüfe bei einem Review, ob diese Elemente korrekt verwendet werden:

*   `<header>`: Für den Kopfbereich der Seite oder eines Abschnitts (oft mit Logo, Hauptnavigation).
*   `<nav>`: Speziell für die Hauptnavigationsblöcke.
*   `<main>`: Umschließt den einzigartigen Hauptinhalt der Seite. Es sollte nur ein `<main>`-Element pro Seite geben.
*   `<aside>`: Für Inhalte, die nur lose mit dem Hauptinhalt in Verbindung stehen, wie eine Seitenleiste mit weiterführenden Links oder Werbung.
*   `<footer>`: Für den Fußbereich der Seite oder eines Abschnitts (oft mit Copyright, Kontaktinformationen, Links zum Impressum).
*   `<section>`: Gruppiert thematisch zusammengehörige Inhalte. Eine `section` sollte fast immer eine eigene Überschrift haben.
*   `<article>`: Für in sich geschlossene, eigenständige Inhalte, die potenziell syndiziert werden könnten (z. B. ein Blogbeitrag, ein Forenpost, ein Produkt in einer Liste).

So sieht die moderne Variante aus:

```html
<!-- Gut: Klare Struktur mit semantischen HTML5-Tags -->
<header>...</header>
<nav>...</nav>
<main>
  <article>...</article>
  <aside>...</aside>
</main>
<footer>...</footer>
```

Achte darauf, dass nicht einfach jeder `<div>` durch ein `<section>` ersetzt wird. Eine `section` impliziert eine thematische Gruppierung. Ein reiner Styling-Container sollte weiterhin ein `<div>` bleiben.

#### Buttons vs. Links: Eine Frage der Aktion

Dies ist einer der kritischsten Punkte für die Barrierefreiheit und Benutzerfreundlichkeit. Die Regel ist einfach, wird aber oft missachtet:

*   Ein Link (`<a>`) navigiert den Nutzer zu einer neuen Seite oder zu einem anderen Teil der aktuellen Seite (Ankerlink).
*   Ein Button (`<button>`) löst eine Aktion auf der *aktuellen* Seite aus (z. B. ein Formular absenden, ein Modal öffnen, einen Mediaplayer starten).

Sehr oft sieht man Konstrukte wie diese:

```html
<!-- Schlecht: Ein div, das sich als Button ausgibt -->
<div class="button" onclick="openModal()">Mehr erfahren</div>

<!-- Schlecht: Ein Link, der keine Navigation auslöst -->
<a href="#" onclick="submitForm()">Formular absenden</a>
```

Diese Ansätze sind aus mehreren Gründen problematisch:

1.  **Nicht per Tastatur erreichbar:** Ein `<div>` ist standardmäßig nicht fokussierbar. Ein Nutzer, der nur mit der Tastatur navigiert, kann es nicht erreichen. Man müsste `tabindex="0"` hinzufügen, was aber weitere Probleme nach sich zieht.
2.  **Falsche Semantik für Screenreader:** Ein Screenreader liest bei einem `<a>`-Tag „Link“ vor und bei einem `<button>`-Tag „Schaltfläche“. Ein `<div>` ist einfach nur ein `<div>`. Der Nutzer weiß nicht, dass er damit interagieren kann.
3.  **Fehlendes Browser-Verhalten:** Ein `<button>`-Element kann per Leertaste oder Enter-Taste ausgelöst werden. Ein `<a>`-Tag nur per Enter. Ein `<div>` gar nicht. Dieses erwartete Verhalten geht verloren.

Im Review solltest du darauf bestehen, dass die korrekten Elemente verwendet werden:

```html
<!-- Gut: Ein Button für eine Aktion auf der Seite -->
<button type="button" onclick="openModal()">Mehr erfahren</button>

<!-- Gut: Ein Link, der zu einer neuen Seite führt -->
<a href="/ueber-uns.html">Über uns</a>
```

#### Textauszeichnung mit Bedacht

Ähnlich wie bei Überschriften werden auch Textauszeichnungen wie `<b>` und `<i>` oft rein aus stilistischen Gründen gewählt. Die semantischen Alternativen sind jedoch `<strong>` und `<em>`.

*   `<strong>`: Kennzeichnet Text von großer Wichtigkeit, Dringlichkeit oder Ernsthaftigkeit. Screenreader heben diesen Text oft durch eine andere Stimmlage hervor.
*   `<b>` (Bring Attention To): Zieht die Aufmerksamkeit auf Text, ohne ihm eine besondere Wichtigkeit zu verleihen. Geeignet für Produktnamen in einem Fließtext oder Schlüsselwörter in einer Zusammenfassung.
*   `<em>` (Emphasis): Betont ein Wort oder einen Satz, was die Bedeutung des Satzes verändern kann. Screenreader ändern hier ebenfalls die Betonung.
*   `<i>` (Idiomatic Text): Kennzeichnet Text, der sich vom Rest abhebt, wie ein Fachbegriff, ein Gedanke oder ein Wort in einer anderen Sprache.

Die Faustregel lautet: Wenn du den Text fett oder kursiv darstellen willst, um eine *Bedeutung* zu transportieren (Wichtigkeit, Betonung), nutze `<strong>` oder `<em>`. Wenn es rein um die visuelle Darstellung geht, ohne dass eine tiefere Bedeutung impliziert wird, sind `<b>` und `<i>` in Ordnung – obwohl man in vielen Fällen die Auszeichnung besser direkt im CSS vornimmt.

#### Bilder und ihre Alternativtexte

Jedes `<img>`-Element, das eine Information transportiert, *muss* ein `alt`-Attribut haben. Dieses Attribut ist kein Ort für SEO-Keywords, sondern eine Beschreibung des Bildinhalts für Nutzer, die das Bild nicht sehen können.

Beim Review von `alt`-Texten solltest du auf Folgendes achten:

1.  **Ist das Attribut vorhanden?** Ein fehlendes `alt`-Attribut ist fast immer ein Fehler.
2.  **Beschreibt der Text das Bild?** `alt="Foto von einem Hund"` ist schlecht. `alt="Ein goldener Retriever jagt einem roten Ball auf einer grünen Wiese nach."` ist gut. Der Text sollte den *Inhalt und Zweck* des Bildes wiedergeben.
3.  **Ist das Bild rein dekorativ?** Wenn ein Bild nur zur Zierde dient und keinerlei Information transportiert (z. B. eine geschwungene Trennlinie), sollte das `alt`-Attribut leer gelassen werden: `alt=""`. Das ist wichtig! Ein leeres `alt`-Attribut signalisiert einem Screenreader: „Dieses Bild kannst du ignorieren.“ Ein fehlendes Attribut führt dazu, dass der Screenreader stattdessen versucht, den Dateinamen (`IMG_8472.jpg`) vorzulesen, was sehr störend ist.
4.  **Ist das Bild ein Link?** Wenn ein `<img>`-Tag von einem `<a>`-Tag umschlossen ist, sollte der `alt`-Text nicht das Bild beschreiben, sondern das Ziel des Links. `alt="Zur Startseite"` ist hier besser als `alt="Firmenlogo"`.

Ein guter Semantik-Check geht weit über das hinaus, was Maschinen leisten können. Er erfordert Empathie für den Nutzer und ein tiefes Verständnis dafür, wie HTML-Strukturen von Browsern, Suchmaschinen und assistiven Technologien interpretiert werden. Indem du diese Punkte in deinen Code-Reviews berücksichtigst, trägst du maßgeblich dazu bei, dass das Web für alle zugänglicher, verständlicher und robuster wird.
