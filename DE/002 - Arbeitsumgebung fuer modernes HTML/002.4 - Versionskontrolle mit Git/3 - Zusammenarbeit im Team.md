# Zusammenarbeit im Team

### Zusammenarbeit im Team: Git als gemeinsames Fundament

Bisher hast du Git vielleicht vor allem als eine Art Super-Backup für deine eigenen Projekte kennengelernt. Du konntest Schnappschüsse deines Codes erstellen, zu früheren Versionen zurückspringen und ohne Angst experimentieren. Das allein ist schon unglaublich wertvoll. Aber die wahre Stärke von Git entfaltet sich erst, wenn du nicht mehr allein arbeitest. Sobald zwei oder mehr Personen an demselben Projekt beteiligt sind, wird Git vom nützlichen Werkzeug zum unverzichtbaren Rückgrat der gesamten Zusammenarbeit.

Die grundlegende Idee hinter Git ist, dass es ein *verteiltes* Versionskontrollsystem ist. Das bedeutet, jeder im Team hat eine vollständige Kopie des gesamten Projektverlaufs auf seinem eigenen Rechner. Das ist ein entscheidender Unterschied zu älteren Systemen, bei denen es nur einen zentralen Server gab und jeder direkt darauf arbeitete. Doch wie bleiben all diese verteilten Kopien synchron? Wie stellt man sicher, dass die Arbeit von Person A nicht versehentlich die Arbeit von Person B überschreibt? Die Antwort liegt in der Kombination aus Remote-Repositories und einem disziplinierten Arbeitsablauf, den wir uns jetzt ansehen werden.

#### Das zentrale Nervensystem: Remote-Repositories

Auch wenn jeder eine lokale Kopie hat, braucht ein Team einen gemeinsamen, offiziellen Anlaufpunkt – eine „Source of Truth“. Diesen Ort nennen wir **Remote-Repository** oder einfach „Remote“. Stell es dir wie ein zentrales Lager vor, in dem die offizielle, aktuellste Version des Projekts aufbewahrt wird. Plattformen wie GitHub, GitLab oder Bitbucket sind spezialisierte Anbieter, die solche Remote-Repositories für dich hosten und mit nützlichen Werkzeugen wie Issue-Tracking und Code-Reviews anreichern.

Wenn du einem bestehenden Projekt beitrittst, ist dein erster Schritt nicht `git init`, sondern `git clone`. Mit diesem Befehl lädst du eine exakte Kopie des Remote-Repositories auf deinen Computer, inklusive der gesamten Historie.

```bash
git clone https://github.com/projekt-team/unsere-webseite.git
```

Nachdem du den Befehl ausgeführt hast, hast du einen neuen Ordner namens `unsere-webseite` auf deinem Rechner. Dieses lokale Repository ist bereits mit dem Remote-Repository verbunden. Git gibt dieser Standardverbindung den Namen `origin`. Du kannst deine konfigurierten Remotes jederzeit mit `git remote -v` überprüfen.

Von nun an gibt es zwei grundlegende Befehle, um deine lokale Kopie mit dem Remote zu synchronisieren:

1.  **`git push`**: Mit diesem Befehl „schiebst“ du deine lokalen, committeten Änderungen zum Remote-Repository hoch. Du teilst deine fertige Arbeit also mit dem Rest des Teams.
2.  **`git pull`**: Mit diesem Befehl „ziehst“ du die neuesten Änderungen, die andere Teammitglieder auf den Remote gepusht haben, herunter und integrierst sie in deine lokale Arbeitskopie.

Technisch gesehen ist `git pull` eine Kombination aus zwei anderen Befehlen: `git fetch` (was die Änderungen nur herunterlädt, aber noch nicht integriert) und `git merge` (was die heruntergeladenen Änderungen mit deinem aktuellen Stand zusammenführt). Für den Anfang reicht es aber völlig aus, `git pull` als den Befehl zu kennen, um dich auf den neuesten Stand zu bringen.

#### Parallele Welten: Die Macht der Branches

Stell dir vor, das ganze Team würde ständig direkt auf dem Hauptentwicklungszweig (oft `main` oder `master` genannt) arbeiten. Jeder `push` würde sofort den Code für alle anderen verändern. Das wäre pures Chaos. Ein Teammitglied könnte unfertigen Code hochladen, der das Projekt für alle anderen unbrauchbar macht, während eine andere Person gerade versucht, einen wichtigen Bug zu beheben.

Hier kommen Branches ins Spiel. Ein Branch ist wie eine Abzweigung vom Hauptweg, eine Art paralleles Universum deines Projekts. Du kannst einen neuen Branch erstellen, um an einem neuen Feature oder einem Bugfix zu arbeiten, ohne den stabilen `main`-Branch zu beeinträchtigen. Dein Branch ist deine private Werkstatt. Du kannst darin experimentieren, Commits erstellen, Fehler machen und alles korrigieren, ohne dass es irgendjemanden im Team stört.

Ein typischer Arbeitsablauf für ein neues Feature sieht so aus:

1.  **Stelle sicher, dass dein `main`-Branch aktuell ist.** Bevor du mit etwas Neuem beginnst, solltest du immer die neueste Version des Projekts haben.

    ```bash
    git checkout main
    git pull origin main
    ```

2.  **Erstelle einen neuen Branch für deine Aufgabe.** Gib ihm einen aussagekräftigen Namen, damit jeder weiß, worum es geht. Eine gängige Konvention ist, den Typ der Arbeit (z.B. `feature`, `fix`, `docs`) und eine kurze Beschreibung zu verwenden.

    ```bash
    git checkout -b feature/neues-kontaktformular
    ```
    Der Befehl `checkout -b` ist eine Abkürzung, die einen neuen Branch erstellt (`-b`) und dich direkt dorthin wechseln lässt (`checkout`).

3.  **Arbeite an deinem Feature.** Jetzt bist du in deinem sicheren Branch. Du kannst HTML-Dateien ändern, CSS hinzufügen, Commits erstellen – ganz wie du es gewohnt bist.

    ```bash
    # ... du änderst Code, speicherst Dateien ...
    git add .
    git commit -m "Feat: Grundstruktur für Kontaktformular hinzugefügt"
    ```

4.  **Teile deinen Branch mit dem Team.** Wenn du deine Arbeit zeigen, ein Backup erstellen oder mit jemand anderem auf demselben Branch arbeiten möchtest, pushst du ihn zum Remote-Repository. Beim ersten Mal musst du Git sagen, wohin der Branch gepusht werden soll.

    ```bash
    git push -u origin feature/neues-kontaktformular
    ```
    Das Flag `-u` (kurz für `--set-upstream`) merkt sich diese Verbindung. Zukünftig reicht ein einfaches `git push` aus diesem Branch, um ihn auf `origin` zu aktualisieren.

#### Wenn Welten kollidieren: Merging und Konflikte

Sobald deine Arbeit auf dem Feature-Branch abgeschlossen und getestet ist, möchtest du sie natürlich in den `main`-Branch integrieren. Dieser Prozess wird **Merging** genannt. Du fügst quasi die Änderungen aus deinem Branch in einen anderen Branch (z. B. `main`) ein.

Manchmal verläuft das reibungslos. Wenn in der Zwischenzeit niemand anderes dieselben Codezeilen im `main`-Branch verändert hat, kann Git die Änderungen einfach wie ein Reißverschluss zusammenführen.

Oft kommt es aber zu **Merge-Konflikten**. Keine Panik! Ein Merge-Konflikt ist keine Fehlermeldung, sondern eine Frage von Git an dich. Er tritt auf, wenn du und ein anderes Teammitglied dieselbe Zeile in derselben Datei auf unterschiedliche Weise geändert habt. Git weiß nicht, welche Version die richtige ist, und bittet dich als Entwickler, die Entscheidung zu treffen.

Wenn ein Konflikt auftritt, markiert Git die betroffene Stelle in der Datei direkt im Code, etwa so:

```html
<<<<<<< HEAD
  <p>Willkommen auf unserer brandneuen Webseite!</p>
=======
  <p>Herzlich Willkommen auf unserer überarbeiteten Homepage!</p>
>>>>>>> feature/neue-begruessung
```

Git zeigt dir hier ganz klar das Problem:

*   Der Teil zwischen `<<<<<<< HEAD` und `=======` ist die Version aus deinem aktuellen Branch (in dem du den Merge durchführst, z.B. `main`). `HEAD` ist der Zeiger auf den aktuellen Commit.
*   Der Teil zwischen `=======` und `>>>>>>> feature/neue-begruessung` ist die Version aus dem Branch, den du hereinmergen möchtest.

Deine Aufgabe ist es nun, diese Datei zu öffnen und den Konflikt manuell zu lösen:

1.  Entscheide, welcher Code behalten werden soll. Manchmal ist es die eine Version, manchmal die andere, und oft ist es eine Kombination aus beidem.
2.  Lösche die Konfliktmarker (`<<<<<<<`, `=======`, `>>>>>>>`) und den Code, den du nicht mehr brauchst.
3.  Speichere die Datei.
4.  Füge die nun korrigierte Datei zum Staging-Bereich hinzu (`git add <dateiname>`).
5.  Schließe den Merge mit einem neuen Commit ab (`git commit`). Git schlägt dir hierfür meist schon eine passende Commit-Nachricht vor.

Merge-Konflikte fühlen sich am Anfang vielleicht einschüchternd an, aber sie sind ein normaler und wichtiger Teil der Teamarbeit. Sie zwingen Entwickler zur Kommunikation und stellen sicher, dass keine Arbeit versehentlich verloren geht.

#### Mehr als nur Code: Pull Requests als Diskussionsforum

In professionellen Teams wird ein Merge in den `main`-Branch selten direkt auf dem lokalen Rechner durchgeführt. Stattdessen nutzt man eine Funktion von Plattformen wie GitHub, die sich **Pull Request** (PR) oder bei GitLab **Merge Request** (MR) nennt.

Ein Pull Request ist eine formelle Anfrage, deine Änderungen aus deinem Feature-Branch in einen anderen Branch (z.B. `main`) zu mergen. Aber er ist so viel mehr als das: Er ist ein Forum für **Code-Reviews**.

Der Prozess sieht typischerweise so aus:
1.  Du pushst deinen fertigen Feature-Branch auf den Remote (`origin`).
2.  Auf der Weboberfläche von GitHub (oder einer ähnlichen Plattform) erstellst du einen neuen Pull Request. Du gibst an: „Ich möchte meinen Branch `feature/neues-kontaktformular` in den Branch `main` mergen.“
3.  Du fügst eine Beschreibung hinzu, was du getan hast und warum. Vielleicht verlinkst du auch auf ein dazugehöriges Ticket im Projektmanagement-Tool.
4.  Du weist ein oder mehrere Teammitglieder als „Reviewer“ zu.
5.  Diese Reviewer schauen sich nun deinen Code an. Sie können Kommentare direkt zu einzelnen Codezeilen hinterlassen, Fragen stellen, Verbesserungsvorschläge machen oder auf potenzielle Fehler hinweisen.
6.  Es entsteht eine Diskussion. Du kannst auf die Kommentare antworten und eventuell geforderte Änderungen direkt in deinem Branch durchführen und erneut pushen. Der Pull Request aktualisiert sich automatisch.
7.  Erst wenn mindestens ein (oder je nach Teamregel auch mehrere) Reviewer den Code für gut befunden und genehmigt haben („Approved“), wird der Pull Request per Klick auf einen Button auf der Webseite gemerged.

Dieser Prozess stellt eine enorme Qualitätssteigerung sicher. Vier Augen sehen mehr als zwei. Fehler werden früher gefunden, Wissen wird im Team geteilt und es entsteht ein einheitlicherer Programmierstil. Der Pull Request ist das Herzstück der modernen, kollaborativen Softwareentwicklung und eine der wichtigsten Praktiken, die du dir aneignen kannst.
