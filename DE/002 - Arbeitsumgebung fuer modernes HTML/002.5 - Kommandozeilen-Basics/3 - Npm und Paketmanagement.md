# npm und Paketmanagement

### npm und Paketmanagement

Stell dir vor, du baust ein komplexes Modell aus Legosteinen. Du könntest jeden einzelnen Stein selbst herstellen – das wäre jedoch unglaublich aufwendig. Viel schlauer ist es, auf fertige Bausteine von Lego zurückzugreifen. Du suchst dir einfach die passenden Teile aus dem Katalog aus, bestellst sie, und sie werden dir geliefert. Du musst nur noch wissen, welche Teile du brauchst, und sie zusammenfügen.

In der Welt der Webentwicklung ist das ganz ähnlich. Du musst nicht jede Funktion, jede Animation oder jedes Hilfsprogramm von Grund auf neu schreiben. Eine riesige Gemeinschaft von Entwicklerinnen und Entwicklern hat bereits unzählige wiederverwendbare Codeteile – sogenannte **Pakete** oder **Module** – erstellt und teilt sie öffentlich. Das können kleine Helfer sein, die das Datum formatieren, oder komplexe Bibliotheken, die 3D-Grafiken im Browser ermöglichen.

Hier kommt das Paketmanagement ins Spiel. Ein Paketmanager ist ein Werkzeug, das dir hilft, diese externen Codeteile (die "Legosteine") für dein Projekt zu finden, zu installieren, zu verwalten und auf dem neuesten Stand zu halten. Für die JavaScript-Welt, und damit auch für die moderne HTML- und CSS-Entwicklung, ist der mit Abstand wichtigste Paketmanager **npm**.

#### Was ist npm?

npm steht für **Node Package Manager**. Es besteht aus zwei Kernkomponenten:

1.  **Ein Kommandozeilen-Werkzeug (CLI):** Das ist das Programm `npm`, das du in deinem Terminal ausführst. Du nutzt es, um Pakete zu installieren, zu deinstallieren oder deine Projekt-Skripte auszuführen. Wenn du Node.js installierst, wird npm automatisch mitinstalliert.
2.  **Ein Online-Register (Registry):** Dies ist eine riesige, öffentliche Datenbank unter [npmjs.com](https://www.npmjs.com), in der Hunderttausende von Open-Source-Paketen gespeichert sind. Man kann es sich wie einen gigantischen App-Store für Code vorstellen. Wenn du `npm install` ausführst, kontaktiert das CLI-Werkzeug dieses Register, um das gewünschte Paket herunterzuladen.

Auch wenn du "nur" HTML und CSS schreibst, wirst du schnell mit Werkzeugen in Berührung kommen, die npm benötigen. Denk an Tools zur Code-Formatierung (wie Prettier), zur CSS-Optimierung (wie PostCSS) oder sogar an kleine lokale Webserver, um deine Seite live im Browser zu sehen. npm ist das Tor zu diesem modernen Entwickler-Ökosystem.

#### Das Herz deines Projekts: die `package.json`

Jedes Projekt, das npm nutzt, hat eine zentrale Konfigurationsdatei: die `package.json`. Sie ist das Gehirn und das Gedächtnis deines Projekts. Du kannst sie dir wie die Bauanleitung und die Teileliste für dein Lego-Modell vorstellen. In dieser Datei im JSON-Format wird alles Wichtige festgehalten:

*   **Metadaten:** Name des Projekts, Version, Beschreibung, Autor, etc.
*   **Abhängigkeiten (Dependencies):** Eine exakte Liste aller externen Pakete, die dein Projekt zum Laufen benötigt.
*   **Entwicklungsabhängigkeiten (Dev Dependencies):** Eine Liste von Paketen, die du nur während der Entwicklung brauchst (z. B. Test-Tools, Code-Formatierer), aber nicht im fertigen Produkt.
*   **Skripte (Scripts):** Abkürzungen für häufig genutzte Kommandozeilen-Befehle, um deinen Arbeitsablauf zu vereinfachen.

Um eine `package.json` für ein neues Projekt zu erstellen, navigierst du in deinem Terminal in den Projektordner und führst den folgenden Befehl aus:

```bash
npm init
```

npm stellt dir daraufhin einige Fragen (Projektname, Version, etc.). Du kannst die meisten davon einfach mit der Enter-Taste bestätigen. Wenn du diesen Prozess beschleunigen und einfach die Standardwerte übernehmen möchtest, kannst du ein `-y` (für "yes") Flag anhängen:

```bash
npm init -y
```

Danach findest du in deinem Ordner eine neue Datei namens `package.json`, die in etwa so aussieht:

```json
{
  "name": "mein-html-projekt",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

Diese Datei ist nun bereit, mit Leben gefüllt zu werden.

#### Pakete installieren und verwalten

Der häufigste Anwendungsfall für npm ist die Installation von Paketen. Nehmen wir an, du möchtest dein Projekt mit **Prettier**, einem sehr populären Code-Formatierer, ausstatten. Prettier ist ein typisches Entwicklungswerkzeug – es hilft dir beim Schreiben von sauberem Code, wird aber nicht Teil deiner fertigen Webseite sein. Daher installierst du es als "Dev Dependency".

Der Befehl dafür lautet:

```bash
npm install prettier --save-dev
```

Lass uns diesen Befehl zerlegen:
*   `npm install`: Der Kernbefehl, um ein Paket zu installieren. Du kannst auch die Kurzform `npm i` verwenden.
*   `prettier`: Der Name des Pakets, das du aus dem npm-Register herunterladen möchtest.
*   `--save-dev`: Dieses Flag teilt npm mit, dass es sich um eine Entwicklungsabhängigkeit handelt. npm wird daraufhin einen Eintrag im `devDependencies`-Abschnitt deiner `package.json` anlegen. Für Pakete, die deine Webseite zur Laufzeit benötigt (z. B. eine JavaScript-Bibliothek für Animationen), würdest du das Flag weglassen oder `--save` verwenden, was sie als normale `dependencies` speichert.

Nachdem du den Befehl ausgeführt hast, passieren drei wichtige Dinge:
1.  Ein neuer Ordner namens `node_modules` wird in deinem Projekt erstellt. In diesem Ordner legt npm den gesamten Code für `prettier` und alle Pakete, von denen `prettier` selbst abhängig ist, ab. Dieser Ordner kann sehr groß werden und sollte **niemals** in ein Git-Repository eingecheckt werden.
2.  Deine `package.json` wird aktualisiert und enthält nun einen neuen Abschnitt:

    ```json
    {
      ...
      "devDependencies": {
        "prettier": "^2.8.8"
      }
    }
    ```
3.  Eine neue Datei namens `package-lock.json` wird erstellt.

#### Die Rolle von `node_modules` und `package-lock.json`

Der `node_modules`-Ordner ist quasi dein lokales Lager für alle heruntergeladenen "Legosteine". Wenn du dein Projekt an jemand anderen weitergibst, schickst du diesen riesigen Ordner nicht mit. Stattdessen gibst du nur die `package.json` und die `package-lock.json` weiter. Die andere Person kann dann in ihrem Terminal einfach `npm install` ausführen, und npm wird anhand dieser beiden Dateien den `node_modules`-Ordner mit exakt denselben Paketen in exakt denselben Versionen wiederherstellen.

Das ist die Magie des Paketmanagements: Die `package.json` sagt, *welche* Pakete du brauchst, und die `package-lock.json` friert die *exakten Versionen* dieser Pakete ein. Die `package-lock.json` ist extrem wichtig, denn sie garantiert, dass das Projekt heute, in einem Monat und auf dem Computer deines Teamkollegen exakt gleich funktioniert. Sie verhindert das klassische "Aber bei mir läuft's!"-Problem.

#### Nützliche npm-Befehle im Überblick

Hier sind einige weitere Befehle, die dir im Alltag begegnen werden:

*   **Pakete deinstallieren:** Wenn du ein Paket nicht mehr benötigst, kannst du es mit `uninstall` entfernen.
    ```bash
    npm uninstall prettier --save-dev
    ```
*   **Pakete aktualisieren:** Um alle Pakete auf die neuesten Versionen zu aktualisieren, die laut `package.json` erlaubt sind:
    ```bash
    npm update
    ```
*   **Installierte Pakete anzeigen:** Um eine Baumansicht aller installierten Pakete zu sehen:
    ```bash
    npm list
    ```

#### Die Macht der npm Scripts

Eines der mächtigsten Features von npm ist die Möglichkeit, eigene Skripte zu definieren. Im `scripts`-Abschnitt deiner `package.json` kannst du Kürzel für längere oder wiederkehrende Kommandozeilenbefehle anlegen.

Erinnerst du dich an unseren Code-Formatierer Prettier? Anstatt jedes Mal den langen Befehl zum Formatieren deiner Dateien einzutippen, können wir ein Skript dafür anlegen. Öffne deine `package.json` und ändere den `scripts`-Teil wie folgt:

```json
"scripts": {
  "format": "prettier --write ."
},
```

Hier haben wir ein neues Skript namens `format` erstellt. Der Befehl `prettier --write .` weist Prettier an, alle Dateien im aktuellen Verzeichnis (`.`) zu finden und automatisch zu formatieren (`--write`).

Um dieses Skript nun auszuführen, tippst du in dein Terminal:

```bash
npm run format
```

npm sucht nun in deiner `package.json` nach dem Skript `format` und führt den dazugehörigen Befehl für dich aus. Das ist unglaublich praktisch, um Arbeitsabläufe zu automatisieren. Du könntest Skripte für das Starten eines Entwicklungsservers (`npm run start`), das Optimieren von CSS (`npm run build:css`) oder viele andere Aufgaben erstellen.

#### Globale vs. lokale Pakete

Bisher haben wir Pakete immer lokal in einem Projekt installiert. Das ist der Standard und in 99 % der Fälle die richtige Vorgehensweise. Jedes Projekt hat so seine eigenen, unabhängigen Abhängigkeiten im `node_modules`-Ordner.

In seltenen Fällen möchte man ein Kommandozeilen-Werkzeug aber systemweit verfügbar machen, unabhängig vom aktuellen Projekt. In diesem Fall kann man ein Paket "global" installieren, indem man das `-g` Flag verwendet:

```bash
npm install -g http-server
```

Das Paket `http-server` ist ein gutes Beispiel. Es startet einen einfachen Webserver in jedem beliebigen Ordner. Nach der globalen Installation kannst du von überall in deinem Terminal den Befehl `http-server` ausführen.

Sei jedoch vorsichtig mit globalen Installationen. Für Projekt-Abhängigkeiten solltest du sie unbedingt vermeiden, da sie zu schwer nachvollziehbaren Versionierungskonflikten führen können. Die goldene Regel lautet: **Installiere Pakete immer lokal, es sei denn, es ist ein reines Kommandozeilen-Werkzeug, das du systemweit wie eine eigenständige Anwendung nutzen möchtest.**

Mit npm hast du einen mächtigen Verbündeten an deiner Seite. Es automatisiert die mühsame Verwaltung von Code-Abhängigkeiten und öffnet dir die Tür zu einem riesigen Universum von Werkzeugen und Bibliotheken, die deine Arbeit als Webentwickler einfacher, schneller und professioneller machen.
