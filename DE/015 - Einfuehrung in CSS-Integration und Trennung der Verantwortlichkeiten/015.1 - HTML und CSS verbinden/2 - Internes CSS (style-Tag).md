# Internes CSS (style-Tag)

### Internes CSS: Styling direkt im HTML-Dokument

Nachdem wir uns mit Inline-CSS beschäftigt haben, das direkt an einzelne HTML-Tags geknüpft wird, gehen wir nun einen Schritt weiter. Stell dir vor, du möchtest nicht nur ein einzelnes Element, sondern alle Überschriften oder alle Absätze auf einer Seite einheitlich gestalten. Mit Inline-CSS müsstest du jeden einzelnen Tag anfassen – ein mühsames und fehleranfälliges Unterfangen. Hier kommt das interne CSS ins Spiel, eine Methode, die dir mehr Kontrolle und Effizienz für das Styling einer einzelnen HTML-Seite bietet.

#### Das `<style>`-Tag: Dein CSS-Container im Kopf

Internes CSS wird mithilfe des `<style>`-Tags definiert. Dieses Tag ist ein spezieller Container, der ausschließlich dazu dient, CSS-Regeln aufzunehmen. Der entscheidende Punkt ist sein Standort: Das `<style>`-Tag gehört immer in den `<head>`-Bereich deines HTML-Dokuments.

Warum im `<head>`? Der Browser liest ein HTML-Dokument von oben nach unten. Indem du die Stilregeln im Kopf der Seite platzierst, gibst du dem Browser alle notwendigen Design-Informationen, bevor er überhaupt damit beginnt, den sichtbaren Inhalt im `<body>` darzustellen. Das sorgt für einen sauberen und effizienten Ladevorgang und verhindert, dass die Seite kurz ohne Stile angezeigt und dann plötzlich "neu formatiert" wird (ein Phänomen, das als "Flash of Unstyled Content" bekannt ist).

Schauen wir uns ein einfaches Beispiel an:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Beispiel für Internes CSS</title>
    
    <style>
        body {
            background-color: #f4f4f4;
            font-family: Arial, sans-serif;
            color: #333;
        }

        h1 {
            color: #005a9c; /* Ein dunkles Blau */
        }

        p {
            line-height: 1.6;
        }
    </style>

</head>
<body>

    <h1>Willkommen auf meiner Seite</h1>
    <p>Dies ist ein Absatz, der mit internem CSS gestaltet wird. Beachte die Schriftart, die Farbe und den Zeilenabstand.</p>
    <p>Auch dieser zweite Absatz übernimmt dieselben Stile, ohne dass wir ihn einzeln anfassen mussten.</p>

</body>
</html>
```

In diesem Beispiel siehst du klar die Struktur. Innerhalb des `<head>`-Tags befindet sich das `<style>`-Tag. Alles, was zwischen `<style>` und `</style>` steht, ist reiner CSS-Code, genau so, wie du ihn kennenlernst. Wir haben hier drei Regeln definiert:
1.  Eine Regel für den gesamten `<body>`, die die Hintergrundfarbe, die Schriftfamilie und die Standard-Textfarbe festlegt.
2.  Eine Regel für alle `<h1>`-Überschriften, die ihre Farbe in ein dunkles Blau ändert.
3.  Eine Regel für alle `<p>`-Elemente, die den Zeilenabstand für bessere Lesbarkeit erhöht.

Der große Vorteil ist sofort ersichtlich: Du schreibst die Regel für `p` nur ein einziges Mal, und sie gilt automatisch für jeden Absatz auf dieser Seite. Wenn du dich später entscheidest, den Zeilenabstand zu ändern, musst du das nur an einer einzigen Stelle tun – innerhalb des `<style>`-Tags.

#### Die Stärken von internem CSS

Wann ist die Verwendung von internem CSS eine gute Idee? Es gibt einige Szenarien, in denen diese Methode ihre Stärken voll ausspielt.

**1. Einzelne, eigenständige Seiten:**
Wenn du eine einzelne Webseite erstellst, die für sich allein steht – zum Beispiel eine "Coming Soon"-Seite, eine einfache Landingpage oder ein Online-Lebenslauf –, ist internes CSS perfekt. Alle für diese Seite relevanten Informationen, sowohl die Struktur (HTML) als auch das Design (CSS), sind in einer einzigen Datei gebündelt. Das macht die Datei portabel und einfach zu verwalten. Du musst nicht mehrere Dateien im Auge behalten.

**2. Schnelle Prototypen und Tests:**
Beim Entwickeln und Experimentieren mit Layouts und Designs ist es oft praktisch, HTML und CSS in einer Datei zu haben. Du kannst schnell Änderungen vornehmen und die Auswirkungen sofort im Browser sehen, ohne zwischen verschiedenen Dateien wechseln zu müssen.

**3. HTML-E-Mails:**
Dies ist ein sehr wichtiger und spezifischer Anwendungsfall. Viele E-Mail-Clients haben aus Sicherheitsgründen oder aufgrund veralteter Technik große Probleme mit externen Stylesheets (die wir im nächsten Kapitel behandeln). Internes CSS im `<style>`-Tag wird von vielen modernen Clients gut unterstützt und ist oft die zuverlässigste Methode, um komplexe E-Mail-Layouts zu gestalten.

**4. Spezifische Seitenvorlagen:**
Stell dir eine große Webseite vor, die hauptsächlich ein einheitliches Design verwendet. Es könnte jedoch eine ganz spezielle Seite geben, zum Beispiel eine einmalige Werbeaktion, die ein völlig anderes Aussehen benötigt. Anstatt das globale Stylesheet mit Regeln zu überladen, die nur für diese eine Seite gelten, könntest du die spezifischen Stile als internes CSS direkt in diese eine HTML-Datei einfügen.

#### Die Grenzen und Nachteile

So praktisch internes CSS in bestimmten Situationen auch ist, es hat einen entscheidenden Nachteil, der es für die meisten größeren Webprojekte ungeeignet macht: **Die fehlende Skalierbarkeit.**

Die Stilregeln gelten immer nur für das eine HTML-Dokument, in dem sie definiert sind. Sobald deine Webseite aus mehr als einer Seite besteht (z. B. "Startseite", "Über uns", "Kontakt"), stößt du an eine Grenze. Wenn du ein einheitliches Design für alle Seiten möchtest, müsstest du den gesamten Inhalt des `<style>`-Tags kopieren und in jede einzelne HTML-Datei einfügen.

Stell dir vor, deine Webseite hat 20 Seiten und du möchtest die Link-Farbe von Blau auf Grün ändern. Du müsstest 20 Dateien öffnen und an derselben Stelle die Änderung vornehmen. Das ist nicht nur zeitaufwändig, sondern auch eine riesige Fehlerquelle. Man vergisst leicht eine Datei, und schon ist das Design inkonsistent.

Dieses Problem widerspricht einem wichtigen Prinzip in der Softwareentwicklung: **DRY (Don't Repeat Yourself – Wiederhole dich nicht)**. Guter Code ist wartbar, und das bedeutet, dass wiederkehrende Logik oder Definitionen an einem zentralen Ort gespeichert werden sollten.

Ein weiterer Nachteil betrifft die **Performance**. Wenn ein Besucher deine Webseite durchstöbert und von der Startseite zur "Über uns"-Seite navigiert, muss der Browser bei der Verwendung von internem CSS die gleichen Stilregeln erneut herunterladen, da sie Teil der neuen HTML-Datei sind. Das erhöht die Ladezeit und den Datenverbrauch, auch wenn es sich nur um geringe Mengen handelt.

#### Trennung der Verantwortlichkeiten

Internes CSS ist ein wichtiger Schritt weg vom Chaos des Inline-CSS. Es bündelt die Stile für eine Seite an einem zentralen Ort und ermöglicht die Nutzung von mächtigen CSS-Selektoren wie Klassen und IDs. Es kratzt jedoch nur an der Oberfläche dessen, was eine saubere Trennung der Verantwortlichkeiten ("Separation of Concerns") bedeutet.

Das Idealziel ist eine klare Trennung:
*   **HTML** ist ausschließlich für die **Struktur und Semantik** des Inhalts zuständig.
*   **CSS** ist ausschließlich für die **Präsentation und das Design** zuständig.
*   **JavaScript** (das wir später behandeln) ist für die **Interaktivität und das Verhalten** zuständig.

Mit internem CSS sind Struktur und Präsentation immer noch in derselben Datei vermischt. Es ist ein Kompromiss – besser als Inline-CSS, aber noch nicht die sauberste Lösung für skalierbare Projekte.

Für ebenjene skalierbaren Projekte gibt es eine dritte, leistungsfähigere Methode: externes CSS. Diese Methode ermöglicht es uns, unsere Stilregeln in eine komplett separate `.css`-Datei auszulagern und diese dann mit beliebig vielen HTML-Seiten zu verknüpfen. Das ist der Goldstandard für die Webentwicklung und das Thema unseres nächsten Kapitels. Doch das Verständnis für internes CSS ist fundamental, denn es zeigt dir den Weg und die Logik, wie CSS innerhalb eines Dokuments wirken kann, und rüstet dich für die speziellen Anwendungsfälle, in denen es die beste Wahl bleibt.
