# Zusammenarbeit im Team

### Zusammenarbeit im Team: Die wahre Stärke von Git

Bisher hast du Git vielleicht vor allem als eine Art super-leistungsfähiges Backup-System für deine eigenen Projekte kennengelernt. Du kannst Änderungen nachverfolgen, zu alten Versionen zurückspringen und mit einem guten Gefühl experimentieren, weil du weißt, dass nichts wirklich verloren gehen kann. Das ist fantastisch und allein schon ein Grund, Git zu lieben. Doch die wahre Magie, der eigentliche Grund, warum Git die Entwicklungswelt im Sturm erobert hat, entfaltet sich erst, wenn du nicht mehr allein arbeitest.

In der realen Welt der Webentwicklung sind Soloprojekte die Ausnahme. Meistens arbeitest du mit anderen Entwicklern, Designern und Projektmanagern an einem gemeinsamen Code. Stell dir vor, du und zwei Kollegen sollt an derselben Website arbeiten. Du kümmerst dich um das neue Navigationsmenü, ein Kollege überarbeitet den Footer und die dritte Person implementiert ein Kontaktformular. Ihr alle müsst Änderungen an den gleichen HTML- und CSS-Dateien vornehmen. Wie koordiniert man das, ohne sich gegenseitig die Arbeit zu überschreiben oder Chaos zu verursachen?

Genau hier kommt Git ins Spiel und verwandelt potenzielles Chaos in einen strukturierten, nachvollziehbaren Prozess.

#### Das Konzept des "Remote Repository"

Der Schlüssel zur Zusammenarbeit ist das sogenannte „Remote Repository“. Stell es dir als eine zentrale, offizielle Version eures Projekts vor, die auf einem Server im Internet liegt. Jeder im Team hat eine vollständige, lokale Kopie dieses Projekts auf dem eigenen Rechner. Deine lokale Kopie ist dein privater Arbeitsbereich. Hier kannst du nach Herzenslust experimentieren, speichern, Fehler machen und wieder korrigieren. Niemand sieht deine Arbeit, bis du dich entscheidest, sie mit dem Team zu teilen.

Plattformen wie GitHub, GitLab oder Bitbucket sind die beliebtesten Anbieter für das Hosting dieser Remote Repositories. Sie bieten nicht nur den Speicherplatz, sondern auch eine Weboberfläche, die die Zusammenarbeit mit zusätzlichen Werkzeugen wie Issue-Tracking und Code-Reviews enorm erleichtert.

Um mit der Arbeit zu beginnen, lädst du nicht einfach nur Dateien herunter. Du „klonst“ das gesamte Repository.

```bash
git clone https://github.com/unser-team/tolles-projekt.git
```

Dieser eine Befehl macht mehrere Dinge: Er lädt alle Projektdateien herunter, inklusive der gesamten Git-Historie. Außerdem richtet er automatisch eine Verbindung zwischen deiner lokalen Kopie und dem Remote Repository ein. Diese Verbindung wird standardmäßig „origin“ genannt.

#### Der grundlegende Arbeitszyklus im Team

Die Zusammenarbeit mit Git folgt einem einfachen, aber mächtigen Rhythmus aus Holen, Arbeiten und Teilen.

**1. Änderungen holen (Pull)**

Bevor du mit deiner eigenen Arbeit beginnst, solltest du immer sicherstellen, dass deine lokale Version des Projekts auf dem neuesten Stand ist. Vielleicht hat ein Kollege in der Zwischenzeit eine wichtige Fehlerbehebung hochgeladen. Mit `git pull` holst du dir alle Änderungen, die seit deinem letzten Klonen oder Pullen auf dem Remote Repository gemacht wurden, und fügst sie in deine lokale Arbeitskopie ein.

```bash
# Holt die neuesten Änderungen vom Remote-Server und integriert sie
git pull origin main
```

Der Befehl `git pull` ist eigentlich eine Kombination aus zwei anderen Befehlen: `git fetch` (holt die Änderungen, ohne sie anzuwenden) und `git merge` (integriert die geholten Änderungen). Für den Anfang reicht es aber völlig, `git pull` zu kennen.

**2. Lokal arbeiten (Add & Commit)**

Jetzt kannst du wie gewohnt arbeiten. Du erstellst neue Dateien, änderst bestehende und speicherst deine Fortschritte mit `git add` und `git commit` in deiner lokalen Historie. Dieser Teil des Prozesses ist identisch mit der Arbeit an einem Soloprojekt. Deine Commits existieren vorerst nur auf deinem Rechner.

**3. Änderungen teilen (Push)**

Wenn du mit einem Arbeitspaket fertig bist und deine Änderungen dem Team zur Verfügung stellen möchtest, schiebst du sie mit `git push` auf das Remote Repository.

```bash
# Schiebt deine lokalen Commits auf den Server
git push origin main
```

Dieser Befehl nimmt alle Commits, die du lokal gemacht hast und die auf dem Server noch nicht vorhanden sind, und lädt sie hoch. Ab diesem Moment können deine Kollegen deine Arbeit sehen und sie sich mit `git pull` ebenfalls holen.

Was aber, wenn jemand anderes genau in dem Moment, in dem du gearbeitet hast, ebenfalls Änderungen gepusht hat? Git würde deinen Push blockieren und dich darauf hinweisen, dass die Historien voneinander abweichen. Die Lösung ist einfach: Du musst zuerst `git pull` ausführen, um die neuen Änderungen des Kollegen zu integrieren. Manchmal führt Git diese Zusammenführung automatisch durch. In seltenen Fällen, wenn ihr beide exakt dieselben Zeilen in derselben Datei geändert habt, entsteht ein sogenannter „Merge-Konflikt“, den du manuell auflösen musst. Git hilft dir dabei, indem es die betroffenen Stellen in der Datei markiert.

#### Branching: Der Königsweg für paralleles Arbeiten

Der oben beschriebene Zyklus funktioniert gut für kleine Änderungen. Aber was passiert bei größeren Aufgaben, die mehrere Tage dauern? Ständig auf dem Haupt-Branch (der meist `main` oder `master` heißt) zu arbeiten, wäre riskant. Unfertiger Code könnte das Projekt für alle unbrauchbar machen.

Die Lösung ist eine der mächtigsten Funktionen von Git: **Branching**.

Ein Branch ist wie eine alternative Zeitlinie für dein Projekt. Wenn du einen neuen Branch erstellst, erzeugst du eine Abzweigung vom aktuellen Zustand. In diesem Branch kannst du nun völlig isoliert an deinem neuen Feature arbeiten, Commits machen und experimentieren, ohne den Haupt-Branch zu beeinflussen. Der `main`-Branch bleibt stabil und funktionsfähig – er enthält immer die letzte „gute“ Version des Codes.

Der Arbeitsablauf für ein neues Feature sieht typischerweise so aus:

**1. Einen neuen Branch erstellen und dorthin wechseln**

Nehmen wir an, du sollst ein neues Navigationsmenü erstellen. Du stellst sicher, dass du auf dem aktuellen `main`-Branch bist (`git pull origin main`) und erstellst dann deinen Feature-Branch.

```bash
# Erstellt einen neuen Branch namens "feature/neues-navi" und wechselt sofort dorthin
git checkout -b feature/neues-navi
```

Eine gute Namenskonvention (z. B. `feature/`, `bugfix/`) hilft dem ganzen Team, den Überblick zu behalten.

**2. Auf dem Branch arbeiten**

Jetzt bist du in deiner eigenen, sicheren Arbeitsumgebung. Du kannst deine HTML-Struktur für das Menü anlegen, das CSS schreiben und so viele Commits machen, wie du brauchst. Der `main`-Branch bleibt von alldem unberührt.

**3. Den Branch teilen**

Auch dein Branch existiert zunächst nur lokal. Um Feedback von Kollegen zu bekommen oder einfach nur deine Arbeit zu sichern, kannst du den Branch ebenfalls auf das Remote Repository pushen.

```bash
# Pusht den neuen Branch zum ersten Mal und setzt die Verbindung ("upstream")
git push -u origin feature/neues-navi
```

Das `-u` (kurz für `--set-upstream`) musst du nur beim ersten Mal machen. Es sagt Git, dass dein lokaler Branch `feature/neues-navi` mit dem gleichnamigen Branch auf `origin` verbunden ist. Zukünftige `git push`- und `git pull`-Befehle auf diesem Branch sind dann einfacher.

**4. Änderungen integrieren: Der Pull Request**

Wenn dein Feature fertig und getestet ist, soll es zurück in den `main`-Branch fließen. Technisch gesehen würdest du dafür den Befehl `git merge` verwenden. In der modernen Teamarbeit macht man das jedoch fast nie direkt.

Stattdessen nutzt man eine Funktion von Plattformen wie GitHub, die sich **Pull Request** (PR) oder bei GitLab **Merge Request** (MR) nennt.

Ein Pull Request ist im Grunde ein formaler Antrag: „Hallo Team, ich habe meine Arbeit auf dem Branch `feature/neues-navi` beendet. Bitte schaut euch meinen Code an und erlaubt mir, ihn in den `main`-Branch zu integrieren (to merge).“

Dieser Prozess ist das Herzstück der modernen Zusammenarbeit:

*   **Sichtbarkeit:** Jeder im Team kann sehen, welche Änderungen du vorschlägst.
*   **Code Review:** Kollegen können deinen Code Zeile für Zeile kommentieren, Fragen stellen und Verbesserungsvorschläge machen. Das ist eine der besten Methoden, um die Code-Qualität hochzuhalten und voneinander zu lernen.
*   **Diskussion:** Ihr könnt über die beste Lösung diskutieren, bevor der Code Teil der Haupt-Codebasis wird.
*   **Automatisierte Tests:** Oft sind Pull Requests mit automatisierten Systemen verknüpft, die prüfen, ob dein Code die Website kaputtmacht, bevor er überhaupt gemerged wird.

Erst wenn der Pull Request von den Kollegen genehmigt wurde, wird der Code – meist per Klick auf einen Button in der Weboberfläche von GitHub – in den `main`-Branch gemerged. Anschließend kann der nun überflüssige Feature-Branch gelöscht werden.

Dieser Workflow – `pull`, `branch`, `commit`, `push`, `pull request` – mag anfangs etwas aufwendiger klingen als das einfache Speichern von Dateien. Doch er bringt eine unbezahlbare Ordnung, Sicherheit und Qualität in die Teamarbeit. Er erlaubt es Dutzenden von Entwicklern, gleichzeitig und effizient an hochkomplexen Projekten zu arbeiten, ohne sich in die Quere zu kommen. Für dich als angehenden Webentwickler ist das Verständnis dieses Prozesses nicht nur eine technische Fähigkeit, sondern eine grundlegende Kompetenz für die professionelle Arbeit.
