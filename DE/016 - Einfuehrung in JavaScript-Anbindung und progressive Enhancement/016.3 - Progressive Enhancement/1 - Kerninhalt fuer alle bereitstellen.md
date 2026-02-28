# Kerninhalt für alle bereitstellen

# Kerninhalt für alle bereitstellen

Stell dir vor, du baust ein Haus. Du beginnst nicht mit der Dachrinne oder den Fenstern. Du beginnst mit einem soliden Fundament. Etwas, das allen Stürmen trotzt und die gesamte Struktur trägt. Erst wenn dieses Fundament sicher steht, baust du die Wände, setzt das Dach auf und kümmerst dich um die Inneneinrichtung, die Elektrik und die Wasserleitungen.

Im Webdesign ist diese Philosophie unter dem Namen **Progressive Enhancement** bekannt. Sie ist der Gegenentwurf zu einem Vorgehen, bei dem du mit der komplexesten Technologie beginnst und dann versuchst, "Fallback"-Lösungen für ältere Browser oder eingeschränkte Umgebungen zu schaffen (ein Ansatz, der als *Graceful Degradation* bekannt ist). Progressive Enhancement dreht diesen Spieß um: Du beginnst mit dem Wesentlichen, dem Kern deines Angebots, und stellst sicher, dass es für absolut jeden und unter allen Umständen zugänglich ist. Danach – und nur danach – fügst du Schicht für Schicht Verbesserungen hinzu, die das Erlebnis für Nutzer mit modernen Browsern und schnellen Verbindungen bereichern.

Der Kerninhalt ist dein Fundament. Und dieses Fundament wird mit HTML gebaut.

### Die Schichten des Weberlebnisses

Um dieses Prinzip zu verinnerlichen, ist es hilfreich, eine Webseite als eine Torte mit drei Schichten zu betrachten. Jede Schicht baut auf der vorherigen auf, aber die unterste Schicht ist auch für sich allein nahrhaft und vollständig.

#### Schicht 1: Der Inhalt und die Struktur (HTML)

Dies ist die Basis. Dein HTML-Dokument enthält die reinen Informationen – den Text, die Bilder, die Links, die Formulare. Es ist semantisch korrekt strukturiert, sodass nicht nur Menschen, sondern auch Maschinen (wie Suchmaschinen-Crawler oder Screenreader) den Inhalt verstehen können.

Ein grundlegendes Prinzip des Progressive Enhancement ist, dass diese HTML-Schicht für sich allein voll funktionsfähig sein muss. Ein Link muss zu einer anderen Seite führen. Ein Formular muss ohne JavaScript an den Server gesendet werden können. Ein Video sollte als HTML5-`<video>`-Element eingebunden sein, das der Browser nativ abspielen kann.

Nehmen wir ein einfaches Suchformular als Beispiel. In seiner grundlegendsten Form ist es reines HTML:

```html
<form action="/suche" method="GET">
  <label for="search-query">Suche:</label>
  <input type="search" id="search-query" name="q">
  <button type="submit">Suchen</button>
</form>
```

Dieses Formular funktioniert überall. Egal, ob JavaScript aktiviert ist, ob CSS geladen wird oder welche exotische Browsereinstellung ein Nutzer hat – er kann einen Suchbegriff eingeben, auf "Suchen" klicken und wird auf die Ergebnisseite (`/suche?q=suchbegriff`) weitergeleitet. Der Kerninhalt und die Kernfunktionalität sind für alle gesichert.

#### Schicht 2: Die Präsentation (CSS)

Sobald das HTML-Fundament steht, kommt die zweite Schicht: das Aussehen. Mit CSS machst du deine Webseite ansprechend und benutzerfreundlich. Du definierst Farben, Schriftarten, Layouts und Abstände. Du sorgst dafür, dass das Suchformular nicht wie eine graue Wüstenlandschaft aussieht, sondern sich nahtlos in dein Design einfügt.

```css
/* Eine einfache Gestaltung für unser Formular */
form {
  display: flex;
  gap: 8px;
  align-items: center;
}

label {
  font-weight: bold;
}

input[type="search"] {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button[type="submit"] {
  padding: 10px 15px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
```

Diese Schicht ist eine Verbesserung. Wenn das CSS aus irgendeinem Grund nicht geladen werden kann (z. B. wegen einer schlechten Netzwerkverbindung), ist die Webseite vielleicht nicht schön, aber sie ist immer noch voll funktionsfähig. Der Nutzer kann das Formular weiterhin bedienen. Die Torte schmeckt auch ohne Glasur.

#### Schicht 3: Das Verhalten (JavaScript)

Die oberste Schicht ist die Interaktivität, die du mit JavaScript hinzufügst. Hier entfaltet sich das volle Potenzial des modernen Webs. Diese Schicht sollte das bestehende, funktionierende Erlebnis verbessern, es aber niemals ersetzen oder zur Voraussetzung machen.

Für unser Suchformular könnten wir folgende Verbesserungen mit JavaScript hinzufügen:

1.  **Live-Suchvorschläge:** Während der Nutzer tippt, sendet JavaScript im Hintergrund Anfragen an den Server und zeigt eine Liste passender Vorschläge unter dem Suchfeld an.
2.  **AJAX-Formularversand:** Statt die Seite neu zu laden, fängt JavaScript das Absenden des Formulars ab, schickt die Daten via `fetch` an den Server und zeigt die Ergebnisse dynamisch auf derselben Seite an.

Der entscheidende Punkt ist: Was passiert, wenn das JavaScript fehlschlägt? Vielleicht hat der Nutzer es deaktiviert, eine Browser-Erweiterung blockiert dein Skript, oder es tritt ein Netzwerkfehler beim Laden der JS-Datei auf. Beim Progressive Enhancement lautet die Antwort: Nichts Schlimmes. Das Formular fällt einfach auf sein ursprüngliches HTML-Verhalten zurück. Der Nutzer tippt seinen Begriff ein, klickt auf den Button, und die Seite lädt neu, um die Ergebnisse anzuzeigen. Das Erlebnis ist nicht ganz so geschmeidig, aber es funktioniert. Die Kernfunktionalität bleibt erhalten.

### Ein praktisches Beispiel: Das Akkordeon-Widget

Ein klassisches Beispiel für Progressive Enhancement ist ein Akkordeon oder ein "Disclosure Widget", bei dem Inhalte per Klick ein- und ausgeklappt werden.

**Schritt 1: Das HTML-Fundament**

Ohne JavaScript gibt es keine Möglichkeit, Inhalte dynamisch ein- und auszublenden. Was ist also der logische Grundzustand? Alle Inhalte müssen sichtbar sein. So stellst du sicher, dass jeder – auch Suchmaschinen – alle Informationen lesen kann.

```html
<div class="accordion">
  <div>
    <h2>Frage 1: Was ist Progressive Enhancement?</h2>
    <div class="accordion-content">
      <p>Es ist eine Strategie im Webdesign, die darauf abzielt, Kerninhalte und -funktionalitäten für so viele Nutzer wie möglich zugänglich zu machen...</p>
    </div>
  </div>
  <div>
    <h2>Frage 2: Warum ist es wichtig?</h2>
    <div class="accordion-content">
      <p>Es sorgt für Robustheit, bessere Zugänglichkeit und eine gute Grundlage für SEO, da die Inhalte nicht von clientseitigem Scripting abhängig sind.</p>
    </div>
  </div>
</div>
```

In diesem Zustand ist die Seite eine einfache Liste von Fragen und Antworten. Perfekt lesbar und funktional.

**Schritt 2: CSS als Vorbereitung**

Das CSS gestaltet die Elemente, verbirgt aber zunächst nichts. Es sorgt nur für eine saubere Optik.

```css
.accordion h2 {
  background-color: #f1f1f1;
  padding: 12px;
  margin: 0;
  border-bottom: 1px solid #ddd;
}

.accordion-content {
  padding: 0 12px;
  border-bottom: 1px solid #ddd;
}
```

**Schritt 3: Die JavaScript-Verbesserung**

Jetzt kommt die Magie. Unser JavaScript hat mehrere Aufgaben:

1.  Es signalisiert, dass es aktiv ist. Eine gängige Methode ist, dem `<html>`- oder `<body>`-Tag eine Klasse hinzuzufügen.
2.  Es verbirgt die Inhalte, die standardmäßig sichtbar waren.
3.  Es fügt die Klick-Funktionalität hinzu, um die Inhalte wieder sichtbar zu machen.
4.  Es verbessert die Barrierefreiheit durch ARIA-Attribute.

```javascript
// Führe den Code aus, sobald das DOM geladen ist.
document.addEventListener('DOMContentLoaded', () => {
  // 1. Signalisiere, dass JS aktiv ist.
  document.documentElement.classList.add('js-enabled');

  const accordionHeaders = document.querySelectorAll('.accordion h2');

  accordionHeaders.forEach(header => {
    // Vorbereitung für die Barrierefreiheit
    const content = header.nextElementSibling;
    const contentId = 'content-' + Math.random().toString(36).substr(2, 9);
    content.id = contentId;

    header.setAttribute('aria-expanded', 'false');
    header.setAttribute('aria-controls', contentId);
    
    // Mache den Header klickbar (semantisch besser als nur ein div)
    const button = document.createElement('button');
    button.innerHTML = header.innerHTML;
    button.setAttribute('aria-expanded', 'false'); // Sync mit Header
    button.setAttribute('aria-controls', contentId);
    header.innerHTML = '';
    header.appendChild(button);

    // 3. Füge die Klick-Funktionalität hinzu
    button.addEventListener('click', () => {
      const isExpanded = button.getAttribute('aria-expanded') === 'true';
      
      // Zustand umkehren
      button.setAttribute('aria-expanded', !isExpanded);
      header.setAttribute('aria-expanded', !isExpanded); // Sync den H2-Wrapper
      content.hidden = isExpanded; // HTML5 hidden-Attribut nutzen
    });
  });
});
```

Jetzt brauchen wir noch ein kleines CSS-Update, das nur greift, wenn JavaScript aktiv ist:

```css
/* 2. Verberge die Inhalte nur, wenn JS läuft */
.js-enabled .accordion-content {
  /* Statt display: none nutzen wir das 'hidden' Attribut,
     das von unserem JS gesteuert wird. Initial setzen wir es hier. */
  display: none;
}

/* Zeige den Inhalt, wenn er nicht 'hidden' ist */
.js-enabled .accordion-content:not([hidden]) {
  display: block;
}

/* Style den Button im Header für bessere Interaktion */
.js-enabled .accordion h2 button {
  width: 100%;
  text-align: left;
  background: none;
  border: none;
  padding: 0;
  font: inherit;
  cursor: pointer;
}
```

Das Ergebnis: Nutzer ohne JavaScript sehen weiterhin die offene Liste der Fragen und Antworten. Nutzer mit JavaScript sehen ein sauberes, interaktives Akkordeon. Wir haben das Erlebnis verbessert, ohne jemanden auszuschließen.

### Warum dieser Ansatz Gold wert ist

Das Bereitstellen des Kerninhalts für alle ist mehr als nur eine technische Übung. Es ist eine Haltung, die deine Arbeit grundlegend verbessert:

*   **Robustheit:** Deine Webseite ist widerstandsfähig. Sie funktioniert auch bei langsamen Verbindungen, in Firmennetzwerken mit strengen Firewalls, auf alten Geräten oder wenn dein CDN für JavaScript-Dateien ausfällt.
*   **Zugänglichkeit (Accessibility):** Du schaffst eine grundsolide Basis für Menschen, die auf assistierende Technologien wie Screenreader angewiesen sind. Diese Werkzeuge arbeiten am besten mit klarem, semantischem HTML.
*   **Suchmaschinenoptimierung (SEO):** Suchmaschinen-Crawler sind wie Nutzer ohne JavaScript. Sie analysieren primär dein HTML. Wenn deine Inhalte nur per JavaScript nachgeladen werden, riskierst du, dass sie nicht oder nur unvollständig indiziert werden. Mit Progressive Enhancement liegt dein gesamter Inhalt von Anfang an klar und deutlich vor.
*   **Wartbarkeit und Zukunftssicherheit:** Ein Code, der in klaren Schichten aufgebaut ist, ist leichter zu verstehen, zu debuggen und zu erweitern. Du kannst die JavaScript-Schicht austauschen oder modernisieren, ohne das Fundament aus HTML und CSS anrühren zu müssen.

Indem du mit dem Kerninhalt beginnst und sicherstellst, dass er für alle zugänglich ist, baust du nicht nur Webseiten. Du baust verlässliche, inklusive und langlebige digitale Produkte. Du baust ein Haus auf einem Felsfundament, nicht auf Sand.
