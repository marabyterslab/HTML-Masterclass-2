# Hypertext-Konzept

### Das Hypertext-Konzept: Mehr als nur ein Link

Wenn du heute im Internet surfst, ist eine Handlung so selbstverständlich wie das Atmen: Du klickst auf einen Link. Ein Wort, ein Satz oder ein Bild leuchtet auf, vielleicht ändert es seine Farbe, und mit einem Klick landest du an einem völlig neuen Ort – auf einer anderen Seite, in einem anderen Dokument, manchmal sogar auf einer komplett anderen Website. Diese scheinbar simple Mechanik ist das Fundament des gesamten World Wide Web. Sie ist die praktische Umsetzung eines Konzepts, das älter ist als das Web selbst: das Konzept des Hypertexts.

Um zu verstehen, was HTML im Kern ausmacht, müssen wir uns von der Idee eines traditionellen Dokuments verabschieden. Ein Buch liest du normalerweise linear, von der ersten bis zur letzten Seite. Die Struktur ist vorgegeben, der Pfad ist klar. Hypertext bricht radikal mit dieser Linearität. Er stellt sich Information nicht als eine einzelne, lange Kette vor, sondern als ein Netz von Knotenpunkten (Informationseinheiten), die durch Querverweise (Links) miteinander verbunden sind. Du als Leser entscheidest, welchem Pfad du folgst. Jeder Klick ist eine bewusste Entscheidung, eine neue Route durch das Informationsnetz zu nehmen.

#### Die Visionäre: Von Memex zu Xanadu

Die Idee des Hypertexts entstand lange bevor es die technischen Mittel gab, sie global umzusetzen. Einer der ersten Vordenker war der amerikanische Ingenieur Vannevar Bush. Bereits 1945, in seinem Aufsatz „As We May Think“, beschrieb er eine fiktive Maschine namens „Memex“. Bush beklagte, dass die Menge an wissenschaftlichem Wissen so rasant wuchs, dass es für einen Einzelnen unmöglich wurde, den Überblick zu behalten. Starre, alphabetische oder numerische Ablagesysteme empfand er als unnatürlich, weil das menschliche Gehirn nicht so funktioniert. Unser Denken springt assoziativ von einer Idee zur nächsten.

Der Memex sollte dieses assoziative Denken nachbilden. Bush stellte sich einen Schreibtisch vor, in dem riesige Mengen an Informationen auf Mikrofilm gespeichert waren. Der Benutzer könnte Dokumente auf Bildschirmen betrachten und – das ist der entscheidende Punkt – eigene, persönliche Verbindungen, sogenannte „assoziative Pfade“ (associative trails), zwischen ihnen herstellen. So könnte ein Biologe, der einen Artikel über Vererbung liest, eine direkte Verbindung zu einem anderen Artikel über statistische Mathematik herstellen, den er Wochen zuvor gelesen hat. Diese Verbindung würde gespeichert und könnte jederzeit wieder aufgerufen oder mit anderen geteilt werden. Der Memex war die theoretische Geburt des Hyperlinks – der Traum von einer Maschine, die Wissen so vernetzt, wie unser Verstand es tut.

Der Begriff „Hypertext“ selbst wurde jedoch erst in den 1960er Jahren von dem Soziologen und Philosophen Ted Nelson geprägt. Nelson hatte eine noch weitaus radikalere Vision namens „Projekt Xanadu“. Xanadu sollte ein globales, universelles Repositorium für alle geschriebenen Texte der Menschheit sein. Jedes Dokument sollte eine einzigartige Adresse haben. Anders als im heutigen Web sollten Links in Xanadu nicht nur in eine Richtung funktionieren, sondern bidirektional sein. Das bedeutet, wenn Dokument A auf Dokument B verlinkt, würde Dokument B automatisch wissen, dass es von A verlinkt wird, und diesen Rückverweis anzeigen. Außerdem sollte es kein „Copy & Paste“ geben. Stattdessen würde man Teile eines Dokuments in ein anderes „transkludieren“ (transclude), also live einbetten. Der ursprüngliche Kontext und die Urheberschaft blieben so immer erhalten, was eine automatische und faire Abrechnung von Tantiemen für Autoren ermöglicht hätte.

Nelsons Vision war grandios, aber technisch extrem komplex und konnte sich in ihrer Reinform nie durchsetzen. Doch seine Ideen und der von ihm geprägte Begriff „Hypertext“ legten das intellektuelle Fundament für das, was kommen sollte.

#### Die Umsetzung: Tim Berners-Lee und das World Wide Web

Die Person, die den Hypertext aus der Welt der Theorie in die globale Praxis holte, war Tim Berners-Lee. Als Physiker am europäischen Kernforschungszentrum CERN stand er in den späten 1980er Jahren vor einem ähnlichen Problem wie Vannevar Bush Jahrzehnte zuvor: Informationen waren auf unzähligen, nicht miteinander verbundenen Computern gespeichert, in unterschiedlichen Formaten und nur für die Person zugänglich, die wusste, wo und wie sie suchen musste. Die Zusammenarbeit war ein Albtraum.

Berners-Lee schlug eine pragmatische, dezentrale Lösung vor, die auf drei Kerntechnologien basierte:

1.  **URL (Uniform Resource Locator):** Eine eindeutige Adresse für jedes Dokument im Netzwerk. So wie jede Wohnung eine Postanschrift hat, bekommt jede Ressource im Web eine URL.
2.  **HTTP (Hypertext Transfer Protocol):** Ein einfaches Protokoll, eine Sprache, mit der Computer (Clients und Server) diese Ressourcen anfordern und austauschen können.
3.  **HTML (Hypertext Markup Language):** Eine einfache Auszeichnungssprache, um Dokumente zu strukturieren und – das ist der Kern – um Hyperlinks zu erstellen, die auf andere URLs verweisen.

Im Vergleich zu Nelsons Xanadu war Berners-Lees System radikal einfach. Links waren unidirektional (sie funktionieren nur in eine Richtung), und es gab keine eingebaute Versionskontrolle oder ein Rechtemanagement. Aber genau diese Einfachheit war der Schlüssel zum Erfolg. Jeder konnte mit geringem Aufwand HTML-Dokumente erstellen, sie auf einem Server ablegen und mit anderen Dokumenten auf der ganzen Welt verknüpfen. Das World Wide Web war geboren – als eine praktische, funktionierende Implementierung der Hypertext-Idee.

#### Anatomie eines Hyperlinks in HTML

Das Herzstück des Hypertext-Konzepts in HTML ist ein einziges, aber unglaublich mächtiges Element: der Anker-Tag `<a>`. Schauen wir uns seinen Aufbau genau an.

```html
<a href="https://www.beispiel.de/ueber-uns.html">Lerne mehr über uns</a>
```

Dieser simple Code erzeugt den typischen blauen, unterstrichenen Link, den du kennst. Er besteht aus mehreren Teilen:

*   **Das öffnende Tag `<a>`:** Es signalisiert dem Browser, dass hier ein Anker (englisch: anchor) beginnt. Ein Anker kann sowohl ein Link-Startpunkt als auch ein Link-Ziel sein.
*   **Das Attribut `href`:** Dies ist die Abkürzung für „Hypertext Reference“ und ist das wichtigste Attribut. Sein Wert ist die URL des Ziels, zu dem der Link führen soll. Ohne `href` ist ein `<a>`-Tag kein funktionierender Link.
*   **Der Linktext:** Der Inhalt zwischen dem öffnenden (`<a>`) und dem schließenden (`</a>`) Tag ist das, was der Benutzer auf der Seite sieht und anklicken kann. In unserem Beispiel ist das „Lerne mehr über uns“. Dieser Text sollte immer aussagekräftig sein und dem Benutzer verraten, was ihn am Ziel erwartet.
*   **Das schließende Tag `</a>`:** Es beendet das Link-Element.

Die URL im `href`-Attribut kann **absolut** oder **relativ** sein.

*   Eine **absolute URL** enthält das komplette Adressschema, inklusive Protokoll (`https://`) und Domainnamen (`www.beispiel.de`). Sie wird fast immer für externe Links verwendet, also für Links, die auf eine andere Website verweisen.

    ```html
    <a href="https://de.wikipedia.org/wiki/Hypertext">Mehr auf Wikipedia lesen</a>
    ```

*   Eine **relative URL** gibt den Pfad zum Zieldokument *relativ zum aktuellen Dokument* an. Sie wird für interne Links innerhalb derselben Website verwendet. Dies macht eine Website portabler – du kannst sie auf einen anderen Server umziehen, ohne alle Links ändern zu müssen.

    ```html
    <!-- Link zu einer Datei im selben Verzeichnis -->
    <a href="kontakt.html">Kontakt</a>

    <!-- Link zu einer Datei in einem Unterverzeichnis -->
    <a href="produkte/details.html">Produktdetails</a>

    <!-- Link zu einer Datei im übergeordneten Verzeichnis -->
    <a href="../index.html">Zurück zur Startseite</a>
    ```

#### Mehr als nur Seitenverweise: Fragmente und Hypermedia

Das Hypertext-Konzept in HTML geht noch weiter. Ein Link muss nicht immer zum Anfang einer Seite führen. Mithilfe von sogenannten Fragment-Identifiern kannst du direkt zu einem bestimmten Abschnitt innerhalb eines Dokuments springen. Dazu vergibst du dem Zielelement eine eindeutige `id` und verweist im `href`-Attribut mit einem Rautezeichen (`#`) darauf.

```html
<!-- Das ist das Ziel irgendwo weiter unten auf der Seite -->
<h2 id="kapitel3">Kapitel 3: Fortgeschrittene Techniken</h2>
<p>Hier steht der Inhalt des dritten Kapitels...</p>

<!-- Das ist der Link, der dorthin springt -->
<a href="#kapitel3">Springe direkt zu Kapitel 3</a>
```

Das ist extrem nützlich für Inhaltsverzeichnisse auf langen Seiten oder für FAQs.

Darüber hinaus beschränkt sich Hypertext nicht nur auf Textdokumente. Die Verknüpfung verschiedener Medientypen – Text, Bilder, Videos, Töne, PDFs – wird als **Hypermedia** bezeichnet. Jeder Link in HTML kann auf jede Art von Ressource verweisen, solange diese über eine URL erreichbar ist. Ein Klick kann dich also genauso gut zu einem Bild, einem Video-Stream oder einer herunterladbaren Datei führen.

Jedes Mal, wenn du ein `<a>`-Element in deinen Code schreibst, nimmst du also an dieser revolutionären Idee teil. Du webst einen weiteren Faden in das globale Netz, schaffst neue Pfade und gibst den Nutzern die Freiheit, Informationen auf ihre eigene, nicht-lineare Weise zu entdecken. HTML ist die Sprache, die diese Verbindungen ermöglicht und damit die abstrakte Vision des Hypertexts in die lebendige, atmende Realität des World Wide Web übersetzt.
