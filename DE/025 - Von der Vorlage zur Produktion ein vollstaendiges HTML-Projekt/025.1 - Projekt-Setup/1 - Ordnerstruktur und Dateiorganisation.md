# Ordnerstruktur und Dateiorganisation

### Ordnerstruktur und Dateiorganisation: Das Fundament deines Webprojekts

Stell dir vor, dein Webprojekt ist eine Werkstatt. Wenn Werkzeuge und Materialien überall verstreut liegen, wirst du die meiste Zeit mit Suchen verbringen, anstatt etwas zu erschaffen. Liegt hingegen alles an seinem festen Platz, kannst du dich voll und ganz auf deine Arbeit konzentrieren. Genauso verhält es sich mit der Ordnerstruktur und Dateiorganisation deines Webprojekts. Eine durchdachte Struktur ist kein Luxus, sondern eine absolute Notwendigkeit. Sie ist das Fundament, auf dem du effizient, wartbar und skalierbar aufbauen kannst.

Am Anfang eines Projekts mag es verlockend sein, einfach alle Dateien – HTML, CSS, JavaScript und Bilder – in einen einzigen Ordner zu werfen. Bei einer Handvoll Dateien funktioniert das vielleicht noch. Doch sobald dein Projekt wächst, auch nur ein klein wenig, verwandelt sich diese Einfachheit in pures Chaos. Du verlierst den Überblick, das Verknüpfen von Dateien wird fehleranfällig und die Zusammenarbeit mit anderen Entwicklern praktisch unmöglich. Eine saubere Struktur hingegen macht dein Projekt selbsterklärend.

#### Das Projektverzeichnis (Root)

Jedes Webprojekt beginnt mit einem Hauptordner, dem sogenannten Projektverzeichnis oder Root-Verzeichnis (englisch: *root* für Wurzel). Dieser Ordner umschließt dein gesamtes Projekt. Alles, was zu deiner Webseite gehört, befindet sich innerhalb dieses einen Ordners. Gib ihm einen aussagekräftigen Namen, der den Inhalt widerspiegelt, zum Beispiel `portfolio-website` oder `rezept-blog`.

Innerhalb dieses Hauptordners entfaltet sich die eigentliche Magie der Organisation. Der wichtigste Bewohner dieses Ordners ist fast immer eine Datei namens `index.html`.

**Die `index.html`-Datei**

Die `index.html` ist die Visitenkarte deines Projekts. Webserver sind standardmäßig so konfiguriert, dass sie nach genau dieser Datei suchen, wenn ein Besucher deine Domain aufruft (z. B. `www.deine-domain.de`). Sie ist der Haupteingang, die Startseite deiner Webseite. Jedes Webprojekt, das online gehen soll, benötigt eine `index.html` im Hauptverzeichnis.

Weitere HTML-Dateien, wie `ueber-uns.html` oder `kontakt.html`, können ebenfalls direkt im Hauptverzeichnis liegen, besonders bei kleineren Projekten. Das ist übersichtlich und vollkommen in Ordnung.

#### Dedizierte Ordner für verschiedene Dateitypen

Der Schlüssel zu einer guten Organisation liegt in der Trennung von Zuständigkeiten. HTML ist für die Struktur, CSS für das Design und JavaScript für die Interaktivität zuständig. Diese logische Trennung solltest du auch in deiner Ordnerstruktur widerspiegeln.

**Der CSS-Ordner**

Deine Stylesheet-Dateien, die das Aussehen deiner Webseite definieren, gehören in einen eigenen Ordner. Übliche Namen dafür sind `css` oder `styles`. Indem du alle CSS-Dateien an einem Ort sammelst, weißt du und jeder andere sofort, wo nach Design-Regeln gesucht werden muss. Eine typische Datei in diesem Ordner wäre `main.css` oder `style.css`.

**Der JavaScript-Ordner**

Gleiches gilt für deine JavaScript-Dateien. Skripte, die für Animationen, Formularvalidierungen oder andere interaktive Elemente verantwortlich sind, platzierst du in einem Ordner namens `js` oder `scripts`. Eine Haupt-Skriptdatei könnte `main.js` oder `app.js` heißen.

**Der Ordner für Medien und andere Ressourcen (Assets)**

Eine Webseite besteht selten nur aus Code. Du wirst Bilder, vielleicht eigene Schriftarten, Videos oder Icons verwenden. All diese Dateien werden als "Assets" bezeichnet. Es hat sich bewährt, für diese Ressourcen einen übergeordneten Ordner anzulegen, der oft `assets` oder `public` genannt wird.

Innerhalb des `assets`-Ordners schaffst du dann weitere, spezifischere Unterordner:

*   **`images` (oder `img`):** Hier kommen all deine Bilddateien hinein, wie Logos (`logo.svg`), Hintergrundbilder (`hero-hintergrund.jpg`) oder Produktfotos (`produkt-schuh.png`).
*   **`fonts`:** Falls du benutzerdefinierte Schriftarten verwendest (z. B. im WOFF2-Format), ist dies der richtige Ort für sie.
*   **`icons`:** Für kleine Grafiken wie Social-Media-Symbole oder UI-Icons. Manchmal ist dieser Ordner auch ein Unterordner von `images`.

Diese Struktur sorgt für maximale Klarheit. Wenn du ein Bild suchst, schaust du in `assets/images`. Wenn du das Styling anpassen musst, öffnest du eine Datei in `css`.

#### Eine beispielhafte Projektstruktur

Lass uns diese Prinzipien in einer konkreten Ordnerstruktur visualisieren. So könnte ein typisches, gut organisiertes kleines bis mittelgroßes Webprojekt aussehen:

```
mein-webprojekt/
├── index.html
├── ueber-uns.html
├── kontakt.html
│
├── css/
│   └── style.css
│
├── js/
│   └── main.js
│
└── assets/
    ├── images/
    │   ├── logo.svg
    │   ├── heldenbild.jpg
    │   └── team/
    │       ├── anna.jpg
    │       └── max.jpg
    │
    └── fonts/
        └── OpenSans-Regular.woff2
```

Schauen wir uns diese Struktur genauer an:

*   **`mein-webprojekt/`**: Das ist unser Hauptverzeichnis.
*   **`index.html`, `ueber-uns.html`, `kontakt.html`**: Die HTML-Seiten liegen direkt im Root. Sie bilden die Hauptnavigation der Webseite.
*   **`css/`**: Ein Ordner, der ausschließlich unsere Stylesheets enthält. Momentan nur `style.css`.
*   **`js/`**: Ein Ordner für alle JavaScript-Dateien.
*   **`assets/`**: Ein Sammelordner für alle Medien.
    *   **`images/`**: Beherbergt alle Bilder. Du siehst hier sogar einen weiteren Unterordner `team/`, um die Teamfotos thematisch zu gruppieren. Das zeigt, wie du die Struktur bei Bedarf weiter verfeinern kannst.
    *   **`fonts/`**: Enthält die Dateien für unsere benutzerdefinierte Schriftart.

Diese Struktur ist logisch, leicht verständlich und lässt sich problemlos erweitern. Wenn ein Blog hinzukommt, könntest du neue HTML-Dateien hinzufügen oder vielleicht sogar einen Ordner `blog/` für die Blogartikel anlegen.

#### Konventionen für die Dateibenennung

Nicht nur die Ordnerstruktur, auch die Benennung der einzelnen Dateien ist entscheidend für ein sauberes Projekt. Hier haben sich einige ungeschriebene Gesetze etabliert, an die du dich unbedingt halten solltest.

1.  **Nur Kleinbuchstaben verwenden:** Webserver, insbesondere solche, die auf Linux/Unix-Systemen laufen, unterscheiden zwischen Groß- und Kleinschreibung (`image.JPG` und `image.jpg` sind zwei verschiedene Dateien). Um Verwirrung und Fehler zu vermeiden, benenne alle deine Dateien und Ordner konsequent in Kleinbuchstaben.

2.  **Keine Leerzeichen oder Sonderzeichen:** Leerzeichen in Dateinamen werden in URLs in unschöne Zeichenketten wie `%20` umgewandelt. Das ist nicht nur schwer zu lesen, sondern kann auch zu Fehlern führen. Verwende stattdessen einen Bindestrich (`-`), um Wörter zu trennen. Benutze auch keine Umlaute (ä, ö, ü) oder andere Sonderzeichen.

    *   **Schlecht:** `Über uns.html`, `mein heldenbild.jpg`
    *   **Gut:** `ueber-uns.html`, `mein-heldenbild.jpg`

3.  **Sei beschreibend, aber kurz:** Der Dateiname sollte den Inhalt der Datei widerspiegeln. `header-background.jpg` ist unendlich viel besser als `bild_01.jpg`. Wenn du in sechs Monaten auf dein Projekt zurückblickst, wirst du dir für diese Klarheit danken. Vermeide jedoch übermäßig lange Namen.

Eine gute Ordner- und Dateistruktur ist mehr als nur eine persönliche Vorliebe. Sie ist ein Zeichen von Professionalität und ein entscheidender Faktor für den langfristigen Erfolg deines Projekts. Sie erleichtert dir die Arbeit, macht die Fehlersuche einfacher und ermöglicht es anderen, sich schnell in deinem Code zurechtzufinden. Investiere die paar Minuten zu Beginn eines jeden Projekts, um diese saubere Grundlage zu schaffen – es wird sich tausendfach auszahlen.
