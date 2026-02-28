# Struktur vs. Darstellung

### Kapitel 1.3: Struktur vs. Darstellung: Die goldene Regel des Webs

Stell dir vor, du baust ein Haus. Was kommt zuerst? Du gießt das Fundament, ziehst die tragenden Wände hoch und setzt das Dach darauf. Du schaffst eine stabile, logische Struktur. Erst danach entscheidest du, welche Farbe die Wände bekommen, welchen Bodenbelag du verlegst und welche Vorhänge an die Fenster kommen. Du würdest niemals versuchen, einen Vorhang in die Luft zu hängen und dann eine Wand darum herum zu bauen.

Genau dieses fundamentale Prinzip – die strikte Trennung von Struktur und Darstellung – ist die wichtigste Regel, die du im modernen Webdesign verstehen musst. HTML ist dein Architekt für das Haus, CSS ist dein Innenarchitekt.

**Struktur (Der Inhalt und seine Bedeutung)**
Die Struktur ist das "Was". Es geht um den reinen Inhalt und seine logische Gliederung.
- Was ist dieser Text? Eine Überschrift erster Ordnung? Ein normaler Absatz?
- Was ist dieses Element? Eine Liste von Navigationspunkten? Ein Zitat? Ein Bild mit einer Bildunterschrift?

Deine Aufgabe als HTML-Autor ist es, dem Inhalt eine Bedeutung zu geben. Du zeichnest ihn semantisch korrekt aus. Das Wort „semantisch“ bedeutet hier nichts anderes als „auf die Bedeutung bezogen“. Du sagst dem Browser (und anderen Maschinen wie Suchmaschinen oder Screenreadern) unmissverständlich, welche Rolle ein bestimmter Teil deines Inhalts spielt. Dafür ist HTML da. Nur dafür.

**Darstellung (Das Aussehen)**
Die Darstellung ist das "Wie". Es geht ausschließlich darum, wie die strukturierte Information visuell präsentiert wird.
- Wie sieht die Überschrift aus? Welche Schriftart, welche Größe, welche Farbe hat sie?
- Wie ist die Navigation angeordnet? Horizontal nebeneinander oder vertikal untereinander?
- Wie viel Abstand ist zwischen den Absätzen? Gibt es einen Rahmen um das Bild?

Für all diese Fragen ist eine andere Sprache zuständig: Cascading Style Sheets, kurz CSS. Mit CSS definierst du die visuellen Regeln, die auf deine HTML-Struktur angewendet werden.

#### Ein Blick zurück: Die dunkle Zeit der Vermischung

Um wirklich zu schätzen, warum diese Trennung so heilig ist, müssen wir eine kurze Reise in die Vergangenheit des Webs unternehmen. In den frühen Tagen von HTML gab es CSS noch nicht oder es war nicht weit verbreitet. Entwickler standen vor einem Problem: Sie hatten nur HTML, wollten ihre Seiten aber trotzdem irgendwie gestalten.

Die Lösung war eine Notlösung: Man missbrauchte HTML für die Darstellung. Es entstanden HTML-Tags, deren einziger Zweck es war, das Aussehen zu beeinflussen.

Schauen wir uns ein typisches Beispiel aus dieser Ära an. Man wollte eine zentrierte, rote Überschrift in der Schriftart Arial. Der Code dafür hätte so aussehen können:

```html
<!-- NICHT NACHMACHEN! Veralteter und schlechter Stil. -->
<center>
  <font face="Arial" color="red" size="5">
    Willkommen auf meiner Webseite!
  </font>
</center>
```

Auf den ersten Blick mag das harmlos erscheinen. Es funktioniert ja, die Überschrift wird wie gewünscht dargestellt. Doch dieser Ansatz ist eine technische Katastrophe, und zwar aus mehreren Gründen:

1.  **Albtraum bei der Wartung:** Stell dir eine Webseite mit 100 Unterseiten vor. Auf jeder Seite gibt es solche Überschriften. Nun entscheidet der Kunde, dass alle Überschriften nicht mehr rot, sondern blau sein sollen. Was nun? Du musst 100 einzelne HTML-Dateien öffnen und an jeder Stelle `color="red"` zu `color="blue"` ändern. Das ist nicht nur extrem zeitaufwendig, sondern auch unglaublich fehleranfällig.

2.  **Mangelnde Barrierefreiheit:** Ein Screenreader, eine Software für sehbehinderte Menschen, liest den HTML-Code vor. Was soll er mit `<font>` oder `<center>` anfangen? Diese Tags sagen nichts über die Bedeutung des Inhalts aus. Der Screenreader weiß nicht, dass "Willkommen auf meiner Webseite!" eine wichtige Überschrift ist. Er sieht nur Text, der irgendwie formatiert ist. Die logische Struktur der Seite geht komplett verloren. Suchmaschinen haben ein ähnliches Problem: Sie können die Wichtigkeit von Inhalten nur schwer einschätzen.

3.  **Aufgeblähter Code:** Jede einzelne Formatierungsanweisung muss direkt im HTML-Code wiederholt werden. Das bläht die Dateigröße unnötig auf, was zu längeren Ladezeiten führt – ein entscheidender Faktor für die Nutzerzufriedenheit.

4.  **Keine Flexibilität:** Was ist, wenn du dieselbe Webseite auf einem kleinen Smartphone-Display anzeigen willst? Oder vielleicht möchtest du eine spezielle, druckerfreundliche Version deiner Seite anbieten, ohne Bilder und mit einer einfachen serifenlosen Schrift. Mit in HTML hartcodiertem Styling ist das praktisch unmöglich. Du müsstest komplett separate HTML-Dateien für jeden Anwendungsfall pflegen.

Diese Vermischung von Struktur und Darstellung führte in eine Sackgasse. Das Web brauchte eine bessere Lösung.

#### Die moderne Lösung: Saubere Trennung mit CSS

Die Lösung ist die heute etablierte Praxis: HTML kümmert sich um die Struktur, CSS um die Darstellung. Schauen wir uns an, wie wir das vorherige Beispiel auf die moderne, korrekte Art umsetzen.

Zuerst schreiben wir das HTML. Wir fragen uns: Was *ist* dieser Text? Es ist die wichtigste Überschrift der Seite. Also verwenden wir das semantisch korrekte Element dafür: `<h1>`.

**Die HTML-Datei (z. B. `index.html`):**
```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Moderne Webseite</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <h1>Willkommen auf meiner Webseite!</h1>

</body>
</html>
```

Das ist alles. Der HTML-Code ist sauber, kurz und semantisch eindeutig. Jede Maschine versteht sofort: `<h1>` umschließt die Hauptüberschrift. Das `<link>`-Tag im `<head>`-Bereich stellt die Verbindung zu einer externen CSS-Datei her, in der wir nun die gesamte Gestaltung definieren.

**Die CSS-Datei (z. B. `style.css`):**
```css
h1 {
  text-align: center;
  color: red;
  font-family: Arial, sans-serif;
  font-size: 2em; /* Eine flexiblere Art, die Schriftgröße festzulegen */
}
```

Siehst du die Eleganz dieser Lösung?

1.  **Einfache Wartung:** Wenn der Kunde jetzt blaue Überschriften wünscht, änderst du *eine einzige Zeile* in der `style.css`-Datei: `color: blue;`. Speichern, hochladen, fertig. Alle 100 Seiten, die diese CSS-Datei verwenden, werden sofort aktualisiert.

2.  **Hervorragende Barrierefreiheit:** Der Screenreader sieht das `<h1>`-Tag und verkündet: „Überschrift Ebene 1: Willkommen auf meiner Webseite!“. Die Bedeutung ist klar. Suchmaschinen wissen, dass dies der wichtigste Titel auf der Seite ist und gewichten ihn entsprechend.

3.  **Schlanker, effizienter Code:** Der HTML-Code bleibt frei von Styling-Müll. Die CSS-Datei wird vom Browser des Besuchers beim ersten Aufruf heruntergeladen und zwischengespeichert (gecacht). Bei allen folgenden Seitenaufrufen muss sie nicht erneut geladen werden, was die Ladezeit der gesamten Webseite drastisch reduziert.

4.  **Maximale Flexibilität:** Mit CSS kannst du mühelos verschiedene Darstellungen für unterschiedliche Ausgabegeräte definieren. Du kannst Regeln schreiben, die nur für Bildschirme ab einer bestimmten Breite gelten (Responsive Design), oder komplett andere Stile für den Ausdruck der Seite festlegen (`@media print`). All das, ohne eine einzige Zeile deines HTML-Codes anfassen zu müssen.

#### Was bedeutet das für deine Arbeit?

Diese Trennung ist mehr als nur eine technische Empfehlung – sie ist eine Denkweise. Wenn du HTML schreibst, musst du lernen, dein Gehirn in den „Struktur-Modus“ zu schalten. Stelle dir bei jedem Inhalt die Frage:

**„Welche Bedeutung hat dieser Inhalt?“**

und *niemals*:

**„Wie soll dieser Inhalt aussehen?“**

Wenn du einen Textabschnitt hervorheben möchtest, weil er besonders wichtig ist, verwendest du `<strong>`. Du verwendest es nicht, weil du den Text fett haben willst. Dass Browser `<strong>` standardmäßig fett darstellen, ist eine Konvention, aber nicht der eigentliche Zweck des Tags. Der Zweck ist die Betonung der Wichtigkeit. Wenn du später entscheidest, dass wichtige Texte nicht fett, sondern unterstrichen und in einer anderen Farbe erscheinen sollen, änderst du das mit einer einzigen CSS-Regel für `strong`-Elemente.

Genauso verhält es sich mit `<em>` (emphasis, Betonung) versus `<i>` (italic). Semantisch korrekt ist `<em>`, wenn du einem Wort eine sprachliche Betonung geben willst. `<i>` ist eher für Dinge wie Fachbegriffe oder Schiffsnamen gedacht, also für Text, der sich stilistisch vom Rest abhebt, ohne eine besondere Betonung zu haben. Das Aussehen (kursiv) kannst du für beide per CSS jederzeit ändern.

Die konsequente Trennung von Struktur und Darstellung ist das Fundament für professionelle, wartbare, barrierefreie und zukunftssichere Webseiten. Es ist die eine Regel, die über allen anderen steht. Wenn du dieses Prinzip verinnerlichst, bist du bereits auf dem besten Weg, nicht nur Code zu schreiben, sondern das Web wirklich zu verstehen.
