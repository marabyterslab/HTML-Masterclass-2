# Titel-Attribut und Tooltips

### Zusatzinformationen auf den zweiten Blick: Das `title`-Attribut und Tooltips

Du kennst nun das Herzstück eines jeden Links: den Anker-Tag `<a>` mit seinem `href`-Attribut, das das Ziel festlegt. Der Text zwischen `<a>` und `</a>` wiederum gibt dem Nutzer einen direkten Hinweis darauf, wohin die Reise geht. Aber was ist, wenn dieser sichtbare Text nicht ausreicht? Was, wenn du zusätzliche Informationen bereitstellen möchtest, ohne die Seite mit Text zu überladen? Genau hier kommt das `title`-Attribut ins Spiel.

#### Was ist das `title`-Attribut?

Das `title`-Attribut ist ein sogenanntes globales Attribut. "Global" bedeutet in diesem Zusammenhang, dass du es auf nahezu jedes HTML-Element anwenden kannst, nicht nur auf Links. Seine Hauptaufgabe ist es, zusätzliche, beschreibende Informationen zu einem Element zu liefern.

In der Praxis äußert sich das meistens in Form eines kleinen Pop-ups, das erscheint, wenn ein Nutzer mit der Maus über das Element fährt und einen Moment verweilt. Dieses Pop-up wird als "Tooltip" bezeichnet. Der Text, den du dem `title`-Attribut zuweist, wird zum Inhalt dieses Tooltips.

Stellen wir uns einen einfachen Link vor:

```html
<a href="dokumente/datenschutzerklaerung_v3.pdf">Unsere Datenschutzrichtlinien</a>
```

Dieser Link ist funktional und klar. Aber wir können ihn mit einem `title`-Attribut anreichern, um dem Nutzer mehr Kontext zu geben, bevor er überhaupt klickt.

```html
<a href="dokumente/datenschutzerklaerung_v3.pdf" title="Öffnet die aktuelle Datenschutzerklärung als PDF-Dokument in einem neuen Tab.">Unsere Datenschutzrichtlinien</a>
```

Wenn du nun mit dem Mauszeiger über den Link "Unsere Datenschutzrichtlinien" fährst, erscheint nach einer kurzen Verzögerung ein kleines Fenster mit dem Text: "Öffnet die aktuelle Datenschutzerklärung als PDF-Dokument in einem neuen Tab." Dieser kleine Hinweis kann extrem nützlich sein. Er informiert den Nutzer darüber, dass es sich um ein PDF handelt, und gibt vielleicht sogar einen Hinweis auf das Verhalten des Links (obwohl das Öffnen in einem neuen Tab technisch durch das `target`-Attribut gesteuert wird).

#### Mehr als nur Links: `title` in Aktion

Wie bereits erwähnt, ist das `title`-Attribut nicht auf Anker-Tags beschränkt. Seine Fähigkeit, kontextbezogene Zusatzinformationen zu liefern, macht es zu einem flexiblen Werkzeug für viele Situationen.

**Bilder mit Zusatzinformationen**

Bei Bildern (`<img>`) gibt es oft Verwirrung zwischen dem `alt`- und dem `title`-Attribut. Merke dir diese einfache Regel:

*   Das `alt`-Attribut (Alternativtext) beschreibt den *Inhalt* des Bildes für den Fall, dass es nicht geladen werden kann oder von einem Screenreader für sehbehinderte Nutzer vorgelesen wird. Es ist ein Ersatz für das Bild.
*   Das `title`-Attribut liefert *zusätzliche* Informationen zum Bild, wenn es sichtbar ist.

Ein Beispiel:

```html
<img src="bilder/berlin-brandenburger-tor-nacht.jpg" 
     alt="Das Brandenburger Tor in Berlin, bei Nacht beleuchtet." 
     title="Foto aufgenommen von Anna Musterfrau im September 2023.">
```

Hier erfüllt jedes Attribut seine spezifische Aufgabe. Der `alt`-Text beschreibt, was zu sehen ist. Der `title`-Text gibt eine ergänzende Information, in diesem Fall den Fotonachweis, der als Tooltip erscheint.

**Abkürzungen und Akronyme**

Eine semantisch sehr saubere und empfohlene Verwendung des `title`-Attributs ist in Kombination mit dem `<abbr>`-Tag für Abkürzungen. Es ermöglicht dir, die ausgeschriebene Bedeutung einer Abkürzung bereitzustellen, ohne den Lesefluss zu stören.

```html
<p>Die Spezifikationen des <abbr title="World Wide Web Consortium">W3C</abbr> sind der Standard für die Webentwicklung.</p>
```

Fährt ein Nutzer über "W3C", verrät der Tooltip, wofür diese Abkürzung steht. Das ist elegant und verbessert das Verständnis deines Textes.

#### Die Grenzen des `title`-Attributs: Eine kritische Betrachtung

So nützlich das `title`-Attribut auch scheint, es hat entscheidende Nachteile, die du unbedingt kennen musst. Die größte Schwäche liegt im Bereich der Zugänglichkeit (Accessibility) und der mobilen Nutzung.

**Problem 1: Touch-Geräte**

Die grundlegende Interaktion, die einen Tooltip auslöst, ist das "Hovern" – das Schweben des Mauszeigers über einem Element. Auf Smartphones und Tablets gibt es dieses Konzept nicht. Ein Nutzer kann nur tippen. Damit ist der Inhalt des `title`-Attributs für die riesige Gruppe der mobilen Nutzer praktisch unsichtbar und unerreichbar.

**Problem 2: Tastaturnavigation**

Viele Nutzer navigieren aus Notwendigkeit (z.B. bei motorischen Einschränkungen) oder aus Effizienzgründen mit der Tastatur durch eine Webseite, meistens mit der `Tab`-Taste. In den meisten Browsern wird der Inhalt des `title`-Attributs nicht angezeigt, wenn ein Element per Tastatur den Fokus erhält. Auch diese Nutzergruppe schließt du also aus.

**Problem 3: Screenreader**

Die Unterstützung durch Screenreader ist inkonsistent. Einige lesen den `title`-Inhalt vor, andere ignorieren ihn standardmäßig, wieder andere benötigen spezielle Einstellungen, um ihn zu aktivieren. Sich darauf zu verlassen, dass sehbehinderte Nutzer die Information erhalten, ist daher ein Glücksspiel.

**Die goldene Regel für die Verwendung von `title`**

Aus diesen Problemen leitet sich eine fundamentale Regel ab:

**Informationen, die für das Verständnis des Inhalts oder die Bedienung der Webseite essenziell sind, dürfen NIEMALS ausschließlich im `title`-Attribut stehen.**

Das `title`-Attribut ist ausschließlich für *ergänzende, nicht kritische* Informationen gedacht. Es ist ein "Nice-to-have", kein "Must-have". Wenn eine Information wichtig ist, muss sie direkt im sichtbaren Text der Seite stehen.

**Ein schlechtes Beispiel:**

Stell dir eine Icon-Leiste ohne Textbeschriftung vor.

```html
<!-- FALSCH! Kritische Information ist versteckt. -->
<a href="/einstellungen" title="Einstellungen"><img src="icon-zahnrad.svg" alt="Icon"></a>
<a href="/profil" title="Mein Profil"><img src="icon-benutzer.svg" alt="Icon"></a>
```

Ein sehender Maus-Nutzer kann die Funktion vielleicht erraten, aber mobile Nutzer, Tastatur-Nutzer und viele Screenreader-Nutzer haben keine Ahnung, wohin diese Links führen. Der `alt`-Text ist hier ebenfalls nicht hilfreich.

**Ein gutes Beispiel:**

```html
<!-- BESSER! Funktion ist klar, title bietet nur eine kleine Ergänzung. -->
<button type="submit" title="Die eingegebenen Daten werden dauerhaft gespeichert.">Speichern</button>
```

Hier ist die primäre Funktion ("Speichern") für jeden klar ersichtlich. Der `title`-Text bietet lediglich eine unkritische Zusatzinformation über die Konsequenz der Handlung. Wer sie nicht sieht, verpasst nichts Wesentliches.

#### Styling von Tooltips? Nur mit Tricks

Ein letzter Punkt, der oft aufkommt, ist die Gestaltung der Tooltips. Die vom Browser erzeugten Tooltips, die durch das `title`-Attribut entstehen, sind betriebssystemabhängig und lassen sich mit CSS nicht gestalten. Ihr Aussehen (Schriftart, Farbe, Größe) ist fest vorgegeben.

Wenn du vollständig gestaltbare Tooltips benötigst, musst du auf Techniken mit CSS und oft auch JavaScript zurückgreifen. Dabei werden in der Regel keine `title`-Attribute verwendet, sondern die Informationen in `data-*`-Attributen gespeichert und per CSS (z.B. mit den Pseudoelementen `::before` oder `::after`) oder durch dynamisch erzeugte HTML-Elemente sichtbar gemacht. Das ist jedoch ein fortgeschrittenes Thema, das über die Grundlagen von HTML hinausgeht.

Für den Moment ist es wichtig, dass du das `title`-Attribut als das verstehst, was es ist: ein einfaches, natives HTML-Werkzeug, um unkritische Zusatzinformationen auf Desktop-Geräten bereitzustellen – nicht mehr und nicht weniger. Setze es bewusst und mit Bedacht ein, immer mit dem Gedanken an die Zugänglichkeit deiner Webseite im Hinterkopf.
