# Ungeordnete Listen (ul)

### Ungeordnete Listen (ul)

Stell dir vor, du schreibst eine Einkaufsliste: Milch, Eier, Brot, Butter. Spielt es eine Rolle, in welcher Reihenfolge du diese Dinge aufschreibst oder später in den Einkaufswagen legst? In den meisten Fällen nicht. Das Wichtigste ist, dass du am Ende alles hast. Genau für solche Fälle, in denen die Reihenfolge der Elemente keine Rolle spielt, wurde in HTML die ungeordnete Liste geschaffen.

Das `<ul>`-Element, eine Abkürzung für „Unordered List“, ist der Container, der eine Sammlung von Listeneinträgen umschließt, bei denen die Sequenz irrelevant ist. Es signalisiert dem Browser und assistiven Technologien wie Screenreadern: „Achtung, hier folgt eine Aufzählung von zusammengehörigen Punkten, deren Anordnung aber nicht von Bedeutung ist.“

#### Die grundlegende Struktur

Eine ungeordnete Liste besteht immer aus zwei Arten von Tags, die untrennbar zusammengehören:

1.  **Das `<ul>`-Tag:** Dieses Element umschließt die gesamte Liste. Es definiert Anfang und Ende der Aufzählung.
2.  **Das `<li>`-Tag:** Jedes einzelne Element innerhalb der Liste wird von einem `<li>`-Tag (für „List Item“) umschlossen.

Ein einfaches, aber klares Beispiel ist eine Liste von Früchten:

```html
<ul>
  <li>Äpfel</li>
  <li>Bananen</li>
  <li>Orangen</li>
  <li>Erdbeeren</li>
</ul>
```

Wenn du diesen Code in einem Browser anzeigst, wirst du feststellen, dass er die Liste standardmäßig mit Aufzählungspunkten (meist ausgefüllten Kreisen) darstellt. Das ist die visuelle Konvention für eine ungeordnete Liste. Jeder `<li>`-Eintrag erzeugt dabei eine neue Zeile mit einem vorangestellten Punkt.

Die goldene Regel hierbei ist: Direkte Kinder eines `<ul>`-Elements dürfen ausschließlich `<li>`-Elemente sein. Du kannst nicht einfach einen Absatz (`<p>`) oder eine Überschrift (`<h2>`) direkt in ein `<ul>`-Tag einfügen. Das wäre semantisch falsch und würde gegen die HTML-Spezifikation verstoßen.

```html
<!-- FALSCH: Ein <p>-Tag darf nicht direkt in einer <ul> sein -->
<ul>
  <p>Hier sind meine Lieblingsobstsorten:</p>
  <li>Äpfel</li>
  <li>Bananen</li>
</ul>

<!-- KORREKT: Der Text gehört außerhalb oder in ein <li>-Element -->
<p>Hier sind meine Lieblingsobstsorten:</p>
<ul>
  <li>Äpfel</li>
  <li>Bananen</li>
</ul>
```

#### Semantik vor Aussehen

Es ist verlockend, das `<ul>`-Element nur wegen der Aufzählungspunkte und der Einrückung zu verwenden. Doch das widerspricht dem Grundprinzip der semantischen Auszeichnung. HTML dient dazu, die *Bedeutung* und *Struktur* deiner Inhalte zu beschreiben, nicht deren Aussehen.

Wenn du eine Liste von Produktmerkmalen hast, ist `<ul>` perfekt:

*   Lange Akkulaufzeit
*   Wasserabweisendes Gehäuse
*   Hochauflösendes Display

Hier ist die Reihenfolge der Merkmale austauschbar. Die Aussage bleibt dieselbe. Wenn du jedoch nur einen Textblock einrücken möchtest, ohne dass es sich um eine Liste handelt, solltest du dafür CSS verwenden (zum Beispiel mit `padding` oder `margin`). Der Missbrauch von Listenelementen für rein visuelle Effekte schadet der Barrierefreiheit und der Maschinenlesbarkeit deiner Webseite. Ein Screenreader würde einen eingerückten Absatz fälschlicherweise als „Liste mit einem Eintrag“ vorlesen, was für den Nutzer verwirrend wäre.

Das Aussehen der Aufzählungspunkte kannst du übrigens vollständig mit CSS steuern. Die Eigenschaft `list-style-type` erlaubt es dir, die Standardpunkte durch Kreise (`circle`), Quadrate (`square`) oder sogar eigene Bilder zu ersetzen. Du kannst sie auch komplett entfernen (`none`), was besonders bei Navigationsmenüs häufig genutzt wird.

```css
/* Ändert die Aufzählungspunkte in Quadrate */
ul {
  list-style-type: square;
}

/* Entfernt die Aufzählungspunkte komplett */
ul.navigation {
  list-style-type: none;
}
```

Diese Trennung von Struktur (HTML) und Präsentation (CSS) ist ein zentrales Konzept im Webdesign.

#### Verschachtelte Listen

Was aber, wenn deine Liste mehr Struktur benötigt? Stell dir vor, du möchtest deine Einkaufsliste nach Kategorien ordnen. Ungeordnete Listen können problemlos ineinander verschachtelt werden, um Hierarchien abzubilden.

Der Trick dabei ist, dass eine neue Liste (`<ul>`) immer *innerhalb* eines `<li>`-Elements der übergeordneten Liste platziert werden muss. Sie wird also zu einem Teil dieses Listeneintrags.

Sehen wir uns ein Beispiel an, das eine Einkaufsliste in die Kategorien „Obst“ und „Milchprodukte“ unterteilt:

```html
<ul>
  <li>
    Obst
    <ul>
      <li>Äpfel</li>
      <li>Bananen</li>
      <li>Trauben</li>
    </ul>
  </li>
  <li>
    Milchprodukte
    <ul>
      <li>Milch</li>
      <li>Käse</li>
      <li>Joghurt</li>
    </ul>
  </li>
  <li>Brot</li>
</ul>
```

In diesem Code siehst du, dass die Listen für die Unterkategorien nicht einfach irgendwo in der Hauptliste stehen. Die Liste mit Äpfeln, Bananen und Trauben ist ein Kind des `<li>`-Elements, das „Obst“ enthält. Dadurch entsteht eine klare Baumstruktur.

Browser visualisieren diese Verschachtelung typischerweise durch eine weitere Einrückung und oft auch durch eine Änderung des Aufzählungspunkts (z. B. von einem ausgefüllten Kreis zu einem unausgefüllten Kreis oder einem Quadrat). Dies macht die hierarchische Beziehung sofort visuell erkennbar.

#### Der häufigste Anwendungsfall: Navigationsmenüs

Einer der verbreitetsten und wichtigsten Anwendungsfälle für ungeordnete Listen hat auf den ersten Blick gar nichts mit klassischen Aufzählungen zu tun: Navigationsmenüs.

Eine Sammlung von Links, die dich zu verschiedenen Teilen einer Webseite führt, ist semantisch nichts anderes als eine Liste von Navigationspunkten. Die Reihenfolge ist hier zwar oft bewusst gewählt, aber nicht streng sequenziell im Sinne einer Schritt-für-Schritt-Anleitung. Daher ist `<ul>` die perfekte Wahl.

Eine typische Navigationsleiste im HTML-Code sieht so aus:

```html
<nav>
  <ul>
    <li><a href="/startseite">Startseite</a></li>
    <li><a href="/ueber-uns">Über uns</a></li>
    <li><a href="/produkte">Produkte</a></li>
    <li><a href="/kontakt">Kontakt</a></li>
  </ul>
</nav>
```

Die `<a>`-Tags (Anker-Tags für die Links) werden einfach in die `<li>`-Elemente gepackt. Mit CSS werden dann die Aufzählungspunkte entfernt (`list-style-type: none;`), die Listeneinträge nebeneinander angeordnet (`display: flex;`) und ansprechend gestaltet. Auch hier zeigt sich die Stärke der semantischen Auszeichnung: Für einen sehenden Benutzer ist es eine horizontale Leiste, für einen Screenreader oder eine Suchmaschine bleibt es eine klar strukturierte Liste von Links – perfekt für die Zugänglichkeit und die Indexierung.

Zusammenfassend lässt sich sagen, dass die ungeordnete Liste ein fundamentales und vielseitiges Werkzeug in deinem HTML-Repertoire ist. Sie wird immer dann eingesetzt, wenn du eine Gruppe zusammengehöriger Elemente präsentieren möchtest, deren interne Reihenfolge für das Verständnis nicht entscheidend ist. Von einfachen Stichpunktlisten über Produktmerkmale bis hin zu komplexen, verschachtelten Navigationsstrukturen – das `<ul>`-Element bietet die semantisch korrekte Grundlage.
