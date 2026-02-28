# Einsatz von Kommentaren

### Einsatz von Kommentaren

Stell dir vor, du arbeitest an einem großen Bauprojekt. Du hinterlässt Markierungen an Wänden, schreibst Notizen auf Blaupausen und beschriftest Kisten mit Baumaterial. Diese Hinweise sind für den fertigen Hausbesitzer unsichtbar und irrelevant, aber für dich und dein Team sind sie während des Bauprozesses von unschätzbarem Wert. HTML-Kommentare sind genau das: deine Notizen und Markierungen im digitalen Bauplan deiner Webseite.

Ein Kommentar ist ein Textabschnitt in deinem HTML-Code, der vom Browser vollständig ignoriert wird. Er wird nicht auf der Webseite angezeigt und hat keinerlei Einfluss auf die Struktur oder das Aussehen deiner Seite. Sein einziger Zweck ist es, Menschen, die den Quellcode lesen – also dich selbst in der Zukunft oder deine Teamkollegen – mit Informationen zu versorgen.

Die Syntax ist einfach und leicht zu merken. Ein Kommentar beginnt immer mit `<!--` und endet mit `-->`.

```html
<!-- Dies ist ein HTML-Kommentar. Der Browser wird diesen Text nicht anzeigen. -->
<p>Dieser Text hingegen ist für jeden sichtbar.</p>
```

Alles, was sich zwischen diesen beiden Markierungen befindet, ist Teil des Kommentars. Das können einzelne Wörter, ganze Sätze oder sogar mehrere Zeilen Code sein.

```html
<!--
  Autor: Dein Name
  Erstellt am: 24.10.2023
  Zweck: Dies ist der Header-Bereich der Webseite.
-->
<header>
  <h1>Meine Webseite</h1>
</header>
```

#### Wofür solltest du Kommentare verwenden?

Kommentare sind keine Dekoration; sie sind ein Werkzeug für professionelles Arbeiten. Wenn du sie klug einsetzt, machst du deinen Code verständlicher, wartbarer und für die Zusammenarbeit geeigneter. Hier sind die wichtigsten Anwendungsfälle:

**1. Erklärungen und Dokumentation**

Dies ist der klassische Anwendungsfall. Du nutzt Kommentare, um komplexe oder nicht sofort ersichtliche Teile deines Codes zu erklären. Es geht nicht darum, das Offensichtliche zu beschreiben. Ein Kommentar wie `<!-- Ein Absatz -->` vor einem `<p>`-Tag ist nutzlos. Ein guter Kommentar erklärt das *Warum*, nicht das *Was*.

Stell dir vor, du hast einen komplizierten HTML-Abschnitt mit mehreren verschachtelten `<div>`-Elementen für ein spezielles Layout.

```html
<!-- Beginn des dreispaltigen Feature-Blocks.
     Die zusätzliche Verschachtelung mit .grid-wrapper ist notwendig,
     um einen zentrierten Container mit voller Breite für den Hintergrund zu ermöglichen.
-->
<div class="feature-background">
  <div class="grid-wrapper">
    <!-- ... hier folgt der komplexe Inhalt ... -->
  </div>
</div>
```

Dieser Kommentar erklärt, warum die Struktur so ist, wie sie ist – eine Information, die aus dem reinen HTML-Code nicht sofort hervorgeht und die einem Kollegen (oder deinem zukünftigen Ich) viel Zeit sparen kann.

**2. Code temporär deaktivieren (Auskommentieren)**

Einer der praktischsten Einsatzzwecke für Kommentare ist das "Auskommentieren" von Code. Angenommen, du arbeitest an einem neuen Feature, das aber noch nicht fertig ist oder einen Fehler verursacht. Anstatt den Code zu löschen und Gefahr zu laufen, ihn zu verlieren, kannst du ihn einfach in einen Kommentarblock einschließen.

```html
<main>
  <h1>Willkommen auf unserer Seite!</h1>
  <p>Hier sind unsere Hauptinhalte.</p>

  <!-- Das neue, unfertige Kontaktformular vorübergehend deaktivieren -->
  <!--
  <section class="contact-form">
    <h2>Kontaktieren Sie uns!</h2>
    <form>
      ...
    </form>
  </section>
  -->

</main>
```

Der Browser ignoriert den gesamten `section`-Block, als wäre er nicht da. Sobald du bereit bist, weiter daran zu arbeiten, entfernst du einfach die Kommentar-Tags `<!--` und `-->`, und der Code ist wieder aktiv. Dies ist eine alltägliche Technik beim Testen und bei der Fehlersuche (Debugging).

**3. Erinnerungen und To-dos hinterlassen**

Manchmal stößt du während der Entwicklung auf ein Problem, das du später beheben musst, oder du hast eine Idee für eine zukünftige Verbesserung. Kommentare sind perfekt, um solche Notizen direkt an der relevanten Stelle im Code zu hinterlassen. Oft verwenden Entwickler standardisierte Schlüsselwörter, um diese Kommentare leichter wiederzufinden.

```html
<!-- TODO: Die Verlinkungen im Footer müssen noch aktualisiert werden. -->
<footer>
  ...
</footer>

<!-- FIXME: Dieser Abschnitt verursacht auf mobilen Geräten ein Layout-Problem. -->
<div class="image-gallery">
  ...
</div>
```

-   `TODO`: Markiert eine Aufgabe, die noch erledigt werden muss.
-   `FIXME`: Weist auf ein bekanntes Problem oder einen Fehler hin, der behoben werden muss.
-   `NOTE` oder `INFO`: Dient der Hervorhebung einer wichtigen Information.

Viele Code-Editoren erkennen diese Schlüsselwörter und heben sie farblich hervor, was die Übersichtlichkeit weiter verbessert.

**4. Strukturelle Markierungen**

In sehr langen und komplexen HTML-Dateien kann es hilfreich sein, große Abschnitte mit Kommentaren zu markieren. Dies dient der reinen Orientierung und hilft dir, den Code schneller zu überfliegen.

```html
<!-- ================================================== -->
<!--                     HEADER START                   -->
<!-- ================================================== -->
<header>
  ...
</header>
<!-- ================================================== -->
<!--                      HEADER END                    -->
<!-- ================================================== -->


<!-- ================================================== -->
<!--                 MAIN CONTENT START                 -->
<!-- ================================================== -->
<main>
  ...
</main>
<!-- ================================================== -->
<!--                  MAIN CONTENT END                  -->
<!-- ================================================== -->
```

Obwohl dieser Stil etwas aus der Mode gekommen ist, kann er in riesigen Dateien immer noch eine wertvolle Navigationshilfe sein.

#### Die goldene Regel: Kommentare sind öffentlich!

Ein extrem wichtiger Punkt, den du niemals vergessen darfst: **Kommentare im HTML-Code sind für jeden einsehbar.** Auch wenn sie nicht auf der Webseite selbst erscheinen, sind sie Teil des Quellcodes, den der Browser herunterlädt. Jeder Besucher kann mit einem Rechtsklick auf deine Seite und der Auswahl von "Seitenquelltext anzeigen" (oder einer ähnlichen Option in seinem Browser) deinen gesamten HTML-Code inklusive aller Kommentare lesen.

Das bedeutet: **Hinterlasse niemals sensible Informationen in Kommentaren!**

-   Keine Passwörter oder Zugangsdaten.
-   Keine API-Schlüssel.
-   Keine internen Notizen über Kunden oder Projekte.
-   Keine unfertigen oder peinlichen Bemerkungen.

Gehe immer davon aus, dass alles, was du in einen HTML-Kommentar schreibst, auf einem öffentlichen Plakat in der Mitte eines Marktplatzes steht.

#### Technische Details und Fallstricke

Obwohl die Syntax einfach ist, gibt es zwei technische Details, die du kennen solltest:

**1. Kommentare können nicht verschachtelt werden.**
Du kannst keinen Kommentar innerhalb eines anderen Kommentars erstellen. Der Grund ist, dass der Parser den Kommentar beendet, sobald er auf das erste schließende `-->`-Tag trifft.

Dieser Code funktioniert nicht wie erwartet:

```html
<!-- Äußerer Kommentar beginnt
  <p>Ein bisschen Text.</p>
  <!-- Innerer Kommentar. ACHTUNG: Das hier wird alles kaputt machen! -->
  <p>Noch mehr Text.</p>
--> Äußerer Kommentar sollte hier enden, tut er aber nicht.
```

Der Browser sieht das erste `-->` (das des inneren Kommentars) und beendet den gesamten Kommentar an dieser Stelle. Der restliche Text, `<p>Noch mehr Text.</p> -->`, wird dann als fehlerhafter HTML-Code interpretiert und kann zu unerwarteten Anzeigefehlern führen.

**2. Keine doppelten Bindestriche im Kommentar.**
Laut der offiziellen HTML-Spezifikation darf der Text innerhalb eines Kommentars nicht die Zeichenfolge `--` enthalten.

```html
<!-- Das hier ist technisch gesehen -- ungültig! -->
```

Die meisten modernen Browser sind tolerant und stellen diesen Code trotzdem korrekt dar, aber es ist eine schlechte Praxis und kann in manchen Systemen (z. B. XML-Parsern) zu Problemen führen. Wenn du eine Trennlinie in einem Kommentar benötigst, verwende stattdessen Gleichheitszeichen (`===`) oder einzelne Bindestriche mit Leerzeichen (`- - -`).

#### Ein Blick zurück: Bedingte Kommentare

Wenn du jemals an älteren Webseiten arbeitest, könntest du auf eine seltsame Art von Kommentar stoßen, die so aussieht:

```html
<!--[if IE 9]>
  <link rel="stylesheet" type="text/css" href="ie9-styles.css">
<![endif]-->
```

Dies ist ein sogenannter "bedingter Kommentar" (Conditional Comment). Es war eine Microsoft-spezifische Erweiterung für den Internet Explorer (IE). Sie erlaubte es Entwicklern, bestimmten HTML-Code nur für bestimmte Versionen des IE zu laden. In der Vergangenheit war dies ein wichtiges Werkzeug, um die zahlreichen Fehler und Eigenheiten dieses Browsers zu umgehen.

Da der Internet Explorer heute nicht mehr relevant ist, **solltest du bedingte Kommentare in neuen Projekten nicht mehr verwenden.** Sie sind ein Relikt der Vergangenheit, aber es ist gut zu wissen, was sie sind, falls du ihnen in der Wildnis begegnest.
