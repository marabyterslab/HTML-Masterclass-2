# Header und Footer

### Header und Footer: Die Rahmen deiner Webseite

Stell dir eine Webseite wie ein Dokument vor, zum Beispiel einen offiziellen Brief oder eine Buchseite. Fast jedes gut strukturierte Dokument hat einen klaren Anfang und ein klares Ende. Ein Brief hat einen Briefkopf mit dem Absender und oft einem Logo. Ein Buch hat auf jeder Seite eine Kopfzeile mit dem Kapiteltitel und eine Fußzeile mit der Seitenzahl. Diese Bereiche geben dem Inhalt einen Rahmen, bieten Orientierung und wiederholen wichtige Informationen, ohne Teil des eigentlichen Hauptinhalts zu sein.

In HTML übernehmen die Elemente `<header>` und `<footer>` genau diese Rolle. Sie sind semantische Container, die den einführenden und abschließenden Inhalt einer Seite oder eines Seitenabschnitts markieren. Sie sagen dem Browser, Screenreadern und Suchmaschinen: „Hey, alles hier drin ist der einleitende Kram“ oder „Das hier ist der Abschluss“. Damit schaffst du eine logische und zugängliche Struktur.

#### Das `<header>`-Element: Der erste Eindruck zählt

Das `<header>`-Element ist für eine Gruppe von einleitenden oder navigatorischen Hilfsmitteln vorgesehen. Es ist der Bereich, den Nutzer typischerweise als Erstes wahrnehmen, um sich zu orientieren.

Was gehört typischerweise in einen Header?

*   **Das Logo der Webseite:** Meist ein `<img>`-Tag, das in einen `<a>`-Tag gehüllt ist, der zurück zur Startseite führt.
*   **Der Titel oder Slogan der Seite:** Oft in Form von `<h1>`-`<h6>`-Tags oder einem einfachen `<p>`-Tag.
*   **Die Hauptnavigation:** Fast immer in einem `<nav>`-Element untergebracht, das die wichtigsten Links der Seite enthält.
*   **Ein Suchformular:** Ein `<form>`-Element, das es Nutzern ermöglicht, die Seite zu durchsuchen.
*   **Sekundäre Informationen:** Zum Beispiel Links zum Login, zur Sprachauswahl oder zum Warenkorb.

Der wichtigste Punkt beim `<header>` ist sein Kontext. Er kann auf zwei Ebenen existieren:

1.  **Als Kopf der gesamten Seite:** Dies ist der häufigste Anwendungsfall. Der `<header>` ist hier ein direktes Kind des `<body>`-Elements und enthält die globalen Informationen für die gesamte Website.

```html
<body>
  <header>
    <a href="/" id="logo">
      <img src="logo.svg" alt="Firmenlogo von WebMeister">
    </a>
    <nav>
      <ul>
        <li><a href="/produkte">Produkte</a></li>
        <li><a href="/ueber-uns">Über uns</a></li>
        <li><a href="/kontakt">Kontakt</a></li>
      </ul>
    </nav>
    <form action="/suche" method="get">
      <input type="search" name="q" placeholder="Seite durchsuchen...">
      <button type="submit">Suchen</button>
    </form>
  </header>

  <main>
    <!-- Der Hauptinhalt der Seite kommt hier hin -->
  </main>

  <footer>
    <!-- Der Fußbereich der Seite kommt hier hin -->
  </footer>
</body>
```

In diesem Beispiel ist der `<header>` der unverkennbare Kopf der gesamten Webseite. Er dient als Orientierungspunkt, egal auf welcher Unterseite du dich befindest.

2.  **Als Kopf eines Inhaltsabschnitts:** Ein `<header>` kann auch innerhalb von anderen semantischen Elementen wie `<article>` oder `<section>` verwendet werden. In diesem Kontext dient er als Einleitung für genau diesen spezifischen Abschnitt.

```html
<article>
  <header>
    <h1>Die Kunst des semantischen HTML</h1>
    <p>Veröffentlicht am <time datetime="2023-10-27">27. Oktober 2023</time> von Alex Schmidt</p>
    <p class="lead">Ein Leitfaden für sauberen und verständlichen Code.</p>
  </header>

  <p>Hier beginnt der eigentliche Inhalt des Artikels. Der obige Header hat uns bereits verraten, worum es geht, wer ihn geschrieben hat und wann er veröffentlicht wurde.</p>
  
  <!-- weiterer Artikelinhalt... -->
</article>
```

Hier siehst du, dass der `<header>` nicht die gesamte Seite, sondern nur den Artikel einleitet. Er enthält den Titel, das Datum und den Autor – also Metadaten, die direkt zum Artikel gehören. Eine Webseite kann also durchaus mehrere `<header>`-Elemente enthalten, solange jeder seinen eigenen, klar abgegrenzten Kontext hat.

Eine häufige Fehlerquelle für Einsteiger ist die Verwechslung von `<header>` mit `<head>`. Merke dir: Der `<head>`-Bereich enthält unsichtbare Metadaten für den Browser (wie den Titel im Tab, Zeichensatz, verlinkte CSS-Dateien). Das `<header>`-Element hingegen enthält sichtbare Inhalte für den Nutzer am Anfang einer Seite oder eines Abschnitts.

#### Das `<footer>`-Element: Der saubere Abschluss

Analog zum `<header>` markiert das `<footer>`-Element den Fußbereich einer Seite oder eines Abschnitts. Er enthält in der Regel Informationen über den umschließenden Inhalt.

Typische Inhalte für einen Footer sind:

*   **Copyright-Informationen:** Der klassische Hinweis wie „© 2023 Firmenname“.
*   **Rechtliche Hinweise:** Links zum Impressum, zur Datenschutzerklärung oder zu den AGB.
*   **Kontaktinformationen:** Oft innerhalb eines `<address>`-Elements.
*   **Links zu verwandten Seiten:** Sitemap, FAQ oder Social-Media-Profile.
*   **Autorinformationen:** Wenn sie nicht im `<header>` eines Artikels stehen.
*   **Ein „Nach oben“-Link:** Um dem Nutzer das Scrollen zu ersparen.

Genau wie der `<header>` ist auch der `<footer>` kontextabhängig.

1.  **Als Fuß der gesamten Seite:** Der globale `<footer>` am Ende des `<body>` ist der Standardfall. Er fasst die Meta-Informationen der gesamten Website zusammen.

```html
<body>
  <header>
    <!-- ... -->
  </header>

  <main>
    <!-- Der Hauptinhalt der Seite -->
  </main>

  <footer>
    <p>&copy; 2023 WebMeister GmbH. Alle Rechte vorbehalten.</p>
    <nav>
      <ul>
        <li><a href="/impressum">Impressum</a></li>
        <li><a href="/datenschutz">Datenschutz</a></li>
        <li><a href="/kontakt">Kontakt</a></li>
      </ul>
    </nav>
    <address>
      WebMeister GmbH<br>
      Musterstraße 1<br>
      12345 Musterstadt
    </address>
  </footer>
</body>
```

Dieser Footer gilt für die gesamte Präsenz und bietet rechtliche sowie kontaktbezogene Informationen, die auf jeder Seite verfügbar sein sollten.

2.  **Als Fuß eines Inhaltsabschnitts:** Innerhalb eines `<article>` kann ein `<footer>` zusätzliche Informationen zum Artikel selbst liefern, wie zum Beispiel Kategorien, Tags oder Share-Buttons.

```html
<article>
  <header>
    <h1>Die Kunst des semantischen HTML</h1>
    <!-- ... -->
  </header>

  <p>Der Hauptinhalt des Artikels...</p>

  <footer>
    <p>Kategorien: <a href="/kategorie/html">HTML</a>, <a href="/kategorie/webdev">Webentwicklung</a></p>
    <p>Tags: #semantik, #bestpractice</p>
    <div>
      <span>Teilen auf:</span>
      <!-- Links zu sozialen Netzwerken -->
    </div>
  </footer>
</article>
```

Dieser `<footer>` schließt den Artikel ab und hat nichts mit dem globalen Seiten-Footer zu tun. Er gehört logisch und strukturell ausschließlich zu diesem `<article>`.

#### Warum das alles so wichtig ist: Semantik für Mensch und Maschine

Du könntest versucht sein zu denken: „Warum der Aufwand? Ich kann doch einfach alles mit `<div>`-Elementen und passenden CSS-Klassen wie `class="header"` und `class="footer"` bauen.“ Das würde visuell vielleicht zum selben Ergebnis führen, aber du würdest den entscheidenden Vorteil von semantischem HTML verlieren: die Bedeutung.

1.  **Barrierefreiheit (Accessibility):** Screenreader, die von Menschen mit Sehbehinderungen genutzt werden, erkennen `<header>` und `<footer>` als sogenannte „Landmarks“ (Orientierungspunkte). Ein Nutzer kann so direkt zum Hauptinhalt springen und muss sich nicht durch die immer gleiche Navigation im Header lesen. Der `<header>` wird als „Banner“ und der `<footer>` als „Content Information“ interpretiert. Das macht die Navigation auf deiner Seite um ein Vielfaches effizienter.

2.  **Suchmaschinenoptimierung (SEO):** Suchmaschinen wie Google analysieren die Struktur deiner Seite, um deren Inhalt zu verstehen. Ein `<h1>` in einem `<header>` hat für sie eine andere Gewichtung als ein Link im `<footer>`. Durch die klare Trennung hilfst du der Suchmaschine, die Hierarchie und Relevanz deiner Inhalte korrekt zu bewerten.

3.  **Wartbarkeit des Codes:** Für dich und andere Entwickler ist der Code sofort lesbar. Wenn du `<header>` siehst, weißt du sofort, welche Rolle dieser Block spielt, ohne erst die CSS-Klassen analysieren zu müssen. Dein Code dokumentiert sich quasi selbst.

Indem du `<header>` und `<footer>` bewusst und kontextbezogen einsetzt, baust du nicht nur eine Webseite, sondern eine robuste, zugängliche und zukunftssichere Informationsarchitektur. Sie sind das Fundament, auf dem das Layout und die Interaktion deiner Seite aufbauen – ein stabiler Rahmen für deine Inhalte.
