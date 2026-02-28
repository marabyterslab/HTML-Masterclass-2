# Delegation von Events

### Delegation von Events: Effizientes Event-Handling für dynamische Inhalte

Stell dir vor, du baust eine interaktive To-do-Liste. Jedes Element in dieser Liste soll durchgestrichen werden können, sobald du darauf klickst. Ein erster, naheliegender Ansatz wäre, jedem einzelnen Listenelement einen eigenen Event-Listener hinzuzufügen.

```html
<ul id="todo-liste">
  <li>Wäsche waschen</li>
  <li>Einkaufen gehen</li>
  <li>JavaScript lernen</li>
</ul>
```

Mit JavaScript könntest du nun alle `<li>`-Elemente auswählen und jedem eine Funktion für das `click`-Event zuweisen.

```javascript
// Der "naive" Ansatz
const listItems = document.querySelectorAll('#todo-liste li');

listItems.forEach(item => {
  item.addEventListener('click', function() {
    item.style.textDecoration = 'line-through';
  });
});
```

Dieser Ansatz funktioniert. Aber er hat zwei wesentliche Nachteile, die in realen Anwendungen schnell zum Problem werden.

1.  **Performance:** Was ist, wenn deine Liste nicht drei, sondern dreihundert oder dreitausend Einträge hat? Jeder einzelne Event-Listener ist ein Objekt im Speicher deines Browsers. Viele Hunderte davon können die Leistung deiner Seite spürbar beeinträchtigen. Es ist, als würdest du für jeden einzelnen Mitarbeiter in einer riesigen Firma einen eigenen Portier einstellen, anstatt einen am Haupteingang.

2.  **Dynamische Inhalte:** Was passiert, wenn der Benutzer einen neuen To-do-Punkt zur Liste hinzufügt? Das neue `<li>`-Element, das du mit JavaScript erzeugst und in den DOM einfügst, war noch nicht da, als dein initiales Skript lief. Folglich hat es auch keinen Event-Listener. Du müsstest daran denken, jedem neu hinzugefügten Element manuell wieder einen Listener anzuhängen. Das ist umständlich und eine häufige Fehlerquelle.

Hier kommt ein eleganteres und weitaus leistungsfähigeres Konzept ins Spiel: die **Delegation von Events**.

#### Das Prinzip der Delegation

Die Idee hinter der Event-Delegation ist einfach und genial zugleich: Anstatt jedem Kind-Element einen eigenen Event-Listener zu geben, hängst du einen einzigen Listener an ein gemeinsames Eltern-Element.

Dieses Prinzip macht sich ein fundamentales Verhalten von Events im Browser zunutze: das **Event Bubbling**. Wenn ein Event auf einem Element ausgelöst wird – zum Beispiel ein Klick auf ein `<li>` –, dann "hört" nicht nur dieses Element das Event. Nachdem das Event auf dem Ziel (dem `<li>`) ausgelöst wurde, wandert es im DOM-Baum nach oben, von Elternteil zu Elternteil, bis es das `<html>`-Element und schließlich das `document`-Objekt erreicht. Es blubbert quasi wie eine Luftblase an die Oberfläche.

Bei der Delegation fangen wir dieses "blubbernde" Event auf einer höheren Ebene ab, zum Beispiel auf dem `<ul>`-Element. Der Listener auf dem `<ul>` wird also auch dann ausgelöst, wenn du auf eines seiner `<li>`-Kinder klickst.

Der entscheidende Trick dabei ist, innerhalb der Event-Handler-Funktion herauszufinden, welches Kind-Element das Event ursprünglich ausgelöst hat.

#### Die Umsetzung in der Praxis

Schauen wir uns unsere To-do-Liste erneut an, diesmal mit dem Delegations-Ansatz. Wir fügen noch einen Button hinzu, um neue Aufgaben zu erstellen und das Problem der dynamischen Inhalte zu demonstrieren.

```html
<ul id="todo-liste">
  <li>Wäsche waschen</li>
  <li>Einkaufen gehen</li>
  <li>JavaScript lernen</li>
</ul>
<button id="neue-aufgabe">Neue Aufgabe hinzufügen</button>
```

Jetzt schreiben wir das JavaScript. Anstatt alle `<li>`-Elemente zu selektieren, nehmen wir uns nur das übergeordnete `<ul>`-Element und hängen unseren einzigen Event-Listener dort an.

```javascript
const todoListe = document.getElementById('todo-liste');

todoListe.addEventListener('click', function(event) {
  // Wer hat das Event ausgelöst?
  console.log(event.target);
});
```

Wenn du jetzt auf eines der Listenelemente klickst, siehst du in der Konsole das jeweilige `<li>`-Element. Der `event`-Parameter, der automatisch an jede Event-Handler-Funktion übergeben wird, ist hier unser wichtigstes Werkzeug. Die Eigenschaft `event.target` verweist immer auf das Element, das das Event ursprünglich ausgelöst hat – also genau das Element, das uns interessiert. `event.currentTarget` würde hingegen auf das Element verweisen, an dem der Listener hängt – in diesem Fall das `<ul>`.

Jetzt haben wir aber ein kleines Problem: Was passiert, wenn du in den Leerraum zwischen den `<li>`-Elementen klickst? Das `click`-Event wird trotzdem ausgelöst, weil du ja immer noch in das `<ul>`-Element klickst. In diesem Fall wäre `event.target` das `<ul>`-Element selbst. Wir wollen unsere Logik aber nur ausführen, wenn tatsächlich auf ein `<li>` geklickt wurde.

Wir müssen also filtern. Wir prüfen, ob das `event.target` das Element ist, auf das wir reagieren wollen. Eine sehr saubere Methode dafür ist die `matches()`-Methode, die auf jedem Element verfügbar ist.

```javascript
const todoListe = document.getElementById('todo-liste');

todoListe.addEventListener('click', function(event) {
  // Prüfe, ob das geklickte Element ein <li> innerhalb unserer Liste ist.
  if (event.target && event.target.matches('li')) {
    // Ja, es war ein Listenelement! Jetzt können wir damit arbeiten.
    event.target.style.textDecoration = 'line-through';
    console.log('Aufgabe erledigt:', event.target.textContent);
  }
});
```

Mit dieser `if`-Bedingung stellen wir sicher, dass unser Code nur dann ausgeführt wird, wenn das Event von einem `<li>`-Element stammt. Klicks auf den Hintergrund der Liste werden elegant ignoriert.

#### Die wahre Stärke: Umgang mit dynamischen Inhalten

Jetzt kommt der Moment, in dem die Event-Delegation ihre volle Stärke ausspielt. Fügen wir die Funktionalität für unseren Button hinzu, um neue Aufgaben zu erstellen.

```javascript
const neueAufgabeButton = document.getElementById('neue-aufgabe');
let aufgabenZaehler = 3;

neueAufgabeButton.addEventListener('click', function() {
  aufgabenZaehler++;
  const neueAufgabe = document.createElement('li');
  neueAufgabe.textContent = `Neue Aufgabe Nr. ${aufgabenZaehler}`;
  todoListe.appendChild(neueAufgabe);
});
```

Wenn du nun auf den Button klickst, wird ein neues `<li>`-Element erzeugt und an die Liste angehängt. Und jetzt das Beste: Klicke auf dieses brandneue Element. Es funktioniert! Es wird sofort durchgestrichen.

Warum? Weil es uns völlig egal ist, wie viele `<li>`-Elemente in der Liste sind oder wann sie hinzugefügt wurden. Unser einziger Event-Listener sitzt geduldig auf dem `<ul>`-Elternteil und wartet. Sobald ein Klick von einem seiner Nachkommen nach oben "blubbert", fängt er ihn ab, prüft mit `event.target.matches('li')`, ob es sich um ein Listenelement handelt, und führt dann die Logik aus. Wir müssen uns nie wieder Gedanken darüber machen, neuen Elementen manuell Event-Listener hinzuzufügen.

#### Vorteile der Event-Delegation

Fassen wir die Vorteile dieses Musters noch einmal zusammen.

Erstens sparst du erheblich an **Speicher und Rechenleistung**. Ein einziger Event-Listener für potenziell Tausende von Elementen ist deutlich effizienter als Tausende einzelner Listener. Bei sehr großen und komplexen Webanwendungen ist dies ein entscheidender Faktor für eine flüssige Benutzererfahrung.

Zweitens wird dein **Code einfacher und wartbarer**. Die Logik für die Event-Behandlung ist an einem zentralen Ort gebündelt. Du musst nicht mehr an verschiedenen Stellen deines Codes daran denken, Event-Listener hinzuzufügen oder – was oft vergessen wird – auch wieder zu entfernen, wenn Elemente aus dem DOM verschwinden.

Drittens gewinnst du eine enorme **Flexibilität**. Dein Code funktioniert automatisch für Inhalte, die zu einem späteren Zeitpunkt per AJAX nachgeladen oder vom Benutzer dynamisch erzeugt werden.

#### Gibt es auch Nachteile?

Die Event-Delegation ist ein mächtiges Werkzeug, aber nicht für jede Situation die perfekte Lösung. Ein wichtiger Punkt ist, dass nicht alle Events "bubblen". Events wie `focus`, `blur` oder `load` steigen nicht im DOM-Baum auf und können daher nicht auf diese Weise delegiert werden. Für die meisten Interaktions-Events wie `click`, `mousedown`, `keyup` oder `mouseover` funktioniert die Delegation jedoch einwandfrei.

Wenn du in einem Kind-Element die Event-Propagation bewusst mit `event.stopPropagation()` unterbrichst, wird das Event den delegierten Listener auf dem Eltern-Element nie erreichen. Das kann beabsichtigt sein, aber man muss es im Hinterkopf behalten, da es zu schwer auffindbaren Fehlern führen kann.

In den allermeisten Anwendungsfällen, insbesondere bei Listen, Tabellen, Galerien oder jedem anderen Container mit vielen gleichartigen, interaktiven Kind-Elementen, ist die Event-Delegation jedoch der überlegene Ansatz. Sie ist ein klares Zeichen für sauberen, effizienten und zukunftssicheren JavaScript-Code.
