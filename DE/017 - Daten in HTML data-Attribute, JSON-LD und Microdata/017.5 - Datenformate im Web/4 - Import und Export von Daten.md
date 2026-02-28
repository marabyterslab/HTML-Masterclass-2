# Import und Export von Daten

# Import und Export von Daten: Deine Webseite im Datenaustausch

Eine Webseite ist selten eine isolierte Insel. Vielmehr ist sie Teil eines riesigen, vernetzten Ökosystems. Daten fließen ständig hin und her: von Servern zu Browsern, von einer Anwendung zur nächsten, von deiner Webseite zu den Nutzern und umgekehrt. In diesem Kapitel werfen wir einen genauen Blick darauf, wie du Daten gezielt exportieren und importieren kannst. Dabei geht es nicht nur um den klassischen Download-Button, sondern auch um die grundlegenden Mechanismen, die das moderne Web antreiben.

### Daten exportieren: Was deine Seite der Welt anbietet

Wenn wir von "Export" sprechen, meinen wir im einfachsten Fall, dass ein Nutzer Daten von deiner Webseite auf seinen eigenen Computer herunterladen kann. Das können Berichte, Tabellen, Bilder oder Konfigurationsdateien sein. HTML bietet hierfür einfache, aber mächtige Werkzeuge.

#### Der klassische Weg: Der `download`-Attribut

Der vertrauteste Weg, einen Download anzubieten, ist ein einfacher Link. Normalerweise führt ein Klick auf einen `<a>`-Tag zur verlinkten Ressource und der Browser versucht, sie anzuzeigen – eine HTML-Seite wird gerendert, ein Bild angezeigt, ein PDF im Browser-Plugin geöffnet.

Mit dem `download`-Attribut kannst du dieses Verhalten ändern. Es signalisiert dem Browser: "Zeige diese Datei nicht an, sondern biete sie dem Nutzer direkt zum Speichern an."

Stell dir vor, du bietest einen monatlichen Bericht als CSV-Datei an. Der HTML-Code dafür wäre denkbar einfach:

```html
<a href="/daten/monatsbericht-juni.csv" download>Monatsbericht Juni herunterladen</a>
```

Sobald ein Nutzer auf diesen Link klickt, öffnet sich der "Speichern unter..."-Dialog seines Betriebssystems. Der Dateiname wird aus der URL übernommen, in diesem Fall `monatsbericht-juni.csv`.

Das Schöne daran ist, dass du dem `download`-Attribut auch einen Wert zuweisen kannst. Dieser Wert wird dann als vorgeschlagener Dateiname verwendet. Das ist besonders nützlich, wenn deine URLs nicht sehr sprechend sind, zum Beispiel bei dynamisch generierten Dateien.

```html
<a href="/api/generate-report.php?id=123" download="Kundenbericht_Q2_2024.csv">
  Quartalsbericht für Kunde 123 herunterladen
</a>
```

Hier würde der Nutzer die Datei unter dem Namen `Kundenbericht_Q2_2024.csv` speichern, obwohl die URL ganz anders aussieht.

#### Daten im laufenden Betrieb erzeugen: Data URIs

Manchmal liegen die Daten, die du zum Download anbieten möchtest, nicht als fertige Datei auf dem Server. Vielleicht werden sie direkt im Browser durch eine Nutzereingabe oder eine JavaScript-Funktion erzeugt. Hier kommen Data URIs ins Spiel.

Ein Data URI (Uniform Resource Identifier) erlaubt es dir, Daten direkt im Link selbst zu kodieren, anstatt auf eine externe Datei zu verweisen. Das Schema ist einfach: `data:[<mediatype>][;base64],<data>`.

Für eine einfache Textdatei könnte das so aussehen:

```html
<a href="data:text/plain;charset=utf-8,Hallo Welt! Dies ist der Inhalt meiner Datei." download="hallo.txt">
  Dynamische Textdatei herunterladen
</a>
```

Ein Klick auf diesen Link erzeugt eine Textdatei namens `hallo.txt` mit dem angegebenen Inhalt, ohne dass jemals eine Anfrage an einen Server gesendet wurde. Alles passiert direkt im Browser.

Für binäre Daten wie Bilder wird der Inhalt meist Base64-kodiert, um sicherzustellen, dass alle Zeichen URL-sicher sind. Data URIs sind extrem praktisch für kleine, dynamisch generierte Inhalte, stoßen aber bei großen Datenmengen schnell an ihre Grenzen, da die URL-Länge in den meisten Browsern limitiert ist.

#### Strukturierte Datenformate: CSV und JSON

Wenn Maschinen miteinander reden, brauchen sie eine gemeinsame Sprache. Einfacher Text ist oft nicht ausreichend, weil die Struktur fehlt. Hier kommen standardisierte Datenformate ins Spiel, allen voran CSV und JSON.

**CSV (Comma-Separated Values)** ist ein Urgestein des Datenaustauschs. Es ist ein einfaches textbasiertes Format, um tabellarische Daten darzustellen. Jede Zeile repräsentiert einen Datensatz, und die Werte innerhalb einer Zeile werden durch ein Trennzeichen – meist ein Komma – getrennt.

Eine typische CSV-Datei für Nutzerdaten könnte so aussehen:

```
ID,Vorname,Nachname,Email
1,Max,Mustermann,max@example.com
2,Erika,Mustermann,erika@example.com
3,John,Doe,john.doe@example.org
```

CSV ist leichtgewichtig, von Menschen lesbar und wird von praktisch jeder Tabellenkalkulationssoftware (wie Excel oder Google Sheets) verstanden. Wenn du also tabellarische Daten zum Export anbietest, ist CSV oft eine exzellente Wahl.

**JSON (JavaScript Object Notation)** ist das De-facto-Standardformat für moderne Web-APIs. Es ist ebenfalls textbasiert, aber im Gegensatz zu CSV kann es komplexe, verschachtelte Datenstrukturen abbilden, nicht nur flache Tabellen. Es kennt verschiedene Datentypen wie Zahlen, Zeichenketten, Booleans, Arrays und Objekte.

Die gleichen Nutzerdaten als JSON sähen so aus:

```json
[
  {
    "id": 1,
    "vorname": "Max",
    "nachname": "Mustermann",
    "email": "max@example.com"
  },
  {
    "id": 2,
    "vorname": "Erika",
    "nachname": "Mustermann",
    "email": "erika@example.com"
  },
  {
    "id": 3,
    "vorname": "John",
    "nachname": "Doe",
    "email": "john.doe@example.org"
  }
]
```

JSON ist die bevorzugte Wahl, wenn Daten programmatisch weiterverarbeitet werden sollen, da es sich direkt in JavaScript-Objekte (und ähnliche Strukturen in anderen Sprachen) umwandeln lässt.

Für den Export über HTML ändert sich nichts am Prinzip: Du bietest eine `.csv`- oder `.json`-Datei über einen `<a>`-Tag mit dem `download`-Attribut an. Die Erzeugung dieser Datei geschieht jedoch in der Regel serverseitig.

### Daten importieren: Wie deine Seite Informationen aufnimmt

Der Import von Daten ist das Gegenstück zum Export. Hier geht es darum, Daten von außerhalb in deine Webanwendung zu laden, sei es durch eine Nutzeraktion oder automatisiert aus einer anderen Quelle.

#### Der Startpunkt: Das `<input type="file">`-Element

Wenn du einem Nutzer erlauben möchtest, eine Datei von seinem Computer hochzuladen, ist das `<input type="file">`-Element das Mittel der Wahl. Es ist das Tor, durch das Daten in deine Anwendung gelangen können.

```html
<label for="file-upload">Wähle eine CSV-Datei zum Importieren aus:</label>
<input type="file" id="file-upload" name="userfile">
```

Dieses simple HTML-Element rendert einen Button, der den Dateiauswahldialog des Betriebssystems öffnet. Allein kann dieses Element jedoch nichts weiter tun, als die Auswahl einer Datei zu ermöglichen. Die eigentliche Verarbeitung der Datei geschieht nicht mit HTML, sondern mit JavaScript im Frontend oder durch das Absenden eines Formulars an ein Backend.

Mit dem `accept`-Attribut kannst du dem Browser einen Hinweis geben, welche Dateitypen der Nutzer auswählen sollte. Dies ist keine Sicherheitsmaßnahme, sondern eine Hilfe für den Nutzer, da der Dateidialog die Auswahl entsprechend filtern kann.

```html
<input type="file" id="json-importer" accept=".json, application/json">
```

#### Die Verarbeitung im Browser mit JavaScript

Sobald ein Nutzer eine Datei ausgewählt hat, kann JavaScript darauf zugreifen und sie direkt im Browser verarbeiten. Dies ist besonders nützlich für clientseitige Anwendungen, bei denen Daten nicht zwingend an einen Server gesendet werden müssen.

Mit der `FileReader`-API kann JavaScript den Inhalt der ausgewählten Datei lesen. Stell dir vor, ein Nutzer lädt eine JSON-Datei mit Konfigurationseinstellungen hoch.

Der HTML-Teil bleibt einfach:
```html
<input type="file" id="config-loader" accept=".json">
<pre id="output"></pre>
```

Der dazugehörige JavaScript-Code würde auf eine Änderung des Inputs lauschen, die Datei lesen und den Inhalt verarbeiten:

```javascript
const fileInput = document.getElementById('config-loader');
const outputElement = document.getElementById('output');

fileInput.addEventListener('change', (event) => {
  const file = event.target.files[0];

  if (!file) {
    return;
  }

  const reader = new FileReader();

  reader.onload = (e) => {
    try {
      const fileContent = e.target.result;
      const configData = JSON.parse(fileContent);
      // Die JSON-Daten sind nun als JavaScript-Objekt verfügbar
      // Hier könntest du die Einstellungen in deiner Anwendung anwenden
      outputElement.textContent = JSON.stringify(configData, null, 2);
    } catch (error) {
      outputElement.textContent = 'Fehler: Die Datei konnte nicht als JSON verarbeitet werden.';
    }
  };

  reader.readAsText(file);
});
```
In diesem Beispiel stellt HTML die Benutzeroberfläche (`<input>`) und den Anzeigeort (`<pre>`) bereit. JavaScript füllt die Lücke, indem es die Logik für das Lesen und Verarbeiten der Datei liefert. Dies ist ein perfektes Beispiel für das Zusammenspiel der Kerntechnologien des Webs.

#### Automatischer Import: Daten von APIs abrufen

Der häufigste Anwendungsfall für den Datenimport im modernen Web ist jedoch nicht der manuelle Upload durch einen Nutzer, sondern der automatische Abruf von Daten über eine API (Application Programming Interface). Deine Webseite kann wie ein Client agieren, der Daten von einem Server anfordert – zum Beispiel aktuelle Wetterdaten, Börsenkurse oder die neuesten Beiträge eines Blogs.

Dieser Prozess wird fast ausschließlich von JavaScript gesteuert, typischerweise mit der `fetch()`-API. HTML spielt hier die Rolle des strukturellen Behälters, der die abgerufenen Daten aufnimmt und darstellt.

Ein typisches Szenario: Du möchtest eine Liste von Nutzern von einer API laden und anzeigen.

Dein HTML könnte einen leeren Platzhalter enthalten:
```html
<h1>Unsere Teammitglieder</h1>
<ul id="user-list">
  <li>Daten werden geladen...</li>
</ul>
```

Das dazugehörige JavaScript holt die Daten und füllt die Lücke:
```javascript
const userListElement = document.getElementById('user-list');

fetch('https://api.example.com/users')
  .then(response => {
    if (!response.ok) {
      throw new Error('Netzwerkantwort war nicht in Ordnung.');
    }
    return response.json(); // Wandelt die Antwort in ein JSON-Objekt um
  })
  .then(users => {
    userListElement.innerHTML = ''; // Leert die "Laden..."-Nachricht
    users.forEach(user => {
      const listItem = document.createElement('li');
      listItem.textContent = `${user.name} (${user.email})`;
      userListElement.appendChild(listItem);
    });
  })
  .catch(error => {
    userListElement.innerHTML = '<li>Fehler beim Laden der Daten.</li>';
    console.error('Fetch-Fehler:', error);
  });
```

Hier siehst du erneut die klare Arbeitsteilung: HTML definiert, *wo* die Daten erscheinen sollen und stellt eine anfängliche Struktur bereit. JavaScript kümmert sich um den gesamten Prozess des Abrufens, Verarbeitens und Einfügens der Daten in diese Struktur. Die Daten selbst werden dabei üblicherweise im JSON-Format übertragen.

### Ein breiteres Verständnis von Import und Export

Wenn du die Konzepte aus diesem Modul – `data-`Attribute, JSON-LD und Microdata – mit einbeziehst, erweitert sich die Bedeutung von Import und Export. Strukturierte Daten wie JSON-LD, die du in den `<head>` deiner Seite einbettest, sind eine Form des *passiven Exports*. Du stellst deine Daten nicht aktiv zum Download bereit, aber du machst sie maschinenlesbar verfügbar für jeden, der sie abrufen und verstehen möchte – allen voran Suchmaschinen.

Wenn der Googlebot deine Seite crawlt und das JSON-LD für ein Rezept findet, *importiert* er diese strukturierten Daten in seine eigenen Systeme, um sie in den Suchergebnissen als Rich Snippet anzuzeigen. Dein HTML wird so zu einer API für die Welt. Import und Export sind also nicht nur auf Klicks und Dateien beschränkt, sondern sind fundamentale Prinzipien des Datenaustauschs im Web, die auf vielen verschiedenen Ebenen stattfinden.
