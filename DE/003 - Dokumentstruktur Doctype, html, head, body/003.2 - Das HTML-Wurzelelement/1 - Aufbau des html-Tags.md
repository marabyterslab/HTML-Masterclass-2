# Aufbau des html-Tags

### Das `<html>`-Element: Das Fundament Deiner Webseite

Jedes Mal, wenn du eine Webseite erstellst, beginnst du mit einem grundlegenden Fundament. So wie ein Haus auf einem soliden Kellergeschoss steht, benötigt auch jedes HTML-Dokument ein stabiles Basiselement, das alles andere umschließt. In der Welt von HTML ist dieses Fundament das `<html>`-Element. Es ist das allererste und zugleich umfassendste Element deiner gesamten Seite. Man nennt es auch das **Wurzelelement** (Root Element), denn von ihm zweigt die gesamte Struktur deines Dokuments ab, ganz so wie Äste, Zweige und Blätter von der Wurzel eines Baumes.

#### Die grundlegende Struktur

Stell dir vor, du hast ein leeres Blatt Papier vor dir. Bevor du anfängst zu schreiben, legst du einen Rahmen fest. In HTML sieht dieser grundlegende Rahmen immer gleich aus. Das `<html>`-Element umschließt zwei direkte und unverzichtbare Kinder: den `<head>`- und den `<body>`-Bereich.

Ein minimales, aber absolut korrektes HTML-Dokument sieht so aus:

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Metadaten und Dokument-Informationen kommen hierher -->
  </head>
  <body>
    <!-- Der sichtbare Inhalt der Webseite kommt hierher -->
  </body>
</html>
```

Lass uns diesen Aufbau kurz auseinandernehmen:

1.  `<!DOCTYPE html>`: Dies ist keine HTML-Markierung (Tag), sondern eine Anweisung an den Browser. Sie teilt ihm mit: „Achtung, was jetzt kommt, ist ein HTML5-Dokument.“ Diese Zeile muss immer ganz am Anfang stehen.
2.  `<html>`: Unmittelbar danach folgt der öffnende `<html>`-Tag. Er signalisiert den Beginn des eigentlichen HTML-Inhalts. Alles, was zu deiner Webseite gehört (mit Ausnahme des Doctype), muss sich innerhalb dieses Elements befinden.
3.  `<head>`: Der „Kopf“ des Dokuments. Hier platzierst du Informationen *über* die Seite, nicht den sichtbaren Inhalt selbst. Dazu gehören der Titel, der im Browser-Tab angezeigt wird, Verknüpfungen zu CSS-Dateien, Metadaten für Suchmaschinen und vieles mehr.
4.  `<body>`: Der „Körper“ des Dokuments. Hier landet alles, was der Besucher deiner Webseite tatsächlich im Browserfenster sehen soll: Texte, Bilder, Videos, Überschriften, Listen und interaktive Elemente.
5.  `</html>`: Ganz am Ende schließt dieser Tag das Wurzelelement und damit das gesamte HTML-Dokument ab.

Es ist eine goldene Regel: In einem HTML-Dokument gibt es immer nur **ein** `<html>`-Element. Es umschließt exakt **einen** `<head>`- und **einen** `<body>`-Bereich, und zwar immer in dieser Reihenfolge.

#### Die wichtigsten Attribute des `<html>`-Elements

Ein HTML-Tag besteht nicht nur aus seinem Namen, sondern kann auch zusätzliche Informationen in Form von **Attributen** enthalten. Diese Attribute werden direkt im öffnenden Tag platziert und geben dem Browser wichtige Anweisungen. Für das `<html>`-Element sind einige davon von zentraler Bedeutung.

##### Das wichtigste Attribut: `lang`

Das wohl wichtigste Attribut für das `<html>`-Element ist `lang`. Es gibt die primäre Sprache des Dokumenteninhalts an. Warum ist das so unglaublich wichtig? Aus mehreren Gründen:

1.  **Barrierefreiheit (Accessibility):** Screenreader, also Programme, die Webseiten für Menschen mit Sehbehinderungen vorlesen, nutzen das `lang`-Attribut, um die richtige Aussprache und Betonung zu wählen. Ein deutscher Text, der mit englischer Aussprache vorgelesen wird, ist kaum verständlich. Mit `<html lang="de">` stellst du sicher, dass die Software die deutsche Sprachausgabe verwendet.
2.  **Suchmaschinenoptimierung (SEO):** Suchmaschinen wie Google verwenden diese Information, um deine Webseite korrekt zu katalogisieren und sie Nutzern anzuzeigen, die nach Inhalten in dieser Sprache suchen. Eine Seite mit `lang="de"` hat eine höhere Chance, bei deutschen Suchanfragen gut platziert zu werden.
3.  **Browser-Funktionen:** Der Browser selbst nutzt die Sprachangabe für nützliche Funktionen. Er kann beispielsweise automatisch eine Übersetzungsfunktion anbieten, wenn die Sprache des Dokuments nicht mit der bevorzugten Sprache des Nutzers übereinstimmt. Auch die Rechtschreibprüfung in Formularfeldern oder die korrekte Silbentrennung basieren auf dieser Angabe.

Die Werte für das `lang`-Attribut sind standardisierte Sprachcodes nach ISO 639-1. Hier sind einige gängige Beispiele:

```html
<!-- Für eine deutsche Webseite -->
<html lang="de">

<!-- Für eine englische Webseite -->
<html lang="en">

<!-- Für eine französische Webseite -->
<html lang="fr">
```

Du kannst sogar regionale Varianten angeben, indem du einen Ländercode anhängst. `en-US` steht für amerikanisches Englisch, während `en-GB` britisches Englisch bezeichnet. Für Deutsch wären `de-AT` (Österreich) oder `de-CH` (Schweiz) mögliche Varianten. Für die meisten Fälle genügt jedoch der einfache zweibuchstabige Code.

##### Die Schreibrichtung festlegen: das `dir`-Attribut

Während die meisten Sprachen, die du kennst, von links nach rechts geschrieben werden, gibt es auch Sprachen wie Arabisch, Hebräisch oder Persisch, die von rechts nach links geschrieben werden. Um den Browser anzuweisen, das Layout entsprechend anzupassen, gibt es das `dir`-Attribut (von engl. *direction*).

Es hat zwei mögliche Werte:

*   `ltr`: Left-to-right (von links nach rechts). Dies ist der Standardwert und muss für Sprachen wie Deutsch oder Englisch nicht extra angegeben werden.
*   `rtl`: Right-to-left (von rechts nach links).

Eine Webseite auf Arabisch würde also folgendermaßen beginnen:

```html
<html lang="ar" dir="rtl">
```

Der Browser richtet dann nicht nur den Text, sondern auch andere Layout-Elemente wie Scrollleisten oder Formularfelder von rechts nach links aus.

##### Ein Relikt aus der Vergangenheit: `xmlns`

Vielleicht stolperst du gelegentlich über ein weiteres Attribut im `<html>`-Tag: `xmlns="http://www.w3.org/1999/xhtml"`. Dieses Attribut steht für „XML Namespace“ und hat seine Wurzeln in XHTML, einer strengeren Variante von HTML, die den Regeln von XML folgt.

In modernem HTML5 ist dieses Attribut nicht mehr zwingend erforderlich. Der `<!DOCTYPE html>` reicht aus, um den Browser in den richtigen Modus zu versetzen. Dennoch wird es von vielen Entwickler-Tools oder Content-Management-Systemen aus Gründen der Abwärtskompatibilität oder Konformität mit XML-basierten Werkzeugen weiterhin eingefügt. Es schadet nicht, es im Code zu haben, aber wenn du eine neue HTML5-Seite von Grund auf schreibst, kannst du es in der Regel weglassen.

#### Das `<html>`-Element und das DOM

Wenn ein Browser deine HTML-Datei lädt, passiert mehr, als dass er nur Text anzeigt. Er analysiert die Struktur und baut im Hintergrund ein internes Modell der Seite auf, das **Document Object Model (DOM)**. Dieses Modell ist eine Baumstruktur, die die hierarchische Beziehung aller Elemente zueinander darstellt.

An der Spitze dieses Baumes, als absolute Wurzel, steht das `<html>`-Element. In JavaScript kannst du auf dieses Element direkt zugreifen, und zwar über `document.documentElement`.

Dieser Zugriff ist unglaublich mächtig. Du könntest zum Beispiel per JavaScript die Sprache der gesamten Seite dynamisch ändern oder ein dunkles Farbschema aktivieren, indem du dem `<html>`-Element eine CSS-Klasse hinzufügst.

Ein kleines Beispiel in JavaScript, um das Wurzelelement in der Entwicklerkonsole deines Browsers auszugeben:

```javascript
// Gibt das <html>-Element als Objekt zurück
console.log(document.documentElement);
```

Wenn du diesen Code auf einer beliebigen Webseite ausführst, siehst du das komplette `<html>`-Element mit all seinen Attributen und untergeordneten Knoten. Dies zeigt eindrücklich, wie fundamental seine Rolle nicht nur für die statische Struktur, sondern auch für die dynamische Manipulation mit JavaScript ist.

Das `<html>`-Element mag auf den ersten Blick unscheinbar wirken – es ist schließlich nur ein umschließender Container. Doch in Wahrheit ist es der Dreh- und Angelpunkt deines gesamten Webdokuments. Es schafft den Kontext, definiert die Grundsprache und dient als Anker für die gesamte sichtbare und unsichtbare Struktur deiner Seite. Eine solide Kenntnis seiner Funktion und seiner Attribute ist der erste und wichtigste Schritt auf dem Weg zu professionell erstellten Webseiten.
