# Screenreader-Verhalten

### Screenreader-Verhalten: Wie deine Website interpretiert wird

Stell dir vor, du schließt für einen Moment die Augen und versuchst, eine Website zu bedienen. Du kannst die visuelle Gestaltung nicht sehen – keine Farben, keine Layouts, keine Schriftgrößen. Alles, was dir bleibt, ist die Struktur und der Inhalt, der dir von einer Computerstimme vorgelesen wird. Genau das ist die Realität für Nutzerinnen und Nutzer von Screenreadern. Ein Screenreader ist kein Browser, der deine Seite „sieht“. Er ist eine Software, die den Code deiner Website – genauer gesagt den Accessibility Tree, der vom Browser aus dem DOM-Tree erstellt wird – interpretiert und in Sprache oder Brailleschrift umwandelt.

Um barrierefreie Websites zu entwickeln, musst du verstehen, wie diese Interpretation funktioniert. Es geht nicht darum, wie etwas aussieht, sondern darum, was es *bedeutet*. Und genau hier kommt semantisches HTML ins Spiel. Für einen Screenreader ist ein `<div>` mit einer `<h1>`-Optik nicht dasselbe wie ein echtes `<h1>`-Element. Das eine ist ein anonymer Container, das andere ist eine klare Ansage: „Achtung, hier beginnt der wichtigste Abschnitt dieser Seite.“

#### Die lineare Natur und die Suche nach Orientierung

Standardmäßig liest ein Screenreader eine Webseite von oben nach unten, Element für Element, so wie es im Quellcode steht. Das ist der sogenannte „virtuelle Cursor“ oder Lesemodus. Ein Nutzer könnte sich also theoretisch den gesamten Inhalt einer Seite von der ersten Zeile des Headers bis zur letzten Zeile des Footers vorlesen lassen. In der Praxis wäre das jedoch extrem ineffizient und frustrierend, besonders auf inhaltsreichen Seiten.

Sichtige Nutzer scannen eine Seite visuell. Sie erfassen das Layout in Sekundenbruchteilen, identifizieren den Header, die Navigation, den Hauptinhalt und den Footer. Sie überfliegen Überschriften, um relevante Abschnitte zu finden. Screenreader-Nutzer benötigen ebenfalls Mechanismen, um schnell zu navigieren und Inhalte zu überfliegen. Diese Mechanismen werden direkt durch dein HTML bereitgestellt.

Die wichtigsten Navigationsmethoden sind:

1.  **Navigation über Orientierungspunkte (Landmarks)**
2.  **Navigation über Überschriften**
3.  **Navigation über Links und Formularelemente**

#### 1. Orientierungspunkte: Die Landkarte deiner Seite

Semantische HTML5-Elemente wie `<header>`, `<nav>`, `<main>`, `<aside>`, `<section>` und `<footer>` sind für einen Screenreader nicht nur einfache Tags. Sie sind fundamentale **Orientierungspunkte** (Landmarks). Ein Nutzer kann seinen Screenreader anweisen, eine Liste aller Orientierungspunkte auf der Seite anzuzeigen und direkt zu einem bestimmten Bereich zu springen.

Stell es dir so vor:

*   **`<header>`:** Wird als „Banner“ oder „Seitenkopf“ angekündigt. Der Nutzer weiß sofort: Hier finde ich das Logo und vielleicht die Hauptnavigation.
*   **`<nav>`:** Wird als „Navigation“ angekündigt. Der Nutzer kann direkt hierher springen, um zu anderen Seiten der Website zu gelangen.
*   **`<main>`:** Wird als „Hauptinhalt“ angekündigt. Das ist der wichtigste Befehl überhaupt. Er ermöglicht es dem Nutzer, den gesamten einleitenden Teil (Header, Navigation) zu überspringen und direkt zum Kern der Seite zu gelangen. Ohne ein `<main>`-Element muss sich der Nutzer jedes Mal erneut durch die wiederkehrenden Elemente am Seitenanfang kämpfen.
*   **`<footer>`:** Wird als „Seitenfuß“ oder „Inhaltsinfo“ angekündigt. Hier erwartet der Nutzer Kontaktinformationen, Impressum oder Social-Media-Links.

Wenn du stattdessen nur `<div>`-Elemente verwendest, entfernst du diese eingebaute Landkarte.

**Negativbeispiel (die „Div-Suppe“):**

```html
<div class="header">
  <!-- Inhalt des Headers -->
</div>
<div class="navigation">
  <!-- Inhalt der Navigation -->
</div>
<div class="main-content">
  <!-- Inhalt des Hauptteils -->
</div>
<div class="footer">
  <!-- Inhalt des Footers -->
</div>
```

Ein Screenreader, der auf diesen Code trifft, sieht nur eine flache Abfolge von vier generischen `div`-Containern. Der Nutzer hat keine Möglichkeit, direkt zum Hauptinhalt zu springen. Er weiß nicht, wo die Navigation beginnt oder endet. Deine Seite ist ein Labyrinth ohne Schilder.

**Positivbeispiel (semantisch korrekt):**

```html
<header>
  <!-- Inhalt des Headers -->
</header>
<nav>
  <!-- Inhalt der Navigation -->
</nav>
<main>
  <!-- Inhalt des Hauptteils -->
</main>
<footer>
  <!-- Inhalt des Footers -->
</footer>
```

Hier ist die Struktur sofort klar. Der Screenreader kündigt jeden Bereich mit seiner Rolle an, und der Nutzer kann mühelos zwischen diesen Orientierungspunkten wechseln.

#### 2. Überschriften: Das Inhaltsverzeichnis deiner Seite

Überschriften (`<h1>` bis `<h6>`) sind die zweite entscheidende Navigationsebene. Sie sind nicht einfach nur größerer oder fetterer Text. Sie bilden die Gliederung deines Inhalts. Ein Screenreader-Nutzer kann sich eine Liste aller Überschriften auf der Seite anzeigen lassen, geordnet nach ihrer Ebene (1 bis 6).

Das ermöglicht es, den Inhalt einer Seite in Sekundenschnelle zu erfassen und direkt zu dem Abschnitt zu springen, der für ihn relevant ist. Dafür ist es jedoch unerlässlich, dass du die Überschriftenhierarchie logisch und korrekt einhältst:

*   Es sollte nur eine `<h1>` pro Seite geben, die den Haupttitel der Seite beschreibt.
*   Überschriftenebenen sollten nicht übersprungen werden. Auf eine `<h2>` folgt eine `<h3>`, nicht direkt eine `<h4>`.

Betrachte folgenden Code:

```html
<main>
  <h1>Der ultimative Guide zu HTML</h1>
  <p>Einleitungstext...</p>
  
  <h2>Grundlagen der Semantik</h2>
  <p>Text zu den Grundlagen...</p>
  
  <h3>Was sind Tags?</h3>
  <p>Text über Tags...</p>

  <h2>Formulare und Interaktivität</h2>
  <p>Text zu Formularen...</p>
</main>
```

Der Screenreader-Nutzer kann sich folgende Gliederung anzeigen lassen:
*   Überschrift Ebene 1: Der ultimative Guide zu HTML
*   Überschrift Ebene 2: Grundlagen der Semantik
    *   Überschrift Ebene 3: Was sind Tags?
*   Überschrift Ebene 2: Formulare und Interaktivität

Er kann nun direkt zum Abschnitt „Formulare und Interaktivität“ springen, ohne den gesamten Text über die Grundlagen lesen zu müssen. Wenn du stattdessen `<div>`s mit CSS-Klassen wie `.headline-1` oder `.sub-title` verwendest, geht diese gesamte Funktionalität verloren.

#### 3. Interaktive Elemente und ihre Beschriftung

Jedes interaktive Element – ein Link, ein Button, ein Formularfeld – wird von einem Screenreader mit seiner Rolle, seinem Namen und oft auch seinem Zustand (z. B. „aktiviert“) angekündigt. Der „Name“ eines Elements ist hierbei entscheidend.

**Links:**
Der Name eines Links ist sein Textinhalt. Ein Screenreader-Nutzer kann sich eine Liste aller Links auf einer Seite anzeigen lassen, um schnell zu navigieren. Deshalb sind nichtssagende Link-Texte wie „Hier klicken“ oder „Mehr erfahren“ ein Desaster für die Barrierefreiheit.

**Negativbeispiel:**
*   „Um den Bericht herunterzuladen, klicken Sie `<a>hier</a>`."
*   „Mehr Informationen zu unseren Produkten finden Sie `<a>hier</a>`."

In einer Liste von Links sieht der Nutzer nur „hier“, „hier“, „hier“ und hat keine Ahnung, wohin diese Links führen.

**Positivbeispiel:**
*   „Laden Sie den `<a>Jahresbericht 2023 (PDF)</a>` herunter."
*   „Erfahren Sie mehr `<a>über unsere innovativen Kaffeemaschinen</a>`."

Hier ist jeder Link-Text aussagekräftig und beschreibt klar das Ziel.

**Bilder:**
Bilder sind für einen Screenreader unsichtbar, es sei denn, du gibst ihnen eine textliche Alternative. Dafür ist das `alt`-Attribut da.

*   **Informative Bilder:** Wenn ein Bild eine Information vermittelt, die nicht bereits im umgebenden Text steht, muss diese Information im `alt`-Attribut beschrieben werden.
    ```html
    <img src="diagramm-umsatz.png" alt="Balkendiagramm, das den Umsatz von 2020 bis 2023 zeigt, mit einem starken Anstieg im letzten Jahr.">
    ```
    Der Screenreader liest vor: „Bild: Balkendiagramm, das den Umsatz …“.
*   **Dekorative Bilder:** Wenn ein Bild rein dekorativ ist (z. B. ein Schmuckelement oder eine Hintergrundgrafik), sollte das `alt`-Attribut leer gelassen werden (`alt=""`). Dies ist ein wichtiges Signal für den Screenreader, das Bild komplett zu ignorieren. Lässt du das `alt`-Attribut ganz weg, versuchen manche Screenreader stattdessen, den Dateinamen (`diagramm-umsatz.png`) vorzulesen, was nur für Verwirrung sorgt.

**Formulare:**
Die Verbindung zwischen einem Formularfeld und seiner Beschriftung ist essenziell. Ohne sie weiß der Nutzer nicht, welche Information in ein ` <input>`-Feld eingegeben werden soll. Die korrekte Verknüpfung erfolgt über das `<label>`-Element und die Attribute `for` und `id`.

```html
<label for="email-input">E-Mail-Adresse</label>
<input type="email" id="email-input">
```

Wenn der Nutzer nun mit dem Screenreader auf das Eingabefeld fokussiert, hört er: „E-Mail-Adresse, Eingabefeld“. Ohne das `<label>` würde er nur „Eingabefeld“ hören und müsste raten, was er eingeben soll.

Dein HTML-Code ist also mehr als nur eine Anweisung für den Browser, wie er etwas darstellen soll. Er ist das primäre Skript für Screenreader und andere assistierende Technologien. Jedes semantische Tag, das du verwendest, jede korrekte Überschriftenhierarchie und jedes aussagekräftige `alt`-Attribut ist ein Wegweiser, der Menschen mit Behinderungen hilft, sich auf deiner Seite zurechtzufinden. Gutes, sauberes und semantisches HTML ist die unumgängliche Grundlage für eine barrierefreie digitale Welt.
