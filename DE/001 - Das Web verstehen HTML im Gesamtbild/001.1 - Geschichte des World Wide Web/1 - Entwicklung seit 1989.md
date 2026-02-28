# Entwicklung seit 1989

### Entwicklung seit 1989: Vom Forschungsprojekt zum globalen Netz

Stell dir vor, es ist das Jahr 1989. Die Welt ist eine andere: Das Internet existiert zwar schon als Netzwerk für Militär und Universitäten, aber es ist unübersichtlich und schwer zu bedienen. Es gibt keine einfache Möglichkeit, Informationen zu durchsuchen und miteinander zu verknüpfen. Genau dieses Problem wollte ein britischer Physiker namens Tim Berners-Lee am europäischen Kernforschungszentrum CERN in der Schweiz lösen. Er war frustriert davon, wie schwierig es war, Forschungsergebnisse zwischen Tausenden von Mitarbeitern auszutauschen, die auf unterschiedlichen Computersystemen arbeiteten.

Seine Idee, die er in einem Aufsatz mit dem Titel "Information Management: A Proposal" vorstellte, war revolutionär und doch verblüffend einfach: ein System, das auf Hypertext basiert. Dokumente sollten nicht mehr isoliert existieren, sondern durch "Links" miteinander verbunden sein, sodass man von einer Information zur nächsten springen konnte. Um diese Vision umzusetzen, entwickelte er drei grundlegende Technologien, die bis heute das Fundament des Webs bilden:

1.  **HTML (HyperText Markup Language):** Die Sprache, mit der man die Struktur von Webdokumenten beschreibt – also was eine Überschrift ist, was ein Absatz und was ein Link.
2.  **URI (Uniform Resource Identifier):** Eine eindeutige Adresse für jede Ressource im Netz. Heute kennen wir sie meist als URL (Uniform Resource Locator).
3.  **HTTP (Hypertext Transfer Protocol):** Das Protokoll, das festlegt, wie Browser und Server miteinander kommunizieren, um HTML-Dokumente und andere Ressourcen anzufordern und zu übertragen.

1991 ging die erste Website der Welt online: `info.cern.ch`. Sie war extrem schlicht und bestand nur aus Text und Links. Sie erklärte, was das World Wide Web ist und wie man es benutzen kann. Doch dieser unscheinbare Anfang war der Startschuss für eine digitale Revolution.

#### Die Explosion der 90er-Jahre und die Browserkriege

Zunächst war das Web ein Werkzeug für Wissenschaftler. Der Wendepunkt für die breite Öffentlichkeit kam 1993 mit dem **Mosaic-Browser**. Er war der erste Browser, der Bilder direkt im Text anzeigen konnte, anstatt sie in einem separaten Fenster zu öffnen. Plötzlich war das Web nicht mehr nur Textwüste, sondern ein visuelles Medium. Das war der Moment, in dem das Web für alle interessant wurde.

Die Entwickler von Mosaic gründeten bald darauf eine Firma und veröffentlichten den **Netscape Navigator**, der schnell zum dominantesten Browser des Planeten wurde. Microsoft erkannte die Gefahr und zog mit dem **Internet Explorer** nach, den es kostenlos mit seinem Betriebssystem Windows bündelte. Damit begann der erste "Browserkrieg".

Dieser Wettstreit hatte zwei Seiten. Einerseits trieb er die Innovationen rasant voran. JavaScript wurde von Netscape erfunden, um Webseiten interaktiv zu machen. CSS (Cascading Style Sheets) wurde vorgeschlagen, um die Gestaltung vom Inhalt zu trennen. Andererseits führte der Krieg zu einem Chaos an proprietären, nicht standardisierten HTML-Tags. Netscape erfand den berüchtigten `<blink>`-Tag, während Microsoft mit dem `<marquee>`-Tag (Laufschrift) konterte. Entwickler waren gezwungen, für jeden Browser eine eigene Version ihrer Website zu bauen, was zu den berüchtigten "Best viewed with..."-Buttons führte.

```html
<!-- Ein Relikt aus der chaotischen Zeit der Browserkriege -->
<html>
  <head>
    <title>Meine coole 90er-Jahre Seite</title>
  </head>
  <body>
    <marquee>Willkommen auf meiner Homepage!</marquee>
    <h1><blink>SUPER WICHTIG!</blink></h1>
    <p>Diese Seite sieht am besten im Netscape Navigator 4 aus.</p>
  </body>
</html>
```

#### Der Ruf nach Standards: Das W3C und der Weg zur Vernunft

Um dieses Chaos zu beenden und das Web als offene, universelle Plattform zu erhalten, gründete Tim Berners-Lee 1994 das **World Wide Web Consortium (W3C)**. Das Ziel des W3C war und ist es, offene Standards für Webtechnologien zu entwickeln.

Ende der 90er-Jahre veröffentlichte das W3C mit **HTML 4.01** einen Meilenstein. Dieser Standard predigte die strikte Trennung von Inhalt (HTML), Präsentation (CSS) und Verhalten (JavaScript). Tags wie `<font>` oder Attribute wie `bgcolor`, die nur für die Optik zuständig waren, galten als veraltet. Stattdessen sollte HTML sich auf die semantische Bedeutung des Inhalts konzentrieren: Was *ist* dieser Text? Eine Überschrift? Eine Liste? Ein Zitat? Wie es aussieht, sollte allein CSS entscheiden.

Anfang der 2000er-Jahre versuchte man, das Web noch sauberer und strenger zu machen. **XHTML 1.0** wurde geboren – eine Neuformulierung von HTML als XML-Anwendung. Jedes Tag musste geschlossen werden, alles musste kleingeschrieben und nach strengen Regeln formuliert sein. Die Idee war gut, aber für viele Webentwickler war der Umstieg zu mühsam, und ein einziger kleiner Fehler konnte dazu führen, dass die gesamte Seite im Browser nicht mehr angezeigt wurde.

#### Das Web 2.0: Nutzer werden zu Gestaltern

Etwa zur Mitte der 2000er-Jahre änderte sich das Web grundlegend. Es war nicht mehr nur ein Ort zum Konsumieren von Informationen, sondern wurde zu einer interaktiven Plattform. Das "Web 2.0" war geboren. Blogs, Wikis (wie Wikipedia) und soziale Netzwerke (wie Facebook) explodierten. Nutzer erstellten nun selbst die Inhalte.

Technisch wurde dies durch eine Technik namens **AJAX (Asynchronous JavaScript and XML)** ermöglicht. AJAX erlaubte es, Daten vom Server nachzuladen, *ohne* die gesamte Seite neu zu laden. Wenn du auf einer Seite einen "Gefällt mir"-Button klickst und sich nur der Zähler ändert, steckt dahinter dieses Prinzip. Webseiten fühlten sich plötzlich an wie richtige Programme direkt im Browser.

In dieser Zeit erstarkten auch die Browser, die auf Webstandards setzten. **Mozilla Firefox**, ein Nachfahre des Netscape Navigators, bot eine starke Alternative zum damals dominierenden, aber in seiner Entwicklung stagnierenden Internet Explorer 6. Später betrat Google mit **Chrome** die Bühne und setzte neue Maßstäbe bei Geschwindigkeit und der Unterstützung moderner Webstandards.

#### Die mobile Revolution und HTML5

Der nächste große Umbruch kam 2007 mit der Vorstellung des ersten iPhones. Plötzlich hatten Millionen von Menschen das Internet in ihrer Hosentasche. Das mobile Surfen wurde zum Massenphänomen. Das stellte das Web vor neue Herausforderungen. Webseiten mussten nun auf kleinen Touchscreens genauso gut funktionieren wie auf großen Monitoren (Stichwort: Responsive Web Design).

Eine weitere Herausforderung war, dass mobile Geräte wie das iPhone auf proprietäre Plugins wie Adobe Flash verzichteten, die damals für fast alle Videos und Animationen im Web verantwortlich waren. Es brauchte eine offene, standardisierte Lösung.

Die Antwort war **HTML5**. Die Arbeit daran begann schon 2004 durch eine Gruppe namens **WHATWG (Web Hypertext Application Technology Working Group)**, die unzufrieden mit dem langsamen Fortschritt und dem Fokus auf XHTML beim W3C war. HTML5 war kein kompletter Neuanfang, sondern eine pragmatische Weiterentwicklung von HTML 4. Es führte eine Fülle neuer, mächtiger Funktionen ein:

*   **Semantische Elemente:** Anstatt seitenweise nur `<div>`-Container zu verwenden, gab es nun sprechende Tags wie `<header>`, `<footer>`, `<nav>`, `<article>` und `<section>`. Das macht den Code nicht nur für Menschen lesbarer, sondern auch für Maschinen (z. B. Suchmaschinen oder Screenreader für Menschen mit Sehbehinderung).

```html
<!-- Struktur einer Seite mit den neuen HTML5-Elementen -->
<body>
  <header>
    <h1>Mein Blog</h1>
    <nav>
      <ul>
        <li><a href="/">Startseite</a></li>
        <li><a href="/ueber-mich">Über mich</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <h2>Ein neuer Beitrag</h2>
      <p>Hier steht der Inhalt des Artikels...</p>
    </article>
  </main>

  <footer>
    <p>&copy; 2023 Mein Name</p>
  </footer>
</body>
```

*   **Multimedia-Tags:** Mit `<video>` und `<audio>` konnten Videos und Tondateien endlich direkt im Browser abgespielt werden, ganz ohne externe Plugins.
*   **Verbesserte Formulare:** Neue Eingabetypen wie `date`, `email` oder `number` brachten eine eingebaute Validierung und bessere Bedienbarkeit, vor allem auf mobilen Geräten.
*   **Leistungsstarke APIs:** HTML5 führte Schnittstellen (APIs) für den Zugriff auf Gerätefunktionen wie Geolocation, lokalen Speicher (LocalStorage) oder das Zeichnen von Grafiken direkt im Browser (`<canvas>`) ein.

#### Die Gegenwart: Ein lebendiger Standard

HTML ist heute kein starres Regelwerk mehr, das alle paar Jahre eine neue Versionsnummer bekommt. Stattdessen wird es von der WHATWG als **Living Standard** (lebendiger Standard) gepflegt. Das bedeutet, HTML wird kontinuierlich weiterentwickelt. Browser implementieren neue Funktionen, sobald sie stabil sind. Der Fokus liegt auf Pragmatismus, Rückwärtskompatibilität und der Lösung realer Probleme für Entwickler und Nutzer.

Die Reise von einem einfachen Vorschlag am CERN zu dem komplexen, allgegenwärtigen Ökosystem, das wir heute nutzen, ist eine der faszinierendsten Geschichten der modernen Technik. HTML hat sich dabei von einer simplen Auszeichnungssprache für wissenschaftliche Dokumente zu dem robusten Fundament für globale Kommunikation, Unterhaltung und interaktive Anwendungen entwickelt, auf dem unsere digitale Welt ruht.
