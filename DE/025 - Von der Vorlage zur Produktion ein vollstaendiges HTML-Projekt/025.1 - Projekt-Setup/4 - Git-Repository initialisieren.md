# Git-Repository initialisieren

### Dein Projekt unter Versionskontrolle: Das Git-Repository initialisieren

Stell dir vor, du hast die ersten grundlegenden Dateien für dein neues HTML-Projekt erstellt. In deinem Projektordner liegen eine `index.html`, ein `style.css` und vielleicht ein Unterordner für Bilder. Alles ist an seinem Platz, und du bist bereit, dein Projekt weiterzuentwickeln. Doch mit jeder Änderung, die du vornimmst, schwingt eine leise Sorge mit: Was, wenn du etwas löschst, das du später doch wieder brauchst? Was, wenn du einen Fehler einbaust und nicht mehr genau weißt, wie du zum letzten funktionierenden Zustand zurückkehren kannst?

Der unbegrenzte „Rückgängig“-Befehl, der über eine einzelne Sitzung im Editor hinausgeht, existiert nicht – es sei denn, du schaffst ihn dir selbst. Genau hier kommt die Versionskontrolle mit Git ins Spiel. Git ist wie eine Zeitmaschine für deinen Code. Es erlaubt dir, gezielte „Schnappschüsse“ deines gesamten Projekts zu speichern, wann immer du einen wichtigen Meilenstein erreicht hast. So kannst du jederzeit zu einem früheren Zustand zurückspringen, Änderungen vergleichen oder einfach nur nachvollziehen, wie sich dein Projekt entwickelt hat.

Der allererste Schritt, um diese Superkraft für dein Projekt zu aktivieren, ist die Initialisierung eines Git-Repositorys.

#### Was ist ein Repository?

Bevor wir den Befehl ausführen, lass uns kurz klären, was ein „Repository“ (oft auch kurz „Repo“ genannt) eigentlich ist. Im Grunde ist es dein Projektordner, der um eine entscheidende Komponente erweitert wird: eine Datenbank, die die gesamte Geschichte deines Projekts aufzeichnet. Diese Datenbank wird in einem versteckten Unterordner namens `.git` in deinem Hauptprojektverzeichnis abgelegt.

Dieser `.git`-Ordner ist das Herzstück von Git. Er enthält alle Informationen über deine Commits (die gespeicherten Schnappschüsse), deine Branches (verschiedene Entwicklungslinien) und vieles mehr. Für dich bedeutet das: Solange dieser Ordner existiert und intakt ist, ist die gesamte Historie deines Projekts sicher. Du selbst musst mit diesem Ordner fast nie direkt interagieren – Git kümmert sich im Hintergrund um alles. Die Anwesenheit dieses `.git`-Ordners ist es, was einen normalen Ordner in ein Git-Repository verwandelt.

#### Der magische Befehl: `git init`

Der Prozess, ein neues, leeres Git-Repository zu erstellen, ist erstaunlich einfach. Er besteht aus einem einzigen Befehl: `git init`. Dieser Befehl steht für „initialize“ (initialisieren).

Um ihn auszuführen, musst du eine Kommandozeile (auch Terminal oder Konsole genannt) verwenden. Das mag am Anfang vielleicht etwas einschüchternd wirken, aber es ist das primäre Werkzeug für die Arbeit mit Git und ein unverzichtbarer Begleiter in der Webentwicklung.

Stell dir vor, dein Projekt befindet sich im folgenden Pfad auf deinem Computer: `/Users/deinname/Dokumente/mein-html-projekt`.

1.  **Öffne die Kommandozeile.** Auf macOS findest du sie unter dem Namen „Terminal“, auf Windows ist es oft die „Eingabeaufforderung“ oder die modernere „PowerShell“. Auch der in viele Code-Editoren wie Visual Studio Code integrierte Terminal ist eine hervorragende Wahl.

2.  **Navigiere in deinen Projektordner.** Die Kommandozeile startet normalerweise in deinem Benutzerverzeichnis. Du musst ihr sagen, dass sie in dein Projektverzeichnis wechseln soll. Das geschieht mit dem Befehl `cd` (change directory).

    ```bash
    cd /Users/deinname/Dokumente/mein-html-projekt
    ```
    *Tipp: Oft kannst du den Ordner einfach aus deinem Dateimanager in das Terminalfenster ziehen, um den Pfad automatisch einzufügen.*

3.  **Initialisiere das Repository.** Sobald du dich im richtigen Verzeichnis befindest, gibst du den entscheidenden Befehl ein und drückst die Enter-Taste.

    ```bash
    git init
    ```

Wenn alles geklappt hat, erhältst du eine Bestätigungsmeldung, die ungefähr so aussieht:

```bash
Initialized empty Git repository in /Users/deinname/Dokumente/mein-html-projekt/.git/
```

Diese Meldung sagt dir zwei Dinge: Erstens war der Befehl erfolgreich. Zweitens hat Git in deinem aktuellen Verzeichnis den versteckten `.git`-Ordner angelegt. Dein Ordner ist nun offiziell ein Git-Repository. Du hast das Fundament für deine Zeitmaschine gelegt.

#### Was passiert nach `git init`? Der erste Schnappschuss

Mit `git init` hast du Git zwar gesagt, dass es diesen Ordner ab jetzt verwalten soll, aber du hast noch keinen einzigen Schnappschuss deiner Dateien erstellt. Das Repository ist aus der Sicht von Git noch „leer“, obwohl sich bereits deine `index.html` und andere Dateien darin befinden. Git weiß von ihrer Existenz, aber es verfolgt ihre Änderungen noch nicht aktiv.

Um den aktuellen Zustand deines Projekts als ersten historischen Punkt festzuhalten, sind zwei weitere Schritte notwendig: Du musst die Dateien zur Verfolgung hinzufügen (`add`) und diesen Zustand dann mit einer Beschreibung festschreiben (`commit`).

Stell es dir wie das Fotografieren einer wichtigen Szene vor:
1.  **`git add`**: Du wählst aus, was alles auf dem Foto zu sehen sein soll. Du könntest nur eine einzelne Datei auswählen oder, was am Anfang üblich ist, einfach alles im aktuellen Ordner.
2.  **`git commit`**: Du drückst den Auslöser und machst das eigentliche Foto. Gleichzeitig schreibst du auf die Rückseite des Fotos eine Notiz, was darauf zu sehen ist (z. B. „Erstes Layout der Startseite erstellt“).

Der gängigste Weg, um alle Dateien in deinem Projekt für den ersten Schnappschuss vorzubereiten, ist der folgende Befehl:

```bash
git add .
```

Der Punkt `.` ist hier eine Abkürzung für „alles im aktuellen Verzeichnis und in allen Unterverzeichnissen“.

Nachdem du Git gesagt hast, welche Dateien du aufnehmen möchtest, erstellst du den eigentlichen Commit. Dies geschieht mit dem Befehl `git commit`. Du musst immer eine Nachricht hinzufügen, die beschreibt, was du in diesem Schritt getan hast. Dies geschieht mit dem Parameter `-m` (für „message“).

```bash
git commit -m "Initial commit"
```

Die Nachricht „Initial commit“ (oder auf Deutsch „Erster Commit“) ist eine weitverbreitete Konvention für den allerersten Schnappschuss eines Projekts. Sie signalisiert den Startpunkt der Projekthistorie.

#### Der Status Quo: `git status`

Wie kannst du nun überprüfen, was gerade in deinem Repository los ist? Dein wichtigster Freund und Helfer ist der Befehl `git status`. Er gibt dir jederzeit eine klare und verständliche Übersicht über den Zustand deines Projekts aus der Sicht von Git.

Wenn du `git status` direkt nach `git init` ausführst (aber vor `git add`), wird Git dir auflisten, welche Dateien es im Ordner gefunden hat, diese aber noch nicht verfolgt („untracked files“). Sie werden oft in roter Farbe angezeigt.

Nachdem du `git add .` ausgeführt hast, wird `git status` dir dieselben Dateien als „changes to be committed“ (Änderungen, die zum Commit vorgemerkt sind) anzeigen, oft in grüner Farbe.

Und nachdem du deinen ersten Commit mit `git commit` erstellt hast, wird die Ausgabe von `git status` kurz und bündig sein:

```bash
On branch main
nothing to commit, working tree clean
```

Diese Meldung ist das Ziel nach jedem abgeschlossenen Arbeitsschritt. Sie bedeutet: Der aktuelle Zustand deines Ordners entspricht exakt dem letzten gespeicherten Schnappschuss (Commit). Es gibt keine neuen, ungespeicherten Änderungen. Du hast einen sicheren Speicherpunkt erreicht, zu dem du jederzeit zurückkehren kannst.

Mit dem Ausführen von `git init`, `git add .` und `git commit` hast du den Grundstein für eine saubere und sichere Projektentwicklung gelegt. Jede zukünftige Änderung – sei es das Hinzufügen einer neuen Seite, das Ändern des CSS oder das Umstrukturieren von JavaScript-Code – kann nun in kleinen, nachvollziehbaren Schritten festgehalten werden. Dein Projekt hat jetzt ein Gedächtnis.
