# Die erste Regel von ARIA

# Die erste Regel von ARIA

Die erste Regel von ARIA lautet: Benutze kein ARIA.

Das klingt paradox, nicht wahr? Wir sind hier in einem Kapitel über ARIA, und die erste und wichtigste Anweisung ist, es zu meiden. Doch in diesem scheinbaren Widerspruch liegt der Schlüssel zum meisterhaften Umgang mit Web-Barrierefreiheit. Die vollständige Regel, die oft von Accessibility-Experten zitiert wird, ist etwas länger und präziser:

**Wenn du ein natives HTML-Element oder -Attribut mit der Semantik und dem Verhalten, das du benötigst, verwenden kannst, dann verwende es.**

Bevor du also auch nur daran denkst, ein `role`-Attribut zu einem `<div>` hinzuzufügen, atme tief durch und frage dich: Gibt es dafür nicht schon ein HTML-Tag? In den allermeisten Fällen lautet die Antwort: Ja.

### Warum natives HTML immer Vorrang hat

Diese erste Regel ist keine schrullige Empfehlung, sondern das Fundament für robusten, wartbaren und wirklich barrierefreien Code. Es gibt mehrere handfeste Gründe, warum ein einfaches `<button>`-Element einem `div`, das mit ARIA zu einem Button umfunktioniert wurde, immer überlegen sein wird.

#### 1. Eingebautes Verhalten und Tastaturbedienung

Browser und assistive Technologien (wie Screenreader) wissen seit Jahrzehnten, was ein `<button>` ist. Sie wissen, dass er klickbar ist, dass er mit der Eingabe- und der Leertaste ausgelöst werden kann und dass er in der Tab-Reihenfolge der Seite erscheinen sollte. All diese Funktionalität bekommst du geschenkt, ohne eine einzige Zeile JavaScript schreiben zu müssen.

Stell dir vor, du entscheidest dich stattdessen für einen `<span>`, den du mit CSS wie einen Button aussehen lässt. Dein Weg ist nun deutlich steiniger:

*   **Fehlende Semantik:** Ein Screenreader verkündet nur "Text", nicht "Button". Der Nutzer hat keine Ahnung, dass er hier eine Aktion auslösen kann.
*   **Fehlende Fokussierbarkeit:** Ein `<span>` kann standardmäßig nicht mit der Tab-Taste erreicht werden. Nutzer, die auf eine Tastaturnavigation angewiesen sind, können dein Element niemals erreichen.
*   **Fehlendes Auslöseverhalten:** Ein `<span>` reagiert nicht auf die Eingabe- oder Leertaste.

Um diese Mängel zu beheben, müsstest du eine Kette von ARIA-Attributen und JavaScript hinzufügen:

```html
<!-- Falsch: Kompliziert und fehleranfällig -->
<span role="button" tabindex="0" onclick="meineAktion()" onkeydown="handleKeyDown(event)">
  Aktion ausführen
</span>

<script>
  function handleKeyDown(event) {
    // Prüfen, ob die Eingabe- oder Leertaste gedrückt wurde
    if (event.key === 'Enter' || event.key === ' ') {
      meineAktion();
    }
  }
</script>
```

All diese Komplexität – das `role`-Attribut, um die Semantik zu korrigieren, `tabindex="0"`, um es fokussierbar zu machen, und ein JavaScript-Handler für die Tastatur – dient nur dazu, das nachzubauen, was ein einziges HTML-Element von Haus aus mitbringt:

```html
<!-- Richtig: Einfach, robust und semantisch korrekt -->
<button onclick="meineAktion()">Aktion ausführen</button>
```

Der native Button ist kürzer, verständlicher und unendlich robuster. Du musst dich nicht um Tastatur-Events kümmern, und jede assistive Technologie auf diesem Planeten versteht sofort, was zu tun ist.

#### 2. Robustheit und Zukunftssicherheit

HTML ist der Fels in der Brandung des Webs. Die Semantik von Elementen wie `<nav>`, `<ul>`, `<input type="checkbox">` oder `<details>` ist tief in den Browsern verankert. Sie funktioniert einfach. Immer.

Wenn du anfängst, diese Grundbausteine mit ARIA nachzubauen, erschaffst du fragile Konstrukte. Ein kleiner Fehler in deinem JavaScript, ein vergessenes ARIA-Attribut (`aria-checked` bei einer selbstgebauten Checkbox) oder ein Browser-Update, das dein Skript unerwartet beeinflusst, kann die gesamte Funktionalität für bestimmte Nutzergruppen zerstören. Natives HTML hingegen wird von den Browserherstellern gepflegt und ist so konzipiert, dass es auch unter widrigen Umständen (z. B. bei deaktiviertem JavaScript) eine grundlegende Funktion bietet.

#### 3. Weniger Code, bessere Wartbarkeit

Wie das Button-Beispiel zeigt, führt der "ARIA-zuerst"-Ansatz fast immer zu mehr Code. Mehr Code bedeutet mehr potenzielle Fehlerquellen und einen höheren Aufwand bei der Wartung. Dein Kollege, der den Code in sechs Monaten ansieht, wird sich bei einem `<button>` sofort auskennen. Bei einem `<span>` mit drei ARIA-Attributen und einem Verweis auf ein JavaScript-Snippet muss er erst einmal analysieren, was hier überhaupt passieren soll.

### Häufige Fehler: Wenn ARIA unnötig eingesetzt wird

Schauen wir uns ein paar klassische Beispiele an, bei denen Entwickler oft zu ARIA greifen, obwohl es eine perfekte native HTML-Lösung gibt.

#### Die selbstgebaute Checkbox

Oftmals wünschen sich Designer eine Checkbox, die nicht wie die Standard-Checkbox des Betriebssystems aussieht. Ein verbreiteter Fehler ist es, sie mit einem `<div>` nachzubauen.

```html
<!-- Falsch: Viel zu kompliziert -->
<div role="checkbox" aria-checked="false" tabindex="0">
  Ich stimme den Bedingungen zu
</div>
```

Hier fehlt nicht nur die Semantik, sondern auch die Verknüpfung zwischen dem visuellen Element und seinem Label. Der Screenreader liest vielleicht "Checkbox, nicht aktiviert", aber der Text "Ich stimme den Bedingungen zu" wird nicht zwingend als zugehörige Beschriftung erkannt.

Die korrekte, barrierefreie und dennoch voll stylbare Methode ist, die native Checkbox zu verwenden und sie visuell zu verstecken, während das `<label>` als klickbarer und sichtbarer Bereich dient.

```html
<!-- Richtig: Semantisch, barrierefrei und mit CSS anpassbar -->
<style>
  .visually-hidden {
    position: absolute;
    width: 1px;
    height: 1px;
    margin: -1px;
    padding: 0;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    border: 0;
  }
  
  .custom-checkbox-label {
    /* Dein Styling für das Label */
  }
  
  .custom-checkbox-label::before {
    /* Dein Styling für die Fake-Checkbox */
    content: '';
    display: inline-block;
    width: 1em;
    height: 1em;
    border: 1px solid grey;
    margin-right: 0.5em;
  }
  
  /* Styling, wenn die echte Checkbox aktiviert ist */
  .visually-hidden:checked + .custom-checkbox-label::before {
    background-color: dodgerblue;
    /* Hier könnte auch ein Haken-Icon als Hintergrundbild rein */
  }
</style>

<input type="checkbox" id="terms" class="visually-hidden">
<label for="terms" class="custom-checkbox-label">
  Ich stimme den Bedingungen zu
</label>
```

Mit dieser Methode behältst du die gesamte eingebaute Funktionalität der Checkbox – inklusive Klickverhalten des Labels, Statusänderung und Tastaturbedienung –, hast aber die volle gestalterische Freiheit über CSS.

#### Die redundante Navigation

Manchmal sieht man Code wie diesen:

```html
<!-- Falsch: Unnötig und redundant -->
<div role="navigation">
  <ul>
    ...
  </ul>
</div>
```

Das Attribut `role="navigation"` teilt assistiven Technologien mit, dass es sich hierbei um einen Navigationsbereich handelt, einen sogenannten "Landmark". Das ist an sich gut, aber HTML5 hat uns dafür bereits ein dediziertes Element gegeben: `<nav>`.

```html
<!-- Richtig: Klar und semantisch -->
<nav>
  <ul>
    ...
  </ul>
</nav>
```

Das `<nav>`-Element hat die Navigations-Rolle bereits implizit. Das `role`-Attribut ist hier also überflüssig und bläht den Code nur auf. Die erste Regel von ARIA schlägt wieder zu: Wenn es ein natives Element gibt, nutze es.

### Wann ist ARIA dann die richtige Wahl?

Nachdem wir nun eindringlich davor gewarnt haben, ARIA zu verwenden, ist es an der Zeit für die Auflösung: ARIA ist ein unglaublich mächtiges Werkzeug, aber es ist für die Fälle gedacht, in denen HTML an seine Grenzen stößt. ARIA ist kein Ersatz für HTML, sondern eine Erweiterung.

Setze ARIA gezielt und bedacht ein, wenn du eine der folgenden Aufgaben lösen musst:

1.  **Komplexe, dynamische Widgets:** Du baust eine Komponente, für die es kein natives HTML-Äquivalent gibt. Klassische Beispiele sind ein Tab-Panel, eine Baumansicht (Tree View), ein Schieberegler (Slider) oder eine komplexe Datentabelle mit Sortier- und Filterfunktionen. Hier brauchst du ARIA-Rollen (`role="tablist"`, `role="tab"`, `role="tabpanel"`) und -Zustände (`aria-selected`, `aria-expanded`), um die Struktur und den aktuellen Zustand für assistive Technologien verständlich zu machen.

2.  **Live-Regionen und Benachrichtigungen:** Deine Webseite lädt Inhalte dynamisch nach, ohne die Seite neu zu laden. Ein neuer Chat-Beitrag erscheint, eine Fehlermeldung wird unter einem Formularfeld angezeigt oder der Status einer Suche aktualisiert sich. Ein sehender Nutzer bemerkt diese Änderungen sofort. Ein Screenreader-Nutzer bekommt davon nichts mit. Mit `aria-live`-Attributen kannst du Bereiche deiner Seite definieren, deren Änderungen dem Nutzer vorgelesen werden sollen. Das ist eine der wichtigsten und häufigsten Anwendungen von ARIA.

3.  **Semantische Lücken füllen:** Manchmal bietet ein natives Element 90 % dessen, was du brauchst, aber eine kleine Information fehlt. ARIA kann diese Lücke schließen.
    *   `aria-current="page"` in einem Navigationslink, um anzuzeigen, welcher Link zur aktuell angezeigten Seite gehört.
    *   `aria-describedby` an einem Eingabefeld, um es mit einem zusätzlichen Hinweistext zu verknüpfen, der mehr Kontext als das `<label>` liefert.
    *   `aria-invalid="true"` an einem Formularfeld, um nach der Validierung programmatisch zu signalisieren, dass die Eingabe fehlerhaft ist.

In diesen Fällen ersetzt du kein HTML, du *erweiterst* es. Du nimmst ein solides Fundament aus semantischem HTML und fügst gezielt die Informationen hinzu, die nur ARIA liefern kann.

Denk an ARIA wie an ein Set hochspezialisierter Werkzeuge eines Chirurgen. Du würdest niemals ein Skalpell benutzen, um einen Nagel in die Wand zu schlagen, wenn du einen Hammer hast. Genauso solltest du nicht zu ARIA greifen, um einen Button zu bauen, wenn es das `<button>`-Element gibt. Deine Aufgabe als professioneller Webentwickler ist es, das richtige Werkzeug für die jeweilige Aufgabe zu kennen und zu wählen. Und im Web ist das richtige Werkzeug fast immer das einfachste und robusteste: natives, semantisches HTML. Die erste Regel von ARIA ist also nicht nur eine technische Richtlinie, sondern eine Philosophie, die dich zu besserem, saubererem und zugänglicherem Code führt.
