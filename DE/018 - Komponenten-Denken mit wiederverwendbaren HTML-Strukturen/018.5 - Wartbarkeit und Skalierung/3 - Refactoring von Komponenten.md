# Refactoring von Komponenten

# Refactoring von Komponenten

Stell dir vor, deine Werkstatt ist perfekt aufgeräumt. Jedes Werkzeug hat seinen Platz, die Arbeitsfläche ist sauber und du weißt genau, wo du alles findest. In dieser Umgebung kannst du effizient, schnell und sicher arbeiten. Wenn du nun ein neues Projekt beginnst, musst du nicht erst stundenlang nach dem richtigen Schraubendreher suchen oder über Kabel stolpern.

In der Welt der Webentwicklung ist Refactoring genau das: das Aufräumen deiner Werkstatt. Es geht nicht darum, neue Möbel (Features) zu bauen, sondern die bestehende Ordnung zu verbessern, damit zukünftige Arbeiten leichter von der Hand gehen. Beim Refactoring von Komponenten änderst du die *interne Struktur* deines HTML- und CSS-Codes, ohne das *externe Verhalten* – also das, was der Benutzer sieht und womit er interagiert – zu verändern. Das Ziel ist es, deinen Code lesbarer, wartbarer und wiederverwendbarer zu machen. Es ist eine Investition in die Zukunft deines Projekts.

### Wann ist der richtige Zeitpunkt für Refactoring?

Du schreibst nicht einfach Code und planst dann eine große "Refactoring-Woche" ein. Refactoring ist ein kontinuierlicher Prozess. Die besten Gelegenheiten dafür erkennst du an sogenannten "Code Smells" – Anzeichen im Code, die darauf hindeuten, dass es eine bessere, sauberere Lösung geben könnte. Für HTML-Komponenten sind typische Code Smells:

1.  **Duplizierter Code:** Du entdeckst zwei oder mehr Komponenten, die fast identisch sind. Vielleicht hat eine "News-Karte" eine sehr ähnliche Struktur wie eine "Event-Karte". Das ist ein klares Zeichen dafür, dass du eine allgemeinere, wiederverwendbare Basiskomponente erstellen kannst.

2.  **Lange, unübersichtliche Komponenten:** Eine Komponente ist mit so viel HTML und so vielen Klassen vollgestopft, dass du scrollen musst, um sie vollständig zu erfassen. Oftmals verbirgt eine solche "Monsterkomponente" mehrere kleinere, logische Einheiten in sich, die als eigenständige Komponenten viel sinnvoller wären.

3.  **Inkonsistente Namensgebung:** Du hast eine Button-Komponente `.btn-primary` genannt, eine andere aber `main_button` und eine dritte `submit-cta`. Diese Inkonsistenz macht es schwer, den Code zu verstehen und vorherzusagen, wie Elemente benannt sind. Es zwingt dich und dein Team, ständig nachzudenken und nachzuschlagen.

4.  **Starre Strukturen:** Deine Komponente ist so spezifisch gebaut, dass sie nur in einem einzigen Kontext funktioniert. Eine kleine Änderung an anderer Stelle der Seite erfordert eine komplette Kopie und Anpassung der Komponente. Flexible Komponenten lassen sich hingegen leicht anpassen, zum Beispiel durch Modifier-Klassen.

Wenn du auf eines dieser Anzeichen stößt, ist das ein guter Moment, um innezuhalten und über ein Refactoring nachzudenken.

### Der Prozess: Von unordentlich zu sauber

Refactoring ist keine Magie, sondern ein disziplinierter Prozess. Der Schlüssel liegt darin, in kleinen, kontrollierten Schritten vorzugehen, um sicherzustellen, dass du nichts kaputt machst.

**Schritt 1: Identifiziere das Problem**
Schau dir den Code genau an. Was stört dich? Ist es Duplizierung? Ist die Komponente zu komplex? Benenne das Problem konkret. Zum Beispiel: "Die `user-profile-header` und `company-profile-header` Komponenten teilen sich 90 % ihres HTML-Markups und ihrer CSS-Regeln."

**Schritt 2: Definiere das Ziel**
Was möchtest du erreichen? Eine klare Zielsetzung hilft dir, den Fokus zu behalten. Im obigen Beispiel wäre das Ziel: "Erstelle eine generische `.profile-header`-Komponente, die über Modifier-Klassen wie `.profile-header--user` und `.profile-header--company` für die spezifischen Anwendungsfälle angepasst werden kann."

**Schritt 3: Führe die Änderungen schrittweise durch**
Das ist der wichtigste Teil. Ändere nicht alles auf einmal.
*   **Extrahiere:** Ziehe den gemeinsamen Code in eine neue, generische Komponente.
*   **Vereinheitliche:** Passe die Klassennamen an ein konsistentes System an (z. B. BEM – Block, Element, Modifier).
*   **Ersetze:** Tausche eine alte Implementierung nach der anderen durch die neue, refaktorierte Komponente aus.

Nach jedem kleinen Schritt solltest du überprüfen, ob die Komponente immer noch so aussieht und funktioniert wie zuvor. Bei visuellen Komponenten bedeutet das, einen Blick in den Browser zu werfen.

**Schritt 4: Räume auf**
Wenn du alle Vorkommen der alten, problematischen Komponente durch die neue ersetzt hast, lösche den alten Code. Es gibt nichts Verwirrenderes als veralteten, ungenutzten Code, der im Projekt verbleibt.

### Ein praktisches Beispiel: Die Produktkarte

Sehen wir uns ein konkretes Beispiel an. Stell dir vor, du hast in deinem Onlineshop zwei Arten von Produktkarten. Eine normale und eine für Produkte im Angebot. Dein aktueller Code könnte so aussehen:

```html
<!-- Normale Produktkarte -->
<div class="product-box">
  <img src="schuhe.jpg" alt="Bequeme Laufschuhe" class="product-image">
  <h3 class="product-title-text">Bequeme Laufschuhe</h3>
  <p class="price">99,95 €</p>
  <button id="add-to-cart-btn">In den Warenkorb</button>
</div>

<!-- Angebots-Produktkarte -->
<div class="product-box-sale">
  <div class="sale-badge">Angebot!</div>
  <img src="shirt.jpg" alt="Atmungsaktives Sportshirt" class="product-image">
  <h3 class="product-title-text">Atmungsaktives Sportshirt</h3>
  <p class="price-old">39,95 €</p>
  <p class="price-sale">29,95 €</p>
  <button id="add-to-cart-btn-sale">In den Warenkorb</button>
</div>
```

Du erkennst sofort die Probleme:
*   **Duplizierung:** Die Grundstruktur ist fast identisch.
*   **Inkonsistenz:** `.product-box` vs. `.product-box-sale`, `price` vs. `price-old`/`price-sale`, `#add-to-cart-btn` vs. `#add-to-cart-btn-sale`. Die Verwendung von IDs für stilelemente ist zudem problematisch, da IDs pro Seite einzigartig sein müssen.
*   **Mangelnde Flexibilität:** Was, wenn du ein "Neu"-Badge hinzufügen willst? Müsstest du eine dritte Variante `product-box-new` erstellen?

**Refactoring-Plan:**

1.  **Identifizieren:** Duplizierter und inkonsistenter Code für Produktkarten.
2.  **Ziel:** Eine einzige, wiederverwendbare `.product-card`-Komponente erstellen, die über eine Modifier-Klasse `.product-card--on-sale` für den Angebotsfall angepasst werden kann. Die Namensgebung soll dem BEM-Standard folgen.

**Die Umsetzung:**

Zuerst definierst du die neue, saubere HTML-Struktur für eine generische Produktkarte.

**Neues HTML:**
```html
<article class="product-card">
  <img class="product-card__image" src="schuhe.jpg" alt="Bequeme Laufschuhe">
  <div class="product-card__body">
    <h3 class="product-card__title">Bequeme Laufschuhe</h3>
    <div class="product-card__price">
      <span class="product-card__price-current">99,95 €</span>
    </div>
    <button class="product-card__button">In den Warenkorb</button>
  </div>
</article>
```
Diese Struktur ist klar und nutzt BEM-Nomenklatur (`Block__Element`). Nun, wie gehst du mit der Angebots-Variante um? Anstatt alles zu duplizieren, fügst du die Angebots-Elemente hinzu und steuerst ihre Sichtbarkeit und ihr Aussehen über eine Modifier-Klasse auf dem Block-Element (`.product-card--on-sale`).

**Finale, flexible HTML-Struktur:**
```html
<!-- Normale Produktkarte -->
<article class="product-card">
  <div class="product-card__badge-wrapper"></div>
  <img class="product-card__image" src="schuhe.jpg" alt="Bequeme Laufschuhe">
  <div class="product-card__body">
    <h3 class="product-card__title">Bequeme Laufschuhe</h3>
    <div class="product-card__price">
      <span class="product-card__price-current">99,95 €</span>
    </div>
    <button class="product-card__button">In den Warenkorb</button>
  </div>
</article>

<!-- Angebots-Produktkarte mit Modifier-Klasse -->
<article class="product-card product-card--on-sale">
  <div class="product-card__badge-wrapper">
    <span class="product-card__badge">Angebot!</span>
  </div>
  <img class="product-card__image" src="shirt.jpg" alt="Atmungsaktives Sportshirt">
  <div class="product-card__body">
    <h3 class="product-card__title">Atmungsaktives Sportshirt</h3>
    <div class="product-card__price">
      <span class="product-card__price-old">39,95 €</span>
      <span class="product-card__price-current">29,95 €</span>
    </div>
    <button class="product-card__button">In den Warenkorb</button>
  </div>
</article>
```

Der entscheidende Punkt ist, dass beide Karten jetzt dieselbe Grundstruktur und dieselben Basiselemente verwenden. Die Unterschiede werden durch die Modifier-Klasse `.product-card--on-sale` im CSS gesteuert.

**Zugehöriges CSS (vereinfacht):**
```css
/* Basisstile für die Komponente */
.product-card {
  border: 1px solid #ccc;
  border-radius: 8px;
  overflow: hidden;
  text-align: center;
}

.product-card__image {
  max-width: 100%;
  height: auto;
}

.product-card__body {
  padding: 1rem;
}

.product-card__title {
  font-size: 1.2rem;
  margin: 0 0 0.5rem;
}

/* Elemente, die nur im Angebotsfall sichtbar sind, standardmäßig ausblenden */
.product-card__badge,
.product-card__price-old {
  display: none;
}

/* Stile, die NUR durch die Modifier-Klasse aktiviert werden */
.product-card--on-sale {
  border-color: #e74c3c; /* Rote Angebots-Umrandung */
}

.product-card--on-sale .product-card__badge {
  display: inline-block; /* Badge anzeigen */
  background-color: #e74c3c;
  color: white;
  padding: 0.25rem 0.5rem;
  position: absolute; /* Beispiel für Positionierung */
  top: 10px;
  right: 10px;
}

.product-card--on-sale .product-card__price-old {
  display: block; /* Alten Preis anzeigen */
  text-decoration: line-through;
  color: #777;
}

.product-card--on-sale .product-card__price-current {
  color: #e74c3c;
  font-weight: bold;
}
```
Das Ergebnis ist eine saubere, wartbare und skalierbare Komponente. Wenn du morgen ein "Bestseller"-Badge einführen möchtest, musst du nur eine neue Modifier-Klasse `.product-card--bestseller` und die zugehörigen CSS-Regeln hinzufügen, ohne das HTML-Grundgerüst anzufassen. Du hast die Komplexität reduziert und die Wiederverwendbarkeit maximiert.

Das ist die Essenz des Refactorings. Es ist die stille, aber ungemein wichtige Arbeit, die aus einem funktionierenden Projekt ein professionelles, langlebiges und erweiterbares System macht. Es sorgt dafür, dass deine Codebasis nicht zu einer unübersichtlichen Ansammlung von Provisorien wird, sondern zu einer soliden Grundlage, auf der du und dein Team gerne aufbauen.
