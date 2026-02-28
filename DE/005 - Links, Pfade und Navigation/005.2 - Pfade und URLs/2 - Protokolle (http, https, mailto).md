# Protokolle (http, https, mailto)

### Protokolle: Die unsichtbaren Regisseure deiner URLs

Wenn du eine URL in deinen Browser eingibst oder auf einen Link klickst, denkst du wahrscheinlich zuerst an die Adresse der Website, also so etwas wie `www.beispiel.de`. Aber fast immer steht noch etwas davor, ein kleiner, unscheinbarer Teil, der mit einem Doppelpunkt und zwei Schrägstrichen endet: `http://` oder `https://`. Dieser Teil ist das Protokoll, und es ist weit mehr als nur eine Formsache. Es ist die grundlegende Anweisung an deinen Browser, *wie* er mit dem Zielserver kommunizieren soll.

Stell dir vor, du möchtest mit einem Freund kommunizieren. Du könntest ihm einen Brief schreiben, ihn anrufen, eine E-Mail oder eine SMS schicken. Jede dieser Methoden hat ihre eigenen Regeln und Vorgehensweisen – ihr eigenes „Protokoll“. Ein Brief braucht eine Adresse und eine Briefmarke, ein Anruf eine Telefonnummer. Im Internet ist das nicht anders. Das Protokoll legt die Spielregeln für den Datenaustausch fest. Für uns als Webentwickler sind vor allem drei Protokolle von täglicher Bedeutung: HTTP, HTTPS und das etwas anders geartete `mailto`.

#### HTTP: Das Hypertext Transfer Protocol

Das Urgestein des Webs. HTTP steht für **Hypertext Transfer Protocol**. Lass uns diesen Namen einmal auseinandernehmen, denn er verrät schon alles Wichtige:

*   **Hypertext:** Das ist der Kern des Webs. Es beschreibt Dokumente (wie HTML-Seiten), die nicht nur Text enthalten, sondern auch Verknüpfungen (Hyperlinks) zu anderen Dokumenten. Du klickst auf einen Link und springst zu einer neuen Seite – das ist Hypertext in Aktion.
*   **Transfer:** Das Protokoll dient dem Übertragen, dem Transport von Daten. Dein Browser fordert eine Webseite an, und der Server schickt sie ihm.
*   **Protocol:** Es ist ein festgelegter Satz von Regeln, an den sich sowohl der Client (dein Browser) als auch der Server (der Computer, auf dem die Website liegt) halten müssen, damit die Kommunikation reibungslos funktioniert.

Wenn dein Browser eine HTTP-Anfrage stellt, ist das im Grunde eine simple Textnachricht an den Server, die besagt: „Hey, ich hätte gerne die Datei, die unter dieser Adresse liegt.“ Der Server antwortet dann, ebenfalls mit einer Textnachricht, die entweder die angeforderte Datei (z. B. den HTML-Code einer Seite) oder eine Fehlermeldung enthält (wie den berühmten „404 Not Found“-Fehler).

Die große Schwäche von HTTP ist seine Offenheit. Die Kommunikation zwischen deinem Browser und dem Server findet unverschlüsselt statt. Das ist, als würdest du eine Postkarte verschicken. Jeder, der die Postkarte auf ihrem Weg in die Hände bekommt – der Postbote, der Sortierer im Verteilzentrum –, kann mitlesen, was darauf steht. Für das Abrufen einer öffentlichen Nachrichtenseite mag das kein Problem sein. Aber sobald du persönliche Daten eingibst, wie ein Passwort in einem Login-Formular oder deine Kreditkartendaten beim Online-Shopping, wird diese Offenheit zu einem riesigen Sicherheitsrisiko.

Ein typischer HTTP-Link sieht so aus:

```html
<a href="http://example.com/ueber-uns.html">Über uns</a>
```

Heutzutage wirst du HTTP im freien Web immer seltener antreffen. Moderne Browser warnen sogar explizit davor, wenn eine Seite über HTTP geladen wird, insbesondere wenn sie Formulare für Passwörter oder Zahlungsdaten enthält. Dies führt uns direkt zum modernen Standard.

#### HTTPS: Das sichere Hypertext Transfer Protocol

HTTPS ist im Grunde genommen dasselbe wie HTTP, aber mit einer entscheidenden zusätzlichen Schicht: Sicherheit. Das „S“ am Ende steht für **Secure**.

HTTPS nutzt eine Technologie namens **TLS (Transport Layer Security)**, oder deren Vorgänger SSL (Secure Sockets Layer), um die gesamte Kommunikation zwischen deinem Browser und dem Server zu verschlüsseln.

Bleiben wir bei unserer Post-Analogie: Statt einer offenen Postkarte (HTTP) verschickst du nun einen versiegelten, gepanzerten Brief (HTTPS). Niemand, der diesen Brief auf seinem Weg abfängt, kann ihn öffnen und lesen. Nur der vorgesehene Empfänger, der den passenden Schlüssel hat, kann das Siegel brechen und den Inhalt entschlüsseln.

Dieser Prozess funktioniert in zwei Schritten:

1.  **Authentifizierung:** Bevor überhaupt Daten ausgetauscht werden, weist sich der Server gegenüber deinem Browser mit einem digitalen Zertifikat aus. Dein Browser prüft dieses Zertifikat bei einer vertrauenswürdigen dritten Stelle (einer Certificate Authority). So wird sichergestellt, dass du auch wirklich mit dem Server von `deine-bank.de` sprichst und nicht mit einem Betrüger, der sich als dieser ausgibt.
2.  **Verschlüsselung:** Nachdem die Identität des Servers bestätigt ist, handeln Browser und Server einen einzigartigen, geheimen Schlüssel aus. Mit diesem Schlüssel wird ab sofort die gesamte Kommunikation in beide Richtungen verschlüsselt. Jede Anfrage von dir und jede Antwort vom Server ist nur noch ein unlesbarer Datensalat für jeden, der versucht, mitzuhören.

Du erkennst eine sichere HTTPS-Verbindung am `https://` in der Adresszeile und, viel wichtiger, an dem kleinen **Schloss-Symbol** daneben. Dieses Symbol ist das universelle Zeichen für eine sichere, vertrauenswürdige Verbindung.

Für dich als Webentwickler ist die Botschaft klar: **HTTPS ist der Standard. Immer.** Es geht nicht mehr nur um Online-Shops oder Banking. HTTPS schützt die Privatsphäre deiner Nutzer, verhindert, dass Daten manipuliert werden, und wird von Suchmaschinen wie Google als positives Ranking-Signal bewertet. Die Einrichtung ist heute dank Diensten wie Let's Encrypt oft kostenlos und unkompliziert.

Ein Link zu einer sicheren Seite sieht so aus:

```html
<a href="https://www.meine-sichere-seite.de/login">Zum Login</a>
```

#### mailto: Der direkte Draht zum E-Mail-Programm

Das `mailto`-Protokoll ist ein anderer Typ. Es dient nicht dazu, eine Webseite von einem Server abzurufen. Stattdessen ist es eine Anweisung an den Browser, eine Aktion auf dem Computer des Nutzers auszulösen: das Öffnen des standardmäßig eingerichteten E-Mail-Programms (wie Outlook, Apple Mail oder Thunderbird).

Ein einfacher `mailto`-Link ist schnell erstellt. Du schreibst einfach `mailto:` gefolgt von der E-Mail-Adresse des Empfängers in das `href`-Attribut eines Links.

```html
<a href="mailto:info@beispiel.de">Kontaktiere uns per E-Mail</a>
```

Klickt ein Nutzer auf diesen Link, öffnet sich ein neues E-Mail-Fenster, und im „An“-Feld ist bereits `info@beispiel.de` eingetragen. Das ist praktisch und nutzerfreundlich.

Das Geniale an `mailto` ist, dass du weit mehr als nur den Empfänger vorgeben kannst. Mithilfe von Parametern, die du wie bei einer URL mit einem Fragezeichen `?` beginnst und mit einem Und-Zeichen `&` trennst, kannst du die E-Mail weiter vorbereiten.

Die wichtigsten Parameter sind:

*   `subject`: Gibt den Betreff der E-Mail vor.
*   `body`: Füllt den Nachrichtentext der E-Mail vor.
*   `cc`: Fügt einen Empfänger im „CC“-Feld (Kopie) hinzu.
*   `bcc`: Fügt einen Empfänger im „BCC“-Feld (Blindkopie) hinzu.

Ein wichtiger technischer Hinweis: Innerhalb dieser Parameter dürfen keine Leerzeichen oder Sonderzeichen wie Zeilenumbrüche stehen. Du musst sie URL-kodieren. Das wichtigste Zeichen ist das Leerzeichen, das zu `%20` wird. Ein Zeilenumbruch wird zu `%0A`.

Schauen wir uns ein komplexeres Beispiel an. Angenommen, du möchtest einen Support-Link, der automatisch den Betreff ausfüllt und eine kleine Vorlage für den Nachrichtentext liefert:

```html
<a href="mailto:support@web-agentur.de?subject=Anfrage%20zu%20meiner%20Webseite&body=Sehr%20geehrte%20Damen%20und%20Herren,%0A%0Aich%20habe%20eine%20Frage%20bezüglich...%0A%0AMit%20freundlichen%20Grüßen,">Support kontaktieren</a>
```

Wenn ein Nutzer auf diesen Link klickt, geschieht Folgendes:
1.  Das E-Mail-Programm öffnet sich.
2.  Empfänger: `support@web-agentur.de`
3.  Betreff: `Anfrage zu meiner Webseite`
4.  Textfeld:
    ```
    Sehr geehrte Damen und Herren,

    ich habe eine Frage bezüglich...

    Mit freundlichen Grüßen,
    ```

Dies senkt die Hürde für Nutzer, mit dir in Kontakt zu treten, und hilft dir, Anfragen direkt richtig zuzuordnen. Es ist ein kleines, aber mächtiges Werkzeug für eine bessere User Experience.

Während HTTP und HTTPS die Regeln für den Abruf von Informationen aus dem Web definieren, sind Protokolle wie `mailto` also eher Handlungsanweisungen, die eine Brücke von der Webseite zu einer lokalen Anwendung auf dem Computer des Nutzers schlagen. Das Verständnis dieser fundamentalen Protokolle ist entscheidend, um nicht nur zu wissen, *was* ein Link tut, sondern auch *wie* und *warum* er es tut.
