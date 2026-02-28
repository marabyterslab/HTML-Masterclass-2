# Absolute vs. relative Pfade

### Absolute vs. Relative Pfade: Der Wegweiser deiner Website

Stell dir vor, du möchtest einem Freund den Weg zu einem Café beschreiben. Du hast zwei Möglichkeiten. Entweder gibst du ihm die vollständige, offizielle Adresse: "Deutschland, 10117 Berlin, Unter den Linden 77". Das ist eine **absolute** Angabe. Egal, wo auf der Welt sich dein Freund befindet, mit dieser Adresse und einem Navi findet er das Ziel.

Oder du sagst ihm, während ihr beide auf dem Marktplatz steht: "Geh von hier aus geradeaus über den Platz, dann die zweite Straße links und nach 100 Metern siehst du es auf der rechten Seite." Das ist eine **relative** Angabe. Sie ist kurz, praktisch und funktioniert perfekt – aber nur von eurem gemeinsamen Ausgangspunkt aus. Würde er versuchen, dieser Wegbeschreibung von seinem Zuhause in einer anderen Stadt zu folgen, würde er sich hoffnungslos verirren.

Genau dieses Prinzip gilt auch für Pfade im Web. Wenn du in deinem HTML-Code auf eine andere Datei verlinkst – sei es eine andere Webseite, ein Bild, eine CSS-Datei oder ein JavaScript-Skript –, musst du dem Browser den "Weg" dorthin beschreiben. Und dafür nutzt du entweder absolute oder relative Pfade.

#### Der Absolute Pfad – Die vollständige Adresse im Web

Ein absoluter Pfad ist wie die vollständige Postanschrift einer Datei im Internet. Er enthält alle Informationen, die ein Browser benötigt, um eine Ressource von überall auf der Welt eindeutig zu finden. Er beginnt immer mit dem Protokoll (`http://` oder `https://`), gefolgt vom Domainnamen und dann dem vollständigen Pfad zur Datei.

Ein typischer absoluter Pfad sieht so aus:
`https://www.meine-tolle-website.de/images/header-bild.jpg`

Er besteht aus drei Teilen:
1.  **Protokoll:** `https://`
2.  **Domain:** `www.meine-tolle-website.de`
3.  **Pfad zur Datei:** `/images/header-bild.jpg`

Wann verwendest du absolute Pfade? Hauptsächlich dann, wenn du auf eine Ressource verweist, die sich **nicht auf deiner eigenen Website** befindet.

**Beispiel 1: Verlinkung auf eine externe Website**
Wenn du in einem Blogartikel auf Wikipedia verweisen möchtest, musst du die vollständige URL angeben.

```html
<p>
  Weitere Informationen findest du auf 
  <a href="https://de.wikipedia.org/wiki/HTML">Wikipedia</a>.
</p>
```

**Beispiel 2: Einbinden eines Bildes von einem anderen Server**
Manchmal liegen Bilder auf speziellen Servern, sogenannten Content Delivery Networks (CDNs), um sie schneller auszuliefern. Um ein solches Bild einzubinden, brauchst du den absoluten Pfad.

```html
<img src="https://images.pexels.com/photos/12345/landscape.jpg" alt="Eine schöne Landschaft">
```

**Vorteile:**
*   **Eindeutig:** Es gibt keine Missverständnisse. Der Pfad funktioniert immer, egal wo sich die HTML-Datei befindet, die den Link enthält.
*   **Notwendig für externe Ressourcen:** Du hast keine andere Wahl, wenn du auf Inhalte außerhalb deiner eigenen Domain verlinken willst.

**Nachteile:**
*   **Unflexibel:** Wenn du deine Website eines Tages von `http://localhost/test` auf `https://www.meine-tolle-website.de` umziehst, musst du jeden einzelnen absoluten Pfad, der auf deine eigene Domain zeigt, mühsam anpassen. Das macht die Entwicklung und Wartung komplizierter.
*   **Länger und fehleranfälliger beim Tippen.**

Aus diesem Grund solltest du für alle Verlinkungen **innerhalb deines eigenen Projekts** in der Regel auf relative Pfade setzen.

#### Der Relative Pfad – Die Wegbeschreibung vom aktuellen Ort

Ein relativer Pfad beschreibt den Weg zu einer Zieldatei ausgehend vom **Standort der aktuellen Datei**. Er enthält weder Protokoll noch Domainnamen. Der Browser schaut sich an, wo die HTML-Datei liegt, die er gerade anzeigt, und folgt von dort aus deiner "Wegbeschreibung".

Um das zu verstehen, stellen wir uns eine typische Projektstruktur vor:

```
meine-website/
├── index.html
├── about.html
│
├── css/
│   └── style.css
│
├── images/
│   └── logo.png
│
└── portfolio/
    ├── projekt-a.html
    └── images/
        └── screenshot-a.png
```

Schauen wir uns nun an, wie du von verschiedenen Ausgangspunkten aus auf andere Dateien verlinkst.

**1. Verlinken auf Dateien im selben Verzeichnis**

Stell dir vor, du bist in der Datei `index.html` und möchtest auf die Seite `about.html` verlinken. Beide Dateien liegen auf derselben Ebene im Hauptverzeichnis `meine-website/`. Der Pfad ist in diesem Fall einfach der Dateiname.

In `index.html`:
```html
<a href="about.html">Über mich</a>
```

Du könntest auch `./about.html` schreiben. Der `./` steht für "im aktuellen Verzeichnis". Er ist optional, macht aber manchmal die Absicht klarer.

**2. Verlinken auf Dateien in einem Unterverzeichnis**

Du bist immer noch in `index.html` und möchtest nun deine CSS-Datei `style.css` einbinden, die im Unterordner `css/` liegt. Du sagst dem Browser: "Geh in den Ordner `css` und nimm dort die Datei `style.css`."

In `index.html`:
```html
<link rel="stylesheet" href="css/style.css">
```

Dasselbe gilt für das Logo im `images`-Ordner:

In `index.html`:
```html
<img src="images/logo.png" alt="Mein Logo">
```

**3. Verlinken auf Dateien in einem übergeordneten Verzeichnis**

Jetzt wird es interessant. Angenommen, du bearbeitest die Datei `projekt-a.html`, die sich im Unterordner `portfolio/` befindet. Von hier aus möchtest du das Haupt-Stylesheet `style.css` einbinden, das eine Ebene höher im `css`-Ordner liegt.

Du musst dem Browser sagen: "Geh eine Ebene nach oben, und von dort aus in den Ordner `css`." Der Befehl für "eine Ebene nach oben" lautet `../`.

In `portfolio/projekt-a.html`:
```html
<link rel="stylesheet" href="../css/style.css">
```

Lass uns diesen Pfad zerlegen:
*   `../`: Springe aus dem aktuellen Ordner (`portfolio/`) heraus in den übergeordneten Ordner (`meine-website/`).
*   `css/style.css`: Gehe von dort in den Ordner `css/` und wähle die Datei `style.css`.

Was ist, wenn du von `projekt-a.html` auf das Hauptlogo `logo.png` zugreifen möchtest? Der Weg ist ganz ähnlich:

In `portfolio/projekt-a.html`:
```html
<img src="../images/logo.png" alt="Mein Logo">
```

Und wenn du von `projekt-a.html` zurück zur Startseite `index.html` verlinken willst?

In `portfolio/projekt-a.html`:
```html
<a href="../index.html">Zurück zur Startseite</a>
```

**Vorteile:**
*   **Portabilität:** Das ist der entscheidende Vorteil. Du kannst den gesamten Projektordner `meine-website/` an einen beliebigen Ort verschieben – auf einen anderen Computer, auf einen Webserver, unter eine neue Domain – und alle internen Links funktionieren weiterhin tadellos. Deine Website bleibt in sich geschlossen und unabhängig.
*   **Kürzer und übersichtlicher:** Für interne Verlinkungen sind relative Pfade meist kürzer.

**Nachteile:**
*   **Kontextabhängig:** Ein relativer Pfad ist nur in Bezug auf den Speicherort der Quelldatei gültig. Wenn du eine HTML-Datei in einen anderen Ordner verschiebst, musst du wahrscheinlich alle relativen Pfade darin anpassen.

#### Eine Sonderform: Der Root-Relative Pfad

Es gibt noch eine dritte, sehr nützliche Variante, die eine Mischung aus beiden Welten darstellt: der "Root-relative" oder "wurzelrelative" Pfad. Er beginnt mit einem Schrägstrich (`/`).

Dieser Schrägstrich am Anfang sagt dem Browser: "Beginne die Suche nicht im aktuellen Verzeichnis, sondern im Hauptverzeichnis (der 'Root') der Website."

Schauen wir uns wieder unsere Projektstruktur an. Wenn `meine-website/` das Hauptverzeichnis deiner Domain ist, dann verweist `/` direkt dorthin.

*   Der Pfad zum Logo ist von **jeder** Datei aus: `/images/logo.png`
*   Der Pfad zum Stylesheet ist von **jeder** Datei aus: `/css/style.css`
*   Der Pfad zur "Über mich"-Seite ist von **jeder** Datei aus: `/about.html`

In `portfolio/projekt-a.html` könntest du also statt `../css/style.css` auch einfach schreiben:

```html
<link rel="stylesheet" href="/css/style.css">
```

**Vorteile:**
*   **Robust bei Umstrukturierung:** Wenn du die Datei `projekt-a.html` in einen weiteren Unterordner verschiebst, musst du ihre Links nicht anpassen, da der Ausgangspunkt (`/`) immer derselbe bleibt. Das macht sie bei großen, komplexen Websites sehr stabil.

**Wichtiger Hinweis und Nachteil:**
*   **Funktioniert nur auf einem Webserver:** Root-relative Pfade funktionieren nur, wenn die Website über ein Protokoll wie `http://` oder `https://` aufgerufen wird. Wenn du eine HTML-Datei einfach per Doppelklick lokal auf deinem Computer öffnest (die URL im Browser beginnt dann mit `file:///`), weiß der Browser nicht, was das "Hauptverzeichnis der Website" sein soll. Er interpretiert `/` als das Hauptverzeichnis deiner Festplatte (z.B. `C:/`), was natürlich nicht zum Ziel führt. Für die lokale Entwicklung ist es daher oft notwendig, einen lokalen Webserver zu verwenden.

Die Wahl des richtigen Pfadtyps ist keine Geschmacksfrage, sondern eine strategische Entscheidung, die die Wartbarkeit und Portabilität deines Webprojekts maßgeblich beeinflusst. Die Faustregel ist einfach: Für alles, was zu deinem Projekt gehört, nimm relative Pfade. Für alles, was außerhalb liegt, nimm absolute Pfade. Und wenn dein Projekt komplexer wird und auf einem Server läuft, sind root-relative Pfade eine elegante und stabile Alternative für deine interne Verlinkung.
