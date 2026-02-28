# Einrichtung mit Node.js oder Python

### Der lokale Entwicklungsserver: Deine Werkbank mit Node.js oder Python

Wenn du eine HTML-Datei erstellst und sie einfach per Doppelklick in deinem Browser öffnest, siehst du in der Adressleiste etwas wie `file:///C:/Users/DeinName/Projekt/index.html`. Das `file://`-Protokoll zeigt an, dass der Browser direkt auf eine lokale Datei zugreift. Für einfache, in sich geschlossene HTML-Seiten mag das ausreichen. Sobald deine Projekte jedoch komplexer werden, stößt dieser Ansatz schnell an seine Grenzen.

Moderne Webentwicklung nutzt Techniken wie JavaScript-Module, API-Anfragen (Fetching Data) oder Service Worker. Aus Sicherheitsgründen schränken Browser die Funktionalität von Skripten ein, die über das `file://`-Protokoll geladen werden. Ein klassisches Beispiel ist die "Cross-Origin Resource Sharing" (CORS) Policy, die verhindert, dass eine Datei von deiner Festplatte auf eine andere Ressource zugreift, selbst wenn diese im selben Ordner liegt.

Um diese Einschränkungen zu umgehen und eine Umgebung zu schaffen, die einem echten Webserver im Internet gleicht, benötigst du einen lokalen Entwicklungsserver. Dieser Server läuft nur auf deinem Computer und "serviert" deine Dateien über das `http://`-Protokoll, meist unter einer Adresse wie `http://localhost:8080`. Dadurch verhält sich dein Browser so, als würde er auf eine echte Webseite zugreifen, und alle modernen Web-Funktionen stehen dir zur Verfügung.

Glücklicherweise musst du dafür keinen komplexen Webserver wie Apache oder Nginx installieren. Es gibt einfache, kommandozeilenbasierte Werkzeuge, die diese Aufgabe mit einem einzigen Befehl erledigen. Zwei der populärsten und zugänglichsten Wege führen über Node.js und Python. Beide Ansätze sind fantastisch für die HTML-Entwicklung geeignet, unterscheiden sich aber in den Details.

#### Die Node.js-Variante: Modern und komfortabel mit `live-server`

Node.js ist eine Laufzeitumgebung, die es ermöglicht, JavaScript-Code außerhalb eines Webbrowsers auszuführen – also direkt auf deinem Computer. Es hat sich zu einem Eckpfeiler der modernen Webentwicklung entwickelt und bringt einen unschätzbaren Begleiter mit: den Node Package Manager (npm). `npm` ist ein riesiges Ökosystem von kostenlosen, wiederverwendbaren Code-Paketen, die du für deine Projekte nutzen kannst. Eines dieser Pakete ist perfekt für unseren Zweck.

**1. Installation von Node.js**

Falls du Node.js noch nicht installiert hast, ist der erste Schritt der Besuch der offiziellen Webseite unter [nodejs.org](https://nodejs.org/). Dort findest du zwei Hauptversionen zum Download: LTS (Long-Term Support) und Current. Für den Einstieg und eine stabile Arbeitsumgebung ist die **LTS-Version** immer die beste Wahl. Lade den Installer für dein Betriebssystem herunter und folge den Installationsanweisungen. Die Standardeinstellungen sind in der Regel vollkommen ausreichend. Nach der Installation sind sowohl `node` als auch `npm` in deiner Kommandozeile (Terminal, PowerShell, etc.) verfügbar.

Du kannst die erfolgreiche Installation überprüfen, indem du dein Terminal öffnest und folgende Befehle eingibst:

```bash
node -v
npm -v
```

Beide Befehle sollten dir eine Versionsnummer zurückgeben.

**2. Installation von `live-server`**

Nun, da `npm` bereitsteht, können wir das Werkzeug installieren, das uns den magischen lokalen Server bereitstellt: `live-server`. Dieses Paket tut genau das, was sein Name verspricht: Es startet einen Server und überwacht deine Dateien. Sobald du eine HTML-, CSS- oder JavaScript-Datei speicherst, lädt der Server die Seite im Browser automatisch neu. Dieses "Live Reloading" ist ein enormer Gewinn für die Produktivität, da du deine Änderungen sofort und ohne manuelles Aktualisieren siehst.

Um `live-server` zu installieren, öffne dein Terminal und gib folgenden Befehl ein:

```bash
npm install -g live-server
```

Lass uns diesen Befehl kurz aufschlüsseln:
*   `npm install`: Dies ist der Standardbefehl, um ein Paket zu installieren.
*   `-g`: Diese Flagge steht für "global". Das bedeutet, `live-server` wird nicht nur für ein spezifisches Projekt, sondern systemweit installiert. Dadurch kannst du den `live-server`-Befehl von jedem beliebigen Ordner auf deinem Computer ausführen.
*   `live-server`: Der Name des Pakets, das wir installieren möchten.

**3. Den Server starten**

Die Nutzung ist denkbar einfach. Navigiere in deinem Terminal mit dem `cd`-Befehl (change directory) in den Ordner deines HTML-Projekts. Angenommen, dein Projekt liegt unter `~/Dokumente/mein-html-projekt`, würdest du Folgendes tun:

```bash
cd ~/Dokumente/mein-html-projekt
```

Sobald du dich im richtigen Verzeichnis befindest, in dem deine `index.html` liegt, startest du den Server mit einem einzigen Wort:

```bash
live-server
```

Das war's schon! Im Terminal siehst du eine Ausgabe, die dir mitteilt, dass der Server gestartet wurde, normalerweise auf Port 8080. Gleichzeitig sollte sich automatisch ein neues Browserfenster öffnen, das deine `index.html`-Datei unter der Adresse `http://127.0.0.1:8080` anzeigt. (`127.0.0.1` ist eine andere Schreibweise für `localhost`).

Wenn du jetzt eine deiner Projektdateien in deinem Code-Editor änderst und speicherst, wird die Seite im Browser wie von Geisterhand aktualisiert.

#### Die Python-Variante: Der minimalistische Bordcomputer

Python ist eine unglaublich vielseitige und beliebte Programmiersprache. Eine ihrer Stärken ist die umfangreiche Standardbibliothek, die viele nützliche Module direkt mitliefert. Eines dieser Module kann einen einfachen HTTP-Server starten – ganz ohne die Installation zusätzlicher Pakete.

**1. Verfügbarkeit von Python prüfen**

Auf macOS und den meisten Linux-Distributionen ist Python bereits vorinstalliert. Windows-Nutzer müssen es möglicherweise manuell installieren. Besuche dazu die offizielle Webseite unter [python.org](https://python.org/) und lade dir die neueste Version herunter. Wichtig bei der Installation unter Windows: Setze unbedingt das Häkchen bei der Option "Add Python to PATH". Dies stellt sicher, dass du den `python`-Befehl von überall in der Kommandozeile ausführen kannst.

Um zu prüfen, ob Python verfügbar ist und welche Version du hast, öffne dein Terminal und gib Folgendes ein:

```bash
python3 --version
```

Möglicherweise funktioniert auf älteren Systemen oder bei bestimmten Konfigurationen auch dieser Befehl:

```bash
python --version
```

Der Unterschied ist wichtig, denn der Befehl zum Starten des Servers variiert zwischen Python 2 und Python 3. Da Python 2 seit 2020 nicht mehr offiziell unterstützt wird, solltest du idealerweise Python 3 verwenden.

**2. Den Server starten**

Ähnlich wie bei der Node.js-Variante navigierst du zuerst in dein Projektverzeichnis:

```bash
cd ~/Dokumente/mein-html-projekt
```

Bist du im richtigen Ordner, unterscheidet sich der Befehl je nach deiner Python-Version.

**Für Python 3 (die empfohlene Version):**

```bash
python3 -m http.server
```

**Für Python 2 (falls du aus irgendeinem Grund eine ältere Version verwendest):**

```bash
python -m SimpleHTTPServer
```

Was passiert hier?
*   `python3` oder `python` ruft den Python-Interpreter auf.
*   Die Flagge `-m` weist Python an, ein Modul als Skript auszuführen.
*   `http.server` (bzw. `SimpleHTTPServer` in Python 2) ist der Name des eingebauten Moduls, das den Webserver bereitstellt.

Nachdem du den Befehl ausgeführt hast, siehst du im Terminal eine Nachricht wie `Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/)`.

Im Gegensatz zu `live-server` öffnet sich hier nicht automatisch ein Browserfenster. Du musst deinen Browser manuell öffnen und die Adresse `http://localhost:8000` (oder `http://127.0.0.1:8000`) eingeben, um deine Seite zu sehen. Der größte Unterschied ist jedoch, dass dieser einfache Server kein Live Reloading unterstützt. Wenn du eine Datei änderst, musst du die Seite im Browser manuell neu laden (mit F5 oder Cmd+R), um die Änderungen zu sehen.

#### Welchen Weg solltest du wählen?

Beide Methoden führen zum Ziel und stellen dir einen funktionierenden lokalen Webserver zur Verfügung. Die Wahl hängt von deinen Vorlieben und Gegebenheiten ab.

*   **Wähle die Node.js-Variante mit `live-server`**, wenn du einen modernen, komfortablen Workflow bevorzugst. Das automatische Neuladen spart unglaublich viel Zeit und macht den Entwicklungsprozess flüssiger und angenehmer. Wenn du ohnehin planst, dich tiefer mit moderner Webentwicklung (z. B. mit Frameworks wie React, Vue oder Tools wie Webpack) zu beschäftigen, ist die Installation von Node.js ein unvermeidlicher und sinnvoller erster Schritt.

*   **Wähle die Python-Variante**, wenn du eine schnelle, unkomplizierte Lösung ohne zusätzliche Installationen suchst. Wenn Python bereits auf deinem System ist, kannst du sofort loslegen. Dieser Weg ist perfekt, um schnell ein kleines Projekt zu testen oder wenn du auf einem fremden Rechner arbeitest, auf dem du nichts installieren möchtest oder darfst. Der fehlende Komfort des Live Reloading ist der einzige nennenswerte Nachteil.

Für ernsthafte und längere HTML-, CSS- und JavaScript-Projekte ist der durch `live-server` gebotene Komfort kaum zu übertreffen. Für den schnellen Test zwischendurch ist der eingebaute Python-Server jedoch ein unschlagbar schlankes Werkzeug. Am Ende sind beide exzellente Optionen, um die Fesseln des `file://`-Protokolls zu sprengen und deine Webprojekte in einer realistischen Umgebung zu entwickeln.
