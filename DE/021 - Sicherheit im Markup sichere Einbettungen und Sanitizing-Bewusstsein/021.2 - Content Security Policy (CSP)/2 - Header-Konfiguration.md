# Header-Konfiguration

### Die Content Security Policy: Konfiguration über HTTP-Header

Wenn dein Browser eine Webseite anfordert, ist die HTML-Datei nicht das Einzige, was er vom Server erhält. Bevor der eigentliche Inhalt – dein Markup, deine Styles, deine Skripte – eintrifft, findet ein unsichtbarer Dialog statt: der Austausch von HTTP-Headern. Stell sie dir wie eine Art Begleitschreiben oder Beipackzettel für deine Webseite vor. Sie enthalten Metadaten und Anweisungen, die der Browser liest und befolgt, noch bevor er die erste Zeile deines HTML-Codes interpretiert. Genau hier, in diesem vorgelagerten Kommunikationsschritt, entfaltet die Content Security Policy (CSP) ihre volle Wirkung.

Zwar kannst du eine CSP auch über ein `<meta>`-Tag direkt in deinem HTML-Dokument definieren, doch die Konfiguration per HTTP-Header ist die robustere, sicherere und empfohlene Methode. Warum? Weil der Header vom Server gesendet wird und damit eine höhere Autorität besitzt. Der Browser verarbeitet ihn, bevor er überhaupt mit dem Parsen deines Dokuments beginnt. Das bedeutet, dass die Schutzregeln von der ersten Millisekunde an gelten und nicht erst, wenn das `<meta>`-Tag im HTML-Code an der Reihe ist.

#### Der `Content-Security-Policy`-Header im Detail

Der zentrale Header, um den es hier geht, heißt `Content-Security-Policy`. Sein Wert ist ein String, der eine oder mehrere Anweisungen (sogenannte Direktiven) enthält, die durch Semikolons voneinander getrennt sind. Jede Direktive definiert, aus welchen Quellen bestimmte Ressourcentypen geladen werden dürfen.

Eine der grundlegendsten und gleichzeitig wichtigsten Direktiven ist `default-src`. Sie fungiert als eine Art Auffangnetz: Jede Ressourcenart, für die du keine spezifische Regel definierst (wie z. B. `script-src` oder `style-src`), fällt unter die Regel von `default-src`.

Schauen wir uns eine ganz einfache Policy an:

```
Content-Security-Policy: default-src 'self';
```

Was bedeutet das?

*   **`default-src`**: Dies ist die Direktive, die wir setzen.
*   **`'self'`**: Dies ist der erlaubte Quellwert. `'self'` ist ein besonderes Schlüsselwort und bedeutet, dass Ressourcen nur von derselben Herkunft (gleiches Protokoll, gleicher Hostname, gleicher Port) geladen werden dürfen, von der auch das HTML-Dokument selbst stammt. Die einfachen Anführungszeichen sind hier Teil der Syntax und müssen gesetzt werden.

Mit dieser einen Zeile im HTTP-Header deiner Webseite hast du bereits einen enormen Sicherheitssprung gemacht. Jegliche Versuche, Skripte, Bilder, Stylesheets oder andere Inhalte von fremden Domains zu laden, werden vom Browser blockiert. Das schützt effektiv vor vielen Arten von Cross-Site-Scripting (XSS)-Angriffen, bei denen Angreifer versuchen, schädliche Skripte von externen Servern in deine Seite einzuschleusen.

#### Die Konfiguration auf dem Server

Schön und gut, aber wie bringst du deinen Server dazu, diesen Header mit jeder Anfrage auszuliefern? Das hängt stark von deiner Servertechnologie ab. Hier sind einige Beispiele für gängige Setups.

**Apache (über `.htaccess`)**

Wenn du einen Apache-Webserver verwendest, was bei vielen Shared-Hosting-Anbietern der Fall ist, kannst du den Header sehr einfach über eine `.htaccess`-Datei im Hauptverzeichnis deiner Webseite setzen.

```apache
<IfModule mod_headers.c>
  Header set Content-Security-Policy "default-src 'self';"
</IfModule>
```

Der `<IfModule>`-Block stellt sicher, dass der Befehl nur ausgeführt wird, wenn das Apache-Modul `mod_headers` auch wirklich aktiv ist, was Abstürze verhindert.

**Nginx**

Bei Nginx-Servern fügst du die entsprechende Anweisung in deine Konfigurationsdatei (üblicherweise in einem `server` oder `location` Block) ein.

```nginx
server {
  # ... andere Konfigurationen

  add_header Content-Security-Policy "default-src 'self';";

  # ... andere Konfigurationen
}
```

Nach einer Änderung der Konfiguration musst du Nginx neu laden, damit die Änderungen wirksam werden.

**Serverseitige Skriptsprachen (z. B. PHP)**

Wenn deine Webseite dynamisch von einer Skriptsprache wie PHP generiert wird, kannst du den Header direkt im Code setzen. Das ist besonders nützlich, wenn du die Policy dynamisch anpassen möchtest.

```php
<?php
header("Content-Security-Policy: default-src 'self';");
?>
```

Wichtig ist hierbei, dass du die `header()`-Funktion aufrufst, bevor irgendeine Ausgabe an den Browser gesendet wird (also vor jedem HTML, jedem Leerzeichen, einfach allem).

#### Eine realistischere und granularere Policy erstellen

Die Regel `default-src 'self'` ist ein guter Start, aber in der Praxis oft zu restriktiv. Die meisten modernen Webseiten laden Ressourcen von Drittanbietern: Web-Schriftarten von Google Fonts, Analyse-Skripte von Matomo oder Google Analytics, Bilder aus einem Content Delivery Network (CDN).

Deine Aufgabe ist es, eine Whitelist all dieser vertrauenswürdigen Quellen zu erstellen. Dafür bietet CSP eine ganze Reihe spezifischer Direktiven.

*   `script-src`: Erlaubte Quellen für JavaScript.
*   `style-src`: Erlaubte Quellen für CSS.
*   `img-src`: Erlaubte Quellen für Bilder.
*   `font-src`: Erlaubte Quellen für Schriftarten.
*   `connect-src`: Legt fest, wohin Verbindungen (via XHR, WebSockets, Fetch-API) aufgebaut werden dürfen.
*   `frame-src`: Erlaubte Quellen für Inhalte in `<iframe>`s.

Angenommen, deine Webseite verwendet Skripte vom eigenen Server und von Google Analytics, Styles vom eigenen Server und von Google Fonts sowie die dazugehörigen Schriftdateien. Eine passende Policy könnte so aussehen:

```
Content-Security-Policy: default-src 'self'; script-src 'self' https://www.google-analytics.com; style-src 'self' https://fonts.googleapis.com; font-src https://fonts.gstatic.com;
```

Lass uns das auseinandernehmen:

*   **`default-src 'self'`**: Unsere sichere Standardeinstellung bleibt. Alles, was nicht explizit anders geregelt ist, darf nur von der eigenen Domain kommen.
*   **`script-src 'self' https://www.google-analytics.com`**: Skripte dürfen von unserer Domain (`'self'`) und von der Domain von Google Analytics geladen werden.
*   **`style-src 'self' https://fonts.googleapis.com`**: Stylesheets dürfen wir von unserer Domain und von `fonts.googleapis.com` (wo die CSS-Dateien für Google Fonts liegen) laden.
*   **`font-src https://fonts.gstatic.com`**: Die eigentlichen Schriftdateien (`.woff2` etc.) werden von Google über eine andere Domain ausgeliefert. Daher müssen wir `fonts.gstatic.com` für die `font-src`-Direktive freigeben.

Du siehst, die Erstellung einer CSP erfordert eine genaue Kenntnis darüber, welche Ressourcen deine Webseite von wo lädt.

#### Der Umgang mit Inline-Code: Nonces und Hashes

Eines der Kernziele von CSP ist die Verhinderung von XSS. Eine Hauptangriffsfläche dafür sind Inline-Skripte (`<script>...</script>`) und Inline-Event-Handler (`onclick="..."`). Aus diesem Grund blockiert eine strikte CSP standardmäßig jeglichen Inline-Code.

Früher griff man in solchen Fällen oft zu `'unsafe-inline'`, um Inline-Code pauschal zu erlauben. Der Name "unsafe" ist hier Programm: Du öffnest damit wieder eine Tür für potenzielle Angriffe. Moderne CSPs bieten zwei weitaus bessere Alternativen.

**1. Nonces (Number used once)**

Eine Nonce ist ein zufällig generierter, kryptografischer Einmal-Code, den dein Server für jede einzelne Anfrage neu erstellt. Diesen Code fügst du sowohl in den CSP-Header als auch in die `<script>`-Tags ein, die du ausführen möchtest.

**Im PHP-Code (Server):**

```php
<?php
// Erzeuge einen sicheren, zufälligen Base64-String
$nonce = base64_encode(random_bytes(16));

// Setze den Header mit der Nonce
header("Content-Security-Policy: script-src 'self' 'nonce-{$nonce}';");
?>
```

**Im HTML-Code:**

```html
<!DOCTYPE html>
<html>
<head>
  <title>Seite mit Nonce</title>
</head>
<body>
  <!-- Dieses Skript wird nicht ausgeführt, da es keine Nonce hat -->
  <script>alert('Ich werde blockiert!');</script>

  <!-- Dieses Skript wird ausgeführt, weil die Nonce mit dem Header übereinstimmt -->
  <script nonce="<?php echo $nonce; ?>">
    console.log('Ich darf laufen!');
  </script>
</body>
</html>
```

Der Browser vergleicht die Nonce im `script`-Tag mit der im Header. Nur wenn sie übereinstimmen, wird das Skript ausgeführt. Ein Angreifer, der Code in deine Seite einschleusen kann, kann die Nonce nicht erraten, da sie bei jedem Seitenaufruf neu und unvorhersehbar ist.

**2. Hashes**

Wenn du statische Inline-Skripte hast, deren Inhalt sich nie ändert, kannst du deren Hash-Wert (eine Art digitaler Fingerabdruck) in deiner CSP hinterlegen.

Angenommen, du hast dieses Skript in deinem HTML:
`<script>console.log('Hallo Welt!');</script>`

Du kannst den SHA256-Hash des Inhalts `console.log('Hallo Welt!');` berechnen. Das Ergebnis wäre `qznLcsROx4GACP2dm0UCKCzCG-HiZ1guq6ZZDob_Tng=`.

Deine CSP-Direktive würde dann so aussehen:

```
Content-Security-Policy: script-src 'self' 'sha256-qznLcsROx4GACP2dm0UCKCzCG-HiZ1guq6ZZDob_Tng=';
```

Der Browser berechnet beim Laden der Seite ebenfalls den Hash des Skript-Inhalts und vergleicht ihn mit dem Wert im Header. Nur bei einer Übereinstimmung wird es ausgeführt. Dies ist extrem sicher, aber weniger flexibel als Nonces, da jede noch so kleine Änderung am Skript einen neuen Hash erfordert.

#### Testen ohne Risiko: Der Report-Only-Modus

Eine komplexe CSP aus dem Nichts zu implementieren, kann riskant sein. Eine zu restriktive Regel könnte Teile deiner Webseite lahmlegen, ohne dass du es sofort merkst. Hierfür gibt es einen unschätzbar wertvollen Helfer: den `Content-Security-Policy-Report-Only`-Header.

Dieser Header funktioniert exakt wie der normale CSP-Header, mit einem entscheidenden Unterschied: **Er blockiert nichts.** Stattdessen sendet der Browser bei jeder Verletzung der definierten Policy einen JSON-Bericht an eine von dir angegebene URL.

```
Content-Security-Policy-Report-Only: default-src 'self'; ... ; report-uri /csp-violation-report-endpoint;
```

Mit `report-uri` (oder der neueren `report-to`-Direktive) definierst du einen Endpunkt auf deinem Server, der diese Berichte entgegennimmt und speichert. So kannst du deine geplante Policy über Wochen im Live-Betrieb testen, Daten sammeln und sehen, welche Ressourcen blockiert *würden*. Wenn keine unerwarteten Berichte mehr eintreffen, kannst du sicher sein, dass deine Policy vollständig ist, und den Header von `Content-Security-Policy-Report-Only` auf `Content-Security-Policy` umstellen, um den Schutz scharfzuschalten.

Die Konfiguration über HTTP-Header ist der professionelle Weg, deine Webseite mit einer Content Security Policy zu schützen. Sie gibt dir die volle Kontrolle, die höchste Sicherheit und die Werkzeuge, um selbst komplexe Regeln sicher zu implementieren und zu warten.
