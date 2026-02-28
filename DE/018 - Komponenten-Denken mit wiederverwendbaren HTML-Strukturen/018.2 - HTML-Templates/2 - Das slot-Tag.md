# Das slot-Tag

### Das `<slot>`-Tag: Platzhalter für deine eigenen Inhalte

Stell dir vor, du baust eine wiederverwendbare Komponente, zum Beispiel eine schöne Profilkarte. Diese Karte soll immer denselben Rahmen, dieselbe Schriftart und dieselben Abstände haben. Das ist der Kerngedanke hinter wiederverwendbaren HTML-Strukturen, die wir mit dem `<template>`-Tag kennengelernt haben. Aber was ist mit dem Inhalt? Der Name, das Bild und die Biografie auf der Karte sind bei jeder Verwendung anders.

Genau hier kommt das `<slot>`-Tag ins Spiel. Es ist das Herzstück der Flexibilität von Web Components. Ein `<slot>` ist im Grunde ein Platzhalter innerhalb deines Komponententemplates. Du definierst damit eine "Lücke", in die der Nutzer deiner Komponente seinen eigenen, individuellen HTML-Inhalt einfügen kann. Dieser Prozess, bei dem externer Inhalt in die interne Struktur einer Komponente "projiziert" wird, nennt sich Content Projection.

#### Der einfachste Fall: Der Standard-Slot

Um zu verstehen, wie das funktioniert, müssen wir das `<slot>`-Tag im Kontext von Web Components betrachten, also in Verbindung mit einem `<template>` und etwas JavaScript, das ein Custom Element definiert.

Nehmen wir an, wir wollen eine einfache `info-box`-Komponente erstellen. Sie soll einen festen Rahmen und eine feste Überschrift haben, aber der Text im Inneren soll bei jeder Verwendung frei wählbar sein.

Zuerst definieren wir das Template für unsere Komponente:

```html
<template id="info-box-template">
  <style>
    .box {
      border: 2px solid steelblue;
      border-radius: 8px;
      padding: 16px;
      margin: 1em 0;
      font-family: sans-serif;
    }
    h3 {
      margin: 0 0 10px 0;
      color: steelblue;
    }
  </style>
  <div class="box">
    <h3>Wichtige Information</h3>
    <slot></slot>
  </div>
</template>
```

In diesem Template siehst du das entscheidende Element: `<slot></slot>`. Es ist der Platzhalter. Alles, was wir später zwischen die öffnenden und schließenden Tags unserer fertigen Komponente schreiben, wird genau an dieser Stelle eingefügt.

Nun registrieren wir unser Custom Element mit JavaScript, damit der Browser weiß, was er mit `<info-box>` anfangen soll:

```javascript
class InfoBox extends HTMLElement {
  constructor() {
    super();
    // Shadow DOM anhängen, um die Inhalte zu kapseln
    const shadow = this.attachShadow({ mode: 'open' });
    
    // Das Template holen
    const template = document.getElementById('info-box-template');
    const templateContent = template.content;
    
    // Den geklonten Inhalt des Templates an das Shadow DOM anhängen
    shadow.appendChild(templateContent.cloneNode(true));
  }
}

customElements.define('info-box', InfoBox);
```

Jetzt können wir unsere Komponente im HTML verwenden. Und das ist der magische Teil: Der Inhalt, den wir hineinschreiben, landet automatisch im Slot.

```html
<info-box>
  <p>Dies ist eine wichtige Nachricht, die du hier platzieren kannst.</p>
  <p>Du kannst sogar <strong>mehrere</strong> HTML-Elemente einfügen. Sie werden alle in den Slot projiziert.</p>
</info-box>

<info-box>
  <ul>
    <li>Punkt 1</li>
    <li>Punkt 2</li>
  </ul>
</info-box>
```

Wenn du dir das Ergebnis im Browser ansiehst, wirst du feststellen, dass der Browser die Struktur aus dem Template (den `div`-Rahmen und die `h3`-Überschrift) mit dem Inhalt kombiniert, den du in die `<info-box>`-Tags geschrieben hast. Der Absatz und die Liste werden genau dort gerendert, wo im Template das `<slot>`-Tag stand.

Dieser namenlose Slot wird auch als "Default Slot" oder "Standard-Slot" bezeichnet. Er fängt jeden Inhalt auf, der nicht explizit einem anderen Slot zugewiesen wurde.

#### Mehr Struktur mit benannten Slots (Named Slots)

Eine Komponente hat oft mehrere Bereiche, die mit individuellem Inhalt gefüllt werden sollen. Denk an eine typische Karte: Sie hat einen Kopfbereich (Header), einen Hauptbereich (Body) und einen Fußbereich (Footer). Ein einziger Slot reicht hier nicht aus.

Für diesen Zweck können wir Slots benennen, indem wir ihnen ein `name`-Attribut geben.

Erweitern wir unser Beispiel zu einer `person-card`. Das Template könnte so aussehen:

```html
<template id="person-card-template">
  <style>
    /* ... (Styling für die Karte) ... */
    .card { border: 1px solid #ccc; border-radius: 10px; padding: 20px; box-shadow: 2px 2px 8px rgba(0,0,0,0.1); }
    .header { border-bottom: 1px solid #eee; padding-bottom: 10px; margin-bottom: 15px; }
    .footer { border-top: 1px solid #eee; padding-top: 10px; margin-top: 15px; font-size: 0.9em; }
  </style>
  <div class="card">
    <div class="header">
      <slot name="card-header"></slot>
    </div>
    <div class="content">
      <slot></slot> <!-- Der Standard-Slot für den Hauptinhalt -->
    </div>
    <div class="footer">
      <slot name="card-footer"></slot>
    </div>
  </div>
</template>
```

Wir haben jetzt drei Slots:
1.  `<slot name="card-header">`: Ein benannter Slot für den Kopfbereich.
2.  `<slot>`: Der Standard-Slot für den Hauptinhalt.
3.  `<slot name="card-footer">`: Ein benannter Slot für den Fußbereich.

Um nun bei der Verwendung der Komponente zu steuern, welcher Inhalt in welchen Slot gehört, verwenden wir das `slot`-Attribut auf den HTML-Elementen, die wir einfügen möchten.

Hier ist die dazugehörige JavaScript-Klasse (sehr ähnlich wie zuvor):

```javascript
class PersonCard extends HTMLElement {
  constructor() {
    super();
    this.attachShadow({ mode: 'open' });
    this.shadowRoot.appendChild(document.getElementById('person-card-template').content.cloneNode(true));
  }
}

customElements.define('person-card', PersonCard);
```

Und so verwendest du die Komponente mit den benannten Slots:

```html
<person-card>
  <h2 slot="card-header">Max Mustermann</h2>
  
  <!-- Dieser Inhalt hat kein slot-Attribut und landet im Standard-Slot -->
  <p>Web-Entwickler mit einer Leidenschaft für sauberen Code und gutes Design.</p>
  <img src="pfad/zum/bild.jpg" alt="Profilbild von Max">
  
  <div slot="card-footer">
    <a href="#">Kontakt</a> | <a href="#">Portfolio</a>
  </div>
</person-card>
```

Jedes Element mit einem `slot`-Attribut wird in den gleichnamigen `<slot>` im Template projiziert. Das `h2`-Element landet im "card-header"-Slot und der `div` mit den Links im "card-footer"-Slot. Alle Elemente ohne `slot`-Attribut – in diesem Fall der Absatz und das Bild – werden gesammelt und in den namenlosen Standard-Slot eingefügt.

#### Fallback-Inhalt: Was, wenn nichts geliefert wird?

Manchmal möchtest du, dass deine Komponente auch dann sinnvoll aussieht, wenn ein Nutzer vergisst, Inhalt für einen bestimmten Slot bereitzustellen. Du kannst direkt im Template einen Standardinhalt (Fallback Content) definieren. Dieser wird genau dann angezeigt, wenn für diesen Slot kein Inhalt von außen bereitgestellt wird.

Dazu schreibst du den Fallback-Inhalt einfach zwischen die `<slot>`-Tags:

```html
<template id="person-card-template-mit-fallback">
  <!-- ... (styles) ... -->
  <div class="card">
    <div class="header">
      <slot name="card-header">
        <h3>Unbenannte Person</h3>
      </slot>
    </div>
    <div class="content">
      <slot>
        <p>Keine Biografie verfügbar.</p>
      </slot>
    </div>
    <div class="footer">
      <slot name="card-footer">
        <p>Keine weiteren Informationen.</p>
      </slot>
    </div>
  </div>
</template>
```

Wenn du jetzt eine `<person-card>` verwendest und zum Beispiel den Footer weglässt, wird automatisch der Text "Keine weiteren Informationen" angezeigt.

```html
<!-- Diese Karte hat keinen Footer-Inhalt -->
<person-card>
  <h2 slot="card-header">Anna Schmidt</h2>
  <p>UX-Designerin aus Berlin.</p>
</person-card>
```

Das Ergebnis wäre eine Karte mit dem Namen und der Biografie, aber im Fußbereich würde der Fallback-Inhalt aus dem Template erscheinen. Dies macht deine Komponenten robuster und fehlertoleranter.

#### Styling von projizierten Inhalten

Eine der größten Stärken des Shadow DOM ist die Stil-Kapselung. Die CSS-Regeln innerhalb deines `<style>`-Tags im Template gelten nur für die Elemente im Shadow DOM und beeinflussen nicht die Hauptseite. Umgekehrt gelten die Stile der Hauptseite nicht für die Elemente im Shadow DOM.

Aber was ist mit dem Inhalt, den wir per `<slot>` hineinprojizieren? Dieser Inhalt "lebt" technisch gesehen im normalen DOM (dem Light DOM), wird aber im Shadow DOM angezeigt. Das wirft eine interessante Frage auf: Wo wird er gestylt?

Die Antwort ist: an beiden Orten, aber auf unterschiedliche Weise.

1.  **Styling durch den Nutzer:** Der Nutzer, der die Komponente verwendet, kann den projizierten Inhalt ganz normal mit den CSS-Regeln seiner Hauptseite stylen. Wenn er ein `<p>` in einen Slot einfügt, greifen die globalen `p`-Regeln der Seite.
2.  **Styling durch den Komponenten-Autor:** Als Autor der Komponente möchtest du vielleicht bestimmte Stile für die projizierten Elemente vorgeben, damit sie sich nahtlos in das Design deiner Komponente einfügen. Du kannst aber nicht einfach `p { color: red; }` im Shadow DOM schreiben, denn das würde nur für `<p>`-Elemente gelten, die Teil deines Templates sind, nicht für projizierte.

Hierfür gibt es die CSS-Pseudo-Klasse `::slotted()`. Mit ihr kannst du aus dem Shadow DOM heraus die Elemente stylen, die in einen Slot projiziert wurden.

```css
/* Innerhalb des <style>-Tags im Template */
::slotted(h2) {
  /* Diese Regel gilt für jedes h2-Element, das in irgendeinen Slot projiziert wird */
  font-size: 1.5em;
  color: #333;
  margin: 0;
}

::slotted([slot="card-footer"]) {
  /* Diese Regel gilt für das Element, das in den "card-footer"-Slot projiziert wird */
  display: flex;
  justify-content: space-around;
}
```

Mit `::slotted()` baust du eine Brücke zwischen der gekapselten Welt deines Shadow DOM und der Außenwelt. Es erlaubt dir, die Top-Level-Elemente, die in einen Slot eingefügt werden, gezielt anzusprechen. Beachte jedoch, dass `::slotted()` nur diese direkten Elemente ansprechen kann. Du kannst damit nicht tiefer in die Struktur des projizierten Inhalts eingreifen (z.B. ein `<span>` innerhalb eines projizierten `<p>`). Diese Beschränkung ist beabsichtigt: Sie bewahrt die Kapselung und sorgt für eine klare Trennung der Verantwortlichkeiten zwischen Komponenten-Autor und Komponenten-Nutzer.

Das `<slot>`-Element ist somit weit mehr als nur ein einfaches Tag. Es ist ein mächtiges Konzept, das die starren Strukturen von Templates aufbricht und sie in flexible, anpassbare und wirklich wiederverwendbare Bausteine für moderne Webanwendungen verwandelt.
