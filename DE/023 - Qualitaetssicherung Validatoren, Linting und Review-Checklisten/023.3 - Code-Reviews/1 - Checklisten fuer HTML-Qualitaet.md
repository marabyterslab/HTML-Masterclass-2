# Checklisten für HTML-Qualität

### Checklisten für HTML-Qualität: Dein Kompass im Code-Review

Automatisierte Werkzeuge wie Validatoren und Linter sind unverzichtbar. Sie fangen Syntaxfehler, veraltete Elemente oder formale Regelverstöße ab, bevor sie Schaden anrichten können. Doch sie können nicht alles sehen. Sie verstehen den Kontext nicht. Sie können nicht beurteilen, ob dein Code nicht nur *valide*, sondern auch *gut* ist – also semantisch korrekt, barrierefrei, wartbar und durchdacht.

Genau hier kommt der menschliche Faktor ins Spiel: das Code-Review. Und um diesen Prozess systematisch und effektiv zu gestalten, sind Checklisten ein unschätzbares Werkzeug. Sie sind kein starres Korsett, das deine Kreativität einschränkt, sondern ein Geländer, das dich sicher durch die Komplexität eines HTML-Dokuments führt. Eine gute Checkliste stellt sicher, dass du die wichtigen Aspekte nicht vergisst und eine gleichbleibend hohe Qualität gewährleistest.

Lass uns die wichtigsten Bereiche einer solchen Checkliste für HTML-Qualität im Detail betrachten.

#### 1. Struktur und Semantik

Dies ist das Herzstück von HTML. Die Sprache wurde entwickelt, um Dokumenten eine Bedeutung (Semantik) zu geben, nicht nur ein Aussehen. Ein Review muss daher immer prüfen, ob die gewählten Tags den Inhalt korrekt beschreiben.

*   **Korrekte Verwendung von Gliederungselementen:**
    *   Wird die grundlegende Seitenstruktur mit `<header>`, `<nav>`, `<main>`, `<aside>` und `<footer>` sinnvoll abgebildet?
    *   Ist der Hauptinhalt der Seite klar von einem `<main>`-Element umschlossen?
    *   Werden `<section>`- und `<article>`-Elemente korrekt eingesetzt? Eine `<section>` gruppiert thematisch zusammengehörige Inhalte, während ein `<article>` für sich allein stehend Sinn ergeben sollte (wie ein Blogbeitrag oder ein Produkt).
    *   **Anti-Beispiel (Div-Suppe):**
        ```html
        <div class="header">...</div>
        <div class="main-content">
          <div class="post">...</div>
        </div>
        <div class="sidebar">...</div>
        <div class="footer">...</div>
        ```
    *   **Gutes Beispiel:**
        ```html
        <header>...</header>
        <main>
          <article>...</article>
        </main>
        <aside>...</aside>
        <footer>...</footer>
        ```

*   **Logische Überschriftenhierarchie:**
    *   Gibt es genau eine `<h1>` pro Seite (oder pro Sectioning-Root wie `<article>`)?
    *   Folgen die Überschriftenebenen (`<h2>`, `<h3>` etc.) logisch aufeinander, ohne eine Ebene zu überspringen? (Auf eine `<h2>` sollte keine `<h4>` folgen). Dies ist nicht nur für die SEO, sondern vor allem für Nutzer von Screenreadern essenziell, die über Überschriften navigieren.

*   **Sinnvoller Einsatz von Text-Semantik:**
    *   Wird `<strong>` für inhaltlich wichtige (stark betonte) Texte verwendet und nicht nur, um Text fett darzustellen? Für rein visuelle Zwecke ist CSS zuständig. Dasselbe gilt für `<em>` (Betonung) im Gegensatz zu `<i>` (kursiv, z.B. für einen Fachbegriff).
    *   Sind Listen korrekt als `<ul>` (unsortiert), `<ol>` (sortiert) oder `<dl>` (Definitionsliste) ausgezeichnet? Ein häufiger Fehler ist, Absätze mit Spiegelstrichen zu verwenden, statt eine echte Liste zu erstellen.
    *   Werden Zitate mit `<blockquote>` (für längere Blöcke) und `<q>` (für kurze, inline-Zitate) ausgezeichnet?

#### 2. Barrierefreiheit (Accessibility, a11y)

Ein zugängliches Web ist keine Option, sondern eine Notwendigkeit. Viele Aspekte der Barrierefreiheit lassen sich direkt im HTML verankern und sollten bei jedem Review geprüft werden.

*   **Alternative Texte für Bilder:**
    *   Hat jedes `<img>`-Element ein `alt`-Attribut?
    *   Ist der Alternativtext aussagekräftig und beschreibt er den Inhalt des Bildes, falls dieses für den Kontext relevant ist? Beispiel: `alt="Ein Golden Retriever fängt einen roten Ball im Park."` statt `alt="hund"`.
    *   Wenn ein Bild rein dekorativ ist und keinen inhaltlichen Mehrwert bietet, ist das `alt`-Attribut leer (`alt=""`)? Dies signalisiert Screenreadern, das Bild zu ignorieren.

*   **Zugängliche Formulare:**
    *   Ist jedes Formularfeld (`<input>`, `<textarea>`, `<select>`) mit einem `<label>`-Element verknüpft?
    *   Erfolgt die Verknüpfung explizit über das `for`-Attribut des Labels und die `id` des Formularfelds? Dies stellt sicher, dass ein Klick auf das Label das zugehörige Feld fokussiert.
        ```html
        <label for="username">Benutzername:</label>
        <input type="text" id="username" name="username">
        ```
    *   Werden Eingabefelder sinnvoll gruppiert, z.B. mit `<fieldset>` und `<legend>`?

*   **ARIA-Attribute (falls verwendet):**
    *   Werden ARIA-Rollen (Accessible Rich Internet Applications) nur dann eingesetzt, wenn es kein natives HTML-Element für den Zweck gibt? Die erste Regel von ARIA lautet: "Verwende kein ARIA, wenn du es nicht musst."
    *   Sind ARIA-Attribute wie `aria-label`, `aria-expanded` oder `role` korrekt implementiert, um die Funktionalität von dynamischen Komponenten (z.B. Akkordeons, Tabs) für assistierende Technologien verständlich zu machen?

*   **Sprachauszeichnung:**
    *   Ist die Hauptsprache des Dokuments im `<html>`-Tag mit dem `lang`-Attribut deklariert (z.B. `<html lang="de">`)? Dies hilft Screenreadern, den Text mit der richtigen Aussprache vorzulesen.

#### 3. Performance und Best Practices

HTML selbst hat direkten Einfluss darauf, wie schnell und effizient eine Webseite geladen und dargestellt wird.

*   **Optimierung von Medien:**
    *   Wird bei Bildern, die nicht sofort sichtbar sind ("below the fold"), das Attribut `loading="lazy"` verwendet, um das Laden zu verzögern?
    *   Sind die Attribute `width` und `height` bei `<img>`-Tags gesetzt? Dies ermöglicht es dem Browser, den Platz für das Bild zu reservieren, bevor es geladen ist, und verhindert so störende Layout-Verschiebungen (Cumulative Layout Shift).

*   **Platzierung von Ressourcen:**
    *   Werden CSS-Dateien über `<link>`-Tags im `<head>` des Dokuments geladen? Dies stellt sicher, dass die Seite bereits während des Ladens korrekt gestylt wird (verhindert den "Flash of Unstyled Content").
    *   Werden JavaScript-Dateien (`<script>`), die nicht unmittelbar für den initialen Render-Vorgang benötigt werden, am Ende des `<body>`-Tags platziert oder mit den Attributen `defer` oder `async` versehen? Dadurch wird das Blockieren des Seitenaufbaus vermieden.

*   **Minimierung der DOM-Tiefe:**
    *   Ist die HTML-Struktur unnötig tief verschachtelt? Jedes Element im Document Object Model (DOM) kostet Speicher und Rechenzeit. Eine flachere Struktur ist oft performanter. Prüfe, ob überflüssige Wrapper-`<div>`s entfernt werden können.

#### 4. Lesbarkeit und Wartbarkeit

Code wird weitaus häufiger gelesen als geschrieben. Dein HTML sollte daher nicht nur für den Browser, sondern auch für andere Menschen (und dein zukünftiges Ich) verständlich sein.

*   **Konsistente Formatierung:**
    *   Ist der Code sauber und einheitlich eingerückt? Chaotischer Code ist schwer zu überblicken und fehleranfällig.
    *   Werden Attribute in einer konsistenten Reihenfolge geschrieben (z.B. `class`, `id`, `data-*`, `aria-*`)?

*   **Sinnvolle Kommentare:**
    *   Werden Kommentare verwendet, um komplexe oder nicht-offensichtliche Code-Abschnitte zu erklären? Ein Kommentar sollte das *Warum* erklären, nicht das *Was*.
    *   **Schlechter Kommentar:** `<!-- Ein Navigationsmenü -->`
    *   **Guter Kommentar:** `<!-- Hauptnavigation, wird auf Mobilgeräten durch ein Off-Canvas-Menü ersetzt -->`

*   **Klare Klassen- und ID-Namen:**
    *   Auch wenn dies oft in den Bereich von CSS fällt, ist es Teil des HTML-Reviews. Sind die `class`-Namen semantisch und beschreiben sie die Funktion des Elements, nicht sein Aussehen? (z.B. `class="news-teaser"` statt `class="red-box-left"`).

#### 5. Formale Korrektheit

Dieser Bereich überschneidet sich stark mit dem, was ein Validator prüft. Dennoch schadet eine manuelle Kontrolle der Grundlagen nie.

*   **Korrekter Doctype und Zeichensatz:**
    *   Beginnt das Dokument mit `<!DOCTYPE html>`?
    *   Ist der Zeichensatz als erstes Element im `<head>` definiert (`<meta charset="UTF-8">`)?

*   **Valides Nesting:**
    *   Sind alle Elemente korrekt geschachtelt und geschlossen? Ein häufiger Fehler ist das Verschachteln von Block-Elementen (wie `<div>`) innerhalb von Inline-Elementen (wie `<span>`) oder das Platzieren eines `<p>` in einem anderen `<p>`.

*   **Keine veralteten Elemente:**
    *   Werden obsolete Elemente wie `<font>`, `<center>` oder `<b>` (wenn `<strong>` gemeint ist) vermieden? Für die Präsentation ist ausschließlich CSS zuständig.

Eine solche Checkliste mag auf den ersten Blick umfangreich erscheinen. Doch mit der Zeit werden diese Prüfungen zur zweiten Natur. Sie helfen dir, einen systematischen Blick zu entwickeln, der über die reine Funktionalität hinausgeht und die Qualität deines HTML-Codes auf ein professionelles Niveau hebt. Sie ist dein verlässlicher Partner, um sauberen, robusten und zukunftssicheren Code zu schreiben.
