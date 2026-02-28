# Zusammenarbeit im Team

# Zusammenarbeit im Team

Wenn du bisher Git nur für deine eigenen Projekte genutzt hast, hast du bereits eine seiner größten Stärken kennengelernt: die Fähigkeit, eine lückenlose Historie deiner Arbeit zu erstellen und jederzeit zu alten Versionen zurückzukehren. Doch die wahre Magie von Git entfaltet sich erst, wenn du nicht mehr allein arbeitest. In der modernen Webentwicklung ist Teamarbeit die Norm, nicht die Ausnahme. Projekte sind oft zu groß und zu komplex, als dass eine einzelne Person sie stemmen könnte. Genau hier wird Git vom persönlichen Notizbuch zum zentralen Nervensystem eines jeden Entwicklungsteams.

Stell dir für einen Moment eine Welt ohne Git vor. Du arbeitest mit zwei Kollegen an einer neuen Webseite. Du bist für das HTML-Grundgerüst zuständig, eine Kollegin für das CSS und ein Kollege für das JavaScript. Wie tauscht ihr eure Arbeit aus? Schickt ihr euch ZIP-Dateien per E-Mail? „Hier ist die Version von heute, 15:30 Uhr.“ Was passiert, wenn du eine Änderung am HTML vornimmst, während deine Kollegin gerade das CSS für die alte Version schreibt? Ihre Änderungen passen plötzlich nicht mehr. Oder schlimmer: Ihr beide ändert dieselbe Datei, und die letzte Person, die speichert, überschreibt die Arbeit der anderen. Dieses Szenario ist chaotisch, fehleranfällig und frustrierend. Es ist der direkte Weg ins Projektdesaster.

Git löst dieses Problem auf eine elegante und robuste Weise. Das Grundprinzip ist die Trennung zwischen deinem lokalen Arbeitsbereich und einem zentralen, für alle zugänglichen Repository.

## Das Remote Repository: Der gemeinsame Treffpunkt

Bis jetzt lag dein Repository, also die gesamte Projekthistorie, nur auf deinem eigenen Computer. Man spricht hier von einem *lokalen Repository*. Um im Team arbeiten zu können, benötigt ihr einen gemeinsamen Ort, an dem der „offizielle“ Stand des Projektes gespeichert wird. Diesen Ort nennt man *Remote Repository* oder kurz „Remote“.

Plattformen wie GitHub, GitLab oder Bitbucket sind im Grunde nichts anderes als Hosting-Dienste für diese Remote Repositories. Sie bieten nicht nur den Speicherplatz, sondern auch eine Weboberfläche mit vielen nützlichen Werkzeugen für die Zusammenarbeit, wie die Verwaltung von Zugriffsrechten, die Nachverfolgung von Aufgaben (Issues) und die Durchführung von Code-Reviews.

Wenn du einem Team beitrittst, ist dein erster Schritt in der Regel nicht `git init`, sondern `git clone`. Mit diesem Befehl kopierst du ein bestehendes Remote Repository vollständig auf deinen Computer.

```bash
git clone https://github.com/team-projekt/neue-webseite.git
```

Das Wichtige dabei ist: Du lädst nicht nur die aktuellen Dateien herunter. Du kopierst die *gesamte* Historie, jeden einzelnen Commit, jeden Branch, der jemals erstellt wurde. Dein lokales Repository ist damit eine vollwertige, unabhängige Kopie des Projekts. Du könntest theoretisch ohne Internetverbindung weiterarbeiten, Commits erstellen und die gesamte Historie durchsuchen.

### Synchron halten: Pull und Push

Sobald du das Projekt geklont hast, ist dein lokales Repository mit dem Remote Repository verbunden. Git richtet automatisch eine Verknüpfung unter dem Standardnamen `origin` ein, der auf die ursprüngliche URL des Remote Repositorys zeigt. Nun beginnt der grundlegende Arbeitszyklus der Zusammenarbeit:

1.  **Änderungen von anderen holen (`git pull`)**: Bevor du mit deiner eigenen Arbeit beginnst, solltest du immer sicherstellen, dass du auf dem neuesten Stand bist. Vielleicht hat ein Teammitglied in der Zwischenzeit wichtige Änderungen hochgeladen. Der Befehl `git pull` holt alle neuen Commits aus dem Remote Repository und führt sie mit deinem lokalen Stand zusammen (technisch gesehen ist es eine Kombination aus `git fetch` und `git merge`).

2.  **Deine Arbeit erledigen (add, commit)**: Du arbeitest wie gewohnt an deinen Dateien. Du nimmst Änderungen vor, fügst sie mit `git add` zur Staging Area hinzu und erstellst mit `git commit -m "..."` einen oder mehrere logische Commits. All dies geschieht weiterhin nur auf deinem lokalen Rechner. Das Team weiß noch nichts von deiner Arbeit.

3.  **Deine Arbeit teilen (`git push`)**: Wenn du mit einem Arbeitspaket fertig bist und deine Commits stabil sind, teilst du sie mit dem Rest des Teams. Der Befehl `git push` lädt deine neuen, lokalen Commits in das Remote Repository hoch. Sobald der Push erfolgreich war, können deine Kollegen deine Änderungen mit einem `git pull` bei sich integrieren.

Dieser Kreislauf aus `pull`, `commit` und `push` ist das tägliche Brot der Teamarbeit mit Git.

## Branches: Die Kunst der parallelen Entwicklung

Der Pull-Push-Zyklus funktioniert gut, aber was passiert, wenn mehrere Leute gleichzeitig an großen, voneinander abhängigen Features arbeiten? Wenn alle ihre Änderungen direkt in den Hauptzweig (meist `main` oder `master` genannt) pushen, wird es schnell unübersichtlich. Der `main`-Branch könnte instabil werden, weil halbfertige Features hochgeladen werden.

Hier kommen Branches ins Spiel. Du kennst sie bereits als Möglichkeit, verschiedene Ideen auszuprobieren. Im Teamkontext werden sie zur Grundlage für einen organisierten und sicheren Arbeitsablauf. Die goldene Regel lautet: **Der `main`-Branch sollte jederzeit stabil und funktionstüchtig sein.** Direkte Commits in den `main`-Branch sind in den meisten professionellen Teams tabu.

Stattdessen wird für jede neue Aufgabe – sei es ein neues Feature, ein Bugfix oder ein Experiment – ein eigener Branch erstellt. Dieser Arbeitsablauf wird oft als **Feature-Branch-Workflow** bezeichnet und sieht typischerweise so aus:

1.  **Ausgangspunkt schaffen**: Du wechselst auf den `main`-Branch und holst dir mit `git pull` den neuesten Stand, um sicherzustellen, dass du von der aktuellsten stabilen Version ausgehst.

2.  **Neuen Branch erstellen**: Du erstellst einen neuen Branch für deine Aufgabe und gibst ihm einen aussagekräftigen Namen, zum Beispiel `feature/neue-navigation` oder `bugfix/login-fehler`.

    ```bash
    git checkout -b feature/neue-navigation
    ```

3.  **Arbeiten und committen**: Jetzt befindest du dich in deinem eigenen, isolierten Arbeitsbereich. Du kannst hier nach Belieben arbeiten, Commits erstellen, Dinge ausprobieren und sogar Fehler machen, ohne die Arbeit deiner Kollegen oder den stabilen `main`-Branch zu beeinträchtigen.

4.  **Branch veröffentlichen**: Wenn du deine Arbeit mit anderen teilen oder einfach nur ein Backup im Remote Repository haben möchtest, kannst du deinen lokalen Branch mit `git push` hochladen. Beim ersten Mal musst du Git sagen, dass es einen neuen Branch im Remote anlegen soll:

    ```bash
    git push --set-upstream origin feature/neue-navigation
    ```
    Nach diesem ersten Mal reicht ein einfaches `git push`.

## Der Pull Request: Das Gespräch über den Code

Du hast deine Arbeit auf deinem Feature-Branch erledigt und bist bereit, sie in den `main`-Branch zu integrieren. Anstatt die Änderungen nun einfach selbst zu mergen, beginnt in den meisten Teams jetzt der wichtigste Teil der Zusammenarbeit: der **Pull Request** (PR), auf manchen Plattformen auch **Merge Request** (MR) genannt.

Ein Pull Request ist im Kern eine Anfrage: „Hallo Team, ich habe hier auf meinem Branch `feature/neue-navigation` etwas fertiggestellt. Bitte schaut es euch an und gebt euer Einverständnis, es in den `main`-Branch zu übernehmen.“

Du erstellst diesen Pull Request über die Weboberfläche von GitHub oder GitLab. Dort kannst du beschreiben, was du getan hast und warum. Dein Team wird benachrichtigt und kann sich nun deine Änderungen Zeile für Zeile ansehen. Dies ist der Prozess des **Code-Reviews**. Deine Kollegen können Kommentare hinterlassen, Fragen stellen oder Verbesserungsvorschläge machen.

Dieser Schritt ist von unschätzbarem Wert:
*   **Qualitätssicherung**: Vier Augen sehen mehr als zwei. Fehler, die du übersehen hast, werden von anderen gefunden, bevor sie im Hauptprojekt landen.
*   **Wissensaustausch**: Junior-Entwickler lernen von den Kommentaren der Senioren. Senioren bekommen neue Perspektiven auf ihre eigenen Lösungen. Das gesamte Team lernt die Codebasis besser kennen.
*   **Gemeinsame Verantwortung**: Code, der durch ein Review gegangen ist, ist nicht mehr „dein“ Code, sondern „unser“ Code. Das Team trägt gemeinsam die Verantwortung für die Qualität.

Wenn du Feedback erhältst, erstellst du einfach neue Commits auf deinem Feature-Branch, um die Anmerkungen umzusetzen, und pushst diese. Der Pull Request aktualisiert sich automatisch. Sobald alle zufrieden sind und der PR genehmigt wurde, werden deine Änderungen in den `main`-Branch gemerged. Danach kann der nun veraltete Feature-Branch gelöscht werden.

## Konflikte: Wenn zwei Welten kollidieren

Egal wie gut ein Team organisiert ist, irgendwann passiert es: Du versuchst, mit `git pull` die neuesten Änderungen zu holen, oder du willst deinen Branch in den `main`-Branch mergen, und Git hält inne mit einer beunruhigenden Nachricht: `CONFLICT`.

Keine Panik, das ist völlig normal und Teil des Prozesses. Ein Merge-Konflikt entsteht, wenn du und ein anderes Teammitglied dieselben Zeilen in derselben Datei auf unterschiedliche Weise geändert habt. Git ist eine unglaublich schlaue Maschine, aber an diesem Punkt kann es keine Entscheidung treffen. Es weiß nicht, welche Änderung die „richtige“ ist – deine, die deines Kollegen oder vielleicht eine Kombination aus beiden. Also gibt es die Verantwortung an dich, den Menschen, zurück.

Wenn ein Konflikt auftritt, markiert Git die betroffenen Stellen in der Datei direkt im Code. Das sieht dann etwa so aus:

```html
<<<<<<< HEAD
  <div class="navigation-main">
    <!-- Mein neuer Navigations-Code -->
  </div>
=======
  <div class="main-nav">
    <!-- Der Code des Kollegen für die Navigation -->
  </div>
>>>>>>> other-branch-name
```

Git hat die Datei für dich umgeschrieben und zeigt dir beide Versionen:
*   Der Abschnitt zwischen `<<<<<<< HEAD` und `=======` ist deine lokale Änderung (die Version aus deinem aktuellen Branch).
*   Der Abschnitt zwischen `=======` und `>>>>>>>` ist die Änderung, die du gerade hereinholen wolltest (die Version aus dem anderen Branch).

Deine Aufgabe ist es nun, den Konflikt aufzulösen:
1.  Öffne die betroffene Datei in deinem Editor.
2.  Entscheide, wie der endgültige Code aussehen soll. Vielleicht ist deine Version richtig, vielleicht die andere, oder du musst beide kombinieren und anpassen.
3.  Lösche die Konfliktmarker (`<<<<<<<`, `=======`, `>>>>>>>`) und den Code, den du nicht behalten möchtest. Am Ende sollte nur der korrekte, saubere Code übrig bleiben.
4.  Speichere die Datei.
5.  Füge die nun korrigierte Datei mit `git add` der Staging Area hinzu. Damit signalisierst du Git: „Ich habe den Konflikt in dieser Datei gelöst.“
6.  Schließe den Merge-Prozess mit `git commit` ab. Git schlägt dir bereits eine passende Commit-Nachricht vor, die du meist einfach übernehmen kannst.

Konflikte fühlen sich am Anfang vielleicht einschüchternd an, aber sie sind ein lösbares Problem. Der beste Weg, schwere Konflikte zu vermeiden, ist, regelmäßig `git pull` auszuführen und deine Branches klein und fokussiert zu halten. Je kürzer die Lebensdauer eines Branches, desto geringer die Wahrscheinlichkeit, dass sich dein Code zu weit vom `main`-Branch entfernt.

Zusammenarbeit mit Git ist mehr als nur das Teilen von Dateien. Es ist ein strukturierter Prozess, der Kommunikation fördert, Qualität sichert und es einem Team ermöglicht, parallel und doch koordiniert an komplexen Projekten zu arbeiten. Die Befehle sind die Werkzeuge, aber der wahre Gewinn liegt im Workflow, den sie ermöglichen.
