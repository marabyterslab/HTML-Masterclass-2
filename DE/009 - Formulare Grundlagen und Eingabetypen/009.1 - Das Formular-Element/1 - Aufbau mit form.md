# Aufbau mit form

### Das `<form>`-Element: Das Fundament interaktiver Webseiten

Stell dir eine Webseite vor, die nur Informationen anzeigt. Du kannst lesen, schauen, aber nicht interagieren. Das wäre ziemlich langweilig, oder? Das Web lebt von der Interaktion: Du meldest dich bei einem Dienst an, schreibst einen Kommentar, suchst nach einem Produkt oder lädst ein Foto hoch. All diese Aktionen haben eines gemeinsam: Sie benötigen eine Möglichkeit, Daten von dir, dem Benutzer, zu sammeln und an den Server zu senden. Genau hier kommt das `<form>`-Element ins Spiel.

Ein Formular ist im Grunde ein digitaler Fragebogen. Es ist der Container, der alle Eingabefelder, Knöpfe und Beschriftungen zusammenhält, die für eine bestimmte Datensammlung benötigt werden. Ohne das umschließende `<form>`-Tag wüssten die einzelnen Eingabefelder nicht, wohin sie ihre Daten schicken sollen oder dass sie überhaupt zusammengehören.

#### Die grundlegende Struktur

Auf den ersten Blick ist ein `<form>`-Element denkbar einfach. Es ist ein Block-Element, das andere Elemente umschließt.

```html
<form>
  <!-- Hier kommen alle Formular-Elemente hinein -->
  <!-- z.B. <label>, <input>, <textarea>, <button> -->
</form>
```

Was du innerhalb dieses Containers platzierst, bildet dein sichtbares Formular. Die wahre Magie des `<form>`-Elements liegt jedoch nicht in seinem Inhalt, sondern in seinen Attributen. Diese definieren, was mit den gesammelten Daten passieren soll, sobald der Benutzer auf den "Senden"-Button klickt. Die beiden wichtigsten Attribute sind `action` und `method`.

#### Das `action`-Attribut: Wohin mit den Daten?

Das `action`-Attribut ist wie die Adresse auf einem Briefumschlag. Es legt das Ziel fest, an das die Formulardaten gesendet werden. Dies ist in der Regel eine URL, die auf ein serverseitiges Skript verweist (z.B. in PHP, Python, Node.js oder einer anderen serverseitigen Sprache geschrieben). Dieses Skript nimmt die Daten entgegen, verarbeitet sie – speichert sie in einer Datenbank, sendet eine E-Mail oder führt eine Suche durch – und sendet oft eine Antwortseite an den Browser zurück.

```html
<!-- Die Daten werden an ein Skript im selben Verzeichnis gesendet -->
<form action="verarbeiten.php">
  ...
</form>

<!-- Die Daten werden an eine absolute URL gesendet -->
<form action="https://api.example.com/daten-empfangen">
  ...
</form>
```

Lässt du das `action`-Attribut weg oder setzt es auf einen leeren String (`action=""`), werden die Formulardaten an die URL der aktuellen Seite gesendet. Das ist nützlich, wenn die gleiche Seite, die das Formular anzeigt, auch für die Verarbeitung der Daten zuständig ist.

#### Das `method`-Attribut: Wie werden die Daten versendet?

Wenn `action` das "Wohin" ist, dann ist `method` das "Wie". Dieses Attribut bestimmt die HTTP-Methode, die für den Versand der Daten verwendet wird. Für Webformulare gibt es zwei grundlegende Methoden: `GET` und `POST`.

##### Die `GET`-Methode

Die `GET`-Methode hängt die Formulardaten als eine Reihe von Schlüssel-Wert-Paaren an die URL im `action`-Attribut an. Diese werden durch ein Fragezeichen (`?`) von der eigentlichen URL getrennt und die einzelnen Paare durch ein kaufmännisches Und (`&`) verbunden.

Stell dir ein einfaches Suchformular vor:

```html
<form action="/suche" method="get">
  <label for="query">Suche:</label>
  <input type="search" id="query" name="q">
  <button type="submit">Suchen</button>
</form>
```

Wenn du in dieses Feld "HTML Formulare" eingibst und auf "Suchen" klickst, wird dein Browser zu einer URL navigieren, die etwa so aussieht:

`https://deine-webseite.de/suche?q=HTML+Formulare`

**Eigenschaften von `GET`:**

*   **Sichtbar:** Die Daten sind Teil der URL und für jeden sichtbar. Daher ist `GET` absolut ungeeignet für sensible Informationen wie Passwörter oder persönliche Daten.
*   **Längenbeschränkung:** URLs haben eine maximale Länge (die je nach Browser und Server variiert, aber typischerweise um die 2000 Zeichen liegt). Für große Datenmengen ist `GET` also nicht geeignet.
*   **Bookmark-fähig:** Da die Daten Teil der URL sind, kann das Ergebnis einer `GET`-Anfrage einfach als Lesezeichen gespeichert oder geteilt werden. Das ist perfekt für Suchergebnisse oder Filter-Einstellungen.
*   **Idempotent:** Eine `GET`-Anfrage sollte den Zustand auf dem Server nicht verändern. Sie dient nur zum Abrufen von Daten. Mehrmaliges Aufrufen derselben `GET`-URL sollte immer zum gleichen Ergebnis führen.

##### Die `POST`-Methode

Im Gegensatz zu `GET` sendet die `POST`-Methode die Formulardaten nicht in der URL, sondern im sogenannten "Body" (Körper) der HTTP-Anfrage. Diese Daten sind für den Benutzer nicht direkt sichtbar.

Nehmen wir ein Anmeldeformular:

```html
<form action="/login-prozess" method="post">
  <label for="username">Benutzername:</label>
  <input type="text" id="username" name="benutzer">
  
  <label for="password">Passwort:</label>
  <input type="password" id="password" name="passwort">
  
  <button type="submit">Anmelden</button>
</form>
```

Wenn du dieses Formular abschickst, siehst du in der Adresszeile des Browsers nur `https://deine-webseite.de/login-prozess`. Die Daten `benutzer=DeinName` und `passwort=DeinGeheimesPasswort` werden unsichtbar im Hintergrund an den Server übertragen.

**Eigenschaften von `POST`:**

*   **Unsichtbar:** Die Daten erscheinen nicht in der URL, was sie zur richtigen Wahl für sensible Daten macht.
*   **Keine Längenbeschränkung:** Du kannst praktisch unbegrenzte Datenmengen senden, was für das Hochladen von Dateien oder das Senden langer Texte (z.B. aus einem `<textarea>`) notwendig ist.
*   **Nicht Bookmark-fähig:** Da die Daten nicht in der URL enthalten sind, kannst du das Ergebnis einer `POST`-Anfrage nicht einfach als Lesezeichen speichern. Wenn du die Seite neu lädst, fragt dich der Browser oft, ob die Formulardaten erneut gesendet werden sollen.
*   **Nicht idempotent:** Eine `POST`-Anfrage ist dafür gedacht, den Zustand auf dem Server zu verändern (z.B. einen neuen Benutzer anlegen, einen Kommentar posten, eine Bestellung aufgeben).

**Faustregel:** Verwende `GET` für alles, was einer Suche oder einem Abruf von Daten ähnelt (z.B. Suchen, Filtern). Verwende `POST` für alles, was Daten auf dem Server erstellt, ändert oder löscht, sowie für alle Formulare, die sensible oder große Datenmengen enthalten.

#### Das `name`-Attribut: Die Benennung der Daten

Ein Formular kann viele Eingabefelder haben. Damit der Server weiß, welcher Wert zu welchem Feld gehört, muss jedes Eingabefeld, dessen Wert gesendet werden soll, ein `name`-Attribut haben. Der Wert des `name`-Attributs wird zum Schlüssel im Schlüssel-Wert-Paar, das gesendet wird.

```html
<form action="/registrierung" method="post">
  <!-- Der Name "vorname" wird zum Schlüssel für den eingegebenen Wert -->
  <label for="firstname">Vorname:</label>
  <input type="text" id="firstname" name="vorname">

  <!-- Ohne "name"-Attribut würde dieses Feld beim Senden ignoriert! -->
  <label for="middlename">Zweiter Vorname (optional):</label>
  <input type="text" id="middlename">
  
  <button type="submit">Registrieren</button>
</form>
```

Wenn du in das erste Feld "Max" eingibst und das Formular abschickst, empfängt der Server die Daten als `vorname=Max`. Das zweite Feld wird komplett ignoriert, weil es kein `name`-Attribut hat.

#### Weitere nützliche Attribute

Neben `action` und `method` gibt es noch weitere Attribute für das `<form>`-Element, die in bestimmten Situationen sehr hilfreich sind.

*   **`enctype`**: Dieses Attribut gibt an, wie die Formulardaten kodiert werden sollen, bevor sie an den Server gesendet werden. Der Standardwert ist `application/x-www-form-urlencoded`, was für die meisten Formulare korrekt ist. Wenn dein Formular jedoch das Hochladen von Dateien über ein `<input type="file">`-Element ermöglicht, musst du den `enctype` unbedingt auf `multipart/form-data` setzen. Andernfalls wird die Datei nicht korrekt übertragen.

    ```html
    <!-- Notwendig für den Datei-Upload -->
    <form action="/upload" method="post" enctype="multipart/form-data">
      <label for="avatar">Profilbild hochladen:</label>
      <input type="file" id="avatar" name="profilbild">
      <button type="submit">Hochladen</button>
    </form>
    ```

*   **`novalidate`**: Moderne Browser bieten eine eingebaute Validierung für Formularfelder (z.B. wird bei `<input type="email">` geprüft, ob die Eingabe wie eine E-Mail-Adresse aussieht). Wenn du dieses Verhalten unterdrücken möchtest, zum Beispiel weil du eine eigene Validierung mit JavaScript implementieren oder das Formular zu Testzwecken ohne Validierung absenden willst, kannst du das `novalidate`-Attribut hinzufügen.

    ```html
    <form action="/test" method="post" novalidate>
      <!-- Die Browser-Validierung für dieses E-Mail-Feld ist deaktiviert -->
      <label for="email">E-Mail:</label>
      <input type="email" id="email" name="email">
      <button type="submit">Senden</button>
    </form>
    ```

*   **`autocomplete`**: Mit diesem Attribut kannst du dem Browser einen Hinweis geben, ob er versuchen soll, die Felder des Formulars automatisch auszufüllen. Die Standardeinstellung ist `on`. Wenn du dies für ein bestimmtes Formular (z.B. aus Sicherheitsgründen bei einem "Passwort ändern"-Formular) verhindern möchtest, kannst du es auf `off` setzen.

    ```html
    <form action="/change-password" method="post" autocomplete="off">
      ...
    </form>
    ```

Das `<form>`-Element ist also weit mehr als nur ein einfacher Container. Es ist die Kommandozentrale für die gesamte Benutzerinteraktion, die das Sammeln von Daten beinhaltet. Indem du seine Attribute `action`, `method` und `enctype` korrekt einsetzt, stellst du sicher, dass die von deinen Nutzern eingegebenen Informationen zuverlässig und sicher an den richtigen Ort gelangen, um dort verarbeitet zu werden.
