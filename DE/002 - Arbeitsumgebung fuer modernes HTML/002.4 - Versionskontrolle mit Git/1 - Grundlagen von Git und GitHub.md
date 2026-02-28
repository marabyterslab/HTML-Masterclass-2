# Grundlagen von Git und GitHub

### Grundlagen von Git und GitHub

Stell dir vor, du arbeitest an einer wichtigen HTML-Datei für deine neue Webseite. Du speicherst die erste Version als `index_v1.html`. Dann nimmst du Änderungen vor und speicherst sie als `index_v2.html`. Nach dem Feedback eines Freundes entsteht `index_final.html`, und kurz darauf, nach einer brillanten Idee um Mitternacht, `index_wirklich_final.html`. Dieses Namenschaos ist nicht nur unübersichtlich, sondern macht es auch fast unmöglich, nachzuvollziehen, welche Änderung wann und warum gemacht wurde. Was, wenn du zu einer älteren Version zurückkehren musst? Was, wenn du mit anderen zusammenarbeiten möchtest?

Genau hier kommt die Versionskontrolle ins Spiel. Ein Versionskontrollsystem (VCS) ist eine Software, die Änderungen an Dateien über die Zeit aufzeichnet. Es erlaubt dir, spezifische Versionen später wiederherzustellen, den Projektverlauf einzusehen und Änderungen verschiedener Personen nahtlos zusammenzuführen. Das mit Abstand populärste und leistungsfähigste VCS in der modernen Webentwicklung ist Git.

#### Was ist Git? Dein lokales Projektarchiv

Git ist ein **verteiltes Versionskontrollsystem**. Das klingt kompliziert, bedeutet aber etwas sehr Einfaches und Mächtiges: Anstatt dass es einen zentralen Server gibt, der die gesamte Projekthistorie speichert, hat jeder Entwickler, der am Projekt arbeitet, eine vollständige Kopie des gesamten Verlaufs auf seinem eigenen Rechner. Dies macht Git unglaublich schnell, flexibel und ausfallsicher. Du kannst arbeiten, Versionen erstellen und den Verlauf einsehen, auch wenn du offline bist.

Das Kernkonzept von Git ist das Erstellen von "Snapshots" deines Projekts. Jedes Mal, wenn du deinen Fortschritt speichern möchtest, sagst du Git, es solle einen Schnappschuss des aktuellen Zustands aller deiner Dateien machen. Dieser Schnappschuss wird als **Commit** bezeichnet. Git ist dabei sehr effizient: Wenn sich eine Datei nicht geändert hat, speichert es nicht die ganze Datei neu, sondern nur einen Verweis auf die bereits gespeicherte, identische Version.

Um den Überblick zu behalten, arbeitet Git mit drei konzeptionellen Bereichen, in denen sich deine Dateien befinden können:

1.  **Arbeitsverzeichnis (Working Directory):** Das ist einfach dein Projektordner mit all deinen Dateien (`index.html`, `style.css` etc.), so wie du sie gerade siehst und bearbeitest.
2.  **Staging Area (oder "Index"):** Dies ist eine Art Zwischenspeicher. Bevor du einen Commit erstellst, wählst du gezielt aus, welche Änderungen aus deinem Arbeitsverzeichnis in den nächsten Snapshot aufgenommen werden sollen. Du packst deine Änderungen quasi in einen Warenkorb für den nächsten Commit.
3.  **Git-Verzeichnis (.git-Repository):** Hier speichert Git die gesamte Projekthistorie, also alle deine Commits. Es ist ein versteckter Ordner namens `.git` in deinem Projektverzeichnis. Dies ist das Herz deines lokalen Repositorys.

Der grundlegende Arbeitsablauf sieht also so aus: Du änderst Dateien in deinem Arbeitsverzeichnis, fügst diese Änderungen zur Staging Area hinzu und erstellst dann einen Commit, der die Änderungen dauerhaft in deinem Repository speichert.

#### Die wichtigsten Git-Befehle für den Start

Git wird hauptsächlich über die Kommandozeile bedient. Auch wenn es grafische Oberflächen gibt, ist das Verständnis der grundlegenden Befehle essenziell.

**Ein neues Repository initialisieren**
Um Git in einem bestehenden Projektordner zu aktivieren, navigierst du in der Kommandozeile in diesen Ordner und führst folgenden Befehl aus:

```bash
git init
```

Dieser Befehl erstellt den versteckten `.git`-Ordner, und schon ist dein Projekt ein Git-Repository.

**Den Status überprüfen**
Der wohl am häufigsten genutzte Befehl ist `git status`. Er zeigt dir an, welche Dateien geändert wurden, welche für den nächsten Commit vorgemerkt sind und welche von Git noch gar nicht erfasst werden.

```bash
git status
```

**Änderungen zur Staging Area hinzufügen**
Wenn du mit einer Änderung zufrieden bist und sie in den nächsten Commit aufnehmen möchtest, nutzt du den Befehl `git add`.

```bash
# Eine einzelne Datei hinzufügen
git add index.html

# Alle geänderten Dateien im aktuellen Ordner und Unterordnern hinzufügen
git add .
```

Damit hast du die Änderungen "vorgemerkt". Sie sind aber noch nicht permanent gespeichert.

**Einen Commit erstellen**
Um die Änderungen aus der Staging Area dauerhaft als Snapshot in deiner Projekthistorie zu speichern, erstellst du einen Commit. Jeder Commit benötigt eine Nachricht, die beschreibt, was du geändert hast. Gute Commit-Nachrichten sind Gold wert!

```bash
git commit -m "Navigation zur Hauptseite hinzugefügt"
```

Die `-m`-Option steht für "Message" und erlaubt dir, die Nachricht direkt im Befehl mitzugeben. Deine Änderungen sind nun sicher in deinem lokalen Repository gespeichert.

**Die Projekthistorie ansehen**
Um eine Liste aller bisherigen Commits anzuzeigen, verwendest du `git log`. Du siehst, wer den Commit gemacht hat, wann er gemacht wurde und welche Nachricht er hatte.

```bash
git log
```

Jeder Commit hat eine einzigartige Kennung, einen sogenannten Hash (eine lange Zeichenkette aus Buchstaben und Zahlen), über den du ihn jederzeit wiederfinden kannst.

#### Was ist GitHub? Dein Projekt im Web

Jetzt weißt du, was Git ist: ein mächtiges Werkzeug auf deinem Computer. Aber wo kommt GitHub ins Spiel?

**GitHub ist eine webbasierte Plattform, die einen Hosting-Service für Git-Repositorys anbietet.** Es ist sozusagen ein Zuhause für deine Projekte im Internet. Der fundamentale Unterschied ist:
*   **Git** ist die Software, das Werkzeug, die Technologie zur Versionskontrolle.
*   **GitHub** ist ein Service, eine Website, ein Ort, um deine mit Git verwalteten Projekte abzulegen, zu teilen und mit anderen daran zusammenzuarbeiten.

Man könnte es so vergleichen: Git ist wie ein Textverarbeitungsprogramm (z.B. Microsoft Word), mit dem du Dokumente erstellen und deren Versionen verwalten kannst. GitHub ist wie ein Cloud-Speicher (z.B. Google Drive oder Dropbox), wo du diese Dokumente hochladen, sichern und für andere freigeben kannst.

GitHub erweitert die Funktionalität von Git um wichtige soziale und kollaborative Features wie:
*   **Code-Hosting:** Ein zentraler Ort, an dem der "offizielle" Stand des Projekts gespeichert ist.
*   **Kollaboration:** Werkzeuge wie Pull Requests, Code-Reviews und Issue-Tracking, um die Zusammenarbeit im Team zu organisieren.
*   **Sichtbarkeit:** Du kannst deine Projekte als Open Source der ganzen Welt zur Verfügung stellen oder als private Repositorys nur für dich oder dein Team zugänglich machen.

#### Die Verbindung zwischen lokal und remote

Um GitHub zu nutzen, musst du dein lokales Git-Repository mit einem Repository auf GitHub verbinden. Dieses Repository auf GitHub wird als **Remote** bezeichnet.

**Ein Projekt klonen**
Der einfachste Weg, mit einem auf GitHub gehosteten Projekt zu beginnen, ist das Klonen. Du erstellst eine vollständige Kopie eines Remote-Repositorys auf deinem lokalen Rechner.

```bash
git clone https://github.com/benutzername/projektname.git
```

Dieser Befehl lädt nicht nur alle Dateien herunter, sondern auch die gesamte Git-Historie. Die Verbindung zum Remote-Repository (standardmäßig `origin` genannt) wird automatisch eingerichtet.

**Änderungen zu GitHub hochladen (Push)**
Wenn du lokal einige Commits erstellt hast, existieren diese nur auf deinem Computer. Um sie mit dem Remote-Repository auf GitHub zu synchronisieren, musst du sie "pushen".

```bash
git push origin main
```

Dieser Befehl sendet deine Commits vom lokalen `main`-Branch zum `main`-Branch des Remotes `origin`. (`main` ist der heutzutage übliche Name für den Hauptentwicklungszweig, früher oft `master` genannt.)

**Änderungen von GitHub herunterladen (Pull)**
Wenn andere an dem Projekt arbeiten und ihre Änderungen auf GitHub gepusht haben, ist dein lokales Repository nicht mehr auf dem neuesten Stand. Um die Änderungen von anderen zu erhalten, musst du sie "pullen".

```bash
git pull origin main
```

Dieser Befehl holt die neuesten Änderungen vom Remote-Repository und führt sie mit deinem lokalen Arbeitsstand zusammen.

#### Branching: Parallel arbeiten ohne Chaos

Eines der mächtigsten Konzepte in Git ist das **Branching** (Verzweigen). Stell dir den `main`-Branch als den Hauptstamm eines Baumes vor. Er repräsentiert die stabile, funktionierende Version deines Projekts.

Wenn du nun an einer neuen Funktion arbeiten möchtest, zum Beispiel einem neuen Kontaktformular, möchtest du den stabilen Hauptstamm nicht gefährden. Stattdessen erstellst du einen neuen Zweig (einen **Branch**), der vom Hauptstamm abzweigt.

```bash
# Einen neuen Branch erstellen und sofort dorthin wechseln
git checkout -b feature/kontaktformular
```

Jetzt bist du in einer Art parallelen Realität. Alle Commits, die du hier machst, betreffen nur diesen Branch. Der `main`-Branch bleibt unberührt. Du kannst in Ruhe experimentieren, Fehler machen und deine Funktion entwickeln.

Wenn deine Funktion fertig und getestet ist, wechselst du zurück zum `main`-Branch und führst die Änderungen aus deinem Feature-Branch wieder mit dem Hauptstamm zusammen. Dieser Vorgang wird **Merging** genannt.

```bash
# Zurück zum Haupt-Branch wechseln
git checkout main

# Die Änderungen aus dem Feature-Branch in den main-Branch mergen
git merge feature/kontaktformular
```

Auf GitHub wird dieser Prozess oft über **Pull Requests** organisiert. Ein Pull Request ist eine Anfrage, deine Änderungen aus einem Branch in einen anderen zu übernehmen. Es ist der zentrale Ort für Diskussionen, Code-Reviews und die Sicherstellung, dass nur qualitativ hochwertiger Code in den Haupt-Branch gelangt.

Diese Kombination aus lokalem Arbeiten mit Git und der Kollaboration über eine Plattform wie GitHub ist das Fundament der modernen Software- und Webentwicklung. Sie gibt dir die Sicherheit, jederzeit zu einer funktionierenden Version zurückkehren zu können, und die Freiheit, furchtlos neue Ideen auszuprobieren, ohne das Bestehende zu zerstören. Für dich als angehenden HTML-Entwickler ist das Beherrschen dieser Grundlagen ein unverzichtbarer Schritt, um professionell und effizient arbeiten zu können – allein oder im Team.
