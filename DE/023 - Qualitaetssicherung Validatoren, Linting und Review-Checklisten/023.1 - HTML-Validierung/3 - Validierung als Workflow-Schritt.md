# Validierung als Workflow-Schritt

### Vom Code zur Qualität: Validierung als fester Bestandteil deines Workflows

Stell dir vor, du schreibst einen wichtigen Brief. Du achtest auf Rechtschreibung, Grammatik und den richtigen Ton. Du würdest ihn wahrscheinlich nicht einfach losschicken, ohne ihn noch einmal durchzulesen. Warum? Weil Fehler den Inhalt missverständlich machen oder einen unprofessionellen Eindruck hinterlassen können. Beim Schreiben von HTML-Code ist es ganz ähnlich. Dein Code ist eine Nachricht an den Browser, und diese Nachricht sollte so klar und unmissverständlich wie möglich sein.

Viele Entwickler verlassen sich zu Beginn ihrer Karriere auf einen trügerischen Freund: den Browser. Du schreibst etwas HTML, lädst die Seite in Chrome, Firefox oder Safari, und sie sieht gut aus. Problem gelöst, oder? Nicht ganz. Moderne Browser sind extrem fehler-tolerant. Sie sind darauf programmiert, aus dem „kaputtesten“ Code noch irgendetwas Sinnvolles zu rendern. Sie fügen fehlende schließende Tags hinzu, ignorieren falsch verschachtelte Elemente und versuchen zu erraten, was du eigentlich gemeint hast.

Das klingt erst einmal praktisch, ist aber eine gefährliche Falle. Nur weil dein Code in *deinem* Browser auf *deinem* Computer heute funktioniert, heißt das nicht, dass er korrekt ist. Es bedeutet nur, dass der Browser gut im Raten war. Ein anderer Browser, ein zukünftiges Update oder ein Screenreader für barrierefreies Surfen ist vielleicht nicht so nachsichtig. Die Folge sind unvorhersehbare Darstellungsfehler, schlechte Performance oder eine unzugängliche Webseite.

Hier kommt die Validierung ins Spiel. Validierung ist der Prozess, bei dem du deinen HTML-Code gegen die offizielle Spezifikation des World Wide Web Consortiums (W3C) prüfst. Sie ist quasi die Rechtschreib- und Grammatikprüfung für deinen Code. Ein Validator ist kein Meinungs-Tool; er ist ein Schiedsrichter, der deinen Code mit dem offiziellen Regelwerk abgleicht und dir objektiv sagt, wo du gegen die Regeln verstoßen hast.

#### Die Illusion des funktionierenden Codes

Betrachten wir ein einfaches Beispiel. Du möchtest eine unsortierte Liste mit drei Einträgen erstellen. In der Eile vergisst du, ein `<li>`-Element zu schließen:

```html
<!-- Fehlerhaftes HTML -->
<ul>
  <li>Erster Punkt
  <li>Zweiter Punkt</li>
  <li>Dritter Punkt</li>
</ul>
```

Wenn du diese Datei im Browser öffnest, wirst du höchstwahrscheinlich eine perfekt aussehende Liste sehen. Der Browser erkennt, dass nach dem Text "Erster Punkt" ein neues `<li>`-Element beginnt, und schließt das vorherige implizit für dich. Du bemerkst den Fehler nicht.

Gibst du diesen Code jedoch in einen Validator ein, wie den offiziellen [W3C Markup Validation Service](https://validator.w3.org/), erhältst du eine klare Fehlermeldung. Sie wird dich darauf hinweisen, dass ein `<li>`-Tag nicht geschlossen wurde, bevor das nächste begann. Der korrekte, valide Code wäre:

```html
<!-- Valides HTML -->
<ul>
  <li>Erster Punkt</li>
  <li>Zweiter Punkt</li>
  <li>Dritter Punkt</li>
</ul>
```

In diesem kleinen Beispiel sind die Auswirkungen minimal. Aber stell dir eine komplexe Seite mit Hunderten von verschachtelten `<div>`-Elementen vor. Ein einziges fehlendes schließendes Tag kann die gesamte nachfolgende DOM-Struktur durcheinanderbringen. Der Browser versucht vielleicht, den Fehler zu kompensieren, aber das Ergebnis kann ein komplett zerschossenes Layout sein, dessen Ursache du stundenlang suchen musst. Ein Validator findet diesen Fehler in Sekunden.

#### Validierung ist kein nachträglicher Schritt, sondern ein Prozess

Der größte Fehler, den du machen kannst, ist, die Validierung als einen letzten, lästigen Schritt vor der Veröffentlichung zu betrachten. „Ich baue erst mal alles fertig, und dann lasse ich am Ende mal den Validator drüberlaufen.“ Dieser Ansatz führt oft zu Frustration, weil du am Ende vor einer langen Liste von Fehlern stehst, die sich über das gesamte Projekt angesammelt haben.

Wirklich professionelle Entwickler integrieren die Validierung tief in ihren täglichen Arbeitsablauf. Sie wird zu einer Gewohnheit, zu einem Sicherheitsnetz, das sie bei jedem Schritt begleitet.

**1. Manuelle Validierung als Lernwerkzeug**

Wenn du gerade erst anfängst, ist die manuelle Nutzung des W3C-Validators eine hervorragende Übung. Kopiere deinen Code regelmäßig in das Textfeld der Webseite oder gib die URL deiner Testseite an. Du lernst dadurch nicht nur, häufige Fehler zu vermeiden, sondern bekommst auch ein tieferes Verständnis für die HTML-Spezifikation. Du siehst nicht nur, *dass* etwas falsch ist, sondern auch *warum*.

**2. Browser-Erweiterungen für den schnellen Check**

Der nächste Schritt zur Integration in deinen Workflow sind Browser-Erweiterungen. Für alle gängigen Browser gibt es Add-ons, die eine HTML-Validierung mit nur einem Klick direkt auf der angezeigten Seite durchführen. Dies ist weitaus schneller als das Kopieren und Einfügen von Code. Jedes Mal, wenn du eine größere Änderung vorgenommen und im Browser neu geladen hast, kannst du mit einem Klick prüfen, ob noch alles valide ist.

**3. Integration in den Code-Editor: Linting in Echtzeit**

Der wirkungsvollste Schritt ist, die Validierung direkt in deinen Code-Editor zu verlagern. Werkzeuge, die dies tun, werden „Linter“ genannt. Ein Linter ist ein Programm, das deinen Code analysiert, während du ihn schreibst, und dich in Echtzeit auf Fehler, aber auch auf stilistische Probleme oder schlechte Praktiken hinweist.

Für Editoren wie Visual Studio Code, Sublime Text oder Atom gibt es unzählige Erweiterungen (z. B. HTMLHint, linthtml oder die in Emmet integrierten Checks). Sobald du eine solche Erweiterung installiert und konfiguriert hast, werden Fehler direkt im Code farblich markiert oder mit einer kleinen Wellenlinie unterstrichen – genau wie die Rechtschreibprüfung in einem Textverarbeitungsprogramm.

Ein Linter könnte dich zum Beispiel warnen, wenn du:
*   eine ID mehrfach im selben Dokument verwendest.
*   veraltete Tags wie `<font>` oder `<center>` benutzt.
*   `alt`-Attribute bei `<img>`-Tags vergisst.
*   spezielle Zeichen wie `&` oder `<` nicht korrekt als Entitäten (`&amp;`, `&lt;`) kodierst.

Dieser Ansatz ist revolutionär, weil er Fehler verhindert, bevor sie überhaupt entstehen. Du bekommst sofortiges Feedback und entwickelst ganz von allein einen saubereren und korrekteren Programmierstil.

**4. Automatisierte Validierung im Build-Prozess**

In professionellen Teams und größeren Projekten geht man noch einen Schritt weiter. Hier wird die Validierung Teil des automatisierten „Build-Prozesses“. Bevor neuer Code in das Hauptprojekt integriert wird (z. B. in ein Git-Repository), laufen automatisch Skripte, die eine Reihe von Qualitätsprüfungen durchführen. Eine dieser Prüfungen ist die HTML-Validierung.

Wenn ein Entwickler versucht, invaliden HTML-Code beizusteuern, schlägt dieser Prozess fehl. Der Code kann erst dann eingereicht werden, wenn alle Validierungsfehler behoben sind. Dies stellt sicher, dass die Codebasis des gesamten Projekts dauerhaft sauber und standardkonform bleibt. Es ist das ultimative Sicherheitsnetz, das die Qualität für das gesamte Team erzwingt.

#### Mehr als nur Syntax: Der Wert für die Qualitätssicherung

Valider Code ist die Grundlage, aber er ist nicht alles. Ein Validator kann dir sagen, ob deine Syntax korrekt ist, aber er kann dir nicht sagen, ob du die richtigen semantischen Tags verwendet hast. Er kann prüfen, ob ein `<img>`-Tag ein `alt`-Attribut hat, aber nicht, ob der Text darin sinnvoll und beschreibend ist.

Deshalb ist die technische Validierung nur ein Teil einer umfassenden Qualitätssicherung. Sie sollte immer durch manuelle Überprüfungen ergänzt werden, die oft in Form von Code-Reviews durch Kollegen oder anhand von Checklisten stattfinden. Eine solche Checkliste könnte Punkte enthalten wie:

*   **HTML-Validität:** Ist der Code W3C-valide? (Der erste und einfachste Check)
*   **Semantik:** Werden HTML5-Elemente wie `<main>`, `<nav>`, `<article>` und `<section>` korrekt und sinnvoll eingesetzt?
*   **Barrierefreiheit (Accessibility):** Sind alle interaktiven Elemente per Tastatur erreichbar? Sind Kontraste ausreichend? Werden ARIA-Rollen korrekt verwendet?
*   **Lesbarkeit:** Ist der Code sauber formatiert und verständlich für andere Entwickler?

Die maschinelle Validierung fängt die objektiven, technischen Fehler ab. Das befreit dich und dein Team davon, Zeit mit der Suche nach trivialen Syntaxfehlern zu verschwenden. Stattdessen könnt ihr euch in Code-Reviews auf die wichtigeren, konzeptionellen und qualitativen Aspekte konzentrieren.

Indem du die Validierung zu einem festen, frühen und wiederholten Bestandteil deines Workflows machst, wandelst du sie von einer lästigen Pflicht in ein mächtiges Werkzeug um. Es ist ein Zeichen von Professionalität und Handwerkskunst. Es zeigt Respekt gegenüber den Standards des Webs, gegenüber deinen Nutzern und nicht zuletzt gegenüber deinen Entwickler-Kollegen. Valider Code ist kein Selbstzweck – er ist das Fundament für robuste, zugängliche und zukunftssichere Webanwendungen.
