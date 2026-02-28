# Tastaturbedienung

# Navigation ohne Maus: Die Kunst der Tastaturbedienung

Stell dir vor, deine Maus funktioniert plötzlich nicht mehr. Oder du hast dir den Arm gebrochen und kannst sie nur umständlich bedienen. Vielleicht gehörst du aber auch zu den Menschen, die aus Effizienzgründen am liebsten alles mit der Tastatur steuern. Für eine riesige Gruppe von Nutzern ist die Tastaturbedienung keine persönliche Vorliebe, sondern die einzige Möglichkeit, sich im Web zu bewegen. Dazu gehören Menschen mit motorischen Einschränkungen oder blinde Nutzer, die auf Screenreader angewiesen sind, welche wiederum über die Tastatur gesteuert werden.

Eine Webseite, die sich nicht vollständig mit der Tastatur bedienen lässt, ist für diese Menschen schlichtweg unbenutzbar. Als Webentwickler liegt es in deiner Verantwortung, diese grundlegende Form der Barrierefreiheit sicherzustellen. Die gute Nachricht ist: Wenn du semantisches HTML korrekt einsetzt, hast du den größten Teil der Arbeit bereits erledigt.

### Der Fokus – Dein Wegweiser im Web

Das zentrale Konzept der Tastaturnavigation ist der „Fokus“. Der Fokus ist wie ein Scheinwerfer, der auf das aktuell aktive Element auf der Seite gerichtet ist. Nur das Element, das den Fokus hat, kann auf Tastatureingaben reagieren. In den meisten Browsern wird das fokussierte Element durch einen farbigen Rahmen (die „Focus Outline“) hervorgehoben.

Mit der `Tab`-Taste springst du von einem interaktiven Element zum nächsten. Mit `Shift` + `Tab` bewegst du dich in umgekehrter Reihenfolge zurück. Interaktive Elemente sind zum Beispiel Links, Buttons oder Formularfelder. Sobald ein Element den Fokus hat, kannst du es bedienen: Bei einem Link drückst du `Enter`, um ihm zu folgen. Einen Button aktivierst du mit `Enter` oder der `Leertaste`. In einem Textfeld kannst du sofort anfangen zu tippen.

Der visuelle Fokusindikator ist überlebenswichtig. Ein häufiger Fehler in der Webentwicklung ist das Entfernen dieses Rahmens aus ästhetischen Gründen mit CSS:

```css
/* BITTE NICHT SO MACHEN! */
:focus {
  outline: none;
}
```

Wenn du das tust, nimmst du Tastaturnutzern die Orientierung. Sie wissen nicht mehr, wo auf der Seite sie sich befinden. Es ist, als würdest du versuchen, mit verbundenen Augen durch einen Raum zu navigieren. Wenn dir der Standard-Fokusring des Browsers nicht gefällt, ist das kein Problem. Aber anstatt ihn einfach zu entfernen, solltest du ihn durch eine eigene, klar sichtbare Hervorhebung ersetzen.

```css
/* Eine bessere Alternative */
:focus {
  outline: 2px solid #005fcc;
  box-shadow: 0 0 5px rgba(0, 95, 204, 0.7);
  background-color: #e6f0fa;
}
```

Eine noch modernere und oft bessere Lösung ist die Pseudoklasse `:focus-visible`. Sie sorgt dafür, dass der Fokusstil nur dann angezeigt wird, wenn der Nutzer tatsächlich mit der Tastatur navigiert. Klickt jemand mit der Maus auf einen Button, erscheint der benutzerdefinierte Fokusring nicht, was oft als ästhetisch ansprechender empfunden wird. Der Browser ist dabei schlau genug, den Unterschied zu erkennen.

```css
/* Die moderne und empfohlene Methode */
:focus-visible {
  outline: 2px solid #005fcc;
  outline-offset: 2px;
}
```

### Die natürliche Reihenfolge – Warum der Quellcode entscheidet

In welcher Reihenfolge springt der Fokus von Element zu Element? Die Antwort ist einfach und fundamental: in der Reihenfolge, in der die Elemente im HTML-Quellcode (im DOM) stehen.

Das ist einer der Gründe, warum eine logische und semantische Struktur deines HTML-Dokuments so entscheidend ist. Eine typische Seitenstruktur sieht so aus:

1.  Header mit Logo und Hauptnavigation
2.  Hauptinhalt (`<main>`)
3.  Seitenleiste (`<aside>`)
4.  Footer

Wenn dein HTML-Code diese logische Reihenfolge widerspiegelt, wird auch die Fokusreihenfolge intuitiv und nachvollziehbar sein. Der Nutzer tabbt zuerst durch den Header, dann durch den Hauptinhalt und so weiter.

Problematisch wird es, wenn du versuchst, das Layout ausschließlich mit CSS zu manipulieren, ohne die HTML-Struktur anzupassen. Stell dir vor, du hast im HTML zuerst die Seitenleiste und dann den Hauptinhalt notiert, aber mit CSS Grid oder Flexbox die Seitenleiste visuell nach rechts verschoben. Für einen sehenden Nutzer mag das Layout korrekt aussehen. Ein Tastaturnutzer würde jedoch von der Hauptnavigation direkt in die Seitenleiste springen und müsste sich erst durch alle dortigen Links kämpfen, bevor er zum eigentlichen Inhalt der Seite gelangt. Das ist frustrierend und unlogisch.

**Die goldene Regel lautet: Die Lesereihenfolge im Quellcode sollte der visuellen Lesereihenfolge entsprechen.**

### Wer bekommt den Fokus? Interaktive Elemente von Haus aus

Nicht jedes HTML-Element kann standardmäßig den Fokus erhalten. Nur die sogenannten interaktiven Elemente sind von Natur aus Teil der Tab-Reihenfolge. Dazu gehören:

*   `<a>` mit einem `href`-Attribut
*   `<button>`
*   `<input>` (alle Typen, die nicht `hidden` sind)
*   `<select>`
*   `<textarea>`
*   `<summary>` innerhalb eines `<details>`-Elements

Elemente wie `<div>`, `<span>` oder `<p>` sind nicht interaktiv und werden beim Tabbing übersprungen. Das ist auch gut so, denn niemand möchte durch jeden einzelnen Paragraphen einer Seite tabben müssen.

Hier liegt eine der häufigsten Fallen für die Barrierefreiheit. Entwickler erstellen oft klickbare Elemente aus `<div>`s und fügen die Funktionalität mit JavaScript hinzu:

```html
<!-- FALSCH: Ein nicht barrierefreies "Button"-Element -->
<div class="custom-button" onclick="doSomething()">Aktion ausführen</div>
```

Dieses `<div>` hat gleich mehrere Probleme:
1.  **Es ist nicht fokussierbar:** Ein Tastaturnutzer kann es niemals erreichen.
2.  **Es ist nicht aktivierbar:** Selbst wenn man es fokussierbar machen würde, reagiert es nicht auf `Enter` oder die `Leertaste`.
3.  **Es hat keine Semantik:** Ein Screenreader weiß nicht, dass es sich um einen Button handelt. Er liest nur den Text "Aktion ausführen" vor, ohne den Kontext einer interaktiven Schaltfläche.

Die korrekte, semantische und barrierefreie Lösung ist denkbar einfach:

```html
<!-- KORREKT: Ein von Natur aus barrierefreier Button -->
<button type="button" onclick="doSomething()">Aktion ausführen</button>
```

Mit diesem `<button>`-Element erhältst du die gesamte Tastatur-Funktionalität geschenkt. Es ist automatisch fokussierbar, reagiert auf die richtigen Tasten und wird von Screenreadern als "Schaltfläche" angekündigt.

### Das `tabindex`-Attribut: Mächtiges Werkzeug mit Verantwortung

Manchmal möchtest du das Standardverhalten der Fokusreihenfolge gezielt beeinflussen. Dafür gibt es das `tabindex`-Attribut. Es kann drei Arten von Werten annehmen, und du solltest genau wissen, was sie bewirken.

#### `tabindex="0"`

Mit `tabindex="0"` kannst du ein Element, das normalerweise nicht fokussierbar ist (wie ein `<div>` oder `<span>`), in die natürliche Tab-Reihenfolge aufnehmen. Es wird an der Stelle fokussiert, an der es im Quellcode erscheint.

Das ist nützlich, wenn du komplexe, benutzerdefinierte Widgets baust, für die es kein natives HTML-Element gibt. Wenn du zum Beispiel eine interaktive Kartenkomponente aus `<div>`s erstellst, könntest du dem Hauptcontainer `tabindex="0"` geben, damit ein Nutzer ihn mit der Tastatur ansteuern kann. Wichtig ist hierbei, dass du dann auch per JavaScript dafür sorgen musst, dass das Element auf Tastatureingaben (wie die Pfeiltasten zur Navigation auf der Karte) reagiert.

#### `tabindex="-1"`

Der Wert `-1` ist besonders interessant. Er macht ein Element fokussierbar, aber **nicht** über die `Tab`-Taste. Das Element wird aus der natürlichen Tab-Reihenfolge entfernt. Wozu ist das gut? Du kannst den Fokus nun gezielt mit JavaScript auf dieses Element setzen, zum Beispiel mit der Methode `element.focus()`.

Ein klassischer Anwendungsfall ist ein modales Dialogfenster. Wenn sich ein Modal öffnet, möchtest du, dass der Fokus direkt in das Fenster springt (z. B. auf den Schließen-Button oder das erste Eingabefeld). Außerdem soll der Fokus im Modal "gefangen" bleiben, solange es geöffnet ist. Das Dialogfenster selbst (das `<div>`, das den Container darstellt) könnte `tabindex="-1"` erhalten, damit du nach dem Öffnen `modalElement.focus()` aufrufen kannst. Dadurch wird der Screenreader-Fokus direkt dorthin bewegt und der Nutzer weiß sofort, was passiert ist.

#### `tabindex` mit einem positiven Wert (`1`, `2`, `3`, ...)

**Vermeide `tabindex` mit einem Wert größer als 0, wo immer es geht.**

Ein `tabindex="1"`, `tabindex="5"` oder `tabindex="99"` erzwingt eine feste Fokusreihenfolge. Elemente mit einem `tabindex` von 1 werden zuerst angesprungen, dann die mit 2, und so weiter. Erst danach werden alle Elemente mit `tabindex="0"` und die nativ fokussierbaren Elemente in ihrer normalen DOM-Reihenfolge durchlaufen.

Das klingt vielleicht verlockend, um die Reihenfolge zu steuern, aber es ist ein Albtraum für die Wartung und führt fast immer zu einer unlogischen und frustrierenden Benutzererfahrung. Sobald du auch nur ein einziges Element mit einem positiven `tabindex` hinzufügst, musst du die Reihenfolge für alle anderen Elemente manuell verwalten. Ändert sich die Seite, musst du alle Indizes anpassen. Es ist fragil, fehleranfällig und zerstört die natürliche, vom Quellcode vorgegebene Logik. Halte dich an eine saubere HTML-Struktur, dann brauchst du diese Werte nicht.

### Ein praktisches Beispiel: Der Skip-Link

Eine Webseite mit einer umfangreichen Navigation im Header kann für Tastaturnutzer mühsam sein. Bei jedem Seitenwechsel müssen sie sich erneut durch Dutzende von Navigationslinks tabben, bevor sie zum eigentlichen Inhalt gelangen.

Eine elegante Lösung hierfür ist der "Skip-to-Content"-Link oder kurz Skip-Link. Das ist ein Link, der als allererstes Element im `<body>` platziert wird. Er ist standardmäßig visuell verborgen und wird nur sichtbar, wenn er den Fokus erhält – also wenn ein Nutzer direkt nach dem Laden der Seite die `Tab`-Taste drückt.

```html
<body>
  <a href="#main-content" class="skip-link">Zum Hauptinhalt springen</a>
  <header>
    <!-- ... Umfangreiche Navigation ... -->
  </header>
  <main id="main-content" tabindex="-1">
    <!-- ... Der eigentliche Seiteninhalt ... -->
  </main>
</body>
```

Der Link verweist auf die ID des Hauptinhaltsbereichs (`<main>`). Damit der Sprung auch in allen Browsern den Fokus korrekt setzt, erhält das `<main>`-Element ein `tabindex="-1"`.

Das zugehörige CSS sorgt dafür, dass der Link nur bei Fokus sichtbar wird:

```css
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  background: #000;
  color: #fff;
  padding: 8px;
  z-index: 100;
  transition: top 0.3s;
}

.skip-link:focus {
  top: 0;
}

/* Wichtig, damit der Fokus nach dem Sprung korrekt gesetzt wird */
main:focus {
    outline: none;
}
```

Mit dieser einfachen Technik verbesserst du die Benutzerfreundlichkeit für Tastaturnutzer erheblich. Du bietest ihnen eine Abkürzung, die ihre Navigation beschleunigt und effizienter macht. Es ist ein kleines Detail mit großer Wirkung, das zeigt, dass du die Bedürfnisse all deiner Nutzer ernst nimmst.
