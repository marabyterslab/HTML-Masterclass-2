# Bibliotheken zur Bereinigung

### Bibliotheken zur Bereinigung: Die Helfer im Hintergrund

Die manuelle Bereinigung von Nutzereingaben, insbesondere wenn es sich um HTML-Markup handelt, ist eine extrem fehleranfällige und gefährliche Aufgabe. Stell dir vor, du müsstest jede mögliche Variante eines XSS-Angriffs antizipieren. Angreifer sind kreativ; sie verschleiern ihre Payloads in Attributen, kodieren sie auf unzählige Weisen oder nutzen obskure Browser-Eigenheiten aus, um deine Filter zu umgehen. Ein winziger Fehler in deiner Logik, ein übersehener Event-Handler oder eine falsch interpretierte Zeichenkodierung können das Tor für einen erfolgreichen Angriff öffnen.

Genau aus diesem Grund lautet die erste und wichtigste Regel der Input-Sanitization: **Schreibe niemals deinen eigenen Sanitizer.**

Stattdessen greifst du auf erprobte, von Sicherheitsexperten entwickelte und kontinuierlich gepflegte Bibliotheken zurück. Diese Werkzeuge sind darauf spezialisiert, gefährliche Inhalte zu erkennen und zu entfernen, während sie die gewünschten, harmlosen Markup-Strukturen beibehalten. Sie haben unzählige Angriffsvektoren gesehen und wurden über Jahre hinweg gehärtet.

#### Die grundlegenden Strategien: Allowlist vs. Denylist

Bevor wir uns konkrete Bibliotheken ansehen, musst du zwei grundlegende Konzepte verstehen, nach denen sie arbeiten:

1.  **Denylisting (Blacklisting):** Dieser Ansatz versucht, eine Liste bekanntermaßen gefährlicher Elemente und Attribute zu definieren und diese zu entfernen. Du könntest zum Beispiel festlegen, dass `<script>`, `<iframe>` und alle `on*`-Attribute (wie `onclick`, `onerror`) verboten sind. Das Problem? Du wirst niemals alle gefährlichen Varianten erwischen. Was ist mit `<scr<script>ipt>`? Was ist mit einem `href`-Attribut, das `javascript:alert('XSS')` enthält? Denylisting ist ein endloses Katz-und-Maus-Spiel, das du auf lange Sicht verlieren wirst. Es ist unsicher und sollte vermieden werden.

2.  **Allowlisting (Whitelisting):** Dieser Ansatz ist das genaue Gegenteil und der einzig sichere Weg. Statt zu definieren, was verboten ist, definierst du explizit, was erlaubt ist. Du erstellst eine Positivliste aller Elemente und Attribute, denen du vertraust. Alles, was nicht auf dieser Liste steht, wird rigoros entfernt. Du erlaubst zum Beispiel nur die Tags `<p>`, `<strong>`, `<em>` und `<a>`. Für das `<a>`-Tag erlaubst du vielleicht nur das `href`-Attribut, aber nicht `target` oder `onclick`. Dieser Ansatz ist standardmäßig sicher, da unbekannte oder neue Angriffsvektoren automatisch blockiert werden.

Alle seriösen Sanitizing-Bibliotheken arbeiten nach dem Allowlisting-Prinzip.

#### DOMPurify: Der Goldstandard im Browser

Wenn du Benutzereingaben direkt im Frontend mit JavaScript bereinigen musst – zum Beispiel in einer Single-Page-Application (SPA), die Inhalte dynamisch nachlädt –, ist DOMPurify die erste Wahl. Es ist eine kleine, extrem schnelle und sehr sichere Bibliothek.

Ihr größter Vorteil: DOMPurify nutzt nicht seinen eigenen HTML-Parser. Stattdessen delegiert es diese komplexe Aufgabe an den nativen Parser des Browsers. Es lässt den Browser das "schmutzige" HTML in eine DOM-Struktur umwandeln, durchläuft diesen Baum dann und entfernt alles, was nicht explizit auf der Allowlist steht. Anschließend wird der bereinigte DOM-Baum wieder in einen sauberen HTML-String umgewandelt. Dieser Ansatz verhindert eine ganze Klasse von Angriffen (sogenannte Parser-Differential-Angriffe), bei denen Angreifer Unterschiede zwischen deinem serverseitigen Parser und dem Browser-Parser ausnutzen.

Die grundlegende Anwendung ist denkbar einfach:

```javascript
import DOMPurify from 'dompurify';

// Benutzereingabe, die von einem Formular oder einer API kommt
const schmutzigerInput = `
  <p>Das ist ein harmloser Absatz.</p>
  <img src="x" onerror="alert('XSS-Angriff!')">
  <a href="javascript:alert('Noch ein Angriff!')">Böser Link</a>
`;

// Bereinige den Input mit den Standardeinstellungen
const saubererOutput = DOMPurify.sanitize(schmutzigerInput);

// Jetzt kannst du den sauberen Output sicher in dein DOM einfügen
const contentDiv = document.getElementById('user-content');
contentDiv.innerHTML = saubererOutput;

/*
  Was im DOM landet:
  <p>Das ist ein harmloser Absatz.</p>
  <img src="x">
  <a>Böser Link</a>
*/
```

Wie du siehst, wurden der `onerror`-Handler des Bildes und das gefährliche `javascript:`-Protokoll im Link automatisch entfernt. Das `<img>`-Tag selbst wurde beibehalten, aber seines gefährlichen Attributs beraubt. Der `<a>`-Tag verlor sein `href`-Attribut komplett, da sein Inhalt unsicher war.

DOMPurify ist sehr flexibel konfigurierbar. Du kannst genau festlegen, welche Tags und Attribute du erlauben möchtest.

```javascript
// Eine etwas lockerere Konfiguration
const saubererOutput = DOMPurify.sanitize(schmutzigerInput, {
  ALLOWED_TAGS: ['p', 'strong', 'a'],
  ALLOWED_ATTR: ['href']
});

/*
  Was jetzt im DOM landet (das <img>-Tag wird komplett entfernt):
  <p>Das ist ein harmloser Absatz.</p>
  <a>Böser Link</a>
*/
```

#### HTML Purifier: Die Festung für dein Backend

Während DOMPurify im Browser glänzt, findet die wichtigste Bereinigung oft auf dem Server statt, bevor die Daten überhaupt in einer Datenbank gespeichert oder an andere Clients ausgeliefert werden. Für PHP-Anwendungen ist **HTML Purifier** seit vielen Jahren der unangefochtene Champion.

HTML Purifier ist eine extrem robuste und standardkonforme Bibliothek. Sie parst das eingegebene HTML, validiert es gegen strenge DTDs (Document Type Definitions) und baut es von Grund auf neu auf, wobei nur die explizit erlaubten Elemente und Attribute aus der Konfiguration übernommen werden. Das Ergebnis ist nicht nur sicheres, sondern auch standardkonformes HTML.

Die Verwendung in PHP sieht ähnlich konzeptionell aus wie bei DOMPurify:

```php
<?php
// Einbinden der Bibliothek (z.B. via Composer Autoloader)
require_once '/pfad/zu/htmlpurifier/library/HTMLPurifier.auto.php';

// Standardkonfiguration erstellen
$config = HTMLPurifier_Config::createDefault();

// Optional: Konfiguration anpassen
// Erlaube z.B. das 'target'-Attribut für Links, was standardmäßig deaktiviert ist
$config->set('HTML.TargetBlank', true);

// Purifier-Instanz erstellen
$purifier = new HTMLPurifier($config);

// Schmutziges HTML von einem Benutzer
$schmutzigesHTML = '
  <p style="color: blue; font-size: 2em;" onclick="alert(\'XSS\')">Großer Text</p>
  <script>doEvil();</script>
  <a href="https://example.com" target="_blank">Sicherer Link</a>
';

// Das HTML bereinigen
$sauberesHTML = $purifier->purify($schmutzigesHTML);

// Den sauberen Output ausgeben oder speichern
echo $sauberesHTML;

/*
  Die Ausgabe wird sein:
  <p style="color:blue;font-size:2em;">Großer Text</p>
  <a href="https://example.com" target="_blank">Sicherer Link</a>
*/
?>
```

Im Beispiel siehst du, dass der `onclick`-Handler und das gesamte `<script>`-Tag spurlos verschwunden sind. Die erlaubten CSS-Eigenschaften im `style`-Attribut wurden beibehalten (HTML Purifier hat auch eine Allowlist für CSS!), während das `target="_blank"`-Attribut dank unserer Konfigurationsanpassung ebenfalls durchgelassen wurde.

Andere serverseitige Sprachen haben ihre eigenen Äquivalente, die nach demselben Prinzip arbeiten. Für Python ist zum Beispiel **Bleach** eine sehr populäre und gut gepflegte Bibliothek, die eng mit der Entwicklung von DOMPurify verbunden ist.

#### Die richtige Bibliothek für den richtigen Zweck

Die Wahl der Bibliothek hängt von deinem Technologie-Stack und dem Anwendungsfall ab:

*   **Serverseitige Bereinigung (Backend):** Dies ist die wichtigste Verteidigungslinie. Bereinige Daten immer hier, bevor du sie speicherst oder per API auslieferst. Nutze etablierte Bibliotheken wie HTML Purifier (PHP), Bleach (Python), oder ähnliche Pendants für deine Sprache.
*   **Clientseitige Bereinigung (Frontend):** Dies ist eine zusätzliche Schutzschicht, besonders in SPAs, die HTML dynamisch rendern. Sie schützt den Benutzer vor unsicheren Daten, die vielleicht von einer schlecht gesicherten API kommen, und bietet eine gute User Experience, da die Bereinigung sofort stattfindet. DOMPurify ist hier das Mittel der Wahl.

Verlasse dich niemals allein auf die clientseitige Bereinigung. Ein Angreifer kann JavaScript jederzeit deaktivieren oder die API deiner Anwendung direkt aufrufen und so deine Frontend-Validierung umgehen. Die serverseitige Bereinigung ist unverhandelbar.

Der Einsatz dieser Bibliotheken nimmt dir die undankbare und gefährliche Aufgabe ab, das Rad neu zu erfinden. Indem du auf die kollektive Erfahrung der Sicherheits-Community vertraust, die in diesen Tools steckt, machst du deine Anwendung um ein Vielfaches widerstandsfähiger gegen eine der häufigsten Web-Schwachstellen.
