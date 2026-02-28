# Filter und Sortierung

### Filter und Sortierung: Ordnung im digitalen Schaufenster

Stell dir vor, du betrittst ein riesiges Kaufhaus, in dem Tausende von Produkten kreuz und quer in den Regalen liegen. Du suchst ein bestimmtes Paar blauer Laufschuhe in Größe 43, findest aber nur Winterjacken neben Kochtöpfen und Gartenzwergen. Frustrierend, oder? Genau dieses Chaos vermeidest du in einem Onlineshop durch intelligente Filter- und Sortierfunktionen. Sie sind das Herzstück einer guten Benutzererfahrung, besonders im E-Commerce. Sie verwandeln eine unübersichtliche Produktflut in ein übersichtliches, navigierbares Schaufenster, in dem deine Nutzer genau das finden, was sie suchen.

Die Magie passiert zwar letztendlich mit JavaScript, aber das Fundament, auf dem diese Magie wirkt, ist pures, semantisch korrektes HTML. Ohne eine saubere und durchdachte HTML-Struktur sind selbst die cleversten Skripte nutzlos. Lass uns also die Bausteine für ein robustes Filter- und Sortiersystem anschauen.

#### Das Grundgerüst: Filter-Steuerung und Produktliste

Jede Filterlogik braucht zwei Hauptkomponenten: die Steuerelemente (die Filter selbst) und die Elemente, die gefiltert werden sollen (die Produktliste). Strukturell trennen wir diese beiden Bereiche klar voneinander.

Eine typische Aufteilung sieht so aus:

```html
<div class="shop-wrapper">
  
  <!-- Die Filterleiste, oft in einer Seitenleiste -->
  <aside class="filter-sidebar">
    <h2>Filter</h2>
    <!-- Hier kommen die einzelnen Filter-Module rein -->
  </aside>

  <!-- Der Hauptbereich mit den Produkten -->
  <main class="produkt-container">
    <div class="sortier-steuerung">
      <!-- Hier kommt die Sortierung hin -->
    </div>
    <ul class="produkt-liste">
      <!-- Hier werden die Produkte angezeigt -->
    </ul>
  </main>

</div>
```

Das `<aside>`-Element ist semantisch ideal für die Filter, da sie ergänzenden Inhalt zur Hauptansicht (`<main>`) darstellen. Im `<main>`-Bereich haben wir eine Steuerung für die Sortierung und eine ungeordnete Liste (`<ul>`), die unsere Produkte aufnehmen wird. Jedes Produkt wird ein Listenelement (`<li>`) sein.

#### Die Filter-Werkzeuge im Detail

Filter sind im Grunde nichts anderes als Formularelemente. Deine Aufgabe ist es, die richtigen Elemente für den jeweiligen Zweck auszuwählen. Die gesamte Filtersektion sollte von einem `<form>`-Tag umschlossen werden. Das hilft nicht nur bei der Struktur, sondern auch bei der Zugänglichkeit und möglichen Erweiterungen (z. B. eine serverseitige Filterung als Fallback).

##### Checkboxen für Mehrfachauswahl

Checkboxen sind perfekt, wenn der Nutzer mehrere Optionen gleichzeitig auswählen können soll. Typische Beispiele sind Produktkategorien, Marken oder Farben.

```html
<form id="produkt-filter">
  <fieldset>
    <legend>Kategorie</legend>
    <div>
      <input type="checkbox" id="cat-schuhe" name="kategorie" value="schuhe">
      <label for="cat-schuhe">Schuhe</label>
    </div>
    <div>
      <input type="checkbox" id="cat-hosen" name="kategorie" value="hosen">
      <label for="cat-hosen">Hosen</label>
    </div>
    <div>
      <input type="checkbox" id="cat-jacken" name="kategorie" value="jacken">
      <label for="cat-jacken">Jacken</label>
    </div>
  </fieldset>

  <fieldset>
    <legend>Marke</legend>
    <div>
      <input type="checkbox" id="brand-a" name="marke" value="a-brand">
      <label for="brand-a">A-Brand</label>
    </div>
    <div>
      <input type="checkbox" id="brand-b" name="marke" value="b-corp">
      <label for="brand-b">B-Corp</label>
    </div>
  </fieldset>
</form>
```

Achte auf die Details:
*   **`<fieldset>` und `<legend>`:** Sie gruppieren zusammengehörige Formularelemente und geben der Gruppe einen Namen. Das ist Gold wert für die Barrierefreiheit, da Screenreader diese Struktur erkennen und dem Nutzer den Kontext ("Kategorie", "Marke") vorlesen.
*   **`<input type="checkbox">`:** Das eigentliche Filterelement.
*   **`<label>` mit `for`-Attribut:** Jede Checkbox braucht ein Label. Durch die Verknüpfung über die `id` des Inputs mit dem `for`-Attribut des Labels wird der Text klickbar, was die Bedienung erheblich erleichtert.
*   **`name` und `value`:** Das `name`-Attribut gruppiert die Checkboxen (z. B. alle gehören zur Gruppe "kategorie"), während das `value`-Attribut den spezifischen Wert speichert, nach dem gefiltert wird (z. B. "schuhe").

##### Radio-Buttons für Einfachauswahl

Manchmal soll der Nutzer nur eine Option aus einer Gruppe wählen können, zum Beispiel bei der Frage, ob nur reduzierte Artikel angezeigt werden sollen. Hierfür sind Radio-Buttons die richtige Wahl.

```html
<fieldset>
  <legend>Angebote</legend>
  <div>
    <input type="radio" id="sale-all" name="sale-filter" value="all" checked>
    <label for="sale-all">Alle Artikel</label>
  </div>
  <div>
    <input type="radio" id="sale-only" name="sale-filter" value="sale-only">
    <label for="sale-only">Nur Angebote</label>
  </div>
</fieldset>
```

Alle Radio-Buttons, die zur selben Entscheidung gehören, müssen denselben `name`-Wert haben. Dadurch stellt der Browser sicher, dass immer nur einer davon aktiv sein kann.

##### Range-Slider für Preisspannen

Der Preis ist einer der wichtigsten Filter. Ein Schieberegler (`<input type="range">`) ist hier eine intuitive Wahl. Ein einfacher Slider kann einen Maximalpreis festlegen, für eine "Von-Bis"-Spanne werden oft zwei Slider oder eine JavaScript-Bibliothek benötigt. Die HTML-Grundlage bleibt aber dieselbe.

```html
<fieldset>
  <legend>Preis</legend>
  <div>
    <label for="price-range">Bis zu: <span id="price-value">150</span>€</label>
    <input type="range" id="price-range" name="price" min="0" max="500" step="10" value="150">
  </div>
</fieldset>
```

Hierbei ist das `<span>`-Element praktisch, um den aktuell ausgewählten Wert des Sliders per JavaScript anzuzeigen und dem Nutzer direktes Feedback zu geben.

#### Die Sortier-Mechanik: Das Dropdown-Menü

Während Filter die Menge der angezeigten Produkte reduzieren, ändert die Sortierung lediglich deren Reihenfolge. Das klassische UI-Element hierfür ist ein Dropdown-Menü (`<select>`).

```html
<div class="sortier-steuerung">
  <label for="sort-select">Sortieren nach:</label>
  <select name="sortierung" id="sort-select">
    <option value="default">Standard</option>
    <option value="price-asc">Preis: Aufsteigend</option>
    <option value="price-desc">Preis: Absteigend</option>
    <option value="name-asc">Name: A-Z</option>
    <option value="newest">Neueste zuerst</option>
  </select>
</div>
```

Auch hier sind die Details entscheidend:
*   Das `<label>` ist wieder aus Gründen der Barrierefreiheit und Usability unverzichtbar.
*   Jedes `<option>`-Element hat ein `value`-Attribut. Dieser Wert ist für dein JavaScript-Code bestimmt. Er ist kurz, maschinenlesbar und beschreibt die Sortierlogik (z. B. `price-asc` für "Preis aufsteigend"). Der Text innerhalb des `<option>`-Tags ist hingegen das, was der Nutzer sieht.

#### Das Produkt-Raster: Daten für die Logik bereitstellen

Nun kommen wir zum wichtigsten Teil: den Produkten selbst. Wie weiß dein JavaScript, welche Produkte zu welchen Filtern gehören? Die Antwort liegt in `data-*`-Attributen. Diese benutzerdefinierten Attribute sind der Klebstoff, der deine Filtersteuerung mit deinen Produkten verbindet.

Jedes Produkt in deiner Liste (`<li>`) sollte alle Informationen als `data`-Attribute enthalten, die für die Filterung und Sortierung relevant sind.

```html
<ul class="produkt-liste">
  
  <li class="produkt-karte" 
      data-category="schuhe" 
      data-brand="a-brand" 
      data-price="129.99" 
      data-date="2023-10-26">
    <img src="laufschuh-a.jpg" alt="Bequemer Laufschuh von A-Brand">
    <h3>Laufschuh "Runner Pro"</h3>
    <p class="marke">A-Brand</p>
    <p class="preis">129,99 €</p>
  </li>

  <li class="produkt-karte" 
      data-category="hosen" 
      data-brand="b-corp" 
      data-price="79.50" 
      data-date="2023-09-15"
      data-sale="true">
    <img src="jeans-b.jpg" alt="Modische Jeans von B-Corp">
    <h3>Jeans "Urban Style"</h3>
    <p class="marke">B-Corp</p>
    <p class="preis">79,50 € <span class="sale-badge">Sale</span></p>
  </li>

  <li class="produkt-karte" 
      data-category="schuhe" 
      data-brand="b-corp" 
      data-price="149.00" 
      data-date="2023-11-01">
    <img src="wanderschuh-b.jpg" alt="Robuster Wanderschuh von B-Corp">
    <h3>Wanderschuh "Explorer"</h3>
    <p class="marke">B-Corp</p>
    <p class="preis">149,00 €</p>
  </li>

</ul>
```

Schauen wir uns das `data`-Attribut genauer an:
*   `data-category="schuhe"`: Entspricht dem `value` der Kategorie-Checkbox.
*   `data-brand="a-brand"`: Entspricht dem `value` der Marken-Checkbox.
*   `data-price="129.99"`: Ein numerischer Wert, der für Preis-Slider und die Preissortierung verwendet wird.
*   `data-date="2023-10-26"`: Nützlich für die Sortierung "Neueste zuerst".
*   `data-sale="true"`: Ein boolescher Wert für den "Nur Angebote"-Filter.

Mit dieser sauberen HTML-Struktur hat dein JavaScript nun alles, was es braucht.

#### Wie alles zusammenspielt (Ein kurzer Blick auf die Logik)

Obwohl die Implementierung in JavaScript stattfindet, ist das Verständnis der Logik entscheidend, um das HTML richtig zu strukturieren.

1.  **Filterung:** Wenn ein Nutzer eine Checkbox anklickt, liest dein JavaScript die aktiven Filter aus (z. B. "Kategorie: schuhe" und "Marke: b-corp"). Anschließend durchläuft es alle `<li>`-Elemente in der Produktliste. Für jedes Produkt prüft es, ob dessen `data-category` und `data-brand` mit den ausgewählten Filtern übereinstimmen. Produkte, die passen, werden angezeigt (`display: block` oder ähnlich); alle anderen werden ausgeblendet (`display: none`).

2.  **Sortierung:** Wenn der Nutzer eine Option im `<select>`-Menü wählt, liest dein Skript den `value` der Auswahl (z. B. `price-asc`). Es sammelt alle sichtbaren `<li>`-Elemente, liest den entsprechenden `data-price`-Wert jedes Elements aus und sortiert die Elemente basierend auf diesen Werten. Schließlich ordnet es die `<li>`-Elemente im DOM neu an, um die sortierte Reihenfolge widerzuspiegeln.

Du siehst, die gesamte Dynamik basiert auf dem Auslesen von Werten aus dem HTML. Eine klare, konsistente und semantische Struktur ist daher keine Kür, sondern die absolute Pflicht für funktionale, wartbare und zugängliche Filter- und Sortiersysteme. Du hast nun das stabile Fundament gelegt, auf dem die Interaktivität aufgebaut werden kann.
