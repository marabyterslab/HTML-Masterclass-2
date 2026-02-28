# Warenkorb und Checkout

### Warenkorb und Checkout: Die entscheidenden Schritte zum Kauf

Nachdem sich ein Nutzer durch deinen Online-Shop geklickt, Produkte verglichen und seine Favoriten ausgewählt hat, landet er an der wohl wichtigsten Station seiner Reise: dem Warenkorb und dem anschließenden Checkout. Diese beiden Bereiche sind das Herzstück der Konversion. Hier entscheidet sich, ob aus einem Interessenten ein Käufer wird. Deine Aufgabe als Entwickler ist es, diesen Prozess mit sauberem, semantischem HTML so reibungslos und verständlich wie möglich zu gestalten. Eine unklare Struktur oder ein verwirrendes Formular kann hier den entscheidenden Unterschied zwischen einem abgeschlossenen Kauf und einem verlassenen Warenkorb ausmachen.

#### Der Warenkorb: Die digitale Zwischenablage

Der Warenkorb ist mehr als nur eine Liste. Er ist ein interaktiver Bereich, in dem deine Nutzer ihre Auswahl überprüfen, Mengen anpassen und letzte Änderungen vornehmen können, bevor sie sich zum Kauf verpflichten. Die Darstellung der Informationen sollte daher klar, übersichtlich und intuitiv sein.

Für die Auflistung der Produkte im Warenkorb bietet sich ein HTML-Element an, das für genau solche tabellarischen Daten geschaffen wurde: die Tabelle (`<table>`). Auch wenn Tabellen in der Vergangenheit für das Layout ganzer Webseiten missbraucht wurden, ist dies ihr korrekter semantischer Anwendungsfall. Eine Liste von Produkten mit zugehörigen Eigenschaften wie Menge, Einzelpreis und Gesamtpreis ist eine klassische Datentabelle.

Eine typische Struktur für einen Warenkorb könnte so aussehen:

```html
<div class="shopping-cart">
  <h1>Dein Warenkorb</h1>

  <table class="cart-table">
    <thead>
      <tr>
        <th scope="col">Produkt</th>
        <th scope="col">Menge</th>
        <th scope="col">Einzelpreis</th>
        <th scope="col">Gesamt</th>
        <th scope="col"></th> <!-- Spalte für "Entfernen"-Button -->
      </tr>
    </thead>
    <tbody>
      <!-- Beispiel für ein Produkt im Warenkorb -->
      <tr>
        <td>
          <div class="product-info">
            <img src="bild-vom-produkt.jpg" alt="Vorderansicht eines blauen T-Shirts">
            <div>
              <strong>Blaues T-Shirt</strong>
              <small>Größe: M</small>
            </div>
          </div>
        </td>
        <td>
          <label for="quantity-1" class="visually-hidden">Menge für Blaues T-Shirt</label>
          <input type="number" id="quantity-1" name="quantity-1" value="1" min="1" max="10" aria-label="Menge">
        </td>
        <td>29,99 €</td>
        <td>29,99 €</td>
        <td>
          <button type="button" aria-label="Blaues T-Shirt aus dem Warenkorb entfernen">&times;</button>
        </td>
      </tr>
      <!-- Weitere Produkte würden hier folgen -->
    </tbody>
  </table>

  <div class="cart-summary">
    <h2>Zusammenfassung</h2>
    <dl>
      <dt>Zwischensumme</dt>
      <dd>29,99 €</dd>
      <dt>Versandkosten</dt>
      <dd>4,95 €</dd>
      <dt class="total">Gesamtsumme</dt>
      <dd class="total">34,94 €</dd>
    </dl>
    <a href="/checkout" class="button-primary">Zur Kasse gehen</a>
  </div>
</div>
```

Lass uns diese Struktur im Detail betrachten:

*   **`<table>`, `<thead>`, `<tbody>`, `<tr>`, `<th>`, `<td>`**: Diese Elemente bilden das Grundgerüst. `<thead>` enthält die Kopfzeile mit den Spaltenüberschriften (`<th>`). Das `scope="col"`-Attribut ist wichtig für die Barrierefreiheit, da es Screenreadern mitteilt, dass diese Zelle eine Überschrift für die gesamte Spalte ist. Im `<tbody>` befindet sich für jedes Produkt eine Tabellenzeile (`<tr>`).
*   **Produktinformationen**: In der ersten Zelle (`<td>`) gruppieren wir das Bild und den Namen des Produkts. Das `<img>`-Element braucht unbedingt ein aussagekräftiges `alt`-Attribut, das den Inhalt des Bildes für Nutzer beschreibt, die es nicht sehen können.
*   **Mengenanpassung**: Ein `<input type="number">` ist hier die perfekte Wahl. Es bietet dem Nutzer eine einfache Möglichkeit, die Menge über Pfeiltasten oder direkte Eingabe zu ändern. Die Attribute `min` und `max` verhindern Fehleingaben. Ein unsichtbares Label (`<label>`) mit der Klasse `visually-hidden` (die du per CSS ausblenden musst) oder ein `aria-label` sorgt dafür, dass auch Screenreader-Nutzer wissen, wofür dieses Eingabefeld ist.
*   **Artikel entfernen**: Ein `<button>`-Element ist semantisch korrekt, um eine Aktion auszulösen – in diesem Fall das Entfernen eines Artikels. Das `aria-label` ist entscheidend, da das "×"-Symbol allein für assistierende Technologien nicht aussagekräftig wäre.
*   **Zusammenfassung (`cart-summary`)**: Nach der Tabelle folgt der Bereich, der die Kosten aufschlüsselt. Eine Definitionsliste (`<dl>`, `<dt>`, `<dd>`) ist eine elegante und semantisch passende Möglichkeit, um Schlüssel-Wert-Paare wie "Zwischensumme" und den dazugehörigen Betrag darzustellen.
*   **Call to Action**: Der Button "Zur Kasse gehen" ist der logische nächste Schritt. Hier ist es ein Link (`<a>`), da er den Nutzer auf eine neue Seite (`/checkout`) weiterleitet. Stilistisch wird er natürlich wie ein Button aussehen, aber seine Funktion ist die Navigation.

#### Der Checkout: Der Weg zum Abschluss

Der Checkout-Prozess ist der sensibelste Teil des Online-Kaufs. Hier geben Nutzer persönliche Daten ein und vertrauen dir ihr Geld an. Jede Unsicherheit, jede Hürde kann zum Abbruch führen. Die HTML-Struktur muss daher absolut logisch, nachvollziehbar und vertrauenserweckend sein. Das zentrale Element für den gesamten Checkout ist das `<form>`-Element.

Ein moderner Checkout ist oft in logische Schritte oder Abschnitte unterteilt: Lieferadresse, Versandart, Zahlungsmethode und Überprüfung. Für die Gruppierung dieser zusammengehörigen Formularfelder sind die Elemente `<fieldset>` und `<legend>` wie geschaffen. Sie strukturieren nicht nur visuell (mit etwas CSS), sondern schaffen auch eine semantische Verbindung, die für Screenreader von großem Nutzen ist.

Werfen wir einen Blick auf einen Ausschnitt eines Checkout-Formulars:

```html
<form action="/process-order" method="post" class="checkout-form">
  
  <fieldset>
    <legend>1. Lieferadresse</legend>

    <div class="form-group">
      <label for="name">Vollständiger Name</label>
      <input type="text" id="name" name="name" required autocomplete="name">
    </div>

    <div class="form-group">
      <label for="street">Straße und Hausnummer</label>
      <input type="text" id="street" name="street" required autocomplete="shipping street-address">
    </div>

    <div class="form-group-inline">
      <div class="form-group">
        <label for="zip">Postleitzahl</label>
        <input type="text" id="zip" name="zip" required autocomplete="shipping postal-code" inputmode="numeric" pattern="[0-9]{5}">
      </div>
      <div class="form-group">
        <label for="city">Stadt</label>
        <input type="text" id="city" name="city" required autocomplete="shipping address-level2">
      </div>
    </div>
  </fieldset>

  <fieldset>
    <legend>2. Zahlungsmethode</legend>
    
    <div class="form-group-radio">
      <input type="radio" id="payment-cc" name="payment-method" value="cc" checked>
      <label for="payment-cc">Kreditkarte</label>
    </div>
    
    <div class="form-group-radio">
      <input type="radio" id="payment-paypal" name="payment-method" value="paypal">
      <label for="payment-paypal">PayPal</label>
    </div>

    <!-- Weitere Felder für Kreditkartendetails würden hier dynamisch angezeigt werden -->
    <div id="credit-card-details">
      <div class="form-group">
        <label for="cc-number">Kartennummer</label>
        <input type="text" id="cc-number" name="cc-number" required autocomplete="cc-number" inputmode="numeric" placeholder="•••• •••• •••• ••••">
      </div>
      <!-- ... weitere Felder für Ablaufdatum und CVC -->
    </div>
  </fieldset>

  <div class="order-summary-checkout">
    <!-- Hier könnte eine kompakte Version der Warenkorb-Zusammenfassung stehen -->
    <h3>Ihre Bestellung</h3>
    <p>Gesamtsumme: <strong>34,94 €</strong></p>
  </div>
  
  <button type="submit" class="button-primary">Jetzt kostenpflichtig bestellen</button>

</form>
```

Was macht diese Struktur so effektiv?

*   **`<form>` als Container**: Das `<form>`-Element umschließt alle Eingabefelder, die zum Abschluss der Bestellung gehören. Die Attribute `action` und `method` definieren, wohin die Daten gesendet werden, auch wenn dies in modernen Web-Anwendungen oft von JavaScript übernommen wird.
*   **`<fieldset>` und `<legend>`**: Sie gliedern das Formular in verdauliche Abschnitte. Die `<legend>` dient als Überschrift für die jeweilige Gruppe von Feldern und ist semantisch direkt mit ihnen verbunden.
*   **`<label>` und `id`/`for`**: Jedes einzelne Eingabefeld (`<input>`, `<select>`, etc.) benötigt ein `<label>`. Die Verknüpfung über das `for`-Attribut der Beschriftung und die `id` des Eingabefeldes ist fundamental. Sie stellt sicher, dass ein Klick auf das Label den Fokus auf das zugehörige Feld setzt und Screenreader die Beschriftung korrekt vorlesen.
*   **Die richtigen `type`-Attribute**: Die Verwendung spezifischer Typen wie `type="email"` oder `type="tel"` ist nicht nur semantisch korrekt, sondern verbessert auch die Nutzererfahrung erheblich. Auf Mobilgeräten wird dadurch beispielsweise automatisch die passende Tastatur (mit @-Zeichen oder Ziffernblock) angezeigt.
*   **Das `autocomplete`-Attribut**: Dies ist ein enormer Gewinn für die Benutzerfreundlichkeit. Indem du dem Browser mitteilst, welche Art von Information in einem Feld erwartet wird (z. B. `autocomplete="name"` oder `autocomplete="shipping street-address"`), kann er dem Nutzer vorschlagen, die Daten automatisch auszufüllen. Dies spart Zeit, reduziert Tippfehler und senkt die Abbruchrate. Eine vollständige Liste der Werte findest du in der MDN Web Docs.
*   **Radio-Buttons für Auswahlmöglichkeiten**: Für exklusive Optionen wie die Versand- oder Zahlungsmart sind Radio-Buttons (`<input type="radio">`) die richtige Wahl. Alle zusammengehörigen Radio-Buttons müssen dasselbe `name`-Attribut haben, damit immer nur eine Option gleichzeitig ausgewählt werden kann.
*   **Der finale Button**: Der alles entscheidende Button am Ende des Prozesses muss ein `<button type="submit">` sein. Nur so wird das Absenden des Formulars standardkonform ausgelöst – auch wenn der Nutzer die Enter-Taste drückt. Der Text des Buttons, wie "Jetzt kostenpflichtig bestellen", ist zudem gesetzlich vorgeschrieben und schafft Transparenz über die Konsequenzen des Klicks.

Die HTML-Struktur von Warenkorb und Checkout ist das unsichtbare Fundament für einen erfolgreichen Verkaufsprozess. Auch wenn CSS und JavaScript für das Aussehen und die dynamische Funktionalität verantwortlich sind, sorgt ein sauberes, semantisches und barrierefreies HTML dafür, dass der Weg zum Kauf für absolut jeden Nutzer – unabhängig von seinem Gerät oder seinen Fähigkeiten – klar, einfach und sicher ist.
