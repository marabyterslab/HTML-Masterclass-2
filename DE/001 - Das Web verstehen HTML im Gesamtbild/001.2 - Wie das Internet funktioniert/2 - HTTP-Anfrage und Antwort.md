# HTTP-Anfrage und Antwort

### HTTP-Anfrage und Antwort: Das Zwiegespräch des Webs

Jedes Mal, wenn du eine Webseite in deinem Browser aufrufst, einen Link anklickst oder ein Formular abschickst, findet im Hintergrund eine unsichtbare, aber entscheidende Kommunikation statt. Man kann es sich wie ein kurzes, präzises Gespräch zwischen zwei Parteien vorstellen: deinem Webbrowser (dem Client) und dem Computer, auf dem die Webseite gespeichert ist (dem Server). Dieses Gespräch folgt strengen Regeln, einem Protokoll namens **HTTP** – dem Hypertext Transfer Protocol. Es ist die Sprache, die das Web zusammenhält. Schauen wir uns dieses Zwiegespräch, bestehend aus einer Anfrage und einer Antwort, einmal genauer an.

#### Die HTTP-Anfrage: Wenn dein Browser etwas möchte

Der erste Schritt geht immer von deinem Browser aus. Er ist der Client, der etwas vom Server anfordert. Diese Anforderung ist kein formloser Zuruf, sondern eine klar strukturierte Nachricht, die HTTP-Anfrage (HTTP Request). Sie besteht aus bis zu drei Teilen: der Startzeile, den Header-Feldern und einem optionalen Nachrichtenkörper.

##### 1. Die Startzeile

Die erste Zeile einer jeden Anfrage ist die wichtigste. Sie legt fest, *was* der Browser tun möchte, *welche* Ressource er anfordert und *welche Sprachversion* des Protokolls er verwendet.

*   **HTTP-Methode:** Das ist das Verb der Anfrage. Es beschreibt die Aktion, die der Server ausführen soll. Die beiden bekanntesten Methoden sind `GET` und `POST`.
    *   `GET`: Dies ist die bei Weitem häufigste Methode. Sie bedeutet so viel wie: „Gib mir bitte diese Ressource.“ Wenn du eine URL in die Adresszeile eingibst oder auf einen normalen Link klickst, sendet dein Browser eine `GET`-Anfrage. Er fordert einfach nur Daten an, ohne etwas auf dem Server zu verändern.
    *   `POST`: Diese Methode wird verwendet, um Daten an den Server zu senden, damit dieser sie verarbeitet. Ein typisches Beispiel ist das Abschicken eines Kontakt- oder Login-Formulars. Die Daten (dein Name, dein Passwort) werden im Bauch der Anfrage mitgeschickt. `POST` bedeutet also: „Hier hast du Daten, bitte verarbeite sie.“
    *   Es gibt noch weitere Methoden wie `PUT` (um eine Ressource zu erstellen oder zu ersetzen) oder `DELETE` (um eine Ressource zu löschen), die aber eher in der fortgeschrittenen Webentwicklung eine Rolle spielen.

*   **URI (Uniform Resource Identifier):** Das ist die genaue Adresse der gewünschten Ressource auf dem Server. Es ist der Teil der URL, der nach dem Domainnamen kommt. Für die Seite `https://www.beispiel-akademie.de/kurse/html-einfuehrung` wäre der URI `/kurse/html-einfuehrung`.

*   **HTTP-Version:** Am Ende der Zeile steht die Version des Protokolls, die der Browser spricht, meist `HTTP/1.1` oder das neuere `HTTP/2`.

Eine typische Startzeile für den Aufruf einer Webseite sieht also so aus: `GET /index.html HTTP/1.1`.

##### 2. Die Header-Felder

Direkt nach der Startzeile folgt eine Liste von Header-Feldern. Man kann sie sich wie zusätzliche Informationen oder Metadaten vorstellen, die der Browser dem Server mit auf den Weg gibt. Sie funktionieren nach dem einfachen `Schlüssel: Wert`-Prinzip. Einige wichtige Header sind:

*   `Host`: Dieser Header ist unverzichtbar. Er nennt den Domainnamen der Webseite, die du besuchen möchtest (z. B. `Host: www.beispiel-akademie.de`). Warum ist das nötig? Weil auf einem einzigen Server oft Hunderte von verschiedenen Webseiten liegen. Der Server muss wissen, für welche davon die Anfrage bestimmt ist.
*   `User-Agent`: Hier stellt sich dein Browser vor. Er teilt dem Server mit, welcher Browser in welcher Version auf welchem Betriebssystem läuft. Das kann der Server nutzen, um beispielsweise eine für Mobilgeräte optimierte Version der Seite auszuliefern.
*   `Accept`: Damit teilt der Browser dem Server mit, welche Dateiformate er versteht. Zum Beispiel `text/html` für Webseiten, `image/jpeg` für Bilder oder `application/json` für Daten.
*   `Accept-Language`: Hier erfährt der Server, welche Sprachen du bevorzugst, zum Beispiel `de-DE` für deutsches Deutsch. Eine gut konfigurierte Webseite kann dich dann automatisch auf die deutsche Version weiterleiten.

##### 3. Der Nachrichtenkörper (Body)

Dieser Teil ist optional und meistens leer bei `GET`-Anfragen. Wenn du jedoch Daten mit einer `POST`-Anfrage sendest – wie die Zugangsdaten aus einem Login-Formular –, dann werden diese Daten hier im sogenannten Body platziert.

Hier ist ein Beispiel für eine vollständige, aber einfache `GET`-Anfrage, wie sie dein Browser senden könnte, um eine Webseite anzufordern:

```http
GET /artikel/was-ist-html.html HTTP/1.1
Host: www.beispiel-akademie.de
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: de-DE,de;q=0.9
```

---

#### Die HTTP-Antwort: Was der Server zurückgibt

Nachdem der Server die Anfrage erhalten und verarbeitet hat, schickt er eine Antwort (HTTP Response) zurück. Diese ist ähnlich aufgebaut wie die Anfrage und besteht ebenfalls aus einer Statuszeile, Headern und meistens einem Nachrichtenkörper.

##### 1. Die Statuszeile

Auch hier ist die erste Zeile entscheidend. Sie gibt ein schnelles Feedback darüber, ob die Anfrage erfolgreich war.

*   **HTTP-Version:** Die Protokollversion, die der Server verwendet.
*   **Statuscode:** Eine dreistellige Zahl, die das Ergebnis der Anfrage zusammenfasst. Diese Codes sind standardisiert und ein essenzieller Teil der Webkommunikation. Sie sind in fünf Klassen unterteilt:
    *   **1xx (Information):** Selten anzutreffen. Bedeutet so viel wie „Anfrage erhalten, ich arbeite noch.“
    *   **2xx (Erfolg):** Die Anfrage war erfolgreich!
        *   `200 OK`: Der Klassiker. Alles hat geklappt, und die angeforderten Daten sind im Body der Antwort enthalten.
    *   **3xx (Umleitung):** Die angeforderte Ressource ist umgezogen.
        *   `301 Moved Permanently`: Die Ressource hat eine neue, dauerhafte Adresse. Der Browser sollte sich diese merken.
        *   `302 Found`: Eine temporäre Umleitung. Der Browser sollte es beim nächsten Mal wieder unter der alten Adresse versuchen.
    *   **4xx (Client-Fehler):** Der Fehler liegt auf deiner Seite (bzw. auf der des Browsers). Du hast etwas Falsches angefordert.
        *   `404 Not Found`: Der wohl bekannteste Fehlercode. Die angeforderte Ressource konnte auf dem Server nicht gefunden werden. Der Link ist veraltet oder du hast dich vertippt.
        *   `403 Forbidden`: Du hast keine Berechtigung, auf diese Ressource zuzugreifen. Die Tür ist da, aber sie ist für dich verschlossen.
    *   **5xx (Server-Fehler):** Der Fehler liegt beim Server. Er hat ein Problem und konnte die gültige Anfrage nicht bearbeiten.
        *   `500 Internal Server Error`: Ein allgemeiner Sammelfehler. Irgendetwas auf dem Server ist schiefgelaufen – ein Programmierfehler, eine überlastete Datenbank etc.

*   **Statusnachricht:** Eine kurze, für Menschen lesbare Beschreibung des Statuscodes, wie „OK“ oder „Not Found“.

##### 2. Die Header-Felder

Genau wie die Anfrage enthält auch die Antwort Header-Felder, die zusätzliche Informationen über die Antwort selbst liefern.

*   `Content-Type`: Einer der wichtigsten Header. Er teilt dem Browser mit, um welche Art von Daten es sich im Body handelt, z. B. `text/html; charset=utf-8`. Erst dadurch weiß der Browser, dass er den Inhalt als Webseite darstellen und nicht etwa als reinen Text oder als Bild anzeigen soll.
*   `Content-Length`: Gibt die Größe des Nachrichtenkörpers in Bytes an.
*   `Date`: Das Datum und die Uhrzeit, zu der die Antwort vom Server generiert wurde.
*   `Set-Cookie`: Wenn eine Webseite ein Cookie auf deinem Computer speichern möchte (z. B. um dich eingeloggt zu halten), nutzt sie diesen Header, um es an den Browser zu senden.

##### 3. Der Nachrichtenkörper (Body)

Hier befindet sich der eigentliche Inhalt, den du angefordert hast. Wenn du eine Webseite angefordert hast, enthält der Body den gesamten HTML-Code dieser Seite. Wenn du ein Bild angefordert hast, enthält er die binären Bilddaten. Bei einem `404 Not Found` enthält der Body oft eine schön gestaltete HTML-Fehlerseite, die dir erklärt, was schiefgelaufen ist.

Eine typische, erfolgreiche Antwort auf unsere vorherige Anfrage könnte so aussehen:

```http
HTTP/1.1 200 OK
Date: Wed, 14 Dec 2022 10:00:00 GMT
Server: Apache/2.4.1 (Unix)
Content-Type: text/html; charset=UTF-8
Content-Length: 1582

<!DOCTYPE html>
<html>
<head>
    <title>Was ist HTML?</title>
</head>
<body>
    <h1>Eine Einführung in HTML</h1>
    <p>HTML ist die Grundlage jeder Webseite...</p>
    <!-- ... weiterer HTML-Code ... -->
</body>
</html>
```

Sobald dein Browser diese Antwort erhält, liest er die Header, erkennt am `Content-Type`, dass es sich um ein HTML-Dokument handelt, und beginnt sofort damit, den HTML-Code aus dem Body zu interpretieren und die Webseite auf deinem Bildschirm darzustellen. Wenn diese HTML-Seite weitere Ressourcen wie CSS-Dateien, JavaScript-Dateien oder Bilder verlinkt, startet der Browser für jede einzelne dieser Ressourcen einen neuen Zyklus aus HTTP-Anfrage und -Antwort, bis die Seite vollständig geladen ist.
