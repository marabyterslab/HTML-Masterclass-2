# Quellenangabe mit cite

### Quellenangaben mit `<cite>`: Den Urhebern die Ehre erweisen

Stell dir vor, du schreibst einen Blogartikel, eine wissenschaftliche Arbeit oder einfach nur eine Produktbeschreibung. Oft beziehst du dich auf andere Werke: Du zitierst einen Satz aus einem Buch, erwähnst einen inspirierenden Film oder verweist auf einen wegweisenden Fachartikel. Im akademischen Umfeld ist die korrekte Angabe von Quellen eine Selbstverständlichkeit. Aber auch im Web ist es mehr als nur guter Stil – es ist ein Zeichen von Respekt gegenüber dem Urheber und gibt deinem eigenen Inhalt mehr Glaubwürdigkeit.

HTML, als Sprache der Bedeutung (Semantik), bietet uns genau für diesen Zweck ein spezielles Werkzeug: das `<cite>`-Element. Mit ihm kannst du den Titel eines zitierten Werkes auszeichnen und ihm so eine klare, maschinenlesbare Bedeutung geben.

#### Was genau ist ein `<cite>`-Element?

Das `<cite>`-Element ist dafür gedacht, den Titel eines kreativen Werkes zu umschließen. Das klingt zunächst vielleicht etwas abstrakt, aber die Liste solcher Werke ist lang und vielfältig. Dazu gehören zum Beispiel:

*   **Bücher:** <cite>Der Herr der Ringe</cite>
*   **Filme:** <cite>Star Wars: Episode IV – Eine neue Hoffnung</cite>
*   **Songs oder Musikalben:** <cite>Bohemian Rhapsody</cite>
*   **Theaterstücke:** <cite>Faust</cite>
*   **Gedichte:** <cite>Der Erlkönig</cite>
*   **Gemälde oder Skulpturen:** <cite>Die Sternennacht</cite>
*   **Wissenschaftliche Arbeiten oder Berichte:** <cite>Zur Elektrodynamik bewegter Körper</cite>
*   **Websites oder Blog-Posts:** <cite>A List Apart</cite>

Wann immer du den Titel eines solchen Werkes in deinem Text erwähnst, solltest du ihn mit `<cite>`-Tags umschließen.

```html
<p>In meinem letzten Urlaub habe ich endlich <cite>Moby Dick</cite> gelesen. Ein wirklich beeindruckendes Werk!</p>

<p>Der Film <cite>Inception</cite> regt auch Jahre nach seiner Veröffentlichung noch zu Diskussionen an.</p>
```

Die Standarddarstellung in den meisten Browsern ist, den Inhalt des `<cite>`-Elements kursiv zu setzen. Aber lass dich davon nicht täuschen! Der entscheidende Punkt ist nicht das Aussehen, sondern die Bedeutung, die du dem Text damit verleihst.

#### Der häufigste Fehler: `<cite>` ist nicht für Personen!

Hier müssen wir kurz innehalten, denn dies ist der mit Abstand häufigste Fehler im Umgang mit `<cite>`. Das Element ist **ausschließlich für den Titel eines Werkes** gedacht, **niemals für den Namen einer Person oder einer Organisation**.

Ein Zitat stammt zwar von einer Person, aber der Name dieser Person ist kein "kreatives Werk". Er ist einfach nur ein Name.

**Falsch:**
```html
<p>Wie <cite>William Shakespeare</cite> schon sagte: "Sein oder Nichtsein, das ist hier die Frage."</p>
```

**Richtig:**
```html
<p>Wie William Shakespeare schon sagte: "Sein oder Nichtsein, das ist hier die Frage."</p>
```

Noch besser und semantisch wertvoller ist es, das Werk zu nennen, aus dem das Zitat stammt. Hier kommt `<cite>` dann wieder korrekt zum Einsatz:

**Semantisch perfekt:**
```html
<p>Wie William Shakespeare in <cite>Hamlet</cite> schrieb: "Sein oder Nichtsein, das ist hier die Frage."</p>
```

Dieser Unterschied ist fundamental. Suchmaschinen und assistierende Technologien wie Screenreader können so klar zwischen dem Urheber (einer Person) und dem Werk (einem Titel) unterscheiden. Diese präzise Auszeichnung ist der Kern von guter, semantischer HTML.

#### `<cite>` im Zusammenspiel mit Block- und Inline-Zitaten

Am häufigsten wirst du `<cite>` in Kombination mit den Elementen für Zitate verwenden: `<blockquote>` für längere, blockförmige Zitate und `<q>` für kurze, in den Fließtext integrierte Zitate.

Stell dir vor, du möchtest ein längeres Zitat aus einem Buch anführen. Die semantisch korrekte Struktur dafür verwendet oft eine Kombination aus `<figure>`, `<blockquote>` und `<figcaption>`. Das `<cite>`-Element findet dann seinen Platz innerhalb der `<figcaption>` (Bild- oder Figurenbeschriftung), um die Quelle zu benennen.

```html
<figure>
  <blockquote>
    <p>Zwei Dinge sind unendlich, das Universum und die menschliche Dummheit, aber bei dem Universum bin ich mir noch nicht ganz sicher.</p>
  </blockquote>
  <figcaption>
    — Albert Einstein, oft zitiert, obwohl der genaue Ursprung in seinen Werken umstritten ist.
  </figcaption>
</figure>
```

Wenn du hier das genaue Werk angeben könntest, würde es so aussehen:

```html
<figure>
  <blockquote>
    <p>Es ist ein grober Fehler, zu theoretisieren, bevor man Daten hat.</p>
  </blockquote>
  <figcaption>
    — Sherlock Holmes in <cite>Ein Skandal in Böhmen</cite> von Arthur Conan Doyle
  </figcaption>
</figure>
```

Hier siehst du perfekt, wie die Elemente zusammenarbeiten:
*   `<blockquote>` umschließt das Zitat selbst.
*   `<figcaption>` enthält die Zusatzinformation zum Zitat, nämlich den Urheber und die Quelle.
*   `<cite>` zeichnet gezielt den Titel des Werkes aus.

Für kurze Zitate im Fließtext funktioniert das Prinzip analog mit dem `<q>`-Element:

```html
<p>Meine Lieblingszeile aus dem Film <cite>Casablanca</cite> ist und bleibt <q>Ich schau dir in die Augen, Kleines</q>.</p>
```

#### Abgrenzung zu `<i>` und `<em>`

Anfänger neigen manchmal dazu, Elemente nach ihrem Aussehen auszuwählen. `<cite>`, `<i>` (Idiomatic Text) und `<em>` (Emphasis) werden von Browsern standardmäßig kursiv dargestellt. Ihre semantische Bedeutung ist jedoch grundverschieden.

*   **`<em>` (Emphasis):** Wird verwendet, um ein Wort oder eine Phrase zu betonen. Die Betonung verändert die Bedeutung des Satzes. Ein Screenreader würde dieses Wort mit einer anderen Betonung vorlesen.
    ```html
    <p>Du musst das <em>unbedingt</em> heute noch erledigen!</p>
    ```
*   **`<i>` (Idiomatic Text):** Wird für Text verwendet, der sich stilistisch vom Rest abhebt, ohne eine besondere Betonung zu haben. Typische Anwendungsfälle sind Fachbegriffe, fremdsprachige Wörter, Schiffsnamen oder die Gedanken einer Figur.
    ```html
    <p>Das Konzept des <i>Deus ex Machina</i> wird oft kritisiert.</p>
    ```
*   **`<cite>` (Citation):** Wird, wie wir nun wissen, ausschließlich für den Titel eines kreativen Werkes verwendet.
    ```html
    <p>Ich lese gerade <cite>Stolz und Vorurteil</cite>.</p>
    ```

Die Wahl des richtigen Tags hängt also immer von der *Bedeutung* des Inhalts ab, niemals von seiner gewünschten Darstellung.

#### `<cite>` stylen mit CSS

Da wir die Wahl des HTML-Elements von seiner Darstellung entkoppeln, kannst du das Aussehen von `<cite>`-Elementen natürlich frei mit CSS gestalten. Vielleicht passt Kursivschrift nicht zu deinem Design, oder du möchtest Zitate besonders hervorheben.

Angenommen, du möchtest alle Werktitel nicht kursiv, sondern in einer anderen Farbe und mit einer dezenten Unterstreichung darstellen:

```css
cite {
  font-style: normal; /* Hebt die standardmäßige Kursivschrift auf */
  color: #4a69bd;     /* Eine sanfte Blaufarbe */
  border-bottom: 1px dotted #4a69bd;
  padding-bottom: 1px;
}
```

Mit diesem CSS-Code wird jeder Text, den du in `<cite>`-Tags eingeschlossen hast, auf deiner gesamten Website einheitlich und nach deinen Vorstellungen formatiert. Das ist die Stärke der Trennung von Struktur (HTML) und Präsentation (CSS).

#### Der kleine Unterschied: Das `cite`-Attribut

Zum Abschluss noch ein wichtiger Hinweis, um Verwirrung zu vermeiden. Es gibt nicht nur das `<cite>`-**Element**, sondern auch ein `cite`-**Attribut**. Dieses Attribut kann in `<blockquote>`- und `<q>`-Tags verwendet werden und sollte eine URL enthalten, die zur Online-Quelle des Zitats führt.

Das Attribut ist für den Besucher nicht direkt sichtbar, kann aber von Browsern, Suchmaschinen oder anderen Werkzeugen ausgelesen werden.

```html
<blockquote cite="https://www.projekt-gutenberg.org/kafka/prozess/prozess.html">
  <p>Jemand mußte Josef K. verleumdet haben, denn ohne daß er etwas Böses getan hätte, wurde er eines Morgens verhaftet.</p>
</blockquote>
```

Die beste Praxis ist oft, beides zu kombinieren: das `cite`-Attribut für die maschinenlesbare URL und das `<cite>`-Element für den für Menschen lesbaren Titel der Quelle.

```html
<figure>
  <blockquote cite="https://www.projekt-gutenberg.org/kafka/prozess/prozess.html">
    <p>Jemand mußte Josef K. verleumdet haben, denn ohne daß er etwas Böses getan hätte, wurde er eines Morgens verhaftet.</p>
  </blockquote>
  <figcaption>— Erster Satz aus Franz Kafkas Roman <cite>Der Process</cite>.</figcaption>
</figure>
```

Mit diesem Wissen bist du bestens gerüstet, um Quellen und Verweise in deinem HTML-Code nicht nur korrekt, sondern auch semantisch reichhaltig auszuzeichnen. Du gibst damit nicht nur den Urhebern die verdiente Ehre, sondern machst deine Inhalte auch für Maschinen verständlicher und für alle zugänglicher.
