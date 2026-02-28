# Leere alt-Attribute für dekorative Bilder

### Leere alt-Attribute für dekorative Bilder

Du hast gelernt, wie entscheidend das `alt`-Attribut für die Barrierefreiheit ist. Es ist die Brücke, die den visuellen Inhalt eines Bildes für Menschen übersetzt, die ihn nicht sehen können. Doch was ist, wenn ein Bild gar keine inhaltliche Brücke benötigt? Was, wenn es nur da ist, um schön auszusehen? Hier kommt eine ebenso wichtige Technik ins Spiel: das leere `alt`-Attribut.

Die goldene Regel lautet: Jedes `<img>`-Tag im HTML-Code *muss* ein `alt`-Attribut haben. Das ist nicht verhandelbar. Die interessante Frage ist jedoch, was in dieses Attribut hineingehört. In vielen Fällen ist die Antwort: nichts.

#### Was ist ein dekoratives Bild?

Ein Bild gilt als dekorativ, wenn es rein zur visuellen Gestaltung dient und keine neuen, für das Verständnis des Inhalts relevanten Informationen vermittelt. Wenn du das Bild entfernen würdest, ginge dem Text oder der Funktionalität der Seite keine Bedeutung verloren.

Typische Beispiele für dekorative Bilder sind:

*   **Hintergrundmuster oder Texturen:** Bilder, die nur einen visuellen Rahmen schaffen.
*   **Rein ästhetische Trennlinien:** Eine grafische Linie zwischen zwei Absätzen, die auch durch eine einfache horizontale Linie (`<hr>`) ersetzt werden könnte.
*   **Schmuck-Icons:** Icons, die direkt neben einem Text stehen, der ihre Bedeutung bereits vollständig erklärt. Zum Beispiel ein kleines Briefumschlag-Icon neben dem Link-Text "Kontaktiere uns".
*   **Abstrakte grafische Elemente:** Farbverläufe, Pinselstriche oder geometrische Formen, die das Design auflockern, aber keine spezifische Information tragen.

Für all diese Fälle ist ein beschreibender Alternativtext nicht nur unnötig, sondern sogar störend. Stell dir vor, ein Screenreader-Nutzer navigiert durch eine Seite und hört ständig Ansagen wie "blauer, geschwungener Strich", "kleines, graues Zahnrad" oder "roter Punkt". Das ist digitales Rauschen, das vom eigentlichen Inhalt ablenkt und die Nutzungserfahrung frustrierend macht.

#### Die entscheidende Anweisung: `alt=""`

Um dieses Problem zu lösen, gibst du dem Bild ein leeres `alt`-Attribut.

```html
<img src="bilder/blaue-trennlinie.png" alt="">
```

Dieser Code sieht auf den ersten Blick vielleicht wie ein Fehler oder eine vergessene Angabe aus, aber er ist das genaue Gegenteil. Ein leeres `alt`-Attribut ist eine bewusste und wichtige Anweisung an assistive Technologien wie Screenreader. Du teilst ihnen damit explizit mit: "Dieses Bild ist rein dekorativ. Ignoriere es. Es ist für das Verständnis des Inhalts nicht relevant, also lies es nicht vor."

Der Screenreader wird dieses Bild komplett überspringen und direkt zum nächsten relevanten Element übergehen. Das Ergebnis ist eine saubere, fokussierte und effiziente User Experience für Menschen, die auf diese Technologien angewiesen sind.

#### Der Unterschied zum fehlenden `alt`-Attribut

Es ist absolut entscheidend, den Unterschied zwischen einem leeren und einem fehlenden `alt`-Attribut zu verstehen.

**Falsch (fehlendes Attribut):**

```html
<img src="bilder/profilbild.jpg">
```

Wenn das `alt`-Attribut komplett fehlt, befindet sich der Browser in einem Zustand der Unsicherheit. Er weiß nicht, ob du es vergessen hast oder ob das Bild unwichtig ist. Aus diesem Grund versuchen viele Screenreader, das Problem zu "reparieren", indem sie eine Ersatzinformation vorlesen. Meistens ist das der Dateiname des Bildes. Das führt dann zu einer unschönen und verwirrenden Ausgabe wie: "Bild, profilbild-user-123-final-v2.jpg". Das ist für niemanden hilfreich. Ein fehlendes `alt`-Attribut ist immer ein Fehler in der Barrierefreiheit (und ein HTML-Validierungsfehler).

**Richtig (leeres Attribut für dekorative Bilder):**

```html
<img src="bilder/hintergrund-muster.svg" alt="">
```

Hier gibst du eine klare Anweisung. Du signalisierst: "Ich habe an die Barrierefreiheit gedacht und entschieden, dass dieses Bild ignoriert werden soll." Der Screenreader folgt dieser Anweisung und bleibt still.

#### Praktische Anwendungsfälle

Schauen wir uns einige konkrete Beispiele an, um das Prinzip zu verfestigen.

**1. Icon neben einem Link**

Stell dir einen Download-Button vor. Der Text allein ist schon aussagekräftig.

```html
<a href="dokument.pdf">
  <img src="icons/pdf-icon.svg" alt="">
  Jahresbericht herunterladen (PDF, 2 MB)
</a>
```

Der Text "Jahresbericht herunterladen (PDF, 2 MB)" enthält bereits alle notwendigen Informationen. Das PDF-Icon ist eine nützliche visuelle Hilfe für sehende Nutzer, aber für einen Screenreader-Nutzer wäre die Beschreibung "PDF-Symbol" redundant und störend. Mit `alt=""` wird nur der informative Link-Text vorgelesen, was perfekt ist.

**2. Visuelle Trenner**

Du möchtest Abschnitte deines Artikels mit einer eleganten Grafik trennen statt mit einer einfachen `<hr>`.

```html
<p>Dies ist der erste Abschnitt über die Grundlagen von HTML.</p>

<img src="grafiken/schnörkel-trenner.png" alt="">

<p>Hier beginnt der zweite Abschnitt, der sich mit CSS befasst.</p>
```

Eine Beschreibung wie "goldener Schnörkel-Trenner" würde den Lesefluss unnötig unterbrechen. Das Bild hat keine semantische Bedeutung, es ist reines "Eye-Candy". Also wird es mit `alt=""` korrekt als dekorativ markiert.

**3. Hintergrundbilder im Vordergrund**

Manchmal werden Bilder, die eigentlich wie ein Hintergrund wirken, aus technischen Gründen als `<img>`-Tags im HTML platziert. Das können zum Beispiel abstrakte "Blobs" oder Pinselstriche sein, die hinter einer Überschrift liegen.

```html
<div>
  <h2>Unsere Mission</h2>
  <img src="grafiken/blauer-pinselstrich.svg" alt="" class="hintergrund-deko">
</div>
```

Auch hier gilt: Das Bild fügt der Überschrift "Unsere Mission" keine neue Information hinzu. Es ist rein visuell. `alt=""` ist die richtige Wahl. Würdest du stattdessen `alt="Blauer Pinselstrich"` schreiben, würde ein Screenreader "Überschrift Ebene 2, Unsere Mission, Bild, Blauer Pinselstrich" vorlesen, was die klare Hierarchie und den Inhalt stört.

#### Die Grauzone: Wann ist ein Bild wirklich dekorativ?

Die Entscheidung, ob ein Bild informativ oder dekorativ ist, liegt bei dir als Entwickler. Manchmal ist die Grenze fließend. Die beste Methode, um eine Entscheidung zu treffen, ist die "Was-wäre-wenn"-Frage: **Verliert der Inhalt an Bedeutung oder wird er unverständlich, wenn dieses Bild nicht da wäre?**

*   Wenn die Antwort **"Nein, der Inhalt bleibt vollständig verständlich"** lautet, ist das Bild wahrscheinlich dekorativ und sollte `alt=""` erhalten.
*   Wenn die Antwort **"Ja, eine wichtige Information oder ein bestimmter Kontext geht verloren"** lautet, dann ist das Bild informativ und benötigt einen beschreibenden Alternativtext.

Sei ehrlich zu dir selbst. Oft werden Stockfotos zur reinen Auflockerung einer Seite verwendet. Ein Bild von lächelnden Menschen in einem Meeting auf einer "Über uns"-Seite vermittelt vielleicht eine allgemeine Stimmung, aber selten eine konkrete, unverzichtbare Information. In vielen solchen Fällen ist `alt=""` die passendere und nutzerfreundlichere Wahl, als einen generischen Text wie `alt="Mitarbeiter im Meeting"` zu verfassen.

#### Eine Alternative: CSS-Hintergrundbilder

Wenn ein Bild wirklich und zu 100 % dekorativ ist, solltest du auch überlegen, ob es nicht besser als CSS-Hintergrundbild (`background-image`) eingebunden werden kann. Bilder, die über CSS eingefügt werden, sind für assistive Technologien per Definition unsichtbar. Sie existieren nicht im semantischen Dokumentenbaum (DOM) und werden von Screenreadern von vornherein ignoriert.

Die Verwendung von `background-image` ist oft die sauberste Methode für reine Dekoration wie Hintergrundmuster oder visuelle Texturen. Das hält dein HTML schlank und semantisch korrekt, da es sich nur auf den Inhalt konzentriert, während das CSS für die Präsentation zuständig ist.

Die bewusste Entscheidung für `alt=""` bei `<img>`-Tags ist ein Zeichen von Professionalität. Sie zeigt, dass du nicht nur blind Regeln befolgst, sondern den Zweck hinter der Barrierefreiheit verstanden hast: eine möglichst klare und störungsfreie Erfahrung für alle Nutzer zu schaffen. Manchmal ist Schweigen eben Gold.
