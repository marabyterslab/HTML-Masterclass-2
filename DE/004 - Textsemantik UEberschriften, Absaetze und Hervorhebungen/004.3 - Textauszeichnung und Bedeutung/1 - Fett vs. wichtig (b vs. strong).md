# Fett vs. wichtig (b vs. strong)

### Fett vs. Wichtig: Der feine Unterschied zwischen `<b>` und `<strong>`

Wenn du beginnst, dich mit der Auszeichnung von Text in HTML zu beschäftigen, stößt du unweigerlich auf zwei Elemente, die auf den ersten Blick exakt dasselbe tun: `<b>` und `<strong>`. Beide sorgen in den allermeisten Browsern standardmäßig dafür, dass der umschlossene Text fett dargestellt wird. Das führt oft zur Frage: Welches soll ich verwenden? Gibt es überhaupt einen Unterschied?

Die kurze Antwort lautet: Ja, es gibt einen gewaltigen Unterschied. Und dieser Unterschied liegt nicht im Visuellen, sondern in der Bedeutung – der Semantik. Das ist eine der wichtigsten Lektionen in modernem HTML: Es geht nicht nur darum, wie etwas aussieht, sondern darum, was es *bedeutet*.

Stell dir vor, du liest jemandem einen Text vor. Wenn du auf ein Wort triffst, das du betonen möchtest, weil es eine entscheidende Warnung oder eine zentrale Information enthält, würdest du deine Stimme erheben. Du würdest es ernster und lauter aussprechen. Wenn du hingegen einfach nur einen Eigennamen oder ein Stichwort hervorheben möchtest, damit es dem Zuhörer im Redefluss leichter auffällt, würdest du vielleicht nur den Tonfall leicht ändern, ohne ihm mehr Gewicht zu verleihen. Genau diese Unterscheidung treffen wir in HTML mit `<strong>` und `<b>`.

#### `<strong>`: Wenn etwas wirklich wichtig ist

Das `<strong>`-Element ist für Inhalte gedacht, die eine „starke Wichtigkeit, Ernsthaftigkeit oder Dringlichkeit“ haben. Das ist die offizielle Definition, und sie trifft den Nagel auf den Kopf. Wenn du `<strong>` verwendest, sagst du nicht nur dem Browser „mach das fett“, sondern du gibst ihm und anderen Systemen eine tiefere Information.

Denk an folgende Systeme, die deine Webseite interpretieren:

1.  **Screenreader:** Ein Screenreader ist eine Software, die blinden oder sehbehinderten Menschen den Inhalt einer Webseite vorliest. Wenn ein Screenreader auf ein `<strong>`-Element stößt, ändert er die Betonung. Er liest den Text mit einer stärkeren, ernsteren Stimme vor, genau wie du es in einem Gespräch tun würdest. Damit wird die inhaltliche Wichtigkeit für alle Nutzer zugänglich gemacht, unabhängig von ihrer Sehkraft.
2.  **Suchmaschinen:** Suchmaschinen wie Google durchsuchen deine Webseite, um ihren Inhalt zu verstehen und zu indexieren. Wenn sie ein `<strong>`-Element sehen, interpretieren sie den darin enthaltenen Text als besonders relevant für den umgebenden Kontext. Das kann (wenn auch nur geringfügig) dabei helfen, die Relevanz deiner Seite für bestimmte Suchbegriffe zu signalisieren. Du sagst der Suchmaschine: „Hey, dieser Teil hier ist von zentraler Bedeutung.“
3.  **Andere Maschinen und zukünftige Technologien:** Das Web entwickelt sich ständig weiter. Vielleicht wird es in Zukunft Geräte oder Anwendungen geben, die Texte zusammenfassen oder Inhalte auf neue Weise aufbereiten. Ein semantisch korrekt ausgezeichneter Text gibt diesen Systemen die nötigen Hinweise, um den Inhalt richtig zu interpretieren.

**Wann verwendest du `<strong>`?**

Verwende `<strong>` immer dann, wenn der Inhalt ohne diese besondere Betonung an Bedeutung verlieren oder missverstanden werden könnte.

Ein klassisches Beispiel ist eine Warnung:

```html
<p><strong>Achtung:</strong> Berühren Sie auf keinen Fall den roten Knopf, während die Maschine läuft.</p>
```

Hier ist das Wort „Achtung“ von entscheidender Wichtigkeit. Es signalisiert Dringlichkeit und Ernsthaftigkeit. Würde man es nur normal lesen, ginge die alarmierende Natur der Botschaft verloren.

Ein weiteres Beispiel ist die Hervorhebung eines zentralen Punktes in einem Satz:

```html
<p>Um ein guter Programmierer zu werden, ist <strong>kontinuierliches Üben</strong> der absolute Schlüssel zum Erfolg.</p>
```

Hier ist „kontinuierliches Üben“ der wichtigste Teil der Aussage. Der Satz funktioniert auch ohne die Betonung, aber die Hervorhebung unterstreicht die Kernbotschaft.

#### `<b>`: Wenn etwas nur auffallen soll

Das `<b>`-Element hat eine bewegte Geschichte. Ursprünglich stand es schlicht für „bold“ (fett). Es war ein rein präsentationsbezogenes Element, das sagte: „Stelle diesen Text fett dar.“ In der modernen HTML-Welt, in der wir versuchen, Inhalt und Darstellung strikt zu trennen, hat ein solches Element eigentlich keinen Platz mehr.

Deshalb wurde seine Bedeutung neu definiert. Das `<b>`-Element (offiziell für „Bring Attention To“) dient heute dazu, Text stilistisch vom Rest abzuheben, ohne ihm eine besondere Wichtigkeit oder eine andere semantische Betonung zu verleihen. Es ist eine Art letzter Ausweg, wenn kein anderes Element wie `<em>` (Betonung), `<i>` (anderer Tonfall) oder eben `<strong>` (Wichtigkeit) passt.

Du verwendest `<b>`, um die Aufmerksamkeit des Lesers auf bestimmte Wörter oder Sätze zu lenken, deren Inhalt aber nicht wichtiger ist als der Rest.

**Wann verwendest du `<b>`?**

Gute Anwendungsfälle sind zum Beispiel:

*   **Produktnamen** in einem Testbericht:

    ```html
    <p>Das neue <b>SuperPhone 12</b> überzeugt mit einer verbesserten Kamera und längerer Akkulaufzeit.</p>
    ```

    Der Produktname „SuperPhone 12“ ist nicht *wichtiger* als der Rest des Satzes, aber ihn hervorzuheben, hilft dem Leser, den Text schneller zu überfliegen und die relevanten Begriffe zu erfassen.

*   **Schlüsselwörter** in einem abstrakten Text oder einer Anleitung:

    ```html
    <p>Die Funktion `getElementById` ist eine zentrale Methode im <b>Document Object Model (DOM)</b>, um auf HTML-Elemente zuzugreifen.</p>
    ```

    „Document Object Model (DOM)“ ist hier ein Fachbegriff. Ihn optisch abzuheben, ist nützlich für die Lesbarkeit, aber es macht den Begriff nicht ernster oder dringlicher.

*   **Einleitende Sätze** eines Artikels, die in einer Übersicht fett dargestellt werden:

    ```html
    <article>
      <h3>Neues Update für unsere Software</h3>
      <p><b>In dieser Woche veröffentlichen wir das bisher größte Update für unser Tool.</b> Es enthält zahlreiche neue Funktionen, Fehlerbehebungen und eine komplett überarbeitete Benutzeroberfläche.</p>
    </article>
    ```

In all diesen Fällen würde ein Screenreader den Text im `<b>`-Tag nicht anders betonen. Er liest ihn mit normaler Stimme vor, da ihm keine semantische Information über eine besondere Wichtigkeit mitgegeben wurde.

#### Die Macht von CSS: Warum Aussehen nicht alles ist

Der vielleicht überzeugendste Grund, zwischen `<b>` und `<strong>` zu unterscheiden, ist die Trennung von Struktur (HTML) und Präsentation (CSS). Dass beide Tags standardmäßig fett dargestellt werden, ist nur eine Konvention der Browser-Hersteller. Du kannst dieses Verhalten jederzeit mit CSS ändern.

Stell dir vor, du entscheidest später, dass wichtige Warnungen auf deiner Seite nicht fett, sondern rot und unterstrichen sein sollen, um noch mehr aufzufallen. Wenn du semantisch korrekt `<strong>` verwendet hast, ist das eine einzige Zeile CSS:

```css
strong {
  font-weight: normal; /* Das standardmäßige Fett entfernen */
  color: red;
  text-decoration: underline;
}
```

Alle deine wichtigen Texte auf der gesamten Webseite ändern sich nun automatisch. Hättest du stattdessen `<b>` für alles verwendet, müsstest du mühsam an jeder einzelnen Stelle prüfen, ob es sich um eine echte Warnung oder nur um ein hervorgehobenes Schlüsselwort handelt.

Du könntest sogar das genaue Gegenteil tun und das Aussehen von `<b>` und `<strong>` vertauschen, auch wenn das nicht besonders sinnvoll wäre:

```html
<p>
  Dieser Text ist <strong>wichtig</strong>, aber wir stellen ihn kursiv dar.
</p>
<p>
  Dieser Text ist <b>nur hervorgehoben</b>, aber wir stellen ihn fett und rot dar.
</p>
```

```css
strong {
  font-style: italic;
  font-weight: normal; /* Standard-Fett überschreiben */
}

b {
  font-weight: bold;
  color: red;
}
```

Dieses Beispiel zeigt eindrücklich: Die Bedeutung eines Elements (definiert in HTML) und sein Aussehen (definiert in CSS) sind zwei völlig unabhängige Dinge. Deine Aufgabe als Entwickler ist es, dem Inhalt in HTML die korrekte Bedeutung zu geben. Die Aufgabe des Designers ist es dann, dieser Bedeutung über CSS ein passendes Aussehen zu verleihen.

#### Die goldene Regel zur Entscheidung

Wenn du das nächste Mal vor der Wahl zwischen `<b>` und `<strong>` stehst, stelle dir eine einfache Frage:

**„Würde sich die Bedeutung des Satzes ändern oder würde ein entscheidender Punkt verloren gehen, wenn dieser Text nicht besonders betont wird?“**

*   **Ja?** Dann verwende `<strong>`. Es geht um inhaltliche Wichtigkeit.
*   **Nein?** Dann ist es eine rein stilistische Hervorhebung. Prüfe, ob es einen besseren Tag gibt. Wenn nicht, ist `<b>` eine akzeptable Wahl.

Es gibt noch eine dritte Option für rein dekorative Zwecke: das `<span>`-Element mit einer CSS-Klasse. Wenn du Text nur hervorheben willst, weil es dem Design dient (z. B. jedes dritte Wort in einer Überschrift fett machen), wäre das der sauberste Weg:

```html
<p>Willkommen in <span class="brand-highlight">unserem Shop</span>!</p>
```

```css
.brand-highlight {
  font-weight: bold;
}
```

Dies ist semantisch völlig neutral und überlässt die gesamte Gestaltung CSS, was oft die beste Vorgehensweise ist.

Die Unterscheidung zwischen `<b>` und `<strong>` ist also mehr als nur eine akademische Spitzfindigkeit. Sie ist ein zentraler Baustein für barrierefreie, suchmaschinenfreundliche und zukunftssichere Webseiten. Indem du die Semantik der Elemente respektierst, baust du ein robusteres und verständlicheres Web – für Menschen und Maschinen gleichermaßen.
