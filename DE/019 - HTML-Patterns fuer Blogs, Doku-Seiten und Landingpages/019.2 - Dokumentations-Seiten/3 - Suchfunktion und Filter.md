# Suchfunktion und Filter

### Suchfunktion und Filter: Wegweiser durch den Wissensdschungel

Stell dir eine riesige Bibliothek ohne Katalogsystem vor. Du wüsstest, dass das gesuchte Wissen irgendwo in den Regalen steht, aber die Suche danach wäre eine frustrierende, fast unmögliche Aufgabe. Eine Dokumentations-Seite ohne eine gute Such- und Filterfunktion ist wie diese Bibliothek. Sie mag Unmengen an wertvollen Informationen enthalten, doch ohne die richtigen Werkzeuge bleiben diese für deine Nutzer verborgen. Eine effektive Navigation ist kein Luxus, sondern der Kern einer guten User Experience. Deine Nutzer kommen auf deine Seite, um eine Antwort auf eine konkrete Frage zu finden – und das so schnell wie möglich.

#### Das Herzstück: Das Suchfeld

Der universellste Einstiegspunkt in jede Dokumentation ist das Suchfeld. Es ist die erste Anlaufstelle für Nutzer, die genau wissen, was sie suchen, oder zumindest eine Ahnung davon haben. Die HTML-Struktur dafür ist auf den ersten Blick denkbar einfach, doch die semantischen Details machen den Unterschied.

Die Grundlage bildet das `<input>`-Element mit dem Typ `search`.

```html
<input type="search" id="doc-search" name="q" placeholder="Dokumentation durchsuchen...">
```

Warum `type="search"` und nicht einfach `type="text"`? Semantisch teilst du dem Browser und assistiven Technologien mit, dass dieses Feld für eine Suchanfrage bestimmt ist. Viele moderne Browser rendern ein solches Feld zudem mit einem kleinen "x"-Symbol am Ende, das es dem Nutzer erlaubt, die Eingabe mit einem Klick zu löschen. Das ist eine kleine, aber feine Verbesserung der Benutzerfreundlichkeit. Das `placeholder`-Attribut gibt einen visuellen Hinweis auf den Zweck des Feldes, sollte aber niemals ein `<label>`-Element ersetzen.

Für eine robuste und zugängliche Implementierung solltest du das Suchfeld immer in ein `<form>`-Element einbetten und mit einem `<label>` verknüpfen.

```html
<form role="search" class="search-form">
  <label for="doc-search" class="visually-hidden">Suche</label>
  <input type="search" id="doc-search" name="q" placeholder="Dokumentation durchsuchen...">
  <button type="submit" aria-label="Suchen">
    <!-- Hier ein SVG-Icon für eine Lupe einfügen -->
    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
      <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
    </svg>
  </button>
</form>
```

Analysieren wir diese Struktur:

1.  **`<form role="search">`**: Das `form`-Element gruppiert die zusammengehörigen Eingabeelemente. Die `role="search"` ist eine ARIA-Landmark-Role, die Screenreadern signalisiert, dass dieser Bereich der Seite eine Suchfunktion darstellt. Das hilft Nutzern, direkt zu diesem wichtigen Feature zu springen.
2.  **`<label for="doc-search" class="visually-hidden">`**: Jedes Formularfeld braucht ein Label. Es verknüpft den sichtbaren Text mit dem Eingabefeld, was nicht nur die Klickfläche vergrößert, sondern für Screenreader-Nutzer unerlässlich ist. Oft ist das Design so, dass kein sichtbares Label gewünscht ist. In diesem Fall versteckst du es visuell mit einer CSS-Klasse (z. B. `.visually-hidden`), anstatt es wegzulassen. So bleibt es für assistive Technologien erhalten.
3.  **`<button type="submit">`**: Ein expliziter Senden-Button ist wichtig. Er erlaubt es Nutzern, die Suche sowohl durch einen Klick als auch durch das Drücken der Enter-Taste im Suchfeld auszulösen. Wenn du nur ein Icon (wie eine Lupe) verwendest, ist ein `aria-label` wie "Suchen" absolut notwendig, damit Screenreader den Zweck des Buttons ansagen können.

Während das HTML die Struktur vorgibt, wird die eigentliche Logik – das Durchsuchen eines Index, das Filtern von Artikeln und die Anzeige der Ergebnisse – typischerweise mit JavaScript umgesetzt. Die HTML-Struktur ist jedoch das stabile Fundament, auf dem diese Dynamik aufbaut.

#### Die Verfeinerung: Filter

Manchmal ist eine einfache Stichwortsuche zu ungenau. Der Nutzer erhält vielleicht Hunderte von Ergebnissen und muss diese weiter eingrenzen. Hier kommen Filter ins Spiel. Sie erlauben es, die Ergebnismenge anhand spezifischer Kriterien wie Kategorie, Version, Programmiersprache oder Tags zu reduzieren.

HTML bietet uns ein ganzes Arsenal an Formularelementen, um Filter-Optionen semantisch korrekt abzubilden. Die beste Art, eine Gruppe zusammengehöriger Filter zu strukturieren, ist die Verwendung eines `<fieldset>` mit einer `<legend>`.

**Checkboxes für Mehrfachauswahl**

Wenn ein Nutzer mehrere Optionen gleichzeitig auswählen können soll (z. B. Artikel aus der Kategorie "API-Referenz" UND "Tutorials"), sind Checkboxes die richtige Wahl.

```html
<fieldset>
  <legend>Kategorien</legend>
  <div>
    <input type="checkbox" id="cat-api" name="category" value="api">
    <label for="cat-api">API-Referenz</label>
  </div>
  <div>
    <input type="checkbox" id="cat-guides" name="category" value="guides">
    <label for="cat-guides">Anleitungen</label>
  </div>
  <div>
    <input type="checkbox" id="cat-concepts" name="category" value="concepts">
    <label for="cat-concepts">Grundlagen</label>
  </div>
</fieldset>
```

Das `<fieldset>` gruppiert die Checkboxes logisch zusammen, und die `<legend>` dient als Überschrift für diese Gruppe. Dies ist für die Barrierefreiheit von großer Bedeutung, da Screenreader den Kontext ("Kategorien") für jede einzelne Checkbox vorlesen können.

**Radio-Buttons für Einfachauswahl**

Wenn sich Optionen gegenseitig ausschließen (z. B. Sortierung nach "Relevanz" ODER "Datum"), sind Radio-Buttons das Mittel der Wahl. Alle Radio-Buttons, die zum selben `name`-Attribut gehören, bilden eine Gruppe, aus der nur eine Option ausgewählt werden kann.

```html
<fieldset>
  <legend>Sortieren nach</legend>
  <div>
    <input type="radio" id="sort-relevance" name="sort" value="relevance" checked>
    <label for="sort-relevance">Relevanz</label>
  </div>
  <div>
    <input type="radio" id="sort-date" name="sort" value="date">
    <label for="sort-date">Datum (neueste zuerst)</label>
  </div>
</fieldset>
```

Das `checked`-Attribut bei der ersten Option sorgt dafür, dass standardmäßig eine sinnvolle Auswahl getroffen ist.

**Select-Boxen für lange Listen**

Wenn du sehr viele, sich gegenseitig ausschließende Optionen hast (z. B. die Auswahl einer spezifischen Software-Version aus einer langen Liste), kann eine `<select>`-Box platzsparender sein als eine endlose Liste von Radio-Buttons.

```html
<label for="version-select">Version</label>
<select name="version" id="version-select">
  <option value="v3.2">Version 3.2</option>
  <option value="v3.1">Version 3.1</option>
  <option value="v3.0">Version 3.0</option>
  <option value="v2.5">Version 2.5</option>
</select>
```

Diese Filter-Elemente werden oft in einer Seitenleiste (`<aside>`) neben der Ergebnisliste platziert und sind Teil eines größeren `<form>`-Elements.

#### Die Darstellung der Ergebnisse

Nachdem der Nutzer eine Suche oder Filterung ausgelöst hat, muss das Ergebnis klar und strukturiert präsentiert werden. Eine semantische Liste – entweder eine `<ul>` (unsortierte Liste) oder `<ol>` (geordnete Liste, falls die Reihenfolge eine Rolle spielt) – ist hierfür die beste Wahl.

Jedes Suchergebnis wird zu einem Listenelement `<li>`, das typischerweise einen Link zum eigentlichen Artikel, dessen Titel und eine kurze Beschreibung oder einen Auszug enthält.

```html
<div class="search-results" aria-live="polite">
  <h2>Suchergebnisse für "Datenbank"</h2>
  <ul>
    <li>
      <a href="/docs/guides/database-setup/">
        <h3>Datenbank einrichten</h3>
        <p>
          Eine schrittweise Anleitung, um deine erste <mark>Datenbank</mark> für das Projekt zu konfigurieren.
        </p>
      </a>
    </li>
    <li>
      <a href="/docs/api/database-connection/">
        <h3>API: DatabaseConnection</h3>
        <p>
          Die API-Referenz für die `DatabaseConnection`-Klasse zur Verwaltung von <mark>Datenbank</mark>-Verbindungen.
        </p>
      </a>
    </li>
    <!-- Weitere Ergebnisse -->
  </ul>
</div>
```

Beachte zwei wichtige Details in diesem Beispiel:

1.  **`<mark>`-Element**: Du kannst das Suchwort im Ergebnistext mit dem `<mark>`-Tag hervorheben. Dieses Element ist semantisch genau dafür gedacht: Textpassagen zu markieren, die für den aktuellen Kontext des Nutzers von besonderer Relevanz sind. Dies wird typischerweise per JavaScript dynamisch hinzugefügt.
2.  **`aria-live="polite"`**: Wenn die Suchergebnisse dynamisch ohne einen vollständigen Seiten-Neuladevorgang geladen werden, bemerken sehende Nutzer die Änderung sofort. Ein Screenreader-Nutzer jedoch nicht. Das Attribut `aria-live="polite"` auf dem Container der Ergebnisse weist den Screenreader an, seinen Nutzer über die Aktualisierung zu informieren, sobald er seine aktuelle Aufgabe beendet hat. Dies schafft eine inklusive Erfahrung für alle.

Vergiss auch nicht, den Fall zu behandeln, dass keine Ergebnisse gefunden wurden. Anstatt einfach nichts anzuzeigen, solltest du eine klare Rückmeldung geben.

```html
<div class="search-results">
  <h2>Keine Ergebnisse für "kryptonit"</h2>
  <p>Wir konnten leider keine passenden Artikel finden. Versuch es doch mit einem anderen Suchbegriff.</p>
</div>
```

Diese klare Kommunikation verhindert Frustration und hilft dem Nutzer, seine Suche anzupassen.

Die Kombination aus einem semantisch korrekten Suchformular, gut strukturierten Filteroptionen und einer zugänglichen Ergebnisliste bildet das Rückgrat einer jeden nutzerfreundlichen Dokumentation. Dein HTML legt dabei das Fundament, das nicht nur die visuelle Darstellung ermöglicht, sondern auch sicherstellt, dass die Funktionalität für jeden, unabhängig von seinen Fähigkeiten oder dem verwendeten Gerät, robust und verständlich ist.
