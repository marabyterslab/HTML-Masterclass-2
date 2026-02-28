# Bedeutung für Screenreader

### Bedeutung für Screenreader: Wenn das Web eine Stimme bekommt

Stell dir für einen Moment vor, du navigierst durch das Internet, aber nicht mit deinen Augen, sondern mit deinen Ohren. Du siehst die Webseiten nicht, du hörst sie. Genau das ist die tägliche Realität für Millionen von Menschen mit Sehbehinderungen. Ihr zentrales Werkzeug, um am digitalen Leben teilzuhaben, ist ein sogenannter Screenreader. Diese Software ist eine Brücke zwischen der visuellen Welt des Internets und der auditiven Wahrnehmung. Ein Screenreader liest Bildschirminhalte vor – Texte, Links, Überschriften, Formularfelder – und ermöglicht so eine Navigation ohne visuellen Kontakt.

Damit diese Brücke stabil und verlässlich ist, braucht sie ein solides Fundament. Einer der wichtigsten Pfeiler dieses Fundaments ist eine scheinbar winzige Information: die Angabe der Sprache, in der eine Webseite geschrieben ist. Was auf den ersten Blick wie ein kleines Detail wirkt, ist für die Nutzerinnen und Nutzer von Screenreadern von fundamentaler Bedeutung. Es entscheidet darüber, ob eine Webseite verständlicher Inhalt oder nur unverständliches Kauderwelsch ist.

#### Das Problem: Eine falsche Aussprache macht Inhalte unbrauchbar

Ein Screenreader ist im Grunde eine hochentwickelte Text-zu-Sprache-Software (Text-to-Speech, TTS). Er verfügt über verschiedene Stimmen und Aussprache-Regelwerke für unterschiedliche Sprachen. Wenn du eine Webseite besuchst, muss der Screenreader wissen, welches dieser Regelwerke er anwenden soll. Woher nimmt er diese Information? Er verlässt sich auf dich, den Entwickler, und auf das, was du im HTML-Code festgelegt hast.

Wenn du die Sprache nicht definierst, muss der Screenreader raten. In den meisten Fällen greift er auf die Standardsprache zurück, die im Betriebssystem des Nutzers oder in den Screenreader-Einstellungen festgelegt ist. Ist ein Nutzer also beispielsweise in den USA ansässig, ist diese Standardsprache in der Regel Englisch.

Stell dir nun vor, dieser Nutzer besucht deine deutschsprachige Webseite, auf der du das `lang`-Attribut vergessen hast. Der Screenreader geht von englischem Text aus und versucht, die deutschen Wörter mit englischen Ausspracheregeln vorzulesen. Das Ergebnis ist bestenfalls komisch und schlimmstenfalls komplett unverständlich.

Ein einfacher deutscher Satz wie:
„Bitte wählen Sie eine der drei Optionen.“

klingt dann plötzlich phonetisch ungefähr so:
*"Beit wäi-len Sie ei-ne der drei Op-ti-o-nen."*

Das Wort „bitte“ wird nicht als solches erkannt, „wählen“ verliert seinen Umlaut und seine Bedeutung, und der ganze Satz zerfällt in eine Folge bizarrer Laute. Für jemanden, der auf diese auditive Ausgabe angewiesen ist, um den Inhalt zu verstehen, ist die Seite damit praktisch unbenutzbar. Die Barriere, die hier errichtet wird, ist enorm. Es ist, als würde man jemandem ein Buch in einer bekannten Sprache geben, aber mit den Buchstaben eines völlig anderen Alphabets gedruckt.

#### Die Lösung: Das `lang`-Attribut als Wegweiser

Die Lösung für dieses Problem ist erstaunlich einfach und doch so wirkungsvoll: das `lang`-Attribut. Indem du dieses Attribut im einleitenden `<html>`-Tag setzt, gibst du dem Browser und somit auch dem Screenreader die entscheidende Information über die Hauptsprache des Dokuments.

```html
<!DOCTYPE html>
<html lang="de">
  <head>
    <meta charset="UTF-8">
    <title>Meine deutsche Webseite</title>
  </head>
  <body>
    <h1>Willkommen!</h1>
    <p>Dies ist ein Absatz auf Deutsch.</p>
  </body>
</html>
```

Mit dieser einen kleinen Ergänzung – `lang="de"` – passiert im Hintergrund Magisches. Wenn ein Screenreader auf diese Seite trifft, weiß er sofort: „Aha, der Inhalt ist auf Deutsch.“ Er lädt daraufhin die passende deutsche Stimme und das dazugehörige Aussprachemodell. Der Satz „Bitte wählen Sie eine der drei Optionen“ wird nun klar und korrekt mit deutscher Betonung und Phonetik vorgelesen. Die Webseite wird verständlich und zugänglich.

Die Sprachcodes, die du hier verwendest, sind standardisiert. In den meisten Fällen nutzt du die zweibuchstabigen Codes nach ISO 639-1, wie `de` für Deutsch, `en` für Englisch, `fr` für Französisch oder `es` für Spanisch.

#### Mehrsprachigkeit im Detail: Wenn Sprachen sich mischen

Selten ist eine Webseite rein einsprachig. Vielleicht schreibst du einen deutschen Artikel und zitierst darin einen englischen Satz. Oder du verwendest gängige englische Fachbegriffe wie „User Experience“ oder „Call to Action“. Auch für diese Fälle hat HTML eine elegante Lösung.

Das `lang`-Attribut ist nicht auf das `<html>`-Element beschränkt. Du kannst es auf jedem beliebigen HTML-Element verwenden, um einen Sprachwechsel innerhalb des Dokuments zu kennzeichnen.

Stell dir vor, du schreibst einen Blogbeitrag über berühmte Zitate.

```html
<p>
  Ein berühmter Satz aus Shakespeares Hamlet lautet: 
  <q lang="en">To be, or not to be, that is the question.</q> 
  Dieser Satz prägt die Kultur bis heute.
</p>
```

Was passiert hier für einen Screenreader-Nutzer?
1.  Der Screenreader beginnt, den Absatz mit der deutschen Stimme vorzulesen, da die Hauptsprache des Dokuments als `de` definiert ist.
2.  Sobald er beim `<q>`-Element ankommt, erkennt er das Attribut `lang="en"`.
3.  Er hält kurz inne, wechselt nahtlos zur englischen Stimme und liest das Zitat „To be, or not to be, that is the question“ mit korrekter englischer Aussprache und Betonung vor.
4.  Direkt nach dem Zitat schaltet er wieder zurück zur deutschen Stimme, um den Rest des Satzes vorzulesen.

Dieses Erlebnis ist für den Zuhörer flüssig, natürlich und vor allem verständlich. Ohne die Kennzeichnung des Zitats hätte die deutsche Stimme versucht, die englischen Wörter auszusprechen, was zu einem ähnlichen Kauderwelsch wie im vorherigen Beispiel geführt hätte ("To be, or not to be...").

Das Markieren von Sprachwechseln ist ein Zeichen von hoher Qualität und Professionalität. Es zeigt, dass du die Bedürfnisse aller deiner Nutzer ernst nimmst. Du kannst es für einzelne Wörter mit einem `<span>`, für Zitate mit `<q>` oder `<blockquote>` oder für ganze Absätze mit `<p>` verwenden.

```html
<p>
  In der IT sprechen wir oft von der 
  <span lang="en">Single Source of Truth</span>.
</p>
```

#### Jenseits der Stimme: Braille und andere Technologien

Die Bedeutung des `lang`-Attributs endet nicht bei der Sprachausgabe. Screenreader sind oft auch mit Braillezeilen gekoppelt. Das sind Geräte, die Text in Blindenschrift umwandeln, sodass er mit den Fingern gelesen werden kann.

Auch die Brailleschrift ist sprachabhängig. Deutsches Braille verwendet andere Regeln und Abkürzungen (Kurzschrift) als englisches oder französisches Braille. Das `lang`-Attribut stellt sicher, dass der Text korrekt in die jeweilige Brailleschrift übersetzt wird. Eine falsche Sprachangabe führt hier zu falsch geschriebenen Wörtern, die für einen geübten Braille-Leser schwer zu entziffern oder irreführend sind.

Die korrekte Sprachdeklaration ist also ein Eckpfeiler der digitalen Barrierefreiheit. Sie sorgt dafür, dass Inhalte nicht nur irgendwie, sondern korrekt und effizient bei Menschen mit Behinderungen ankommen – sei es akustisch über eine synthetische Stimme oder taktil über eine Braillezeile. Indem du dir die kleine Mühe machst, die Sprache deiner Inhalte konsequent auszuzeichnen, öffnest du deine Webseite für ein viel größeres Publikum und schaffst eine inklusive digitale Erfahrung für alle.
