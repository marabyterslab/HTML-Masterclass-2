# Linktexte und Barrierefreiheit

### Linktexte und Barrierefreiheit

Ein Link ist ein Versprechen. Wenn du einen Link auf deiner Webseite platzierst, gibst du deinen Nutzern ein Versprechen darüber, was sie erwartet, wenn sie darauf klicken. Der Text, der diesen Link darstellt – der sogenannte Linktext – ist die Formulierung dieses Versprechens. Ein guter Linktext ist klar, präzise und ehrlich. Ein schlechter Linktext ist vage, irreführend und schafft Frustration. Im Kontext der Barrierefreiheit ist der Unterschied zwischen gut und schlecht nicht nur eine Frage der Benutzerfreundlichkeit, sondern der grundsätzlichen Nutzbarkeit deiner Seite.

#### Warum „Hier klicken“ nicht ausreicht

Du hast sie sicher schon tausendfach gesehen: Links mit Texten wie „Hier klicken“, „Mehr erfahren“, „Weiterlesen“ oder einfach nur „Link“. Auf den ersten Blick scheinen sie harmlos. Im umgebenden Satz ergibt sich der Kontext ja meist von selbst.

Zum Beispiel so:

```html
<!-- Schlechtes Beispiel -->
<p>
  Wir haben kürzlich unseren Jahresbericht 2023 veröffentlicht. 
  Um den Bericht herunterzuladen, <a href="/reports/jahresbericht-2023.pdf">klicke hier</a>.
</p>
```

Für sehende Nutzer ist das zwar nicht optimal, aber machbar. Sie überfliegen den Satz, verstehen den Kontext und klicken dann auf den blau unterstrichenen Teil. Es ist aber ineffizient. Der Nutzer muss erst den umgebenden Text verarbeiten, um zu verstehen, wohin der Link führt.

Für Menschen, die auf assistierende Technologien wie Screenreader angewiesen sind, ist dieser Ansatz jedoch eine Katastrophe. Ein Screenreader ist eine Software, die den Bildschirminhalt vorliest. Blinde oder stark sehbehinderte Nutzer navigieren damit durch Webseiten. Eine der wichtigsten Navigationsfunktionen eines Screenreaders ist die Möglichkeit, sich eine Liste aller Links auf einer Seite ausgeben zu lassen.

Stell dir nun eine solche Link-Liste vor, die aus dem Inhalt einer Webseite generiert wird:

*   Hier klicken
*   Mehr erfahren
*   Hier klicken
*   Weiterlesen
*   Mehr

Diese Liste ist vollkommen nutzlos. Es gibt keinerlei Kontext. Der Nutzer hat keine Ahnung, wohin „Hier klicken“ führt, ohne mühsam den umgebenden Text zu suchen und zu interpretieren. Die Webseite wird zu einem Labyrinth ohne Wegweiser.

#### Die Kunst des aussagekräftigen Linktextes

Die Lösung ist einfach und wirkungsvoll: Der Linktext selbst sollte das Ziel des Links beschreiben. Er sollte so formuliert sein, dass er auch ohne den umgebenden Kontext verständlich ist.

Nehmen wir unser vorheriges Beispiel und formulieren es um:

```html
<!-- Gutes Beispiel -->
<p>
  Wir haben kürzlich unseren <a href="/reports/jahresbericht-2023.pdf">Jahresbericht 2023 veröffentlicht</a>.
</p>
```

Der Linktext lautet nun „Jahresbericht 2023 veröffentlicht“. Das ist eine klare und unmissverständliche Aussage. In der vom Screenreader generierten Link-Liste erscheint nun dieser Eintrag. Der Nutzer weiß sofort: „Aha, dieser Link führt mich zum Jahresbericht 2023.“

Hier sind ein paar weitere Vorher-Nachher-Beispiele:

**Schlecht:**
> Um unsere Produkte zu sehen, klicken Sie <a href="/produkte">hier</a>.

**Gut:**
> Werfen Sie einen Blick auf <a href="/produkte">unsere Produktübersicht</a>.

**Schlecht:**
> Du willst mehr wissen? <a href="/ueber-uns.html">Weiter...</a>

**Gut:**
> <a href="/ueber-uns.html">Erfahre mehr über unser Team und unsere Geschichte</a>.

Ein guter Linktext beantwortet die Frage des Nutzers: „Was passiert, wenn ich hier klicle?“ Die Antwort sollte immer eine präzise Beschreibung des Ziels sein. Ein positiver Nebeneffekt: Auch Suchmaschinen wie Google verstehen durch aussagekräftige Linktexte besser, worum es auf der verlinkten Seite geht, was sich positiv auf dein Suchmaschinenranking auswirken kann.

#### Wenn Bilder zu Links werden

Manchmal besteht ein Link nicht aus Text, sondern aus einem Bild – zum Beispiel einem Warenkorb-Symbol, einem Logo, das zur Startseite führt, oder einem Social-Media-Icon. Auch hier müssen wir sicherstellen, dass der Link ein verständliches „Versprechen“ abgibt.

Da ein `<img>`-Tag keinen eigenen Textinhalt hat, greifen assistierende Technologien auf das `alt`-Attribut (Alternativtext) zurück. Der Alternativtext eines Bildes innerhalb eines Anker-Tags wird zum Linktext für den Screenreader.

```html
<!-- Gutes Beispiel für einen Bild-Link -->
<a href="/warenkorb.html">
  <img src="icons/warenkorb.svg" alt="Zum Warenkorb">
</a>
```

Hier würde der Screenreader vorlesen: „Link, Zum Warenkorb“. Der Zweck des Links ist damit perfekt beschrieben. Ein fehlendes oder leeres `alt`-Attribut (`alt=""`) würde dazu führen, dass der Screenreader stattdessen versucht, den Dateinamen des Bildes (`warenkorb.svg`) vorzulesen – was selten hilfreich ist.

Es gibt eine wichtige Ausnahme: Wenn ein Link sowohl ein Bild als auch einen sichtbaren Text enthält, sollte das Bild als dekorativ behandelt werden. In diesem Fall gibst du dem `<img>`-Tag ein leeres `alt`-Attribut (`alt=""`), um zu verhindern, dass der Screenreader redundante Informationen vorliest.

```html
<!-- Korrekte Handhabung, wenn Bild UND Text im Link sind -->
<a href="/warenkorb.html">
  <img src="icons/warenkorb.svg" alt="">
  Zum Warenkorb (3 Artikel)
</a>
```

Hier würde der Screenreader den Text „Zum Warenkorb (3 Artikel)“ vorlesen. Das `alt=""` sorgt dafür, dass das Icon ignoriert wird und die Information nicht doppelt ausgegeben wird („Link, Zum Warenkorb (3 Artikel)“ anstatt „Link, Warenkorb-Icon, Zum Warenkorb (3 Artikel)“).

#### Zusätzlichen Kontext schaffen, wenn es nötig ist

Manchmal ist es aus Design- oder Platzgründen schwierig, einen langen, beschreibenden Linktext zu verwenden. Stell dir eine Tabelle mit Produkten vor, bei der in jeder Zeile ein „Details“-Link steht.

| Produktname | Preis | Aktion |
| :--- | :--- | :--- |
| Super-Schraubenzieher | 19,99 € | <a href="/p/1">Details</a> |
| Mega-Hammer | 29,99 € | <a href="/p/2">Details</a> |

Visuell ist der Kontext klar. Für einen Screenreader-Nutzer, der sich die Link-Liste anhört, entsteht aber wieder das Problem von mehrdeutigen Links: „Details“, „Details“, „Details“.

Für solche Fälle gibt es die ARIA-Attribute (Accessible Rich Internet Applications). Mit dem Attribut `aria-label` kannst du einem Link einen zugänglichen Namen geben, der den sichtbaren Text für assistierende Technologien überschreibt.

```html
<!-- Verwendung von aria-label für zusätzlichen Kontext -->
<a href="/p/1" aria-label="Details zum Super-Schraubenzieher">Details</a>
<a href="/p/2" aria-label="Details zum Mega-Hammer">Details</a>
```

Visuell ändert sich nichts. Auf dem Bildschirm steht weiterhin nur „Details“. Ein Screenreader wird jedoch den Inhalt des `aria-label`-Attributs vorlesen. Die Link-Liste würde nun so aussehen:

*   Details zum Super-Schraubenzieher
*   Details zum Mega-Hammer

Damit ist die Eindeutigkeit wiederhergestellt, ohne das visuelle Design zu beeinträchtigen.

#### Die Tücke mit neuen Tabs: `target="_blank"`

Das Attribut `target="_blank"` im Anker-Tag bewirkt, dass der Link in einem neuen Browser-Tab oder -Fenster geöffnet wird. Dies kann Nutzer unerwartet aus ihrem aktuellen Kontext reißen. Insbesondere für Menschen mit kognitiven Einschränkungen oder Screenreader-Nutzer kann dies verwirrend sein, da der „Zurück“-Button des Browsers nicht mehr wie erwartet funktioniert.

Die goldene Regel lautet: Vermeide `target="_blank"`, wo immer es geht. Gib dem Nutzer die Kontrolle. Er kann selbst entscheiden, ob er einen Link in einem neuen Tab öffnen möchte (z. B. per Rechtsklick oder mit Strg/Cmd + Klick).

Wenn es aber zwingende Gründe gibt, einen Link in einem neuen Tab zu öffnen (z. B. weil der Nutzer gerade ein Formular ausfüllt und den Fortschritt nicht verlieren soll), musst du ihn darüber informieren. Diese Information muss sowohl visuell als auch für assistierende Technologien zugänglich sein.

Eine gängige Methode ist, dem Linktext einen visuellen Indikator (z. B. ein kleines Icon) und einen unsichtbaren Text für Screenreader hinzuzufügen.

```html
<a href="externes-dokument.pdf" target="_blank">
  Download des Projektplans
  <span class="sr-only">(öffnet in neuem Tab)</span>
</a>
```

Der Text im `<span>` wird visuell versteckt, aber von Screenreadern vorgelesen. Der Screenreader würde also ansagen: „Link, Download des Projektplans (öffnet in neuem Tab)“.

Die dazugehörige CSS-Klasse `.sr-only` (Abkürzung für „screenreader-only“) ist ein Standard-Snippet in der barrierefreien Webentwicklung und sieht typischerweise so aus:

```css
.sr-only {
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

Diese CSS-Regeln verschieben das Element aus dem sichtbaren Bereich, ohne es komplett zu verbergen (`display: none` oder `visibility: hidden` würden es auch für Screenreader unzugänglich machen).

Indem du diese Prinzipien beherzigst, werden deine Links von vagen Wegweisern zu klaren, verlässlichen und inklusiven Navigationsinstrumenten für alle Menschen im Web.
