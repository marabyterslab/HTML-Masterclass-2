# Das img-Element

### Das `<img>`-Element: Bilder in dein Webdokument einbetten

Ein Bild sagt mehr als tausend Worte – ein Klischee, das im Webdesign eine tiefe Wahrheit birgt. Bilder sind essenziell, um Emotionen zu wecken, Informationen zu vermitteln und Webseiten visuell ansprechend zu gestalten. Das zentrale HTML-Element, um diese visuellen Anker in deine Seite zu integrieren, ist das `<img>`-Element.

Anders als die meisten Elemente, die du bisher kennengelernt hast, ist `<img>` ein sogenanntes „leeres“ oder „void“ Element. Das bedeutet, es hat keinen schließenden Tag wie `</img ...>`. Stattdessen werden alle notwendigen Informationen über Attribute direkt im öffnenden Tag übergeben.

#### Die zwei unverzichtbaren Attribute: `src` und `alt`

Ein `<img>`-Element ist ohne zwei grundlegende Attribute praktisch nutzlos: `src` (Source) und `alt` (Alternativtext).

```html
<img src="pfad/zum/bild.jpg" alt="Beschreibung des Bildinhalts">
```

**Das `src`-Attribut**

Das `src`-Attribut ist das Herzstück des `<img>`-Tags. Es enthält den Pfad zur Bilddatei, die du anzeigen möchtest. Dieser Pfad kann auf zwei Arten angegeben werden:

1.  **Relativer Pfad:** Er bezieht sich auf den Speicherort deiner aktuellen HTML-Datei. Dies ist die gebräuchlichste Methode für Bilder, die Teil deines eigenen Webprojekts sind.
    *   `src="katzenfoto.png"`: Das Bild befindet sich im selben Ordner wie die HTML-Datei.
    *   `src="bilder/katzenfoto.png"`: Das Bild befindet sich in einem Unterordner namens „bilder“.
    *   `src="../bilder/katzenfoto.png"`: Das Bild befindet sich in einem Ordner „bilder“, der eine Ebene über der aktuellen HTML-Datei liegt.

2.  **Absoluter Pfad:** Er gibt die vollständige URL zu einer Bilddatei an, die irgendwo im Internet liegt.
    *   `src="https://cdn.pixabay.com/photo/2017/02/20/18/03/cat-2083492_1280.jpg"`: Das Bild wird von einem externen Server geladen.

**Das `alt`-Attribut**

Das `alt`-Attribut ist aus zwei Gründen absolut notwendig und sollte niemals fehlen. Es bietet einen alternativen Text für das Bild, der angezeigt wird, wenn das Bild aus irgendeinem Grund nicht geladen werden kann (z. B. falscher Pfad, Netzwerkfehler).

Noch wichtiger ist jedoch seine Rolle für die Barrierefreiheit (Accessibility). Screenreader, die von sehbehinderten Nutzern verwendet werden, lesen den Inhalt des `alt`-Attributs vor. Ohne diesen Text wäre der Inhalt des Bildes für diese Nutzergruppe nicht zugänglich.

Ein guter Alternativtext beschreibt präzise, was auf dem Bild zu sehen ist, ohne überflüssige Phrasen wie „Bild von ...“ zu verwenden.

*   **Schlecht:** `<img src="hund.jpg" alt="hund">`
*   **Gut:** `<img src="hund.jpg" alt="Ein Golden Retriever fängt einen roten Ball im Park.">`

Wenn ein Bild rein dekorativen Zwecken dient und keinen inhaltlichen Mehrwert bietet, solltest du das `alt`-Attribut leer lassen (`alt=""`). Dadurch signalisierst du Screenreadern, das Bild zu ignorieren und nicht zu beschreiben.

#### Dimensionen festlegen mit `width` und `height`

Du kannst die Abmessungen eines Bildes direkt im HTML mit den Attributen `width` und `height` festlegen. Die Werte werden in Pixeln angegeben, wobei die Einheit `px` weggelassen wird.

```html
<img src="logo.svg" alt="Firmenlogo" width="200" height="50">
```

Das Festlegen dieser Attribute hat einen entscheidenden Vorteil für die Ladeperformance deiner Seite. Wenn der Browser das HTML parst, weiß er durch diese Angaben genau, wie viel Platz er für das Bild reservieren muss. Er kann den Rest des Layouts bereits aufbauen, während das Bild noch im Hintergrund lädt. Ohne diese Angaben würde der Inhalt beim Laden des Bildes plötzlich verschoben werden, was zu einem unschönen „Springen“ der Seite führt (bekannt als Cumulative Layout Shift).

Obwohl diese Attribute nützlich sind, um den Platz zu reservieren, solltest du die tatsächliche visuelle Gestaltung und insbesondere das responsive Verhalten von Bildern über CSS steuern. Eine gängige Praxis ist es, in CSS die Breite auf 100 % des Elternelements und die Höhe auf `auto` zu setzen, damit das Seitenverhältnis erhalten bleibt und das Bild sich flexibel an verschiedene Bildschirmgrößen anpasst.

```css
img {
  max-width: 100%;
  height: auto;
}
```

#### Zusatzinformationen mit dem `title`-Attribut

Neben `alt` gibt es auch das `title`-Attribut. Es dient dazu, zusätzliche, nicht kritische Informationen bereitzustellen. In den meisten Browsern wird der Inhalt des `title`-Attributs als kleiner Tooltip angezeigt, wenn der Nutzer mit der Maus über das Bild fährt.

```html
<img src="mona-lisa.jpg" 
     alt="Porträt der Mona Lisa von Leonardo da Vinci." 
     title="Leonardo da Vinci, ca. 1503–1506">
```

Wichtig ist die Unterscheidung: `alt` beschreibt den Inhalt des Bildes für den Fall, dass es nicht sichtbar ist. `title` liefert ergänzende Informationen, wenn das Bild sichtbar ist. Verlasse dich aber niemals darauf, dass Nutzer diesen Tooltip sehen; wichtige Informationen gehören in den sichtbaren Text der Webseite.

#### Responsive Bilder für alle Geräte: `srcset` und `sizes`

In der heutigen Zeit, in der Webseiten auf Geräten vom kleinen Smartphone bis zum riesigen 4K-Monitor betrachtet werden, ist es ineffizient, allen Nutzern dasselbe, riesige Bild zu schicken. Ein Smartphone-Nutzer im mobilen Netz benötigt keine 4000 Pixel breite Bilddatei. Hier kommen die Attribute `srcset` und `sizes` ins Spiel, die dem Browser erlauben, die am besten geeignete Bildversion auszuwählen.

**`srcset` (Source Set)**

Mit `srcset` stellst du eine Liste verschiedener Bildversionen und deren tatsächliche Breite zur Verfügung.

```html
<img src="blume-800.jpg"
     srcset="blume-400.jpg 400w,
             blume-800.jpg 800w,
             blume-1200.jpg 1200w"
     alt="Eine rote Mohnblume auf einer grünen Wiese.">
```

Hier bietest du dem Browser drei Versionen des Bildes an: eine mit 400 Pixeln Breite (`400w`), eine mit 800 (`800w`) und eine mit 1200 (`1200w`). Der Browser kann nun anhand der Bildschirmauflösung (z.B. Retina-Displays) und der aktuellen Fenstergröße die passende Datei auswählen. Das `src`-Attribut dient hier als Fallback für ältere Browser, die `srcset` nicht verstehen.

**`sizes`**

Das `srcset`-Attribut allein reicht aber oft nicht aus. Der Browser weiß zwar, wie breit die Bilder sind, aber er weiß nicht, wie viel Platz das Bild im Layout der Webseite einnehmen wird. Wird das Bild über die volle Breite angezeigt oder nur in einer kleinen Spalte?

Hier hilft das `sizes`-Attribut. Es gibt dem Browser „Hinweise“ in Form von Media Queries.

```html
<img src="blume-800.jpg"
     srcset="blume-400.jpg 400w,
             blume-800.jpg 800w,
             blume-1200.jpg 1200w"
     sizes="(max-width: 600px) 100vw, 50vw"
     alt="Eine rote Mohnblume auf einer grünen Wiese.">
```

Lesen wir das `sizes`-Attribut von links nach rechts:
*   `(max-width: 600px) 100vw`: Wenn die Breite des Viewports (des Browserfensters) maximal 600 Pixel beträgt, wird das Bild 100 % der Viewport-Breite einnehmen (`100vw`).
*   `50vw`: In allen anderen Fällen (also bei Viewports breiter als 600 Pixel) wird das Bild 50 % der Viewport-Breite einnehmen.

Mit diesen Informationen kann der Browser eine intelligente Entscheidung treffen. Ist der Nutzer auf einem Smartphone mit 320 Pixeln Breite, weiß der Browser: „Das Bild wird 100 % der Breite einnehmen, also 320 Pixel. Das `400w`-Bild ist dafür am besten geeignet.“ Ist der Nutzer auf einem Desktop mit 1400 Pixeln Breite, rechnet der Browser: „Das Bild wird 50 % einnehmen, also 700 Pixel. Das `800w`-Bild passt hier gut.“

#### Semantischer Kontext: `<figure>` und `<figcaption>`

Manchmal ist ein Bild mehr als nur eine Illustration – es ist eine Abbildung, ein Diagramm oder ein Foto, das eine eigene Beschriftung benötigt. Um Bild und Beschriftung semantisch korrekt zu gruppieren, gibt es die Elemente `<figure>` und `<figcaption>`.

`<figure>` umschließt dabei das Bild (`<img>`) und seine optionale Bildunterschrift (`<figcaption>`).

```html
<figure>
  <img src="eiffelturm.jpg" 
       alt="Der Eiffelturm in Paris bei Nacht, hell erleuchtet.">
  <figcaption>Der Eiffelturm ist das Wahrzeichen von Paris und wurde 1889 fertiggestellt.</figcaption>
</figure>
```

Diese Struktur hilft nicht nur Screenreadern, die Beziehung zwischen Bild und Text zu verstehen, sondern gibt dir auch eine saubere Grundlage für das Styling von Bildern mit Bildunterschriften in CSS.

#### Moderne Lade-Strategien: Das `loading`-Attribut

Um die Ladezeit einer Webseite, die viele Bilder enthält, weiter zu optimieren, wurde das `loading`-Attribut eingeführt. Es steuert, wann der Browser ein Bild herunterladen soll.

```html
<img src="grosses-bild.jpg" alt="..." loading="lazy">
```

Es gibt zwei Hauptwerte:
*   `eager` (Standard): Das Bild wird sofort geladen, unabhängig davon, ob es im sichtbaren Bereich des Nutzers liegt oder nicht.
*   `lazy`: Das Bild wird erst dann geladen, wenn der Nutzer in seine Nähe scrollt. Dies wird als „Lazy Loading“ bezeichnet und ist extrem nützlich für Bilder, die sich weiter unten auf einer langen Seite befinden. Es spart Bandbreite und beschleunigt den initialen Seitenaufbau erheblich.

Das `<img>`-Element ist somit weit mehr als nur ein einfacher Platzhalter für eine Bilddatei. Mit seinen Attributen bietet es dir mächtige Werkzeuge, um Bilder performant, barrierefrei und responsiv in deine Webseiten zu integrieren.
