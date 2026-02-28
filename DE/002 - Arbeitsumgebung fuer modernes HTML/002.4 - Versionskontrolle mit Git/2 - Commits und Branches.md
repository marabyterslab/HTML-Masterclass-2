# Commits und Branches

### Commits und Branches: Das Herzstück deiner Projektgeschichte

Stell dir vor, du schreibst an einem wichtigen Dokument. Nach jedem abgeschlossenen Abschnitt speicherst du eine neue Version: `dokument_v1.html`, `dokument_v2_mit_bildern.html`, `dokument_final.html`, `dokument_final_WIRKLICH_final.html`. Das wird schnell unübersichtlich und fehleranfällig. Was, wenn du eine Änderung aus Version 2 in der finalen Version wieder brauchst? Genau hier revolutioniert Git deine Arbeitsweise mit zwei fundamentalen Konzepten: Commits und Branches.

#### Der Commit – Ein Schnappschuss deiner Arbeit

Ein Commit ist viel mehr als nur eine gespeicherte Datei. Es ist ein bewusster, dauerhafter Schnappschuss deines gesamten Projektverzeichnisses zu einem bestimmten Zeitpunkt. Man könnte ihn mit einem Speicherpunkt in einem Videospiel vergleichen. Du erreichst einen wichtigen Meilenstein, speicherst den Spielstand und kannst jederzeit dorthin zurückkehren, falls später etwas schiefgeht.

Doch bevor du einen solchen Schnappschuss machen kannst, musst du Git genau sagen, welche Änderungen darin enthalten sein sollen. Dieser Prozess besteht aus drei Schritten oder "Zonen":

1.  **Das Arbeitsverzeichnis (Working Directory):** Das ist einfach dein Projektordner. Hier erstellst du neue HTML-Dateien, schreibst CSS oder bearbeitest Bilder. Dieser Ort ist deine Werkbank – hier ist alles in Bewegung und manchmal auch chaotisch.

2.  **Die Staging Area (oder der "Index"):** Dies ist eine Art Warteraum. Bevor du einen finalen Schnappschuss erstellst, wählst du gezielt aus, welche der Änderungen aus deinem Arbeitsverzeichnis Teil des nächsten Commits werden sollen. Vielleicht hast du an drei Dateien gearbeitet, aber nur die Änderungen in zwei davon gehören logisch zusammen und sollen einen Speicherpunkt bilden. Die dritte Datei bleibt unberücksichtigt und wartet auf einen späteren Commit. Mit dem Befehl `git add` fügst du Dateien zur Staging Area hinzu.

3.  **Das Repository (die `.git`-Datenbank):** Dies ist die eigentliche, gesicherte Projekthistorie. Wenn du den Befehl `git commit` ausführst, nimmt Git alles, was sich in der Staging Area befindet, verpackt es zu einem sauberen Schnappschuss, versieht ihn mit einer eindeutigen ID (einem sogenannten Hash) und speichert ihn dauerhaft in der Historie deines Projekts.

Dieser dreistufige Prozess gibt dir die volle Kontrolle. Du kannst kleine, logische und nachvollziehbare Speicherpunkte erstellen, anstatt riesige, unübersichtliche Änderungen auf einmal zu sichern.

Ein Commit wäre jedoch nutzlos ohne eine Beschreibung. Jeder Commit wird von einer Commit-Nachricht begleitet. Diese Nachricht ist deine Chance, dir selbst und deinen Teamkollegen in der Zukunft zu erklären, *warum* du diese Änderungen vorgenommen hast. Eine gute Commit-Nachricht ist Gold wert. Statt "Dateien aktualisiert" solltest du etwas schreiben wie "Fix: Kontaktformular sendet nun korrekt" oder "Feature: Füge eine neue Bildergalerie zur Startseite hinzu". Das ist dein Projekttagebuch.

Ein typischer Arbeitsablauf für einen einzelnen Commit sieht so aus:

```bash
# 1. Überprüfe den Status deiner Dateien. Git zeigt dir, was geändert wurde.
git status

# 2. Wähle die Datei aus, die du für den nächsten Commit vorbereiten möchtest.
# Hier fügen wir die index.html zur Staging Area hinzu.
git add index.html

# 3. Erstelle den eigentlichen Commit mit einer aussagekräftigen Nachricht.
git commit -m "Feat: Ersetze Platzhaltertext auf der Startseite durch finalen Inhalt"
```

Nach diesem Befehl ist dein Schnappschuss sicher in der Projekthistorie gespeichert. Du hast einen sauberen, beschrifteten Meilenstein geschaffen, zu dem du jederzeit zurückkehren kannst.

#### Branches – Parallele Welten für deine Ideen

Stell dir nun vor, du arbeitest an deiner Webseite und hast eine brillante, aber vielleicht etwas riskante Idee für ein neues Navigationsmenü. Du möchtest daran arbeiten, ohne die funktionierende Hauptversion deiner Seite zu gefährden. Würdest du jetzt einfach eine Kopie des gesamten Projektordners anlegen und sie `projekt_neues_menue` nennen? Git bietet eine weitaus elegantere Lösung: Branches.

Ein Branch (deutsch: Zweig) ist eine eigenständige Entwicklungslinie innerhalb deines Projekts. Wenn du ein Git-Repository initialisierst, befindest du dich standardmäßig auf einem Hauptzweig, der meistens `main` (früher `master`) heißt. Man kann sich den `main`-Branch als den stabilen, produktiven Stamm eines Baumes vorstellen.

Wenn du eine neue Funktion entwickeln, einen Bug beheben oder einfach nur etwas ausprobieren möchtest, erstellst du einen neuen Branch, der vom `main`-Branch abzweigt. Dieser neue Branch ist anfangs eine exakte Kopie des Zustands, von dem er abgezweigt wurde. Von diesem Punkt an kannst du jedoch in deinem neuen Branch völlig unabhängig arbeiten. Du kannst neue Commits erstellen, Dateien löschen und experimentieren, ohne den `main`-Branch auch nur im Geringsten zu beeinflussen.

Das ist unglaublich mächtig. Es erlaubt dir:

*   **Sicheres Experimentieren:** Probiere neue Ideen aus. Wenn sie nicht funktionieren, kannst du den Branch einfach verwerfen. Die Hauptversion bleibt unberührt.
*   **Organisierte Entwicklung:** Jede neue Funktion oder jeder Bugfix bekommt einen eigenen Branch. Das hält deine Arbeit sauber und thematisch getrennt.
*   **Paralleles Arbeiten:** In einem Team kann jeder Entwickler an seinem eigenen Branch für eine bestimmte Aufgabe arbeiten, ohne die Arbeit der anderen zu stören.

Das Erstellen und Wechseln von Branches ist denkbar einfach.

```bash
# Erstellt einen neuen Branch namens "feature/neues-navi"
git branch feature/neues-navi

# Wechselt in den neu erstellten Branch. Ab jetzt finden alle Änderungen hier statt.
git switch feature/neues-navi
```

Du kannst auch beides in einem Schritt erledigen:

```bash
# Erstellt den Branch und wechselt direkt dorthin
git switch -c feature/neues-navi
```

Sobald du in deinem neuen Branch bist, ist der Arbeitsablauf genau derselbe wie zuvor: Du änderst Dateien, fügst sie mit `git add` zur Staging Area hinzu und erstellst mit `git commit` neue Schnappschüsse. Diese Commits existieren aber nur in der Geschichte deines `feature/neues-navi`-Branches. Der `main`-Branch weiß davon nichts und bleibt auf seinem alten Stand.

#### Die Welten verbinden – Der Merge

Du hast in deinem `feature/neues-navi`-Branch fleißig gearbeitet und das neue Navigationsmenü ist fertig, getestet und funktioniert einwandfrei. Nun ist es an der Zeit, diese tolle neue Funktion in die Hauptversion deiner Webseite zu integrieren. Dieser Prozess wird "Merging" genannt.

Beim Mergen sagst du Git: "Nimm bitte alle Commits und Änderungen, die im `feature/neues-navi`-Branch passiert sind, und füge sie in den `main`-Branch ein."

Der Vorgang ist unkompliziert. Zuerst wechselst du zurück in den Ziel-Branch, also in den Branch, der die Änderungen empfangen soll.

```bash
# Wechsle zurück zum Haupt-Branch
git switch main
```

Dann führst du den Merge-Befehl aus und gibst an, welcher Branch integriert werden soll.

```bash
# Führe die Historie von "feature/neues-navi" mit "main" zusammen
git merge feature/neues-navi
```

Git analysiert nun die Historien beider Branches. In den meisten Fällen erkennt es automatisch, wie die Änderungen zusammengefügt werden müssen, und erstellt einen neuen "Merge-Commit" im `main`-Branch, der die beiden Entwicklungslinien wieder vereint. Deine Webseite auf dem `main`-Branch enthält nun das brandneue Navigationsmenü.

Manchmal kommt es vor, dass du im Feature-Branch eine Codezeile geändert hast, die in der Zwischenzeit auch jemand anderes im `main`-Branch verändert hat. In diesem Fall kann Git nicht automatisch entscheiden, welche Version die richtige ist. Es meldet einen "Merge-Konflikt". Das ist aber kein Grund zur Panik. Git stoppt den Prozess, markiert die betreffenden Stellen in den Dateien und bittet dich als Entwickler, die Entscheidung zu treffen. Sobald du den Konflikt manuell gelöst hast, schließt du den Merge ab.

Nach einem erfolgreichen Merge ist die Arbeit des Feature-Branches erledigt. Er wird nicht mehr benötigt und kann gelöscht werden, um das Repository sauber zu halten.

```bash
# Lösche den nun überflüssigen Branch
git branch -d feature/neues-navi
```

Die Commits und die wertvolle Arbeit, die in diesem Branch geleistet wurde, sind natürlich nicht verloren – sie sind jetzt ein fester Bestandteil der Geschichte des `main`-Branches.

Die Kombination aus kleinen, atomaren Commits und der flexiblen Nutzung von Branches bildet das Rückgrat moderner Softwareentwicklung. Sie ermöglicht es dir, deine Arbeit sicher zu strukturieren, furchtlos zu experimentieren und die Geschichte deines Projekts klar und nachvollziehbar zu halten – von der ersten `index.html` bis hin zu einem komplexen Webprojekt.
