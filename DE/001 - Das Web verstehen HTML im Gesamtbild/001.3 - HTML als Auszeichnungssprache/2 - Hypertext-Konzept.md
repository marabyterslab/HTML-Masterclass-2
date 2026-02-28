# Hypertext-Konzept

### Das Hypertext-Konzept: Vom linearen Lesen zur vernetzten Welt

Stell dir ein klassisches Buch vor. Du beginnst auf Seite eins, liest zu Seite zwei, dann zu Seite drei und so weiter. Der Weg ist vorgegeben, er ist linear. Du folgst dem Faden, den der Autor für dich ausgelegt hat. Jahrhundertelang war dies die dominante Art, wie wir Wissen in Textform aufgenommen haben. Doch was wäre, wenn ein Text nicht nur ein gerader Pfad, sondern ein ganzes Netz aus Wegen wäre?

Genau das ist die Kernidee von Hypertext. Das Präfix „Hyper-“ kommt aus dem Griechischen und bedeutet so viel wie „über“ oder „jenseits“. Hypertext ist also Text, der über den gewöhnlichen, linearen Text hinausgeht. Er ist nicht an eine feste Reihenfolge gebunden. Stattdessen besteht er aus einzelnen Informationseinheiten – wir nennen sie Knoten oder Seiten –, die durch elektronische Verweise, die berühmten **Hyperlinks** (kurz: Links), miteinander verbunden sind.

Diese Idee ist älter als das World Wide Web selbst. Einer der ersten, der dieses Konzept visionär durchdacht hat, war der amerikanische Ingenieur Vannevar Bush. Bereits 1945, lange vor den ersten Computernetzwerken, beschrieb er in seinem Aufsatz „As We May Think“ ein fiktives Gerät namens „Memex“. Stell dir einen Schreibtisch vor, der nicht nur deine Bücher, Aufzeichnungen und Bilder digital speichert, sondern es dir auch erlaubt, beliebige Querverbindungen zwischen ihnen zu ziehen. Du liest einen Artikel über Biologie und findest eine interessante Stelle über Genetik. Mit dem Memex könntest du sofort eine Verbindung zu einem anderen Artikel über die Vererbungslehre von Gregor Mendel herstellen und so deinen eigenen, individuellen Wissenspfad erstellen. Bushs Vision war es, die starre, alphabetische oder numerische Ordnung von Bibliotheken durch ein System zu ersetzen, das der assoziativen Arbeitsweise des menschlichen Gehirns nachempfunden ist. Wir denken schließlich auch nicht in geraden Linien, sondern springen von einer Idee zur nächsten.

Den Begriff „Hypertext“ prägte dann in den 1960er Jahren der Soziologe und Philosoph Ted Nelson. Seine Vision, das Projekt Xanadu, war noch weitaus radikaler als das, was wir heute als Web kennen. Er träumte von einem globalen, universellen Literatur-System, in dem jedes Dokument mit jedem anderen auf vielfältige Weise verknüpft sein könnte, inklusive eines Systems zur Nachverfolgung von Urheberrechten und Zitaten. Obwohl Xanadu in seiner vollen Komplexität nie realisiert wurde, legten Nelson und andere Pioniere wie Douglas Engelbart, der 1968 in der „Mutter aller Demos“ ein funktionierendes Hypertext-System vorstellte, das intellektuelle Fundament für die Zukunft.

#### Der Durchbruch: Tim Berners-Lees pragmatische Lösung

Die Visionen waren großartig, aber es brauchte eine einfache, pragmatische Umsetzung, um sie für die Welt nutzbar zu machen. Diese kam Ende der 1980er Jahre von Tim Berners-Lee, einem Physiker am europäischen Kernforschungszentrum CERN. Das Problem am CERN war alltäglich und doch fundamental: Wissenschaftler aus aller Welt arbeiteten an gemeinsamen Projekten, doch ihre Informationen waren auf unzähligen, inkompatiblen Computersystemen verstreut. Es gab keine einfache Möglichkeit, ein Forschungsdokument auf einem Computer mit relevanten Daten auf einem anderen zu verknüpfen.

Berners-Lees Lösung war genial in ihrer Einfachheit. Er schuf ein System, das auf drei zentralen Säulen ruhte:

1.  **HTML (HyperText Markup Language):** Eine einfache Sprache, um Dokumente zu strukturieren und – ganz entscheidend – Hyperlinks einzubetten.
2.  **URL (Uniform Resource Locator):** Ein eindeutiges Adressformat, damit jeder Informationsknoten im Netzwerk (jede Seite, jedes Bild) einen einzigartigen Namen hat und gefunden werden kann.
3.  **HTTP (Hypertext Transfer Protocol):** Ein einfaches Protokoll, eine Art Regelsatz, mit dem ein Computer (der Client, z.B. dein Browser) ein Dokument von einem anderen Computer (dem Server) anfordern kann.

Dieses Dreigespann machte das Hypertext-Konzept endlich greifbar und dezentral. Jeder konnte einen Server aufsetzen, HTML-Dokumente erstellen und sie mit anderen Dokumenten irgendwo auf der Welt verlinken. Es gab keine zentrale Kontrollinstanz wie in Nelsons Xanadu-Vision. Diese Offenheit und Einfachheit waren der Schlüssel zum explosiven Erfolg des World Wide Web.

#### Die Anatomie eines Hyperlinks in HTML

Das Herzstück von Hypertext in HTML ist das `<a>`-Element, das für *anchor* (Anker) steht. Ein einfacher Link sieht im Code so aus:

```html
<p>Für weitere Informationen besuche die <a href="https://www.mozilla.org/">offizielle Mozilla-Website</a>.</p>
```

Lass uns diesen Baustein zerlegen, um ihn vollständig zu verstehen:

*   **Das `<a>`-Tag:** Es umschließt den Teil des Inhalts, der klickbar sein soll. In unserem Beispiel sind das die Worte „offizielle Mozilla-Website“. Diesen sichtbaren, klickbaren Teil nennt man den **Ankertext**. Ein guter Ankertext ist deskriptiv; er verrät dem Nutzer, wohin der Link ihn führen wird. Phrasen wie „hier klicken“ sind wenig aussagekräftig und sollten vermieden werden.
*   **Das `href`-Attribut:** Dies ist die wichtigste Eigenschaft des `<a>`-Elements. `href` steht für *Hypertext Reference* und sein Wert ist die Zieladresse – die URL, zu der der Nutzer springen soll, wenn er auf den Link klickt. Ohne ein `href`-Attribut ist ein `<a>`-Tag nur ein nutzloser Platzhalter.

Die URL im `href`-Attribut kann verschiedene Formen annehmen. Man unterscheidet hauptsächlich zwischen absoluten und relativen URLs.

**Absolute URLs** sind vollständige Adressen. Sie enthalten das Protokoll (`https://`), den Domainnamen (`www.mozilla.org`) und den Pfad zur Ressource. Du verwendest sie fast immer, wenn du auf eine komplett andere Website verlinkst.

```html
<a href="https://de.wikipedia.org/wiki/HTML">Artikel über HTML auf Wikipedia</a>
```

**Relative URLs** hingegen sind unvollständige Adressen. Sie beziehen sich auf die Position des aktuellen Dokuments. Stell dir vor, du hast eine Website mit folgender Ordnerstruktur:

```
mein-projekt/
├── index.html
├── kontakt.html
└── bilder/
    └── logo.png
```

Wenn du dich in der Datei `index.html` befindest und auf `kontakt.html` verlinken möchtest, reicht eine relative URL:

```html
<!-- In index.html -->
<a href="kontakt.html">Zu unserer Kontaktseite</a>
```

Der Browser weiß, dass er im selben Ordner nach der Datei `kontakt.html` suchen muss. Möchtest du von `index.html` aus auf das Logo verweisen, sieht der Link so aus:

```html
<!-- In index.html -->
<img src="bilder/logo.png" alt="Unser Firmenlogo">
```

Relative Pfade machen deine Website portabel. Du kannst den gesamten Projektordner verschieben oder auf einen anderen Server hochladen, und alle internen Links werden weiterhin funktionieren, da sie sich nicht auf einen festen Domainnamen beziehen.

#### Hypermedia: Wenn Links mehr als nur Text verbinden

Während die ursprüngliche Idee von „Hypertext“ handelte, wurde schnell klar, dass die Verknüpfungen nicht auf Textdokumente beschränkt sein müssen. Ein Link kann auf jede erdenkliche Art von Ressource im Web verweisen: ein Bild, ein Video, eine Audiodatei, ein PDF-Dokument oder eine Applikation zum Herunterladen.

Damit wurde aus Hypertext **Hypermedia**. Das Web ist kein reines Textmedium. HTML bietet uns Elemente, um Medien direkt in eine Seite einzubetten, wie zum Beispiel das `<img>`-Element für Bilder oder das `<video>`-Element für Videos. Diese Elemente verwenden ebenfalls Adressen (im `src`-Attribut, für *source*), um die Medienressource zu laden. Eine Webseite ist somit selbst ein Hypermedia-Dokument: ein strukturierter Text, der Bilder, Videos und andere Medien enthält und über Hyperlinks mit unzähligen weiteren Hypermedia-Dokumenten verbunden ist.

Das einfache Konzept des Hyperlinks hat die Art und Weise, wie wir auf Informationen zugreifen, navigieren und Wissen organisieren, von Grund auf verändert. Es ist das fundamentale Prinzip, das aus dem Internet ein verknüpftes Netz – ein *World Wide Web* – macht. Ohne Hyperlinks wäre das Web nur eine gigantische, unzugängliche Sammlung von isolierten Dateien. Erst der Link schafft die Verbindung, den Kontext und die Möglichkeit zur freien Erkundung, die das Web so mächtig und revolutionär machen. Jedes Mal, wenn du auf einen blauen, unterstrichenen Text klickst, trittst du in die Fußstapfen der Visionäre, die davon träumten, das Wissen der Welt für jeden nur einen Klick entfernt zugänglich zu machen.
