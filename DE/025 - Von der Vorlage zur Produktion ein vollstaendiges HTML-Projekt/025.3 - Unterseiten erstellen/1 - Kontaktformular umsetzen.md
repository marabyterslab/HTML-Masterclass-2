# Kontaktformular umsetzen

### Das Kontaktformular: Der direkte Draht zu deinen Besuchern

Eine Website ohne Kontaktmöglichkeit ist wie ein Geschäft ohne Eingangstür. Deine Besucher möchten vielleicht eine Frage stellen, ein Angebot anfordern oder dir einfach nur Feedback geben. Ein Kontaktformular ist die professionellste und benutzerfreundlichste Methode, um diesen Austausch zu ermöglichen. Es ist strukturierter als ein einfacher `mailto:`-Link und schützt deine E-Mail-Adresse vor Spam-Bots, die das Web nach E-Mail-Adressen durchsuchen.

In diesem Kapitel bauen wir ein vollständiges, semantisch korrektes und barrierefreies Kontaktformular von Grund auf. Wir konzentrieren uns dabei rein auf die HTML-Struktur. Das Styling mit CSS und die serverseitige Verarbeitung der Daten sind Themen für spätere Module, aber wir legen hier das perfekte Fundament.

#### Das Grundgerüst: Das `<form>`-Element

Jedes Formular auf einer Webseite beginnt mit dem `<form>`-Tag. Er ist der Container für alle Formularelemente – von Texteingabefeldern über Checkboxen bis hin zum Sende-Button. Allein ist dieser Tag unsichtbar, aber er hat zwei entscheidende Attribute, die seine Funktion bestimmen: `action` und `method`.

```html
<form action="skript/verarbeite-formular.php" method="post">
  <!-- Hier kommen alle unsere Formularfelder hin -->
</form>
```

Schauen wir uns die Attribute genauer an:

*   **`action`**: Dieses Attribut enthält die URL der serverseitigen Ressource (z. B. ein PHP-Skript), die die Formulardaten empfangen und verarbeiten soll. Wenn ein Benutzer auf den Sende-Button klickt, werden die Daten an diese Adresse geschickt. Da wir uns in diesem Modul auf HTML konzentrieren, verwenden wir hier einen Platzhalter. In einem echten Projekt würde hier der Pfad zu deinem Backend-Skript stehen, das zum Beispiel eine E-Mail versendet oder die Daten in einer Datenbank speichert.

*   **`method`**: Hier legst du die HTTP-Methode fest, mit der die Daten an den Server gesendet werden. Die beiden gängigsten Methoden sind `GET` und `POST`.
    *   **`GET`**: Die Formulardaten werden als eine Reihe von Name-Wert-Paaren an die URL im `action`-Attribut angehängt. Du hast das sicher schon bei Suchmaschinen gesehen, wo deine Suchanfrage in der Adresszeile des Browsers erscheint. Für Kontaktformulare ist `GET` ungeeignet, da die Daten (inklusive persönlicher Informationen) für jeden sichtbar in der URL stehen und die Länge der URL begrenzt ist.
    *   **`POST`**: Die Formulardaten werden im Körper (Body) der HTTP-Anfrage an den Server gesendet. Sie sind nicht in der URL sichtbar. Dies ist die Standardmethode für Formulare, die sensible oder große Datenmengen übertragen. Stell es dir wie den Unterschied zwischen einer Postkarte (`GET`, jeder kann mitlesen) und einem versiegelten Brief (`POST`, der Inhalt ist privat) vor. Für unser Kontaktformular verwenden wir also immer `method="post"`.

#### Die Bausteine: `<label>` und `<input>`

Ein Formular besteht aus Beschriftungen (`<label>`) und den dazugehörigen Eingabefeldern (`<input>`). Die korrekte Verknüpfung dieser beiden Elemente ist entscheidend für die Benutzerfreundlichkeit und vor allem für die Barrierefreiheit.

Ein `<label>` beschreibt, welche Information in ein Feld eingetragen werden soll. Über das `for`-Attribut wird es direkt mit einem `<input>`-Element verknüpft. Der Wert des `for`-Attributs muss exakt mit dem Wert des `id`-Attributs des zugehörigen `input`-Elements übereinstimmen.

```html
<label for="vorname">Dein Vorname:</label>
<input type="text" id="vorname" name="vorname">
```

Diese Verknüpfung hat zwei riesige Vorteile:
1.  **Benutzerfreundlichkeit**: Wenn ein Benutzer auf den Text des Labels klickt, wird der Cursor automatisch in das zugehörige Eingabefeld gesetzt. Das ist besonders auf mobilen Geräten hilfreich, wo das Treffen kleiner Felder schwierig sein kann.
2.  **Barrierefreiheit**: Screenreader, die von sehbehinderten Menschen genutzt werden, können so die Beschriftung eindeutig dem Eingabefeld zuordnen. Sie lesen dann vor: „Dein Vorname, Eingabefeld“, anstatt nur „Eingabefeld“.

Das `<input>`-Element ist das vielseitigste Formularelement. Sein Verhalten wird hauptsächlich durch das `type`-Attribut bestimmt. Schauen wir uns die wichtigsten Typen für unser Kontaktformular an.

*   **`type="text"`**: Ein einzeiliges Textfeld für allgemeine Eingaben wie Namen oder Betreffzeilen.
*   **`type="email"`**: Ein spezielles Feld für E-Mail-Adressen. Moderne Browser validieren automatisch, ob die Eingabe in etwa wie eine E-Mail-Adresse aussieht (also ein `@`-Zeichen enthält). Auf Mobilgeräten wird zudem oft eine Tastatur mit schnellem Zugriff auf das `@`-Symbol angezeigt.
*   **`type="tel"`**: Für die Eingabe von Telefonnummern. Auch hier passen mobile Browser oft die angezeigte Tastatur an und zeigen einen Ziffernblock an.

Das `name`-Attribut ist ebenfalls unerlässlich. Es dient als Bezeichner für die Daten, wenn sie an den Server gesendet werden. Das serverseitige Skript verwendet diesen Namen, um auf den vom Benutzer eingegebenen Wert zuzugreifen (z. B. `$_POST['vorname']` in PHP).

#### Mehr Platz für Nachrichten: Das `<textarea>`-Element

Für längere Nachrichten, wie den eigentlichen Inhalt einer Kontaktanfrage, ist ein einzeiliges `<input>`-Feld ungeeignet. Hier kommt das `<textarea>`-Element ins Spiel.

```html
<label for="nachricht">Deine Nachricht:</label>
<textarea id="nachricht" name="nachricht" rows="8"></textarea>
```

Im Gegensatz zu `<input>` ist `<textarea>` ein schließendes Tag. Der Text zwischen dem öffnenden und schließenden Tag würde als Standardinhalt im Textfeld erscheinen. Die Attribute `rows` und `cols` (Spalten) können die sichtbare Größe des Feldes definieren, obwohl dies heutzutage meist eleganter mit CSS gelöst wird. Auch hier sind `id` für das Label und `name` für die Datenübermittlung essenziell.

#### Benutzerführung und Validierung im Browser

HTML5 bietet uns einige nützliche Attribute, um die Benutzererfahrung weiter zu verbessern und einfache Fehler zu vermeiden.

*   **`placeholder`**: Dieses Attribut zeigt einen kurzen Texthinweis im Eingabefeld an, der verschwindet, sobald der Benutzer beginnt zu tippen. Es ist nützlich für Beispiele oder kurze Anweisungen. Wichtig: Ein `placeholder` ersetzt niemals ein `<label>`!

    ```html
    <input type="email" id="email" name="email" placeholder="max.mustermann@beispiel.de">
    ```

*   **`required`**: Ein einfaches, aber mächtiges boolesches Attribut. Wenn es einem Formularfeld hinzugefügt wird, kann das Formular nicht abgesendet werden, solange dieses Feld leer ist. Der Browser zeigt eine standardisierte Fehlermeldung an. Dies ist eine Form der clientseitigen Validierung.

    ```html
    <label for="name">Dein Name (Pflichtfeld):</label>
    <input type="text" id="name" name="name" required>
    ```
    Beachte, dass dies nur ein erster Schutz ist. Ein technisch versierter Benutzer kann diese Prüfung umgehen. Eine zuverlässige Validierung muss immer zusätzlich auf dem Server stattfinden.

#### Struktur und Auswahlmöglichkeiten

Manchmal möchtest du dem Benutzer strukturierte Auswahlmöglichkeiten geben, zum Beispiel um den Grund der Kontaktaufnahme zu spezifizieren. Hierfür eignen sich Radio-Buttons oder Checkboxen. Um solche zusammengehörigen Elemente semantisch zu gruppieren, verwenden wir `<fieldset>` und `<legend>`.

*   **`<fieldset>`**: Gruppiert eine Reihe von zusammengehörigen Formularelementen. Visuell wird oft ein Rahmen um die Gruppe gezeichnet.
*   **`<legend>`**: Dient als Überschrift für ein `<fieldset>` und beschreibt den Zweck der darin enthaltenen Elemente.

Ein Beispiel mit Radio-Buttons (`type="radio"`):

```html
<fieldset>
  <legend>Grund deiner Anfrage</legend>

  <input type="radio" id="grund-allgemein" name="anfragegrund" value="allgemein" checked>
  <label for="grund-allgemein">Allgemeine Frage</label>

  <input type="radio" id="grund-support" name="anfragegrund" value="support">
  <label for="grund-support">Technischer Support</label>

  <input type="radio" id="grund-presse" name="anfragegrund" value="presse">
  <label for="grund-presse">Presseanfrage</label>
</fieldset>
```

Wichtige Punkte bei Radio-Buttons:
*   Alle Radio-Buttons, die zu einer Gruppe gehören (von der nur eine Option ausgewählt werden kann), müssen den gleichen `name`-Wert haben (`name="anfragegrund"`).
*   Jeder Radio-Button benötigt einen einzigartigen `id`-Wert für sein Label.
*   Das `value`-Attribut definiert den Wert, der an den Server gesendet wird, wenn diese Option ausgewählt ist. Ohne `value` wüsste der Server nicht, was der Benutzer angeklickt hat.
*   Das `checked`-Attribut kann verwendet werden, um eine Option standardmäßig vorzuselektieren.

Eine Checkbox (`type="checkbox"`) für eine Datenschutz-Zustimmung ist ebenfalls eine häufige Anforderung:

```html
<input type="checkbox" id="datenschutz" name="datenschutz_akzeptiert" value="ja" required>
<label for="datenschutz">Ich habe die <a href="/datenschutz">Datenschutzerklärung</a> gelesen und akzeptiere sie.</label>
```
Hier ist es wichtig, dass der Benutzer aktiv zustimmen muss. Deshalb machen wir die Checkbox mit `required` zu einem Pflichtfeld.

#### Der Abschluss: Der Sende-Button

Zu guter Letzt braucht jedes Formular einen Button, um es abzuschicken. Dafür gibt es zwei gängige Wege:

1.  **`<input type="submit">`**: Der traditionelle Weg. Der Text auf dem Button wird über das `value`-Attribut festgelegt.
    ```html
    <input type="submit" value="Nachricht senden">
    ```

2.  **`<button type="submit">`**: Die modernere und flexiblere Methode. Der Text steht hier direkt zwischen dem öffnenden und schließenden Tag. Der große Vorteil ist, dass ein `<button>`-Element auch andere HTML-Elemente enthalten kann, zum Beispiel ein Icon neben dem Text.
    ```html
    <button type="submit">Nachricht senden</button>
    ```

Beide Varianten lösen bei einem Klick das Absenden des Formulars an die im `action`-Attribut definierte URL aus. Aus Gründen der Flexibilität ist `<button type="submit">` heute meist die bessere Wahl.

#### Das vollständige Kontaktformular im Überblick

Fügen wir nun alle Teile zu einem kompletten, sinnvollen Kontaktformular zusammen. Dieses HTML-Konstrukt ist die perfekte Basis für jedes Projekt.

```html
<form action="skript/verarbeite-formular.php" method="post">

  <p>
    <label for="name">Dein Name:</label><br>
    <input type="text" id="name" name="name" required placeholder="Max Mustermann">
  </p>

  <p>
    <label for="email">Deine E-Mail-Adresse:</label><br>
    <input type="email" id="email" name="email" required placeholder="max.mustermann@beispiel.de">
  </p>

  <fieldset>
    <legend>Grund deiner Anfrage:</legend>
    
    <input type="radio" id="grund-allgemein" name="anfragegrund" value="allgemein" checked>
    <label for="grund-allgemein">Allgemeine Frage</label><br>
    
    <input type="radio" id="grund-support" name="anfragegrund" value="support">
    <label for="grund-support">Technischer Support</label><br>
    
    <input type="radio" id="grund-presse" name="anfragegrund" value="presse">
    <label for="grund-presse">Presseanfrage</label>
  </fieldset>

  <p>
    <label for="betreff">Betreff:</label><br>
    <input type="text" id="betreff" name="betreff" required>
  </p>

  <p>
    <label for="nachricht">Deine Nachricht:</label><br>
    <textarea id="nachricht" name="nachricht" rows="8" required></textarea>
  </p>

  <p>
    <input type="checkbox" id="datenschutz" name="datenschutz_akzeptiert" value="ja" required>
    <label for="datenschutz">Ich stimme zu, dass meine Daten zur Bearbeitung meiner Anfrage verwendet werden.</label>
  </p>
  
  <p>
    <button type="submit">Anfrage absenden</button>
  </p>

</form>
```

Dieses Formular ist semantisch korrekt, verwendet Labels für die Barrierefreiheit, nutzt sinnvolle `input`-Typen und grundlegende HTML5-Validierung. Es ist die reine, funktionale Struktur. Im nächsten Schritt würdest du dieses Gerüst mit CSS optisch ansprechend gestalten und anschließend mit einer serverseitigen Sprache die Logik implementieren, um die eingegebenen Daten tatsächlich zu empfangen und zu verarbeiten. Aber mit diesem sauberen HTML-Code hast du die bestmögliche Grundlage geschaffen.
