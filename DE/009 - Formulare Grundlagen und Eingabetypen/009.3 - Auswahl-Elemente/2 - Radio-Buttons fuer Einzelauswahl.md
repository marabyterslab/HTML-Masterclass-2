# Radio-Buttons für Einzelauswahl

### 9.3 Radio-Buttons für die Einzelauswahl

Stell dir vor, du füllst ein Online-Formular aus und wirst gefragt, wie du kontaktiert werden möchtest: per E-Mail, Telefon oder Post. Von diesen Optionen kannst du logischerweise nur eine auswählen. Genau für solche Fälle, in denen eine exklusive Auswahl aus einer Gruppe von Möglichkeiten getroffen werden muss, wurden Radio-Buttons entwickelt.

Der Name „Radio-Button“ ist eine wunderbare Anspielung auf die alten Autoradios. Dort gab es physische Knöpfe für verschiedene Sender. Wenn du einen Knopf gedrückt hast, sprang der zuvor gedrückte wieder heraus. Es war unmöglich, zwei Sender gleichzeitig ausgewählt zu haben. Dieses Prinzip der „Einer-oder-keiner“-Auswahl (genauer gesagt: „genau einer aus der Gruppe muss gewählt werden“) ist das Herzstück des Radio-Buttons in HTML. Er steht im direkten Gegensatz zur Checkbox, bei der du beliebig viele Optionen aus einer Gruppe ankreuzen kannst.

#### Die grundlegende Struktur

Ein Radio-Button wird, wie viele andere Formularelemente auch, mit dem `<input>`-Tag erstellt. Der entscheidende Unterschied liegt im `type`-Attribut, das hier auf den Wert `radio` gesetzt wird.

Die Magie, die mehrere einzelne Radio-Buttons zu einer funktionierenden Gruppe verbindet, liegt im `name`-Attribut. **Alle Radio-Buttons, die zu derselben Auswahlgruppe gehören, müssen exakt denselben Wert im `name`-Attribut haben.** Nur so weiß der Browser, dass diese Elemente zusammengehören und dass nur eines davon gleichzeitig ausgewählt sein kann.

Ein weiteres unverzichtbares Attribut ist `value`. Während der Text neben dem Radio-Button dem Benutzer beschreibt, wofür die Option steht, enthält das `value`-Attribut den tatsächlichen Wert, der an den Server gesendet wird, wenn das Formular abgeschickt wird. Dieser Wert ist für den Benutzer nicht direkt sichtbar, aber für die serverseitige Verarbeitung essenziell.

Schauen wir uns ein minimales Beispiel an:

```html
<form action="/verarbeitung" method="post">
  <p>Bevorzugte Kontaktmethode:</p>
  
  <input type="radio" id="kontakt-email" name="kontaktart" value="email">
  <label for="kontakt-email">E-Mail</label><br>
  
  <input type="radio" id="kontakt-telefon" name="kontaktart" value="telefon">
  <label for="kontakt-telefon">Telefon</label><br>
  
  <input type="radio" id="kontakt-post" name="kontaktart" value="post">
  <label for="kontakt-post">Post</label>
</form>
```

In diesem Code-Beispiel siehst du drei Radio-Buttons.
1.  **`type="radio"`**: Definiert sie als Radio-Buttons.
2.  **`name="kontaktart"`**: Dieses Attribut ist bei allen drei `input`-Elementen identisch. Das macht sie zu einer Gruppe. Wenn du auf "Telefon" klickst, wird die Auswahl bei "E-Mail" (falls sie vorher aktiv war) automatisch entfernt.
3.  **`value`**: Wenn der Benutzer "E-Mail" auswählt und das Formular abschickt, wird der Datenpunkt `kontaktart=email` an den Server gesendet. Wählt er "Telefon", wird `kontaktart=telefon` gesendet.

#### Die entscheidende Rolle des `<label>`-Elements

Du hast im obigen Beispiel bereits das `<label>`-Tag gesehen. Seine Bedeutung kann gar nicht hoch genug eingeschätzt werden. Ein `<label>` verknüpft ein Stück Text mit einem bestimmten Formularelement. Diese Verknüpfung hat zwei riesige Vorteile:

1.  **Benutzerfreundlichkeit (Usability):** Durch die Verknüpfung wird der Klickbereich des kleinen Radio-Buttons enorm vergrößert. Der Benutzer muss nicht mehr den winzigen Kreis treffen, sondern kann bequem auf den dazugehörigen Text klicken, um die Option auszuwählen. Das ist besonders auf Touch-Geräten ein Segen.
2.  **Barrierefreiheit (Accessibility):** Screenreader, die von sehbehinderten Menschen genutzt werden, verwenden das `<label>`, um vorzulesen, wofür ein Formularelement steht. Ohne ein korrekt verknüpftes Label wüsste der Benutzer nicht, welche Option er gerade ausgewählt hat.

Die Verknüpfung wird über das `for`-Attribut im `<label>` und das `id`-Attribut im `<input>`-Tag hergestellt. Der Wert des `for`-Attributs muss exakt mit dem Wert des `id`-Attributs des zugehörigen `input`-Elements übereinstimmen. Jede `id` auf einer Webseite muss einzigartig sein!

#### Gruppierung mit `<fieldset>` und `<legend>`

Um eine Gruppe von Radio-Buttons nicht nur funktional, sondern auch semantisch und visuell zu bündeln, solltest du die Elemente `<fieldset>` und `<legend>` verwenden.

*   Das `<fieldset>`-Element umschließt die gesamte Gruppe von zusammengehörigen Formularelementen. Browser stellen dies oft standardmäßig mit einem dünnen Rahmen dar.
*   Das `<legend>`-Element dient als Überschrift oder Beschriftung für das `<fieldset>`. Es beschreibt die Frage oder den Zweck der Optionsgruppe.

Dies verbessert die Struktur deines HTML-Codes und hilft assistiven Technologien dabei, den Kontext der Formularfelder besser zu verstehen.

Hier ist unser vorheriges Beispiel, nun semantisch korrekt ausgezeichnet:

```html
<form action="/verarbeitung" method="post">
  <fieldset>
    <legend>Wie möchtest du am liebsten kontaktiert werden?</legend>
    
    <div>
      <input type="radio" id="kontakt-email" name="kontaktart" value="email">
      <label for="kontakt-email">Per E-Mail</label>
    </div>
    
    <div>
      <input type="radio" id="kontakt-telefon" name="kontaktart" value="telefon">
      <label for="kontakt-telefon">Per Telefon</label>
    </div>
    
    <div>
      <input type="radio" id="kontakt-post" name="kontaktart" value="post">
      <label for="kontakt-post">Per Post</label>
    </div>
  </fieldset>
</form>
```
Ich habe hier zusätzlich `<div>`-Container um jedes `input`/`label`-Paar gelegt. Das ist eine gängige Praxis, um die einzelnen Optionen besser strukturieren und mit CSS gestalten zu können, zum Beispiel um sie untereinander anzuzeigen.

#### Eine Option vorselektieren

Manchmal möchtest du dem Benutzer eine Standardoption oder eine empfohlene Wahl vorgeben. Dafür gibt es das boolesche `checked`-Attribut. Du fügst es einfach zu dem `<input>`-Tag hinzu, das standardmäßig ausgewählt sein soll.

```html
<input type="radio" id="kontakt-email" name="kontaktart" value="email" checked>
<label for="kontakt-email">Per E-Mail</label>
```

Beim Laden der Seite wäre in diesem Fall die Option „Per E-Mail“ bereits ausgewählt. Der Benutzer kann seine Auswahl natürlich jederzeit ändern.

Achte darauf, das `checked`-Attribut nur bei **einem einzigen** Radio-Button innerhalb einer Gruppe zu verwenden. Solltest du es fälschlicherweise bei mehreren Buttons einer Gruppe notieren, wird der Browser in der Regel den letzten im Quellcode gefundenen Button als ausgewählt darstellen.

#### Weitere nützliche Attribute

Wie bei anderen Eingabeelementen auch, kannst du bei Radio-Buttons weitere Attribute nutzen, um ihr Verhalten zu steuern.

*   **`disabled`**: Wenn du eine bestimmte Option vorübergehend oder dauerhaft deaktivieren möchtest, kannst du das `disabled`-Attribut verwenden. Ein deaktivierter Radio-Button wird typischerweise ausgegraut dargestellt, kann nicht angeklickt werden und sein Wert wird beim Absenden des Formulars nicht mitgeschickt.

    ```html
    <input type="radio" id="kontakt-post" name="kontaktart" value="post" disabled>
    <label for="kontakt-post">Per Post (derzeit nicht verfügbar)</label>
    ```

*   **`required`**: Um sicherzustellen, dass der Benutzer eine Auswahl in einer Gruppe treffen muss, bevor er das Formular absenden kann, fügst du das `required`-Attribut zu **mindestens einem** der Radio-Buttons in der Gruppe hinzu. Es ist üblich, es zum ersten Element der Gruppe zu schreiben, aber funktional ist es egal, bei welchem es steht. Sobald ein Element in der Gruppe `required` ist, gilt die Anforderung für die gesamte Gruppe. Der Benutzer muss eine der Optionen auswählen.

    ```html
    <input type="radio" id="zustimmung-ja" name="agb" value="ja" required>
    <label for="zustimmung-ja">Ja, ich stimme zu.</label>
    ```

Radio-Buttons sind ein fundamentaler Baustein interaktiver Webformulare. Ihre korrekte Implementierung mit den Attributen `name`, `value` und verknüpften `<label>`-Elementen ist entscheidend für eine gute Benutzererfahrung und eine saubere Datenverarbeitung.
