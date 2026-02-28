# Commits und Branches

### Commits und Branches: Die Bausteine der Versionsgeschichte

Wenn du mit Git arbeitest, wirst du schnell auf zwei zentrale Begriffe stoßen, die das Herzstück der gesamten Versionskontrolle bilden: Commits und Branches. Sie sind die fundamentalen Werkzeuge, mit denen du die Geschichte deines Projekts aufzeichnest, organisierst und sicher verwaltest. Lass uns diese beiden Konzepte im Detail betrachten, denn ihr Verständnis ist der Schlüssel zu einem flüssigen und stressfreien Arbeitsablauf.

#### Der Commit: Ein Schnappschuss deines Projekts

Stell dir einen Commit wie einen Speicherpunkt in einem Videospiel vor. Es ist ein bewusster, von dir ausgelöster Moment, in dem du den exakten Zustand deines gesamten Projekts sicherst. Ein Commit ist mehr als nur eine simple Kopie einer Datei; er ist ein Schnappschuss des gesamten Projektverzeichnisses zu einem bestimmten Zeitpunkt. Jeder Commit enthält nicht nur die vorgenommenen Änderungen, sondern auch wichtige Metadaten: Wer hat die Änderung gemacht, wann wurde sie gemacht und – ganz entscheidend – warum wurde sie gemacht.

Jeder Commit hat eine einzigartige Kennung, einen sogenannten Hash (eine lange, kryptische Zeichenkette wie `a1b2c3d4...`), der ihn unverwechselbar macht. Diese Commits werden in einer Kette aneinandergereiht und bilden so eine lückenlose, nachvollziehbare Historie deines Projekts. Du kannst jederzeit zu jedem dieser "Speicherpunkte" zurückkehren, um zu sehen, wie dein Code aussah, oder um Änderungen rückgängig zu machen.

**Vom Arbeitsverzeichnis zum Commit: Die Staging Area**

Bevor du jedoch einen solchen Schnappschuss erstellen kannst, musst du Git genau sagen, welche Änderungen er enthalten soll. Hier kommt ein wichtiges Zwischenkonzept ins Spiel: die **Staging Area** (manchmal auch "Index" genannt). Du kannst sie dir wie eine Art Wartezimmer oder eine Bühne vorstellen, auf die du die Änderungen stellst, die für den nächsten Commit vorgesehen sind.

Dein Arbeitsablauf sieht typischerweise so aus:

1.  **Arbeitsverzeichnis (Working Directory):** Hier lebst und arbeitest du. Du änderst Dateien, fügst neue hinzu oder löschst alte. In diesem Zustand sind deine Änderungen für Git zwar sichtbar, aber noch nicht für den nächsten Commit vorgemerkt. Wenn du `git status` ausführst, siehst du sie unter "Changes not staged for commit".

2.  **Staging Area:** Mit dem Befehl `git add <dateiname>` wählst du gezielt eine oder mehrere geänderte Dateien aus und fügst sie der Staging Area hinzu. Du bereitest damit quasi den nächsten Commit vor. Dies gibt dir die volle Kontrolle. Vielleicht hast du an drei Dateien gearbeitet, möchtest aber nur die Änderungen von zweien in einem Commit bündeln, weil nur sie logisch zusammengehören.

3.  **Repository:** Sobald du mit deiner Auswahl in der Staging Area zufrieden bist, erstellst du den endgültigen Schnappschuss mit dem Befehl `git commit`. Damit werden alle Änderungen, die sich in der Staging Area befinden, permanent in der Projekthistorie (dem Repository) gespeichert.

Der Befehl zum Committen sieht meist so aus:

```bash
git commit -m "Eine kurze, aussagekräftige Beschreibung der Änderung"
```

Das `-m` steht für "message". Die Commit-Nachricht ist von unschätzbarem Wert. Sie ist deine Nachricht an dein zukünftiges Ich und an deine Teamkollegen. Eine gute Commit-Nachricht erklärt kurz und prägnant, *was* geändert wurde und idealerweise auch *warum*.

Ein Beispiel für einen guten Commit-Titel wäre: "Füge grundlegendes HTML-Gerüst für Kontaktseite hinzu".
Ein weniger hilfreicher Titel wäre: "Änderungen".

Wenn du dir die Historie deines Projekts ansehen möchtest, kannst du das mit `git log` tun. Du erhältst eine Liste aller bisherigen Commits, jeweils mit ihrem Hash, dem Autor, dem Datum und der Commit-Nachricht.

#### Branches: Parallele Universen für deine Arbeit

Jetzt, wo du weißt, wie du den Fortschritt deines Projekts in Form von Commits festhältst, kommt die zweite Superkraft von Git ins Spiel: Branches.

Stell dir vor, die Kette deiner Commits ist die Hauptgeschichte deines Projekts, die Hauptzeitlinie. Was aber, wenn du an einer neuen, experimentellen Funktion arbeiten möchtest, ohne die stabile, funktionierende Hauptversion zu gefährden? Oder wenn du einen Fehler beheben musst, während gleichzeitig an einem neuen Feature gearbeitet wird?

Genau hierfür sind Branches da. Ein Branch ist im Grunde eine separate Arbeitslinie, ein eigenständiger Strang in der Entwicklungshistorie. Du kannst ihn dir wie ein Paralleluniversum vorstellen. Wenn du einen neuen Branch erstellst, erschaffst du eine exakte Kopie des aktuellen Zustands, in der du ungestört arbeiten kannst. Alle Commits, die du in diesem neuen Branch machst, existieren nur dort und haben keinerlei Einfluss auf die Hauptlinie oder andere Branches.

Technisch gesehen ist ein Branch in Git extrem leichtgewichtig. Es ist nicht mehr als ein beweglicher Zeiger, der auf einen bestimmten Commit zeigt. Wenn du einen neuen Branch erstellst, erzeugst du einfach einen neuen Zeiger. Das macht das Erstellen, Wechseln und Löschen von Branches zu einer Sache von Millisekunden.

Standardmäßig heißt der erste Branch in einem neuen Git-Repository `main` (früher oft `master`). Dies ist deine Hauptentwicklungslinie, die idealerweise immer einen stabilen, funktionierenden Zustand deines Projekts repräsentieren sollte.

**Arbeiten mit Branches: Die wichtigsten Befehle**

1.  **Einen neuen Branch erstellen:**
    Um einen neuen Branch zu erstellen, zum Beispiel für ein neues Kontaktformular, verwendest du:
    ```bash
    git branch feature/kontaktformular
    ```
    Dieser Befehl erstellt den neuen Branch, aber du befindest dich immer noch in deinem aktuellen Branch.

2.  **Zwischen Branches wechseln:**
    Um in den neu erstellten Branch zu wechseln und dort zu arbeiten, nutzt du:
    ```bash
    git switch feature/kontaktformular
    ```
    (Ältere Git-Versionen verwenden hierfür `git checkout feature/kontaktformular`, aber `switch` ist der modernere und klarere Befehl.)

3.  **Erstellen und Wechseln in einem Schritt:**
    Da man fast immer direkt nach dem Erstellen in einen neuen Branch wechseln möchte, gibt es dafür eine praktische Abkürzung:
    ```bash
    git switch -c feature/kontaktformular
    ```
    Das `-c` steht für "create".

Sobald du im Branch `feature/kontaktformular` bist, kannst du wie gewohnt arbeiten: Dateien ändern, `git add` und `git commit` ausführen. Diese neuen Commits werden nun an die Spitze dieses Branches gehängt, während der `main`-Branch unberührt an seiner alten Position verweilt.

#### Das Zusammenführen: Der Merge

Du hast deine Arbeit im Feature-Branch erfolgreich abgeschlossen, das Kontaktformular ist fertig und getestet. Nun möchtest du diese Neuerung in die Hauptversion deines Projekts, also in den `main`-Branch, integrieren. Dieser Prozess wird **Merging** (Zusammenführen) genannt.

Der Ablauf ist denkbar einfach:
1.  Wechsle zurück in den Ziel-Branch, in den du die Änderungen integrieren möchtest.
    ```bash
    git switch main
    ```

2.  Führe den Merge-Befehl aus und gib den Namen des Branches an, den du integrieren möchtest.
    ```bash
    git merge feature/kontaktformular
    ```

Git nimmt nun die Commits aus dem `feature/kontaktformular`-Branch und integriert sie in den `main`-Branch. Im einfachsten Fall, wenn sich am `main`-Branch in der Zwischenzeit nichts geändert hat, führt Git einen sogenannten "Fast-Forward"-Merge durch. Das bedeutet, Git muss nur den Zeiger von `main` auf denselben Commit verschieben, auf den auch dein Feature-Branch zeigt. Die Historie bleibt eine saubere, lineare Kette.

#### Ein typischer Arbeitsablauf in der Praxis

Das Zusammenspiel von Commits und Branches ermöglicht einen strukturierten und sicheren Entwicklungsprozess. Ein typischer Arbeitsablauf sieht so aus:

1.  **Starte auf `main`:** Stelle sicher, dass du dich auf dem `main`-Branch befindest und dieser auf dem neuesten Stand ist.
    `git switch main`

2.  **Erstelle einen neuen Branch:** Für jede neue Funktion, jeden Bugfix oder jedes Experiment erstellst du einen eigenen Branch. Gib ihm einen aussagekräftigen Namen.
    `git switch -c bugfix/navigation-alignment`

3.  **Arbeite und committe:** Nimm deine Änderungen vor und speichere deinen Fortschritt in kleinen, logischen Commits. Jeder Commit sollte eine einzelne, abgeschlossene Aufgabe repräsentieren.
    ```bash
    # ... dateien bearbeiten ...
    git add .
    git commit -m "Korrigiere Ausrichtung der Hauptnavigation auf Mobilgeräten"
    ```

4.  **Wechsle zurück und merge:** Wenn deine Arbeit auf dem Branch abgeschlossen ist, wechsle zurück zu `main` und führe die Änderungen zusammen.
    ```bash
    git switch main
    git merge bugfix/navigation-alignment
    ```

5.  **Räume auf:** Nachdem der Branch erfolgreich in `main` gemerged wurde, wird er nicht mehr benötigt. Du kannst ihn löschen, um dein Repository übersichtlich zu halten.
    ```bash
    git branch -d bugfix/navigation-alignment
    ```
    Das `-d` steht für "delete". Git wird dich warnen, wenn du versuchst, einen Branch zu löschen, dessen Änderungen noch nicht gemerged wurden – eine nützliche Sicherheitsvorkehrung.

Durch diese disziplinierte Arbeitsweise bleibt dein `main`-Branch stets sauber und funktionsfähig. Experimente und Entwicklungsarbeiten finden in isolierten Umgebungen (Branches) statt und werden erst dann in die Hauptlinie integriert, wenn sie fertig und stabil sind. Dieses Prinzip ist die Grundlage für professionelle Softwareentwicklung, egal ob du allein oder in einem großen Team arbeitest.
