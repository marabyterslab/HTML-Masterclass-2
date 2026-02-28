# Password und hidden

### Geheime Eingaben: Passwortfelder und versteckte Daten

Nachdem du nun die grundlegenden Texteingabefelder kennst, wenden wir uns zwei speziellen Typen zu, die auf den ersten Blick gegensätzlich wirken: Das eine verbirgt die Eingabe vor neugierigen Blicken, während das andere komplett unsichtbar ist. Beide sind jedoch für die Funktionalität und Sicherheit moderner Webformulare unverzichtbar. Die Rede ist von `input type="password"` und `input type="hidden"`.

#### Das Passwortfeld: Ein Vorhang für die Privatsphäre

Stell dir vor, du sitzt in einem Café und musst dich auf einer Webseite einloggen. Du gibst deine E-Mail-Adresse ein – kein Problem. Doch dann kommt das Passwort. Ohne ein spezielles Passwortfeld würde jeder, der einen kurzen Blick auf deinen Bildschirm erhascht, dein geheimes Passwort im Klartext sehen. Genau dieses Problem löst der Eingabetyp `password`.

Wenn du `type="password"` verwendest, sorgt der Browser dafür, dass jeder eingegebene Buchstabe als Punkt oder Sternchen angezeigt wird. Es ist eine rein visuelle Maskierung auf der Benutzeroberfläche (dem Client), die die Privatsphäre des Nutzers schützt.

Der grundlegende Aufbau ist dir bereits vertraut:

```html
<form action="/login" method="post">
  <div>
    <label for="username">Benutzername:</label>
    <input type="text" id="username" name="username">
  </div>
  <div>
    <label for="passwort">Passwort:</label>
    <input type="password" id="passwort" name="user_pass">
  </div>
  <div>
    <button type="submit">Anmelden</button>
  </div>
</form>
```

Im obigen Beispiel siehst du ein typisches Login-Formular. Das Feld für den Benutzernamen ist ein normales Textfeld, während das Passwortfeld durch `type="password"` definiert wird. Für den Browser und den Server ist es immer noch ein Eingabefeld, das Textdaten sammelt. Der einzige Unterschied liegt in der Darstellung. Das `name`-Attribut (`user_pass`) ist wie immer entscheidend, damit der Server die Daten korrekt zuordnen kann, wenn das Formular abgeschickt wird.

**Eine wichtige Sicherheitsanmerkung**

Es ist absolut entscheidend zu verstehen, dass `type="password"` **keine Verschlüsselung** ist. Es ist lediglich eine visuelle Verschleierung im Browser. Wenn das Formular abgeschickt wird, werden die eingegebenen Zeichen standardmäßig im Klartext an den Server gesendet. Die tatsächliche Sicherheit der Übertragung hängt von zwei Dingen ab:

1.  **Die `method` des Formulars:** Du solltest für sensible Daten wie Passwörter immer `method="post"` verwenden. Bei `method="get"` würden die Formulardaten als Teil der URL sichtbar übertragen (z.B. `.../login?username=max&user_pass=Geheim123`), was extrem unsicher ist.
2.  **HTTPS:** Die Verbindung zwischen dem Browser und dem Server muss über HTTPS (Hypertext Transfer Protocol Secure) verschlüsselt sein. Nur dann ist sichergestellt, dass die POST-Daten während der Übertragung nicht von Dritten mitgelesen werden können.

Ein Passwortfeld ohne HTTPS ist wie ein blickdichter Briefumschlag, der mit einer offenen Postkarte verschickt wird – jeder auf dem Postweg kann den Inhalt trotzdem lesen.

**Nützliche Attribute für Passwortfelder**

Genau wie bei Textfeldern kannst du auch hier Attribute verwenden, um die Benutzerfreundlichkeit und die clientseitige Validierung zu verbessern:

*   `placeholder`: Gibt dem Nutzer einen Hinweis, was er eingeben soll, z. B. "Mindestens 8 Zeichen".
*   `required`: Macht die Eingabe des Passworts zu einer Pflichtangabe.
*   `minlength` und `maxlength`: Legen eine minimale und maximale Länge für das Passwort fest. Dies ist eine erste, einfache Überprüfung, ersetzt aber niemals eine gründliche Validierung auf dem Server.
*   `pattern`: Ermöglicht die Überprüfung des Passworts gegen einen regulären Ausdruck. Du könntest damit beispielsweise erzwingen, dass ein Passwort mindestens einen Großbuchstaben, einen Kleinbuchstaben und eine Zahl enthalten muss.

Hier ein Beispiel mit einigen dieser Attribute:

```html
<label for="new-pass">Neues Passwort:</label>
<input type="password" 
       id="new-pass" 
       name="new_password"
       minlength="8"
       required
       pattern="(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,}"
       title="Muss mindestens eine Zahl, einen Groß- und einen Kleinbuchstaben sowie mindestens 8 Zeichen enthalten.">
```

Das `pattern`-Attribut in diesem Beispiel ist recht komplex. Es prüft, ob der eingegebene Text die Kriterien erfüllt. Das `title`-Attribut ist hier besonders wichtig, da sein Inhalt dem Nutzer als Hinweis angezeigt wird, wenn die Eingabe nicht dem Muster entspricht.

#### Das versteckte Feld: Der unsichtbare Helfer

Kommen wir nun zum `input type="hidden"`. Dieses Feld ist das genaue Gegenteil eines sichtbaren Eingabefeldes. Es wird auf der Webseite überhaupt nicht dargestellt. Der Nutzer kann es weder sehen noch damit interagieren. Du fragst dich jetzt vielleicht: Wozu braucht man ein Eingabefeld, in das niemand etwas eingeben kann?

Die Antwort ist einfach: Versteckte Felder sind nicht für den Nutzer gedacht, sondern für dich, den Entwickler. Sie dienen dazu, Daten zusammen mit einem Formular an den Server zu senden, die der Nutzer nicht ändern soll oder muss. Stell es dir wie eine unsichtbare Notiz vor, die du an das Formular heftest, bevor du es zum Server schickst.

Der Aufbau ist denkbar einfach:

```html
<input type="hidden" name="product_id" value="p-12345">
```

Ein verstecktes Feld benötigt immer ein `name`-Attribut, um auf dem Server identifiziert zu werden, und ein `value`-Attribut, das den zu sendenden Wert enthält. Dieser Wert wird in der Regel nicht von Hand in den HTML-Code geschrieben, sondern dynamisch von der serverseitigen Anwendung (z. B. mit PHP, Python oder Node.js) eingefügt.

**Typische Anwendungsfälle für `type="hidden"`**

Versteckte Felder sind extrem nützlich und werden in vielen Szenarien eingesetzt:

1.  **Tracking von IDs:** Stell dir einen Online-Shop vor. Ein Nutzer klickt auf "Bewertung schreiben" für ein bestimmtes Produkt. Das Formular zum Schreiben der Bewertung muss wissen, auf welches Produkt es sich bezieht. Anstatt den Nutzer die Produkt-ID manuell eingeben zu lassen (was fehleranfällig und unschön wäre), fügst du einfach ein verstecktes Feld hinzu: `<input type="hidden" name="product_id" value="p-12345">`. Wenn das Formular abgeschickt wird, weiß der Server sofort, zu welchem Produkt die Bewertung gehört.

2.  **Session-Management:** Wenn ein Nutzer eingeloggt ist, wird seine Identität oft durch eine Session-ID auf dem Server verwaltet. Manchmal ist es nützlich, diese ID oder eine zugehörige User-ID mit einem Formular zu senden, um sicherzustellen, dass die Aktion dem richtigen Benutzerkonto zugeordnet wird.

3.  **Schutz vor CSRF (Cross-Site Request Forgery):** Dies ist ein sehr wichtiger Sicherheitsaspekt. Um sicherzustellen, dass ein Formular tatsächlich von deiner eigenen Webseite und nicht von einer bösartigen externen Seite abgeschickt wurde, generiert der Server ein einzigartiges, geheimes Token (eine zufällige Zeichenfolge). Dieses Token wird in einem versteckten Feld im Formular platziert. Wenn das Formular abgeschickt wird, prüft der Server, ob das mitgesendete Token mit dem erwarteten Token übereinstimmt. Wenn nicht, wird die Anfrage abgelehnt.
    ```html
    <input type="hidden" name="csrf_token" value="aBC123xyz789SECRET">
    ```

4.  **Zustandsinformationen speichern:** Bei mehrstufigen Formularen (z. B. einem Bestellprozess über mehrere Seiten) kann ein verstecktes Feld verwendet werden, um zu speichern, bei welchem Schritt sich der Nutzer gerade befindet (`<input type="hidden" name="step" value="2">`).

**Sicherheitshinweis für versteckte Felder**

Ähnlich wie beim Passwortfeld gibt es auch hier einen entscheidenden Sicherheitshinweis: "Versteckt" bedeutet nur, dass es auf der Webseite nicht sichtbar ist. **Es bedeutet nicht, dass es geheim ist.** Jeder technisch versierte Nutzer kann sich den Quellcode der Seite ansehen oder die Entwicklertools des Browsers öffnen und den Wert des versteckten Feldes problemlos auslesen und sogar manipulieren.

Speichere daher niemals wirklich sensible Daten (wie Preise, unverschlüsselte Passwörter oder private Schlüssel) in einem versteckten Feld, von denen du annimmst, der Nutzer könne sie nicht sehen. Versteckte Felder sind für nicht-sensible Metadaten gedacht, die den Kontext einer Formularübermittlung liefern. Die Validierung aller ankommenden Daten auf dem Server – auch der aus versteckten Feldern – ist und bleibt unerlässlich.
