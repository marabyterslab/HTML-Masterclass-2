# Integration in den Editor

### Integration in den Editor

Nachdem du nun weißt, was ein Linter ist und welche Macht in ihm steckt, kommen wir zum wohl wichtigsten Schritt: Wie bringst du dieses Werkzeug dazu, dir direkt bei der Arbeit über die Schulter zu schauen? Ein Linter, den du manuell in der Kommandozeile ausführen musst, ist zwar nützlich, aber er unterbricht deinen Arbeitsfluss. Du schreibst Code, speicherst, wechselst zum Terminal, führst den Befehl aus, liest die Ausgabe und gehst zurück zum Code, um die Fehler zu beheben. Das ist umständlich und verlangsamt dich.

Die wahre Magie entfaltet sich, wenn der Linter direkt in deinem Code-Editor arbeitet. Stell dir vor, du schreibst eine Zeile CSS und noch bevor du die Datei speicherst, unterstreicht dein Editor einen Fehler und erklärt dir beim Darüberfahren mit der Maus genau, was das Problem ist. Das ist nicht nur effizienter, es ist auch ein unglaublich wirkungsvolles Lernwerkzeug. Du bekommst sofortiges Feedback und verinnerlichst die guten Praktiken viel schneller.

#### Das Prinzip der Integration

Die Integration eines Linters in einen modernen Code-Editor wie Visual Studio Code, Sublime Text oder Atom folgt fast immer demselben Muster, das aus drei Kernkomponenten besteht:

1.  **Der Linter selbst:** Das ist das eigentliche Programm (z. B. Stylelint, ESLint), das du in der Regel als eine Abhängigkeit in deinem Projekt installierst. Er ist die „Engine“, die die Regeln kennt und deinen Code analysiert.
2.  **Die Konfigurationsdatei:** Eine Datei in deinem Projekt (z. B. `.stylelintrc.json`), die dem Linter sagt, welche Regeln er anwenden soll. Ohne diese Datei weiß der Linter nicht, wonach er suchen soll.
3.  **Die Editor-Erweiterung (Extension/Plugin):** Das ist das Bindeglied. Eine kleine Software, die du in deinem Editor installierst. Sie startet den Linter im Hintergrund, übergibt ihm den Code, den du gerade schreibst, empfängt die Ergebnisse (Fehler und Warnungen) und stellt sie direkt im Editor-Fenster dar.

Diese drei Komponenten müssen zusammenspielen. Die Erweiterung im Editor sucht nach der Konfigurationsdatei in deinem Projekt und nutzt den dort installierten Linter, um deinen Code in Echtzeit zu prüfen.

#### Ein praktisches Beispiel: Stylelint in Visual Studio Code

Lass uns diesen Prozess am Beispiel von Stylelint für CSS in Visual Studio Code (VS Code) durchspielen, einem der beliebtesten Editoren für die Webentwicklung.

**Schritt 1: Linter im Projekt installieren**

Zuerst muss Stylelint Teil deines Projekts werden. Dies stellt sicher, dass jeder, der an diesem Projekt arbeitet (auch du auf einem anderen Computer), exakt dieselbe Version des Linters und dieselben Regeln verwendet. Du installierst es mit einem Paketmanager wie npm:

```bash
npm install --save-dev stylelint stylelint-config-standard
```

Dieser Befehl installiert zwei Pakete: `stylelint` (die Kern-Engine) und `stylelint-config-standard` (ein weit verbreitetes, vernünftiges Set an Regeln, auf dem du aufbauen kannst). Der `--save-dev`-Zusatz speichert sie als Entwicklungswerkzeuge in deiner `package.json`.

**Schritt 2: Konfigurationsdatei anlegen**

Damit Stylelint weiß, welche Regeln es verwenden soll, erstellst du im Hauptverzeichnis deines Projekts eine Datei namens `.stylelintrc.json`. Für den Anfang genügt ein simpler Inhalt, der auf das eben installierte Regelset verweist:

```json
{
  "extends": "stylelint-config-standard"
}
```

Das Schlüsselwort `"extends"` weist Stylelint an, alle Regeln aus dem `stylelint-config-standard`-Paket zu laden. Später kannst du diese Konfiguration erweitern und einzelne Regeln nach deinen Wünschen anpassen.

**Schritt 3: Die Editor-Erweiterung installieren**

Jetzt kommt der Teil, der die Magie in deinen Editor bringt. In VS Code öffnest du die Ansicht für Erweiterungen (das Icon mit den vier Quadraten in der linken Seitenleiste). In das Suchfeld gibst du „Stylelint“ ein. Die offizielle Erweiterung (meist vom Herausgeber „Stylelint“ selbst) ist die, die du suchst. Mit einem Klick auf „Installieren“ wird sie deinem Editor hinzugefügt.

Normalerweise musst du VS Code danach nicht einmal neu starten. Die Erweiterung wird sofort aktiv.

#### Das Ergebnis: Linting in Echtzeit

Was passiert nun? Sobald du eine CSS-Datei in deinem Projekt öffnest, geschieht Folgendes im Hintergrund:

1.  Die Stylelint-Erweiterung in VS Code wird aktiv.
2.  Sie erkennt, dass du eine CSS-Datei bearbeitest.
3.  Sie durchsucht dein Projektverzeichnis nach einer `.stylelintrc.json`-Datei.
4.  Sie findet die Datei und lädt die Konfiguration (`"extends": "stylelint-config-standard"`).
5.  Sie verwendet die `stylelint`-Installation aus dem `node_modules`-Ordner deines Projekts, um den Code in deinem Editor zu analysieren.

Wenn du jetzt gegen eine Regel verstößt – zum Beispiel, wenn du eine ungültige Hex-Farbe wie `#F0F0` schreibst –, siehst du sofort das Ergebnis:

*   **Wellenlinien:** Der fehlerhafte Code wird direkt im Editor mit einer roten oder gelben Wellenlinie unterstrichen.
*   **Tooltip-Informationen:** Wenn du mit der Maus über den unterstrichenen Code fährst, erscheint ein kleines Fenster, das dir den Fehler genau beschreibt. Zum Beispiel: „Unexpected invalid hex color "#F0F0" (color-no-invalid-hex)“. Du siehst also nicht nur, *dass* etwas falsch ist, sondern auch *warum* und welche Regel verletzt wurde.
*   **Problem-Panel:** In der unteren Leiste von VS Code erscheint im „Problems“-Tab eine Liste aller Fehler und Warnungen im gesamten Projekt. Das gibt dir eine perfekte Übersicht über den Qualitätszustand deiner Codebasis.

Du korrigierst den Fehler zu `#F0F0F0`, und augenblicklich verschwinden die Wellenlinie und die Fehlermeldung. Dein Arbeitsfluss wurde nicht unterbrochen. Im Gegenteil, du hast einen Fehler behoben, bevor er überhaupt zu einem Problem werden konnte.

#### Mehr als nur CSS: ESLint für JavaScript und andere Tools

Dieses Prinzip ist universell. Für JavaScript ist **ESLint** das führende Tool. Der Prozess ist identisch:

1.  `npm install --save-dev eslint eslint-config-airbnb-base` (als Beispiel für ein Regelset).
2.  Eine `.eslintrc.js`-Datei im Projekt anlegen.
3.  Die offizielle „ESLint“-Erweiterung in VS Code installieren.

Schon bekommst du die gleiche Art von sofortigem Feedback für deinen JavaScript-Code, das dich auf logische Fehler, veraltete Syntax oder Stilprobleme hinweist.

Auch für HTML gibt es Linter wie **HTMLHint**, obwohl hier die Grenzen zur reinen Validierung und zu Formatierungswerkzeugen fließender sind.

#### Linting trifft auf Formatierung: Das Power-Duo

Oft wirst du im Zusammenhang mit Linting auch auf den Begriff „Formatter“ stoßen. Ein populäres Werkzeug hierfür ist **Prettier**. Es ist wichtig, den Unterschied zu verstehen:

*   Ein **Linter** (wie Stylelint) findet Fehler und Verstöße gegen programmatische Regeln. Er kümmert sich um die *Qualität* deines Codes. (z. B. „Verwende keine `!important`-Regel.“)
*   Ein **Formatter** (wie Prettier) kümmert sich ausschließlich um das *Aussehen* deines Codes. Er formatiert Einrückungen, Zeilenumbrüche und Abstände einheitlich. Er kennt keine „guten“ oder „schlechten“ Regeln, nur Stil.

Die beiden Werkzeuge ergänzen sich perfekt. Viele Entwickler konfigurieren ihren Editor so, dass Prettier den Code bei jedem Speichern automatisch formatiert („Format on Save“). Gleichzeitig überwacht der Linter im Hintergrund kontinuierlich die Code-Qualität. Diese Kombination sorgt für eine extrem saubere, konsistente und fehlerarme Codebasis, ohne dass du aktiv darüber nachdenken musst. Die Integration in den Editor automatisiert diese Qualitätssicherung und macht sie zu einem selbstverständlichen Teil deines Schreibprozesses.
