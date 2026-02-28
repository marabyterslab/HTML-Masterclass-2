# Client-Server-Modell

### Das Herz des Internets: Das Client-Server-Modell

Stell dir vor, du gehst in ein Restaurant. Du bist der Gast, setzt dich an einen Tisch und hast ein Bedürfnis: Du möchtest etwas essen. Du schaust in die Speisekarte und rufst den Kellner. Du gibst deine Bestellung auf – eine Anfrage nach einem bestimmten Gericht. Der Kellner notiert sie und bringt sie in die Küche. Die Küche, die alle Zutaten und das Know-how hat, bereitet dein Essen zu. Sobald es fertig ist, bringt der Kellner es dir zurück an den Tisch – die Antwort auf deine Anfrage.

Dieses einfache Szenario beschreibt perfekt die Grundlage, auf der fast das gesamte Internet funktioniert: das Client-Server-Modell. Es ist ein fundamentaler Dialog, ein ständiges Frage- und Antwortspiel, das im Hintergrund abläuft, wann immer du eine Webseite besuchst, eine E-Mail sendest oder eine App auf deinem Smartphone nutzt. Um zu verstehen, wie HTML-Seiten auf deinen Bildschirm gelangen, müssen wir uns diese beiden Hauptdarsteller und ihre Kommunikation genauer ansehen.

#### Die Hauptdarsteller: Client und Server

In diesem digitalen Restaurant gibt es zwei klare Rollen, die immer wieder neu besetzt werden.

**Der Client: Dein Fenster zum Web**

Der Client ist der „Gast“ in unserer Analogie. Es ist das Programm auf deinem Gerät, das eine Anfrage stellt, weil es etwas benötigt. In den meisten Fällen, wenn du im Web surfst, ist dein Webbrowser (wie Chrome, Firefox oder Safari) der Client. Er ist deine Software, die den Wunsch hat, eine Webseite darzustellen.

Doch ein Client kann viel mehr sein als nur ein Browser:
*   Dein E-Mail-Programm ist ein Client, der neue Mails vom Mailserver abruft.
*   Eine Wetter-App auf deinem Handy ist ein Client, der aktuelle Wetterdaten von einem Server anfordert.
*   Ein Online-Spiel ist ein Client, der Spieldaten mit einem Gameserver austauscht.

Die entscheidende Eigenschaft des Clients ist: **Er ergreift die Initiative.** Er startet die Kommunikation, weil er eine Ressource oder einen Dienst von jemand anderem braucht. Er weiß, was er will, aber er besitzt es nicht selbst.

**Der Server: Das Kraftwerk im Hintergrund**

Der Server ist die „Küche“ und der „Kellner“ in einem. Es ist in der Regel ein leistungsstarker Computer (oder ein Verbund von Computern), der irgendwo auf der Welt in einem Rechenzentrum steht und rund um die Uhr läuft. Seine Hauptaufgabe ist es, auf Anfragen von Clients zu warten und diese zu bedienen.

Ein Server ist im Grunde ein Spezialist. Er speichert Ressourcen und stellt Dienste bereit. Es gibt viele Arten von Servern, die für unterschiedliche Aufgaben optimiert sind:
*   **Webserver:** Ihre Spezialität ist das Speichern und Ausliefern von Webseiten – also HTML-Dateien, CSS-Stylesheets, JavaScript-Code, Bilder und Videos. Wenn du eine URL in deinen Browser eingibst, sprichst du mit einem Webserver. Bekannte Webserver-Software ist zum Beispiel Apache oder Nginx.
*   **Datenbankserver:** Sie sind darauf spezialisiert, riesige Mengen an strukturierten Daten zu speichern, zu verwalten und abrufbar zu machen. Eine Social-Media-Webseite nutzt einen Datenbankserver, um all deine Beiträge und Freundeslisten zu speichern.
*   **Mailserver:** Sie kümmern sich um das Senden, Empfangen und Speichern von E-Mails.

Die entscheidende Eigenschaft des Servers ist: **Er ist reaktiv.** Er wartet passiv, bis eine Anfrage eintrifft. Dann verarbeitet er diese Anfrage, sucht die angeforderte Ressource oder führt einen Dienst aus und sendet eine Antwort zurück an den Client, der gefragt hat.

#### Der Dialog: Request und Response

Die gesamte Kommunikation zwischen Client und Server folgt einem strengen Protokoll, einem festen Ablauf, der als Request-Response-Zyklus (Anfrage-Antwort-Zyklus) bekannt ist. Die Sprache, die sie dabei meistens sprechen, heißt **HTTP** (Hypertext Transfer Protocol) oder die sichere Variante **HTTPS**.

Stellen wir uns den genauen Ablauf vor, wenn du `https://www.beispiel.de/ueber-uns.html` in deinen Browser eingibst und Enter drückst:

**1. Die Anfrage (Request)**

Dein Browser (der Client) erstellt eine formelle Anfrage, eine Art digitalen Bestellzettel. Diese HTTP-Anfrage enthält mehrere wichtige Informationen:

*   **Die Methode:** Sie beschreibt die Art der Anfrage. Die häufigste Methode ist `GET`. Sie bedeutet so viel wie: „Gib mir bitte die Ressource, die unter dieser Adresse liegt.“ Eine andere wichtige Methode ist `POST`, die oft verwendet wird, um Daten an den Server zu senden, zum Beispiel wenn du ein Kontaktformular ausfüllst.
*   **Die Zieladresse:** Der genaue Pfad zur gewünschten Ressource auf dem Server. In unserem Fall ist das `/ueber-uns.html`.
*   **HTTP-Header:** Das sind zusätzliche Metadaten, die dem Server mehr Kontext geben. Hier steht zum Beispiel drin, welchen Browser du verwendest (`User-Agent`), welche Sprachen du bevorzugst (`Accept-Language`) oder welche Arten von Inhalten dein Browser versteht (`Accept`).

Eine stark vereinfachte HTTP-Anfrage könnte so aussehen:

```http
GET /ueber-uns.html HTTP/1.1
Host: www.beispiel.de
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept-Language: de-DE,de;q=0.9
```

Diese Anfrage wird über das Internet an die richtige IP-Adresse des Servers von `beispiel.de` geschickt. (Die Umwandlung des Domainnamens in eine IP-Adresse übernimmt übrigens das DNS, das „Telefonbuch des Internets“, aber das ist eine eigene Geschichte.)

**2. Die Server-Verarbeitung**

Der Webserver von `beispiel.de` hat die ganze Zeit gelauscht und empfängt nun deine Anfrage. Er schaut sie sich genau an:
*   „Aha, eine `GET`-Anfrage.“
*   „Der Client möchte die Datei `/ueber-uns.html`.“
*   „Ich schaue mal auf meiner Festplatte nach, ob ich diese Datei habe.“

In einfachen Fällen wie diesem findet der Server die HTML-Datei, packt sie für den Versand ein und bereitet seine Antwort vor. Bei komplexeren Webseiten könnte hier noch viel mehr passieren. Vielleicht muss der Server erst ein Skript (z.B. in PHP oder Python) ausführen, um die Seite dynamisch zu erstellen, indem er Informationen aus einer Datenbank abruft – zum Beispiel um die aktuellsten Teammitglieder auf der „Über uns“-Seite anzuzeigen.

**3. Die Antwort (Response)**

Nachdem der Server seine Arbeit getan hat, schickt er eine HTTP-Antwort zurück an deinen Browser. Auch diese Antwort ist klar strukturiert:

*   **Der Statuscode:** Eine dreistellige Zahl, die dem Client auf einen Blick mitteilt, ob die Anfrage erfolgreich war. Du kennst einige davon bestimmt:
    *   `200 OK`: Alles super! Hier ist die Ressource, die du wolltest.
    *   `404 Not Found`: Ups, ich konnte die angeforderte Datei unter diesem Pfad nicht finden. Das ist die berühmte „Seite nicht gefunden“-Meldung.
    *   `301 Moved Permanently`: Die Ressource ist dauerhaft umgezogen. Hier ist die neue Adresse.
    *   `500 Internal Server Error`: Mir ist ein interner Fehler passiert. In der Küche ist etwas schiefgelaufen, ich kann deine Bestellung nicht bearbeiten.
*   **HTTP-Header:** Auch die Antwort enthält Metadaten. Zum Beispiel, um welchen Inhaltstyp es sich handelt (`Content-Type: text/html`), wie groß die Datei ist (`Content-Length`) oder wann sie zuletzt geändert wurde.
*   **Der Body (Inhalt):** Das ist das Wichtigste – die eigentlichen Daten, die der Client angefordert hat. In unserem Fall ist das der gesamte HTML-Code der Datei `ueber-uns.html`.

Eine stark vereinfachte HTTP-Antwort könnte so aussehen:

```http
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Content-Length: 1234

<!DOCTYPE html>
<html>
<head>
  <title>Über uns</title>
</head>
<body>
  <h1>Unser Team</h1>
  <p>Das ist unsere Firmengeschichte...</p>
</body>
</html>
```

**4. Die Darstellung im Client**

Dein Browser empfängt diese Antwort. Er sieht den Statuscode `200 OK` und weiß: Erfolg! Dann liest er den `Content-Type`-Header und erkennt, dass er HTML-Code erhalten hat. Nun beginnt seine eigentliche Arbeit als Browser: Er interpretiert (parst) den HTML-Code im Body, baut daraus die Seitenstruktur auf und stellt sie auf deinem Bildschirm dar. Wenn das HTML weitere Ressourcen referenziert – wie ein CSS-Stylesheet, JavaScript-Dateien oder Bilder –, startet der Browser für jede einzelne dieser Ressourcen einen neuen Request-Response-Zyklus. Er stellt also viele kleine Anfragen an den Server, bis die Seite komplett geladen ist.

#### Ein kurzes Gedächtnis: Das Prinzip der Zustandslosigkeit

Eine entscheidende Eigenschaft des HTTP-Protokolls ist seine **Zustandslosigkeit (Statelessness)**. Das bedeutet: Der Server hat kein Gedächtnis. Jede Anfrage ist für ihn eine völlig neue, unabhängige Transaktion. Er weiß nach einer Anfrage nicht mehr, wer du warst oder was du davor angefragt hast. Der Kellner in unserem Restaurant hätte dich also bei jeder neuen Bestellung (z. B. für ein Dessert) wieder gefragt, an welchem Tisch du sitzt.

Das ist einerseits sehr effizient, weil es den Server einfach hält. Andererseits brauchen wir für Dinge wie Warenkörbe oder Login-Bereiche einen „Zustand“. Um dieses Problem zu lösen, wurden Techniken wie Cookies erfunden. Ein Cookie ist eine kleine Information, die der Server dem Client mitschickt und ihn bittet, sie bei jeder zukünftigen Anfrage wieder vorzuzeigen – wie ein Armbändchen, das du am Eingang eines Festivals bekommst, um immer wieder reinzukommen.

Das Client-Server-Modell ist also ein elegantes und robustes System, das eine klare Arbeitsteilung schafft. Der Client ist für die Interaktion mit dem Nutzer und die Darstellung der Daten zuständig. Der Server ist für die Speicherung, Verarbeitung und Bereitstellung dieser Daten verantwortlich. Diese Trennung ermöglicht es dem riesigen, dezentralen Netzwerk, das wir Internet nennen, überhaupt erst zu funktionieren. Jedes Mal, wenn du eine Webseite lädst, bist du Zeuge dieses unermüdlichen Dialogs zwischen einem anfragenden Client und einem dienenden Server.
