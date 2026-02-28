# Validität und Konformität

### Validität und Konformität: Das Regelwerk des Webs

Stell dir vor, du schreibst einen Text in einer Fremdsprache. Du könntest alle Wörter richtig schreiben, aber wenn du die Grammatik und den Satzbau missachtest, wird dein Text schwer verständlich, missverständlich oder im schlimmsten Fall komplett unsinnig. Im Web ist HTML die Sprache, und die „Grammatik“ wird durch Webstandards definiert. Die Einhaltung dieser Regeln nennen wir Validität und Konformität. Auf den ersten Blick mögen diese Begriffe trocken und akademisch klingen, aber sie sind das Fundament für eine professionelle, robuste und zugängliche Website.

#### Was bedeutet Validität?

Ein HTML-Dokument ist **valide**, wenn es den syntaktischen Regeln einer bestimmten HTML-Version exakt folgt. Diese Regeln sind in einer Spezifikation festgelegt, die wie ein offizielles Regelbuch für die Sprache fungiert. Die wichtigsten Organisationen, die diese Spezifikationen pflegen, sind das World Wide Web Consortium (W3C) und die Web Hypertext Application Technology Working Group (WHATWG). Für modernes HTML ist die WHATWG mit ihrem „HTML Living Standard“ die treibende Kraft.

Ein Validator ist ein Werkzeug, das dein HTML-Dokument mit diesen Regeln abgleicht. Er agiert wie ein unbestechlicher Lektor, der deinen Code Zeile für Zeile prüft und dir jeden Grammatikfehler anzeigt.

Ein Validator prüft unter anderem:

*   **Korrekte Verschachtelung:** Jedes Element, das du öffnest, muss korrekt geschlossen werden, bevor sein übergeordnetes Element geschlossen wird. `p><em>Text</em></p>` ist korrekt, `<p><em>Text</p></em>` ist es nicht.
*   **Erlaubte Elemente:** Bestimmte Elemente dürfen nur an bestimmten Stellen oder innerhalb anderer Elemente vorkommen. Ein `<li>` (Listenelement) ergibt beispielsweise nur innerhalb einer `<ul>` (unsortierte Liste) oder `<ol>` (sortierte Liste) Sinn.
*   **Gültige Attribute:** Nicht jedes Attribut ist für jedes Element erlaubt. Das `href`-Attribut ist für einen `<a>`-Tag unerlässlich, aber auf einem `<p>`-Tag hat es nichts zu suchen.
*   **Korrekte Dokumentenstruktur:** Ein valides HTML-Dokument benötigt eine grundlegende Struktur, die mit der Dokumenttyp-Deklaration beginnt und die Elemente `<html>`, `<head>` und `<body>` korrekt anordnet.
*   **Keine veralteten Elemente:** Ältere HTML-Versionen enthielten Elemente wie `<font>` oder `<center>`, die heute als veraltet (obsolet) gelten. Ihre Funktion wurde längst von CSS übernommen. Ein Validator wird dich darauf hinweisen.

Schau dir dieses kleine, fehlerhafte Beispiel an:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Meine fehlerhafte Seite</title>
</head>
<body>
    <h1>Willkommen!
    <p>Hier ist ein <b>wichtiger<em></em></b> Text.
    <img src="bild.jpg">
</body>
</html>
```

Ein Validator würde hier mehrere Fehler finden:

1.  Der `<h1>`-Tag wurde nicht geschlossen.
2.  Der `<em>`-Tag ist leer und der `<b>`-Tag wird nicht korrekt geschlossen (obwohl moderne Browser dies oft verzeihen, ist es syntaktisch falsch).
3.  Dem `<img>`-Tag fehlt das `alt`-Attribut, was für die Barrierefreiheit entscheidend ist und in den HTML5-Regeln als Fehler gewertet wird, wenn das Bild nicht rein dekorativ ist.

Warum ist dieser Aufwand wichtig? Validität ist kein Selbstzweck. Sie führt zu handfesten Vorteilen:

*   **Vorhersehbarkeit und Konsistenz:** Browser sind Meister darin, fehlerhaften Code zu „raten“ und irgendwie darzustellen. Dieses Raten nennt man Fehlerkorrektur (Error Correction). Das Problem: Jeder Browser rät ein bisschen anders. Valider Code minimiert das Raten und sorgt dafür, dass deine Seite in Chrome, Firefox, Safari und anderen Browsern so konsistent wie möglich aussieht und funktioniert.
*   **Fehlersuche (Debugging):** Ein nicht geschlossener `<div>`-Tag kann das gesamte Layout deiner Seite zerstören. Die Suche nach einem solchen Fehler kann Stunden dauern. Ein Validator findet ihn in Sekunden. Er ist dein wichtigstes Werkzeug zur Qualitätssicherung deines Markups.
*   **Zukunftssicherheit:** Code, der sich an die aktuellen Standards hält, hat die höchste Wahrscheinlichkeit, auch in zukünftigen Browser-Generationen korrekt zu funktionieren. Du baust auf einem stabilen Fundament.
*   **Wartbarkeit:** Sauberer, valider Code ist für dich und andere Entwickler, die später daran arbeiten, wesentlich einfacher zu lesen, zu verstehen und zu erweitern.

#### Die Dokumenttyp-Deklaration (DOCTYPE): Der Schalter für die Regeln

Ganz am Anfang jedes validen HTML-Dokuments steht eine entscheidende Zeile: die Dokumenttyp-Deklaration, kurz DOCTYPE.

```html
<!DOCTYPE html>
```

Diese eine Zeile ist kein HTML-Tag, sondern eine Anweisung an den Browser. Sie sagt ihm: „Hallo, das Dokument, das jetzt kommt, ist modernes HTML. Bitte interpretiere es nach den aktuellen, standardkonformen Regeln.“

Ohne diesen DOCTYPE oder mit einem veralteten, fehlerhaften DOCTYPE schaltet der Browser in einen sogenannten **Quirks-Modus**. Dieser Modus ist ein Relikt aus den Zeiten des „Browserkriegs“ in den späten 90er-Jahren. Im Quirks-Modus versucht der Browser, das Verhalten alter, fehlerhafter Browser wie dem Internet Explorer 5 zu emulieren, um die Kompatibilität mit alten Websites zu wahren. Das führt zu unvorhersehbarem Rendering, abweichenden CSS-Interpretationen und ist ein Zustand, den du unter allen Umständen vermeiden möchtest.

Der moderne HTML5-DOCTYPE ist bewusst kurz und einfach gehalten, im Gegensatz zu seinen komplizierten Vorgängern aus der XHTML-Ära. Deine erste Handlung in jedem neuen HTML-Dokument sollte es sein, `<!DOCTYPE html>` an den Anfang zu schreiben. Damit aktivierst du den **Standards-Modus** und stellst die Weichen für sauberen, validen Code.

#### Wie du deine Dokumente validierst

Die bekannteste und verlässlichste Anlaufstelle zur Überprüfung deines HTML-Codes ist der **W3C Markup Validation Service**. Dieses kostenlose Online-Werkzeug ist der Goldstandard. Du kannst es auf drei Arten nutzen:

1.  **Validate by URI:** Gib die URL einer bereits veröffentlichten Webseite ein.
2.  **Validate by File Upload:** Lade eine HTML-Datei von deinem Computer hoch.
3.  **Validate by Direct Input:** Kopiere deinen HTML-Code direkt in ein Textfeld.

Für die Entwicklung ist die dritte Option am praktischsten. Hier ist ein Beispiel für ein minimales, aber valides HTML5-Dokument, das du zum Testen verwenden kannst:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ein valides Dokument</title>
</head>
<body>
    <p>Hallo Welt!</p>
</body>
</html>
```

Wenn du diesen Code in den W3C-Validator einfügst, erhältst du eine grüne Erfolgsmeldung: „Document checking completed. No errors or warnings to show.“ Wenn Fehler gefunden werden, listet der Validator sie dir übersichtlich auf, meist mit Zeilennummer und einer kurzen Erklärung, was falsch ist. Lass dich von einer langen Fehlerliste nicht entmutigen. Oft ist ein einziger Fehler, wie ein nicht geschlossener Tag am Anfang des Dokuments, die Ursache für viele Folgefehler. Korrigiere immer den ersten Fehler in der Liste und validiere erneut.

#### Über Validität hinaus: Konformität und Best Practices

Jetzt kommen wir zu einem wichtigeren, umfassenderen Konzept: der **Konformität**. Ein Dokument kann technisch zu 100 % valide sein, aber trotzdem schlecht. Konformität geht über die reine Syntax hinaus und bezieht die Semantik, die Barrierefreiheit und allgemeine Best Practices mit ein.

Ein konformes Dokument ist nicht nur syntaktisch korrekt, sondern auch:

*   **Semantisch sinnvoll:** Du verwendest HTML-Elemente für ihre eigentliche Bedeutung, nicht nur für ihr Aussehen. Du schreibst `<h1>` für die Hauptüberschrift der Seite, nicht weil der Text dadurch groß und fett wird. Du nutzt `<nav>` für die Hauptnavigation, `<article>` für einen in sich geschlossenen Inhaltsblock und `<footer>` für den Fußbereich. Der Code `<b>Text</b>` und `<strong>Text</strong>` mag optisch identisch aussehen, aber `<strong>` teilt dem Browser und assistiven Technologien (wie Screenreadern) mit, dass dieser Text eine hohe Wichtigkeit hat. Das ist Semantik.
*   **Barrierefrei (Accessible):** Dein Code ist so strukturiert, dass ihn auch Menschen mit Behinderungen nutzen können. Dazu gehört das bereits erwähnte `alt`-Attribut für Bilder, das blinden Nutzern eine Beschreibung des Bildes liefert. Es gehört aber auch die Verwendung korrekter Überschriftenhierarchien, die Kennzeichnung der Dokumentsprache (`<html lang="de">`) und die Gestaltung von Formularen, die per Tastatur bedienbar sind.
*   **Robust:** Dein Code funktioniert auch unter weniger idealen Bedingungen, zum Beispiel wenn JavaScript deaktiviert ist oder das CSS nicht geladen werden kann. Die grundlegende Struktur und der Inhalt bleiben dank solidem HTML zugänglich.

Validität ist also eine notwendige, aber nicht hinreichende Bedingung für ein wirklich gutes HTML-Dokument. Sie ist ein Teil der Konformität. Dein Ziel als professioneller Entwickler sollte es immer sein, konformen Code zu schreiben. Die Validierung ist dabei dein erster und wichtigster Schritt zur Qualitätssicherung. Sie zwingt dich zur Disziplin und Sauberkeit und legt das Fundament, auf dem du eine semantisch reiche, barrierefreie und nutzerfreundliche Web-Erfahrung aufbauen kannst. Betrachte den Validator nicht als lästigen Kritiker, sondern als deinen besten Assistenten auf dem Weg zu exzellentem Code.
