# Styling von validen/invaliden Feldern

### Visuelles Feedback: Styling von validen und invaliden Feldern

Wenn du Formulare auf Webseiten ausfüllst, hast du sicher schon bemerkt, dass manche Felder ihre Farbe ändern, sobald du etwas eingibst. Ein E-Mail-Feld leuchtet vielleicht rot auf, wenn du das "@"-Zeichen vergisst, und wird grün, sobald die Eingabe korrekt ist. Dieses sofortige visuelle Feedback ist kein Zufall, sondern ein entscheidender Teil einer guten User Experience (UX). Es signalisiert dem Nutzer in Echtzeit, ob seine Eingabe den erwarteten Kriterien entspricht, und erspart ihm die Frustration, das gesamte Formular abzusenden, nur um dann eine Fehlermeldung zu erhalten.

Die gute Nachricht ist: Du brauchst dafür nicht zwangsläufig komplexes JavaScript. Dank moderner CSS-Pseudo-Klassen kannst du dieses Verhalten direkt und elegant mit reinem CSS umsetzen.

#### Die Grundlagen: `:valid` und `:invalid`

Das Herzstück des Stylings basierend auf dem Validierungsstatus sind zwei einfache, aber mächtige CSS-Pseudo-Klassen: `:valid` und `:invalid`.

*   **:valid**: Diese Pseudo-Klasse greift, wenn der Inhalt eines Formularelements (wie `<input>`, `<select>` oder `<textarea>`) den vordefinierten Validierungsregeln entspricht.
*   **:invalid**: Diese Pseudo-Klasse greift, wenn der Inhalt die Validierungsregeln verletzt.

Welche Regeln sind das? Diese definierst du direkt in deinem HTML-Code mithilfe von Attributen. Schauen wir uns ein einfaches Beispiel an:

```html
<form>
  <label for="email">E-Mail-Adresse:</label>
  <input type="email" id="email" name="email" required>

  <label for="username">Benutzername (mind. 5 Zeichen):</label>
  <input type="text" id="username" name="username" required minlength="5">
</form>
```

In diesem HTML-Code haben wir zwei Felder mit Validierungsregeln:

1.  Das E-Mail-Feld (`type="email"`) muss eine gültige E-Mail-Adressen-Syntax enthalten und ist dank `required` ein Pflichtfeld.
2.  Das Benutzernamen-Feld (`type="text"`) ist ebenfalls ein Pflichtfeld (`required`) und muss eine Mindestlänge von 5 Zeichen haben (`minlength="5"`).

Jetzt können wir mit `:valid` und `:invalid` darauf reagieren:

```css
/* Grundlegendes Styling für alle Input-Felder */
input {
  border: 2px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  transition: border-color 0.3s ease;
}

/* Styling für invalide Felder */
input:invalid {
  border-color: #e74c3c; /* Ein deutliches Rot */
}

/* Styling für valide Felder */
input:valid {
  border-color: #2ecc71; /* Ein freundliches Grün */
}
```

Mit diesem CSS wird ein Feld rot umrandet, sobald seine Eingabe ungültig ist (z. B. eine leeres Pflichtfeld oder "test" im E-Mail-Feld), und grün, wenn sie gültig ist (z. B. "user@example.com" im E-Mail-Feld).

#### Das Problem des vorschnellen Feedbacks

Wenn du das obige Beispiel ausprobierst, wirst du ein Problem feststellen. Sobald die Seite lädt, sind beide Felder rot umrandet. Warum? Weil beide das `required`-Attribut haben und anfangs leer sind, was sie technisch gesehen "invalid" macht.

Dieses Verhalten ist aus Sicht der User Experience problematisch. Du konfrontierst den Nutzer mit einer Fehlermeldung, bevor er überhaupt die Chance hatte, etwas einzugeben. Das wirkt anklagend und kann Verwirrung stiften. Ein Nutzer sollte erst dann Feedback zu seiner Eingabe erhalten, wenn er mit dem Feld interagiert hat.

#### Eine elegantere Lösung: Feedback zum richtigen Zeitpunkt

Glücklicherweise gibt es eine clevere CSS-Lösung für dieses Problem, die ohne JavaScript auskommt. Wir können die `:placeholder-shown`-Pseudo-Klasse zu unserem Vorteil nutzen. Diese Klasse greift, solange der Platzhalter eines Input-Feldes angezeigt wird. Sobald der Nutzer auch nur ein einziges Zeichen tippt, verschwindet der Platzhalter und die Pseudo-Klasse greift nicht mehr.

Wir können unsere Logik also anpassen: Ein Feld soll nur dann als invalid markiert werden, wenn es **invalid ist UND der Platzhalter nicht mehr angezeigt wird**.

Dafür fügen wir unseren HTML-Feldern zunächst leere `placeholder` hinzu. Das ist notwendig, damit `:placeholder-shown` überhaupt funktionieren kann.

```html
<form>
  <label for="email">E-Mail-Adresse:</label>
  <input type="email" id="email" name="email" required placeholder=" ">

  <label for="username">Benutzername (mind. 5 Zeichen):</label>
  <input type="text" id="username" name="username" required minlength="5" placeholder=" ">
</form>
```

Der `placeholder=" "` mit einem Leerzeichen ist ein kleiner Trick. Er sorgt dafür, dass das Feld einen Platzhalter hat, dieser aber visuell nicht sichtbar ist.

Nun passen wir unseren CSS-Selektor an:

```css
/* Grundlegendes Styling bleibt gleich */
input {
  border: 2px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  transition: border-color 0.3s ease;
}

/* Fokus-Styling für bessere UX */
input:focus {
  outline: none;
  border-color: #3498db; /* Blau bei Fokus */
}

/* NEUER, verbesserter Selektor für invalide Felder */
input:not(:placeholder-shown):invalid {
  border-color: #e74c3c; /* Rot, aber erst nach der Eingabe */
}

/* Optional: Positives Feedback, wenn es nach der Eingabe valide wird */
input:not(:placeholder-shown):valid {
  border-color: #2ecc71; /* Grün, aber erst nach der Eingabe */
}
```

Schauen wir uns den Schlüsselselektor `input:not(:placeholder-shown):invalid` genauer an:

*   `input`: Wählt alle `<input>`-Elemente aus.
*   `:invalid`: Filtert diese Auswahl und behält nur die, die aktuell ungültig sind.
*   `:not(:placeholder-shown)`: Filtert diese Auswahl *nochmals* und behält nur die, bei denen der Platzhalter **nicht** mehr sichtbar ist (also nachdem der Nutzer mit der Eingabe begonnen hat).

Mit dieser Methode erscheinen die roten und grünen Rahmen erst, nachdem der Nutzer mit dem Feld interagiert hat. Das ist eine deutlich angenehmere und hilfreichere Erfahrung.

#### Mehr als nur Rahmen: Visuelles Feedback mit Icons

Farbe allein sollte niemals das einzige Mittel sein, um Informationen zu vermitteln. Menschen mit Farbsehschwächen könnten den Unterschied zwischen dem roten und grünen Rahmen nicht erkennen. Eine gute Praxis ist es, Feedback durch mehrere Kanäle zu geben, zum Beispiel durch die Kombination von Farbe und einem Symbol (Icon).

Wir können dies erreichen, indem wir ein Checkmark- und ein Kreuz-Icon als Hintergrundbild in unsere Input-Felder einfügen. SVG-Icons eignen sich hierfür hervorragend, da sie skalierbar sind und direkt als Data-URI in das CSS eingebettet werden können.

```css
/* --- Vollständiges Beispiel mit Icons --- */

input {
  border: 2px solid #ccc;
  padding: 8px;
  padding-right: 30px; /* Platz für das Icon schaffen */
  border-radius: 4px;
  transition: all 0.3s ease;
  background-repeat: no-repeat;
  background-position: right 8px center;
  background-size: 16px 16px;
}

input:focus {
  outline: none;
  border-color: #3498db;
}

/* Styling für invalide Felder mit Kreuz-Icon */
input:not(:placeholder-shown):invalid {
  border-color: #e74c3c;
  /* Rotes Kreuz als SVG Data-URI */
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 12 12' width='12' height='12' fill='none' stroke='%23e74c3c'%3e%3ccircle cx='6' cy='6' r='4.5'/%3e%3cpath stroke-linejoin='round' d='M5.8 3.6h.4L6 6.5z'/%3e%3ccircle cx='6' cy='8.2' r='.6' fill='%23e74c3c' stroke='none'/%3e%3c/svg%3e");
}

/* Styling für valide Felder mit Haken-Icon */
input:not(:placeholder-shown):valid {
  border-color: #2ecc71;
  /* Grüner Haken als SVG Data-URI */
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8 8'%3e%3cpath fill='%232ecc71' d='M2.3 6.73L.6 4.53c-.4-1.04.46-1.4 1.1-.8l1.1 1.4 3.4-3.8c.6-.63 1.6-.27 1.2.7l-4 4.6c-.43.5-.8.4-1.1.1z'/%3e%3c/svg%3e");
}
```

In diesem Code-Beispiel haben wir einige wichtige Änderungen vorgenommen:

1.  **`padding-right`**: Wir haben dem Input-Feld einen rechten Innenabstand hinzugefügt, damit der Text nicht unter dem Icon liegt.
2.  **`background-*` Eigenschaften**: Wir definieren, dass das Hintergrundbild (unser Icon) sich nicht wiederholen, an einer bestimmten Position (rechts, zentriert) und in einer bestimmten Größe angezeigt werden soll.
3.  **SVG Data-URIs**: Anstatt externe Bilddateien zu laden, betten wir die SVGs direkt in unser CSS ein. Das ist performant und hält den Code an einer Stelle. Die seltsam aussehenden Zeichen wie `%3c` sind URL-kodierte Versionen von Zeichen wie `<` oder `#`, was für die korrekte Interpretation durch den Browser notwendig ist.

Dieses visuelle Feedback ist nun robust, barrierearm und wird erst dann angezeigt, wenn es für den Nutzer relevant ist. Es verwandelt ein einfaches Formular in eine interaktive und hilfreiche Komponente deiner Webseite. Indem du die eingebauten Fähigkeiten von HTML und CSS nutzt, schaffst du eine bessere Nutzererfahrung, ohne die Komplexität deines Codes unnötig zu erhöhen.
