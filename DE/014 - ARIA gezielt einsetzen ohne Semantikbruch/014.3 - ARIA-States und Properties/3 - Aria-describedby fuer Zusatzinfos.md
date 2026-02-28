# aria-describedby für Zusatzinfos

### Mehr als nur ein Label: Zusatzinformationen mit `aria-describedby`

Stell dir ein Formular vor. Es gibt ein Feld für ein Passwort. Direkt darunter steht in kleinerer Schrift ein Hinweis: "Das Passwort muss mindestens 8 Zeichen, einen Großbuchstaben und eine Zahl enthalten." Für sehende Nutzerinnen und Nutzer ist dieser Zusammenhang sofort klar. Das Gehirn verknüpft visuell den Text mit dem darüberliegenden Eingabefeld.

Aber was ist mit Nutzern, die einen Screenreader verwenden? Ein Screenreader liest die Elemente einer Webseite vor. Er würde das Label "Passwort" und das Eingabefeld ansagen. Dann, irgendwann später, würde er auf den separaten Text mit den Passwortanforderungen stoßen. Der direkte, unmittelbare Kontext geht verloren. Der Nutzer muss mental die Verbindung herstellen, was umständlich und fehleranfällig ist.

Genau hier kommt das ARIA-Attribut `aria-describedby` ins Spiel. Es ist wie ein unsichtbarer Faden, der ein Element mit einer oder mehreren Beschreibungen an anderer Stelle auf der Seite verknüpft. Es sagt assistiven Technologien: "Hey, die ausführliche Erklärung für dieses Element findest du dort drüben."

#### Die grundlegende Funktionsweise

Das Prinzip hinter `aria-describedby` ist elegant und einfach. Es basiert auf der Verknüpfung mittels `id`.

1.  **Das beschreibende Element braucht eine `id`:** Das Element, das den zusätzlichen Text enthält (z. B. ein `<p>` oder `<span>`), muss eine eindeutige `id` erhalten.
2.  **Das beschriebene Element bekommt `aria-describedby`:** Das Element, das die Beschreibung benötigt (z. B. ein `<input>`, `<button>` oder `<a>`), erhält das Attribut `aria-describedby`. Der Wert dieses Attributs ist die `id` des beschreibenden Elements.

Schauen wir uns das Passwort-Beispiel in der Praxis an.

Ohne `aria-describedby` ist der Zusammenhang nur visuell:

```html
<label for="password">Passwort</label>
<input type="password" id="password" name="user_password">
<p>Das Passwort muss mindestens 8 Zeichen, einen Großbuchstaben und eine Zahl enthalten.</p>
```

Ein Screenreader würde hier etwa Folgendes ausgeben, wenn der Fokus auf dem Eingabefeld liegt: "Passwort, Eingabefeld, geschützt". Der Hilfetext wird erst vorgelesen, wenn der Nutzer weiter durch die Seite navigiert.

Jetzt fügen wir die magische Verbindung hinzu:

```html
<label for="password">Passwort</label>
<input type="password" id="password" name="user_password" aria-describedby="password-hint">
<p id="password-hint">Das Passwort muss mindestens 8 Zeichen, einen Großbuchstaben und eine Zahl enthalten.</p>
```

Was passiert nun? Wenn ein Screenreader-Nutzer das Passwortfeld fokussiert, hört er etwas wie: "Passwort, Eingabefeld, geschützt. Das Passwort muss mindestens 8 Zeichen, einen Großbuchstaben und eine Zahl enthalten." Die Zusatzinformation wird direkt nach dem Label und der Rolle des Elements vorgelesen. Der Kontext ist sofort klar, die Usability für den Nutzer steigt enorm.

#### Der feine Unterschied: `aria-describedby` vs. `aria-labelledby`

Es ist wichtig, `aria-describedby` nicht mit seinem nahen Verwandten `aria-labelledby` zu verwechseln. Obwohl sie ähnlich funktionieren (beide verweisen auf eine `id`), ist ihr Zweck grundverschieden.

*   **`aria-labelledby` ersetzt den zugänglichen Namen.** Wenn du dieses Attribut verwendest, ignorieren assistive Technologien den Inhalt eines `<label>`-Elements oder den Textinhalt eines Buttons. Der Text aus dem Element, auf das die `id` verweist, wird zum *einzigen* Namen des Elements. Es ist das "Was bin ich?".
*   **`aria-describedby` ergänzt den zugänglichen Namen.** Es fügt eine zusätzliche Beschreibung hinzu, ohne den eigentlichen Namen zu verändern. Es beantwortet die Frage "Was muss ich sonst noch über dich wissen?".

Stell es dir wie eine Person vor:
*   Der Name (das Label oder `aria-labelledby`) ist "Max Mustermann".
*   Die Beschreibung (`aria-describedby`) ist "Projektleiter für das Team Alpha und passionierter Kaffeetrinker."

Du würdest niemals die Beschreibung anstelle des Namens verwenden, um jemanden vorzustellen. Genauso solltest du niemals `aria-describedby` für die primäre Beschriftung eines Elements nutzen.

#### Mehrere Beschreibungen verknüpfen

Eine der Stärken von `aria-describedby` ist die Fähigkeit, ein Element mit *mehreren* Beschreibungen zu verbinden. Das ist besonders nützlich bei Formularen, die dynamisch auf Nutzereingaben reagieren, zum Beispiel mit Fehlermeldungen.

Um mehrere Beschreibungen zu verknüpfen, listest du einfach die `id`s der Beschreibungselemente im Attribut auf, getrennt durch ein Leerzeichen. Die Reihenfolge, in der du die `id`s angibst, bestimmt die Reihenfolge, in der sie vorgelesen werden.

Sehen wir uns ein Beispiel an, bei dem ein Eingabefeld sowohl einen permanenten Hinweis als auch eine dynamisch erscheinende Fehlermeldung hat.

```html
<label for="username">Benutzername</label>
<input type="text" id="username" name="user_name" aria-describedby="username-hint username-error">

<!-- Der permanente Hinweis -->
<p id="username-hint">Darf nur Buchstaben und Zahlen enthalten.</p>

<!-- Die Fehlermeldung, die z.B. per JavaScript eingeblendet wird -->
<div id="username-error" role="alert" style="color: red;">
  Der Benutzername ist bereits vergeben.
</div>
```

Wenn der Nutzer dieses Feld fokussiert, während die Fehlermeldung sichtbar ist, würde ein Screenreader Folgendes ausgeben: "Benutzername, Eingabefeld. Darf nur Buchstaben und Zahlen enthalten. Der Benutzername ist bereits vergeben."

Die Kombination aus dem statischen Hinweis und der dynamischen Fehlermeldung liefert dem Nutzer alle notwendigen Informationen genau dann, wenn er sie braucht, ohne dass er die Seite nach Hinweisen absuchen muss.

#### Sinnvolle Anwendungsfälle (und wann du es lassen solltest)

`aria-describedby` ist ein mächtiges Werkzeug, aber wie bei jedem Werkzeug kommt es auf den richtigen Einsatz an.

**Ideal für:**

*   **Formularhinweise:** Wie im Passwort-Beispiel gezeigt, für Formatierungsregeln, Längenbeschränkungen oder andere Eingabeanforderungen.
*   **Fehlermeldungen:** Um eine klare Verbindung zwischen einem fehlerhaften Feld und der zugehörigen Fehlermeldung herzustellen.
*   **Komplexe Bedienelemente:** Ein Button mit der Beschriftung "Einstellungen speichern" könnte eine Beschreibung haben wie: "Diese Aktion lädt die Seite neu." Dies informiert den Nutzer über eine Konsequenz, die nicht sofort aus dem Label ersichtlich ist.
*   **Tooltips und Infobuttons:** Ein kleines Info-Icon neben einem Feld kann per `aria-describedby` mit seinem ausführlichen Hilfetext verknüpft werden, der in einem Tooltip erscheint.

**Wann du vorsichtig sein solltest:**

*   **Nicht als Ersatz für `<label>`:** Das haben wir bereits geklärt, aber es ist der häufigste Fehler. Jedes interaktive Element braucht einen prägnanten, zugänglichen Namen. Die Beschreibung ist ein Zusatz, kein Ersatz.
*   **Vermeide Romane:** Die Beschreibung sollte präzise und kurz sein. Niemand möchte einen ganzen Absatz vorgelesen bekommen, nur um zu verstehen, was in ein Textfeld gehört. Fasse dich kurz und liefere nur die wirklich notwendigen Informationen.
*   **Nicht für offensichtliche Informationen:** Ein Link mit dem Text "Klicke hier, um unsere Datenschutzrichtlinie zu lesen" braucht keine `aria-describedby` mit dem Inhalt "Öffnet die Seite mit der Datenschutzrichtlinie". Der Link-Text selbst ist bereits beschreibend genug.

#### Sichtbarkeit der Beschreibung

Ein wichtiger Aspekt ist, dass das Element, welches die Beschreibung enthält, ein ganz normales HTML-Element ist. Es unterliegt den normalen Regeln von HTML und CSS. Das bedeutet, du hast die volle Kontrolle darüber, ob und wie diese Information für sehende Nutzer sichtbar ist.

Oft ist der beschreibende Text, wie der Hinweis unter einem Formularfeld, für alle Nutzer sichtbar und nützlich. In manchen Fällen möchtest du die zusätzliche Information aber vielleicht nur für Screenreader-Nutzer bereitstellen, um die visuelle Oberfläche nicht zu überladen.

Dafür kannst du den Text mit CSS visuell verstecken, ihn aber für assistive Technologien zugänglich halten. Eine gängige Methode ist eine sogenannte `visually-hidden` oder `sr-only` (screenreader-only) Klasse.

```css
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border-width: 0;
}
```

Mit dieser CSS-Klasse kannst du eine Beschreibung bereitstellen, die nahtlos in das Screenreader-Erlebnis integriert ist, ohne das visuelle Design zu beeinflussen.

```html
<button aria-describedby="close-warning">X</button>
<span id="close-warning" class="visually-hidden">Schließt das Dialogfenster endgültig.</span>
```

Ein sehender Nutzer sieht nur einen Button mit einem "X". Ein Screenreader-Nutzer hört: "X, Button. Schließt das Dialogfenster endgültig." Dieser kleine Zusatz an Kontext kann den Unterschied zwischen einer klaren und einer verwirrenden Benutzerführung ausmachen.

`aria-describedby` ist somit ein Paradebeispiel für die Philosophie von ARIA: Es überbrückt Lücken in der Semantik von HTML, um ein reichhaltigeres und verständlicheres Web für alle Menschen zu schaffen.
