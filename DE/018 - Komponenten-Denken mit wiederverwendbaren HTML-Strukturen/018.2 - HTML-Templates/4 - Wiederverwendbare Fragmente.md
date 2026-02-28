# Wiederverwendbare Fragmente

### Wiederverwendbare Fragmente: Das DRY-Prinzip im Web

Stell dir vor, du baust eine Website mit zehn verschiedenen Unterseiten. Jede Seite hat denselben Header mit dem Logo und der Navigation und denselben Footer mit den Kontaktinformationen und Social-Media-Links. Der intuitive, aber mühsame Weg wäre, den HTML-Code für den Header und den Footer zu schreiben und ihn dann in jede einzelne deiner zehn HTML-Dateien zu kopieren.

Das funktioniert zunächst. Aber was passiert, wenn du einen neuen Menüpunkt in der Navigation hinzufügen möchtest? Oder wenn sich die Telefonnummer im Footer ändert? Plötzlich musst du zehn verschiedene Dateien öffnen und an exakt den gleichen Stellen die exakt gleiche Änderung vornehmen. Bei zehn Seiten ist das vielleicht noch machbar, wenn auch nervig. Bei hundert Seiten wird es zu einem Albtraum und einer massiven Fehlerquelle.

Hier kommt ein fundamentales Prinzip der Softwareentwicklung ins Spiel: **DRY – Don't Repeat Yourself** (Wiederhole dich nicht). Die Idee ist einfach: Jede Information und jede Logik sollte nur an einer einzigen, unmissverständlichen Stelle in deinem System existieren. Für unser Webdesign-Beispiel bedeutet das: Der Code für den Header sollte nur einmal geschrieben werden. Der Code für den Footer ebenfalls.

Um dieses Prinzip in HTML umzusetzen, gibt es verschiedene Ansätze, die sich über die Jahre entwickelt haben. Sie reichen von serverseitigen Techniken bis hin zu modernen, reinen HTML- und JavaScript-Lösungen.

#### Der klassische Weg: Serverseitige Includes

Eine der ältesten und robustesten Methoden, um HTML-Fragmente wiederzuverwenden, findet auf dem Server statt, bevor die Seite überhaupt an deinen Browser geschickt wird. Technologien wie PHP, Python, Ruby oder Node.js können eine HTML-Seite aus mehreren Einzelteilen dynamisch zusammensetzen.

Nehmen wir PHP als Beispiel, da es auf unzähligen Webservern läuft und das Prinzip sehr einfach zu verstehen ist. Du würdest deinen Header in eine separate Datei namens `header.php` und deinen Footer in `footer.php` auslagern.

**`header.php`:**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meine fantastische Webseite</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <a href="/"><img src="logo.svg" alt="Logo"></a>
        <nav>
            <ul>
                <li><a href="/">Startseite</a></li>
                <li><a href="/ueber-uns.php">Über uns</a></li>
                <li><a href="/kontakt.php">Kontakt</a></li>
            </ul>
        </nav>
    </header>
```

**`footer.php`:**
```html
    <footer>
        <p>&copy; 2024 Meine fantastische Webseite</p>
        <p>Kontakt: info@beispiel.de</p>
    </footer>
</body>
</html>
```

Deine eigentliche Inhaltsseite, zum Beispiel `index.php`, würde dann sehr schlank aussehen. Anstelle des gesamten HTML-Grundgerüsts bindest du die Fragmente einfach mit einer einzigen Anweisung ein.

**`index.php`:**
```php
<?php include 'header.php'; ?>

<main>
    <h1>Willkommen auf der Startseite!</h1>
    <p>Das ist der einzigartige Inhalt dieser Seite.</p>
</main>

<?php include 'footer.php'; ?>
```

Wenn der Server eine Anfrage für `index.php` erhält, führt er den PHP-Code aus. Er liest den Inhalt von `header.php`, fügt ihn ein, dann den Inhalt von `index.php` selbst und schließlich den Inhalt von `footer.php`. An den Browser wird eine einzige, vollständige HTML-Datei gesendet. Der Browser merkt von diesem Prozess nichts.

Wenn du jetzt einen Menüpunkt ändern musst, bearbeitest du nur noch die `header.php`-Datei, und die Änderung erscheint automatisch auf allen Seiten, die diese Datei einbinden. Das ist das DRY-Prinzip in Aktion. Der große Vorteil ist, dass dies ohne JavaScript funktioniert und extrem performant ist. Der Nachteil: Du benötigst eine Serverumgebung, die diese Sprache (z. B. PHP) ausführen kann. Auf einer rein statischen Website, die du einfach per Doppelklick von deiner Festplatte öffnest, funktioniert das nicht.

#### Die moderne HTML-Lösung: Das `<template>`-Element

Was aber, wenn wir wiederverwendbare Fragmente direkt im Browser mit Bordmitteln von HTML und JavaScript verwalten wollen? Hierfür wurde das `<template>`-Element eingeführt.

Ein `<template>`-Tag ist ein besonderer Container. Sein Inhalt wird vom Browser zwar geparst, um sicherzustellen, dass das HTML valide ist, aber er wird **nicht gerendert**. Das bedeutet, der Inhalt ist unsichtbar, Skripte darin werden nicht ausgeführt und Bilder nicht geladen. Er ist sozusagen ein inaktiver, wiederverwendbarer Bauplan, der im Dokument darauf wartet, von JavaScript zum Leben erweckt zu werden.

Stell dir vor, du hast einen Online-Shop und möchtest für jedes Produkt eine identisch aufgebaute Produktkarte anzeigen. Der Code für so eine Karte könnte in einem Template liegen.

```html
<template id="produkt-karte-template">
    <div class="produkt-karte">
        <img class="produkt-bild" src="" alt="Produktbild">
        <h3 class="produkt-titel"></h3>
        <p class="produkt-beschreibung"></p>
        <span class="produkt-preis"></span>
        <button>In den Warenkorb</button>
    </div>
</template>

<main id="produkt-liste">
    <!-- Hier werden die Produktkarten per JavaScript eingefügt -->
</main>
```

Dieses Template schlummert nun im HTML-Dokument. Es ist da, aber es tut nichts. Um es zu nutzen, benötigen wir ein wenig JavaScript. Der Prozess ist immer der gleiche:

1.  Hole dir das Template-Element aus dem DOM.
2.  Greife auf seinen Inhalt zu (über die `.content`-Eigenschaft).
3.  Erstelle eine Kopie (einen "Klon") dieses Inhalts. Es ist wichtig, einen Klon zu erstellen, damit das Original-Template für weitere Kopien erhalten bleibt.
4.  Fülle den Klon mit den spezifischen Daten (z.B. Titel, Preis und Bild des jeweiligen Produkts).
5.  Füge den fertigen Klon an der gewünschten Stelle in die sichtbare Seite ein.

Der zugehörige JavaScript-Code könnte so aussehen:

```javascript
// Beispieldaten für unsere Produkte
const produkte = [
    {
        bild: 'bilder/schuhe.jpg',
        titel: 'Bequeme Laufschuhe',
        beschreibung: 'Perfekt für dein tägliches Training.',
        preis: '89,99 €'
    },
    {
        bild: 'bilder/rucksack.jpg',
        titel: 'Robuster Wanderrucksack',
        beschreibung: 'Dein Begleiter für jedes Abenteuer.',
        preis: '120,00 €'
    }
];

// Das Template und den Container für die Produkte holen
const template = document.getElementById('produkt-karte-template');
const container = document.getElementById('produkt-liste');

// Für jedes Produkt eine Karte erstellen
produkte.forEach(produkt => {
    // 1. & 2. & 3. Einen Klon des Template-Inhalts erstellen
    const klon = template.content.cloneNode(true);

    // 4. Den Klon mit den Produktdaten füllen
    klon.querySelector('.produkt-bild').src = produkt.bild;
    klon.querySelector('.produkt-titel').textContent = produkt.titel;
    klon.querySelector('.produkt-beschreibung').textContent = produkt.beschreibung;
    klon.querySelector('.produkt-preis').textContent = produkt.preis;

    // 5. Den fertigen Klon in den sichtbaren Bereich der Seite einfügen
    container.appendChild(klon);
});
```

Dieser Ansatz ist extrem mächtig. Du definierst die Struktur deines Fragments einmal sauber in HTML und befüllst es dann dynamisch mit beliebigen Daten. Dies ist die Grundlage für das, was wir als "Komponenten-Denken" bezeichnen – die Zerlegung einer Benutzeroberfläche in kleine, wiederverwendbare und in sich geschlossene Bausteine.

#### Flexibilität durch Slots: Platzhalter in Templates

Das `<template>`-Element ist fantastisch für starre Strukturen. Aber was, wenn wir eine Komponente erstellen wollen, die zwar einen festen Rahmen hat, deren Inhalt aber von außen flexibel befüllt werden soll? Ein Beispiel wäre eine Dialogbox, die immer gleich aussieht (Rahmen, Schließen-Button), aber mal einen Text, mal eine Liste oder mal ein Formular enthalten soll.

Hier kommt das `<slot>`-Element ins Spiel. Ein `<slot>` ist ein Platzhalter innerhalb eines Templates. Wenn das Template als Teil eines sogenannten "Web Components" verwendet wird (ein fortgeschrittenes Thema, das auf diesen Grundlagen aufbaut), kann der Inhalt für diese Slots von außen bereitgestellt werden.

Ein einfaches Template für eine Infobox könnte so aussehen:

```html
<template id="info-box-template">
    <div class="info-box">
        <header class="info-box-header">
            <h2>
                <slot name="box-titel">Standardüberschrift</slot>
            </h2>
        </header>
        <div class="info-box-inhalt">
            <slot name="box-inhalt">Hier steht der Standardinhalt.</slot>
        </div>
    </div>
</template>
```

Das `<slot>`-Element hat hier einen `name`-Attribut. Damit können wir gezielt Inhalte in bestimmte Platzhalter einfügen. Der Text innerhalb des Slot-Tags (`Standardüberschrift`) dient als Fallback, falls von außen kein Inhalt bereitgestellt wird.

Die Kombination aus `<template>` und `<slot>` bildet das Herzstück der nativen Web Components. Sie ermöglicht es uns, echte, wiederverwendbare HTML-Komponenten zu bauen, die gekapselt sind und eine klare Schnittstelle nach außen haben – ganz ohne große JavaScript-Frameworks.

Ob du den klassischen serverseitigen Weg oder den modernen clientseitigen Ansatz mit Templates wählst, hängt von deinem Projekt ab. Das zugrundeliegende Ziel ist jedoch dasselbe: Schreibe deinen Code einmal, halte ihn an einem zentralen Ort und vermeide die mühsame und fehleranfällige Arbeit des Kopierens und Einfügens. Dein zukünftiges Ich wird es dir danken.
