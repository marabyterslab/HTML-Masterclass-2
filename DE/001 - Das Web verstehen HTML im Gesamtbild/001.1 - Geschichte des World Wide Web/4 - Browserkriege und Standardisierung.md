# Browserkriege und Standardisierung

### Browserkriege und Standardisierung

Stell dir eine Zeit vor, in der das World Wide Web noch jung war. Ein offener, fast akademischer Raum, in dem das Teilen von Informationen im Vordergrund stand. Die ersten Browser, wie der von Tim Berners-Lee entwickelte WorldWideWeb (später Nexus) oder der bahnbrechende NCSA Mosaic, hatten ein gemeinsames Ziel: Inhalte für alle zugänglich zu machen, egal welches System sie nutzten. Die Regeln waren einfach, HTML war überschaubar, und die Vision war eine von universeller Kompatibilität. Doch diese idealistische Phase sollte nicht lange andauern.

#### Der erste Browserkrieg: Netscape gegen Microsoft

Mitte der 1990er Jahre erkannte die Welt das kommerzielle Potenzial des Internets. Aus dem Team, das Mosaic entwickelt hatte, ging die Firma Netscape hervor und veröffentlichte 1994 den Netscape Navigator. Dieser Browser war schnell, innovativ und eroberte den Markt im Sturm. Zeitweise hielt Netscape einen Marktanteil von über 90 %. Das Web *war* quasi Netscape.

Dieser Erfolg blieb in Redmond, dem Hauptsitz von Microsoft, nicht unbemerkt. Microsoft erkannte die Gefahr: Wenn das Web zur zentralen Plattform würde, könnte die Dominanz des Windows-Betriebssystems an Bedeutung verlieren. Die Antwort ließ nicht lange auf sich warten: der Internet Explorer (IE).

Was folgte, war der erste "Browserkrieg" – ein erbitterter Kampf um die Vorherrschaft im Web. Es war jedoch kein Kampf, der mit besseren Produkten für den Nutzer geführt wurde, sondern mit einer Strategie der Spaltung. Beide Unternehmen begannen, HTML eigenmächtig um neue, proprietäre (also herstellerspezifische) Tags und Funktionen zu erweitern. Das Ziel war, Entwickler an die eigene Plattform zu binden.

Netscape führte zum Beispiel den berüchtigten `<blink>`-Tag ein, der Text auf der Webseite blinken ließ. Microsoft konterte mit dem `<marquee>`-Tag, der Text über den Bildschirm laufen ließ. Was heute wie eine Spielerei klingt, war damals ein ernstes Problem. Wenn du als Entwickler eine Webseite gebaut hast, musstest du dich entscheiden: Optimierst du sie für Netscape oder für den Internet Explorer?

```html
<!-- Dieser Code funktionierte nur in Netscape Navigator -->
<p>
  Willkommen auf meiner Webseite! <blink>Neuigkeiten hier!</blink>
</p>

<!-- Und dieser nur im Internet Explorer -->
<marquee direction="up" height="100">
  Sonderangebote laufen nach oben!
</marquee>
```

Die Webseite sah in jedem Browser anders aus oder funktionierte teilweise gar nicht. Das Mantra für Webentwickler in dieser Zeit lautete zynisch: "Write once, debug everywhere" – einmal schreiben, überall Fehler beheben. Die Inkompatibilitäten beschränkten sich nicht auf HTML. Auch bei JavaScript gab es massive Unterschiede. Microsoft entwickelte eine eigene Version namens JScript, die sich in vielen Details von Netscapes JavaScript unterschied. Die Folge war ein Wirrwarr aus browserspezifischen Code-Abfragen, um die einfachsten interaktiven Funktionen umzusetzen.

Microsoft hatte jedoch einen entscheidenden Vorteil: den Internet Explorer direkt in das Windows-Betriebssystem zu integrieren. Jeder, der einen Windows-PC kaufte, hatte den IE vorinstalliert. Netscape, das man extra herunterladen und installieren musste, verlor dramatisch an Boden. Um das Jahr 2001 hatte der Internet Explorer den Krieg gewonnen und hielt seinerseits einen Marktanteil von über 95 %.

#### Die dunklen Jahre der Stagnation

Mit dem Sieg im Browserkrieg tat Microsoft etwas, was aus unternehmerischer Sicht vielleicht logisch, für das Web aber katastrophal war: Es stellte die Weiterentwicklung des Internet Explorers praktisch ein. Die Version 6, im Jahr 2001 veröffentlicht, blieb über fünf Jahre lang der De-facto-Standard.

Für Webentwickler war IE6 ein Albtraum. Er war voller Sicherheitslücken, interpretierte Webstandards wie HTML und CSS fehlerhaft und auf seine eigene, unvorhersehbare Weise (das "Box Model" von IE6 ist unter Entwicklern legendär für die Kopfschmerzen, die es verursachte). Da fast alle Nutzer diesen Browser verwendeten, mussten Entwickler unzählige Stunden damit verbringen, ihre Webseiten mit speziellen "Hacks" und Workarounds für diesen einen, veralteten Browser lauffähig zu machen. Das Web stagnierte. Innovation fand kaum noch statt, weil jede neue Idee an der Hürde des IE6 scheiterte.

In dieser Zeit wuchs jedoch der Widerstand. Organisationen wie das World Wide Web Consortium (W3C), gegründet von Tim Berners-Lee, arbeiteten unermüdlich an der Definition offener Standards. Ihre Mission war es, das Web aus der Umklammerung eines einzelnen Unternehmens zu befreien und eine gemeinsame, dokumentierte Grundlage für alle zu schaffen. Die Idee war einfach: Wenn sich alle Browser an dieselben Regeln halten, funktionieren Webseiten überall gleich. Der Entwickler kann sich auf den Inhalt und die Funktion konzentrieren, nicht auf die Macken eines bestimmten Browsers.

#### Der zweite Browserkrieg: Ein Kampf für das offene Web

Aus der Asche von Netscape entstand ein neues Projekt: Mozilla. Angetrieben von einer Community und der Vision eines offenen, standardkonformen Webs, veröffentlichte die Mozilla Foundation im Jahr 2004 den Browser Firefox.

Firefox war ein Paukenschlag. Er war sicherer, schneller, unterstützte Webstandards deutlich besser als der IE6 und brachte Innovationen wie das Tabbed Browsing für die breite Masse. Er war Open Source und wurde zur Speerspitze einer Bewegung, die das Web zurückerobern wollte.

Dies war der Beginn des zweiten Browserkriegs, doch die Spielregeln hatten sich geändert. Es ging nicht mehr darum, das Web durch proprietäre Funktionen zu spalten. Im Gegenteil: Die neuen Konkurrenten übertrumpften sich gegenseitig in der bestmöglichen Unterstützung der offiziellen Webstandards.

*   **Mozilla Firefox** trat als Verfechter der offenen Standards und der Privatsphäre der Nutzer an.
*   **Apple** brachte 2003 **Safari** auf den Markt, basierend auf der Open-Source-Engine WebKit, und machte mit dem iPhone ab 2007 das mobile Surfen populär.
*   **Google** betrat 2008 die Bühne mit **Chrome**, ebenfalls basierend auf WebKit. Chrome setzte neue Maßstäbe bei Geschwindigkeit und Stabilität und führte einen rasanten Update-Zyklus ein, der die Konkurrenz unter Druck setzte.

Microsoft wurde aus seiner Lethargie gerissen und musste reagieren. Nachfolgende Versionen des Internet Explorers (IE7, IE8, IE9) bemühten sich langsam, den Anschluss an die Standards zu finden, aber der Ruf war ruiniert und der technologische Rückstand enorm.

#### Die Ära der Standardisierung und der "Evergreen"-Browser

Der zweite Browserkrieg führte zu einem positiven Ergebnis: Die Konkurrenz zwang alle Hersteller, sich den Webstandards des W3C und später der WHATWG (Web Hypertext Application Technology Working Group) anzunähern. Die WHATWG, gegründet von Entwicklern von Apple, Mozilla und Opera, trieb die Entwicklung von HTML5 als "lebendigen Standard" voran – eine pragmatische Weiterentwicklung, die auf den realen Bedürfnissen des Webs basierte.

Heute leben wir in einer weitgehend friedlichen Ära. Die großen Browser – Chrome, Firefox, Safari und Microsofts neuer Edge-Browser (der mittlerweile ebenfalls auf Googles Chromium-Technologie basiert) – sind sich in ihrer Interpretation von HTML, CSS und JavaScript sehr ähnlich. Die Zeiten, in denen du eine komplett andere Webseite für jeden Browser bauen musstest, sind größtenteils vorbei.

Ein entscheidender Faktor dafür ist das Konzept der "Evergreen"-Browser. Anders als früher, als Nutzer jahrelang mit einer veralteten Version arbeiteten, aktualisieren sich moderne Browser automatisch und leise im Hintergrund. Das bedeutet, dass die meisten Menschen immer eine aktuelle, sichere und standardkonforme Version nutzen.

Für dich als zukünftiger Webentwickler ist diese Geschichte von entscheidender Bedeutung. Sie erklärt, warum Webstandards so wichtig sind. Sie sind das Fundament, das sicherstellt, dass deine Arbeit auf Milliarden von Geräten weltweit zugänglich und nutzbar ist. Die Kriege sind vielleicht vorbei, aber die Wachsamkeit für ein offenes und interoperables Web bleibt die gemeinsame Verantwortung von Browserherstellern und Entwicklern wie dir.
