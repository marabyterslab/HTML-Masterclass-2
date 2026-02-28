# Wichtige Plugins und Erweiterungen

### Wichtige Plugins und Erweiterungen

Stell dir deinen Code-Editor wie eine Werkbank vor. Als du ihn installiert hast, war er mit den grundlegendsten Werkzeugen ausgestattet: einem Hammer, ein paar Schraubendrehern und vielleicht einer Säge. Du kannst damit schon eine Menge bauen, aber für präzise, effiziente und professionelle Arbeit brauchst du Spezialwerkzeug. Genau das sind Plugins und Erweiterungen für deinen Editor. Sie verwandeln eine einfache Werkbank in ein voll ausgestattetes Hightech-Labor.

Die Welt der Erweiterungen ist riesig und kann anfangs überwältigend wirken. Für nahezu jedes erdenkliche Problem gibt es ein Plugin. Doch keine Sorge, du musst nicht Hunderte davon kennen. Ein paar wenige, aber mächtige Werkzeuge reichen aus, um deine Produktivität und die Qualität deines Codes um ein Vielfaches zu steigern. Wir konzentrieren uns hier auf die Erweiterungen für Visual Studio Code, da es der mit Abstand beliebteste Editor in der Webentwicklung ist. Die Konzepte und oft sogar die Namen der Plugins sind jedoch auf andere Editoren wie Sublime Text oder Atom übertragbar.

#### Prettier – Der unbestechliche Formatierer

Eines der ersten Plugins, das du installieren solltest, ist **Prettier - Code formatter**. Stell dir vor, du arbeitest an einem Projekt, vielleicht sogar mit anderen Entwicklern. Jeder hat einen leicht anderen Stil, Code zu schreiben. Der eine setzt Leerzeichen hier, der andere dort, Einrückungen sind mal zwei, mal vier Leerzeichen breit. Das Ergebnis ist ein unruhiges, schwer lesbares Codebild.

Prettier löst dieses Problem radikal und elegant. Es ist ein sogenannter „opinionated“ Code-Formatter. Das bedeutet, es hat eine feste Meinung darüber, wie Code aussehen sollte, und setzt diese konsequent um. Du musst keine Regeln konfigurieren (obwohl du es könntest). Du installierst es, aktivierst die Funktion „Format on Save“ (Formatieren beim Speichern) in den VS Code-Einstellungen, und von da an wird dein Code jedes Mal, wenn du die Datei speicherst, automatisch perfekt formatiert.

Ein unformatierter HTML-Schnipsel könnte so aussehen:

```html
<div class="container"> <p>Hallo Welt!</p><ul>
<li>Eins</li><li>Zwei</li>
  </ul></div>
```

Nach dem Speichern verwandelt Prettier ihn automatisch in das hier:

```html
<div class="container">
  <p>Hallo Welt!</p>
  <ul>
    <li>Eins</li>
    <li>Zwei</li>
  </ul>
</div>
```

Der Nutzen geht weit über reine Ästhetik hinaus. Konsistent formatierter Code ist schneller zu lesen, einfacher zu verstehen und leichter zu warten. Du und dein Team verschwenden keine Zeit mehr mit Diskussionen über Code-Stil, denn Prettier nimmt euch diese Arbeit ab.

#### Live Server – Die sofortige Vorschau

Bei der Entwicklung von Webseiten gibt es einen ständigen Kreislauf: Du schreibst Code im Editor, speicherst die Datei, wechselst zum Browser und lädst die Seite neu, um deine Änderungen zu sehen. Dieser Prozess wiederholt sich unzählige Male und frisst wertvolle Zeit und Konzentration.

Hier kommt **Live Server** ins Spiel. Diese Erweiterung startet einen kleinen, lokalen Entwicklungsserver direkt aus VS Code heraus. Mit einem Klick öffnet sich deine HTML-Seite in deinem Standardbrowser. Der eigentliche Zauber passiert aber jetzt: Jedes Mal, wenn du eine HTML-, CSS- oder JavaScript-Datei speicherst, lädt Live Server die Seite im Browser automatisch neu.

Du musst nicht mehr manuell zwischen den Fenstern wechseln und auf F5 drücken. Du schreibst deinen Code, speicherst, und siehst die Auswirkung deiner Änderungen quasi in Echtzeit. Dieser direkte Feedback-Loop beschleunigt den Entwicklungsprozess enorm und macht einfach mehr Spaß. Es fühlt sich an, als würdest du die Webseite direkt formen und gestalten.

#### Emmet – HTML und CSS in Lichtgeschwindigkeit

Emmet ist kein gewöhnliches Plugin, sondern eine Superkraft für jeden Webentwickler. In VS Code und vielen anderen modernen Editoren ist Emmet bereits fest integriert, aber es ist so fundamental wichtig, dass wir es hier wie eine Erweiterung behandeln müssen.

Emmet ermöglicht es dir, komplexe HTML-Strukturen mit einer einzigen, kurzen Code-Zeile zu erstellen. Anstatt mühsam öffnende und schließende Tags zu tippen, schreibst du eine Art CSS-Selektor-Abkürzung, drückst die Tab-Taste, und Emmet entfaltet die gesamte Struktur für dich.

Stell dir vor, du möchtest eine unsortierte Liste mit fünf Listenelementen erstellen, von denen jedes einen Link enthält. Manuell würdest du tippen:

```html
<ul>
  <li><a href=""></a></li>
  <li><a href=""></a></li>
  <li><a href=""></a></li>
  <li><a href=""></a></li>
  <li><a href=""></a></li>
</ul>
```

Mit Emmet schreibst du stattdessen nur das hier:

```
ul>li*5>a
```

Drücke die Tab-Taste, und wie von Zauberhand erscheint die vollständige HTML-Struktur. Emmet kann noch viel mehr: Klassen und IDs hinzufügen, Elemente nummerieren und sogar Blindtext (`lorem`) einfügen. Dieser eine Befehl:

```
div.container>nav>ul.nav-list>li.nav-item-$*4>a{Punkt $}
```

...wird zu:

```html
<div class="container">
  <nav>
    <ul class="nav-list">
      <li class="nav-item-1"><a href="">Punkt 1</a></li>
      <li class="nav-item-2"><a href="">Punkt 2</a></li>
      <li class="nav-item-3"><a href="">Punkt 3</a></li>
      <li class="nav-item-4"><a href="">Punkt 4</a></li>
    </ul>
  </nav>
</div>
```

Die Zeit, die du durch Emmet sparst, ist immens. Es zu meistern ist einer der größten Produktivitäts-Hacks, die du als Webentwickler lernen kannst.

#### Auto Rename Tag – Fehler vermeiden

Ein häufiger Fehler in HTML ist, dass man beim Ändern eines Tags vergisst, auch das zugehörige schließende Tag anzupassen. Du änderst ein `<div>` in ein `<section>`, aber am Ende des Blocks steht immer noch `</div>`. Das kann zu unerwarteten Anzeigefehlern führen, deren Suche frustrierend sein kann.

**Auto Rename Tag** ist ein kleines, aber extrem nützliches Plugin, das genau dieses Problem löst. Wenn du ein öffnendes HTML-Tag umbenennst, benennt die Erweiterung automatisch das korrespondierende schließende Tag mit um – und umgekehrt. Es ist eine simple Funktion, die dir auf lange Sicht viele Kopfschmerzen ersparen wird.

#### IntelliSense for CSS class names in HTML

Wenn dein Projekt wächst, wächst auch deine CSS-Datei. Sich an all die Klassennamen zu erinnern, die du definiert hast, wird schnell unmöglich. Die Erweiterung **IntelliSense for CSS class names in HTML** ist dein externes Gedächtnis.

Sie scannt deine verlinkten CSS-Dateien und bietet dir beim Schreiben des `class`-Attributs in deinem HTML-Code eine Autovervollständigungs-Liste all deiner verfügbaren CSS-Klassen an. Du fängst an, `class="btn` zu tippen, und schon schlägt dir der Editor `btn-primary`, `btn-secondary` und `btn-danger` vor. Das beschleunigt nicht nur das Schreiben, sondern verhindert auch Tippfehler, die zu den häufigsten und nervigsten Fehlern bei der Verknüpfung von HTML und CSS gehören.

#### GitLens – Git supercharged

Früher oder später wirst du mit Git, dem Standard für die Versionskontrolle, in Berührung kommen. VS Code hat bereits eine gute Git-Integration, aber **GitLens** hebt diese auf ein völlig neues Level.

GitLens reichert deinen Editor mit Informationen aus deinem Git-Repository an. Die vielleicht nützlichste Funktion ist die „inline blame annotation“. Am Ende jeder Code-Zeile zeigt dir GitLens dezent an, wer diese Zeile zuletzt geändert hat, wann das war und mit welcher Commit-Nachricht. Wenn du über diese Information fährst, bekommst du noch mehr Details.

Das ist unglaublich hilfreich, um die Geschichte einer Datei zu verstehen. Warum wurde dieser Code geändert? Wer hat daran gearbeitet? Statt mühsam die Git-Historie auf der Kommandozeile durchsuchen zu müssen, siehst du den Kontext direkt dort, wo du ihn brauchst: im Code selbst. GitLens bietet noch viele weitere Funktionen wie einen mächtigen Repository-Browser und Vergleichsansichten, die die Arbeit mit Git direkt im Editor nahtlos und intuitiv machen.

#### Die Werkzeugkiste personalisieren

Diese Liste ist ein exzellenter Startpunkt. Es sind die Werkzeuge, die von Millionen von Entwicklern täglich genutzt werden, um ihre Arbeit besser und schneller zu machen. Sie automatisieren lästige Routineaufgaben, verhindern Fehler und liefern dir wichtige Informationen genau dann, wenn du sie brauchst.

Der Schlüssel ist, mit einer soliden Basis zu starten und deine Werkzeugkiste nach und nach zu erweitern. Wenn du merkst, dass dich eine bestimmte Aufgabe immer wieder Zeit kostet oder frustriert, ist die Wahrscheinlichkeit hoch, dass jemand anderes dieses Problem auch schon hatte – und eine Erweiterung dafür geschrieben hat. Deine Entwicklungsumgebung ist kein starres Gebilde, sondern ein lebendiges, anpassbares Werkzeug, das mit dir und deinen Fähigkeiten wachsen sollte. Experimentiere, probiere neue Plugins aus und behalte die, die deinen Arbeitsfluss wirklich verbessern.
