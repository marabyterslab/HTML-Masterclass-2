# Einrichtung mit Node.js oder Python

### Dein lokaler Entwicklungsserver: Schnellstart mit Node.js oder Python

Wenn du eine HTML-Datei erstellst und sie einfach per Doppelklick in deinem Browser öffnest, siehst du in der Adresszeile etwas wie `file:///C:/Users/DeinName/Dokumente/mein-projekt/index.html`. Das funktioniert für sehr einfache, in sich geschlossene Seiten. Sobald du aber beginnst, mit moderneren Web-Techniken zu arbeiten – wie zum Beispiel JavaScript-Module zu laden oder Daten von einer anderen Datei abzurufen (sogenannte API-Anfragen) – stößt dieser Ansatz an seine Grenzen. Browser haben aus Sicherheitsgründen strenge Regeln, was eine lokale Datei (`file:///`) darf und was nicht. Die wichtigste dieser Regeln ist die „Same-Origin Policy“, die verhindert, dass eine Datei einfach so auf andere Dateien auf deinem Computer zugreift.

Um diese Einschränkungen zu umgehen und deine Webseite in einer Umgebung zu testen, die einer echten Website im Internet sehr nahekommt, benötigst du einen lokalen Webserver. Ein Webserver ist ein Programm, das auf Anfragen von einem Browser (wie `http://localhost:8080`) lauscht und die angeforderten Dateien – also dein HTML, CSS und JavaScript – über das HTTP-Protokoll zurücksendet. „Lokal“ bedeutet in diesem Fall, dass der Server direkt auf deinem eigenen Computer läuft und nur für dich erreichbar ist.

Glücklicherweise musst du dafür keinen komplexen Apache- oder Nginx-Server einrichten. Es gibt wunderbar einfache Werkzeuge, die du mit einer einzigen Kommandozeilenanweisung starten kannst. Zwei der beliebtesten und unkompliziertesten Wege basieren auf Technologien, die in der Webentwicklung ohnehin allgegenwärtig sind: Node.js und Python. Schauen wir uns beide Optionen an.

#### Die Variante mit Node.js

Node.js ist eine Laufzeitumgebung, die es dir erlaubt, JavaScript auch außerhalb eines Webbrowsers auszuführen – zum Beispiel auf einem Server. Es ist das Herzstück eines riesigen Ökosystems an Werkzeugen und Bibliotheken, die von Entwicklern weltweit genutzt werden. Wenn du planst, tiefer in die moderne Webentwicklung mit Frameworks wie React, Vue oder Angular einzutauchen, wirst du um Node.js ohnehin nicht herumkommen.

**1. Installation von Node.js**

Falls du Node.js noch nicht installiert hast, ist das der erste Schritt. Besuche die offizielle Webseite `nodejs.org` und lade die LTS-Version herunter. LTS steht für „Long Term Support“ und ist die stabile, für die meisten Nutzer empfohlene Version. Die Installation ist unkompliziert und folgt den üblichen Schritten eines Installationsprogramms für dein Betriebssystem (Windows, macOS oder Linux).

Mit der Installation von Node.js erhältst du automatisch auch `npm` (Node Package Manager). `npm` ist ein Kommandozeilen-Tool, mit dem du Pakete – also wiederverwendbare Code-Module und Werkzeuge – aus einem riesigen öffentlichen Register installieren und verwalten kannst.

**2. Installation eines einfachen HTTP-Servers**

Es gibt unzählige Pakete für Node.js, die einen einfachen Webserver bereitstellen. Eines der bekanntesten und einfachsten ist `http-server`. Um es zu installieren, öffnest du dein Terminal (oder die Eingabeaufforderung/PowerShell unter Windows) und gibst folgenden Befehl ein:

```bash
npm install -g http-server
```

Lass uns diesen Befehl kurz aufschlüsseln:
*   `npm install`: Dies ist der Befehl, um ein Paket zu installieren.
*   `-g`: Dies ist eine Option (ein sogenannter „Flag“) und steht für „global“. Das bedeutet, das Paket wird nicht nur in deinem aktuellen Projektordner, sondern systemweit installiert. Dadurch kannst du den Befehl `http-server` von jedem beliebigen Verzeichnis auf deinem Computer aus aufrufen.
*   `http-server`: Das ist der Name des Pakets, das du installieren möchtest.

**3. Den Server starten**

Nachdem die Installation abgeschlossen ist, kannst du den Server verwenden. Navigiere in deinem Terminal in den Ordner, in dem sich deine HTML-Dateien befinden. Angenommen, dein Projekt liegt unter `~/Dokumente/mein-html-projekt`, dann würdest du dorthin wechseln:

```bash
cd ~/Dokumente/mein-html-projekt
```

Sobald du im richtigen Verzeichnis bist, startest du den Server mit diesem simplen Befehl:

```bash
http-server
```

Das Terminal wird dir nun eine Ausgabe wie diese anzeigen:

```bash
Starting up http-server, serving ./
Available on:
  http://127.0.0.1:8080
  http://192.168.1.101:8080
Hit CTRL-C to stop the server
```

Dein lokaler Server läuft jetzt! Die Adresse `127.0.0.1` (oder auch `localhost`) ist die Standardadresse für deinen eigenen Computer. Der Teil nach dem Doppelpunkt, hier `8080`, ist der Port – sozusagen die „Wohnungsnummer“ auf der Adresse deines Computers, an die sich der Browser wendet.

Öffne nun deinen Webbrowser und gib `http://localhost:8080` in die Adresszeile ein. Du wirst entweder direkt deine `index.html` sehen (falls eine solche Datei in deinem Ordner existiert) oder eine Liste aller Dateien und Ordner deines Projekts, durch die du navigieren kannst.

Um den Server wieder zu stoppen, wechselst du zurück zum Terminal und drückst die Tastenkombination `Strg + C` (oder `Cmd + C` auf dem Mac).

#### Die Alternative mit Python

Wenn du bereits Python auf deinem System installiert hast – was bei macOS und den meisten Linux-Distributionen standardmäßig der Fall ist –, hast du bereits alles, was du brauchst. Python bringt ein eingebautes Modul mit, das einen einfachen HTTP-Server ohne jegliche zusätzliche Installation starten kann. Das macht diesen Weg zum schnellsten und unkompliziertesten, wenn du einfach nur schnell eine HTML-Datei testen willst.

**1. Überprüfen der Python-Installation**

Öffne dein Terminal und gib `python --version` oder `python3 --version` ein. Wenn eine Versionsnummer angezeigt wird, ist Python installiert. Wichtig ist hier die Unterscheidung zwischen Python 2 und Python 3, da sich der Befehl zum Starten des Servers leicht unterscheidet. Python 2 ist veraltet, aber auf manchen älteren Systemen noch vorhanden. Wir konzentrieren uns auf den modernen Weg mit Python 3.

Solltest du Python noch nicht installiert haben, findest du auf der offiziellen Webseite `python.org` die passende Version für dein Betriebssystem.

**2. Den Server starten**

Genau wie bei der Node.js-Variante navigierst du zuerst in deinem Terminal in den Projektordner, den du bereitstellen möchtest.

```bash
cd ~/Dokumente/mein-html-projekt
```

Bist du im richtigen Verzeichnis, startest du den Server mit folgendem Befehl (für Python 3):

```bash
python3 -m http.server
```

Falls du eine ältere Python-2-Version verwendest, lautet der Befehl:

```bash
python -m SimpleHTTPServer
```

Schauen wir uns auch diesen Befehl genauer an:
*   `python3`: Dies startet den Python-3-Interpreter.
*   `-m`: Dieser Flag weist Python an, ein Modul aus seiner Standardbibliothek als Skript auszuführen.
*   `http.server`: Das ist der Name des Moduls, das den Webserver enthält.

Nachdem du den Befehl ausgeführt hast, siehst du eine Meldung im Terminal, die dir mitteilt, auf welcher Adresse und welchem Port der Server lauscht. Standardmäßig ist dies Port `8000`.

```bash
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

Öffne nun deinen Browser und besuche die Adresse `http://localhost:8000`. Das Ergebnis ist das gleiche wie bei der Node.js-Variante: Du siehst deine Webseite oder eine Dateiliste. Auch hier beendest du den Server mit `Strg + C` im Terminal.

Möchtest du einen anderen Port verwenden, kannst du diesen einfach am Ende des Befehls angeben:

```bash
python3 -m http.server 9999
```

Dieser Befehl startet den Server auf Port `9999`.

#### Welche Methode ist die richtige für dich?

Beide Wege führen zum Ziel und sind für die Entwicklung von HTML-Seiten hervorragend geeignet. Die Wahl hängt oft von deinen persönlichen Vorlieben und deiner bereits vorhandenen Software ab.

*   **Wähle Python, wenn...**
    *   du Python bereits installiert hast und einfach nur den schnellstmöglichen Weg suchst, einen lokalen Server zu starten.
    *   du keine zusätzlichen Werkzeuge installieren möchtest und mit einem minimalistischen Server zufrieden bist.

*   **Wähle Node.js, wenn...**
    *   du ohnehin planst, in die moderne JavaScript-Entwicklung einzusteigen und dich mit `npm` und dem Node.js-Ökosystem vertraut machen möchtest.
    *   du einen etwas konfigurierbareren Server schätzt. `http-server` bietet beispielsweise einfache Optionen, um Caching zu deaktivieren oder den Server automatisch im Browser zu öffnen (`http-server -o`), was den Entwicklungsprozess weiter beschleunigen kann.

Für die Zwecke des Lernens von HTML, CSS und grundlegendem JavaScript sind beide Optionen absolut gleichwertig. Du richtest einmalig einen dieser Server ein und hast damit eine professionelle, realitätsnahe Testumgebung, die dir im weiteren Verlauf deiner Lernreise treue Dienste leisten wird.
