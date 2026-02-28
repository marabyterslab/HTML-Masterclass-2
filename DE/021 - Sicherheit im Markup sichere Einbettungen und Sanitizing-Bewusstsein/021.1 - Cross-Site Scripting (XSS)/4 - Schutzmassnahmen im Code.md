# Schutzmaßnahmen im Code

# Schutzmaßnahmen im Code: Dein Schild gegen XSS

Nachdem wir die Anatomie eines Cross-Site-Scripting-Angriffs verstanden haben, ist es an der Zeit, uns zu wappnen. Die gute Nachricht ist: Du bist einem Angreifer nicht schutzlos ausgeliefert. Mit den richtigen Techniken und einer bewussten Herangehensweise an die Code-Entwicklung kannst du deine Webanwendungen robust und sicher machen. Das Fundament aller folgenden Maßnahmen ist ein einziges, alles entscheidendes Prinzip.

### Das goldene Gebot: Traue niemals Benutzereingaben

Stell dir vor, deine Website ist eine Festung. Jede Information, die von außen kommt, ist ein potenzieller trojanischer Gaul. Dieses Prinzip – „Never trust user input“ – ist der Eckpfeiler der Websicherheit.

Was genau sind „Benutzereingaben“? Die Antwort ist umfassender, als du vielleicht denkst. Es geht nicht nur um das, was jemand in ein Formularfeld tippt. Benutzereingaben sind *alle* Daten, die deine Anwendung von außerhalb deines direkten Kontrollbereichs erhält. Dazu gehören:

*   **Formulardaten:** Der klassische Fall, wie Suchanfragen, Kommentare oder Profildaten.
*   **URL-Parameter:** Alles in der URL nach dem Fragezeichen, z. B. `?id=123` oder `?suche=b%C3%BCcher`.
*   **HTTP-Header:** Informationen wie der `User-Agent`-String oder `Referer`, die vom Browser gesendet werden.
*   **Cookies:** Im Browser des Benutzers gespeicherte Daten.
*   **Daten aus externen APIs:** Informationen, die du von anderen Diensten abrufst.

Jeder dieser Datenpunkte kann manipuliert werden, um schadhaften Code einzuschleusen. Deine Aufgabe als Entwickler ist es, jede einzelne dieser Eingaben zu behandeln, als käme sie von einem Angreifer. Die Verteidigungsstrategie baut auf drei Säulen auf: Validierung, Sanitisierung und – die wichtigste von allen – das Escaping bei der Ausgabe.

### Erste Verteidigungslinie: Validierung von Eingaben

Die Validierung ist dein erster Türsteher. Noch bevor du eine Eingabe weiterverarbeitest oder in deiner Datenbank speicherst, prüfst du, ob sie dem erwarteten Format entspricht. Wenn die Eingabe nicht den Regeln entspricht, wird sie rigoros abgewiesen.

Die Validierung erfolgt meist serverseitig, da clientseitige Validierungen (mit JavaScript) vom Angreifer leicht umgangen werden können. Sie dient als grundlegender Plausibilitätscheck.

*   **Typprüfung:** Erwartest du eine Zahl? Dann prüfe, ob die Eingabe wirklich nur aus Ziffern besteht. Alles andere ist ungültig.
*   **Formatprüfung:** Eine E-Mail-Adresse muss ein `@`-Zeichen und eine Domain enthalten. Ein Datum muss einem bestimmten Format (z. B. `JJJJ-MM-TT`) entsprechen.
*   **Längenprüfung:** Ein Benutzername sollte vielleicht nicht länger als 50 Zeichen sein.
*   **Wertebereichsprüfung:** Das Alter eines Benutzers muss zwischen, sagen wir, 0 und 120 liegen. Eine Eingabe von `500` oder `-10` ist offensichtlich ungültig.
*   **Whitelist-Ansatz:** Wenn eine Eingabe nur einen von wenigen vordefinierten Werten annehmen darf (z. B. eine Auswahl aus einem Drop-down-Menü), prüfe, ob der übermittelte Wert tatsächlich in der Liste der erlaubten Werte enthalten ist.

Ein einfaches Beispiel in PHP zur Validierung einer Altersangabe:

```php
// Annahme: $_POST['age'] kommt von einem Formular
$age = $_POST['age'];

// filter_var ist eine großartige Funktion zur Validierung
if (filter_var($age, FILTER_VALIDATE_INT, ["options" => ["min_range" => 1, "max_range" => 120]])) {
    // Die Eingabe ist eine gültige Ganzzahl im erlaubten Bereich.
    // Wir können sie sicher weiterverarbeiten.
    echo "Dein Alter ist: " . $age;
} else {
    // Die Eingabe ist ungültig. Weise sie ab.
    die("Ungültige Altersangabe.");
}
```

Validierung allein verhindert XSS nicht vollständig, aber sie ist ein extrem wirksamer erster Filter, der eine große Klasse von offensichtlich schädlichen oder unsinnigen Eingaben blockiert.

### Zweite Verteidigungslinie: Sanitisierung

Manchmal möchtest du Benutzereingaben nicht komplett abweisen, sondern sie „reinigen“. Das ist der Prozess der Sanitisierung (englisch: Sanitizing). Hierbei entfernst oder veränderst du potenziell gefährliche Teile der Eingabe, lässt aber den harmlosen Rest durch.

Der klassische Anwendungsfall ist ein Kommentarbereich oder ein Content-Management-System (CMS), in dem Benutzer grundlegende HTML-Formatierungen wie `<b>` (fett) oder `<i>` (kursiv) verwenden dürfen, aber gefährliche Tags wie `<script>` oder Attribute wie `onerror` blockiert werden sollen.

Hier ist der **Whitelist-Ansatz** (Erlaubnisliste) dem **Blacklist-Ansatz** (Verbotsliste) haushoch überlegen.

*   **Blacklist (schlecht):** Du versuchst, eine Liste aller bekannten gefährlichen Tags und Attribute zu erstellen und diese zu entfernen (`<script>`, `<iframe>`, `onclick`, `onerror`, …). Das Problem: Du wirst unweigerlich etwas vergessen. Angreifer sind kreativ und finden immer neue Wege, die ein Blacklist-Filter nicht kennt.
*   **Whitelist (gut):** Du definierst eine kurze, präzise Liste der Elemente und Attribute, die ausdrücklich erlaubt sind. Alles, was nicht auf dieser Liste steht, wird rigoros entfernt. Das ist viel sicherer, weil du nur das durchlässt, was du als ungefährlich eingestuft hast.

**Schreibe niemals deinen eigenen Sanitizer!** Das Parsen und Filtern von HTML ist extrem komplex und fehleranfällig. Verlasse dich stattdessen auf etablierte und kampferprobte Bibliotheken. Eine der bekanntesten für clientseitiges JavaScript ist **DOMPurify**.

```html
<!-- Einbinden der Bibliothek -->
<script src="https://unpkg.com/dompurify@2.3.6/dist/dompurify.min.js"></script>

<div id="output"></div>

<script>
    // Eine potenziell gefährliche Eingabe von einem Benutzer
    let userInput = 'Hallo Welt! <b>Das ist fett.</b><img src="x" onerror="alert(\'XSS\')"> <script>alert("noch mehr XSS")</script>';

    // Sanitisieren der Eingabe mit DOMPurify
    // Standardmäßig erlaubt DOMPurify nur harmlose HTML-Tags und Attribute.
    let cleanHTML = DOMPurify.sanitize(userInput);

    // cleanHTML enthält jetzt: 'Hallo Welt! <b>Das ist fett.</b><img src="x">'
    // Das gefährliche 'onerror'-Attribut und der <script>-Tag wurden entfernt.

    document.getElementById('output').innerHTML = cleanHTML;
</script>
```

DOMPurify hat die Eingabe analysiert und nur die sicheren Teile (`<b>` und `<img>` ohne gefährliche Event-Handler) übrig gelassen.

### Die ultimative Waffe: Escaping bei der Ausgabe

Dies ist die wichtigste und effektivste Maßnahme gegen XSS. Selbst wenn deine Validierung und Sanitisierung versagen, kann das korrekte Escaping einen Angriff im letzten Moment verhindern. Das Prinzip lautet: **Filtere bei der Eingabe, escape bei der Ausgabe.**

Escaping (oder Kodierung) bedeutet, dass du Zeichen mit einer Sonderbedeutung in einem bestimmten Kontext durch eine harmlose, äquivalente Darstellung ersetzt. Im Kontext von HTML sind die wichtigsten Zeichen:

*   `<` wird zu `&lt;` (less than)
*   `>` wird zu `&gt;` (greater than)
*   `&` wird zu `&amp;` (ampersand)
*   `"` wird zu `&quot;` (double quote)
*   `'` wird zu `&#39;` (single quote; oder `&apos;`)

Stell dir vor, ein Benutzer gibt folgenden Kommentar ein: `<script>alert('XSS')</script>`.

Wenn du diesen String einfach so in deine HTML-Seite einfügst, passiert Folgendes:
Der Browser sieht die `<script>`-Tags und interpretiert sie als Anweisung, den darin enthaltenen JavaScript-Code auszuführen. Der Angriff ist erfolgreich.

Wenn du den String aber vor der Ausgabe mit einer Escaping-Funktion behandelst, sieht das Ergebnis so aus: `&lt;script&gt;alert('XSS')&lt;/script&gt;`.

Wenn der Browser diesen kodierten String im HTML sieht, interpretiert er ihn nicht mehr als Code. Stattdessen rendert er ihn als reinen Text, und der Benutzer sieht auf der Seite buchstäblich: `<script>alert('XSS')</script>`. Der Code wird angezeigt, aber **nicht ausgeführt**. Der Angriff ist abgewehrt.

**Kontext ist alles!**
Wo du die Daten ausgibst, bestimmt, *wie* du sie escapen musst.

1.  **Im HTML-Textkörper:** Das ist der häufigste Fall. Hier verwendest du die oben beschriebene HTML-Entitätskodierung.

    Vulnerable PHP-Version:
    ```php
    $comment = $_GET['comment']; // z.B. "<script>alert('XSS')</script>"
    echo "<div>" . $comment . "</div>"; // Führt zum XSS
    ```

    Sichere PHP-Version:
    ```php
    $comment = $_GET['comment'];
    // htmlspecialchars() ist die Go-to-Funktion in PHP für HTML-Escaping.
    echo "<div>" . htmlspecialchars($comment, ENT_QUOTES, 'UTF-8') . "</div>";
    ```
    Das Ergebnis im Browser-Quelltext ist `<div>&lt;script&gt;alert('XSS')&lt;/script&gt;</div>`, was sicher ist.

2.  **In HTML-Attributen:** Hier ist es besonders wichtig, auch die Anführungszeichen zu escapen, um zu verhindern, dass ein Angreifer aus dem Attribut ausbricht.

    Vulnerable Version:
    ```php
    $username = '" onmouseover="alert(\'XSS\')';
    echo '<input type="text" value="' . $username . '">';
    // Ergibt: <input type="text" value="" onmouseover="alert('XSS')">
    ```

    Sichere Version:
    ```php
    $username = '" onmouseover="alert(\'XSS\')';
    echo '<input type="text" value="' . htmlspecialchars($username, ENT_QUOTES) . '">';
    // Ergibt: <input type="text" value="&quot; onmouseover=&quot;alert(&#039;XSS&#039;)">
    ```
    Der `onmouseover`-Event-Handler ist nun nur noch Teil des harmlosen `value`-Strings.

3.  **In JavaScript-Kontexten:** Wenn du Daten von deiner serverseitigen Sprache in einen `<script>`-Block auf deiner Seite einfügen musst, gelten andere Regeln. Hier musst du die Daten für einen JavaScript-String kontextgerecht kodieren. Eine einfache Methode ist die JSON-Kodierung, die Sonderzeichen korrekt behandelt.

4.  **In URLs:** Wenn du eine Benutzereingabe in einem `href`-Attribut verwendest, muss sie URL-kodiert werden, damit Zeichen wie `?` oder `&` nicht die URL-Struktur zerstören.

Moderne Template-Engines (wie Twig für PHP, Jinja für Python oder EJS für Node.js) führen dieses kontextsensitive Escaping oft automatisch durch. Das ist ein großer Sicherheitsgewinn. Verlasse dich darauf und deaktiviere das Auto-Escaping nur in absoluten Ausnahmefällen, in denen du bewusst ungefiltertes HTML ausgeben musst.

### Zusätzlicher Schutzwall: Die Content Security Policy (CSP)

Selbst bei größter Sorgfalt kann ein Fehler passieren. Als zusätzliches Sicherheitsnetz dient die Content Security Policy (CSP). CSP ist keine Maßnahme im Code selbst, sondern eine Anweisung an den Browser, die über einen HTTP-Header gesendet wird.

Mit einer CSP kannst du dem Browser eine strenge Whitelist von Quellen geben, von denen er Inhalte (insbesondere Skripte) laden und ausführen darf.

Ein einfacher, aber sehr effektiver CSP-Header könnte so aussehen:

```
Content-Security-Policy: default-src 'self'; script-src 'self' https://trusted-cdn.com;
```

Diese Regel besagt:

*   `default-src 'self'`: Standardmäßig dürfen alle Ressourcen (Bilder, Stylesheets etc.) nur von der eigenen Domain (`'self'`) geladen werden.
*   `script-src 'self' https://trusted-cdn.com`: Skripte dürfen nur von der eigenen Domain oder von `https://trusted-cdn.com` geladen werden.

Wie hilft das gegen XSS? Angenommen, ein Angreifer schafft es, `<script src="https://evil-attacker.com/malware.js"></script>` in deine Seite einzuschleusen. Selbst wenn das Skript-Tag im HTML steht, wird der Browser mit der obigen CSP den Ladevorgang blockieren, da `evil-attacker.com` nicht in der `script-src`-Whitelist aufgeführt ist.

Eine noch strengere CSP kann auch Inline-Skripte und `eval()`-ähnliche Funktionen verbieten, was eine riesige Klasse von XSS-Angriffen von vornherein unmöglich macht. Die Implementierung einer CSP erfordert Planung, bietet aber eine enorme zusätzliche Sicherheitsebene.

Sicherheit ist kein Zustand, sondern ein Prozess. Durch die konsequente Anwendung von Validierung, Sanitisierung und vor allem kontextsensitivem Escaping bei der Ausgabe schaffst du ein robustes Fundament, das deine Anwendung und ihre Nutzer vor den allgegenwärtigen Gefahren des Cross-Site Scripting schützt.
