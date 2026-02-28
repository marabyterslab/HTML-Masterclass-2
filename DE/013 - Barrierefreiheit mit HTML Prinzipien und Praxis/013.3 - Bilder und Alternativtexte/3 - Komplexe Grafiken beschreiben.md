# Komplexe Grafiken beschreiben

### Komplexe Grafiken beschreiben: Wenn `alt` nicht ausreicht

Du weißt inzwischen, wie wichtig der `alt`-Text für Bilder ist. Für ein Logo, ein Foto oder ein einfaches Icon ist eine kurze, prägnante Beschreibung im `alt`-Attribut oft völlig ausreichend. Doch was machst du, wenn das Bild nicht nur dekorativ ist, sondern komplexe Informationen enthält? Stell dir ein Balkendiagramm vor, das die Umsatzzahlen der letzten vier Quartale zeigt, eine Infografik, die den Wasserkreislauf erklärt, oder einen Organisationsplan deines Unternehmens.

Ein `alt="Balkendiagramm der Quartalsumsätze"` wäre hier zwar technisch korrekt, aber für eine Person, die auf einen Screenreader angewiesen ist, vollkommen nutzlos. Die entscheidende Information – die eigentlichen Daten, die Trends, die Kernaussage der Grafik – geht komplett verloren. Hier stoßen wir an die Grenzen des `alt`-Attributs, das bewusst für kurze Beschreibungen konzipiert wurde. Für komplexe Grafiken brauchen wir robustere Methoden.

Das Grundprinzip lautet: Stelle sicher, dass die Informationen und die Funktion der Grafik für alle Nutzer gleichermaßen zugänglich sind. Es geht nicht darum, das visuelle Erscheinungsbild pixelgenau zu beschreiben („ein blauer Balken, der bis zur 50er-Marke reicht“), sondern darum, die darin enthaltenen Daten und die Schlussfolgerung, die sich daraus ergibt, zu vermitteln.

Glücklicherweise bietet uns HTML mehrere ausgezeichnete Wege, um diese Herausforderung zu meistern.

#### Methode 1: Die Beschreibung im Fließtext

Die einfachste und oft effektivste Methode ist, die Informationen der Grafik direkt im umgebenden Text bereitzustellen. Die Grafik dient dann als visuelle Unterstützung für den Text, der die volle Erklärung enthält.

In diesem Fall wird der `alt`-Text zu einer Art Brücke. Er identifiziert die Grafik und verweist auf die Beschreibung im Text.

Stell dir vor, du hast folgendes Balkendiagramm auf deiner Seite:

```html
<h2>Umsatzentwicklung im letzten Geschäftsjahr</h2>

<p>Das vergangene Jahr zeigte eine positive Entwicklung unserer Umsätze. 
Nach einem soliden Start im ersten Quartal konnten wir in den darauffolgenden 
Quartalen eine stetige Steigerung verzeichnen, die im vierten Quartal ihren 
Höhepunkt erreichte.</p>

<img src="quartalsumsatz.png" 
     alt="Balkendiagramm der Quartalsumsätze. Die genauen Daten sind im folgenden Absatz aufgeführt.">

<p>Die detaillierten Umsatzzahlen pro Quartal:
   - Q1: 45.000 €
   - Q2: 52.000 €
   - Q3: 61.000 €
   - Q4: 75.000 €
</p>
```

Dieser Ansatz ist genial in seiner Einfachheit und Robustheit:
1.  **Universell zugänglich:** Die Information ist für absolut jeden sichtbar und lesbar, unabhängig von irgendwelchen Hilfstechnologien.
2.  **SEO-freundlich:** Suchmaschinen können den Textinhalt problemlos indizieren und verstehen den Kontext der Grafik.
3.  **Wartungsfreundlich:** Die Daten sind direkt im HTML-Inhalt und leicht zu aktualisieren.

#### Methode 2: Semantische Gruppierung mit `<figure>` und `<figcaption>`

HTML5 hat uns die Elemente `<figure>` und `<figcaption>` geschenkt, die wie für diesen Zweck gemacht sind. Ein `<figure>`-Element repräsentiert eine in sich geschlossene Inhaltseinheit, die oft aus einem Bild, Diagramm, Code-Schnipsel oder Ähnlichem und einer dazugehörigen Beschriftung besteht. Die Beschriftung wird mit `<figcaption>` ausgezeichnet.

Diese Methode ist ideal, um eine Grafik und ihre Beschreibung semantisch miteinander zu verknüpfen.

```html
<figure>
  <img src="quartalsumsatz.png" 
       alt="Balkendiagramm, das einen stetigen Anstieg der Umsätze über vier Quartale zeigt.">
  <figcaption>
    Umsatzentwicklung im letzten Geschäftsjahr. Die Umsätze stiegen von 45.000 € in Q1 auf 75.000 € in Q4.
  </figcaption>
</figure>

<!-- Für noch detailliertere Daten kann die Beschreibung im Fließtext folgen -->
<p>Die genauen Zahlen im Detail: Q1: 45.000 €, Q2: 52.000 €, Q3: 61.000 €, Q4: 75.000 €.</p>
```

In diesem Beispiel hat der `alt`-Text eine etwas andere Rolle. Er beschreibt die Kernaussage und den Typ der Grafik. Die `<figcaption>` liefert eine für alle sichtbare Überschrift oder eine kurze Zusammenfassung. Die vollständigen Daten können immer noch im Fließtext oder, noch besser, direkt im Anschluss an die `<figure>` stehen.

Die Kombination aus `<figure>`, `<figcaption>` und einer textlichen Beschreibung ist eine semantisch saubere und sehr zugängliche Lösung.

#### Methode 3: Interaktive Beschreibungen mit `<details>` und `<summary>`

Manchmal ist die Beschreibung einer Grafik sehr lang – zum Beispiel eine vollständige Datentabelle für ein komplexes Diagramm. Diese permanent sichtbar zu halten, könnte das Layout der Seite überladen. Hier bieten die HTML-Elemente `<details>` und `<summary>` eine elegante, interaktive Lösung.

Das `<details>`-Element erzeugt einen ausklappbaren Bereich, der standardmäßig geschlossen ist. Der Inhalt des `<summary>`-Elements ist immer sichtbar und dient als Klick-Label, um den restlichen Inhalt ein- oder auszublenden.

```html
<figure>
  <img src="quartalsumsatz.png" 
       alt="Balkendiagramm der Quartalsumsätze. Details zu den Daten können unter der Grafik eingeblendet werden.">
  <figcaption>Umsatzentwicklung im letzten Geschäftsjahr.</figcaption>
</figure>

<details>
  <summary>Detaillierte Umsatzzahlen und Analyse anzeigen</summary>
  <div>
    <p>Die Grafik zeigt einen positiven Trend über das gesamte Geschäftsjahr. Hier sind die exakten Daten:</p>
    <table>
      <thead>
        <tr>
          <th>Quartal</th>
          <th>Umsatz</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Q1</td>
          <td>45.000 €</td>
        </tr>
        <tr>
          <td>Q2</td>
          <td>52.000 €</td>
        </tr>
        <tr>
          <td>Q3</td>
          <td>61.000 €</td>
        </tr>
        <tr>
          <td>Q4</td>
          <td>75.000 €</td>
        </tr>
      </tbody>
    </table>
    <p><strong>Analyse:</strong> Das Wachstum von Q1 zu Q4 beträgt über 66 %, was auf erfolgreiche Marketingmaßnahmen im zweiten Halbjahr zurückzuführen ist.</p>
  </div>
</details>
```

Diese Methode ist exzellent, weil sie:
*   **Platz spart:** Der Hauptinhalt der Seite bleibt übersichtlich.
*   **Wahlfreiheit bietet:** Nutzer können selbst entscheiden, ob sie die Details sehen möchten.
*   **Ohne JavaScript funktioniert:** Es ist eine native HTML-Lösung, die in allen modernen Browsern unterstützt wird.
*   **Barrierefrei ist:** Screenreader erkennen `<details>` und `<summary>` korrekt und können den Zustand (offen/geschlossen) ansagen und den Inhalt bei Bedarf vorlesen.

Für die Daten eines Diagramms ist eine HTML-Tabelle (`<table>`), wie im Beispiel gezeigt, die semantisch korrekteste und zugänglichste Form.

#### Ein Blick in die Vergangenheit: Das `longdesc`-Attribut

Vielleicht stößt du bei deiner Recherche oder in älterem Code auf das `longdesc`-Attribut. Die Idee dahinter war, eine URL zu einer separaten Seite anzugeben, die eine lange Beschreibung des Bildes enthält.

Beispiel (nicht zur Nachahmung empfohlen):
```html
<img src="diagramm.png" alt="Komplexes Diagramm" longdesc="diagramm-beschreibung.html">
```

Obwohl die Absicht gut war, hat sich `longdesc` in der Praxis nie wirklich durchgesetzt und gilt heute als veraltet. Die Gründe dafür sind einleuchtend:
*   **Mangelnde Unterstützung:** Die Browser- und Screenreader-Unterstützung war immer lückenhaft und unzuverlässig.
*   **Kein visueller Hinweis:** Sehende Nutzer ohne Hilfstechnologie hatten keine Ahnung, dass eine Langbeschreibung existiert. Dies verstößt gegen das Prinzip, allen Nutzern die gleichen Informationen zur Verfügung zu stellen.
*   **Schlechte User Experience:** Der Nutzer muss die aktuelle Seite verlassen, um die Beschreibung zu lesen, was den Lesefluss unterbricht.

Die modernen, oben vorgestellten Methoden sind dem `longdesc`-Attribut in jeder Hinsicht überlegen. Vermeide es daher in neuen Projekten.

#### Die Kunst der guten Beschreibung

Unabhängig von der gewählten technischen Methode kommt es auf die Qualität der Beschreibung selbst an. Hier sind ein paar Richtlinien:
1.  **Beginne mit der Kernaussage:** Was ist die wichtigste Botschaft, die die Grafik vermittelt? "Das Diagramm zeigt ein kontinuierliches Umsatzwachstum im Laufe des Jahres."
2.  **Liefere die Daten:** Gib die zugrundeliegenden Daten in einer strukturierten Form an. Listen oder Tabellen sind hierfür ideal.
3.  **Beschreibe die Struktur (falls relevant):** Bei einem Flussdiagramm beschreibst du die einzelnen Schritte, Verzweigungen und Entscheidungen. Bei einer Karte nennst du die wichtigen Orte und ihre Beziehungen zueinander.

Indem du diese Techniken anwendest, stellst du sicher, dass deine Inhalte nicht nur schön aussehen, sondern dass die darin enthaltenen Informationen wirklich für jeden zugänglich sind. Du machst das Web damit ein Stück besser und inklusiver.
