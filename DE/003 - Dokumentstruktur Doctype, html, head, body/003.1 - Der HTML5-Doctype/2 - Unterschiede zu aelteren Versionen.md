# Unterschiede zu älteren Versionen

### Unterschiede zu älteren Versionen

Heute schreibst du ganz selbstverständlich `<!DOCTYPE html>` an den Anfang deines Dokuments und denkst wahrscheinlich nicht weiter darüber nach. Diese kurze, prägnante Zeile ist so einfach, dass man sie sich mühelos merken kann. Doch das war nicht immer so. Ein Blick in die Vergangenheit von HTML offenbart, warum dieser einfache Doctype eine kleine Revolution war und was sich dahinter verbirgt. Um die Genialität des modernen Doctypes zu verstehen, müssen wir eine kleine Zeitreise in die Ära vor HTML5 machen.

#### Die Welt vor HTML5: SGML und die Qual der Wahl

Bevor HTML5 die Webentwicklung vereinfachte, basierte HTML auf einer viel älteren und komplexeren Sprache namens **SGML (Standard Generalized Markup Language)**. SGML ist sozusagen die Mutter vieler Auszeichnungssprachen, und HTML war als eine ihrer „Anwendungen“ definiert. Das bedeutete, dass jeder HTML-Dialekt eine formale Definition brauchte, die seine Regeln, erlaubten Elemente und Attribute festlegte. Diese Definition nannte man **DTD (Document Type Definition)**.

Der Doctype in älteren HTML-Versionen war daher kein einfacher Schalter, sondern ein direkter Verweis auf eine solche DTD. Er teilte dem Browser mit: „Hallo, dieses Dokument folgt den Regeln, die in der folgenden Definitionsdatei festgelegt sind. Bitte interpretiere es entsprechend.“

Schauen wir uns einmal einen typischen Doctype für HTML 4.01 an, einer der am weitesten verbreiteten Versionen vor HTML5:

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```

Auf den ersten Blick wirkt diese Zeile kryptisch und einschüchternd. Lass uns sie Stück für Stück auseinandernehmen, um zu verstehen, was sie bedeutet:

*   `<!DOCTYPE HTML`: Dies deklariert, dass das Wurzelelement des Dokuments `<html>` ist. Das ist der Teil, der dem modernen Doctype noch am ähnlichsten ist.
*   `PUBLIC`: Dieses Schlüsselwort gibt an, dass die folgende DTD öffentlich zugänglich ist.
*   `"-//W3C//DTD HTML 4.01//EN"`: Das ist der sogenannte **Formal Public Identifier (FPI)**. Er ist wie eine eindeutige Seriennummer für die DTD.
    *   `-`: Zeigt an, dass der Name nicht von der ISO (International Organization for Standardization) standardisiert wurde.
    *   `//W3C`: Die Organisation, die die DTD veröffentlicht hat – in diesem Fall das World Wide Web Consortium.
    *   `//DTD HTML 4.01`: Die Art des Dokuments und seine Version.
    *   `//EN`: Die Sprache der DTD, hier Englisch.
*   `"http://www.w3.org/TR/html4/strict.dtd"`: Das ist eine URL, unter der die DTD-Datei tatsächlich zu finden war. Ein Browser oder ein Validierungswerkzeug konnte diese URL aufrufen, um das Regelwerk herunterzuladen und dein Dokument dagegen zu prüfen.

Du siehst also, der alte Doctype war eine sehr formale und maschinenlesbare Deklaration, die tief in den Konventionen von SGML verwurzelt war.

#### Die drei Geschmacksrichtungen: Strict, Transitional und Frameset

Die Komplexität hörte hier aber nicht auf. HTML 4.01 gab es nicht nur in einer Version, sondern gleich in drei verschiedenen „Geschmacksrichtungen“, jede mit ihrem eigenen Doctype:

1.  **Strict (Streng)**:
    ```html
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
    ```
    Die „reine Lehre“ von HTML. Diese DTD erlaubte keine veralteten (engl. *deprecated*) Elemente und Attribute. Insbesondere waren rein präsentationsbezogene Tags wie `<font>` oder Attribute wie `bgcolor` verboten. Die Strict-Version zwang Entwickler dazu, die Trennung von Inhalt (HTML) und Präsentation (CSS) konsequent umzusetzen. In einer idealen Welt hätten alle diese Version genutzt.

2.  **Transitional (Übergang)**:
    ```html
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    ```
    Dies war die pragmatische Version und in der Praxis die am häufigsten verwendete. Sie erlaubte neben den modernen HTML-4-Elementen auch viele der alten, veralteten Tags und Attribute. Der Gedanke dahinter war, Entwicklern den Übergang von älteren, präsentationsorientierten Praktiken zu den neuen, strukturorientierten Standards zu erleichtern. Du konntest also weiterhin ein `<font>`-Tag verwenden, auch wenn es als schlechter Stil galt.

3.  **Frameset (Rahmensatz)**:
    ```html
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
    ```
    Diese spezielle Version wurde für Webseiten verwendet, die Framesets nutzten, um eine Seite in mehrere, voneinander unabhängige Dokumente aufzuteilen. In einem Frameset-Dokument wurde das `<body>`-Element durch ein `<frameset>`-Element ersetzt. Framesets sind heute obsolet und werden aus gutem Grund nicht mehr verwendet, aber damals benötigten sie ihren eigenen Doctype.

#### Der Sonderfall XHTML

Als wäre das nicht schon genug, trat um die Jahrtausendwende **XHTML (Extensible HyperText Markup Language)** auf den Plan. XHTML war im Grunde eine Neuformulierung von HTML als eine strikte Anwendung von **XML (Extensible Markup Language)**. Die Idee war, das Web strenger, sauberer und maschinenlesbarer zu machen.

XHTML brachte seine eigenen, noch längeren Doctypes mit sich. Hier ist ein Beispiel für XHTML 1.0 Strict:

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

XHTML zwang Entwickler zu einer sehr sauberen Schreibweise:
*   Alle Elemente mussten kleingeschrieben werden.
*   Alle Attributwerte mussten in Anführungszeichen stehen.
*   Alle Elemente mussten korrekt geschlossen werden. Leere Elemente wie `<br>` oder `<img>` benötigten einen schließenden Schrägstrich: `<br />`, `<img />`.

Obwohl die Idee hinter XHTML edel war, empfanden viele Entwickler die strikten Regeln und die komplexen Doctypes als Belastung.

#### Der Doctype-Switch: Quirks Mode vs. Standards Mode

Die wichtigste praktische Funktion des Doctypes war jedoch nicht nur die Validierung, sondern der sogenannte **Doctype-Switch**. In den frühen Tagen des Webs interpretierten Browser wie der Internet Explorer 5 oder Netscape 4 HTML und CSS sehr unterschiedlich und oft fehlerhaft. Als neuere Browser versuchten, die offiziellen Webstandards korrekt umzusetzen, standen sie vor einem Problem: Millionen von bestehenden Webseiten waren für die alten, fehlerhaften Browser-Implementierungen gebaut worden und würden in einem modernen, standardkonformen Browser kaputt aussehen.

Die Lösung war genial und pragmatisch zugleich: Browser implementierten zwei verschiedene Darstellungsmodi:

*   **Quirks Mode (Kompatibilitätsmodus)**: Wenn ein Browser auf ein altes oder fehlendes Doctype stieß, schaltete er in diesen Modus. Darin emulierte er das fehlerhafte Verhalten alter Browser, damit alte Webseiten nicht zerbrachen. Das CSS-Box-Modell verhielt sich zum Beispiel anders, und viele Fehler wurden stillschweigend ignoriert.
*   **Standards Mode (Standardmodus)**: Wenn ein Browser einen modernen, vollständigen Doctype (wie einen der oben genannten HTML-4.01- oder XHTML-Doctypes) erkannte, schaltete er in den Standards Mode. In diesem Modus versuchte der Browser, die HTML- und CSS-Spezifikationen so genau wie möglich zu befolgen.

Der Doctype war also der magische Schalter, der dem Browser mitteilte, welchen Darstellungsmodus er verwenden sollte. Die Wahl des richtigen Doctypes war entscheidend für eine konsistente und vorhersagbare Darstellung über verschiedene Browser hinweg.

#### Die HTML5-Revolution: Einfachheit als Ziel

Mit der Entwicklung von HTML5 wurde klar, dass die alte, auf SGML basierende Komplexität ein Hindernis war. HTML5 wurde nicht mehr als SGML-Anwendung definiert. Stattdessen definierten seine Entwickler einen eigenen, präzisen Parsing-Algorithmus, den alle Browser-Hersteller implementieren sollten. Damit wurde die Notwendigkeit, auf eine externe DTD-Datei zu verweisen, überflüssig.

Die Hauptaufgabe des Doctypes änderte sich. Es ging nicht mehr darum, eine spezifische Version von HTML oder ein Regelwerk zu deklarieren. Sein einziger und wichtigster Zweck ist heute: **dem Browser zu signalisieren, dass er die Seite im Standards Mode rendern soll.**

Deshalb konnte der HTML5-Doctype so radikal vereinfacht werden:

```html
<!DOCTYPE html>
```

Diese eine Zeile ist das kürzestmögliche Zeichen-Muster, das zuverlässig in allen Browsern den Standards Mode auslöst. Sie ist absichtlich kurz, leicht zu merken und frei von Versionsnummern. Die Idee ist, dass dieser Doctype für alle zukünftigen Versionen von HTML gültig bleiben wird. HTML ist nun ein „lebendiger Standard“, der sich kontinuierlich weiterentwickelt, ohne harte Brüche wie von Version 4 zu 5.

Zusammenfassend lässt sich sagen: Während die alten Doctypes komplexe Verweise auf spezifische Regelwerke waren, die zwischen verschiedenen Modi und Versionen unterschieden, ist der HTML5-Doctype ein einfacher, universeller Schalter. Er befreit dich von der Last der Vergangenheit und sorgt mit minimalem Aufwand dafür, dass dein Code von modernen Browsern auf die bestmögliche und standardkonforme Weise interpretiert wird.
