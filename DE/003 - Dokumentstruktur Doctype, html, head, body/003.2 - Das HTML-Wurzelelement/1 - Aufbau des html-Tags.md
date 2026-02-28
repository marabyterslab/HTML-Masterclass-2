# Aufbau des html-Tags

### Der Grundstein deiner Webseite: Das `<html>`-Element

Stell dir jede Webseite, die du baust, wie einen Baum vor. Sie hat Wurzeln, einen Stamm, Äste und Blätter. In der Welt von HTML ist das `<html>`-Element der Stamm dieses Baumes. Es ist das allererste und grundlegendste Element, das alles andere umschließt. Man nennt es deshalb auch das **Wurzelelement** (Root Element), denn in ihm wurzelt die gesamte Struktur deines Dokuments. Jedes andere HTML-Tag, das du schreibst, muss sich innerhalb dieses einen `<html>`-Tags befinden.

Wenn ein Browser deine HTML-Datei öffnet, sucht er als Erstes nach diesem Tag. Es signalisiert ihm: „Achtung, hier beginnt ein HTML-Dokument. Alles, was nun folgt, gehört zu dieser Webseite.“ Ohne dieses Wurzelelement wüsste der Browser nicht, wie er den Inhalt interpretieren soll.

Die grundlegendste Struktur sieht so aus:

```html
<html>
  <!-- Alle anderen Elemente kommen hier hinein -->
</html>
```

Dieser einfache Aufbau ist jedoch noch nicht vollständig. Der Stamm eines Baumes teilt sich in der Regel in große Hauptäste auf. Genauso hat auch das `<html>`-Element genau zwei direkte „Kinder“, die immer vorhanden sein müssen.

#### Die unzertrennlichen Geschwister: `<head>` und `<body>`

Innerhalb des `<html>`-Elements gibt es eine klare Trennung von Aufgaben. Diese Trennung wird durch zwei weitere wichtige Tags erreicht: den `<head>`-Tag (Kopf) und den `<body>`-Tag (Körper). Du kannst dir das wie bei einem Lebewesen vorstellen: Der Kopf enthält das Gehirn und steuert alles im Hintergrund, während der Körper das ist, was man von außen sieht und womit man interagiert.

1.  **Der `<head>`-Bereich: Die Schaltzentrale im Verborgenen**

    Der `<head>` ist der erste direkte Nachkomme des `<html>`-Tags. Er enthält alle Metadaten und Informationen *über* deine Webseite, die für den Browser, Suchmaschinen oder andere Computersysteme wichtig sind, aber nicht direkt auf der Seite sichtbar dargestellt werden. Man könnte ihn als das Gehirn oder die Steuerzentrale deiner Webseite bezeichnen.

    Hier platzierst du unter anderem:
    *   Den Titel deiner Webseite, der in der Registerkarte (Tab) des Browsers angezeigt wird (`<title>`).
    *   Informationen über den Zeichensatz, damit Umlaute und Sonderzeichen korrekt dargestellt werden (`<meta charset="UTF-8">`).
    *   Verknüpfungen zu externen CSS-Dateien, um deine Seite zu gestalten (`<link>`).
    *   Metadaten für Suchmaschinen, wie eine Beschreibung der Seite oder Schlüsselwörter (`<meta>`).
    *   Verknüpfungen zu JavaScript-Dateien, die das Verhalten deiner Seite steuern (`<script>`).

    Der Inhalt des `<head>`-Bereichs ist also essenziell für die Funktionalität und das Erscheinungsbild der Seite, bleibt für den Besucher aber unsichtbar – mit Ausnahme des Titels im Browser-Tab.

2.  **Der `<body>`-Bereich: Die sichtbare Bühne**

    Direkt nach dem schließenden `</head>`-Tag folgt der `<body>`-Tag. Er ist der zweite und letzte direkte Nachkomme des `<html>`-Elements. Hier kommt alles hinein, was der Besucher deiner Webseite tatsächlich im Browserfenster sehen und womit er interagieren soll.

    Das umfasst den gesamten sichtbaren Inhalt:
    *   Überschriften (`<h1>`, `<h2>`, etc.)
    *   Textabsätze (`<p>`)
    *   Bilder (`<img>`)
    *   Links (`<a>`)
    *   Listen (`<ul>`, `<ol>`)
    *   Tabellen (`<table>`)
    *   Formulare (`<form>`)
    *   Und alle anderen inhaltlichen Elemente.

Zusammen ergibt sich also folgende Grundstruktur:

```html
<html>
  <head>
    <!-- Metadaten und Verknüpfungen (unsichtbar) -->
  </head>
  <body>
    <!-- Der gesamte sichtbare Inhalt der Webseite -->
  </body>
</html>
```

Diese Zweiteilung ist fundamental. Es gibt keine Ausnahmen von dieser Regel: Jedes `<html>`-Element muss genau einen `<head>` und genau einen `<body>` als direkte Kinder enthalten.

#### Attribute: Die Eigenschaften des Wurzelelements

Wie die meisten HTML-Elemente kann auch das `<html>`-Tag zusätzliche Informationen in Form von Attributen erhalten. Attribute sind kleine Anweisungen oder Beschreibungen, die direkt im öffnenden Tag platziert werden und das Verhalten oder die Bedeutung des Elements näher definieren. Für das `<html>`-Tag gibt es ein besonders wichtiges Attribut, das du niemals vergessen solltest: das `lang`-Attribut.

**Das `lang`-Attribut: Die Sprache des Inhalts**

Das `lang`-Attribut gibt die primäre Sprache des Inhalts deiner Webseite an. Das ist eine winzige, aber unglaublich wertvolle Information für Maschinen.

```html
<html lang="de">
```

Dieses Beispiel teilt dem Browser und anderen Systemen mit, dass der Hauptinhalt dieser Seite auf Deutsch verfasst ist. Warum ist das so wichtig?

*   **Barrierefreiheit:** Screenreader, die blinden oder sehbehinderten Menschen Webseiten vorlesen, können durch diese Angabe die richtige Sprachausgabe mit der korrekten Aussprache und Betonung wählen. Ein deutscher Text, der mit englischer Aussprache vorgelesen wird, ist kaum verständlich.
*   **Suchmaschinenoptimierung (SEO):** Suchmaschinen wie Google nutzen diese Information, um deine Seite korrekt zu kategorisieren und sie Nutzern anzuzeigen, die nach Inhalten in dieser Sprache suchen. Eine Seite mit `lang="de"` wird bei deutschen Suchanfragen höher gewichtet.
*   **Browser-Funktionen:** Moderne Browser können diese Angabe nutzen, um automatische Übersetzungsfunktionen anzubieten oder die Rechtschreibprüfung in Formularfeldern auf die richtige Sprache einzustellen.

Du solltest immer den zweibuchstabigen ISO-639-1-Code für die Sprache verwenden (z. B. `de` für Deutsch, `en` für Englisch, `fr` für Französisch). Bei Bedarf kannst du auch eine Region hinzufügen, um Dialekte oder regionale Unterschiede zu spezifizieren, wie `en-US` für amerikanisches Englisch oder `de-AT` für österreichisches Deutsch.

**Das `dir`-Attribut: Die Schreibrichtung**

Ein weiteres, wenn auch seltener genutztes Attribut ist `dir`, das die Schreibrichtung des Textes festlegt. In den meisten westlichen Sprachen ist dies nicht notwendig, da die Standardeinstellung `ltr` (left-to-right, also von links nach rechts) ist. Für Sprachen wie Arabisch, Hebräisch oder Farsi, die von rechts nach links geschrieben werden, ist dieses Attribut jedoch unerlässlich.

```html
<html lang="ar" dir="rtl">
```

Hier wird festgelegt, dass die Seite auf Arabisch ist (`ar`) und die Schreibrichtung `rtl` (right-to-left) verwendet.

#### Das Gesamtbild: Eine minimale, gültige HTML-Struktur

Wenn wir nun alle Teile zusammensetzen, erhalten wir die kleinste, aber vollständig korrekte Struktur eines HTML5-Dokuments. Bevor das `<html>`-Tag beginnt, muss allerdings noch eine allererste Zeile stehen: der **Doctype**.

`<!DOCTYPE html>`

Diese Zeile ist technisch gesehen kein HTML-Tag, sondern eine Deklaration oder eine Anweisung an den Browser. Sie teilt ihm mit: „Dieses Dokument ist ein HTML5-Dokument. Bitte interpretiere es nach den modernen Webstandards.“ Ohne diese Deklaration könnten Browser in einen alten Kompatibilitätsmodus (den sogenannten „Quirks Mode“) verfallen, was zu unerwarteten Darstellungsfehlern führen kann.

Eine vollständige und minimale HTML-Datei sieht also so aus:

```html
<!DOCTYPE html>
<html lang="de">
  <head>
    <meta charset="UTF-8">
    <title>Meine erste Webseite</title>
  </head>
  <body>
    <h1>Hallo Welt!</h1>
    <p>Dies ist der sichtbare Inhalt meiner Webseite.</p>
  </body>
</html>
```

In diesem Code siehst du das perfekte Zusammenspiel:
1.  Der `DOCTYPE` legt den Dokumenttyp fest.
2.  Das `<html>`-Element mit dem `lang`-Attribut umhüllt alles als Wurzelelement.
3.  Der `<head>`-Bereich enthält unsichtbare, aber wichtige Metadaten wie den Zeichensatz und den Titel.
4.  Der `<body>`-Bereich enthält den gesamten sichtbaren Inhalt, der dem Benutzer angezeigt wird.

Dieses Grundgerüst ist die Ausgangsbasis für jede Webseite, die du jemals erstellen wirst. Es ist die stabile und logische Struktur, auf der alle weiteren Inhalte, Designs und Funktionen aufbauen.
