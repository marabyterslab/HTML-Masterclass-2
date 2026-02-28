# Aufbau des html-Tags

### Das `<html>`-Tag: Die Wurzel deines Dokuments

Stell dir eine Webseite wie ein Haus vor. Bevor du Wände einziehst, ein Dach deckst oder Räume einrichtest, brauchst du ein Fundament und das Grundstück, auf dem alles steht. In der Welt von HTML ist das `<html>`-Tag genau das: das alles umschließende Wurzelelement. Es ist der absolute Anfang und das absolute Ende deines gesamten HTML-Codes. Jedes andere Tag, jeder Text und jedes Bild, das du auf deiner Seite platzierst, muss sich innerhalb dieses einen, großen Containers befinden.

Direkt nach der Dokumenttyp-Deklaration (`<!DOCTYPE html>`) ist das `<html>`-Tag das erste Element, das du schreibst. Es signalisiert dem Browser unmissverständlich: "Achtung, ab hier beginnt ein HTML-Dokument."

#### Die grundlegende Struktur

In seiner einfachsten Form umschließt das `<html>`-Tag zwei direkte Kinderelemente: den `<head>`- und den `<body>`-Bereich. Diese Aufteilung ist fundamental und logisch:

1.  **`<head>` (Der Kopf):** Hier platzierst du alle Metadaten und Informationen *über* das Dokument, die für den Besucher nicht direkt sichtbar sind. Dazu gehören der Titel der Seite, der im Browser-Tab erscheint, Verknüpfungen zu CSS-Dateien für das Styling, Informationen für Suchmaschinen und die Zeichenkodierung.
2.  **`<body>` (Der Körper):** Dieser Bereich enthält alles, was der Benutzer im Browserfenster tatsächlich sieht und womit er interagiert. Überschriften, Absätze, Bilder, Links, Videos – der gesamte sichtbare Inhalt deiner Webseite gehört hier hinein.

Ein minimales, aber vollständiges HTML-Gerüst sieht also immer so aus:

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Metadaten und Informationen über das Dokument -->
  </head>
  <body>
    <!-- Der sichtbare Inhalt der Webseite -->
  </body>
</html>
```

Es gibt keine Ausnahmen von dieser Regel. Du kannst niemals ein `<p>`-Tag oder ein `<img>`-Tag direkt in das `<html>`-Tag schreiben. Sie gehören immer in den `<body>`. Ebenso gehört ein `<title>`-Tag immer in den `<head>`. Das `<html>`-Element fungiert als ordnender Rahmen für diese beiden Hauptbereiche.

#### Das wichtigste Attribut: `lang`

Obwohl das `<html>`-Tag auch ohne Attribute funktioniert, gibt es eines, das du praktisch immer verwenden solltest: das `lang`-Attribut. Es gibt die primäre Sprache des Dokumenteninhalts an.

```html
<!DOCTYPE html>
<html lang="de">
  <head>
    ...
  </head>
  <body>
    ...
  </body>
</html>
```

Warum ist das so wichtig? Aus mehreren Gründen, die weit über reine Formsache hinausgehen:

*   **Barrierefreiheit (Accessibility):** Screenreader, also Programme, die blinden oder sehbehinderten Menschen Webseiten vorlesen, nutzen das `lang`-Attribut, um die richtige Aussprache und Betonung zu wählen. Ein deutscher Text, der mit englischer Aussprache vorgelesen wird, ist kaum verständlich. Mit `lang="de"` stellst du sicher, dass die Sprachausgabe korrekt funktioniert.
*   **Suchmaschinenoptimierung (SEO):** Suchmaschinen wie Google verwenden diese Information, um den Inhalt korrekt zu klassifizieren und ihn Nutzern anzuzeigen, die nach Inhalten in dieser spezifischen Sprache suchen. Eine Seite mit `lang="de"` hat eine höhere Chance, bei deutschen Suchanfragen gut platziert zu werden.
*   **Browser-Funktionen:** Moderne Browser können das `lang`-Attribut nutzen, um kontextbezogene Funktionen anzubieten. Dazu gehören automatische Übersetzungsangebote ("Möchten Sie diese Seite übersetzen?"), die korrekte Silbentrennung oder die Auswahl des passenden Wörterbuchs für die Rechtschreibprüfung in Formularfeldern.

Die Werte für das `lang`-Attribut sind standardisierte Sprachcodes nach ISO 639-1. Einige gängige Beispiele sind:

*   `de` für Deutsch
*   `en` für Englisch
*   `fr` für Französisch
*   `es` für Spanisch

Du kannst auch regionale Varianten angeben, indem du einen Ländercode anhängst. `en-US` steht beispielsweise für amerikanisches Englisch, während `en-GB` für britisches Englisch steht. Für Deutsch könntest du `de-AT` für Österreich oder `de-CH` für die Schweiz verwenden, falls dein Inhalt spezifische regionale Eigenheiten aufweist. In den meisten Fällen genügt jedoch der einfache Sprachcode wie `de` oder `en`.

#### Weitere Attribute: `dir` und `xmlns`

Neben `lang` gibt es noch weitere Attribute, die du am `<html>`-Tag antreffen könntest, auch wenn sie seltener benötigt werden.

##### Das `dir`-Attribut

Das `dir`-Attribut (für "direction", Richtung) legt die Schreibrichtung des Textes fest. Für die meisten Sprachen, die du kennst, ist dies `ltr` (left-to-right, von links nach rechts). Da dies der Standardwert ist, musst du ihn normalerweise nicht explizit angeben.

Interessant wird es bei Sprachen, die von rechts nach links geschrieben werden, wie Arabisch, Hebräisch oder Persisch. Für eine solche Seite würdest du das Attribut `dir="rtl"` (right-to-left) setzen.

```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
  <head>
    <title>صفحة باللغة العربية</title>
  </head>
  <body>
    <h1>مرحبا بالعالم</h1>
  </body>
</html>
```

Durch das Setzen von `dir="rtl"` am Wurzelelement stellt der Browser sicher, dass die gesamte Layout-Logik von rechts nach links ausgerichtet wird, was für diese Sprachen entscheidend ist.

##### Ein Blick in die Vergangenheit: Das `xmlns`-Attribut

Wenn du dir älteren Code oder Code ansiehst, der für XHTML (eine strengere, auf XML basierende Variante von HTML) geschrieben wurde, könntest du auf das `xmlns`-Attribut stoßen:

```html
<!-- Beispiel aus XHTML, NICHT notwendig für HTML5 -->
<html xmlns="http://www.w3.org/1999/xhtml" lang="de">
  ...
</html>
```

`xmlns` steht für "XML Namespace". In der Welt von XML dient es dazu, eindeutig zu deklarieren, zu welchem "Vokabular" die verwendeten Tags gehören. Für XHTML war dies zwingend erforderlich.

**In modernem HTML5 ist das `xmlns`-Attribut überflüssig und hat keine Funktion mehr.** Die Dokumenttyp-Deklaration `<!DOCTYPE html>` genügt, um dem Browser mitzuteilen, dass er es mit HTML zu tun hat. Du kannst es also getrost weglassen. Es zu kennen hilft dir aber, Code von älteren Webseiten zu verstehen.

#### Das perfekte Grundgerüst

Zusammenfassend lässt sich sagen, dass das `<html>`-Tag die unverzichtbare Hülle für dein gesamtes Dokument ist. Es schafft die grundlegende Struktur, indem es den Kopf- vom Körperbereich trennt, und gibt mit dem `lang`-Attribut eine entscheidende Information über den Inhalt weiter.

Ein professionelles und sauberes Startdokument, das du als Vorlage für jedes deiner Projekte verwenden kannst, sieht daher wie folgt aus:

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <!-- Die Zeichenkodierung ist entscheidend für die korrekte Darstellung von Sonderzeichen -->
  <meta charset="UTF-8">

  <!-- Stellt sicher, dass die Seite auf Mobilgeräten korrekt skaliert wird -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- Der Titel, der im Browser-Tab angezeigt wird -->
  <title>Titel deiner Seite</title>
</head>
<body>
  
  <!-- Ab hier beginnt der sichtbare Inhalt deiner Webseite. -->

</body>
</html>
```

Dieses Gerüst ist dein Ausgangspunkt. Es enthält das Wurzelelement `<html>` mit der wichtigen Sprachangabe und einen minimal ausgestatteten `<head>`-Bereich. Von hier aus kannst du beginnen, dein Haus zu bauen – Raum für Raum, Inhalt für Inhalt.
