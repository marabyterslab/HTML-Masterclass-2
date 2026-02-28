# Komprimierung (Gzip/Brotli)

### Mehr als nur Minimierung: Die Kraft der Komprimierung mit Gzip und Brotli

Nachdem du deinen Code durch Minimierung von überflüssigen Zeichen befreit hast, ist es Zeit für den nächsten, entscheidenden Schritt in der Performance-Optimierung: die Komprimierung. Stell dir vor, du hast einen Text von allen unnötigen Leerzeichen und Kommentaren befreit. Der Text ist jetzt kürzer, aber die Wörter und Buchstaben sind immer noch dieselben. Komprimierung geht einen Schritt weiter. Sie ist wie ein digitaler Reißverschluss für deine Daten. Bevor der Server eine Datei, wie zum Beispiel dein HTML-, CSS- oder JavaScript-Dokument, an den Browser schickt, packt er sie in ein deutlich kleineres Paket. Der Browser empfängt dieses Paket, entpackt es blitzschnell und kann den Inhalt dann wie gewohnt verarbeiten.

Der ganze Prozess geschieht im Hintergrund, ist für den Nutzer unsichtbar und spart eine enorme Menge an Übertragungszeit. Kleinere Dateien bedeuten schnellere Downloads, eine geringere Belastung für mobile Datenvolumen und letztendlich eine Webseite, die sich spürbar schneller anfühlt.

Die grundlegende Idee hinter den meisten Komprimierungsalgorithmen ist das Erkennen und Ersetzen von Wiederholungen. Stell dir einen einfachen Satz vor: „Der schnelle braune Fuchs springt über den schnellen braunen Hund.“ Das Wort „schnellen“ und „braunen“ kommt zweimal vor. Anstatt diese Wörter komplett zu wiederholen, könnte ein Algorithmus sie beim zweiten Mal durch einen kurzen Verweis auf ihr erstes Vorkommen ersetzen. Das spart Platz. Moderne Algorithmen tun dies nicht auf Wort-, sondern auf Zeichen- und Byte-Ebene und sind dabei unglaublich effizient.

Im Webkontext gibt es zwei dominierende Komprimierungsalgorithmen, die du kennen musst: Gzip und Brotli.

#### Gzip: Der bewährte Klassiker

Gzip (GNU Zip) ist seit Jahrzehnten der De-facto-Standard für die Komprimierung von Webinhalten. Die Wahrscheinlichkeit ist hoch, dass du schon auf unzähligen Webseiten gesurft hast, die mit Gzip komprimierte Inhalte ausgeliefert haben, ohne es je zu bemerken. Gzip basiert auf dem DEFLATE-Algorithmus, einer cleveren Kombination aus LZ77 und Huffman-Kodierung.

Ohne zu tief in die Kryptografie einzutauchen, kannst du dir das so vorstellen:

1.  **LZ77** findet wiederholte Zeichenketten in den Daten und ersetzt sie durch einen Verweis (einen Pointer), der sagt: „Schau X Bytes zurück und kopiere Y Bytes von dort.“ Das ist extrem effektiv bei textbasierten Dateien wie HTML oder CSS, wo sich Klassennamen, Tags und Eigenschaften oft wiederholen.
2.  **Huffman-Kodierung** analysiert anschließend die verbleibenden Daten. Zeichen, die sehr häufig vorkommen (wie das Leerzeichen oder der Buchstabe ‚e‘), bekommen einen sehr kurzen Code, während seltene Zeichen (wie ‚q‘ oder ‚x‘) einen längeren Code erhalten. Das ist wie eine Art digitales Morse-Alphabet, das für die jeweilige Datei optimiert ist.

Die Kombination dieser beiden Techniken macht Gzip zu einem sehr robusten und schnellen Allrounder. Es bietet ein exzellentes Verhältnis von Komprimierungsrate zu Rechenaufwand. Fast jeder Webserver und Browser auf diesem Planeten unterstützt Gzip, was es zu einer absolut sicheren Wahl macht. Die Komprimierung von Textdateien kann ihre Größe oft um 70 % bis 80 % reduzieren – ein gewaltiger Gewinn mit minimalem Aufwand.

Wichtig zu verstehen ist, dass Gzip bei bereits komprimierten Dateiformaten wie Bildern (JPEG, PNG) oder Videos (MP4) kaum oder gar keine Wirkung hat. Diese Formate haben ihre eigenen, hochspezialisierten Komprimierungsverfahren. Der Versuch, eine JPEG-Datei mit Gzip zu komprimieren, kann sie im schlimmsten Fall sogar geringfügig größer machen. Daher wird die Komprimierung gezielt nur auf textbasierte Ressourcen angewendet: HTML, CSS, JavaScript, SVG, JSON und Schriftarten.

#### Brotli: Der moderne Herausforderer

Brotli ist ein von Google entwickelter, modernerer Komprimierungsalgorithmus. Er wurde speziell mit dem Ziel entworfen, die Komprimierungsraten im Web weiter zu verbessern, und das gelingt ihm auch eindrucksvoll. In den meisten Fällen kann Brotli Dateien noch einmal deutlich kleiner machen als Gzip – oft um zusätzliche 15 % bis 25 %.

Was macht Brotli so viel besser? Der entscheidende Vorteil von Brotli ist sein statisches Wörterbuch. Während Gzip sein Wörterbuch für Wiederholungen ausschließlich aus der zu komprimierenden Datei selbst erstellen muss, bringt Brotli ein riesiges, vordefiniertes Wörterbuch mit. Dieses Wörterbuch enthält über 13.000 gängige Wörter, Phrasen und Code-Schnipsel aus einer riesigen Analyse von Texten und HTML-Code aus dem gesamten Internet.

Das gibt Brotli einen gewaltigen Vorsprung. Wenn es in deinem HTML-Code auf den Tag `<div class="` oder in deinem CSS auf die Eigenschaft `background-color:` stößt, muss es nicht erst auf eine Wiederholung warten. Es kann diese häufigen Muster sofort durch einen sehr kurzen Code aus seinem internen Wörterbuch ersetzen.

Der Nachteil? Die Komprimierung mit Brotli auf dem Server kann – je nach Komprimierungslevel – etwas länger dauern als mit Gzip. Der Server muss mehr Arbeit investieren, um die optimale Komprimierung zu finden. Aber das ist ein Trade-off, der sich lohnt. Die Komprimierung geschieht nur einmal auf dem Server (und das Ergebnis wird oft zwischengespeichert), während Tausende von Nutzern von der kleineren Dateigröße profitieren. Noch wichtiger ist, dass die Dekomprimierung im Browser, also das Entpacken der Datei, bei Brotli extrem schnell ist, oft sogar schneller als bei Gzip. Für die wahrgenommene Ladezeit beim Nutzer ist Brotli also ein klarer Gewinn.

Mittlerweile unterstützen alle modernen Browser Brotli, sodass es heute die bevorzugte Methode ist, wenn dein Server sie anbietet.

#### Wie alles zusammenspielt: Der Content-Negotiation-Tanz

Du fragst dich vielleicht, woher der Server weiß, welche Komprimierungsmethode er verwenden soll. Kann der Browser des Nutzers überhaupt Brotli? Was passiert, wenn nicht?

Hier kommt ein eleganter Mechanismus namens „Content Negotiation“ ins Spiel. Es ist ein kleiner Dialog zwischen Browser und Server:

1.  **Der Browser fragt an:** Jedes Mal, wenn dein Browser eine Ressource von einem Server anfordert, schickt er eine Liste von Dingen mit, die er versteht. Dies geschieht im `Accept-Encoding`-HTTP-Header. Ein moderner Browser sendet hier typischerweise etwas wie: `Accept-Encoding: gzip, deflate, br`. Damit teilt er dem Server mit: „Hallo, ich kann Gzip, Deflate (ein älterer Algorithmus) und Brotli (br) verstehen.“
2.  **Der Server antwortet:** Der Server schaut sich diese Liste an. Wenn er für die angeforderte Datei eine mit Brotli komprimierte Version hat und sieht, dass der Browser `br` unterstützt, schickt er diese Version. In seiner Antwort fügt er den `Content-Encoding: br`-HTTP-Header hinzu. Damit sagt er: „Hier ist die Datei. Achtung, sie ist mit Brotli komprimiert.“
3.  **Fallback:** Wenn der Server kein Brotli unterstützt oder keine Brotli-Version der Datei hat, prüft er die nächste Option: Gzip. Wenn er Gzip unterstützt und der Browser es auch tut, sendet er die Gzip-Version mit dem Header `Content-Encoding: gzip`.
4.  **Keine Komprimierung:** Wenn keine gemeinsame Methode gefunden wird (was heute extrem selten ist), schickt der Server die Datei unkomprimiert.

Dieser Prozess stellt sicher, dass immer die bestmögliche Komprimierung verwendet wird, die von beiden Seiten unterstützt wird, ohne dass ältere Browser ausgeschlossen werden.

#### Aktivierung auf dem Server

Die Aktivierung der Komprimierung ist in der Regel eine Sache der Serverkonfiguration. Du musst sie also nicht in deinem HTML- oder CSS-Code einstellen. Die genauen Schritte hängen von deinem Hosting-Anbieter und der Server-Software ab. Bei vielen modernen Hosting-Plattformen und Content Delivery Networks (CDNs) ist die Komprimierung bereits standardmäßig aktiviert oder kann mit einem einzigen Klick im Kontrollpanel eingeschaltet werden.

Falls du deinen eigenen Server verwaltest, sind hier beispielhafte Konfigurationen für die beiden gängigsten Webserver, Apache und Nginx.

**Beispiel für Apache (.htaccess):**

Für Apache benötigst du die Module `mod_deflate` (für Gzip) und optional `mod_brotli`.

```apache
# Gzip-Komprimierung aktivieren
<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css text/javascript application/javascript application/json application/x-javascript application/xml application/rss+xml image/svg+xml
</IfModule>

# Brotli-Komprimierung aktivieren (hat Vorrang vor Gzip, wenn der Browser es unterstützt)
<IfModule mod_brotli.c>
  AddOutputFilterByType BROTLI_COMPRESS text/html text/plain text/xml text/css text/javascript application/javascript application/json application/x-javascript application/xml application/rss+xml image/svg+xml
</IfModule>
```

**Beispiel für Nginx (nginx.conf):**

In Nginx werden die Einstellungen direkt in der Konfigurationsdatei vorgenommen.

```nginx
# Gzip-Komprimierung
gzip on;
gzip_vary on;
gzip_proxied any;
gzip_comp_level 6;
gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript image/svg+xml;

# Brotli-Komprimierung
brotli on;
brotli_comp_level 6;
brotli_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript image/svg+xml;
```

#### Überprüfung in den Entwicklertools

Ob deine Webseite erfolgreich komprimiert ausgeliefert wird, kannst du ganz einfach selbst überprüfen.

1.  Öffne deine Webseite in einem Browser wie Chrome oder Firefox.
2.  Öffne die Entwicklertools (meist mit der Taste `F12` oder per Rechtsklick -> „Untersuchen“).
3.  Wechsle zum Tab „Netzwerk“ (oder „Network“).
4.  Lade die Seite neu (mit `Strg + R` oder `Cmd + R`), um den Netzwerkverkehr aufzuzeichnen.
5.  Klicke auf eine deiner Dateien, zum Beispiel das Haupt-HTML-Dokument oder eine CSS-Datei.
6.  In der Detailansicht, die sich öffnet, suche nach den „Antwort-Headern“ (Response Headers).

Dort solltest du einen Eintrag wie `Content-Encoding: br` oder `Content-Encoding: gzip` finden. Das ist der Beweis, dass die Komprimierung aktiv ist. Oft zeigen die Entwicklertools auch zwei verschiedene Größen an: die übertragene Größe (Transferred Size) und die tatsächliche Größe (Resource Size). Die übertragene Größe wird deutlich kleiner sein – das ist deine Ersparnis durch die Komprimierung.

Komprimierung ist kein optionales Extra, sondern eine fundamentale Technik für moderne Web-Performance. Sie arbeitet Hand in Hand mit der Minimierung, um die Dateigrößen drastisch zu reduzieren und deine Webseite für jeden Besucher schneller zu machen.
