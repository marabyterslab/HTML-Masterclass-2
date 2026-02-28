# Wann alt-Text nötig ist

### Wann Alt-Text nötig ist

Stell dir vor, du telefonierst mit einem Freund und versuchst, ihm den Inhalt einer Webseite zu beschreiben, die er gerade nicht sehen kann. Du würdest ihm den Text vorlesen, die Links erklären und bei den Bildern innehalten. Was sagst du dann? „Hier ist ein Bild.“ Das ist nicht sehr hilfreich. Du würdest wahrscheinlich beschreiben, *was auf dem Bild zu sehen ist*, vor allem, wenn es für das Verständnis des restlichen Inhalts wichtig ist.

Genau das ist die Aufgabe des Alternativtextes, kurz Alt-Text. Er ist deine verbale Brücke für Menschen, die Bilder auf deiner Webseite nicht sehen können. Das sind nicht nur blinde oder sehbehinderte Nutzer, die auf Screenreader angewiesen sind – Programme, die den Bildschirminhalt vorlesen. Es betrifft auch Nutzer mit langsamen Internetverbindungen, bei denen Bilder nicht laden, oder solche, die Bilder in ihrem Browser bewusst deaktiviert haben. Sogar Suchmaschinen wie Google nutzen den Alt-Text, um den Inhalt eines Bildes zu verstehen und es besser zu indexieren.

Die Kernfrage lautet also nicht *ob*, sondern *wann* und *wie* du Alt-Text einsetzt. Die Antwort hängt vollständig von der Funktion des Bildes auf deiner Seite ab. Jedes Bild fällt in eine von wenigen Kategorien, und für jede gibt es eine klare Regel.

#### Der häufigste Fall: Informative Bilder

Das sind die Arbeitstiere unter den Bildern. Sie transportieren Informationen, die für das Verständnis des Kontexts relevant sind. Wenn du das Bild entfernen würdest, ginge eine wichtige Information verloren.

Ein informatives Bild kann sein:
*   Ein Foto, das ein Produkt, eine Person oder einen Ort zeigt.
*   Ein Diagramm, das Daten visualisiert.
*   Ein Screenshot, der einen Prozess erklärt.
*   Ein Icon, das eine Bedeutung hat (z. B. ein Einkaufswagen-Symbol).

Für diese Bilder ist ein aussagekräftiger Alt-Text absolut unerlässlich. Der Text sollte kurz und prägnant beschreiben, was auf dem Bild zu sehen ist und warum es wichtig ist.

Stell dir einen Blogartikel über Kaffeezubereitung vor. Darin ist ein Bild einer French Press.

**Schlechter Alt-Text:**
```html
<img src="french-press.jpg" alt="Bild">
```
oder
```html
<img src="french-press.jpg" alt="Kaffeemaschine">
```
Das ist zu vage. "Bild" ist nutzlos, und "Kaffeemaschine" ist nicht spezifisch genug.

**Guter Alt-Text:**
```html
<img src="french-press.jpg" alt="Eine gläserne French Press, gefüllt mit frisch gebrühtem Kaffee.">
```
Dieser Text ist deskriptiv. Ein Screenreader würde vorlesen: „Eine gläserne French Press, gefüllt mit frisch gebrühtem Kaffee.“ Der Nutzer weiß sofort, worum es geht und kann den visuellen Kontext nachvollziehen.

Vermeide es, mit „Ein Bild von…“ oder „Grafik, die zeigt…“ zu beginnen. Der Screenreader kündigt bereits an, dass es sich um ein Bild handelt. Geh direkt zur Beschreibung über.

#### Wenn Bilder nur schmücken: Dekorative Bilder

Manchmal ist ein Bild einfach nur da, um gut auszusehen. Es trägt keine neuen Informationen zum Inhalt bei. Das können Hintergrundmuster, Trennlinien, oder abstrakte Designelemente sein. Wenn du ein solches Bild entfernen würdest, würde der Text immer noch denselben Sinn ergeben.

In diesem Fall wäre ein beschreibender Alt-Text für einen Screenreader-Nutzer reines Rauschen. Stell dir vor, du liest einen Artikel und nach jedem zweiten Absatz sagt dir jemand: „Hier ist eine blaue, geschwungene Linie.“ Das ist störend und lenkt vom eigentlichen Inhalt ab.

Für dekorative Bilder gibt es eine spezielle, sehr wichtige Regel: Du lässt das `alt`-Attribut nicht weg, sondern du setzt es auf einen leeren String.

```html
<img src="blaue-trennlinie.svg" alt="">
```

Das ist ein entscheidender Unterschied. Ein fehlendes `alt`-Attribut ist ein technischer Fehler. Viele Screenreader versuchen dann, den Dateinamen des Bildes vorzulesen, was zu etwas wie „IMG_7345_final.jpg“ führen kann – absolut unverständlich und verwirrend. Ein leeres `alt=""` hingegen ist ein klares Signal an den Screenreader: „Dieses Bild ist rein dekorativ. Du kannst es ignorieren. Fahr mit dem nächsten Inhalt fort.“

#### Wenn Bilder eine Funktion haben: Links und Buttons

Bilder werden oft als klickbare Elemente verwendet. Ein Logo, das zur Startseite führt, ein Lupen-Icon für eine Suchleiste oder ein Social-Media-Icon, das zu einem Profil verlinkt.

Hier ändert sich die Aufgabe des Alt-Textes fundamental. Er soll nicht beschreiben, wie das Bild *aussieht*, sondern welche *Aktion* es auslöst oder wohin es *führt*.

Nehmen wir das Firmenlogo in der Kopfzeile einer Webseite, das typischerweise zur Startseite verlinkt ist.

**Falsch:**
```html
<a href="/">
  <img src="logo.svg" alt="Logo der Firma Sonnenschein">
</a>
```
Ein Screenreader würde sagen: „Link, Bild, Logo der Firma Sonnenschein.“ Der Nutzer weiß zwar, was das Bild zeigt, aber nicht, was passiert, wenn er klickt.

**Richtig:**
```html
<a href="/">
  <img src="logo.svg" alt="Startseite der Firma Sonnenschein">
</a>
```
Jetzt ist die Ansage klar: „Link, Bild, Startseite der Firma Sonnenschein.“ Der Zweck des Links ist sofort verständlich.

Das Gleiche gilt für einen Button, der nur ein Icon enthält:
```html
<button type="submit">
  <img src="suche-lupe.svg" alt="Suche starten">
</button>
```
Der Alt-Text „Lupe“ wäre eine Beschreibung, aber „Suche starten“ ist die Funktion – und genau das ist hier entscheidend.

#### Wenn Text im Bild ist

Eine Grundregel im Webdesign lautet: Vermeide es, wichtigen Text in Bilder zu packen. Text in Bildern kann nicht von Screenreadern gelesen, nicht von Suchmaschinen indiziert und nicht vom Nutzer markiert oder kopiert werden. Er skaliert oft schlecht auf unterschiedlichen Bildschirmgrößen und ist für Menschen mit Sehschwäche schwerer zu lesen.

Manchmal lässt es sich aber nicht vermeiden, zum Beispiel bei Logos mit einem Slogan oder bei einem speziell gestalteten Werbebanner. In diesem Fall ist die Regel einfach: Der Alt-Text muss den exakten Text wiedergeben, der im Bild steht.

Angenommen, du hast ein Banner für einen Sale:
```html
<img src="sommer-sale.png" alt="Sommerschlussverkauf: Bis zu 50 % Rabatt auf alle T-Shirts.">
```
So stellst du sicher, dass die Information, die visuell vermittelt wird, auch für alle anderen zugänglich ist.

#### Komplexe Bilder: Infografiken und Diagramme

Was ist mit Bildern, die so viele Informationen enthalten, dass ein kurzer Alt-Text nicht ausreicht? Denke an eine komplexe Infografik oder ein wissenschaftliches Diagramm. Ein Alt-Text mit 300 Wörtern wäre unpraktisch und würde den Lesefluss stören.

Hier gibt es eine zweistufige Lösung.
1.  **Der Alt-Text gibt eine kurze Zusammenfassung.** Er beschreibt, was das Bild im Allgemeinen darstellt.
2.  **Der umgebende Fließtext oder ein separater Abschnitt liefert die vollständige Beschreibung.**

Ein Beispiel für ein Balkendiagramm, das den Umsatz pro Quartal zeigt:

```html
<img src="umsatz-q1-q4.png" alt="Balkendiagramm der Umsätze für das letzte Geschäftsjahr. Eine detaillierte Aufschlüsselung folgt im nächsten Absatz.">

<p>
  Das Diagramm zeigt eine stetige Umsatzsteigerung über die vier Quartale. 
  Der Umsatz im ersten Quartal (Q1) betrug 1,2 Millionen Euro. Im zweiten Quartal (Q2) stieg er auf 1,5 Millionen Euro, gefolgt von 1,4 Millionen Euro in Q3. Das vierte Quartal (Q4) war mit 2,1 Millionen Euro das stärkste.
</p>
```

Auf diese Weise erhält der Screenreader-Nutzer zuerst einen Überblick über das Bild (`alt`-Text) und kann sich dann entscheiden, die ausführliche Beschreibung im Text zu lesen, die auch für sehende Nutzer nützlich ist.

Die Entscheidung, wann und welcher Alt-Text nötig ist, ist keine rein technische, sondern eine zutiefst menschliche. Es geht um Empathie und Kontext. Frag dich bei jedem `<img>`-Tag, das du schreibst: „Welche Erfahrung würde ein Nutzer verpassen, wenn dieses Bild nicht da wäre, und wie kann ich diese Lücke mit Worten füllen?“ Wenn du diese Frage zur Gewohnheit machst, wird barrierefreies Webdesign für dich zur zweiten Natur.
