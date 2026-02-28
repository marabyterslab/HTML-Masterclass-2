# Profil und Einstellungen

### Dein digitales Ich: Profil- und Einstellungsseiten strukturieren

Wenn du einen Admin-Bereich oder ein Dashboard baust, schaffst du einen exklusiven Raum für deine Nutzer. Innerhalb dieses Raums gibt es kaum eine Seite, die persönlicher ist als die Profil- und Einstellungsseite. Hier verwalten Menschen ihre Identität auf deiner Plattform, passen ihre Erfahrung an und kontrollieren ihre Daten. Für dich als Entwickler bedeutet das, eine klare, intuitive und semantisch korrekte Struktur zu schaffen, die diese Interaktionen so reibungslos wie möglich macht.

Die Grundlage für fast jede Einstellungsseite ist das `<form>`-Element. Es ist der Container, der alle Eingabefelder, Schalter und Knöpfe zusammenhält und dafür sorgt, dass die gesammelten Daten an den Server gesendet werden können. Stell dir eine einzige, große Form für die gesamte Seite vor. Das ist oft der pragmatischste Ansatz, da Nutzer in der Regel mehrere Änderungen auf einmal vornehmen und dann auf einen einzigen "Speichern"-Button klicken wollen.

#### Die Anatomie einer Profilseite

Eine typische Profil- und Einstellungsseite lässt sich in mehrere logische Bereiche unterteilen. Wir werden uns diese Bereiche Schritt für Schritt ansehen und das passende HTML-Markup dafür entwickeln.

##### 1. Persönliche Informationen und das Profilbild

Dies ist das Herzstück des Profils. Hier hinterlegen Nutzer ihren Namen, ihre E-Mail-Adresse und vielleicht eine kurze Biografie. Ein zentrales Element ist auch das Profilbild.

Für die Strukturierung dieser Felder verwenden wir `<label>`- und `<input>`-Paare. Das `<label>` ist aus Gründen der Barrierefreiheit unerlässlich: Es verbindet den sichtbaren Text mit dem Eingabefeld, sodass Screenreader den Zweck des Feldes vorlesen können und Nutzer auf den Text klicken können, um das Feld zu aktivieren.

Ein typischer Aufbau für die persönlichen Daten könnte so aussehen:

```html
<section aria-labelledby="profil-info-heading">
  <h2 id="profil-info-heading">Persönliche Informationen</h2>

  <div class="form-group">
    <label for="fullName">Vollständiger Name</label>
    <input type="text" id="fullName" name="fullName" value="Max Mustermann">
  </div>

  <div class="form-group">
    <label for="username">Benutzername</label>
    <input type="text" id="username" name="username" value="max_m" aria-describedby="username-hint">
    <small id="username-hint">Dein einzigartiger Name auf dieser Plattform.</small>
  </div>

  <div class="form-group">
    <label for="email">E-Mail-Adresse</label>
    <input type="email" id="email" name="email" value="max@example.com" disabled>
    <small>Deine E-Mail-Adresse kann nicht geändert werden.</small>
  </div>

  <div class="form-group">
    <label for="bio">Über mich</label>
    <textarea id="bio" name="bio" rows="4">Leidenschaftlicher Web-Entwickler und Kaffeeliebhaber.</textarea>
  </div>
</section>
```

Ein paar wichtige Details in diesem Code:
*   **`<section>` und `aria-labelledby`**: Wir gruppieren zusammengehörige Felder in einer `<section>`. Das `aria-labelledby`-Attribut verweist auf die ID der Überschrift `<h2>` und schafft so eine starke semantische Verbindung für assistierende Technologien.
*   **`value`-Attribut**: Da es sich um eine *Bearbeitungsseite* handelt, sind die Felder mit den bereits vorhandenen Daten des Nutzers vorausgefüllt. Dafür nutzen wir das `value`-Attribut (bzw. den Inhalt des `<textarea>`). Ein `placeholder` wäre hier unpassend.
*   **`disabled`**: In diesem Beispiel kann die E-Mail-Adresse nicht geändert werden. Das `disabled`-Attribut verhindert die Bearbeitung des Feldes und sorgt dafür, dass sein Wert nicht mit dem Formular gesendet wird.
*   **`aria-describedby`**: Für den Benutzernamen gibt es einen zusätzlichen Hinweis. Mit `aria-describedby` verknüpfen wir das Eingabefeld mit der ID des Hinweistextes. Ein Screenreader wird diesen Text vorlesen, wenn der Nutzer das Feld fokussiert.

Das **Profilbild** ist ein spezieller Fall. Es besteht meist aus der Anzeige des aktuellen Bildes und einer Möglichkeit, ein neues hochzuladen.

```html
<div class="form-group profile-picture-group">
  <label for="profilePictureUpload">Profilbild</label>
  <img src="/path/to/current-avatar.jpg" alt="Aktuelles Profilbild von Max Mustermann" class="current-avatar">
  <input type="file" id="profilePictureUpload" name="profilePicture" accept="image/png, image/jpeg">
  <small>JPG oder PNG, maximal 5 MB.</small>
</div>
```

Hier kombinieren wir ein `<img>`-Element zur Vorschau mit einem `<input type="file">`, das dem Nutzer die Auswahl einer Datei von seinem Gerät ermöglicht. Das `accept`-Attribut ist eine nützliche Hilfe, da es dem Browser mitteilt, welche Dateitypen der Dialog anzeigen soll.

##### 2. Account-Sicherheit

Ein weiterer kritischer Bereich sind die Sicherheitseinstellungen, allen voran die Passwortänderung und die Option, den Account zu löschen. Diese Aktionen haben weitreichende Konsequenzen und sollten daher klar und unmissverständlich gestaltet sein.

Die Passwortänderung folgt einem bewährten Muster: aktuelles Passwort, neues Passwort und dessen Bestätigung.

```html
<section aria-labelledby="security-heading">
  <h2 id="security-heading">Sicherheit</h2>

  <div class="form-group">
    <label for="currentPassword">Aktuelles Passwort</label>
    <input type="password" id="currentPassword" name="currentPassword">
  </div>

  <div class="form-group">
    <label for="newPassword">Neues Passwort</label>
    <input type="password" id="newPassword" name="newPassword">
  </div>

  <div class="form-group">
    <label for="confirmPassword">Neues Passwort bestätigen</label>
    <input type="password" id="confirmPassword" name="confirmPassword">
  </div>
</section>
```

Der `type="password"` ist hier entscheidend. Er sorgt dafür, dass der Browser die Eingabe maskiert und die Zeichen nicht im Klartext anzeigt.

Das **Löschen des Accounts** ist eine "destruktive Aktion". Sie sollte sich visuell und funktional von den übrigen Speicher-Aktionen abheben. Oft wird sie nicht über den primären "Speichern"-Button abgewickelt, sondern führt zu einer eigenen Bestätigungsseite oder einem modalen Dialog. Im HTML können wir dies als Button mit einem warnenden Hinweis darstellen.

```html
<section aria-labelledby="danger-zone-heading">
  <h2 id="danger-zone-heading" class="danger-zone-title">Gefahrenzone</h2>
  <div class="danger-zone-content">
    <p>Wenn du deinen Account löschst, werden alle deine Daten permanent entfernt. Diese Aktion kann nicht rückgängig gemacht werden.</p>
    <button type="button" class="button-danger">Meinen Account endgültig löschen</button>
  </div>
</section>
```

Beachte den `type="button"`. Ein Button ohne Typ oder mit `type="submit"` würde das Formular absenden. Mit `type="button"` stellen wir sicher, dass er nur auf einen Klick reagiert, den wir dann mit JavaScript abfangen können, um zum Beispiel einen Bestätigungsdialog zu öffnen.

##### 3. Benachrichtigungen und Präferenzen

Hier gibst du dem Nutzer die Kontrolle darüber, wie und wann er von deiner Anwendung kontaktiert werden möchte. Checkboxen für An/Aus-Optionen oder Radio-Buttons für eine Auswahl aus mehreren Möglichkeiten sind hier die perfekten Werkzeuge.

Um eine Gruppe von zusammengehörigen Optionen semantisch zu bündeln, sind `<fieldset>` und `<legend>` die erste Wahl. Das `<legend>`-Element beschreibt die gesamte Gruppe, was die Verständlichkeit, insbesondere für Screenreader-Nutzer, enorm verbessert.

```html
<section aria-labelledby="notifications-heading">
  <h2 id="notifications-heading">Benachrichtigungen</h2>

  <fieldset>
    <legend>E-Mail-Benachrichtigungen</legend>

    <div class="form-check">
      <input type="checkbox" id="newsletter" name="notifications" value="newsletter" checked>
      <label for="newsletter">Wöchentlicher Newsletter</label>
    </div>

    <div class="form-check">
      <input type="checkbox" id="productUpdates" name="notifications" value="updates">
      <label for="productUpdates">Wichtige Produkt-Updates</label>
    </div>
    
    <div class="form-check">
      <input type="checkbox" id="activity" name="notifications" value="activity" checked>
      <label for="activity">Benachrichtigungen über Aktivitäten in meinem Account</label>
    </div>
  </fieldset>
</section>
```

Bei den Checkboxen ist das `checked`-Attribut dafür zuständig, eine Box standardmäßig zu aktivieren, basierend auf den aktuellen Einstellungen des Nutzers.

Für eine exklusive Auswahl, wie zum Beispiel die Wahl des Farbschemas (Hell/Dunkel), sind Radio-Buttons ideal. Der Schlüssel hierbei ist, dass alle Radio-Buttons, die zu einer Gruppe gehören, denselben `name`-Attributwert haben.

```html
<section aria-labelledby="appearance-heading">
  <h2 id="appearance-heading">Erscheinungsbild</h2>

  <fieldset>
    <legend>Wähle dein bevorzugtes Farbschema</legend>

    <div class="form-check">
      <input type="radio" id="theme-light" name="theme" value="light">
      <label for="theme-light">Hell</label>
    </div>

    <div class="form-check">
      <input type="radio" id="theme-dark" name="theme" value="dark" checked>
      <label for="theme-dark">Dunkel</label>
    </div>

    <div class="form-check">
      <input type="radio" id="theme-system" name="theme" value="system">
      <label for="theme-system">Systemeinstellung verwenden</label>
    </div>
  </fieldset>
</section>
```

#### Das Gesamtbild und der Abschluss

Wenn wir all diese Teile zusammensetzen, erhalten wir eine gut strukturierte, semantisch reiche und barrierefreie HTML-Grundlage für eine Profil- und Einstellungsseite. Der letzte, aber entscheidende Teil ist der Button, der all die Änderungen speichert.

```html
<form action="/save-profile" method="post">
  
  <!-- Hier kommen alle <section>-Blöcke von oben hinein -->
  <!-- Persönliche Informationen, Sicherheit, Benachrichtigungen etc. -->

  <div class="form-actions">
    <button type="submit">Änderungen speichern</button>
    <button type="reset">Zurücksetzen</button>
  </div>
</form>
```

Der `<button type="submit">` ist der Standard-Button, der beim Klick das Formular an die im `action`-Attribut des `<form>`-Tags definierte URL sendet. Ein `<button type="reset">` kann ebenfalls nützlich sein. Er setzt alle Felder im Formular auf ihre ursprünglichen Werte zurück, die beim Laden der Seite vorhanden waren.

Die hier gezeigte HTML-Struktur ist das Fundament. Sie enthält keine visuellen Stile, aber sie ist so aufgebaut, dass du mit CSS gezielt Klassen wie `.form-group`, `.form-check` oder `.button-danger` ansprechen kannst, um ein ansprechendes und benutzerfreundliches Design zu erstellen. Die saubere Semantik stellt sicher, dass deine Seite für alle Nutzer, unabhängig von ihrem Gerät oder ihren Fähigkeiten, verständlich und bedienbar ist.
