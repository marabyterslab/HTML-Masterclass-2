# HTMLHint und Stylelint

### Linting für Struktur und Stil: HTMLHint und Stylelint

Nachdem du die Grundlagen der Validierung kennengelernt hast, die sicherstellt, dass dein Code den formalen Spezifikationen entspricht, gehen wir nun einen Schritt weiter. Validierung sagt dir, ob dein Code *syntaktisch korrekt* ist. Linting hingegen hilft dir dabei, sicherzustellen, dass dein Code auch *gut* ist. Es ist wie der Unterschied zwischen einem grammatikalisch korrekten Satz und einem stilistisch eleganten, gut lesbaren Text. Linting-Tools sind deine automatisierten Code-Reviewer, die auf vordefinierte Regeln für Stil, Best Practices und potenzielle Fehler achten.

In der Welt von HTML und CSS gibt es zwei unschätzbar wertvolle Helfer, die in keinem modernen Entwicklungsworkflow fehlen sollten: HTMLHint für deine Markup-Struktur und Stylelint für deine Stylesheets.

#### HTMLHint – Dein Wächter für sauberes HTML

Stell dir vor, du arbeitest in einem Team an einer großen Webseite. Eine Person schreibt Attribute in Großbuchstaben, die andere in Kleinbuchstaben. Jemand vergisst regelmäßig das `alt`-Attribut bei Bildern, und ein anderer erzeugt aus Versehen doppelte IDs, was später zu unvorhersehbaren JavaScript-Fehlern führt. Hier kommt HTMLHint ins Spiel.

HTMLHint ist ein statisches Analysewerkzeug für HTML. "Statisch" bedeutet, dass es deinen Code analysiert, ohne ihn auszuführen. Es durchkämmt deine `.html`-Dateien und gleicht sie mit einem von dir definierten Regelwerk ab. Das Ziel ist es, Einheitlichkeit zu schaffen, häufige Fehler zu vermeiden und die Qualität deines Markups zu steigern.

**Installation und Konfiguration**

Die gängigste Art, HTMLHint zu nutzen, ist über Node.js und seinen Paketmanager npm (Node Package Manager). Wenn du Node.js auf deinem System installiert hast, kannst du HTMLHint ganz einfach zu deinem Projekt hinzufügen:

```bash
npm install htmlhint --save-dev
```

Damit das Werkzeug weiß, nach welchen Regeln es suchen soll, benötigst du eine Konfigurationsdatei. Standardmäßig ist das eine Datei namens `.htmlhintrc` im Hauptverzeichnis deines Projekts. In dieser Datei, die meist im JSON-Format geschrieben wird, legst du alle Regeln fest, die für dein Projekt gelten sollen.

Eine einfache `.htmlhintrc`-Datei könnte so aussehen:

```json
{
  "tag-pair": true,
  "attr-lowercase": true,
  "attr-value-double-quotes": true,
  "doctype-first": true,
  "spec-char-escape": true,
  "id-unique": true,
  "src-not-empty": true,
  "alt-require": true
}
```

Schauen wir uns einige dieser Regeln genauer an, um zu verstehen, was sie bewirken:

*   `"tag-pair": true`: Stellt sicher, dass jeder öffnende Tag auch einen schließenden Tag hat (Ausnahmen wie `<br>` oder `<img>` werden natürlich berücksichtigt). Dies verhindert grundlegende Strukturfehler.
*   `"attr-lowercase": true`: Erzwingt, dass alle Attributnamen in Kleinbuchstaben geschrieben werden (z. B. `class` statt `CLASS`). Dies sorgt für einen konsistenten Stil.
*   `"id-unique": true`: Eine der wichtigsten Regeln. Sie prüft, ob jede ID im Dokument nur einmal vorkommt. Doppelte IDs sind ungültiges HTML und eine häufige Fehlerquelle für CSS und JavaScript.
*   `"alt-require": true`: Fördert die Barrierefreiheit, indem es sicherstellt, dass jedes `<img>`-Element ein `alt`-Attribut besitzt. Für dekorative Bilder kann es leer sein (`alt=""`), aber es muss vorhanden sein.
*   `"doctype-first": true`: Überprüft, ob die `<!DOCTYPE>`-Deklaration ganz am Anfang der Datei steht, was für die korrekte Darstellung im Browser entscheidend ist.

Die komplette Liste der Regeln findest du in der offiziellen Dokumentation von HTMLHint. Das Schöne daran ist die Flexibilität: Du und dein Team entscheidet, welche Regeln für euer Projekt sinnvoll sind.

**Anwendung in der Praxis**

Sobald alles konfiguriert ist, kannst du HTMLHint über die Kommandozeile ausführen, um beispielsweise alle HTML-Dateien in einem Ordner zu prüfen:

```bash
npx htmlhint ./src/**/*.html
```

Die wahre Stärke von Lintern entfaltet sich jedoch, wenn sie direkt in deinen Code-Editor integriert sind. Für gängige Editoren wie Visual Studio Code gibt es Erweiterungen, die HTMLHint nutzen. Sie unterstreichen Fehler direkt während du schreibst – ähnlich wie die Rechtschreibprüfung in einem Textverarbeitungsprogramm. So bekommst du sofortiges Feedback und kannst Fehler beheben, bevor sie überhaupt in die Versionskontrolle gelangen.

#### Stylelint – Der Sheriff für dein CSS

Was HTMLHint für dein HTML ist, ist Stylelint für dein CSS – nur noch viel mächtiger und flexibler. CSS kann schnell unübersichtlich werden, besonders in großen Projekten. Unterschiedliche Schreibweisen für Farben (`#fff` vs. `#FFFFFF`), inkonsistente Einrückungen, eine uneinheitliche Reihenfolge von Eigenschaften oder das versehentliche Überschreiben von wichtigen Stilen sind alltägliche Herausforderungen.

Stylelint ist ein moderner Linter, der nicht nur CSS, sondern auch Syntax-Erweiterungen wie SCSS oder Less versteht. Er hilft dir, Fehler zu vermeiden und konsistente Konventionen in deinem Code durchzusetzen.

**Installation und Konfiguration**

Auch Stylelint wird typischerweise über npm installiert. Oftmals installiert man neben dem Kernpaket auch eine vordefinierte Konfiguration als Startpunkt, zum Beispiel die weit verbreitete Standardkonfiguration:

```bash
npm install stylelint stylelint-config-standard --save-dev
```

Die Konfiguration erfolgt in einer Datei namens `.stylelintrc.json`. Hier legst du fest, welche Konfiguration du erweitern möchtest und welche individuellen Regeln du zusätzlich aktivieren oder anpassen willst.

Eine typische Startkonfiguration sieht so aus:

```json
{
  "extends": "stylelint-config-standard",
  "rules": {
    "indentation": 2,
    "selector-class-pattern": "^[a-z0-9]+(?:-[a-z0-9]+)*(?:__[a-z0-9]+(?:-[a-z0-9]+)*)?(?:--[a-z0-9]+(?:-[a-z0-9]+)*)?$",
    "declaration-block-no-duplicate-properties": true,
    "color-hex-case": "lower"
  }
}
```

Lass uns auch hier einige Regeln genauer betrachten:

*   `"extends": "stylelint-config-standard"`: Dieser Eintrag ist fundamental. Er sagt Stylelint, dass es alle Regeln aus dem Paket `stylelint-config-standard` laden soll. Das erspart dir eine Menge Arbeit, da du eine solide Basis an Best-Practice-Regeln erhältst.
*   `"rules": { ... }`: In diesem Objekt kannst du die geerbten Regeln überschreiben oder neue hinzufügen.
*   `"indentation": 2`: Legt die Einrückung auf 2 Leerzeichen fest. Eine klassische Stilregel, die für ein einheitliches Erscheinungsbild des Codes sorgt.
*   `"selector-class-pattern": "..."`: Dies ist ein Beispiel für die enorme Mächtigkeit von Stylelint. Diese Regel erzwingt ein bestimmtes Namensschema für deine CSS-Klassen, hier im Beispiel ein Muster, das mit der BEM-Methodik (Block, Element, Modifier) kompatibel ist. Ein Klassenname wie `.card__title--highlighted` wäre gültig, während `.CardTitle` einen Fehler auslösen würde. Das ist extrem hilfreich, um eine konsistente und verständliche Nomenklatur im gesamten Projekt zu gewährleisten.
*   `"color-hex-case": "lower"`: Sorgt dafür, dass alle Hex-Farbcodes in Kleinbuchstaben geschrieben werden (z. B. `#ffffff` statt `#FFFFFF`).

Angenommen, du hast folgenden CSS-Code, der gegen einige dieser Regeln verstößt:

```css
.Header {
    COLOR: #FFF;
    padding: 10PX;
    padding: 15px; /* Duplikateigenschaft */
}
```

Stylelint würde dir mehrere Fehler melden:
1.  Der Selektor `.Header` entspricht nicht dem `selector-class-pattern` (Großbuchstabe).
2.  Die Eigenschaft `COLOR` sollte kleingeschrieben werden (`property-case`).
3.  Der Hex-Code `#FFF` sollte kleingeschrieben werden (`#fff`).
4.  Die Einheit `PX` sollte kleingeschrieben werden (`px`) (`unit-case`).
5.  Die Eigenschaft `padding` ist doppelt vorhanden (`declaration-block-no-duplicate-properties`).

Dieses sofortige Feedback hilft dir, deinen Code nicht nur funktional, sondern auch sauber und wartbar zu halten.

**Anwendung und Integration**

Ähnlich wie bei HTMLHint kannst du Stylelint über die Kommandozeile aufrufen:

```bash
npx stylelint "**/*.css"
```

Der Befehl durchsucht alle Unterverzeichnisse nach `.css`-Dateien und prüft sie. Die Option `--fix` kann sogar viele der gemeldeten Stilprobleme automatisch beheben, was dir eine Menge Zeit spart.

Auch hier ist die Integration in den Code-Editor der beste Weg, um von Stylelint zu profitieren. Eine entsprechende Erweiterung zeigt dir Fehler in Echtzeit an und ermöglicht es dir oft, Korrekturen mit einem Klick oder einer Tastenkombination durchzuführen.

#### Die Synergie der Werkzeuge

HTMLHint und Stylelint sind mehr als nur einzelne Werkzeuge; sie sind Teil einer umfassenden Strategie zur Qualitätssicherung. Sie erzwingen nicht nur eine einheitliche Codebasis, was die Zusammenarbeit in Teams massiv erleichtert, sondern schulen dich auch darin, von Anfang an besseren Code zu schreiben. Du entwickelst ein Gespür für saubere Strukturen und konsistente Stile.

In einem professionellen Entwicklungsumfeld werden diese Tools oft in den sogenannten Build-Prozess oder in CI/CD-Pipelines (Continuous Integration/Continuous Deployment) integriert. Das bedeutet, dass jedes Mal, wenn ein Entwickler versucht, neuen Code zum Projekt beizutragen, diese Linter automatisch im Hintergrund laufen. Schlägt einer der Checks fehl, wird der neue Code blockiert, bis die Fehler behoben sind. Dies stellt eine grundlegende Qualitätsstufe für das gesamte Projekt sicher.

Indem du HTMLHint und Stylelint in deinen täglichen Arbeitsablauf integrierst, verlagerst du den Fokus von "funktioniert es?" hin zu "ist es gut gemacht, wartbar und für die Zukunft gerüstet?". Du schaffst eine solide, verlässliche Grundlage, auf der komplexe und langlebige Webanwendungen entstehen können.
