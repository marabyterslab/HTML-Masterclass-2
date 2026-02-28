# Funktionsweise von CSP

### Die Funktionsweise der Content Security Policy (CSP)

Stell dir deinen Browser als eine extrem vertrauensselige Person vor. Wenn er eine Webseite von einem Server erhält, geht er grundsätzlich davon aus, dass alles, was darin enthalten ist, gut und gewollt ist. Er lädt Bilder, führt Skripte aus und rendert Stylesheets von jeder beliebigen Quelle, die im HTML-Code angegeben ist. Diese grundlegende Offenheit ist einerseits eine der Stärken des Webs, andererseits aber auch eine seiner größten Schwachstellen.

Das Kernproblem, das die Content Security Policy (CSP) zu lösen versucht, ist das unkontrollierte Laden und Ausführen von externen und internen Ressourcen. Die größte Gefahr hierbei ist Cross-Site Scripting (XSS). Bei einem XSS-Angriff gelingt es einem Angreifer, bösartigen JavaScript-Code in eine Webseite einzuschleusen, die dann im Browser eines anderen Benutzers ausgeführt wird. Dieser Code läuft im Kontext der angegriffenen Seite und kann somit auf sensible Daten wie Cookies, Session-Informationen oder persönliche Daten zugreifen, Aktionen im Namen des Nutzers ausführen oder die Seite manipulieren.

Hier kommt CSP ins Spiel. Anstatt dem Browser zu erlauben, blind alles zu laden, was ihm vorgesetzt wird, gibst du ihm mit einer CSP eine strikte Anweisung – eine Art Gästeliste. Nur Ressourcen, die auf dieser Liste stehen, dürfen geladen und verarbeitet werden. Alles andere wird rigoros blockiert.

#### Die Umsetzung: Ein HTTP-Header

Eine Content Security Policy ist kein HTML-Tag und auch kein JavaScript-Code. Sie wird als HTTP-Response-Header vom Server an den Browser gesendet. Das ist ein entscheidender Punkt: Die Regeln werden festgelegt, *bevor* der Browser überhaupt beginnt, den Inhalt der Seite zu parsen. Der Header lautet `Content-Security-Policy`.

Ein sehr einfacher CSP-Header könnte so aussehen:

```http
Content-Security-Policy: default-src 'self';
```

Dieser Header teilt dem Browser mit: "Lade standardmäßig nur Ressourcen von der gleichen Herkunft (gleiches Protokoll, gleicher Host, gleicher Port) wie das HTML-Dokument selbst." Jede Anfrage für ein Bild, ein Skript oder ein Stylesheet von einer anderen Domain wie einem CDN oder einem Analyse-Dienst würde mit dieser Regel blockiert werden.

#### Die Bausteine der Policy: Direktiven und Quellen

Eine CSP besteht aus einer oder mehreren **Direktiven**, die durch ein Semikolon getrennt sind. Jede Direktive steuert eine bestimmte Art von Ressource. Dahinter folgt eine Liste von erlaubten **Quellen**.

Hier sind einige der wichtigsten Direktiven:

*   `default-src`: Dies ist die Standard-Direktive. Wenn für eine spezifische Ressourcenart (wie `script-src` oder `img-src`) keine Regel definiert ist, greift die `default-src`. Es ist eine gute Praxis, diese so restriktiv wie möglich zu setzen, zum Beispiel auf `'self'`.
*   `script-src`: Definiert, von welchen Quellen JavaScript-Dateien geladen und ausgeführt werden dürfen. Dies ist die wichtigste Direktive zur Abwehr von XSS-Angriffen.
*   `style-src`: Legt die erlaubten Quellen für CSS-Dateien und Inline-Styles fest.
*   `img-src`: Steuert, von wo Bilder geladen werden dürfen.
*   `font-src`: Definiert erlaubte Quellen für Schriftarten.
*   `connect-src`: Beschränkt die Ziele, zu denen der Browser über Schnittstellen wie `fetch()`, `XMLHttpRequest` oder WebSockets eine Verbindung aufbauen darf.
*   `frame-src`: Bestimmt, welche URLs in `<iframe>`- oder `<frame>`-Elemente eingebettet werden dürfen.
*   `object-src`: Kontrolliert die Quellen für Plugins wie `<object>`, `<embed>` und `<applet>`. Es wird dringend empfohlen, diese Direktive auf `'none'` zu setzen, da Plugins wie Flash ein historisches Sicherheitsrisiko darstellen.

Für jede dieser Direktiven kannst du eine oder mehrere Quellen angeben. Die häufigsten Quellenwerte sind:

*   `'self'`: Erlaubt das Laden von Ressourcen von der exakt gleichen Herkunft.
*   `'none'`: Blockiert alle Ressourcen dieses Typs.
*   `https://*.beispiel.de`: Eine spezifische URL oder eine Domain mit einem Wildcard. Erlaubt das Laden von `https://cdn.beispiel.de`, aber nicht von `http://cdn.beispiel.de` (da das Protokoll nicht übereinstimmt) oder `https://boeses.beispiel.de.com`.
*   `data:`: Erlaubt die Verwendung von Data-URIs (z. B. für base64-kodierte Bilder).

#### Der Kampf gegen Inline-Code: `unsafe-inline` und die Alternativen

Standardmäßig verbietet eine CSP die Ausführung von Inline-JavaScript (Code innerhalb von `<script>`-Tags oder in Event-Handlern wie `onclick`) und die Anwendung von Inline-Styles (Styles im `style`-Attribut). Dies ist eine entscheidende Sicherheitsmaßnahme, da die meisten XSS-Angriffe auf der Injektion von genau solchem Inline-Code basieren.

Manchmal ist Inline-Code jedoch schwer zu vermeiden. In solchen Fällen gibt es das Schlüsselwort `'unsafe-inline'`.

```http
Content-Security-Policy: script-src 'self' 'unsafe-inline';
```

Wie der Name schon sagt, ist dies **unsicher**. Es hebelt einen der zentralen Schutzmechanismen von CSP aus. Du solltest es nur verwenden, wenn es absolut keine andere Möglichkeit gibt.

Glücklicherweise gibt es zwei moderne und sichere Alternativen, um bestimmten Inline-Code zu erlauben: Nonces und Hashes.

**1. Nonce (Number used once)**

Eine Nonce ist ein einzigartiger, zufällig generierter kryptografischer Token, der für jede einzelne Serverantwort neu erstellt wird. Du fügst diesen Token sowohl in den CSP-Header als auch in das Skript-Tag im HTML ein.

Dein Server generiert also eine zufällige Zeichenkette, z. B. `EDNnf03nceIOfn39fn3e9h3sdfa`.

Der HTTP-Header sieht dann so aus:

```http
Content-Security-Policy: script-src 'self' 'nonce-EDNnf03nceIOfn39fn3e9h3sdfa';
```

Und das HTML-Skript-Tag so:

```html
<script nonce="EDNnf03nceIOfn39fn3e9h3sdfa">
  // Dieser Code wird ausgeführt, da die Nonce übereinstimmt.
  console.log("Hello from a nonced script!");
</script>
```

Ein Angreifer kann keinen bösartigen Code einschleusen, da er die zufällig generierte Nonce für genau diese eine Seitenladung nicht erraten kann.

**2. Hash**

Ein Hash ist eine weitere sichere Methode. Anstatt einen Token zu generieren, berechnest du den SHA256-, SHA384- oder SHA512-Hash des *Inhalts* deines Inline-Skripts und fügst diesen Hash in den CSP-Header ein.

Angenommen, dein Inline-Skript ist: `alert('Hello, world.');`.

Der SHA256-Hash dieses exakten Inhalts (ohne die `<script>`-Tags) lautet `'sha256-qznLcsROx4GACP2dm0UCKCzCG-HiZ1guq6ZZDob_Tng='`.

Dein CSP-Header würde dann so aussehen:

```http
Content-Security-Policy: script-src 'self' 'sha256-qznLcsROx4GACP2dm0UCKCzCG-HiZ1guq6ZZDob_Tng=';
```

Der Browser berechnet nun selbst den Hash jedes Inline-Skripts auf der Seite und vergleicht ihn mit den im Header erlaubten Hashes. Nur wenn es eine Übereinstimmung gibt, wird das Skript ausgeführt. Dies ist besonders nützlich für statische Skripte, die sich nie ändern.

#### Eine realistische Policy

Eine gute, restriktive CSP für eine moderne Webseite könnte etwa so aussehen:

```http
Content-Security-Policy:
  default-src 'self';
  script-src 'self' https://stats.beispiel.de;
  style-src 'self' 'unsafe-inline' https://fonts.googleapis.com;
  img-src 'self' data: https://cdn.beispiel.de;
  font-src 'self' https://fonts.gstatic.com;
  connect-src 'self' https://api.beispiel.de;
  frame-src 'none';
  object-src 'none';
  report-uri /csp-violation-report-endpoint;
```

Schlüsseln wir das auf:
*   `default-src 'self'`: Standardmäßig ist nur die eigene Domain erlaubt.
*   `script-src 'self' https://stats.beispiel.de`: Skripte dürfen nur von der eigenen Domain oder vom Statistik-Dienst geladen werden. Inline-Skripte sind verboten.
*   `style-src 'self' 'unsafe-inline' https://fonts.googleapis.com`: Stylesheets von der eigenen Domain und Google Fonts sind erlaubt. Hier wurde aus Bequemlichkeit `'unsafe-inline'` hinzugefügt, was in der Praxis oft vorkommt, aber idealerweise durch Hashes oder Nonces ersetzt werden sollte.
*   `img-src 'self' data: https://cdn.beispiel.de`: Bilder von der eigenen Domain, als Data-URI oder vom CDN sind erlaubt.
*   `font-src`, `connect-src`: Legen Quellen für Schriften und API-Aufrufe fest.
*   `frame-src 'none'`, `object-src 'none'`: Verhindern das Einbetten von Frames und Plugins vollständig.
*   `report-uri ...`: Eine sehr nützliche Direktive.

#### Verstöße melden: `report-uri` und `report-to`

Die `report-uri`-Direktive (und ihr modernerer Nachfolger `report-to`) ist ein fantastisches Werkzeug für die Wartung deiner CSP. Du gibst hier einen Endpunkt auf deinem Server an. Immer wenn der Browser eine Ressource aufgrund deiner CSP blockiert, sendet er einen kleinen JSON-Bericht an diese URL.

Ein solcher Bericht enthält Informationen wie:
*   `document-uri`: Die Seite, auf der der Verstoß stattfand.
*   `violated-directive`: Die CSP-Regel, die verletzt wurde.
*   `blocked-uri`: Die URL der blockierten Ressource.
*   `source-file`: Die Quelldatei, die versuchte, die Ressource zu laden.

Mit diesen Berichten kannst du deine Webseite überwachen und herausfinden, ob deine CSP zu streng ist und legitime Ressourcen blockiert oder ob jemand versucht, deine Seite anzugreifen.

#### Testen ohne Blockieren: Der `Report-Only`-Modus

Eine strenge CSP direkt auf einer produktiven Seite zu aktivieren, kann riskant sein – es könnte sein, dass du versehentlich wichtige Funktionen deiner Seite lahmlegst. Aus diesem Grund gibt es den Header `Content-Security-Policy-Report-Only`.

Wenn du diesen Header verwendest, wendet der Browser die Policy an und sendet bei Verstößen Berichte an deine `report-uri`, aber er **blockiert nichts**. Dies erlaubt dir, eine neue Policy sicher zu testen, die Berichte zu analysieren und die Regeln so lange anzupassen, bis du sicher bist, dass sie korrekt ist. Erst dann schaltest du auf den erzwingenden `Content-Security-Policy`-Header um.

Zusammenfassend ist CSP also eine deklarative Verteidigungslinie, die direkt im Browser wirkt. Du verlagerst die Sicherheitslogik von einem reaktiven "Hoffentlich wird kein bösartiger Code eingeschleust" zu einem proaktiven "Nur dieser explizit erlaubte Code darf überhaupt ausgeführt werden". Es ist eine der effektivsten Maßnahmen, um deine Webanwendung vor einer der häufigsten Angriffsklassen im Web zu schützen.
