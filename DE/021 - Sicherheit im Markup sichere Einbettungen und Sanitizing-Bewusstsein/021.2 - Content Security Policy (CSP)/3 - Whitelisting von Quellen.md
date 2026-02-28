# Whitelisting von Quellen

# Die Content Security Policy: Dein Türsteher für Webinhalte

Stell dir deine Webseite wie einen exklusiven Club vor. Du als Betreiber entscheidest, wer hineindarf und was im Inneren passieren soll. Im echten Leben hast du dafür Türsteher, die die Gästeliste prüfen. Im Web ist die Lage komplizierter. Deine Webseite lädt Inhalte aus vielen verschiedenen Quellen: Skripte, Stylesheets, Bilder, Schriftarten, und vieles mehr. Standardmäßig vertraut der Browser fast jeder Anweisung, die er in deinem HTML-Dokument findet.

Genau hier liegt eine der größten Gefahren: Cross-Site Scripting (XSS). Bei einem XSS-Angriff schafft es ein Angreifer, bösartigen Code – meist JavaScript – in deine Seite einzuschleusen. Das kann über einen Kommentar, ein Nutzerprofil oder eine manipulierte URL geschehen. Sobald dieser Code auf deiner Seite ist, wird er vom Browser eines Besuchers ausgeführt, als wäre er dein eigener. Der bösartige Code hat vollen Zugriff auf die Session des Nutzers, kann Cookies stehlen, Formulareingaben abgreifen oder die Seite manipulieren.

Um das zu verhindern, brauchst du einen digitalen Türsteher. Genau das ist die Content Security Policy (CSP).

### Das Prinzip des Whitelistings

Die CSP kehrt das Standardmodell des Vertrauens um. Statt alles zu erlauben, was nicht explizit verboten ist, verbietet sie standardmäßig alles, was nicht explizit erlaubt ist. Du erstellst eine "Whitelist" – eine Positivliste – von Quellen, denen du vertraust. Nur Inhalte, die von diesen genehmigten Quellen stammen, darf der Browser laden und ausführen. Alles andere wird blockiert.

Diese Policy wird nicht in deinem HTML-Code selbst definiert (obwohl das auch eingeschränkt möglich ist), sondern als HTTP-Header vom Server an den Browser gesendet. Der Header heißt `Content-Security-Policy`.

Ein sehr einfacher CSP-Header könnte so aussehen:

```http
Content-Security-Policy: default-src 'self';
```

Analysieren wir diesen kurzen Befehl:

*   **`default-src`**: Das ist eine *Direktive*. Sie ist die Standard-Regel für alle Arten von Inhalten, für die du keine spezifischere Regel definierst.
*   **`'self'`**: Das ist eine *Quellenangabe*. Das Schlüsselwort `'self'` (in einfachen Anführungszeichen) bedeutet, dass Inhalte nur von derselben Herkunft (gleiches Protokoll, gleicher Host, gleicher Port) geladen werden dürfen, von der auch die HTML-Seite selbst stammt.

Mit dieser einen Zeile hast du bereits einen riesigen Schritt in Richtung Sicherheit gemacht. Jedes Skript, jedes Bild und jedes Stylesheet von einer fremden Domain (z.B. einem CDN oder einem Tracking-Dienst) würde vom Browser blockiert werden.

### Die Direktiven: Regeln für jede Inhaltsart

Natürlich ist die Welt selten so einfach. Die meisten Webseiten laden Inhalte von verschiedenen Orten. Deshalb bietet die CSP eine ganze Reihe von Direktiven, mit denen du sehr feingranulare Regeln erstellen kannst. Hier sind die wichtigsten:

*   **`script-src`**: Definiert erlaubte Quellen für JavaScript. Dies ist die wichtigste Direktive zur Abwehr von XSS.
*   **`style-src`**: Legt fest, woher Stylesheets (CSS) geladen werden dürfen.
*   **`img-src`**: Bestimmt die erlaubten Quellen für Bilder.
*   **`font-src`**: Für Schriftarten.
*   **`connect-src`**: Limitiert die Endpunkte, mit denen die Seite über APIs (z.B. `fetch()` oder `XMLHttpRequest`) kommunizieren darf.
*   **`frame-src`**: Definiert, welche Quellen in `<iframe>`s eingebettet werden dürfen.
*   **`media-src`**: Für Audio- und Video-Dateien.

Wenn `default-src` gesetzt ist, dient es als Fallback für all diese und weitere Direktiven. Es ist eine gute Praxis, `default-src` restriktiv zu setzen (z.B. auf `'none'` oder `'self'`) und dann für jede benötigte Inhaltsart spezifische Ausnahmen zu definieren.

### Quellen definieren: Woher darf's denn kommen?

Neben dem Schlüsselwort `'self'` kannst du verschiedene Arten von Quellen angeben. Mehrere Quellen für eine Direktive werden einfach durch Leerzeichen getrennt.

*   **Hostnamen**: Du kannst spezifische Domains erlauben.
    `img-src 'self' https://cdn.meine-seite.de;`
    Dieser Regel erlaubt Bilder von der eigenen Domain und von deinem spezifischen CDN. Beachte, dass das Protokoll (https://) mit angegeben wird.
*   **Wildcards**: Du kannst Wildcards verwenden, um Subdomains abzudecken.
    `script-src https://*.google-analytics.com;`
    Dies würde Skripte von `www.google-analytics.com` und jedem anderen Host unter `google-analytics.com` erlauben. Sei hierbei vorsichtig: Wenn ein Angreifer eine deiner erlaubten Subdomains unter seine Kontrolle bringt, kann er von dort aus Code ausführen.
*   **Schlüsselwörter**:
    *   `'none'`: Verbietet das Laden dieser Inhaltsart vollständig. `frame-src 'none';` ist eine exzellente Regel, um Clickjacking-Angriffe zu erschweren.
    *   `'unsafe-inline'`: Erlaubt die Ausführung von Inline-JavaScript (in `<script>`-Tags ohne `src`-Attribut) und Inline-CSS (in `style`-Attributen). Dies untergräbt einen Großteil des CSP-Schutzes und sollte unbedingt vermieden werden.
    *   `'unsafe-eval'`: Erlaubt die Nutzung von text-zu-code-Funktionen wie `eval()`. Auch dies ist eine gefährliche Einstellung.

### Das Problem mit Inline-Code und die sichere Lösung

Einer der größten Schutzeffekte der CSP ist das standardmäßige Verbot von Inline-Skripten und -Styles. Warum? Weil genau das die häufigste Methode ist, wie XSS-Payloads in eine Seite injiziert werden. Ein Angreifer, der `<script>alert('XSS')</script>` in deine Seite einschleust, wird durch eine gute CSP blockiert.

Manchmal ist Inline-Code jedoch unvermeidlich oder für die Performance wichtig. Ihn global mit `'unsafe-inline'` zu erlauben, ist wie die Vordertür deines Clubs wieder weit aufzusperren. Glücklicherweise gibt es zwei moderne und sichere Mechanismen, um gezielt Ausnahmen zu erlauben: Nonces und Hashes.

#### 1. Nonce (Number used once)

Eine Nonce ist eine zufällig generierte, einzigartige Zeichenkette, die für jede einzelne Seitenanfrage neu erstellt wird.

**Der Prozess sieht so aus:**

1.  Dein Server generiert bei jeder Anfrage einen kryptografisch sicheren Zufallswert, z.B. `nonce-aBcDeF123456`.
2.  Dieser Wert wird sowohl im `Content-Security-Policy`-Header...
    ```http
    Content-Security-Policy: script-src 'self' 'nonce-aBcDeF123456';
    ```
3.  ...als auch im HTML-Code als Attribut bei dem spezifischen Skript-Tag eingefügt, das du erlauben möchtest.
    ```html
    <script nonce="aBcDeF123456">
      // Dieser Inline-Code ist jetzt erlaubt.
      console.log('Dieses Skript wird ausgeführt.');
    </script>
    ```

Der Browser prüft nun: "Gibt es ein Skript-Tag mit einer Nonce, die exakt mit der im CSP-Header deklarierten Nonce übereinstimmt?" Nur wenn ja, wird das Skript ausgeführt. Da der Angreifer die für diese eine Anfrage generierte Nonce nicht erraten kann, kann er keinen bösartigen Code einschleusen, der von dieser Regel profitiert.

Hier ein simples PHP-Beispiel zur Veranschaulichung:

```php
<?php
// 1. Eine sichere, zufällige Nonce generieren
$nonce = base64_encode(random_bytes(16));

// 2. Den CSP-Header mit der Nonce setzen
header("Content-Security-Policy: script-src 'self' 'nonce-{$nonce}'");
?>
<!DOCTYPE html>
<html>
<head>
    <title>CSP mit Nonce</title>
</head>
<body>
    <h1>Sicheres Inline-Skript</h1>

    <!-- 3. Die gleiche Nonce im Skript-Tag verwenden -->
    <script nonce="<?php echo $nonce; ?>">
        // Nur dieser Block wird ausgeführt
        document.body.style.backgroundColor = 'lightgreen';
    </script>

    <script>
        // Dieser Block wird vom Browser blockiert!
        alert('Dieses Skript hat keine Nonce und ist verboten.');
    </script>
</body>
</html>
```

#### 2. Hash

Die Alternative zur Nonce ist ein Hash. Hierbei erstellst du einen kryptografischen Hash (z.B. SHA256) des *exakten Inhalts* deines Inline-Skripts. Diesen Hash fügst du dann in den CSP-Header ein.

**Der Prozess:**

1.  Du hast ein statisches Inline-Skript:
    `<script>console.log('Hallo Welt!');</script>`
2.  Du berechnest den SHA256-Hash des Inhalts `console.log('Hallo Welt!');`. Das Ergebnis ist (zum Beispiel) `'sha256-qZlYxUy...='`.
3.  Diesen Hash fügst du in deinen CSP-Header ein:
    ```http
    Content-Security-Policy: script-src 'self' 'sha256-qZlYxUy...=';
    ```

Der Browser berechnet nun selbst den Hash jedes Inline-Skripts auf der Seite und vergleicht ihn mit den Hashes in der Policy. Stimmt einer überein, wird das Skript ausgeführt.

Hashes eignen sich hervorragend für statischen Inline-Code, der sich nie ändert. Für dynamisch generierte Skripte sind sie unpraktisch, da sich der Inhalt und damit auch der Hash ständig ändern würde. Hier sind Nonces die bessere Wahl.

### Eine Policy entwickeln und überwachen

Eine CSP von null aufzubauen kann für eine komplexe Seite eine Herausforderung sein. Ein guter Startpunkt ist eine rein überwachende Policy. Dafür verwendest du den Header `Content-Security-Policy-Report-Only`.

```http
Content-Security-Policy-Report-Only:
  default-src 'self';
  script-src 'self' https://stats.example.com;
  report-uri /csp-violation-report-endpoint;
```

Mit diesem Header blockiert der Browser nichts. Stattdessen sendet er bei jeder Verletzung deiner definierten Policy einen JSON-Bericht an die angegebene `report-uri`. So kannst du deine Webseite im Live-Betrieb beobachten, alle benötigten Quellen identifizieren und deine Policy schrittweise verfeinern, ohne die Funktionalität für deine Nutzer zu beeinträchtigen. Sobald du sicher bist, dass deine Policy korrekt ist und nichts Wichtiges blockiert, wechselst du von `Content-Security-Policy-Report-Only` zum scharf geschalteten `Content-Security-Policy`-Header.

Die Einführung einer Content Security Policy ist eine der wirksamsten Maßnahmen, um deine Webanwendung gegen XSS und andere Injection-Angriffe zu härten. Es zwingt dich, ein klares Inventar deiner externen Abhängigkeiten zu führen und die Kontrolle darüber zu behalten, welche Inhalte auf deiner Seite ausgeführt werden dürfen. Dein digitaler Türsteher sorgt dafür, dass nur geladene Gäste auf deiner Party sind.
