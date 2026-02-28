# Vor- und Nachteile gegenüber JSON-LD

### Microdata und RDFa: Ein direkter Vergleich mit JSON-LD

Nachdem du nun die Mechanismen von Microdata und RDFa kennengelernt hast, stehst du vielleicht vor der Frage: Wann setze ich was ein? Und was ist mit diesem JSON-LD, das so oft als die moderne Alternative genannt wird? Diese Frage ist absolut berechtigt, denn alle drei Technologien verfolgen dasselbe Ziel – deine Webinhalte für Maschinen verständlich zu machen –, gehen dabei aber fundamental unterschiedliche Wege. Lass uns die Ansätze direkt vergleichen, um ihre jeweiligen Stärken und Schwächen klar herauszuarbeiten.

#### Der fundamentale Unterschied: Integration vs. Trennung

Der größte und wichtigste Unterschied zwischen Microdata/RDFa und JSON-LD liegt darin, *wo* die strukturierten Daten im HTML-Dokument leben.

**Microdata und RDFa sind integrativ.** Sie nisten sich direkt in dein bestehendes HTML ein. Du nimmst deine sichtbaren Elemente – eine Überschrift, einen Absatz, ein Bild – und reicherst sie mit zusätzlichen Attributen (`itemscope`, `itemprop`, `property` usw.) an. Die strukturierten Daten sind also untrennbar mit dem Inhalt verbunden, den der Benutzer sieht.

Stell dir eine einfache Produktbeschreibung vor. Mit Microdata könnte sie so aussehen:

```html
<div itemscope itemtype="http://schema.org/Product">
  <h1 itemprop="name">Der ultimative Web-Entwickler-Kaffeebecher</h1>
  <img itemprop="image" src="kaffeebecher.jpg" alt="Ein Kaffeebecher mit Code-Schnipseln">
  <p itemprop="description">
    Der perfekte Begleiter für lange Nächte vor dem Code. Hält deinen Kaffee warm und deine Motivation hoch.
  </p>
  <div itemprop="offers" itemscope itemtype="http://schema.org/Offer">
    <span itemprop="priceCurrency" content="EUR">€</span>
    <span itemprop="price" content="14.99">14,99</span>
  </div>
</div>
```

Du siehst sofort: Die Metadaten sind direkt an die `<h1>`, `<img>`, `<p>` und `<span>`-Tags gekoppelt.

**JSON-LD verfolgt den Ansatz der Trennung.** Hier schreibst du deine strukturierten Daten in einen separaten Block, der für den Benutzer unsichtbar ist. Dieser Block ist in der Regel ein `<script>`-Tag vom Typ `application/ld+json`, das du meist im `<head>` oder am Ende des `<body>` deiner Seite platzierst. Dieser Block enthält ein JSON-Objekt, das die Informationen der Seite beschreibt, ohne die sichtbaren HTML-Tags zu berühren.

Dieselbe Produktbeschreibung mit JSON-LD würde so aussehen:

```html
<script type="application/ld+json">
{
  "@context": "http://schema.org",
  "@type": "Product",
  "name": "Der ultimative Web-Entwickler-Kaffeebecher",
  "image": "kaffeebecher.jpg",
  "description": "Der perfekte Begleiter für lange Nächte vor dem Code. Hält deinen Kaffee warm und deine Motivation hoch.",
  "offers": {
    "@type": "Offer",
    "priceCurrency": "EUR",
    "price": "14.99"
  }
}
</script>

<!-- Das sichtbare HTML kann völlig frei von Metadaten sein -->
<div>
  <h1>Der ultimative Web-Entwickler-Kaffeebecher</h1>
  <img src="kaffeebecher.jpg" alt="Ein Kaffeebecher mit Code-Schnipseln">
  <p>
    Der perfekte Begleiter für lange Nächte vor dem Code. Hält deinen Kaffee warm und deine Motivation hoch.
  </p>
  <div>
    <span>€</span>
    <span>14,99</span>
  </div>
</div>
```

Dieser grundlegende Unterschied – integrativ versus getrennt – ist die Quelle fast aller Vor- und Nachteile, die wir nun genauer betrachten.

---

#### Vorteile von Microdata und RDFa

Warum solltest du dich also für den integrativen Ansatz entscheiden? Es gibt einige Szenarien, in denen er durchaus seine Berechtigung hat.

**1. Direkte Kopplung an den Inhalt (Single Source of Truth)**

Der wohl stärkste Vorteil von Microdata und RDFa ist, dass die Daten genau dort stehen, wo der Inhalt ist. Wenn du den Preis eines Produkts auf deiner Webseite änderst, änderst du ihn direkt im `<span>`-Tag. Da das `itemprop="price"`-Attribut am selben Tag hängt, ist die Wahrscheinlichkeit gering, dass du vergisst, auch die strukturierten Daten zu aktualisieren.

Bei JSON-LD existieren die Daten an zwei Stellen: einmal im sichtbaren HTML für den Benutzer und einmal im unsichtbaren JSON-Block für die Maschinen. Wenn du den Preis im HTML änderst, musst du daran denken, ihn auch im `<script>`-Block zu ändern. Tust du das nicht, entsteht eine Diskrepanz. Suchmaschinen wie Google könnten im schlimmsten Fall annehmen, du versuchst, sie zu täuschen (z. B. einen niedrigeren Preis in den strukturierten Daten anzeigen, um Klicks zu generieren), was zu Abstrafungen führen kann. Microdata erzwingt hier eine gewisse Disziplin und kann die Wartung in einfachen Systemen erleichtern, da es nur eine „Quelle der Wahrheit“ gibt.

**2. Einfachheit bei simplen Strukturen**

Wenn du nur wenige, einfache Informationen auszeichnen möchtest – zum Beispiel den Autor und das Veröffentlichungsdatum eines Blogartikels –, kann das Hinzufügen von ein paar Attributen schneller und direkter sein als das Erstellen eines kompletten JSON-Strukturbaums.

```html
<article itemscope itemtype="http://schema.org/BlogPosting">
  <h1 itemprop="headline">Mein erster Blogartikel</h1>
  <p>Veröffentlicht am <time itemprop="datePublished" datetime="2023-10-27">27. Oktober 2023</time>
     von <span itemprop="author">Maria Musterfrau</span>.</p>
</article>
```

Das ist kurz, prägnant und für jeden, der HTML versteht, sofort nachvollziehbar. Der Overhead, einen separaten JSON-Block zu schreiben, könnte hier übertrieben wirken.

---

#### Nachteile von Microdata und RDFa (und die Stärken von JSON-LD)

Hand aufs Herz: In der modernen Webentwicklung überwiegen oft die Nachteile des integrativen Ansatzes. Google selbst empfiehlt mittlerweile JSON-LD als bevorzugtes Format, und das aus guten Gründen.

**1. Code-Unordnung und Komplexität**

Sobald deine Datenstrukturen komplexer werden, verwandelt sich der Vorteil der Integration schnell in einen Nachteil. Dein HTML wird mit einer Vielzahl von `itemprop`, `itemscope` und `itemtype`-Attributen überladen. Das macht den Code schwerer lesbar, unübersichtlicher und fehleranfälliger.

Stell dir vor, unser Produkt hat zusätzlich mehrere Bewertungen, einen Hersteller und verschiedene Angebote. Mit Microdata wird dein HTML schnell zu einem schwer wartbaren Geflecht aus verschachtelten `div`- und `span`-Elementen, die nur dazu da sind, die Datenstruktur abzubilden.

JSON-LD glänzt hier. Dein HTML bleibt sauber und semantisch korrekt und kümmert sich nur um die Darstellung. Die gesamte Komplexität der Datenstruktur wird in den sauberen, gut lesbaren JSON-Block ausgelagert. Das Prinzip der „Separation of Concerns“ (Trennung der Zuständigkeiten) wird hier vorbildlich umgesetzt: HTML für die Struktur, CSS für das Aussehen, JavaScript für die Interaktivität und JSON-LD für die reinen Daten.

**2. Mangelnde Flexibilität für nicht-sichtbare Daten**

Was ist, wenn du Daten bereitstellen möchtest, die für den Benutzer gar nicht sichtbar sind? Ein klassisches Beispiel ist die SKU (Stock Keeping Unit) oder die GTIN (Global Trade Item Number) eines Produkts. Diese Informationen sind für Maschinen (z. B. Google Shopping) extrem wichtig, für den menschlichen Besucher aber oft irrelevant.

Mit Microdata müsstest du auf einen Trick zurückgreifen und `<meta>`-Tags verwenden, um diese unsichtbaren Daten zu integrieren:

```html
<div itemscope itemtype="http://schema.org/Product">
  <meta itemprop="sku" content="12345-ABC">
  <h1 itemprop="name">Produktname</h1>
  ...
</div>
```

Das fühlt sich wie ein Workaround an und bläht dein HTML weiter auf.

In JSON-LD ist das überhaupt kein Problem. Du fügst einfach eine weitere Eigenschaft zu deinem JSON-Objekt hinzu. Die Daten müssen nicht im sichtbaren Teil der Seite vorhanden sein. Das gibt dir die Freiheit, wesentlich reichhaltigere und detailliertere Daten bereitzustellen, ohne dein Design oder deinen sichtbaren Inhalt zu beeinträchtigen.

```javascript
{
  "@context": "http://schema.org",
  "@type": "Product",
  "name": "Produktname",
  "sku": "12345-ABC", // Einfach hier hinzufügen
  "gtin13": "9780123456789", // Und hier auch
  ...
}
```

**3. Schwierigere dynamische Verwaltung**

In der Ära moderner JavaScript-Frameworks wie React, Vue oder Angular werden Webinhalte oft dynamisch auf dem Client generiert. In diesem Umfeld ist es viel einfacher und natürlicher, ein JavaScript-Objekt (also JSON) zu erstellen oder zu manipulieren und es dann in ein `<script>`-Tag zu schreiben.

Das dynamische Hinzufügen, Entfernen oder Ändern von HTML-Attributen in einem bereits gerenderten DOM-Baum ist umständlicher und fehleranfälliger. Da JSON das native Datenformat von JavaScript ist, fügt sich JSON-LD nahtlos in moderne Entwicklungsworkflows ein. Du kannst deine strukturierten Daten direkt aus deiner API-Antwort generieren und auf die Seite bringen, komplett entkoppelt von deiner Komponenten-Logik zur Darstellung.

**4. Einfachere Implementierung über Tag-Manager**

Für Marketing-Teams oder SEO-Spezialisten, die nicht direkt im Code arbeiten, ist JSON-LD ein Segen. Es kann relativ einfach über Tag-Management-Systeme (wie den Google Tag Manager) auf einer Webseite eingefügt werden, ohne dass ein Entwickler den Quellcode der Seite ändern muss. Man kann ein Skript erstellen, das die nötigen Informationen von der Seite ausliest (z. B. den Produkttitel aus der `<h1>`) und dynamisch das JSON-LD-Objekt zusammenbaut und injiziert. Mit Microdata oder RDFa wäre ein solcher Eingriff in die bestehende HTML-Struktur ungleich komplexer und riskanter.

#### Eine Entscheidungshilfe

Die Wahl zwischen Microdata/RDFa und JSON-LD hängt also stark von deinem Projekt, deinem Tech-Stack und deinen Prioritäten ab.

**Wähle Microdata oder RDFa, wenn:**

*   Du an einer sehr einfachen, meist statischen Webseite arbeitest.
*   Dein Content-Management-System (CMS) oder Template-System die Annotation von HTML-Attributen sehr einfach macht.
*   Die absolute Synchronität zwischen sichtbarem Inhalt und Metadaten für dich oberste Priorität hat und du das Risiko einer Daten-Diskrepanz minimieren willst.

**Wähle JSON-LD (in den meisten Fällen), wenn:**

*   Deine Datenstrukturen komplex oder verschachtelt sind.
*   Du Daten bereitstellen musst, die nicht auf der Seite sichtbar sind.
*   Du mit einem modernen JavaScript-Framework arbeitest (SPA).
*   Du eine saubere Trennung von Inhalt und Daten für bessere Wartbarkeit bevorzugst.
*   Die strukturierten Daten dynamisch oder über externe Tools wie einen Tag-Manager verwaltet werden sollen.

Obwohl Microdata und RDFa immer noch valide und funktionierende Technologien sind, hat sich der Wind klar in Richtung JSON-LD gedreht. Seine Flexibilität, Wartbarkeit und die hervorragende Integration in moderne Web-Architekturen machen es zur bevorzugten Wahl für die meisten neuen Projekte.
