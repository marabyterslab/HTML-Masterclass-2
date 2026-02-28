# Footer und Meta-Links

### Der Footer – Abschluss und Wegweiser deiner Webseite

Stell dir deine Webseite wie ein gutes Buch vor. Der Header ist das Cover und das Inhaltsverzeichnis, der Hauptteil sind die spannenden Kapitel, und der Footer? Der Footer ist der Anhang, das Glossar und die Information über den Autor. Er ist oft das Letzte, was ein Besucher sieht, und damit deine letzte Chance, einen bleibenden, professionellen Eindruck zu hinterlassen. Er ist weit mehr als nur ein Ablageort für unwichtige Links; er ist ein fundamentales Element für die Benutzerfreundlichkeit, das Vertrauen und die Vollständigkeit deiner gesamten Seite.

In diesem Kapitel bauen wir den Footer für unsere Startseite. Dabei geht es nicht nur darum, ein paar Links an den unteren Rand zu klatschen. Wir werden sehen, wie ein semantisch korrekter Footer aufgebaut wird, welche Inhalte er typischerweise beherbergt und wie er zu einem unauffälligen, aber mächtigen Werkzeug deiner Webseite wird.

#### Die semantische Grundlage: Das `<footer>`-Element

Bevor wir über Inhalte nachdenken, brauchen wir das richtige Fundament. In HTML5 gibt es dafür ein eigenes, semantisches Element: `<footer`>. Dieses Tag signalisiert dem Browser, Suchmaschinen und assistiven Technologien (wie Screenreadern) eindeutig: "Hier beginnen die Abschlussinformationen für den übergeordneten Abschnitt."

In den meisten Fällen wirst du einen Haupt-Footer für deine gesamte Seite haben. Dieser `<footer`>-Tag ist dann ein direktes Kind des `<body>`-Elements.

```html
<body>
    <header>
        <!-- Header-Inhalt hier -->
    </header>

    <main>
        <!-- Hauptinhalt der Seite hier -->
    </main>

    <footer>
        <!-- Alle Footer-Inhalte kommen hier hinein -->
    </footer>
</body>
```

Das `<footer`>-Element ist ein sogenanntes „Sectioning Root“-Element. Das bedeutet, es kann eine eigene Gliederung haben, ohne die Hauptgliederung des Dokuments zu beeinflussen. Es ist auch wichtig zu wissen, dass du mehrere `<footer`>-Elemente auf einer Seite haben kannst. Ein `<article`> oder ein `<section`>-Tag könnte zum Beispiel seinen eigenen kleinen Footer mit Informationen zum Autor oder Veröffentlichungsdatum haben. In unserem Fall konzentrieren wir uns jedoch auf den einen, großen Seiten-Footer.

#### Was gehört in einen guten Footer?

Ein Footer ist wie ein Schweizer Taschenmesser – er kann viele verschiedene Werkzeuge enthalten. Welche du brauchst, hängt von deinem Projekt ab. Es gibt jedoch eine Reihe von Standardelementen, die Nutzer erwarten und die für fast jede Webseite sinnvoll sind.

##### 1. Copyright und rechtliche Hinweise

Der Klassiker. Fast jeder Footer enthält einen Copyright-Hinweis. Er signalisiert, dass die Inhalte auf der Seite urheberrechtlich geschützt sind und wann die Seite zuletzt maßgeblich aktualisiert wurde.

Das Copyright-Symbol (©) erzeugst du mit der HTML-Entität `&copy;`. Ein typischer Hinweis sieht so aus:

```html
<footer>
    <p>&copy; 2023 Dein Firmenname. Alle Rechte vorbehalten.</p>
</footer>
```

In der Praxis wird das Jahr oft dynamisch mit JavaScript eingefügt, damit du es nicht jedes Jahr manuell ändern musst. Für unser reines HTML-Projekt genügt aber vorerst die statische Jahreszahl.

##### 2. Meta-Links: Das rechtliche Pflichtprogramm

Hier wird es besonders wichtig, gerade im deutschsprachigen Raum. "Meta-Links" sind Verweise auf Seiten, die nicht direkt zum Hauptangebot gehören, aber für den Betrieb der Webseite essenziell oder rechtlich vorgeschrieben sind. Dazu gehören:

*   **Impressum:** In Deutschland gesetzlich vorgeschrieben. Es enthält Informationen über den Betreiber der Webseite.
*   **Datenschutzerklärung:** Seit der DSGVO (Datenschutz-Grundverordnung) ein absolutes Muss. Hier erklärst du, wie du mit den Daten deiner Nutzer umgehst.
*   **AGB (Allgemeine Geschäftsbedingungen):** Wenn du Produkte oder Dienstleistungen anbietest, sind deine AGB hier gut platziert.

Diese Links sind ein starkes Vertrauenssignal. Sie zeigen, dass du transparent arbeitest und dich an die Spielregeln hältst. Strukturell fassen wir diese Links am besten in einer Navigationsliste zusammen, denn genau das sind sie: eine Form der Navigation.

```html
<footer>
    <nav>
        <ul>
            <li><a href="/impressum.html">Impressum</a></li>
            <li><a href="/datenschutz.html">Datenschutz</a></li>
            <li><a href="/agb.html">AGB</a></li>
        </ul>
    </nav>
    <p>&copy; 2023 Dein Firmenname. Alle Rechte vorbehalten.</p>
</footer>
```

Die Verwendung von `<nav`> teilt Screenreadern mit, dass hier ein Navigationsblock beginnt, was die Barrierefreiheit verbessert.

##### 3. Kontaktinformationen und Adresse

Möchtest du, dass Kunden oder Nutzer dich erreichen können? Der Footer ist der perfekte Ort, um Kontaktinformationen zu platzieren. Nutzer, die gezielt nach einer Telefonnummer oder Adresse suchen, scrollen oft instinktiv nach ganz unten.

Für Adressdaten gibt es das semantische `<address`>-Element. Es ist speziell für Kontaktinformationen der Person oder Organisation gedacht, die für das Dokument oder den nächstgelegenen `<article>`-Abschnitt verantwortlich ist.

```html
<address>
    Dein Firmenname<br>
    Musterstraße 123<br>
    12345 Musterstadt<br>
    <a href="mailto:info@deinefirma.de">info@deinefirma.de</a><br>
    <a href="tel:+49123456789">+49 (0) 123 / 456 789</a>
</address>
```

Die `mailto:`- und `tel:`-Präfixe in den `href`-Attributen sind kleine, aber feine Helfer. Sie sorgen dafür, dass auf einem Smartphone beim Klick direkt die E-Mail-App oder die Telefonfunktion geöffnet wird – ein großer Gewinn für die Benutzerfreundlichkeit.

##### 4. Sitemap und erweiterte Navigation

Bei größeren Webseiten mit vielen Unterseiten kann der Footer als eine Art Mini-Sitemap dienen. Du kannst die wichtigsten Bereiche deiner Webseite hier noch einmal verlinken und in thematische Gruppen unterteilen. Das hilft nicht nur Nutzern, sich schnell zu orientieren, sondern auch Suchmaschinen, die Struktur deiner Seite besser zu verstehen.

Diese Navigationsstruktur wird oft in mehreren Spalten angelegt. Jede Spalte bekommt eine Überschrift und eine Liste mit Links.

```html
<div>
    <h3>Produkte</h3>
    <ul>
        <li><a href="/produkt-a.html">Produkt A</a></li>
        <li><a href="/produkt-b.html">Produkt B</a></li>
        <li><a href="/preise.html">Preise</a></li>
    </ul>
</div>
<div>
    <h3>Unternehmen</h3>
    <ul>
        <li><a href="/ueber-uns.html">Über uns</a></li>
        <li><a href="/karriere.html">Karriere</a></li>
        <li><a href="/presse.html">Presse</a></li>
    </ul>
</div>
```

Diese Blöcke würdest du innerhalb deines `<footer`>-Elements anordnen, oft mithilfe von `div`-Containern, die du später mit CSS zu einem Spaltenlayout formatierst.

##### 5. Social-Media-Links

Die Verknüpfung zu deinen Social-Media-Profilen ist ein Standard geworden. Auch diese Links gehören in den Footer. Üblicherweise werden sie als kleine Icons dargestellt. Die HTML-Grundlage dafür ist wieder eine einfache Liste von Links. Die visuelle Darstellung als Icon ist dann eine Aufgabe für CSS, oft in Kombination mit Icon-Bibliotheken wie Font Awesome oder SVG-Grafiken.

```html
<div>
    <h3>Folge uns</h3>
    <ul>
        <li><a href="https://twitter.com/deinprofil" target="_blank" rel="noopener noreferrer">Twitter</a></li>
        <li><a href="https://linkedin.com/deinprofil" target="_blank" rel="noopener noreferrer">LinkedIn</a></li>
        <li><a href="https://github.com/deinprofil" target="_blank" rel="noopener noreferrer">GitHub</a></li>
    </ul>
</div>
```

Achte auf die Attribute `target="_blank"` und `rel="noopener noreferrer"`. `target="_blank"` öffnet den Link in einem neuen Tab, was bei externen Links üblich ist, um den Nutzer auf deiner Seite zu halten. `rel="noopener noreferrer"` ist eine wichtige Sicherheitsmaßnahme, die verhindert, dass die neu geöffnete Seite Zugriff auf das ursprüngliche Fensterobjekt erhält.

#### Ein vollständiges Beispiel zusammengefügt

Lass uns nun all diese Elemente zu einem kompletten, gut strukturierten Footer für unsere Projekt-Startseite zusammensetzen. Wir verwenden `div`-Elemente, um die verschiedenen Bereiche zu gruppieren und für das spätere Styling mit CSS vorzubereiten.

```html
<footer>
    <div class="footer-container">

        <!-- Spalte 1: Kontaktinformationen -->
        <div class="footer-column">
            <h3>Kontakt</h3>
            <address>
                HTML-Masterclass AG<br>
                Pixel-Allee 42<br>
                10115 Web-Berlin<br>
                <a href="mailto:hallo@html-masterclass.de">hallo@html-masterclass.de</a><br>
                <a href="tel:+49301234567">+49 (30) 123 45 67</a>
            </address>
        </div>

        <!-- Spalte 2: Sitemap/Navigation -->
        <div class="footer-column">
            <h3>Navigation</h3>
            <nav>
                <ul>
                    <li><a href="/kurse.html">Alle Kurse</a></li>
                    <li><a href="/ueber-uns.html">Über uns</a></li>
                    <li><a href="/blog.html">Blog</a></li>
                    <li><a href="/kontakt.html">Kontakt</a></li>
                </ul>
            </nav>
        </div>

        <!-- Spalte 3: Social Media -->
        <div class="footer-column">
            <h3>Folge uns</h3>
            <ul class="social-links">
                <li><a href="#" target="_blank" rel="noopener noreferrer" aria-label="Besuche uns auf Twitter">Twitter</a></li>
                <li><a href="#" target="_blank" rel="noopener noreferrer" aria-label="Besuche uns auf LinkedIn">LinkedIn</a></li>
                <li><a href="#" target="_blank" rel="noopener noreferrer" aria-label="Besuche uns auf YouTube">YouTube</a></li>
            </ul>
        </div>

    </div>

    <!-- Untere Zeile für Copyright und Meta-Links -->
    <div class="footer-bottom">
        <p>&copy; 2023 HTML-Masterclass AG. Alle Rechte vorbehalten.</p>
        <nav class="meta-nav">
            <ul>
                <li><a href="/impressum.html">Impressum</a></li>
                <li><a href="/datenschutz.html">Datenschutz</a></li>
            </ul>
        </nav>
    </div>
</footer>
```

In diesem Beispiel haben wir eine klare Struktur geschaffen. Der `footer-container` fasst die Hauptspalten zusammen. Der `footer-bottom`-Bereich ist für die abschließenden rechtlichen Informationen reserviert, die oft visuell etwas abgetrennt sind.

Ein wichtiger Punkt zur Barrierefreiheit: Wenn deine Social-Media-Links später nur aus Icons bestehen, ist der Link-Text nicht mehr sichtbar. In diesem Fall ist das `aria-label`-Attribut, das wir hinzugefügt haben, entscheidend. Es gibt Screenreadern eine textliche Beschreibung des Links, z.B. "Besuche uns auf Twitter", und macht die Funktion des Links auch für blinde Nutzer verständlich.

Der Footer ist also kein Nachgedanke, sondern ein integraler Bestandteil deiner Webseite. Ein gut gemachter Footer rundet das Nutzererlebnis ab, schafft Vertrauen, verbessert die Navigation und stellt sicher, dass du rechtlichen Anforderungen genügst. Mit der richtigen semantischen Struktur legst du das perfekte Fundament, auf dem später ein ansprechendes und funktionales Design mit CSS aufbauen kann.
