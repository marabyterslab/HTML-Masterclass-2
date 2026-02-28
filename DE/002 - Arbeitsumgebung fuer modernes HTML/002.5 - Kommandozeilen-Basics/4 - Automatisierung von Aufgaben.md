# Automatisierung von Aufgaben

### Mehr Zeit für Kreativität: Aufgaben in der Kommandozeile automatisieren

Du hast nun die Grundlagen der Kommandozeile kennengelernt und kannst dich sicher im Dateisystem bewegen, Dateien erstellen und Programme ausführen. Das ist ein fantastischer erster Schritt. Doch die wahre Stärke der Kommandozeile entfaltet sich erst, wenn du aufhörst, sie nur als interaktives Werkzeug zu sehen, und anfängst, sie als deinen persönlichen, unermüdlichen Assistenten zu betrachten. Die Rede ist von der Automatisierung wiederkehrender Aufgaben.

Jeder Entwickler kennt sie: die kleinen, repetitiven Tätigkeiten, die immer wieder anfallen. Ein neues Projekt anlegen? Du erstellst einen Ordner, darin einen `css`- und einen `js`-Ordner, eine `index.html`, eine `style.css` und eine `script.js`. Bilder für deine Webseite optimieren? Du öffnest ein Programm, ziehst die Bilder hinein, stellst die Kompressionsrate ein und speicherst sie – für jedes Bild einzeln. Diese Aufgaben sind nicht schwer, aber sie kosten Zeit und mentale Energie, die du viel besser in die kreative und logische Arbeit an deinem Code investieren könntest.

Hier kommt die Automatisierung ins Spiel. Indem du der Kommandozeile einmal sagst, wie eine Abfolge von Schritten aussieht, kann sie diese für dich jederzeit und in Sekundenschnelle ausführen. Das spart nicht nur Zeit, sondern reduziert auch Fehler, da der Prozess immer exakt gleich abläuft.

#### Was sind Shell-Skripte?

Die einfachste und universellste Form der Automatisierung in der Kommandozeile sind Shell-Skripte. Ein Shell-Skript ist nichts anderes als eine einfache Textdatei, in der du die Befehle, die du sonst nacheinander von Hand eingeben würdest, untereinander schreibst. Stell es dir wie ein Kochrezept für deinen Computer vor. Du schreibst die Zutaten (die Befehle) und die Zubereitungsschritte (ihre Reihenfolge) auf, und die Shell (z.B. Bash oder Zsh) kocht das Gericht für dich.

Lasst uns das an einem ganz einfachen Beispiel durchspielen. Wir erstellen ein Skript, das uns einfach begrüßt.

1.  **Datei erstellen:** Erstelle eine Datei mit der Endung `.sh`, was für „Shell“ steht. Der Name ist beliebig, aber die Endung ist eine gängige Konvention.
    ```bash
    touch hallo.sh
    ```

2.  **Skript schreiben:** Öffne die Datei `hallo.sh` in einem Texteditor deiner Wahl. Die allererste Zeile eines Shell-Skripts sollte der sogenannte „Shebang“ sein. Er sieht so aus: `#!/bin/bash`. Diese Zeile teilt dem Betriebssystem mit, welches Programm (in diesem Fall die Bash-Shell) den Code in dieser Datei ausführen soll. Darunter schreiben wir einfach einen `echo`-Befehl.
    ```bash
    #!/bin/bash
    
    echo "Hallo Welt! Ich bin ein Skript und bereit zu arbeiten."
    ```

3.  **Ausführbar machen:** Standardmäßig sind neue Textdateien aus Sicherheitsgründen nicht ausführbar. Du musst dem System explizit die Erlaubnis geben, diese Datei als Programm zu starten. Das geschieht mit dem Befehl `chmod` (change mode).
    ```bash
    chmod +x hallo.sh
    ```
    Der Teil `+x` bedeutet „füge die Ausführungsberechtigung (e**x**ecute) hinzu“.

4.  **Skript ausführen:** Jetzt kannst du dein Skript starten. Da sich die Datei im aktuellen Verzeichnis befindet, musst du dem Pfad ein `./` voranstellen. Das signalisiert der Shell, dass sie im aktuellen Ordner (`.`) nach der Datei suchen soll.
    ```bash
    ./hallo.sh
    ```
    Wenn alles geklappt hat, siehst du die Ausgabe: `Hallo Welt! Ich bin ein Skript und bereit zu arbeiten.`

Herzlichen Glückwunsch! Du hast soeben deinen ersten digitalen Assistenten programmiert.

#### Ein praktisches Beispiel: Ein neues Projekt anlegen

Das „Hallo Welt“-Beispiel ist nett, aber lass uns etwas Nützliches bauen. Wir schreiben ein Skript, das die typische Ordnerstruktur für ein kleines Webprojekt anlegt.

Erstelle eine neue Datei namens `create-project.sh` und füge folgenden Inhalt ein:

```bash
#!/bin/bash

# Erstelle den Hauptordner für das Projekt
mkdir "mein-neues-projekt"

# Wechsle in den neuen Ordner
cd "mein-neues-projekt"

# Erstelle die untergeordneten Ordner
mkdir "css"
mkdir "js"

# Erstelle die leeren Dateien
touch index.html
touch css/style.css
touch js/script.js

echo "Projekt 'mein-neues-projekt' wurde erfolgreich erstellt!"
```

Mache auch diese Datei mit `chmod +x create-project.sh` ausführbar und führe sie mit `./create-project.sh` aus. Schau dir das Ergebnis mit `ls -R` an. Du wirst sehen, dass die gesamte Struktur sauber angelegt wurde – mit nur einem einzigen Befehl.

Das ist schon viel besser, aber das Skript hat einen Haken: Es erstellt immer ein Projekt mit dem Namen „mein-neues-projekt“. Was, wenn du ein Projekt anders nennen möchtest? Wir müssen das Skript flexibler machen. Dafür nutzen wir sogenannte **Argumente**. Argumente sind Werte, die du einem Skript beim Aufruf mitgibst. Innerhalb des Skripts kannst du auf sie mit speziellen Variablen zugreifen: `$1` für das erste Argument, `$2` für das zweite und so weiter.

Lass uns unser Skript verbessern:

```bash
#!/bin/bash

# Prüfe, ob ein Projektname als Argument übergeben wurde
if [ -z "$1" ]; then
  echo "Fehler: Bitte gib einen Projektnamen an."
  echo "Beispiel: ./create-project.sh mein-projektname"
  exit 1
fi

# Verwende das erste Argument als Projektnamen
PROJEKT_NAME=$1

# Erstelle den Hauptordner für das Projekt
mkdir "$PROJEKT_NAME"

# Wechsle in den neuen Ordner
cd "$PROJEKT_NAME"

# Erstelle die untergeordneten Ordner
mkdir "css"
mkdir "js"

# Erstelle die leeren Dateien
touch index.html
touch css/style.css
touch js/script.js

echo "Projekt '$PROJEKT_NAME' wurde erfolgreich erstellt!"
```

Jetzt kannst du das Skript so aufrufen: `./create-project.sh cooles-portfolio`. Es wird nun einen Ordner namens `cooles-portfolio` mit der gesamten Struktur darin erstellen. Die kleine `if`-Abfrage am Anfang sorgt dafür, dass das Skript eine hilfreiche Fehlermeldung ausgibt, falls du vergisst, einen Namen anzugeben.

#### Die schnelle Abkürzung: Aliase

Manchmal ist ein ganzes Skript zu viel des Guten. Oft möchtest du nur einen langen, umständlichen Befehl, den du häufig brauchst, durch eine kurze, einprägsame Abkürzung ersetzen. Hierfür gibt es **Aliase**.

Ein klassisches Beispiel ist der `ls`-Befehl. Die Variante `ls -alF` ist oft nützlicher als das einfache `ls`, weil sie versteckte Dateien anzeigt (`a`), eine übersichtliche Liste ausgibt (`l`) und den Dateityp markiert (`F`). Ständig `ls -alF` zu tippen, ist mühsam. Erstellen wir einen Alias:

```bash
alias ll='ls -alF'
```

Gib diesen Befehl in dein Terminal ein. Wenn du jetzt `ll` eingibst und Enter drückst, führt die Shell stattdessen `ls -alF` aus. Genial, oder?

Der einzige Nachteil: Dieser Alias ist nur für die aktuelle Terminal-Sitzung gültig. Sobald du das Fenster schließt, ist er vergessen. Um einen Alias dauerhaft zu speichern, musst du ihn in die Konfigurationsdatei deiner Shell eintragen. Diese Datei liegt in deinem Home-Verzeichnis und heißt je nach Shell:
*   Für Bash: `~/.bashrc` oder `~/.bash_profile`
*   Für Zsh: `~/.zshrc`

Öffne die für dich passende Datei in einem Texteditor und füge die Zeile `alias ll='ls -alF'` am Ende hinzu. Speichere die Datei. Damit die Änderung wirksam wird, musst du entweder ein neues Terminalfenster öffnen oder die Konfigurationsdatei mit dem `source`-Befehl neu laden: `source ~/.zshrc` (oder die entsprechende Datei für deine Shell). Von nun an steht dir der `ll`-Befehl in jeder Terminalsitzung zur Verfügung.

#### Von Shell-Skripten zu modernen Build-Tools

Die hier gezeigten Shell-Skripte und Aliase sind die universellen, grundlegenden Bausteine der Kommandozeilen-Automatisierung. Sie funktionieren auf fast jedem Unix-ähnlichen System (wie macOS und Linux) und sind unglaublich mächtig.

Im modernen Webentwicklungs-Alltag wirst du jedoch feststellen, dass viele Aufgaben von spezialisierten Werkzeugen übernommen werden, die auf diesen Prinzipien aufbauen. Tools wie Node.js und dessen Paketmanager `npm` haben die Automatisierung auf eine neue Ebene gehoben. Statt globale Shell-Skripte zu schreiben, definierst du projektspezifische Skripte direkt in einer Datei namens `package.json`.

Ein Ausschnitt aus einer `package.json` könnte so aussehen:

```json
{
  "name": "mein-modernes-projekt",
  "version": "1.0.0",
  "description": "",
  "scripts": {
    "start": "live-server .",
    "build:css": "sass --watch scss/main.scss css/style.css",
    "build:js": "esbuild js/app.js --bundle --outfile=dist/bundle.js"
  }
}
```

Hier werden unter dem Schlüssel `"scripts"` verschiedene Aufgaben definiert. Mit dem Befehl `npm run start` würdest du zum Beispiel einen lokalen Entwicklungsserver starten. `npm run build:css` würde einen Sass-Compiler anweisen, deine `scss`-Dateien zu beobachten und in `css` umzuwandeln.

Auch wenn die Syntax anders aussieht, ist das zugrundeliegende Konzept dasselbe: Du gibst einem kurzen, einfachen Befehl (`npm run start`) einen Namen, hinter dem sich eine längere, komplexere Anweisung verbirgt. Das Verständnis von Shell-Skripten gibt dir das Fundament, um zu verstehen, was diese modernen Tools unter der Haube eigentlich tun. Sie führen letztendlich auch nur Kommandozeilenbefehle aus.

Die Automatisierung ist eine Denkweise. Sobald du anfängst, dich zu fragen: „Muss ich das wirklich von Hand machen?“, bist du auf dem besten Weg, ein effizienterer und produktiverer Entwickler zu werden. Du lagerst die langweilige Routinearbeit an den Computer aus, damit du dich auf das konzentrieren kannst, was wirklich zählt: großartige Dinge für das Web zu erschaffen.
