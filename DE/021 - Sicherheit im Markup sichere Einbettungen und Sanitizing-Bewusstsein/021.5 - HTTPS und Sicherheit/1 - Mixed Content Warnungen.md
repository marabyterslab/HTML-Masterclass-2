# Mixed Content Warnungen

### Mixed Content Warnungen

Stell dir vor, du hast deine Website erfolgreich auf HTTPS umgestellt. Überall in der Adressleiste des Browsers leuchtet das beruhigende grüne oder graue Schloss-Symbol. Deine Nutzer fühlen sich sicher, die Datenübertragung ist verschlüsselt, und alles scheint perfekt. Doch dann bemerkst du, dass bestimmte Bilder nicht laden, ein JavaScript-Slider nicht funktioniert oder der Browser plötzlich eine Warnung anzeigt, obwohl das Schloss-Symbol noch da ist. Herzlich willkommen in der Welt des „Mixed Content“.

#### Was genau ist Mixed Content?

Mixed Content, zu Deutsch „gemischter Inhalt“, entsteht, wenn eine Webseite, die über eine sichere HTTPS-Verbindung geladen wird, Ressourcen wie Bilder, Skripte oder Stylesheets über eine unsichere HTTP-Verbindung nachlädt. Die Hauptseite selbst ist sicher, aber einige ihrer Bausteine sind es nicht.

Um das zu veranschaulichen, kannst du dir deine HTTPS-Seite wie ein gepanzertes, abgeriegeltes Haus vorstellen. Jede Ressource, die du über HTTPS lädst, kommt durch die gesicherte Haupttür. Eine Ressource, die über HTTP geladen wird, kommt jedoch durch ein offenes Fenster. Auch wenn das Haus selbst sicher ist, bietet dieses offene Fenster einen potenziellen Angriffspunkt und schwächt die gesamte Sicherheitsarchitektur.

Ein Browser, der auf eine solche Situation stößt, steht vor einem Dilemma. Er kann nicht einfach behaupten, die Seite sei komplett sicher, denn das stimmt nicht. Gleichzeitig möchte er die Seite nicht komplett blockieren, da sie größtenteils sicher ist. Die Reaktion des Browsers hängt entscheidend davon ab, welche Art von unsicherem Inhalt geladen wird.

#### Die zwei Arten von Mixed Content: Passiv und Aktiv

Nicht jeder gemischte Inhalt wird gleich behandelt, denn nicht jeder Inhalt stellt die gleiche Bedrohung dar. Aus diesem Grund unterscheiden Browser zwischen passivem und aktivem Mixed Content.

##### Passiver Mixed Content (Display Content)

Passiver Inhalt ist Content, der die Seite nicht verändern oder mit ihr interagieren kann. Er kann nicht auf das DOM (Document Object Model) zugreifen, keine Cookies auslesen oder den Nutzer auf andere Seiten umleiten. Er ist gewissermaßen „nur zur Ansicht“ da.

Typische Beispiele für passiven Inhalt sind:
*   Bilder (`<img>`)
*   Audio-Dateien (`<audio>`)
*   Video-Dateien (`<video>`)
*   Ressourcen, die per CSS geladen werden, wie `background-image`

**Die Gefahr:** Obwohl dieser Inhalt passiv ist, stellt er dennoch ein Sicherheitsrisiko dar. Ein Angreifer, der sich im selben Netzwerk befindet (z. B. in einem öffentlichen WLAN), könnte einen Man-in-the-Middle-Angriff durchführen. Er könnte die unverschlüsselte HTTP-Anfrage für ein Bild abfangen und stattdessen ein anderes Bild ausliefern – zum Beispiel eine anstößige Grafik oder eine gefälschte Werbeanzeige. Außerdem könnte der Angreifer durch das Abfangen der Anfrage sensible Informationen über die Aktivitäten des Nutzers sammeln, da er sehen kann, welche Bilder auf welcher Seite geladen werden.

**Die Reaktion des Browsers:** Moderne Browser blockieren passiven Mixed Content oft nicht standardmäßig, um die Benutzererfahrung nicht zu stören. Stattdessen zeigen sie eine Warnung in der Entwicklerkonsole an. Das grüne Schloss-Symbol in der Adressleiste kann sich in ein Informationssymbol (ein „i“ im Kreis) oder ein durchgestrichenes Schloss ändern, um den Nutzer darauf hinzuweisen, dass die Seite nicht vollständig sicher ist.

Ein typischer Fehler im Markup sieht so aus:

```html
<!-- Die Seite wird über https://deine-seite.de geladen -->
<img src="http://externe-seite.com/logo.png" alt="Ein unsicheres Logo">
```

Die Konsole würde eine Warnung wie diese ausgeben:
`Mixed Content: The page at 'https://deine-seite.de' was loaded over HTTPS, but requested an insecure image 'http://externe-seite.com/logo.png'. This content should also be served over HTTPS.`

##### Aktiver Mixed Content (Scriptable Content)

Aktiver Inhalt ist weitaus gefährlicher. Es handelt sich um Ressourcen, die mit der Seite interagieren, das DOM verändern und potenziell auf sensible Daten zugreifen können. Sie haben die volle Kontrolle über die Seite, auf der sie ausgeführt werden.

Typische Beispiele für aktiven Inhalt sind:
*   Skripte (`<script>`)
*   Stylesheets (`<link rel="stylesheet">`), da sie weitere Ressourcen wie Schriftarten oder Bilder importieren können
*   Iframes (`<iframe>`)
*   AJAX-Anfragen (via `XMLHttpRequest` oder `fetch()`)
*   Alles, was über `<object>` eingebunden wird

**Die Gefahr:** Hier ist das Bedrohungspotenzial enorm. Ein Angreifer, der ein über HTTP geladenes Skript abfängt und durch bösartigen Code ersetzt, kann praktisch alles tun:
*   Cookies auslesen und die Session des Nutzers kapern.
*   Eingaben aus Formularen (wie Passwörter oder Kreditkartendaten) stehlen.
*   Den Nutzer auf eine Phishing-Seite umleiten.
*   Werbung oder Malware auf der Seite einblenden.

Ein unsicher geladenes Skript hebelt die gesamte Sicherheit der HTTPS-Verbindung aus.

**Die Reaktion des Browsers:** Aufgrund dieses hohen Risikos sind moderne Browser hier sehr streng. **Aktiver Mixed Content wird standardmäßig blockiert.** Die Ressource wird einfach nicht geladen. Das ist gut für die Sicherheit, aber schlecht für die Funktionalität deiner Seite. Wenn ein wichtiges JavaScript-Framework oder ein kritisches CSS-File über HTTP geladen wird, funktioniert deine Seite möglicherweise nicht mehr richtig oder sieht kaputt aus.

Ein solcher Fehler im Markup könnte so aussehen:

```html
<!-- Die Seite wird über https://deine-seite.de geladen -->
<script src="http://cdn-anbieter.com/library.js"></script>
```

Der Browser blockiert diese Anfrage und gibt eine deutlich schärfere Fehlermeldung in der Konsole aus:
`Mixed Content: The page at 'https://deine-seite.de' was loaded over HTTPS, but requested an insecure script 'http://cdn-anbieter.com/library.js'. This request has been blocked; the content must be served over HTTPS.`

#### Mixed Content finden und beheben

Der erste Schritt zur Lösung des Problems ist, die unsicheren Ressourcen zu identifizieren. Der beste Ort dafür ist die **Entwicklerkonsole** deines Browsers (meist über F12 oder `Ctrl+Shift+I` / `Cmd+Opt+I` erreichbar). Im Tab „Konsole“ (oder „Console“) werden alle Mixed-Content-Warnungen und -Fehler klar aufgelistet, inklusive der genauen URL der problematischen Ressource.

Sobald du die Übeltäter gefunden hast, gibt es mehrere Lösungsansätze.

##### 1. URLs auf HTTPS umstellen

Die einfachste und direkteste Lösung ist, alle `http://`-Links in deinem Quellcode, deiner Datenbank oder deinem Content-Management-System durch `https://`-Links zu ersetzen.

**Vorher:**
`<img src="http://example.com/bild.jpg">`

**Nachher:**
`<img src="https://example.com/bild.jpg">`

Prüfe natürlich vorher, ob die Ressource auch tatsächlich über HTTPS verfügbar ist. Die meisten externen Anbieter (CDNs, APIs, etc.) unterstützen heutzutage HTTPS. Wenn ein Anbieter das nicht tut, solltest du ernsthaft darüber nachdenken, eine Alternative zu suchen.

##### 2. Protokoll-relative URLs verwenden

Eine früher beliebte Technik waren protokoll-relative URLs, die ohne `http:` oder `https: ` auskommen. Der Browser verwendet dann automatisch das Protokoll, mit dem die Hauptseite geladen wurde.

**Beispiel:**
`<script src="//ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>`

Wenn deine Seite über HTTPS geladen wird, lädt der Browser das Skript ebenfalls über HTTPS. Wird sie über HTTP geladen, nutzt er HTTP.

Diese Methode hat jedoch einen Haken und wird heute seltener empfohlen. Das Ziel sollte sein, deine Website *ausschließlich* über HTTPS anzubieten. Wenn du protokoll-relative URLs verwendest und deine Seite aus irgendeinem Grund doch über HTTP aufgerufen wird, würden auch alle Ressourcen unsicher geladen. Die explizite Angabe von `https://` ist daher oft die robustere und sicherere Wahl.

##### 3. Content-Security-Policy (CSP) einsetzen

Für eine umfassende und zukunftssichere Lösung kannst du den `Content-Security-Policy`-HTTP-Header verwenden. Dieser Header gibt dem Browser genaue Anweisungen, von welchen Quellen er Inhalte laden darf. Eine spezielle Direktive ist hier besonders nützlich: `upgrade-insecure-requests`.

Wenn du diesen Header auf deinem Server konfigurierst, wandelst du dein gepanzertes Haus in ein intelligentes Haus um. Die Anweisung lautet: „Lieber Browser, falls du im HTML-Code eine `http://`-Ressource findest, versuche bitte automatisch, sie über `https://` zu laden, bevor du eine unsichere Anfrage sendest.“

Der Header sieht so aus:

```
Content-Security-Policy: upgrade-insecure-requests;
```

Dieser eine Header kann eine Vielzahl von Mixed-Content-Problemen auf einen Schlag lösen, insbesondere bei passiven Inhalten. Er fängt alte HTTP-Links in Inhalten ab, die du vielleicht übersehen hast. Für aktive Inhalte funktioniert er auch, aber da Browser diese sowieso blockieren, ist der Effekt hier weniger dramatisch.

Du konfigurierst diesen Header in der Konfigurationsdatei deines Webservers (z. B. `.htaccess` bei Apache oder `nginx.conf` bei Nginx) oder direkt in deiner serverseitigen Anwendung.

Mixed Content ist ein häufiges Problem bei der Umstellung auf HTTPS, aber eines, das du mit dem richtigen Wissen und den richtigen Werkzeugen schnell in den Griff bekommen kannst. Indem du sicherstellst, dass deine sichere Seite auch nur sichere Ressourcen lädt, schließt du eine oft übersehene Sicherheitslücke und schützt deine Nutzer und deine Anwendung effektiv.
