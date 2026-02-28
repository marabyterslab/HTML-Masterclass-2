# Secure Cookies

### Sichere Cookies: Wie du Daten im Browser effektiv schützt

Cookies sind das Gedächtnis des Webs. Sie sind kleine Textdateien, die eine Website auf deinem Computer speichert, um sich an dich zu erinnern. Ohne sie müsstest du dich bei jedem einzelnen Klick auf einer Website neu einloggen. Sie speichern Warenkörbe, merken sich deine Spracheinstellungen und ermöglichen personalisierte Erlebnisse. Man kann sie sich wie eine digitale Garderobenmarke vorstellen: Du gibst deinen Mantel ab (loggst dich ein), bekommst eine Marke (das Cookie) und solange du diese Marke bei dir trägst, weiß die Garderobe (der Server), welcher Mantel dir gehört.

Diese kleine Textdatei ist jedoch auch ein wertvolles Ziel für Angreifer. Wenn jemand deine „Garderobenmarke“ stiehlt, kann er sich als du ausgeben und auf deine Daten zugreifen. Genau deshalb ist es entscheidend, Cookies so sicher wie möglich zu gestalten. Moderne Browser bieten dafür eine Reihe von Attributen, die du beim Setzen eines Cookies mitgeben kannst. Sie fungieren als Sicherheitsregeln, die der Browser strikt befolgt. Sehen wir uns die wichtigsten im Detail an.

#### Das `Secure`-Attribut: Nur über verschlüsselte Verbindungen

Stell dir vor, du sitzt in einem öffentlichen Café und nutzt das kostenlose WLAN. Wenn du eine Website über eine unverschlüsselte Verbindung (HTTP) aufrufst, werden alle Daten, einschließlich deiner Cookies, im Klartext durch das Netzwerk geschickt. Jeder im selben Netzwerk könnte diesen Datenverkehr mitlesen und deine Cookies stehlen – ein klassischer „Man-in-the-Middle“-Angriff.

Hier kommt das `Secure`-Attribut ins Spiel. Wenn ein Cookie mit diesem Attribut gesetzt wird, weist es den Browser an, dieses Cookie *ausschließlich* über eine sichere, verschlüsselte HTTPS-Verbindung zu senden. Versucht der Browser, die Website über HTTP zu erreichen, bleibt das Cookie sicher im „Tresor“ des Browsers und wird nicht mitgeschickt.

Ein `Set-Cookie`-Header in der HTTP-Antwort des Servers sieht dann so aus:

```http
Set-Cookie: sessionID=a3fWa; Secure
```

Für jede moderne Website, die HTTPS verwendet (was heute der Standard sein sollte), ist das `Secure`-Attribut für alle sensiblen Cookies, insbesondere für Session-Cookies, eine absolute Notwendigkeit. Es ist die erste und grundlegendste Verteidigungslinie gegen das Abhören von Cookies im Netzwerk.

#### Das `HttpOnly`-Attribut: Schutz vor Skript-Diebstahl

Eine der häufigsten Schwachstellen im Web ist Cross-Site Scripting (XSS). Bei einem XSS-Angriff gelingt es einem Angreifer, bösartigen JavaScript-Code in eine ansonsten vertrauenswürdige Website einzuschleusen. Dieser Code wird dann im Browser anderer Besucher ausgeführt.

Was könnte so ein Skript tun? Es könnte zum Beispiel versuchen, auf die Cookies der Seite zuzugreifen. Über `document.cookie` kann JavaScript alle Cookies auslesen, die für die aktuelle Seite zugänglich sind. Wenn ein Angreifer so an dein Session-Cookie gelangt, kann er deine Sitzung kapern und sich in deinem Namen auf der Website bewegen.

Das `HttpOnly`-Attribut ist die direkte Antwort auf diese Bedrohung. Es verbietet den Zugriff auf das Cookie über JavaScript. Der Browser sorgt dafür, dass das Cookie zwar bei jeder Anfrage an den Server mitgesendet wird, aber für clientseitige Skripte unsichtbar bleibt. `document.cookie` wird dieses Cookie einfach nicht mehr anzeigen.

```http
Set-Cookie: sessionID=a3fWa; Secure; HttpOnly
```

Selbst wenn deine Website eine XSS-Schwachstelle haben sollte, schützt das `HttpOnly`-Attribut dein wichtigstes Gut – die Session-ID – davor, gestohlen zu werden. Es ist eine entscheidende Maßnahme zur Risikominderung. Cookies, die nur vom Server benötigt werden und nicht von deinem Frontend-JavaScript gelesen oder manipuliert werden müssen (was auf die meisten Session-Cookies zutrifft), sollten immer dieses Attribut tragen.

#### Das `SameSite`-Attribut: Abwehr von seitenübergreifenden Angriffen

Ein weiterer raffinierter Angriff ist die Cross-Site Request Forgery (CSRF). Stell dir vor, du bist auf deiner Banking-Website eingeloggt. Dein Browser hat dafür ein gültiges Session-Cookie gespeichert. Nun öffnest du in einem anderen Tab eine bösartige E-Mail und klickst auf einen verlockend aussehenden Link, der angeblich Katzenvideos zeigt.

Dieser Link führt aber in Wahrheit zu einer Seite, die im Hintergrund, ohne dein Wissen, eine Anfrage an deine Banking-Website sendet – zum Beispiel eine Überweisung. Da der Browser bei jeder Anfrage an die Banking-Website automatisch dein gültiges Session-Cookie mitschickt, hält die Bank die Anfrage für legitim und führt die Überweisung aus. Du wurdest dazu gebracht, eine Aktion auszuführen, die du nicht beabsichtigt hast.

Das `SameSite`-Attribut wurde entwickelt, um genau das zu verhindern. Es gibt dem Browser Anweisungen, unter welchen Umständen ein Cookie mit einer Anfrage an eine Website gesendet werden darf. Es gibt drei mögliche Werte:

1.  **`Strict`**
    Das ist die sicherste Einstellung. Der Browser sendet das Cookie *nur* dann, wenn die Anfrage von derselben Website stammt. Das bedeutet, selbst wenn du auf einen harmlosen Link von einer externen Seite klickst, der dich zu deinem eingeloggten Profil auf der Zielseite führt, würde das Cookie nicht mitgesendet werden. Du müsstest dich also eventuell neu anmelden. Das bietet maximalen Schutz vor CSRF, kann aber die Benutzerfreundlichkeit beeinträchtigen.

    ```http
    Set-Cookie: sessionID=a3fWa; SameSite=Strict
    ```

2.  **`Lax`**
    Dies ist der Standardwert in den meisten modernen Browsern und bietet einen guten Kompromiss zwischen Sicherheit und Benutzerfreundlichkeit. Der Browser sendet das Cookie bei einer „Top-Level-Navigation“ mit, also wenn du zum Beispiel auf einen Link klickst und sich die URL in der Adresszeile ändert. Das Cookie wird jedoch nicht bei Anfragen gesendet, die im Hintergrund von anderen Websites ausgelöst werden (z. B. durch eingebettete Bilder, iframes oder Formular-POST-Anfragen). Das verhindert die typischen CSRF-Angriffsszenarien.

    ```http

    Set-Cookie: sessionID=a3fWa; SameSite=Lax
    ```

3.  **`None`**
    Diese Einstellung erlaubt es dem Browser, das Cookie bei jeder Anfrage mitzusenden, egal von wo sie stammt. Dies ist nur in speziellen Anwendungsfällen nötig, zum Beispiel bei Diensten, die über mehrere Domains hinweg funktionieren (z. B. Werbe-Tracker oder Single-Sign-On-Systeme). Wenn du `SameSite=None` verwendest, *musst* du zwingend auch das `Secure`-Attribut setzen. Der Browser erzwingt dies, um zu verhindern, dass diese weitreichenden Cookies über ungesicherte Verbindungen gesendet werden.

    ```http
    Set-Cookie: trackingID=xyz987; SameSite=None; Secure
    ```

#### Cookie-Präfixe: Eingebaute Sicherheitsgarantien

Um die korrekte Verwendung dieser Attribute weiter zu fördern und versehentliche Fehlkonfigurationen zu vermeiden, wurden Cookie-Präfixe eingeführt. Wenn der Name eines Cookies mit einem dieser Präfixe beginnt, erzwingt der Browser bestimmte Sicherheitsregeln.

*   **`__Secure-`**: Wenn ein Cookie-Name mit `__Secure-` beginnt (z. B. `__Secure-sessionID`), akzeptiert der Browser dieses Cookie nur, wenn es zusammen mit dem `Secure`-Attribut gesetzt wird. Dies stellt sicher, dass das Cookie niemals versehentlich über eine ungesicherte HTTP-Verbindung gesendet werden kann.

*   **`__Host-`**: Dieses Präfix ist noch strenger. Ein Cookie-Name, der mit `__Host-` beginnt (z. B. `__Host-userToken`), wird vom Browser nur akzeptiert, wenn alle folgenden Bedingungen erfüllt sind:
    *   Es wird mit dem `Secure`-Attribut gesetzt.
    *   Es hat kein `Domain`-Attribut (das Cookie ist also an den exakten Host gebunden, nicht an eine ganze Domain inklusive Subdomains).
    *   Das `Path`-Attribut ist auf `/` gesetzt (das Cookie gilt für die gesamte Website).

Diese Präfixe sind eine Art Vertrag zwischen dir und dem Browser. Du signalisierst: "Dieses Cookie ist extrem wichtig", und der Browser antwortet: "Verstanden, ich werde es nur akzeptieren, wenn du die höchsten Sicherheitsstandards einhältst."

Ein maximal abgesichertes Session-Cookie könnte also so aussehen:

```http
Set-Cookie: __Host-session=a3fWa; Secure; HttpOnly; SameSite=Strict; Path=/
```

#### Lebensdauer und Geltungsbereich: `Max-Age` und `Path`

Zuletzt sind auch die Attribute wichtig, die die Lebensdauer und den Geltungsbereich eines Cookies definieren.

*   **`Expires`** oder **`Max-Age`**: Diese Attribute bestimmen, wie lange ein Cookie gültig ist. `Expires` verwendet ein konkretes Datum, während `Max-Age` die Lebensdauer in Sekunden angibt. Wird keines von beiden gesetzt, handelt es sich um ein „Session-Cookie“, das gelöscht wird, sobald du den Browser schließt. Für sensible Daten ist es ratsam, die Lebensdauer so kurz wie möglich zu halten.

*   **`Domain`** und **`Path`**: Diese Attribute legen fest, für welche Domains und Pfade auf deiner Website das Cookie gültig ist. Eine zu weite Definition (z. B. `Domain=.meinefirma.com`) kann ein Sicherheitsrisiko darstellen, da das Cookie dann auch an potenziell weniger sichere Subdomains gesendet wird. Die Verwendung des `__Host-`-Präfixes hilft, dieses Risiko zu minimieren, indem es das `Domain`-Attribut komplett verbietet.

Das Absichern von Cookies ist kein optionales Extra, sondern ein fundamentaler Baustein der Websicherheit. Durch die bewusste und korrekte Kombination der Attribute `Secure`, `HttpOnly` und `SameSite` baust du robuste Verteidigungslinien gegen die häufigsten Angriffsvektoren auf und schützt die Daten deiner Nutzer effektiv.
