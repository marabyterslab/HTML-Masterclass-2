# Das cite-Element für Quellenangaben

### Das `cite`-Element für Quellenangaben

In der digitalen Welt, genau wie in der akademischen oder journalistischen, ist es von entscheidender Bedeutung, Quellen korrekt anzugeben. Wenn du Inhalte von anderen zitierst oder auf kreative Werke verweist, gibst du nicht nur die gebührende Anerkennung, sondern schaffst auch Transparenz und Vertrauen bei deinen Lesern. HTML bietet uns für genau diesen Zweck ein spezifisches, semantisches Element: das `<cite>`-Element.

Auf den ersten Blick mag es einfach erscheinen, doch seine korrekte Anwendung ist entscheidend für einen sauberen und bedeutungsvollen Code. Lass uns gemeinsam tief in die Welt der Zitate und Quellenangaben eintauchen.

#### Was genau ist das `<cite>`-Element?

Das `<cite>`-Element wird verwendet, um den Titel eines kreativen Werkes auszuzeichnen. Das ist der wichtigste Punkt, den du dir merken musst: Es kennzeichnet den **Titel des Werkes**, nicht den Autor, nicht das Zitat selbst und auch nicht eine URL.

Was zählt als "kreatives Werk"? Die Definition ist erfreulich breit und umfasst unter anderem:

*   **Bücher:** *Per Anhalter durch die Galaxis*
*   **Filme:** *The Matrix*
*   **Songs oder Musikalben:** *Bohemian Rhapsody*
*   **Theaterstücke:** *Faust*
*   **Gemälde oder Skulpturen:** *Die Mona Lisa*
*   **Fernsehsendungen:** *Breaking Bad*
*   **Artikel oder Blog-Posts:** *10 Tipps für besseres HTML*
*   **Gedichte:** *Der Erlkönig*
*   **Websites oder Computerspiele:** *Wikipedia*, *The Legend of Zelda*
*   **Gerichtsfälle oder wissenschaftliche Arbeiten**

Indem du diese Titel in `<cite>`-Tags einschließt, teilst du dem Browser und anderen Maschinen (wie Suchmaschinen oder Screenreadern) mit: "Dieser Text hier ist nicht nur irgendein Text, er ist der Titel eines Werkes."

Standardmäßig stellen die meisten Browser den Inhalt eines `<cite>`-Elements kursiv dar. Aber lass dich davon nicht täuschen! Es ist ein weit verbreiteter Fehler, `<cite>` zu verwenden, nur weil man kursiven Text möchte. HTML geht es um Bedeutung (Semantik), nicht um Aussehen (Präsentation). Wenn du Text aus stilistischen Gründen kursiv setzen möchtest, ohne ihm eine spezifische Bedeutung zu geben, solltest du das `<i>`-Element oder besser noch CSS (`font-style: italic;`) verwenden. Das `<cite>`-Element ist ausschließlich für die semantische Auszeichnung von Werktiteln reserviert.

Hier ist ein einfaches Beispiel für die Verwendung im Fließtext:

```html
<p>Mein Lieblingsbuch von Douglas Adams ist <cite>Per Anhalter durch die Galaxis</cite>. Es hat meine Sicht auf das Universum und Handtücher für immer verändert.</p>
```

In diesem Satz ist klar ersichtlich, dass "Per Anhalter durch die Galaxis" der Titel eines Buches ist. Das ist die Kernfunktion von `<cite>`.

#### Die Kombination mit `<blockquote>` und `<q>`

Die wahre Stärke des `<cite>`-Elements zeigt sich, wenn du es zusammen mit den Elementen für Zitate verwendest: `<blockquote>` für längere, blockförmige Zitate und `<q>` für kurze, inline Zitate.

Stell dir vor, du möchtest ein berühmtes Zitat aus einem Film auf deiner Webseite einbinden. Die korrekte Struktur dafür wäre, das Zitat selbst in ein `<blockquote>`-Element zu setzen und die Quelle danach anzugeben.

```html
<blockquote>
  <p>Du nimmst die blaue Pille — die Geschichte endet, du wachst in deinem Bett auf und glaubst, was du auch immer glauben willst. Du nimmst die rote Pille — du bleibst im Wunderland und ich zeige dir, wie tief der Kaninchenbau reicht.</p>
</blockquote>
<p>— Morpheus in <cite>The Matrix</cite></p>
```

Diese Struktur ist sauber und semantisch einwandfrei. Der `<blockquote>` enthält das Zitat. Ein separater Absatz (`<p>`) oder ein `<footer>`-Element innerhalb einer `<figure>` (eine noch fortschrittlichere Methode) enthält die Quellenangabe. Und innerhalb dieser Quellenangabe wird der Filmtitel `<cite>The Matrix</cite>` korrekt als Werk ausgezeichnet.

Das Gleiche gilt für kurze Zitate mit dem `<q>`-Element:

```html
<p>Goethes berühmte Worte <q>Edel sei der Mensch, hilfreich und gut!</q> stammen aus seinem Gedicht <cite>Das Göttliche</cite>.</p>
```

Auch hier wird das Zitat mit `<q>` und der Titel des Werkes, aus dem es stammt, mit `<cite>` ausgezeichnet.

#### Der Unterschied zwischen dem `cite`-Element und dem `cite`-Attribut

Jetzt wird es ein wenig knifflig, aber es ist ein entscheidender Punkt für das vollständige Verständnis. Es gibt nicht nur das `<cite>`-**Element**, sondern auch ein `cite`-**Attribut**. Dieses Attribut kann auf `<blockquote>`- und `<q>`-Elementen verwendet werden.

Der Zweck des `cite`-Attributs ist es, eine URL anzugeben, die zur Online-Quelle des Zitats führt. Dieser Link wird für den Benutzer nicht sichtbar angezeigt. Er dient als maschinenlesbare Metainformation für Browser, Suchmaschinen oder andere Tools, die den Ursprung des Zitats programmatisch nachvollziehen wollen.

Schauen wir uns unser `<blockquote>`-Beispiel von vorhin an und erweitern es um das `cite`-Attribut:

```html
<blockquote cite="https://www.imdb.com/title/tt0133093/quotes/qt0322533">
  <p>Du nimmst die blaue Pille — die Geschichte endet, du wachst in deinem Bett auf und glaubst, was du auch immer glauben willst. Du nimmst die rote Pille — du bleibst im Wunderland und ich zeige dir, wie tief der Kaninchenbau reicht.</p>
</blockquote>
<p>— Morpheus in <cite>The Matrix</cite></p>
```

Hier haben wir das Beste aus beiden Welten:

1.  **Das `cite`-Attribut** im `<blockquote>`-Tag enthält einen direkten Link zur Quelle des Zitats. Diese Information ist für Maschinen bestimmt.
2.  **Das `<cite>`-Element** im nachfolgenden Absatz zeichnet den Titel des Werkes (*The Matrix*) für menschliche Leser sichtbar aus.

Denk an diese Eselsbrücke:
*   Das **Attribut** `cite="..."` ist eine unsichtbare URL für die Maschine.
*   Das **Element** `<cite>...</cite>` ist der sichtbare Titel für den Menschen.

Beide zusammen zu verwenden ist die goldene Regel für perfekte, semantische Zitate.

#### Häufige Fehler, die du vermeiden solltest

Die korrekte Anwendung von `<cite>` ist ein Zeichen von professionellem HTML. Achte darauf, die folgenden typischen Fehler zu vermeiden.

**Fehler 1: Personen im `<cite>`-Element**

Der häufigste Fehler ist, den Namen einer Person in `<cite>`-Tags zu setzen. Eine Person ist kein kreatives Werk.

```html
<!-- FALSCH -->
<p><cite>Albert Einstein</cite> sagte einst: "Phantasie ist wichtiger als Wissen."</p>

<!-- RICHTIG -->
<p>Albert Einstein sagte einst: "Phantasie ist wichtiger als Wissen."</p>
```

Der Name des Autors oder Sprechers gehört nicht in ein `<cite>`-Element. Er ist einfach nur Text. Wenn du den Namen hervorheben möchtest, könntest du ihn mit `<strong>` betonen, aber semantisch ist er einfach der Name einer Person.

**Fehler 2: Das Zitat selbst im `<cite>`-Element**

Das `<cite>`-Element ist für den Titel der Quelle, nicht für den zitierten Text.

```html
<!-- FALSCH -->
<p>Mein Motto ist: <cite>Carpe Diem</cite>.</p>

<!-- RICHTIG (wenn es als allgemeiner Ausspruch gemeint ist) -->
<p>Mein Motto ist: <q>Carpe Diem</q>.</p>

<!-- RICHTIG (wenn es als Zitat aus einem bestimmten Werk gemeint ist) -->
<p>In seinem Werk <cite>Oden</cite> schrieb Horaz die berühmten Worte <q>Carpe Diem</q>.</p>
```

Für den zitierten Text sind `<blockquote>` und `<q>` die richtigen Werkzeuge.

**Fehler 3: Missbrauch für stilistische Zwecke**

Wie bereits erwähnt, nutze `<cite>` niemals nur, weil du kursiven Text benötigst. Das untergräbt die gesamte Idee von semantischem HTML. Dein Code verliert an Bedeutung, wird für assistierende Technologien wie Screenreader schwerer verständlich und ist schlechter wartbar. Wenn du das Aussehen von Text steuern möchtest, ist CSS dein Freund.

#### Das Aussehen von `<cite>` mit CSS anpassen

Da wir nun wissen, dass `<cite>` eine semantische Bedeutung hat, können wir diese nutzen, um alle Werktitel auf unserer Website einheitlich zu gestalten. Vielleicht gefällt dir die standardmäßige kursive Darstellung nicht, oder du möchtest Zitate deutlicher hervorheben.

Mit einer einfachen CSS-Regel kannst du das Aussehen aller `<cite>`-Elemente gezielt verändern.

```css
cite {
  font-style: normal; /* Hebt die kursive Schrift auf */
  color: #005a9c;     /* Gibt dem Titel eine spezifische Farbe */
  font-weight: bold;   /* Macht den Titel fett */
}
```

Wenn du diesen CSS-Code in dein Stylesheet einfügst, werden alle mit `<cite>` ausgezeichneten Werktitel nicht mehr kursiv, sondern fett und in einem Blauton dargestellt. Dies zeigt die wahre Kraft von semantischem HTML: Du trennst Struktur und Bedeutung (HTML) von der Präsentation (CSS). Dadurch kannst du das Design deiner gesamten Website ändern, indem du nur eine einzige Zeile CSS anpasst, ohne jemals deinen HTML-Code anfassen zu müssen.

Die korrekte Verwendung des `<cite>`-Elements ist ein kleiner, aber feiner Baustein auf dem Weg zu einer qualitativ hochwertigen, zugänglichen und zukunftssicheren Webseite. Es zeigt, dass du nicht nur darüber nachdenkst, wie etwas aussieht, sondern auch, was es bedeutet.
