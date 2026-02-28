# Boilerplate erstellen

### Das Fundament deines Projekts: Eine Boilerplate erstellen

Jedes Mal, wenn du ein neues Webprojekt beginnst, stehst du vor der gleichen Aufgabe: Du musst eine grundlegende Dateistruktur und eine `index.html`-Datei mit den wesentlichen Elementen anlegen. Diese wiederkehrende Routine kann mühsam sein und ist fehleranfällig. Was, wenn du das `viewport`-Meta-Tag vergisst? Oder die falsche Zeichenkodierung wählst? Hier kommt das Konzept der „Boilerplate“ ins Spiel.

Stell dir eine Boilerplate als deine persönliche, professionelle Startvorlage für jedes HTML-Projekt vor. Es ist ein Satz von Dateien und Code, den du als Grundlage verwendest. Anstatt bei null anzufangen, beginnst du mit einem soliden, durchdachten Fundament, das bereits bewährte Praktiken („Best Practices“) enthält. Das spart nicht nur Zeit, sondern stellt auch sicher, dass jedes deiner Projekte mit einem hohen Qualitätsstandard startet.

#### Warum du eine Boilerplate brauchst

Der größte Vorteil ist die Effizienz. Du musst nicht bei jedem Projektstart das Rad neu erfinden und grundlegende HTML-Strukturen, Meta-Tags und Verknüpfungen zu CSS- oder JavaScript-Dateien manuell eintippen. Aber es geht um mehr als nur Zeitersparnis:

*   **Konsistenz:** Deine Projekte haben alle den gleichen, sauberen Ausgangspunkt. Das macht es einfacher, zwischen ihnen zu wechseln und den Code zu verstehen.
*   **Fehlervermeidung:** Wichtige Elemente wie die `DOCTYPE`-Deklaration, die Zeichenkodierung oder das `viewport`-Tag sind von Anfang an korrekt gesetzt. Du läufst nicht Gefahr, sie zu vergessen und dich später über seltsames Verhalten auf mobilen Geräten zu wundern.
*   **Best Practices:** Eine gute Boilerplate enthält bereits die grundlegenden Bausteine für eine moderne, zugängliche und suchmaschinenfreundliche Webseite.

#### Die Anatomie einer minimalen HTML-Boilerplate

Eine Boilerplate ist mehr als nur eine leere HTML-Datei. Sie ist ein sorgfältig zusammengestelltes Grundgerüst. Lass uns die `index.html` Zeile für Zeile durchgehen und verstehen, warum jedes Element an seinem Platz ist.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Titel der Seite</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    
    <h1>Hallo Welt!</h1>

    <script src="js/main.js" defer></script>
</body>
</html>
```

Lass uns diese Struktur aufschlüsseln.

**`<!DOCTYPE html>`**
Diese Zeile ist kein HTML-Tag, sondern eine Anweisung an den Browser, ein sogenannter „Doctype“. Sie muss immer ganz am Anfang deines Dokuments stehen. Sie teilt dem Browser mit: „Achtung, hier kommt ein modernes HTML5-Dokument.“ Ohne diese Anweisung schaltet der Browser in den sogenannten „Quirks Mode“, einen Kompatibilitätsmodus für sehr alte Webseiten, was zu unvorhersehbaren Darstellungsfehlern führen kann.

**`<html lang="de">`**
Dies ist das Wurzelelement deines gesamten Dokuments. Alles andere befindet sich innerhalb dieses Tags. Das Attribut `lang="de"` ist von großer Bedeutung. Es gibt an, dass die Hauptsprache des Dokuments Deutsch ist. Dies ist wichtig für:
*   **Suchmaschinen:** Sie können den Inhalt besser klassifizieren.
*   **Accessibility (Barrierefreiheit):** Screenreader wissen, in welcher Sprache sie den Text vorlesen sollen.
*   **Browser-Funktionen:** Rechtschreibprüfungen oder Übersetzungstools funktionieren zuverlässiger.

**Der `<head>`-Bereich: Die Kommandozentrale**
Der `<head>` enthält Metadaten über dein Dokument – also Informationen, die nicht direkt auf der Seite sichtbar sind, aber für den Browser, Suchmaschinen und andere Systeme entscheidend sind.

**`<meta charset="UTF-8">`**
Dies ist eines der wichtigsten Meta-Tags. Es legt die Zeichenkodierung für dein Dokument fest. `UTF-8` ist der universelle Standard, der fast alle Zeichen und Symbole der Welt abbilden kann, einschließlich deutscher Umlaute wie ä, ö, ü und Sonderzeichen. Ohne diese Angabe könnte dein Browser die Zeichen falsch interpretieren, was zu unleserlichem Kauderwelsch (z. B. „fÃ¼r“ anstelle von „für“) führt.

**`<meta name="viewport" content="width=device-width, initial-scale=1.0">`**
Dieses Tag ist das Herzstück des responsiven Webdesigns. Es gibt mobilen Browsern Anweisungen, wie die Seite dargestellt werden soll.
*   `width=device-width`: Teilt dem Browser mit, dass die Breite der Seite der Breite des Geräts entsprechen soll. Damit wird verhindert, dass mobile Browser die Seite verkleinert als Desktop-Version darstellen.
*   `initial-scale=1.0`: Legt den anfänglichen Zoom-Level fest. `1.0` bedeutet kein Zoom – die Seite wird in ihrer tatsächlichen Größe angezeigt.

Ohne dieses Tag würde deine Webseite auf einem Smartphone winzig klein und unlesbar erscheinen, weil der Browser versuchen würde, die gesamte Desktop-Breite auf den kleinen Bildschirm zu quetschen.

**`<title>Titel der Seite</title>`**
Der Inhalt dieses Tags ist entscheidend. Er erscheint an drei wichtigen Stellen:
1.  Im Tab des Browsers.
2.  Als Name für Lesezeichen.
3.  Als Überschrift in den Suchergebnissen von Google und anderen Suchmaschinen.
Ein aussagekräftiger Titel ist also sowohl für die Benutzerfreundlichkeit als auch für die Suchmaschinenoptimierung (SEO) unerlässlich.

**`<link rel="stylesheet" href="css/style.css">`**
Diese Zeile verbindet deine HTML-Datei mit deinem Stylesheet. Der Browser liest diese Anweisung und lädt die in `style.css` definierten CSS-Regeln, um deine Seite zu gestalten. Die Platzierung im `<head>` sorgt dafür, dass die Stile geladen werden, bevor der Inhalt im `<body>` gerendert wird, was ein ungestaltetes Aufblitzen der Seite („Flash of Unstyled Content“) verhindert.

**Der `<body>`-Bereich: Der sichtbare Inhalt**
Hier platzierst du alles, was der Benutzer tatsächlich auf der Webseite sehen soll: Überschriften, Texte, Bilder, Links und so weiter. In unserer Boilerplate steht hier nur ein Platzhalter-`<h1>`-Element.

**`<script src="js/main.js" defer></script>`**
Ähnlich wie bei der CSS-Datei verknüpft diese Zeile dein HTML mit einer JavaScript-Datei. Die Platzierung und das `defer`-Attribut sind hierbei entscheidend. Früher war es üblich, `<script>`-Tags ganz am Ende des `<body>` zu platzieren. Die moderne und bessere Methode ist jedoch, sie im `<head>` zu platzieren und das `defer`-Attribut zu verwenden.
`defer` weist den Browser an, die JavaScript-Datei im Hintergrund herunterzuladen, während der Rest der HTML-Seite weiter verarbeitet wird. Das Skript wird erst dann ausgeführt, wenn das gesamte HTML-Dokument fertig geladen und analysiert (geparst) ist. Dies verhindert, dass das Laden von JavaScript das Rendern deiner Seite blockiert, was die wahrgenommene Ladezeit erheblich verbessert.

#### Mehr als nur eine Datei: Die Ordnerstruktur

Eine gute Boilerplate besteht nicht nur aus der `index.html`. Sie definiert auch eine sinnvolle und skalierbare Ordnerstruktur. Eine bewährte, einfache Struktur sieht so aus:

```
mein-projekt/
├── css/
│   └── style.css
├── js/
│   └── main.js
├── img/
└── index.html
```

*   **`index.html`**: Liegt im Hauptverzeichnis (Root) deines Projekts.
*   **`css/`**: Ein Ordner, der alle deine CSS-Dateien enthält. Für den Anfang reicht eine `style.css`.
*   **`js/`**: Ein Ordner für all deine JavaScript-Dateien. Eine `main.js` ist ein guter Startpunkt.
*   **`img/`**: Ein Ordner, in dem du alle Bilder und Grafiken für dein Projekt ablegst.

Diese Trennung von Struktur (HTML), Präsentation (CSS) und Verhalten (JavaScript) ist ein zentrales Prinzip der modernen Webentwicklung. Sie hält dein Projekt sauber, organisiert und wartbar.

#### Deine Boilerplate in der Praxis

Wenn du nun ein neues Projekt beginnst, kopierst du einfach diesen gesamten Ordner, benennst ihn um und fängst an, ihn mit Leben zu füllen.

Deine `style.css` könnte am Anfang leer sein oder bereits ein paar grundlegende Resets enthalten:

```css
/* css/style.css */

/* Hier beginnen deine Styles */
body {
    font-family: sans-serif;
    line-height: 1.6;
}
```

Und deine `main.js` wartet auf ihre ersten Anweisungen:

```javascript
// js/main.js

console.log("Skript geladen!");
```

Mit dieser soliden Grundlage hast du die Gewissheit, dass die technischen Basics deines Projekts stimmen. Du kannst dich voll und ganz auf das konzentrieren, was wirklich zählt: den Inhalt, das Design und die Funktionalität deiner Webseite. Deine Boilerplate ist dein zuverlässiger erster Mitarbeiter, der dir die langweilige, aber wichtige Vorarbeit abnimmt.
