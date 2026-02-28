# Redundante ARIA-Attribute

### Die Kunst des Weglassens: Redundante ARIA-Attribute

Wenn du dich mit ARIA (Accessible Rich Internet Applications) beschäftigst, stolperst du schnell über eine der wichtigsten Grundregeln, die oft zitiert wird: „Die erste Regel von ARIA ist, kein ARIA zu verwenden.“ Das klingt zunächst paradox, bringt aber den Kern der Sache auf den Punkt. ARIA ist ein mächtiges Werkzeug, um die Barrierefreiheit von Webanwendungen zu verbessern, aber es ist als Ergänzung zu HTML gedacht, nicht als Ersatz. Es soll semantische Lücken füllen, die natives HTML allein nicht schließen kann.

Einer der häufigsten Fehler im Umgang mit ARIA ist die Redundanz – also die Verwendung von ARIA-Attributen, die Informationen wiederholen, die der Browser bereits durch das native HTML-Element kennt. Das ist nicht nur unnötig, sondern kann im schlimmsten Fall sogar zu Verwirrung bei assistiven Technologien (AT) wie Screenreadern führen und die Wartung deines Codes erschweren. Stell es dir so vor, als würdest du ein Schild mit der Aufschrift „Dies ist eine Tür“ an eine ganz normale Tür hängen. Jeder weiß bereits, dass es eine Tür ist. Das Schild ist überflüssig und stiftet eher Verwirrung als Klarheit.

In diesem Kapitel schauen wir uns an, welche ARIA-Attribute oft überflüssigerweise hinzugefügt werden und wie du sie vermeidest, indem du dich auf die eingebaute Semantik von HTML verlässt.

#### Die goldene Regel: Vertraue auf natives HTML

Moderne HTML5-Elemente bringen von Haus aus eine Menge semantischer Bedeutung mit. Ein `<button>`-Element *ist* ein Button. Ein `<nav>`-Element *ist* eine Navigation. Ein `<input type="checkbox">` *ist* eine Checkbox. Der Browser übersetzt diese native Semantik direkt in den sogenannten Accessibility Tree (die Barrierefreiheits-Struktur), den assistive Technologien nutzen, um die Seite zu interpretieren.

Wenn du nun ein ARIA-Attribut hinzufügst, das genau dieselbe Information liefert, gibst du dem Browser eine Anweisung, die er bereits kennt. Das ist im besten Fall nutzloser Code. Im schlechteren Fall kann es zu Konflikten kommen, wenn du zum Beispiel versehentlich einen falschen Wert angibst oder wenn zukünftige Browser-Updates das Verhalten ändern.

Schauen wir uns einige klassische Beispiele für Redundanz an.

#### Landmark-Rollen auf semantischen HTML5-Elementen

HTML5 hat uns eine Reihe von Elementen geschenkt, die wichtige Bereiche einer Webseite definieren, die sogenannten „Landmarks“. Diese helfen Nutzern von Screenreadern, schnell zu wichtigen Abschnitten wie der Hauptnavigation oder dem Footer zu springen. Vor HTML5 musste man dafür `<div>`-Elemente mit ARIA-Rollen verwenden. Heute ist das nicht mehr nötig.

**Falsch (redundant):**

```html
<header role="banner">
  <!-- Seitenkopf -->
</header>

<nav role="navigation">
  <!-- Hauptnavigation -->
</nav>

<main role="main">
  <!-- Hauptinhalt -->
</main>

<footer role="contentinfo">
  <!-- Seitenfuß -->
</footer>
```

**Richtig:**

```html
<header>
  <!-- Seitenkopf -->
</header>

<nav>
  <!-- Hauptnavigation -->
</nav>

<main>
  <!-- Hauptinhalt -->
</main>

<footer>
  <!-- Seitenfuß -->
</footer>
```

Die Elemente `<header>`, `<nav>`, `<main>` und `<footer>` haben ihre entsprechenden Landmark-Rollen (`banner`, `navigation`, `main`, `contentinfo`) bereits fest eingebaut. Die explizite Zuweisung über `role` ist also reines Rauschen im Code. Du wiederholst nur, was ohnehin schon da ist.

#### Rollen für interaktive Elemente

Ähnlich verhält es sich mit interaktiven Elementen wie Buttons, Links oder Formularfeldern. Ihre Rolle ist durch das HTML-Tag selbst definiert.

**Buttons**

Ein `<button>`-Element wird von assistiven Technologien automatisch als Button erkannt.

**Falsch (redundant):**

```html
<button role="button">Speichern</button>
```

**Richtig:**

```html
<button>Speichern</button>
```

Die `role="button"` ist hier absolut überflüssig. Nutze sie nur dann, wenn du ein Element, das von Natur aus kein Button ist (wie ein `<div>` oder `<span>`), aus zwingenden Gründen zu einem Button machen musst. Aber selbst dann ist es fast immer die bessere Wahl, einfach ein `<button>`-Element zu verwenden und es mit CSS nach deinen Wünschen zu gestalten.

**Links**

Ein `<a>`-Element mit einem `href`-Attribut ist die Definition eines Links.

**Falsch (redundant):**

```html
<a href="/kontakt" role="link">Kontakt</a>
```

**Richtig:**

```html
<a href="/kontakt">Kontakt</a>
```

Solange das `href`-Attribut vorhanden ist, weiß der Browser, dass es sich um einen Link handelt. Die `role="link"` ist implizit vorhanden.

#### Zustände und Eigenschaften in Formularfeldern

Formulare sind ein Hotspot für redundante ARIA-Attribute, weil HTML hier bereits sehr mächtige native Attribute zur Verfügung stellt.

**Deaktivierte Elemente**

Um ein Element zu deaktivieren, solltest du immer das `disabled`-Attribut von HTML verwenden und nicht `aria-disabled`.

**Falsch (semantisch unvollständig):**

```html
<button aria-disabled="true">Senden</button>
```

**Richtig (und besser):**

```html
<button disabled>Senden</button>
```

Warum ist das `disabled`-Attribut besser? Es tut mehr als nur den Zustand an assistive Technologien zu kommunizieren. Es verhindert auch, dass das Element den Fokus erhält oder bei Formularübermittlungen gesendet wird. Zudem kannst du es einfach mit CSS über den `:disabled`-Selektor gestalten. `aria-disabled="true"` teilt dem Screenreader zwar mit, dass das Element deaktiviert ist, aber es bleibt weiterhin fokussierbar und klickbar, wenn du dies nicht zusätzlich mit JavaScript verhinderst. Du müsstest also mehr Arbeit investieren, um das gleiche Ergebnis wie mit dem einfachen `disabled`-Attribut zu erzielen.

**Checkboxen und Radio-Buttons**

Der Zustand „ausgewählt“ wird bei Checkboxen und Radio-Buttons über das `checked`-Attribut gesteuert.

**Falsch (redundant und fehleranfällig):**

```html
<input type="checkbox" role="checkbox" aria-checked="true"> Ich stimme zu
```

**Richtig:**

```html
<input type="checkbox" checked> Ich stimme zu
```

Das `type="checkbox"` definiert bereits die `role="checkbox"`. Das `checked`-Attribut setzt den Zustand. `aria-checked` ist für diesen Anwendungsfall überflüssig. Es wird für benutzerdefinierte Steuerelemente benötigt, die wie Checkboxen aussehen und sich so verhalten, aber nicht aus einem `<input>`-Element bestehen.

**Pflichtfelder**

Um ein Feld als Pflichtfeld zu kennzeichnen, gibt es das `required`-Attribut.

**Falsch (redundant):**

```html
<label for="email">E-Mail:</label>
<input type="email" id="email" aria-required="true">
```

**Richtig:**

```html
<label for="email">E-Mail:</label>
<input type="email" id="email" required>
```

Genau wie `disabled` bietet auch `required` mehr als nur die Semantik für Screenreader. Es aktiviert die clientseitige Validierung des Browsers und stellt CSS-Pseudoklassen wie `:required` und `:invalid` für das Styling bereit.

**Beschriftungen von Formularfeldern**

Eine der wichtigsten Regeln für barrierefreie Formulare ist die korrekte Verknüpfung von `<label>` und `<input>`. Wenn diese Verknüpfung besteht, wird der Text des Labels automatisch zum „accessible name“ des Eingabefeldes.

**Falsch (redundant):**

```html
<label for="username">Benutzername:</label>
<input type="text" id="username" aria-label="Benutzername">
```

**Richtig:**

```html
<label for="username">Benutzername:</label>
<input type="text" id="username">
```

Da das `<label>` bereits über das `for`-Attribut mit dem `<input>` verbunden ist, ist `aria-label` hier überflüssig. Ein Screenreader würde den Namen „Benutzername“ jetzt doppelt oder widersprüchlich hören, je nach Implementierung. `aria-label` ist dann sinnvoll, wenn es *kein* sichtbares Label gibt, zum Beispiel bei einem Button, der nur ein Icon enthält.

```html
<!-- Guter Anwendungsfall für aria-label -->
<button aria-label="Suchen">
  <svg><!-- Lupe-Icon --></svg>
</button>
```

#### Warum Redundanz schadet

Du fragst dich vielleicht: „Was ist so schlimm daran? Es schadet doch nicht, oder?“ In manchen Fällen mag es neutral sein, aber es birgt Risiken:

1.  **Konfliktpotenzial:** Was passiert, wenn das native HTML und das ARIA-Attribut unterschiedliche Informationen liefern? Zum Beispiel `<input type="checkbox" checked aria-checked="false">`. Welcher Angabe soll eine assistive Technologie vertrauen? Solche Konflikte führen zu unvorhersehbarem Verhalten.
2.  **Erhöhter Wartungsaufwand:** Dein Code wird unnötig aufgebläht. Wenn du den Zustand eines Elements mit JavaScript änderst, musst du daran denken, sowohl das native Attribut (z. B. `disabled`) als auch das ARIA-Attribut (`aria-disabled`) zu aktualisieren. Das ist eine zusätzliche Fehlerquelle.
3.  **Verwischung des Wissens:** Wenn du dich daran gewöhnst, ARIA überall hinzuzufügen, verlierst du das Gefühl dafür, was HTML von Haus aus kann. Du beginnst, ARIA als Krücke zu benutzen, anstatt die soliden Grundlagen von semantischem HTML zu meistern.

Die einfache Faustregel lautet: **Wenn HTML es kann, lass HTML es tun.** Greife erst dann zu ARIA, wenn du an die Grenzen der nativen HTML-Semantik stößt. Das ist typischerweise bei komplexen, dynamischen Widgets der Fall, die es in HTML nicht standardmäßig gibt, wie ein Karussell, eine Registerkarten-Navigation (Tabs) oder eine aufklappbare Combobox. In diesen Fällen ist ARIA unerlässlich, um Rollen, Zustände und Eigenschaften zu vermitteln. Aber für die alltäglichen Bausteine des Webs – Buttons, Links, Formulare und Seitenstruktur – ist natives HTML fast immer die beste, robusteste und einfachste Wahl.
