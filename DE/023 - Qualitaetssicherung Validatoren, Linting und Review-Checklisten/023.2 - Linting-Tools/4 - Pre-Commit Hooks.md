# Pre-Commit Hooks

### Pre-Commit Hooks: Dein automatischer Qualitätswächter

Nachdem du nun die Welt der Linters und Formatierer wie ESLint, Stylelint und Prettier kennengelernt hast, weißt du, wie mächtig diese Werkzeuge sind, um die Codequalität und -konsistenz in einem Projekt sicherzustellen. Sie finden Fehler, setzen Stilregeln durch und formatieren deinen Code automatisch. Doch es gibt eine menschliche Schwachstelle in diesem Prozess: Du musst daran denken, sie auch auszuführen. In der Hektik eines Projekts, kurz vor einer wichtigen Deadline, kann es schnell passieren, dass man vergisst, den Linter laufen zu lassen, bevor man seinen Code in das Repository committet.

Genau hier kommt ein weiteres, extrem nützliches Werkzeug aus dem Git-Ökosystem ins Spiel: Git Hooks. Stell dir einen Git Hook als einen automatischen Türsteher für dein Repository vor. Bevor eine bestimmte Git-Aktion (wie ein Commit oder ein Push) abgeschlossen wird, kann dieser Türsteher ein Skript ausführen, um zu überprüfen, ob alles in Ordnung ist. Wenn das Skript erfolgreich durchläuft, wird die Tür geöffnet und die Aktion fortgesetzt. Wenn das Skript jedoch fehlschlägt, wird die Aktion blockiert.

Für unsere Zwecke der Qualitätssicherung ist der `pre-commit` Hook der interessanteste. Wie der Name schon sagt, wird er ausgeführt, *bevor* eine Commit-Nachricht eingegeben und der eigentliche Commit erstellt wird. Dies ist der perfekte Zeitpunkt, um unsere Linters und Formatierer automatisch auf den Code anzuwenden, den du gerade committen möchtest.

#### Wie Git Hooks funktionieren (und ihre Grenzen)

Jedes Mal, wenn du ein Git-Repository initialisierst oder klonst, erstellt Git in seinem internen Verzeichnis `.git` einen Ordner namens `hooks`. Darin findest du eine Reihe von Beispiel-Skriptdateien, wie `pre-commit.sample`, `prepare-commit-msg.sample` und so weiter. Um einen Hook zu aktivieren, musst du lediglich die `.sample`-Endung von der entsprechenden Datei entfernen.

Du könntest also ein Shell-Skript namens `pre-commit` erstellen, das deine Linting-Befehle ausführt.

```bash
#!/bin/sh

# Führe ESLint für alle JavaScript-Dateien aus
npm run lint:js

# Prüfe, ob ESLint Fehler gefunden hat
if [ $? -ne 0 ]; then
  echo "ESLint hat Fehler gefunden. Bitte behebe sie vor dem Commit."
  exit 1 # Verhindert den Commit
fi

# Führe Prettier zur Formatierungsprüfung aus
npm run format:check

# Prüfe, ob Prettier Fehler gefunden hat
if [ $? -ne 0 ]; then
  echo "Prettier hat Formatierungsprobleme gefunden. Bitte formatiere den Code vor dem Commit."
  exit 1 # Verhindert den Commit
fi

exit 0 # Erlaubt den Commit
```

Dieses manuelle Vorgehen hat jedoch einen entscheidenden Nachteil: Der `.git`-Ordner wird nicht versioniert, also nicht mit dem Rest deines Projekts geteilt. Das bedeutet, jeder Entwickler in deinem Team müsste diese Hook-Skripte manuell einrichten und aktuell halten. Das ist fehleranfällig und alles andere als praktisch.

#### Die moderne Lösung: `husky` und `lint-staged`

Glücklicherweise gibt es elegante Werkzeuge, die dieses Problem lösen und die Verwaltung von Git Hooks zu einem Kinderspiel machen. Die beliebteste Kombination in der modernen Webentwicklung besteht aus `husky` und `lint-staged`.

*   **Husky:** Ist ein Werkzeug, das es dir erlaubt, Git Hooks einfach über deine `package.json`-Datei oder separate Konfigurationsdateien zu verwalten. Wenn ein Teammitglied das Projekt auscheckt und `npm install` ausführt, installiert Husky automatisch die konfigurierten Hooks im lokalen `.git`-Verzeichnis. So wird sichergestellt, dass jeder im Team die gleichen Qualitätsprüfungen verwendet.

*   **Lint-Staged:** Ist der intelligente Partner von Husky. Den Linter bei jedem Commit über das *gesamte* Projekt laufen zu lassen, kann bei großen Codebasen sehr lange dauern. Das ist ineffizient und frustrierend. `lint-staged` löst dieses Problem, indem es deine Linter- und Formatierer-Befehle *nur* auf den Dateien ausführt, die du mit `git add` zur Staging Area hinzugefügt hast – also genau die Dateien, die Teil deines nächsten Commits sein werden. Das ist blitzschnell und präzise.

#### Schritt-für-Schritt-Einrichtung

Lass uns ansehen, wie du diese beiden Werkzeuge in deinem Projekt einrichtest. Voraussetzung ist, dass du bereits ein `package.json` in deinem Projekt hast und Tools wie ESLint oder Prettier konfiguriert sind.

**1. Installation**

Zuerst installierst du `husky` und `lint-staged` als Entwicklungsabhängigkeiten (dev dependencies).

```bash
npm install --save-dev husky lint-staged
```

**2. Husky initialisieren**

Nach der Installation musst du Husky einmalig initialisieren. Dieser Befehl erstellt ein `.husky`-Verzeichnis in deinem Projekt und konfiguriert Git so, dass es dieses Verzeichnis für Hooks verwendet.

```bash
npx husky init
```

Gleichzeitig fügt dieser Befehl ein `prepare`-Skript zu deiner `package.json` hinzu. Dieses Skript stellt sicher, dass Husky nach jeder `npm install`-Ausführung korrekt installiert wird, was für die Zusammenarbeit im Team unerlässlich ist.

**3. Den Pre-Commit Hook erstellen**

Jetzt erstellst du den eigentlichen Hook. Du weist Husky an, vor jedem Commit den Befehl `npx lint-staged` auszuführen.

```bash
npx husky add .husky/pre-commit "npx lint-staged"
```

Dieser Befehl erzeugt eine neue Datei unter `.husky/pre-commit`. Anders als der ursprüngliche `.git/hooks`-Ordner ist dieser `.husky`-Ordner Teil deines Projekts und wird mit Git versioniert.

**4. `lint-staged` konfigurieren**

Der letzte Schritt ist die Konfiguration von `lint-staged`. Du musst ihm sagen, welche Befehle für welche Dateitypen ausgeführt werden sollen. Dies geschieht am einfachsten direkt in deiner `package.json`.

```json
// package.json
{
  // ... andere Konfigurationen
  "lint-staged": {
    "*.{js,jsx}": [
      "eslint --fix",
      "prettier --write"
    ],
    "*.{html,css,scss,md}": "prettier --write"
  }
}
```

Schauen wir uns diese Konfiguration genauer an:

*   `"*.{js,jsx}"`: Dies ist ein sogenannter "Glob-Pattern". Er zielt auf alle Dateien mit der Endung `.js` oder `.jsx` ab, die sich in der Staging Area befinden.
*   `["eslint --fix", "prettier --write"]`: Für diese JavaScript-Dateien werden zwei Befehle nacheinander ausgeführt. Zuerst versucht ESLint, Probleme automatisch zu beheben (`--fix`). Anschließend formatiert Prettier die Dateien (`--write`).
*   `"*.{html,css,scss,md}"`: Dieser Pattern wählt HTML-, CSS-, SCSS- und Markdown-Dateien aus.
*   `"prettier --write"`: Diese Dateien werden einfach durch Prettier formatiert.

#### Der Arbeitsablauf in der Praxis

Was passiert nun, wenn du versuchst, Code zu committen?

1.  Du änderst einige Dateien (z. B. eine `index.html` und ein `script.js`).
2.  Du fügst deine Änderungen zur Staging Area hinzu: `git add index.html script.js`.
3.  Du startest den Commit-Vorgang: `git commit -m "Neue Funktion implementiert"`.

Jetzt greift die Automatisierung:

*   **Trigger:** Git erkennt den `pre-commit`-Hook und führt das Skript in `.husky/pre-commit` aus.
*   **Husky & Lint-Staged:** Dieses Skript startet `npx lint-staged`.
*   **Ausführung:** `lint-staged` prüft seine Konfiguration.
    *   Es findet die `script.js` in der Staging Area und führt darauf `eslint --fix` und `prettier --write` aus.
    *   Es findet die `index.html` und führt darauf `prettier --write` aus.
*   **Ergebnis:**
    *   **Fall A (Erfolg):** Wenn alle Befehle ohne Fehler durchlaufen (z. B. weil Prettier eine fehlende Einrückung korrigiert hat oder ESLint keine Fehler fand), schließt `lint-staged` erfolgreich ab. Die automatisch korrigierten Dateien werden dem Commit hinzugefügt, und der Commit-Vorgang wird fortgesetzt. Du wirst aufgefordert, deine Commit-Nachricht einzugeben, und der Commit wird erfolgreich erstellt – mit perfekt formatiertem und fehlerfreiem Code.
    *   **Fall B (Fehlschlag):** Wenn ESLint einen Fehler findet, den es nicht automatisch beheben kann (z. B. eine unbenutzte Variable), gibt der `eslint`-Befehl einen Fehlercode zurück. `lint-staged` erkennt diesen Fehler, bricht den gesamten Prozess ab und zeigt dir die Fehlermeldung von ESLint direkt in deinem Terminal an. Der Commit wird *nicht* erstellt. Du bist gezwungen, den Fehler manuell zu beheben, die Datei erneut zu `add`en und den Commit neu zu starten.

#### Der unschätzbare Wert von Pre-Commit Hooks

Durch die Automatisierung dieser Qualitätsprüfungen erreichst du mehrere wichtige Ziele. Du stellst sicher, dass kein fehlerhafter oder schlecht formatierter Code versehentlich in die Codebasis gelangt. Dies führt zu einer viel saubereren und konsistenteren Git-Historie, da du keine nachfolgenden Commits mit Nachrichten wie "Code-Formatierung korrigiert" oder "Linter-Fehler behoben" mehr benötigst.

Vor allem aber entlastet es dich und dein Team von der mentalen Last, ständig an diese manuellen Überprüfungen denken zu müssen. Die Qualitätssicherung wird zu einem unsichtbaren, aber verlässlichen Teil des Entwicklungsprozesses. Du kannst dich voll und ganz auf das Schreiben von Code und das Lösen von Problemen konzentrieren, im Vertrauen darauf, dass dein automatischer Qualitätswächter im Hintergrund wacht und sicherstellt, dass nur erstklassiger Code seinen Weg in das Repository findet.
