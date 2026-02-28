# Checkboxen für Mehrfachauswahl

### Checkboxen für die Mehrfachauswahl

Stell dir vor, du erstellst ein Formular, in dem ein Nutzer seine Interessen angeben soll, zum Beispiel für einen Newsletter. Hobbys, Musikgenres, Lieblingsthemen – selten hat man hier nur eine einzige Präferenz. Genau für solche Fälle, in denen null, eine oder mehrere Optionen aus einer Liste ausgewählt werden können, gibt es in HTML das perfekte Werkzeug: die Checkbox.

Im Gegensatz zu Radio-Buttons, die dich auf eine einzige Wahl beschränken (wie die Wahl zwischen "männlich", "weiblich" oder "divers"), bieten Checkboxen volle Freiheit. Du kannst alle ankreuzen, gar keine oder eine beliebige Kombination dazwischen. Ein klassisches Beispiel ist die Pizzabestellung online: Du kannst Salami, Pilze und extra Käse auswählen – eine typische Mehrfachauswahl.

#### Die grundlegende Syntax einer Checkbox

Das Erstellen einer Checkbox ist erstaunlich einfach. Es handelt sich um ein `<input>`-Element, bei dem das `type`-Attribut auf den Wert `checkbox` gesetzt wird.

```html
<input type="checkbox">
```

Wenn du diesen Code in einer HTML-Datei speicherst und im Browser öffnest, siehst du bereits ein kleines, anklickbares Kästchen. Es ist funktional, aber noch nicht sehr nützlich. Ihm fehlen zwei entscheidende Dinge: eine Beschriftung, damit der Nutzer weiß, wofür das Kästchen steht, und Attribute, die dem Browser und dem Server sagen, was mit den Daten passieren soll.

#### Die entscheidenden Attribute: `name` und `value`

Damit eine Checkbox in einem Formular sinnvoll ist, benötigt sie mindestens zwei weitere Attribute: `name` und `value`.

*   **`name`**: Dieses Attribut gruppiert zusammengehörige Checkboxen. Wenn du zum Beispiel nach den Interessen deiner Nutzer fragst, könnten alle Checkboxen den `name="interessen"` tragen. Wenn das Formular abgeschickt wird, weiß der Server, dass alle ausgewählten Werte zu dieser einen Kategorie "interessen" gehören.
*   **`value`**: Dieses Attribut enthält den eigentlichen Wert, der an den Server gesendet wird, wenn die Checkbox *ausgewählt* ist. Dieser Wert ist für den Nutzer nicht direkt sichtbar, aber für die Datenverarbeitung unerlässlich. Wenn der Nutzer beispielsweise das Kästchen für "Sport" ankreuzt, könnte der `value` `"sport"` sein.

Sehen wir uns ein konkretes Beispiel an:

```html
<p>Welche Themen interessieren dich?</p>
<input type="checkbox" name="interessen" value="technologie">
<input type="checkbox" name="interessen" value="sport">
<input type="checkbox" name="interessen" value="kultur">
```

In diesem Code haben wir drei Checkboxen. Sie alle teilen sich den `name` "interessen", was sie logisch miteinander verbindet. Jede hat jedoch einen einzigartigen `value`, der die spezifische Option repräsentiert. Wenn ein Nutzer "Technologie" und "Kultur" auswählt und das Formular abschickt, würde der Server in etwa die Information `interessen=technologie` und `interessen=kultur` erhalten. Die Checkbox für "Sport" wurde nicht angeklickt, also wird ihr Wert auch nicht gesendet.

#### Beschriftungen mit `<label>`: Ein Muss für die Benutzerfreundlichkeit

Unser obiges Beispiel hat ein großes Problem: Der Nutzer sieht nur drei Kästchen ohne jeglichen Kontext. Wir müssen ihm sagen, welche Option zu welchem Kästchen gehört. Die beste und semantisch korrekteste Methode dafür ist das `<label>`-Element.

Ein `<label>` verbessert nicht nur die Lesbarkeit deines Codes und deiner Seite, sondern auch die Benutzerfreundlichkeit und die Barrierefreiheit. Indem du ein `<label>` mit einem `<input>`-Element verknüpfst, schaffst du eine größere Klickfläche. Der Nutzer kann dann nicht nur auf das winzige Kästchen, sondern auch auf den Text der Beschriftung klicken, um die Checkbox zu aktivieren oder zu deaktivieren.

Die Verknüpfung erfolgt über das `for`-Attribut im `<label>` und das `id`-Attribut im `<input>`. Der Wert des `for`-Attributs muss exakt mit dem Wert des `id`-Attributs übereinstimmen. Jede `id` auf einer Webseite muss einzigartig sein.

Erweitern wir unser Beispiel:

```html
<p>Welche Themen interessieren dich?</p>

<input type="checkbox" id="tech" name="interessen" value="technologie">
<label for="tech">Technologie</label>
<br>

<input type="checkbox" id="sport" name="interessen" value="sport">
<label for="sport">Sport</label>
<br>

<input type="checkbox" id="kultur" name="interessen" value="kultur">
<label for="kultur">Kultur</label>
```

Dieses Markup ist jetzt sowohl für sehende Nutzer als auch für assistierende Technologien wie Screenreader viel verständlicher und einfacher zu bedienen. Die `<br>`-Tags sorgen hier für einen einfachen Zeilenumbruch, in einem echten Projekt würdest du dies wahrscheinlich mit CSS eleganter lösen.

#### Eine Checkbox vorauswählen: Das `checked`-Attribut

Manchmal möchtest du, dass eine Checkbox bereits beim Laden der Seite standardmäßig ausgewählt ist. Das kann nützlich sein, um eine empfohlene Option hervorzuheben oder bei Opt-out-Szenarien (z. B. "Ja, ich möchte den Newsletter abonnieren", das standardmäßig aktiviert ist).

Dafür gibt es das boolesche Attribut `checked`. Du fügst es einfach zum `<input>`-Tag hinzu. Es benötigt keinen Wert.

```html
<input type="checkbox" id="newsletter" name="newsletter_abo" value="ja" checked>
<label for="newsletter">Ja, ich möchte den wöchentlichen Newsletter erhalten.</label>
```

In diesem Fall wird die Seite mit einem bereits angekreuzten Kästchen geladen. Der Nutzer kann es natürlich jederzeit wieder deaktivieren.

#### Gruppen strukturieren mit `<fieldset>` und `<legend>`

Wenn du eine Gruppe von zusammengehörigen Checkboxen hast, ist es eine gute Praxis, diese auch visuell und semantisch zu gruppieren. HTML bietet hierfür die Elemente `<fieldset>` und `<legend>`.

*   **`<fieldset>`**: Dieses Element umschließt eine Gruppe von Formularelementen. Browser stellen ein `<fieldset>` standardmäßig oft mit einem Rahmen dar, was die Zusammengehörigkeit der Elemente visuell unterstreicht.
*   **`<legend>`**: Dieses Element dient als Überschrift oder Beschriftung für das `<fieldset>`. Es beschreibt den Zweck der darin enthaltenen Formularelemente.

Diese Kombination ist besonders wertvoll für die Barrierefreiheit. Ein Screenreader wird die `<legend>` vorlesen, bevor er die einzelnen Optionen der Gruppe aufzählt. Das gibt Nutzern mit Sehbehinderungen wichtigen Kontext.

Unser Interessen-Beispiel sieht damit noch professioneller aus:

```html
<form action="/daten-verarbeiten" method="post">
  <fieldset>
    <legend>Welche Themen interessieren dich?</legend>

    <div>
      <input type="checkbox" id="tech" name="interessen" value="technologie">
      <label for="tech">Technologie</label>
    </div>

    <div>
      <input type="checkbox" id="sport" name="interessen" value="sport" checked>
      <label for="sport">Sport</label>
    </div>

    <div>
      <input type="checkbox" id="kultur" name="interessen" value="kultur">
      <label for="kultur">Kultur</label>
    </div>
  </fieldset>
  
  <button type="submit">Auswahl absenden</button>
</form>
```

Hier haben wir die Checkboxen und ihre Labels in einem `<fieldset>` zusammengefasst und mit einer `<legend>` versehen. Die `<div>`-Elemente dienen der Strukturierung, damit jede Checkbox-Label-Paarung in einer eigenen Zeile steht – eine gängige und saubere Praxis, die sich mit CSS gut gestalten lässt.

#### Weitere nützliche Attribute: `disabled` und `required`

Zwei weitere Attribute können im Kontext von Checkboxen relevant sein:

*   **`disabled`**: Wenn du dieses boolesche Attribut zu einer Checkbox hinzufügst, wird sie ausgegraut und kann vom Nutzer nicht mehr verändert werden. Das ist nützlich, wenn eine Option unter bestimmten Umständen nicht verfügbar sein soll.

    ```html
    <input type="checkbox" id="premium" name="features" value="premium" disabled>
    <label for="premium">Premium-Funktion (nur für Pro-Nutzer)</label>
    ```

*   **`required`**: Dieses Attribut stellt sicher, dass ein Formularfeld ausgefüllt werden muss. Bei einer einzelnen Checkbox, wie z. B. der Zustimmung zu den AGB, ist die Verwendung einfach: Der Nutzer muss das Kästchen ankreuzen, um das Formular abschicken zu können.

    ```html
    <input type="checkbox" id="agb" name="agb_zugestimmt" value="true" required>
    <label for="agb">Ich habe die Allgemeinen Geschäftsbedingungen gelesen und stimme ihnen zu.</label>
    ```

Bei einer Gruppe von Checkboxen verhält sich `required` anders als man vielleicht erwarten würde. Es stellt nicht sicher, dass *mindestens eine* aus der Gruppe ausgewählt wird. Wenn du das `required`-Attribut auf eine Checkbox in einer Gruppe anwendest, muss genau *diese eine* Checkbox ausgewählt werden. Die Anforderung "Wähle mindestens eine Option" muss typischerweise mit JavaScript umgesetzt werden.

Checkboxen sind ein grundlegendes, aber mächtiges Werkzeug in der Welt der HTML-Formulare. Sie bieten die notwendige Flexibilität für alle Szenarien, in denen eine Mehrfachauswahl erwünscht ist, und sind mit den richtigen Begleitelementen wie `<label>` und `<fieldset>` sowohl benutzerfreundlich als auch barrierefrei umsetzbar.
