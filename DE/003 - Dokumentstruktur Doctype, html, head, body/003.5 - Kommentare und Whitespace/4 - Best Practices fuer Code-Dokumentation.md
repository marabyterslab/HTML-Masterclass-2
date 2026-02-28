# Best Practices für Code-Dokumentation

### Mehr als nur Notizen: Best Practices der Code-Dokumentation

Stell dir vor, du öffnest ein Projekt, an dem du vor sechs Monaten zuletzt gearbeitet hast. Du schaust auf eine komplexe HTML-Struktur mit Dutzenden von verschachtelten `<div>`-Elementen und kryptischen Klassennamen. Ein vages Gefühl der Erinnerung beschleicht dich, aber die genaue Absicht hinter bestimmten Code-Zeilen ist wie weggewischt. Warum wurde hier ein `<span>` anstelle eines `<strong>` verwendet? Weshalb ist dieser eine Container mit Inline-Styles versehen, obwohl der Rest über eine externe CSS-Datei gestylt wird?

Genau in diesen Momenten wird dir die wahre Bedeutung von guter Code-Dokumentation schlagartig bewusst. Kommentare sind nicht nur Notizen für andere Entwickler in deinem Team; sie sind in erster Linie eine Botschaft an dein zukünftiges Ich. Sie sind die Brotkrumen, die du heute auslegst, damit du morgen den Weg durch den Wald deines eigenen Codes zurückfindest.

#### Kommentiere das „Warum“, nicht das „Was“

Die wichtigste Regel für eine effektive Dokumentation lässt sich in einem einzigen Satz zusammenfassen: Erkläre, *warum* du etwas tust, nicht, *was* du tust. Dein Code sollte idealerweise selbsterklärend sein. Ein gut benanntes HTML-Element oder eine klare CSS-Klasse verrät bereits, was seine Aufgabe ist.

Betrachte dieses schlechte Beispiel:

```html
<!-- Dies ist die Hauptnavigation -->
<nav class="main-navigation">
  <!-- Eine ungeordnete Liste für die Links -->
  <ul>
    <!-- Ein Listenelement -->
    <li><a href="/">Startseite</a></li>
  </ul>
</nav>
```

Diese Kommentare sind vollkommen überflüssig. Das `<nav>`-Tag sagt uns bereits, dass es sich um eine Navigation handelt. Die Klasse `main-navigation` verstärkt diese Information. Jeder, der grundlegendes HTML versteht, weiß, was `<ul>` und `<li>` sind. Solche Kommentare blähen den Code nur auf und lenken vom Wesentlichen ab. Sie sind wie ein Straßenschild, auf dem „Straße“ steht.

Ein guter Kommentar hingegen liefert Kontext, den der Code allein nicht vermitteln kann. Er erklärt die Hintergründe einer Entscheidung, weist auf Besonderheiten hin oder warnt vor potenziellen Problemen.

Hier ist ein deutlich besseres Beispiel:

```html
<!-- Wir verwenden hier ein <div> anstelle eines <button>, 
     weil ein externer A/B-Testing-Dienst nur Klicks auf <div>s mit einer 
     bestimmten Klasse tracken kann. Die Button-Funktionalität (ARIA-Rollen, 
     Tastatur-Events) wird über 'button-enhancer.js' hinzugefügt. -->
<div class="custom-button promo-cta" role="button" tabindex="0">
  Jetzt Angebot sichern!
</div>
```

Dieser Kommentar ist Gold wert. Er erklärt eine auf den ersten Blick seltsame Entscheidung (ein `<div>` als Button) und liefert die Begründung (technische Einschränkung eines externen Tools). Er gibt sogar einen Hinweis darauf, wo die zugehörige Logik zu finden ist (`button-enhancer.js`). Dein Kollege – oder du in sechs Monaten – wird dir dafür danken.

#### Struktur und Klarheit: Wie du Kommentare effektiv einsetzt

Neben dem Inhalt ist auch die Form deiner Kommentare entscheidend. In HTML umschließt du einen Kommentar mit `<!--` und `-->`. Diese können sich über eine oder mehrere Zeilen erstrecken. Eine bewährte Methode, um größere HTML-Dokumente zu gliedern, ist die Verwendung von Abschnittskommentaren. Sie dienen als visuelle Anker und helfen dabei, sich schnell in einer langen Datei zurechtzufinden.

So könntest du zum Beispiel den Header-Bereich deiner Seite klar kennzeichnen:

```html
<!-- =================================================================
     HAUPTNAVIGATION START
     ================================================================== -->
<header class="site-header">
  <div class="logo">
    <a href="/">Mein Logo</a>
  </div>
  <nav class="main-navigation">
    <!-- ... Navigationslinks ... -->
  </nav>
</header>
<!-- =================================================================
     HAUPTNAVIGATION ENDE
     ================================================================== -->
```

Diese „Banner“-Kommentare stechen sofort ins Auge und schaffen eine klare visuelle Trennung zwischen den logischen Blöcken deiner Seite.

Eine weitere häufige Anwendung ist das temporäre Auskommentieren von Code. Wenn du etwas testen möchtest, ohne einen Code-Block komplett zu löschen, ist das ein nützliches Werkzeug.

```html
<div class="content">
  <p>Dieser Absatz ist sichtbar.</p>
  
  <!-- Temporär für Testzwecke deaktiviert (Ticket #472) -->
  <!-- 
  <div class="beta-feature">
    <p>Diese neue Funktion wird gerade entwickelt.</p>
  </div>
  -->
  
  <p>Dieser Absatz ist ebenfalls sichtbar.</p>
</div>
```

Achte jedoch darauf, auskommentierten Code nicht dauerhaft im Projekt zu belassen. Er sollte vor dem finalen Deployment oder der Übergabe in die Versionskontrolle (z. B. Git) entfernt werden, um den Code sauber zu halten. Ein kurzer Hinweis, warum etwas auskommentiert wurde (wie im Beispiel mit der Ticket-Nummer), ist dabei sehr hilfreich.

#### Die Fallstricke: Was du vermeiden solltest

So nützlich gute Kommentare sind, so schädlich können schlechte sein. Hier sind einige typische Fehler, die du unbedingt vermeiden solltest:

1.  **Veraltete Kommentare:** Der schlimmste Kommentar ist ein falscher Kommentar. Wenn du den Code änderst, musst du unbedingt auch die zugehörigen Kommentare anpassen. Ein Kommentar, der eine Funktionalität beschreibt, die nicht mehr existiert, ist irreführender und frustrierender als gar kein Kommentar. Er wird zur Lüge im Code.
2.  **Platzhalter-Kommentare:** Kommentare wie `// TODO: Hier später aufräumen` oder `<!-- Fix this -->` sind zwar gut gemeint, aber oft werden sie zu digitalen Ruinen, die nie wieder jemand anfasst. Wenn du ein `TODO` hinterlässt, sei spezifisch: Was genau muss getan werden? Warum? Gibt es eine Ticket-Nummer dazu? Beispiel: `<!-- TODO (#812): Auf das neue <dialog>-Element umstellen, sobald Browser-Support für IE11 entfällt. -->`
3.  **Unprofessionelle Kommentare:** Dein Code ist ein professionelles Produkt. Witze, Frust-Ablassungen oder abfällige Bemerkungen über den Code eines Kollegen haben darin nichts zu suchen. Halte deine Kommentare sachlich, klar und respektvoll.

#### Ein Blick über den Tellerrand: Kommentare in CSS und JavaScript

Die Prinzipien guter Dokumentation gelten natürlich nicht nur für HTML. Auch in CSS und JavaScript, den beiden anderen Säulen des modernen Webs, sind Kommentare unverzichtbar. Die Syntax unterscheidet sich, aber die Philosophie bleibt dieselbe.

In **CSS** verwendest du `/*` und `*/`, um einen Kommentarblock zu erstellen:

```css
/* =================================================================
   Button-Stile
   ================================================================= */

/* Haupt-Call-to-Action-Button */
.cta-button {
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
}

/* 
 * Wir verwenden hier !important, um einen Inline-Stil aus einem 
 * externen WordPress-Plugin zu überschreiben, das wir nicht 
 * direkt bearbeiten können. Siehe Dokumentation: [Link zum Ticket]
 */
.cta-button-in-sidebar {
  width: 100% !important; 
}
```

In **JavaScript** hast du zwei Möglichkeiten: einzeilige Kommentare mit `//` und mehrzeilige Blöcke mit `/* ... */`.

```javascript
// Berechnet den Bruttopreis basierend auf dem Nettopreis und dem Steuersatz.
// Der Steuersatz sollte als Dezimalzahl übergeben werden (z. B. 0.19 für 19 %).
function calculateGrossPrice(netPrice, taxRate) {
  // Wichtige Validierung, um Division durch Null oder ungültige Werte zu verhindern.
  if (netPrice <= 0 || taxRate < 0) {
    return 0;
  }
  return netPrice * (1 + taxRate);
}
```

In beiden Sprachen gilt: Erkläre komplexe Algorithmen, unübliche CSS-Regeln oder Workarounds für Browser-Bugs. Dokumentiere die Absicht hinter deinem Code.

#### Die stille Dokumentation: Whitespace und Einrückung

Zum Abschluss sei noch eine Form der Dokumentation erwähnt, die ganz ohne Worte auskommt: die Struktur deines Codes selbst. Konsequente und saubere Einrückung (Whitespace) ist eine Art „stiller Kommentar“. Sie visualisiert die Hierarchie und die Beziehungen zwischen den Elementen.

Betrachte diese beiden Code-Blöcke. Sie sind funktional identisch, aber ihre Lesbarkeit könnte unterschiedlicher nicht sein.

**Schlecht:**
```html
<div><ul><li><a href="#">Punkt 1</a></li><li><a href="#">Punkt 2</a>
<div><p>Ein verschachtelter Text</p></div></li></ul></div>
```

**Gut:**
```html
<div>
  <ul>
    <li>
      <a href="#">Punkt 1</a>
    </li>
    <li>
      <a href="#">Punkt 2</a>
      <div>
        <p>Ein verschachtelter Text</p>
      </div>
    </li>
  </ul>
</div>
```

Der zweite Block ist sofort verständlich. Du kannst die Schachtelung der Elemente auf einen Blick erfassen, ohne eine einzige Zeile lesen zu müssen. Eine saubere Code-Struktur reduziert den Bedarf an erklärenden Kommentaren und macht deinen Code von Grund auf wartbarer.

Denke daran: Guter Code ist nicht nur funktional, er ist auch lesbar und verständlich. Kommentare und eine saubere Struktur sind keine lästige Pflicht, sondern ein Zeichen von Professionalität und Empathie – gegenüber deinen Teamkollegen und vor allem gegenüber dir selbst. Dein Code ist nicht nur eine Anweisung für den Computer; er ist auch eine Kommunikationsform für Menschen.
