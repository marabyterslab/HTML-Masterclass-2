# Installation und Konfiguration

### Installation und Konfiguration deiner Entwicklungsumgebung

Jeder Handwerker braucht eine gut ausgestattete Werkstatt. Für dich als Webentwickler ist diese Werkstatt digital und besteht aus den Werkzeugen, die du täglich nutzt, um Code zu schreiben. Das Herzstück dieser Werkstatt ist dein Code-Editor. Zwar könntest du HTML-Code theoretisch in jedem einfachen Texteditor wie dem Windows-Editor oder TextEdit auf dem Mac schreiben, aber das wäre, als würdest du versuchen, ein Haus nur mit einem Taschenmesser zu bauen. Es ist möglich, aber unglaublich mühsam und fehleranfällig.

Ein moderner Code-Editor ist weit mehr als nur ein Programm zum Tippen. Er ist ein intelligenter Assistent, der dich mit Funktionen wie Syntaxhervorhebung, Code-Vervollständigung und Fehlererkennung unterstützt. Er macht deine Arbeit nicht nur schneller und effizienter, sondern auch angenehmer.

Für unsere gemeinsame Reise durch die Welt des modernen HTML werden wir uns auf einen der beliebtesten und leistungsfähigsten Editoren konzentrieren, der sich in den letzten Jahren zum De-facto-Standard in der Webentwicklung entwickelt hat: **Visual Studio Code**, kurz VS Code. Er ist kostenlos, quelloffen und für Windows, macOS und Linux verfügbar. Seine größte Stärke liegt in seiner unglaublichen Anpassbarkeit durch Erweiterungen, mit denen du den Editor genau auf deine Bedürfnisse zuschneiden kannst.

#### Die Installation von Visual Studio Code

Der erste Schritt zu deiner professionellen Arbeitsumgebung ist die Installation des Editors. Dieser Prozess ist unkompliziert und in wenigen Minuten erledigt.

Besuche die offizielle Website unter `code.visualstudio.com`. Die Seite erkennt in der Regel automatisch dein Betriebssystem und bietet dir den passenden Download-Button direkt auf der Startseite an. Klicke darauf, um die Installationsdatei herunterzuladen.

**Unter Windows:**
Nach dem Download führst du die `.exe`-Datei aus. Ein Installationsassistent führt dich durch den Prozess. Akzeptiere die Lizenzvereinbarung und folge den Anweisungen. Achte während der Installation besonders auf den Schritt „Zusätzliche Aufgaben auswählen“. Hier solltest du sicherstellen, dass die Optionen „Zu PATH hinzufügen“ und die Kontextmenü-Einträge wie „Mit Code öffnen“ aktiviert sind. Dies erleichtert dir später das Öffnen von Projektordnern direkt aus dem Datei-Explorer.

**Unter macOS:**
Die heruntergeladene Datei ist ein `.zip`-Archiv. Nach dem Entpacken findest du die Anwendung „Visual Studio Code“. Ziehe diese einfach in deinen „Programme“-Ordner. Das war es schon. Um VS Code noch einfacher starten zu können, kannst du ihn nach dem ersten Start mit einem Rechtsklick auf das Icon im Dock und der Auswahl von „Optionen > Im Dock behalten“ dort fixieren.

**Unter Linux:**
Für die meisten Debian-basierten Distributionen (wie Ubuntu) lädst du das `.deb`-Paket herunter und installierst es über das Software-Center oder im Terminal mit dem Befehl `sudo apt install ./<dateiname>.deb`. Für Fedora, Red Hat oder SUSE steht ein `.rpm`-Paket zur Verfügung.

Nach der erfolgreichen Installation kannst du VS Code starten und wirst von einem Willkommensbildschirm begrüßt, der dir erste Hinweise und Links zur Dokumentation bietet.

#### Ein erster Blick: Die Benutzeroberfläche

Wenn du VS Code zum ersten Mal öffnest, mag die Oberfläche zunächst komplex wirken. Lass uns die wichtigsten Bereiche kurz durchgehen, damit du dich schnell zurechtfindest:

1.  **Aktivitätsleiste (Activity Bar):** Ganz links befindet sich eine schmale Leiste mit Symbolen. Von hier aus schaltest du zwischen den Hauptansichten um: dem Explorer zum Verwalten deiner Dateien, der Suche, der Quellcodeverwaltung (Git), dem Debugger und der Ansicht für Erweiterungen.
2.  **Seitenleiste (Side Bar):** Direkt neben der Aktivitätsleiste. Hier wird der Inhalt der jeweils aktiven Ansicht angezeigt, meistens der Datei-Explorer deines geöffneten Projektordners.
3.  **Editor-Bereich:** Dies ist der größte Bereich in der Mitte. Hier schreibst und bearbeitest du deinen Code. Du kannst diesen Bereich teilen und mehrere Dateien nebeneinander öffnen.
4.  **Statusleiste (Status Bar):** Die Leiste ganz unten am Fensterrand. Sie zeigt dir nützliche Informationen zum aktuellen Projekt, wie die Zeilen- und Spaltennummer deines Cursors, die Zeichenkodierung (sollte immer UTF-8 sein) und eventuelle Fehler oder Warnungen.

Nimm dir einen Moment Zeit, um dich mit diesen Bereichen vertraut zu machen. Die Bedienung ist sehr intuitiv und wird dir schnell in Fleisch und Blut übergehen.

#### Grundlegende Konfigurationen für einen besseren Arbeitsfluss

VS Code funktioniert bereits nach der Installation sehr gut, aber mit ein paar kleinen Anpassungen können wir unsere Arbeitsumgebung noch komfortabler und effizienter gestalten. Alle Einstellungen findest du, indem du auf das Zahnrad-Symbol unten links in der Aktivitätsleiste klickst und „Einstellungen“ wählst oder die Tastenkombination `Strg + ,` (Windows/Linux) bzw. `Cmd + ,` (macOS) verwendest.

**Automatisches Speichern (Auto Save):**
Eine der nützlichsten Funktionen ist das automatische Speichern. Anstatt nach jeder kleinen Änderung manuell `Strg + S` drücken zu müssen, kannst du VS Code anweisen, dies für dich zu tun. Suche in den Einstellungen nach „Auto Save“ und ändere den Wert von `off` auf `onFocusChange`. Nun wird eine Datei immer dann automatisch gespeichert, wenn du das Editor-Fenster verlässt, zum Beispiel, um in deinen Browser zu wechseln und das Ergebnis anzusehen. Das spart unzählige Tastendrücke und verhindert, dass du vergisst zu speichern.

**Farbthema und Schriftart:**
Das Aussehen deines Editors hat einen großen Einfluss darauf, wie gerne und wie lange du ermüdungsfrei darin arbeiten kannst. VS Code wird mit mehreren Farbthemen (hell und dunkel) ausgeliefert. Du kannst das Thema über die Einstellungen (suche nach „Color Theme“) oder schneller über den Befehlspaletten-Shortcut `Strg + Umschalt + P` (oder `Cmd + Umschalt + P`), gefolgt von der Eingabe „Color Theme“, ändern. Wähle ein Thema, das für deine Augen angenehm ist.

Ebenso kannst du die Schriftgröße („Font Size“) und die Schriftart („Font Family“) anpassen, um die Lesbarkeit zu optimieren.

#### Die Superkräfte deines Editors: Erweiterungen (Extensions)

Die wahre Stärke von VS Code liegt in seinem riesigen Ökosystem an Erweiterungen. Das sind kleine Zusatzprogramme, die du direkt im Editor installieren kannst, um neue Funktionen hinzuzufügen. Klicke dazu auf das viereckige Symbol (wie vier Bausteine) in der Aktivitätsleiste, um den Marktplatz für Erweiterungen zu öffnen.

Für die HTML-Entwicklung gibt es ein paar unverzichtbare Helfer, die du dir von Anfang an installieren solltest:

**1. Live Server:**
Normalerweise musst du nach jeder Änderung an deiner HTML-Datei zum Browser wechseln und die Seite manuell aktualisieren, um das Ergebnis zu sehen. Das wird schnell lästig. Die Erweiterung „Live Server“ von Ritwick Dey löst dieses Problem elegant. Nach der Installation erscheint in der Statusleiste unten rechts ein „Go Live“-Button. Wenn du diesen klickst, während du eine HTML-Datei geöffnet hast, startet die Erweiterung einen kleinen lokalen Entwicklungsserver und öffnet deine Seite im Standardbrowser. Der Clou: Jedes Mal, wenn du deine HTML- oder CSS-Datei speicherst, lädt die Seite im Browser automatisch neu. Dieser sofortige visuelle Feedback-Zyklus beschleunigt deine Entwicklung enorm.

**2. Prettier - Code Formatter:**
Ein sauber und einheitlich formatierter Code ist nicht nur schöner anzusehen, sondern auch leichter zu lesen und zu warten. „Prettier“ ist ein sogenannter „opinionated“ Code-Formatter, was bedeutet, dass er dir die Arbeit des Formatierens komplett abnimmt und deinen Code nach einem festen Regelwerk automatisch einrückt und umbricht.

Nach der Installation solltest du VS Code so konfigurieren, dass er Prettier bei jedem Speichervorgang automatisch ausführt. Gehe dazu wieder in die Einstellungen (`Strg + ,`) und suche nach „Format On Save“. Setze hier einen Haken. Suche anschließend nach „Default Formatter“ und wähle „Prettier - Code Formatter“ aus der Dropdown-Liste aus. Von nun an wird dein Code bei jedem Speichern perfekt formatiert, ohne dass du dich darum kümmern musst.

```html
<!-- Vor Prettier -->
< body ><h1   style="color:blue;" >Hallo Welt!</h1 ><p>Dies ist ein
schlecht formatierter Absatz.</p   ></body>
```

```html
<!-- Nach dem Speichern mit Prettier -->
<body>
  <h1 style="color: blue">Hallo Welt!</h1>
  <p>Dies ist ein schlecht formatierter Absatz.</p>
</body>
```

**3. Emmet (bereits integriert):**
Emmet ist keine Erweiterung, die du installieren musst, sondern eine mächtige Funktion, die bereits in VS Code fest eingebaut ist. Es ist ein Toolkit, das es dir ermöglicht, komplexe HTML-Strukturen mit kurzen, CSS-ähnlichen Abkürzungen zu schreiben.

Das grundlegendste und wichtigste Emmet-Kürzel ist das Ausrufezeichen (`!`). Öffne eine neue, leere HTML-Datei (z. B. `index.html`), tippe ein einziges Ausrufezeichen in die erste Zeile und drücke die `Tab`-Taste. Emmet entfaltet dieses Kürzel augenblicklich in ein vollständiges HTML5-Grundgerüst.

```html
<!-- Du tippst nur das hier: -->
!
```

```html
<!-- Und nach Drücken der Tab-Taste wird daraus: -->
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

Dies allein spart dir bei jedem neuen Projekt wertvolle Zeit und stellt sicher, dass du immer mit einer korrekten und standardkonformen Basis startest.

#### Dein erster Arbeitsablauf in der Praxis

Mit dem installierten und konfigurierten Editor bist du nun bestens gerüstet. Lass uns den typischen Arbeitsablauf einmal durchspielen:

1.  **Projektordner erstellen:** Lege irgendwo auf deinem Computer einen neuen, leeren Ordner für dein erstes Projekt an, zum Beispiel `mein-erstes-projekt`.
2.  **Ordner in VS Code öffnen:** Starte VS Code. Wähle „Datei > Ordner öffnen“ und navigiere zu deinem neu erstellten Ordner. Alternativ kannst du, wenn du es bei der Installation unter Windows aktiviert hast, einfach mit der rechten Maustaste auf den Ordner klicken und „Mit Code öffnen“ wählen.
3.  **Datei erstellen:** In der Seitenleiste (Explorer) siehst du nun deinen leeren Ordner. Klicke auf das kleine Datei-Symbol mit dem Pluszeichen, um eine neue Datei zu erstellen. Nenne sie `index.html`.
4.  **HTML-Grundgerüst erzeugen:** Tippe in die leere Datei ein `!` und drücke `Tab`. Das HTML-Grundgerüst erscheint.
5.  **Inhalt hinzufügen:** Füge innerhalb des `<body>`-Tags eine einfache Überschrift ein, zum Beispiel `<h1>Hallo aus VS Code!</h1>`.
6.  **Live Server starten:** Klicke auf den „Go Live“-Button in der Statusleiste unten rechts. Dein Browser sollte sich öffnen und deine Überschrift anzeigen.
7.  **Änderungen live sehen:** Gehe zurück zu VS Code und ändere den Text in der Überschrift. Sobald du die Datei speicherst (was dank `onFocusChange` passiert, sobald du zum Browser wechselst), wird die Seite im Browser automatisch aktualisiert und zeigt deine Änderung.

Du hast nun eine professionelle, effiziente und angenehme Arbeitsumgebung eingerichtet. Dieser Aufbau aus einem leistungsstarken Editor, automatischem Neuladen im Browser und automatischer Code-Formatierung bildet das Fundament, auf dem du deine HTML-Kenntnisse nun systematisch aufbauen kannst.
