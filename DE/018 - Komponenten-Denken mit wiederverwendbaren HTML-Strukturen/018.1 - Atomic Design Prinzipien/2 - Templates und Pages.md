# Templates und Pages

### Templates und Pages: Das große Ganze zusammenfügen

Nachdem wir uns durch Atome, Moleküle und Organismen gearbeitet haben, erreichen wir nun die letzten beiden Stufen der Atomic-Design-Methodik: Templates und Pages. Hier fügt sich alles zusammen, was du bisher in kleineren Teilen konzipiert und gebaut hast. Diese beiden Stufen sind entscheidend, um zu sehen, ob dein Designsystem nicht nur in der Theorie, sondern auch in der Praxis funktioniert. Sie sind der Moment der Wahrheit für deine Komponenten.

#### Was ist ein Template? Der Bauplan der Seite

Stell dir ein Template als den Bauplan für eine bestimmte Art von Seite vor. Es ist eine konkrete Zusammenstellung von Organismen, die in einer bestimmten Struktur angeordnet sind. Ein Template definiert das Layout und die grundlegende Anordnung der Inhalte, aber es enthält noch keine echten, finalen Inhalte. Stattdessen arbeitest du hier mit Platzhaltern.

Der Hauptzweck eines Templates ist es, die inhaltliche Struktur einer Seite festzulegen. Du beantwortest hier Fragen wie:

*   Wo befindet sich die Hauptnavigation (ein Navigations-Organismus)?
*   Wo wird der Hauptinhalt platziert (zum Beispiel ein Artikel-Organismus)?
*   Gibt es eine Seitenleiste (ein Sidebar-Organismus) und wo steht sie?
*   Wie ist der Header- und der Footer-Organismus aufgebaut und positioniert?

Der entscheidende Punkt ist, dass Templates noch vom Inhalt entkoppelt sind. Du verwendest Platzhaltertexte wie "Lorem ipsum" für Absätze, generische Überschriften wie "[Titel des Blogartikels]" und Platzhalterbilder (z. B. graue Boxen mit Größenangaben).

Warum ist diese Trennung so wichtig? Weil sie dir erlaubt, dich ausschließlich auf die Struktur und das Layout zu konzentrieren. Du kannst testen, ob dein Komponentensystem als Ganzes funktioniert. Halten die Beziehungen zwischen den Organismen? Bricht das Layout an bestimmten Stellen oder bei verschiedenen Bildschirmgrößen? Ein Template ist im Grunde ein hochwertiger Wireframe, der bereits mit den echten, gestylten Komponenten deines Systems gebaut wurde.

Schauen wir uns ein einfaches Beispiel für ein Blogartikel-Template an. Es könnte Organismen wie einen Header, einen Artikel-Hauptteil, eine Sidebar und einen Footer enthalten.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[Seitentitel] - Unser Blog</title>
    <!-- Link zu den CSS-Styles, die alle Komponenten stylen -->
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <!-- organism-main-header -->
    <header class="main-header">
        <!-- molecule-logo -->
        <a href="/" class="logo">Logo</a>
        <!-- organism-main-navigation -->
        <nav class="main-nav">
            <ul>
                <li><a href="#">Thema 1</a></li>
                <li><a href="#">Thema 2</a></li>
                <li><a href="#">Über uns</a></li>
            </ul>
        </nav>
    </header>

    <main class="content-wrapper">
        <!-- organism-article-content -->
        <article class="blog-post">
            <!-- molecule-page-title -->
            <h1>[Titel des Blogartikels]</h1>
            
            <!-- molecule-meta-info -->
            <div class="meta-info">
                <span>Veröffentlicht am [Datum] von [Autor]</span>
            </div>
            
            <img src="https://via.placeholder.com/800x400" alt="Platzhalterbild für Artikel">
            
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
            <p>Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
        </article>

        <!-- organism-sidebar -->
        <aside class="sidebar">
            <h3>Neueste Beiträge</h3>
            <ul>
                <li><a href="#">[Titel eines anderen Artikels]</a></li>
                <li><a href="#">[Titel eines anderen Artikels]</a></li>
                <li><a href="#">[Titel eines anderen Artikels]</a></li>
            </ul>
        </aside>
    </main>

    <!-- organism-footer -->
    <footer class="main-footer">
        <p>&copy; [Jahr] Dein Unternehmen. Alle Rechte vorbehalten.</p>
    </footer>

</body>
</html>
```

In diesem Code siehst du klar die Struktur. Die Inhalte sind austauschbar und generisch. Du könntest dieses eine Template für potenziell Hunderte von verschiedenen Blogartikeln verwenden. Es ist die Schablone, die du immer wieder neu befüllen kannst.

#### Was ist eine Page? Das lebendige Ergebnis

Die Page ist die letzte und konkreteste Stufe im Atomic Design. Eine Page ist eine spezifische Instanz eines Templates, die mit echtem, repräsentativem Inhalt gefüllt ist. Hier ersetzt du die "Lorem ipsum"-Texte, die Platzhalterbilder und die generischen Überschriften durch reale Daten.

Wenn das Template der Bauplan des Hauses ist, dann ist die Page das fertig eingerichtete Haus, in dem Menschen leben. Du siehst nicht nur, wo die Küche ist, sondern auch, welche Farbe die Schränke haben und was im Kühlschrank steht.

Der Zweck einer Page ist es, die Effektivität deines Designsystems unter realen Bedingungen zu testen. Hier siehst du, wie sich deine Komponenten verhalten, wenn sie mit der Unberechenbarkeit von echtem Inhalt konfrontiert werden:

*   Was passiert, wenn ein Redakteur eine extrem lange Überschrift für einen Blogartikel wählt? Bricht das Layout? Wird der Text unleserlich?
*   Wie sieht die Seite aus, wenn ein Artikel nur sehr wenig Text, aber viele Bilder enthält?
*   Was geschieht, wenn der Name eines Autors viel länger ist als der Platzhalter "[Autor]"?
*   Funktionieren die Komponenten auch mit nutzergenerierten Inhalten, die vielleicht unerwartete Zeichen oder Formatierungen enthalten?

Pages sind der ultimative Test für die Robustheit und Flexibilität deines Systems. Sie sind auch das, was du Stakeholdern, Kunden oder deinem Team zeigst, um das finale Design zu präsentieren und Feedback einzuholen. Niemand kann ein Design wirklich beurteilen, wenn er nur "Lorem ipsum" liest. Erst mit echtem Inhalt wird das Erlebnis greifbar.

Nehmen wir unser Blogartikel-Template und erstellen daraus eine konkrete Page:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Warum Komponenten-Denken deine Webentwicklung revolutioniert - Unser Blog</title>
    <!-- Link zu den CSS-Styles, die alle Komponenten stylen -->
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <!-- organism-main-header -->
    <header class="main-header">
        <!-- molecule-logo -->
        <a href="/" class="logo">WebMeister</a>
        <!-- organism-main-navigation -->
        <nav class="main-nav">
            <ul>
                <li><a href="/html">HTML</a></li>
                <li><a href="/css">CSS</a></li>
                <li><a href="/ueber-uns">Über uns</a></li>
            </ul>
        </nav>
    </header>

    <main class="content-wrapper">
        <!-- organism-article-content -->
        <article class="blog-post">
            <!-- molecule-page-title -->
            <h1>Warum Komponenten-Denken deine Webentwicklung revolutioniert</h1>
            
            <!-- molecule-meta-info -->
            <div class="meta-info">
                <span>Veröffentlicht am 18. Oktober 2023 von Eva Klein</span>
            </div>
            
            <img src="/images/artikel/komponenten-denken.jpg" alt="Eine schematische Darstellung von ineinander verschachtelten Bausteinen.">
            
            <p>In der modernen Webentwicklung hat sich ein Paradigmenwechsel vollzogen. Weg von monolithischen, seitenbasierten Ansätzen, hin zu einem modularen, komponentenbasierten Denken. Dieses Prinzip, populär gemacht durch Frameworks wie React und Vue, aber auch durch Methodiken wie Atomic Design, verändert fundamental, wie wir digitale Produkte konzipieren, gestalten und entwickeln.</p>
            <p>Der Kerngedanke ist einfach: Statt eine komplette Seite als eine Einheit zu betrachten, zerlegen wir sie in ihre kleinsten, wiederverwendbaren Einzelteile. Ein einfacher Button, ein Suchfeld, eine Navigationsleiste – all das werden zu eigenständigen, gekapselten Komponenten, die unabhängig voneinander entwickelt, getestet und wiederverwendet werden können. Dieser Ansatz bringt eine enorme Effizienz und Konsistenz in große Projekte.</p>
        </article>

        <!-- organism-sidebar -->
        <aside class="sidebar">
            <h3>Neueste Beiträge</h3>
            <ul>
                <li><a href="/artikel/css-grid-vs-flexbox">CSS Grid vs. Flexbox: Was wann nutzen?</a></li>
                <li><a href="/artikel/barrierefreies-webdesign">Grundlagen des barrierefreien Webdesigns</a></li>
                <li><a href="/artikel/performance-optimierung">5 einfache Tipps zur Performance-Optimierung</a></li>
            </ul>
        </aside>
    </main>

    <!-- organism-footer -->
    <footer class="main-footer">
        <p>&copy; 2023 WebMeister. Alle Rechte vorbehalten.</p>
    </footer>

</body>
</html>
```

Der Unterschied ist sofort ersichtlich. Der HTML-Code ist strukturell identisch mit dem des Templates, aber jeder Platzhalter wurde durch spezifische, sinnvolle Inhalte ersetzt. Diese Page fühlt sich lebendig und echt an.

#### Die Synergie: Warum du beides brauchst

Templates und Pages sind kein "Entweder-oder", sondern ein untrennbares Duo. Ihr Zusammenspiel ist das Herzstück der letzten Phase des Atomic Designs.

*   **Templates** definieren die Struktur und das System. Sie sind die Quelle der Wahrheit für das Layout. Wenn du eine Änderung am Layout vornehmen willst, tust du das im Template. Diese Änderung wirkt sich dann auf alle Pages aus, die auf diesem Template basieren.
*   **Pages** validieren das System. Sie sind die Testfälle für deine Templates und Komponenten. Es ist sinnvoll, mehrere Pages aus einem einzigen Template zu erstellen, um verschiedene Inhalts-Szenarien und Extremfälle (Edge Cases) zu testen. Du könntest zum Beispiel eine Page "Blogartikel mit langem Titel", eine "Blogartikel ohne Beitragsbild" und eine "Blogartikel mit Kommentaren" erstellen, um sicherzustellen, dass dein System mit all diesen Variationen umgehen kann.

Diese klare Trennung von Struktur (Template) und Inhalt (Page) ermöglicht eine parallele Arbeitsweise. Während du als Entwickler am Template feilst und die Responsivität sicherstellst, kann ein Content-Manager bereits die realen Inhalte für die Pages vorbereiten. Am Ende wird beides zusammengefügt, um das finale, funktionierende Produkt zu erschaffen.

Indem du von Atomen über Moleküle und Organismen bis hin zu Templates und Pages denkst, baust du nicht nur einzelne Webseiten. Du erschaffst ein durchdachtes, skalierbares und wartbares Designsystem, das die Grundlage für konsistente und hochwertige digitale Erlebnisse legt.
