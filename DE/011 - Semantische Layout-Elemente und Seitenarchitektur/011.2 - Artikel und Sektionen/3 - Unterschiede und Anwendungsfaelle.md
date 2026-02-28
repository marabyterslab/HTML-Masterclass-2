# Unterschiede und Anwendungsfälle

# `<article>` und `<section>`: Die Kunst der feinen Unterschiede

Auf den ersten Blick wirken die HTML-Elemente `<article>` und `<section>` sehr ähnlich. Beide dienen dazu, deinen Inhalt semantisch zu gruppieren und von anderen Bereichen abzugrenzen. Viele Entwickler verwenden sie fast austauschbar, was zu einer unklaren Dokumentstruktur führen kann. Doch der Unterschied zwischen ihnen ist fundamental und entscheidend für eine saubere, zugängliche und maschinenlesbare Seitenarchitektur. Wenn du diesen Unterschied einmal verinnerlicht hast, wird die Strukturierung deiner Webseiten intuitiv und logisch.

## Das `<article>`-Element: Ein in sich geschlossenes Werk

Stell dir das `<article>`-Element wie einen Zeitungsartikel, einen Blogbeitrag oder einen Forenpost vor. Sein wesentliches Merkmal ist die **Eigenständigkeit**. Der Inhalt innerhalb eines `<article>`-Tags sollte für sich allein stehen und Sinn ergeben können. Wenn du ihn aus dem Kontext deiner Webseite herauslösen und an anderer Stelle – zum Beispiel in einem RSS-Feed, auf einer anderen Webseite oder in einer App – wieder einfügen würdest, müsste er immer noch vollständig verständlich sein.

Ein `<article>` ist eine komplette, in sich geschlossene Einheit. Es ist ein Stück Inhalt, das potenziell syndiziert, also unabhängig von der restlichen Seite verteilt werden kann.

**Typische Anwendungsfälle für `<article>` sind:**

*   Ein einzelner Blogbeitrag
*   Ein Nachrichtenartikel
*   Ein Beitrag in einem Forum
*   Ein einzelner Kommentar in einem Kommentarbereich
*   Ein Produkt auf einer Kategorieseite in einem Onlineshop
*   Eine interaktive Widget-Anwendung wie ein Wetter- oder Aktien-Widget

Jeder dieser Inhalte kann für sich allein existieren. Ein Blogbeitrag braucht nicht zwingend die umgebende Seitenleiste, um verstanden zu werden. Ein Produkt in einem Shop hat seine eigene Überschrift, Beschreibung, sein Bild und seinen Preis und bildet eine logische Einheit.

Schauen wir uns ein einfaches Beispiel an. Auf einer Blog-Übersichtsseite wäre jeder einzelne Beitrag ein eigenständiges `<article>`.

```html
<main>
  <h1>Mein Tech-Blog</h1>

  <article class="blog-post-summary">
    <h2>Die Zukunft von CSS: Was uns erwartet</h2>
    <p>CSS hat sich in den letzten Jahren rasant entwickelt. Von Grid und Flexbox bis hin zu Container Queries – die Möglichkeiten sind endlos. In diesem Artikel werfen wir einen Blick auf die kommenden Features...</p>
    <a href="/blog/zukunft-von-css">Weiterlesen</a>
    <footer>
      <p>Veröffentlicht am 12. Oktober 2023 von Alex</p>
    </footer>
  </article>

  <article class="blog-post-summary">
    <h2>Semantisches HTML: Mehr als nur Tags</h2>
    <p>Warum `<div>`-Suppen ein Problem sind und wie du mit semantischen Elementen wie `<article>`, `<section>` und `<nav>` deine Webseite für alle verbesserst.</p>
    <a href="/blog/semantisches-html">Weiterlesen</a>
    <footer>
      <p>Veröffentlicht am 28. September 2023 von Alex</p>
    </footer>
  </article>

</main>
```

Jedes dieser `<article>`-Elemente könnte problemlos in einen RSS-Reader geladen werden und würde dort immer noch als kohärente Informationseinheit funktionieren.

## Das `<section>`-Element: Ein thematischer Baustein

Im Gegensatz zum `<article>` ist ein `<section>`-Element nicht für sich allein stehend konzipiert. Seine Aufgabe ist es, Inhalte **thematisch zu gruppieren**. Es ist ein Abschnitt innerhalb eines größeren Kontexts. Wenn `<article>` ein komplettes Buch sein kann, ist `<section>` ein Kapitel darin. Ein Kapitel ergibt isoliert betrachtet oft wenig Sinn; es benötigt den Kontext des Buches, um seine volle Bedeutung zu entfalten.

Eine `<section>` bündelt also zusammengehörige Inhalte. Die entscheidende Regel lautet: Ein `<section>`-Element sollte fast immer eine eigene Überschrift (`<h1>` - `<h6>`) haben, die das Thema dieses Abschnitts klar benennt. Wenn du keinen passenden Titel für einen Abschnitt findest, ist es wahrscheinlich kein `<section>`, sondern eher ein `<div>` für reines Styling.

**Typische Anwendungsfälle für `<section>` sind:**

*   Ein "Einleitung"-Kapitel auf einer langen Artikelseite
*   Eine Gruppe von Kontaktinformationen ("Anfahrt", "Kontaktformular", "Öffnungszeiten") auf einer Kontaktseite
*   Der Bereich "Neueste Nachrichten" auf einer Startseite
*   Eine Liste von Features auf einer Produkt-Detailseite

Hier ist ein Beispiel für eine Kontaktseite, die durch `<section>`-Elemente klar gegliedert ist:

```html
<main>
  <h1>Kontaktieren Sie uns</h1>
  <p>Wir freuen uns, von Ihnen zu hören. Hier finden Sie alle Möglichkeiten, mit uns in Kontakt zu treten.</p>

  <section>
    <h2>Unsere Adresse</h2>
    <p>Musterfirma GmbH<br>Technologiestraße 5<br>12345 Digitalstadt</p>
    <!-- Hier könnte eine Karte eingebettet sein -->
  </section>

  <section>
    <h2>Schreiben Sie uns eine Nachricht</h2>
    <form>
      <!-- Formular-Felder hier -->
    </form>
  </section>

  <section>
    <h2>Telefonische Erreichbarkeit</h2>
    <p>Du erreichst uns montags bis freitags von 9:00 bis 17:00 Uhr unter der Nummer +49 123 456789.</p>
  </section>

</main>
```

Keine dieser Sektionen würde für sich allein genommen und an anderer Stelle platziert einen vollständigen Sinn ergeben. "Unsere Adresse" ist nur im Kontext einer Kontaktseite wirklich nützlich.

## Der entscheidende Unterschied: Der Eigenständigkeits-Test

Die Kernfrage, die du dir stellen solltest, lautet:

**"Kann dieser Inhaltsblock für sich allein stehen und wäre er auch außerhalb dieser Seite noch verständlich und nützlich?"**

*   **Ja?** Dann ist es sehr wahrscheinlich ein `<article>`.
*   **Nein?** Dann ist es sehr wahrscheinlich eine `<section>`, die einen Teil des übergeordneten Inhalts thematisch gruppiert.

Dieser einfache Test – man könnte ihn auch den "Syndication-Test" nennen – löst die meisten Unklarheiten auf.

## Verschachtelung: Wie `<article>` und `<section>` zusammenspielen

Jetzt wird es interessant, denn du kannst diese Elemente auch ineinander verschachteln. Das ist kein Widerspruch, sondern eine logische Konsequenz ihrer Definition.

### Fall 1: `<section>` innerhalb von `<article>`

Dies ist der häufigste Anwendungsfall. Du hast einen langen, in sich geschlossenen Beitrag (`<article>`) und möchtest ihn zur besseren Lesbarkeit in thematische Kapitel (`<section>`) unterteilen.

```html
<article>
  <h1>Die Kunst des Brotbackens</h1>
  
  <section>
    <h2>Die Wahl des richtigen Mehls</h2>
    <p>Nicht jedes Mehl ist gleich. Für ein rustikales Sauerteigbrot benötigst du ein starkes Weizen- oder Roggenmehl...</p>
  </section>

  <section>
    <h2>Der Sauerteig-Starter: Pflege und Fütterung</h2>
    <p>Dein Starter ist das Herz deines Brotes. Er braucht regelmäßige Pflege, um aktiv und triebstark zu bleiben...</p>
  </section>

  <section>
    <h2>Der Backvorgang: Temperatur und Dampf</h2>
    <p>Eine hohe Anfangstemperatur und ausreichend Dampf sind entscheidend für eine knusprige Kruste und eine lockere Krume...</p>
  </section>

</article>
```

Der gesamte Beitrag über das Brotbacken ist ein `<article>`. Er ist eigenständig. Die einzelnen Kapitel über Mehl, Sauerteig und den Backvorgang sind thematische Unterteilungen dieses Artikels und daher perfekte Kandidaten für `<section>`.

### Fall 2: `<article>` innerhalb von `<section>`

Auch das ist möglich und sinnvoll. Stell dir die Startseite einer Nachrichten-Website vor. Dort könnte es einen Bereich namens "Aktuelles aus der Politik" geben. Dieser Bereich ist eine thematische Gruppierung (`<section>`). Innerhalb dieses Bereichs werden mehrere einzelne Nachrichtenmeldungen angezeigt. Jede dieser Meldungen ist ein in sich geschlossenes Werk und somit ein `<article>`.

```html
<main>

  <!-- Andere Inhalte der Startseite -->

  <section>
    <h2>Aktuelles aus der Politik</h2>

    <article>
      <h3>Neues Klimaschutzgesetz verabschiedet</h3>
      <p>Der Bundestag hat heute mit großer Mehrheit das neue Klimaschutzgesetz beschlossen, das weitreichende Änderungen für Industrie und Verbraucher mit sich bringt.</p>
      <a href="/politik/klimaschutzgesetz">Mehr erfahren</a>
    </article>

    <article>
      <h3>Bildungsreform: Die wichtigsten Punkte</h3>
      <p>Die Kultusministerkonferenz einigte sich auf eine umfassende Reform des Bildungssystems. Die Pläne stoßen auf geteiltes Echo.</p>
      <a href="/politik/bildungsreform">Mehr erfahren</a>
    </article>
    
  </section>

  <!-- Andere Sektionen wie "Sport" oder "Wirtschaft" -->

</main>
```

Hier gruppiert die `<section>` thematisch zusammengehörige, aber dennoch eigenständige `<article>`-Elemente.

## Die unverzichtbare Rolle von Überschriften

Wie bereits erwähnt, ist eine Überschrift ein starkes Indiz für die Notwendigkeit von `<section>` oder `<article>`. Beide Elemente helfen dabei, eine logische Dokumentstruktur (Document Outline) zu schaffen. Suchmaschinen und assistierende Technologien wie Screenreader nutzen diese Struktur, um den Inhalt deiner Seite zu verstehen und dem Nutzer eine einfache Navigation zu ermöglichen. Ein Nutzer eines Screenreaders kann beispielsweise von Überschrift zu Überschrift springen. Wenn deine Sektionen und Artikel klar betitelt sind, schaffst du eine enorme Verbesserung der Benutzerfreundlichkeit.

Die wichtigste Regel ist jedoch, eine bewusste Entscheidung zu treffen. Anstatt gedankenlos ein `<div>` zu verwenden, frage dich kurz: Ist dieser Inhalt eigenständig oder ist er Teil eines größeren Ganzen? Allein diese Überlegung wird die semantische Qualität deines HTML-Codes dramatisch verbessern. `<article>` und `<section>` sind keine komplizierten Werkzeuge, sondern präzise Instrumente, um deiner Webseite eine klare und verständliche Architektur zu verleihen.
