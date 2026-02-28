# Automatisierung von Aufgaben

### Automatisierung von Aufgaben: Lass den Computer für dich arbeiten

Stell dir vor, du arbeitest an einer Webseite. Du schreibst ein wenig HTML, wechselst dann zu deiner CSS-Datei, um das Styling anzupassen, und vielleicht optimierst du noch ein Bild, bevor du es einfügst. Nach jeder kleinen Änderung speicherst du die Dateien, wechselst zum Browser und lädst die Seite neu, um das Ergebnis zu sehen. Das klingt nach einem normalen Arbeitsablauf, oder? Aber wenn du das hundertmal am Tag machst, summieren sich diese kleinen, sich wiederholenden Schritte zu einer beträchtlichen Zeitspanne. Zeit, in der du nicht kreativ bist, sondern nur mechanische Handgriffe ausführst.

Genau hier kommt die Automatisierung ins Spiel. Die Kommandozeile ist nicht nur ein Werkzeug, um Befehle einzeln auszuführen. Ihre wahre Stärke liegt darin, Abläufe zu definieren, die der Computer dann selbstständig für dich erledigt. Das Prinzip ist einfach: Anstatt immer wieder dieselben fünf Befehle von Hand einzutippen, schreibst du sie einmal in eine Datei und sagst dem Computer: „Führe diese Datei aus.“

Automatisierung im Entwickleralltag bedeutet, repetitive Aufgaben an die Maschine abzugeben. Das spart nicht nur Zeit und Nerven, sondern reduziert auch menschliche Fehler. Ein Tippfehler in einem langen Befehl kann frustrierend sein; ein automatisiertes Skript macht diesen Fehler nie, sobald es einmal korrekt eingerichtet ist. Es sorgt für Konsistenz und macht deinen Arbeitsprozess zuverlässiger und professioneller.

#### Die einfachste Form: Shell-Skripte

Die grundlegendste Methode zur Automatisierung auf der Kommandozeile ist das Shell-Skript. Ein Shell-Skript ist nichts anderes als eine einfache Textdatei, in der du eine Reihe von Kommandozeilenbefehlen untereinander schreibst – genau in der Reihenfolge, in der sie ausgeführt werden sollen.

Nehmen wir ein praktisches Beispiel: Jedes Mal, wenn du ein neues Webprojekt startest, benötigst du vermutlich eine ähnliche Ordnerstruktur. Sagen wir, du brauchst einen Ordner für CSS, einen für JavaScript und einen für Bilder. Außerdem brauchst du eine `index.html`, eine `style.css` und eine `main.js`. Anstatt diese jedes Mal von Hand mit `mkdir` und `touch` zu erstellen, kannst du ein Skript dafür schreiben.

Erstelle eine Datei mit dem Namen `neues-projekt.sh` und schreibe die folgenden Zeilen hinein:

```bash
#!/bin/bash

# Dieses Skript erstellt eine grundlegende Projektstruktur

echo "Erstelle Projektverzeichnisse..."
mkdir css js images

echo "Erstelle grundlegende Dateien..."
touch index.html css/style.css js/main.js

echo "Projektstruktur erfolgreich erstellt!"
```

Die erste Zeile, `#!/bin/bash`, ist ein sogenannter „Shebang“. Er teilt dem Betriebssystem mit, welches Programm (in diesem Fall die Bash-Shell) das Skript ausführen soll. Die Zeilen, die mit einem `#` beginnen, sind Kommentare und werden bei der Ausführung ignoriert. Sie dienen nur dazu, den Code für dich und andere lesbar zu machen.

Um dieses Skript auszuführen, navigierst du in deinem Terminal in den Ordner, in dem die Datei liegt, und gibst den folgenden Befehl ein:

```bash
bash neues-projekt.sh
```

Und voilà! Mit einem einzigen Befehl hast du eine komplette, saubere Projektstruktur erstellt. Das ist die Essenz der Automatisierung: Definiere einen Prozess einmal und führe ihn dann beliebig oft mit minimalem Aufwand aus.

#### Der moderne Standard: npm-Skripte

Während Shell-Skripte universell und mächtig sind, hat sich in der modernen Webentwicklung, insbesondere im JavaScript-Ökosystem, ein anderer Ansatz als Standard etabliert: npm-Skripte. Wahrscheinlich kennst du `npm` (Node Package Manager) als Werkzeug zur Installation von Paketen und Bibliotheken. Aber npm kann noch viel mehr – es ist auch ein exzellenter „Task Runner“, also ein Werkzeug zum Ausführen von Aufgaben.

Die Magie geschieht in einer Datei, die das Herzstück fast jedes modernen Webprojekts ist: der `package.json`. Diese Datei enthält nicht nur Informationen über dein Projekt und seine Abhängigkeiten, sondern auch ein spezielles Feld namens `"scripts"`. Hier kannst du deine eigenen Kommandozeilenbefehle unter einem einfachen, einprägsamen Namen ablegen.

Stell dir vor, du verwendest einen CSS-Präprozessor wie Sass. Dein Arbeitsablauf besteht darin, Sass-Code in einer `.scss`-Datei zu schreiben, den du dann in reguläres CSS umwandeln (kompilieren) musst, damit der Browser ihn versteht. Der Befehl dafür könnte so aussehen: `sass scss/main.scss css/style.css`. Diesen Befehl jedes Mal zu tippen, ist mühsam und fehleranfällig.

Mit npm-Skripten kannst du diesen Prozess elegant vereinfachen. In deiner `package.json` fügst du dem `scripts`-Objekt einen Eintrag hinzu:

```json
{
  "name": "mein-projekt",
  "version": "1.0.0",
  "description": "",
  "scripts": {
    "compile:css": "sass scss/main.scss css/style.css"
  }
}
```

Jetzt kannst du im Terminal einfach Folgendes eingeben:

```bash
npm run compile:css
```

`npm` sucht nun in deiner `package.json` nach dem Skript mit dem Namen `compile:css` und führt den dahinterstehenden Befehl für dich aus. Der Name `compile:css` ist dabei frei wählbar. Du könntest ihn auch `build-styles` oder `kartoffelsalat` nennen – wichtig ist nur, dass er für dich und dein Team verständlich ist.

Der wahre Vorteil zeigt sich, wenn die Aufgaben komplexer werden. Du kannst beispielsweise einen „Watch“-Modus starten, der deine Dateien überwacht und bei jeder Änderung automatisch die Kompilierung durchführt. Der Befehl dafür lautet oft `sass --watch scss/main.scss:css/style.css`. Auch den kannst du in ein npm-Skript packen:

```json
{
  "name": "mein-projekt",
  "version": "1.0.0",
  "description": "",
  "scripts": {
    "compile:css": "sass scss/main.scss css/style.css",
    "watch:css": "sass --watch scss/main.scss:css/style.css"
  }
}
```

Jetzt musst du dir nur noch `npm run watch:css` merken, und schon hast du einen automatischen Helfer, der dir das lästige manuelle Kompilieren nach jeder Änderung abnimmt.

#### Aufgaben kombinieren und Prozesse orchestrieren

Die Stärke von npm-Skripten liegt auch in ihrer Kombinierbarkeit. Du kannst komplexe Befehlsketten erstellen, die mehrere Schritte nacheinander ausführen. Angenommen, du möchtest für die Veröffentlichung deiner Webseite (den „Build“-Prozess) mehrere Dinge tun:

1.  Den alten `dist`-Ordner (distribution/Verteilung), in dem die fertigen Dateien liegen, löschen, um sauber zu starten.
2.  Dein Sass zu CSS kompilieren und das Ergebnis im `dist`-Ordner ablegen.
3.  Dein JavaScript-Code bündeln und minimieren und ebenfalls im `dist`-Ordner speichern.

Du könntest für jeden dieser Schritte ein eigenes Skript anlegen und sie dann in einem übergeordneten `build`-Skript zusammenfassen. Der Operator `&&` sorgt dafür, dass die Befehle nacheinander ausgeführt werden – der nächste aber nur dann, wenn der vorherige erfolgreich war.

```json
{
  "name": "mein-projekt",
  "version": "1.0.0",
  "description": "",
  "scripts": {
    "clean": "rm -rf dist",
    "build:css": "sass scss/main.scss dist/style.css",
    "build:js": "esbuild js/main.js --bundle --minify --outfile=dist/bundle.js",
    "build": "npm run clean && npm run build:css && npm run build:js"
  }
}
```

Mit diesem Setup kannst du deinen gesamten Build-Prozess mit einem einzigen, einfachen Befehl starten:

```bash
npm run build
```

Dieser eine Befehl verbirgt die gesamte Komplexität der einzelnen Schritte. Er ist die Schnittstelle zu deinem Projekt. Ein neuer Entwickler im Team muss nicht die genauen Befehle für Sass oder das JavaScript-Tool `esbuild` kennen. Er muss nur wissen, dass `npm run build` die fertige Webseite erstellt. Das macht die Zusammenarbeit enorm viel einfacher.

#### Ein Blick auf das große Ganze: Build-Tools

Npm-Skripte sind der Klebstoff, der moderne Webentwicklung zusammenhält. Sie sind der Ausgangspunkt für fast jede Form der Automatisierung. Für sehr komplexe Projekte, in denen Dutzende von Aufgaben koordiniert werden müssen – wie Code-Prüfung (Linting), Bildoptimierung, das Starten eines lokalen Entwicklungsservers mit Live-Reload und vieles mehr – greift man oft auf spezialisierte Werkzeuge wie Vite, Webpack oder Parcel zurück.

Diese Tools sind darauf ausgelegt, hochoptimierte und komplexe Build-Prozesse zu verwalten. Das Faszinierende daran ist jedoch, dass du auch diese mächtigen Werkzeuge fast immer über npm-Skripte steuerst. Wenn du ein neues Projekt mit einem Framework wie React oder Vue startest, wirst du in der `package.json` typische Skripte wie `dev`, `build` und `preview` finden.

Hinter `npm run dev` verbirgt sich dann der Befehl, der das komplexe Build-Tool anweist, einen Entwicklungsserver zu starten. Und `npm run build` löst den Prozess aus, der deine Anwendung für die Veröffentlichung optimiert.

Was du hier gelernt hast – die Fähigkeit, Aufgaben über die Kommandozeile zu definieren und zu automatisieren – ist also keine Nischenfähigkeit. Es ist die Grundlage, auf der die gesamte moderne Webentwicklung aufbaut. Indem du die sich wiederholenden, mechanischen Teile deiner Arbeit an den Computer delegierst, schaffst du dir Freiraum für das, was wirklich zählt: kreative Problemlösungen und die Entwicklung großartiger Webseiten.
