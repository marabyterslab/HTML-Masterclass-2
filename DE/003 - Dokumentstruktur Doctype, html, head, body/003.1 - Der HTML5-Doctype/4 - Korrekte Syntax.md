# Korrekte Syntax

### Korrekte Syntax: Der HTML5-Doctype als Fundament

Stell dir vor, du beginnst ein Gespräch mit jemandem, der mehrere Sprachen fließend spricht. Bevor du loslegst, ist es hilfreich, kurz zu klären, in welcher Sprache ihr euch unterhalten werdet. Das vermeidet Missverständnisse und sorgt dafür, dass deine Botschaft genau so ankommt, wie du sie meinst. Genau diese Funktion erfüllt die erste Zeile in jedem modernen HTML-Dokument: die Doctype-Deklaration.

Die allererste Zeile deines HTML-Dokuments ist eine Verabredung mit dem Browser. Sie lautet schlicht und einfach:

```html
<!DOCTYPE html>
```

Diese eine Zeile ist das Fundament, auf dem deine gesamte Webseite aufgebaut ist. Bevor wir uns ansehen, wie der Rest der Grundstruktur aussieht, ist es entscheidend, dass du verstehst, was diese Deklaration tut und warum sie absolut unverzichtbar ist.

#### Was der Doctype ist (und was er nicht ist)

Auf den ersten Blick könnte man meinen, `<!DOCTYPE html>` sei ein HTML-Tag, ähnlich wie `<p>` oder `<h1>`. Das ist jedoch nicht der Fall. Du wirst feststellen, dass es keinen schließenden Tag wie `</!DOCTYPE>` gibt.

Die Doctype-Deklaration ist eine **Anweisung** (oder eine Instruktion) für den Webbrowser. Sie teilt ihm mit, nach welchen Regeln er das nachfolgende Dokument interpretieren und darstellen soll. Mit `<!DOCTYPE html>` sagst du unmissverständlich: "Hallo Browser, was jetzt kommt, ist ein HTML5-Dokument. Bitte nutze dein modernstes Regelwerk, um diese Seite zu rendern."

Diese Anweisung muss immer ganz am Anfang stehen. Keine Leerzeichen, keine Kommentare, absolut nichts darf davor kommen.

#### Die entscheidende Rolle: Standards-Modus vs. Quirks-Modus

Warum ist diese Anweisung so wichtig? Um das zu verstehen, müssen wir eine kleine Zeitreise in die turbulenten Anfänge des Webs machen. In den späten 90er-Jahren, während der sogenannten "Browserkriege", kochte jeder Browserhersteller sein eigenes Süppchen. Es gab kaum einheitliche Standards, und Webentwickler mussten unzählige Tricks anwenden, damit ihre Seiten im Netscape Navigator auch nur annähernd so aussahen wie im Internet Explorer.

Um die Kompatibilität mit alten, fehlerhaft geschriebenen Webseiten zu wahren, entwickelten die Browser einen speziellen Modus: den **Quirks-Modus** (von englisch *quirk*, die Eigenart, die Marotte). Wenn ein Browser auf ein HTML-Dokument ohne oder mit einer veralteten Doctype-Deklaration stößt, schaltet er in diesen Kompatibilitätsmodus. Er versucht dann, das Dokument so zu rendern, wie es ein Browser aus dem Jahr 1998 getan hätte. Das Resultat? Chaos. CSS-Box-Modelle verhalten sich falsch, Layouts brechen zusammen und das Verhalten von Elementen wird unvorhersehbar und inkonsistent zwischen verschiedenen Browsern. Der Quirks-Modus ist ein Relikt, das du unter allen Umständen vermeiden möchtest.

Der Gegenpol dazu ist der **Standards-Modus** (oder "Strict Mode"). Diesen Modus aktiviert der Browser, wenn er eine saubere und moderne Doctype-Deklaration wie `<!DOCTYPE html>` findet. Im Standards-Modus hält sich der Browser strikt an die aktuellen Webstandards von Organisationen wie dem W3C und der WHATWG. Das sorgt für ein vorhersagbares, konsistentes und zuverlässiges Rendering über alle modernen Browser hinweg – von Chrome über Firefox und Safari bis hin zu Edge.

Deine wichtigste Aufgabe als Entwickler ist es also, mit der Doctype-Deklaration sicherzustellen, dass der Browser immer den Standards-Modus verwendet. Der einfache HTML5-Doctype ist der goldene Schlüssel dafür.

#### Ein kurzer Blick zurück: Die komplizierte Vergangenheit

Vielleicht fragst du dich, warum dieser simple Doctype eine so große Sache ist. Der Grund ist, dass es früher deutlich komplizierter war. Vor HTML5 basierten die Doctypes auf sogenannten DTDs (Document Type Definitions), was zu langen und kryptischen Deklarationen führte.

Hier nur zwei Beispiele, damit du den Unterschied siehst:

**HTML 4.01 Strict Doctype:**
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```

**XHTML 1.0 Transitional Doctype:**
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```

Diese Ungetüme waren nicht nur schwer zu merken und fehleranfällig bei der Eingabe, sondern sie zwangen den Browser auch, eine externe Definitionsdatei (die DTD) zu referenzieren.

Die Einführung von HTML5 war hier eine Revolution der Einfachheit. Der neue Doctype `<!DOCTYPE html>` ist nicht mehr an eine DTD gebunden. Seine einzige Aufgabe ist es, den Standards-Modus auszulösen. Er ist kurz, prägnant und leicht zu merken.

#### Die minimale, korrekte Grundstruktur

Nachdem du nun die Bedeutung des Doctypes verstanden hast, können wir die restliche Grundstruktur eines jeden HTML5-Dokuments aufbauen. Eine syntaktisch korrekte und vollständige HTML-Datei benötigt neben dem Doctype noch einige weitere wesentliche Elemente.

Hier ist das absolute Minimum, das jede deiner HTML-Dateien enthalten sollte:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Titel der Seite</title>
</head>
<body>
    <!-- Hier kommt dein sichtbarer Inhalt hin -->
</body>
</html>
```

Lass uns diese Struktur Zeile für Zeile durchgehen, um ihre syntaktische Rolle zu verstehen:

1.  `<!DOCTYPE html>`
    Wie besprochen, die essenzielle Anweisung an den Browser. Sie steht immer an erster Stelle.

2.  `<html lang="de">`
    Dies ist das Wurzelelement (*root element*), das alle anderen HTML-Elemente umschließt. Das Attribut `lang="de"` ist von großer Bedeutung. Es deklariert die Hauptsprache des Dokuments als Deutsch. Dies ist wichtig für:
    *   **Suchmaschinen (SEO):** Sie können den Inhalt besser kategorisieren und den richtigen Zielgruppen anzeigen.
    *   **Barrierefreiheit (Accessibility):** Screenreader für sehbehinderte Nutzer wissen dadurch, in welcher Sprache sie den Text vorlesen sollen, was die Aussprache und Betonung korrekt macht.
    *   **Browser-Funktionen:** Rechtschreibprüfungen oder Übersetzungstools funktionieren zuverlässiger.
    Du solltest dieses Attribut immer an die primäre Sprache deines Inhalts anpassen (z. B. `lang="en"` für Englisch).

3.  `<head>`
    Der Kopf des Dokuments. Der Inhalt des `<head>`-Elements wird nicht direkt auf der Webseite angezeigt (mit Ausnahme des `<title>`). Er enthält Metadaten – also Informationen *über* das Dokument. Dazu gehören der Zeichensatz, der Titel, Verknüpfungen zu CSS-Dateien und vieles mehr.

4.  `<meta charset="UTF-8">`
    Diese Meta-Information ist fast genauso wichtig wie der Doctype. Sie legt die Zeichenkodierung für das Dokument fest. `UTF-8` ist der universelle Standard, der praktisch alle Zeichen und Symbole aller Sprachen der Welt abdeckt. Ohne diese Angabe kann es passieren, dass Sonderzeichen wie Umlaute (ä, ö, ü) oder das Eszett (ß) im Browser falsch als seltsame Symbole (z.B. `�`) dargestellt werden. Diese Zeile sollte immer eine der ersten im `<head>` sein.

5.  `<title>Titel der Seite</title>`
    Der Inhalt dieses Tags ist der Text, der im Tab des Browsers, in Lesezeichen oder in den Ergebnissen von Suchmaschinen angezeigt wird. Jedes HTML-Dokument muss ein `<title>`-Element im `<head>` haben. Es ist nicht nur für die Benutzerfreundlichkeit, sondern auch für die Suchmaschinenoptimierung von zentraler Bedeutung.

6.  `<body>`
    Hier kommt alles hinein, was der Besucher deiner Webseite tatsächlich sehen und womit er interagieren soll: Texte, Überschriften, Bilder, Videos, Links, Formulare und so weiter. Der `<body>`-Tag enthält den gesamten sichtbaren Inhalt deines Dokuments.

#### Häufige Fehler und wie du sie vermeidest

Die Einhaltung der korrekten Grundsyntax ist der erste Schritt zu professionellem und fehlerfreiem Code. Hier sind einige typische Fehler, auf die du achten solltest:

*   **Etwas vor dem Doctype:** Schon ein einziges Leerzeichen oder ein HTML-Kommentar vor `<!DOCTYPE html>` kann manche Browser in den Quirks-Modus zwingen. Die erste Spalte der ersten Zeile muss mit `<` beginnen.
*   **Falsche Schreibweise des Doctypes:** Obwohl Browser oft tolerant sind, ist die offizielle und korrekte Schreibweise `<!DOCTYPE html>`. Halte dich an diese Konvention. `DOCTYPE` wird in der Regel großgeschrieben, um es von den Tags zu unterscheiden.
*   **Vergessene Metadaten:** Oft werden das `lang`-Attribut im `<html>`-Tag oder das `<meta charset="UTF-8">`-Tag vergessen. Diese kleinen Details haben jedoch große Auswirkungen auf die Zugänglichkeit und korrekte Darstellung deiner Seite.
*   **Sichtbarer Inhalt im `<head>`:** Der `<head>`-Bereich ist ausschließlich für Metadaten gedacht. Jeglicher Inhalt, der auf der Seite erscheinen soll, gehört in den `<body>`.

Indem du dir von Anfang an angewöhnst, jedes Projekt mit dieser sauberen und syntaktisch korrekten Grundstruktur zu beginnen, legst du ein stabiles Fundament. Du stellst sicher, dass Browser deine Absichten richtig verstehen und deine Webseite so darstellen, wie du es geplant hast – zuverlässig und über alle Plattformen hinweg.
