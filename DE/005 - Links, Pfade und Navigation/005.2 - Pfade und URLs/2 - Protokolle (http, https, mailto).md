# Protokolle (http, https, mailto)

### Protokolle: Die unsichtbaren Regeln hinter http, https und mailto

Wenn du eine Webadresse, eine URL, betrachtest, ist der allererste Teil davon oft so selbstverständlich, dass du ihn kaum noch wahrnimmst: das Protokoll. Es ist der Teil, der mit `://` endet, wie zum Beispiel `http://` oder `https://`. Dieses kleine Präfix ist jedoch von entscheidender Bedeutung, denn es legt die fundamentalen Regeln fest, nach denen dein Browser mit einem Server kommunizieren soll. Stell es dir wie die Wahl einer Sprache vor, bevor du ein Gespräch beginnst. Sprichst du Deutsch, Englisch oder Gebärdensprache? Das Protokoll ist die vereinbarte „Sprache“ für den Datenaustausch im Web.

In diesem Kapitel tauchen wir in die drei Protokolle ein, denen du beim Erstellen von Links in HTML am häufigsten begegnen wirst: HTTP, sein sicherer Nachfolger HTTPS und das spezialisierte Protokoll `mailto` für E-Mail-Links.

#### HTTP: Das Arbeitspferd des Webs

Das Kürzel HTTP steht für **Hypertext Transfer Protocol**. Lass uns diesen Namen einmal auseinandernehmen, um zu verstehen, was er bedeutet:

*   **Hypertext:** Das ist im Grunde der Text, aus dem das Web besteht – Text, der Links (Hyperlinks) zu anderen Dokumenten enthalten kann. Jede Webseite, die du besuchst, ist ein Hypertext-Dokument.
*   **Transfer:** Das bedeutet schlicht „Übertragung“. Es geht darum, Daten von einem Ort zum anderen zu bewegen.
*   **Protocol:** Das ist ein Satz von Regeln und Konventionen, die festlegen, wie die Kommunikation abzulaufen hat.

Zusammengesetzt beschreibt HTTP also die Regeln für die Übertragung von Webseiten und deren Bestandteilen (wie Bilder, CSS-Dateien und Skripte) über das Internet.

Die Kommunikation via HTTP folgt einem einfachen Prinzip: dem Anfrage-Antwort-Modell (Request-Response).

1.  **Die Anfrage (Request):** Dein Browser (der Client) sendet eine Anfrage an einen Webserver. Diese Anfrage sagt im Wesentlichen: „Hallo Server, ich hätte gerne die Ressource unter der Adresse `/ueber-uns.html`“.
2.  **Die Antwort (Response):** Der Server empfängt die Anfrage, sucht die angeforderte Datei und schickt sie zusammen mit einem Statuscode zurück. Ein bekannter Statuscode ist `200 OK` (alles in Ordnung, hier sind die Daten) oder der berüchtigte `404 Not Found` (ich konnte die angeforderte Ressource nicht finden).

HTTP ist „zustandslos“ (stateless). Das bedeutet, der Server merkt sich standardmäßig nichts über deine vorherigen Anfragen. Jede Anfrage wird so behandelt, als wäre es die erste. Das macht das Protokoll sehr robust und einfach, aber es erfordert zusätzliche Techniken wie Cookies, um zum Beispiel einen Warenkorb über mehrere Seiten hinweg zu erhalten.

Ein Link, der das HTTP-Protokoll verwendet, sieht in deinem HTML-Code so aus:

```html
<a href="http://beispiel-webseite.de/blog/artikel-1">Lies unseren neuesten Artikel</a>
```

Wenn ein Nutzer auf diesen Link klickt, weist das `http://` den Browser an, eine unverschlüsselte Anfrage an den Server `beispiel-webseite.de` zu senden, um die Ressource unter dem Pfad `/blog/artikel-1` abzurufen. Heute wirst du reines HTTP jedoch immer seltener antreffen, denn es hat eine entscheidende Schwäche: die fehlende Sicherheit.

#### HTTPS: Die sichere Verbindung

Stell dir vor, du schickst eine Postkarte. Jeder, der sie auf dem Weg in die Hände bekommt – der Postbote, die Mitarbeiter im Sortierzentrum – kann sie lesen. Genau so funktioniert die Kommunikation über HTTP. Daten wie Passwörter, Kreditkartennummern oder persönliche Nachrichten werden im Klartext übertragen und können von Angreifern im selben Netzwerk mitgelesen werden.

Hier kommt HTTPS ins Spiel. Das „S“ am Ende steht für **Secure** (sicher). HTTPS ist im Grunde dasselbe Protokoll wie HTTP, aber mit einer zusätzlichen Sicherheitsschicht: **SSL/TLS** (Secure Sockets Layer / Transport Layer Security). Diese Schicht sorgt für drei entscheidende Sicherheitsmerkmale:

1.  **Verschlüsselung:** Die Daten, die zwischen deinem Browser und dem Server ausgetauscht werden, sind verschlüsselt. Anstatt einer lesbaren Postkarte schickst du nun einen versiegelten, unentzifferbaren Brief. Selbst wenn jemand die Daten abfängt, kann er damit nichts anfangen, da ihm der Schlüssel zur Entschlüsselung fehlt.
2.  **Authentifizierung:** HTTPS stellt sicher, dass du wirklich mit dem Server sprichst, mit dem du sprechen möchtest. Durch ein sogenanntes SSL/TLS-Zertifikat kann der Server seine Identität beweisen. Das verhindert, dass sich Angreifer als deine Bank oder dein Lieblings-Onlineshop ausgeben, um deine Daten abzugreifen (sogenannte Man-in-the-Middle-Angriffe).
3.  **Integrität:** Das Protokoll gewährleistet, dass die Daten während der Übertragung nicht unbemerkt verändert wurden. Es wird eine Art digitale Prüfsumme erstellt. Kommen die Daten beim Empfänger mit einer anderen Prüfsumme an, wird die Verbindung als kompromittiert erkannt.

Früher war HTTPS hauptsächlich für Online-Banking und E-Commerce-Seiten reserviert. Heute ist es der De-facto-Standard für das gesamte Web. Moderne Browser wie Chrome oder Firefox markieren Webseiten, die noch über HTTP laufen, explizit als „nicht sicher“. Suchmaschinen wie Google bevorzugen HTTPS-Seiten in ihren Suchergebnissen. Es gibt also keinen guten Grund mehr, auf die sichere Variante zu verzichten.

Ein Link, der HTTPS verwendet, ist im HTML-Code kaum von seinem unsicheren Gegenstück zu unterscheiden:

```html
<a href="https://dein-sicherer-onlineshop.de/warenkorb">Zum Warenkorb</a>
```

Für dich als Entwickler bedeutet das: Verwende wann immer möglich `https://`. Wenn du auf externe Ressourcen verlinkst, wähle immer die HTTPS-Variante der URL, falls eine verfügbar ist.

#### Mailto: Der direkte Draht zum E-Mail-Programm

Während HTTP und HTTPS dazu dienen, Ressourcen von einem Server abzurufen und im Browser darzustellen, verfolgt das `mailto`-Protokoll einen völlig anderen Zweck. Es interagiert nicht mit einem Webserver, sondern mit einer Anwendung auf dem Computer des Nutzers: dem standardmäßig eingerichteten E-Mail-Programm (z. B. Outlook, Apple Mail, Thunderbird).

Ein `mailto`-Link ist eine einfache und effektive Möglichkeit, deinen Besuchern die Kontaktaufnahme per E-Mail zu ermöglichen. Klickt ein Nutzer auf einen solchen Link, öffnet sich ein neues E-Mail-Fenster, in dem die Empfängeradresse bereits ausgefüllt ist.

Die einfachste Form eines `mailto`-Links sieht so aus:

```html
<a href="mailto:kontakt@meine-firma.de">Schreib uns eine E-Mail!</a>
```

Das ist aber noch nicht alles. Du kannst den Link mit zusätzlichen Parametern anreichern, um dem Nutzer noch mehr Arbeit abzunehmen. Diese Parameter werden wie bei URLs mit einem Fragezeichen (`?`) eingeleitet und mit einem Und-Zeichen (`&`) voneinander getrennt.

**Betreff vorab ausfüllen (`subject`)**

Du kannst einen Standardbetreff für die E-Mail festlegen. Das hilft dir, E-Mails, die über deine Webseite kommen, besser zuzuordnen.

```html
<a href="mailto:support@meine-firma.de?subject=Supportanfrage von der Webseite">Kontaktiere den Support</a>
```

**Textkörper vorab ausfüllen (`body`)**

Du kannst sogar schon einen Teil des E-Mail-Textes vorgeben, zum Beispiel eine kurze Begrüßung oder eine Vorlage für eine Anfrage.

```html
<a href="mailto:info@meine-firma.de?subject=Anfrage für ein Angebot&body=Hallo, ich hätte gerne weitere Informationen zu...">Fordere ein Angebot an</a>
```

**Weitere Empfänger hinzufügen (`cc` und `bcc`)**

Du kannst auch Empfänger für eine Kopie (CC) oder eine Blindkopie (BCC) festlegen.

```html
<a href="mailto:projekt@meine-firma.de?cc=chef@meine-firma.de&subject=Neues Projekt">Projektvorschlag senden</a>
```

**Wichtiger Hinweis zur Formatierung:**
In URLs und somit auch in `mailto`-Links dürfen keine Leerzeichen oder Zeilenumbrüche vorkommen. Diese müssen speziell kodiert werden. Ein Leerzeichen wird zu `%20` und ein Zeilenumbruch (um Text im `body` auf mehrere Zeilen zu verteilen) wird zu `%0A`.

Hier ist ein komplexes Beispiel, das alles kombiniert:

```html
<a href="mailto:info@beispiel-event.de?subject=Anmeldung%20zum%20Workshop&body=Hiermit%20melde%20ich%20mich%20verbindlich%20an.%0A%0AMein%20Name:%20%0AMeine%20Adresse:%20">Jetzt für den Workshop anmelden</a>
```

Dieser Link öffnet eine E-Mail an `info@beispiel-event.de` mit dem Betreff „Anmeldung zum Workshop“. Der Textkörper enthält bereits den Satz „Hiermit melde ich mich verbindlich an.“ gefolgt von zwei neuen Zeilen und Vorlagen für den Namen und die Adresse.

Beachte bei `mailto`-Links jedoch immer, dass ihr Erfolg davon abhängt, ob der Nutzer ein E-Mail-Programm auf seinem System installiert und konfiguriert hat. Bei Nutzern, die ausschließlich Webmail-Dienste (wie Gmail oder GMX) im Browser verwenden, funktioniert ein `mailto`-Link möglicherweise nicht wie erwartet oder gar nicht, es sei denn, der Browser wurde entsprechend konfiguriert. Dennoch ist es eine weitverbreitete und nützliche Methode für Kontaktmöglichkeiten.
