# Verschachtelung von Listen

### Verschachtelung von Listen: Struktur in der Struktur

Nachdem du nun die Grundlagen von geordneten und ungeordneten Listen kennst, gehen wir einen entscheidenden Schritt weiter. In der realen Welt sind Informationen selten flach und linear. Oft gibt es Hauptpunkte, die wiederum eigene Unterpunkte haben. Denk an das Inhaltsverzeichnis eines Buches, eine Einkaufsliste, die nach Abteilungen im Supermarkt sortiert ist, oder die Navigationsleiste einer komplexen Webseite. Um solche hierarchischen Strukturen in HTML abzubilden, nutzen wir die Verschachtelung von Listen.

Das Prinzip ist erstaunlich einfach, aber ungemein mächtig: Jedes Listenelement (`<li>`) ist ein Container, der nicht nur Text, sondern auch andere HTML-Elemente aufnehmen kann – einschließlich einer komplett neuen Liste.

#### Das Grundprinzip der Verschachtelung

Stell dir vor, du planst eine Reise und erstellst eine Packliste. Einige Punkte auf dieser Liste sind einfach, wie "Reisepass". Andere sind komplexer, wie "Kleidung", denn hier möchtest du genauer auflisten, was du einpacken musst. Genau das ist ein perfekter Anwendungsfall für eine verschachtelte Liste.

Die goldene Regel der Verschachtelung lautet: **Eine neue Liste (`<ul>` oder `<ol>`) wird immer *innerhalb* eines Listenelementes (`<li>`) der übergeordneten Liste platziert.**

Sieh dir dieses grundlegende Beispiel an. Wir erstellen eine ungeordnete Liste mit Reisezielen. Eines dieser Ziele, Italien, hat mehrere Städte, die wir besuchen wollen. Diese Städte bilden eine Unterliste.

```html
<ul>
  <li>Deutschland</li>
  <li>
    Italien
    <ul>
      <li>Rom</li>
      <li>Florenz</li>
      <li>Venedig</li>
    </ul>
  </li>
  <li>Frankreich</li>
</ul>
```

Analysieren wir diesen Code Schritt für Schritt:
1.  Wir beginnen mit einer normalen ungeordneten Liste (`<ul>`).
2.  Die ersten und letzten Hauptpunkte ("Deutschland" und "Frankreich") sind einfache `<li>`-Elemente.
3.  Das zweite `<li>`-Element für "Italien" ist besonders. Es enthält nicht nur den Text "Italien", sondern direkt danach, noch vor dem schließenden `</li>`-Tag, beginnt eine komplett neue `<ul>`.
4.  Diese innere Liste enthält die spezifischen Städte als eigene `<li>`-Elemente.
5.  Nachdem die innere Liste mit `</ul>` geschlossen wurde, wird auch das übergeordnete `<li>`-Element für "Italien" mit `</li>` geschlossen.

Im Browser wird dies standardmäßig so dargestellt, dass die innere Liste eingerückt ist und oft ein anderes Aufzählungszeichen verwendet (z. B. ein Kreis statt einer ausgefüllten Scheibe). Diese visuelle Darstellung signalisiert dem Betrachter sofort die hierarchische Beziehung. Die genaue Darstellung ist jedoch eine Sache des Browser-Standard-Stylesheets und kann mit CSS vollständig angepasst werden. Für uns in HTML zählt allein die korrekte semantische Struktur.

#### Typische Fehler, die du vermeiden solltest

Die korrekte Verschachtelung ist logisch, aber es gibt zwei häufige Fehler, die zu ungültigem HTML-Code und unerwartetem Verhalten führen.

**Fehler 1: Die verschachtelte Liste zwischen `<li>`-Elementen platzieren.**

```html
<!-- FALSCH! -->
<ul>
  <li>Hauptpunkt 1</li>
  <ul>
    <li>Unterpunkt 1.1</li>
    <li>Unterpunkt 1.2</li>
  </ul>
  <li>Hauptpunkt 2</li>
</ul>
```

Dieser Code ist semantisch falsch. Ein `<ul>`- oder `<ol>`-Element darf als direkte Kinder nur `<li>`-Elemente (und einige andere, seltenere Elemente) enthalten. Eine weitere Liste gehört nicht direkt dazwischen. Sie muss, wie oben gezeigt, Teil des Inhalts eines `<li>`-Elements sein.

**Fehler 2: Die verschachtelte Liste nach dem `<li>`-Element platzieren.**

```html
<!-- EBENFALLS FALSCH! -->
<ul>
  <li>Hauptpunkt 1</li>
  <li>Hauptpunkt 2</li>
  </ul>
  <ul>
    <li>Unterpunkt 2.1</li>
  </ul>
```

Auch das ist nicht korrekt, da hier einfach zwei separate Listen nacheinander stehen. Es besteht keine strukturelle Verbindung zwischen "Hauptpunkt 2" und "Unterpunkt 2.1". Die Verschachtelung erzeugt eine Eltern-Kind-Beziehung, die hier komplett fehlt.

Merke dir also: Die Unterliste ist immer eine Detaillierung oder ein Bestandteil des übergeordneten Listenelements und gehört daher logisch und syntaktisch *in* dieses Element hinein.

#### Kombination verschiedener Listentypen

Die wahre Flexibilität zeigt sich, wenn du beginnst, geordnete und ungeordnete Listen zu mischen. Das ermöglicht es dir, noch aussagekräftigere Strukturen zu bauen. Stell dir eine Anleitung vor: Die Hauptschritte sollten nummeriert sein (eine geordnete Liste), aber die für einen Schritt benötigten Materialien müssen nicht in einer bestimmten Reihenfolge abgearbeitet werden (eine ungeordnete Liste).

Hier ist ein Beispiel für ein einfaches Rezept:

```html
<h1>Rezept: Pfannkuchen</h1>
<ol>
  <li>
    Zutaten vorbereiten
    <ul>
      <li>250g Mehl</li>
      <li>2 Eier</li>
      <li>500ml Milch</li>
      <li>Eine Prise Salz</li>
    </ul>
  </li>
  <li>
    Teig anrühren
  </li>
  <li>
    In der Pfanne ausbacken
  </li>
</ol>
```

In diesem Code siehst du eine äußere geordnete Liste (`<ol>`), die die Hauptschritte des Rezepts darstellt. Der erste Schritt, "Zutaten vorbereiten", ist jedoch komplexer. Um die benötigten Zutaten übersichtlich darzustellen, fügen wir innerhalb des ersten `<li>`-Elements eine ungeordnete Liste (`<ul>`) ein.

Dieses Muster ist extrem nützlich und spiegelt wider, wie wir Informationen natürlich organisieren: eine geordnete Abfolge von Aktionen, bei der eine Aktion eine ungeordnete Sammlung von Dingen erfordert.

#### Mehrere Ebenen der Verschachtelung

Die Verschachtelung ist nicht auf eine einzige Ebene beschränkt. Du kannst Listen so tief verschachteln, wie es für deine Inhaltsstruktur sinnvoll ist. Ein klassisches Beispiel hierfür ist die Navigation einer großen Webseite.

```html
<ul>
  <li>
    Produkte
    <ul>
      <li>
        Software
        <ul>
          <li>Grafikdesign</li>
          <li>Videobearbeitung</li>
        </ul>
      </li>
      <li>
        Hardware
        <ul>
          <li>Laptops</li>
          <li>Monitore</li>
        </ul>
      </li>
    </ul>
  </li>
  <li>Über Uns</li>
  <li>Kontakt</li>
</ul>
```

Hier haben wir eine dreistufige Hierarchie:
1.  Die Hauptebene ("Produkte", "Über Uns", "Kontakt").
2.  Die zweite Ebene unter "Produkte" ("Software", "Hardware").
3.  Die dritte Ebene unter "Software" und "Hardware" mit den jeweiligen spezifischen Produktkategorien.

Jede neue `<ul>` ist korrekt in einem `<li>` der darüberliegenden Ebene platziert. Während dies technisch unbegrenzt möglich ist, solltest du aus Gründen der Benutzerfreundlichkeit und Übersichtlichkeit eine zu tiefe Verschachtelung vermeiden. Wenn deine Struktur mehr als drei oder vier Ebenen tief wird, ist das oft ein Zeichen dafür, dass die Informationsarchitektur möglicherweise zu kompliziert ist und vereinfacht werden sollte.

#### Die semantische Bedeutung und Barrierefreiheit

Warum ist diese syntaktische Strenge so wichtig? Weil sie eine klare, maschinenlesbare Bedeutung transportiert. Für einen sehenden Benutzer ist die Einrückung ein visueller Hinweis auf die Hierarchie. Für eine Maschine oder eine assistive Technologie wie einen Screenreader ist die korrekte HTML-Struktur der einzige Anhaltspunkt.

Ein Screenreader, der von blinden oder sehbehinderten Menschen genutzt wird, liest eine korrekt verschachtelte Liste so vor, dass die Struktur deutlich wird. Er könnte zum Beispiel ansagen: "Liste mit 3 Einträgen. Eintrag 1: Produkte. Hat eine verschachtelte Liste mit 2 Einträgen. Eintrag 1: Software. Hat eine verschachtelte Liste mit 2 Einträgen...". Diese Information ist entscheidend, um die Beziehung der Inhalte zueinander zu verstehen und effizient durch die Seite zu navigieren.

Würdest du versuchen, eine solche Struktur nur visuell mit Einrückungen (z. B. durch CSS oder Leerzeichen) zu fälschen, ginge diese gesamte semantische Information verloren. Für einen Screenreader wären es dann nur noch separate, unzusammenhängende Listen oder Absätze. Die korrekte Verschachtelung ist also ein fundamentaler Baustein für die Erstellung barrierefreier und zugänglicher Webseiten. Es ist ein perfektes Beispiel dafür, wie HTML nicht nur das Aussehen, sondern vor allem die Bedeutung und Struktur deiner Inhalte definiert.
