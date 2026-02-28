# Konfiguration von Regeln

### Konfiguration von Regeln

Linting-Tools sind keine starren, unnachgiebigen Wächter. Ihre wahre Stärke entfalaltet sich erst durch Anpassung. Du würdest ja auch kein Werkzeug verwenden, das nicht richtig in deiner Hand liegt oder für eine andere Aufgabe gedacht ist. Genau hier kommt die Konfiguration der Regeln ins Spiel. Sie ist das Herzstück jedes Linters und erlaubt es dir, das Werkzeug exakt auf die Bedürfnisse deines Projekts, deines Teams und deines persönlichen Arbeitsstils zuzuschneiden. Ohne eine durchdachte Konfiguration kann ein Linter schnell von einem nützlichen Helfer zu einer Quelle ständiger Frustration werden.

#### Die Anatomie einer Regel

Jede Regel in einem Linter, sei es ESLint für JavaScript oder Stylelint für CSS, folgt einem einfachen, aber mächtigen Schema. Um sie zu konfigurieren, musst du ihre drei Kernkomponenten verstehen: die Regel-ID, die Schweregrad-Stufe und die optionalen Einstellungen.

**1. Die Regel-ID (Rule ID)**
Jede Regel hat einen eindeutigen Namen, eine Art Kennzeichen. Dieser Name ist meist kurz, beschreibend und in Kebab-Case (Wörter-mit-Bindestrichen) geschrieben. Beispiele hierfür sind `no-unused-vars` (keine ungenutzten Variablen), `indent` (Einrückungsstil) oder `quotes` (Art der Anführungszeichen). Diese ID ist der Schlüssel, mit dem du eine spezifische Regel in deiner Konfigurationsdatei ansprichst.

**2. Der Schweregrad (Severity Level)**
Nicht jeder Regelverstoß ist gleich schlimm. Ein fehlendes Semikolon ist vielleicht ein Stilbruch, aber eine unbenutzte Variable könnte auf einen logischen Fehler im Code hindeuten. Deshalb kannst du für jede Regel festlegen, wie der Linter auf einen Verstoß reagieren soll. Es gibt typischerweise drei Stufen:

*   `"off"` oder `0`: Die Regel wird komplett ignoriert. Der Linter prüft diesen Aspekt deines Codes nicht. Das ist nützlich, wenn eine Regel für dein Projekt keinen Sinn ergibt oder im Widerspruch zu anderen Werkzeugen steht.
*   `"warn"` oder `1`: Der Linter meldet einen Verstoß als Warnung. In den meisten Editoren wird dies durch eine gelbe Unterstreichung oder ein Symbol angezeigt. Eine Warnung unterbricht in der Regel nicht deinen Build-Prozess oder deine Continuous-Integration-Pipeline. Sie dient als freundlicher Hinweis, dass hier etwas nicht dem vereinbarten Standard entspricht, aber nicht kritisch ist. Das ist ideal für stilistische Präferenzen.
*   `"error"` oder `2`: Der Linter behandelt einen Verstoß als Fehler. Code-Editoren markieren dies meist prominent in Rot. Wichtiger noch: Ein Fehler führt dazu, dass der Linter-Prozess mit einem Fehlercode beendet wird. Das stoppt Build-Prozesse und verhindert, dass Code mit offensichtlichen Problemen in die Codebasis eingecheckt werden kann. Diese Stufe ist für Regeln reserviert, die auf potenzielle Bugs, logische Fehler oder gravierende Stilbrüche hinweisen.

**3. Die Optionen (Options)**
Viele Regeln sind nicht nur einfache An/Aus-Schalter. Sie benötigen weitere Informationen, um ihre Arbeit korrekt zu erledigen. Die Regel für die Einrückung (`indent`) muss zum Beispiel wissen, ob du Tabs oder Leerzeichen bevorzugst und wie viele Leerzeichen du verwenden möchtest. Diese zusätzlichen Einstellungen werden als Optionen übergeben.

In der Konfigurationsdatei wird eine Regel mit Optionen typischerweise als Array dargestellt. Das erste Element im Array ist immer der Schweregrad, das zweite (und manchmal auch weitere) Element enthält die Optionen.

Schauen wir uns das am Beispiel der `quotes`-Regel in ESLint an:

```json
{
  "rules": {
    "quotes": ["error", "single"]
  }
}
```

Hier sagen wir dem Linter:
1.  Wir konfigurieren die Regel `quotes`.
2.  Verstöße sollen als Fehler (`"error"`) behandelt werden.
3.  Die Option ist `"single"`, was bedeutet, dass nur einfache Anführungszeichen (`'`) erlaubt sind.

Manche Regeln akzeptieren auch ein Objekt für komplexere Konfigurationen:

```json
{
  "rules": {
    "quotes": ["error", "double", { "avoidEscape": true }]
  }
}
```

Diese Konfiguration erzwingt doppelte Anführungszeichen (`"`), erlaubt aber ausnahmsweise einfache, falls dadurch das Escapen von Zeichen innerhalb des Strings vermieden werden kann.

#### Die Konfigurationsdatei in der Praxis

Die ganze Magie passiert in einer zentralen Konfigurationsdatei, die im Wurzelverzeichnis deines Projekts liegt. Für ESLint heißt sie oft `.eslintrc.json`, für Stylelint `.stylelintrc.json`. Obwohl es verschiedene Formate wie JavaScript oder YAML gibt, ist JSON aufgrund seiner Einfachheit sehr verbreitet.

Eine grundlegende `.eslintrc.json`-Datei könnte so aussehen:

```json
{
  "extends": "eslint:recommended",
  "rules": {
    "indent": ["error", 2],
    "semi": ["warn", "always"],
    "no-console": "off"
  }
}
```

Lass uns diese Datei Zeile für Zeile durchgehen:

*   `"extends": "eslint:recommended"`: Dies ist eine der wichtigsten und nützlichsten Funktionen. Anstatt hunderte von Regeln manuell zu konfigurieren, kannst du eine vorgefertigte Konfiguration als Basis verwenden. `eslint:recommended` ist ein von den ESLint-Entwicklern gepflegtes Set von Regeln, die häufige Fehler und problematische Muster im JavaScript-Code aufdecken. Du startest also nicht bei null, sondern mit einer soliden Grundlage. Andere beliebte Konfigurationen sind beispielsweise die von Airbnb oder StandardJS.

*   `"rules": { ... }`: In diesem Objekt nimmst du deine individuellen Anpassungen vor. Alle Regeln, die du hier definierst, überschreiben die Einstellungen aus der Konfiguration, die du unter `extends` angegeben hast.
    *   `"indent": ["error", 2]`: Wir überschreiben die Standard-Einrückungsregel. Wir möchten eine Einrückung von 2 Leerzeichen erzwingen und Verstöße als Fehler behandeln.
    *   `"semi": ["warn", "always"]`: Wir möchten, dass am Ende von Anweisungen immer ein Semikolon steht (`"always"`). Da dies aber eher eine Stilfrage ist, behandeln wir fehlende Semikolons nur als Warnung (`"warn"`).
    *   `"no-console": "off"`: Die `eslint:recommended`-Konfiguration markiert die Verwendung von `console.log()` als Warnung, um zu verhindern, dass Debug-Ausgaben im Produktionscode landen. Für die Entwicklungsphase kann das störend sein. Mit `"off"` schalten wir diese Regel komplett ab.

#### Regeln finden und verstehen

Du musst die unzähligen verfügbaren Regeln natürlich nicht auswendig kennen. Die offizielle Dokumentation deines Linters ist hier dein bester Freund. Auf der ESLint- oder Stylelint-Website findest du eine vollständige Liste aller verfügbaren Kernregeln.

Jede Regel-Dokumentation erklärt dir:
*   Was die Regel tut und warum sie nützlich ist.
*   Welche Optionen sie akzeptiert.
*   Beispiele für korrekten ("guten") und fehlerhaften ("schlechten") Code gemäß dieser Regel.

Es ist eine gute Praxis, sich mit den Regeln vertraut zu machen, die in populären Konfigurationen wie `eslint:recommended` oder dem Airbnb Style Guide enthalten sind. So entwickelst du ein Gefühl dafür, was als "gute Praxis" in der Community gilt.

#### Mehr als nur Regeln: Plugins und Overrides

Die Konfigurationsmöglichkeiten gehen noch weiter. Manchmal benötigst du spezielle Regeln, die nicht im Kern des Linters enthalten sind – zum Beispiel zur Überprüfung von Barrierefreiheits-Attributen in HTML (via JSX) oder für ein bestimmtes Framework wie Vue oder React.

Hier kommen **Plugins** ins Spiel. Ein Plugin ist eine Sammlung von benutzerdefinierten Regeln, die du installieren und in deiner Konfiguration aktivieren kannst. Zum Beispiel fügt das `eslint-plugin-vue` Regeln hinzu, die spezifisch für die Syntax und die besten Praktiken von Vue.js-Komponenten sind.

Manchmal möchtest du auch unterschiedliche Regeln für verschiedene Dateitypen in deinem Projekt anwenden. Deine Testdateien haben zum Beispiel oft andere Anforderungen als dein Anwendungs-Code. Dafür gibt es **Overrides**. Mit einem `overrides`-Block in deiner Konfigurationsdatei kannst du Regeln gezielt für bestimmte Dateien oder Verzeichnisse anpassen.

Ein Beispiel:

```json
{
  "extends": "eslint:recommended",
  "rules": {
    // Globale Regeln für das gesamte Projekt
  },
  "overrides": [
    {
      "files": ["*.test.js", "*.spec.js"],
      "rules": {
        "no-undef": "off"
      }
    }
  ]
}
```

In diesem Beispiel wird die Regel `no-undef`, die die Verwendung nicht deklarierter Variablen verbietet, speziell für alle Dateien, die auf `.test.js` oder `.spec.js` enden, deaktiviert. Das ist nützlich, weil Test-Frameworks oft globale Funktionen wie `describe` oder `it` bereitstellen, die der Linter sonst als Fehler ankreiden würde.

Die Konfiguration von Regeln ist ein iterativer Prozess. Starte mit einer soliden Basis, passe sie an die Bedürfnisse deines Projekts an und scheue dich nicht, sie im Laufe der Zeit zu verfeinern. Eine gut konfigurierte Linter-Datei ist wie ein Vertrag innerhalb deines Teams: Sie definiert, wie ihr Code schreiben wollt, und hilft euch automatisch dabei, diesen Standard konsistent einzuhalten. Sie ist ein lebendiges Dokument, das mit deinem Projekt wächst und sich weiterentwickelt.
