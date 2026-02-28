# Responsive Images (srcset)

### Responsive Images mit `srcset` – Das richtige Bild für jedes Gerät

In den Anfängen des Webs war die Welt einfach. Du hattest ein Bild, und das hast du mit einem `<img>`-Tag und einem `src`-Attribut in deine Seite eingebunden. Dieses eine Bild wurde dann allen Nutzern angezeigt, egal ob sie mit einem riesigen Desktop-Monitor oder einem winzigen Handy-Bildschirm auf deine Seite kamen. Aus heutiger Sicht ist das eine massive Performance-Bremse und eine Verschwendung von Daten. Stell dir vor, ein Nutzer mit einer langsamen mobilen Internetverbindung muss ein 4000 Pixel breites Bild herunterladen, nur um es auf einem 360 Pixel breiten Display anzusehen. Das ist nicht nur frustrierend für den Nutzer, sondern verbraucht auch unnötig viel Datenvolumen.

Genau hier setzt das Konzept der responsiven Bilder an. Die Idee ist einfach: Statt eines einzigen Bildes für alle bietest du dem Browser eine Auswahl an verschiedenen Bildgrößen an. Der Browser, der die Gegebenheiten des Nutzers am besten kennt (Bildschirmgröße, Pixeldichte, Netzwerkgeschwindigkeit), kann dann selbst die am besten geeignete Version auswählen und herunterladen. Das wichtigste Werkzeug, das uns HTML dafür an die Hand gibt, ist das `srcset`-Attribut.

#### Die Anatomie des `srcset`-Attributs

Das `srcset`-Attribut erweitert das klassische `<img>`-Tag. Du übergibst ihm nicht nur eine einzige Bildquelle, sondern eine durch Kommas getrennte Liste von Bildkandidaten. Jeder Kandidat besteht aus zwei Teilen: der URL zum Bild und einem sogenannten Deskriptor, der das Bild beschreibt.

Es gibt zwei Arten von Deskriptoren, die du verwenden kannst:

1.  **Der Width-Deskriptor (`w`):** Er beschreibt die tatsächliche, intrinsische Breite des Bildes in Pixeln.
2.  **Der Pixel-Density-Deskriptor (`x`):** Er beschreibt, für welche Geräte-Pixeldichte das Bild optimiert ist (z. B. `2x` für Retina-Displays).

Obwohl der `x`-Deskriptor einfacher erscheint, ist der `w`-Deskriptor in den meisten Fällen die mächtigere und flexiblere Wahl. Schauen wir uns beide im Detail an.

#### Der Width-Deskriptor (`w`) – Die bevorzugte Methode

Der Width-Deskriptor ist die moderne und empfohlene Art, responsive Bilder umzusetzen, insbesondere in einem flexiblen, responsiven Layout. Du teilst dem Browser mit, wie breit jede Bilddatei in Wirklichkeit ist.

Ein einfaches Beispiel könnte so aussehen:

```html
<img src="bild-klein.jpg"
     srcset="bild-klein.jpg 480w,
             bild-mittel.jpg 800w,
             bild-gross.jpg 1200w"
     alt="Ein beschreibender Alternativtext.">
```

Was passiert hier?

*   Wir bieten dem Browser drei Versionen eines Bildes an.
*   `bild-klein.jpg 480w`: Diese Bilddatei ist 480 Pixel breit.
*   `bild-mittel.jpg 800w`: Diese Datei ist 800 Pixel breit.
*   `bild-gross.jpg 1200w`: Und diese ist 1200 Pixel breit.

Du gibst dem Browser also eine Speisekarte mit verschiedenen Optionen und ihren Eigenschaften. Aber eine wichtige Information fehlt noch: Wie viel Platz wird das Bild auf der Webseite überhaupt einnehmen? Ein Bild, das 1200 Pixel breit ist, mag für ein Vollbild-Banner passend sein, aber für ein kleines Vorschaubild in einer Seitenleiste wäre es viel zu groß.

Hier kommt das `sizes`-Attribut ins Spiel.

#### Das `sizes`-Attribut: Der unverzichtbare Partner von `srcset`

Wenn du den `w`-Deskriptor verwendest, ist das `sizes`-Attribut zwingend erforderlich. Es ist die Brücke zwischen deinen Bildoptionen (`srcset`) und deinem CSS-Layout. Mit `sizes` teilst du dem Browser mit, wie groß der Anzeigebereich für das Bild bei unterschiedlichen Viewport-Größen sein wird.

Die Syntax von `sizes` besteht aus einer Reihe von "Media Condition"-Wert-Paaren, gefolgt von einem Standardwert.

Schauen wir uns ein vollständiges, praxisnahes Beispiel an:

```html
<img src="foto-800.jpg"
     srcset="foto-400.jpg 400w,
             foto-800.jpg 800w,
             foto-1200.jpg 1200w,
             foto-1600.jpg 1600w"
     sizes="(max-width: 600px) 100vw, 50vw"
     alt="Ein schönes Landschaftsfoto bei Sonnenuntergang.">
```

Lass uns das `sizes`-Attribut auseinandernehmen:

*   `(max-width: 600px) 100vw`: Dieser Teil sagt: "Wenn die Breite des Viewports (des Browserfensters) maximal 600 Pixel beträgt, wird dieses Bild 100% der Viewport-Breite (`100vw`) einnehmen."
*   `50vw`: Das ist der Standardwert. Er gilt, wenn keine der vorherigen Bedingungen zutrifft. "In allen anderen Fällen (also bei Viewports über 600 Pixel Breite) wird das Bild 50% der Viewport-Breite einnehmen."

**Der Entscheidungsprozess des Browsers**

Jetzt hat der Browser alle Informationen, die er braucht, um eine intelligente Entscheidung zu treffen:

1.  **Layout-Größe bestimmen:** Der Browser prüft zuerst die aktuelle Viewport-Breite. Nehmen wir an, du bist auf einem Tablet mit einer Viewport-Breite von 900 Pixeln. Die erste Bedingung `(max-width: 600px)` trifft nicht zu. Also greift der Standardwert: Das Bild wird `50vw`, also 50% von 900 Pixeln = 450 Pixel breit sein.

2.  **Pixeldichte berücksichtigen:** Nun prüft der Browser die Pixeldichte des Geräts. Ein Standard-Display hat eine Dichte von `1x`. Ein "Retina"-Display hat typischerweise `2x` oder sogar `3x`. Nehmen wir an, dein Tablet hat ein 2x-Display. Um gestochen scharf auszusehen, benötigt das Bild, das im Layout 450 Pixel breit ist, eine Quelldatei mit mindestens `450 * 2 = 900` Pixeln.

3.  **Bestes Bild auswählen:** Mit diesem Wissen schaut sich der Browser die Liste in `srcset` an:
    *   `foto-400.jpg` (400w) - Zu klein.
    *   `foto-800.jpg` (800w) - Kommt nah ran, aber ist etwas kleiner als die benötigten 900 Pixel.
    *   `foto-1200.jpg` (1200w) - Perfekt! Es ist das kleinste Bild, das die benötigten 900 Pixel übersteigt. Der Browser wird dieses Bild herunterladen.
    *   `foto-1600.jpg` (1600w) - Wäre auch groß genug, aber unnötig groß und würde mehr Daten verbrauchen.

Der Browser wählt also immer das kleinste Bild, das die Anforderung erfüllt, um Daten zu sparen. Er kann sogar noch cleverer sein: Wenn er feststellt, dass die Netzwerkverbindung extrem langsam ist, kann er sich bewusst für eine kleinere Bildversion entscheiden, um die Ladezeit zu verkürzen, auch wenn das Bild dann nicht ganz so gestochen scharf ist. Du gibst die Kontrolle ab und vertraust darauf, dass der Browser die beste Entscheidung für den Nutzer trifft.

#### Der Pixel-Density-Deskriptor (`x`) – Der einfache Fall

Manchmal ist dein Layout nicht so flexibel. Stell dir ein Logo oder ein Icon vor, das immer eine feste Größe hat, zum Beispiel `100px` x `100px`, unabhängig von der Bildschirmgröße. Hier möchtest du nur eine Version für Standard-Displays und eine schärfere Version für hochauflösende Displays bereitstellen.

Für diesen Fall eignet sich der `x`-Deskriptor:

```html
<img src="logo-1x.png"
     srcset="logo-1x.png 1x,
             logo-2x.png 2x"
     width="100"
     height="100"
     alt="Firmenlogo">
```

Hier ist die Logik viel direkter:

*   `logo-1x.png 1x`: Diese Datei wird für Geräte mit einer Standard-Pixeldichte (1x) verwendet.
*   `logo-2x.png 2x`: Diese Datei wird für Geräte mit doppelter Pixeldichte (2x) verwendet.

Der Browser schaut sich nur die Pixeldichte des Geräts an und wählt die passende Datei. `logo-1x.png` könnte eine Größe von 100x100 Pixeln haben, während `logo-2x.png` für die doppelte Auflösung 200x200 Pixel groß sein sollte, um auf einem 2x-Display scharf auszusehen, wenn es mit `width="100"` angezeigt wird.

Der `x`-Deskriptor ist einfacher zu verstehen, aber weil er die Layout-Größe des Bildes komplett ignoriert, ist er für responsive, fließende Designs, bei denen Bilder ihre Größe ändern, ungeeignet. Nutze ihn also nur für Bilder mit fester Anzeigegröße.

#### Die Rolle des alten `src`-Attributs

Du hast vielleicht bemerkt, dass in allen Beispielen das `src`-Attribut immer noch vorhanden ist. Das ist absolut entscheidend! Das `src`-Attribut dient als Fallback (Rückfallebene) für sehr alte Browser, die `srcset` noch nicht verstehen. Diese Browser ignorieren `srcset` und `sizes` einfach und laden das Bild, das im `src`-Attribut angegeben ist.

Es ist eine gute Praxis, im `src`-Attribut eine sinnvolle Standardgröße anzugeben – oft ist das eine der kleineren oder mittleren Versionen. So stellst du sicher, dass alle Nutzer zumindest ein funktionierendes Bild sehen.

Durch den intelligenten Einsatz von `srcset` und `sizes` schlägst du mehrere Fliegen mit einer Klappe: Du verbesserst die Ladeleistung deiner Webseite drastisch, sparst Datenvolumen für deine Nutzer (insbesondere mobil) und sorgst gleichzeitig dafür, dass deine Bilder auf jedem Gerät, von der Smartwatch bis zum 8K-Monitor, gestochen scharf und in der optimalen Qualität angezeigt werden. Es ist ein fundamentaler Baustein für moderne, performante und nutzerfreundliche Webentwicklung.
