# Das lang-Attribut im html-Tag

### Die Sprache des Dokuments: Das `lang`-Attribut im `<html>`-Tag

Wenn du eine Webseite erstellst, kommunizierst du nicht nur mit den Menschen, die sie besuchen, sondern auch mit den Maschinen, die sie verarbeiten. Browser, Suchmaschinen, Screenreader und andere assistierende Technologien müssen den Inhalt deiner Seite verstehen, um ihn korrekt darstellen, indexieren und vorlesen zu können. Eine der fundamentalsten Informationen, die du ihnen geben kannst, ist die primäre Sprache, in der dein Dokument verfasst ist. Genau hier kommt das `lang`-Attribut ins Spiel.

#### Was ist das `lang`-Attribut und wo gehört es hin?

Das `lang`-Attribut ist ein globales Attribut in HTML, was bedeutet, dass es theoretisch auf jedem Element platziert werden kann. Seine wichtigste und primäre Position ist jedoch direkt im öffnenden `<html>`-Tag. Wenn du es dort setzt, deklarierst du die Hauptsprache für das gesamte HTML-Dokument.

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Ein deutsches Dokument</title>
</head>
<body>
  <p>Dieser gesamte Inhalt wird als deutschsprachig interpretiert.</p>
</body>
</html>
```

Indem du `lang="de"` im `<html>`-Tag angibst, teilst du allen verarbeitenden Systemen mit: "Der Standardinhalt auf dieser Seite ist Deutsch." Diese eine Zeile Code hat weitreichende und wichtige Auswirkungen, die weit über eine reine Formsache hinausgehen.

#### Warum diese Angabe so entscheidend ist

Vielleicht denkst du, dass es doch offensichtlich ist, in welcher Sprache eine Seite geschrieben ist. Für einen Menschen, der die Sprache beherrscht, stimmt das auch. Für eine Software ist es jedoch eine komplexe Aufgabe, eine Sprache ohne explizite Angabe zu erraten. Die Deklaration über das `lang`-Attribut schafft Eindeutigkeit und aktiviert eine ganze Reihe nützlicher Funktionen.

**1. Barrierefreiheit und Screenreader**

Dies ist wohl der wichtigste Grund. Menschen mit Sehbehinderungen nutzen Screenreader, um sich Webseiten vorlesen zu lassen. Diese Software-Tools verwenden Sprachsynthese-Engines, um Text in gesprochene Worte umzuwandeln. Die korrekte Aussprache hängt aber massiv von der Sprache ab.

Stell dir das englische Wort "eleven" vor. Ein deutscher Screenreader würde es vielleicht als "e-le-fen" aussprechen. Wenn die Seite jedoch korrekt mit `lang="en"` deklariert ist, weiß der Screenreader, dass er die englische Sprachsynthese verwenden muss, und spricht es korrekt als /ɪˈlɛvən/ aus. Das Gleiche gilt für deutsche Wörter wie "Eichhörnchen" oder "Fahrvergnügen", die für eine englische Sprachausgabe eine unüberwindbare Hürde wären. Die richtige `lang`-Angabe ist also keine Option, sondern eine Grundvoraussetzung für eine barrierefreie Webseite.

**2. Suchmaschinenoptimierung (SEO)**

Suchmaschinen wie Google oder Bing möchten ihren Nutzern die relevantesten Ergebnisse liefern. Dazu gehört auch die Sprache. Wenn jemand in Deutschland auf Deutsch nach "Rezept für Apfelstrudel" sucht, möchte er deutsche Rezepte finden, keine englischen oder spanischen.

Das `lang`-Attribut ist ein starkes Signal für Suchmaschinen, um den Inhalt geografisch und sprachlich zuzuordnen. Eine Seite mit `lang="de"` wird mit höherer Wahrscheinlichkeit an Nutzer im deutschsprachigen Raum ausgespielt, die auf Deutsch suchen. Du hilfst der Suchmaschine also, deine Zielgruppe besser zu erreichen.

**3. Browser-Funktionalität**

Auch moderne Webbrowser nutzen diese Information für verschiedene Zwecke:
*   **Rechtschreibprüfung:** Wenn du Formularfelder wie `<textarea>` anbietest, kann der Browser die Rechtschreibprüfung in der korrekten Sprache aktivieren.
*   **Silbentrennung:** Mit der CSS-Eigenschaft `hyphens: auto;` kann der Browser Wörter am Zeilenende automatisch trennen. Die Regeln für die Silbentrennung sind jedoch von Sprache zu Sprache völlig unterschiedlich. Ohne `lang`-Attribut funktioniert die automatische Silbentrennung oft gar nicht oder falsch.
*   **Übersetzungs-Tools:** Browser bieten oft an, eine Seite automatisch zu übersetzen, wenn sie erkennen, dass die Seitensprache (deklariert durch `lang`) nicht der bevorzugten Sprache des Nutzers entspricht. Fehlt das Attribut, kann diese Funktion unzuverlässig sein.
*   **Typografie:** Bestimmte Sprachen haben spezifische typografische Regeln, zum Beispiel bei Anführungszeichen. Mit CSS und dem `:lang()`-Selektor kannst du unterschiedliche Stile für verschiedene Sprachen definieren.

#### Die richtigen Sprachcodes verwenden

Der Wert des `lang`-Attributs ist kein willkürlicher Text. Er folgt einem standardisierten Format, das in der Regel auf dem **ISO 639-1**-Standard für Sprachcodes basiert. Dies sind zweibuchstabige Kürzel, die eine Sprache eindeutig identifizieren.

Hier sind einige gängige Beispiele:
*   `de`: Deutsch
*   `en`: Englisch
*   `es`: Spanisch
*   `fr`: Französisch
*   `it`: Italienisch
*   `ja`: Japanisch
*   `zh`: Chinesisch

Du solltest immer den primären Sprachcode verwenden.

**Regionale Varianten und Dialekte**

Manchmal reicht der zweibuchstabige Code nicht aus, weil du eine spezifische regionale Variante der Sprache meinst. Zum Beispiel unterscheidet sich britisches Englisch von amerikanischem Englisch in der Schreibweise, im Vokabular und in manchen Redewendungen. In solchen Fällen kannst du einen Ländercode nach **ISO 3166-1** anhängen.

Das Format lautet dann `sprache-REGION`.
*   `en-GB`: Britisches Englisch (Great Britain)
*   `en-US`: Amerikanisches Englisch (United States)
*   `de-AT`: Österreichisches Deutsch (Austria)
*   `de-CH`: Schweizer Hochdeutsch (Confoederatio Helvetica)
*   `fr-CA`: Kanadisches Französisch (Canada)

Die Faustregel lautet: Sei so spezifisch wie nötig, aber so allgemein wie möglich. Wenn dein Inhalt für alle Deutschsprachigen gleichermaßen verständlich ist, ist `lang="de"` die beste Wahl. Schreibst du jedoch einen juristischen Fachtext, der sich explizit auf österreichische Gesetze bezieht, wäre `lang="de-AT"` präziser und damit die bessere Angabe.

#### Umgang mit mehreren Sprachen auf einer Seite

Was tust du, wenn deine Seite hauptsächlich auf Deutsch ist, aber ein Zitat oder einen Absatz in einer anderen Sprache enthält? Da `lang` ein globales Attribut ist, kannst du es auch auf jedes andere HTML-Element anwenden, um die Sprache für diesen spezifischen Teil des Inhalts zu überschreiben.

Stell dir vor, du schreibst einen Blogartikel über ein englisches Sprichwort:

```html
<html lang="de">
<head>
  <title>Englische Sprichwörter</title>
</head>
<body>
  <h1>Die Bedeutung von Sprichwörtern</h1>
  <p>Ein bekanntes englisches Sprichwort lautet:
    <q lang="en">An apple a day keeps the doctor away.</q>
    Dieses Zitat wird oft verwendet, um die Wichtigkeit einer gesunden Ernährung zu betonen.
  </p>
</body>
</html>
```

In diesem Beispiel ist das gesamte Dokument als deutsch (`lang="de"`) deklariert. Das `<q>`-Element (für kurze Zitate) erhält jedoch das Attribut `lang="en"`. Damit signalisierst du: "Achtung, nur dieser kleine Teil hier ist auf Englisch." Ein Screenreader wird an dieser Stelle nahtlos zur englischen Sprachausgabe wechseln, um das Zitat korrekt vorzulesen, und danach wieder zurück ins Deutsche schalten. Auch eine automatische Rechtschreibprüfung würde diesen Satz nach englischen Regeln prüfen.

#### Ein häufiges Missverständnis: `lang` vs. `xml:lang`

Vielleicht stößt du in älteren Tutorials oder im Kontext von XHTML auf das Attribut `xml:lang`. XHTML war eine strengere, auf XML basierende Version von HTML. In XML-Dokumenten wird `xml:lang` zur Sprachdeklaration verwendet.

Für modernes HTML5 gilt folgende einfache Regel: **Verwende immer das `lang`-Attribut.** Es ist der korrekte Standard.

Wenn du aus Gründen der Rückwärtskompatibilität eine Seite schreiben musst, die auch von alten XML-Parsern verarbeitet werden soll (ein seltener Anwendungsfall, bekannt als "Polyglot Markup"), kannst du beide Attribute angeben. Der Wert muss dabei identisch sein.

```html
<!-- Nur für Polyglot-Markup, nicht für Standard-HTML5 nötig -->
<html lang="de" xml:lang="de">
  ...
</html>
```

Für die allermeisten Webprojekte, die du heute startest, ist die alleinige Verwendung von `lang` vollkommen ausreichend und korrekt.

Das Setzen des `lang`-Attributs ist eine kleine, einfache Handlung mit enormer Wirkung. Es ist ein Eckpfeiler für eine zugängliche, suchmaschinenfreundliche und technisch saubere Webseite. Mach es dir zur Gewohnheit, es in jedem deiner HTML-Dokumente als eine der ersten Amtshandlungen im `<html>`-Tag zu deklarieren. Deine Nutzer – und die Maschinen – werden es dir danken.
