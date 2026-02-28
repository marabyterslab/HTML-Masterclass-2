# Core Web Vitals (LCP, CLS, FID)

### Core Web Vitals: Die Messung der Nutzererfahrung

Wenn du eine Website erstellst, denkst du wahrscheinlich zuerst an Inhalte, Design und Funktionalität. Das ist auch richtig so, denn das ist der Kern deines Angebots. Aber es gibt einen entscheidenden Aspekt, der oft übersehen wird und doch darüber entscheidet, ob Nutzer auf deiner Seite bleiben oder sie frustriert verlassen: die User Experience, also die Nutzererfahrung. Es geht nicht nur darum, *was* du anbietest, sondern auch *wie* du es anbietest. Eine langsame, instabile oder träge Seite kann selbst die besten Inhalte wertlos machen.

Google hat diesen Gedanken aufgegriffen und einen Satz von Metriken eingeführt, die genau diese Erfahrung messbar machen sollen: die Core Web Vitals. Sie sind keine abstrakten technischen Werte, sondern konzentrieren sich auf drei zentrale Aspekte der Nutzerwahrnehmung: die Ladeleistung, die Interaktivität und die visuelle Stabilität. Diese drei Säulen werden durch die Metriken Largest Contentful Paint (LCP), First Input Delay (FID) und Cumulative Layout Shift (CLS) repräsentiert. Lass uns diese drei Kennzahlen im Detail betrachten, denn sie sind entscheidend für den Erfolg deiner Webseite.

#### Largest Contentful Paint (LCP): Wie schnell wird das Wesentliche sichtbar?

Stell dir vor, du betrittst einen Raum. Du scannst ihn nicht Pixel für Pixel ab, sondern dein Blick fällt sofort auf das größte oder wichtigste Objekt – vielleicht ein großes Gemälde, ein Fenster mit einer tollen Aussicht oder eine Personengruppe. Ähnlich verhält es sich, wenn ein Nutzer deine Webseite aufruft. Der **Largest Contentful Paint (LCP)** misst die Zeit vom Beginn des Ladevorgangs bis zu dem Moment, in dem das größte sichtbare Bildelement oder der größte Textblock im sichtbaren Bereich (dem Viewport) vollständig gerendert ist.

Der LCP ist ein Indikator für die *wahrgenommene* Ladegeschwindigkeit. Er beantwortet die Frage des Nutzers: "Ist diese Seite nützlich für mich?" Wenn das Hauptelement – sei es das Hero-Image, die Überschrift eines Artikels oder ein Produktbild – schnell erscheint, vermittelt die Seite den Eindruck, schnell und einsatzbereit zu sein.

**Was sind gute LCP-Werte?**
- **Gut:** Unter 2,5 Sekunden
- **Verbesserungswürdig:** Zwischen 2,5 und 4 Sekunden
- **Schlecht:** Über 4 Sekunden

**Was verursacht einen schlechten LCP?**
Die häufigsten Übeltäter sind große Ressourcen, die das Rendering blockieren oder selbst lange zum Laden brauchen.
1.  **Langsame Server-Antwortzeiten:** Wenn dein Server lange braucht, um überhaupt die ersten Daten zu senden (hohe Time to First Byte, TTFB), verzögert sich alles Weitere.
2.  **Render-blockierendes JavaScript und CSS:** Wenn der Browser auf große CSS- oder JavaScript-Dateien warten muss, bevor er überhaupt mit dem Rendern der Hauptinhalte beginnen kann, leidet der LCP.
3.  **Große Mediendateien:** Ein riesiges, unkomprimiertes Bild im Header ist der klassische LCP-Killer. Auch Videos oder große Hintergrundbilder können hier problematisch sein.
4.  **Client-seitiges Rendering:** Frameworks, die die gesamte Seite erst im Browser des Nutzers mit JavaScript zusammensetzen, haben oft einen schlechten LCP, weil der Browser erst viel Code ausführen muss, bevor etwas Sichtbares erscheint.

**Wie kannst du deinen LCP verbessern?**
- **Optimiere Bilder:** Komprimiere deine Bilder, verwende moderne Formate wie WebP oder AVIF und nutze responsive Bilder mit dem `srcset`-Attribut, um für jedes Gerät die passende Größe auszuliefern.
- **Priorisiere kritische Ressourcen:** Du kannst dem Browser einen Hinweis geben, welche Ressource für den LCP entscheidend ist. Mit `<link rel="preload">` sorgst du dafür, dass das Hauptbild oder die wichtigste Schriftart früher geladen wird.

```html
<head>
  <link rel="preload" as="image" href="mein-wichtiges-hero-bild.webp">
</head>
```
- **Reduziere Render-blocking-Ressourcen:** Lade nur das CSS, das für den sichtbaren Bereich („above the fold“) wirklich nötig ist, direkt im HTML und den Rest asynchron. Verschiebe JavaScript-Dateien mit den Attributen `defer` oder `async` ans Ende des Ladevorgangs.
- **Nutze ein Content Delivery Network (CDN):** Ein CDN liefert deine Inhalte von Servern aus, die geografisch näher am Nutzer sind, was die Latenz und damit die Ladezeiten drastisch reduziert.

#### First Input Delay (FID): Wie schnell reagiert die Seite auf eine Aktion?

Du hast eine Seite geladen, siehst einen Button und klickst darauf. Und... nichts passiert. Du klickst nochmal. Immer noch nichts. Erst nach einer gefühlten Ewigkeit reagiert die Seite. Dieses frustrierende Erlebnis ist genau das, was der **First Input Delay (FID)** misst.

Der FID misst die Zeitspanne zwischen der *ersten* Interaktion eines Nutzers (z.B. ein Klick, ein Fingertipp) und dem Zeitpunkt, an dem der Browser tatsächlich in der Lage ist, auf diese Interaktion zu reagieren. Wichtig ist hier: Der FID misst nicht die gesamte Zeit der Ereignisverarbeitung, sondern nur die *Verzögerung* davor. Es ist die Wartezeit in der Schlange, bevor du überhaupt bedient wirst.

Ein hoher FID entsteht fast immer, wenn der Haupt-Thread des Browsers blockiert ist. Der Haupt-Thread ist so etwas wie der fleißige Hauptarbeiter des Browsers: Er ist für das Parsen von HTML, das Ausführen von CSS und JavaScript und das Reagieren auf Nutzereingaben zuständig. Wenn er gerade mit einer langen, komplexen JavaScript-Aufgabe beschäftigt ist, kann er nicht gleichzeitig auf deinen Klick reagieren. Die Interaktion muss warten, bis die aktuelle Aufgabe abgeschlossen ist.

**Was sind gute FID-Werte?**
- **Gut:** Unter 100 Millisekunden
- **Verbesserungswürdig:** Zwischen 100 und 300 Millisekunden
- **Schlecht:** Über 300 Millisekunden

**Was verursacht einen schlechten FID?**
- **Lange JavaScript-Tasks:** Große Skripte, die komplexe Berechnungen durchführen oder das DOM stark manipulieren, können den Haupt-Thread für längere Zeit blockieren.
- **Unoptimierte JavaScript-Frameworks:** Manche Frameworks erzeugen bei der Initialisierung der Seite sehr viel Arbeit für den Browser.
- **Skripte von Drittanbietern:** Analyse-Tools, Werbe-Skripte oder Social-Media-Widgets können ebenfalls massive JavaScript-Aufgaben ausführen und die Reaktionsfähigkeit deiner Seite beeinträchtigen.

**Wie kannst du deinen FID verbessern?**
- **Teile lange Aufgaben auf:** Statt eines riesigen JavaScript-Blocks, der 500ms läuft, kannst du diesen in fünf kleinere Blöcke à 100ms aufteilen. Zwischen diesen Blöcken hat der Browser dann Zeit, auf Nutzereingaben zu reagieren.
- **Nutze `async` und `defer`:** Sorge dafür, dass unwichtige Skripte das Laden der Seite nicht blockieren.

```html
<!-- Defer verschiebt die Ausführung, bis das HTML geparst ist -->
<script defer src="mein-skript.js"></script>

<!-- Async lädt parallel und führt aus, sobald verfügbar -->
<script async src="analyse-tool.js"></script>
```
- **Verwende Web Worker:** Für sehr rechenintensive Aufgaben, die nicht direkt das UI betreffen, kannst du Web Worker nutzen. Sie führen JavaScript in einem separaten Hintergrund-Thread aus und blockieren so nicht den Haupt-Thread.
- **Überprüfe deine Third-Party-Skripte:** Analysiere, welche externen Skripte deine Seite verlangsamen, und überlege, ob du sie wirklich alle brauchst oder ob es performantere Alternativen gibt.

Ein kleiner Ausblick: Google entwickelt die Metriken stetig weiter. Der FID wird zukünftig durch die umfassendere Metrik **Interaction to Next Paint (INP)** ersetzt. Während FID nur die Verzögerung der *ersten* Interaktion misst, bewertet INP die Latenz *aller* Interaktionen während des gesamten Seitenbesuchs und gibt so ein noch besseres Bild der allgemeinen Reaktionsfähigkeit.

#### Cumulative Layout Shift (CLS): Wie stabil ist das Layout?

Das ist vielleicht der nervigste aller schlechten Nutzererfahrungen. Du liest einen Artikel und möchtest auf einen Link tippen. Doch genau in dem Moment, in dem dein Finger den Bildschirm berührt, lädt ein Werbebanner über dem Text, verschiebt den gesamten Inhalt nach unten, und du tippst versehentlich auf die Werbung. Das ist ein Layout Shift. Der **Cumulative Layout Shift (CLS)** misst die Summe aller unerwarteten Layout-Verschiebungen, die während der gesamten Lebensdauer einer Seite auftreten.

Ein guter CLS-Wert bedeutet, dass sich die Elemente auf deiner Seite nach dem ersten Laden nicht mehr unvorhersehbar bewegen. Die Seite fühlt sich stabil und zuverlässig an. Ein schlechter Wert hingegen sorgt für Frust und kann Nutzer zu ungewollten Aktionen verleiten.

Der CLS wird als dimensionsloser Score berechnet, der sich aus zwei Faktoren zusammensetzt: dem Anteil des sichtbaren Bereichs, der von der Verschiebung betroffen ist (Impact Fraction), und der Distanz, um die sich die Elemente verschoben haben (Distance Fraction).

**Was sind gute CLS-Werte?**
- **Gut:** Unter 0,1
- **Verbesserungswürdig:** Zwischen 0,1 und 0,25
- **Schlecht:** Über 0,25

**Was verursacht einen schlechten CLS?**
- **Bilder ohne feste Dimensionen:** Wenn du ein `<img>`-Element ohne `width`- und `height`-Attribute einfügst, weiß der Browser nicht, wie viel Platz er dafür reservieren soll. Er rendert erst den Text, und wenn das Bild dann geladen ist, springt der Text plötzlich nach unten.
- **Werbung, Einbettungen und iframes ohne reservierten Platz:** Ähnlich wie bei Bildern, wenn dynamisch geladene Inhalte keinen fest definierten Platzhalter haben, drücken sie beim Erscheinen den restlichen Inhalt zur Seite.
- **Web-Schriftarten, die Layout-Shifts verursachen:** Wenn eine Systemschriftart angezeigt wird und später durch eine Web-Schriftart ersetzt wird, die andere Abmessungen hat, kann dies den gesamten Textfluss verändern und zu Verschiebungen führen (Flash of Unstyled Text, FOUT).
- **Dynamisch hinzugefügte Inhalte:** Wenn du beispielsweise ein "Cookie-Banner" am oberen Rand der Seite einblendest, nachdem der Hauptinhalt bereits sichtbar ist, drückt dieses Banner alles nach unten.

**Wie kannst du deinen CLS verbessern?**
- **Gib Bildern und Videos immer Dimensionen an:** Der einfachste und wichtigste Fix. Gib `width` und `height` direkt im HTML an. Der Browser kann dann das Seitenverhältnis berechnen und den korrekten Platz reservieren, noch bevor das Bild geladen ist.

```html
<!-- So nicht: -->
<img src="katzenbild.jpg">

<!-- Besser so: -->
<img src="katzenbild.jpg" width="400" height="300" alt="Süße Katze">
```
Moderne CSS-Eigenschaften wie `aspect-ratio` können hierbei ebenfalls hervorragend unterstützen.
- **Reserviere Platz für dynamische Inhalte:** Wenn du weißt, dass an einer bestimmten Stelle eine Werbung oder ein anderes Widget geladen wird, erstelle einen Container-`div` mit einer festen `min-height`, der den Platz freihält.
- **Optimiere das Laden von Schriftarten:** Verwende `font-display: swap;` in deiner `@font-face`-Regel, um die Zeit zu minimieren, in der Text unsichtbar ist. Lade wichtige Schriftarten vorab mit `<link rel="preload">`, um Layout-Shifts durch Schriftart-Tausch zu reduzieren.
- **Vermeide Animationen, die das Layout verändern:** Nutze für Animationen CSS-Eigenschaften wie `transform` anstelle von `top`, `left` oder `margin`, da `transform` keine Neuberechnung des Layouts auslöst.

Die Core Web Vitals sind mehr als nur technische Kennzahlen für Suchmaschinen. Sie sind ein Kompass, der dir hilft, deine Webseite aus der Perspektive deiner Nutzer zu sehen und zu optimieren. Eine schnelle, reaktionsschnelle und stabile Seite ist die Grundlage für eine positive Erfahrung – und zufriedene Nutzer sind die, die wiederkommen.
