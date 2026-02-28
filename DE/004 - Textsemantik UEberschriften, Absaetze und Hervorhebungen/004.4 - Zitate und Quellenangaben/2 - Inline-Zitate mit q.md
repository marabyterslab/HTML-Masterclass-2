# Inline-Zitate mit q

### Inline-Zitate mit `<q>`: Kurze Anführungen im Fließtext

Nicht jedes Zitat ist ein langer, wuchtiger Textblock, der einen eigenen Absatz verdient. Oft möchten wir nur einen kurzen Satz, einen Halbsatz oder sogar ein einzelnes Wort aus einer fremden Quelle direkt in unseren eigenen Text einweben. Stell dir einen Satz vor wie: „Der Autor betonte, es sei ‚eine Frage der Perspektive‘, und fuhr dann fort.“ Genau für solche Fälle wurde in HTML das `<q>`-Element geschaffen.

Das `<q>`-Tag (von englisch *quote*, also Zitat) ist das semantische Gegenstück zum `<blockquote>`-Element, das du bereits für längere, absatzbildende Zitate kennengelernt hast. Während `<blockquote>` einen ganzen Block für sich beansprucht, fügt sich `<q>` nahtlos in den Textfluss ein – es ist ein sogenanntes **Inline-Element**.

#### Die Magie der automatischen Anführungszeichen

Auf den ersten Blick könnte man denken: Warum der Aufwand? Ich kann doch einfach normale Anführungszeichen auf meiner Tastatur tippen. Hier kommt die semantische Kraft von HTML ins Spiel. Wenn du ein Zitat mit `<q>` umschließt, tust du mehr, als nur Zeichen zu setzen. Du gibst dem Browser und anderen Systemen (wie Suchmaschinen oder Screenreadern) eine explizite Information: „Dieser Textabschnitt ist ein direktes Zitat.“

Der größte praktische Vorteil dieses Vorgehens ist, dass der Browser automatisch die korrekten Anführungszeichen setzt. Du schreibst im Code nur den reinen Text innerhalb des Tags.

```html
<p>In seinem berühmten Vortrag sagte er: <q>Semantik ist der Schlüssel zu einem zugänglichen und nachhaltigen Web</q>.</p>
```

Im Browser wird dies in der Regel wie folgt dargestellt, abhängig von der Spracheinstellung des Dokuments:

> In seinem berühmten Vortrag sagte er: „Semantik ist der Schlüssel zu einem zugänglichen und nachhaltigen Web“.

Du musst dir also keine Gedanken darüber machen, ob du in deiner Sprache einfache (`'`) oder doppelte (`"`), typografisch korrekte („ “) oder französische Anführungszeichen (« ») verwenden musst. Der Browser kümmert sich darum, basierend auf der im `<html>`-Tag deklarierten Sprache (z. B. `<html lang="de">`). Dies macht deinen Code sauberer und deine Inhalte international anpassungsfähiger.

Solltest du aus gestalterischen Gründen dennoch die Art der Anführungszeichen beeinflussen wollen, kannst du dies mit CSS tun. Die Eigenschaft `quotes` erlaubt es dir, die öffnenden und schließenden Zeichen für Zitate zu definieren.

```css
/* Ändert die Standard-Anführungszeichen in Guillemets (französische Anführungszeichen) */
q {
  quotes: "«" "»";
}

/* Für verschachtelte Zitate können weitere Paare hinzugefügt werden */
q {
  quotes: "«" "»" "‹" "›";
}
```

Die erste Zeile im CSS-Beispiel würde dazu führen, dass dein Zitat so aussieht:

> In seinem berühmten Vortrag sagte er: «Semantik ist der Schlüssel zu einem zugänglichen und nachhaltigen Web».

Ohne semantisches Markup mit `<q>` wäre eine solche automatische und zentrale Steuerung der Zitatdarstellung nicht möglich.

#### Quellenangabe mit dem `cite`-Attribut

Genau wie sein großer Bruder `<blockquote>` unterstützt auch das `<q>`-Element das `cite`-Attribut. Dieses Attribut ist dazu da, eine URL zur Quelle des Zitats anzugeben. Diese Information ist für den Betrachter der Webseite standardmäßig nicht sichtbar, aber sie ist von unschätzbarem Wert für Maschinen.

Suchmaschinen können diese Verknüpfung nutzen, um die Herkunft deiner Informationen zu validieren und den Kontext besser zu verstehen. Browser-Plugins oder assistive Technologien könnten dem Nutzer die Möglichkeit bieten, direkt zur Quelle zu springen.

Ein Beispiel mit Quellenangabe sieht so aus:

```html
<p>
  Wie Tim Berners-Lee einmal anmerkte: 
  <q cite="https://www.w3.org/People/Berners-Lee/FAQ.html#Spelling">
    The power of the Web is in its universality.
  </q> 
  Dieser Grundsatz ist heute relevanter denn je.
</p>
```

Hier wird klar kommuniziert, woher das Zitat stammt. Es ist eine saubere und maschinenlesbare Form der Quellenangabe, die direkt mit dem Zitat verknüpft ist.

#### Abgrenzung: Wann `<q>` und wann nicht?

Die Entscheidung, ob du das `<q>`-Element, `<blockquote>` oder einfach nur Anführungszeichen verwenden solltest, hängt von der Semantik ab. Hier sind klare Richtlinien für dich:

1.  **`<q>` vs. `<blockquote>`**: Die Regel ist einfach. Ist das Zitat kurz und Teil eines Satzes oder Absatzes? Dann verwende `<q>`. Nimmt das Zitat einen oder mehrere eigene Absätze ein und steht für sich allein? Dann ist `<blockquote>` die richtige Wahl. `<q>` ist inline, `<blockquote>` ist block-level.

2.  **`<q>` vs. normale Anführungszeichen (`"..."`)**: Verwende `<q>`, wann immer du ein **echtes, wörtliches Zitat** aus einer anderen Quelle wiedergibst. Wenn du jedoch Anführungszeichen verwendest, um ein Wort ironisch hervorzuheben (sogenannte „Scare Quotes“), einen Begriff zu definieren oder einen Dialog in einer fiktiven Geschichte zu schreiben, sind einfache typografische Anführungszeichen oft ausreichend. Der entscheidende Faktor ist: Zitierst du jemanden oder etwas? Wenn ja, ist `<q>` semantisch korrekt.

    *   **Korrekt (Zitat):** Er nannte es <q>einen Quantensprung in der Technologie</q>.
    *   **Auch korrekt (kein Zitat, sondern Hervorhebung):** Das war sein sogenanntes „Meisterwerk“.

3.  **`<q>` vs. `<em>` oder `<i>`**: Verwechsle Zitate nicht mit Betonung oder reiner Kursivschrift. `<em>` (Emphasis) wird verwendet, um einem Wort eine besondere Betonung zu verleihen, die den Sinn des Satzes verändert. `<i>` (Idiomatic Text) wird für Fachbegriffe, fremdsprachige Wörter oder Gedanken verwendet. Keines dieser Elemente ist für die Auszeichnung von Zitaten gedacht. Die Verwendung des falschen Tags schwächt die semantische Struktur deines Dokuments und kann zu Problemen bei der Barrierefreiheit und der maschinellen Verarbeitung führen.

#### Barrierefreiheit und Styling

Für Nutzer von Screenreadern ist das `<q>`-Tag ein wertvoller Hinweis. Eine gute Vorlesesoftware kann ihre Stimme oder Betonung anpassen, um den Beginn und das Ende eines Zitats zu signalisieren. Dies schafft eine klarere und verständlichere Hörerfahrung als ein einfacher Text, bei dem die Anführungszeichen nur vorgelesen werden.

Auch gestalterisch bietet dir das `<q>`-Element durch seine Existenz als eigenständiges HTML-Element viele Möglichkeiten. Du kannst Zitate nicht nur durch die Anführungszeichen, sondern auch visuell hervorheben, zum Beispiel durch eine leicht andere Schriftfarbe, einen dezenten Hintergrund oder Kursivschrift.

```css
q {
  color: #555;
  font-style: italic;
}

/* Man kann sogar die Anführungszeichen selbst stylen! */
q::before {
  content: open-quote;
  color: #999;
  font-weight: bold;
}

q::after {
  content: close-quote;
  color: #999;
  font-weight: bold;
}
```

Mit diesen CSS-Regeln würdest du nicht nur den zitierten Text kursiv und in einem dunklen Grau darstellen, sondern auch die automatisch generierten Anführungszeichen fett und in einem helleren Grau färben. Das `<q>`-Tag gibt dir also eine semantische Grundlage, auf der du aufbauen kannst – sowohl für die Maschine als auch für das menschliche Auge. Es ist ein kleines, aber mächtiges Werkzeug für die präzise Auszeichnung von Textinhalten.
