# Fieldset und Legend

### Gruppieren mit `fieldset` und `legend`: Mehr als nur ein Rahmen

Stell dir ein längeres Formular vor. Vielleicht eine Anmeldung für einen Workshop, bei der du persönliche Daten, deine Essenswünsche und die gewünschte T-Shirt-Größe angeben sollst. Oder ein klassischer Checkout-Prozess mit einer Liefer- und einer separaten Rechnungsadresse. Visuell können wir solche Formulare oft leicht erfassen. Wir sehen Überschriften, Abstände und grafische Trennlinien, die uns helfen, zusammengehörige Felder auf einen Blick zu erkennen.

Doch was passiert, wenn diese visuellen Hilfen wegfallen? Für Menschen, die auf assistierende Technologien wie Screenreader angewiesen sind, kann ein unstrukturiertes Formular schnell zu einem Labyrinth werden. Wenn ein Screenreader einfach nur eine lange Liste von Eingabefeldern vorliest – "Vorname", "Nachname", "Straße", "Hausnummer", dann wieder "Vorname", "Nachname", "Straße", "Hausnummer" – fehlt der entscheidende Kontext. Gehören die zweiten Felder zur Rechnungsadresse? Oder zu einer zweiten Person? Ohne klare semantische Gruppierung ist das Raten vorprogrammiert und die Benutzerfreundlichkeit leidet enorm.

Genau hier kommen die HTML-Elemente `<fieldset>` und `<legend>` ins Spiel. Sie sind deine wichtigsten Werkzeuge, um in Formularen für Ordnung und Klarheit zu sorgen – und das auf eine Weise, die weit über das rein Visuelle hinausgeht.

#### Das `<fieldset>`-Element: Der semantische Container

Das `<fieldset>`-Element ist dazu da, eine Gruppe von zusammengehörigen Formularelementen logisch zu umschließen. Stell es dir wie einen unsichtbaren Container vor, der dem Browser und assistierenden Technologien sagt: "Alles, was sich hier drin befindet, gehört thematisch zusammen."

Standardmäßig rendern die meisten Browser ein `<fieldset>` mit einem dünnen Rahmen um den Inhalt. Das ist ein visueller Hinweis, aber es ist wichtig zu verstehen, dass dies nur ein Nebeneffekt ist. Die eigentliche Superkraft des `<fieldset>` liegt in seiner semantischen Bedeutung. Du schaffst eine programmatisch erkennbare Beziehung zwischen den Elementen.

Ein typisches Anwendungsbeispiel ist eine Gruppe von Radio-Buttons oder Checkboxen, die sich auf eine einzige Frage beziehen.

```html
<p>Wie möchtest du von uns kontaktiert werden?</p>
<input type="radio" id="contact_email" name="contact" value="email">
<label for="contact_email">E-Mail</label>

<input type="radio" id="contact_phone" name="contact" value="phone">
<label for="contact_phone">Telefon</label>

<input type="radio" id="contact_sms" name="contact" value="sms">
<label for="contact_sms">SMS</label>
```

Ohne Gruppierung liest ein Screenreader vielleicht die Frage vor, gefolgt von den einzelnen Optionen. Das funktioniert, aber es ist nicht optimal. Es fehlt eine explizite Verbindung.

Wenn wir diese Elemente in ein `<fieldset>` packen, schaffen wir diese Verbindung:

```html
<fieldset>
  <!-- Hier kommt gleich die Beschriftung rein -->
  
  <input type="radio" id="contact_email" name="contact" value="email">
  <label for="contact_email">E-Mail</label>

  <input type="radio" id="contact_phone" name="contact" value="phone">
  <label for="contact_phone">Telefon</label>

  <input type="radio" id="contact_sms" name="contact" value="sms">
  <label for="contact_sms">SMS</label>
</fieldset>
```

Jetzt weiß der Browser: Diese drei Radio-Buttons bilden eine Einheit. Aber diese Einheit hat noch keinen Namen. Es ist wie eine Kiste ohne Aufschrift. Um dieses Problem zu lösen, brauchen wir das `<legend>`-Element.

#### Das `<legend>`-Element: Die Beschriftung der Gruppe

Das `<legend>`-Element gibt deinem `<fieldset>` einen Namen. Es ist die offizielle Beschriftung für die Gruppe von Formularelementen und muss immer das **erste Kindelement** eines `<fieldset>` sein.

Wenn ein Screenreader auf ein `<fieldset>` stößt, sucht er nach einem `<legend>`-Element und liest dessen Inhalt als Erstes vor. Danach kündigt er die einzelnen Steuerelemente innerhalb der Gruppe an. Dies liefert den entscheidenden Kontext, der vorher gefehlt hat.

Schauen wir uns unser Beispiel von eben an, aber diesmal vollständig mit `<legend>`:

```html
<fieldset>
  <legend>Wie möchtest du von uns kontaktiert werden?</legend>
  
  <input type="radio" id="contact_email" name="contact" value="email">
  <label for="contact_email">E-Mail</label>

  <input type="radio" id="contact_phone" name="contact" value="phone">
  <label for="contact_phone">Telefon</label>

  <input type="radio" id="contact_sms" name="contact" value="sms">
  <label for="contact_sms">SMS</label>
</fieldset>
```

Der Unterschied in der Ausgabe eines Screenreaders ist gewaltig. Statt einer losen Abfolge von Elementen hört der Nutzer nun etwas wie:

> "Gruppe, Wie möchtest du von uns kontaktiert werden? Optionsfeld, nicht ausgewählt, E-Mail, 1 von 3. Optionsfeld, nicht ausgewählt, Telefon, 2 von 3. Optionsfeld, nicht ausgewählt, SMS, 3 von 3."

Die `<legend>` wird zur Überschrift der Gruppe. Bei jedem Element innerhalb des `<fieldset>` kann der Screenreader diese Gruppenüberschrift bei Bedarf wiederholen, sodass der Nutzer nie den Kontext verliert, selbst wenn er durch das Formular navigiert. Der `p`-Tag mit der Frage aus unserem ersten Beispiel wird damit überflüssig, denn die `<legend>` übernimmt diese Aufgabe auf semantisch korrekte Weise.

#### Ein komplexeres Beispiel: Liefer- und Rechnungsadresse

Die wahre Stärke von `<fieldset>` und `<legend>` zeigt sich bei komplexeren Strukturen. Nehmen wir das Beispiel der Liefer- und Rechnungsadresse. Ohne Gruppierung wäre der HTML-Code eine lange, repetitive Liste von `<label>`- und `<input>`-Paaren.

```html
<!-- Schlecht zugängliches Beispiel -->
<h3>Lieferadresse</h3>
<label for="ship_street">Straße</label>
<input type="text" id="ship_street" name="ship_street">
<!-- ... weitere Felder für die Lieferadresse ... -->

<h3>Rechnungsadresse</h3>
<label for="bill_street">Straße</label>
<input type="text" id="bill_street" name="bill_street">
<!-- ... weitere Felder für die Rechnungsadresse ... -->
```

Ein sehender Nutzer erkennt die Struktur durch die `<h3>`-Überschriften. Für einen Screenreader-Nutzer ist die Verbindung zwischen der Überschrift und den zugehörigen Feldern jedoch nicht so stark und eindeutig wie bei einem `<fieldset>`.

Die barrierefreie und semantisch korrekte Lösung sieht so aus:

```html
<form>
  <fieldset>
    <legend>Lieferadresse</legend>
    
    <label for="ship_street">Straße</label>
    <input type="text" id="ship_street" name="ship_street">
    
    <label for="ship_city">Stadt</label>
    <input type="text" id="ship_city" name="ship_city">
    
    <label for="ship_zip">Postleitzahl</label>
    <input type="text" id="ship_zip" name="ship_zip">
  </fieldset>

  <fieldset>
    <legend>Rechnungsadresse</legend>
    
    <label for="bill_street">Straße</label>
    <input type="text" id="bill_street" name="bill_street">
    
    <label for="bill_city">Stadt</label>
    <input type="text" id="bill_city" name="bill_city">
    
    <label for="bill_zip">Postleitzahl</label>
    <input type="text" id="bill_zip" name="bill_zip">
  </fieldset>
</form>
```

Wenn ein Nutzer nun in das Feld für die Straße der Rechnungsadresse navigiert, kann der Screenreader verkünden: "Gruppe, Rechnungsadresse. Eingabefeld, Straße." Der Kontext ist sofort klar und unmissverständlich. Die Verwirrung, die durch doppelte Feldbezeichnungen ("Straße", "Stadt") entstehen könnte, wird vollständig aufgelöst.

#### Styling von `fieldset` und `legend`

Ein häufiger Grund, warum Entwickler zögern, `<fieldset>` und `<legend>` zu verwenden, ist das Standard-Styling der Browser. Der Rahmen um das `<fieldset>` und die Positionierung der `<legend>` passen oft nicht in ein modernes Webdesign.

Die gute Nachricht ist: Du bist nicht an dieses Aussehen gebunden. Du kannst beides mit CSS nach Belieben anpassen, ohne ihre semantische Bedeutung und die damit verbundenen Vorteile für die Barrierefreiheit zu verlieren.

Du möchtest den Standardrahmen entfernen und die Legende wie eine normale Überschrift aussehen lassen? Kein Problem.

```css
fieldset {
  /* Standard-Browser-Styles zurücksetzen */
  border: none;
  padding: 0;
  margin: 0;
  
  /* Optional: Etwas Abstand zwischen den Fieldsets schaffen */
  margin-bottom: 2rem;
}

legend {
  /* Standard-Browser-Styles zurücksetzen */
  padding: 0;
  
  /* Wie eine Überschrift stylen */
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 1rem;
  
  /* Wichtig: legend behält seine Breite bei, wenn es nicht explizit gesetzt wird */
  width: 100%;
}
```

Mit diesem CSS entfernst du die visuellen Standardeinstellungen und übernimmst die volle Kontrolle über das Design. Das `<fieldset>` verhält sich nun wie ein normaler Container (ähnlich einem `<div>`), und die `<legend>` wie eine Überschrift. Aber unter der Haube bleibt die unschätzbare semantische Struktur für assistierende Technologien erhalten. Das ist der Kern des Prinzips der progressiven Verbesserung: Zuerst kommt die semantisch korrekte und zugängliche HTML-Struktur, dann die visuelle Gestaltung mit CSS.

#### Wann du `fieldset` nicht verwenden solltest

Bei all den Vorteilen ist es auch wichtig zu wissen, wann der Einsatz von `<fieldset>` übertrieben wäre. Verwende es nur dann, wenn du eine Gruppe von **mehreren** Steuerelementen hast, die eine **gemeinsame Beschriftung** benötigen.

Ein einfaches Login-Formular mit einem Feld für die E-Mail-Adresse und einem für das Passwort benötigt kein `<fieldset>`. Jedes Eingabefeld hat sein eigenes, eindeutiges `<label>`, das für sich allein verständlich ist. Ein `<fieldset>` würde hier nur unnötige "Verbosity" für Screenreader-Nutzer erzeugen, da bei jedem Feld eine zusätzliche Gruppen-Legende angesagt würde. Die Faustregel lautet: Gruppiere, wenn es das Verständnis verbessert und Mehrdeutigkeiten beseitigt.

Durch den bewussten und korrekten Einsatz von `<fieldset>` und `<legend>` machst du deine Formulare nicht nur logischer und strukturierter, sondern du baust eine entscheidende Brücke für Menschen, die das Web anders erleben. Du gibst Kontext, schaffst Klarheit und sorgst dafür, dass deine Formulare für alle nutzbar sind.
