# Cross-Site-Request-Forgery (CSRF)

### Cross-Site-Request-Forgery (CSRF): Wenn deine Formulare fremdgesteuert werden

Stell dir vor, du bist auf deiner Lieblings-Social-Media-Plattform angemeldet. Du liest gerade Kommentare, als du eine E-Mail von einem Freund mit einem Link zu einem lustigen Katzenvideo erhältst. Du klickst darauf, schaust dir das Video an, lachst und kehrst dann zu deinem Social-Media-Profil zurück. Plötzlich stellst du fest, dass deine E-Mail-Adresse in den Profileinstellungen geändert wurde. Du hast das aber nie getan. Was ist passiert? Du bist möglicherweise Opfer eines Cross-Site-Request-Forgery-Angriffs geworden.

Dieser Angriff ist raffiniert, weil er nicht dich direkt angreift, sondern das Vertrauen ausnutzt, das eine Website in dich – oder genauer gesagt, in deinen Browser – hat. Lass uns das Schritt für Schritt aufschlüsseln.

#### Was ist eine Request Forgery?

Der Name klingt kompliziert, aber die Idee dahinter ist recht einfach zu verstehen.

*   **Cross-Site**: Der Angriff wird von einer anderen Website (z. B. der mit dem Katzenvideo) aus initiiert als die, auf der die Aktion ausgeführt werden soll (deine Social-Media-Plattform).
*   **Request**: Es geht um eine HTTP-Anfrage, wie sie dein Browser ständig sendet, zum Beispiel wenn du ein Formular abschickst.
*   **Forgery**: Das bedeutet "Fälschung". Der Request, der an die Social-Media-Plattform gesendet wird, ist gefälscht. Er stammt nicht von einer bewussten Handlung von dir, sondern wurde dir untergeschoben.

Im Kern zielt ein CSRF-Angriff darauf ab, dich dazu zu bringen, eine ungewollte Aktion auf einer Website auszuführen, auf der du gerade angemeldet bist. Der Angreifer zwingt deinen Browser, eine Anfrage an diese Website zu senden, und die Website denkt, diese Anfrage käme von dir.

#### Wie funktioniert der Angriff im Detail?

Um CSRF zu verstehen, müssen wir uns an eine grundlegende Eigenschaft des Webs erinnern: Cookies. Wenn du dich auf einer Website anmeldest, speichert diese oft ein sogenanntes Session-Cookie in deinem Browser. Dieses Cookie ist wie ein digitaler Ausweis. Jedes Mal, wenn dein Browser eine Anfrage an diese Website schickt (z. B. um dein Profil zu laden), sendet er dieses Cookie automatisch mit. Der Server erkennt das Cookie, weiß "Ah, das ist der angemeldete Nutzer" und gewährt den Zugriff.

Genau hier liegt der Knackpunkt: Dein Browser ist sehr pflichtbewusst. Er sendet die Cookies für eine Domain (`meine-plattform.de`) bei *jeder* Anfrage an diese Domain mit, ganz egal, von wo aus diese Anfrage gestartet wurde.

Sehen wir uns unser Beispiel von vorhin genauer an:

1.  **Du bist angemeldet**: Du bist auf `meine-soziale-plattform.de` eingeloggt. Dein Browser hat ein gültiges Session-Cookie für diese Domain.

2.  **Du besuchst die bösartige Seite**: Du klickst auf den Link und landest auf `lustige-katzenvideos.com`. Der Angreifer hat diese Seite präpariert.

3.  **Der versteckte Angriff**: Auf dieser Seite befindet sich ein unsichtbares Formular. Es ist so gestaltet, dass es exakt dem Formular zum Ändern der E-Mail-Adresse auf `meine-soziale-plattform.de` entspricht.

    ```html
    <!-- Versteckt auf lustige-katzenvideos.com -->
    <form id="csrf-form" action="https://meine-soziale-plattform.de/einstellungen/email-aendern" method="POST" style="display:none;">
      <input type="email" name="neue_email" value="hacker@beispiel.com">
      <input type="submit" value="Speichern">
    </form>
    ```

4.  **Die automatische Ausführung**: Ein kleines JavaScript auf der Angreiferseite sorgt dafür, dass dieses Formular sofort abgeschickt wird, sobald du die Seite lädst.

    ```javascript
    // Dieses Skript läuft auf lustige-katzenvideos.com
    window.onload = function() {
      document.getElementById('csrf-form').submit();
    };
    ```

5.  **Der Browser gehorcht**: Dein Browser sieht die Anweisung, das Formular abzuschicken. Er erstellt eine POST-Anfrage an `https://meine-soziale-plattform.de/einstellungen/email-aendern`. Und jetzt kommt der entscheidende Teil: Weil die Anfrage an `meine-soziale-plattform.de` gerichtet ist, hängt der Browser automatisch dein gültiges Session-Cookie an diese Anfrage an.

6.  **Der Server wird getäuscht**: Der Server von `meine-soziale-plattform.de` empfängt die Anfrage. Er sieht eine gültige Anfrage zum Ändern der E-Mail-Adresse, und er sieht ein gültiges Session-Cookie. Für den Server sieht alles legitim aus. Er hat keine Möglichkeit zu wissen, dass diese Anfrage nicht von dir durch einen Klick auf seiner eigenen Seite, sondern von einer fremden Website ausgelöst wurde. Er ändert die E-Mail-Adresse auf `hacker@beispiel.com`.

Der Angriff war erfolgreich, ohne dass du etwas davon mitbekommen hast, während du ein Katzenvideo angesehen hast. Betroffen sind vor allem Aktionen, die einen Zustand auf dem Server verändern (sogenannte *state-changing operations*), wie das Ändern von Daten, das Löschen eines Accounts, das Senden einer Nachricht oder das Überweisen von Geld.

### Wie du deine Formulare schützt

Glücklicherweise gibt es sehr wirksame Methoden, um CSRF-Angriffe zu verhindern. Die Verantwortung dafür liegt bei dir als Entwickler der Website.

#### Der Synchronizer-Token-Ansatz (CSRF-Token)

Dies ist die gängigste und sicherste Methode. Die Idee ist, jeder Anfrage eine Art "geheime Zutat" hinzuzufügen, die ein Angreifer nicht kennen kann. Diese geheime Zutat ist ein sogenanntes CSRF-Token.

So funktioniert es:

1.  **Token-Erzeugung**: Wenn der Server eine Seite mit einem Formular an dich sendet, erzeugt er ein einzigartiges, zufälliges und schwer zu erratendes Token. Dieses Token wird auf dem Server in deiner Session gespeichert.

2.  **Token im Formular einbetten**: Das gleiche Token wird in das HTML-Formular als verstecktes Feld eingefügt.

    ```html
    <form action="/einstellungen/email-aendern" method="POST">
      <label for="email">Neue E-Mail-Adresse:</label>
      <input type="email" id="email" name="neue_email">

      <!-- Das ist das geheime CSRF-Token -->
      <input type="hidden" name="csrf_token" value="a1b2c3d4-e5f6-7890-g1h2-i3j4k5l6m7n8">

      <button type="submit">Speichern</button>
    </form>
    ```

3.  **Überprüfung bei der Verarbeitung**: Wenn das Formular abgeschickt wird, sendet der Browser das `csrf_token` mit den anderen Formulardaten an den Server. Der Server führt dann einen simplen, aber entscheidenden Abgleich durch: Er vergleicht das Token aus dem Formular mit dem Token, das er in deiner Session gespeichert hat.

    ```php
    <?php
    session_start();

    // Stimmt das Token aus dem Formular mit dem in der Session überein?
    if ($_POST['csrf_token'] === $_SESSION['csrf_token']) {
      // Ja, die Anfrage ist legitim. Verarbeite die Daten.
      echo "E-Mail-Adresse erfolgreich geändert!";
    } else {
      // Nein, das ist ein möglicher CSRF-Angriff. Breche die Verarbeitung ab.
      die("Ungültige Anfrage!");
    }
    ?>
    ```

Warum ist das so wirksam? Ein Angreifer auf einer fremden Website kann zwar ein Formular erstellen, das eine Anfrage an deine Seite schickt. Aber aufgrund der **Same-Origin-Policy** des Browsers kann sein JavaScript den Inhalt deiner Seite nicht auslesen. Er kann also das korrekte, für deine Session gültige CSRF-Token nicht in Erfahrung bringen. Er kann zwar ein Feld `csrf_token` in sein gefälschtes Formular einbauen, aber er kann den richtigen Wert nicht erraten. Die Überprüfung auf dem Server wird fehlschlagen, und der Angriff wird abgewehrt.

#### SameSite-Cookies

Eine modernere, browserseitige Verteidigungslinie sind `SameSite`-Cookies. Dies ist ein Attribut, das du beim Setzen eines Cookies mitgeben kannst. Es weist den Browser an, unter welchen Umständen er ein Cookie mitsenden darf.

Es gibt drei mögliche Werte:

*   `SameSite=Strict`: Das Cookie wird **niemals** bei Anfragen gesendet, die von einer fremden Seite ausgehen. Das ist sehr sicher, kann aber die Benutzerfreundlichkeit beeinträchtigen. Wenn ein Nutzer zum Beispiel aus einer E-Mail einen Link zu deiner Seite anklickt, wäre er nicht mehr eingeloggt, weil der Browser das Session-Cookie nicht mitschickt.

*   `SameSite=Lax`: Das Cookie wird bei Cross-Site-Anfragen nur dann gesendet, wenn es sich um eine "sichere" Top-Level-Navigation handelt, also im Wesentlichen, wenn der Nutzer auf einen normalen Link (`GET`-Request) klickt. Es wird **nicht** bei `POST`-Anfragen gesendet, die von einer fremden Seite ausgelöst werden. Dies ist der Standard in den meisten modernen Browsern und verhindert die klassische CSRF-Angriffsform, die wir oben beschrieben haben.

*   `SameSite=None`: Das Cookie wird immer mitgesendet. Dies ist das alte Verhalten und sollte nur in speziellen Fällen (z. B. bei APIs, die von anderen Domains genutzt werden sollen) und immer in Verbindung mit dem `Secure`-Attribut (nur über HTTPS) verwendet werden.

Obwohl `SameSite=Lax` bereits einen hervorragenden Basisschutz bietet, solltest du dich nicht allein darauf verlassen. Ältere Browser unterstützen das Attribut möglicherweise nicht. Die beste Strategie ist **Defense in Depth** (mehrstufige Verteidigung): Implementiere CSRF-Tokens in deinen Formularen *und* setze deine Session-Cookies auf `SameSite=Lax`.

#### Prüfung des Origin- oder Referer-Headers

Eine weitere, wenn auch weniger robuste Methode ist die Überprüfung des `Origin`- oder `Referer`-HTTP-Headers. Diese Header geben an, von welcher Seite eine Anfrage stammt. Dein Server könnte prüfen, ob die Anfrage von deiner eigenen Domain kommt.

Diese Methode ist jedoch nicht kugelsicher. Diese Header können aus Datenschutzgründen von Browsern oder Proxys entfernt werden, und in manchen Konstellationen lassen sie sich fälschen. Sie können als zusätzliche Schutzschicht dienen, sollten aber niemals der einzige Schutzmechanismus sein.

CSRF ist ein klassisches Beispiel dafür, wie grundlegende Webmechanismen ausgenutzt werden können. Als Entwickler ist es deine Aufgabe, dieses Vertrauensverhältnis zwischen Browser und Server nicht blind zu akzeptieren, sondern durch kluge Maßnahmen wie CSRF-Tokens abzusichern. So stellst du sicher, dass die Aktionen, die deine Nutzer ausführen, auch wirklich die Aktionen sind, die sie ausführen wollten.
