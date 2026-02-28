# Subresource Integrity (SRI)

### Subresource Integrity (SRI): Vertrauen ist gut, Kontrolle ist besser

Stell dir vor, du baust eine moderne Webseite. Um die Ladezeiten zu optimieren und die Serverlast zu reduzieren, nutzt du wie viele andere Entwickler auch ein Content Delivery Network (CDN). Anstatt gängige Bibliotheken wie jQuery, Bootstrap oder eine Schriftart von deinem eigenen Server auszuliefern, bindest du sie direkt von einem spezialisierten, externen Hoster ein. Das ist klug, denn CDNs sind global verteilt, blitzschnell und die Chancen stehen gut, dass der Browser deines Nutzers die Datei bereits von einer anderen Webseite kennt und im Cache hat.

Deine Einbindung im HTML könnte so aussehen:

```html
<!-- Einbindung einer beliebten JavaScript-Bibliothek von einem CDN -->
<script src="https://cdn.example.com/library/1.2.3/library.min.js"></script>

<!-- Einbindung eines CSS-Frameworks von einem anderen CDN -->
<link rel="stylesheet" href="https://cdn.another-example.com/framework/4.5.6/framework.min.css">
```

Auf den ersten Blick ist alles perfekt. Deine Seite lädt schnell, und du sparst Bandbreite. Aber hier verbirgt sich ein fundamentales Sicherheitsproblem: Du vertraust dem CDN-Anbieter blind. Was passiert, wenn dieser CDN-Server kompromittiert wird? Ein Angreifer könnte die `library.min.js`-Datei durch eine manipulierte Version ersetzen, die bösartigen Code enthält – zum Beispiel einen Keylogger, der Passwörter stiehlt, oder eine Ransomware, die die Daten deiner Nutzer verschlüsselt.

Dein HTML-Code hat sich nicht geändert. Deine Seite verweist immer noch auf dieselbe URL. Doch anstatt nützlichen Code zu laden, liefert der kompromittierte Server nun Schadsoftware aus, die im Sicherheitskontext deiner Domain ausgeführt wird. Für den Browser und deine Nutzer sieht es so aus, als käme der schädliche Code direkt von deiner Seite. Dein Vertrauen in die "Lieferkette" wurde ausgenutzt. Genau hier setzt Subresource Integrity (SRI) an.

#### Das Prinzip: Ein digitales Siegel

Subresource Integrity ist ein Sicherheitsmechanismus, der es dem Browser ermöglicht, zu überprüfen, ob eine von einem externen Server geladene Ressource (wie ein Skript oder ein Stylesheet) ohne Manipulation ausgeliefert wurde. Die Idee ist einfach und genial zugleich: Du gibst dem Browser nicht nur die URL der Ressource, sondern auch einen "digitalen Fingerabdruck" dieser Datei mit.

Wenn der Browser die Datei herunterlädt, berechnet er selbst deren Fingerabdruck und vergleicht ihn mit dem, den du in deinem HTML-Code angegeben hast. Stimmen die beiden Fingerabdrücke überein, ist alles in Ordnung, und die Ressource wird ausgeführt oder angewendet. Weichen sie jedoch voneinander ab, bedeutet das, dass die Datei auf dem Weg zu dir oder auf dem Server selbst verändert wurde. In diesem Fall wird der Browser die Ausführung der Ressource blockieren und einen Fehler in der Konsole melden. Die potenzielle Gefahr ist gebannt.

#### So funktioniert es in der Praxis

Um SRI zu nutzen, fügst du zwei Attribute zu deinem `<script>`- oder `<link>`-Tag hinzu: `integrity` und `crossorigin`.

Schauen wir uns das `integrity`-Attribut genauer an. Es enthält den besagten Fingerabdruck, der aus zwei Teilen besteht:
1.  **Der Hash-Algorithmus:** Gibt an, welche kryptografische Funktion zur Erzeugung des Fingerabdrucks verwendet wurde. Üblich sind hier `sha256`, `sha384` oder `sha512`. Je höher die Zahl, desto stärker (und länger) der Hash, was ihn resistenter gegen Kollisionen macht. `sha384` gilt heute als ein sehr guter Kompromiss aus Sicherheit und Performance.
2.  **Der Hash-Wert:** Dies ist der eigentliche Fingerabdruck, der als Base64-kodierter String dargestellt wird.

Ein vollständiges Beispiel sieht dann so aus:

```html
<script src="https://code.jquery.com/jquery-3.6.0.min.js"
        integrity="sha256-o88AwQnZB+VDvE9tvIXrMQaPlFFSUTR+nldQm1LuPXQ="
        crossorigin="anonymous"></script>
```

Was passiert nun im Browser?
1.  Der Browser sieht den `<script>`-Tag und die URL.
2.  Er bemerkt das `integrity`-Attribut und weiß, dass er eine SRI-Prüfung durchführen muss.
3.  Er lädt die Datei `jquery-3.6.0.min.js` vom Server herunter.
4.  **Bevor er den JavaScript-Code ausführt**, berechnet er den SHA-256-Hash der heruntergeladenen Datei.
5.  Er vergleicht den selbst berechneten Hash mit dem Wert im `integrity`-Attribut (`o88AwQnZB+...`).
6.  **Fall A (Erfolg):** Die Hashes stimmen überein. Die Datei ist unverändert. Der Browser führt das Skript aus.
7.  **Fall B (Fehler):** Die Hashes stimmen nicht überein. Der Browser verwirft die heruntergeladene Datei, führt sie **nicht** aus und wirft einen `Failed to find a valid digest...`-Fehler in der Entwicklerkonsole. Deine Webseite ist vor der manipulierten Ressource geschützt.

#### Das unverzichtbare `crossorigin`-Attribut

Du hast vielleicht das `crossorigin="anonymous"`-Attribut bemerkt und dich gefragt, wozu es dient. Es ist für die Funktion von SRI von entscheidender Bedeutung. Per Voreinstellung verbieten Browser aus Sicherheitsgründen (Same-Origin Policy), dass eine Webseite auf den genauen Inhalt von Ressourcen zugreift, die von einer anderen Domain geladen werden.

Damit der Browser jedoch den Hash-Wert einer heruntergeladenen Datei berechnen kann, muss er auf deren Inhalt zugreifen dürfen. Das `crossorigin`-Attribut signalisiert dem Server, dass eine Cross-Origin-Anfrage gestellt wird. Der Wert `anonymous` sorgt dafür, dass bei dieser Anfrage keine Cookies oder andere Anmeldeinformationen mitgesendet werden. Der externe Server muss die Anfrage mit einem passenden CORS-Header (`Access-Control-Allow-Origin: *`) beantworten. Tut er das, erlaubt er dem Browser den Lesezugriff auf die Ressource, die SRI-Prüfung kann stattfinden.

**Wichtig:** Wenn du das `integrity`-Attribut verwendest, aber `crossorigin` vergisst, wird die Ressource in den meisten modernen Browsern gar nicht erst geladen, um das "Leaken" von Informationen über verschiedene Origins hinweg zu verhindern. Die Regel lautet also: **SRI immer zusammen mit `crossorigin="anonymous"` verwenden.**

#### Wie du die Hash-Werte erzeugst

Die kryptografischen Hash-Werte denkst du dir natürlich nicht aus und tippst sie auch nicht ab. Es gibt mehrere einfache Wege, sie zu erhalten:

1.  **Vom CDN-Anbieter:** Die meisten seriösen CDNs bieten den vollständigen HTML-Tag inklusive des korrekten `integrity`-Hashes direkt zum Kopieren an. Das ist der einfachste und sicherste Weg.
2.  **Mit Kommandozeilen-Tools:** Wenn du die Datei lokal gespeichert hast, kannst du den Hash selbst generieren. Auf Linux- oder macOS-Systemen ist das oft ein Einzeiler im Terminal.

   Um einen SHA-384-Hash für eine Datei namens `framework.min.css` zu erzeugen, könntest du diesen Befehl nutzen:

   ```bash
   openssl dgst -sha384 -binary framework.min.css | openssl base64 -A
   ```

   Das Ergebnis ist der Base64-kodierte Hash, den du direkt in dein `integrity`-Attribut einfügen kannst.

3.  **Online-Generatoren:** Es gibt Webseiten, die SRI-Hashes für dich generieren. Hier ist jedoch Vorsicht geboten. Nutze sie nur bei öffentlichen, bekannten Bibliotheken und sei dir bewusst, dass du der Webseite, die den Hash generiert, vertrauen musst.

#### Mehrere Hashes für die Zukunftssicherheit

Was passiert, wenn ein Hash-Algorithmus wie `sha256` in Zukunft als unsicher eingestuft wird? SRI hat auch dafür eine Lösung. Du kannst mehrere, durch Leerzeichen getrennte Hash-Werte im `integrity`-Attribut angeben. Der Browser wählt dann den stärksten Algorithmus aus, den er unterstützt. Es ist eine gute Praxis, mit dem stärksten zu beginnen.

```html
<script src="https://cdn.example.com/library.js"
        integrity="sha512-Vj9g3... sha384-U8g7f... sha256-O88Aw..."
        crossorigin="anonymous"></script>
```

In diesem Fall würde ein moderner Browser den `sha512`-Hash für die Überprüfung verwenden. Ein älterer Browser, der `sha512` vielleicht noch nicht kennt, könnte auf `sha384` zurückgreifen.

#### Grenzen und Anwendungsbereiche

Subresource Integrity ist ein mächtiges Werkzeug, aber kein Allheilmittel. Es ist wichtig, seine Grenzen zu verstehen:

*   **Schutz vor Manipulation, nicht vor Fehlern:** SRI schützt dich davor, dass eine Ressource *nach* ihrer ursprünglichen Veröffentlichung manipuliert wird. Es schützt dich nicht davor, von Anfang an eine bösartige Bibliothek einzubinden. Du musst der Quelle der Bibliothek (z. B. dem offiziellen jQuery-Team) weiterhin vertrauen.
*   **Nur für statische Ressourcen:** Der Mechanismus funktioniert nur, wenn sich der Inhalt einer Datei nicht ändert. Sobald der CDN-Anbieter eine neue Version der Bibliothek unter derselben URL ausliefert (z. B. ein Bugfix-Update), wird dein alter Hash-Wert nicht mehr übereinstimmen, und der Browser wird die Ressource blockieren. Das bedeutet, bei jedem Update einer externen Ressource musst du auch den `integrity`-Hash in deinem HTML-Code aktualisieren. Build-Tools können diesen Prozess automatisieren.
*   **Gilt für `<script>` und `<link>`:** SRI ist primär für JavaScript-Dateien (`<script src="...">`) und CSS-Dateien (`<link rel="stylesheet" href="...">`) gedacht und wird von allen modernen Browsern unterstützt.

Durch den gezielten Einsatz von Subresource Integrity schließt du eine signifikante Sicherheitslücke in der modernen Webentwicklung. Du verwandelst blindes Vertrauen in eine überprüfbare Tatsache und stellst sicher, dass der Code, den du einbinden möchtest, auch exakt der Code ist, den deine Nutzer am Ende erhalten. Es ist ein kleiner, aber entscheidender Baustein für eine robustere und sicherere Webanwendung.
