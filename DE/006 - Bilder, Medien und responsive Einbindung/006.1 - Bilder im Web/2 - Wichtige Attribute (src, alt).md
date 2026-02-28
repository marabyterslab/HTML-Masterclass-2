# Wichtige Attribute (src, alt)

### Die Seele eines Bildes – Die Attribute `src` und `alt`

Ein Bild in HTML einzubinden, beginnt immer mit dem `<img>`-Tag. Doch wenn du nur `<img`> in deinen Code schreibst, passiert rein gar nichts. Dieser Tag ist von Natur aus leer, ein reiner Platzhalter. Er wird erst durch seine Attribute mit Leben gefüllt. Zwei dieser Attribute sind so fundamental, dass ohne sie ein Bild weder existieren noch seinen vollen Zweck erfüllen kann: `src` und `alt`. Man könnte sie als das Herz und die Seele jedes Bildes im Web bezeichnen.

#### `src` – Der Wegweiser zum Bild

Das Attribut `src` ist die Abkürzung für „source“, also Quelle. Es ist die absolut unverzichtbare Wegbeschreibung für den Browser. Du teilst ihm damit mit, wo genau die Bilddatei liegt, die er an dieser Stelle anzeigen soll. Ohne ein `src`-Attribut weiß der Browser nicht, *was* er darstellen soll, und das `<img>`-Element bleibt unsichtbar und funktionslos.

Stell dir das `src`-Attribut wie eine genaue Adressangabe vor. Je nachdem, von wo du kommst und wohin du willst, kann diese Adresse unterschiedlich aussehen. Im Web-Kontext unterscheiden wir hauptsächlich zwischen drei Arten von Pfaden, die du im `src`-Attribut verwenden kannst.

##### 1. Relative Pfade

Ein relativer Pfad beschreibt den Ort einer Datei im Verhältnis zur aktuellen HTML-Datei. Das ist die gebräuchlichste und flexibelste Methode für Bilder, die Teil deines eigenen Webprojekts sind.

*   **Im selben Ordner:** Wenn sich deine Bilddatei (`logo.png`) im exakt selben Ordner wie deine HTML-Datei (`index.html`) befindet, ist der Pfad denkbar einfach:

    ```html
    <img src="logo.png">
    ```

*   **In einem Unterordner:** In den meisten Projekten ist es sinnvoll, Bilder zur besseren Übersicht in einem eigenen Ordner (z.B. `bilder` oder `images`) zu sammeln. Liegt deine `index.html` im Hauptverzeichnis und das Bild `hero.jpg` im Unterordner `bilder`, sieht der Pfad so aus:

    ```html
    <img src="bilder/hero.jpg">
    ```
    Du sagst dem Browser also: „Gehe von hier aus in den Ordner `bilder` und lade dort die Datei `hero.jpg`“.

*   **In einem übergeordneten Ordner:** Manchmal musst du aus einem Unterordner heraus auf ein Bild zugreifen, das eine Ebene höher liegt. Stell dir vor, du hast eine HTML-Datei in `seiten/kontakt.html` und möchtest auf das `logo.png` im Hauptverzeichnis zugreifen. Dafür verwendest du zwei Punkte und einen Schrägstrich (`../`):

    ```html
    <img src="../logo.png">
    ```
    `../` bedeutet „gehe eine Verzeichnisebene nach oben“.

Der große Vorteil von relativen Pfaden ist die Portabilität. Du kannst deinen gesamten Projektordner auf einen anderen Server oder einen anderen Computer verschieben, und alle Bildverknüpfungen funktionieren weiterhin, solange die interne Ordnerstruktur erhalten bleibt.

##### 2. Absolute Pfade vom Web-Root

Ein absoluter Pfad beginnt immer mit einem Schrägstrich (`/`). Dieser Schrägstrich repräsentiert das Stammverzeichnis (Root) deiner Website auf dem Webserver. Egal, in welchem Unterordner sich deine HTML-Datei befindet, ein Pfad, der mit `/` beginnt, startet die Suche immer ganz oben in der Hierarchie deiner Website.

Angenommen, dein Logo liegt immer im Ordner `images` direkt im Stammverzeichnis deiner Domain. Dann kannst du von jeder beliebigen Unterseite deiner Website aus darauf zugreifen mit:

```html
<img src="/images/logo.png">
```

Diese Methode ist nützlich in sehr großen, verschachtelten Projekten, da du dir keine Gedanken darüber machen musst, wie viele Ebenen du mit `../` nach oben klettern musst. Du hast einen festen, verlässlichen Ankerpunkt.

##### 3. Absolute URLs

Du bist nicht darauf beschränkt, nur Bilder von deinem eigenen Server zu laden. Du kannst auch eine vollständige URL als Quelle angeben, um ein Bild von einer völlig anderen Website zu laden.

```html
<img src="https://images.pexels.com/photos/12345/beispiel-bild.jpeg">
```

Dies wird oft für die Einbindung von Bildern über Content Delivery Networks (CDNs) oder Bild-Hosting-Dienste genutzt. Bedenke dabei jedoch, dass du eine Abhängigkeit zu einem externen Dienst schaffst. Ist dieser Dienst nicht erreichbar, wird auch dein Bild nicht geladen. Außerdem solltest du immer sicherstellen, dass du die Lizenz- und Urheberrechte für das „Hotlinking“, also das direkte Verlinken von fremden Ressourcen, besitzt.

#### `alt` – Die Stimme des Bildes

Während `src` dem Browser sagt, *wo* das Bild ist, erklärt das `alt`-Attribut, *was* das Bild ist. `alt` steht für „Alternativtext“. Dieser Text ist aus mehreren fundamentalen Gründen nicht nur eine gute Praxis, sondern eine absolute Notwendigkeit für eine professionelle und zugängliche Website.

##### 1. Barrierefreiheit (Accessibility)

Das ist der wichtigste Grund für die Existenz des `alt`-Attributs. Menschen mit Sehbehinderungen nutzen sogenannte Screenreader – Software, die den Inhalt einer Webseite vorliest. Ein Screenreader kann ein Bild nicht „sehen“. Wenn er auf ein `<img>`-Tag stößt, liest er stattdessen den Inhalt des `alt`-Attributs vor.

*   **Ohne `alt`-Text:** Der Screenreader sagt vielleicht „Bild“ oder liest den Dateinamen vor, wie „IMG_8472.jpg“. Das ist für den Nutzer völlig nutzlos und reißt ihn aus dem Kontext.
*   **Mit gutem `alt`-Text:** Der Nutzer erhält eine Beschreibung, die den Inhalt und Zweck des Bildes vermittelt und ihm ein vollständiges Verständnis der Seite ermöglicht.

Ohne `alt`-Text schließt du einen Teil der Nutzer von den Informationen auf deiner Seite aus. Das Web ist für alle da, und der `alt`-Text ist ein entscheidender Baustein dafür.

##### 2. Suchmaschinenoptimierung (SEO)

Suchmaschinen wie Google sind im Grunde blind. Sie können zwar immer besser Bildinhalte analysieren, aber ihre primäre Informationsquelle über den Inhalt eines Bildes ist und bleibt der `alt`-Text. Indem du eine präzise Beschreibung im `alt`-Attribut lieferst, hilfst du der Suchmaschine zu verstehen, worum es in dem Bild geht. Das verbessert nicht nur die Chancen, dass dein Bild in der Bildersuche gefunden wird, sondern stärkt auch den thematischen Kontext deiner gesamten Seite, was sich positiv auf dein allgemeines Ranking auswirken kann.

##### 3. Fallback bei Anzeigeproblemen

Was passiert, wenn die im `src`-Attribut angegebene Bilddatei nicht gefunden wird? Vielleicht hast du dich im Pfad vertippt, die Datei umbenannt oder der externe Server ist offline. In diesem Fall kann der Browser das Bild nicht laden. Stattdessen zeigt er ein unschönes „kaputtes Bild“-Symbol an. Wenn du jedoch einen `alt`-Text angegeben hast, wird dieser Text anstelle des Bildes angezeigt. Der Nutzer sieht dann zwar nicht das Bild, aber er versteht dank des Textes, was er hätte sehen sollen. Der Kontext der Seite bleibt erhalten.

##### Wie schreibt man guten Alternativtext?

Einen `alt`-Text zu schreiben ist eine Kunst für sich. Es geht darum, den Inhalt und die Funktion des Bildes prägnant zu vermitteln.

*   **Sei beschreibend, aber kurz:** Beschreibe, was auf dem Bild zu sehen ist. Vermeide überflüssige Floskeln wie „Ein Bild von …“ oder „Grafik, die zeigt …“. Der Browser und der Screenreader wissen bereits, dass es sich um ein Bild handelt.
    *   *Schlecht:* `<img src="hund.jpg" alt="Ein Bild von einem Hund">`
    *   *Gut:* `<img src="hund.jpg" alt="Ein Golden Retriever jagt einem roten Ball auf einer grünen Wiese.">`

*   **Berücksichtige den Kontext:** Der beste `alt`-Text hängt vom umgebenden Inhalt ab. Wenn ein Bild einen technischen Prozess illustriert, der bereits im Text ausführlich beschrieben wird, kann der `alt`-Text kürzer ausfallen. Wenn das Bild hingegen die einzige Quelle einer Information ist, muss der `alt`-Text diese Information vollständig wiedergeben.

*   **Sonderfall: Dekorative Bilder:** Manchmal dient ein Bild rein der Dekoration, zum Beispiel eine ornamentale Trennlinie oder ein abstraktes Hintergrundmuster. Solche Bilder tragen keinen inhaltlichen Wert. Würde ein Screenreader sie beschreiben, würde das den Lesefluss nur stören. In diesem Fall lässt du das `alt`-Attribut nicht weg, sondern du setzt es leer.

    ```html
    <img src="trennlinie.svg" alt="">
    ```
    Ein leeres `alt=""` ist ein klares Signal an assistive Technologien wie Screenreader: „Dieses Bild ist unwichtig, ignoriere es bitte.“ Ein komplett fehlendes `alt`-Attribut hingegen gilt als Fehler, da der Screenreader nicht weiß, ob der Entwickler es vergessen hat oder es absichtlich leer sein soll.

Zusammenfassend lässt sich sagen: `src` und `alt` sind ein unzertrennliches Duo. `src` ist die technische Anweisung, die das Visuelle auf den Bildschirm bringt. `alt` ist die menschliche und semantische Brücke, die sicherstellt, dass die Botschaft des Bildes jeden erreicht – Mensch wie Maschine, bei perfekter Verbindung und auch wenn mal etwas schiefgeht. Ein `<img>`-Tag ohne `src` ist nutzlos. Ein `<img>`-Tag ohne `alt` ist unvollständig und unprofessionell.
