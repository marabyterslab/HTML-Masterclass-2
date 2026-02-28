# Standard-Modus vs. Quirks-Modus

### Standard-Modus vs. Quirks-Modus: Ein Schalter mit Geschichte

Stell dir vor, dein Browser hätte zwei Persönlichkeiten. Die eine ist modern, regelkonform, berechenbar und hält sich strikt an die neuesten Webstandards. Die andere ist ein wenig chaotisch, altmodisch und interpretiert Regeln auf ihre ganz eigene, manchmal seltsame Weise – so wie in den Anfangstagen des Internets. Genau das ist im Grunde der Unterschied zwischen dem Standard-Modus und dem Quirks-Modus. Der `<!DOCTYPE>` am Anfang deines HTML-Dokuments ist der Lichtschalter, der entscheidet, welche dieser beiden Persönlichkeiten dein Browser für die Darstellung deiner Webseite aktiviert.

#### Eine kurze Reise in die Vergangenheit: Die Browserkriege

Um zu verstehen, warum es den Quirks-Modus überhaupt gibt, müssen wir eine kleine Zeitreise in die späten 1990er Jahre machen. Das war die Ära der ersten großen „Browserkriege“, hauptsächlich zwischen Netscape Navigator und dem Internet Explorer von Microsoft. Damals gab es noch keine fest etablierten, universell befolgten Webstandards wie heute. Jeder Browser-Hersteller kochte sein eigenes Süppchen. Sie implementierten CSS und HTML auf unterschiedliche Weisen und fügten eigene, proprietäre Features hinzu, um Entwickler an ihre Plattform zu binden.

Das Ergebnis war Chaos. Eine Webseite, die im Netscape Navigator perfekt aussah, konnte im Internet Explorer völlig zerschossen sein – und umgekehrt. Entwickler verbrachten unzählige Stunden damit, umständliche Hacks und Workarounds zu schreiben, um ihre Seiten in beiden Welten einigermaßen benutzbar zu machen. Viele Webseiten aus dieser Zeit wurden speziell für die fehlerhaften und inkonsistenten Darstellungsweisen (die „Quirks“) dieser alten Browser optimiert.

Als sich die Wogen langsam glätteten und Organisationen wie das World Wide Web Consortium (W3C) begannen, verbindliche Standards für HTML und CSS zu schaffen, standen die Browser-Hersteller vor einem Dilemma: Wie konnten sie ihre neuen, standardkonformen Rendering-Engines einführen, ohne dabei Millionen von alten Webseiten zu zerstören, die auf den alten Fehlern aufbauten?

Die Lösung war eine Weiche, ein Mechanismus, der dem Browser signalisiert, welche Interpretationsregeln er anwenden soll. Dieser Mechanismus ist der Doctype.

#### Der Quirks-Modus: Ein Relikt aus der Vergangenheit

Wenn ein Browser eine HTML-Datei ohne Doctype oder mit einem veralteten, unvollständigen Doctype aus der Zeit vor HTML4 findet, schaltet er in den sogenannten **Quirks-Modus** (auf Deutsch etwa „Eigenheiten-“ oder „Macken-Modus“).

In diesem Modus versucht der Browser, die Rendering-Fehler und das nicht standardkonforme Verhalten alter Browser wie dem Internet Explorer 5.5 zu emulieren. Er tut dies, um die Abwärtskompatibilität zu gewährleisten und sicherzustellen, dass Webseiten, die vor 20 Jahren erstellt wurden, heute nicht völlig unbrauchbar sind.

Im Quirks-Modus verhalten sich viele CSS-Eigenschaften anders als erwartet. Das berühmteste und folgenreichste Beispiel ist das **CSS Box Model**.

Stell dir eine einfache Box vor:

```html
<!DOCTYPE html>
<!-- Moment, für dieses Beispiel lassen wir den Doctype mal weg -->
<html>
<head>
  <title>Box Model Test</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <div class="box">
    Hier ist etwas Inhalt.
  </div>

</body>
</html>
```

Und das zugehörige CSS:

```css
.box {
  width: 300px;
  height: 150px;
  padding: 20px;
  border: 10px solid navy;
  background-color: lightblue;
}
```

Im Quirks-Modus interpretiert der Browser die `width`-Eigenschaft als die *Gesamtbreite* der Box, inklusive `padding` und `border`. Die 300px Breite werden also aufgeteilt in den Inhaltsbereich, den Innenabstand und den Rahmen. Der eigentliche Platz für den Inhalt wäre demnach `300px - (2 * 20px padding) - (2 * 10px border) = 240px`. Die visuelle Box auf dem Bildschirm ist exakt 300px breit.

Das mag auf den ersten Blick logisch erscheinen, widerspricht aber dem offiziellen W3C-Standard.

#### Der Standard-Modus: Die richtige Art, Dinge zu tun

Wenn du, wie es absolut korrekt ist, dein Dokument mit dem HTML5-Doctype `<!DOCTYPE html>` beginnst, aktiviert der Browser den **Standard-Modus** (engl. *Standards Mode*). Dies ist der Modus, in dem du immer arbeiten möchtest.

Im Standard-Modus hält sich der Browser so genau wie möglich an die aktuellen HTML- und CSS-Spezifikationen. Das Rendering ist vorhersehbar, konsistent über verschiedene Browser hinweg und ermöglicht die Nutzung aller modernen Web-Technologien wie Flexbox, Grid, oder fortgeschrittene JavaScript-APIs.

Nehmen wir unser Box-Beispiel von oben, diesmal aber in einem Dokument mit dem korrekten Doctype:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Box Model Test - Standard-Modus</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <div class="box">
    Hier ist etwas Inhalt.
  </div>

</body>
</html>
```

Mit dem exakt gleichen CSS wie zuvor ist das Ergebnis nun ein anderes:
Die Eigenschaft `width: 300px;` bezieht sich im Standard-Modus **ausschließlich auf den Inhaltsbereich**. `padding` und `border` werden *zusätzlich* zur Breite addiert.

Die visuelle Gesamtbreite der Box auf dem Bildschirm ist also:
`300px (width) + 2 * 20px (padding links/rechts) + 2 * 10px (border links/rechts) = 360px`.

Dieser Unterschied ist fundamental. Wenn du im Quirks-Modus landest, ohne es zu merken, wirst du dich stundenlang fragen, warum deine Layouts nicht stimmen, warum Elemente breiter sind als erwartet und warum alles um einige Pixel verschoben ist.

#### Der Vollständigkeit halber: Der "Almost Standards Mode"

Es gibt noch einen dritten, selteneren Modus, den sogenannten **Almost Standards Mode**. Er wird durch einige ältere Doctypes (wie den XHTML 1.0 Transitional Doctype) ausgelöst. Dieser Modus verhält sich fast genauso wie der vollständige Standard-Modus, behält aber eine einzige, sehr spezifische Eigenheit aus dem Quirks-Modus bei: die vertikale Größenberechnung von Bildern in Tabellenzellen. Für die moderne Webentwicklung ist dieser Modus praktisch irrelevant, da der HTML5-Doctype immer den vollen Standard-Modus auslöst.

#### Was das für dich heute bedeutet

Die Geschichte ist interessant, aber die praktische Konsequenz für deine tägliche Arbeit ist denkbar einfach und absolut unmissverständlich:

**Beginne jede einzelne HTML-Datei immer und ausnahmslos mit `<!DOCTYPE html>` in der allerersten Zeile.**

Dieser einfache String ist deine Garantie dafür, dass alle modernen Browser deine Webseite im Standard-Modus rendern. Er ist kein HTML-Tag, sondern eine Anweisung (eine sogenannte „Preamble“) an den Browser. Mit dieser Anweisung sagst du: „Lieber Browser, vergiss all die alten Macken. Bitte nutze deine beste, modernste und standardkonformste Rendering-Engine, um dieses Dokument zu verarbeiten.“

Ohne diesen Doctype fällst du in den Quirks-Modus, und das führt zu einer Welt voller Schmerz und Frustration:
*   CSS-Layouts (insbesondere mit `float`, `flex` oder `grid`) verhalten sich unvorhersehbar.
*   JavaScript-APIs, die auf exakte Elementgrößen angewiesen sind, könnten falsche Werte zurückgeben.
*   Die Darstellung deiner Seite kann sich zwischen Chrome, Firefox, Safari und Edge dramatisch unterscheiden, selbst bei einfachem CSS.
*   Du wirst Stunden mit der Fehlersuche verbringen, die du dir hättest sparen können.

#### Wie du den Modus deiner Seite überprüfen kannst

Du bist dir nicht sicher, in welchem Modus eine Seite gerade gerendert wird? Die Entwicklerwerkzeuge deines Browsers geben dir Auskunft. Öffne die Konsole (meist mit F12 oder `Cmd+Option+J`) und gib folgenden Befehl ein:

```js
document.compatMode
```

Das Ergebnis wird einer von zwei Werten sein:
*   `'CSS1Compat'`: Dies bedeutet, der Browser befindet sich im **Standard-Modus** (oder im Almost Standards Mode). Alles ist gut.
*   `'BackCompat'`: Dies steht für "Backwards Compatibility Mode" und bedeutet, der Browser ist im **Quirks-Modus**. Du solltest dringend einen `<!DOCTYPE html>` an den Anfang deines Dokuments setzen.

Der Quirks-Modus ist ein faszinierendes Stück Web-Geschichte und ein cleverer Kniff, um das alte Web am Leben zu erhalten. Aber für deine Arbeit als moderner Webentwickler ist er ein Feind. Dein Ziel ist es, immer und ausschließlich im Standard-Modus zu arbeiten. Der Schlüssel dazu ist die erste Zeile deines Codes: `<!DOCTYPE html>`.
