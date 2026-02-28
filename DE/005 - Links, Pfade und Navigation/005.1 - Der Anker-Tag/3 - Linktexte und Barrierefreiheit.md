# Linktexte und Barrierefreiheit

## Linktexte und Barrierefreiheit

Ein Link ist mehr als nur ein technisches Element, das dich von A nach B bringt. Er ist ein Versprechen an deine Nutzer. Der Text, auf den man klickt – der sogenannte Anker- oder Linktext – ist die Formulierung dieses Versprechens. Er schafft eine Erwartungshaltung darüber, was hinter dem Klick wartet. Ein gut formulierter Linktext ist entscheidend für eine intuitive Navigation und eine positive Nutzererfahrung. Noch wichtiger wird er jedoch, wenn wir über Barrierefreiheit sprechen.

Für Menschen, die auf assistive Technologien wie Screenreader angewiesen sind, ist der Linktext oft der einzige Anhaltspunkt, um den Inhalt einer Seite zu erfassen und sich darauf zu bewegen. Ein schlecht gewählter Linktext kann eine Webseite unbenutzbar machen. Schauen wir uns genauer an, wie du Links gestaltest, die für wirklich jeden funktionieren.

### Das Todesurteil für gute Linktexte: „Hier klicken“

Du hast es sicher schon tausendmal gesehen: Links, die mit „hier“, „mehr erfahren“, „weiterlesen“ oder „hier klicken“ beschriftet sind. Auf den ersten Blick mag das harmlos erscheinen, doch es ist eine der größten Sünden in der Webentwicklung, sowohl aus Sicht der Usability als auch der Barrierefreiheit.

Stell dir vor, du könntest eine Webseite nicht sehen und würdest einen Screenreader benutzen. Viele Nutzer solcher Programme navigieren, indem sie sich eine Liste aller Links auf der Seite vorlesen lassen. Diese Liste könnte dann so aussehen:

*   hier klicken
*   hier
*   hier klicken
*   mehr
*   weiterlesen
*   hier

Diese Liste ist völlig nutzlos. Es fehlt jeglicher Kontext. Worüber erfahre ich „mehr“? Wohin gelange ich, wenn ich „hier“ klicke? Der Nutzer ist gezwungen, den gesamten umgebenden Text zu lesen, um den Zweck eines jeden Links zu verstehen. Das ist mühsam und ineffizient.

Ein guter Linktext funktioniert auch ohne den umgebenden Satz. Er ist selbsterklärend.

**Schlechtes Beispiel:**

```html
<p>
  Um unsere detaillierte Produktbroschüre herunterzuladen,
  <a href="/downloads/broschuere.pdf">klicke hier</a>.
</p>
```

**Gutes Beispiel:**

```html
<p>
  Lade unsere <a href="/downloads/broschuere.pdf">detaillierte Produktbroschüre (PDF)</a>
  herunter, um alle Informationen zu erhalten.
</p>
```

Im zweiten Beispiel ist der Linktext „detaillierte Produktbroschüre (PDF)“ aussagekräftig. Der Nutzer weiß sofort, was er bekommt. Der Zusatz „(PDF)“ ist ebenfalls hilfreich, da er über das Dateiformat informiert und darauf hinweist, dass die Datei möglicherweise heruntergeladen und mit einer anderen Anwendung geöffnet wird.

### Eigenschaften eines guten Linktextes

Ein barrierefreier und nutzerfreundlicher Linktext sollte immer die folgenden Kriterien erfüllen:

1.  **Aussagekräftig:** Er beschreibt klar und präzise, wohin der Link führt oder welche Aktion er auslöst. Was erwartet den Nutzer nach dem Klick? Ein neuer Artikel, ein Download, eine Kontaktseite?
2.  **Konkret:** Vermeide vage Formulierungen. Statt „Erfahre mehr über unsere Öffnungszeiten“ ist „Unsere Öffnungszeiten ansehen“ direkter und klarer.
3.  **Einzigartig (auf der Seite):** Wenn mehrere Links auf einer Seite den gleichen Linktext haben, sollten sie auch zum exakt gleichen Ziel führen. Unterschiedliche Ziele mit identischem Linktext sind extrem verwirrend.
4.  **Verständlich ohne Kontext:** Wie im Beispiel oben gezeigt, sollte der Linktext für sich allein stehen können.

Vermeide es außerdem, die URL selbst als Linktext zu verwenden, es sei denn, die URL ist der eigentliche Inhalt, der kommuniziert werden soll (z. B. in einem Text über Domainnamen).

**Schlechtes Beispiel:**

```html
<p>
  Besuche uns auf https://www.beispiel-firma.de/ueber-uns/team/management.
</p>
```

**Gutes Beispiel:**

```html
<p>
  Lerne <a href="https://www.beispiel-firma.de/ueber-uns/team/management">unser Management-Team</a> kennen.
</p>
```

Ein Screenreader würde die schlechte Variante Buchstabe für Buchstabe vorlesen, was eine Qual ist. Die gute Variante ist kurz, prägnant und informativ.

### Links, die nur aus Icons bestehen

Manchmal besteht ein Link nur aus einem Symbol, zum Beispiel einem Warenkorb-Icon, einem Druckersymbol oder einem Kreuz zum Schließen eines Fensters. Für sehende Nutzer ist die Bedeutung oft klar, aber für einen Screenreader ist ein Bild ohne textliche Alternative leer und bedeutungslos.

Hier kommt die Magie von ARIA (Accessible Rich Internet Applications) ins Spiel. Speziell das `aria-label`-Attribut ist hier dein bester Freund. Es erlaubt dir, einen zugänglichen Namen für ein Element zu definieren, der nur von assistiven Technologien gelesen wird, aber nicht sichtbar ist.

Betrachten wir einen Löschen-Button, der nur ein Mülleimer-Icon enthält:

**Schlechtes Beispiel (unzugänglich):**

```html
<a href="/items/123/delete">
  <img src="/icons/trash.svg" alt=""> <!-- Leeres alt-Attribut! -->
</a>
```

Ein Screenreader würde hier entweder nichts oder den Dateinamen des Bildes vorlesen. Beides ist nicht hilfreich.

**Gutes Beispiel (zugänglich):**

```html
<a href="/items/123/delete" aria-label="Eintrag 123 löschen">
  <img src="/icons/trash.svg" alt="" role="presentation">
</a>
```

Hier passiert etwas Wichtiges:
*   Das `aria-label` gibt dem Link einen klaren, verständlichen Namen für Screenreader: „Eintrag 123 löschen“.
*   Das `img`-Element hat ein leeres `alt`-Attribut (`alt=""`) und zusätzlich `role="presentation"`. Dies signalisiert dem Screenreader, dass das Bild rein dekorativ ist und ignoriert werden soll. Die gesamte Information kommt vom umgebenden `<a>`-Tag. So wird verhindert, dass der Screenreader redundante oder verwirrende Informationen (wie den Dateinamen) ausgibt.

#### Eine kurze Warnung zum `title`-Attribut

Vielleicht denkst du jetzt an das `title`-Attribut, das einen kleinen Tooltip anzeigt, wenn man mit der Maus darüberfährt. Es ist verlockend, es für zusätzliche Informationen zu nutzen.

```html
<!-- Bitte nicht so machen für wichtige Infos! -->
<a href="/items/123/delete" title="Eintrag löschen">
  <img src="/icons/trash.svg" alt="">
</a>
```

Vermeide diesen Ansatz für Barrierefreiheit. Das `title`-Attribut hat einige entscheidende Nachteile:
*   Es ist auf Touch-Geräten nicht zugänglich, da es kein „Hover“-Ereignis gibt.
*   Viele Screenreader ignorieren das `title`-Attribut standardmäßig oder lesen es nur in bestimmten Konfigurationen vor.
*   Es ist für Tastaturnutzer, die nicht die Maus benutzen, oft nicht sichtbar.

Verwende `aria-label` für Informationen, die für assistive Technologien bestimmt sind. Das `title`-Attribut ist nur für nebensächliche, nicht kritische Zusatzinformationen geeignet.

### Links, die in einem neuen Tab öffnen

Manchmal ist es sinnvoll, einen Link in einem neuen Browser-Tab zu öffnen, zum Beispiel bei externen Links oder beim Öffnen von PDF-Dokumenten. Dies geschieht mit dem Attribut `target="_blank"`.

```html
<a href="https.example.com" target="_blank">Besuche unsere Partnerseite</a>
```

Aus Sicherheitsgründen solltest du `target="_blank"` immer mit `rel="noopener noreferrer"` kombinieren. Das verhindert, dass die neu geöffnete Seite Kontrolle über die ursprüngliche Seite erlangen kann.

```html
<a href="https.example.com" target="_blank" rel="noopener noreferrer">
  Besuche unsere Partnerseite
</a>
```

Das Öffnen eines neuen Tabs kann für manche Nutzer jedoch desorientierend sein, insbesondere für Menschen mit kognitiven Einschränkungen oder Screenreader-Nutzer. Der „Zurück“-Button des Browsers funktioniert nicht mehr wie erwartet, und der Kontext geht verloren.

Die beste Praxis ist es, den Nutzer darüber zu informieren, dass sich ein neuer Tab öffnen wird.

**Möglichkeit 1: Visueller Hinweis**

Du kannst den Hinweis direkt in den Linktext schreiben oder ein kleines Icon hinzufügen.

```html
<a href="partner.pdf" target="_blank" rel="noopener noreferrer">
  Unsere Partnerbroschüre (öffnet in neuem Tab)
</a>
```

**Möglichkeit 2: Hinweis für Screenreader**

Wenn du den visuellen Text nicht überladen möchtest, kannst du die Information für Screenreader-Nutzer verstecken. Dafür nutzt man oft eine CSS-Klasse, die Text visuell verbirgt, ihn aber für Screenreader lesbar lässt.

Zuerst das CSS:

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

Und dann das HTML:

```html
<a href="partner.pdf" target="_blank" rel="noopener noreferrer">
  Unsere Partnerbroschüre
  <span class="visually-hidden">(öffnet in neuem Tab)</span>
</a>
```

Ein sehender Nutzer liest nur „Unsere Partnerbroschüre“. Ein Screenreader-Nutzer hört „Unsere Partnerbroschüre (öffnet in neuem Tab)“. So erhalten alle Nutzer die für sie relevanten Informationen.

### Wenn Bilder zu Links werden

Eine letzte wichtige Regel betrifft Bilder, die vollständig von einem Anker-Tag umschlossen sind. In diesem Fall übernimmt das `alt`-Attribut des Bildes die Funktion des Linktextes.

Stell dir ein Bild eines neuen Produkts vor, das zur Produktseite verlinkt.

**Schlechtes Beispiel:**

```html
<a href="/produkte/super-widget">
  <img src="super-widget.jpg" alt="Ein Foto des Super-Widgets">
</a>
```

Der `alt`-Text „Ein Foto des Super-Widgets“ beschreibt zwar das Bild, aber nicht das Ziel des Links. Ein Screenreader würde ankündigen: „Link, Bild, Ein Foto des Super-Widgets.“ Der Nutzer weiß nicht, dass er durch einen Klick zur Produktseite gelangt.

**Gutes Beispiel:**

```html
<a href="/produkte/super-widget">
  <img src="super-widget.jpg" alt="Details zum neuen Super-Widget ansehen">
</a>
```

Hier beschreibt der `alt`-Text die Aktion, die der Link auslöst. Er dient als perfekter, aussagekräftiger Linktext. Die Regel lautet also: Wenn ein Bild der einzige Inhalt eines Links ist, muss sein `alt`-Text den Zweck des Links beschreiben, nicht nur das Bild selbst.

Indem du diese Prinzipien befolgst, stellst du sicher, dass die Navigation auf deiner Webseite nicht nur für eine sehende Mehrheit mit Maus intuitiv ist, sondern für absolut jeden – unabhängig davon, wie er oder sie auf das Web zugreift.
