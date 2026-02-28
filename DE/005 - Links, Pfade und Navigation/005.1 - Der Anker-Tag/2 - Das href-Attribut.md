# Das href-Attribut

### Das href-Attribut: Das Herzstück jedes Links

Wenn der Anker-Tag `<a>` das Fahrzeug für die Navigation im Web ist, dann ist das `href`-Attribut sein Motor und sein Navigationssystem in einem. Ohne `href` ist ein `<a>`-Element nur ein Stück Text ohne Funktion. Erst dieses Attribut haucht ihm Leben ein und sagt dem Browser, wohin die Reise gehen soll, wenn ein Nutzer darauf klickt. Der Name `href` ist eine Abkürzung für "Hypertext Reference" und beschreibt damit exakt seine Aufgabe: Es ist die Referenz, das Ziel des Hyperlinks.

Stell dir vor, du schreibst einen Brief und möchtest den Empfänger auf eine andere Adresse verweisen. Du würdest die Adresse vollständig aufschreiben. Im Web ist das `href`-Attribut genau diese Adressangabe.

Die grundlegende Syntax ist denkbar einfach:

```html
<a href="ziel-adresse">Klickbarer Text</a>
```

Was du als "ziel-adresse" einsetzt, kann jedoch sehr unterschiedlich sein und bestimmt maßgeblich das Verhalten des Links. Lass uns die verschiedenen Arten von Zielen, die du mit dem `href`-Attribut ansteuern kannst, im Detail betrachten.

#### 1. Absolute URLs: Der Weg in die weite Welt

Die gebräuchlichste Form der Verlinkung ist die zu einer komplett anderen Webseite. Wenn du von deiner Seite auf Google, Wikipedia oder den Blog eines Freundes verlinken möchtest, verwendest du eine sogenannte **absolute URL**.

Eine absolute URL ist eine vollständige Webadresse, die alle Informationen enthält, die ein Browser benötigt, um eine Ressource im Internet eindeutig zu finden. Sie besteht typischerweise aus:

*   **Protokoll:** Meist `https://` (oder das veraltete `http://`).
*   **Domain:** Der Name der Webseite, z. B. `www.wikipedia.org`.
*   **Pfad:** Der spezifische Ort der Datei auf dem Server, z. B. `/wiki/HTML`.

Zusammengesetzt ergibt das eine vollständige Adresse.

```html
<a href="https://www.wikipedia.org/wiki/HTML">Erfahre mehr über HTML auf Wikipedia</a>
```

Wenn ein Nutzer auf diesen Link klickt, weiß der Browser unmissverständlich: "Verlasse die aktuelle Seite (oder öffne einen neuen Tab) und lade den Inhalt von dieser exakten Adresse."

**Wichtig:** Bei der Verlinkung zu externen Seiten musst du immer das Protokoll (`https://` oder `http://`) angeben. Lässt du es weg, würde der Browser annehmen, dass du eine Seite innerhalb deiner eigenen Website meinst, was zu einem Fehler führen würde.

#### 2. Relative Pfade: Die Navigation im eigenen Haus

Mindestens genauso oft wie du nach außen verlinkst, wirst du innerhalb deiner eigenen Website navigieren. Du möchtest von der Startseite zur "Über uns"-Seite, von dort zum Kontaktformular und wieder zurück. Hierfür wären absolute URLs umständlich und fehleranfällig. Was passiert, wenn du deine Website von einer Test-Domain auf die endgültige Domain umziehst? Du müsstest jeden einzelnen Link anpassen.

Genau hier kommen **relative Pfade** ins Spiel. Sie beschreiben den Weg vom aktuellen Dokument zum Zieldokument. Stell dir die Ordnerstruktur deiner Website wie die Räume in einem Haus vor. Ein relativer Pfad ist wie eine Wegbeschreibung: "Gehe aus diesem Raum raus, den Flur entlang und dann in die zweite Tür links."

Schauen wir uns eine typische Projektstruktur an:

```
projekt/
├── index.html
├── ueber-uns.html
└── kontakt/
    └── impressum.html
└── bilder/
    └── logo.png
```

##### Auf derselben Ebene verlinken

Angenommen, du bist in der Datei `index.html` und möchtest zur Seite `ueber-uns.html` verlinken. Da beide Dateien im selben Ordner (`projekt/`) liegen, reicht es, einfach den Dateinamen anzugeben.

```html
<!-- Dieser Code steht in index.html -->
<a href="ueber-uns.html">Lerne unser Team kennen</a>
```

Der Browser interpretiert das als: "Suche im selben Verzeichnis, in dem sich die aktuelle Datei befindet, nach einer Datei namens `ueber-uns.html`."

##### In einen Unterordner verlinken

Wenn du von der `index.html` auf das `impressum.html` verlinken willst, musst du dem Browser sagen, dass er zuerst in den Ordner `kontakt/` gehen soll.

```html
<!-- Dieser Code steht in index.html -->
<a href="kontakt/impressum.html">Zum Impressum</a>
```

Du gibst also den Namen des Ordners an, gefolgt von einem Schrägstrich (`/`) und dann dem Dateinamen.

##### Aus einem Unterordner heraus verlinken

Jetzt wird es interessant. Du bist im `impressum.html` (also im Ordner `kontakt/`) und möchtest zurück zur Startseite `index.html`. Du musst dem Browser sagen, dass er eine Ordnerebene "nach oben" gehen soll. Das machst du mit zwei Punkten und einem Schrägstrich (`../`).

```html
<!-- Dieser Code steht in kontakt/impressum.html -->
<a href="../index.html">Zurück zur Startseite</a>
```

`../` bedeutet "gehe eine Verzeichnisebene höher". Von `kontakt/` aus landest du wieder im Hauptordner `projekt/`, wo die `index.html` liegt. Müsstest du zwei Ebenen nach oben, würdest du `../../` schreiben.

##### Wurzelrelative Pfade: Der universelle Startpunkt

Es gibt noch eine dritte Art von Pfaden, die eine Mischung aus der Kürze relativer und der Eindeutigkeit absoluter Pfade darstellt: der **wurzelrelative Pfad**. Er beginnt immer mit einem Schrägstrich (`/`).

Dieser Schrägstrich sagt dem Browser: "Beginne die Suche nicht im aktuellen Ordner, sondern im Stammverzeichnis (der 'Root') der gesamten Website."

Egal, ob du dich in `index.html` oder in `kontakt/impressum.html` befindest, der Link zum Impressum sieht mit einem wurzelrelativen Pfad immer gleich aus:

```html
<!-- Dieser Link funktioniert von überall auf der Website -->
<a href="/kontakt/impressum.html">Zum Impressum</a>
```

Der Vorteil ist, dass du diese Links kopieren und auf jeder beliebigen Seite deiner Website einfügen kannst, ohne sie anpassen zu müssen. Sie sind robust gegenüber Verschiebungen von Dateien, solange die Gesamtstruktur ab dem Stammverzeichnis gleich bleibt.

#### 3. Ankerlinks: Sprungmarken innerhalb einer Seite

Manchmal möchtest du nicht auf eine andere Seite verlinken, sondern zu einem bestimmten Abschnitt auf derselben Seite springen. Das ist besonders bei langen Artikeln oder FAQs nützlich, um ein Inhaltsverzeichnis zu erstellen. Diese Sprungmarken nennt man **Ankerlinks**.

Dazu benötigst du zwei Dinge:

1.  **Das Ziel:** Ein Element auf der Seite, das eine eindeutige `id` besitzt. Meistens ist das eine Überschrift.
2.  **Den Link:** Ein `<a>`-Tag, dessen `href`-Attribut mit einem Hashtag (`#`) beginnt, gefolgt von der `id` des Zielelements.

Schauen wir uns das an einem Beispiel an:

```html
<!-- Oben auf der Seite: Das Inhaltsverzeichnis -->
<nav>
  <ul>
    <li><a href="#kapitel1">Zu Kapitel 1</a></li>
    <li><a href="#kapitel2">Zu Kapitel 2</a></li>
  </ul>
</nav>

<!-- Weiter unten im Text: Die Zielelemente mit ihren IDs -->
<h2 id="kapitel1">Das ist Kapitel 1</h2>
<p>Hier steht sehr viel Text...</p>

<h2 id="kapitel2">Das ist Kapitel 2</h2>
<p>Hier steht noch mehr Text...</p>
```

Klickst du auf den Link "Zu Kapitel 2", scrollt der Browser die Seite automatisch so, dass die Überschrift mit der `id="kapitel2"` am oberen Rand des sichtbaren Bereichs erscheint.

Dieses Prinzip funktioniert auch seitenübergreifend. Du kannst von der Startseite direkt zu einem bestimmten Abschnitt auf der "Über uns"-Seite springen:

```html
<a href="ueber-uns.html#team">Direkt zum Team-Abschnitt</a>
```

#### 4. Spezielle Protokolle: Mehr als nur Webseiten

Das `href`-Attribut kann nicht nur HTTP-Protokolle verarbeiten. Es gibt einige spezielle Schemata, die Aktionen im Betriebssystem des Nutzers auslösen können.

##### E-Mails senden mit `mailto:`

Du kannst einen Link erstellen, der beim Klick das Standard-E-Mail-Programm des Nutzers öffnet und bereits eine Empfängeradresse eingetragen hat.

```html
<a href="mailto:info@beispiel.de">Schreib uns eine E-Mail</a>
```

Du kannst sogar noch weiter gehen und einen Betreff und einen vordefinierten Text für die E-Mail mitgeben. Die Parameter werden mit einem Fragezeichen (`?`) an die Adresse angehängt und mit einem Und-Zeichen (`&`) voneinander getrennt. Leerzeichen müssen dabei speziell kodiert werden (meist als `%20`).

```html
<a href="mailto:info@beispiel.de?subject=Anfrage%20von%20der%20Webseite&body=Sehr%20geehrte%20Damen%20und%20Herren,">
  Kontakt mit vorausgefülltem Betreff
</a>
```

##### Anrufe starten mit `tel:`

Auf mobilen Geräten ist es extrem nützlich, Telefonnummern klickbar zu machen. Das `tel:`-Protokoll sorgt dafür, dass sich die Telefon-App mit der angegebenen Nummer öffnet.

```html
<a href="tel:+491234567890">Ruf uns an: +49 123 4567890</a>
```

Es ist eine gute Praxis, die Nummer im internationalen Format mit einem Pluszeichen (`+`) und der Landesvorwahl anzugeben.

##### Das Hashtag als Platzhalter

Manchmal möchtest du einen Link haben, der zwar wie ein Link aussieht, aber beim Klick (noch) nirgendwo hinführen soll. Dies ist oft der Fall, wenn die Funktionalität des Links später mit JavaScript hinzugefügt wird. In solchen Fällen wird oft ein Hashtag als Platzhalter verwendet.

```html
<a href="#">Ein Link, der nichts tut</a>
```

Ein Klick auf diesen Link führt die Seite nicht neu, aber er hat einen kleinen Nebeneffekt: Der Browser springt an den Anfang der Seite. Dieses Verhalten ist wichtig zu kennen, wenn du beginnst, mit JavaScript zu interagieren.

Das `href`-Attribut ist also weitaus mehr als nur eine einfache Adressangabe. Es ist ein mächtiges Werkzeug, mit dem du die gesamte Navigation deiner Website steuerst, den Nutzer zu externen Quellen führst, ihm die Interaktion per E-Mail oder Telefon erleichterst und die Struktur innerhalb deiner eigenen Dokumente zugänglich machst. Die Beherrschung seiner verschiedenen Formen – absolut, relativ, Anker und spezielle Protokolle – ist ein fundamentaler Baustein auf deinem Weg zum kompetenten Webentwickler.
