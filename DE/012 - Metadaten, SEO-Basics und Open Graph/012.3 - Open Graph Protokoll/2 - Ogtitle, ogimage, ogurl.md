# og:title, og:image, og:url

### Die drei Musketiere deiner Webseite: og:title, og:image und og:url

Wenn du einen Link auf einer sozialen Plattform teilst, erwartest du, dass eine ansprechende Vorschau erscheint – eine Art digitale Visitenkarte für deine Webseite. Diese Vorschau ist kein Zufallsprodukt. Sie wird gezielt durch das Open Graph Protokoll gesteuert. Während es eine ganze Reihe von Open Graph Tags gibt, bilden drei davon das unumstößliche Fundament. Man könnte sie als die drei Musketiere deiner Webseite bezeichnen, die dafür kämpfen, dass deine Inhalte im riesigen Ozean des Social Web nicht untergehen: `og:title`, `og:image` und `og:url`. Ohne diese drei ist jede weitere Optimierung quasi bedeutungslos. Lass uns eintauchen und jeden dieser grundlegenden Bausteine im Detail betrachten.

#### og:title – Mehr als nur eine Überschrift

Der `og:title` ist der Titel deines Inhalts, so wie er in der Social-Media-Vorschau angezeigt werden soll. Er ist oft das Erste, was ein Nutzer liest, und entscheidet maßgeblich darüber, ob jemand auf deinen Link klickt oder einfach weiterscrollt.

Du fragst dich vielleicht: „Moment mal, dafür habe ich doch schon den `<title>`-Tag in meinem HTML-Dokument. Wozu brauche ich noch einen?“ Das ist eine exzellente und wichtige Frage. Der `<title>`-Tag ist in erster Linie für zwei Dinge optimiert: für die Anzeige im Browser-Tab und für die Suchmaschinenoptimierung (SEO) bei Google & Co. Er ist oft sachlicher formuliert und enthält vielleicht auch den Namen deiner Webseite, um Kontext zu schaffen.

Der `og:title` hingegen ist ausschließlich für den sozialen Kontext gedacht. Hier hast du die Freiheit, einen Titel zu formulieren, der speziell darauf ausgelegt ist, Neugier zu wecken, Emotionen anzusprechen und zum Teilen zu animieren. Er kann identisch mit deinem `<title>`-Tag sein, muss es aber nicht.

Stell dir vor, du hast einen Blogartikel mit dem Titel „Eine detaillierte Analyse der Kaffeebohnenveredelung – Schmidt Kaffeemaschinen“. Das ist ein guter, informativer `<title>` für Google. Für Social Media könnte ein `og:title` wie „Das Geheimnis hinter dem perfekten Kaffee: So veredelst du jede Bohne!“ jedoch viel besser funktionieren. Er ist direkter, persönlicher und weckt Interesse.

**Implementierung und Best Practices für `og:title`:**

*   **Prägnanz:** Halte den Titel kurz und knackig. Die meisten Plattformen schneiden Titel nach etwa 60-70 Zeichen ab. Formuliere das Wichtigste also am Anfang.
*   **Relevanz:** Der Titel muss exakt den Inhalt der Seite widerspiegeln. Irreführende Titel (Clickbait) führen zu enttäuschten Nutzern und können das Vertrauen in deine Marke nachhaltig schädigen.
*   **Einzigartigkeit:** Jede teilbare Seite deiner Webseite sollte einen eigenen, einzigartigen `og:title` haben.

So sieht der Tag im `<head>` deines HTML-Dokuments aus:

```html
<meta property="og:title" content="Das Geheimnis hinter dem perfekten Kaffee: So veredelst du jede Bohne!">
```

#### og:image – Das Aushängeschild deines Inhalts

Wenn der `og:title` die Überschrift ist, dann ist das `og:image` das Plakat. In einem schnelllebigen Newsfeed ist das Bild der mit Abstand stärkste Blickfang. Ein gutes Bild kann den Unterschied zwischen Ignorieren und Interagieren ausmachen. Ohne ein explizit definiertes `og:image` versucht die Social-Media-Plattform, selbst ein passendes Bild von deiner Seite zu extrahieren. Das Ergebnis ist oft unvorhersehbar und selten optimal – vielleicht wird dein Logo, ein Werbebanner oder ein kleines, unbedeutendes Icon aus dem Footer ausgewählt. Das willst du unbedingt vermeiden.

Mit dem `og:image`-Tag übernimmst du die volle Kontrolle und legst genau fest, welches Bild als Vorschau dienen soll.

**Implementierung und Best Practices für `og:image`:**

*   **Dimensionen:** Die ideale Größe für ein Open Graph Bild ist 1200 x 630 Pixel. Dieses Seitenverhältnis von 1.91:1 stellt sicher, dass dein Bild auf den meisten Plattformen (wie Facebook, LinkedIn und X) groß und ohne unschönen Beschnitt dargestellt wird. Kleinere Bilder funktionieren auch, sollten aber mindestens 600 x 315 Pixel groß sein, um noch als "großes" Vorschaubild zu gelten.
*   **Dateigröße:** Halte die Dateigröße so gering wie möglich, idealerweise unter 5 MB. Die Crawler der Plattformen haben nur begrenzt Zeit, deine Seite zu analysieren. Zu große Bilder können den Ladevorgang verlangsamen und dazu führen, dass die Vorschau fehlschlägt.
*   **Inhalt:** Das Bild sollte den Inhalt deiner Seite visuell unterstützen und ansprechend sein. Es kann Text enthalten (z. B. den Titel deines Artikels), aber achte darauf, dass dieser auch auf kleinen mobilen Geräten gut lesbar ist.
*   **Absolute URL:** Gib immer die vollständige, absolute URL zum Bild an, inklusive `https://`. Relative Pfade wie `/images/kaffee.jpg` funktionieren nicht.

Zusätzlich zum Haupt-Tag gibt es noch einige nützliche Helfer-Tags für das Bild:

*   `og:image:width` und `og:image:height`: Mit diesen Tags gibst du die genauen Dimensionen des Bildes an. Das hilft dem Crawler der Plattform, das Bild korrekt zu skalieren, noch bevor es vollständig heruntergeladen wurde.
*   `og:image:alt`: Hier hinterlegst du einen alternativen Text für das Bild. Das ist essenziell für die Barrierefreiheit (Screenreader lesen diesen Text vor) und hilft auch den Algorithmen, den Bildinhalt besser zu verstehen.

Ein vollständiges Beispiel für die Bild-Tags im `<head>` sieht so aus:

```html
<meta property="og:image" content="https://www.deine-kaffee-seite.de/images/kaffeebohnen-veredeln.jpg">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta property="og:image:alt" content="Nahaufnahme von gerösteten Kaffeebohnen in einer Schale.">
```

#### og:url – Die kanonische Heimat deines Links

Der `og:url`-Tag mag auf den ersten Blick am wenigsten spektakulär wirken, ist aber technisch gesehen von enormer Bedeutung. Er legt die sogenannte kanonische URL deiner Seite fest. Das ist die eine, wahre und offizielle Adresse deines Inhalts.

Warum ist das so wichtig? Eine einzelne Webseite kann oft über verschiedene URLs erreichbar sein. Denk nur an Varianten mit oder ohne `www`, mit `http` oder `httpss`, oder mit angehängten Tracking-Parametern, wie sie im Online-Marketing üblich sind (`?utm_source=twitter` oder `?sessionid=...`).

Für eine Maschine ist `https://deine-seite.de/artikel` eine andere URL als `https://deine-seite.de/artikel?ref=social`. Ohne eine klare Anweisung würden Social-Media-Plattformen jede dieser Varianten als separate Seite behandeln. Das hätte zur Folge, dass sich Likes, Kommentare und Shares auf die verschiedenen URL-Varianten verteilen würden. Ein Beitrag, der eigentlich 100 Mal geteilt wurde, könnte so in der Zählung als zwei Beiträge mit je 50 Shares erscheinen. Deine Interaktionsmetriken wären zersplittert und würden an Aussagekraft verlieren.

Der `og:url`-Tag löst dieses Problem. Du legst damit die eine, saubere und finale URL fest, unter der alle sozialen Interaktionen zusammenlaufen sollen. Egal, mit welchem Parameter-Anhang ein Link geteilt wird – die Plattform weiß dank `og:url`, zu welcher Haupt-URL diese Interaktion gehört.

**Implementierung und Best Practices für `og:url`:**

*   **Konsistenz:** Die hier angegebene URL sollte mit der kanonischen URL übereinstimmen, die du vielleicht schon über den `<link rel="canonical" ...>`-Tag für Suchmaschinen definierst.
*   **Absolut und sauber:** Verwende immer die vollständige, absolute URL ohne Session-IDs, Tracking-Parameter oder andere unnötige Anhängsel.

So wird der `og:url`-Tag in den `<head>`-Bereich eingefügt:

```html
<meta property="og:url" content="https://www.deine-kaffee-seite.de/geheimnis-perfekter-kaffee">
```

#### Das Gesamtbild: Alle drei im Einsatz

Diese drei Tags arbeiten Hand in Hand, um die perfekte Vorschau zu erstellen. Wenn ein Nutzer deinen Link teilt, passiert im Hintergrund Folgendes: Der Crawler der Plattform (z.B. von Facebook) besucht deine Seite, liest den `<head>`-Bereich aus und sucht gezielt nach den Open Graph Tags.

1.  Er findet den `og:url` und weiß: "Okay, alle Interaktionen für diesen Link bündle ich unter dieser Adresse."
2.  Er findet den `og:title` und nutzt ihn als klickstarke Überschrift für die Vorschau.
3.  Er findet das `og:image` (und die dazugehörigen Helfer-Tags) und lädt dieses Bild als visuelles Aushängeschild.

Zusammen ergeben sie eine kohärente, ansprechende und technisch saubere Vorschau, die deine Inhalte im besten Licht präsentiert. Ein Blick in den Quelltext einer gut optimierten Seite zeigt dieses Trio in harmonischer Eintracht:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Eine detaillierte Analyse der Kaffeebohnenveredelung – Schmidt Kaffeemaschinen</title>

    <!-- Open Graph Basis-Tags -->
    <meta property="og:title" content="Das Geheimnis hinter dem perfekten Kaffee: So veredelst du jede Bohne!">
    <meta property="og:type" content="article">
    <meta property="og:image" content="https://www.deine-kaffee-seite.de/images/kaffeebohnen-veredeln.jpg">
    <meta property="og:image:width" content="1200">
    <meta property="og:image:height" content="630">
    <meta property="og:image:alt" content="Nahaufnahme von gerösteten Kaffeebohnen in einer Schale.">
    <meta property="og:url" content="https://www.deine-kaffee-seite.de/geheimnis-perfekter-kaffee">
    
    <!-- Weitere Metadaten ... -->
</head>
<body>
    <!-- ... Dein Seiteninhalt ... -->
</body>
</html>
```

Die Beherrschung dieser drei grundlegenden Open Graph Tags ist kein "Nice-to-have", sondern eine absolute Notwendigkeit für jeden, der Inhalte im Web erstellt und möchte, dass diese erfolgreich geteilt werden. Sie sind dein grundlegendes Werkzeug, um die Darstellung deiner Marke und deiner Botschaften auf den größten Kommunikationsplattformen der Welt selbst in die Hand zu nehmen.
