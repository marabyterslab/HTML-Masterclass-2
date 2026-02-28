# Priorisierung von Ressourcen

### Priorisierung von Ressourcen: Dem Browser den Weg weisen

Stell dir vor, du baust ein Haus. Du hast alle Materialien auf der Baustelle: Ziegel, Zement, Fenster, Dachziegel und die teure Kücheneinrichtung. Was machst du zuerst? Logischerweise baust du zuerst das Fundament und die Wände, bevor du die Küche installierst. Würdest du mit der Küche beginnen, stünde sie im Weg und würde den gesamten Bauprozess verlangsamen.

Ein Webbrowser steht vor einer ganz ähnlichen Herausforderung, wenn er deine Webseite lädt. Er erhält das HTML-Dokument und beginnt, es von oben nach unten zu lesen. Dabei stößt er auf Anweisungen, weitere Ressourcen zu laden: CSS-Dateien, JavaScript-Dateien, Bilder, Schriftarten und mehr. Der Browser hat eine begrenzte Anzahl an Verbindungen, die er gleichzeitig aufbauen kann, und begrenzte Rechenleistung. Er muss also entscheiden, was am wichtigsten ist. Seine Standardentscheidungen sind oft gut, aber nicht immer optimal für das Nutzererlebnis.

Hier kommst du ins Spiel. Als Entwickler kannst du dem Browser gezielte Hinweise geben, welche Ressourcen er priorisieren soll. Du kannst ihm quasi den Bauplan für deine Seite in die Hand drücken und sagen: „Beginne mit diesem, das ist das Fundament. Jenes kannst du später holen, das ist nur Dekoration.“ Diese gezielte Priorisierung ist ein entscheidender Hebel für eine schnelle und als schnell empfundene Ladezeit.

#### Das Standardverhalten des Browsers verstehen

Um die Priorisierung zu steuern, musst du zuerst verstehen, wie der Browser ohne deine Hilfe denkt. Wenn er auf verschiedene Ressourcen-Tags im HTML stößt, weist er ihnen intern Prioritäten zu.

*   **HTML:** Das Dokument selbst hat immer die höchste Priorität. Ohne es weiß der Browser gar nicht, was er sonst tun soll.
*   **CSS:** Stylesheets, die im `<head>` via `<link rel="stylesheet">` eingebunden sind, erhalten eine sehr hohe Priorität. Sie sind **render-blockierend**. Der Browser wird die Seite nicht darstellen (also „malen“), bevor er dieses CSS heruntergeladen und verarbeitet hat. Warum? Um einen unschönen „Flash of Unstyled Content“ (FOUC) zu vermeiden, bei dem der Nutzer kurz eine nackte HTML-Seite sieht, bevor das Styling greift.
*   **JavaScript:** Skripte, die ohne spezielle Attribute im `<head>` stehen, haben ebenfalls eine hohe Priorität. Sie sind nicht nur render-blockierend, sondern auch **parser-blockierend**. Trifft der Browser auf ein `<script src="...">`, stoppt er das Verarbeiten des restlichen HTML, lädt das Skript, führt es aus und macht erst dann weiter. Der Grund dafür ist historisch: Ein Skript könnte potenziell mit `document.write()` das restliche DOM verändern, also wartet der Browser sicherheitshalber.
*   **Bilder und andere Medien:** Bilder, die im sichtbaren Bereich der Seite sind, erhalten eine mittlere bis hohe Priorität. Bilder, die weiter unten („below the fold“) liegen, bekommen eine niedrigere Priorität.
*   **Schriftarten:** Schriftarten werden oft erst spät entdeckt, nämlich dann, wenn der Browser beim Rendern feststellt, dass er eine bestimmte Schriftart für einen Textabschnitt benötigt, die im CSS referenziert wird. Ihre Lade-Priorität ist hoch, aber ihre Entdeckung ist das Problem.

Dieses Standardverhalten führt oft dazu, dass wichtige visuelle Elemente (wie ein großes Hintergrundbild oder eine spezielle Schriftart für die Überschrift) erst sehr spät geladen werden, während vielleicht ein unwichtiges JavaScript für einen Cookie-Banner den gesamten Prozess blockiert.

#### JavaScript bändigen mit `async` und `defer`

Die größte Blockadequelle ist oft JavaScript. Glücklicherweise geben uns zwei einfache HTML-Attribute die Macht, das Ladeverhalten von Skripten fundamental zu ändern: `defer` und `async`.

##### `defer`: Die sichere und geordnete Variante

Das `defer`-Attribut signalisiert dem Browser: „Lade dieses Skript herunter, während du weiterhin das HTML verarbeitest. Halte nicht an. Führe das Skript aber erst aus, wenn du mit dem gesamten HTML fertig bist, kurz bevor das `DOMContentLoaded`-Ereignis ausgelöst wird.“

```html
<script src="library.js" defer></script>
<script src="main-app.js" defer></script>
```

Die Vorteile sind enorm:
1.  **Kein Parser-Blocking:** Das HTML wird ohne Unterbrechung verarbeitet, was die erste Darstellung der Seite (First Contentful Paint) beschleunigt.
2.  **Garantierte Ausführungsreihenfolge:** Skripte mit `defer` werden in der Reihenfolge ausgeführt, in der sie im Dokument erscheinen. Im obigen Beispiel wird also `library.js` garantiert vor `main-app.js` ausgeführt.
3.  **DOM ist verfügbar:** Wenn die Skripte ausgeführt werden, ist das gesamte DOM bereits aufgebaut. Sie können also sofort sicher auf alle Elemente der Seite zugreifen.

`defer` ist heute die beste Wahl für die meisten Skripte, die für die Funktionalität der Seite notwendig sind und auf das DOM zugreifen müssen.

##### `async`: Für unabhängige Einzelgänger

Das `async`-Attribut ist noch radikaler. Es sagt dem Browser: „Lade dieses Skript im Hintergrund herunter. Sobald der Download abgeschlossen ist, unterbrich sofort, was auch immer du gerade tust (auch das Parsen von HTML), und führe das Skript aus.“

```html
<script src="analytics.js" async></script>
<script src="ads.js" async></script>
```

Das hat wichtige Konsequenzen:
1.  **Kein Parser-Blocking während des Downloads:** Wie bei `defer` wird das HTML weiterverarbeitet, während das Skript lädt.
2.  **Parser-Blocking während der Ausführung:** Die Ausführung unterbricht das Parsen.
3.  **Keine garantierte Reihenfolge:** Wenn du mehrere `async`-Skripte hast, werden sie in der Reihenfolge ausgeführt, in der sie fertig heruntergeladen sind. Ein kleines Skript kann also ein großes überholen.
4.  **Keine Garantie für ein vollständiges DOM:** Da das Skript ausgeführt wird, sobald es bereit ist, kann es sein, dass das HTML-Dokument zu diesem Zeitpunkt noch nicht vollständig verarbeitet wurde.

`async` eignet sich perfekt für unabhängige Skripte von Drittanbietern, die nicht vom DOM oder anderen Skripten auf deiner Seite abhängen. Typische Kandidaten sind Tracking-Skripte (wie Google Analytics), Werbe-Skripte oder kleine Widgets.

#### Vorausschauend laden mit Resource Hints

Manchmal weißt du als Entwickler besser als der Browser, welche Ressourcen in naher Zukunft gebraucht werden. Mit Resource Hints, die du als `<link>`-Tags im `<head>` platzierst, kannst du dem Browser dieses Wissen mitteilen.

##### `preload`: Wichtig für die aktuelle Seite

Mit `<link rel="preload">` gibst du dem Browser die Anweisung, eine Ressource mit hoher Priorität herunterzuladen, weil du sie für die *aktuelle* Seite dringend benötigst. Der Browser lädt die Datei, tut aber sonst nichts damit – er führt kein Skript aus und wendet kein CSS an. Er legt sie nur in den Cache, damit sie sofort verfügbar ist, wenn sie tatsächlich gebraucht wird.

Das ist besonders nützlich für Ressourcen, die der Browser erst spät entdecken würde. Ein klassisches Beispiel sind Schriftarten, die in einer CSS-Datei definiert sind. Der Browser muss erst das HTML laden, dann das CSS laden und verarbeiten, und erst dann merkt er, dass er eine Schriftart braucht. Das kann zu einem sichtbaren „Flash of Unstyled Text“ (FOUT) führen, bei dem der Text kurz in einer Systemschriftart erscheint.

Mit `preload` kannst du das verhindern:

```html
<head>
  <!-- Sag dem Browser, diese Schriftart sofort mit hoher Priorität zu laden -->
  <link rel="preload" href="/fonts/meine-schrift.woff2" as="font" type="font/woff2" crossorigin>
  
  <!-- Lade das CSS, das die Schriftart verwendet -->
  <link rel="stylesheet" href="/css/styles.css">
</head>
```

Das `as`-Attribut ist hier entscheidend. Es teilt dem Browser den Typ der Ressource mit (`font`, `style`, `script`, `image` etc.), damit er die Priorisierung korrekt vornehmen und die richtigen Sicherheitsrichtlinien anwenden kann. Bei Schriftarten ist auch `crossorigin` wichtig, selbst wenn sie von derselben Domain geladen werden.

Ein anderer Anwendungsfall ist das Laden eines wichtigen Hintergrundbildes für den Header-Bereich, das über CSS (`background-image`) eingebunden wird. Auch dieses würde der Browser erst spät entdecken.

**Aber Achtung:** Setze `preload` mit Bedacht ein. Jede `preload`-Anweisung konkurriert um Bandbreite. Wenn du zu viele unwichtige Ressourcen vorlädst, könnten sie wichtigere Ressourcen wie das kritische CSS oder JavaScript blockieren. Nutze es nur für wirklich kritische, spät entdeckte Ressourcen.

##### `prefetch`: Wahrscheinlich wichtig für die nächste Seite

`<link rel="prefetch">` ist der entspannte Bruder von `preload`. Es ist ein Hinweis an den Browser, eine Ressource mit *niedriger* Priorität herunterzuladen, weil sie wahrscheinlich für die *nächste* Navigation des Nutzers benötigt wird. Der Browser nutzt dafür Leerlaufzeiten, um die Datei im Hintergrund zu laden, ohne den Ladevorgang der aktuellen Seite zu stören.

Stell dir einen mehrstufigen Bestellprozess vor. Wenn der Nutzer auf der Warenkorb-Seite ist, ist es sehr wahrscheinlich, dass er als Nächstes zur Kasse-Seite geht. Du könntest also das Haupt-Skript oder die CSS-Datei der Kasse-Seite vorab laden:

```html
<!-- Auf der warenkorb.html -->
<link rel="prefetch" href="/js/kasse.js" as="script">
<link rel="prefetch" href="/css/kasse.css" as="style">
```

Wenn der Nutzer dann auf „Zur Kasse“ klickt, liegen die benötigten Dateien bereits im Cache und die nächste Seite lädt blitzschnell. `prefetch` ist eine fantastische Methode, um die gefühlte Geschwindigkeit bei seitenübergreifenden Interaktionen dramatisch zu verbessern.

##### `preconnect`: Die Verbindung frühzeitig aufbauen

Jedes Mal, wenn der Browser eine Ressource von einer neuen Domain laden muss (z. B. Google Fonts, ein CDN, eine API), muss er zuerst eine Verbindung herstellen. Das beinhaltet einen DNS-Lookup, einen TCP-Handshake und eine TLS-Verschlüsselung. Dieser Prozess kann leicht mehrere hundert Millisekunden dauern, bevor auch nur ein einziges Byte der eigentlichen Ressource übertragen wird.

Mit `<link rel="preconnect">` kannst du dem Browser sagen: „Ich werde bald Ressourcen von dieser Domain benötigen. Baue doch schon mal die Verbindung im Hintergrund auf.“

Ein klassischer Fall ist Google Fonts. Die CSS-Datei kommt von `fonts.googleapis.com`, die Schriftdateien selbst aber von `fonts.gstatic.com`. Um das zu beschleunigen, kannst du beide Verbindungen vorwärmen:

```html
<head>
  <!-- Verbindung zum CSS-Host aufbauen -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <!-- Verbindung zum Font-Host aufbauen -->
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

  <!-- Erst jetzt die eigentliche CSS-Datei anfordern -->
  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
</head>
```
Der Verbindungsaufbau passiert nun parallel zum Laden anderer Ressourcen, und wenn die eigentliche Anfrage für das CSS und die Schriftarten kommt, ist die Leitung bereits offen. Das spart wertvolle Zeit auf dem kritischen Ladepfad.

Durch den bewussten Einsatz dieser Techniken nimmst du dem Browser die Raterunde ab und übernimmst selbst die Regie. Du definierst, was das Fundament deiner Seite ist und was nur Dekoration. Du verwandelst den Browser von einem einfachen Arbeiter, der eine Liste von oben nach unten abarbeitet, in einen effizienten Bauleiter, der genau weiß, welcher Schritt als Nächstes kommt, um dem Nutzer so schnell wie möglich ein stabiles, nutzbares und schönes Ergebnis zu präsentieren.
