# Installation und Konfiguration

### Installation und Konfiguration

Deine Reise in die Welt der modernen Webentwicklung beginnt mit dem wichtigsten Werkzeug in deinem digitalen Werkzeugkasten: dem Code-Editor. Man könnte meinen, dass ein einfaches Textprogramm ausreicht, um HTML zu schreiben – und technisch gesehen stimmt das auch. Aber ein moderner Code-Editor ist so viel mehr als das. Er ist deine Werkstatt, dein Assistent und dein Qualitätsmanager in einem. Er hilft dir, Fehler zu vermeiden, schneller zu schreiben und den Überblick über komplexe Projekte zu behalten.

Die Auswahl des richtigen Editors ist der erste grundlegende Schritt, um eine produktive und angenehme Arbeitsumgebung zu schaffen.

#### Die Wahl des richtigen Editors: Visual Studio Code

Es gibt viele ausgezeichnete Code-Editoren auf dem Markt, wie Sublime Text oder die Editoren der JetBrains-Familie. Für den Einstieg und auch für den professionellen Alltag hat sich jedoch ein Editor als Quasi-Standard in der Webentwicklung etabliert: **Visual Studio Code**, oft einfach als **VS Code** bezeichnet.

Warum ist VS Code so beliebt?

1.  **Kostenlos und Open Source:** Er wird von Microsoft entwickelt, ist aber komplett kostenlos und sein Quellcode ist öffentlich zugänglich.
2.  **Plattformübergreifend:** Er läuft nativ auf Windows, macOS und Linux. Du kannst also auf jedem System mit der gleichen vertrauten Umgebung arbeiten.
3.  **Extrem erweiterbar:** Die wahre Stärke von VS Code liegt in seinem riesigen Ökosystem an Erweiterungen (Extensions). Du kannst den Editor mit unzähligen kostenlosen Plugins für nahezu jeden erdenklichen Zweck anpassen und erweitern.
4.  **Leistungsstark und schnell:** Trotz seines riesigen Funktionsumfangs bleibt VS Code erstaunlich schnell und ressourcenschonend.
5.  **Integrierte Werkzeuge:** Er bringt von Haus aus wichtige Werkzeuge mit, wie eine Git-Integration zur Versionskontrolle und ein eingebautes Terminal, sodass du den Editor seltener verlassen musst.

In diesem Kapitel konzentrieren wir uns daher vollständig auf die Installation und Konfiguration von Visual Studio Code. Die Prinzipien lassen sich jedoch auch auf andere moderne Editoren übertragen.

#### Installation von Visual Studio Code

Die Installation ist erfreulich unkompliziert. Der beste Weg ist immer der direkte Download von der offiziellen Website, um sicherzustellen, dass du eine authentische und aktuelle Version erhältst.

1.  Öffne deinen Webbrowser und navigiere zur offiziellen Website: [https://code.visualstudio.com/](https://code.visualstudio.com/)
2.  Die Website erkennt in der Regel automatisch dein Betriebssystem und bietet dir den passenden Download-Button prominent an. Klicke darauf, um den Installer herunterzuladen.
3.  Führe die heruntergeladene Datei aus und folge den Anweisungen des Installationsassistenten.

Während der Installation unter Windows wirst du einige Optionen sehen. Es ist sehr empfehlenswert, die folgenden Optionen zu aktivieren:

*   **"Zu Path hinzufügen" (Add to PATH):** Dies ist meist standardmäßig aktiviert und sehr wichtig. Es ermöglicht dir, VS Code direkt aus deinem Systemterminal mit dem Befehl `code` zu starten.
*   **"Code als Editor für unterstützte Dateitypen registrieren":** Dadurch wird VS Code zum Standardprogramm für viele Code-Dateien.
*   **"Aktion 'Mit Code öffnen' zum Windows-Explorer-Datei-Kontextmenü hinzufügen"** und **"...Verzeichnis-Kontextmenü hinzufügen":** Diese beiden Optionen sind extrem praktisch. Sie ermöglichen es dir, mit einem Rechtsklick auf eine Datei oder einen Ordner diesen direkt in VS Code zu öffnen.

Nachdem die Installation abgeschlossen ist, starte Visual Studio Code. Du wirst von einem Willkommensbildschirm begrüßt, der dir erste Anlaufstellen und Tipps bietet.

#### Die Benutzeroberfläche: Ein erster Überblick

Auf den ersten Blick mag die Oberfläche komplex wirken, aber sie ist logisch und durchdacht aufgebaut. Die wichtigsten Bereiche sind:

*   **Aktivitätsleiste (Activity Bar):** Ganz links findest du eine schmale Leiste mit Symbolen. Jedes Symbol öffnet eine andere Ansicht in der Seitenleiste. Die wichtigsten sind der Explorer (Dateien und Ordner), die Suche, die Quellcodeverwaltung (Git) und die Erweiterungen.
*   **Seitenleiste (Side Bar):** Direkt neben der Aktivitätsleiste. Hier wird der Inhalt der ausgewählten Ansicht angezeigt, meistens dein Projekt-Explorer.
*   **Editorbereich:** Der größte Bereich in der Mitte. Hier öffnest du deine Dateien und schreibst den eigentlichen Code. Du kannst diesen Bereich teilen, um mehrere Dateien nebeneinander anzuzeigen.
*   **Panel:** Ein Bereich am unteren Rand, der bei Bedarf ein- und ausgeblendet werden kann (mit `Strg + J` oder `Cmd + J`). Hier findest du das integrierte Terminal, die Konsole für Fehlermeldungen und weitere Werkzeuge.
*   **Statusleiste (Status Bar):** Die schmale Leiste ganz unten. Sie zeigt nützliche Informationen über die geöffnete Datei an, wie die Zeilen- und Spaltennummer, die Zeichenkodierung (sollte immer UTF-8 sein) und eventuelle Fehler oder Warnungen.

Nimm dir einen Moment Zeit, um dich mit diesen Bereichen vertraut zu machen. Klicke auf die Symbole in der Aktivitätsleiste und sieh dir an, wie sich die Seitenleiste verändert.

#### Grundlegende Konfiguration

VS Code ist bereits nach der Installation sehr gut nutzbar, aber mit ein paar kleinen Anpassungen kannst du deine Arbeitsumgebung noch komfortabler und effizienter gestalten. Die Einstellungen erreichst du über das Zahnrad-Symbol links unten und den Menüpunkt "Settings" oder über die Tastenkombination `Strg + ,` (Windows/Linux) bzw. `Cmd + ,` (macOS).

Du landest in einer grafischen Oberfläche, in der du nach Einstellungen suchen und diese einfach ändern kannst. Für eine direktere Kontrolle gibt es auch eine Konfigurationsdatei im JSON-Format (`settings.json`). Du kannst zu ihr wechseln, indem du auf das kleine Dokumenten-Symbol oben rechts in der Einstellungsansicht klickst.

Hier sind einige grundlegende Einstellungen, die für die HTML-Entwicklung besonders nützlich sind. Du kannst sie entweder über die grafische Oberfläche suchen oder direkt in deine `settings.json` einfügen.

```json
{
  // Ändert die Schriftgröße im Editor. Passe den Wert nach deinem Geschmack an.
  "editor.fontSize": 16,

  // Setzt die Anzahl der Leerzeichen, die ein Tabulator darstellt.
  // In der Webentwicklung sind 2 oder 4 Leerzeichen üblich.
  "editor.tabSize": 2,

  // Sorgt dafür, dass lange Zeilen automatisch umgebrochen werden und du nicht horizontal scrollen musst.
  "editor.wordWrap": "on",

  // Speichert eine Datei automatisch, wenn du den Fokus vom Editorfenster wegnimmst.
  // Das verhindert Datenverlust und ist die Grundlage für andere Automatisierungen.
  "files.autoSave": "onFocusChange",

  // Zeigt Leerzeichen als kleine Punkte an. Das hilft, versehentliche doppelte
  // Leerzeichen oder eine Mischung aus Tabs und Leerzeichen zu erkennen.
  "editor.renderWhitespace": "boundary",

  // Stellt sicher, dass am Ende jeder Datei eine neue Zeile eingefügt wird.
  // Dies ist eine Konvention in vielen Entwicklungsumgebungen.
  "files.insertFinalNewline": true
}
```

Diese wenigen Einstellungen verbessern die Lesbarkeit und Handhabung deines Codes bereits erheblich.

#### Die Superkräfte: Essenzielle Erweiterungen

Jetzt kommen wir zum Herzstück von VS Code: den Erweiterungen. Sie verwandeln deinen Editor von einem guten Werkzeug in eine maßgeschneiderte Entwicklungsumgebung. Du installierst sie über das "Extensions"-Symbol (sieht aus wie vier Quadrate) in der Aktivitätsleiste. Suche dort einfach nach dem Namen der Erweiterung und klicke auf "Install".

Hier ist eine Liste von unverzichtbaren Erweiterungen für den Start mit HTML:

**1. Live Server**
Dies ist vielleicht die wichtigste Erweiterung für jeden Webentwickler-Anfänger. Normalerweise müsstest du deine HTML-Datei speichern und dann manuell das Browserfenster aktualisieren, um deine Änderungen zu sehen. *Live Server* automatisiert diesen Prozess. Er startet einen kleinen, lokalen Entwicklungsserver und öffnet deine HTML-Seite im Browser. Jedes Mal, wenn du deine Datei speicherst, wird die Seite im Browser automatisch neu geladen. Das beschleunigt deinen Arbeitsfluss enorm. Nach der Installation findest du unten rechts in der Statusleiste einen "Go Live"-Button, um den Server zu starten.

**2. Prettier - Code Formatter**
Code-Formatierung bezieht sich auf den Stil, wie dein Code geschrieben ist – also Einrückungen, Zeilenumbrüche und Leerzeichen. Ein konsistenter Stil macht Code viel leichter lesbar und verständlich. *Prettier* ist ein "opinionated" Code-Formatter, was bedeutet, dass er dir die Entscheidungen abnimmt und deinen Code automatisch nach einem festen Regelwerk formatiert.

Um das Beste aus Prettier herauszuholen, solltest du VS Code so konfigurieren, dass es bei jedem Speichern automatisch formatiert. Füge dazu die folgende Zeile in deine `settings.json` ein:

```json
{
  // ... deine anderen Einstellungen
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```

So sieht ein unformatierter Code-Schnipsel aus:

```html
<p >Dies ist ein <strong>sehr     wichtiger</strong>
Absatz, der sehr schlecht     formatiert ist.</p><ul><li>Punkt 1</li><li>Punkt 2</li></ul>
```

Nach dem Speichern verwandelt Prettier ihn automatisch in das hier:

```html
<p>
  Dies ist ein <strong>sehr wichtiger</strong>
  Absatz, der sehr schlecht formatiert ist.
</p>
<ul>
  <li>Punkt 1</li>
  <li>Punkt 2</li>
</ul>
```

Der Unterschied ist Tag und Nacht. Du musst dir nie wieder Gedanken über die Formatierung machen; dein Code bleibt immer sauber und konsistent.

**3. Emmet (bereits integriert!)**
Emmet ist keine Erweiterung, die du installieren musst, sondern eine mächtige Funktion, die bereits in VS Code eingebaut ist. Sie ist aber so wichtig, dass sie hier erwähnt werden muss. Emmet erlaubt dir, komplexe HTML-Strukturen mit kurzen, CSS-ähnlichen Abkürzungen zu schreiben.

Gib in einer leeren HTML-Datei einfach ein Ausrufezeichen `!` ein und drücke die `Tab`- oder `Enter`-Taste. Emmet generiert für dich sofort das komplette HTML5-Grundgerüst.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body></body>
</html>
```

Ein weiteres Beispiel: Du möchtest eine ungeordnete Liste mit drei Listenelementen, die jeweils einen Link enthalten. Statt alles von Hand zu tippen, schreibst du einfach:

`ul>li*3>a`

... und drückst `Tab`. Emmet erzeugt daraus:

```html
<ul>
  <li><a href=""></a></li>
  <li><a href=""></a></li>
  <li><a href=""></a></li>
</ul>
```

Emmet ist ein gigantischer Produktivitäts-Booster, den du von Anfang an nutzen solltest.

**4. Path Intellisense**
Diese kleine, aber feine Erweiterung hilft dir bei einer häufigen Fehlerquelle: falschen Dateipfaden. Wenn du ein Bild (`<img>`), ein Stylesheet (`<link>`) oder ein Skript (`<script>`) einbinden willst, beginnt diese Erweiterung automatisch, dir die verfügbaren Dateien und Ordner vorzuschlagen, während du den Pfad tippst. Das spart Zeit und verhindert Tippfehler.

Mit diesem Setup – einem installierten und konfigurierten VS Code, ergänzt durch die Erweiterungen Live Server und Prettier – hast du eine solide, professionelle und äußerst effiziente Arbeitsumgebung geschaffen. Du bist nun bestens gerüstet, um dich voll und ganz auf das Schreiben von sauberem und modernem HTML zu konzentrieren.
