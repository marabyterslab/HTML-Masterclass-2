# Kursiv vs. betont (i vs. em)

### Kursiv oder betont? Der feine Unterschied zwischen `<i>` und `<em>`

Auf den ersten Blick scheinen die HTML-Tags `<i>` und `<em>` Zwillinge zu sein. Wenn du sie in einer einfachen HTML-Datei verwendest und im Browser anschaust, ist das Ergebnis in der Standardeinstellung identisch: Der umschlossene Text wird kursiv dargestellt. Das führt viele Anfänger zu der Annahme, dass es egal ist, welchen der beiden Tags sie verwenden. Doch dieser Schein trügt gewaltig. Hinter diesen beiden Tags verbirgt sich eine der fundamentalsten Lektionen in modernem HTML: der Unterschied zwischen Präsentation und Semantik.

Lass uns diese beiden Elemente entwirren und verstehen, warum die Wahl zwischen ihnen eine bewusste und wichtige Entscheidung ist.

#### Semantik ist König: Was dein Code *bedeutet*

Bevor wir tief in die Details von `<i>` und `<em>` eintauchen, müssen wir über das Herzstück von modernem HTML sprechen: die Semantik. Semantischer Code ist Code, der nicht nur beschreibt, wie etwas aussehen soll, sondern was etwas *ist* oder welche *Bedeutung* es hat.

Stell dir vor, du schreibst ein Dokument. Du hast Überschriften, Absätze, Zitate und Listen. In HTML verwendest du dafür Tags wie `<h1>`, `<p>`, `<blockquote>` und `<ul>`. Du sagst dem Browser damit nicht: „Mach diesen Text groß und fett.“ Du sagst ihm: „Das ist die wichtigste Überschrift auf dieser Seite.“ Der Browser entscheidet dann standardmäßig, sie groß und fett darzustellen, aber die ursprüngliche Information war die *Bedeutung* (eine Überschrift erster Ordnung), nicht der Stil.

Genau dieses Prinzip gilt auch für die Textauszeichnung im Fließtext.

#### `<em>`: Die Betonung liegt auf der Betonung

Das `<em>`-Element ist der Inbegriff semantischer Auszeichnung. Das „em“ steht für „emphasis“, also „Betonung“. Wenn du ein Wort oder eine Phrase in `<em>`-Tags einschließt, teilst du dem Browser und anderen Systemen (wie Suchmaschinen oder Screenreadern) mit, dass dieser Teil des Textes eine besondere Betonung erhalten soll.

Denk darüber nach, wie du sprichst. Manchmal veränderst du deine Stimmlage, um einem Wort mehr Gewicht zu verleihen und so die Bedeutung des gesamten Satzes zu verändern.

Schauen wir uns diesen Satz an:
`Ich habe das nicht gesagt.`

Dieser Satz ist neutral. Nun setzen wir `<em>` ein und beobachten, wie sich die implizite Bedeutung verschiebt:

```html
<p><em>Ich</em> habe das nicht gesagt.</p>
```
**Bedeutung:** Jemand anderes hat es gesagt, aber nicht ich.

```html
<p>Ich habe das <em>nicht</em> gesagt.</p>
```
**Bedeutung:** Ich bestreite die Aussage vehement.

```html
<p>Ich habe das nicht <em>gesagt</em>.</p>
```
**Bedeutung:** Ich habe es vielleicht gedacht, geschrieben oder angedeutet, aber nicht laut ausgesprochen.

In jedem dieser Fälle ändert die Betonung die Kernaussage des Satzes. Das `<em>`-Element ist genau dafür gemacht, diese Art von sprachlicher Betonung im Code abzubilden.

Der wichtigste Aspekt dabei ist die Zugänglichkeit (Accessibility). Ein Screenreader, der blinden oder sehbehinderten Nutzern den Inhalt einer Webseite vorliest, wird den Text innerhalb eines `<em>`-Tags mit einer veränderten, betonten Intonation wiedergeben. Er wird also genau die Betonung vermitteln, die du als Autor beabsichtigt hast. Würdest du stattdessen ein rein stilistisches Element verwenden, ginge diese wichtige Information für diese Nutzergruppe verloren.

#### `<i>`: Die neue Rolle eines alten Bekannten

Das `<i>`-Element hat eine bewegte Geschichte. Sein Name kommt von „italic“, also „kursiv“. In den frühen Tagen des Web war seine Aufgabe rein präsentationsbezogen: Mach diesen Text kursiv. Das war’s. In der modernen, semantischen Welt von HTML5 wäre ein solch reines Styling-Element eigentlich überflüssig – dafür haben wir schließlich CSS.

Warum gibt es den `<i>`-Tag also noch? Weil seine Bedeutung neu definiert wurde. Er wurde quasi recycelt und hat eine neue semantische Aufgabe bekommen.

Der `<i>`-Tag wird heute für Text verwendet, der sich aus einem bestimmten Grund vom normalen Fließtext abhebt, aber keine besondere Betonung oder Wichtigkeit trägt. Die offizielle Spezifikation beschreibt es als „text in an alternate voice or mood“, also Text in einer alternativen Stimme oder Stimmung.

Das klingt zunächst etwas vage, aber es gibt ganz klare Anwendungsfälle dafür:

*   **Fachbegriffe oder technische Termini:** Wenn du einen Begriff einführst, der eine spezielle Definition hat.
    ```html
    <p>In der Webentwicklung ist das <em>Document Object Model</em>, kurz <i>DOM</i>, eine Programmierschnittstelle.</p>
    ```
    Hier wird „DOM“ nicht betont, sondern als Fachterminus gekennzeichnet.

*   **Fremdsprachige Wörter oder Phrasen:** Ein Wort aus einer anderen Sprache, das im Text verwendet wird.
    ```html
    <p>Sein Lebensmotto war <i>carpe diem</i>.</p>
    ```
    „Carpe diem“ wird nicht stärker betont als der Rest des Satzes, es ist einfach nur eine lateinische Phrase.

*   **Namen von Schiffen oder Fahrzeugen:**
    ```html
    <p>Die <i>Titanic</i> sank auf ihrer Jungfernfahrt.</p>
    ```

*   **Gedanken einer Figur:** Oft werden innere Monologe kursiv gesetzt.
    ```html
    <p>Er blickte aus dem Fenster und dachte, <i>was für ein seltsamer Tag</i>.</p>
    ```

In all diesen Beispielen ändert das kursiv gesetzte Wort nicht die Betonung des Satzes. Wenn du den Satz laut vorlesen würdest, würdest du deine Stimme bei „DOM“, „carpe diem“ oder „Titanic“ wahrscheinlich nicht anheben. Du würdest sie einfach als Teil des Satzes lesen. Der Text hebt sich lediglich in seiner *Art* vom Rest ab. Ein Screenreader wird hier standardmäßig keine andere Stimmlage verwenden.

#### Die Trennung von Inhalt und Darstellung: CSS kommt ins Spiel

Die größte Verwirrung entsteht, weil Browser sowohl `<em>` als auch `<i>` standardmäßig kursiv darstellen. Aber das ist nur eine Konvention, eine Voreinstellung im Browser-Stylesheet. Die wahre Kraft der semantischen Trennung zeigt sich, wenn du CSS (Cascading Style Sheets) verwendest.

Du hast die volle Kontrolle darüber, wie diese Elemente aussehen. Ihre HTML-Bedeutung bleibt davon unberührt.

Stell dir vor, du möchtest auf deiner Webseite jede Betonung (`<em>`) nicht nur kursiv, sondern auch rot und fett hervorheben, um sie noch deutlicher zu machen. Mit CSS ist das ein Kinderspiel:

```css
em {
  font-style: italic; /* bleibt kursiv */
  font-weight: bold; /* wird zusätzlich fett */
  color: #c0392b;     /* wird rot */
}
```

Gleichzeitig könntest du entscheiden, dass Fachbegriffe (`<i>`), um sie klarer als solche zu kennzeichnen, vielleicht eine leicht andere Hintergrundfarbe und gar nicht kursiv sein sollen:

```css
i {
  font-style: normal; /* nicht mehr kursiv */
  background-color: #f2f2f2;
  padding: 2px 4px;
  border-radius: 3px;
  font-family: monospace;
}
```

Mit diesem CSS würde dein vorheriges Beispiel so aussehen:

`<p>In der Webentwicklung ist das <em>Document Object Model</em>, kurz <i>DOM</i>, eine Programmierschnittstelle.</p>`

Der Text „Document Object Model“ wäre nun fett, kursiv und rot, während „DOM“ normal geschrieben, aber mit einem grauen Hintergrund unterlegt wäre. Du hast das Aussehen komplett verändert, aber die semantische Bedeutung im HTML-Code ist exakt dieselbe geblieben. Ein System, das nur den HTML-Code liest, weiß immer noch: Das eine ist eine Betonung, das andere ein Fachterminus.

#### Eine einfache Faustregel: Der „Sprechtest“

Wenn du dir unsicher bist, welchen Tag du verwenden sollst, mach den „Sprechtest“:

1.  **Lies den Satz laut vor.**
2.  **Veränderst du instinktiv deine Stimme, um das Wort oder die Phrase hervorzuheben und die Bedeutung zu beeinflussen?**

*   **Ja?** -> Dann ist `<em>` die richtige Wahl. Du willst eine echte Betonung.
*   **Nein?** -> Dann frage dich, ob der Text in eine der `<i>`-Kategorien fällt (Fachbegriff, fremdes Wort, Gedanke etc.). Wenn ja, ist `<i>` perfekt.

**Und was ist, wenn es in keine dieser Kategorien passt?**
Was, wenn du Text einfach nur aus rein dekorativen, visuellen Gründen kursiv darstellen möchtest, ohne jegliche semantische Bedeutung? In diesem Fall solltest du weder `<em>` noch `<i>` verwenden. Die korrekte Vorgehensweise ist, ein neutrales `<span>`-Element zu nutzen und ihm eine CSS-Klasse zu geben.

HTML:
```html
<p>Dieser Text ist <span class="visually-italic">nur aus ästhetischen Gründen</span> kursiv.</p>
```

CSS:
```css
.visually-italic {
  font-style: italic;
}
```
Damit trennst du die Präsentation (das Aussehen) sauber von der Struktur (der Bedeutung). Dein HTML-Code bleibt semantisch rein und überlässt das Styling vollständig dem CSS – genau so, wie es im modernen Webdesign sein sollte.

#### Parallele zu `<b>` und `<strong>`

Dieser fundamentale Unterschied zwischen Semantik und Präsentation ist kein Einzelfall. Eine exakte Parallele findest du bei den Tags `<b>` und `<strong>`. Früher stand `<b>` einfach für „bold“ (fett). Heute hat es, ähnlich wie `<i>`, eine neue semantische Bedeutung: „Bring Attention To“ – Text, auf den die Aufmerksamkeit gelenkt werden soll, ohne dass er wichtiger ist (z.B. Produktnamen in einer Rezension). `<strong>` hingegen bedeutet, dass der Inhalt eine starke Wichtigkeit („strong importance“) hat. Auch hier rendern Browser beide standardmäßig fett, aber ihre Bedeutung ist grundverschieden. Das Prinzip bleibt dasselbe: Wähle den Tag, der die *Bedeutung* deines Inhalts am besten beschreibt, nicht sein Aussehen.
