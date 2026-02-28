# Automatisierung von Aufgaben

### Automatisierung von Aufgaben: Wenn die Kommandozeile für dich arbeitet

Stell dir vor, du beginnst ein neues Webprojekt. Was sind die ersten Schritte? Wahrscheinlich erstellst du einen neuen Ordner. In diesem Ordner erstellst du weitere Ordner, typischerweise für CSS, JavaScript und Bilder. Dann legst du eine `index.html`, eine `style.css` und eine `main.js` Datei an. Das machst du nicht nur einmal, sondern für fast jedes kleine und große Projekt. Nach dem zehnten Mal wird es eintönig, nach dem fünfzigsten Mal ist es nur noch lästige Routine.

Genau hier kommt die wahre Stärke der Kommandozeile ins Spiel: die Automatisierung von genau solchen wiederkehrenden Aufgaben. Der Gedanke dahinter ist einfach: Warum solltest du immer wieder die gleichen Befehle eintippen, wenn der Computer das für dich erledigen kann? Du schreibst einmal eine Anleitung – ein sogenanntes Skript – und der Computer folgt ihr jedes Mal aufs Neue, fehlerfrei und in Sekundenschnelle.

#### Deine ersten Helfer: Shell-Skripte

Die einfachste Form der Automatisierung auf der Kommandozeile sind Shell-Skripte. Ein Shell-Skript ist im Grunde nichts anderes als eine Textdatei, in der du die Befehle, die du sonst nacheinander von Hand eingeben würdest, untereinander aufschreibst. Die Shell liest diese Datei dann Zeile für Zeile und führt die Befehle aus.

Bleiben wir bei unserem Beispiel, dem Anlegen einer neuen Projektstruktur. Die Befehle dafür könnten so aussehen:

```bash
mkdir mein-neues-projekt
cd mein-neues-projekt
mkdir css js images
touch index.html css/style.css js/main.js
```

Diese Befehlsfolge funktioniert, aber wir müssen jedes Mal den Projektnamen (`mein-neues-projekt`) manuell ändern. Das können wir besser machen. Lass uns ein Skript erstellen, das uns diese Arbeit abnimmt.

Erstelle eine neue Datei mit dem Namen `neues_projekt.sh`. Das `.sh` am Ende steht für "Shell" und ist eine gängige Konvention für Shell-Skripte. In diese Datei schreiben wir Folgendes:

```bash
#!/bin/bash

# Ein Skript, das eine neue Projektstruktur erstellt.

mkdir $1
cd $1
mkdir css js images
touch index.html css/style.css js/main.js

echo "Projekt '$1' wurde erfolgreich erstellt!"
```

Schauen wir uns das genauer an:

*   `#!/bin/bash`: Diese erste Zeile nennt sich "Shebang". Sie teilt dem Betriebssystem mit, welches Programm zum Ausführen dieses Skripts verwendet werden soll. In diesem Fall ist es die `bash`-Shell, die auf den meisten Systemen (Linux, macOS) Standard ist.
*   `# Ein Skript...`: Zeilen, die mit einem `#` beginnen, sind Kommentare. Sie werden von der Shell ignoriert und dienen nur dir und anderen zur Erklärung des Codes.
*   `$1`: Das ist der magische Teil. `$1` ist ein Platzhalter für das erste Argument, das du dem Skript beim Aufruf mitgibst. Wenn du also später `neues_projekt.sh super-projekt` ausführst, wird jedes `$1` im Skript durch `super-projekt` ersetzt.
*   `echo "..."`: Der `echo`-Befehl gibt einfach den nachfolgenden Text auf der Kommandozeile aus. Eine kleine Erfolgsmeldung ist immer eine gute Sache.

Bevor du dieses Skript ausführen kannst, musst du dem System noch sagen, dass es sich um eine ausführbare Datei handelt. Standardmäßig sind Textdateien aus Sicherheitsgründen nicht ausführbar. Das änderst du mit dem Befehl `chmod` (change mode):

```bash
chmod +x neues_projekt.sh
```

`+x` bedeutet "füge die Ausführungsberechtigung hinzu". Jetzt ist dein Skript bereit. Du kannst es direkt aus dem Verzeichnis, in dem es liegt, aufrufen:

```bash
./neues_projekt.sh mein-erstes-automatisches-projekt
```

Der `./` am Anfang ist wichtig. Er sagt der Shell: "Suche die Datei `neues_projekt.sh` nicht irgendwo im System, sondern genau hier, im aktuellen Verzeichnis." Nach der Ausführung wirst du sehen, dass ein neuer Ordner mit der kompletten, sauberen Struktur angelegt wurde – mit nur einem einzigen Befehl.

#### Abkürzungen für den Alltag: Aliase

Manchmal ist ein komplettes Skript zu viel des Guten. Oft sind es nur einzelne, lange Befehle, die man ständig tippt und abkürzen möchte. Ein klassisches Beispiel ist `ls -la`, um eine detaillierte Liste aller Dateien (auch der versteckten) anzuzeigen. Dafür gibt es Aliase.

Ein Alias ist ein von dir definierter Spitzname für einen längeren Befehl. Du kannst ihn ganz einfach mit dem `alias`-Befehl erstellen:

```bash
alias ll='ls -la'
```

Wenn du jetzt `ll` in deine Kommandozeile eingibst und Enter drückst, führt die Shell stattdessen `ls -la` aus. Das spart Tipparbeit und fühlt sich einfach flüssiger an.

Der Haken an der Sache: Ein so erstellter Alias gilt nur für die aktuelle Terminalsitzung. Sobald du das Fenster schließt, ist er wieder weg. Um einen Alias dauerhaft zu speichern, musst du ihn in die Konfigurationsdatei deiner Shell eintragen. Diese Datei liegt in deinem Benutzerverzeichnis (dem Ordner, in dem du landest, wenn du ein Terminal öffnest) und ist normalerweise versteckt.

*   Für die **Bash**-Shell heißt die Datei meist `.bashrc` oder `.bash_profile`.
*   Für die **Zsh**-Shell (Standard auf neueren macOS-Versionen) heißt sie `.zshrc`.

Öffne die für dich passende Datei in einem Texteditor und füge die Zeile `alias ll='ls -la'` am Ende hinzu. Speichere die Datei. Damit die Änderungen wirksam werden, musst du entweder ein neues Terminalfenster öffnen oder den Befehl `source ~/.bashrc` (bzw. `source ~/.zshrc`) ausführen, der die Konfigurationsdatei neu einliest. Von nun an steht dir dein Alias `ll` in jeder Terminalsitzung zur Verfügung.

#### Der moderne Standard: npm-Skripte

Wenn du beginnst, mit modernen Werkzeugen für die Webentwicklung wie CSS-Präprozessoren, JavaScript-Build-Tools oder Live-Servern zu arbeiten, wirst du schnell auf den Node Package Manager, kurz `npm`, stoßen. `npm` ist weit mehr als nur ein Werkzeug zum Installieren von Paketen – es ist auch ein unglaublich mächtiger und weit verbreiteter Task-Runner.

Das Herzstück eines jeden `npm`-Projekts ist die Datei `package.json`. In dieser Datei werden nicht nur die Abhängigkeiten deines Projekts verwaltet, sondern es gibt auch einen speziellen Bereich namens `"scripts"`. Hier kannst du deine eigenen Kommandozeilen-Aufgaben definieren, die projektspezifisch sind.

Stell dir vor, du nutzt das Paket `live-server`, um deine Webseite während der Entwicklung lokal mit automatischer Neulade-Funktion anzuzeigen. Normalerweise würdest du in dein Projektverzeichnis navigieren und `live-server` eintippen. Mit einem npm-Skript wird das standardisiert und für jeden, der an dem Projekt arbeitet, nachvollziehbar.

Eine einfache `package.json` könnte so aussehen:

```json
{
  "name": "mein-projekt",
  "version": "1.0.0",
  "description": "Ein Beispielprojekt für npm-Skripte",
  "scripts": {
    "start": "live-server",
    "build": "echo 'Build-Prozess noch nicht implementiert.'"
  }
}
```

Der `"scripts"`-Block enthält Schlüssel-Wert-Paare. Der Schlüssel ist der Name des Skripts (z. B. `"start"`), und der Wert ist der Befehl, der ausgeführt werden soll (z. B. `"live-server"`).

Um diese Skripte auszuführen, verwendest du den Befehl `npm run` gefolgt vom Skriptnamen. Um den Server zu starten, würdest du also tippen:

```bash
npm run start
```

Das Tolle daran ist, dass `npm` automatisch weiß, wo die Programme (wie `live-server`) liegen, die du über `npm` installiert hast. Du musst dir keine Gedanken über Pfade machen. `start` ist übrigens ein besonderer Skriptname. Du kannst ihn auch einfach mit `npm start` aufrufen.

Der wahre Vorteil zeigt sich, wenn die Aufgaben komplexer werden. Du kannst Befehle mit `&&` verketten, um sie nacheinander auszuführen. Angenommen, du möchtest vor dem Deployment deine HTML-, CSS- und JS-Dateien in einen separaten `dist`-Ordner (für "distribution") kopieren. Dein Build-Skript könnte so aussehen:

```json
"scripts": {
  "start": "live-server",
  "build": "rm -rf dist && mkdir dist && cp index.html css/style.css js/main.js dist/"
}
```

Mit einem einzigen Befehl, `npm run build`, löschst du den alten `dist`-Ordner (falls vorhanden), erstellst einen neuen und kopierst alle relevanten Dateien hinein. Das ist nicht nur bequem, sondern auch zuverlässig. Du vergisst keine Datei und die Schritte werden immer in der richtigen Reihenfolge ausgeführt.

Shell-Skripte, Aliase und npm-Skripte sind die Grundpfeiler der Automatisierung auf der Kommandozeile. Sie nehmen dir repetitive Arbeit ab, reduzieren Fehlerquellen und machen deine Arbeitsabläufe professioneller und effizienter. Indem du lernst, die Kommandozeile nicht nur als Eingabewerkzeug, sondern als programmierbare Umgebung zu verstehen, machst du einen entscheidenden Schritt vom reinen Anwender zum Gestalter deiner eigenen, optimierten Arbeitsumgebung.
