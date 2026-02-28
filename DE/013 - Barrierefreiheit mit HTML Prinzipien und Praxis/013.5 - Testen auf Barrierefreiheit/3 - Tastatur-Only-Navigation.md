# Tastatur-Only-Navigation

### Tastatur-Only-Navigation: Die Welt ohne Maus erleben

Stell dir für einen Moment vor, deine Maus ist kaputt. Oder du hast dir den Arm gebrochen und kannst sie nur umständlich bedienen. Vielleicht gehörst du auch zu den „Power-Usern“, die aus Effizienzgründen lieber die Hände auf der Tastatur lassen. Oder, und das ist der entscheidende Punkt für die Barrierefreiheit, du bist auf assistive Technologien wie eine Bildschirmlesesoftware (Screenreader) oder eine Mund-Maus angewiesen, die primär oder ausschließlich über Tastaturbefehle gesteuert werden.

Für all diese Menschen ist die alleinige Bedienbarkeit einer Webseite per Tastatur keine Frage der Vorliebe, sondern eine absolute Notwendigkeit. Wenn eine Funktion nur mit der Maus erreichbar ist, ist sie für diese Nutzergruppe schlichtweg nicht existent. Deshalb gehört der Test der Tastatur-Navigation zu den fundamentalsten und gleichzeitig aufschlussreichsten Prüfungen der Barrierefreiheit, die du durchführen kannst. Es ist ein Test, der dich zwingt, deine eigene Webseite aus einer völlig neuen Perspektive zu erfahren.

#### Die Werkzeuge des Testers: Deine Tastatur

Für den grundlegenden Test benötigst du keine speziellen Tools. Deine Tastatur hat bereits alles, was du brauchst. Die wichtigsten Tasten sind:

*   **`Tab`**: Bewegt den Fokus zum nächsten interaktiven Element (Link, Button, Formularfeld etc.).
*   **`Shift + Tab`**: Bewegt den Fokus zum vorherigen interaktiven Element.
*   **`Enter`**: Aktiviert ein Element, das den Fokus hat (z. B. folgt einem Link oder löst einen Button aus).
*   **`Leertaste`**: Wählt Checkboxen aus oder ab, aktiviert Buttons.
*   **Pfeiltasten (`↑`, `↓`, `←`, `→`)**: Werden zur Navigation innerhalb von Komponentengruppen verwendet, wie z. B. bei Radio-Buttons, Auswahllisten, Menüs oder Slidern.
*   **`Esc`**: Schließt in der Regel modale Dialoge, Pop-ups oder aufklappende Menüs.

Der Test ist denkbar einfach: Lege deine Maus zur Seite und versuche, deine Webseite ausschließlich mit diesen Tasten zu bedienen. Versuche, jede einzelne Funktion auszuführen. Kannst du durch das Hauptmenü navigieren? Kannst du einen Artikel lesen und auf einen darin enthaltenen Link klicken? Kannst du das Kontaktformular ausfüllen und absenden?

Während dieses Prozesses achtest du auf vier entscheidende Aspekte.

#### 1. Der sichtbare Fokus: "Wo bin ich?"

Das absolut Wichtigste bei der Tastaturnavigation ist die Sichtbarkeit des Fokus. Wenn du die `Tab`-Taste drückst, muss zu jeder Zeit klar und deutlich erkennbar sein, welches Element gerade den Fokus hat. Browser bieten dafür standardmäßig einen visuellen Indikator, meist einen blauen oder schwarzen Rahmen (die sogenannte „Fokus-Kontur“ oder „Focus Ring“).

Leider ist eine der häufigsten Sünden im Webdesign, diesen Indikator aus ästhetischen Gründen zu entfernen:

```css
/* BITTE NICHT SO! Dies ist ein schwerwiegendes Barrierefreiheitsproblem. */
:focus {
  outline: none;
}
```

Wenn du diesen Code in deinem CSS findest, entfernst du die einzige Orientierungshilfe für Tastaturnutzer. Sie springen unsichtbar von Element zu Element und haben keine Ahnung, wo sie sich auf der Seite befinden oder was passiert, wenn sie `Enter` drücken.

Wenn dir der Standard-Fokusring des Browsers nicht gefällt, ist die Lösung nicht, ihn zu entfernen, sondern ihn an dein Design anzupassen. Gestalte einen eigenen, deutlich sichtbaren Fokus-Stil, der einen guten Kontrast zum Hintergrund hat. Eine moderne und nutzerfreundliche Methode ist die Verwendung der Pseudoklasse `:focus-visible`. Sie sorgt dafür, dass der Fokus-Stil primär bei Tastaturnavigation angezeigt wird, aber nicht unbedingt bei einem Mausklick, was oft der ursprüngliche Grund für das Entfernen des `outline` war.

```css
/* Eine gute, barrierefreie Alternative */
:focus-visible {
  outline: 3px solid #005fcc; /* Eine deutliche Farbe */
  outline-offset: 2px;
  border-radius: 4px; /* Optional, für eine schönere Optik */
}
```

**Beim Testen fragst du dich also:** Sehe ich *immer* und *sofort*, welches Element fokussiert ist?

#### 2. Die logische Reihenfolge: Ein sinnvoller Weg

Wenn du dich mit der `Tab`-Taste durch die Seite bewegst, sollte die Reihenfolge der fokussierten Elemente logisch und vorhersehbar sein. In den meisten westlichen Sprachen bedeutet das von links nach rechts und von oben nach unten – also entsprechend der visuellen Lesereihenfolge.

Solange du sauberes, semantisches HTML schreibst, ist die Fokusreihenfolge in der Regel von Natur aus korrekt, da sie der Reihenfolge der Elemente im DOM (Document Object Model) folgt. Probleme entstehen oft durch kreative CSS-Layouts. Mit Flexbox (`order`-Eigenschaft) oder CSS Grid kannst du Elemente visuell an eine ganz andere Stelle verschieben, als sie im HTML-Quellcode stehen. Für einen sehenden Nutzer mag das Layout perfekt aussehen, aber ein Tastaturnutzer springt dann möglicherweise vom Header direkt in den Footer und erst danach zur Hauptnavigation, was extrem verwirrend ist.

**Beim Testen fragst du dich also:** Entspricht die Sprungreihenfolge der visuellen und logischen Struktur der Seite? Oder springt der Fokus unvorhersehbar hin und her?

#### 3. Die Erreichbarkeit: Keine Sackgassen

Jedes interaktive Element, das ein Nutzer mit der Maus bedienen kann, muss auch per Tastatur erreichbar und bedienbar sein. Das klingt selbstverständlich, ist aber eine häufige Fehlerquelle.

Das klassische Problem sind Elemente, die zwar interaktiv sind, aber nicht aus semantisch korrektem HTML bestehen. Entwickler neigen manchmal dazu, `<div>`- oder `<span>`-Elemente mit einem JavaScript-`onclick`-Event zu versehen, um sie wie Buttons oder Links aussehen und funktionieren zu lassen.

```html
<!-- Schlecht: Nicht per Tastatur fokussierbar -->
<div class="custom-button" onclick="doSomething()">Klick mich</div>
```

Ein `<div>` ist von Natur aus nicht interaktiv. Browser nehmen es daher nicht in die `Tab`-Reihenfolge auf. Ein Tastaturnutzer wird dieses Element niemals erreichen. Die Lösung ist einfach und robust: Nutze die richtigen HTML-Elemente für den richtigen Zweck.

```html
<!-- Gut: Nativ fokussierbar und bedienbar -->
<button type="button" onclick="doSomething()">Klick mich</button>
```

Ein `<button>`-Element ist von Haus aus per Tastatur fokussierbar und kann mit `Enter` oder der `Leertaste` aktiviert werden. Dasselbe gilt für `<a>`-Elemente mit einem `href`-Attribut, `<input>`-Felder und andere Formularelemente.

#### Die Rolle von `tabindex`

Manchmal musst du jedoch Komponenten bauen, für die es kein natives HTML-Element gibt. In solchen Fällen kannst du die Fokus-Reihenfolge mit dem `tabindex`-Attribut steuern.

*   **`tabindex="0"`**: Fügt ein Element, das normalerweise nicht fokussierbar ist (wie ein `<div>`), in die natürliche `Tab`-Reihenfolge ein. Es wird an der Position fokussiert, an der es im DOM erscheint. Dies sollte sparsam und nur dann eingesetzt werden, wenn du benutzerdefinierte interaktive Komponenten (Widgets) erstellst.

    ```html
    <!-- Macht ein Div fokussierbar. Zusätzliche ARIA-Attribute und Event-Handler für Enter/Space sind nötig! -->
    <div tabindex="0" role="button" onclick="doSomething()" onkeydown="handleKeyDown(event)">
      Klick mich
    </div>
    ```

*   **`tabindex="-1"`**: Macht ein Element programmatisch fokussierbar (z. B. über JavaScript mit `element.focus()`), entfernt es aber aus der natürlichen `Tab`-Reihenfolge. Das ist nützlich, um den Fokus gezielt zu steuern, etwa um ihn nach einer Aktion auf eine Fehlermeldung oder den Beginn des Hauptinhalts zu setzen, ohne die normale Tab-Navigation zu stören.

*   **`tabindex` mit einem positiven Wert (`1`, `2`, `3`, ...)**: **Vermeide dies unter allen Umständen!** Ein positiver `tabindex` erzwingt eine feste, starre Fokus-Reihenfolge. Elemente mit `tabindex="1"` werden zuerst angesprungen, dann die mit `tabindex="2"` und so weiter, bevor die Elemente ohne `tabindex` oder mit `tabindex="0"` an die Reihe kommen. Dies zerstört die natürliche, vom DOM abgeleitete Reihenfolge und führt fast immer zu einer unlogischen und frustrierenden Nutzererfahrung. Es ist ein Albtraum für die Wartung und ein klares Anzeichen für ein schlecht strukturiertes Dokument.

**Beim Testen fragst du dich also:** Kann ich wirklich *jedes* klickbare Element auch mit der Tastatur erreichen und auslösen?

#### 4. Die Tastaturfalle: Kein Entkommen?

Eine Tastaturfalle (Keyboard Trap) ist einer der kritischsten Barrierefreiheitsfehler. Sie tritt auf, wenn ein Nutzer mit der Tastatur in eine Komponente oder einen Bereich der Webseite navigieren kann, diesen aber nicht mehr verlassen kann, um zum Rest der Seite zurückzukehren. Der Fokus ist gefangen und dreht sich nur noch innerhalb der Komponente im Kreis. `Tab` und `Shift + Tab` führen nicht mehr aus der Falle heraus.

Dieses Problem tritt häufig bei schlecht implementierten modalen Dialogen, Cookie-Bannern, Video-Playern oder eingebetteten Widgets von Drittanbietern (z. B. Social-Media-Feeds) auf. Der einzige Ausweg für den Nutzer ist oft, den Tab zu schließen oder die Seite komplett neu zu laden.

**Beim Testen fragst du dich also:** Wenn ich in ein modales Fenster, ein Pop-up oder ein komplexes Widget navigiere, komme ich mit `Tab` oder `Shift + Tab` auch wieder heraus? Funktioniert die `Esc`-Taste, um den Dialog zu schließen?

Der Test der Tastatur-Navigation ist mehr als eine technische Prüfung. Er ist ein Akt der Empathie. Er zwingt dich, die Hürden zu erleben, die viele Menschen täglich im Web überwinden müssen. Eine Webseite, die sich flüssig und logisch mit der Tastatur bedienen lässt, ist nicht nur barrierefrei, sondern in der Regel auch gut strukturiert, robust und für alle Nutzer – mit oder ohne Maus – eine bessere Erfahrung.
