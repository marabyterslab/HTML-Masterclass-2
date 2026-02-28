# Installation und Konfiguration

### Dein digitales Handwerkszeug: Installation und Konfiguration

Nachdem wir die theoretischen Grundlagen des Webs und die Rolle von HTML beleuchtet haben, wird es nun Zeit, die Ärmel hochzukrempeln und deine Arbeitsumgebung einzurichten. Jede gute Handwerkerin und jeder gute Handwerker braucht das richtige Werkzeug. Für uns als Webentwickler ist das wichtigste Werkzeug der Code-Editor. Er ist unsere Werkbank, unser Schreibblock und unser intelligenter Assistent in einem.

Ein Code-Editor ist weit mehr als ein einfaches Textprogramm wie Notepad oder TextEdit. Während diese Programme reinen Text ohne Formatierung speichern, ist ein Code-Editor speziell für das Schreiben von Programmier- und Auszeichnungssprachen optimiert. Er hilft dir mit Funktionen wie Syntax-Hervorhebung (Syntax Highlighting), bei der verschiedene Teile deines Codes farblich markiert werden, um die Lesbarkeit drastisch zu erhöhen. Stell dir vor, HTML-Tags sind blau, Attribute grün und Textinhalte weiß – so erkennst du auf einen Blick die Struktur und mögliche Fehler. Hinzu kommen Autovervollständigung, die dir beim Tippen Vorschläge macht, und eine integrierte Dateiverwaltung, die das Arbeiten an ganzen Projekten statt nur an einzelnen Dateien erleichtert.

#### Die Wahl des richtigen Editors: Visual Studio Code

Der Markt für Code-Editoren ist groß, doch in den letzten Jahren hat sich ein Werkzeug als De-facto-Standard in der Webentwicklung etabliert: Visual Studio Code, kurz VS Code. Er wird von Microsoft entwickelt, ist kostenlos, Open Source und für Windows, macOS sowie Linux verfügbar. Seine immense Popularität verdankt er seiner Geschwindigkeit, seiner Flexibilität und vor allem seinem riesigen Ökosystem an Erweiterungen (Extensions), mit denen du den Editor genau auf deine Bedürfnisse zuschneiden kannst.

Für dieses Curriculum werden wir uns auf VS Code konzentrieren. Die hier vorgestellten Konzepte lassen sich aber meist auch auf andere moderne Editoren wie Sublime Text oder die Editoren der JetBrains-Familie übertragen.

#### Installation von Visual Studio Code

Die Installation von VS Code ist erfreulich unkompliziert. Der erste und wichtigste Schritt führt dich auf die offizielle Website: [code.visualstudio.com](https://code.visualstudio.com/). Lade Programme immer nur von der offiziellen Quelle herunter, um sicherzustellen, dass du eine saubere, virenfreie und aktuelle Version erhältst.

Die Website erkennt in der Regel automatisch dein Betriebssystem und bietet dir den passenden Download-Button an. Klicke darauf und lade die Installationsdatei herunter.

**Unter Windows:**
Starte die heruntergeladene `.exe`-Datei. Der Installationsassistent ist selbsterklärend. An einer Stelle wirst du jedoch nach zusätzlichen Aufgaben gefragt. Hier empfehle ich dir dringend, die folgenden Optionen zu aktivieren:

*   **"Zu PATH hinzufügen (nach Neustart verfügbar)"**: Diese Option ist extrem wichtig. Sie ermöglicht es dir, VS Code später direkt aus der Kommandozeile mit dem Befehl `code .` in einem bestimmten Ordner zu öffnen.
*   **"Aktion 'Mit Code öffnen' dem Windows-Explorer-Dateikontextmenü hinzufügen"**: Fügt einen Eintrag im Rechtsklick-Menü für Dateien hinzu.
*   **"Aktion 'Mit Code öffnen' dem Windows-Explorer-Verzeichnis-Kontextmenü hinzufügen"**: Fügt denselben praktischen Eintrag auch für Ordner hinzu, sodass du ein ganzes Projekt per Rechtsklick in VS Code öffnen kannst.

Schließe die Installation ab und starte den Editor.

**Unter macOS:**
Die heruntergeladene Datei ist ein `.zip`-Archiv. Entpacke es, und du erhältst die Anwendung "Visual Studio Code.app". Ziehe diese einfach in deinen "Programme"-Ordner. Das war es schon. Um VS Code auch komfortabel aus dem Terminal starten zu können, öffne den Editor, drücke `Cmd + Shift + P`, um die Befehlspalette zu öffnen, tippe `Shell Command` ein und wähle den Befehl `Shell-Befehl: 'code' in PATH installieren` aus.

**Unter Linux:**
Je nach Distribution kannst du das heruntergeladene `.deb`- (für Debian/Ubuntu) oder `.rpm`-Paket (für Fedora/CentOS) mit dem Paketmanager deiner Wahl installieren. Alternativ bieten viele Distributionen VS Code auch direkt in ihren Software-Repositories an.

#### Die erste Konfiguration: Mach es zu deinem Werkzeug

Wenn du VS Code zum ersten Mal öffnest, wirst du von einem Willkommensbildschirm begrüßt. Nimm dir einen Moment Zeit, um dich mit der Benutzeroberfläche vertraut zu machen. Auf der linken Seite befindet sich die Aktivitätsleiste mit Symbolen für den Explorer (deine Dateien und Ordner), die Suche, die Quellcodeverwaltung (Git), das Debugging und die Erweiterungen. Der größte Teil des Fensters ist der Editorbereich, in dem du deinen Code schreiben wirst.

Die wahre Stärke von VS Code liegt in seiner Anpassbarkeit. Du kannst fast alles nach deinen Wünschen einstellen. Die Einstellungen findest du über das Zahnrad-Symbol unten links oder über die Tastenkombination `Strg + ,` (Windows/Linux) bzw. `Cmd + ,` (macOS).

Hier sind ein paar grundlegende Einstellungen, die dir den Start erleichtern:

*   **Auto Save (Automatisches Speichern)**: Gehe in die Einstellungen und suche nach `Auto Save`. Ändere den Wert von `off` auf `afterDelay`. Das bewirkt, dass deine Dateien nach einer kurzen Verzögerung automatisch gespeichert werden, sobald du aufhörst zu tippen. Du wirst nie wieder vergessen, eine Datei zu speichern, bevor du sie im Browser testest.
*   **Tab Size (Tabulatorgröße)**: In der Webentwicklung ist es üblich, Einrückungen mit zwei Leerzeichen anstelle der standardmäßigen vier vorzunehmen. Suche nach `Tab Size` und ändere den Wert auf `2`.
*   **Word Wrap (Zeilenumbruch)**: Damit du bei langen Zeilen nicht horizontal scrollen musst, ist ein automatischer Zeilenumbruch hilfreich. Suche nach `Word Wrap` und stelle die Option auf `on`.

#### Unverzichtbare Erweiterungen für die HTML-Entwicklung

Jetzt kommen wir zum spannendsten Teil: den Erweiterungen. Sie sind wie Apps für deinen Editor und erweitern seine Funktionalität enorm. Klicke auf das Puzzleteil-Symbol in der Aktivitätsleiste, um den Marktplatz für Erweiterungen zu öffnen. Hier kannst du nach den folgenden Erweiterungen suchen und sie mit einem Klick auf "Installieren" hinzufügen.

**1. Live Server**
Dies ist die wahrscheinlich wichtigste Erweiterung für den Anfang. Normalerweise müsstest du eine HTML-Datei speichern und dann manuell das Browserfenster aktualisieren, um deine Änderungen zu sehen. *Live Server* automatisiert diesen Prozess. Er startet einen kleinen, lokalen Webserver und öffnet deine Seite im Browser. Jedes Mal, wenn du deine HTML- oder CSS-Datei speicherst, wird die Seite im Browser automatisch neu geladen. Das beschleunigt deinen Entwicklungszyklus ungemein.

Nach der Installation findest du unten rechts in der Statusleiste von VS Code einen "Go Live"-Button. Klicke darauf, während du eine HTML-Datei geöffnet hast, und die Magie beginnt.

**2. Prettier - Code formatter**
*Prettier* ist ein sogenannter "opinionated code formatter". Das bedeutet, er nimmt dir die Arbeit ab, deinen Code manuell zu formatieren (Einrückungen, Leerzeichen, Zeilenumbrüche). Er wendet ein konsistentes Regelset auf deinen Code an und sorgt dafür, dass er immer sauber und lesbar aussieht. Das ist nicht nur für dich selbst hilfreich, sondern unerlässlich, wenn du später im Team arbeitest.

Um Prettier optimal zu nutzen, solltest du ihn so einstellen, dass er bei jedem Speichern automatisch läuft. Gehe dazu wieder in die Einstellungen, suche nach `Format On Save` und setze dort einen Haken. Suche anschließend nach `Default Formatter` und wähle aus der Dropdown-Liste "Prettier - Code formatter" aus. Von nun an wird dein Code jedes Mal, wenn du speicherst, automatisch aufgeräumt.

Ein Beispiel: Du schreibst unordentlichen Code wie diesen:
```html
<body><h1>Hallo Welt!</h1><p>Dies ist ein     sehr unordentlicher
Paragraph.</p></body>
```

Nach dem Speichern macht Prettier daraus automatisch:
```html
<body>
  <h1>Hallo Welt!</h1>
  <p>Dies ist ein sehr unordentlicher Paragraph.</p>
</body>
```

**3. Emmet (bereits integriert)**
Emmet ist keine Erweiterung, die du installieren musst, sondern eine mächtige Funktionalität, die in VS Code bereits fest eingebaut ist. Emmet ermöglicht es dir, komplexe HTML-Strukturen mit kurzen, CSS-ähnlichen Abkürzungen zu schreiben.

Anstatt eine komplette HTML-Grundstruktur manuell zu tippen, öffne eine leere `index.html`-Datei, tippe ein einziges Ausrufezeichen (`!`) und drücke die `Tab`- oder `Enter`-Taste. Emmet entfaltet dies sofort zu einem vollständigen HTML5-Grundgerüst:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

Ein anderes Beispiel: Du möchtest eine ungeordnete Liste mit drei Listenelementen erstellen. Anstatt alles auszutippen, schreibst du einfach `ul>li*3` und drückst `Tab`. Das Ergebnis ist:

```html
<ul>
    <li></li>
    <li></li>
    <li></li>
</ul>
```
Emmet ist ein unglaublich produktives Werkzeug, das dir im Laufe deiner Karriere unzählige Tastenanschläge ersparen wird.

Mit einem installierten und konfigurierten VS Code, ausgestattet mit den wichtigsten Erweiterungen, bist du nun bestens gerüstet. Du hast eine professionelle Entwicklungsumgebung geschaffen, die dir hilft, sauberen, fehlerfreien und gut strukturierten Code zu schreiben. Deine Werkbank ist eingerichtet – im nächsten Kapitel beginnen wir, darauf unser erstes richtiges Werkstück zu erschaffen.
