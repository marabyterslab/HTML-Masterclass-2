# Erstellung von HTML-Styleguides

### Erstellung von HTML-Styleguides

Stell dir vor, du kommst in ein neues Projektteam oder übernimmst den Code einer Kollegin oder eines Kollegen. Du öffnest die erste HTML-Datei und siehst Einrückungen mit vier Leerzeichen. In der nächsten Datei werden Tabs verwendet. Attribute sind mal in doppelten, mal in einfachen Anführungszeichen geschrieben. Klassennamen sind mal deskriptiv (`.product-card`), mal kryptisch (`.pc-123`) oder rein visuell (`.red-bold-text`).

Dieses Chaos ist nicht nur unschön, es ist auch ineffizient. Es verlangsamt die Entwicklung, erschwert die Wartung und macht die Einarbeitung neuer Teammitglieder zu einer Qual. Die Lösung für dieses Problem ist ein Styleguide – eine Sammlung verbindlicher Regeln und Konventionen für das Schreiben von Code. Ein HTML-Styleguide ist sozusagen das Grundgesetz deines Projekts für alles, was mit Markup zu tun hat. Er schafft eine „Single Source of Truth“ und sorgt dafür, dass jeder im Team die gleiche Sprache spricht.

#### Warum ein Styleguide unverzichtbar ist

Ein Styleguide ist mehr als nur eine Liste von Vorschriften. Er ist ein Werkzeug für Qualität und Effizienz. Die Hauptvorteile sind:

*   **Konsistenz:** Jede HTML-Datei im Projekt sieht aus, als wäre sie von derselben Person geschrieben worden. Das macht den Code vorhersehbar und leichter zu lesen.
*   **Lesbarkeit:** Ein klar strukturierter und einheitlich formatierter Code ist für Menschen einfacher zu verstehen und zu verarbeiten.
*   **Wartbarkeit:** Wenn du oder jemand anderes in sechs Monaten eine Änderung vornehmen muss, erleichtert ein konsistenter Stil das Zurechtfinden und minimiert das Risiko, neue Fehler einzubauen.
*   **Effiziente Zusammenarbeit:** Diskussionen über Formatierungsfragen („Tabs oder Spaces?“) werden ein für alle Mal beendet. Das Team kann sich auf die Lösung von Problemen konzentrieren, anstatt über Stilfragen zu debattieren.
*   **Einfacheres Onboarding:** Neue Teammitglieder können sich am Styleguide orientieren und sind wesentlich schneller produktiv.

#### Die Kernbereiche eines HTML-Styleguides

Ein guter HTML-Styleguide muss nicht Hunderte von Seiten umfassen. Er sollte sich auf die wichtigsten Aspekte konzentrieren, die für Konsistenz sorgen. Hier sind die entscheidenden Bausteine.

##### 1. Allgemeine Formatierungsregeln

Dies sind die grundlegendsten Regeln, die das visuelle Erscheinungsbild deines Codes definieren.

*   **Einrückung (Indentation):** Lege fest, ob Tabs oder Leerzeichen verwendet werden. Die gängigste und empfohlene Praxis sind zwei Leerzeichen. Egal, wofür du dich entscheidest, die Hauptsache ist, dass es einheitlich ist.

    ```html
    <!-- Gut: Konsistente Einrückung mit 2 Leerzeichen -->
    <ul>
      <li>Erster Punkt</li>
      <li>Zweiter Punkt</li>
    </ul>
    
    <!-- Schlecht: Gemischte oder inkonsistente Einrückung -->
    <ul>
       <li>Erster Punkt</li>
     <li>Zweiter Punkt</li>
    </ul>
    ```

*   **Groß- und Kleinschreibung:** Alle Element- und Attributnamen sollten konsequent kleingeschrieben werden. Dies entspricht dem gängigen Standard und verbessert die Lesbarkeit.

    ```html
    <!-- Gut: Kleinschreibung -->
    <img src="bild.jpg" alt="Ein beschreibender Text.">
    
    <!-- Schlecht: Gemischte Schreibweise -->
    <IMG SRC="bild.jpg" ALT="Ein beschreibender Text.">
    ```

*   **Anführungszeichen:** Verwende für Attributwerte immer doppelte Anführungszeichen (`"`). Das ist der am weitesten verbreitete Standard und vermeidet Probleme, falls der Attributwert selbst ein einfaches Anführungszeichen enthält.

    ```html
    <!-- Gut -->
    <a href="#" class="navigation-link">Startseite</a>
    
    <!-- Schlecht -->
    <a href='#' class='navigation-link'>Startseite</a>
    ```

##### 2. Dokumentstruktur und Semantik

Hier geht es um den korrekten Aufbau eines HTML-Dokuments und die sinnvolle Verwendung von Elementen.

*   **HTML-Grundgerüst:** Definiere ein minimales, standardisiertes Grundgerüst für jede neue HTML-Datei.

    ```html
    <!DOCTYPE html>
    <html lang="de">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Seitentitel</title>
      <link rel="stylesheet" href="style.css">
    </head>
    <body>
      <!-- Seiteninhalt hier -->
    </body>
    </html>
    ```
    Wichtige Punkte hierbei sind der `<!DOCTYPE html>`, das `lang`-Attribut im `<html>`-Tag für die Barrierefreiheit und Suchmaschinenoptimierung sowie die grundlegenden `<meta>`-Tags.

*   **Semantische Elemente:** Dies ist einer der wichtigsten Punkte. Dein Styleguide sollte darauf bestehen, HTML-Elemente entsprechend ihrer Bedeutung zu verwenden, nicht ihres Aussehens. Nutze `<nav>` für die Navigation, `<main>` für den Hauptinhalt, `<article>` für in sich geschlossene Inhalte und `<footer>` für den Fußbereich. Vermeide die exzessive Nutzung von `<div>` und `<span>`, wo ein semantisches Element passender wäre (die sogenannte „div-itis“).

    ```html
    <!-- Gut: Semantisch korrekt -->
    <header>
      <h1>Meine Webseite</h1>
      <nav>
        <ul>
          <li><a href="#">Home</a></li>
          <li><a href="#">Über uns</a></li>
        </ul>
      </nav>
    </header>
    
    <!-- Schlecht: Nicht-semantische "div-Suppe" -->
    <div class="header">
      <div class="title">Meine Webseite</div>
      <div class="navigation">
        <div class="list">
          <div class="list-item"><a href="#">Home</a></div>
          <div class="list-item"><a href="#">Über uns</a></div>
        </div>
      </div>
    </div>
    ```

*   **Kommentare:** Definiere, wann und wie Kommentare verwendet werden sollen. Kommentare sollten komplexe oder nicht-intuitive Code-Abschnitte erklären, aber nicht das Offensichtliche beschreiben.

    ```html
    <!-- Gut: Erklärt, warum dieser Abschnitt existiert -->
    <!-- Beginn des Modals für die Benutzerregistrierung -->
    <section class="modal" id="registration-modal">
      ...
    </section>
    <!-- Ende des Modals für die Benutzerregistrierung -->
    
    <!-- Schlecht: Unnötiger Kommentar -->
    <!-- Dies ist eine Liste -->
    <ul>
      ...
    </ul>
    ```

##### 3. Attribute

Auch bei der Verwendung von Attributen hilft eine klare Linie.

*   **Boolesche Attribute:** Schreibe boolesche Attribute ohne Wert. Ihre Anwesenheit impliziert den Wert `true`.

    ```html
    <!-- Gut -->
    <input type="checkbox" disabled>
    
    <!-- Schlecht -->
    <input type="checkbox" disabled="disabled">
    ```

*   **Reihenfolge der Attribute:** Eine konsistente Reihenfolge von Attributen macht Elemente leichter „scanbar“. Eine logische und verbreitete Reihenfolge ist:
    1.  `class`
    2.  `id`, `name`
    3.  `data-*`
    4.  `src`, `for`, `type`, `href`
    5.  `title`, `alt`
    6.  `aria-*`, `role`

    ```html
    <!-- Gut: Konsistente Reihenfolge -->
    <a class="button button-primary" id="submit-btn" data-action="save" href="#">Speichern</a>
    
    <!-- Schlecht: Zufällige Reihenfolge -->
    <a href="#" data-action="save" class="button button-primary" id="submit-btn">Speichern</a>
    ```

##### 4. Benennungskonventionen

Dies ist oft der Bereich mit dem größten Wildwuchs. Eine klare Benennungsstrategie für Klassen und IDs ist Gold wert.

*   **Klassen vs. IDs:** Definiere klar, wann was verwendet wird.
    *   **ID:** Verwende eine ID nur für ein Element, das auf der Seite garantiert einzigartig ist. IDs eignen sich gut für Seitenanker (z.B. `<section id="kontakt">`) und als Haken für JavaScript, um ein bestimmtes Element zu manipulieren.
    *   **Klasse:** Klassen sind für alles andere da. Sie sind wiederverwendbar und dienen primär dem Styling über CSS. Ein Element kann mehrere Klassen haben.

*   **Methodik für Klassennamen:** Um Chaos bei den Klassennamen zu vermeiden, empfiehlt es sich, eine Methodik wie **BEM (Block, Element, Modifier)** zu verwenden. BEM sorgt für strukturierte, aussagekräftige und selbsterklärende Klassennamen.
    *   **Block:** Eine eigenständige, wiederverwendbare Komponente (z.B. `.card`, `.nav`, `.search-form`).
    *   **Element:** Ein Teil eines Blocks, der ohne ihn keinen Sinn ergibt (z.B. `.card__title`, `.nav__link`, `.search-form__input`). Verbunden durch zwei Unterstriche (`__`).
    *   **Modifier:** Eine Variante oder ein Zustand eines Blocks oder Elements (z.B. `.card--highlighted`, `.nav--dark`, `.search-form__button--disabled`). Verbunden durch zwei Bindestriche (`--`).

    ```html
    <!-- Beispiel für eine Komponente mit BEM -->
    <div class="card card--featured">
      <img class="card__image" src="image.jpg" alt="...">
      <h3 class="card__title">Ein besonderer Artikel</h3>
      <a href="#" class="card__button card__button--primary">Mehr lesen</a>
    </div>
    ```
    Durch die Verwendung von BEM wird die Beziehung zwischen HTML und CSS sofort klar, und das Risiko von Stilkonflikten sinkt drastisch.

##### 5. Barrierefreiheit (Accessibility)

Ein professioneller Styleguide muss Barrierefreiheit als festen Bestandteil integrieren.

*   **`alt`-Attribute:** Jedes `<img>`-Element, das inhaltliche Informationen transportiert, muss ein aussagekräftiges `alt`-Attribut haben. Dekorative Bilder sollten ein leeres `alt`-Attribut (`alt=""`) erhalten, damit Screenreader sie ignorieren.
*   **Formular-Labels:** Jedes Formularelement (`<input>`, `<textarea>`, `<select>`) benötigt ein zugeordnetes `<label>`, das entweder über das `for`-Attribut oder durch Umschließen des Elements verknüpft ist.
*   **ARIA-Rollen:** Definiere, wann und wie ARIA-Attribute (`aria-*`) verwendet werden sollen, um die Semantik für assistierende Technologien zu verbessern, insbesondere bei dynamischen, mit JavaScript erstellten Komponenten.

#### Den Styleguide leben und automatisieren

Ein Styleguide nützt nichts, wenn er in einem Wiki verstaubt. Er muss Teil des täglichen Arbeitsablaufs werden.

*   **Dokumentation:** Halte den Styleguide an einem zentralen, für alle zugänglichen Ort fest (z.B. im Projekt-Wiki, in einer Markdown-Datei im Repository).
*   **Code-Reviews:** Nutze den Styleguide als objektive Grundlage für Feedback in Code-Reviews. Anstatt subjektiver Meinungen („Ich finde das so schöner“) kann man sich auf die gemeinsam vereinbarten Regeln beziehen.
*   **Linting:** Der beste Weg, einen Styleguide durchzusetzen, ist die Automatisierung. Tools wie **HTMLHint** oder **ESLint mit HTML-Plugins** können so konfiguriert werden, dass sie den Code automatisch auf die Einhaltung der Regeln prüfen. Ein Linter kann Fehler wie fehlende `alt`-Attribute, falsche Einrückung oder die Verwendung von `style`-Attributen direkt im Editor oder beim Commit-Prozess aufzeigen.

Ein HTML-Styleguide ist eine Investition, die sich schnell auszahlt. Er schafft eine solide Grundlage für qualitativ hochwertigen, wartbaren und skalierbaren Code. Er reduziert Reibungsverluste im Team und ermöglicht es dir und deinen Kollegen, euch auf das zu konzentrieren, was wirklich zählt: großartige Web-Erlebnisse zu schaffen.
