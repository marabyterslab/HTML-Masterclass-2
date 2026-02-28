# Lazy Loading mit loading=lazy

### Lazy Loading: Bilder und iframes erst bei Bedarf laden

Stell dir vor, du besuchst eine Webseite, die einen langen Artikel mit vielen Bildern enthält. Klassischerweise würde dein Browser versuchen, sofort beim ersten Aufruf alle Inhalte dieser Seite zu laden – das HTML, das CSS, das JavaScript und eben auch jedes einzelne Bild, vom ersten bis zum allerletzten im Footer. Das ist so, als würdest du ein Restaurant betreten und der Kellner würde dir sofort alle Gänge des Menüs gleichzeitig auf den Tisch stellen, obwohl du erst bei der Vorspeise bist. Das Ergebnis: ein überladener Tisch, eine längere Wartezeit zu Beginn und eine Menge Essen, das du vielleicht gar nicht anrührst.

Im Web führt dieses Verhalten zu längeren Ladezeiten, einem höheren Datenverbrauch (besonders kritisch auf mobilen Geräten mit begrenztem Datenvolumen) und einer schlechteren Nutzererfahrung. Die Lösung für dieses Problem ist eine Technik, die sich „Lazy Loading“ nennt – das „faule Laden“. Die Idee dahinter ist bestechend einfach: Lade eine Ressource, wie ein Bild oder einen iframe, erst dann, wenn sie tatsächlich gebraucht wird, also kurz bevor sie in den sichtbaren Bereich des Nutzers (den sogenannten „Viewport“) scrollt.

#### Der alte Weg: Komplexität mit JavaScript

Bevor HTML eine native Lösung anbot, war Lazy Loading eine Angelegenheit für JavaScript. Entwickler mussten auf Bibliotheken zurückgreifen oder eigene Skripte schreiben, die ständig die Scroll-Position des Nutzers überwachten. Sie prüften, welche Bilder sich dem Viewport näherten, und tauschten dann dynamisch einen Platzhalter (oft ein kleines, unscharfes Bild oder eine `data-src`-Attribut) gegen das eigentliche `src`-Attribut aus, um den Ladevorgang auszulösen.

Diese Methode funktionierte, brachte aber auch Nachteile mit sich:
- **Zusätzliches JavaScript:** Jede Webseite musste zusätzlichen Code laden und ausführen, was die Komplexität und die Ladezeit potenziell erhöhte.
- **Performance-Overhead:** Das ständige Überwachen der Scroll-Position kann, wenn es nicht gut optimiert ist, die Leistung der Seite beeinträchtigen.
- **Wartungsaufwand:** Man war von externen Bibliotheken abhängig oder musste eigenen Code pflegen.

Moderne JavaScript-Lösungen nutzen die `Intersection Observer API`, die wesentlich performanter ist, aber immer noch die Implementierung von JavaScript erfordert. Doch die gute Nachricht ist: Für den Großteil aller Anwendungsfälle brauchst du das heute nicht mehr.

#### Die native Lösung: Das `loading`-Attribut

Mit der Einführung des `loading`-Attributs hat HTML eine elegante und extrem einfache Möglichkeit geschaffen, Lazy Loading direkt im Browser zu steuern – ganz ohne eine einzige Zeile JavaScript. Dieses Attribut kann auf `<img>`- und `<iframe>`-Tags angewendet werden und teilt dem Browser mit, wie er die Lade-Priorität dieser Elemente behandeln soll.

Das Attribut kennt zwei Hauptwerte:

1.  `loading="lazy"`
2.  `loading="eager"`

Schauen wir uns an, was sie bedeuten.

##### `loading="lazy"`: Das Warten auf den richtigen Moment

Wenn du einem Bild oder iframe `loading="lazy"` hinzufügst, gibst du dem Browser die Anweisung: „Lade diese Ressource erst, wenn der Nutzer kurz davor ist, sie zu sehen.“

```html
<img src="schönes-bild-weiter-unten.jpg" 
     alt="Ein schönes Bild, das weiter unten auf der Seite erscheint."
     loading="lazy"
     width="800"
     height="600">
```

Der Browser lädt dieses Bild nicht sofort beim initialen Seitenaufbau. Stattdessen wartet er, bis der Nutzer so weit nach unten scrollt, dass sich das Bild dem sichtbaren Bereich nähert. „Nähert“ ist hier ein wichtiger Punkt: Der Browser ist clever genug, das Bild nicht erst dann zu laden, wenn es exakt im Viewport ist, sondern schon ein Stückchen davor. So wird sichergestellt, dass das Bild bereits geladen ist, wenn der Nutzer es erreicht, und keine unschöne leere Fläche entsteht. Dieser Puffer variiert je nach Browser und der Verbindungsgeschwindigkeit des Nutzers.

##### `loading="eager"`: Sofort laden, ohne Verzögerung

Der Wert `eager` bewirkt das genaue Gegenteil. Er weist den Browser an, die Ressource sofort zu laden, unabhängig davon, wo sie sich auf der Seite befindet.

```html
<img src="wichtiges-logo-im-header.png" 
     alt="Unser Firmenlogo."
     loading="eager"
     width="200"
     height="50">
```

Das ist das traditionelle Ladeverhalten. Tatsächlich ist `eager` der Standardwert, den der Browser annimmt, wenn du das `loading`-Attribut komplett weglässt. Warum sollte man es also explizit setzen? Es kann die Lesbarkeit deines Codes verbessern und deine Absicht klarstellen, besonders für Bilder, die für den ersten Eindruck der Seite entscheidend sind (dazu gleich mehr).

#### Best Practices: Wann du was verwenden solltest

Die Einführung des `loading`-Attributs bedeutet nicht, dass du es blind auf jedes einzelne Bild anwenden solltest. Wie bei jedem Werkzeug kommt es auf den richtigen Einsatz an.

##### Bilder „Above the Fold“ (im direkt sichtbaren Bereich)

Bilder, die sich beim ersten Laden der Seite sofort im sichtbaren Bereich befinden, sollten **niemals** mit `loading="lazy"` versehen werden. Dazu gehören zum Beispiel:
- Dein Logo im Header
- Ein großes Hero-Image oder Banner direkt unter der Navigation
- Produktbilder auf einer Detailseite, die sofort sichtbar sind

Wenn du diese kritischen Bilder verzögert lädst, verschlechterst du die wahrgenommene Ladezeit. Der Nutzer starrt auf eine leere Fläche, während er darauf wartet, dass der wichtigste Inhalt erscheint. Dies wirkt sich negativ auf den sogenannten **Largest Contentful Paint (LCP)** aus, einen der wichtigsten Messwerte für die Web-Performance (Core Web Vitals).

**Regel:** Für alle Bilder, die sofort sichtbar sind, verwende `loading="eager"` oder lass das Attribut einfach weg.

##### Bilder „Below the Fold“ (außerhalb des sichtbaren Bereichs)

Jedes Bild, das der Nutzer erst durch Scrollen erreichen muss, ist ein perfekter Kandidat für `loading="lazy"`. Das sind zum Beispiel:
- Bilder in langen Blogartikeln
- Vorschaubilder in einer Fotogalerie
- Produktbilder in einer langen Kategorieseite
- Icons und Grafiken im Footer der Webseite

Hier entfaltet Lazy Loading sein volles Potenzial: Die initiale Ladezeit der Seite wird drastisch verkürzt, da der Browser sich nur auf die sichtbaren Inhalte konzentrieren muss.

**Regel:** Für alle Bilder, die nicht sofort sichtbar sind, ist `loading="lazy"` die beste Wahl.

```html
<!-- Oben auf der Seite: Sofort laden -->
<header>
  <img src="logo.svg" alt="Logo" width="150" height="40"> <!-- loading="eager" ist Standard -->
</header>
<main>
  <img src="hero-banner.jpg" alt="Willkommens-Banner" width="1200" height="400">

  <h1>Unser fantastischer Artikel</h1>
  <p>Einleitungstext, der sofort sichtbar ist...</p>

  <!-- Weiter unten im Artikel: Verzögert laden -->
  <p>Viel Text später kommt dann dieses Bild...</p>
  <img src="bild-mitten-im-text.jpg" 
       alt="Eine Illustration zum Thema."
       loading="lazy"
       width="600"
       height="400">
  
  <p>Und noch viel mehr Text...</p>
  <img src="weiteres-bild-im-text.jpg" 
       alt="Eine weitere Illustration."
       loading="lazy"
       width="600"
       height="400">
</main>
```

#### Lazy Loading für iframes: Ein echter Performance-Gewinn

Noch wichtiger als bei Bildern ist der Einsatz von `loading="lazy"` bei `<iframe>`-Elementen. Ein iframe lädt eine komplette, eigenständige Webseite in deine Seite hinein. Das bedeutet, er bringt sein eigenes HTML, CSS, JavaScript und seine eigenen Bilder mit. Das ist ein enormer Aufwand, der oft unnötig ist, wenn sich der iframe weit unten auf der Seite befindet.

Typische Anwendungsfälle für iframes, die von Lazy Loading stark profitieren, sind:
- Eingebettete YouTube- oder Vimeo-Videos
- Google-Maps-Karten
- Social-Media-Widgets (z. B. eine Twitter-Timeline)
- Werbebanner

Ein YouTube-Video-Embed kann leicht über ein Megabyte an Daten nachladen. Wenn sich dieses Video im Footer befindet, ist es eine enorme Verschwendung von Ressourcen, es sofort zu laden.

```html
<!-- Eine eingebettete Karte, die erst beim Scrollen geladen wird -->
<iframe src="https://www.google.com/maps/embed?..."
        width="600"
        height="450"
        style="border:0;"
        allowfullscreen=""
        loading="lazy"
        title="Standort unseres Büros auf Google Maps">
</iframe>
```

Indem du hier `loading="lazy"` hinzufügst, verbesserst du die Performance deiner Seite dramatisch, ohne dass der Nutzer einen Nachteil bemerkt.

#### Ein unverzichtbarer Partner: `width` und `height`

Wenn du Lazy Loading verwendest, gibt es eine Sache, die du unbedingt beachten musst: Gib deinen Bildern und iframes immer explizite `width`- und `height`-Attribute.

Warum ist das so wichtig? Wenn ein Bild noch nicht geladen ist, weiß der Browser nicht, wie viel Platz er dafür reservieren soll. Sobald das Bild dann durch Scrollen geladen wird, springt der Inhalt der Seite plötzlich nach unten, um Platz für das Bild zu machen. Dieses Springen wird als **Cumulative Layout Shift (CLS)** bezeichnet und ist extrem störend für den Nutzer. Es ist ebenfalls ein Core Web Vital, den es zu vermeiden gilt.

Durch die Angabe von `width` und `height` kann der Browser das Seitenverhältnis des Bildes berechnen und von Anfang an den korrekten Platz im Layout reservieren, auch wenn das Bild selbst noch nicht geladen ist. So bleibt das Layout stabil, und es kommt zu keinen unschönen Verschiebungen.

```html
<!-- Gut: Platz wird reserviert, kein Layout-Shift beim Laden -->
<img src="beispiel.jpg" 
     alt="Ein Beispielbild."
     loading="lazy"
     width="1280"
     height="720">

<!-- Schlecht: Der Browser weiß nicht, wie groß das Bild ist, was zu Layout-Shifts führt -->
<img src="beispiel.jpg" 
     alt="Ein Beispielbild."
     loading="lazy">
```

#### Browser-Kompatibilität und Fallback

Die Unterstützung für das `loading`-Attribut ist in allen modernen Browsern (Chrome, Firefox, Safari, Edge) hervorragend. Aber was passiert in älteren Browsern, die das Attribut nicht kennen?

Die Antwort ist erfreulich einfach: Sie ignorieren es. Ein alter Browser, der `loading="lazy"` nicht versteht, wird das Bild einfach so laden, wie er es immer getan hat – also sofort. Das bedeutet, die Webseite funktioniert weiterhin einwandfrei. Du bekommst zwar nicht den Performance-Vorteil des Lazy Loadings, aber es geht auch nichts kaputt. Dieses Prinzip nennt man „Graceful Degradation“ (würdevolles Altern). Für die allermeisten Webseiten ist dieser Ansatz heute völlig ausreichend.
