# Falsche Verwendung von Rollen

### Falsche Verwendung von Rollen

ARIA-Rollen sind ein mächtiges Werkzeug. Sie ermöglichen es dir, die Semantik von Elementen zu definieren oder zu überschreiben, um assistiven Technologien wie Screenreadern mitzuteilen, was ein bestimmter Teil deiner Webseite ist und wie er sich verhält. Diese Macht bringt jedoch auch eine große Verantwortung mit sich. Eine falsch zugewiesene Rolle kann mehr schaden als nutzen. Sie kann eine Benutzeroberfläche von „etwas unklar“ zu „komplett unbrauchbar“ für Menschen machen, die auf diese Technologien angewiesen sind.

In diesem Kapitel schauen wir uns die häufigsten Fehler bei der Verwendung von ARIA-Rollen an und wie du sie vermeidest. Der oberste Grundsatz, an den du dich immer erinnern solltest, ist die erste Regel von ARIA: Verwende ARIA nicht, wenn du stattdessen ein natives HTML-Element mit der passenden Semantik nutzen kannst.

#### Fehler 1: Die Semantik nativer Elemente überschreiben

Dies ist wohl der schwerwiegendste und leider auch einer der häufigsten Fehler. HTML-Elemente wie `<button>`, `<h1>` bis `<h6>`, `<nav>`, `<a>` oder `<input>` haben eine eingebaute, implizite Rolle. Ein Browser und ein Screenreader wissen genau, was ein `<button>`-Element ist und wie es sich verhalten soll. Wenn du versuchst, diese grundlegende Bedeutung mit einem `role`-Attribut zu ändern, stiftest du Chaos.

Stell dir vor, du schreibst folgenden Code:

```html
<!-- FALSCH: Überschreibt eine fundamentale Rolle -->
<h1 role="button">Jetzt klicken, um zu kaufen</h1>
```

Was passiert hier? Du nimmst das semantisch wichtigste Überschriften-Element der Seite, `<h1>`, und sagst einem Screenreader: „Hey, ignoriere, dass dies die Hauptüberschrift ist. Behandle es wie einen Button.“ Für einen sehenden Benutzer sieht es vielleicht immer noch wie eine große Überschrift aus, die vielleicht wie ein Button gestaltet ist. Für einen Screenreader-Benutzer verschwindet jedoch die Überschrift aus der Gliederung der Seite. Er kann nicht mehr über die Überschriften-Navigation zu diesem Punkt springen. Stattdessen findet er an dieser Stelle einen „Button“.

Aber die Probleme hören hier nicht auf. Ein natives `<button>`-Element bringt eine ganze Reihe von Funktionalitäten mit, die ein `<h1>` nicht hat:
*   Es ist standardmäßig per Tastatur (Tab-Taste) fokussierbar.
*   Es kann mit der Leertaste oder der Enter-Taste ausgelöst werden.
*   Es wird assistiven Technologien als interaktives Element gemeldet.

Dein `<h1 role="button">` hat nichts davon. Du hast zwar die Rolle geändert, aber nicht das Verhalten. Du müsstest nun manuell mit JavaScript die gesamte Tastaturinteraktion und den Fokus (`tabindex="0"`) hinzufügen, um die Erwartungen zu erfüllen, die du mit `role="button"` geweckt hast. Du erschaffst dir eine Menge unnötiger Arbeit und eine hohe Fehleranfälligkeit für ein Problem, das mit dem richtigen Element gar nicht existieren würde.

Hier ein weiteres Beispiel für die falsche Richtung:

```html
<!-- FALSCH: Eine Schaltfläche als Link ausgeben -->
<button role="link">Gehe zur Startseite</button>
```

Ein Button führt eine Aktion auf der aktuellen Seite aus (z. B. ein Formular absenden, ein Modal öffnen). Ein Link navigiert zu einer neuen Ressource oder einem anderen Teil der Seite. Indem du die Rolle eines Buttons zu einem Link änderst, verwirrst du den Benutzer. Er erwartet das Verhalten eines Links (z. B. Rechtsklick, um in neuem Tab zu öffnen), bekommt aber die Funktionalität eines Buttons. Die korrekte Lösung wäre hier, einfach ein `<a>`-Element zu verwenden und es mit CSS wie einen Button aussehen zu lassen.

**Merke dir:** Vertraue der nativen Semantik. Ändere niemals die Rolle eines Elements, das bereits eine starke, eindeutige Bedeutung hat. Wenn du einen Button brauchst, nutze `<button>`. Wenn du eine Überschrift brauchst, nutze `<h1>`.

#### Fehler 2: Redundante Rollen zuweisen

Ein weniger schädlicher, aber dennoch unnötiger und unsauberer Fehler ist die Zuweisung von Rollen, die das Element bereits von Natur aus besitzt.

Schau dir diese Beispiele an:

```html
<!-- UNNÖTIG: Redundante Rollenzuweisung -->
<nav role="navigation">
  ...
</nav>

<button role="button">Senden</button>

<input type="checkbox" role="checkbox" />
```

Das `<nav>`-Element hat die implizite Landmark-Rolle `navigation`. Das `<button>`-Element hat die implizite Rolle `button`. Und ein `<input type="checkbox">` hat die implizite Rolle `checkbox`. Das `role`-Attribut in diesen Fällen hinzuzufügen, ist überflüssig. Es ist, als würdest du auf ein Auto zeigen und sagen: „Das ist ein Auto mit der Rolle eines Autos.“

In den meisten modernen Browsern und Screenreadern richtet dieser Code keinen direkten Schaden an. Die Software ist oft klug genug, die Redundanz zu erkennen und zu ignorieren. Es gibt jedoch zwei gute Gründe, dies zu vermeiden:

1.  **Code-Sauberkeit und Wartbarkeit:** Redundanter Code bläht deine HTML-Struktur auf und kann bei anderen Entwicklern Verwirrung stiften. Sie könnten sich fragen, ob es einen speziellen Grund für diese explizite Zuweisung gab, und zögern, den Code zu bereinigen.
2.  **Potenzielle Konflikte:** In der Vergangenheit und in manchen älteren Browser-Screenreader-Kombinationen konnte eine explizite Rollenzuweisung die implizite Rolle tatsächlich auf eine Weise überschreiben, die zu subtilen Fehlern führte. Es ist eine gute defensive Programmierpraxis, unnötige Angaben zu vermeiden.

Die Regel ist einfach: Wenn das HTML-Element bereits die Semantik liefert, die du brauchst, füge kein `role`-Attribut hinzu.

#### Fehler 3: Eine Rolle zuweisen, ohne das erwartete Verhalten zu implementieren

Eine ARIA-Rolle ist ein Versprechen. Wenn du einem generischen `<div>` die Rolle `button` gibst, versprichst du dem Benutzer, dass sich dieses Element wie ein Button verhalten wird. Dieses Versprechen musst du mit JavaScript einlösen.

Betrachte dieses sehr verbreitete, aber unzugängliche Muster:

```html
<!-- FALSCH und UNZUGÄNGLICH -->
<div role="button" class="fancy-button">
  Klick mich
</div>

<script>
  document.querySelector('.fancy-button').addEventListener('click', () => {
    console.log('Button wurde geklickt!');
  });
</script>
```

Für einen Mausbenutzer funktioniert das vielleicht. Aber was ist mit jemandem, der nur die Tastatur benutzt?
*   Das `<div>` ist nicht fokussierbar. Ein Benutzer kann es mit der Tab-Taste nicht erreichen.
*   Selbst wenn du es mit `tabindex="0"` fokussierbar machst, reagiert es nicht auf die Leertaste oder die Enter-Taste, wie es ein echter Button tun würde.

Ein Screenreader wird zwar „Klick mich, Button“ ansagen, aber der Benutzer kann diesen Button nicht bedienen. Du hast ein Versprechen gegeben (`role="button"`) und es sofort gebrochen. Das ist frustrierender, als wenn es gar nicht als Button deklariert worden wäre.

Um dieses Versprechen zu halten, müsstest du den Code erheblich erweitern:

```html
<!-- Korrekt, aber unnötig komplex -->
<div role="button" class="fancy-button" tabindex="0">
  Klick mich
</div>

<script>
  const button = document.querySelector('.fancy-button');

  function handleClick() {
    console.log('Button wurde geklickt!');
  }

  button.addEventListener('click', handleClick);

  button.addEventListener('keydown', (event) => {
    // Führe die Aktion bei Enter oder Leertaste aus
    if (event.key === 'Enter' || event.key === ' ') {
      // Verhindere Standardaktionen wie das Scrollen der Seite bei Leertaste
      event.preventDefault();
      handleClick();
    }
  });
</script>
```

Dieser Code funktioniert. Aber vergleiche den Aufwand mit der nativen HTML-Lösung:

```html
<!-- Einfach, korrekt und zugänglich -->
<button class="fancy-button">
  Klick mich
</button>
```

Das `<button>`-Element erledigt all das für dich, ohne eine einzige Zeile JavaScript. Die Lektion hier ist klar: Weise eine Rolle nur dann zu, wenn du auch bereit und in der Lage bist, alle Verhaltensweisen zu implementieren, die mit dieser Rolle verbunden sind. Und selbst dann frage dich: Gibt es nicht doch ein natives Element, das diese Arbeit für mich übernimmt?

#### Fehler 4: Abstrakte Rollen verwenden

Die ARIA-Spezifikation definiert einige Rollen als „abstrakt“. Diese Rollen sind nicht für den direkten Gebrauch in deinem HTML-Code gedacht. Sie dienen als konzeptionelle Grundlage oder als Oberkategorien für andere, konkretere Rollen. Wenn du sie trotzdem verwendest, werden sie von assistiven Technologien in der Regel ignoriert oder führen zu unvorhersehbarem Verhalten.

Einige Beispiele für abstrakte Rollen sind:
*   `widget`
*   `structure`
*   `landmark`
*   `window`
*   `input`

Du würdest zum Beispiel niemals so etwas schreiben:

```html
<!-- FALSCH: Verwendung einer abstrakten Rolle -->
<div role="widget">Ein interaktives Element</div>
```

Die Rolle `widget` ist eine Überkategorie für alle interaktiven Elemente wie `button`, `slider`, `checkbox` und so weiter. Einem Screenreader `widget` mitzuteilen, ist so, als würdest du jemandem sagen: „Hier ist ein Fahrzeug.“ Das ist nicht hilfreich. Ist es ein Fahrrad, ein Auto oder ein Flugzeug? Genauso muss ein Screenreader wissen, ob es ein `button`, ein `slider` oder etwas anderes Spezifisches ist. Verwende also immer die konkreteste und passendste Rolle aus der Spezifikation.

Die falsche Verwendung von Rollen ist eine der Hauptursachen für Zugänglichkeitsprobleme, die durch ARIA erst geschaffen werden. Indem du diese typischen Fehler vermeidest, stellst du sicher, dass deine ARIA-Implementierungen die Benutzererfahrung verbessern, anstatt sie zu verschlechtern. Denke immer daran: HTML zuerst. ARIA nur, wenn es absolut notwendig ist.
