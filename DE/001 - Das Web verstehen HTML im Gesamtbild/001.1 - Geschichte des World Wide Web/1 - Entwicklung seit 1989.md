# Entwicklung seit 1989

### Die Entwicklung seit 1989: Von statischen Dokumenten zur globalen Plattform

Stell dir vor, es ist das Jahr 1989. Die Welt ist eine andere: Das Internet existiert zwar schon in akademischen und militärischen Kreisen, aber es ist ein kompliziertes, textbasiertes Universum, das für die meisten Menschen unzugänglich ist. In Genf, am europäischen Kernforschungszentrum CERN, sitzt ein britischer Physiker namens Tim Berners-Lee und grübelt über ein Problem. Wie können Tausende von Forschern auf der ganzen Welt ihre Ergebnisse und Dokumente einfach und effizient miteinander teilen, ohne dass jeder ein anderes Computersystem oder eine andere Software benutzt?

Seine Lösung war nicht nur eine einzelne Erfindung, sondern ein geniales Trio von Technologien, das die Welt für immer verändern sollte:

1.  **HTML (HyperText Markup Language):** Eine einfache Sprache, um Dokumente zu strukturieren. Mit ihr konnte man Überschriften, Absätze, Listen und vor allem Links definieren.
2.  **URL (Uniform Resource Locator):** Eine eindeutige Adresse für jedes einzelne Dokument im Netzwerk, so wie eine Postanschrift für ein Haus.
3.  **HTTP (Hypertext Transfer Protocol):** Das Regelwerk, das festlegte, wie ein Browser eine URL an einen Server sendet und wie der Server das entsprechende HTML-Dokument zurückschickt.

1991 ging die erste Webseite der Welt online. Sie lief auf einem NeXT-Computer in Berners-Lees Büro und erklärte, was das World Wide Web ist. Sie war einfach, rein textbasiert, aber sie enthielt die revolutionäre Idee des Hyperlinks – ein Wort, auf das du klicken konntest, um zu einem anderen Dokument zu springen. Das war die Geburtsstunde des Webs, wie wir es kennen.

#### Die ersten Browser und der Sprung in die Öffentlichkeit

Zunächst war das Web eine Angelegenheit für Wissenschaftler. Doch das änderte sich 1993 schlagartig. Das CERN gab die Web-Technologie für die Öffentlichkeit frei, ohne Lizenzgebühren. Im selben Jahr veröffentlichte ein Team an der University of Illinois den ersten grafischen Webbrowser: **Mosaic**.

Mosaic war eine Sensation. Er konnte nicht nur Text, sondern auch Bilder direkt auf einer Seite anzeigen. Plötzlich war das Web nicht mehr nur eine Sammlung von Textdokumenten, sondern ein visuelles Medium. Das war der Moment, in dem das Web aus den Universitäten ausbrach und die Fantasie der Öffentlichkeit eroberte. Schnell gründeten Teile des Mosaic-Teams eine Firma und entwickelten den Nachfolger: **Netscape Navigator**. Mitte der 90er-Jahre war Netscape das Synonym für das Surfen im Web.

#### Der erste Browserkrieg: Chaos und Kreativität

Der Erfolg von Netscape rief Microsoft auf den Plan. 1995 veröffentlichte das Unternehmen den **Internet Explorer**, der direkt in das Windows-Betriebssystem integriert war. Damit begann der erste "Browserkrieg". Beide Unternehmen versuchten, die Nutzer mit immer neuen, exklusiven Funktionen auf ihre Seite zu ziehen.

Diese Zeit war wild und chaotisch. Netscape erfand das `<blink>`-Tag, das Text blinken ließ. Microsoft konterte mit dem `<marquee>`-Tag, das Text über den Bildschirm laufen ließ. Jeder Browser interpretierte HTML, CSS (das damals noch in den Kinderschuhen steckte) und das brandneue JavaScript auf seine eigene Weise.

Für Webentwickler war das ein Albtraum. Du musstest deine Webseite oft zweimal bauen – einmal für Netscape und einmal für den Internet Explorer. Es war üblich, auf Webseiten den Hinweis "Optimiert für Netscape Navigator" oder "Best viewed with Internet Explorer" zu finden.

Ein typisches Stück HTML aus dieser Zeit könnte so ausgesehen haben, vollgestopft mit reinen Präsentations-Tags, die heute als schlechter Stil gelten:

```html
<html>
  <body bgcolor="#FFFFFF" text="#000000">
    <center>
      <font size="+3" color="blue">
        Herzlich Willkommen auf meiner Homepage!
      </font>
      <br>
      <marquee>Schaut euch um!</marquee>
    </center>
    <p>
      Hier findet ihr Infos über mein Hobby.
    </p>
  </body>
</html>
```

Inmitten dieses Chaos wurde 1994 das **World Wide Web Consortium (W3C)** unter der Leitung von Tim Berners-Lee gegründet. Das Ziel: das Web vor der Zersplitterung zu bewahren und gemeinsame Standards zu entwickeln, an die sich alle Browserhersteller halten sollten. Es war ein langer, mühsamer Kampf um die Seele des offenen Webs.

#### Die Ära der Webstandards: Ein Ruf nach Ordnung

Ende der 90er-Jahre, nach dem Platzen der Dotcom-Blase, setzte ein Umdenken ein. Unternehmen erkannten, dass das Web mehr war als eine Spielerei. Es war ein ernstzunehmendes Geschäftsfeld, und dafür brauchte man Stabilität, Zuverlässigkeit und Barrierefreiheit. Der Ruf nach Webstandards wurde lauter.

Das W3C veröffentlichte Spezifikationen für HTML 4.01 und später **XHTML 1.0**. XHTML war ein Versuch, HTML strenger und sauberer zu machen, indem man es den Regeln von XML unterwarf. Jeder Tag musste geschlossen werden, alles musste kleingeschrieben werden. Es war eine Reaktion auf den unsauberen Code, der im Browserkrieg entstanden war.

Gleichzeitig wurde die Trennung von Inhalt, Präsentation und Verhalten zur obersten Maxime. Die goldene Regel lautete:

*   **HTML** ist nur für die Struktur und Bedeutung des Inhalts zuständig.
*   **CSS (Cascading Style Sheets)** ist ausschließlich für das Aussehen (Farben, Layout, Schriftarten) verantwortlich.
*   **JavaScript** kümmert sich um die Interaktivität und das Verhalten der Seite.

Diese Trennung machte den Code sauberer, wartbarer und zugänglicher für Menschen mit Behinderungen und für Suchmaschinen.

#### Web 2.0: Du wirst zum Teil des Netzes

Mitte der 2000er-Jahre machte ein neuer Begriff die Runde: **Web 2.0**. Es war weniger eine technische Revolution als ein Wandel in der Nutzung des Webs. Das Web wurde von einem reinen "Read-Only"-Medium zu einer "Read-Write"-Plattform. Es ging nicht mehr nur darum, Informationen zu konsumieren, sondern sie selbst zu erstellen und zu teilen.

Blogs, Wikis (wie Wikipedia), soziale Netzwerke (wie Facebook) und Videoplattformen (wie YouTube) explodierten. Die Technologie, die dies ermöglichte, war **AJAX (Asynchronous JavaScript and XML)**. AJAX erlaubte es einer Webseite, Daten im Hintergrund vom Server nachzuladen, ohne die gesamte Seite neu laden zu müssen. Plötzlich fühlten sich Webseiten an wie Desktop-Anwendungen – schnell, flüssig und interaktiv. Google Maps war eines der ersten Paradebeispiele, das zeigte, was mit dieser Technik möglich war.

#### Die mobile Revolution und das lebendige HTML5

Im Jahr 2007 stellte Apple das erste iPhone vor. Dieses Ereignis veränderte das Web erneut von Grund auf. Plötzlich surften Millionen von Menschen auf kleinen Touchscreens. Webseiten, die für große Monitore und Mauszeiger konzipiert waren, funktionierten auf diesen Geräten nur schlecht oder gar nicht.

Gleichzeitig weigerte sich Apple, die damals weitverbreitete Flash-Technologie von Adobe auf dem iPhone zu unterstützen, die für viele Animationen und Videos im Web verantwortlich war. Dies beschleunigte die Entwicklung eines neuen, mächtigen Webstandards: **HTML5**.

HTML5 war kein radikaler Bruch mit der Vergangenheit, sondern eine pragmatische Weiterentwicklung. Es wurde entwickelt, um die realen Bedürfnisse von modernen Webanwendungen zu erfüllen. Zu den wichtigsten Neuerungen gehörten:

*   **Semantische Tags:** Anstatt deine Seite nur mit `<div>`-Containern zu strukturieren, konntest du jetzt selbsterklärende Tags wie `<header>`, `<footer>`, `<nav>`, `<article>` und `<section>` verwenden. Das macht den Code nicht nur für Menschen lesbarer, sondern auch für Suchmaschinen und Screenreader, die den Inhalt besser interpretieren können.

    *Vorher (mit `div`s):*
    ```html
    <div id="header">...</div>
    <div id="nav">...</div>
    <div class="post">...</div>
    ```

    *Nachher (mit HTML5):*
    ```html
    <header>...</header>
    <nav>...</nav>
    <article>...</article>
    ```

*   **Native Multimedia-Elemente:** Mit den `<video>`- und `<audio>`-Tags konntest du Videos und Tondateien direkt im Browser abspielen, ohne auf externe Plugins wie Flash angewiesen zu sein. Das war der Todesstoß für Flash und ein großer Sieg für offene Webstandards.

*   **Leistungsstarke APIs:** HTML5 brachte eine Fülle von Schnittstellen (APIs) für JavaScript mit, die den Browser in eine vollwertige Anwendungsplattform verwandelten. Dazu gehören die Geolocation API (um den Standort des Nutzers abzufragen), Local Storage (um Daten im Browser zu speichern) oder Canvas (um 2D-Grafiken und Animationen zu zeichnen).

Im Gegensatz zu früheren Versionen wird HTML5 als **"Living Standard"** (lebendiger Standard) von der WHATWG (Web Hypertext Application Technology Working Group) weiterentwickelt. Das bedeutet, es gibt keine großen, starren Versionssprünge mehr wie von HTML4 zu HTML5. Stattdessen wird der Standard kontinuierlich verbessert und um neue Funktionen erweitert, sobald die Browser sie unterstützen.

Die Reise des Webs von 1989 bis heute ist eine faszinierende Geschichte von Innovation, Konkurrenz und dem ständigen Ringen um Offenheit und Standardisierung. Was als einfaches Werkzeug zum Teilen von Forschungsdokumenten begann, hat sich zur wichtigsten Kommunikations- und Informationsplattform der Menschheit entwickelt – und HTML ist und bleibt das fundamentale Skelett, auf dem all das aufgebaut ist.
