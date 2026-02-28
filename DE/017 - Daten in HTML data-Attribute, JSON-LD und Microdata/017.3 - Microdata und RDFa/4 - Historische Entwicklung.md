# Historische Entwicklung

### Historische Entwicklung: Vom dummen Dokument zum intelligenten Datennetz

Wenn du heute eine Webseite baust, denkst du wahrscheinlich in erster Linie an den Menschen, der sie besuchen wird. Du möchtest, dass sie gut aussieht, dass die Informationen klar strukturiert sind und dass die Bedienung intuitiv ist. Das war auch das ursprüngliche Ziel des World Wide Web: ein riesiges Netz aus verlinkten Dokumenten zu schaffen, die von Menschen gelesen und verstanden werden können. Doch schon sehr früh gab es eine Vision, die weit darüber hinausging – die Vision eines "Semantischen Webs".

#### Am Anfang war das Chaos: Das Web der reinen Darstellung

Stell dir das frühe Web der 90er-Jahre vor. HTML war eine einfache Sprache, deren Hauptzweck es war, Text zu strukturieren und darzustellen. Mit Tags wie `<b>` für Fettschrift, `<i>` für Kursivschrift und Tabellen für das Layout (`<table border="1">`) wurde versucht, das Aussehen von gedruckten Dokumenten im Browser nachzubilden.

Für einen Menschen war das super. Du konntest eine Webseite über ein Filmfestival aufrufen und lesen:

```html
<h1>Großes Filmfestival Berlin</h1>
<p>
  <b>Film:</b> Der Pate<br>
  <b>Regisseur:</b> Francis Ford Coppola<br>
  <b>Datum:</b> 15. Oktober 2024<br>
  <b>Ort:</b> Kino International
</p>
```

Du als Mensch verstehst sofort, worum es geht. Du erkennst den Namen des Films, den Regisseur, das Datum und den Veranstaltungsort. Eine Maschine – zum Beispiel eine Suchmaschine wie AltaVista oder das frühe Google – sah jedoch nur eine Ansammlung von Wörtern. Sie wusste nicht, dass "Der Pate" ein Film ist oder dass "Francis Ford Coppola" eine Person ist, die in einer bestimmten Beziehung (nämlich als Regisseur) zu diesem Film steht. Für die Maschine war das nur Text. Das Web war ein gigantisches, unstrukturiertes Archiv von "dummen" Dokumenten. Die Suche funktionierte rein über Schlüsselwörter, ohne das eigentliche Verständnis für den Kontext.

#### Die Vision des Tim Berners-Lee: Das Semantische Web

Der Erfinder des World Wide Web, Tim Berners-Lee, hatte von Anfang an mehr im Sinn. Seine Vision war die eines Semantischen Webs – eines Webs, in dem Informationen nicht nur für Menschen, sondern auch für Maschinen verständlich sind. Die Idee war, den Webseiten eine zusätzliche Bedeutungsebene (Semantik) zu geben. Ein Computer sollte in der Lage sein, Zusammenhänge zu erkennen: Diese Webseite beschreibt ein Event. Dieses Event hat einen Namen, einen Ort und ein Datum. An diesem Event wird ein Film gezeigt. Dieser Film hat einen Regisseur.

Um diese Vision technisch umzusetzen, schlug das World Wide Web Consortium (W3C) das **Resource Description Framework (RDF)** vor. RDF ist ein Modell, um Aussagen über Dinge (Ressourcen) in Form von Tripeln zu machen: Subjekt-Prädikat-Objekt. Zum Beispiel:

*   (Der Pate) - (hat Regisseur) - (Francis Ford Coppola)
*   (Der Pate) - (ist ein) - (Film)

Das war ein mächtiges Konzept, aber die erste Umsetzung, RDF/XML, war für den durchschnittlichen Webentwickler eine echte Hürde. Es war komplex, wortreich und lebte oft in separaten Dateien oder unhandlichen Blöcken innerhalb des HTMLs. Es fühlte sich fremd an und setzte sich in der breiten Masse der Webentwicklung nie wirklich durch. Die Vision war großartig, aber die praktische Umsetzung war zu kompliziert.

#### Der pragmatische Ansatz: Microformats

Die Entwicklergemeinschaft erkannte das Problem. Die Lösung musste einfacher sein und sich nahtlos in das bestehende HTML integrieren. So entstand Mitte der 2000er-Jahre die Idee der **Microformats**. Der Grundgedanke war genial einfach: Lasst uns bestehende HTML-Attribute, hauptsächlich das `class`-Attribut, wiederverwenden, um Semantik hinzuzufügen.

Anstatt neue, komplexe Sprachen zu erfinden, einigte man sich auf eine Reihe von vordefinierten `class`-Namen, die eine bestimmte Bedeutung hatten. Ein bekanntes Beispiel ist `hCard` zur Auszeichnung von Kontaktinformationen. Unser Beispiel von oben könnte mit Microformats so aussehen:

```html
<div class="vevent">
  <h1 class="summary">Großes Filmfestival Berlin</h1>
  <p>
    Film: <span class="description">Der Pate</span><br>
    Regisseur: <span class="attendee">Francis Ford Coppola</span><br>
    Datum: <time class="dtstart" datetime="2024-10-15">15. Oktober 2024</time><br>
    Ort: <span class="location">Kino International</span>
  </p>
</div>
```

Plötzlich konnte eine Maschine, die die Microformats-Spezifikation kannte, diese Seite parsen und verstehen: Aha, das hier ist ein Event (`vevent`). Der Name ist "Großes Filmfestival Berlin" (`summary`), es beginnt am 15. Oktober 2024 (`dtstart`) und findet im "Kino International" (`location`) statt.

Microformats waren ein riesiger Erfolg, weil sie pragmatisch waren. Sie erforderten kein tiefes Wissen über komplexe Datenmodelle. Du musstest nur die richtigen Klassennamen kennen und anwenden. Der große Nachteil war jedoch ihre begrenzte Flexibilität. Es gab nur eine festgelegte Anzahl von Formaten (für Events, Kontakte, Rezensionen etc.). Wollte man etwas beschreiben, für das es kein Microformat gab, hatte man Pech.

#### Die Konkurrenten betreten die Bühne: RDFa und Microdata

Die Notwendigkeit einer flexibleren Lösung, die aber immer noch einfacher als RDF/XML war, führte zur Entwicklung von zwei konkurrierenden Standards, die beide versuchten, das Problem auf ihre Weise zu lösen.

**1. RDFa (Resource Description Framework in Attributes)**

RDFa war die Antwort des W3C. Es war der Versuch, die volle Kraft von RDF direkt in HTML-Attribute zu bringen. Mit Attributen wie `vocab` (um ein Vokabular wie Schema.org zu definieren), `typeof` (um den Typ eines Objekts festzulegen, z. B. "Person" oder "Movie") und `property` (um eine Eigenschaft dieses Objekts zu beschreiben, z. B. "name" oder "director") konnte man extrem ausdrucksstarke und präzise Datenstrukturen direkt im HTML abbilden.

RDFa war technisch überlegen und extrem flexibel, da es jedes beliebige RDF-Vokabular verwenden konnte. Es litt aber unter dem Ruf, immer noch etwas zu komplex und akademisch zu sein.

**2. Microdata**

Etwa zur gleichen Zeit entwickelte eine andere Gruppe, die WHATWG (Web Hypertext Application Technology Working Group), zu der Leute von Apple, Mozilla und Google gehörten, einen eigenen Standard: **Microdata**. Das Ziel war, einen Mittelweg zwischen der Einfachheit von Microformats und der Flexibilität von RDFa zu finden.

Microdata führte eine Handvoll neuer Attribute ein, die sehr intuitiv waren:

*   `itemscope`: Markiert den Beginn eines neuen Objekts (eines "Items").
*   `itemtype`: Definiert den Typ des Objekts mithilfe einer URL zu einem Vokabular.
*   `itemprop`: Definiert eine Eigenschaft des Objekts.

Unser Beispiel mit Microdata würde so aussehen:

```html
<div itemscope itemtype="http://schema.org/Movie">
  <h1 itemprop="name">Der Pate</h1>
  <p>
    Regisseur: 
    <span itemprop="director" itemscope itemtype="http://schema.org/Person">
      <span itemprop="name">Francis Ford Coppola</span>
    </span>
    <br>
    Aufführung im Rahmen des Events:
    <span itemprop="event" itemscope itemtype="http://schema.org/Event">
      <span itemprop="name">Großes Filmfestival Berlin</span>
      am <meta itemprop="startDate" content="2024-10-15">15. Oktober 2024
      im <span itemprop="location">Kino International</span>.
    </span>
  </p>
</div>
```

Hier siehst du, wie wir ein `Movie`-Objekt definieren und darin ein `Person`-Objekt (den Regisseur) und ein `Event`-Objekt (das Festival) verschachteln.

#### Der Wendepunkt: Schema.org und der Sieg von Microdata

Der entscheidende Moment im Wettstreit der Standards kam 2011. Die großen Suchmaschinen – Google, Bing und Yahoo! (später auch Yandex) – taten sich zusammen und riefen das Projekt **Schema.org** ins Leben. Schema.org ist ein riesiges, gemeinsames Vokabular zur Beschreibung von allem Möglichen: Personen, Orten, Produkten, Rezepten, Filmen, Büchern und vielem mehr.

Die Empfehlung der Suchmaschinen war klar: Nutzt das Schema.org-Vokabular mit Microdata, um eure Inhalte für uns verständlich zu machen. Wenn ihr das tut, belohnen wir euch mit "Rich Snippets" – also den erweiterten Suchergebnissen mit Sternchenbewertungen, Preisen, Veranstaltungsdaten und so weiter.

Dieser Anreiz war so stark, dass Microdata schlagartig zum De-facto-Standard für semantische Auszeichnungen im Web wurde. Es war nicht unbedingt der technisch eleganteste Standard, aber er war einfach genug und hatte die mächtigste Unterstützung, die man sich vorstellen kann.

#### Der aktuelle Stand: JSON-LD übernimmt die Führung

Die Geschichte endet hier jedoch nicht. Während Microdata das HTML direkt mit semantischen Attributen "anreicherte", empfanden viele Entwickler dies als eine Vermischung von Belangen. Das HTML, das für die Struktur und den Inhalt zuständig ist, wurde mit Metadaten überfrachtet.

Die Lösung für dieses Problem kam in Form von **JSON-LD (JavaScript Object Notation for Linked Data)**. Anstatt die Attribute direkt an die HTML-Tags zu hängen, platziert man bei diesem Ansatz einen einzigen `<script>`-Block im `<head>` oder `<body>` der Seite. In diesem Skript werden alle semantischen Daten sauber und strukturiert in einem JSON-Format definiert.

Der große Vorteil: Die Daten sind vom HTML-Markup entkoppelt. Das macht die Pflege einfacher und den HTML-Code sauberer. Google empfiehlt heute JSON-LD als bevorzugte Methode zur Implementierung von strukturierten Daten.

Obwohl JSON-LD heute dominiert, ist das Verständnis der historischen Entwicklung von Microformats über RDFa bis hin zu Microdata entscheidend. Sie alle verfolgten dasselbe Ziel: dem Web Bedeutung zu verleihen. Die Konzepte von Vokabularen, Typen und Eigenschaften, die du in Microdata und RDFa lernst, sind exakt dieselben, die auch in JSON-LD verwendet werden. Du lernst also das Fundament, auf dem die moderne, maschinenlesbare Webkommunikation aufgebaut ist. Die Syntax hat sich weiterentwickelt, aber die Vision von Tim Berners-Lee ist heute relevanter denn je.
