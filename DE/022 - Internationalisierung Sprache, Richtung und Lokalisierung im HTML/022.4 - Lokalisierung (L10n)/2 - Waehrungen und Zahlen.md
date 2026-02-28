# Währungen und Zahlen

### Währungen und Zahlen: Mehr als nur Ziffern

Wenn du global denkst, musst du auch global handeln. Das gilt ganz besonders für Zahlen und Währungen auf deiner Webseite. Es mag auf den ersten Blick wie ein kleines Detail erscheinen, aber die Art und Weise, wie du Zahlen darstellst, hat einen enormen Einfluss auf die Benutzerfreundlichkeit und das Vertrauen deiner Besucher. Eine Zahl ist eben nicht einfach nur eine Zahl, und ein Preis ist so viel mehr als eine Ziffer mit einem Symbol davor.

Stell dir vor, du betreibst einen Onlineshop und ein Kunde aus den USA sieht einen Preis, der als "1.299 €" angegeben ist. Für ihn könnte das wie "eintausendzweihundertneunundneunzig Euro" aussehen. Ein deutscher Kunde hingegen liest "1,299 €" als "einen Euro und 299 Tausendstel", also knapp 1,30 €. Ein kleiner Punkt, ein kleines Komma – und schon entsteht ein riesiges Missverständnis, das im schlimmsten Fall zu Kaufabbrüchen oder verärgerten Kunden führt.

#### Die Tücken der lokalen Konventionen

Die Darstellung von Zahlen und Währungen ist tief in der Kultur und Sprache einer Region verwurzelt. Was für dich selbstverständlich ist, kann für jemanden aus einem anderen Land völlig fremd sein. Die Hauptunterschiede lassen sich in drei Bereiche gliedern:

1.  **Dezimaltrennzeichen:** In Deutschland, Österreich und vielen anderen europäischen Ländern verwenden wir ein Komma (`,`), um den ganzzahligen vom gebrochenen Teil einer Zahl zu trennen (z. B. `3,14159`). Im englischsprachigen Raum und in vielen asiatischen Ländern wird dafür ein Punkt (`.`) verwendet (z. B. `3.14159`).

2.  **Tausendertrennzeichen:** Um große Zahlen lesbarer zu machen, gruppieren wir Ziffern. Auch hier gehen die Konventionen weit auseinander.
    *   **Deutschland/Österreich:** Ein Punkt (`1.000.000`)
    *   **USA/Großbritannien:** Ein Komma (`1,000,000`)
    *   **Frankreich:** Ein geschütztes Leerzeichen (`1 000 000`)
    *   **Schweiz:** Ein Apostroph (`1'000'000`)

3.  **Währungssymbole und ihre Position:** Die Formatierung von Währungen ist noch komplexer.
    *   **Symbol:** Jede Währung hat ihr eigenes Symbol (€, $, £, ¥) oder einen ISO-Code (EUR, USD, GBP, JPY).
    *   **Position:** Das Symbol kann vor dem Betrag stehen (`$100.00`) oder danach (`100,00 €`).
    *   **Abstand:** Manchmal steht ein Leerzeichen zwischen Betrag und Symbol (`100,00 €`), manchmal nicht (`$100.00`). Oft ist dies ein geschütztes Leerzeichen (`&nbsp;`), um einen unschönen Zeilenumbruch zu verhindern.

Du siehst: Es gibt keine universelle Regel. Der Schlüssel zu einer guten Lokalisierung liegt darin, die Konventionen deiner Zielgruppe zu respektieren und zu implementieren.

#### HTMLs Rolle: Die semantische Grundlage

HTML ist eine Struktursprache. Seine Aufgabe ist es, deinem Inhalt eine Bedeutung zu geben, nicht, ihn zu gestalten. Daher bietet HTML von sich aus keine direkten Mechanismen, um die Zahl `1234.56` je nach Besucher als `1.234,56` oder `1,234.56` auszugeben. Das ist die Aufgabe von CSS (für reines Design) und vor allem JavaScript (für dynamische Logik).

Was HTML aber tun kann und sollte, ist, die Daten so semantisch korrekt wie möglich auszuzeichnen. Hierfür gibt es das `<data>`-Element. Es erlaubt dir, einen maschinenlesbaren Wert mit einem für Menschen lesbaren Inhalt zu verknüpfen.

Stell dir vor, du hast einen Preis, der auf dem Server bereits für ein deutsches Publikum formatiert wurde:

```html
<p>Preis: 19,99 €</p>
```

Für eine Maschine ist dieser String `"19,99 €"` schwer zu verarbeiten. Besser ist es, den reinen, standardisierten Wert mitzuliefern:

```html
<p>Preis: <data value="19.99">19,99 €</data></p>
```

Der `value`-Attributwert (`19.99`) ist nun eindeutig und international verständlich. Ein Skript könnte diesen Wert leicht auslesen und weiterverarbeiten, zum Beispiel für eine Währungsumrechnung.

Für eine noch bessere Semantik, besonders bei Preisen, kombinierst du das `data`-Element oft mit `data-*`-Attributen, um die Währung explizit anzugeben:

```html
<p>
  Preis: 
  <span class="price">
    <data value="19.99" data-currency="EUR">19,99 €</data>
  </span>
</p>
```

Damit schaffst du eine saubere Trennung: Der Inhalt des Elements ist für den Menschen, die Attribute sind für die Maschine. Das ist die perfekte Grundlage für die dynamische Formatierung.

#### Die Magie der Internationalisierungs-API in JavaScript

Die eigentliche Arbeit der Lokalisierung von Zahlen und Währungen auf der Client-Seite übernimmt JavaScript. Früher war dies eine komplexe Aufgabe, die oft den Einsatz großer Bibliotheken erforderte. Heute hat jeder moderne Browser eine leistungsstarke, eingebaute Schnittstelle dafür: die **Internationalization API**, kurz `Intl`.

Das zentrale Objekt für unsere Zwecke ist `Intl.NumberFormat`. Es ist ein Konstruktor, der ein Formatierungsobjekt erzeugt, das auf spezifische Sprach- und Ländereinstellungen (eine sogenannte "Locale") zugeschnitten ist.

Schauen wir uns ein einfaches Beispiel an. Wir haben eine Zahl und möchten sie für den deutschen und den amerikanischen Markt formatieren:

```javascript
const number = 1234567.89;

// Formatierung für Deutschland (de-DE)
const germanFormatter = new Intl.NumberFormat('de-DE');
console.log(germanFormatter.format(number)); 
// Ausgabe: "1.234.567,89"

// Formatierung für die USA (en-US)
const usFormatter = new Intl.NumberFormat('en-US');
console.log(usFormatter.format(number));
// Ausgabe: "1,234,567.89"
```

Wie du siehst, kümmert sich `Intl.NumberFormat` automatisch um die korrekten Tausender- und Dezimaltrennzeichen, basierend auf dem Locale-Code, den du übergibst (z. B. `de-DE`).

Noch eindrucksvoller wird es bei der Formatierung von Währungen. Hierfür übergeben wir ein zweites Argument an den Konstruktor, ein Objekt mit Konfigurationsoptionen. Die wichtigsten sind `style` und `currency`.

```javascript
const price = 1999.50;

// Preisformatierung für Deutschland in Euro
const euroFormatter = new Intl.NumberFormat('de-DE', {
  style: 'currency',
  currency: 'EUR' // ISO 4217 Währungscode
});
console.log(euroFormatter.format(price));
// Ausgabe: "1.999,50 €"

// Preisformatierung für die USA in US-Dollar
const dollarFormatter = new Intl.NumberFormat('en-US', {
  style: 'currency',
  currency: 'USD'
});
console.log(dollarFormatter.format(price));
// Ausgabe: "$1,999.50"

// Preisformatierung für Japan in Yen (beachte die Rundung, da Yen keine Dezimalstellen hat)
const yenFormatter = new Intl.NumberFormat('ja-JP', {
  style: 'currency',
  currency: 'JPY'
});
console.log(yenFormatter.format(price));
// Ausgabe: "￥2,000"
```

Das ist die ganze Magie. Du musst nicht wissen, ob das Euro-Symbol vor oder nach dem Betrag steht oder ob ein Leerzeichen verwendet wird. `Intl` kennt die Konventionen für hunderte von Locales und wendet sie korrekt an. Die Verwendung der standardisierten ISO 4217-Währungscodes (`EUR`, `USD`, `JPY`) ist dabei entscheidend, um Eindeutigkeit zu gewährleisten.

#### HTML und JavaScript verbinden: Eine praktische Anwendung

Nun führen wir alles zusammen. Wir erstellen eine HTML-Struktur, die unformatierte, maschinenlesbare Daten enthält, und verwenden JavaScript, um diese Daten für den Benutzer korrekt darzustellen.

Unser HTML könnte so aussehen:

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Produktseite</title>
</head>
<body>

  <h1>Unser Top-Produkt</h1>
  <p>
    Ein fantastisches Produkt zu einem unschlagbaren Preis von 
    <span class="price" data-value="49.99" data-currency="EUR"></span>!
  </p>
  <p>
    Verfügbar in den USA für 
    <span class="price" data-value="54.95" data-currency="USD"></span>.
  </p>

  <script src="formatter.js"></script>
</body>
</html>
```

Wir haben leere `<span>`-Elemente mit `data-*`-Attributen, die den Wert und die Währung enthalten. Das `lang`-Attribut im `<html>`-Tag gibt an, dass die Hauptsprache der Seite Deutsch ist. Das kann als Fallback für unsere Formatierung dienen.

Unser JavaScript in der Datei `formatter.js` könnte nun die Elemente suchen und den Inhalt dynamisch einfügen:

```javascript
document.addEventListener('DOMContentLoaded', () => {
  // Versuche, die Browsersprache des Benutzers zu ermitteln.
  // Falls nicht verfügbar, nutze die Sprache der Seite (aus dem lang-Attribut) 
  // oder falle auf Englisch (en-US) zurück.
  const userLocale = navigator.language || document.documentElement.lang || 'en-US';

  // Finde alle Elemente mit der Klasse 'price'
  const priceElements = document.querySelectorAll('.price');

  priceElements.forEach(element => {
    // Lies die Daten aus den data-Attributen aus
    const value = parseFloat(element.dataset.value);
    const currency = element.dataset.currency;

    // Stelle sicher, dass Wert und Währung gültig sind
    if (!isNaN(value) && currency) {
      try {
        // Erstelle einen Formatter für die erkannte Locale
        const formatter = new Intl.NumberFormat(userLocale, {
          style: 'currency',
          currency: currency,
          minimumFractionDigits: 2 // Sorge für immer zwei Nachkommastellen
        });
        
        // Formatiere den Preis und füge ihn in das Element ein
        element.textContent = formatter.format(value);
      } catch (error) {
        // Falls die Locale oder Währung ungültig ist, zeige einen Fallback an
        console.error("Fehler bei der Preisformatierung:", error);
        element.textContent = `${value.toFixed(2)} ${currency}`;
      }
    }
  });
});
```

Dieser Code durchläuft beim Laden der Seite alle Elemente mit der Klasse `price`. Er liest den Wert und die Währung aus, ermittelt die bevorzugte Sprache des Benutzers aus dem Browser und formatiert den Preis entsprechend. Das Ergebnis ist eine perfekt lokalisierte Darstellung, die sich an den Besucher anpasst, ohne dass du den HTML-Code ändern musst.

Die Darstellung von Zahlen und Währungen ist ein Paradebeispiel für progressive Verbesserung: Du beginnst mit semantisch reichem HTML, das die reinen Daten enthält. Das allein ist schon wertvoll. Dann fügst du mit JavaScript eine Schicht hinzu, die diese Daten in eine benutzerfreundliche, kontextsensitive Darstellung verwandelt. So schaffst du eine globale Webseite, die sich an jedem Ort der Welt zu Hause fühlt.
