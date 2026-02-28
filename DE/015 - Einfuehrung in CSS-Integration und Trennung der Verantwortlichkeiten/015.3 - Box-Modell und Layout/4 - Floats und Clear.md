# Floats und Clear

### Floats und Clear: Elemente aus dem Fluss nehmen

Stell dir eine Webseite als einen Fluss vor. Block-Elemente wie Überschriften oder Absätze sind wie Steine, die du nacheinander in diesen Fluss legst. Jeder neue Stein platziert sich brav unter dem vorherigen. Inline-Elemente sind wie kleinere Kiesel, die sich im Textfluss aneinanderreihen. Das ist der normale, vorhersehbare Dokumentenfluss. Aber was, wenn du einen Stein – sagen wir, ein Bild – an den Rand des Flusses legen und das Wasser (den Text) darum herumfließen lassen möchtest? Genau hier kommt die CSS-Eigenschaft `float` ins Spiel.

#### Was ist `float`?

Die Eigenschaft `float` wurde ursprünglich genau für diesen Zweck entworfen: um Text um Bilder oder andere Elemente fließen zu lassen, so wie du es aus Zeitungen oder Magazinen kennst. Wenn du einem Element `float` zuweist, nimmst du es aus diesem normalen Dokumentenfluss heraus und lässt es entweder am linken oder am rechten Rand seines Elternelements "schwimmen". Der restliche Inhalt des Elternelements erkennt dieses "schwimmende" Element und fließt elegant um es herum.

Die `float`-Eigenschaft hat hauptsächlich drei Werte, die für dich relevant sind:

*   `left`: Das Element wird an den linken Rand des Elternelements verschoben.
*   `right`: Das Element wird an den rechten Rand des Elternelelements verschoben.
*   `none`: Das Element verhält sich normal und wird nicht aus dem Fluss genommen (das ist der Standardwert).

Sehen wir uns ein klassisches Beispiel an. Du hast einen Textabsatz und möchtest ein Bild darin platzieren, um den Inhalt aufzulockern.

**HTML:**

```html
<div class="artikel">
  <img src="bild.jpg" alt="Ein beschreibender Text für das Bild">
  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
</div>
```

Ohne CSS würde das Bild einfach über dem Textabsatz stehen, da `<img>` und `<p>` in diesem Kontext wie Block-Elemente behandelt werden. Sie nehmen jeweils eine eigene Zeile ein.

Jetzt fügen wir etwas CSS hinzu:

**CSS:**

```css
.artikel img {
  float: left;
  margin-right: 15px; /* Etwas Abstand zwischen Bild und Text */
  margin-bottom: 5px;  /* Etwas Abstand nach unten */
}
```

Mit `float: left;` wird das Bild sofort aus dem normalen Fluss genommen und an den linken Rand des `.artikel`-Containers geschoben. Der Text im `<p>`-Tag erkennt das Bild, respektiert dessen Platz und fließt rechts daneben weiter, bis er unter das Bild rutscht, sobald der vertikale Platz des Bildes aufgebraucht ist. Das Ergebnis ist ein sauberes, professionelles Layout, das wir aus Printmedien kennen.

#### Das Problem mit dem kollabierenden Elternelement

Floats sind mächtig, aber sie bringen eine knifflige Nebenwirkung mit sich. Da gefloatete Elemente aus dem normalen Dokumentenfluss entfernt werden, verliert ihr Elternelement die Fähigkeit, ihre Höhe zu "sehen" oder zu berücksichtigen.

Stell dir einen Container vor, der ausschließlich gefloatete Elemente enthält. Aus Sicht des Layouts ist dieser Container nun leer, da all seine Kinder aus dem Fluss genommen wurden. Das Resultat: Der Container "kollabiert" auf eine Höhe von null.

Schauen wir uns das an einem Beispiel an, bei dem wir ein Layout mit zwei Spalten erstellen wollen:

**HTML:**

```html
<div class="container">
  <div class="spalte-links">Inhalt der linken Spalte...</div>
  <div class="spalte-rechts">Inhalt der rechten Spalte...</div>
</div>
```

**CSS:**

```css
.container {
  border: 2px solid #333;
  width: 100%;
}

.spalte-links {
  float: left;
  width: 60%;
  background-color: #f2f2f2;
}

.spalte-rechts {
  float: left;
  width: 40%;
  background-color: #e3e3e3;
}
```

Wenn du diesen Code ausführst, wirst du etwas Seltsames bemerken. Die beiden Spalten stehen zwar nebeneinander, wie wir es wollten, aber der schwarze Rahmen des `.container`-Elements ist nicht um sie herum. Er ist nur als eine dünne Linie ganz oben sichtbar. Warum? Weil der Container seine gefloateten Kinder nicht mehr in seiner Höhenberechnung berücksichtigt und daher auf eine Höhe von null kollabiert ist. Alle nachfolgenden Elemente auf der Webseite würden nun direkt unter diesen Rahmen rutschen und sich mit den Spalten überlappen. Das ist ein klassisches Layout-Problem, das durch Floats entsteht.

#### Die Lösung: `clear`

Um dieses Problem zu lösen, brauchen wir einen Weg, dem Browser zu sagen: "Stopp! Bevor du mit dem nächsten Element weitermachst, warte, bis die gefloateten Elemente über dir abgeschlossen sind." Genau das tut die Eigenschaft `clear`.

`clear` wird auf ein Element angewendet, das *nach* den gefloateten Elementen kommt. Es weist dieses Element an, nicht neben einem gefloateten Element zu beginnen, sondern sich darunter zu positionieren.

Die `clear`-Eigenschaft hat folgende wichtige Werte:

*   `left`: Das Element wird unter alle linksseitig gefloateten Elemente verschoben.
*   `right`: Das Element wird unter alle rechtsseitig gefloateten Elemente verschoben.
*   `both`: Das Element wird unter alle gefloateten Elemente verschoben, egal ob sie links oder rechts floaten. Dies ist der sicherste und am häufigsten verwendete Wert.

Eine alte, aber simple Methode, um unser kollabierendes Container-Problem zu lösen, war das Einfügen eines leeren Elements mit `clear: both;` am Ende des Containers.

**HTML (Alte Methode):**

```html
<div class="container">
  <div class="spalte-links">...</div>
  <div class="spalte-rechts">...</div>
  <div style="clear: both;"></div> <!-- Leeres Element nur für das Clearing -->
</div>
```

Dieses leere `div` zwingt den `.container`, sich so weit auszudehnen, bis er dieses clearende Element umschließt. Da das clearende Element unterhalb der gefloateten Spalten positioniert wird, dehnt sich der Container korrekt auf die Höhe seiner höchsten gefloateten Spalte aus.

Das Problem bei dieser Methode ist, dass sie unschön ist. Du fügst ein HTML-Element hinzu, das keine semantische Bedeutung hat und nur aus Präsentationsgründen existiert. Das widerspricht dem Prinzip der Trennung von Inhalt (HTML) und Darstellung (CSS).

#### Die moderne Lösung: Der Clearfix-Hack

Glücklicherweise gibt es eine saubere, reine CSS-Lösung, die als "Clearfix" bekannt ist. Anstatt ein zusätzliches HTML-Element einzufügen, verwenden wir ein CSS-Pseudo-Element (`::after`), um ein unsichtbares Block-Element am Ende des Containers zu erzeugen und diesem dann `clear: both;` zuzuweisen.

Der moderne Clearfix sieht so aus:

**CSS:**

```css
.clearfix::after {
  content: "";
  display: block;
  clear: both;
}
```

Und so wendest du ihn an:

**HTML (Moderne Methode):**

```html
<div class="container clearfix">
  <div class="spalte-links">Inhalt der linken Spalte...</div>
  <div class="spalte-rechts">Inhalt der rechten Spalte...</div>
  <!-- Kein leeres div mehr nötig! -->
</div>
```

**Was passiert hier genau?**

1.  `.clearfix::after`: Wir zielen auf ein Pseudo-Element ab, das *nach* dem gesamten Inhalt des Elements mit der Klasse `.clearfix` eingefügt wird.
2.  `content: "";`: Dieses Pseudo-Element muss einen Inhalt haben, um überhaupt gerendert zu werden. Ein leerer String reicht aus.
3.  `display: block;`: Wir machen dieses unsichtbare Element zu einem Block-Element, damit es die `clear`-Eigenschaft überhaupt annehmen und eine eigene Zeile beanspruchen kann.
4.  `clear: both;`: Das ist der entscheidende Teil. Dieses unsichtbare Block-Element wird nun angewiesen, unter alle vorhergehenden Floats zu rutschen.

Indem dieses unsichtbare Element an das Ende des Containers gezwungen wird (unter die Floats), muss der Container seine Höhe so weit ausdehnen, dass er es umschließen kann. Das Problem des kollabierenden Containers ist elegant und ohne zusätzliches HTML-Markup gelöst.

#### Der Stellenwert von Floats heute

Es ist wichtig zu verstehen, dass `float` über viele Jahre die primäre Methode war, um komplexe, spaltenbasierte Layouts im Web zu erstellen. Es war ein Hack, eine Zweckentfremdung einer Eigenschaft, die eigentlich nur für das Umfließen von Text gedacht war.

Heute haben wir mit **Flexbox** und **CSS Grid** weitaus bessere, leistungsfähigere und intuitivere Werkzeuge für das Layout einer gesamten Seite. Diese modernen Techniken sind speziell für die Erstellung von komplexen, flexiblen und responsiven Layouts konzipiert und lösen die Probleme, die `float` mit sich brachte, von Grund auf.

Solltest du `float` also gar nicht mehr verwenden? Doch, aber für seinen ursprünglichen Zweck. Wenn du ein Bild oder eine Infobox hast, die von Text umflossen werden soll, ist `float` nach wie vor die perfekte und semantisch korrekte Wahl. Für das übergeordnete Seitenlayout, also die Anordnung deiner Hauptbereiche wie Header, Sidebar, Hauptinhalt und Footer, solltest du jedoch auf Flexbox oder Grid zurückgreifen. Sie sind die Werkzeuge der Wahl für modernes Webdesign.
