# Definitionslisten (dl)

### Definitionslisten: Mehr als nur ein Wörterbuch

Nachdem du nun geordnete und ungeordnete Listen kennengelernt hast, die sich hervorragend für Aufzählungen oder schrittweise Anleitungen eignen, stoßen wir auf eine dritte, oft unterschätzte Listenart: die Definitionsliste, ausgezeichnet mit dem `<dl>`-Element. Auf den ersten Blick mag ihr Name suggerieren, sie sei ausschließlich für Glossare oder Wörterbücher gedacht. Doch ihre wahre Stärke liegt in der semantischen Darstellung von jeglichen Name-Wert-Paaren oder Begriff-Beschreibung-Gruppen.

Stell dir vor, du möchtest nicht einfach nur eine Liste von Dingen aufzählen, sondern zu jedem Punkt eine Erläuterung geben. Genau hier kommt die Definitionsliste ins Spiel. Sie besteht aus drei wesentlichen Elementen:

*   **`<dl>` (Definition List):** Dies ist das umschließende Element, das die gesamte Liste als solche definiert. Es fungiert als Container für alle dazugehörigen Begriffe und deren Beschreibungen.
*   **`<dt>` (Definition Term):** Dieses Element enthält den Begriff, den Namen oder den Schlüssel, den du definieren oder beschreiben möchtest.
*   **`<dd>` (Definition Description):** Dieses Element liefert die dazugehörige Beschreibung, die Definition oder den Wert für das vorangehende `<dt>`-Element.

#### Die grundlegende Struktur

Im einfachsten Fall hast du einen Begriff und eine dazugehörige Beschreibung. Der HTML-Code dafür ist wunderbar logisch und einfach zu lesen. Nehmen wir an, wir erstellen ein kleines Glossar zu Webtechnologien:

```html
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language. Die Standardsprache zur Erstellung von Webseiten und Webanwendungen. Sie strukturiert den Inhalt semantisch.</dd>

  <dt>CSS</dt>
  <dd>Cascading Style Sheets. Eine Stylesheet-Sprache, die verwendet wird, um das Aussehen und die Formatierung eines in einer Auszeichnungssprache geschriebenen Dokuments zu beschreiben.</dd>

  <dt>JavaScript</dt>
  <dd>Eine Programmiersprache, die es ermöglicht, interaktive Elemente auf Webseiten zu implementieren, wie z. B. Animationen, Formularvalidierungen oder das dynamische Nachladen von Inhalten.</dd>
</dl>
```

In diesem Beispiel siehst du klar die Paarung: `<dt>` gibt den Begriff vor, das direkt folgende `<dd>` liefert die Erklärung. Browser stellen dies standardmäßig oft so dar, dass die `<dd>`-Elemente leicht eingerückt sind, um die Zusammengehörigkeit visuell zu unterstreichen. Aber wie du weißt, sollten wir uns niemals allein auf die Standarddarstellung verlassen – die Semantik ist das, was zählt.

#### Flexible Strukturen: Mehr als nur 1:1-Beziehungen

Die wahre Flexibilität von Definitionslisten zeigt sich, wenn wir von der starren 1:1-Beziehung abweichen. Die HTML-Spezifikation erlaubt hier interessante und sehr nützliche Gruppierungen.

**Mehrere Begriffe, eine Beschreibung**

Manchmal haben mehrere Begriffe dieselbe Bedeutung oder teilen sich eine gemeinsame Beschreibung. Anstatt die Beschreibung zu wiederholen, kannst du einfach mehrere `<dt>`-Elemente hintereinander platzieren, gefolgt von einem einzigen `<dd>`-Element.

```html
<dl>
  <dt>HTTP</dt>
  <dt>Hypertext Transfer Protocol</dt>
  <dd>Ein Protokoll zur Übertragung von Daten im World Wide Web. Es dient als Grundlage für die Kommunikation zwischen Webbrowsern und Webservern.</dd>

  <dt>SSL</dt>
  <dt>TLS</dt>
  <dd>Secure Sockets Layer bzw. Transport Layer Security sind Verschlüsselungsprotokolle zur sicheren Datenübertragung im Internet.</dd>
</dl>
```

Semantisch ist dies absolut korrekt. Es teilt dem Browser (und assistiven Technologien wie Screenreadern) mit, dass sowohl "HTTP" als auch "Hypertext Transfer Protocol" durch den nachfolgenden Text beschrieben werden.

**Ein Begriff, mehrere Beschreibungen**

Genauso ist der umgekehrte Fall möglich. Ein einzelner Begriff kann mehrere Bedeutungen, Aspekte oder Beschreibungen haben. Dafür notierst du ein `<dt>`-Element, gefolgt von mehreren `<dd>`-Elementen.

```html
<dl>
  <dt>Cookie</dt>
  <dd>Im Webkontext: Eine kleine Textdatei, die von einem Webserver an einen Browser gesendet und auf dem Computer des Nutzers gespeichert wird, um Informationen über die Sitzung zu erhalten.</dd>
  <dd>Im kulinarischen Kontext: Ein kleines, flaches und süßes Gebäck, das oft aus Mehl, Zucker und Fett hergestellt wird.</dd>
</dl>
```

Jedes `<dd>` steht hier für eine eigenständige Beschreibung des Begriffs "Cookie".

#### Anwendungsfälle jenseits des Glossars

Jetzt, wo du die Struktur und Flexibilität kennst, wird schnell klar, dass Definitionslisten weit über reine Wortdefinitionen hinausgehen. Sie sind das semantisch korrekte Werkzeug für unzählige Situationen, in denen du Schlüssel-Wert-Paare darstellst.

**Produktspezifikationen:**
Eine Produktseite ist ein perfektes Beispiel. Statt einer unstrukturierten Liste oder einer missbrauchten Tabelle kannst du eine Definitionsliste verwenden.

```html
<dl>
  <dt>Prozessor</dt>
  <dd>NextGen Fusion Core X2</dd>
  
  <dt>Arbeitsspeicher</dt>
  <dd>32 GB LPDDR5 RAM</dd>

  <dt>Display</dt>
  <dd>14-Zoll Liquid Retina XDR Display</dd>
  
  <dt>Anschlüsse</dt>
  <dd>2x Thunderbolt 4</dd>
  <dd>1x HDMI</dd>
  <dd>1x SDXC-Kartensteckplatz</dd>
</dl>
```

Beachte das letzte Beispiel für "Anschlüsse": Hier haben wir einen Begriff mit mehreren zugehörigen Werten, die als separate `<dd>`-Elemente aufgeführt werden.

**Fragen und Antworten (FAQs):**
Eine FAQ-Seite ist im Grunde eine Sammlung von Begriff-Beschreibung-Paaren. Die Frage ist der "Term" (`<dt>`), die Antwort die "Description" (`<dd>`).

```html
<dl>
  <dt>Wie lange dauert der Versand?</dt>
  <dd>In der Regel verlässt deine Bestellung innerhalb von 24 Stunden unser Lager. Die Zustellung durch den Versanddienstleister dauert zusätzlich 1-2 Werktage.</dd>

  <dt>Kann ich meine Bestellung zurücksenden?</dt>
  <dd>Ja, du hast ein 30-tägiges Rückgaberecht auf alle unbenutzten Artikel in Originalverpackung.</dd>
</dl>
```

**Metadaten:**
Auch für die Darstellung von Metadaten, wie zum Beispiel bei einem Blogartikel oder einem Kunstwerk, sind Definitionslisten ideal.

```html
<dl>
  <dt>Autor</dt>
  <dd>Alex Meyer</dd>
  
  <dt>Veröffentlicht am</dt>
  <dd>15. Juli 2024</dd>
  
  <dt>Kategorie</dt>
  <dd>Webentwicklung</dd>
  
  <dt>Tags</dt>
  <dd>HTML</dd>
  <dd>Semantik</dd>
  <dd>Best Practices</dd>
</dl>
```

#### Semantik vor Aussehen: Warum `dl` die richtige Wahl ist

Du könntest versucht sein, eine ähnliche Struktur visuell mit anderen Mitteln nachzubauen. Vielleicht eine ungeordnete Liste, bei der du den Anfang jeder Zeile fett formatierst, oder sogar eine Tabelle mit zwei Spalten. Das mag auf dem Bildschirm ähnlich aussehen, aber semantisch wäre es falsch.

*   Eine **ungeordnete Liste (`<ul>`)** teilt dem Computer mit: "Dies ist eine Liste gleichrangiger Elemente." Die innere Beziehung zwischen "Prozessor" und "NextGen Fusion Core X2" geht dabei komplett verloren.
*   Eine **Tabelle (`<table>`)** ist für tabellarische Daten gedacht, also für Daten, bei denen sowohl die Zeilen als auch die Spalten eine eigene Bedeutung haben. Für einfache Schlüssel-Wert-Paare ist eine Tabelle oft semantischer "Overkill" und kann für assistive Technologien schwieriger zu interpretieren sein.

Eine Definitionsliste hingegen kommuniziert exakt die richtige Bedeutung: "Hier kommt eine Gruppe von Begriffen, und zu jedem folgt eine oder mehrere zugehörige Beschreibungen." Ein Screenreader kann einem Nutzer mit Sehbehinderung beispielsweise vorlesen: "Term: Prozessor. Description: NextGen Fusion Core X2." Die Verbindung ist sofort klar und unmissverständlich.

Indem du das `<dl>`-Element für seine vorgesehenen Zwecke einsetzt, schreibst du nicht nur sauberen und logischen Code, sondern schaffst auch eine solidere Grundlage für Styling mit CSS, für die Verarbeitung durch JavaScript und vor allem für eine bessere Zugänglichkeit (Barrierefreiheit) deiner Webseite. Sie ist ein kraftvolles Werkzeug in deinem semantischen HTML-Baukasten.
