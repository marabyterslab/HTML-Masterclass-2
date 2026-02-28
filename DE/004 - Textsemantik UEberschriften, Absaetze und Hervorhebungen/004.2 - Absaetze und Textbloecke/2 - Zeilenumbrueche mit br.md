# Zeilenumbrüche mit br

### Zeilenumbrüche mit `br`

In der Welt des Texts gibt es Momente, in denen du eine Zeile beenden und in der nächsten weiterschreiben möchtest, ohne dabei einen komplett neuen Absatz zu beginnen. Stell dir ein Gedicht oder eine Postanschrift vor. Die Zeilenumbrüche sind hier kein gestalterisches Mittel, sondern ein wesentlicher Teil des Inhalts selbst. Genau für diesen Zweck stellt dir HTML das `<br>`-Element zur Verfügung.

Das Kürzel `br` steht für "break" (Umbruch). Es ist eines der einfachsten Elemente in HTML, doch sein korrekter Einsatz ist ein Zeichen für sauberes und semantisch korrektes Handwerk.

#### Was ist das `<br>`-Element?

Das `<br>`-Tag ist ein sogenanntes leeres oder "void" Element. Das bedeutet, es hat keinen Inhalt und benötigt daher auch kein schließendes Tag. Du schreibst einfach `<br>`, um an einer bestimmten Stelle im Text einen Zeilenumbruch zu erzwingen.

Ein klassisches Beispiel ist die Formatierung einer Adresse:

```html
<p>
  Max Mustermann<br>
  Musterstraße 123<br>
  12345 Musterstadt
</p>
```

Ohne die `<br>`-Tags würde der Browser den gesamten Text als eine einzige, durchgehende Zeile darstellen, da er die Zeilenumbrüche im HTML-Quellcode ignoriert:

> Max Mustermann Musterstraße 123 12345 Musterstadt

Mit den `<br>`-Elementen erhältst du jedoch die gewünschte, strukturierte Darstellung:

> Max Mustermann
> Musterstraße 123
> 12345 Musterstadt

Hier siehst du den fundamentalen Zweck des `<br>`-Elements: Es fügt einen Zeilenumbruch ein, wo dieser eine inhaltliche Bedeutung hat. Die Adresse ist *ein* zusammenhängender Informationsblock (daher in einem einzigen `<p>`-Element), aber die einzelnen Teile gehören aus logischen Gründen in separate Zeilen.

#### Der semantisch korrekte Einsatz

Die wichtigste Regel, die du dir im Umgang mit `<br>` merken solltest, lautet: **Verwende `<br>` nur für Zeilenumbrüche, die Teil des Inhalts sind, nicht zur visuellen Gestaltung.**

Wann ist ein Zeilenumbruch Teil des Inhalts?

1.  **Gedichte und Liedtexte:** Die Gliederung in Verse ist entscheidend für Rhythmus, Reim und Bedeutung. Ein Gedicht ohne seine Zeilenumbrüche ist kein Gedicht mehr.

    ```html
    <p>
      Zwei Wege boten sich im gelben Walde dar,<br>
      und leider konnt ich nicht beide gehn,<br>
      ein einzger Wandrer, lange stand ich da<br>
      und schaute einen an, so weit ich nur konnt sehn...
    </p>
    ```

2.  **Adressen:** Wie im ersten Beispiel gezeigt, ist die Unterteilung einer Adresse in Zeilen eine Konvention, die ihre Lesbarkeit und logische Gliederung sicherstellt.

3.  **Signaturen in E-Mails oder Briefen:** Auch hier sind die Zeilenumbrüche oft ein fester Bestandteil der Struktur.

    ```html
    <p>
      Mit freundlichen Grüßen,<br>
      Dein Web-Entwickler-Team
    </p>
    ```

In all diesen Fällen würde das Entfernen des Zeilenumbruchs die Bedeutung oder die korrekte Interpretation des Inhalts verändern. Der Umbruch ist nicht nur Kosmetik, sondern Information.

#### Der häufigste Fehler: `<br>` als Abstandshalter

Nun kommen wir zu dem Punkt, an dem die meisten Anfänger `<br>` missbrauchen: zur Erzeugung von vertikalem Abstand. Du möchtest etwas mehr Luft zwischen zwei Absätzen oder einem Bild und dem folgenden Text? Es ist verlockend, einfach ein oder zwei `<br>`-Tags einzufügen.

```html
<!-- FALSCH! Dies ist semantisch inkorrekt und schlechter Stil. -->
<p>Dies ist der erste Absatz.</p>
<br>
<br>
<p>Dies ist der zweite Absatz, der weiter unten stehen soll.</p>
```

Warum ist das ein Problem?

1.  **Es verletzt die Trennung von Inhalt und Präsentation:** HTML ist für die Struktur und die semantische Bedeutung deines Inhalts zuständig. CSS ist für das Aussehen, also die Präsentation, verantwortlich. Der Abstand zwischen Elementen ist eine rein visuelle Eigenschaft. Indem du `<br>` zur Gestaltung verwendest, vermischst du diese beiden Verantwortlichkeiten. Dein HTML wird unsauber und schwerer zu warten.

2.  **Es ist unflexibel:** Was passiert, wenn du dich entscheidest, dass der Abstand zwischen den Absätzen größer oder kleiner sein soll? Bei der `<br>`-Methode müsstest du jede einzelne Stelle in deinem HTML-Code aufsuchen und `<br>`-Tags hinzufügen oder entfernen. Das ist ineffizient und fehleranfällig. Mit CSS änderst du eine einzige Zeile in deiner Stylesheet-Datei, und die Änderung wird auf der gesamten Website konsistent angewendet.

3.  **Es schadet der Barrierefreiheit:** Screenreader, die blinden oder sehbehinderten Menschen Webseiten vorlesen, interpretieren ein `<br>` als Zeilenumbruch. Mehrere `<br>` hintereinander können als "Leerzeile, Leerzeile" vorgelesen werden, was den Lesefluss stört und für Verwirrung sorgt. Der zusätzliche Abstand hat keine semantische Bedeutung und sollte daher für assistierende Technologien unsichtbar sein.

**Die richtige Lösung: CSS nutzen**

Der korrekte Weg, um Abstände zwischen Elementen zu erzeugen, ist die Verwendung der CSS-Eigenschaften `margin` oder `padding`. Um den Abstand zwischen zwei Absätzen zu vergrößern, würdest du den unteren Außenabstand (`margin-bottom`) des ersten Absatzes oder den oberen Außenabstand (`margin-top`) des zweiten Absatzes definieren.

Hier ist der korrekte Code für das obige Beispiel:

**HTML (sauber und semantisch):**

```html
<p>Dies ist der erste Absatz.</p>
<p>Dies ist der zweite Absatz.</p>
```

**CSS (verantwortlich für das Aussehen):**

```css
p {
  margin-bottom: 2em; /* Fügt einen Abstand unter jedem Absatz hinzu */
}
```

Mit diesem Ansatz bleibt dein HTML rein strukturell. Die gesamte visuelle Gestaltung wird zentral und flexibel in deinem CSS gesteuert.

#### Abgrenzung zum `<p>`-Element

Ein weiterer wichtiger Punkt ist die Unterscheidung zwischen einem `<br>` und dem Beginn eines neuen `<p>`-Elements. Ein `<p>`-Tag umschließt einen thematisch zusammenhängenden Textblock – einen Paragraphen. Wenn du einen neuen Gedanken oder ein neues Thema beginnst, verwendest du ein neues `<p>`-Element. Browser fügen zwischen zwei `<p>`-Elementen standardmäßig einen visuellen Abstand ein, um diese thematische Trennung zu verdeutlichen.

Ein `<br>` hingegen erzeugt nur einen Zeilenumbruch *innerhalb* eines bestehenden Textblocks. Es signalisiert keine thematische Trennung.

Vergleiche die beiden Beispiele:

**Verwendung von `<br>` in einem Absatz:**

```html
<p>
  Die Sonne ging langsam unter.<br>
  Der Himmel färbte sich rot.
</p>
```

Hier handelt es sich um zwei eng zusammengehörige Sätze, die denselben Moment beschreiben. Das `<br>` erzeugt lediglich einen poetischen oder stilistischen Umbruch innerhalb desselben Gedankenblocks.

**Verwendung von zwei separaten Absätzen:**

```html
<p>Die Sonne ging langsam unter. Der Himmel färbte sich rot und die Vögel verstummten allmählich.</p>
<p>In der Ferne heulte ein Wolf. Die Nacht begann, ihre Herrschaft über das Land auszubreiten.</p>
```

Hier haben wir zwei unterschiedliche Absätze. Der erste beschreibt den Sonnenuntergang, der zweite leitet zur Nacht über und führt ein neues Element (den Wolf) ein. Die Verwendung von zwei `<p>`-Elementen ist hier semantisch korrekt, da eine thematische Zäsur stattfindet.

Zusammenfassend lässt sich sagen: Das `<br>`-Element ist ein kleines, aber feines Werkzeug in deinem HTML-Kasten. Nutze es mit Bedacht und nur dann, wenn der Zeilenumbruch eine inhaltliche Notwendigkeit darstellt. Für alles, was die visuelle Gestaltung und die Abstände betrifft, ist CSS dein verlässlicher Partner. Diese saubere Trennung ist ein Grundpfeiler professioneller Webentwicklung.
