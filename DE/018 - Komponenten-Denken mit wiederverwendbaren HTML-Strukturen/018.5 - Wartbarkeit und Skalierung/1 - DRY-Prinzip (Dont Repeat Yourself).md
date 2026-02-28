# DRY-Prinzip (Dont Repeat Yourself)

### Das DRY-Prinzip: Warum du dich nicht wiederholen solltest

Stell dir vor, du baust eine Website mit zehn verschiedenen Unterseiten. Jede dieser Seiten soll die gleiche Navigationsleiste am oberen Rand und den gleichen Footer am unteren Rand haben. Du bist fleißig und kopierst den HTML-Code für die Navigation und den Footer einfach in jede deiner zehn HTML-Dateien. Alles funktioniert, die Seite sieht super aus. Doch dann kommt der Moment, in dem du einen neuen Menüpunkt hinzufügen oder eine Telefonnummer im Footer ändern musst. Plötzlich stehst du vor einer mühsamen und fehleranfälligen Aufgabe: Du musst zehn Dateien öffnen und an exakt der gleichen Stelle die exakt gleiche Änderung vornehmen. Vergisst du eine einzige Datei oder machst du nur einen kleinen Tippfehler, ist deine Website inkonsistent.

Genau dieses Problem adressiert eines der fundamentalsten Prinzipien in der Softwareentwicklung: das DRY-Prinzip. DRY steht für „Don’t Repeat Yourself“ – „Wiederhole dich nicht“. Die Kernaussage ist simpel, aber ihre Auswirkungen auf die Qualität, Wartbarkeit und Skalierbarkeit deines Codes sind gewaltig.

Das Prinzip besagt, dass jede Information oder jedes Stück Logik in einem System nur eine einzige, eindeutige und maßgebliche Repräsentation haben sollte. Übertragen auf dein HTML bedeutet das: Jeder wiederkehrende Block von Code – sei es eine Navigationsleiste, eine Produktkarte in einem Onlineshop oder ein simpler Button – sollte nur an einem einzigen Ort definiert werden. An allen anderen Stellen, an denen du ihn benötigst, wird er nur noch referenziert oder eingebunden.

#### Der „nasse“ Code: Ein Beispiel für Wiederholung

Um die Nachteile von Wiederholungen zu verstehen, schauen wir uns ein konkretes Beispiel an. Nehmen wir an, du erstellst eine Seite, die mehrere Produkte anzeigt. Jedes Produkt wird durch eine „Karte“ mit einem Bild, einem Titel, einer Beschreibung und einem Preis dargestellt. Ohne das DRY-Prinzip im Hinterkopf könnte dein Code so aussehen:

```html
<!-- index.html -->

<h1>Unsere Produkte</h1>

<div class="produkt-liste">

  <!-- Produkt 1 -->
  <div class="produkt-karte">
    <img src="bilder/schuhe.jpg" alt="Bequeme Laufschuhe">
    <h2>Bequeme Laufschuhe</h2>
    <p>Diese Schuhe sind perfekt für dein tägliches Training.</p>
    <span class="preis">99,95 €</span>
    <button>In den Warenkorb</button>
  </div>

  <!-- Produkt 2 -->
  <div class="produkt-karte">
    <img src="bilder/rucksack.jpg" alt="Robuster Wanderrucksack">
    <h2>Robuster Wanderrucksack</h2>
    <p>Dein Begleiter für jedes Abenteuer in den Bergen.</p>
    <span class="preis">79,50 €</span>
    <button>In den Warenkorb</button>
  </div>

  <!-- Produkt 3 -->
  <div class="produkt-karte">
    <img src="bilder/flasche.jpg" alt="Isolierte Trinkflasche">
    <h2>Isolierte Trinkflasche</h2>
    <p>Hält deine Getränke 12 Stunden kalt oder warm.</p>
    <span class="preis">24,99 €</span>
    <button>In den Warenkorb</button>
  </div>

</div>
```

Dieser Code wird oft scherzhaft als „WET“ bezeichnet, was für „Write Everything Twice“ (oder „We Enjoy Typing“) steht. Auf den ersten Blick scheint er harmlos. Aber was passiert, wenn du die Struktur aller Produktkarten ändern möchtest? Vielleicht soll der Preis jetzt über der Beschreibung stehen, oder der Button soll eine neue CSS-Klasse für ein anderes Styling bekommen. Du müsstest jede einzelne Karte manuell bearbeiten. Bei drei Karten ist das vielleicht noch machbar, aber bei dreißig oder dreihundert wird es zum Albtraum.

Die Probleme von WET-Code sind offensichtlich:
*   **Hoher Wartungsaufwand:** Änderungen müssen an vielen Stellen durchgeführt werden.
*   **Hohe Fehleranfälligkeit:** Es ist leicht, eine Stelle zu übersehen oder Fehler beim Kopieren und Einfügen zu machen.
*   **Schlechte Lesbarkeit:** Die HTML-Datei wird unnötig aufgebläht. Die wesentliche Struktur der Seite – eine Liste von Produkten – geht in den sich wiederholenden Details der einzelnen Karten unter.

#### Der trockene Code: Abstraktion als Lösung

Die Lösung besteht darin, die wiederkehrende Struktur zu abstrahieren. Statt die gesamte Produktkarte immer wieder zu kopieren, definieren wir sie einmal als wiederverwendbare Komponente.

In der reinen Webentwicklung ohne Frameworks wird dies oft serverseitig gelöst, zum Beispiel mit Sprachen wie PHP, Python oder JavaScript (Node.js). Das Konzept bleibt aber immer dasselbe. Wir erstellen eine separate Datei für unsere Komponente, zum Beispiel `produkt-karte.php`.

```html
<!-- produkt-karte.php -->

<div class="produkt-karte">
  <img src="<?php echo $bild_pfad; ?>" alt="<?php echo $bild_alt; ?>">
  <h2><?php echo $titel; ?></h2>
  <p><?php echo $beschreibung; ?></p>
  <span class="preis"><?php echo $preis; ?> €</span>
  <button>In den Warenkorb</button>
</div>
```

Beachte die Platzhalter wie `<?php echo $titel; ?>`. Dies sind Variablen, die wir beim Einbinden der Komponente mit den spezifischen Daten für jedes Produkt füllen.

Unsere Hauptdatei `index.php` wird dadurch dramatisch sauberer und verständlicher. Sie kümmert sich nur noch um die übergeordnete Struktur und die Daten, nicht mehr um das Detail-Markup jeder einzelnen Karte.

```php
<!-- index.php -->

<h1>Unsere Produkte</h1>

<div class="produkt-liste">

  <?php
    $bild_pfad = "bilder/schuhe.jpg";
    $bild_alt = "Bequeme Laufschuhe";
    $titel = "Bequeme Laufschuhe";
    $beschreibung = "Diese Schuhe sind perfekt für dein tägliches Training.";
    $preis = "99,95";
    include 'produkt-karte.php';
  ?>

  <?php
    $bild_pfad = "bilder/rucksack.jpg";
    $bild_alt = "Robuster Wanderrucksack";
    $titel = "Robuster Wanderrucksack";
    $beschreibung = "Dein Begleiter für jedes Abenteuer in den Bergen.";
    $preis = "79,50";
    include 'produkt-karte.php';
  ?>

  <?php
    $bild_pfad = "bilder/flasche.jpg";
    $bild_alt = "Isolierte Trinkflasche";
    $titel = "Isolierte Trinkflasche";
    $beschreibung = "Hält deine Getränke 12 Stunden kalt oder warm.";
    $preis = "24,99";
    include 'produkt-karte.php';
  ?>

</div>
```

Wenn du nun die Struktur der Produktkarte ändern möchtest – zum Beispiel den Preis an eine andere Stelle verschieben –, musst du nur noch eine einzige Datei bearbeiten: `produkt-karte.php`. Die Änderung wirkt sich sofort auf alle Produkte auf deiner gesamten Website aus. Das ist die Macht des DRY-Prinzips.

#### DRY gilt nicht nur für HTML-Strukturen

Das Prinzip der Wiederverwendung ist universell und zieht sich durch alle Bereiche der Webentwicklung.

*   **In CSS:** Anstatt Inline-Styles wie `style="color: red; font-weight: bold;"` für jeden wichtigen Text zu verwenden, definierst du einmal eine Klasse in deiner CSS-Datei, zum Beispiel `.wichtiger-text { color: red; font-weight: bold; }`. Danach kannst du diese Klasse `class="wichtiger-text"` an beliebig viele HTML-Elemente vergeben. Eine Änderung in der CSS-Datei aktualisiert alle Vorkommen.
*   **In JavaScript:** Anstatt denselben Codeblock zur Validierung eines Formularfeldes an mehreren Stellen zu kopieren, schreibst du eine einzige Funktion `validateField(field)` und rufst diese Funktion bei Bedarf mit dem entsprechenden Feld auf.

#### Die wahren Vorteile von trockenem Code

Wenn du das DRY-Prinzip konsequent anwendest, profitierst du auf mehreren Ebenen:

1.  **Wartbarkeit:** Dies ist der größte Vorteil. Fehler müssen nur an einer Stelle behoben werden, Änderungen sind zentral und schnell umsetzbar. Dein Code altert besser und bleibt auch bei wachsenden Anforderungen beherrschbar.
2.  **Zuverlässigkeit:** Indem du Code-Duplizierung vermeidest, reduzierst du die Anzahl potenzieller Fehlerquellen. Es ist unmöglich, bei einer Änderung eine der Kopien zu vergessen, wenn es nur eine einzige Quelle der Wahrheit gibt.
3.  **Lesbarkeit:** Dein Code wird semantischer und ausdrucksstärker. Die `index.php` von oben beschreibt klar ihre Absicht: „Zeige eine Liste von Produkten.“ Die schmutzigen Details, wie eine einzelne Produktkarte aufgebaut ist, sind in eine eigene Datei ausgelagert.
4.  **Wiederverwendbarkeit:** Einmal definierte Komponenten, wie unsere Produktkarte, können leicht in anderen Kontexten oder sogar in anderen Projekten wiederverwendet werden.

#### Die Kunst der richtigen Abstraktion

Das DRY-Prinzip klingt einfach, doch seine meisterhafte Anwendung erfordert Übung. Eine häufige Falle ist die „verfrühte Abstraktion“. Manchmal sehen zwei Code-Blöcke zufällig gleich aus, repräsentieren aber konzeptionell völlig unterschiedliche Dinge.

Stell dir vor, du hast eine Produktkarte in deinem Shop und eine Artikelkarte in deinem Blog. Beide bestehen heute vielleicht aus einem Bild, einer Überschrift und einem kurzen Text. Es wäre verlockend, sie zu einer einzigen Komponente `karte.html` zusammenzufassen. Doch was passiert, wenn die Produktkarte in Zukunft einen „In den Warenkorb“-Button benötigt, während die Artikelkarte eine „Geschätzte Lesezeit“ anzeigen soll? Eine zu früh zusammengefasste Komponente wird dann zu einem Klotz am Bein, weil du sie mit Logik für beide Anwendungsfälle überfrachten musst.

Eine gute Faustregel ist die „Dreier-Regel“ (Rule of Three): Wenn du etwas zum ersten Mal schreibst, schreib es einfach hin. Wenn du es ein zweites Mal an einer anderen Stelle benötigst, kopiere es ruhig. Erst wenn du denselben Code ein drittes Mal brauchst, ist es ein starkes Signal, dass du eine Abstraktion schaffen und den Code in eine wiederverwendbare Komponente oder Funktion auslagern solltest.

Das DRY-Prinzip ist somit mehr als nur eine technische Regel; es ist eine Denkweise. Es ermutigt dich, Muster zu erkennen, Strukturen zu planen und Code zu schreiben, der nicht nur heute funktioniert, sondern auch in Zukunft leicht zu pflegen und zu erweitern ist. Es ist das Fundament für saubere, skalierbare und professionelle Webentwicklung.
