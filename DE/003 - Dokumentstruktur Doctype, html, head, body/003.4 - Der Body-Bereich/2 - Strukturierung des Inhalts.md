# Strukturierung des Inhalts

### Strukturierung des Inhalts

Stell dir vor, du öffnest ein Buch, bei dem der gesamte Text in einem einzigen, riesigen Absatz ohne Überschriften, Absätze oder Kapitel gedruckt ist. Es wäre eine Qual, darin zu lesen, geschweige denn, bestimmte Informationen zu finden. Was dieses Buch unlesbar macht, ist das Fehlen von Struktur. Genau wie ein Buch oder ein Zeitungsartikel benötigt auch eine Webseite eine klare, logische Struktur, damit ihre Inhalte verständlich sind – und das nicht nur für menschliche Besucher, sondern auch für Maschinen.

Der `<body>`-Bereich deines HTML-Dokuments ist die Bühne, auf der dein gesamter sichtbarer Inhalt präsentiert wird. Aber einfach nur Text und Bilder hineinzuschreiben, reicht nicht aus. Die Kunst besteht darin, diesen Inhalt mit den richtigen HTML-Elementen so zu gliedern, dass er eine Bedeutung erhält. Diese Praxis nennen wir semantische Auszeichnung. Semantik bedeutet hier, dass die von dir verwendeten HTML-Tags dem Inhalt eine Bedeutung verleihen. Ein `<h1>`-Tag sagt zum Beispiel nicht nur: „Mach diesen Text groß und fett“, sondern: „Das ist die Hauptüberschrift dieser Seite.“

Diese semantische Struktur ist aus zwei entscheidenden Gründen von unschätzbarem Wert:

1.  **Für Menschen:** Eine gute Struktur führt den Blick des Lesers. Überschriften lassen Inhalte schnell überfliegen (scannen), Absätze gliedern Gedanken, und Listen machen Aufzählungen übersichtlich. Menschen mit Sehbehinderungen, die auf Screenreader angewiesen sind, können dank einer sauberen Struktur von Überschrift zu Überschrift springen und so eine Seite effizient navigieren, anstatt sich Wort für Wort durch eine Textwüste kämpfen zu müssen.
2.  **Für Maschinen:** Suchmaschinen wie Google analysieren die Struktur deiner Seite, um deren Inhalt und Relevanz zu verstehen. Eine Hauptüberschrift (`<h1>`) hat für sie mehr Gewicht als eine Unterüberschrift (`<h2>`). Klar definierte Abschnitte helfen der Suchmaschine, die thematischen Schwerpunkte deiner Seite zu erkennen. Dies hat direkten Einfluss auf dein Suchmaschinenranking (SEO).

#### Die Grundbausteine: Überschriften und Absätze

Die fundamentalsten Werkzeuge zur Gliederung von Text sind Überschriften und Absätze.

**Überschriften (`<h1>` bis `<h6>`)**
HTML stellt dir sechs Ebenen von Überschriften zur Verfügung, von `<h1>` (die wichtigste) bis `<h6>` (die unwichtigste). Stell sie dir wie die Gliederung in einem Dokument vor:

*   `<h1>`: Der Titel des gesamten Dokuments. Es sollte pro Seite nur eine einzige `<h1>` geben.
*   `<h2>`: Ein Hauptkapitel oder ein wichtiger Abschnitt.
*   `<h3>`: Ein Unterkapitel oder ein Unterabschnitt von `<h2>`.
*   `<h4>` bis `<h6>`: Weitere Unterteilungen.

Das Wichtigste dabei ist die Hierarchie. Du solltest niemals eine Ebene überspringen, nur weil dir das Aussehen einer bestimmten Überschrift besser gefällt. Springe also nicht von einer `<h2>` direkt zu einer `<h4>`. Das Aussehen steuerst du später ohnehin mit CSS. Die HTML-Struktur muss logisch korrekt bleiben.

```html
<body>
  <h1>Die faszinierende Welt der Honigbiene</h1>
  <p>Eine Einführung in das Leben und die Organisation eines Bienenstaates.</p>
  
  <h2>Der Bienenstaat: Eine perfekte Organisation</h2>
  <p>Ein Bienenvolk besteht aus Zehntausenden von Individuen, die perfekt zusammenarbeiten.</p>
  
  <h3>Die Königin</h3>
  <p>Die einzige Aufgabe der Königin ist das Legen von Eiern.</p>
  
  <h3>Die Arbeiterinnen</h3>
  <p>Arbeiterinnen übernehmen alle anderen Aufgaben im Stock.</p>
  
  <h2>Die Kommunikation: Der Schwänzeltanz</h2>
  <p>Bienen nutzen einen komplexen Tanz, um Futterquellen zu kommunizieren.</p>
</body>
```

**Absätze (`<p>`)**
Das `<p>`-Element (für Paragraph) ist das Arbeitspferd für Fließtext. Es umschließt einen thematisch zusammenhängenden Textblock und erzeugt automatisch einen visuellen Abstand zum nächsten Element. Verwende es für jeden Textabsatz. Versuche niemals, Absätze durch mehrere `<br>`-Tags (Zeilenumbrüche) zu simulieren. Ein `<p>`-Tag gibt dem Text eine semantische Bedeutung – „dies ist ein Absatz“ –, während `<br>` nur ein reiner, bedeutungsloser Zeilenumbruch ist.

#### Gruppen bilden: Semantische Sektionen

Während Überschriften und Absätze einzelne Textblöcke strukturieren, helfen dir Sektionierungs-Elemente dabei, deine gesamte Seite in größere, logische Bereiche aufzuteilen. Vor der Einführung von HTML5 nutzte man dafür fast ausschließlich das universelle `<div>`-Element. Ein `<div>` ist ein generischer Container ohne eigene semantische Bedeutung. Er sagt nur: „Hier beginnt eine Gruppe von Elementen.“ Das ist immer noch nützlich, um Elemente für Styling-Zwecke (mit CSS) oder für Funktionalität (mit JavaScript) zu bündeln.

HTML5 hat jedoch eine Reihe von Elementen eingeführt, die `<div>`s in vielen Fällen ersetzen und dem Browser sowie Suchmaschinen genau sagen, welche Art von Inhalt sich in einem Bereich befindet.

**`<header>`**
Das `<header>`-Element repräsentiert eine Gruppe von einleitenden oder navigatorischen Hilfsmitteln. Es enthält typischerweise das Logo der Website, den Seitentitel (`<h1>`) und die Hauptnavigation. Wichtig: Verwechsle es nicht mit dem `<head>`-Tag! Der `<head>`-Bereich enthält unsichtbare Metadaten, während der `<header>`-Inhalt sichtbar auf der Seite erscheint. Ein `<header>` kann für die gesamte Seite, aber auch für einen kleineren Abschnitt wie einen `<article>` verwendet werden.

**`<nav>`**
Das `<nav>`-Element ist speziell für die Hauptnavigationsblöcke deiner Seite gedacht. Hier platzierst du die wichtigsten Links, die den Benutzer durch deine Website führen, wie zum Beispiel „Home“, „Über uns“ oder „Kontakt“.

**`<main>`**
Dieses Element ist von zentraler Bedeutung. Es umschließt den Hauptinhalt deines Dokuments. Der Inhalt innerhalb von `<main>` sollte einzigartig für diese spezifische Seite sein und sich nicht auf anderen Seiten wiederholen (wie es bei Kopf- und Fußzeilen der Fall ist). Es darf pro Seite nur ein einziges `<main>`-Element geben.

**`<article>`**
Ein `<article>`-Element umschließt einen in sich geschlossenen, unabhängigen Inhalt, der potenziell auch außerhalb der Seite Sinn ergeben würde – zum Beispiel in einem RSS-Feed. Typische Beispiele sind ein Blogbeitrag, ein Zeitungsartikel, ein Forenpost oder ein Produkt in einem Online-Shop.

**`<section>`**
Das `<section>`-Element gruppiert thematisch zusammengehörige Inhalte. Der entscheidende Unterschied zu einem `<article>` ist, dass der Inhalt einer `<section>` nicht zwangsläufig für sich allein stehen kann. Eine `<section>` ist eher wie ein Kapitel in einem Buch. Eine Faustregel besagt: Wenn du den Inhalt sinnvoll mit einer Überschrift versehen kannst, ist `<section>` oft die richtige Wahl. So könnte ein `<article>` über ein Land verschiedene `<section>`s für „Geschichte“, „Geografie“ und „Kultur“ enthalten.

**`<aside>`**
Das `<aside>`-Element ist für Inhalte gedacht, die nur am Rande mit dem Hauptinhalt zu tun haben. Stell es dir wie eine Randnotiz in einem Buch vor. Typische Beispiele sind eine Sidebar mit weiterführenden Links, eine Autorenbiografie am Ende eines Artikels oder Werbeblöcke.

**`<footer>`**
Ähnlich wie der `<header>` markiert der `<footer>` den Fußbereich eines Abschnitts. Für die gesamte Seite enthält er oft Copyright-Informationen, Links zu Datenschutzrichtlinien oder Kontaktinformationen. Ein `<footer>` kann aber auch am Ende eines `<article>` stehen und dort zum Beispiel den Autor und das Veröffentlichungsdatum nennen.

#### Ein praktisches Beispiel

Sehen wir uns an, wie diese Elemente zusammen eine gut strukturierte Seite ergeben. Stell dir eine einfache Blog-Seite vor:

```html
<body>

  <header>
    <img src="logo.png" alt="Mein Blog Logo">
    <nav>
      <ul>
        <li><a href="/">Startseite</a></li>
        <li><a href="/ueber-mich">Über mich</a></li>
        <li><a href="/kontakt">Kontakt</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <header>
        <h1>HTML-Struktur ist der Schlüssel zum Erfolg</h1>
        <p>Veröffentlicht am 24. Oktober 2023 von Alex</p>
      </header>
      
      <section>
        <h2>Warum Semantik wichtig ist</h2>
        <p>Semantisches HTML hilft nicht nur Suchmaschinen, sondern verbessert auch die Barrierefreiheit für alle Nutzer...</p>
      </section>
      
      <section>
        <h2>Die wichtigsten Strukturelemente</h2>
        <p>Werfen wir einen Blick auf die Bausteine wie header, main, footer und article...</p>
      </section>
      
      <footer>
        <p>Kategorien: Webentwicklung, HTML</p>
      </footer>
    </article>
    
    <aside>
      <h3>Neueste Beiträge</h3>
      <ul>
        <li><a href="#">CSS-Grid verstehen</a></li>
        <li><a href="#">Einstieg in JavaScript</a></li>
      </ul>
    </aside>
  </main>

  <footer>
    <p>&copy; 2023 Mein Blog. Alle Rechte vorbehalten.</p>
  </footer>

</body>
```

In diesem Beispiel siehst du die klare Gliederung: Ein globaler `<header>` mit Logo und Navigation, ein `<footer>` mit dem Copyright. Das `<main>`-Element umschließt den einzigartigen Inhalt, der aus dem Haupt-`<article>` und einer `<aside>`-Sidebar besteht. Der Artikel selbst ist wiederum mit einem eigenen `<header>`, mehreren `<section>`s und einem `<footer>` strukturiert.

Diese Struktur ist das Fundament, auf dem alles Weitere aufbaut. Bevor du auch nur eine Zeile CSS schreibst, um deine Seite schön zu machen, oder JavaScript, um sie interaktiv zu gestalten, muss die semantische HTML-Struktur stehen. Sie ist das stabile Skelett, das deinem Inhalt Form, Bedeutung und Zugänglichkeit verleiht.
