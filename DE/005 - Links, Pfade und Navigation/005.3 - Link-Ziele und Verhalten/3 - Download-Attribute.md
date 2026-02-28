# Download-Attribute

### Das `download`-Attribut: Dateien zum Herunterladen anbieten

In den meisten Fällen, wenn du einen Link (`<a>`-Element) erstellst, erwartest du ein ganz bestimmtes Verhalten: Ein Klick darauf soll den Nutzer zu einer anderen Webseite oder einem anderen Abschnitt auf derselben Seite navigieren. Doch was ist, wenn das Ziel des Links gar keine Webseite ist, die im Browser angezeigt werden soll, sondern eine Datei, die der Nutzer direkt auf seinem Computer speichern soll?

Stell dir den klassischen Anwendungsfall vor: Du bietest auf deiner Webseite ein PDF-Dokument an. Ein Lebenslauf, eine Broschüre oder ein technisches Datenblatt. Klickt ein Nutzer auf einen normalen Link, der auf dieses PDF verweist, passiert meistens eines von zwei Dingen: Entweder der Browser navigiert von deiner Seite weg und zeigt das PDF in seinem integrierten PDF-Viewer im selben Tab an, oder er öffnet es in einem neuen Tab. In beiden Fällen hat der Nutzer deine Webseite verlassen, um sich den Inhalt anzusehen. Oft ist das aber gar nicht das, was du möchtest. Du willst, dass der Nutzer die Datei direkt auf seinem Computer speichert, ohne deine Seite zu verlassen.

Genau hier kommt das `download`-Attribut ins Spiel. Es ist ein einfaches, aber extrem nützliches boolesches Attribut für das `<a>`-Element, das dem Browser eine klare Anweisung gibt: „Behandle das Ziel dieses Links nicht als Navigationsziel, sondern als Datei zum Herunterladen.“

#### Die grundlegende Anwendung

In seiner einfachsten Form fügst du das `download`-Attribut einfach ohne Wert zum `<a>`-Tag hinzu.

```html
<a href="/dokumente/quartalsbericht-q3.pdf" download>
  Quartalsbericht Q3 herunterladen (PDF)
</a>
```

Wenn ein Nutzer nun auf diesen Link klickt, wird der Browser das PDF nicht mehr im Fenster anzeigen. Stattdessen öffnet sich der bekannte „Datei speichern unter…“-Dialog des Betriebssystems, und der Nutzer kann die Datei direkt in einem Ordner seiner Wahl ablegen. Der ursprüngliche Dateiname (`quartalsbericht-q3.pdf`) wird dabei als Vorschlag im Speicherdialog verwendet. Das ist schon ein gewaltiger Unterschied in der Nutzererfahrung. Der Nutzer bleibt auf deiner Seite und erhält die Datei, wie von dir beabsichtigt.

Dieses Verhalten ist nicht auf PDFs beschränkt. Es funktioniert mit allen Dateitypen, die ein Browser potenziell selbst darstellen könnte:

*   **Bilder:** Normalerweise würde ein Link zu einer `.jpg`- oder `.png`-Datei das Bild direkt im Browser anzeigen. Mit `download` wird es stattdessen heruntergeladen.
*   **Textdateien:** Eine `.txt`- oder `.html`-Datei wird ebenfalls zum Download angeboten, anstatt sie als reinen Text oder gerenderte Seite darzustellen.
*   **Mediendateien:** Auch Video- oder Audiodateien (`.mp4`, `.mp3`), die der Browser abspielen könnte, werden zum Speichern angeboten.

Für Dateitypen, die der Browser ohnehin nicht versteht, wie zum Beispiel `.zip`-Archive oder `.exe`-Dateien, ist das `download`-Attribut streng genommen nicht immer notwendig, da der Browser hier von sich aus meist einen Download anstößt. Es schadet jedoch nicht, das Attribut aus Gründen der Klarheit und Konsistenz trotzdem zu verwenden. So stellst du sicher, dass das Verhalten über alle Browser hinweg einheitlich ist.

#### Einen benutzerdefinierten Dateinamen vorschlagen

Eine noch mächtigere Funktion des `download`-Attributs zeigt sich, wenn du ihm einen Wert zuweist. Der Wert, den du dem Attribut gibst, wird dem Nutzer als neuer Dateiname vorgeschlagen.

Stell dir vor, deine Dateien auf dem Server haben aus technischen Gründen kryptische oder sehr lange Namen, zum Beispiel durch eine Datenbank-ID oder einen Zeitstempel. Ein Dateiname wie `doc_id_83749_v4_final_rev2.pdf` ist für den Endnutzer alles andere als schön. Hier kannst du Abhilfe schaffen:

```html
<a href="/files/doc_id_83749_v4_final_rev2.pdf" download="Jahresbericht-Marketing-2023.pdf">
  Jahresbericht Marketing 2023 herunterladen
</a>
```

Wenn der Nutzer auf diesen Link klickt, öffnet sich der Speicherdialog mit dem sauberen und verständlichen Dateinamen `Jahresbericht-Marketing-2023.pdf`. Der ursprüngliche, unschöne Dateiname bleibt für den Nutzer komplett verborgen. Dies ist eine fantastische Möglichkeit, die Nutzererfahrung zu verbessern und für Ordnung auf den Festplatten deiner Besucher zu sorgen.

Du kannst diese Technik auch nutzen, um die Dateiendung zu ändern, obwohl das nur in seltenen Fällen sinnvoll ist. Der Browser orientiert sich am `Content-Type`-Header des Servers, um den tatsächlichen Dateityp zu bestimmen, aber der vorgeschlagene Name kann angepasst werden.

#### Wichtige Einschränkungen: Die Same-Origin-Policy

Das `download`-Attribut ist ein mächtiges Werkzeug, unterliegt aber aus Sicherheitsgründen einer entscheidenden Einschränkung: der **Same-Origin-Policy**. Das bedeutet, das Attribut funktioniert zuverlässig nur dann, wenn die Datei, auf die der Link verweist, von derselben Herkunft (Origin) stammt wie die Webseite, auf der sich der Link befindet.

Eine "Herkunft" ist eine Kombination aus Protokoll (z.B. `https`), Hostname (z.B. `www.deine-webseite.de`) und Port (z.B. `:80` oder `:443`).

*   **Funktioniert:** Ein Link auf `https://www.deine-webseite.de` verweist auf eine Datei unter `https://www.deine-webseite.de/dateien/bild.jpg`.
*   **Funktioniert nicht:** Ein Link auf `https://www.deine-webseite.de` verweist auf eine Datei unter `https://cdn.example.com/dateien/bild.jpg`.

Wenn du versuchst, das `download`-Attribut für eine sogenannte *Cross-Origin*-Ressource (also eine Datei auf einer anderen Domain) zu verwenden, wird der Browser das Attribut in der Regel ignorieren. Der Link wird sich dann wie ein normaler Link verhalten – er navigiert den Nutzer zur Ressource, anstatt einen Download auszulösen.

Warum diese Einschränkung? Stell dir eine bösartige Webseite vor. Sie könnte einen Link platzieren, der aussieht wie „Lade unser süßes Katzenbild herunter“, aber in Wirklichkeit auf eine wichtige, private Datei auf einer anderen Webseite verweist, bei der du vielleicht gerade eingeloggt bist (z.B. `https://deine-bank.de/kontouebersicht.pdf`). Ohne die Same-Origin-Policy könnte die bösartige Seite den Download dieser Datei unter einem harmlosen Namen (`katzenbild.jpg`) auslösen und dich so zum Herunterladen sensibler Daten verleiten, ohne dass du die ursprüngliche URL siehst. Die Browsersicherheit verhindert dieses Szenario, indem sie die Kontrolle über das Download-Verhalten bei der Ziel-Domain belässt.

#### Die serverseitige Alternative: `Content-Disposition`

Wenn du eine Datei von einer anderen Domain zum Download anbieten musst (z.B. von einem Content Delivery Network, CDN), gibt es eine serverseitige Lösung. Der Server, der die Datei ausliefert, kann einen speziellen HTTP-Header mitsenden: den `Content-Disposition`-Header.

Wenn der Server die Datei mit dem folgenden Header ausliefert, weist er den Browser an, einen Download zu starten, unabhängig davon, ob das `download`-Attribut im HTML-Link vorhanden ist:

`Content-Disposition: attachment; filename="gewuenschter-dateiname.zip"`

Dieser Header hat Vorrang vor dem clientseitigen `download`-Attribut. Er ist der robusteste Weg, einen Download zu erzwingen, erfordert aber Zugriff auf die Konfiguration des Webservers. Das `download`-Attribut im HTML ist dagegen die perfekte Lösung, wenn du keine Kontrolle über den Server hast oder einfach nur eine schnelle, unkomplizierte clientseitige Lösung für deine eigenen Dateien benötigst.

#### Dynamische Downloads mit Data-URLs

Eine besonders interessante Anwendung des `download`-Attributs ergibt sich im Zusammenspiel mit JavaScript und Data-URLs. Eine Data-URL ermöglicht es, Daten direkt im `href`-Attribut zu kodieren, anstatt auf eine externe Ressource zu verweisen.

Du könntest zum Beispiel dynamisch im Browser eine Textdatei erstellen und sie dem Nutzer zum Download anbieten, ohne dass jemals eine Kommunikation mit dem Server stattfindet.

```html
<a id="download-link" href="data:text/plain;charset=utf-8,Hallo Welt! Dies ist eine dynamisch erstellte Textdatei." download="notiz.txt">
  Notiz herunterladen
</a>
```

Ein Klick auf diesen Link lädt eine Datei namens `notiz.txt` herunter, deren Inhalt „Hallo Welt! Dies ist eine dynamisch erstellte Textdatei.“ ist. Das ist extrem nützlich für Webanwendungen, bei denen Nutzer Daten generieren (z.B. Konfigurationen, Exporte, Berichte) und diese als Datei speichern möchten. Mit JavaScript kannst du den Inhalt der Data-URL und den Wert des `download`-Attributs zur Laufzeit erzeugen und dem Nutzer so eine vollständig clientseitige Exportfunktion bieten.

Das `download`-Attribut ist somit weit mehr als nur eine kleine Bequemlichkeit. Es ist ein fundamentales Werkzeug zur Steuerung der Nutzererfahrung, das den Unterschied zwischen einer verwirrenden Navigation und einem klaren, zielgerichteten Dateidownload ausmacht.
