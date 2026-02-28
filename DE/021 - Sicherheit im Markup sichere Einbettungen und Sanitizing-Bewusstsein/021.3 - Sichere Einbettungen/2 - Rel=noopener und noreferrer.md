# Rel=noopener und noreferrer

### Sichere Links in neuen Tabs: Die Wichtigkeit von `rel="noopener"` und `rel="noreferrer"`

Fast jeder, der eine Webseite baut, kennt und nutzt das `target`-Attribut bei Links. Insbesondere der Wert `_blank` ist ein alter Bekannter. Du verwendest ihn, um einen Link in einem neuen Browser-Tab oder -Fenster zu öffnen. Das ist praktisch, denn so bleiben die Besucher auf deiner Seite, während sie sich den verlinkten Inhalt ansehen können.

Ein typischer Link dieser Art sieht so aus:

```html
<a href="https://beispiel-externe-seite.com" target="_blank">
  Besuche diese interessante externe Seite!
</a>
```

Auf den ersten Blick wirkt das harmlos und nützlich. Doch hinter diesem einfachen Attribut verbirgt sich eine potenzielle Sicherheitslücke, die lange Zeit übersehen wurde und die du unbedingt kennen und verstehen solltest.

#### Die versteckte Gefahr: `window.opener` und Tabnabbing

Wenn du einen Link mit `target="_blank"` öffnest, erhält die neu geöffnete Seite über JavaScript Zugriff auf das Fensterobjekt der ursprünglichen Seite. Dies geschieht über die Eigenschaft `window.opener`. Solange die neu geöffnete Seite zur selben Domain gehört wie deine, ist das meist unproblematisch und manchmal sogar gewollt.

Wenn du jedoch auf eine externe, fremde Seite verlinkst, gibst du dieser Seite eine gewisse Kontrolle über den Tab, aus dem sie geöffnet wurde. Die externe Seite kann dann über `window.opener` auf deine Seite zugreifen und sie manipulieren. Die gefährlichste Manipulation ist die Änderung der URL deiner Seite.

Stell dir folgendes Szenario vor, das als "Tabnabbing" bekannt ist:

1.  Ein Nutzer ist auf deiner vertrauenswürdigen Webseite `deine-seite.de` eingeloggt.
2.  Er klickt auf einen Link zu `externe-boesartige-seite.com`, der sich in einem neuen Tab öffnet. Der Link ist mit `target="_blank"`, aber ohne weitere Sicherheitsattribute gesetzt.
3.  Während der Nutzer sich auf dem neuen Tab umsieht, führt die bösartige Seite im Hintergrund unbemerkt JavaScript-Code aus. Dieser Code greift auf `window.opener` zu und ändert die URL deiner ursprünglichen Seite.

Der bösartige JavaScript-Code könnte so simpel sein:

```javascript
// Dieser Code läuft auf der externen, bösartigen Seite
if (window.opener) {
  // Leite die ursprüngliche Seite auf eine Phishing-Seite um
  window.opener.location = "https://fake-login.deine-seite.de";
}
```

4.  Der Nutzer schließt den Tab mit der externen Seite und kehrt zu deinem Tab zurück. Er bemerkt nicht, dass sich die Seite im Hintergrund geändert hat. Statt deiner echten App sieht er nun eine exakte Kopie deiner Login-Seite.
5.  Da er davon ausgeht, dass seine Sitzung abgelaufen ist, gibt er arglos seine Zugangsdaten ein. Diese werden direkt an den Angreifer gesendet.

Dieses Szenario ist erschreckend effektiv, weil es auf dem Vertrauen des Nutzers zu deiner Seite aufbaut. Der Nutzer befindet sich die ganze Zeit im selben Browser-Tab, in dem deine Seite ursprünglich geladen war, und die URL in der Adresszeile kann so gefälscht sein, dass sie echt aussieht.

#### Die Lösung, Teil 1: `rel="noopener"`

Um diese Sicherheitslücke zu schließen, wurde das `rel`-Attribut um den Wert `noopener` erweitert. Wenn du dieses Attribut zu deinem Link hinzufügst, wird die `window.opener`-Eigenschaft im neu geöffneten Tab auf `null` gesetzt. Die neue Seite hat somit keine Referenz und keinen Zugriff mehr auf deine Seite. Die Verbindung wird gekappt.

Die korrigierte, sichere Version des Links sieht so aus:

```html
<a href="https://beispiel-externe-seite.com" target="_blank" rel="noopener">
  Besuche diese interessante externe Seite! (Jetzt sicher)
</a>
```

Damit hast du die Tabnabbing-Gefahr vollständig gebannt. Die externe Seite kann deine Seite nicht mehr manipulieren.

Es gibt noch einen weiteren, positiven Nebeneffekt: In manchen Browsern können Seiten, die über `window.opener` verbunden sind, im selben Prozess laufen. Wenn die neu geöffnete Seite rechenintensive JavaScript-Operationen ausführt, kann das die Performance deiner eigenen Seite beeinträchtigen. `noopener` kann auch hier helfen, indem es die Prozesse voneinander isoliert und so die Performance deiner Seite schützt.

#### Die Lösung, Teil 2: `rel="noreferrer"`

Neben `noopener` gibt es noch einen weiteren nützlichen Wert für das `rel`-Attribut: `noreferrer`. Dieser Wert löst ein anderes, datenschutzrelevantes Problem.

Wenn ein Nutzer von einer Seite A auf eine Seite B klickt, sendet der Browser standardmäßig einen sogenannten `Referer`-HTTP-Header an den Server von Seite B. Dieser Header enthält die URL der Herkunftsseite (Seite A). Das ist für Webseitenbetreiber nützlich, um zu analysieren, woher ihre Besucher kommen.

In manchen Fällen möchtest du diese Information aber vielleicht nicht preisgeben, zum Beispiel aus Datenschutzgründen oder wenn die URL deiner Seite sensible Informationen enthält (was generell vermieden werden sollte, aber vorkommen kann).

Der Wert `noreferrer` weist den Browser an, diesen `Referer`-Header wegzulassen. Die Zielseite erfährt also nicht, von welcher Seite der Nutzer gekommen ist.

Das Wichtigste an `noreferrer` im Kontext der Sicherheit ist jedoch: **`noreferrer` beinhaltet implizit auch das Verhalten von `noopener`**. Ein Link mit `rel="noreferrer"` setzt also ebenfalls `window.opener` auf `null` und schützt dich vor Tabnabbing.

Ein Link mit diesem Attribut sieht so aus:

```html
<a href="https://beispiel-externe-seite.com" target="_blank" rel="noreferrer">
  Besuche diese interessante externe Seite! (Sicher und privat)
</a>
```

#### Die goldene Regel: `noopener` und `noreferrer` gemeinsam nutzen

Du fragst dich jetzt vielleicht: Welchen Wert soll ich nun verwenden? `noopener` oder `noreferrer`?

Die etablierte Best Practice ist, beide zu verwenden:

```html
<a href="https://beispiel-externe-seite.com" target="_blank" rel="noopener noreferrer">
  Der sicherste Link zu einer externen Seite
</a>
```

Warum beide, wenn `noreferrer` die Funktion von `noopener` bereits enthält?

1.  **Maximale Kompatibilität:** Es gab in der Vergangenheit sehr alte Browser-Versionen, die zwar `noopener` verstanden, aber `noreferrer` nicht in der gleichen Weise mit der `opener`-Sicherheit verknüpften. Die Angabe beider Werte stellt sicher, dass der Sicherheitsaspekt (`noopener`) und der Datenschutzaspekt (`noreferrer`) so breit wie möglich abgedeckt sind.
2.  **Klarheit und Lesbarkeit:** Wenn ein anderer Entwickler deinen Code liest, macht die explizite Nennung von `noopener` sofort klar, dass du die Sicherheitslücke bedacht hast. Es kommuniziert deine Absicht unmissverständlich.

Daher lautet die klare Empfehlung: **Immer, wenn du `target="_blank"` verwendest, um auf eine Ressource zu verlinken, die du nicht vollständig kontrollierst, füge `rel="noopener noreferrer"` hinzu.**

#### Was moderne Browser heute tun

Die Entwickler der großen Browser haben auf diese Sicherheitslücke reagiert. Inzwischen verhalten sich die meisten modernen Browser (wie Chrome, Firefox, Safari und Edge) so, als ob `rel="noopener"` bei allen Links mit `target="_blank"` standardmäßig gesetzt wäre, selbst wenn du es nicht in deinem HTML-Code angibst.

Das ist eine großartige Verbesserung für die Sicherheit des gesamten Webs. Trotzdem solltest du dich nicht darauf verlassen und das Attribut weglassen. Es gibt gute Gründe, es weiterhin explizit zu setzen:

*   **Abwärtskompatibilität:** Du kannst nie sicher sein, dass alle deine Nutzer die neuste Browser-Version verwenden. Um auch Nutzer mit älteren Browsern zu schützen, ist das explizite Attribut unerlässlich.
*   **Code-Qualität und Werkzeuge:** Viele Code-Linter und Security-Scanner werden dich warnen, wenn du ein `target="_blank"` ohne `rel="noopener"` verwendest. Deinen Code von Anfang an sauber zu schreiben, erspart dir spätere Korrekturen.
*   **`noreferrer` ist nicht standardmäßig:** Das automatische Verhalten der Browser betrifft nur `noopener`. Wenn du auch den `Referer`-Header unterdrücken möchtest, musst du `noreferrer` nach wie vor explizit hinzufügen.

Indem du `rel="noopener noreferrer"` weiterhin manuell setzt, schreibst du robusten, sicheren und zukunftssicheren Code.

#### Gibt es Ausnahmen?

In 99 % der Fälle ist die Regel "immer `noopener noreferrer` bei `target="_blank"`" korrekt. Es gibt jedoch seltene, legitime Anwendungsfälle, in denen du bewusst den Zugriff über `window.opener` benötigst.

Dies ist typischerweise der Fall, wenn du eine Web-Anwendung entwickelst, bei der zwei Fenster, die du beide kontrollierst, miteinander kommunizieren müssen. Ein klassisches Beispiel ist ein Pop-up-Fenster für einen OAuth-Login (z.B. "Login mit Google"), das nach erfolgreicher Authentifizierung eine Nachricht an das Hauptfenster zurücksenden muss, um den Login-Prozess abzuschließen. Ein anderes Beispiel wäre ein Pop-up zur Bildauswahl in einem CMS, das die URL des ausgewählten Bildes an den Editor im Hauptfenster übergibt.

In diesen kontrollierten Szenarien, in denen du sowohl die Quelle als auch das Ziel des Links besitzt und der Funktionalität vertraust, kannst du auf `rel="noopener"` verzichten. Für alle anderen Links, insbesondere solche, die auf externe Webseiten zeigen, ist es ein absolutes Muss.
