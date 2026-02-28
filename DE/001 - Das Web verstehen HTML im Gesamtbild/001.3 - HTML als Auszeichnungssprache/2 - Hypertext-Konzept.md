# Hypertext-Konzept

### Die Seele des Webs: Das Hypertext-Konzept

Stell dir ein klassisches Buch vor. Du beginnst auf der ersten Seite und liest dich linear bis zur letzten durch. Seite für Seite, Kapitel für Kapitel, in einer vom Autor festgelegten Reihenfolge. Diese Struktur ist seit Jahrhunderten die Norm für die Weitergabe von Wissen und Geschichten. Sie ist linear, vorhersehbar und in sich geschlossen.

Doch was wäre, wenn ein Text nicht wie eine Einbahnstraße, sondern wie ein Netz aus unzähligen Wegen wäre? Was, wenn du von einem Gedanken direkt zu einem verwandten Gedanken springen könntest, unabhängig davon, wo dieser im Gesamtwerk steht? Was, wenn du als Leser die volle Kontrolle über deine Reiseroute durch die Informationen hättest?

Genau das ist die grundlegende Idee von Hypertext.

Hypertext ist ein Konzept, das Texte – und allgemeiner, Informationen – nicht als lineare Abfolge, sondern als ein Netzwerk von Knoten (Informationseinheiten) und Verknüpfungen (Links) betrachtet. Ein Wort, ein Satz oder ein Bild in einem Dokument kann eine direkte Verbindung zu einer völlig anderen Informationseinheit herstellen, sei es im selben Dokument oder in einem ganz anderen. Du als Nutzer entscheidest, ob du einem Link folgst, und erschaffst so deinen eigenen, individuellen Pfad durch das Wissen.

#### Die Wurzeln einer revolutionären Idee

Obwohl wir Hypertext heute untrennbar mit dem World Wide Web verbinden, ist die Idee selbst deutlich älter. Sie wurzelt in dem Wunsch, die starren Fesseln des gedruckten Wortes zu sprengen und eine Informationsstruktur zu schaffen, die der Funktionsweise unseres Gehirns ähnlicher ist. Unser Denken ist assoziativ; ein Gedanke führt zum nächsten, oft auf unvorhersehbare Weise.

Der Visionär Vannevar Bush beschrieb bereits 1945 in seinem berühmten Aufsatz "As We May Think" ein hypothetisches Gerät namens "Memex". Der Memex sollte es einem Forscher ermöglichen, all seine Bücher, Aufzeichnungen und Kommunikationen auf Mikrofilm zu speichern und mechanisch abzurufen. Das revolutionäre daran war die Möglichkeit, "assoziative Spuren" zu schaffen – also persönliche Verbindungen zwischen zwei beliebigen Informationseinheiten herzustellen und diese Pfade später erneut zu beschreiten oder mit anderen zu teilen. Bush legte damit den philosophischen Grundstein für Hypertext.

Den Begriff selbst prägte der Soziologe und Philosoph Ted Nelson in den 1960er Jahren. Seine Vision, das "Projekt Xanadu", war noch weitreichender als das, was wir heute als Web kennen. Es sah ein universelles, globales Hypertext-System vor, in dem jedes Dokument eindeutig adressierbar wäre, Plagiate durch ein ausgeklügeltes System der Quellenverfolgung unmöglich würden und Links in beide Richtungen funktionieren sollten. Obwohl Xanadu in seiner ursprünglichen Form nie vollständig realisiert wurde, inspirierte Nelsons Konzept Generationen von Informatikern.

Die Person, die diese visionären Ideen schließlich in eine funktionierende, weltweit zugängliche Realität umsetzte, war Tim Berners-Lee. Ende der 1980er Jahre arbeitete er am CERN, dem Europäischen Kernforschungszentrum. Er stand vor dem Problem, dass Forschungsinformationen auf unzähligen, inkompatiblen Computersystemen verstreut waren. Seine Lösung war ein System, das zwei bestehende Technologien auf geniale Weise kombinierte: die Vernetzungsstruktur des Internets und das Konzept des Hypertexts. Er schuf das World Wide Web. Und um die Hypertext-Dokumente für dieses Web zu erstellen, entwickelte er eine einfache, aber wirkungsvolle Sprache: die **H**yper**T**ext **M**arkup **L**anguage, kurz HTML.

#### HTML: Die Sprache, die Hypertext zum Leben erweckt

HTML ist also nicht nur eine Sprache zur Strukturierung von Inhalten; ihr Name und ihr Kernzweck sind untrennbar mit dem Hypertext-Konzept verbunden. HTML gibt dir die Werkzeuge an die Hand, um die Verknüpfungen zu schaffen, die aus einer Sammlung von isolierten Dokumenten ein zusammenhängendes Netz – ein "Web" – machen.

Das zentrale Element für die Umsetzung von Hypertext in HTML ist der Anker-Tag (engl. *anchor*): `<a>`. Mit diesem unscheinbaren Tag erschaffst du die Links, die das Surfen im Web überhaupt erst ermöglichen.

Schauen wir uns ein einfaches Beispiel an:

```html
<p>Für weitere Informationen über die Geschichte des Webs, besuche bitte die <a href="geschichte.html">entsprechende Seite</a>.</p>
```

Lass uns diesen Code zerlegen:

*   `<a>`: Dies ist das öffnende Tag des Anker-Elements. Es signalisiert dem Browser: "Achtung, hier beginnt ein Link."
*   `href`: Dies ist ein Attribut des `<a>`-Tags und steht für **H**ypertext **Ref**erence. Der Wert dieses Attributs (`"geschichte.html"`) ist das Ziel des Links – die Adresse der Ressource, zu der navigiert werden soll.
*   `entsprechende Seite`: Dies ist der Inhalt des Anker-Elements. Es ist der Text, der für den Nutzer sichtbar und klickbar ist. Browser stellen diesen Link-Text standardmäßig oft blau und unterstrichen dar.
*   `</a>`: Dies ist das schließende Tag. Es markiert das Ende des Links.

Wenn ein Nutzer auf den Text "entsprechende Seite" klickt, weist der Browser den Computer an, die im `href`-Attribut angegebene Datei `geschichte.html` zu laden und anzuzeigen. Ein einfacher Klick, und schon bist du von einem Dokument zum nächsten gesprungen. Das ist die Magie des Hypertexts in Aktion.

#### Mehr als nur Verweise auf andere Seiten

Die Macht des Hypertexts in HTML geht weit über einfache Verknüpfungen zwischen verschiedenen Dokumenten hinaus. Das `<a>`-Element ist unglaublich vielseitig.

**Interne Links (Anker-Links):** Du kannst Links erstellen, die nicht zu einer anderen Seite, sondern zu einem bestimmten Abschnitt auf derselben Seite führen. Das ist besonders bei langen Dokumenten nützlich, um dem Nutzer das Scrollen zu ersparen. Dazu vergibst du dem Zielelement eine `id` und verweist im `href`-Attribut darauf, eingeleitet durch ein Raute-Zeichen (`#`).

```html
<!-- Oben auf der Seite befindet sich das Inhaltsverzeichnis -->
<nav>
  <ul>
    <li><a href="#kapitel1">Zum ersten Kapitel</a></li>
    <li><a href="#kapitel2">Zum zweiten Kapitel</a></li>
  </ul>
</nav>

<!-- Viel später im Dokument... -->
<h2 id="kapitel1">Das ist das erste Kapitel</h2>
<p>Hier steht der Inhalt des ersten Kapitels...</p>

<!-- Und noch später... -->
<h2 id="kapitel2">Das ist das zweite Kapitel</h2>
<p>Hier steht der Inhalt des zweiten Kapitels...</p>
```

Ein Klick auf "Zum ersten Kapitel" lässt den Browser sofort zur Überschrift mit der `id="kapitel1"` springen.

**Absolute Links:** Links müssen nicht auf Dateien im selben Projektordner verweisen. Sie können auf jede beliebige Adresse im gesamten World Wide Web zeigen. Solche Links, die das Protokoll (`https://`) und den vollständigen Domainnamen enthalten, nennt man absolute URLs.

```html
<p>Eine großartige Quelle für Web-Dokumentation ist das <a href="https://developer.mozilla.org/">MDN Web Docs</a>.</p>
```

**Links zu anderen Ressourcen:** Hypertext ist nicht auf Text beschränkt – es ist Hyper*media*. Ein Link kann auf jede Art von Ressource verweisen: ein PDF-Dokument, ein Bild, eine Videodatei oder eine ZIP-Datei zum Herunterladen.

```html
<a href="downloads/research-paper.pdf">Forschungsarbeit als PDF herunterladen</a>
```

**Funktionale Links:** Links können sogar Aktionen auslösen, wie zum Beispiel das E-Mail-Programm des Nutzers zu öffnen.

```html
<a href="mailto:kontakt@beispiel.de">Schreibe uns eine E-Mail</a>
```

#### Die philosophische Bedeutung

Das Hypertext-Konzept hat die Art und Weise, wie wir auf Informationen zugreifen und sie konsumieren, grundlegend verändert. Es hat die traditionelle Hierarchie zwischen Autor und Leser aufgebrochen. In einem Hypertext-System ist der Leser nicht länger ein passiver Empfänger, sondern ein aktiver Navigator. Er entscheidet selbst, welche Verbindungen er verfolgt und welche Informationen für ihn relevant sind.

Diese Dezentralisierung und die Ermächtigung des Nutzers sind das Herzstück des offenen Webs. Jeder kann ein Dokument erstellen und es mit jedem anderen Dokument auf der Welt verknüpfen. Es gibt keine zentrale Instanz, die diese Verknüpfungen genehmigen muss. Diese Freiheit hat eine beispiellose Explosion von Kreativität und Wissensaustausch ermöglicht. Das World Wide Web ist im Grunde ein gigantisches, chaotisches, aber unglaublich leistungsfähiges Hypertext-System, das von Millionen von Menschen gleichzeitig aufgebaut und navigiert wird.

Wenn du also das nächste Mal ein `<a>`-Tag schreibst, denke einen Moment daran, dass du nicht nur einen simplen Link erzeugst. Du webst einen weiteren Faden in das große, globale Netz der Informationen. Du nutzt ein Konzept, das älter ist als das Web selbst, und trägst dazu bei, die Struktur zu schaffen, die das digitale Zeitalter definiert. Der Link ist die fundamentale Einheit des Webs, und das Hypertext-Konzept ist seine Seele.
