# Grundlagen von Git und GitHub

### Grundlagen von Git und GitHub

Stell dir vor, du arbeitest an einer wichtigen HTML-Datei für deine neue Webseite. Du speicherst sie als `index_v1.html`. Du änderst etwas, bist dir aber nicht sicher, und speicherst die neue Version als `index_v2.html`. Am nächsten Tag hast du eine brillante Idee, die alles umwirft. Das Ergebnis: `index_final.html`. Dein Kollege schaut drüber und hat ein paar Anmerkungen. Nun liegt auf deinem Desktop `index_final_korrigiert.html`. Ein paar Tage später merkst du, dass die Idee aus `v2` doch die beste war, aber du findest die genaue Stelle nicht mehr. Dieses Chaos ist ein alltägliches Problem in der Entwicklung – nicht nur bei Code, sondern bei jeder Art von digitalen Projekten.

Genau hier kommt die Versionskontrolle ins Spiel. Sie ist wie eine lückenlose, intelligente Historie für dein Projekt. Statt eines Berges unübersichtlicher Dateikopien hast du eine saubere Zeitachse, auf der du jeden einzelnen Arbeitsschritt nachvollziehen, vergleichen und bei Bedarf sogar zurückspulen kannst. Das mit Abstand wichtigste Werkzeug dafür ist Git.

#### Was ist Git? Eine Zeitmaschine für deinen Code

Git ist ein sogenanntes **verteiltes Versionskontrollsystem**. Das klingt kompliziert, aber die Idee dahinter ist genial einfach.

*   **Versionskontrollsystem:** Es verfolgt Änderungen an Dateien über die Zeit. Jede gespeicherte Änderung wird zu einem "Schnappschuss" (im Git-Jargon "Commit") deines gesamten Projekts zu einem bestimmten Zeitpunkt. Du kannst jederzeit zu einem dieser Schnappschüsse zurückkehren.
*   **Verteilt:** Im Gegensatz zu älteren Systemen, bei denen die gesamte Projekthistorie auf einem zentralen Server lag, hat bei Git jeder, der am Projekt arbeitet, eine vollständige Kopie der gesamten Historie auf seinem eigenen Rechner. Das macht es unglaublich schnell und flexibel. Du kannst auch offline arbeiten, Commits erstellen und deine Arbeitsschritte sichern, ohne eine Internetverbindung zu benötigen.

Um Git zu verstehen, musst du drei zentrale Bereiche kennen, zwischen denen deine Dateien hin- und herwandern:

1.  **Arbeitsverzeichnis (Working Directory):** Das ist einfach der Ordner auf deinem Computer, in dem deine Projektdateien liegen – deine `index.html`, dein `style.css` und so weiter. Hier nimmst du deine Änderungen vor, wie du es gewohnt bist.
2.  **Staging Area (oder Index):** Dies ist eine Art Zwischenspeicher, ein Wartebereich für Änderungen. Bevor du einen permanenten Schnappschuss deines Projekts erstellst, legst du alle Änderungen, die zu diesem Schnappschuss gehören sollen, in die Staging Area. Das ist extrem nützlich, weil du so deine Änderungen bündeln kannst. Vielleicht hast du einen Tippfehler in der `index.html` korrigiert und gleichzeitig eine neue Funktion im JavaScript begonnen. Du möchtest aber nur den Tippfehler in einem sauberen, kleinen Commit speichern. Dann fügst du nur die `index.html` zur Staging Area hinzu und lässt die JavaScript-Datei erstmal im Arbeitsverzeichnis.
3.  **Repository (.git-Verzeichnis):** Das ist das Herzstück deines Git-Projekts. Es ist ein versteckter Ordner namens `.git` in deinem Projektverzeichnis. Hier speichert Git die gesamte Historie, alle Schnappschüsse (Commits) und alle Informationen über dein Projekt. Dies ist die eigentliche Zeitmaschine. Du solltest diesen Ordner niemals manuell bearbeiten.

Der typische Arbeitsablauf sieht also so aus:
1.  Du bearbeitest eine oder mehrere Dateien in deinem **Arbeitsverzeichnis**.
2.  Du wählst die Änderungen aus, die du in den nächsten Schnappschuss aufnehmen möchtest, und fügst sie zur **Staging Area** hinzu.
3.  Du erstellst einen **Commit**, der die Dateien aus der Staging Area permanent in deinem **Repository** speichert.

#### Die wichtigsten Befehle für deinen Alltag

Du interagierst mit Git über die Kommandozeile (das Terminal oder die Eingabeaufforderung). Auch wenn es anfangs ungewohnt erscheint, wirst du schnell merken, wie effizient und mächtig dieser Weg ist.

**Ein neues Repository initialisieren**
Um die Versionskontrolle für ein bestehendes Projekt zu starten, navigierst du in deinem Terminal in den Projektordner und führst diesen Befehl aus:

```bash
git init
```

Git erstellt nun das versteckte `.git`-Verzeichnis, und schon ist dein Projekt unter Versionskontrolle.

**Den Status überprüfen**
Der wohl am häufigsten genutzte Befehl. Er zeigt dir jederzeit an, was gerade in deinem Projekt los ist: welche Dateien geändert wurden, welche sich in der Staging Area befinden und welche noch gar nicht von Git erfasst sind.

```bash
git status
```

Mach es dir zur Gewohnheit, diesen Befehl ständig zu verwenden. Er ist dein verlässlicher Kompass.

**Änderungen zur Staging Area hinzufügen**
Wenn du mit einer Änderung zufrieden bist, bereitest du sie für den nächsten Commit vor.

```bash
# Eine einzelne Datei hinzufügen
git add index.html

# Alle geänderten Dateien im aktuellen Verzeichnis und Unterverzeichnissen hinzufügen
git add .
```

**Einen Commit erstellen**
Nachdem du eine oder mehrere Änderungen "gestaged" hast, erstellst du den Schnappschuss. Jeder Commit braucht eine Nachricht, die beschreibt, *was* du getan hast. Gute Commit-Nachrichten sind Gold wert – für dich in sechs Monaten und für deine Teamkollegen.

```bash
git commit -m "Navigation im Header hinzugefügt"
```

Die `-m`-Option steht für "Message". Die Nachricht sollte kurz und prägnant sein und in der Gegenwartsform beschreiben, was der Commit tut (z. B. "Fügt hinzu", "Korrigiert", "Entfernt").

**Die Historie ansehen**
Um dir die Kette deiner bisherigen Commits anzusehen, verwendest du `git log`.

```bash
git log
```

Du siehst eine Liste aller Commits mit ihrer einzigartigen ID (ein langer "Hash"), dem Autor, dem Datum und der Commit-Nachricht.

#### Git ist nicht GitHub: Werkzeug vs. Plattform

Dieser Punkt sorgt oft für Verwirrung, ist aber ganz einfach zu trennen:

*   **Git** ist das Werkzeug, die Software, die auf deinem Computer läuft und die Versionshistorie verwaltet.
*   **GitHub** (sowie ähnliche Dienste wie GitLab oder Bitbucket) ist eine Online-Plattform, ein Webservice, auf dem du deine Git-Repositories **hosten** kannst.

Du kannst Git also perfekt allein auf deinem Rechner nutzen, ohne jemals von GitHub gehört zu haben. Die wahre Stärke entfaltet sich aber erst im Zusammenspiel. GitHub ist quasi das soziale Netzwerk für deinen Code. Es gibt dir:

*   **Ein Backup:** Dein Code liegt sicher in der Cloud. Wenn dein Laptop kaputtgeht, ist dein Projekt nicht verloren.
*   **Kollaboration:** Du kannst andere zu deinem Projekt einladen. Mehrere Personen können gleichzeitig am selben Code arbeiten, ihre Änderungen teilen und zusammenführen.
*   **Ein Portfolio:** Dein öffentliches GitHub-Profil wird zu deinem Entwickler-Lebenslauf. Potenzielle Arbeitgeber können sich deine Projekte ansehen und einen Eindruck von deiner Arbeitsweise bekommen.

#### Die Brücke zu GitHub: Remote-Repositories

Ein auf GitHub gehostetes Repository wird aus der Sicht deines lokalen Projekts als "Remote" (entferntes Repository) bezeichnet. Die Interaktion zwischen deinem lokalen und dem Remote-Repository ist der Schlüssel zur Zusammenarbeit und Sicherung.

**Ein Projekt klonen**
Der häufigste Weg, um mit einem auf GitHub existierenden Projekt zu beginnen, ist das Klonen. Du erstellst eine vollständige Kopie des Remote-Repositorys – inklusive der gesamten Historie – auf deinem lokalen Rechner.

```bash
git clone https://github.com/benutzername/projektname.git
```

Diesen Befehl führst du nur einmal am Anfang aus. Danach arbeitest du in dem neu erstellten Ordner.

**Änderungen zu GitHub hochladen (Push)**
Wenn du lokal einen oder mehrere Commits erstellt hast, existieren diese zunächst nur auf deinem Computer. Um sie mit dem Remote-Repository auf GitHub zu synchronisieren und für andere sichtbar zu machen, verwendest du `git push`.

```bash
git push
```

Dieser Befehl "schiebt" deine neuen Commits auf den Server.

**Änderungen von GitHub herunterladen (Pull)**
Wenn ein Teamkollege seine Änderungen gepusht hat, ist dein lokales Repository nicht mehr auf dem neuesten Stand. Um die Änderungen von GitHub auf deinen Rechner zu holen und mit deiner Arbeitskopie zu verschmelzen, nutzt du `git pull`.

```bash
git pull
```

Es ist eine gute Praxis, vor Beginn deiner Arbeit immer erst einen `git pull` auszuführen, um sicherzustellen, dass du auf der aktuellsten Version des Projekts aufbaust.

Der grundlegende Zyklus der Zusammenarbeit sieht also oft so aus: `pull -> arbeiten (add, commit) -> push`.

#### Die Macht der Branches (Zweige)

Bisher haben wir nur über eine einzige Zeitachse gesprochen. Was aber, wenn du an einer neuen, experimentellen Funktion arbeiten möchtest, ohne die stabile Hauptversion deines Projekts zu gefährden? Dafür gibt es Branches.

Ein Branch ist wie eine Abzweigung in deiner Entwicklungshistorie. Du kannst einen neuen Branch erstellen und darin arbeiten, so viel du willst. Du kannst Commits erstellen, Fehler machen und alles ausprobieren. Währenddessen bleibt der Haupt-Branch (meist `main` oder `master` genannt) unberührt und stabil. Wenn du mit deiner Funktion fertig und zufrieden bist, kannst du deinen Branch wieder mit dem Haupt-Branch zusammenführen ("mergen").

**Einen neuen Branch erstellen und dorthin wechseln**
Der `checkout`-Befehl ist dein Werkzeug, um zwischen Branches zu navigieren. Mit der `-b`-Option erstellst du einen neuen Branch und wechselst direkt dorthin.

```bash
git checkout -b feature/neues-kontaktformular
```

Jetzt bist du im Branch `feature/neues-kontaktformular`. Alle Commits, die du jetzt machst, landen auf dieser separaten Zeitlinie.

**Zu einem anderen Branch wechseln**
Um zurück zum Haupt-Branch zu gelangen, lässt du die `-b`-Option weg:

```bash
git checkout main
```

Die Arbeit mit Branches ist ein fundamentaler Bestandteil von Git und ermöglicht saubere, parallele Entwicklungsprozesse.

Git und GitHub mögen anfangs einschüchternd wirken, aber sie sind unverzichtbare Werkzeuge in der modernen Webentwicklung. Sie bringen Ordnung ins Chaos, ermöglichen professionelle Zusammenarbeit und sichern deine wertvolle Arbeit. Indem du dir die hier vorgestellten Grundlagen aneignest und sie in deinen täglichen Arbeitsablauf integrierst, legst du ein solides Fundament für deine gesamte weitere Karriere als Entwickler.
