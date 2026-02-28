# Einrichtung mit Node.js oder Python

### Einrichtung mit Node.js oder Python

Wenn du beginnst, moderne Webseiten zu entwickeln, wirst du schnell an einen Punkt kommen, an dem das einfache Öffnen einer HTML-Datei im Browser nicht mehr ausreicht. Sobald du mit JavaScript Daten nachladen möchtest oder Module verwendest, stößt du auf Sicherheitsbeschränkungen, die dein Browser aus gutem Grund auferlegt. Die Lösung ist ein lokaler Entwicklungsserver. Er simuliert auf deinem Computer eine echte Webserver-Umgebung und umgeht diese Hürden.

Die gute Nachricht ist: Du musst dafür keine komplizierte Server-Software wie Apache oder Nginx installieren und konfigurieren. Für die Frontend-Entwicklung gibt es wunderbar einfache Werkzeuge, die du mit einer einzigen Zeile im Terminal startest. Zwei der beliebtesten und unkompliziertesten Wege basieren auf Technologien, die du als Webentwickler ohnehin früher oder später kennenlernen wirst: Node.js und Python. Schauen wir uns beide Möglichkeiten an.

#### Der Weg mit Node.js: Schnell und vielseitig

Node.js ist eine Laufzeitumgebung, die es dir erlaubt, JavaScript außerhalb des Webbrowsers auszuführen – also direkt auf deinem Computer. Das hat die Webentwicklung revolutioniert und ein riesiges Ökosystem an Werkzeugen hervorgebracht. Eines dieser Werkzeuge ist perfekt für unsere Zwecke geeignet.

**Voraussetzung: Node.js und npm**

Bevor du loslegen kannst, musst du sicherstellen, dass Node.js auf deinem System installiert ist. Falls nicht, kannst du es von der offiziellen Webseite (nodejs.org) herunterladen. Die Installation ist unkompliziert und mit wenigen Klicks erledigt. Mit Node.js wird automatisch auch `npm` (Node Package Manager) installiert. `npm` ist ein Kommandozeilen-Tool, mit dem du Pakete – also wiederverwendbare Code-Module und Werkzeuge – aus einem riesigen, öffentlichen Register herunterladen und verwalten kannst.

Um zu prüfen, ob alles korrekt installiert ist, öffne dein Terminal (die Kommandozeile, PowerShell oder ein integriertes Terminal in deinem Code-Editor) und gib folgende Befehle ein:

```bash
node -v
```

Dieser Befehl sollte dir die installierte Version von Node.js anzeigen, zum Beispiel `v18.17.1`.

```bash
npm -v
```

Dieser Befehl zeigt dir die Version von npm an, etwa `9.6.7`. Wenn bei beiden Befehlen eine Versionsnummer erscheint, bist du startklar.

**Der Helfer: `live-server`**

Es gibt unzählige Entwicklungsserver im npm-Register, aber einer der einfachsten und beliebtesten ist `live-server`. Sein größter Vorteil ist, wie der Name schon andeutet, das „Live Reloading“. Das bedeutet: Jedes Mal, wenn du eine HTML-, CSS- oder JavaScript-Datei in deinem Projekt speicherst, lädt der Server die Seite im Browser automatisch neu. Das erspart dir unzählige manuelle Klicks auf den „Aktualisieren“-Button und beschleunigt deinen Arbeitsfluss enorm.

Die Installation von `live-server` ist ein einziger Befehl. Wir installieren ihn global mit der Option `-g`, damit du ihn von jedem beliebigen Ordner auf deinem Computer aus starten kannst.

```bash
npm install -g live-server
```

Nachdem die Installation abgeschlossen ist, ist das Tool einsatzbereit.

**Den Server starten**

Die Anwendung ist denkbar einfach. Navigiere in deinem Terminal in den Ordner, in dem sich dein HTML-Projekt befindet. Das ist der Ordner, der deine `index.html` und eventuell weitere Unterordner für CSS, JavaScript oder Bilder enthält.

Angenommen, dein Projekt liegt unter `~/Dokumente/mein-html-projekt`. Du wechselst dorthin mit dem Befehl:

```bash
cd ~/Dokumente/mein-html-projekt
```

Sobald du im richtigen Verzeichnis bist, gib einfach den folgenden Befehl ein:

```bash
live-server
```

Das war's schon! Dein Terminal zeigt dir nun eine Meldung an, dass der Server gestartet wurde, und dein Standard-Browser öffnet sich automatisch mit der Adresse, unter der dein Projekt nun erreichbar ist. Meistens ist das etwas wie `http://127.0.0.1:8080`. Die IP-Adresse `127.0.0.1` (auch bekannt als `localhost`) verweist immer auf deinen eigenen Computer.

Jetzt kannst du in deinem Code-Editor an deinen Dateien arbeiten. Speichere eine Änderung in deiner `index.html` oder deiner CSS-Datei – und schau zu, wie sich die Seite im Browser wie von Geisterhand aktualisiert. Um den Server zu beenden, wechselst du zurück ins Terminal und drückst die Tastenkombination `Strg + C` (oder `Cmd + C` auf dem Mac).

#### Die Alternative mit Python: Bordmittel nutzen

Vielleicht hast du Python bereits für andere Zwecke auf deinem Computer installiert oder möchtest dir die Installation von Node.js vorerst sparen. Python ist besonders auf macOS und vielen Linux-Distributionen bereits vorinstalliert. Auch für Windows-Nutzer ist es eine populäre und einfach zu installierende Sprache.

Der große Vorteil des Python-Weges: Du musst absolut nichts zusätzlich installieren. Python bringt von Haus aus ein kleines, aber feines Modul mit, das einen einfachen HTTP-Server startet.

**Voraussetzung: Python**

Überprüfe zuerst, ob und welche Version von Python installiert ist. Öffne dein Terminal und versuche es mit folgendem Befehl:

```bash
python3 --version
```

Wenn eine Versionsnummer erscheint (z. B. `Python 3.11.4`), ist alles bestens. Falls dieser Befehl fehlschlägt, versuche es mit:

```bash
python --version
```

Auf älteren Systemen könnte dies die Version von Python 2 anzeigen. Für die Webentwicklung solltest du immer Python 3 verwenden. Falls du Python noch nicht installiert hast, findest du es auf der offiziellen Webseite (python.org).

**Den Server starten**

Ähnlich wie bei der Node.js-Variante navigierst du zuerst in deinem Terminal in den Hauptordner deines Webprojekts.

```bash
cd ~/Dokumente/mein-html-projekt
```

Dort angekommen, startest du den Server mit einem einzigen Befehl. Für Python 3 lautet er:

```bash
python3 -m http.server
```

Lass uns diesen Befehl kurz aufschlüsseln:
*   `python3` ruft den Python-Interpreter auf.
*   Die Option `-m` steht für „Modul“ und weist Python an, ein bestimmtes Modul als Skript auszuführen.
*   `http.server` ist der Name des eingebauten Moduls, das einen einfachen Webserver bereitstellt.

Nachdem du den Befehl ausgeführt hast, siehst du im Terminal eine Meldung wie diese:

```bash
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

Dein Server läuft nun auf Port 8000. Anders als `live-server` öffnet Python den Browser nicht automatisch. Du musst also manuell einen neuen Tab öffnen und die Adresse `http://localhost:8000` oder `http://127.0.0.1:8000` eingeben.

Ein wichtiger Unterschied zur `live-server`-Lösung ist, dass der Python-Server kein automatisches Neuladen der Seite unterstützt. Wenn du eine Datei änderst und speicherst, musst du im Browser von Hand auf den Aktualisieren-Button klicken, um deine Änderungen zu sehen. Das ist zwar ein kleiner Komfortverlust, für den schnellen Start aber oft völlig ausreichend.

Auch hier beendest du den Server im Terminal mit `Strg + C`.

#### Node.js oder Python – Was ist die richtige Wahl für dich?

Beide Wege führen zum Ziel: einem funktionierenden lokalen Entwicklungsserver. Die Entscheidung hängt oft von deinen persönlichen Vorlieben und deiner bestehenden Arbeitsumgebung ab.

*   **Wähle den Node.js-Weg mit `live-server`**, wenn du ohnehin planst, tiefer in die moderne Webentwicklung mit JavaScript einzutauchen. Die Installation von Node.js ist eine Investition, die sich auszahlen wird, da fast alle modernen Build-Tools, Frameworks und Bibliotheken darauf aufbauen. Der Komfort des Live Reloadings ist ein unschätzbarer Vorteil, der dir im Alltag viel Zeit spart.

*   **Wähle den Python-Weg**, wenn du eine schnelle und unkomplizierte Lösung ohne zusätzliche Installationen suchst. Wenn Python bereits auf deinem System ist, bist du buchstäblich nur einen Befehl von einem laufenden Server entfernt. Es ist die perfekte Wahl für minimalistische Setups oder wenn du nur schnell eine Kleinigkeit testen möchtest, ohne dein System mit weiteren globalen Paketen zu belasten.

Egal, für welche Methode du dich entscheidest, du hast damit einen entscheidenden Schritt in Richtung einer professionellen Entwicklungsumgebung gemacht. Du kannst nun an Projekten arbeiten, die über eine einzelne, statische HTML-Seite hinausgehen, und bist bestens für die kommenden, spannenderen Themen der Webentwicklung gerüstet.
