# Performance-Check

### Performance-Check: Die Jagd nach Millisekunden

Du hast es sicher schon selbst erlebt: Du klickst auf einen Link und starrst dann auf eine weiße Seite. Langsam, ganz langsam, bauen sich die ersten Elemente auf. Ein Bild erscheint, dann ein Textblock, und gerade als du auf einen Button klicken willst, springt das ganze Layout, weil eine Werbeanzeige nachgeladen wurde. Frustrierend, oder? Genau dieses Gefühl möchtest du den Besuchern deiner Website ersparen.

Nachdem du dein Projekt mit Inhalt gefüllt und mit CSS gestaltet hast, kommt ein entscheidender, oft vernachlässigter Schritt: der Feinschliff der Performance. In der Welt des Webs ist Geschwindigkeit keine Kür, sondern eine Pflicht. Eine schnelle Website sorgt nicht nur für zufriedene Nutzer, sondern wird auch von Suchmaschinen wie Google mit einem besseren Ranking belohnt. Es geht hier nicht um bloße Zahlen, sondern um die wahrgenommene Ladezeit – das Gefühl, dass eine Seite flüssig und reaktionsschnell ist.

#### Die Werkzeuge des Handwerks: Messen statt Raten

Bevor du anfängst, blind an deinem Code herumzuschrauben, musst du den aktuellen Zustand deiner Website analysieren. Bauchgefühl hilft hier nicht weiter. Die gute Nachricht ist, dass du die wichtigsten Werkzeuge bereits in deinem Browser findest: die Entwicklertools (meist erreichbar mit F12 oder Rechtsklick -> "Untersuchen").

Innerhalb dieser Tools ist der Reiter **Lighthouse** (manchmal auch "Audits") dein bester Freund. Lighthouse ist ein automatisiertes Werkzeug von Google, das deine Seite auf verschiedene Aspekte wie Performance, Barrierefreiheit, Best Practices und SEO überprüft. Für unser Thema ist der Performance-Score am wichtigsten.

Wenn du einen Lighthouse-Bericht für deine Seite erstellst, erhältst du nicht nur eine Punktzahl von 0 bis 100, sondern auch eine detaillierte Liste mit konkreten Metriken und Verbesserungsvorschlägen. Diese Vorschläge sind dein Fahrplan zur Optimierung. Lass uns die wichtigsten Metriken genauer ansehen, die Google unter dem Namen **Core Web Vitals** zusammenfasst.

#### Die entscheidenden Metriken: Core Web Vitals

Die Core Web Vitals sind drei spezifische Kennzahlen, die das Nutzererlebnis beim Laden einer Seite messen: Ladezeit, Interaktivität und visuelle Stabilität.

1.  **Largest Contentful Paint (LCP):** Diese Metrik misst, wie lange es dauert, bis das größte sichtbare Element (meist ein großes Bild, ein Video oder ein Textblock) im Viewport des Nutzers geladen ist. Ein guter LCP-Wert liegt unter 2,5 Sekunden. Er beantwortet die Frage des Nutzers: "Ist hier überhaupt was Relevantes?"

2.  **Interaction to Next Paint (INP):** Diese Metrik ist der Nachfolger von First Input Delay (FID) und misst die Reaktionsfähigkeit deiner Seite. Sie erfasst die Zeit von dem Moment, in dem ein Nutzer mit der Seite interagiert (z. B. ein Klick auf einen Button), bis der Browser eine visuelle Rückmeldung gibt. Stell dir vor, du klickst auf einen Akkordeon-Button und es dauert eine gefühlte Ewigkeit, bis er sich öffnet. Das ist ein schlechter INP. Ein guter Wert liegt unter 200 Millisekunden.

3.  **Cumulative Layout Shift (CLS):** Diese Metrik misst die visuelle Stabilität. Sie erfasst, wie stark sich Elemente auf der Seite unerwartet verschieben, während sie geladen wird. Das klassische Beispiel ist der Text, der nach unten rutscht, weil darüber ein Bild oder eine Werbeanzeige nachgeladen wird. Ein CLS-Wert nahe null ist ideal.

Neben diesen drei Hauptmetriken gibt dir Lighthouse auch Auskunft über weitere Kennzahlen wie den **First Contentful Paint (FCP)**, der misst, wann *irgendetwas* (Text, Bild, etc.) auf dem Bildschirm erscheint, und die **Time to Interactive (TTI)**, die den Zeitpunkt angibt, an dem die Seite vollständig interaktiv ist.

#### Die häufigsten Bremsklötze und wie du sie löst

Der Lighthouse-Bericht gibt dir bereits konkrete Hinweise. Die meisten Performance-Probleme lassen sich jedoch auf einige wenige, typische Ursachen zurückführen.

##### 1. Bilder, die ewige Bremse

Unoptimierte Bilder sind der häufigste Grund für langsame Ladezeiten. Ein Foto direkt aus der Digitalkamera hat oft mehrere Megabyte – viel zu groß für das Web.

*   **Richtige Dimensionen:** Lade ein Bild niemals in einer höheren Auflösung hoch, als es auf der Seite dargestellt wird. Wenn ein Bild auf deiner Website nur 800 Pixel breit angezeigt wird, sollte die Bilddatei auch nur 800 Pixel breit sein, nicht 4000.
*   **Moderne Formate:** Nutze moderne Bildformate wie **WebP** oder **AVIF**. Sie bieten bei gleicher visueller Qualität eine deutlich geringere Dateigröße als klassische JPEGs oder PNGs.
*   **Responsive Bilder:** Verwende das `<img>`-Element mit den Attributen `srcset` und `sizes`, um dem Browser verschiedene Bildgrößen für unterschiedliche Bildschirmbreiten anzubieten. So lädt ein Smartphone nicht unnötig das riesige Desktop-Bild.
*   **Lazy Loading:** Bilder, die nicht sofort sichtbar sind (z. B. weiter unten auf der Seite), müssen auch nicht sofort geladen werden. Mit dem Attribut `loading="lazy"` weist du den Browser an, diese Bilder erst dann zu laden, wenn der Nutzer in ihre Nähe scrollt.

Ein optimiertes Bild-Tag könnte so aussehen:

```html
<img 
  src="fallback-image.jpg"
  srcset="image-400w.webp 400w, 
          image-800w.webp 800w, 
          image-1200w.webp 1200w"
  sizes="(max-width: 600px) 400px, 
         (max-width: 1000px) 800px, 
         1200px"
  alt="Eine aussagekräftige Beschreibung des Bildes"
  width="1200"
  height="800"
  loading="lazy"
>
```

Achte auch darauf, immer `width` und `height` anzugeben. Dadurch reserviert der Browser den Platz für das Bild, noch bevor es geladen ist, und verhindert so einen Layout Shift (CLS).

##### 2. Renderblockierendes CSS und JavaScript

Wenn der Browser auf dein HTML stößt, fängt er an, die Seite von oben nach unten zu rendern. Trifft er dabei auf eine CSS- oder JavaScript-Datei, hält er inne, lädt die Datei herunter und führt sie aus, bevor er mit dem Rendern der restlichen Seite fortfährt. Dieses Verhalten blockiert das Rendering und verlangsamt die wahrgenommene Ladezeit.

*   **CSS optimieren:**
    *   CSS-Dateien gehören immer in den `<head>` deines HTML-Dokuments. So weiß der Browser frühzeitig, wie die Seite aussehen soll, und muss sie später nicht neu zeichnen.
    *   Halte dein CSS schlank. Entferne ungenutzte Regeln.
    *   **Minifiziere** deine CSS-Dateien. Dabei werden alle unnötigen Zeichen wie Leerzeichen und Kommentare entfernt, um die Dateigröße zu reduzieren. Tools hierfür sind in den meisten modernen Build-Prozessen (wie Vite oder Webpack) integriert.

*   **JavaScript optimieren:**
    *   JavaScript ist oft der größte Performance-Flaschenhals. Lade nur Skripte, die du wirklich brauchst.
    *   Platziere deine `<script>`-Tags möglichst am Ende des `<body>`, kurz vor dem schließenden `</body>`-Tag. Dadurch wird der HTML-Inhalt bereits angezeigt, während das Skript noch lädt.
    *   Noch besser ist die Verwendung der Attribute `defer` oder `async`.
        *   `<script defer src="mein-skript.js"></script>`: Der Browser lädt das Skript parallel zum Parsen des HTML herunter und führt es erst aus, wenn das HTML-Dokument vollständig analysiert wurde. Dies ist in den meisten Fällen die beste Wahl.
        *   `<script async src="mein-skript.js"></script>`: Der Browser lädt das Skript ebenfalls parallel, führt es aber aus, sobald es heruntergeladen ist, unabhängig vom HTML-Parsing. Dies kann das Rendering unterbrechen und ist nur für unabhängige Skripte (z. B. manche Tracking-Skripte) sinnvoll.

##### 3. Die Last der HTTP-Anfragen

Jede einzelne Datei (HTML, CSS, JS, Bilder, Schriftarten) erfordert eine separate Anfrage an den Server. Jede dieser Anfragen hat einen gewissen Overhead. Früher war es daher üblich, CSS- und JS-Dateien zu einer einzigen großen Datei zusammenzufassen ("Bundling"). Mit modernen Protokollen wie HTTP/2 und HTTP/3 ist das nicht mehr ganz so kritisch, aber die Regel bleibt: Weniger Anfragen sind meist besser.

Überprüfe im **Network**-Tab der Entwicklertools, was deine Seite alles lädt. Sei besonders kritisch bei Skripten von Drittanbietern (Analytics, Social-Media-Widgets, Werbenetzwerke). Jedes externe Skript ist ein potenzielles Risiko für die Performance und die Stabilität deiner Seite, da du keine Kontrolle darüber hast.

##### 4. Ein sauberes Fundament: Server und HTML

*   **Server-Antwortzeit (Time to First Byte - TTFB):** Selbst die bestoptimierte Seite ist langsam, wenn der Server ewig braucht, um die erste Antwort zu schicken. Ein gutes Hosting ist hier entscheidend.
*   **Caching:** Sorge dafür, dass der Browser statische Ressourcen wie CSS, JavaScript und Bilder zwischenspeichern kann. Dadurch müssen sie bei wiederholten Besuchen nicht erneut heruntergeladen werden. Die Konfiguration hierfür geschieht auf dem Server.
*   **Content Delivery Network (CDN):** Ein CDN speichert Kopien deiner Website auf Servern, die über die ganze Welt verteilt sind. Ein Nutzer aus Australien erhält die Daten dann von einem Server in Sydney statt aus Frankfurt, was die Ladezeit drastisch verkürzt.
*   **Schlankes HTML:** Ein überladenes, tief verschachteltes DOM verlangsamt das Rendern. Halte deine HTML-Struktur so einfach und semantisch wie möglich.

Performance-Optimierung ist ein iterativer Prozess. Du misst, du identifizierst einen Flaschenhals, du behebst ihn und du misst erneut. Schon kleine Änderungen, wie das Komprimieren eines Bildes oder das Hinzufügen von `defer` zu einem Skript, können eine spürbare Wirkung haben und aus einer frustrierend langsamen eine erfreulich schnelle Website machen.
