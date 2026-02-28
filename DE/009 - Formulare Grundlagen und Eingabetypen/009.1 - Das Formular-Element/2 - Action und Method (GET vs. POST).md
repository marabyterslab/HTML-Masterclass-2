# Action und Method (GET vs. POST)

### Action und Method: Die Postboten deiner Formulardaten

Ein HTML-Formular ist im Grunde ein Sammler. Es sammelt Informationen, die du oder ein anderer Nutzer eingeben. Aber was passiert, nachdem der Nutzer auf den „Senden“-Button geklickt hat? Die gesammelten Daten schweben ja nicht einfach so im luftleeren Raum. Sie müssen an einen bestimmten Ort geschickt und auf eine bestimmte Art und Weise transportiert werden. Genau hier kommen die beiden wichtigsten Attribute des `<form>`-Elements ins Spiel: `action` und `method`.

Stell dir vor, du möchtest einen Brief verschicken. Du brauchst zwei Dinge: eine Adresse, an die der Brief gehen soll, und eine Versandmethode, also ob du ihn als Standardbrief, als Einschreiben oder als Paket aufgibst. In der Welt der HTML-Formulare ist `action` die Adresse und `method` die Versandart.

#### Das `action`-Attribut: Das Ziel der Reise

Das `action`-Attribut ist wahrscheinlich das einfachere der beiden. Es legt fest, wohin die Formulardaten gesendet werden sollen. Der Wert dieses Attributs ist eine URL – die Adresse einer serverseitigen Ressource, die darauf vorbereitet ist, die Daten zu empfangen und zu verarbeiten.

Diese Ressource ist oft ein Skript, das in einer Sprache wie PHP, Python, Ruby oder Node.js geschrieben ist. Dieses Skript nimmt die Daten entgegen, prüft sie, speichert sie vielleicht in einer Datenbank, verschickt eine E-Mail oder führt eine andere Aktion aus.

Schauen wir uns ein einfaches Beispiel an:

```html
<form action="/skripte/registrierung.php" method="post">
  <!-- Hier stehen deine ganzen input-Felder -->
  <button type="submit">Registrieren</button>
</form>
```

In diesem Fall werden alle Daten aus dem Formular an die Datei `registrierung.php` im Ordner `/skripte` auf demselben Server geschickt. Der Browser packt die Daten zusammen und sendet sie an diese URL.

Das `action`-Attribut kann auch auf eine externe URL verweisen, zum Beispiel auf die API eines Drittanbieters:

```html
<form action="https://api.newsletter-anbieter.com/subscribe" method="post">
  <!-- ... -->
</form>
```

Was passiert, wenn du das `action`-Attribut weglässt oder es leer lässt (`action=""`)? In diesem Fall sendet der Browser die Formulardaten an die URL der aktuellen Seite. Das ist nützlich für Formulare, die sich selbst verarbeiten, wie zum Beispiel eine Suchfunktion auf einer Ergebnisseite, die sich bei jeder neuen Suche selbst neu lädt.

Zusammengefasst: `action` gibt das „Wohin“ an.

#### Das `method`-Attribut: Die Art des Versands

Während `action` das Ziel bestimmt, legt `method` fest, *wie* die Daten dorthin gelangen. Es gibt verschiedene HTTP-Methoden (auch „Verben“ genannt), aber für HTML-Formulare sind fast ausschließlich zwei relevant: `GET` und `POST`. Die Wahl zwischen diesen beiden ist keine Geschmacksfrage, sondern eine fundamentale Entscheidung, die die Sicherheit, Funktionalität und das Verhalten deiner Webanwendung beeinflusst.

Wenn du kein `method`-Attribut angibst, verwendet der Browser standardmäßig `GET`.

##### Die GET-Methode: Offen und transparent

Wenn du ein Formular mit der `GET`-Methode abschickst, packt der Browser alle Formulardaten (die `name`- und `value`-Paare deiner Eingabefelder) zusammen und hängt sie als eine lange Zeichenkette an die URL an, die im `action`-Attribut steht.

Nehmen wir ein einfaches Suchformular:

```html
<form action="/suche" method="get">
  <label for="query">Suche:</label>
  <input type="text" id="query" name="q">
  <button type="submit">Suchen</button>
</form>
```

Wenn ein Nutzer „HTML Formulare“ in das Suchfeld eingibt und auf „Suchen“ klickt, wird der Browser zu einer neuen URL navigieren, die etwa so aussieht:

`https://deine-webseite.de/suche?q=HTML+Formulare`

Schauen wir uns diese URL genauer an:
*   `https://deine-webseite.de/suche`: Das ist der Teil aus dem `action`-Attribut.
*   `?`: Das Fragezeichen trennt die Basis-URL von den Formulardaten.
*   `q=HTML+Formulare`: Das sind die Daten. `q` ist der `name` des Input-Feldes. `HTML+Formulare` ist der Wert, den der Nutzer eingegeben hat. Leerzeichen werden dabei durch ein `+` (oder `%20`) ersetzt, und andere Sonderzeichen werden ebenfalls kodiert (URL-Encoding).

Wenn es mehrere Felder gäbe, würden sie durch ein kaufmännisches Und (`&`) getrennt:

`.../suche?q=HTML+Formulare&kategorie=webdev`

**Eigenschaften der GET-Methode:**

1.  **Sichtbarkeit:** Die Daten sind für jeden sichtbar – in der Adresszeile des Browsers, im Browserverlauf, in Server-Logfiles und wenn der Link geteilt wird. Das macht `GET` absolut ungeeignet für sensible Daten wie Passwörter oder persönliche Informationen.
2.  **Längenbeschränkung:** URLs haben eine maximale Länge. Je nach Browser und Server liegt diese Grenze typischerweise bei etwa 2000 Zeichen. Für große Datenmengen, wie zum Beispiel den Inhalt eines langen Blogartikels, ist `GET` daher nicht geeignet.
3.  **Bookmark-Fähigkeit:** Da alle Parameter in der URL enthalten sind, kann das Ergebnis einer `GET`-Anfrage einfach als Lesezeichen gespeichert, per E-Mail verschickt oder geteilt werden. Jeder, der den Link öffnet, sieht exakt dieselbe Ergebnisseite. Das ist perfekt für Suchergebnisse oder gefilterte Ansichten in einem Onlineshop.
4.  **Idempotenz:** Dieses technische Wort bedeutet, dass eine Anfrage beliebig oft wiederholt werden kann, ohne dass sich der Zustand auf dem Server ändert. Eine Suche nach „Katzenvideos“ ändert nichts an der Datenbank der Katzenvideos. Sie liefert nur Daten. `GET`-Anfragen sollten immer idempotent sein – sie sind dazu da, Daten abzurufen, nicht sie zu verändern.

**Wann du GET verwenden solltest:** Für Aktionen, die Daten abrufen und den Zustand auf dem Server nicht verändern. Typische Beispiele sind Suchanfragen, das Filtern von Produkten oder das Sortieren von Tabellen.

##### Die POST-Methode: Diskret und leistungsstark

Im Gegensatz zu `GET` werden die Daten bei der `POST`-Methode nicht an die URL angehängt. Stattdessen werden sie im „Körper“ (Body) der HTTP-Anfrage verpackt und an den Server gesendet. Die URL in der Adresszeile des Browsers bleibt sauber und zeigt nur den Wert des `action`-Attributs.

Hier ist ein typisches Login-Formular:

```html
<form action="/login-verarbeiten.php" method="post">
  <label for="username">Benutzername:</label>
  <input type="text" id="username" name="benutzer">
  <label for="password">Passwort:</label>
  <input type="password" id="password" name="passwort">
  <button type="submit">Anmelden</button>
</form>
```

Nach dem Absenden dieses Formulars lautet die URL in der Adresszeile einfach:

`https://deine-webseite.de/login-verarbeiten.php`

Der Benutzername und das Passwort sind nicht sichtbar. Sie reisen verdeckt im Rumpf der Anfrage mit.

**Wichtiger Sicherheitshinweis:** Nur weil die Daten nicht in der URL sichtbar sind, heißt das nicht, dass sie verschlüsselt oder sicher sind. Ohne eine HTTPS-Verbindung (erkennbar am `https://` in der URL) werden die Daten immer noch im Klartext über das Internet gesendet und können von Angreifern abgefangen werden. `POST` sorgt für Diskretion in der Benutzeroberfläche, aber nur HTTPS sorgt für echte Sicherheit bei der Übertragung.

**Eigenschaften der POST-Methode:**

1.  **Unsichtbarkeit:** Die Daten erscheinen nicht in der URL, im Browserverlauf oder in den üblichen Server-Logs. Das ist der Hauptgrund, warum `POST` für sensible Daten wie Passwörter, Kreditkarteninformationen oder persönliche Nachrichten verwendet wird.
2.  **Keine Längenbeschränkung:** Praktisch gesehen gibt es keine Begrenzung für die Datenmenge, die du mit `POST` senden kannst (obwohl Webserver oft eigene Limits konfigurieren). Das macht `POST` zur einzigen Wahl für das Hochladen von Dateien, das Senden langer Texte oder komplexer, verschachtelter Daten.
3.  **Nicht Bookmark-fähig:** Da die Daten nicht Teil der URL sind, kann das Ergebnis einer `POST`-Anfrage nicht sinnvoll als Lesezeichen gespeichert werden. Würdest du es versuchen, würde das Lesezeichen nur die Ziel-URL ohne die gesendeten Daten speichern, was wahrscheinlich zu einer Fehlermeldung oder einer leeren Seite führt.
4.  **Nicht idempotent:** Eine `POST`-Anfrage ist dazu gedacht, den Zustand auf dem Server zu verändern. Sie legt einen neuen Benutzer an, bucht einen Flug, sendet eine Bestellung ab oder veröffentlicht einen Kommentar. Wenn du eine solche Anfrage wiederholst, wird die Aktion erneut ausgeführt (du würdest also zwei Bestellungen aufgeben). Genau aus diesem Grund warnen Browser dich mit einer Meldung wie „Möchten Sie dieses Formular erneut senden?“, wenn du versuchst, eine Seite neu zu laden, die durch eine `POST`-Anfrage entstanden ist.

**Wann du POST verwenden solltest:** Immer dann, wenn du Daten an den Server sendest, um dort etwas zu erstellen, zu ändern oder zu löschen. Also für Registrierungen, Logins, Kontaktformulare, Bestellvorgänge, das Hochladen von Dateien und jede andere Aktion, die eine Zustandsänderung zur Folge hat.

#### GET vs. POST: Die direkte Gegenüberstellung

| Eigenschaft           | GET                                                        | POST                                                       |
| --------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| **Datenübertragung**  | In der URL (als Query-String)                              | Im Körper (Body) der HTTP-Anfrage                          |
| **Sichtbarkeit**      | Daten sind in URL, Verlauf und Logs sichtbar               | Daten sind nicht direkt sichtbar                           |
| **Datenlimit**        | Ja, ca. 2000 Zeichen                                       | Praktisch unbegrenzt                                       |
| **Lesezeichen**       | Ja, die Ergebnis-URL kann gespeichert und geteilt werden   | Nein, das Ergebnis ist nicht per URL reproduzierbar        |
| **Idempotenz**        | Ja (sollte es sein)                                        | Nein                                                       |
| **Typischer Anwendungsfall** | Daten abrufen (Suche, Filter)                              | Daten verändern (Anlegen, Ändern, Löschen)                 |

Die Entscheidung zwischen `GET` und `POST` ist eine der grundlegendsten Weichenstellungen bei der Arbeit mit Formularen. Eine gute Faustregel lautet: Wenn das Formular eine Aktion auslöst, die man als „Lesen“ oder „Anfragen“ bezeichnen könnte, benutze `GET`. Wenn die Aktion eher „Schreiben“, „Erstellen“ oder „Ändern“ ist, benutze `POST`. Indem du diese einfache Regel befolgst, stellst du sicher, dass deine Formulare sich vorhersehbar, sicher und im Einklang mit den Konventionen des Webs verhalten.
