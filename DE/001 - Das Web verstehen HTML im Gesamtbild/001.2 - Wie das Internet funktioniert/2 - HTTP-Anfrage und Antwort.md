# HTTP-Anfrage und Antwort

### HTTP-Anfrage und Antwort: Der Dialog des Webs

Stell dir vor, du sitzt in einem Café und möchtest einen Kaffee bestellen. Du rufst den Kellner, sagst ihm genau, was du möchtest („Einen Cappuccino, bitte“), und vielleicht fügst du noch eine Zusatzinformation hinzu („mit Hafermilch“). Der Kellner nimmt deine Bestellung auf, geht zur Kaffeemaschine, bereitet den Cappuccino zu und bringt ihn dir zurück. Vielleicht sagt er dabei noch etwas wie „Hier, bitte schön, frisch gemacht“ und stellt die Tasse vor dich hin.

Genau dieser Dialog – eine klare Bitte und eine passende Antwort – ist das Herzstück der Kommunikation im World Wide Web. Nur dass hier nicht du und der Kellner miteinander sprechen, sondern dein Webbrowser (der Client) und ein Webserver. Die Sprache, die sie verwenden, nennt sich **HTTP**, das „Hypertext Transfer Protocol“. Jedes Mal, wenn du eine Webseite aufrufst, ein Bild lädst oder ein Formular abschickst, findet im Hintergrund ein solcher Dialog statt, bestehend aus einer HTTP-Anfrage (Request) und einer HTTP-Antwort (Response). Lass uns diesen Dialog einmal genauer unter die Lupe nehmen.

#### Die HTTP-Anfrage: Deine Bestellung ans Web

Deine Anfrage an einen Server ist keine formlose E-Mail, sondern eine streng strukturierte Nachricht. Sie besteht aus bis zu drei Teilen: der Startzeile, den Headern und einem optionalen Nachrichtenkörper.

##### 1. Die Startzeile (Request Line)

Die allererste Zeile einer Anfrage legt die drei wichtigsten Dinge fest: die Methode, die Ressource und die Protokollversion.

Ein Beispiel für eine Startzeile könnte so aussehen:

```http
GET /artikel/toller-beitrag.html HTTP/1.1
```

- **Methode:** Das erste Wort, hier `GET`, ist die HTTP-Methode. Sie beschreibt die Absicht deiner Anfrage. `GET` ist die mit Abstand häufigste Methode und bedeutet so viel wie: „Gib mir bitte die Daten für diese Ressource.“ Du verwendest sie jedes Mal, wenn du eine Webseite oder ein Bild abrufst. Eine andere wichtige Methode ist `POST`. Sie wird typischerweise verwendet, um Daten an den Server zu *senden*, zum Beispiel wenn du ein Kontaktformular ausfüllst oder dich auf einer Seite einloggst.
- **Ressource (URI):** Der zweite Teil, hier `/artikel/toller-beitrag.html`, ist der Pfad zur gewünschten Ressource auf dem Server. Man nennt dies den Uniform Resource Identifier (URI). Es ist quasi die genaue Angabe, *was* du vom Server haben möchtest.
- **Protokollversion:** Am Ende steht die verwendete HTTP-Version, meist `HTTP/1.1` oder `HTTP/2`. Dies teilt dem Server mit, nach welchen Regeln der „Dialog“ geführt werden soll.

##### 2. Die Header (Kopfzeilen)

Direkt nach der Startzeile folgen die Header. Das sind Schlüssel-Wert-Paare, die zusätzliche Informationen und Kontext zur Anfrage liefern – vergleichbar mit den Zusatzinformationen „mit Hafermilch“ bei deiner Kaffeebestellung. Jeder Header steht in einer eigenen Zeile.

Hier sind einige typische und wichtige Header einer Anfrage:

```http
Host: www.beispiel-akademie.de
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: de-DE,de;q=0.9,en-US;q=0.8,en;q=0.7
```

- **`Host`**: Dieser Header ist Pflicht. Er gibt den Domainnamen des Servers an, den du kontaktieren möchtest. Das ist wichtig, weil auf einer einzigen Server-IP-Adresse oft Hunderte von verschiedenen Webseiten gehostet werden. Der `Host`-Header sagt dem Server, für welche dieser Webseiten deine Anfrage bestimmt ist.
- **`User-Agent`**: Hier stellt sich dein Browser vor. Er teilt dem Server mit, welcher Browser in welcher Version auf welchem Betriebssystem läuft. Manchmal nutzen Server diese Information, um den Inhalt leicht anzupassen und für deinen Browser zu optimieren.
- **`Accept`**: Damit teilt dein Browser dem Server mit, welche Arten von Inhalten er versteht und bevorzugt. `text/html` sagt zum Beispiel: „Ich kann HTML-Seiten darstellen.“ `image/webp` signalisiert, dass der Browser auch moderne Bildformate verarbeiten kann.
- **`Accept-Language`**: Dieser Header informiert den Server über deine bevorzugte Sprache. Viele Webseiten nutzen diese Information, um dir automatisch die deutsche Version einer Seite auszuliefern, falls eine verfügbar ist.

##### 3. Der Nachrichtenkörper (Request Body)

Der Nachrichtenkörper ist ein optionaler Teil der Anfrage. Bei einer einfachen `GET`-Anfrage, mit der du nur Daten abrufen willst, gibt es keinen Body. Wenn du aber Daten an den Server sendest, zum Beispiel mit der `POST`-Methode, dann enthält der Body genau diese Daten. Wenn du ein Formular mit deinem Namen und deiner E-Mail-Adresse abschickst, könnten diese Informationen so im Body stehen:

```http
name=Max+Mustermann&email=max@beispiel.de
```

Dieser Teil ist also der eigentliche Inhalt, den du an den Server übermittelst.

#### Die HTTP-Antwort: Die Lieferung vom Server

Nachdem deine Anfrage beim Server eingegangen und verarbeitet wurde, schickt dieser eine Antwort zurück. Auch diese Antwort ist klar strukturiert und ähnelt in ihrem Aufbau der Anfrage. Sie besteht ebenfalls aus einer Statuszeile, Headern und meistens einem Nachrichtenkörper.

##### 1. Die Statuszeile (Status Line)

Die erste Zeile der Server-Antwort gibt dir eine schnelle Rückmeldung über das Ergebnis deiner Anfrage.

Ein Beispiel für eine erfolgreiche Antwort:

```http
HTTP/1.1 200 OK
```

- **Protokollversion:** Auch hier wird die verwendete HTTP-Version angegeben.
- **Statuscode:** Die Zahl `200` ist der Statuscode. Dies ist der wichtigste Teil der Statuszeile. Es ist ein dreistelliger Code, der den Erfolg oder Misserfolg der Anfrage signalisiert. Die Codes sind in Klassen eingeteilt:
    - **2xx (Erfolg):** Alles hat geklappt. `200 OK` ist der bekannteste Code und bedeutet, dass die Anfrage erfolgreich war und die Ressource geliefert wird.
    - **3xx (Umleitung):** Du wirst woanders hingeschickt. `301 Moved Permanently` teilt dem Browser mit, dass die angeforderte Ressource dauerhaft unter einer neuen Adresse zu finden ist.
    - **4xx (Client-Fehler):** Der Fehler liegt auf deiner Seite. Der berühmteste Code hier ist `404 Not Found`, der bedeutet, dass die angeforderte Ressource auf dem Server nicht existiert. `403 Forbidden` heißt, dass du keine Berechtigung hast, darauf zuzugreifen.
    - **5xx (Server-Fehler):** Der Fehler liegt auf der Seite des Servers. `500 Internal Server Error` ist ein allgemeiner Fehler, der signalisiert, dass auf dem Server etwas schiefgelaufen ist.
- **Statusmeldung:** `OK` ist eine kurze, für Menschen lesbare Beschreibung des Statuscodes.

##### 2. Die Header (Kopfzeilen)

Genau wie die Anfrage enthält auch die Antwort Header, die Metadaten über die Antwort selbst liefern.

Hier sind einige typische Antwort-Header:

```http
Date: Mon, 23 May 2023 22:38:34 GMT
Server: Apache/2.4.1 (Unix)
Content-Length: 5123
Content-Type: text/html; charset=UTF-8
```

- **`Date`**: Zeitstempel, wann die Antwort generiert wurde.
- **`Server`**: Informationen über die Software, die der Webserver verwendet (z.B. Apache, Nginx).
- **`Content-Length`**: Die Größe des Nachrichtenkörpers in Bytes. So weiß dein Browser, wie viele Daten er erwarten muss.
- **`Content-Type`**: Einer der wichtigsten Header. Er beschreibt die Art des Inhalts im Nachrichtenkörper. `text/html` sagt dem Browser, dass er jetzt ein HTML-Dokument empfängt und es als Webseite rendern soll. Bei einem Bild könnte hier `image/jpeg` stehen, bei einer CSS-Datei `text/css`. Der Zusatz `charset=UTF-8` gibt die Zeichenkodierung an, damit Umlaute und Sonderzeichen korrekt dargestellt werden.

##### 3. Der Nachrichtenkörper (Response Body)

Dies ist der Teil, auf den du gewartet hast: die eigentliche Ressource. Wenn du eine HTML-Seite angefordert hast, enthält der Body den vollständigen HTML-Quellcode dieser Seite. Wenn du ein Bild angefordert hast, enthält der Body die binären Daten des Bildes.

Für eine Anfrage nach einer Webseite sieht der Body also zum Beispiel so aus:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Meine Webseite</title>
</head>
<body>
    <h1>Willkommen!</h1>
    <p>Das ist der Inhalt, der vom Server geliefert wurde.</p>
</body>
</html>
```

Dein Browser empfängt diesen Text, erkennt dank des `Content-Type: text/html`-Headers, dass es sich um HTML handelt, und beginnt sofort damit, diesen Code zu interpretieren und die sichtbare Webseite für dich auf dem Bildschirm darzustellen.

#### Das große Ganze

Dieser Dialog aus Anfrage und Antwort ist das fundamentale Prinzip, auf dem das gesamte Web aufbaut. Er geschieht in Sekundenbruchteilen, unsichtbar für dich als Nutzer. Und er passiert nicht nur einmal pro Seitenaufruf. Die erste Anfrage holt das HTML-Dokument. Der Browser liest dieses Dokument und entdeckt darin vielleicht Verweise auf eine CSS-Datei, mehrere JavaScript-Dateien und ein Dutzend Bilder. Für jede einzelne dieser Dateien startet er eine neue HTTP-Anfrage an den Server, und für jede erhält er eine separate HTTP-Antwort. Eine moderne Webseite kann so leicht aus 50, 100 oder mehr solchen Dialogen bestehen.

Das Verständnis dieses einfachen, aber kraftvollen Mechanismus ist der Schlüssel zum Verständnis, wie das Web wirklich funktioniert. Es ist die Basis, auf der Technologien wie HTML, CSS und JavaScript überhaupt erst ihre Wirkung entfalten können. Jede HTML-Datei, die du schreibst, ist am Ende der Inhalt, der im Nachrichtenkörper einer HTTP-Antwort über das Netz transportiert wird, um im Browser eines Nutzers zum Leben erweckt zu werden.
