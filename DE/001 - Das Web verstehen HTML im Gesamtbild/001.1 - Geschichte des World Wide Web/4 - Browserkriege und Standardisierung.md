# Browserkriege und Standardisierung

### Browserkriege und Standardisierung: Der Kampf um die Seele des Webs

Wenn du heute eine Webseite baust, kannst du dich mit hoher Wahrscheinlichkeit darauf verlassen, dass sie in Chrome, Firefox, Safari und Edge mehr oder weniger identisch aussieht und funktioniert. Das ist eine Errungenschaft, die alles andere als selbstverständlich ist. Sie ist das Ergebnis eines langen, turbulenten Kampfes, der als die „Browserkriege“ in die Geschichte eingegangen ist – ein Kampf, der das Web geformt hat, wie wir es heute kennen.

#### Die Pioniere und der erste Funke

In den allerersten Tagen des Webs gab es keine Kriege. Es gab nur eine Vision. Tim Berners-Lee entwickelte nicht nur HTML, HTTP und URLs, sondern auch den ersten Browser, den er passenderweise „WorldWideWeb“ nannte. Er war Browser und Editor in einem. Doch das Web explodierte erst richtig mit der Ankunft von Mosaic im Jahr 1993. Mosaic war der erste Browser, der Bilder direkt im Text anzeigen konnte und eine grafische Benutzeroberfläche bot, die auch für Laien verständlich war. Plötzlich war das Web nicht mehr nur ein Werkzeug für Wissenschaftler, sondern ein Ort zum Entdecken.

Die Entwickler von Mosaic erkannten das gewaltige Potenzial. Ein Teil des Teams gründete eine Firma namens Netscape Communications und brachte 1994 den Netscape Navigator auf den Markt. Dieser Browser war schneller, stabiler und innovativer als alles, was es bisher gab. Innerhalb kürzester Zeit eroberte er über 90 % des Marktes. Für die meisten Menschen war Netscape Navigator *das* Internet. Wenn du „ins Netz“ gingst, hast du das blaue „N“-Logo angeklickt.

#### Der erste Browserkrieg: Netscape gegen Microsoft

In Redmond, dem Hauptquartier von Microsoft, hatte man das Internet anfangs verschlafen. Man setzte auf eigene Onlinedienste wie MSN. Doch der kometenhafte Aufstieg von Netscape war ein Weckruf. Microsoft erkannte, dass der Browser das Tor zu einer neuen digitalen Welt war – und wer das Tor kontrolliert, kontrolliert die Welt.

Microsofts Antwort war der Internet Explorer (IE). Die erste Version war kaum der Rede wert, aber Microsoft hatte zwei entscheidende Vorteile: schier unendliche Ressourcen und das Windows-Betriebssystem. Mit dem Start von Windows 95 begann Microsoft, den Internet Explorer aggressiv zu vermarkten und, was noch wichtiger war, ihn kostenlos mit dem Betriebssystem zu bündeln. Netscape kostete Geld. Der Kampf hatte begonnen.

Was folgte, war ein erbitterter Wettlauf um Features. Beide Unternehmen versuchten, Entwickler und Nutzer auf ihre Seite zu ziehen, indem sie ständig neue, proprietäre HTML-Tags und Technologien in ihre Browser einbauten. Netscape erfand JavaScript (ursprünglich LiveScript genannt), um Webseiten dynamisch zu machen, und führte Tags wie `<blink>` ein, die heute als Paradebeispiel für schlechtes Webdesign gelten.

Microsoft zog nach, entwickelte mit JScript eine eigene, zu JavaScript kompatible Sprache und brachte eigene Schöpfungen wie das `<marquee>`-Tag (Laufschrift) und Technologien wie ActiveX in den Browser. Das Web wurde zu einem digitalen Wilden Westen. Für Webentwickler war diese Zeit die Hölle. Du konntest nicht einfach eine Webseite bauen. Du musstest eine Webseite für Netscape Navigator *und* eine für den Internet Explorer bauen. Oft bedeutete das, zwei komplett getrennte Codebasen zu pflegen oder komplexe Skripte zu schreiben, die erkannten, welcher Browser gerade die Seite aufrief, um dann den passenden Code auszuliefern. Ein typisches JavaScript aus dieser Zeit konnte so aussehen:

```js
// So musste man früher auf Elemente zugreifen, um sie zu manipulieren
if (document.all) {
  // Code für den Internet Explorer 4+
  // "document.all" war eine proprietäre Microsoft-Erfindung
  var meinElement = document.all['wichtigesElement'];
  meinElement.style.color = 'blue';
} else if (document.layers) {
  // Code für den Netscape Navigator 4
  // "document.layers" war eine proprietäre Netscape-Erfindung
  var meinElement = document.layers['wichtigesElement'];
  meinElement.color = 'blue'; // Ja, die APIs waren auch komplett anders
}
```

Dieser Zustand war unhaltbar. Die Vision eines einzigen, universellen Webs zerbrach in inkompatible Fragmente. Am Ende konnte Netscape dem Druck von Microsoft nicht standhalten. Die kostenlose Integration des IE in Windows, das damals auf über 90 % aller PCs lief, war eine Waffe, gegen die Netscape keine Chance hatte. Um das Jahr 2000 hatte der Internet Explorer den Krieg gewonnen und hielt einen Marktanteil von über 95 %. Netscape war besiegt.

#### Die dunkle Zeit der Stagnation

Nachdem Microsoft den Krieg gewonnen hatte, geschah etwas Paradoxes: Die Innovation hörte auf. Der Internet Explorer 6, 2001 veröffentlicht, wurde zum de-facto-Standard, weil er quasi ein Monopol hatte. Microsoft sah keine Notwendigkeit mehr, den Browser weiterzuentwickeln oder ihn an die offiziellen Webstandards anzupassen, die vom World Wide Web Consortium (W3C) mühsam erarbeitet wurden.

Für Jahre war das Web in der IE6-Ära gefangen. Entwickler mussten sich mit seinen unzähligen Fehlern, Sicherheitslücken und seiner mangelhaften Unterstützung für moderne Standards wie CSS herumschlagen. Anstatt für das offene Web zu programmieren, programmierte man für die Eigenheiten eines einzigen, veralteten Browsers. Das bremste den Fortschritt des gesamten Webs für fast ein halbes Jahrzehnt.

#### Der zweite Browserkrieg und die Wiedergeburt der Standards

Doch aus der Asche von Netscape entstand etwas Neues. Netscape hatte seinen Quellcode kurz vor dem Ende als Open-Source-Projekt freigegeben. Aus diesem Code entstand die Mozilla Foundation, die sich zum Ziel setzte, einen neuen, standardkonformen und nutzerfreundlichen Browser zu schaffen. Im Jahr 2004 veröffentlichten sie Firefox 1.0.

Firefox war ein Paukenschlag. Er war sicherer, bot revolutionäre Features wie Tabbed Browsing und Pop-up-Blocker und hielt sich vor allem an die Webstandards. Entwickler liebten ihn, weil ihr Code einfach funktionierte, ohne spezielle Hacks für einen bestimmten Browser.

Das Aufkommen von Firefox markierte den Beginn des zweiten Browserkriegs. Aber diesmal waren die Regeln anders. Es ging nicht mehr darum, das Web mit proprietären Features zu fragmentieren. Im Gegenteil: Der Wettbewerb drehte sich nun darum, wer die Webstandards am besten, schnellsten und vollständigsten umsetzen konnte.

Andere große Player betraten die Bühne. Apple, das zuvor den Internet Explorer auf seinen Macs ausgeliefert hatte, entwickelte 2003 seinen eigenen Browser, Safari, basierend auf der Open-Source-Engine WebKit. Und 2008 schockierte Google die Welt mit der Veröffentlichung von Chrome. Chrome setzte neue Maßstäbe in Sachen Geschwindigkeit und Stabilität und gewann rasant an Marktanteil. Auch Google setzte auf die WebKit-Engine und trieb die Entwicklung von Webstandards massiv voran. Microsoft geriet unter Druck und musste mit neueren Versionen des Internet Explorers (und später mit seinem Nachfolger Edge) langsam aber sicher auf den Pfad der Standardkonformität zurückkehren.

#### Frieden durch Standardisierung

Heute leben wir in einer relativ friedlichen Ära. Die Browserkriege im alten Stil sind vorbei. Stattdessen gibt es einen gesunden Wettbewerb. Chrome ist zwar der dominante Browser, aber Firefox, Safari und Edge sind starke Konkurrenten. Der entscheidende Unterschied ist, dass sich heute alle großen Browserhersteller zu den gemeinsamen Webstandards bekennen.

Organisationen wie das W3C und die WHATWG (Web Hypertext Application Technology Working Group) definieren, wie HTML, CSS und JavaScript funktionieren sollen. Die Browser-Hersteller arbeiten in diesen Gremien sogar zusammen, um die Zukunft des Webs zu gestalten. Der Wettbewerb findet nun auf einer anderen Ebene statt: Geschwindigkeit, Sicherheit, Entwickler-Tools und Benutzerfreundlichkeit.

Für dich als angehenden Webentwickler ist das ein Segen. Du lernst ein Set an Regeln – HTML, CSS, JavaScript – und kannst darauf vertrauen, dass dein Code in allen modernen Browsern funktioniert. Die Zeiten, in denen du für jeden Browser eine eigene Version deiner Webseite schreiben musstest, sind glücklicherweise vorbei. Die Browserkriege waren eine schmerzhafte, aber notwendige Phase in der Pubertät des Webs. Sie haben uns gelehrt, dass das Web nur dann sein volles Potenzial entfalten kann, wenn es auf offenen, für alle zugänglichen Standards basiert.
