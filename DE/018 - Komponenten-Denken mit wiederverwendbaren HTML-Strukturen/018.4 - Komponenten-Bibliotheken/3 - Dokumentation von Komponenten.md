# Dokumentation von Komponenten

### Die Kunst der Komponentendokumentation

Stell dir vor, du hast eine brillante, wiederverwendbare Komponente entwickelt. Sie ist elegant, performant und löst ein gängiges Problem in deinem Projekt. Du bist zu Recht stolz darauf. Doch was passiert, wenn ein Kollege aus deinem Team – oder dein zukünftiges Ich in sechs Monaten – diese Komponente verwenden möchte? Ohne eine klare Anleitung ist deine geniale Entwicklung nur ein Stück Code, dessen Zweck und Anwendungsmöglichkeiten erst mühsam entschlüsselt werden müssen. Hier kommt die Dokumentation ins Spiel. Sie ist kein lästiges Anhängsel, sondern ein integraler Bestandteil einer Komponente, der ihren Wert erst wirklich entfaltet.

Eine gute Dokumentation ist wie eine Brücke zwischen dem Entwickler einer Komponente und denjenigen, die sie nutzen. Sie schafft Klarheit, fördert die Konsistenz im gesamten Projekt und beschleunigt die Entwicklung enorm, weil niemand das Rad neu erfinden oder durch Quellcode rätseln muss. In diesem Kapitel schauen wir uns an, was eine erstklassige Komponentendokumentation ausmacht.

#### Die Anatomie einer perfekten Dokumentation

Eine umfassende Dokumentation beantwortet nicht nur die Frage „Wie benutze ich das?“, sondern auch „Warum und wann benutze ich das?“. Betrachten wir die wesentlichen Bausteine am Beispiel einer fiktiven `Card`-Komponente.

##### 1. Name und Absicht

Jede Dokumentation sollte mit den Grundlagen beginnen: einem klaren Namen und einer prägnanten Beschreibung des Zwecks.

*   **Name:** `Card`-Komponente
*   **Absicht:** Stellt eine in sich geschlossene Informationseinheit dar, meist bestehend aus Bild, Titel, Text und einer Handlungsaufforderung (Call-to-Action). Ideal für Blog-Teaser, Produktübersichten oder Team-Profile.

Diese kurze Einleitung gibt sofort Kontext und hilft anderen zu entscheiden, ob diese Komponente die richtige für ihren Anwendungsfall ist.

##### 2. Visuelle Darstellung und Zustände

Menschen sind visuelle Wesen. Zeige, wie die Komponente aussieht! Ein Bild sagt oft mehr als tausend Worte Code. Füge einen Screenshot oder eine Live-Vorschau der Komponente in ihrem Standardzustand ein.

Noch wichtiger ist es, auch die verschiedenen Variationen und Zustände zu zeigen. Eine Komponente verhält sich selten statisch. Was passiert bei einem `:hover` über einem Link? Wie sieht eine "hervorgehobene" Variante aus? Wie eine "deaktivierte"? Visuelle Beispiele für jeden Zustand sind Gold wert.

##### 3. Der Basis-Code (Markup)

Dies ist der Kern für die praktische Anwendung. Stelle ein sauberes, direkt kopierbares HTML-Snippet bereit, das die Grundstruktur der Komponente zeigt. Halte es so einfach wie möglich, um den Einstieg zu erleichtern.

Für unsere `Card`-Komponente könnte das so aussehen:

```html
<article class="card">
  <img src="pfad/zum/bild.jpg" alt="Eine sinnvolle Bildbeschreibung" class="card__image">
  <div class="card__content">
    <h3 class="card__title">Titel der Karte</h3>
    <p class="card__text">Dies ist ein kurzer Beschreibungstext, der den Inhalt der Karte zusammenfasst.</p>
    <a href="#" class="card__link">Mehr erfahren</a>
  </div>
</article>
```

Achte darauf, dass dein Code-Beispiel semantisch korrekt ist. Die Verwendung von `<article>` signalisiert, dass der Inhalt für sich allein stehen kann. Das `alt`-Attribut ist ausgefüllt, um die Wichtigkeit von Barrierefreiheit von Anfang an zu betonen.

##### 4. Optionen und Modifikatoren

Selten passt eine Komponente in ihrer Standardausführung für jeden Zweck. Hier kommen Konfigurationsmöglichkeiten ins Spiel. Bei reinen HTML/CSS-Komponenten sind dies oft Modifikator-Klassen. Liste diese systematisch auf, am besten in einer Tabelle.

| Klasse / Modifikator | Typ     | Beschreibung                                                                       | Standard |
| -------------------- | ------- | ---------------------------------------------------------------------------------- | -------- |
| `.card--featured`    | Klasse  | Hebt die Karte visuell hervor, z. B. durch einen farbigen Rahmen oder Schatten.    | Nein     |
| `.card--horizontal`  | Klasse  | Ordnet Bild und Inhalt nebeneinander statt untereinander an.                       | Nein     |
| `.card--no-image`    | Klasse  | Passt das Layout für Karten an, die kein Bild enthalten.                           | Nein     |

Diese Tabelle macht auf einen Blick klar, wie du die Komponente anpassen kannst. Bei komplexeren Systemen, die JavaScript oder CSS Custom Properties nutzen, würde diese Tabelle auch Parameter oder Variablen enthalten.

##### 5. Anwendungsbeispiele (Use Cases)

Zeige die Komponente in Aktion! Erstelle mehrere Code-Beispiele, die verschiedene Konfigurationen und Kontexte abbilden.

**Beispiel 1: Eine hervorgehobene Karte**

```html
<article class="card card--featured">
  <!-- ... Inhalt ... -->
</article>
```

**Beispiel 2: Eine horizontale Karte ohne Bild**

```html
<article class="card card--horizontal card--no-image">
  <div class="card__content">
    <h3 class="card__title">Wichtige Ankündigung</h3>
    <p class="card__text">Ein längerer Text, der die volle Breite der Karte nutzt, da kein Bild vorhanden ist.</p>
    <a href="#" class="card__link">Details anzeigen</a>
  </div>
</article>
```

Diese Beispiele nehmen Nutzern die Denkarbeit ab und zeigen die Flexibilität deiner Komponente.

##### 6. Hinweise zur Barrierefreiheit (Accessibility)

Eine moderne Komponente muss für alle zugänglich sein. Deine Dokumentation ist der perfekte Ort, um auf die eingebauten Accessibility-Features hinzuweisen und Anleitungen für deren korrekte Nutzung zu geben.

*   **Bild-Alternativtexte:** Erkläre, warum das `alt`-Attribut im `<img>`-Tag entscheidend ist und welche Art von Text dort erwartet wird.
*   **Semantische Struktur:** Begründe die Wahl der HTML-Tags. Warum `<article>` statt `<div>`? Warum `<h3>` für den Titel? Dies schärft das Bewusstsein für eine saubere HTML-Struktur.
*   **Tastaturbedienung:** Stelle sicher, dass alle interaktiven Elemente (wie der Link `card__link`) per Tastatur erreichbar und bedienbar sind. Erwähne dies explizit.
*   **ARIA-Attribute:** Falls du ARIA-Rollen oder -Attribute verwendest (z.B. `aria-label` für einen Button mit reinem Icon), erkläre deren Zweck und korrekte Anwendung.

##### 7. Do’s and Don’ts (Gebote und Verbote)

Manchmal ist es genauso wichtig zu sagen, was man *nicht* tun sollte. Eine Liste mit klaren Regeln hilft, häufige Fehler zu vermeiden und die Integrität des Designs zu wahren.

*   **Do:** Verwende prägnante und kurze Titel, die auf eine Zeile passen.
*   **Don't:** Verschachtele keine weiteren interaktiven Elemente wie Buttons oder Links im `card__content`, wenn die gesamte Karte bereits ein Link ist. Dies führt zu ungültigem HTML und Verwirrung bei der Bedienung.
*   **Do:** Stelle sicher, dass der Kontrast zwischen Textfarbe und Hintergrundfarbe den WCAG-Richtlinien entspricht.
*   **Don't:** Entferne die Klasse `card__title` nicht, auch wenn du den Titel visuell verstecken möchtest. Sie ist wichtig für die semantische Struktur und Screenreader.

#### Werkzeuge für lebendige Dokumentation

Das manuelle Schreiben von Dokumentation in einem separaten Dokument birgt die Gefahr, dass sie veraltet, sobald der Code sich ändert. Moderne Werkzeuge helfen dabei, eine sogenannte „Living Documentation“ oder ein „Living Style Guide“ zu erstellen – eine Dokumentation, die direkt mit der Codebasis verbunden ist und sich oft automatisch aktualisiert.

*   **Storybook:** Obwohl es stark in der Welt von JavaScript-Frameworks wie React oder Vue verankert ist, ist Storybook ein Paradebeispiel für komponentenbasierte Dokumentation. Es ermöglicht dir, Komponenten isoliert zu entwickeln und interaktiv zu präsentieren. Du kannst verschiedene Zustände und Konfigurationen durchspielen, ohne die eigentliche Anwendung starten zu müssen.
*   **Pattern Lab:** Ein Tool, das auf dem Konzept des Atomic Design aufbaut. Es hilft dir, dein gesamtes Designsystem zu organisieren und zu dokumentieren, von den kleinsten Atomen (wie Farben und Schriftarten) bis hin zu komplexen Seiten. Pattern Lab generiert eine statische Website aus deinen Komponenten und deren Dokumentation.
*   **Statische Seiten-Generatoren (SSGs):** Werkzeuge wie Eleventy, Astro oder Jekyll sind perfekt geeignet, um eine maßgeschneiderte Dokumentations-Website zu erstellen. Du kannst Markdown-Dateien für die Beschreibung verwenden und deine HTML/CSS-Komponenten direkt in die Seite einbetten, um Live-Vorschauen zu erzeugen.

Der Schlüsselgedanke hinter diesen Werkzeugen ist, die Dokumentation so nah wie möglich am Code zu halten. Wenn die Dokumentation Teil des Entwicklungsprozesses wird und nicht nur ein nachträglicher Gedanke ist, bleibt sie relevant, nützlich und korrekt.

Eine gut dokumentierte Komponente ist ein Geschenk an dein Team und an dich selbst. Sie ist ein Zeichen von Professionalität und vorausschauendem Denken. Sie verwandelt eine Sammlung von Code-Schnipseln in eine robuste, verständliche und leicht zu wartende Komponenten-Bibliothek – das Fundament für jedes erfolgreiche Webprojekt.
