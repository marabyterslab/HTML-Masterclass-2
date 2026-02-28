# Commits und Branches

### Commits und Branches: Die Bausteine der Versionskontrolle

Stell dir vor, du schreibst den Code für eine komplexe neue Funktion deiner Webseite. Nach stundenlanger Arbeit funktioniert alles perfekt. Doch dann entscheidest du dich, eine kleine Sache zu optimieren, und plötzlich ist alles kaputt. Nichts geht mehr, und du weißt nicht einmal genau, welche deiner letzten Änderungen das Problem verursacht hat. Ohne Versionskontrolle wäre das ein Albtraum. Mit Git ist es nur eine kleine Unannehmlichkeit. Die Werkzeuge, die dir hier helfen, sind Commits und Branches – die fundamentalen Bausteine deiner Arbeit mit Git.

#### Der Commit: Dein persönlicher Speicherpunkt

Ein **Commit** ist im Grunde ein Schnappschuss deines gesamten Projekts zu einem bestimmten Zeitpunkt. Man kann ihn sich wie einen Speicherpunkt in einem Videospiel vorstellen. Jedes Mal, wenn du einen wichtigen Meilenstein erreicht hast – eine Funktion fertiggestellt, einen Bug behoben oder auch nur einen logischen Arbeitsschritt abgeschlossen hast –, erstellst du einen Commit. Dieser Speicherpunkt wird dauerhaft in der Projekthistorie von Git gesichert.

Das Besondere an einem Commit ist, dass er nicht nur die Änderungen an den Dateien enthält, sondern den Zustand *aller* Dateien im Projekt zu diesem Zeitpunkt festhält. Jeder Commit hat eine einzigartige Kennung, einen sogenannten „Hash“ (z. B. `a1b2c3d4...`), einen Autor, ein Datum und – ganz wichtig – eine Commit-Nachricht.

##### Die Commit-Nachricht: Deine Notiz an die Zukunft

Die Commit-Nachricht ist deine Chance, in klaren Worten zu beschreiben, *was* und *warum* du etwas geändert hast. Eine gute Commit-Nachricht ist Gold wert. Monate später, wenn du oder jemand aus deinem Team versucht nachzuvollziehen, warum ein bestimmter Codeabschnitt so aussieht, wie er aussieht, wird eine Nachricht wie „Fix user login bug“ viel hilfreicher sein als „updates“ oder „stuff“. Nimm dir die Zeit, aussagekräftige Nachrichten zu schreiben. Dein zukünftiges Ich wird es dir danken.

##### Der Weg zum Commit: Die Staging Area

Bevor du einen Commit erstellst, durchlaufen deine Änderungen einen wichtigen Zwischenschritt: die **Staging Area** (manchmal auch „Index“ genannt). Stell dir dein Projektverzeichnis als deine Werkbank vor (das „Working Directory“). Hier bearbeitest du deine HTML-, CSS- und JavaScript-Dateien.

Wenn du mit einer Änderung zufrieden bist und sie für den nächsten Speicherpunkt (Commit) vormerken möchtest, fügst du sie zur Staging Area hinzu. Du kannst dir die Staging Area wie eine Kiste vorstellen, in die du sorgfältig ausgewählte Werkstücke für den nächsten Transport legst. Du musst nicht alles auf einmal hinzufügen. Vielleicht hast du an drei Dateien gearbeitet, aber nur die Änderungen in zwei davon gehören logisch zusammen und sollen in den nächsten Commit.

Dieser Prozess gibt dir die volle Kontrolle. Du kannst präzise und atomare Commits erstellen, die jeweils nur eine einzige, logische Änderung enthalten. Das macht deine Projekthistorie sauber, lesbar und nachvollziehbar.

Der typische Arbeitsablauf sieht so aus:

1.  **Änderung durchführen:** Du bearbeitest eine oder mehrere Dateien in deinem Projekt.
2.  **Änderungen zur Staging Area hinzufügen:** Mit dem Befehl `git add` wählst du aus, welche Änderungen du für den nächsten Commit vorbereiten möchtest.
3.  **Commit erstellen:** Mit `git commit` nimmst du alle Änderungen, die sich in der Staging Area befinden, und erstellst daraus einen neuen, dauerhaften Schnappschuss in deiner Projekthistorie.

Schauen wir uns das an einem konkreten Beispiel an. Du hast deine `index.html` und dein `style.css` geändert. Du möchtest aber nur die HTML-Änderung committen.

```bash
# Zeigt dir den aktuellen Status deines Projekts.
# Git wird dir sagen, dass 'index.html' und 'style.css' geändert wurden.
git status

# Füge nur die index.html zur Staging Area hinzu.
git add index.html

# Erstelle den Commit mit den Änderungen aus der Staging Area.
git commit -m "Füge Navigationsleiste zur Startseite hinzu"
```

Jetzt ist ein neuer Speicherpunkt erstellt, der nur die Änderung an der `index.html` enthält. Deine Änderungen an `style.css` sind immer noch in deinem Arbeitsverzeichnis, bereit für einen späteren, separaten Commit. Mit `git log` kannst du dir die Historie aller deiner Commits ansehen.

#### Branches: Parallele Welten für deinen Code

Commits allein sind schon mächtig, aber ihre wahre Stärke entfalten sie erst in Kombination mit **Branches**. Ein Branch (deutsch: Zweig) ist im Grunde eine eigenständige Entwicklungslinie innerhalb deines Projekts.

Stell dir die Historie deines Projekts als einen Zeitstrahl vor, auf dem jeder Commit ein Punkt ist. Der Hauptentwicklungszweig, der in der Regel die stabile, funktionierende Version deines Projekts enthält, heißt meistens `main` (früher oft `master`).

Was aber, wenn du eine neue, experimentelle Funktion entwickeln willst? Du möchtest den stabilen `main`-Branch nicht mit unfertigem Code „verschmutzen“. Hier kommt ein neuer Branch ins Spiel.

Wenn du einen neuen Branch erstellst, sagst du Git im Prinzip: „Ich möchte hier eine neue, parallele Zeitlinie beginnen, die auf dem aktuellen Stand basiert.“ Ab diesem Moment existieren zwei Linien: der ursprüngliche `main`-Branch und dein neuer Branch, zum Beispiel namens `neues-feature`.

Das Tolle daran ist, dass ein Branch in Git extrem „leicht“ ist. Es ist nicht so, als würdest du dein ganzes Projektverzeichnis kopieren. Ein Branch ist im Grunde nur ein kleiner, beweglicher Zeiger, der auf einen bestimmten Commit zeigt. Das Erstellen und Wechseln von Branches ist daher blitzschnell.

##### Wofür brauchst du Branches?

1.  **Sicheres Experimentieren:** Du kannst neue Ideen ausprobieren, Code komplett umstrukturieren oder Bibliotheken testen, ohne Angst haben zu müssen, die funktionierende Hauptversion zu zerstören. Wenn die Idee nicht funktioniert, wirfst du den Branch einfach weg. Kein Schaden angerichtet.
2.  **Parallele Entwicklung:** In einem Team kann jeder Entwickler an seiner eigenen Funktion in einem separaten Branch arbeiten. Niemand kommt sich in die Quere. Wenn eine Funktion fertig ist, werden die Änderungen aus dem Feature-Branch wieder in den `main`-Branch integriert.
3.  **Organisation:** Du kannst Branches für alles Mögliche verwenden: neue Features (`feature/user-profile`), Bugfixes (`hotfix/login-error`), Redesigns und so weiter. Das hält deine Arbeit sauber und strukturiert.

##### Arbeiten mit Branches

Die Arbeit mit Branches ist unkompliziert. Hier sind die grundlegenden Befehle:

```bash
# Zeigt dir alle vorhandenen Branches an. Der aktive Branch ist mit einem * markiert.
git branch

# Erstellt einen neuen Branch namens 'feature/kontaktformular'
git branch feature/kontaktformular

# Wechselt in den neu erstellten Branch. Ab jetzt finden alle deine Commits
# auf dieser neuen Zeitlinie statt, ohne 'main' zu beeinflussen.
git switch feature/kontaktformular
```

Jetzt bist du in deinem neuen Branch. Du kannst hier arbeiten, neue Commits erstellen, und der `main`-Branch bleibt davon völlig unberührt. Wenn du deine Arbeit am Kontaktformular abgeschlossen und getestet hast, möchtest du diese Änderungen natürlich in dein Hauptprojekt übernehmen.

##### Das Zusammenführen: `git merge`

Der Prozess, die Änderungen von einem Branch in einen anderen zu integrieren, nennt sich **Merging**. Du wechselst dazu zurück in den Ziel-Branch (in der Regel `main`) und führst den Befehl `git merge` aus.

```bash
# Wechsle zurück zum Haupt-Branch
git switch main

# Führe die Historie von 'feature/kontaktformular' mit der von 'main' zusammen.
git merge feature/kontaktformular
```

Git analysiert nun die Commits in beiden Branches und fügt die Änderungen aus deinem Feature-Branch in den `main`-Branch ein. In den meisten Fällen geschieht dies vollautomatisch und problemlos. Dein `main`-Branch enthält jetzt den Code für das neue Kontaktformular und ist auf dem neuesten Stand. Nach einem erfolgreichen Merge kannst du den Feature-Branch löschen, da er seinen Zweck erfüllt hat.

Manchmal kann es vorkommen, dass du und ein Kollege (oder du selbst in zwei verschiedenen Branches) dieselbe Zeile in derselben Datei geändert habt. In diesem Fall kann Git nicht automatisch entscheiden, welche Version die richtige ist. Es entsteht ein **Merge-Konflikt**. Das ist aber kein Grund zur Panik. Git stoppt den Merge-Prozess, markiert die problematischen Stellen in den betroffenen Dateien und überlässt dir die Entscheidung, wie der Code am Ende aussehen soll. Sobald du den Konflikt manuell gelöst hast, schließt du den Merge ab.

Commits und Branches sind das Herzstück von Git. Commits geben dir die Sicherheit, jeden Schritt deiner Arbeit nachvollziehen und wiederherstellen zu können. Branches geben dir die Freiheit, strukturiert, parallel und ohne Risiko neue Wege zu gehen. Wenn du diese beiden Konzepte verstanden hast, hast du den Schlüssel zur modernen, professionellen Software- und Webentwicklung in der Hand.
