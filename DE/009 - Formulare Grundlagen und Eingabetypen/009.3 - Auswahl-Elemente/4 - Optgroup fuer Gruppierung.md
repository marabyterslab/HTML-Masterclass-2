# Optgroup für Gruppierung

### Ordnung im Drop-down: Listen mit `<optgroup>` strukturieren

Stell dir vor, du erstellst ein Formular, in dem der Benutzer sein Lieblingsauto aus einer langen Liste auswählen soll. Diese Liste enthält Modelle von verschiedenen Herstellern – Audi, BMW, Mercedes, Toyota, Honda, Ford, Chevrolet und so weiter. Wenn du all diese Optionen einfach als eine lange, flache Liste in einem `<select>`-Element anzeigtest, wäre das Ergebnis schnell unübersichtlich. Der Benutzer müsste die gesamte Liste durchsuchen, um sein gewünschtes Modell zu finden. Das ist nicht nur mühsam, sondern auch fehleranfällig.

Genau für dieses Problem bietet HTML eine elegante und semantisch korrekte Lösung: das `<optgroup>`-Element. Der Name steht für "Option Group" und beschreibt seine Funktion perfekt. Es erlaubt dir, zusammengehörige `<option>`-Elemente innerhalb einer Auswahlliste zu bündeln und ihnen eine gemeinsame Überschrift zu geben.

#### Die grundlegende Struktur

Das `<optgroup>`-Element ist ein Kind-Element des `<select>`-Tags und umschließt eine oder mehrere `<option>`-Tags. Die Magie geschieht durch ein einziges, aber dafür obligatorisches Attribut: `label`. Der Wert dieses `label`-Attributs wird vom Browser als nicht auswählbare Überschrift für die jeweilige Gruppe dargestellt.

Schauen wir uns das an einem einfachen Beispiel an. Wir möchten eine Auswahl an europäischen Städten anbieten, gruppiert nach Ländern.

```html
<label for="city-select">Wähle eine Stadt:</label>

<select name="cities" id="city-select">
  <optgroup label="Deutschland">
    <option value="berlin">Berlin</option>
    <option value="hamburg">Hamburg</option>
    <option value="muenchen">München</option>
  </optgroup>
  <optgroup label="Frankreich">
    <option value="paris">Paris</option>
    <option value="marseille">Marseille</option>
    <option value="lyon">Lyon</option>
  </optgroup>
  <optgroup label="Spanien">
    <option value="madrid">Madrid</option>
    <option value="barcelona">Barcelona</option>
    <option value="sevilla">Sevilla</option>
  </optgroup>
</select>
```

Wenn du diesen Code im Browser öffnest, siehst du ein Drop-down-Menü. Klickst du darauf, entfaltet sich die Liste, aber sie ist nicht mehr flach und unstrukturiert. Stattdessen siehst du die Überschriften "Deutschland", "Frankreich" und "Spanien". Diese Überschriften sind typischerweise fett gedruckt und leicht eingerückt. Du kannst sie nicht anklicken oder auswählen – sie dienen ausschließlich der visuellen und strukturellen Gliederung. Unter jeder Überschrift findest du die jeweiligen Städte, die ganz normal ausgewählt werden können.

Durch diese einfache Gruppierung hast du die Benutzerfreundlichkeit (Usability) deines Formulars erheblich verbessert. Benutzer können die Liste nun viel schneller überfliegen (scannen) und finden die für sie relevanten Optionen mit deutlich weniger kognitivem Aufwand.

#### Ein praktisches Anwendungsbeispiel: Fahrzeugauswahl

Kehren wir zu unserem ursprünglichen Beispiel mit den Automodellen zurück. Eine gut strukturierte Auswahlliste könnte hier den Unterschied zwischen einem zufriedenen und einem frustrierten Benutzer ausmachen.

```html
<label for="car-model">Wähle dein Fahrzeugmodell:</label>

<select name="car" id="car-model">
  <option value="">-- Bitte wählen --</option>
  
  <optgroup label="Deutsche Hersteller">
    <option value="audi-a4">Audi A4</option>
    <option value="bmw-3er">BMW 3er</option>
    <option value="mercedes-c-klasse">Mercedes-Benz C-Klasse</option>
    <option value="vw-golf">Volkswagen Golf</option>
  </optgroup>
  
  <optgroup label="Japanische Hersteller">
    <option value="toyota-corolla">Toyota Corolla</option>
    <option value="honda-civic">Honda Civic</option>
    <option value="mazda-3">Mazda 3</option>
  </optgroup>
  
  <optgroup label="US-Hersteller">
    <option value="ford-mustang">Ford Mustang</option>
    <option value="chevrolet-camaro">Chevrolet Camaro</option>
    <option value="tesla-model3">Tesla Model 3</option>
  </optgroup>
</select>
```

In diesem Code siehst du ein paar wichtige Aspekte:

1.  **Platzhalter-Option:** Die erste `<option>` mit einem leeren `value`-Attribut dient als Platzhalter. Sie ermutigt den Benutzer, eine bewusste Auswahl zu treffen. Da sie außerhalb jeder `<optgroup>` steht, erscheint sie ganz oben in der Liste.
2.  **Semantische Gruppierung:** Die Gruppen sind nicht willkürlich, sondern folgen einer klaren Logik (Herkunftsland des Herstellers). Dies schafft eine intuitive Struktur.
3.  **Klarheit:** Ein Benutzer, der einen Toyota sucht, weiß sofort, dass er im Abschnitt "Japanische Hersteller" nachsehen muss, und kann die anderen Gruppen ignorieren.

#### Das `disabled`-Attribut für ganze Gruppen

Manchmal möchtest du vielleicht eine ganze Gruppe von Optionen vorübergehend deaktivieren. Stell dir vor, in unserem Beispiel sind Fahrzeuge von US-Herstellern momentan nicht lieferbar. Anstatt jede einzelne `<option>` manuell mit dem `disabled`-Attribut zu versehen, kannst du das Attribut direkt auf das `<optgroup>`-Element anwenden.

```html
<select name="car" id="car-model">
  <option value="">-- Bitte wählen --</option>
  
  <optgroup label="Deutsche Hersteller">
    <option value="audi-a4">Audi A4</option>
    <option value="bmw-3er">BMW 3er</option>
  </optgroup>
  
  <optgroup label="Japanische Hersteller">
    <option value="toyota-corolla">Toyota Corolla</option>
    <option value="honda-civic">Honda Civic</option>
  </optgroup>
  
  <optgroup label="US-Hersteller" disabled>
    <option value="ford-mustang">Ford Mustang</option>
    <option value="chevrolet-camaro">Chevrolet Camaro</option>
  </optgroup>
</select>
```

Das Ergebnis: Die Überschrift "US-Hersteller" und alle darunterliegenden Optionen (Ford Mustang, Chevrolet Camaro) werden im Drop-down-Menü ausgegraut dargestellt. Der Benutzer kann keine dieser Optionen mehr auswählen. Dies ist eine sehr effiziente Methode, um die verfügbaren Auswahlmöglichkeiten dynamisch zu steuern, beispielsweise basierend auf anderen Formulareingaben oder Daten aus einer Datenbank.

#### Styling von `<optgroup>` mit CSS

Jetzt kommt ein Punkt, der für viele Webentwickler wichtig ist: das Styling. Wie kannst du das Aussehen der `<optgroup>`-Überschriften an das Design deiner Webseite anpassen?

Die ehrliche Antwort ist: nur sehr begrenzt. Formularelemente wie `<select>`, `<option>` und `<optgroup>` werden zu großen Teilen vom Betriebssystem des Benutzers und nicht vom Browser gerendert. Das bedeutet, dass deine Möglichkeiten, sie mit CSS zu gestalten, stark eingeschränkt sind.

Ein paar grundlegende Eigenschaften funktionieren in den meisten modernen Browsern jedoch recht zuverlässig. Du kannst zum Beispiel die Textfarbe und den Schriftstil der `label` ändern.

```css
optgroup {
  font-style: italic;
  font-weight: bold;
  color: #555;
}
```

Mit diesem CSS-Code würden die Gruppenüberschriften fett und kursiv in einem dunklen Grauton erscheinen. Komplexere Eigenschaften wie `background-color`, `padding` oder `border` haben jedoch entweder gar keinen Effekt oder werden von Browser zu Browser sehr inkonsistent dargestellt.

Wenn du ein vollständig angepasstes Design für deine Drop-down-Menüs benötigst, führt in der Regel kein Weg an einer JavaScript-basierten Lösung vorbei. Dabei wird das native `<select>`-Element versteckt und durch eine Kombination aus `<div>`-, `<ul>`- und `<li>`-Elementen nachgebaut, die du dann nach Belieben mit CSS gestalten kannst. Für die meisten Standardanwendungen ist das aber ein unnötiger Mehraufwand, und die native Funktionalität des `<optgroup>`-Elements reicht völlig aus.

#### Der Mehrwert für die Barrierefreiheit

Über die visuelle Ordnung hinaus bietet `<optgroup>` einen erheblichen Vorteil für die Barrierefreiheit (Accessibility). Benutzer, die auf Screenreader angewiesen sind, profitieren enorm von der zusätzlichen Struktur.

Wenn ein Screenreader auf ein `<select>`-Element mit `<optgroup>` trifft, liest er nicht nur die Optionen vor. Er kündigt auch den Beginn jeder Gruppe an, indem er den Inhalt des `label`-Attributs vorliest. Ein Benutzer könnte also so etwas hören wie: "Gruppe: Deutsche Hersteller, hat 4 Elemente", gefolgt von den einzelnen Optionen innerhalb dieser Gruppe.

Diese zusätzliche kontextuelle Information hilft blinden oder sehbehinderten Benutzern, die Struktur der Liste mental zu erfassen und gezielter zu navigieren. Die Verwendung von `<optgroup>` ist also nicht nur ein "Nice-to-have" für die Optik, sondern ein wichtiger Beitrag zu einem inklusiveren Web. Du verwendest semantisches HTML, um die Bedeutung und Beziehung von Inhalten zu beschreiben, was die Kernidee hinter gutem Webdesign ist.

Letztendlich ist das `<optgroup>`-Element ein kleines, aber mächtiges Werkzeug in deinem HTML-Werkzeugkasten. Es erfordert minimalen Aufwand in der Implementierung, liefert aber einen maximalen Gewinn für die Übersichtlichkeit, Benutzerfreundlichkeit und Barrierefreiheit deiner Formulare. Wann immer du es mit einer langen Auswahlliste zu tun hast, solltest du prüfen, ob eine logische Gruppierung der Optionen sinnvoll ist. Deine Benutzer werden es dir danken.
