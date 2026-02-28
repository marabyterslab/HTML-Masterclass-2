# Einsatz von Kommentaren

### Einsatz von Kommentaren

Stell dir vor, du schreibst ein sehr langes und komplexes HTML-Dokument. Nach einigen Wochen oder Monaten kehrst du zu deinem Code zurück, um eine Änderung vorzunehmen. Wirst du dich noch an jede einzelne Zeile erinnern? Wirst du sofort verstehen, warum du eine bestimmte Struktur gewählt hast oder was ein kryptischer `div`-Block mit der ID `data-cont-ax7` eigentlich bezweckt? Wahrscheinlich nicht. Und genau hier kommen Kommentare ins Spiel.

Kommentare sind Notizen, die du direkt in deinem HTML-Code hinterlässt. Sie sind für dich und andere Entwickler gedacht, die deinen Code lesen. Der Browser ignoriert sie vollständig. Das bedeutet, ein Besucher deiner Webseite wird sie niemals sehen – es sei denn, er schaut sich gezielt den Quelltext der Seite an. Kommentare sind also eine essenzielle Form der Kommunikation: mit deinem zukünftigen Ich und mit deinem Team. Sie sind das Schmiermittel für wartbaren und verständlichen Code.

#### Die Anatomie eines HTML-Kommentars

Die Syntax für einen Kommentar in HTML ist einfach und unverkennbar. Er beginnt mit `<!--` und endet mit `-->`. Alles, was du zwischen diese beiden Markierungen schreibst, wird vom Browser als Kommentar behandelt und nicht auf der Webseite dargestellt.

Hier ist ein einfaches Beispiel:

```html
<!-- Dies ist ein einfacher Kommentar. Er wird auf der Webseite nicht angezeigt. -->
<p>Dieser Text ist jedoch für jeden sichtbar.</p>
```

Ein Kommentar kann sich über eine oder mehrere Zeilen erstrecken. Es gibt keine separate Syntax für einzeilige oder mehrzeilige Kommentare, was die Handhabung sehr flexibel macht.

```html
<!--
  Dies ist ein mehrzeiliger Kommentar.
  Er eignet sich hervorragend, um komplexere Sachverhalte
  oder ganze Code-Blöcke zu erklären.
-->
```

Eine wichtige Regel, die du beachten solltest: Verschachtele keine Kommentare. Das bedeutet, du kannst nicht einen Kommentar innerhalb eines anderen Kommentars platzieren. Die meisten modernen Browser kommen damit zwar irgendwie zurecht, aber es ist ungültiges HTML und kann zu unvorhersehbarem Verhalten führen. Der erste `-->`, den der Browser findet, beendet den gesamten Kommentarblock.

Ebenso solltest du die Zeichenfolge `--` innerhalb des Kommentarinhalts vermeiden. Auch dies ist technisch nicht erlaubt und kann, obwohl moderne Browser tolerant sind, in älteren Systemen oder bei manchen Werkzeugen zu Problemen führen.

**Falsch:**
```html
<!-- Dies ist ein <!-- verschachtelter --> Kommentar. Das funktioniert nicht! -->
```

**Besser vermeiden:**
```html
<!-- Bitte beachte die folgende Anweisung--sie ist wichtig. -->
```

#### Warum du Kommentare verwenden solltest: Die vier Hauptgründe

Kommentare sind kein Selbstzweck. Sie sollten strategisch eingesetzt werden, um den Code besser zu machen. Es gibt vier primäre Anwendungsfälle, in denen Kommentare Gold wert sind.

##### 1. Code erklären und dokumentieren

Dies ist der klassischste Anwendungsfall. Manchmal ist HTML-Code nicht selbsterklärend. Vielleicht hast du eine komplizierte Verschachtelung von Elementen erstellt, um einen bestimmten visuellen Effekt zu erzielen, oder du verwendest eine spezifische `id` oder `class`, die mit einem komplexen JavaScript-Skript interagiert. Ein kurzer Kommentar kann hier den entscheidenden Kontext liefern.

```html
<!--
  Wichtiger Hinweis: Die folgende `div`-Struktur ist für das
  CSS-Grid des Hauptlayouts notwendig. Die Klasse "promo-box-special"
  löst eine spezielle Animation aus, die in `animations.js` definiert ist.
-->
<div id="promo-container" class="promo-box-special">
  <!-- ... Inhalt der Promo-Box ... -->
</div>
```

Eine gängige Konvention unter Entwicklern ist die Verwendung von speziellen Schlüsselwörtern wie `TODO` oder `FIXME`, um auf offene Aufgaben oder bekannte Probleme im Code hinzuweisen.

*   **`TODO`**: Markiert eine Stelle, an der noch etwas implementiert werden muss.
*   **`FIXME`**: Weist auf einen bekannten Fehler hin, der behoben werden muss.

```html
<!-- TODO: Den Platzhalter-Text durch den echten Inhalt vom CMS ersetzen. -->
<p>Lorem ipsum dolor sit amet...</p>

<!-- FIXME: Diese Tabelle ist auf mobilen Geräten nicht korrekt responsiv. -->
<table>
  <!-- ... Tabellendaten ... -->
</table>
```

##### 2. Code vorübergehend deaktivieren (Auskommentieren)

Einer der praktischsten Einsatzzwecke für Kommentare ist das Debugging. Stell dir vor, ein Teil deiner Webseite funktioniert nicht richtig, und du vermutest, dass ein bestimmter HTML-Block das Problem verursacht. Anstatt den Code zu löschen und ihn später mühsam wiederherzustellen, kannst du ihn einfach "auskommentieren".

Dazu setzt du den gesamten Block zwischen die Kommentar-Tags `<!--` und `-->`. Der Browser wird diesen Teil des Codes ignorieren, als wäre er nicht da. So kannst du schnell testen, ob deine Vermutung richtig war, ohne den Code dauerhaft zu entfernen.

```html
<h1>Willkommen auf unserer Webseite</h1>

<!--
  Der folgende Slider verursacht aktuell einen Anzeigefehler.
  Ich deaktiviere ihn vorübergehend, um das Problem zu untersuchen.

<div class="image-slider">
  <img src="bild1.jpg" alt="Erstes Bild">
  <img src="bild2.jpg" alt="Zweites Bild">
</div>
-->

<p>Hier geht der restliche Inhalt der Seite weiter.</p>
```

Wenn du den Fehler gefunden und behoben hast, entfernst du einfach die Kommentar-Tags, und der Code ist wieder aktiv. Diese Technik ist ein unverzichtbares Werkzeug im Alltag eines jeden Webentwicklers.

##### 3. Deinen Code strukturieren

Bei sehr langen und umfangreichen HTML-Dateien kann es schnell unübersichtlich werden. Kommentare eignen sich hervorragend, um dein Dokument in logische Abschnitte zu unterteilen. Sie dienen als visuelle Anker und Überschriften direkt im Code, die dir helfen, dich schneller zurechtzufinden.

Du kannst zum Beispiel den Anfang und das Ende großer Bereiche wie des Headers, der Navigation oder des Footers markieren.

```html
<body>

  <!-- ================================================================= -->
  <!-- START: Hauptnavigation (Header)                                   -->
  <!-- ================================================================= -->
  <header>
    <nav>
      <!-- ... Navigationslinks ... -->
    </nav>
  </header>
  <!-- ================================================================= -->
  <!-- END: Hauptnavigation (Header)                                     -->
  <!-- ================================================================= -->


  <main>
    <!-- ... Hauptinhalt der Seite ... -->
  </main>


  <!-- ================================================================= -->
  <!-- START: Fußzeile (Footer)                                          -->
  <!-- ================================================================= -->
  <footer>
    <p>&copy; 2023 Meine Webseite</p>
  </footer>
  <!-- ================================================================= -->
  <!-- END: Fußzeile (Footer)                                            -->
  <!-- ================================================================= -->

</body>
```

Diese Art der Strukturierung macht deinen Code nicht nur für dich selbst, sondern auch für Kollegen, die vielleicht zum ersten Mal damit arbeiten, wesentlich lesbarer und zugänglicher.

##### 4. Metadaten und Copyright-Hinweise hinterlassen

Manchmal werden Kommentare auch genutzt, um Metainformationen über das Dokument zu hinterlegen. Das können zum Beispiel der Name des Autors, das Erstellungsdatum oder ein Copyright-Hinweis sein. Auch wenn es dafür oft bessere Orte gibt (z. B. in Versionskontrollsystemen wie Git), ist es eine gängige Praxis.

```html
<!--
  Autor: Max Mustermann
  Erstellt am: 15.10.2023
  Letzte Änderung: 22.11.2023
  Projekt: HTML-Masterclass Webseite
-->
```

#### Die Kunst des richtigen Kommentierens: Was du vermeiden solltest

So nützlich Kommentare auch sind, ihr übermäßiger oder falscher Gebrauch kann mehr schaden als nutzen. Guter Code sollte so weit wie möglich selbsterklärend sein. Ein Kommentar sollte das "Warum" erklären, nicht das "Was".

**Vermeide redundante Kommentare:**
Ein Kommentar, der nur das wiederholt, was der Code bereits offensichtlich aussagt, ist überflüssig und bläht den Code nur auf.

**Schlecht:**
```html
<!-- Dies ist ein Absatz -->
<p>Ein Textabsatz.</p>
```

**Gut:**
```html
<!-- Dieser Absatz wird nur angezeigt, wenn der Benutzer eingeloggt ist,
     gesteuert durch die serverseitige Logik. -->
<p>Willkommen zurück, lieber Benutzer!</p>
```

**Halte Kommentare aktuell:**
Ein veralteter Kommentar ist schlimmer als gar kein Kommentar. Wenn du den Code änderst, musst du unbedingt auch die zugehörigen Kommentare anpassen. Ein Kommentar, der eine Funktionalität beschreibt, die nicht mehr existiert, führt Entwickler in die Irre und kostet wertvolle Zeit.

**Das größte Tabu: Sensible Informationen**
Dies ist der wichtigste Punkt, den du dir merken musst: **HTML-Kommentare sind öffentlich!** Jeder kann sie sehen, indem er im Browser auf "Seitenquelltext anzeigen" klickt.

Platziere deshalb **niemals** sensible Daten in Kommentaren. Dazu gehören:
*   Passwörter oder Zugangsdaten
*   API-Schlüssel
*   Interne Notizen über Kunden oder unfertige Geschäftsstrategien
*   Server-Pfade oder Datenbankinformationen
*   Jegliche Art von vertraulichen Informationen

Stell dir Kommentare immer wie Notizen auf einem Post-it vor, das du an einen öffentlichen Aushang klebst. Schreibe nur dorthin, was jeder lesen darf.

#### Ein Blick in die Vergangenheit: Bedingte Kommentare

Wenn du mit älteren Webseiten oder E-Mail-Templates arbeitest, könntest du auf eine besondere Art von Kommentaren stoßen: bedingte Kommentare (Conditional Comments). Dies war eine spezielle Syntax, die nur vom Internet Explorer (IE) von Version 5 bis 9 interpretiert wurde. Sie erlaubte es Entwicklern, bestimmte HTML-Blöcke nur für bestimmte IE-Versionen zu laden, um dessen zahlreiche Darstellungsfehler und Eigenheiten zu umgehen.

Ein Beispiel sah so aus:

```html
<!--[if IE 8]>
  <p>Du verwendest den veralteten Internet Explorer 8. Bitte aktualisiere deinen Browser.</p>
  <link rel="stylesheet" type="text/css" href="ie8-fixes.css">
<![endif]-->
```

Diese Technik ist heute **obsolet** und sollte in der modernen Webentwicklung nicht mehr verwendet werden, da der Internet Explorer nicht mehr unterstützt wird. Es ist jedoch nützlich, diese Syntax zu kennen, falls du sie in einem alten Projekt entdeckst. Du weißt dann, dass es sich um einen historischen Hack handelt, um mit den Problemen eines längst vergangenen Browsers umzugehen.
