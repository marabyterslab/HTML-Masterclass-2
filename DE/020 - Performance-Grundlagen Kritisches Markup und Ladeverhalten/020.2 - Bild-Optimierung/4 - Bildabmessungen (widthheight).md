# Bildabmessungen (width/height)

### Die unterschätzte Macht der Attribute `width` und `height`

Auf den ersten Blick wirken die HTML-Attribute `width` und `height` für Bilder fast schon trivial. Du gibst die Breite und Höhe deines Bildes an, und der Browser zeigt es an. Einfach, oder? Doch hinter diesen beiden Attributen verbirgt sich einer der wichtigsten Hebel für die wahrgenommene Ladeleistung und die visuelle Stabilität deiner Webseite. Ihre korrekte Verwendung ist ein entscheidender Schritt, um eine professionelle und nutzerfreundliche Erfahrung zu schaffen.

#### Das Problem: Wenn das Layout tanzt

Stell dir vor, du liest einen interessanten Artikel auf einer Webseite. Du bist mitten in einem Satz, und plötzlich springt der Text, den du gerade liest, nach unten, weil über ihm ein großes Bild oder eine Werbeanzeige nachgeladen wurde. Du hast deine Leseposition verloren und bist frustriert. Vielleicht hast du sogar schon auf einen Link geklickt, der durch die Verschiebung unter deinem Mauszeiger weggesprungen ist, sodass du versehentlich auf etwas anderes klickst.

Dieses Phänomen nennt sich **Layout Shift** (Layout-Verschiebung). Wenn mehrere dieser Verschiebungen während des Ladevorgangs auftreten, summieren sie sich zu einem Wert, den Google als **Cumulative Layout Shift (CLS)** bezeichnet. CLS ist einer der drei Core Web Vitals, also eine der zentralen Metriken, mit denen Google die Nutzererfahrung einer Webseite bewertet. Ein hoher CLS-Wert führt nicht nur zu Frust bei deinen Besuchern, sondern kann sich auch negativ auf dein Suchmaschinenranking auswirken.

Woher kommt dieses Problem? Wenn der Browser das HTML deiner Seite analysiert, stößt er auf ein `<img>`-Tag. Er weiß, dass er ein Bild laden muss, kennt aber dessen Dimensionen noch nicht. Das Bild selbst muss erst vom Server heruntergeladen werden. In der Zwischenzeit fährt der Browser mit dem Rendern der restlichen Seite fort. Für das Bild reserviert er zunächst keinen Platz – oder nur eine winzige, standardmäßige Fläche. Erst wenn das Bild vollständig geladen ist, kennt der Browser seine wahren Abmessungen (z. B. 800 x 600 Pixel). In diesem Moment beansprucht das Bild schlagartig seinen Platz, und alle nachfolgenden Elemente werden nach unten oder zur Seite gedrückt. Das Layout "tanzt".

Hier ist ein Beispiel für ein `<img>`-Tag, das dieses Problem verursacht:

```html
<!-- Problematisch: Der Browser kennt die Bildgröße nicht im Voraus -->
<img src="bilder/landschaft.jpg" alt="Weite Berglandschaft bei Sonnenuntergang">
```

#### Die Lösung: Dem Browser einen Hinweis geben

Genau hier kommen die Attribute `width` und `height` ins Spiel. Wenn du sie im HTML-Code deines Bildes angibst, gibst du dem Browser die entscheidende Information, die er benötigt, um das Problem zu verhindern.

```html
<!-- Korrekt: Der Browser weiß, wie viel Platz er reservieren muss -->
<img src="bilder/landschaft.jpg" width="800" height="600" alt="Weite Berglandschaft bei Sonnenuntergang">
```

Was passiert nun im Hintergrund?

1.  Der Browser liest das `<img>`-Tag und sieht die Attribute `width="800"` und `height="600"`.
2.  Auch wenn das Bild selbst noch nicht geladen ist, kennt der Browser jetzt das **Seitenverhältnis** (Aspect Ratio) des Bildes. In diesem Fall ist es 800 / 600, was einem Verhältnis von 4:3 entspricht.
3.  Der Browser reserviert sofort einen leeren "Container" auf der Seite, der genau dieses Seitenverhältnis hat. Die restlichen Inhalte der Seite werden um diesen Platzhalter herum angeordnet.
4.  Wenn das Bild schließlich geladen wird, füllt es einfach den bereits reservierten Platz aus. Es kommt zu keinerlei Verschiebung des Layouts. Der CLS-Wert bleibt bei null.

Wichtig ist hierbei zu verstehen, dass die Werte für `width` und `height` in HTML als **einheitslose Zahlen** interpretiert werden. Sie entsprechen den tatsächlichen Pixel-Dimensionen (der intrinsischen Größe) deines Bildes. Gib hier immer die Originalgröße des Bildes an, das du lädst.

#### `width`/`height` und Responsive Design: Kein Widerspruch

Jetzt fragst du dich vielleicht: "Moment mal, wenn ich feste Pixelwerte wie `width="800"` angebe, zerstört das nicht mein responsives Design? Ich will doch nicht, dass mein Bild auf einem Smartphone 800 Pixel breit ist!"

Das ist ein exzellenter und wichtiger Gedanke. Früher war das tatsächlich ein Problem. Heute arbeiten die HTML-Attribute und modernes CSS jedoch perfekt zusammen. Die HTML-Attribute dienen primär dazu, dem Browser das **Seitenverhältnis** mitzuteilen, damit er den Platz reservieren kann. Die endgültige, visuelle Größe des Bildes wird weiterhin von CSS gesteuert.

In fast allen modernen Webseiten-Setups (z. B. durch CSS-Frameworks oder CSS-Resets) findet sich eine Regel wie diese:

```css
img {
  max-width: 100%;
  height: auto;
}
```

Schauen wir uns an, wie diese beiden Technologien harmonieren:

*   **`height: auto;`**: Diese CSS-Regel weist den Browser an, die Höhe des Bildes automatisch an die Breite anzupassen, um das ursprüngliche Seitenverhältnis beizubehalten.
*   **`max-width: 100%;`**: Diese Regel sorgt dafür, dass das Bild niemals breiter wird als sein Elternelement (z. B. eine Spalte oder der Hauptinhaltsbereich). Wenn das Elternelement schmaler als die im HTML angegebene Breite des Bildes (z. B. 800px) ist, skaliert das Bild proportional herunter.

Das Ergebnis ist das Beste aus beiden Welten:
1.  **HTML `width` und `height`** informieren den Browser über das Seitenverhältnis, um Layout-Verschiebungen (CLS) zu verhindern.
2.  **CSS `max-width` und `height: auto`** sorgen dafür, dass das Bild flexibel und responsiv bleibt und sich an die verfügbare Bildschirmgröße anpasst.

Die im HTML-Attribut angegebene `width` fungiert also als Obergrenze, die durch `max-width: 100%` in CSS bei Bedarf nach unten korrigiert wird.

#### Noch wichtiger bei Lazy Loading

Die Bedeutung von `width` und `height` wird noch größer, wenn du die moderne Technik des **Lazy Loading** (verzögertes Laden) einsetzt. Mit dem Attribut `loading="lazy"` weist du den Browser an, Bilder erst dann zu laden, wenn sie in den sichtbaren Bereich des Nutzers (den Viewport) scrollen.

```html
<!-- Best Practice: Platz reservieren UND verzögert laden -->
<img src="bilder/sonnenblume.jpg" 
     width="1200" 
     height="800" 
     alt="Nahaufnahme einer leuchtend gelben Sonnenblume"
     loading="lazy">
```

Das ist fantastisch für die initiale Ladezeit, da nicht sofort alle Bilder heruntergeladen werden müssen. Stell dir jedoch vor, du würdest hier `width` und `height` weglassen. Der Nutzer scrollt die Seite herunter, ein Bild kommt in den Viewport, der Ladevorgang startet, und *genau in diesem Moment*, während der Nutzer aktiv mit der Seite interagiert, springt das Layout. Das ist die schlechtestmögliche Nutzererfahrung.

Wenn du also `loading="lazy"` verwendest, ist die Angabe von `width` und `height` nicht nur eine Empfehlung, sondern praktisch eine Notwendigkeit, um die visuelle Stabilität deiner Seite zu gewährleisten.

Zusammenfassend lässt sich sagen, dass diese beiden einfachen HTML-Attribute eine enorme Auswirkung haben. Sie sind kein Relikt aus alten Zeiten, sondern ein fundamentales Werkzeug für moderne, performante und nutzerfreundliche Webseiten. Indem du dem Browser die Dimensionen deiner Bilder mitteilst, verhinderst du frustrierende Layout-Verschiebungen, verbesserst deine Core Web Vitals und schaffst eine ruhige, stabile und professionelle Umgebung für deine Besucher. Es ist einer dieser kleinen Handgriffe mit maximaler positiver Wirkung.
