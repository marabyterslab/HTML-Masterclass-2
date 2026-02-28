# Einsatz von Kommentaren

### Kommentare in HTML: Die unsichtbaren Helfer in deinem Code

Stell dir vor, du schreibst ein langes, komplexes HTML-Dokument. Du arbeitest tagelang daran, fügst neue Abschnitte hinzu, verschiebst Elemente und baust eine ausgeklügelte Struktur auf. Nach ein paar Wochen oder Monaten schaust du dir den Code erneut an, um eine kleine Änderung vorzunehmen. Plötzlich stehst du vor einem Rätsel: Warum hast du diesen `<div>`-Container an genau dieser Stelle platziert? Welche Funktion hatte dieser kompliziert verschachtelte Block noch mal?

Genau hier kommen Kommentare ins Spiel. Sie sind Notizen, die du direkt in deinem HTML-Code hinterlassen kannst. Das Besondere daran: Der Webbrowser ignoriert sie vollständig. Sie werden auf der Webseite nicht angezeigt und haben keinerlei Einfluss auf die Darstellung oder Funktion. Sie existieren einzig und allein für die Menschen, die den Code lesen – also für dich in der Zukunft oder für deine Kollegen im Team.

Die Syntax für einen HTML-Kommentar ist einfach und unverkennbar:

```html
<!-- Das hier ist ein Kommentar. Alles zwischen diesen Zeichen wird vom Browser ignoriert. -->
```

Ein Kommentar beginnt mit `<!--` (eine öffnende spitze Klammer, ein Ausrufezeichen und zwei Bindestriche) und endet mit `-->` (zwei Bindestriche und eine schließende spitze Klammer). Alles, was sich dazwischen befindet, ist Teil des Kommentars. Das können einzelne Wörter, ganze Sätze oder sogar mehrere Zeilen sein.

```html
<!-- 
  Dies ist ein mehrzeiliger Kommentar.
  Er eignet sich hervorragend, um komplexere Sachverhalte
  oder ganze Code-Blöcke zu erläutern.
-->
```

#### Warum solltest du Kommentare verwenden?

Auf den ersten Blick mag es wie zusätzliche Arbeit erscheinen, neben dem eigentlichen Code auch noch Erklärungen zu schreiben. Doch in der Praxis sind gut gesetzte Kommentare von unschätzbarem Wert. Sie erfüllen mehrere wichtige Funktionen.

##### 1. Dein Gedächtnis als Entwickler

Der häufigste Grund für Kommentare ist, dir selbst eine Gedächtnisstütze zu hinterlassen. Du triffst während der Entwicklung unzählige kleine und große Entscheidungen. Ein Kommentar kann den Kontext für eine solche Entscheidung festhalten.

Nehmen wir an, du musst aus technischen Gründen eine unübliche Lösung für ein Navigationsmenü implementieren. Ohne einen Kommentar würdest du dich in sechs Monaten vielleicht fragen, warum du diesen „komischen“ Code geschrieben hast, und ihn fälschlicherweise durch eine scheinbar einfachere, aber in diesem speziellen Fall nicht funktionierende Variante ersetzen.

```html
<!-- 
  Wichtiger Hinweis: Dieses Dropdown-Menü muss eine feste Höhe von 300px haben,
  da ein externes JavaScript-Plugin sonst die Position falsch berechnet.
  Nicht ändern, ohne das Plugin "external-menu.js" zu prüfen!
-->
<div class="dropdown-menu" style="height: 300px;">
  <!-- ... Menüpunkte ... -->
</div>
```
Dieser Kommentar bewahrt dein Zukunfts-Ich vor stundenlangem Debugging.

##### 2. Kommunikation im Team

Selten arbeitet man allein an einem Webprojekt. Kommentare sind ein zentrales Werkzeug für die Zusammenarbeit. Sie ermöglichen es dir, deinen Teammitgliedern zu erklären, was ein bestimmter Code-Abschnitt tut und vor allem, *warum* er es tut. Das ist besonders wichtig bei komplexen oder nicht sofort ersichtlichen Code-Teilen. Anstatt dass jeder Kollege den Code von Grund auf analysieren muss, kann er einfach deinen Kommentar lesen und versteht sofort die Absicht dahinter.

##### 3. Temporäres Auskommentieren von Code

Eine extrem nützliche Anwendung von Kommentaren ist das "Auskommentieren" von Code. Stell dir vor, du möchtest testen, wie deine Seite ohne einen bestimmten Bereich aussieht, zum Beispiel ohne die Seitenleiste. Anstatt den gesamten HTML-Block zu löschen (und ihn später mühsam wiederherstellen zu müssen), kannst du ihn einfach in einen Kommentar verwandeln.

```html
<main>
  <h1>Willkommen auf unserer Webseite</h1>
  <p>Dies ist der Hauptinhalt.</p>

  <!-- Seitenleiste vorübergehend deaktiviert, um das Layout zu testen.
  <!--
  <aside>
    <h2>Neuigkeiten</h2>
    <p>Hier stehen die neuesten Nachrichten.</p>
  </aside>
  -->

</main>
```
Der Browser wird den `<aside>`-Block nun komplett ignorieren, als wäre er nicht da. Um ihn wieder zu aktivieren, entfernst du einfach die Kommentarzeichen `<!--` und `-->`. Diese Technik ist ein unverzichtbares Werkzeug beim Testen und bei der Fehlersuche (Debugging).

##### 4. Strukturierung des Dokuments

Bei sehr langen HTML-Dateien kann es schwierig werden, den Überblick zu behalten. Du kannst Kommentare verwenden, um visuelle Trennlinien und Überschriften in deinem Code zu erzeugen. Das hilft dir, schnell zu dem Abschnitt zu navigieren, den du bearbeiten möchtest.

```html
<body>

  <!-- ====================================================== -->
  <!-- Header-Bereich: Logo und Hauptnavigation               -->
  <!-- ====================================================== -->
  <header>
    <!-- ... -->
  </header>

  <!-- ====================================================== -->
  <!-- Hauptinhaltsbereich mit Artikeln                       -->
  <!-- ====================================================== -->
  <main>
    <!-- ... -->
  </main>

  <!-- ====================================================== -->
  <!-- Footer-Bereich: Copyright und Kontaktinformationen     -->
  <!-- ====================================================== -->
  <footer>
    <!-- ... -->
  </footer>

</body>
```
Solche strukturierenden Kommentare machen deinen Code deutlich lesbarer und wartbarer.

#### Die Kunst des guten Kommentierens: Was du vermeiden solltest

So nützlich Kommentare auch sind, es gibt auch Fallstricke. Schlechte oder falsche Kommentare können mehr schaden als nutzen.

##### Kommentiere das „Warum“, nicht das „Was“

Ein häufiger Anfängerfehler ist es, Kommentare zu schreiben, die nur beschreiben, was der Code ohnehin schon selbsterklärend tut.

```html
<!-- Ein Absatz-Tag -->
<p>Hallo Welt!</p>
```

Dieser Kommentar ist nutzlos. Jeder, der HTML liest, weiß, dass `<p>` ein Absatz ist. Ein guter Kommentar erklärt die Absicht, die hinter dem Code steckt, oder den Grund für eine ungewöhnliche Entscheidung.

```html
<!-- 
  Dieser Absatz wird für Screenreader-Nutzer versteckt,
  da die Information im folgenden Bild bereits enthalten ist.
-->
<p class="visually-hidden">Eine Grafik mit den neuesten Verkaufszahlen.</p>
```
Dieser Kommentar ist wertvoll, denn er erklärt, *warum* eine bestimmte CSS-Klasse verwendet wird.

##### Halte Kommentare aktuell

Ein veralteter Kommentar ist schlimmer als kein Kommentar. Wenn du den Code änderst, musst du unbedingt auch die dazugehörigen Kommentare anpassen. Stellt ein Kommentar eine Funktionalität in Aussicht, die längst entfernt wurde, führt das zu massiver Verwirrung.

##### Gib keine sensiblen Informationen preis

Dies ist eine goldene Regel: **Schreibe niemals Passwörter, API-Schlüssel, interne Notizen oder andere sensible Daten in HTML-Kommentare!**

Obwohl Kommentare auf der Webseite nicht sichtbar sind, werden sie vollständig an den Browser des Nutzers übertragen. Jeder kann sie mit einem Rechtsklick und „Seitenquelltext anzeigen“ (oder über die Entwicklertools) im Klartext lesen.

```html
<!-- FALSCH! NIEMALS SO ETWAS MACHEN! -->
<!-- Temporärer Zugang für den Admin: user: admin, pass: Start123 -->
```
Solche Informationen in deinem Quellcode sind ein enormes Sicherheitsrisiko.

##### Vorsicht bei der Verschachtelung

HTML-Kommentare können nicht ineinander verschachtelt werden. Der Browser beendet den Kommentar beim ersten Vorkommen von `-->`.

```html
<!-- Äußerer Kommentar Start
  <p>Ein bisschen Text.</p>
  <!-- Innerer Kommentar -->  <-- Dieser schließt den äußeren Kommentar!
  <p>Dieser Text wird wieder angezeigt!</p>
--> <-- Dieses Zeichen ist jetzt ungültig und kann zu Fehlern führen.
```
In diesem Beispiel würde der Browser den Kommentar bereits nach `<!-- Innerer Kommentar -->` beenden. Der Text „Dieser Text wird wieder angezeigt!“ wäre plötzlich wieder Teil des aktiven HTML-Codes.

#### Eine historische Randnotiz: Conditional Comments

Früher, in den Zeiten des Internet Explorers (insbesondere Version 9 und älter), gab es eine spezielle Art von Kommentaren, die sogenannten „Conditional Comments“. Sie sahen fast wie normale Kommentare aus, wurden aber von bestimmten Browser-Versionen als Anweisungen interpretiert.

```html
<!--[if IE 9]>
  <link rel="stylesheet" type="text/css" href="ie9-styles.css">
<![endif]-->
```
Dieser Code würde nur vom Internet Explorer 9 gelesen werden, der dann die spezielle CSS-Datei `ie9-styles.css` lädt. Alle anderen Browser hätten dies als normalen Kommentar behandelt.

**Wichtig:** Diese Technik ist heute komplett veraltet und sollte in modernen Webprojekten nicht mehr verwendet werden. Sie ist jedoch ein interessantes Beispiel dafür, wie Kommentare in der Vergangenheit kreativ für technische Lösungen genutzt wurden.
