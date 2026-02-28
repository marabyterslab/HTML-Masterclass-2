# Client-Server-Modell

### Das Client-Server-Modell: Ein Dialog im Web

Stell dir vor, du sitzt in einem Restaurant. Du bist der Gast und hast einen Wunsch: Du möchtest etwas essen. Du schaust in die Speisekarte, entscheidest dich und rufst den Kellner. Du gibst deine Bestellung auf. Der Kellner notiert sie und bringt sie in die Küche. Dort bereiten die Köche dein Gericht zu. Sobald es fertig ist, bringt der Kellner es an deinen Tisch. Du erhältst genau das, was du bestellt hast (oder solltest es zumindest).

Dieses einfache Szenario beschreibt im Grunde perfekt das Client-Server-Modell, das dem gesamten World Wide Web zugrunde liegt. Es ist ein fundamentaler Dialog zwischen zwei Parteien: einem, der eine Anfrage stellt (dem Client), und einem, der eine Antwort liefert (dem Server). Lass uns diese Rollen und den Ablauf genauer betrachten.

#### Der Client: Dein Fenster zum Web

In unserer Restaurant-Analogie bist du der Gast. Im Web ist der **Client** die Software, die du verwendest, um auf Informationen zuzugreifen. In den allermeisten Fällen ist das dein Webbrowser – sei es Google Chrome, Mozilla Firefox, Apple Safari oder Microsoft Edge. Aber auch andere Programme können Clients sein, zum Beispiel eine Smartphone-App, die Wetterdaten abruft, oder ein E-Mail-Programm.

Die Hauptaufgabe des Clients ist es, eine **Anfrage** (englisch: *Request*) zu formulieren und an einen Server zu senden. Wenn du eine Webadresse wie `https://www.beispiel.de` in die Adresszeile deines Browsers eingibst und die Enter-Taste drückst, erstellst du genau eine solche Anfrage. Du sagst damit: "Hallo, ich hätte gerne die Startseite von beispiel.de". Der Client ist also der aktive Part, der den Dialog initiiert. Er weiß, was er will, und fragt danach.

#### Der Server: Das unermüdliche Gehirn im Hintergrund

Die Küche im Restaurant, die auf Bestellungen wartet und Gerichte zubereitet, ist das Gegenstück zum **Server**. Ein Server ist im Kern ein leistungsstarker Computer (oder ein Verbund von Computern), auf dem eine spezielle Software läuft, die permanent auf Anfragen von Clients lauscht. Diese Software wird Webserver genannt, bekannte Beispiele sind Apache oder Nginx.

Im Gegensatz zum Client, der nur bei Bedarf aktiv wird, ist der Server immer "im Dienst". Er wartet geduldig, Tag und Nacht, darauf, dass eine Anfrage eintrifft. Seine Aufgabe ist es, diese Anfrage zu verstehen, die gewünschte Ressource zu finden – zum Beispiel eine HTML-Datei, ein Bild, ein Video oder Daten aus einer Datenbank – und diese in einer **Antwort** (englisch: *Response*) an den anfragenden Client zurückzuschicken.

Ein Server speichert und verwaltet also die Webseiten und alle zugehörigen Dateien. Wenn du eine eigene Webseite ins Netz stellen möchtest, mietest du im Grunde Speicherplatz auf einem solchen Server, damit er deine HTML-, CSS- und JavaScript-Dateien an die Browser der Welt ausliefern kann.

#### Die Kommunikation: Wie Client und Server miteinander sprechen

Damit der Dialog zwischen Gast und Küche funktioniert, brauchen sie eine gemeinsame Sprache und Regeln. Der Gast bestellt nicht, indem er wirre Laute von sich gibt, sondern indem er ein Gericht aus der Karte nennt. Der Kellner liefert nicht einfach irgendein Essen, sondern das bestellte Gericht auf einem Teller.

Im Web wird diese gemeinsame Sprache durch Protokolle geregelt. Das wichtigste Protokoll für uns ist das **Hypertext Transfer Protocol**, kurz **HTTP** (oder seine sichere Variante **HTTPS**). HTTP definiert exakt, wie eine Anfrage des Clients auszusehen hat und wie die Antwort des Servers strukturiert sein muss.

**Der Request des Clients**

Eine HTTP-Anfrage, die dein Browser sendet, besteht aus mehreren Teilen. Vereinfacht sieht sie so aus:

```http
GET /index.html HTTP/1.1
Host: www.beispiel.de
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
```

Schauen wir uns die wichtigsten Zeilen an:

1.  **`GET /index.html HTTP/1.1`**: Das ist die sogenannte *Request Line*.
    *   `GET` ist die Methode. Sie sagt dem Server, was der Client tun möchte. `GET` bedeutet "Ich möchte eine Ressource abrufen". Das ist die häufigste Methode, wenn du eine Webseite aufrufst. Eine andere wichtige Methode ist `POST`, die verwendet wird, um Daten an den Server zu senden (z.B. bei der Anmeldung auf einer Webseite oder dem Abschicken eines Kontaktformulars).
    *   `/index.html` ist der Pfad zur gewünschten Ressource. Das `/` steht für das Hauptverzeichnis der Webseite.
    *   `HTTP/1.1` ist die Version des Protokolls, die verwendet wird.

2.  **`Host: www.beispiel.de`**: Dieser Teil, ein sogenannter *Header*, gibt an, welcher Server gemeint ist. Auf einem physischen Computer können nämlich mehrere Webseiten (und damit mehrere Server-Instanzen) laufen.

3.  **`User-Agent: ...`**: Dieser Header verrät dem Server, welcher Browser in welcher Version die Anfrage stellt. Das kann nützlich sein, damit der Server eventuell eine für diesen Browser optimierte Version der Seite ausliefern kann.

**Die Response des Servers**

Nachdem der Server die Anfrage erhalten und verarbeitet hat, schickt er eine Antwort zurück. Auch diese folgt einer klaren Struktur:

```http
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Content-Length: 1270

<!DOCTYPE html>
<html>
<head>
  <title>Beispielseite</title>
</head>
<body>
  <h1>Hallo Welt!</h1>
  <p>Dies ist der Inhalt der Webseite.</p>
</body>
</html>
```

Analysieren wir auch diese Antwort:

1.  **`HTTP/1.1 200 OK`**: Das ist die *Status Line*.
    *   `200` ist der **Statuscode**. Er signalisiert dem Client, ob die Anfrage erfolgreich war. `200 OK` bedeutet: "Alles in Ordnung, hier sind die Daten, die du wolltest." Du bist sicher schon auf andere Codes gestoßen: `404 Not Found` bedeutet, dass die angeforderte Ressource nicht existiert. Ein `500 Internal Server Error` signalisiert, dass auf der Serverseite etwas schiefgelaufen ist.
2.  **`Content-Type: text/html`**: Dieser Header teilt dem Browser mit, welche Art von Inhalt er empfängt. In diesem Fall ist es ein HTML-Dokument. Wäre es ein Bild, stünde hier vielleicht `image/jpeg`. Dies ist entscheidend, damit der Browser weiß, wie er die Daten verarbeiten und darstellen soll.
3.  **Leerzeile**: Eine einzelne Leerzeile trennt die Header vom eigentlichen Inhalt.
4.  **Der Body**: Nach der Leerzeile folgt der eigentliche Inhalt der Antwort, der sogenannte *Body* oder die *Payload*. Und genau hier findest du das, worum es in diesem Kurs geht: den **HTML-Code** der Webseite.

#### Der vollständige Kreislauf

Fassen wir den gesamten Prozess noch einmal zusammen, von deinem Klick bis zur angezeigten Webseite:

1.  **Du gibst eine URL ein**: Du tippst `https://www.beispiel.de` in deinen Browser (den Client).
2.  **Der Client erstellt einen Request**: Dein Browser formuliert eine HTTP-`GET`-Anfrage für die Startseite.
3.  **Die Reise durchs Netz**: Die Anfrage wird über das Internet an die Adresse geschickt, die hinter `www.beispiel.de` steckt. DNS-Server (Domain Name System) helfen dabei, den Namen in die richtige IP-Adresse des Servers zu übersetzen.
4.  **Der Server empfängt den Request**: Der Webserver auf dem Zielcomputer nimmt die Anfrage entgegen.
5.  **Der Server verarbeitet die Anfrage**: Er schaut nach, welche Datei angefordert wurde (`/`), findet die entsprechende `index.html`-Datei auf seiner Festplatte.
6.  **Der Server erstellt eine Response**: Er packt den Inhalt der HTML-Datei in den Body einer HTTP-Antwort, fügt den Statuscode `200 OK` und passende Header wie `Content-Type: text/html` hinzu.
7.  **Die Rückreise**: Die Antwort wird über das Internet zurück an deinen Browser geschickt.
8.  **Der Client rendert die Seite**: Dein Browser empfängt die Antwort. Er liest den `Content-Type`-Header, erkennt, dass es sich um HTML handelt, und beginnt, den Code im Body zu interpretieren und die Webseite visuell auf deinem Bildschirm darzustellen.

Ein wichtiger Punkt: Eine Webseite besteht selten nur aus einer einzigen HTML-Datei. Innerhalb des HTML-Codes finden sich oft Verweise auf weitere Ressourcen wie CSS-Dateien für das Styling, JavaScript-Dateien für die Interaktivität und Bilddateien. Sobald der Browser auf solche Verweise stößt, startet er für jede einzelne dieser Dateien einen neuen Client-Server-Dialog: Er stellt eine neue `GET`-Anfrage für die CSS-Datei, eine für die JavaScript-Datei, eine für jedes Bild und so weiter. Eine komplexe Webseite kann so Dutzende oder sogar Hunderte solcher kleinen Dialoge auslösen, bis alles geladen ist.

Das Client-Server-Modell ist also eine klare Arbeitsteilung. Der Client ist für die Darstellung und die Interaktion mit dir zuständig, der Server für die Speicherung, Verwaltung und Auslieferung der Daten. Wenn du HTML schreibst, erstellst du genau die Dokumente, die der Server als Antwort auf eine Anfrage des Clients verschicken wird. Dieses grundlegende Verständnis der Kommunikation ist der Schlüssel, um zu verstehen, wie deine Codezeilen letztendlich zu einer lebendigen Webseite im Browser eines Nutzers auf der anderen Seite der Welt werden.
