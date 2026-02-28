# Grundlagen von Git und GitHub

### Grundlagen von Git und GitHub: Die Zeitmaschine für deinen Code

Kennst du das? Du arbeitest an deiner HTML-Datei, nennst sie `index.html`. Nach ein paar Änderungen speicherst du eine Sicherheitskopie als `index_alt.html`. Dann probierst du ein neues Layout aus und speicherst es als `index_neues_layout.html`. Ein Freund gibt dir Feedback, du änderst etwas und speicherst es als `index_neues_layout_final.html`. Eine Woche später stellst du fest, dass die allererste Version doch die beste war, aber du hast keine Ahnung mehr, welche Datei das ist und was du seitdem alles geändert hast. Das Chaos ist perfekt.

Genau für dieses Problem – und für viele weitere – wurde die Versionskontrolle erfunden. Und das mit Abstand beliebteste Werkzeug dafür ist Git.

#### Was ist Git? Eine neue Denkweise

Stell dir Git nicht als kompliziertes Programmierwerkzeug vor, sondern als eine Art hochentwickeltes Speicher-System mit einem perfekten Gedächtnis. Anstatt willkürlich Dateien mit neuen Namen zu speichern, hilft dir Git dabei, gezielte „Schnappschüsse“ (sogenannte **Commits**) deines gesamten Projektordners zu machen. Jeder dieser Schnappschüsse enthält eine exakte Momentaufnahme all deiner Dateien – HTML, CSS, JavaScript, Bilder, alles.

Zu jedem Schnappschuss schreibst du eine kurze Nachricht, was du gerade geändert hast, zum Beispiel „Header-Navigation hinzugefügt“ oder „Kontaktformular-Styling korrigiert“. Deine Projekthistorie wird so zu einer Kette von klar dokumentierten Änderungen. Du kannst jederzeit zu jedem beliebigen Schnappschuss in der Vergangenheit zurückspringen, Änderungen vergleichen oder versehentlich gelöschte Dateien wiederherstellen. Es ist wie eine Zeitmaschine für deinen Code.

Der entscheidende Unterschied zu anderen Systemen ist, dass Git **verteilt** ist. Das bedeutet, jeder, der am Projekt arbeitet, hat eine vollständige Kopie der gesamten Projekthistorie auf seinem eigenen Computer. Du bist nicht von einem zentralen Server abhängig, um auf frühere Versionen zuzugreifen.

#### Die drei Zonen eines Git-Projekts

Um zu verstehen, wie Git funktioniert, musst du dir drei konzeptionelle Bereiche vorstellen, zwischen denen deine Dateien hin- und herwandern:

1.  **Das Arbeitsverzeichnis (Working Directory):** Das ist einfach dein Projektordner, so wie du ihn im Finder oder Explorer siehst. Hier schreibst und bearbeitest du deine `index.html` oder deine `style.css`. Es sind deine ganz normalen, aktuellen Dateien.
2.  **Die Staging Area (oder der „Index“):** Dies ist eine Art Wartebereich. Bevor du einen Schnappschuss (Commit) erstellst, sagst du Git explizit, welche Änderungen aus deinem Arbeitsverzeichnis Teil dieses Schnappschusses sein sollen. Stell es dir wie einen Warenkorb vor: Du läufst durch den Supermarkt (dein Arbeitsverzeichnis) und legst nur die Artikel in den Korb (die Staging Area), die du an der Kasse bezahlen möchtest. Vielleicht hast du in fünf Dateien experimentiert, möchtest aber nur die Änderungen aus zwei Dateien in den nächsten Schnappschuss aufnehmen. Die Staging Area gibt dir diese Kontrolle.
3.  **Das Repository (die `.git`-Datenbank):** Das ist die eigentliche Zeitmaschine. Wenn du die Dateien aus der Staging Area „committest“, erstellt Git einen permanenten Schnappschuss und speichert ihn sicher in einem versteckten Ordner namens `.git` innerhalb deines Projektordners. Dieses Verzeichnis ist das Herz deines Git-Projekts; es enthält die gesamte Historie.

#### Der grundlegende Arbeitsablauf mit Git

Die tägliche Arbeit mit Git folgt meist einem einfachen, sich wiederholenden Zyklus. Die Befehle dafür gibst du typischerweise in einem Terminal oder einer Kommandozeile ein.

**1. Ein Repository initialisieren**

Um Git in einem bestehenden Projektordner zu aktivieren, navigierst du in deinem Terminal in diesen Ordner und führst einmalig diesen Befehl aus:

```bash
git init
```

Dieser Befehl erstellt den versteckten `.git`-Ordner. Ab diesem Moment überwacht Git deinen Projektordner.

**2. Änderungen zur Staging Area hinzufügen**

Nachdem du eine oder mehrere Dateien bearbeitet hast (z. B. deine HTML-Datei), musst du Git mitteilen, dass diese Änderungen für den nächsten Schnappschuss vorgemerkt werden sollen.

```bash
# Fügt eine einzelne Datei hinzu
git add index.html

# Fügt alle geänderten und neuen Dateien im aktuellen Ordner hinzu
git add .
```

Mit `git add` verschiebst du die Änderungen aus dem Arbeitsverzeichnis in die Staging Area.

**3. Einen Commit erstellen**

Wenn du mit den vorgemerkten Änderungen zufrieden bist, erstellst du den eigentlichen Schnappschuss – den Commit. Jeder Commit braucht eine aussagekräftige Nachricht, damit du (oder andere) später noch wisst, was passiert ist.

```bash
git commit -m "Navigation im Header mit Links zu Unterseiten ergänzt"
```

Der Teil nach `-m` (für „message“) ist deine Commit-Nachricht. Nun ist dieser Zustand deines Projekts sicher in deiner Historie gespeichert.

**4. Den Status überprüfen**

Du bist unsicher, welche Dateien geändert wurden oder was sich in der Staging Area befindet? Dieser Befehl ist dein bester Freund:

```bash
git status
```

`git status` gibt dir eine klare Übersicht über den aktuellen Zustand: welche Dateien geändert, aber noch nicht gestaged wurden, was in der Staging Area ist und ob alles auf dem neuesten Stand ist.

**5. Die Historie ansehen**

Um dir die Kette deiner bisherigen Commits anzusehen, verwendest du:

```bash
git log
```

Dieser Befehl listet alle Schnappschüsse in umgekehrter chronologischer Reihenfolge auf, inklusive Autor, Datum und der Commit-Nachricht.

#### Und was ist nun GitHub?

Bisher hat sich alles nur auf deinem lokalen Computer abgespielt. Git ist das Werkzeug, die Software, die diese Versionskontrolle ermöglicht. **GitHub** hingegen ist eine Web-Plattform, ein Dienst, der eine Heimat für deine Git-Repositories im Internet bietet.

Stell es dir so vor: Git ist der Motor, GitHub ist das Auto mit einer schicken Karosserie, Sitzen und einem Navigationssystem. GitHub nimmt deine lokalen Git-Repositories und stellt sie online zur Verfügung. Das hat riesige Vorteile:

*   **Backup:** Dein Code ist sicher in der Cloud gespeichert. Wenn dein Laptop kaputtgeht, ist dein Projekt nicht verloren.
*   **Kollaboration:** Du kannst andere Entwickler zu deinem Projekt auf GitHub einladen. Sie können den Code herunterladen, eigene Änderungen vornehmen und diese vorschlagen. GitHub bietet Werkzeuge, um diese Änderungen zu diskutieren und sauber in das Hauptprojekt zu integrieren.
*   **Portfolio:** Dein GitHub-Profil wird zu deinem öffentlichen Portfolio. Potenzielle Arbeitgeber oder Kunden können sich deine Projekte ansehen und einen Eindruck von deiner Arbeitsweise bekommen.

#### Der Arbeitsablauf mit GitHub

Um mit GitHub zu arbeiten, kommen ein paar weitere Befehle ins Spiel, die die Brücke zwischen deinem lokalen Repository und dem auf GitHub schlagen.

**1. `git clone`**

Wenn du ein bestehendes Projekt von GitHub auf deinen Computer holen möchtest, benutzt du `git clone`, gefolgt von der URL des Repositories.

```bash
git clone https://github.com/benutzername/projektname.git
```

Dies lädt nicht nur die aktuellen Dateien herunter, sondern die gesamte Git-Historie.

**2. `git push`**

Nachdem du lokal einen oder mehrere Commits erstellt hast, existieren diese Änderungen nur auf deinem Computer. Um sie mit dem Repository auf GitHub zu synchronisieren, „schiebst“ du sie dorthin:

```bash
git push
```

Damit lädst du deine neuen Commits auf den GitHub-Server hoch, sodass sie auch für andere sichtbar und verfügbar sind.

**3. `git pull`**

Wenn ein Teamkollege Änderungen gemacht und diese per `push` auf GitHub hochgeladen hat, ist dein lokales Repository nicht mehr auf dem neuesten Stand. Um die neuen Änderungen von GitHub herunterzuladen und mit deiner lokalen Version zu verschmelzen, benutzt du:

```bash
git pull
```

Dieser Befehl holt die neuesten Commits vom Server und integriert sie in dein Arbeitsverzeichnis.

#### Warum das alles für HTML entscheidend ist

Für die Entwicklung von Webseiten, selbst für einfache HTML- und CSS-Projekte, ist dieser Werkzeugkasten aus Git und GitHub revolutionär. Du kannst ohne Angst experimentieren. Probiere ein komplett neues CSS-Grid-Layout aus. Wenn es nicht funktioniert, kehrst du mit einem einzigen Befehl zum letzten funktionierenden Zustand zurück, anstatt mühsam Änderungen rückgängig zu machen.

Noch besser: GitHub bietet eine Funktion namens **GitHub Pages**. Damit kannst du deine HTML-, CSS- und JavaScript-Projekte direkt aus einem GitHub-Repository heraus als live erreichbare Webseite hosten – und das völlig kostenlos. Jedes Mal, wenn du eine Änderung per `git push` auf dein GitHub-Repository hochlädst, wird deine Webseite automatisch aktualisiert. Dies ist der perfekte Weg, um deine Projekte der Welt zu zeigen, ohne dich mit kompliziertem Webhosting auseinandersetzen zu müssen.

Git und GitHub mögen am Anfang einschüchternd wirken, aber sie sind das Fundament moderner Software- und Webentwicklung. Indem du dir von Beginn an angewöhnst, deine Projekte mit Git zu verwalten, schaffst du eine professionelle, sichere und stressfreie Arbeitsumgebung, die mit deinen Fähigkeiten und der Komplexität deiner Projekte wachsen kann.
