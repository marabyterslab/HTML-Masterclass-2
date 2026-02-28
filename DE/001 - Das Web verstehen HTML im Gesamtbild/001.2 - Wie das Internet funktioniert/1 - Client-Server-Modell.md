# Client-Server-Modell

### Das Client-Server-Modell: Ein Gespräch zwischen deinem Browser und dem Web

Stell dir vor, du sitzt in einem Restaurant. Du bist der Gast und hast einen Wunsch: Du möchtest ein bestimmtes Gericht von der Speisekarte. Du allein kannst dieses Gericht aber nicht zubereiten, denn die Küche, die Zutaten und der Koch sind im hinteren Teil des Restaurants. Also rufst du einen Kellner, gibst deine Bestellung auf, und der Kellner überbringt sie an die Küche. Die Küche bereitet das Gericht zu und gibt es dem Kellner, der es dir an den Tisch bringt.

Genau dieses Prinzip, nur in digitaler Form, ist das Herzstück des Internets: das Client-Server-Modell. Es ist ein fundamentales Konzept, das beschreibt, wie zwei Computer miteinander kommunizieren, um Aufgaben zu verteilen und Informationen auszutauschen. Wenn du verstehst, wie dieses „Gespräch“ abläuft, verstehst du, was passiert, wenn du eine Webseite aufrufst.

In unserer Restaurant-Analogie bist du der **Client**. Die Küche ist der **Server**. Deine Bestellung ist die **Anfrage** (Request), und das servierte Gericht ist die **Antwort** (Response).

#### Wer ist der Client?

Ein Client ist ein Programm oder ein Gerät, das einen Dienst oder eine Ressource von einem anderen Computer, dem Server, anfordert. In deinem Alltag als Webnutzer ist dein **Webbrowser** (wie Chrome, Firefox, Safari oder Edge) der wichtigste Client. Wenn du eine Webadresse in die Adresszeile eingibst und die Eingabetaste drückst, initiierst du als Client eine Anfrage.

Aber nicht nur Browser sind Clients. Dein E-Mail-Programm (wie Outlook oder Apple Mail) ist ein Client, der E-Mails von einem Mail-Server abruft. Eine App auf deinem Smartphone, die das Wetter anzeigt, ist ein Client, der Wetterdaten von einem Wetter-Server anfordert. Der Client ist immer der aktive Part, der den Kommunikationsprozess startet, weil er etwas benötigt.

Die Hauptaufgabe des Clients im Webkontext ist es:
1.  Eine Anfrage an einen Server zu senden, um eine Ressource (z. B. eine HTML-Seite) zu erhalten.
2.  Die Antwort des Servers zu empfangen und zu verarbeiten.
3.  Die verarbeiteten Daten für dich darzustellen – also die Webseite anzuzeigen.

#### Was ist der Server?

Ein Server ist im Grunde ein leistungsstarker Computer, der permanent mit dem Internet verbunden ist und darauf wartet, Anfragen von Clients zu erhalten. Der Begriff „Server“ kann sich sowohl auf die Hardware (die physische Maschine) als auch auf die Software beziehen, die darauf läuft (z. B. ein Webserver-Programm wie Apache oder Nginx).

Der Server ist der passive, aber dienende Part im Modell. Er wartet geduldig, bis ein Client anklopft. Wenn eine Anfrage eintrifft, ist es seine Aufgabe:
1.  Die Anfrage zu analysieren und zu verstehen, was der Client möchte.
2.  Die angeforderte Ressource zu finden (z. B. eine HTML-Datei auf seiner Festplatte) oder dynamisch zu erstellen (z. B. durch Ausführen eines Programms).
3.  Eine Antwort zu formulieren, die die Ressource oder eine Fehlermeldung enthält.
4.  Diese Antwort zurück an den Client zu senden.

Ein Server ist darauf ausgelegt, viele Anfragen von vielen verschiedenen Clients gleichzeitig zu bedienen – genau wie eine Restaurantküche, die Bestellungen von Dutzenden Tischen gleichzeitig entgegennimmt.

#### Der Dialog im Detail: Der Request-Response-Zyklus

Die gesamte Kommunikation zwischen Client und Server folgt einem strengen Protokoll, dem sogenannten **Request-Response-Zyklus**. Schauen wir uns Schritt für Schritt an, was passiert, wenn du `https://www.beispiel.de/index.html` in deinen Browser eingibst.

**1. Die Übersetzung: Von der Domain zur IP-Adresse**

Dein Browser kann mit dem Namen `www.beispiel.de` zunächst nichts anfangen. Computer im Internet identifizieren sich über einzigartige numerische Adressen, die sogenannten **IP-Adressen** (z. B. `93.184.216.34`). Dein Browser muss also zuerst herausfinden, welche IP-Adresse zum Domainnamen `www.beispiel.de` gehört. Dazu fragt er einen speziellen Server, den **DNS-Server (Domain Name System)**. Du kannst dir das DNS wie das Telefonbuch des Internets vorstellen: Du schlägst einen Namen nach und bekommst die zugehörige Nummer. Sobald der Browser die IP-Adresse hat, weiß er, an welche „Tür“ er klopfen muss.

**2. Der Client formuliert die Anfrage (HTTP Request)**

Jetzt, da der Browser die Adresse des Servers kennt, erstellt er eine formelle Anfrage nach einem standardisierten Regelwerk, dem **Hypertext Transfer Protocol (HTTP)**. Eine solche Anfrage ist im Grunde eine einfache Textnachricht, die aus mehreren Teilen besteht. Eine vereinfachte Version könnte so aussehen:

```http
GET /index.html HTTP/1.1
Host: www.beispiel.de
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36
Accept-Language: de-DE,de;q=0.9
```

Schlüsseln wir das kurz auf:
- **`GET /index.html HTTP/1.1`**: Dies ist die wichtigste Zeile, die sogenannte Request Line.
    - `GET`: Die Methode. Sie sagt dem Server, was der Client tun möchte. `GET` bedeutet: „Ich möchte eine Ressource von dir haben.“ (Eine andere bekannte Methode ist `POST`, die bedeutet: „Ich schicke dir Daten, bitte verarbeite sie“, z. B. beim Absenden eines Kontaktformulars.)
    - `/index.html`: Der Pfad zur Ressource. Der Client möchte die Datei `index.html` aus dem Hauptverzeichnis der Webseite.
    - `HTTP/1.1`: Die Version des Protokolls, das verwendet wird.
- **`Host: www.beispiel.de`**: Gibt an, welche Webseite auf dem Server gemeint ist, da ein Server oft mehrere Webseiten beherbergt.
- **`User-Agent`**: Verrät dem Server, welcher Browser und welches Betriebssystem die Anfrage stellt. Das kann nützlich sein, um die Webseite für bestimmte Geräte zu optimieren.
- **`Accept-Language`**: Teilt dem Server mit, welche Sprache der Nutzer bevorzugt (hier: Deutsch).

**3. Der Server verarbeitet die Anfrage**

Der Webserver unter der IP-Adresse `93.184.216.34` empfängt diese Textnachricht. Seine Software liest die Anfrage Zeile für Zeile.
- „Aha, eine `GET`-Anfrage.“
- „Der Client möchte die Datei `/index.html`.“
- „Ich schaue mal auf meiner Festplatte nach, ob ich diese Datei habe.“

Nehmen wir an, die Datei existiert. Der Server liest den Inhalt der Datei – also den gesamten HTML-Code.

**4. Der Server sendet die Antwort (HTTP Response)**

Nun erstellt der Server seinerseits eine Antwortnachricht, die ebenfalls dem HTTP-Standard folgt. Auch sie besteht aus mehreren Teilen:

```http
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Content-Length: 1256

<!DOCTYPE html>
<html>
<head>
    <title>Beispielseite</title>
</head>
<body>
    <h1>Willkommen!</h1>
    <p>Dies ist eine Beispiel-HTML-Seite.</p>
    <img src="/bilder/logo.png">
</body>
</html>
```

Analysieren wir auch diese Antwort:
- **`HTTP/1.1 200 OK`**: Dies ist die Statuszeile.
    - `200`: Der Statuscode. `200` ist der Code für „Erfolg“ oder „Alles in Ordnung“. Du kennst sicher auch einen anderen berühmten Code: `404 Not Found`. Er bedeutet, der Server hat die Anfrage verstanden, aber die angeforderte Ressource nicht gefunden.
    - `OK`: Eine kurze, menschenlesbare Beschreibung des Statuscodes.
- **`Content-Type: text/html`**: Ein extrem wichtiger Header. Er teilt dem Browser mit, welche Art von Daten er im Hauptteil der Antwort erwarten kann. Hier ist es HTML-Text. Für ein Bild wäre es z. B. `image/jpeg`.
- **`Content-Length: 1256`**: Gibt an, wie groß die gesendeten Daten sind (in Bytes).
- **Der leere Bereich**: Eine Leerzeile trennt die Metadaten (Header) vom eigentlichen Inhalt.
- **Der Body (Nachrichtenkörper)**: Hier folgt der eigentliche Inhalt der Datei `index.html` – der HTML-Code, den du schreibst und lernst.

**5. Der Client verarbeitet die Antwort**

Dein Browser empfängt diese Antwort. Er liest zuerst die Header.
- „Status `200 OK` – super, hat geklappt!“
- „`Content-Type` ist `text/html`. Ich weiß also, dass ich den Body als HTML-Dokument interpretieren muss.“

Nun beginnt der Browser, den HTML-Code im Body Zeile für Zeile zu lesen (diesen Prozess nennt man „Parsen“). Er baut daraus die interne Struktur der Webseite auf. Dabei stößt er auf weitere Anweisungen. In unserem Beispiel findet er den Tag `<img src="/bilder/logo.png">`.

Und jetzt passiert etwas Entscheidendes: Der Browser erkennt, dass er eine weitere Ressource benötigt, um die Seite vollständig darzustellen – nämlich das Bild `logo.png`. Was tut er? Er startet einen komplett neuen Client-Server-Zyklus!

Er formuliert eine neue HTTP-Anfrage: `GET /bilder/logo.png HTTP/1.1` an denselben Server. Der Server antwortet, diesmal hoffentlich mit `200 OK`, dem `Content-Type: image/png` und den Bilddaten im Body.

Eine einzige Webseite kann so Dutzende oder sogar Hunderte solcher kleinen „Gespräche“ auslösen – für jede CSS-Datei, jede JavaScript-Datei, jedes Bild und jede Schriftart. Der Browser ist der Dirigent, der all diese Anfragen koordiniert und am Ende alle Puzzleteile zusammensetzt, um dir die fertige, visuelle Webseite zu präsentieren.

#### Warum ist dieses Modell für dich wichtig?

Das Client-Server-Modell ist keine abstrakte Theorie. Es ist die Grundlage für deine Arbeit mit HTML.
- **HTML ist die Sprache der Antwort:** Der HTML-Code, den du schreibst, ist fast immer der Inhalt, der im Body einer HTTP-Antwort vom Server zum Client geschickt wird.
- **Kontext für Links und Ressourcen:** Wenn du einen Link (`<a>`), ein Bild (`<img>`) oder ein Stylesheet (`<link>`) einfügst, definierst du damit potenzielle, zukünftige Client-Anfragen. Du sagst dem Browser: „Wenn du diesen Teil der Seite darstellst, musst du eventuell eine weitere Anfrage an diesen Ort senden.“
- **Grundlage für die Fehlersuche:** Wenn eine Webseite nicht richtig lädt, hilft dir das Wissen über dieses Modell. Zeigt der Browser einen `404`-Fehler? Dann liegt das Problem wahrscheinlich auf dem Server (Datei fehlt oder Pfad ist falsch). Wird die Seite falsch dargestellt? Dann könnte der HTML-Code fehlerhaft sein, und der Client (Browser) kann ihn nicht richtig interpretieren.

Indem du das ständige Gespräch zwischen dem anfragenden Client und dem antwortenden Server verstehst, begreifst du, dass eine HTML-Datei nicht nur ein isoliertes Dokument ist. Sie ist der zentrale Baustein in einem dynamischen Kommunikationsprozess, der das World Wide Web erst möglich macht.
