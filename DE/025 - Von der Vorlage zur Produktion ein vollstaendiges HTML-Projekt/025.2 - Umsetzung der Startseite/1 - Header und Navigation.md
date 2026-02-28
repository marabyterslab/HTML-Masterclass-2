# Header und Navigation

### Header und Navigation: Der erste Eindruck zählt

Wenn ein Besucher auf deine Webseite kommt, ist der Header das Erste, was er sieht. Er ist das digitale Willkommensschild, der erste Händedruck und der Wegweiser in einem. In diesem Bereich, der typischerweise ganz oben auf jeder Seite platziert ist, finden sich die wichtigsten Elemente deiner Markenidentität und die zentrale Navigation. Eine gut durchdachte Kopfzeile schafft Vertrauen, erleichtert die Orientierung und prägt den gesamten Eindruck deiner Online-Präsenz. Deshalb ist es entscheidend, diesen Bereich nicht nur funktional, sondern auch semantisch korrekt mit HTML aufzubauen.

#### Das `<header>`-Element: Mehr als nur der obere Rand

In HTML gibt es ein spezielles Element, das genau für diesen Zweck geschaffen wurde: das `<header>`-Element. Es ist wichtig zu verstehen, dass `<header>` nicht nur ein beliebiger Container ist, den man am oberen Rand der Seite platziert. Es ist ein semantisches Element, das dem Browser und assistiven Technologien wie Screenreadern mitteilt: „Hier beginnt der einleitende Inhalt der Seite oder eines bestimmten Abschnitts.“

In der Regel umschließt das `<header>`-Element dein Logo, den Namen der Webseite und die Hauptnavigation. Es kann aber auch andere Elemente wie eine Suchleiste, einen Slogan oder Links zu sozialen Medien enthalten. Eine Webseite kann sogar mehrere `<header>`-Elemente haben. Zum Beispiel könnte jeder `<article>`-Block (ein Blogbeitrag) einen eigenen kleinen Header mit Überschrift und Autorinformationen haben. Für unser Projekt, die Startseite, konzentrieren wir uns jedoch auf den globalen Seiten-Header, der auf jeder Unterseite wiederverwendet wird.

Die grundlegende Struktur sieht denkbar einfach aus:

```html
<header>
  <!-- Hier kommen Logo, Navigation und andere Elemente hinein -->
</header>
```

Mit diesem einzelnen Tag hast du bereits eine wichtige semantische Grundlage geschaffen. Du hast einen klaren Bereich für den gesamten Kopfbereich deiner Seite definiert.

#### Der Dreh- und Angelpunkt: Die Navigation mit `<nav>`

Das Herzstück fast jedes Headers ist die Navigation. Ohne sie wären Besucher auf deiner Seite verloren. Um die Hauptnavigation einer Seite semantisch korrekt auszuzeichnen, stellt HTML das `<nav>`-Element zur Verfügung.

Das `<nav>`-Element ist speziell für Navigationsblöcke gedacht. Das sind Gruppen von Links, die den Benutzer zu den Hauptbereichen deiner Webseite oder zu wichtigen externen Seiten führen. Dazu gehören die Hauptmenüleiste im Header, aber auch Navigationslinks in einer Seitenleiste oder im Footer. Du solltest `<nav>` nicht für jede beliebige Gruppe von Links verwenden. Eine Liste von Sponsoren-Links im Fließtext wäre zum Beispiel kein Fall für `<nav>`. Für unsere Hauptnavigation im Header ist es jedoch genau das richtige Werkzeug.

Indem du deine Navigationslinks in ein `<nav>`-Element packst, hilfst du nicht nur Suchmaschinen, die Struktur deiner Seite zu verstehen. Du bietest vor allem Nutzern von Screenreadern einen riesigen Vorteil. Diese können gezielt zu Navigationsblöcken springen, anstatt sich durch die gesamte Seite lesen zu müssen, um zum Menü zu gelangen.

#### Die richtige Struktur für Menüpunkte: Ungeordnete Listen

Wie aber strukturierst du die einzelnen Links innerhalb des `<nav>`-Elements? Die bewährte und semantisch korrekteste Methode ist die Verwendung einer ungeordneten Liste (`<ul>`). Warum eine Liste? Weil eine Navigation im Grunde genau das ist: eine Liste von Zielen, zu denen der Benutzer navigieren kann.

Jeder Menüpunkt wird zu einem Listenelement (`<li>`), und innerhalb dieses Listenelements platzierst du den eigentlichen Link (`<a>`). Diese Verschachtelung ist das A und O einer sauberen und robusten Navigationsstruktur.

Schauen wir uns an, wie das in der Praxis aussieht:

```html
<nav>
  <ul>
    <li><a href="/index.html">Startseite</a></li>
    <li><a href="/ueber-uns.html">Über uns</a></li>
    <li><a href="/leistungen.html">Leistungen</a></li>
    <li><a href="/kontakt.html">Kontakt</a></li>
  </ul>
</nav>
```

Diese Struktur hat mehrere Vorteile:
1.  **Semantisch klar:** Es ist eine Navigationssektion, die eine Liste von Links enthält. Klarer geht es nicht.
2.  **Standardkonform:** Dies ist der etablierte Standard, den Entwickler und Tools erwarten.
3.  **Leicht zu stylen:** Mit CSS kannst du die Listeneigenschaften (wie die Aufzählungszeichen) leicht entfernen und die Listenelemente nebeneinander anordnen, um ein horizontales Menü zu erstellen. Die saubere HTML-Struktur ist die perfekte Grundlage dafür.

#### Das Gesamtbild: Logo und Navigation im `<header>` vereint

Fügen wir nun alle Teile zusammen, um einen vollständigen, professionellen Header für unsere Projekt-Startseite zu erstellen. Unser Header soll ein Logo enthalten, das zurück zur Startseite verlinkt, und unsere Hauptnavigation.

Das Logo kann ein einfacher Text sein oder, wie in den meisten Fällen, ein Bild. Wichtig ist, dass das Logo selbst ein Link ist, der den Benutzer zur Startseite (`/` oder `index.html`) führt.

```html
<header>
  <div class="header-container">
    <a href="/" class="logo">
      <img src="img/logo.svg" alt="Logo von WebWorks Kreativagentur">
    </a>

    <nav aria-label="Hauptnavigation">
      <ul>
        <li><a href="/">Start</a></li>
        <li><a href="/projekte.html">Projekte</a></li>
        <li><a href="/agentur.html">Agentur</a></li>
        <li><a href="/blog.html">Blog</a></li>
        <li><a href="/kontakt.html">Kontakt</a></li>
      </ul>
    </nav>
  </div>
</header>
```

Analysieren wir diesen Codeblock im Detail:
*   **`<header>`:** Der äußere Container, der den gesamten Kopfbereich semantisch definiert.
*   **`<div class="header-container">`:** Oft wird ein zusätzlicher `<div>` innerhalb des Headers verwendet. Dieser dient rein gestalterischen Zwecken, zum Beispiel um dem Inhalt eine maximale Breite zu geben und ihn auf großen Bildschirmen zu zentrieren, während der `<header>` selbst die volle Breite einnehmen kann (z. B. für eine Hintergrundfarbe).
*   **`<a href="/" class="logo">`:** Das Logo ist ein Link zur Startseite. Dies ist eine fest etablierte Konvention im Webdesign, die Benutzer erwarten.
*   **`<img src="..." alt="...">`:** Das eigentliche Logo-Bild. Das `alt`-Attribut ist hier absolut entscheidend. Es beschreibt das Bild für Screenreader-Nutzer und für den Fall, dass das Bild nicht geladen werden kann. Es sollte den Namen des Unternehmens oder der Marke enthalten.
*   **`<nav aria-label="Hauptnavigation">`:** Hier siehst du eine wichtige Ergänzung: das `aria-label`-Attribut. ARIA (Accessible Rich Internet Applications) hilft dabei, Webseiten für Menschen mit Behinderungen zugänglicher zu machen. Mit `aria-label="Hauptnavigation"` gibst du diesem spezifischen `<nav>`-Block einen eindeutigen Namen. Ein Screenreader wird dann ansagen: „Hauptnavigation, Liste mit 5 Elementen“, anstatt nur „Navigation“. Dies ist besonders nützlich, wenn du mehrere `<nav>`-Elemente auf einer Seite hast (z. B. eine im Header und eine im Footer).
*   **`<ul>`, `<li>`, `<a>`:** Unsere bewährte Struktur für die Menüpunkte.

#### Wichtige Unterscheidung: `<header>` vs. `<head>`

Ein häufiger Stolperstein für Einsteiger ist die Verwechslung der Elemente `<header>` und `<head>`. Obwohl sie ähnlich klingen, haben sie völlig unterschiedliche Aufgaben und dürfen niemals verwechselt werden.

*   **`<head>` (der Kopf):** Dieses Element steht ganz am Anfang deines HTML-Dokuments, direkt nach dem `<html>`-Tag und vor dem `<body>`-Tag. Der Inhalt des `<head>`-Elements ist für den Besucher auf der Webseite **nicht sichtbar**. Er enthält Metadaten über das Dokument, wie den Titel der Seite (der im Browser-Tab angezeigt wird), Verknüpfungen zu CSS-Stylesheets und JavaScript-Dateien, Zeichenkodierung und andere technische Informationen für den Browser und Suchmaschinen. Denk an den `<head>` als den Maschinenraum deiner Webseite.
*   **`<header>` (die Kopfzeile):** Dieses Element befindet sich immer innerhalb des `<body>`. Sein Inhalt ist für den Besucher **sichtbar**. Es definiert, wie wir gelernt haben, den einleitenden Bereich einer Seite oder eines Abschnitts. Denk an den `<header>` als die Empfangshalle deiner Webseite.

Kurz gesagt: `<head>` ist für die Maschine, `<header>` ist für den Menschen.

#### Vorausschauend denken: Die Basis für responsives Design

Die hier gezeigte HTML-Struktur ist nicht nur semantisch sauber, sondern auch extrem flexibel. Sie ist die perfekte Grundlage für ein responsives Design, das auf allen Geräten gut aussieht und funktioniert.

Auf einem großen Desktop-Bildschirm wirst du die `<li>`-Elemente mithilfe von CSS wahrscheinlich horizontal anordnen. Auf einem kleinen Smartphone-Bildschirm ist dafür oft nicht genug Platz. Hier kommt das berühmte „Hamburger-Menü“ ins Spiel: Die Navigationsliste (`<ul>`) wird standardmäßig ausgeblendet und nur durch einen Klick auf ein Menü-Icon (den „Hamburger“) sichtbar gemacht.

Die HTML-Struktur, die wir geschaffen haben, unterstützt dieses Verhalten perfekt. Das JavaScript, das für das Ein- und Ausblenden zuständig ist, hat mit der `<ul>`-Liste ein klares Element, das es ansprechen kann. Ohne diese saubere, logische Gliederung wäre die Implementierung solcher modernen Features deutlich komplizierter und fehleranfälliger.

Indem du deinen Header und deine Navigation von Anfang an mit diesen semantischen HTML-Elementen aufbaust, legst du das Fundament für eine zugängliche, suchmaschinenfreundliche und zukunftssichere Webseite. Du schreibst nicht nur Code, der funktioniert – du schreibst Code, der eine Bedeutung hat.
