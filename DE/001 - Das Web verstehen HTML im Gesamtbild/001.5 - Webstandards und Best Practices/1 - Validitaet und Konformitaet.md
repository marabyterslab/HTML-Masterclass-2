# Validität und Konformität

### Validität und Konformität: Die Spielregeln des Webs

Stell dir vor, du spielst ein Brettspiel mit Freunden, aber jeder von euch hat eine leicht unterschiedliche Version der Spielanleitung. Der eine glaubt, man darf mit einer Sechs noch einmal würfeln, der andere nicht. Das Ergebnis? Chaos, Missverständnisse und am Ende funktioniert das Spiel nicht mehr so, wie es vom Erfinder gedacht war.

Im World Wide Web ist es ganz ähnlich. Die „Spielanleitung“ für HTML wird von Gremien wie dem World Wide Web Consortium (W3C) und der Web Hypertext Application Technology Working Group (WHATWG) geschrieben. Diese Anleitungen, die sogenannten Spezifikationen, legen ganz genau fest, wie HTML-Code geschrieben werden muss, damit er überall gleich verstanden wird. Wenn wir uns an diese Regeln halten, schreiben wir „validen“ und „konformen“ Code. Doch was bedeuten diese Begriffe genau und warum sind sie so wichtig für deine Arbeit als Webentwickler?

#### Was bedeutet Validität?

Validität ist im Grunde die grammatikalische Korrektheit deines HTML-Codes. So wie die deutsche Sprache Regeln für Satzbau, Rechtschreibung und Zeichensetzung hat, hat auch HTML eine feste Grammatik. Ein HTML-Dokument ist valide, wenn es diesen Regeln exakt folgt.

Diese Regeln definieren zum Beispiel:
*   Welche Tags es überhaupt gibt (z.B. `<p>`, `<div>`, `<span>`).
*   Welche Attribute ein bestimmtes Tag haben darf (z.B. ein `<img>`-Tag darf ein `src`- und ein `alt`-Attribut haben, ein `<p>`-Tag aber nicht).
*   Wie Tags ineinander verschachtelt werden dürfen (z.B. darf ein `<li>`-Element nur innerhalb von `<ul>` oder `<ol>` stehen, und ein `<p>`-Tag darf keinen weiteren `<p>`-Tag enthalten).
*   Ob ein Tag geschlossen werden muss (z.B. muss `<p>` mit `</p>` geschlossen werden, während `<br>` für sich allein steht).

Um zu überprüfen, ob dein Code valide ist, musst du ihn nicht von Hand mit der Spezifikation abgleichen. Dafür gibt es spezialisierte Werkzeuge, die sogenannten Validatoren. Der bekannteste ist der W3C Markup Validation Service. Du kannst ihm eine URL geben, eine Datei hochladen oder deinen Code direkt hineinkopieren, und er prüft ihn Zeile für Zeile auf grammatikalische Fehler – wie eine Rechtschreibprüfung für deinen Code.

Schauen wir uns ein einfaches Beispiel für invaliden Code an:

```html
<p>Hier ist ein Absatz, der eine wichtige Information enthält.
  <p>Und hier ist fälschlicherweise ein zweiter Absatz im ersten.</p>
</p>
```

Dieser Code ist nicht valide. Die HTML-Spezifikation besagt klar, dass ein Absatz-Element (`<p>`) kein weiteres Block-Element wie einen anderen Absatz enthalten darf. Ein Validator würde hier einen Fehler melden. Die korrekte, valide Version sähe so aus:

```html
<p>Hier ist ein Absatz, der eine wichtige Information enthält.</p>
<p>Und hier ist ein zweiter Absatz, der korrekt nach dem ersten steht.</p>
```

Du wirst jetzt vielleicht denken: „Aber mein Browser zeigt den ersten Code doch trotzdem irgendwie an!“ Und du hast absolut recht. Moderne Webbrowser sind extrem fehlertolerant. Wenn sie auf invaliden Code stoßen, werfen sie nicht einfach einen Fehler und geben auf. Stattdessen versuchen sie zu raten, was du wohl gemeint haben könntest, und korrigieren den Fehler im Stillen. Man nennt diesen Prozess „Error Correction“ oder umgangssprachlich das Verarbeiten von „Tag Soup“.

Das klingt zunächst praktisch, birgt aber eine gewaltige Gefahr.

#### Warum Validität so entscheidend ist

Wenn jeder Browser Fehler auf seine eigene, leicht unterschiedliche Weise korrigiert, verlierst du die Kontrolle. Dein Code wird unberechenbar. Das ist der Hauptgrund, warum valider Code eine der wichtigsten Best Practices in der Webentwicklung ist. Lass uns die Vorteile im Detail betrachten:

**1. Vorhersehbarkeit und Konsistenz:**
Wenn dein Code valide ist, gibt es keine Zweideutigkeiten. Jeder Browser, der sich an die Standards hält, wird dein HTML exakt gleich interpretieren und dieselbe Grundstruktur (das Document Object Model, kurz DOM) aufbauen. Du schließt damit eine riesige Quelle für seltsame und schwer zu findende Bugs aus, bei denen deine Seite in Chrome super aussieht, in Firefox aber leicht verschoben ist und im Safari komplett anders reagiert. Valider Code ist die Basis für ein konsistentes Verhalten über alle Plattformen hinweg.

**2. Zukünftige Kompatibilität:**
Browser entwickeln sich ständig weiter. Ihre Algorithmen zur Fehlerkorrektur können sich mit jeder neuen Version ändern. Wenn du dich darauf verlässt, dass ein Browser deinen fehlerhaften Code heute auf eine bestimmte Weise „repariert“, gibt es keine Garantie, dass er das in zwei Jahren immer noch so tun wird. Eine zukünftige, standardkonformere Browser-Version könnte deinen Code plötzlich ganz anders interpretieren, und deine Seite geht kaputt. Valider Code hingegen ist zukunftssicher. Er basiert auf den festgeschriebenen Regeln und wird auch in zukünftigen Browsern wie erwartet funktionieren.

**3. Barrierefreiheit (Accessibility):**
Dies ist vielleicht der wichtigste Punkt. Nicht nur Menschen mit ihren Augen betrachten deine Webseite. Assistive Technologien wie Screenreader für blinde oder sehbehinderte Nutzer lesen den Code und interpretieren seine Struktur, um den Inhalt verständlich vorzutragen. Diese Programme sind auf eine saubere, logische und korrekte Dokumentenstruktur angewiesen. Ein falsch verschachteltes Listenelement, eine fehlende Tabellenüberschrift oder eine kaputte Überschriftenhierarchie können eine Seite für diese Nutzer völlig unbrauchbar machen. Valider Code ist die Grundlage für eine barrierefreie Webseite.

**4. Suchmaschinenoptimierung (SEO):**
Die Crawler von Suchmaschinen wie Google sind ebenfalls Maschinen, die deinen Code analysieren, um den Inhalt und die Relevanz deiner Seite zu verstehen. Ein sauberes, valides HTML-Dokument erleichtert es ihnen, die Struktur deiner Inhalte zu erkennen – was die Hauptüberschrift ist, was eine Liste von Merkmalen und was ein einfacher Textabsatz. Eine klare Struktur kann sich positiv auf dein Ranking auswirken.

**5. Professionalität und Wartbarkeit:**
Valider Code ist ein Zeichen von Professionalität und Sorgfalt. Er ist für dich und deine Kollegen leichter zu lesen, zu verstehen und zu warten. Wenn du dich an die offiziellen Regeln hältst, schaffst du eine verlässliche Grundlage, auf der andere aufbauen können, ohne erst deine individuellen „Dialekte“ und Fehler umgehen zu müssen.

#### Konformität: Mehr als nur korrekte Grammatik

Während Validität sich auf die Einhaltung der reinen Syntaxregeln konzentriert, geht der Begriff **Konformität** (Conformance) einen Schritt weiter. Ein HTML-Dokument ist konform, wenn es nicht nur valide ist, sondern auch allen anderen Regeln und semantischen Vorgaben der Spezifikation entspricht.

Das klingt vielleicht abstrakt, lässt sich aber an einem Beispiel gut verdeutlichen. Betrachte diesen Code:

```html
<!-- Dieser Code ist technisch valide -->
<h1>Impressum</h1>
<p>Hier finden Sie unsere Kontaktinformationen.</p>
```
Dieser Code-Schnipsel ist aus rein grammatikalischer Sicht valide. Das `<h1>`-Tag ist korrekt geschrieben und enthält Text. Es gibt keine Syntaxfehler.

Aber ist er auch konform? Das kommt darauf an. Die HTML-Spezifikation besagt, dass `<h1>` die Hauptüberschrift einer Seite oder eines Hauptabschnitts sein soll. Wenn dieser Code auf einer separaten Impressums-Seite steht, ist er konform. Wenn er aber nur ein kleiner Abschnitt am Ende deiner Startseite ist, deren eigentliche Hauptüberschrift „Willkommen bei der HTML-Masterclass“ lautet, dann ist der Code zwar valide, aber **nicht konform**. Du missbrauchst das `<h1>`-Element für etwas, wofür es semantisch nicht gedacht ist. Die korrekte, konforme Verwendung wäre hier wahrscheinlich ein `<h2>` oder `<h3>`, je nach Hierarchie der Seite.

Konformität bedeutet also, HTML so zu verwenden, wie es gedacht ist: zur Beschreibung der Bedeutung und Struktur deines Inhalts. Es geht darum, das richtige Werkzeug für die jeweilige Aufgabe zu wählen. Du verwendest `<em>` für Betonung, nicht weil es Text kursiv macht. Du verwendest `<ul>` für eine ungeordnete Liste, nicht weil es dir Einrückungen und Punkte liefert. Das Aussehen steuerst du mit CSS; die Struktur und Bedeutung definierst du mit konformem HTML.

#### Pragmatismus in der realen Welt

Das Ziel sollte immer sein, zu 100 % validen und konformen Code zu schreiben. In der Praxis wirst du jedoch manchmal auf Situationen stoßen, in denen das schwierig ist. Vielleicht bindest du ein Werbebanner eines Drittanbieters ein, das invaliden Code erzeugt, oder das Content-Management-System deines Kunden lässt dir keine andere Wahl.

In solchen Momenten ist es wichtig, die Prinzipien hinter Validität und Konformität zu verstehen. Der Sinn ist nicht, blind einen grünen Haken im Validator zu jagen. Der Sinn ist es, die daraus resultierenden Vorteile – Konsistenz, Zukunftssicherheit, Barrierefreiheit und Wartbarkeit – zu erreichen. Wenn du einen Kompromiss eingehen musst, kannst du eine fundierte Entscheidung treffen, welche Auswirkungen dieser Fehler haben könnte. Ein falsch platziertes `<div>` ist vielleicht ärgerlich, aber eine kaputte Überschriftenstruktur kann deine Seite für manche Nutzer unzugänglich machen.

Am Anfang deiner Reise als Webentwickler solltest du jedoch eine Null-Toleranz-Politik gegenüber Fehlern in deinem eigenen Code verfolgen. Nutze den Validator regelmäßig. Mach es dir zur Gewohnheit, deinen Code zu prüfen und zu verstehen, warum ein Fehler ein Fehler ist. So baust du von Grund auf ein tiefes Verständnis für die Regeln des Webs auf – die Grundlage, um robuste, zugängliche und professionelle Webseiten zu erschaffen.
