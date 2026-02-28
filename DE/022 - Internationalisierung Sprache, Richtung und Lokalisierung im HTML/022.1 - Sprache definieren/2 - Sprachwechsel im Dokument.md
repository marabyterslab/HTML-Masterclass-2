# Sprachwechsel im Dokument

### Sprachwechsel innerhalb eines Dokuments

In der Regel legst du die Hauptsprache deines HTML-Dokuments einmal zentral im `<html>`-Tag fest, zum Beispiel mit `<html lang="de">`. Damit gibst du den grundlegenden Kontext für Browser, Suchmaschinen und assistierende Technologien vor. Die Realität im Web ist jedoch oft mehrsprachig. Texte enthalten Zitate in ihrer Originalsprache, englische Fachbegriffe haben sich im deutschen Sprachgebrauch etabliert oder du möchtest den Titel eines ausländischen Films oder Buches korrekt auszeichnen.

Genau für diese Fälle bietet HTML eine einfache, aber wirkungsvolle Lösung: das `lang`-Attribut kann nicht nur auf dem `<html>`-Element, sondern auf jedem beliebigen HTML-Element verwendet werden. Indem du die Sprache für einen bestimmten Teil deines Inhalts explizit kennzeichnest, schaffst du einen enormen Mehrwert in den Bereichen Barrierefreiheit, Suchmaschinenoptimierung und sogar bei der Darstellung.

#### Warum ein Sprachwechsel wichtig ist

Bevor wir uns die technische Umsetzung ansehen, lass uns kurz innehalten und verstehen, warum diese kleine Auszeichnung so einen großen Unterschied macht.

1.  **Barrierefreiheit (Accessibility):** Für Menschen, die auf Screenreader angewiesen sind, ist die korrekte Sprachauszeichnung essenziell. Ein Screenreader nutzt die im `lang`-Attribut definierte Sprache, um die passende Sprachausgabe mit der richtigen Aussprache und Betonung zu wählen. Ein deutscher Satz, der plötzlich einen englischen Einschub enthält, würde von einer rein deutschen Sprachausgabe oft unverständlich oder komisch ausgesprochen werden. Markierst du den englischen Teil mit `lang="en"`, wechselt der Screenreader für diesen Abschnitt nahtlos zur englischen Sprachausgabe und liest ihn korrekt vor. Das Leseerlebnis wird dadurch flüssig und verständlich.

2.  **Suchmaschinenoptimierung (SEO):** Suchmaschinen wie Google analysieren den Inhalt deiner Seite sehr genau. Wenn du fremdsprachige Inhalte korrekt auszeichnest, hilfst du der Suchmaschine, den Kontext und die Bedeutung deines Textes besser zu verstehen. Sie kann erkennen, dass es sich nicht um einen Tippfehler oder unverständlichen Kauderwelsch handelt, sondern um ein bewusst platziertes Zitat oder einen Fachbegriff. Dies kann die Qualität der Indexierung verbessern.

3.  **Browser-Funktionen:** Moderne Browser bieten eine Vielzahl von Hilfsfunktionen. Dazu gehören automatische Übersetzungsvorschläge, Rechtschreibprüfungen in Formularfeldern und die Silbentrennung. Wenn du die Sprache eines Textabschnitts korrekt definierst, können diese Werkzeuge präziser arbeiten. Der Browser wird nicht versuchen, eine deutsche Rechtschreibprüfung auf einen englischen Satz anzuwenden, und die Silbentrennung richtet sich nach den Regeln der jeweiligen Sprache.

4.  **Styling mit CSS:** Du kannst unterschiedliche Sprachen auch visuell anders darstellen. Vielleicht möchtest du Zitate in einer anderen Schriftart anzeigen oder japanischen Text, der eine spezielle Schriftart für eine gute Lesbarkeit benötigt, gezielt formatieren. Mit der CSS-Pseudoklasse `:lang()` ist das problemlos möglich.

#### Die praktische Anwendung des `lang`-Attributs

Die Anwendung ist denkbar einfach. Du nimmst das Element, das den fremdsprachigen Inhalt umschließt, und fügst das `lang`-Attribut mit dem passenden Sprachcode hinzu. Meistens ist ein semantisch neutrales `<span>`-Element eine gute Wahl, wenn es kein anderes passendes Element gibt.

Stell dir vor, du schreibst einen Blogartikel auf Deutsch und möchtest einen englischen Satz einfügen.

**Ohne Sprachauszeichnung:**

```html
<p>Die Entwicklerin sagte auf der Konferenz: This is a game changer.</p>
```

Ein Screenreader würde versuchen, „This is a game changer“ mit deutscher Phonetik auszusprechen, was seltsam klingen würde.

**Mit korrekter Sprachauszeichnung:**

```html
<p>Die Entwicklerin sagte auf der Konferenz: <span lang="en">This is a game changer</span>.</p>
```

Hier umschließt das `<span>`-Element den englischen Teil. Das `lang="en"`-Attribut signalisiert allen Systemen: „Achtung, der Inhalt dieses Elements ist auf Englisch.“

#### Anwendungsfälle im Detail

Schauen wir uns einige typische Szenarien an, in denen ein Sprachwechsel im Dokument sinnvoll und notwendig ist.

##### Zitate in Originalsprache

Es ist üblich, berühmte Zitate in ihrer Ursprungssprache wiederzugeben. Kombiniere hier das `lang`-Attribut mit semantisch passenden Elementen wie `<q>` (für kurze, inline-Zitate) oder `<blockquote>` (für längere, block-level-Zitate).

```html
<p>
  Wie Shakespeare schon schrieb: <q lang="en-GB">To be, or not to be, that is the question</q>.
  Das fasst das Dilemma perfekt zusammen.
</p>

<figure>
  <blockquote lang="fr">
    <p>L'enfer, c'est les autres.</p>
  </blockquote>
  <figcaption>— Jean-Paul Sartre, <cite>Huis clos</cite></figcaption>
</figure>
```

Im ersten Beispiel wird ein kurzes englisches Zitat (spezifisch britisches Englisch mit `en-GB`) inline ausgezeichnet. Im zweiten Beispiel ist ein ganzes `<blockquote>`-Element als französisch (`fr`) markiert.

##### Fremdwörter und Fachbegriffe

Unsere Sprache ist durchsetzt mit Begriffen aus anderen Sprachen, insbesondere aus dem Englischen im IT-Bereich. Auch wenn sie uns geläufig sind, ist es technisch korrekt, sie auszuzeichnen.

```html
<p>
  Wir müssen den <span lang="en">Bug</span> im neuen <span lang="en">Feature</span> schnell beheben.
  Das nächste <span lang="en">Release</span> ist für Freitag geplant, daher ist das
  die höchste Priorität für das <span lang="en">Development-Team</span>.
</p>
```

Auch wenn es nach viel Aufwand für einzelne Wörter aussieht, ist der Nutzen für assistierende Technologien erheblich.

##### Titel von Werken

Buchtitel, Filmtitel, Songtitel oder auch Namen von Organisationen sollten in ihrer Originalsprache ausgezeichnet werden, oft in Kombination mit dem `<cite>`-Element.

```html
<p>
  Einer meiner Lieblingsfilme ist <cite lang="en">Blade Runner</cite>. 
  Die Buchvorlage dazu, <cite lang="en">Do Androids Dream of Electric Sheep?</cite>, 
  ist ebenfalls fantastisch.
</p>
```

Dies stellt sicher, dass ein Screenreader „Blade Runner“ nicht deutsch ausspricht, sondern korrekt als englischen Titel vorliest.

#### Styling basierend auf der Sprache mit CSS

Wie bereits erwähnt, eröffnet dir die korrekte Sprachauszeichnung auch gestalterische Möglichkeiten. Die CSS-Pseudoklasse `:lang()` wählt Elemente basierend auf dem Wert ihres `lang`-Attributs aus.

Angenommen, du möchtest alle englischen Textpassagen kursiv darstellen und für japanischen Text eine spezielle, gut lesbare Schriftart verwenden.

```css
/* Wähle alle Elemente mit dem Attribut lang="en" */
:lang(en) {
  font-style: italic;
  color: #555;
}

/* Wähle alle Elemente mit dem Attribut lang="ja" */
:lang(ja) {
  font-family: "Noto Sans JP", sans-serif;
  font-size: 1.1em;
}
```

Mit diesem CSS würden die folgenden HTML-Elemente entsprechend formatiert:

```html
<p>
  Mein Motto ist: <span lang="en">Keep it simple</span>.
</p>

<p>
  Das japanische Wort für „Danke“ ist <span lang="ja">ありがとう</span> (<span lang="ja-Latn">arigatō</span>).
</p>
```

Beachte im zweiten Beispiel, wie sogar verschiedene Schriftsysteme derselben Sprache (Japanisch in Kana/Kanji und in lateinischer Umschrift `ja-Latn`) unterschiedlich behandelt werden könnten.

#### Ein kurzer Blick auf `xml:lang`

Wenn du dich tiefer mit der Materie befasst, wirst du vielleicht auf das Attribut `xml:lang` stoßen. Es stammt aus der XML-Welt und erfüllt denselben Zweck wie `lang`. In der Zeit von XHTML war es üblich und sogar notwendig, beide Attribute zu verwenden, um die Kompatibilität zu gewährleisten:

```xml
<!-- XHTML-Syntax -->
<p xmlns="http://www.w3.org/1999/xhtml">
  Dies ist ein Satz mit einem <span lang="en" xml:lang="en">englischen Teil</span>.
</p>
```

Für modernes HTML5 lautet die klare Empfehlung: **Verwende nur das `lang`-Attribut.** Es ist ausreichend und korrekt. Das `xml:lang`-Attribut ist nur in XML-basierten Kontexten wie XHTML oder SVG von Bedeutung. Wenn du reines HTML schreibst, kannst du es getrost ignorieren.

Die Fähigkeit, die Sprache für einzelne Teile deines Dokuments zu deklarieren, ist ein mächtiges Werkzeug. Es ist ein Detail, das oft übersehen wird, aber einen fundamentalen Beitrag zu einem zugänglichen, verständlichen und professionellen Webauftritt leistet. Es zeigt, dass du nicht nur an die visuelle Darstellung denkst, sondern auch an die strukturelle Qualität und die universelle Nutzbarkeit deiner Inhalte.
