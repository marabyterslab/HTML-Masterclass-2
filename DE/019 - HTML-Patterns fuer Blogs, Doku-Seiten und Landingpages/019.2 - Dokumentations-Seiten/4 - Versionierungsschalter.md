# Versionierungsschalter

### Der Versionierungsschalter: Dokumentation für jede Epoche

Wenn du eine Dokumentationsseite für ein Softwareprojekt, eine API oder eine Bibliothek erstellst, stehst du vor einer besonderen Herausforderung: Veränderung. Software lebt, sie entwickelt sich weiter. Version 1.0 hat andere Funktionen als Version 2.0, und manche Methoden, die in Version 2.5 als "deprecated" (veraltet) markiert wurden, sind in Version 3.0 vielleicht komplett verschwunden.

Deine Nutzer sind dabei nicht immer auf dem neuesten Stand. Ein Entwicklerteam, das auf einer älteren, stabilen Version deines Produkts aufbaut, benötigt zwingend die Dokumentation für genau diese Version. Ein neues Team, das gerade einsteigt, sollte hingegen direkt mit der neuesten Version arbeiten. Wie stellst du sicher, dass jeder die richtige Information zur richtigen Zeit findet? Die Antwort ist ein eleganter und essenzieller HTML-Pattern: der Versionierungsschalter.

#### Das Grundprinzip: Eine URL pro Version

Das Herzstück eines jeden Versionierungssystems auf einer Webseite ist eine klare und verlässliche URL-Struktur. Bevor du auch nur eine Zeile HTML schreibst, muss die Strategie für die Adressierung der verschiedenen Versionen feststehen. Die bewährteste Methode ist, die Versionsnummer als Teil des URL-Pfades zu integrieren.

Stell dir vor, deine Dokumentation liegt unter `docs.deine-firma.de`. Die Struktur könnte so aussehen:

*   **Version 2.1:** `https://docs.deine-firma.de/v2.1/komponente-a.html`
*   **Version 2.2:** `https://docs.deine-firma.de/v2.2/komponente-a.html`
*   **Neueste Version:** `https://docs.deine-firma.de/latest/komponente-a.html`

Ein Alias wie `/latest/` ist eine fantastische Ergänzung. Er verweist immer auf die aktuellste stabile Version und gibt dir einen permanenten Link, den du in Tutorials und Marketingmaterialien verwenden kannst, ohne ihn bei jedem Update anpassen zu müssen.

Mit dieser sauberen URL-Struktur als Fundament wird der HTML-Schalter zu einer reinen Navigationsaufgabe: Er muss den Nutzer lediglich von der einen URL zur anderen leiten.

#### Pattern 1: Die semantische Navigationsliste

Die einfachste und aus Sicht der Barrierefreiheit robusteste Methode ist eine klassische Navigationsliste. Sie ist für jeden sofort verständlich, funktioniert ohne JavaScript und wird von Screenreadern und Suchmaschinen perfekt interpretiert.

Das HTML dafür ist erfrischend unkompliziert. Wir verwenden ein `<nav>`-Element, da es sich um eine Form der Seitennavigation handelt, und darin eine ungeordnete Liste `<ul>`.

```html
<nav aria-label="Dokumentationsversionen">
  <ul>
    <li><a href="/v1.0/index.html">Version 1.0</a></li>
    <li><a href="/v2.0/index.html">Version 2.0</a></li>
    <li>
      <a href="/v2.1/index.html" aria-current="page">Version 2.1 (Aktuell)</a>
    </li>
    <li><a href="/latest/index.html">Neueste Version (latest)</a></li>
  </ul>
</nav>
```

Lass uns dieses kleine Stück Code genauer betrachten:

1.  **`<nav aria-label="Dokumentationsversionen">`**: Das `<nav>`-Element signalisiert, dass hier ein Navigationsblock beginnt. Das `aria-label`-Attribut ist Gold wert für die Barrierefreiheit. Ein Screenreader wird dem Nutzer ansagen: „Navigation, Dokumentationsversionen“, was den Kontext sofort klar macht. Ohne dieses Label würde der Nutzer nur „Liste mit vier Einträgen“ hören.

2.  **`<ul>` und `<li>`**: Eine simple Liste ist die semantisch korrekte Art, eine Gruppe von gleichwertigen Navigationslinks zu strukturieren. Jede Version ist ein Listeneintrag.

3.  **`<a href="...">`**: Jeder Link verweist direkt auf die Startseite der jeweiligen Dokumentationsversion. Der Pfad (`/v2.1/index.html`) ist hierbei der entscheidende Teil.

4.  **`aria-current="page"`**: Dieses Attribut ist ein kleiner Superheld der Barrierefreiheit. Es teilt assistiven Technologien (wie Screenreadern) mit, dass dieser Link auf die **aktuell angezeigte Seite** verweist. Visuell würdest du diesen Link wahrscheinlich hervorheben (z.B. fett oder mit einer anderen Farbe), und `aria-current="page"` ist das technische Äquivalent dazu. Es schafft Klarheit und Orientierung.

Mit ein wenig CSS kannst du diese Liste leicht als Dropdown-Menü, als horizontale Button-Gruppe oder als seitliche Navigationsleiste gestalten. Die HTML-Grundlage bleibt dabei dieselbe: solide, verständlich und zugänglich.

#### Pattern 2: Das kompakte Dropdown mit `<select>`

Manchmal ist der Platz knapp, besonders im Header einer Seite oder auf mobilen Geräten. Eine lange Liste von Versionen kann schnell unübersichtlich werden. In solchen Fällen ist ein Dropdown-Menü, implementiert mit dem `<select>`-Element, eine beliebte Alternative. Es ist kompakt und den meisten Nutzern bestens vertraut.

Um es semantisch korrekt und funktional zu gestalten, binden wir das `<select>`-Element in ein `<form>` ein und geben ihm ein aussagekräftiges `<label>`.

```html
<form class="version-switcher">
  <label for="version-select">Version wechseln:</label>
  <select id="version-select" name="version">
    <option value="/v1.0/">Version 1.0</option>
    <option value="/v2.0/">Version 2.0</option>
    <option value="/v2.1/" selected>Version 2.1</option>
    <option value="/latest/">Neueste Version</option>
  </select>
</form>
```

Hier passiert schon etwas mehr:

1.  **`<form>`**: Das Formular dient als Container. Technisch gesehen senden wir hier zwar keine Daten an einen Server, aber es bietet einen guten semantischen Rahmen.

2.  **`<label for="version-select">`**: Ein `<label>` ist für die Barrierefreiheit von Formularelementen unverzichtbar. Es verknüpft den sichtbaren Text („Version wechseln:“) mit dem `<select>`-Element über die `for`- und `id`-Attribute. Ein Klick auf das Label setzt den Fokus auf das Dropdown, und Screenreader lesen das Label vor, wenn das Element fokussiert wird.

3.  **`<select id="version-select" name="version">`**: Das ist unser eigentliches Dropdown-Menü.

4.  **`<option value="...">`**: Jede `<option>` repräsentiert eine wählbare Version. Der entscheidende Teil ist das `value`-Attribut. Hier hinterlegen wir den relativen URL-Pfad zur jeweiligen Version. Der Text zwischen den `<option>`-Tags ist das, was der Nutzer sieht (z.B. „Version 2.1“).

5.  **`selected`**: Das `selected`-Attribut wird auf die `<option>` gesetzt, die der aktuell angezeigten Version entspricht. Der Browser wählt diesen Eintrag standardmäßig aus, wenn die Seite geladen wird.

**Die Magie des JavaScripts**

Im Gegensatz zur reinen Link-Liste benötigt dieses `<select>`-Pattern ein kleines bisschen JavaScript, um zu funktionieren. Das HTML allein kann den Nutzer nicht weiterleiten, wenn eine andere Option gewählt wird. Das dazugehörige JavaScript ist jedoch denkbar einfach. Es lauscht auf eine Änderung im Dropdown (`change`-Event) und leitet den Browser dann an die im `value` der ausgewählten Option hinterlegte URL weiter.

```javascript
// Finde das select-Element im Dokument
const versionSelect = document.getElementById('version-select');

// Füge einen Event-Listener hinzu, der auf Änderungen reagiert
versionSelect.addEventListener('change', function() {
  // Hole den Wert (die URL) der ausgewählten Option
  const newVersionUrl = this.value;

  // Leite den Browser zur neuen URL weiter
  if (newVersionUrl) {
    window.location.href = newVersionUrl;
  }
});
```

Dieser Ansatz ist elegant, weil er die Verantwortlichkeiten klar trennt:
*   **HTML** strukturiert die Auswahlmöglichkeiten und stellt die Ziel-URLs bereit.
*   **CSS** kümmert sich um das Aussehen des Dropdowns.
*   **JavaScript** fügt die Interaktivität hinzu und führt die Weiterleitung aus.

Falls JavaScript im Browser des Nutzers deaktiviert sein sollte, passiert einfach nichts. Das ist nicht ideal, aber die Seite bleibt benutzbar. Für eine robustere Lösung könntest du dem `<form>`-Element einen "Go"-Button hinzufügen. Ohne JavaScript würde ein Klick auf diesen Button das Formular an den Server senden (wo eine Weiterleitung stattfinden könnte), während du mit JavaScript den Button versteckst und die automatische Weiterleitung per `change`-Event aktivierst. Dies nennt man "Progressive Enhancement".

#### Welches Pattern ist das richtige für dich?

Die Wahl zwischen der Link-Liste und dem `<select>`-Dropdown hängt von deinem Design und deinen Prioritäten ab.

*   **Verwende die Navigationsliste (`<nav>` und `<ul>`)**, wenn:
    *   Du nur wenige Versionen hast (z.B. 2-4).
    *   Barrierefreiheit und eine funktionsfähige Seite ohne JavaScript oberste Priorität haben.
    *   Du die Versionen prominent und direkt anklickbar darstellen möchtest.

*   **Verwende das `<select>`-Dropdown**, wenn:
    *   Du viele Versionen zur Auswahl anbieten musst und Platz sparen willst.
    *   Du eine UI bevorzugst, die den Nutzern von anderen Webseiten vertraut ist.
    *   Ein kleines bisschen JavaScript für deine Seite kein Problem darstellt.

Beide Patterns lösen die gleiche Aufgabe auf eine fachlich korrekte Weise. Ein gut implementierter Versionierungsschalter ist kein auffälliges Feature, sondern ein stiller Helfer im Hintergrund. Er reduziert Frustration, schafft Vertrauen und sorgt dafür, dass deine Dokumentation für jeden Nutzer, egal auf welcher Version er sich befindet, ein verlässlicher Partner bleibt.
