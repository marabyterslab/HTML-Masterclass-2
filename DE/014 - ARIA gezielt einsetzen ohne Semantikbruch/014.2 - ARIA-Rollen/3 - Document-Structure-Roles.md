# Document-Structure-Roles

### Rollen für die Dokumentstruktur: Das Skelett deiner Seite für alle verständlich machen

Stell dir eine Webseite wie ein Gebäude vor. Die semantischen HTML5-Elemente wie `<header>`, `<nav>`, `<main>` und `<footer>` sind wie die standardisierten Räume: Eingangshalle, Flure, Hauptsaal und Keller. Jeder, der das Gebäude betritt, weiß instinktiv, wofür diese Räume da sind. Für Nutzer von assistiven Technologien, wie Screenreadern, sind diese semantischen Elemente extrem wertvoll. Sie ermöglichen es ihnen, eine Seite schnell zu überblicken und direkt zu dem Bereich zu springen, der sie interessiert – ganz so, als würden sie einen Lageplan des Gebäudes betrachten.

Doch was tust du, wenn du in einem Gebäude arbeitest, das keine klar definierten Räume hat? Vielleicht wurde es mit generischen Bausteinen wie unzähligen `<div>`-Elementen errichtet, sei es aus historischen Gründen, durch ein bestimmtes JavaScript-Framework oder weil die Umstände es einfach nicht anders zuließen. Hier kommen die ARIA Document-Structure-Roles ins Spiel. Sie sind wie nachträglich angebrachte Schilder, die einem ansonsten unstrukturierten Raum eine klare Bedeutung geben. Du sagst dem Browser und damit auch den assistiven Technologien: „Hey, dieser `<div>` hier ist nicht irgendein Container, er *fungiert als* Navigationsleiste.“

Bevor wir tief in die einzelnen Rollen eintauchen, gilt es, die allererste und wichtigste Regel von ARIA zu verinnerlichen: **Wenn du ein natives HTML-Element verwenden kannst, das die benötigte Semantik bereits mitbringt, dann nutze es!** ARIA ist ein mächtiges Werkzeug zur Verbesserung der Barrierefreiheit, aber es ist kein Ersatz für sauberes, semantisches HTML. Setze es gezielt dort ein, wo HTML an seine Grenzen stößt.

#### Die wichtigsten Landmark-Rollen im Überblick

Die bedeutendsten Rollen für die Dokumentstruktur sind die sogenannten „Landmark Roles“. Sie markieren die Hauptbereiche deiner Seite und schaffen so eine Art Inhaltsverzeichnis, durch das Screenreader-Nutzer navigieren können.

##### `role="banner"`
Diese Rolle kennzeichnet den Kopfbereich deiner Webseite. Er enthält in der Regel das Logo, den Namen der Website und vielleicht eine primäre Tagline. Im Wesentlichen ist es das ARIA-Äquivalent zum `<header>`-Element, wenn dieses als globaler Seitenkopf verwendet wird.

*   **Natives HTML-Element:** `<header>`
*   **Anwendung:** Verwende `banner` für den obersten, seitenweiten Kopfbereich. Pro Seite sollte es nur eine `banner`-Rolle geben.

```html
<!-- Schlecht: Semantik fehlt -->
<div class="site-header">
  <img src="logo.svg" alt="Firmenlogo">
  <h1>Unsere Webseite</h1>
</div>

<!-- Besser mit ARIA -->
<div role="banner" class="site-header">
  <img src="logo.svg" alt="Firmenlogo">
  <h1>Unsere Webseite</h1>
</div>

<!-- Ideal: Natives HTML -->
<header class="site-header">
  <img src="logo.svg" alt="Firmenlogo">
  <h1>Unsere Webseite</h1>
</header>
```

##### `role="navigation"`
Wie der Name schon sagt, kennzeichnet diese Rolle einen Navigationsbereich mit Links, die zu den Hauptbereichen der Website oder zu wichtigen Unterseiten führen.

*   **Natives HTML-Element:** `<nav>`
*   **Anwendung:** Ideal für die Hauptnavigation, eine Brotkrümel-Navigation oder ein Inhaltsverzeichnis auf der Seite. Wenn du mehrere `navigation`-Bereiche auf einer Seite hast (z. B. Hauptnavigation und eine untergeordnete Navigation im Footer), solltest du sie mit `aria-label` eindeutig benennen.

```html
<!-- Besser mit ARIA -->
<div role="navigation" aria-label="Hauptnavigation">
  <ul>
    <li><a href="/">Startseite</a></li>
    <li><a href="/produkte">Produkte</a></li>
    <li><a href="/kontakt">Kontakt</a></li>
  </ul>
</div>

<!-- Ideal: Natives HTML -->
<nav aria-label="Hauptnavigation">
  <ul>
    <li><a href="/">Startseite</a></li>
    <li><a href="/produkte">Produkte</a></li>
    <li><a href="/kontakt">Kontakt</a></li>
  </ul>
</nav>
```

##### `role="main"`
Diese Rolle ist eine der wichtigsten. Sie markiert den Hauptinhalt deines Dokuments. Der Inhalt innerhalb von `main` sollte einzigartig für die jeweilige Seite sein und nicht aus wiederkehrenden Elementen wie Kopf- oder Fußzeilen bestehen.

*   **Natives HTML-Element:** `<main>`
*   **Anwendung:** Es darf pro Seite nur ein einziges Element mit der `main`-Rolle geben. Screenreader bieten oft eine Tastenkombination an, um direkt zu diesem Bereich zu springen.

```html
<!-- Besser mit ARIA -->
<div role="main">
  <h2>Willkommen auf unserer Produktseite</h2>
  <p>Hier finden Sie alle Informationen zu unseren neuesten Angeboten...</p>
</div>

<!-- Ideal: Natives HTML -->
<main>
  <h2>Willkommen auf unserer Produktseite</h2>
  <p>Hier finden Sie alle Informationen zu unseren neuesten Angeboten...</p>
</main>
```

##### `role="complementary"`
Diese Rolle ist für Inhalte gedacht, die zwar in Beziehung zum Hauptinhalt stehen, aber auch für sich allein stehen könnten. Man kann sie aus dem Hauptinhalt herauslösen, ohne dessen grundlegende Bedeutung zu verändern. Klassische Beispiele sind Seitenleisten mit verwandten Artikeln, Wetter-Widgets oder Werbeanzeigen.

*   **Natives HTML-Element:** `<aside>`
*   **Anwendung:** Perfekt für die typische „Sidebar“.

```html
<!-- Besser mit ARIA -->
<div role="complementary">
  <h3>Verwandte Themen</h3>
  <ul>
    <li><a href="#">Thema A</a></li>
    <li><a href="#">Thema B</a></li>
  </ul>
</div>

<!-- Ideal: Natives HTML -->
<aside>
  <h3>Verwandte Themen</h3>
  <ul>
    <li><a href="#">Thema A</a></li>
    <li><a href="#">Thema B</a></li>
  </ul>
</aside>
```

##### `role="contentinfo"`
Diese Rolle kennzeichnet den Fußbereich der Webseite. Hier finden sich typischerweise Informationen wie Copyright-Hinweise, Links zum Impressum, Datenschutzbestimmungen oder Kontaktinformationen.

*   **Natives HTML-Element:** `<footer>`
*   **Anwendung:** Verwende `contentinfo` für den globalen Seitenfuß. Ähnlich wie `banner` sollte es pro Seite nur eine `contentinfo`-Rolle geben.

```html
<!-- Besser mit ARIA -->
<div role="contentinfo">
  <p>&copy; 2023 Meine Firma. Alle Rechte vorbehalten.</p>
  <a href="/impressum">Impressum</a>
</div>

<!-- Ideal: Natives HTML -->
<footer>
  <p>&copy; 2023 Meine Firma. Alle Rechte vorbehalten.</p>
  <a href="/impressum">Impressum</a>
</footer>
```

##### `role="search"`
Diese Rolle ist selbsterklärend: Sie markiert einen Bereich, der eine Suchfunktion enthält. Das ist für Nutzer assistiver Technologien hilfreich, da sie so schnell die Suchfunktion der Seite finden können.

*   **Natives HTML-Element:** Es gibt kein direktes Äquivalent, aber seit Kurzem das `<search>`-Element, das aber noch nicht von allen Browsern voll unterstützt wird. Üblicherweise wird ein `<form>`-Element für die Suche verwendet.
*   **Anwendung:** Umschließe dein Suchformular mit einem Element, das diese Rolle trägt.

```html
<!-- Besser mit ARIA -->
<div role="search">
  <form action="/suche" method="get">
    <label for="search-input">Seite durchsuchen:</label>
    <input type="search" id="search-input" name="q">
    <button type="submit">Suchen</button>
  </form>
</div>

<!-- Ideal (in Zukunft): Natives HTML -->
<search>
  <form action="/suche" method="get">
    <label for="search-input">Seite durchsuchen:</label>
    <input type="search" id="search-input" name="q">
    <button type="submit">Suchen</button>
  </form>
</search>
```

##### `role="region"`
Die `region`-Rolle ist eine generische Landmark-Rolle für einen wichtigen Bereich der Seite, für den keine der spezifischeren Rollen (wie `navigation` oder `main`) passt. Ein typisches Beispiel wäre ein Bereich für „Neuigkeiten“ oder „Bevorstehende Termine“.
Ein entscheidender Punkt bei `role="region"` ist: Ein solcher Bereich **muss** einen zugänglichen Namen haben, damit er für Nutzer von Screenreadern einen Sinn ergibt. Andernfalls wird er als "Region" ohne weitere Beschreibung angesagt, was nutzlos ist. Du vergibst den Namen über `aria-label` oder `aria-labelledby`.

*   **Natives HTML-Element:** `<section>` (wenn es eine Überschrift hat)
*   **Anwendung:** Nur für wichtige, zusammenhängende Inhaltsblöcke verwenden, die du als navigierbaren Punkt hervorheben möchtest.

```html
<!-- Falsch: Ohne Label ist die Rolle nutzlos -->
<div role="region">
  ...
</div>

<!-- Besser mit ARIA und Label -->
<div role="region" aria-label="Aktuelle Nachrichten">
  <h2>Aktuelle Nachrichten</h2>
  <p>Neues aus aller Welt...</p>
</div>

<!-- Ideal: Natives HTML (die Überschrift gibt dem Abschnitt seinen Namen) -->
<section aria-label="Aktuelle Nachrichten">
  <h2>Aktuelle Nachrichten</h2>
  <p>Neues aus aller Welt...</p>
</section>
```

#### Mehr als nur Landmarks: Weitere nützliche Struktur-Rollen

Neben den großen Landmark-Rollen gibt es weitere ARIA-Rollen, die dir helfen, kleinere, aber ebenso wichtige Inhaltsstrukturen semantisch anzureichern.

*   **`role="article"`:** Äquivalent zum `<article>`-Element. Kennzeichnet einen in sich geschlossenen, eigenständigen Inhalt, der potenziell syndiziert werden könnte, wie ein Blogbeitrag, ein Foren-Post oder ein Zeitungsartikel.
*   **`role="list"` und `role="listitem"`:** Die Entsprechungen für `<ul>` bzw. `<ol>` und `<li>`. Du solltest sie nur in absoluten Ausnahmefällen verwenden, wenn die Verwendung nativer Listenelemente technisch unmöglich ist, da du die gesamte Funktionalität (z. B. das Ansagen der Anzahl der Listenelemente) selbst nachbilden musst.
*   **`role="figure"` und `role="figcaption"`:** Entsprechen den Elementen `<figure>` und `<figcaption>`. Sie werden verwendet, um eine Abbildung, ein Diagramm oder ein Codebeispiel mit einer zugehörigen Bildunterschrift zu gruppieren.
*   **`role="form"`:** Kennzeichnet ein Formular. Das ist oft redundant, wenn du bereits das native `<form>`-Element verwendest. Es kann aber nützlich sein, um eine Sammlung von Formularelementen, die nicht in einem echten `<form>`-Tag stehen, als logische Einheit zu gruppieren. Auch hier ist eine Beschriftung via `aria-label` dringend zu empfehlen.

#### Ein Wort der Warnung: ARIA mit Bedacht einsetzen

Der wichtigste Grundsatz bleibt: ARIA ist eine Ergänzung, kein Ersatz. Ein entscheidender technischer Aspekt, den du verstehen musst, ist, dass eine ARIA-Rolle die native Semantik eines Elements **überschreibt**.

Wenn du zum Beispiel schreibst:
`<h1 role="button">Klick mich</h1>`

... dann teilst du dem Browser und den assistiven Technologien mit: „Ignoriere die Tatsache, dass dies eine Überschrift der Ebene 1 ist. Behandle es stattdessen wie einen Button.“ Ein Screenreader wird es als „Klick mich, Button“ ansagen, nicht als Überschrift. Der semantische Wert der Überschrift ist verloren.

Das ist ein gewolltes Verhalten, um komplexe Widgets zu bauen, aber es kann auch zu einem semantischen Bruch führen, wenn es falsch eingesetzt wird. Die Document-Structure-Roles, die wir hier besprochen haben, sind relativ sicher, da sie meist auf generische `<div>`- oder `<span>`-Elemente angewendet werden, die von Haus aus keine starke Semantik besitzen. Aber sobald du beginnst, ARIA auf semantisch reichen Elementen wie Überschriften, Links oder Listen zu verwenden, musst du genau wissen, was du tust.

Indem du die Strukturrollen von ARIA gezielt und korrekt einsetzt, baust du die wichtigen „Wegweiser“ in deine Seite ein, die für Nutzer assistiver Technologien den Unterschied zwischen einer unübersichtlichen Ansammlung von Inhalten und einer klar strukturierten, leicht navigierbaren Umgebung ausmachen.
