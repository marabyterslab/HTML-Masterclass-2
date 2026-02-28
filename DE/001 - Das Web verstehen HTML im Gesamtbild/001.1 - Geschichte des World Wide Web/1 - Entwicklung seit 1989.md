# Entwicklung seit 1989

### Entwicklung seit 1989: Vom Hypertext-Projekt zur globalen Plattform

Stell dir eine Welt ohne das Web vor. Kein schnelles Nachschlagen auf Wikipedia, kein Video-Streaming, keine sozialen Netzwerke. Es ist schwer vorstellbar, doch diese Welt ist gar nicht so lange her. Die Geschichte des World Wide Web, wie du es heute kennst, beginnt 1989 in einem Forschungsinstitut in der Schweiz.

Am CERN, der Europäischen Organisation für Kernforschung, stand der britische Physiker Tim Berners-Lee vor einem Problem: Wissenschaftler aus aller Welt arbeiteten an gemeinsamen Projekten, doch ihre Informationen waren auf unterschiedlichen, inkompatiblen Computersystemen verstreut. Der Austausch war mühsam und ineffizient. Berners-Lees Idee war so einfach wie genial: ein universelles, verknüpftes Informationssystem, das über das Internet zugänglich ist. Er nannte es das „World Wide Web“.

Um diese Vision umzusetzen, entwickelte er drei fundamentale Technologien, die bis heute das Fundament des Webs bilden:

1.  **HTML (Hypertext Markup Language):** Eine einfache Sprache, um Dokumente zu strukturieren und sie miteinander zu verknüpfen (Hyperlinks).
2.  **URL (Uniform Resource Locator):** Eine eindeutige Adresse für jede Ressource im Web, damit man sie finden kann – wie eine Hausanschrift für eine Webseite.
3.  **HTTP (Hypertext Transfer Protocol):** Das Protokoll, also die Sprache, mit der sich Webbrowser und Webserver unterhalten, um HTML-Dokumente anzufordern und zu übertragen.

1991 ging die erste Webseite der Welt online. Sie war schlicht, textbasiert und erklärte, was das World Wide Web ist. Doch der wahre Wendepunkt kam 1993, als das CERN die Web-Technologie für die Öffentlichkeit kostenlos freigab. Diese Entscheidung war monumental. Sie verhinderte, dass das Web von einem einzigen Unternehmen kontrolliert werden konnte, und ebnete den Weg für eine explosive, dezentrale Entwicklung.

#### Der Aufstieg der grafischen Browser und der erste Browserkrieg

Die ersten Webbrowser waren rein textbasiert. Das änderte sich schlagartig 1993 mit der Veröffentlichung von **Mosaic**, dem ersten Browser, der Text und Bilder auf derselben Seite darstellen konnte. Plötzlich war das Web nicht mehr nur für Wissenschaftler interessant, sondern visuell ansprechend und für jedermann zugänglich. Mosaic war der Funke, der das Feuer entfachte.

Kurz darauf, 1994, gründeten einige der Mosaic-Entwickler die Firma Netscape und veröffentlichten den **Netscape Navigator**. Dieser Browser wurde schnell zum Marktführer und definierte, wie die Menschen das frühe Web erlebten. Microsoft erkannte die Bedrohung und zog mit dem **Internet Explorer** nach, den es kostenlos mit seinem Betriebssystem Windows bündelte.

Damit begann der erste „Browserkrieg“ (ca. 1995–2001). Netscape und Microsoft kämpften erbittert um die Vorherrschaft auf dem Browsermarkt. Dieser Wettstreit hatte zwei Seiten: Einerseits trieb er die Innovation rasant voran. Neue HTML-Tags und Funktionen wurden in kürzester Zeit entwickelt. Andererseits führte er zu Chaos. Beide Unternehmen führten eigene, proprietäre HTML-Tags ein, die nur in ihrem jeweiligen Browser funktionierten. Entwickler waren gezwungen, Webseiten doppelt zu bauen oder mit dem berüchtigten Hinweis „Optimiert für Netscape Navigator“ oder „Best viewed with Internet Explorer“ zu versehen. Tags wie `<blink>` (blinkender Text) oder `<marquee>` (Laufschrift) sind heute Relikte aus dieser chaotischen Zeit.

#### Die Geburt von Standards: W3C, CSS und JavaScript

Um diesem Wildwuchs Einhalt zu gebieten, gründete Tim Berners-Lee 1994 das **World Wide Web Consortium (W3C)**. Diese Organisation hatte und hat das Ziel, offene Standards für das Web zu entwickeln und so sicherzustellen, dass es für alle zugänglich und interoperabel bleibt.

In dieser Phase wurden zwei weitere Technologien geboren, die das Web für immer verändern sollten:

**JavaScript (1995):** Ursprünglich von Netscape unter dem Namen „LiveScript“ entwickelt, ermöglichte JavaScript erstmals Interaktivität auf Webseiten. Statt nur statische Dokumente anzuzeigen, konnten Seiten nun auf Benutzereingaben reagieren, Formulare validieren oder Inhalte dynamisch verändern, ohne dass die Seite komplett neu geladen werden musste. Das Web wurde von einem reinen Lesemedium zu einem interaktiven Medium.

**CSS (Cascading Style Sheets, 1996):** Dies war vielleicht die wichtigste Entwicklung für ein sauberes und strukturiertes Web. Vor CSS wurde das Aussehen einer Webseite direkt in HTML definiert. Farben, Schriftgrößen und Layouts wurden mit Tags wie `<font>` oder Attributen wie `bgcolor` festgelegt. Das machte den Code unübersichtlich und schwer zu pflegen.

Stell dir den Unterschied so vor:

**Vor CSS (Styling direkt in HTML):**
```html
<html>
  <body bgcolor="#FFFFFF">
    <center>
      <font color="#FF0000" size="+3">Meine knallrote Überschrift</font>
    </center>
    <p>
      <font color="#0000FF">Dies ist ein blauer Textabsatz.</font>
    </p>
  </body>
</html>
```

CSS ermöglichte die Trennung von Inhalt (HTML) und Präsentation (CSS). Der HTML-Code sollte nur noch die Struktur und die Bedeutung des Inhalts beschreiben, während eine separate CSS-Datei das gesamte Design steuert.

**Nach CSS (Trennung von Struktur und Design):**

*HTML-Datei:*
```html
<html>
  <body>
    <h1>Meine Überschrift</h1>
    <p>Dies ist ein Textabsatz.</p>
  </body>
</html>
```

*CSS-Datei:*
```css
body {
  background-color: #FFFFFF;
}

h1 {
  text-align: center;
  color: #FF0000;
  font-size: 2.5em;
}

p {
  color: #0000FF;
}
```

Diese Trennung war revolutionär. Sie machte Webseiten nicht nur einfacher zu erstellen und zu warten, sondern auch zugänglicher und flexibler. Dasselbe HTML-Dokument konnte mit verschiedenen CSS-Dateien völlig unterschiedlich aussehen, zum Beispiel für den Druck oder für Geräte mit kleinen Bildschirmen.

#### Web 2.0, die mobile Revolution und das semantische Web

Anfang der 2000er-Jahre endete der erste Browserkrieg mit einem klaren Sieg für den Internet Explorer. Doch dessen Entwicklung stagnierte daraufhin für Jahre (Stichwort: Internet Explorer 6). In dieser Zeit erstarkte die Web-Standards-Bewegung. Projekte wie **Mozilla Firefox** (2004) traten als moderne, standardkonforme Alternative an und gewannen schnell an Popularität.

Mitte der 2000er Jahre sprach man vom **Web 2.0**. Dies war kein technischer Standard, sondern ein Paradigmenwechsel: Das Web entwickelte sich von einer Sammlung statischer Seiten zu einer Plattform für dynamische Anwendungen und nutzergenerierte Inhalte. Blogs, soziale Netzwerke wie Facebook und Videoplattformen wie YouTube explodierten. Technisch wurde dies durch **AJAX** (Asynchronous JavaScript and XML) ermöglicht, eine Technik, mit der Webseiten Daten im Hintergrund mit dem Server austauschen konnten, ohne die Seite neu zu laden. Das Nutzererlebnis wurde flüssiger und ähnelte dem von Desktop-Anwendungen.

Der nächste große Umbruch kam 2007 mit der Einführung des ersten **iPhones**. Plötzlich mussten Webseiten nicht mehr nur auf großen Monitoren funktionieren, sondern auch auf kleinen Touchscreens. Die Ära des mobilen Webs hatte begonnen. Technologien wie Adobe Flash, die auf dem Desktop für Animationen und Videos weit verbreitet waren, funktionierten auf dem iPhone nicht und verloren schnell an Bedeutung. Stattdessen setzten sich offene Standards wie HTML, CSS und JavaScript endgültig durch. Konzepte wie **Responsive Web Design** wurden zur Norm – die Idee, eine Website so zu gestalten, dass sie sich flexibel an jede Bildschirmgröße anpasst.

#### Die Ära von HTML5 und das moderne Web

Um den neuen Anforderungen von Web-Anwendungen, Video, Audio und mobilen Geräten gerecht zu werden, begann das W3C mit der Arbeit an **HTML5**. Es war das größte Update für HTML seit Jahren und brachte entscheidende Neuerungen:

*   **Semantische Elemente:** Neue Tags wie `<header>`, `<footer>`, `<nav>`, `<article>` und `<section>` gaben Webseiten eine klarere, maschinenlesbare Struktur.
*   **Multimedia:** Die `<video>`- und `<audio>`-Tags ermöglichten die Einbettung von Medien ohne externe Plugins wie Flash.
*   **Grafik:** Das `<canvas>`-Element bot eine Zeichenfläche für Grafiken und Animationen direkt im Browser, gesteuert durch JavaScript.
*   **Formulare:** Neue Eingabetypen wie `email`, `tel` oder `date` verbesserten die Benutzerfreundlichkeit von Formularen, insbesondere auf mobilen Geräten.

Eine wichtige Veränderung war auch der Entwicklungsprozess selbst. HTML ist heute ein „Living Standard“, der von der **WHATWG (Web Hypertext Application Technology Working Group)** kontinuierlich weiterentwickelt wird. Es gibt keine großen, starren Versionen mehr, sondern stetige, inkrementelle Verbesserungen, die von allen modernen Browsern fortlaufend implementiert werden.

Heute ist das Web allgegenwärtig. Es läuft auf Desktops, Laptops, Tablets, Smartphones, Uhren und Fernsehern. Die Entwicklung wird von mächtigen JavaScript-Frameworks wie React, Angular und Vue.js vorangetrieben, die die Erstellung komplexer Single-Page-Anwendungen ermöglichen. CSS hat mit Flexbox und Grid leistungsstarke Werkzeuge für anspruchsvolle Layouts erhalten.

Die Reise von Tim Berners-Lees ursprünglicher Vision eines einfachen Hypertext-Systems zu der globalen, interaktiven Anwendungsplattform, die wir heute nutzen, ist eine faszinierende Geschichte von Innovation, Konkurrenz und dem gemeinsamen Streben nach offenen Standards. Und im Zentrum von allem steht nach wie vor HTML – die einfache, aber kraftvolle Sprache, die das Skelett für jede einzelne Webseite bildet.
