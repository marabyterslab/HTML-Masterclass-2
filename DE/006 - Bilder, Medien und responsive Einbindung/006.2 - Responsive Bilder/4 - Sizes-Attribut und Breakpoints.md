# Sizes-Attribut und Breakpoints

### Das `sizes`-Attribut und Breakpoints: Bilder in der richtigen Größe servieren

Im letzten Kapitel haben wir das `srcset`-Attribut kennengelernt. Du weißt jetzt, wie du dem Browser ein Menü verschiedener Bildgrößen zur Verfügung stellst, damit er die passende Datei für die Pixeldichte des jeweiligen Displays auswählen kann. Mit dem `w`-Deskriptor haben wir dem Browser sogar die tatsächliche Breite jeder Bilddatei mitgeteilt. Das ist ein gewaltiger Schritt nach vorn für die Performance und die Bildqualität.

Aber eine entscheidende Information fehlt dem Browser noch. Stell dir vor, du gibst ihm eine Speisekarte mit kleinen, mittleren und großen Portionen (`srcset`). Der Browser weiß, wie groß sein Magen ist (die Auflösung des Viewports), aber er weiß nicht, für welchen Anlass das Essen ist. Ist es nur ein kleiner Snack am Rande oder die Hauptspeise, die den ganzen Teller füllen soll?

Genau dieses Problem löst das `sizes`-Attribut. Es schließt die Lücke zwischen den verfügbaren Bildgrößen (`srcset`) und dem tatsächlichen Platz, den ein Bild im Layout deiner Webseite einnehmen wird. Ohne `sizes` muss der Browser eine Annahme treffen – und die ist meistens: Das Bild füllt die gesamte Breite des Viewports. Das führt oft dazu, dass er eine viel zu große Bilddatei herunterlädt.

#### Die Aufgabe des `sizes`-Attributs

Das `sizes`-Attribut ist dein direkter Draht zum Browser, um ihm mitzuteilen: „Hey, hör zu, dieses Bild wird unter bestimmten Bedingungen so und so viel Platz auf dem Bildschirm einnehmen.“ Du gibst ihm quasi eine Bauanleitung für dein Layout, bevor das CSS überhaupt vollständig geladen und interpretiert wurde.

Diese Information ist entscheidend, denn der Browser trifft die Entscheidung für den Bild-Download sehr früh im Ladevorgang – oft, bevor er weiß, wie dein CSS das Layout am Ende gestalten wird. Mit `sizes` gibst du ihm die nötigen Hinweise, um eine intelligente, vorausschauende Entscheidung zu treffen.

Die Syntax von `sizes` mag auf den ersten Blick etwas gewöhnungsbedürftig aussehen, aber sie ist logisch aufgebaut. Sie besteht aus einer Liste von Paaren, getrennt durch Kommas:

1.  **Eine Medienbedingung (Media Condition):** Das ist im Grunde eine Media Query, wie du sie aus CSS kennst, zum Beispiel `(max-width: 600px)`. Sie definiert einen bestimmten Breakpoint oder eine Bedingung für den Viewport.
2.  **Eine Breitenangabe:** Das ist die Breite, die das Bild einnimmt, *wenn die Medienbedingung zutrifft*. Diese Breite wird nicht in Prozent, sondern relativ zum Viewport oder in festen Einheiten angegeben.

Der letzte Eintrag in der Liste hat keine Medienbedingung. Er dient als Standardwert (Default), der greift, wenn keine der vorherigen Bedingungen zutrifft.

Schauen wir uns ein einfaches Beispiel an. Ein Bild, das immer die volle Breite des Viewports einnimmt (z. B. ein Hero-Image).

```html
<img srcset="held-480w.jpg 480w,
             held-800w.jpg 800w,
             held-1200w.jpg 1200w,
             held-1600w.jpg 1600w"
     sizes="100vw"
     src="held-800w.jpg"
     alt="Eine Berglandschaft im Sonnenaufgang.">
```

Hier ist `sizes="100vw"` die Anweisung an den Browser. `vw` steht für „Viewport Width“. `100vw` bedeutet also „100 % der Breite des Viewports“.

Was passiert nun?
- Der Browser sieht ein Gerät mit einer Breite von 375px.
- Dank `sizes="100vw"` weiß er: Das Bild wird 375px breit sein.
- Er schaut in `srcset` nach der kleinsten Datei, die mindestens 375px breit ist. Das ist `held-480w.jpg`. Perfekt. Eine kleine, schnelle Datei wird geladen.
- Auf einem Tablet mit 780px Breite rechnet er: Das Bild wird 780px breit sein. Er wählt `held-800w.jpg`.
- Auf einem Desktop mit 1440px Breite wählt er `held-1600w.jpg`.

Ohne `sizes` hätte der Browser vielleicht angenommen, das Bild füllt den ganzen Bildschirm und hätte auf dem kleinen 375px-Gerät trotzdem die `held-1600w.jpg` geladen – eine massive Verschwendung von Daten und Ladezeit.

#### Wenn das Layout komplexer wird: Breakpoints in Aktion

Die wahre Stärke von `sizes` zeigt sich in Layouts, die sich an verschiedenen Breakpoints ändern. Stell dir einen typischen Blog-Artikel vor.

- Auf kleinen Bildschirmen (z. B. unter 700px) soll das Artikelbild die volle Breite einnehmen.
- Auf größeren Bildschirmen ist der Artikeltext in einer Spalte, die maximal 700px breit ist. Das Bild soll sich dieser Breite anpassen.

Dein CSS könnte etwa so aussehen:

```css
.artikel-bild {
    width: 100%; /* Standard für kleine Bildschirme */
    height: auto;
}

@media (min-width: 700px) {
    .artikel-bild {
        max-width: 700px; /* Begrenzung auf großen Bildschirmen */
    }
}
```

Wie übersetzt du diese Logik nun in das `sizes`-Attribut? Du beschreibst das Verhalten des Bildes aus Sicht des Viewports.

```html
<img srcset="artikel-480w.jpg 480w,
             artikel-700w.jpg 700w,
             artikel-900w.jpg 900w"
     sizes="(min-width: 700px) 700px, 100vw"
     src="artikel-700w.jpg"
     alt="Ein aufgeschlagenes Buch auf einem Holztisch.">
```

Lass uns diesen `sizes`-Wert zerlegen: `(min-width: 700px) 700px, 100vw`.
Der Browser liest das von links nach rechts:

1.  **Prüfe die erste Bedingung:** Ist die Viewport-Breite mindestens 700px (`min-width: 700px`)?
    - **Ja?** Super. Dann nimm den zugehörigen Wert: Das Bild wird `700px` breit sein. Der Browser sucht nun in `srcset` nach der passenden Datei (in diesem Fall `artikel-700w.jpg` oder `artikel-900w.jpg`, je nach Pixeldichte).
    - **Nein?** Dann gehe zur nächsten Option.

2.  **Die nächste Option ist `100vw`**. Dieser Wert hat keine Bedingung, er ist der Standardwert (Fallback).
    - Wenn der Viewport also schmaler als 700px ist (z. B. 400px), greift dieser Wert. Der Browser weiß: Das Bild wird `100vw`, also 400px breit sein. Er wird die `artikel-480w.jpg`-Datei laden.

Du siehst, das `sizes`-Attribut ist eine exakte Abbildung deiner CSS-Layout-Regeln, nur in einer Form, die der Browser schon vor dem CSS-Rendering versteht.

#### Ein fortgeschrittenes Beispiel: Spalten-Layouts

Noch deutlicher wird der Nutzen bei mehrspaltigen Layouts. Stell dir eine Galerie vor:

- Unter 600px: Jedes Bild ist in einer eigenen Reihe (100 % breit).
- Zwischen 600px und 900px: Zwei Bilder pro Reihe (ca. 50 % breit).
- Über 900px: Drei Bilder pro Reihe (ca. 33 % breit).

Wir müssen diese Logik jetzt in `sizes` abbilden. Wir nehmen an, dass zwischen den Bildern ein kleiner Abstand ist, daher sind die Breiten nicht exakt 50 % oder 33 %. Nehmen wir an, das Layout füllt nicht die ganze Viewport-Breite, sondern hat links und rechts etwas Rand.

```html
<img srcset="galerie-320w.jpg 320w,
             galerie-450w.jpg 450w,
             galerie-600w.jpg 600w"
     sizes="(min-width: 900px) 33vw, (min-width: 600px) 50vw, 100vw"
     src="galerie-450w.jpg"
     alt="Nahaufnahme einer bunten Blume.">
```

Lass uns den Entscheidungsprozess des Browsers nachvollziehen:

- **Viewport ist 1200px breit:**
    - `(min-width: 900px)` trifft zu. Das Bild wird also `33vw` breit sein. 33 % von 1200px sind ca. 396px. Der Browser lädt `galerie-450w.jpg`.

- **Viewport ist 750px breit:**
    - `(min-width: 900px)` trifft nicht zu.
    - `(min-width: 600px)` trifft zu. Das Bild wird `50vw` breit sein. 50 % von 750px sind 375px. Der Browser lädt ebenfalls `galerie-450w.jpg`.

- **Viewport ist 400px breit:**
    - Keine der Medienbedingungen trifft zu.
    - Der Standardwert `100vw` greift. Das Bild wird `100vw`, also 400px breit sein. Der Browser lädt `galerie-450w.jpg`.

Die Reihenfolge der Bedingungen im `sizes`-Attribut spielt übrigens keine Rolle, da der Browser einfach die erste zutreffende Bedingung auswertet. Es hat sich jedoch bewährt, eine logische Reihenfolge (z. B. von groß nach klein) beizubehalten, damit der Code für dich und andere Entwickler lesbar bleibt.

#### Die Präzision mit `calc()` erhöhen

Manchmal reichen `vw`-Angaben nicht aus, weil dein Layout feste Abstände (Paddings, Margins, Gaps) hat. Dein CSS für das Drei-Spalten-Layout könnte zum Beispiel so aussehen:

```css
.galerie {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem; /* 16px Abstand */
    padding: 1rem;
}
```

Hier ist die Bildbreite nicht einfach `33vw`. Es ist komplizierter. Glücklicherweise kannst du im `sizes`-Attribut die CSS-Funktion `calc()` verwenden, um diese Komplexität abzubilden.

Die Berechnung für eine Spalte wäre ungefähr: `(100vw - Gesamtpadding - Gesamtgaps) / 3`.
Das `sizes`-Attribut könnte dann so aussehen:

```html
<img ...
     sizes="(min-width: 900px) calc((100vw - 4rem) / 3), 
            (min-width: 600px) calc((100vw - 3rem) / 2), 
            calc(100vw - 2rem)"
     ...>
```
Hier wird es schon sehr spezifisch und erfordert, dass du dein CSS-Layout genau kennst. Aber diese Präzision sorgt dafür, dass der Browser eine noch bessere Entscheidung treffen kann und wirklich nur die Pixel lädt, die absolut notwendig sind.

#### Eine wichtige Verbindung: `sizes` und CSS

Das `sizes`-Attribut ist kein Ersatz für CSS. Es ist eine HTML-basierte Information für den Browser, die dein CSS-Layout widerspiegeln sollte. Das ist ein entscheidender Punkt: **Wenn du dein CSS-Layout änderst, musst du auch das `sizes`-Attribut im HTML anpassen.**

Veränderst du zum Beispiel einen Breakpoint von `900px` auf `1024px` in deiner CSS-Datei, aber vergisst, dies im `sizes`-Attribut nachzuziehen, lieferst du dem Browser falsche Informationen. Er wird dann weiterhin basierend auf dem 900px-Breakpoint die Bilder laden, was zu suboptimalen Ergebnissen führt. `sizes` und CSS gehen Hand in Hand.

Das Zusammenspiel von `srcset` und `sizes` ist die moderne, leistungsstärkste Methode, um responsive Bilder in Webseiten einzubinden. Es gibt dem Browser die volle Kontrolle und alle notwendigen Informationen, um für jeden Nutzer, auf jedem Gerät und bei jeder Verbindungsgeschwindigkeit die bestmögliche Erfahrung zu schaffen: gestochen scharfe Bilder, die blitzschnell laden.
