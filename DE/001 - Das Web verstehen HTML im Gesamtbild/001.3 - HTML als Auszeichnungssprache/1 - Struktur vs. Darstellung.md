# Struktur vs. Darstellung

### Struktur vs. Darstellung: Die goldene Regel des Webs

Stell dir vor, du baust ein Haus. Was kommt zuerst? Das Fundament, die tragenden Wände, das Dach – die Struktur. Du würdest niemals mit der Wandfarbe oder der Auswahl der Vorhänge beginnen, bevor die Mauern stehen. Diese grundlegende Logik aus der realen Welt ist eine der wichtigsten und mächtigsten Ideen im Webdesign, und sie lässt sich in einem einfachen Prinzip zusammenfassen: der Trennung von Struktur und Darstellung.

HTML ist dein Architekt und Bauingenieur. Es ist ausschließlich dafür verantwortlich, die **Struktur** deines Inhalts zu definieren. Mit HTML sagst du dem Browser: „Das hier ist eine Überschrift erster Ordnung. Das ist ein Absatz. Dies ist eine unsortierte Liste mit drei Einträgen. Und hier beginnt der Hauptinhalt der Seite.“ Du beschreibst die semantische, also die bedeutungsmäßige, Rolle jedes einzelnen Elements. Du gibst deinem Inhalt einen Sinn.

CSS (Cascading Style Sheets) ist dein Innenarchitekt und Dekorateur. CSS kümmert sich um die **Darstellung** – also darum, wie die strukturierte Information am Ende aussieht. Es beantwortet Fragen wie: „Welche Schriftart soll die Überschrift haben? Welche Farbe hat der Text im Absatz? Wie viel Abstand soll zwischen den Listeneinträgen sein? Soll der Hauptinhalt in der Mitte der Seite zentriert sein und einen leichten Schatten haben?“

Diese Trennung ist keine akademische Spitzfindigkeit, sondern das Fundament für sauberen, wartbaren und zukunftssicheren Code. Um zu verstehen, warum das so ist, müssen wir eine kleine Zeitreise in die „dunklen“ Anfangstage des Webs machen.

#### Die Sünden der Vergangenheit: Als alles eins war

In den 1990er-Jahren gab es diese strikte Trennung noch nicht. Man wollte Webseiten nicht nur strukturieren, sondern sie auch gestalten. Also wurden HTML-Tags und Attribute erfunden, die direkt das Aussehen beeinflussten.

Ein klassisches Beispiel ist der `<font>`-Tag. Wolltest du einen Text in Rot und in einer bestimmten Schriftart darstellen, sah dein Code vielleicht so aus:

```html
<p>
  <font color="red" face="Arial" size="4">
    Dies ist ein sehr wichtiger Hinweis!
  </font>
</p>
```

Oder vielleicht wolltest du den Hintergrund deiner gesamten Seite gelb färben. Das ging direkt im `<body>`-Tag:

```html
<body bgcolor="yellow">
  ... dein gesamter Seiteninhalt ...
</body>
```

Um Elemente zu zentrieren, nutzte man den `<center>`-Tag. Um Text fett darzustellen, den `<b>`-Tag (für *bold*). Ganze Webseiten-Layouts wurden mit unsichtbaren Tabellen (`<table>`) konstruiert, eine Technik, die eigentlich für die Darstellung von tabellarischen Daten gedacht war.

Auf den ersten Blick mag das praktisch erscheinen. Man schreibt seinen Inhalt und formatiert ihn direkt an Ort und Stelle. Doch dieser Ansatz führte zu gewaltigen Problemen, die das Web an den Rand der Unüberschaubarkeit brachten:

1.  **Albtraum bei Änderungen:** Stell dir eine Webseite mit 100 Unterseiten vor. Der Kunde entscheidet, dass die rote Schriftfarbe der wichtigen Hinweise nun blau sein soll. Mit dem alten Ansatz müsstest du 100 HTML-Dateien öffnen und an jeder einzelnen Stelle den Wert `color="red"` zu `color="blue"` ändern. Ein winziger Design-Wunsch führt zu stundenlanger, fehleranfälliger Arbeit.

2.  **Aufgeblähter und unleserlicher Code:** Die HTML-Dateien wurden riesig. Sie waren ein unentwirrbares Knäuel aus strukturellem Inhalt und gestalterischen Anweisungen. Es wurde extrem schwierig, den eigentlichen Inhalt – zum Beispiel einen Artikeltext – in diesem Wust aus `<font>`-Tags und `bgcolor`-Attributen zu finden.

3.  **Mangelnde Flexibilität:** Was ist, wenn du dieselbe Webseite auf einem kleinen Handy-Display anders darstellen möchtest als auf einem großen Desktop-Monitor? Oder wenn du eine spezielle, druckerfreundliche Version deiner Seite anbieten willst, ohne Bilder und mit schwarzem Text auf weißem Grund? Mit im HTML verankerten Stilen war das praktisch unmöglich. Man hätte für jedes Gerät und jeden Anwendungsfall eine komplett neue Version der HTML-Datei erstellen müssen.

4.  **Schlechte Barrierefreiheit:** Die wohl wichtigste Schwäche. Programme wie Screenreader, die blinden oder sehbehinderten Menschen Webseiten vorlesen, sind auf eine klare, semantische Struktur angewiesen. Ein Screenreader versteht, dass `<h1>` die wichtigste Überschrift der Seite ist. Er weiß aber nicht, was `<font size="6">` bedeuten soll. Ist das wichtig? Ist es nur groß? Der `<b>`-Tag sagt nur „mache diesen Text fett“. Der semantisch korrekte `<strong>`-Tag hingegen sagt „dieser Text hat eine starke Wichtigkeit“. Die Bedeutung geht im reinen Styling verloren, und damit wird die Webseite für viele Menschen unbenutzbar.

Diese Probleme machten klar: Es braucht einen besseren Weg. Die Lösung war die radikale Trennung von Struktur (HTML) und Darstellung (CSS).

#### Der moderne Ansatz: Jeder macht das, was er am besten kann

Heute sind Tags wie `<font>` und `<center>` sowie Attribute wie `bgcolor` veraltet und sollten unter keinen Umständen mehr verwendet werden. Der moderne Workflow sieht so aus:

1.  **HTML definiert die reine Struktur und Bedeutung.**
2.  **CSS wird in einer separaten Datei geschrieben und gestaltet die HTML-Struktur.**
3.  **Die HTML-Datei wird mit der CSS-Datei verknüpft.**

Schauen wir uns ein konkretes Beispiel an. Wir wollen eine kleine Box mit einer Überschrift und einem kurzen Text erstellen.

**Der alte, schlechte Weg (Struktur und Darstellung vermischt):**

```html
<!-- NICHT NACHMACHEN! DIES IST EIN BEISPIEL FÜR SCHLECHTEN STIL. -->
<table width="300" border="1" cellpadding="10" bgcolor="#f2f2f2">
  <tr>
    <td>
      <b><font face="Arial" color="#333333">Kapitelüberschrift</font></b>
      <br><br>
      <font face="Georgia" color="#555555">
        Dies ist der Einleitungstext für das Kapitel. Er erklärt,
        worum es in den folgenden Abschnitten gehen wird.
      </font>
    </td>
  </tr>
</table>
```

Dieser Code ist schwer zu lesen und extrem unflexibel. Er missbraucht eine Tabelle für das Layout und verwendet veraltete Tags für die Gestaltung.

**Der neue, gute Weg (Struktur und Darstellung getrennt):**

Zuerst schreiben wir das saubere, semantische HTML. Wir beschreiben, *was* die Elemente sind: eine Box (die ein thematisch zusammengehöriger Abschnitt ist, also ein `<section>`), eine Überschrift zweiter Ordnung (`<h2>`) und ein Absatz (`<p>`).

**`index.html`:**
```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Gutes Beispiel</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <section class="info-box">
    <h2>Kapitelüberschrift</h2>
    <p>
      Dies ist der Einleitungstext für das Kapitel. Er erklärt,
      worum es in den folgenden Abschnitten gehen wird.
    </p>
  </section>

</body>
</html>
```

Beachte die Zeile `<link rel="stylesheet" href="style.css">` im `<head>`. Sie ist der entscheidende Klebstoff, der unsere HTML-Struktur mit den Gestaltungsregeln in der CSS-Datei verbindet. Das HTML selbst ist nun frei von jeglichem Design-Ballast. Es ist rein und beschreibt nur noch den Inhalt.

Jetzt kommt der zweite Schritt: die Gestaltung in einer separaten CSS-Datei.

**`style.css`:**
```css
.info-box {
  width: 300px;
  border: 1px solid black;
  padding: 10px;
  background-color: #f2f2f2;
}

.info-box h2 {
  font-family: Arial, sans-serif;
  color: #333333;
  font-weight: bold;
  margin-top: 0; /* Verhindert Standard-Abstand der Überschrift oben */
}

.info-box p {
  font-family: Georgia, serif;
  color: #555555;
}
```

Das Ergebnis im Browser ist optisch identisch mit dem alten Beispiel. Aber unter der Haube haben wir eine Revolution vollzogen.

#### Die unschätzbaren Vorteile der Trennung

Warum ist dieser zweite Weg so viel besser? Die Vorteile spiegeln exakt die Nachteile des alten Ansatzes wider:

*   **Zentrale Wartbarkeit:** Wenn der Kunde nun die Hintergrundfarbe aller Info-Boxen auf der gesamten Webseite von Hellgrau auf Hellblau ändern möchte, musst du nur eine einzige Zeile in der `style.css`-Datei ändern: `background-color: #eaf6ff;`. Fertig. Tausende Seiten werden in Sekunden aktualisiert.

*   **Hervorragende Lesbarkeit:** Sowohl die HTML- als auch die CSS-Datei sind für sich genommen klar und verständlich. Ein Entwickler, der den Inhalt ändern muss, öffnet die HTML-Datei. Ein Designer, der das Aussehen anpassen will, öffnet die CSS-Datei. Jeder findet sich sofort zurecht.

*   **Maximale Flexibilität (Responsive Design):** Mit CSS können wir auf verschiedene Bedingungen reagieren. Wir können dem Browser sagen: „Wenn der Bildschirm schmaler als 600 Pixel ist, mache die Info-Box 100% breit und erhöhe die Schriftgröße.“ Das geschieht mit sogenannten Media Queries in derselben CSS-Datei, ohne das HTML auch nur anzufassen.

*   **Barrierefreiheit (Accessibility):** Unser HTML ist jetzt semantisch. Ein Screenreader erkennt eine `<section>`, eine `<h2>` und einen `<p>`. Er versteht die Hierarchie und die Bedeutung des Inhalts und kann ihn für den Nutzer korrekt interpretieren.

*   **Suchmaschinenoptimierung (SEO):** Auch Suchmaschinen wie Google lieben sauberen, semantischen Code. Sie können eine klar strukturierte Seite besser verstehen, indexieren und bewerten, was sich positiv auf dein Ranking auswirken kann.

Die Trennung von Struktur und Darstellung ist also mehr als nur eine „Best Practice“. Es ist eine grundlegende Philosophie, die das moderne Web erst möglich gemacht hat. Dein HTML ist das stabile, zeitlose Fundament – der Inhalt und seine Bedeutung ändern sich selten. Dein CSS ist die flexible, austauschbare Fassade, die du jederzeit an neue Trends, Geräte und Wünsche anpassen kannst.

Denke immer daran: Dein HTML ist das *Was*, dein CSS ist das *Wie*. Meistere diese Trennung, und du baust nicht nur Webseiten – du erschaffst robuste, flexible und zukunftssichere digitale Erlebnisse.
