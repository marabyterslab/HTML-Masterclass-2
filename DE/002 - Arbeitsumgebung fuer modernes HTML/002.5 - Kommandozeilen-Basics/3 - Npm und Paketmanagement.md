# npm und Paketmanagement

### npm und Paketmanagement

Wenn du beginnst, in der modernen Webentwicklung zu arbeiten, wirst du schnell feststellen, dass du selten alles von Grund auf neu erfindest. Stattdessen baust du auf der Arbeit unzähliger anderer Entwicklerinnen und Entwickler auf. Du nutzt fertige Code-Bausteine – sogenannte Pakete – für Aufgaben wie das Erstellen eines Bilder-Sliders, das Formatieren von Daten oder das Verwalten des Anwendungszustands. Doch wie behältst du den Überblick über all diese externen Code-Teile in deinem Projekt? Wie stellst du sicher, dass sie in der richtigen Version vorhanden sind und wie installierst du sie überhaupt? Hier kommen Paketmanager ins Spiel, und der bei Weitem populärste in der Welt von JavaScript ist **npm**.

#### Was ist npm eigentlich?

npm steht für **Node Package Manager**. Wie der Name schon verrät, ist es eng mit Node.js verbunden. Node.js ist eine Laufzeitumgebung, die es ermöglicht, JavaScript-Code außerhalb eines Webbrowsers auszuführen, also direkt auf deinem Computer. Wenn du Node.js installierst, wird npm automatisch mitinstalliert.

npm selbst besteht aus zwei Hauptkomponenten:

1.  **Ein Kommandozeilen-Tool (CLI):** Das ist das Programm, das du in deinem Terminal aufrufst, um Pakete zu installieren, zu aktualisieren oder zu verwalten. Wenn du `npm install` eingibst, interagierst du mit diesem Tool.
2.  **Ein Online-Register (npm Registry):** Dies ist eine riesige, öffentliche Datenbank mit hunderttausenden von Open-Source-Paketen. Du kannst sie dir wie einen gigantischen App-Store für Entwickler vorstellen. Wenn du ein Paket installierst, lädt das npm-CLI es von diesem Register herunter.

Ein "Paket" ist dabei einfach ein Ordner mit Code und einer speziellen Datei, die es beschreibt. Es kann eine kleine Hilfsfunktion, eine komplexe Bibliothek wie React oder ein komplettes Framework sein.

#### Das Herzstück deines Projekts: die `package.json`

Bevor du auch nur ein einziges Paket installierst, solltest du deinem Projekt eine Art Ausweis oder eine "Stückliste" geben. Diese zentrale Konfigurationsdatei heißt `package.json`. Sie ist eine einfache Textdatei im JSON-Format (JavaScript Object Notation) und enthält alle wichtigen Metadaten über dein Projekt.

Um eine `package.json`-Datei in deinem Projektordner zu erstellen, öffnest du dein Terminal, navigierst in den Ordner und führst den folgenden Befehl aus:

```bash
npm init
```

Dieses Kommando startet einen interaktiven Assistenten, der dich nach einigen Informationen fragt, wie dem Namen deines Projekts, der Version, einer Beschreibung und dem Autor. Du kannst die meisten Fragen einfach mit der Enter-Taste bestätigen, um die Standardwerte zu übernehmen. Wenn du den Prozess beschleunigen möchtest, kannst du auch die `-y`-Flagge verwenden, die automatisch für alle Fragen "Ja" antwortet:

```bash
npm init -y
```

Danach findest du in deinem Projektordner eine neue Datei namens `package.json`, die etwa so aussehen könnte:

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

Diese Datei ist der Dreh- und Angelpunkt für npm. Sie listet nicht nur allgemeine Informationen auf, sondern wird auch festhalten, welche Pakete dein Projekt benötigt.

#### Pakete installieren: Abhängigkeiten verwalten

Stellen wir uns vor, du möchtest eine Bibliothek namens `lodash` verwenden, die viele nützliche Hilfsfunktionen für JavaScript bereitstellt. Um sie zu deinem Projekt hinzuzufügen, nutzt du den Befehl `npm install`:

```bash
npm install lodash
```

Wenn du diesen Befehl ausführst, passieren mehrere Dinge im Hintergrund:

1.  npm kontaktiert das npm-Register und sucht nach dem Paket `lodash`.
2.  Es lädt die neueste stabile Version des Pakets herunter.
3.  Es erstellt einen neuen Ordner in deinem Projekt namens `node_modules`. In diesem Ordner wird der gesamte Code von `lodash` (und eventuellen Paketen, von denen `lodash` selbst abhängt) abgelegt.
4.  Es aktualisiert deine `package.json`-Datei und fügt `lodash` unter einem neuen Abschnitt namens `dependencies` hinzu.

Deine `package.json` sieht danach in etwa so aus:

```json
{
  "name": "mein-html-projekt",
  "version": "1.0.0",
  ...
  "dependencies": {
    "lodash": "^4.17.21"
  }
}
```

Der `dependencies`-Abschnitt listet alle Pakete auf, die dein Projekt zum Laufen benötigt. Das kleine Hütchen-Symbol (`^`) vor der Versionsnummer ist Teil der "semantischen Versionierung" (SemVer) und bedeutet, dass npm bei zukünftigen Installationen auch neuere, kompatible Versionen installieren darf.

#### Entwicklungsabhängigkeiten vs. Produktionsabhängigkeiten

Manche Werkzeuge benötigst du nur während der Entwicklung, aber nicht für die fertige Website, die du am Ende online stellst. Beispiele dafür sind Tools zum automatischen Neuladen der Seite im Browser (Live-Server), zur Code-Formatierung (Prettier) oder zum Kompilieren von SASS zu CSS.

Solche Pakete werden als "Entwicklungsabhängigkeiten" (Dev Dependencies) installiert. Du verwendest dafür die `--save-dev`-Flagge (oder die Kurzform `-D`):

```bash
npm install prettier --save-dev
```

Dieser Befehl tut im Grunde dasselbe wie der vorherige, aber er fügt `prettier` zu einem separaten Abschnitt namens `devDependencies` in deiner `package.json` hinzu. Dies signalisiert anderen Entwicklern (und automatisierten Systemen), dass dieses Paket nicht Teil des finalen Produkts sein muss.

#### Die Magie von `npm install` ohne Paketnamen

Jetzt kommt der wirklich smarte Teil des Paketmanagements. Der `node_modules`-Ordner kann sehr, sehr groß werden, da er den Code aller Pakete und deren Abhängigkeiten enthält. Es ist daher eine goldene Regel, diesen Ordner **niemals** in ein Versionskontrollsystem wie Git einzuchecken.

Stattdessen teilst du nur deine `package.json`-Datei. Wenn nun ein Kollege dein Projekt herunterlädt, enthält es keinen `node_modules`-Ordner. Wie bekommt er all die benötigten Pakete? Ganz einfach: Er navigiert im Terminal in den Projektordner und führt `npm install` aus, aber diesmal **ohne einen Paketnamen anzugeben**:

```bash
npm install
```

npm liest nun die `dependencies` und `devDependencies` aus der `package.json`-Datei aus und installiert automatisch alle dort aufgeführten Pakete in den exakt benötigten Versionen. So kann jeder im Team mit einem einzigen Befehl die exakt gleiche Arbeitsumgebung herstellen.

#### Die `package-lock.json`: Exakte Versionen garantieren

Du hast vielleicht bemerkt, dass npm nach der ersten Installation eine weitere Datei erstellt hat: `package-lock.json`. Diese Datei solltest du, anders als `node_modules`, unbedingt mit in dein Versionskontrollsystem aufnehmen.

Was macht sie? Während die `package.json` oft flexible Versionsbereiche angibt (z. B. `^4.17.21`), zeichnet die `package-lock.json` die **exakte** Version jedes einzelnen installierten Pakets und Unter-Pakets auf. Sie ist wie ein detaillierter Lieferschein deines `node_modules`-Ordners.

Das ist extrem wichtig für die Reproduzierbarkeit. Sie stellt sicher, dass jeder Entwickler im Team und auch der Build-Server auf dem Webhoster exakt dieselbe Codebasis verwendet. Das verhindert die gefürchteten "Aber bei mir funktioniert es!"-Probleme, die durch subtile Unterschiede in den Paketversionen entstehen können. Wenn `npm install` ausgeführt wird und eine `package-lock.json` vorhanden ist, wird diese als primäre Quelle für die Installation verwendet.

#### Weitere nützliche npm-Befehle

Das npm-Kommandozeilen-Tool ist sehr mächtig. Hier sind einige weitere Befehle, die dir im Alltag begegnen werden:

*   **Pakete aktualisieren:** `npm update`
    Dieser Befehl prüft, ob es für deine Pakete neuere Versionen gibt, die den in der `package.json` definierten Regeln (z. B. dem `^`) entsprechen, und aktualisiert sie.

*   **Pakete deinstallieren:** `npm uninstall <paketname>`
    Dieser Befehl entfernt ein Paket aus deinem `node_modules`-Ordner und aus deiner `package.json`.

*   **Skripte ausführen:** `npm run <skriptname>`
    In der `package.json` gibt es einen `scripts`-Bereich. Hier kannst du eigene Kommandozeilen-Befehle für dein Projekt definieren. Ein typisches Beispiel wäre ein Skript zum Starten eines lokalen Entwicklungsservers:
    ```json
    "scripts": {
      "start": "live-server src/"
    }
    ```
    Du könntest dieses Skript dann einfach mit `npm run start` im Terminal ausführen. Das ist eine unglaublich nützliche Methode, um komplexe Build-Prozesse zu automatisieren und zu vereinfachen.

*   **Pakete ausführen ohne Installation:** `npx`
    `npx` ist ein Begleit-Tool von npm, das es dir erlaubt, ein Paket direkt aus dem npm-Register auszuführen, ohne es permanent in deinem Projekt installieren zu müssen. Das ist ideal für Werkzeuge, die man nur einmalig benötigt, wie zum Beispiel das Erstellen eines neuen Projekts mit einem Framework-Generator. Ein bekanntes Beispiel ist `create-react-app`:
    ```bash
    npx create-react-app mein-neues-projekt
    ```
    Dieser Befehl lädt `create-react-app` temporär herunter, führt es aus und verwirft es danach wieder.

npm ist weit mehr als nur ein Werkzeug zum Herunterladen von Code. Es ist das Fundament, auf dem moderne JavaScript-Projekte aufgebaut sind. Es ermöglicht dir, auf einfache Weise auf das riesige Ökosystem von Open-Source-Modulen zuzugreifen, deine Projekt-Abhängigkeiten sauber zu verwalten und deine Arbeitsabläufe zu automatisieren. Wenn du die Grundlagen von `npm init`, `npm install` und der Rolle der `package.json` verstanden hast, hast du einen entscheidenden Schritt in die Welt der professionellen Webentwicklung gemacht.
