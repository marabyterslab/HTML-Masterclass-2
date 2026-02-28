# Strukturierung eigener Bibliotheken

### Strukturierung eigener Bibliotheken

Wenn du anfängst, wiederverwendbare HTML-Strukturen zu bauen, ist das ein bisschen so, als würdest du anfangen, eine Werkzeugkiste zu füllen. Am Anfang hast du einen Hammer, einen Schraubenzieher und eine Zange. Du weißt immer genau, wo alles liegt. Aber je mehr Projekte du machst, desto mehr Werkzeuge sammelst du an. Bald hast du Dutzende von Schraubenziehern in verschiedenen Größen, mehrere Hämmer für unterschiedliche Zwecke und eine unübersichtliche Sammlung von Zangen. Wenn du jetzt schnell den kleinen Kreuzschlitzschraubenzieher brauchst, verbringst du mehr Zeit mit Suchen als mit Arbeiten.

Eine Komponenten-Bibliothek ist deine digitale Werkzeugkiste. Ohne eine durchdachte Struktur wird sie schnell unübersichtlich, schwer zu warten und für dich und andere kaum nutzbar. Eine gute Struktur hingegen macht deine Bibliothek intuitiv, skalierbar und zu einer echten Arbeitserleichterung. Lass uns gemeinsam anschauen, wie du eine solche Struktur aufbauen kannst.

#### Die kleinste Einheit: Die Komponenten-Mappe

Jede Komponente in deiner Bibliothek sollte für sich allein stehen können. Das bedeutet, dass alle Dateien, die direkt zu dieser Komponente gehören – HTML, CSS, JavaScript und Dokumentation – an einem einzigen Ort gebündelt sein sollten. Der einfachste und sauberste Weg, dies zu erreichen, ist, für jede Komponente eine eigene Mappe (einen Ordner) anzulegen.

Stell dir vor, du erstellst eine einfache Button-Komponente. Anstatt eine zentrale `style.css`-Datei zu haben, in der die Stile für den Button neben hunderten anderen Regeln leben, schaffst du eine dedizierte Mappe:

```
/button
├── button.html
├── button.css
├── button.js
└── README.md
```

Schauen wir uns die einzelnen Dateien genauer an:

*   **`button.html`**: Diese Datei enthält die reine HTML-Struktur deiner Komponente. Sie sollte sauber und semantisch sein und alle Variationen zeigen, die deine Komponente haben kann.

    ```html
    <!-- Standard-Button -->
    <button class="btn">Klick mich</button>
    
    <!-- Primärer Button für wichtige Aktionen -->
    <button class="btn btn--primary">Bestätigen</button>
    
    <!-- Sekundärer Button für weniger wichtige Aktionen -->
    <button class="btn btn--secondary">Abbrechen</button>
    ```

*   **`button.css`**: Hier leben alle CSS-Regeln, die *ausschließlich* für die Button-Komponente gelten. Durch diese Kapselung verhinderst du, dass sich Stile gegenseitig unbeabsichtigt beeinflussen.

    ```css
    .btn {
      display: inline-block;
      padding: 10px 20px;
      font-size: 16px;
      border-radius: 5px;
      border: 1px solid #ccc;
      background-color: #f0f0f0;
      cursor: pointer;
      text-align: center;
      text-decoration: none;
    }
    
    .btn--primary {
      background-color: #007bff;
      color: #ffffff;
      border-color: #007bff;
    }
    
    .btn--secondary {
      background-color: #6c757d;
      color: #ffffff;
      border-color: #6c757d;
    }
    ```

*   **`button.js`**: Falls deine Komponente interaktives Verhalten benötigt (z.B. einen Klick-Effekt oder die Kommunikation mit einer API), gehört der entsprechende JavaScript-Code in diese Datei. Für unseren einfachen Button ist dies vielleicht nicht nötig, aber bei komplexeren Komponenten wie einem aufklappbaren Menü (Dropdown) oder einem Modal-Fenster ist es unerlässlich.

*   **`README.md`**: Dies ist vielleicht die wichtigste Datei in der Mappe. Sie ist die Gebrauchsanweisung für deine Komponente. Hier dokumentierst du, wofür die Komponente da ist, welche Variationen (Klassen) sie hat und wie man sie korrekt einsetzt. Eine gute Dokumentation ist der Schlüssel zur Wiederverwendbarkeit.

Dieser Ansatz – eine Mappe pro Komponente – ist der Grundpfeiler einer sauberen Bibliotheksstruktur. Es macht jede Komponente zu einer kleinen, eigenständigen Einheit, die du einfach kopieren, verschieben oder in anderen Projekten wiederverwenden kannst.

#### Das große Ganze: Die Bibliotheks-Architektur

Nachdem wir die kleinste Einheit definiert haben, zoomen wir nun heraus und betrachten die gesamte Ordnerstruktur deiner Bibliothek. Einfach alle Komponenten-Mappen in einen großen `components`-Ordner zu werfen, funktioniert für den Anfang, aber sobald du mehr als zehn oder zwanzig Komponenten hast, brauchst du eine feinere Gliederung.

Eine sehr bewährte Methode zur Strukturierung ist die Anlehnung an das Konzept des "Atomic Design". Du musst die Philosophie dahinter nicht strikt befolgen, aber die grundlegende Idee der Gruppierung nach Komplexität ist extrem hilfreich.

Eine typische Struktur könnte so aussehen:

```
/meine-bibliothek
├── src/
│   ├── components/
│   │   ├── 1-atoms/
│   │   │   ├── button/
│   │   │   ├── input/
│   │   │   ├── label/
│   │   │   └── heading/
│   │   ├── 2-molecules/
│   │   │   ├── search-form/
│   │   │   ├── newsletter-signup/
│   │   │   └── card-header/
│   │   └── 3-organisms/
│   │       ├── site-header/
│   │       ├── product-grid/
│   │       └── footer/
│   ├── global/
│   │   ├── variables.css
│   │   ├── reset.css
│   │   └── typography.css
│   └── js/
│       └── main.js
└── docs/
    └── index.html
```

Lass uns diese Struktur aufschlüsseln:

*   **`/src` (Source)**: Dies ist der Hauptordner, in dem dein gesamter Quellcode lebt. Es ist eine gängige Konvention, den Code, den du schreibst, vom Code, der am Ende ausgeliefert wird (z.B. nach einer Kompilierung), zu trennen.

*   **`/src/components`**: Hier befinden sich alle deine wiederverwendbaren UI-Komponenten, unterteilt in Kategorien. Die Nummerierung (`1-`, `2-`, `3-`) ist optional, hilft aber dabei, die Ordner im Dateisystem in der richtigen Reihenfolge zu sortieren.
    *   **`atoms` (Atome)**: Das sind die kleinsten, unteilbaren Bausteine deiner UI. Dazu gehören Buttons, Eingabefelder, Überschriften und Absätze. Sie haben für sich allein oft keinen großen Nutzen, sind aber die Grundlage für alles andere.
    *   **`molecules` (Moleküle)**: Hier kombinierst du mehrere Atome zu funktionierenden Einheiten. Ein Suchformular (`search-form`) ist ein klassisches Molekül: Es besteht aus einem `label`-Atom, einem `input`-Atom und einem `button`-Atom.
    *   **`organisms` (Organismen)**: Das sind komplexere Baugruppen, die aus Molekülen und/oder Atomen bestehen und einen ganzen Abschnitt einer Webseite bilden. Ein Seitenkopf (`site-header`) ist ein Organismus, der ein Logo (Atom), eine Navigation (Molekül) und vielleicht ein Suchformular (Molekül) enthalten kann.

Diese Gliederung hilft dir, den Zweck und die Abhängigkeiten einer Komponente sofort zu verstehen. Wenn du etwas im `atoms`-Ordner änderst, weißt du, dass dies potenziell Auswirkungen auf viele Moleküle und Organismen haben kann.

#### Globale Stile und die Rolle der Kaskade

Nicht jeder Stil gehört in eine Komponenten-Mappe. Bestimmte Regeln sollen für deine gesamte Webseite oder Anwendung gelten. Diese globalen Stile finden ihren Platz in einem separaten Ordner, zum Beispiel `/src/global`.

*   **`reset.css` oder `normalize.css`**: Eine dieser Dateien sollte immer die Grundlage deiner CSS-Architektur bilden. Sie sorgt dafür, dass die Standard-Stile der verschiedenen Browser angeglichen werden und du eine konsistente Basis hast, auf der du aufbauen kannst.

*   **`variables.css`**: Hier definierst du Design-Tokens – zentrale Werte, die du in deinem gesamten Projekt wiederverwenden möchtest. In modernem CSS nutzt du dafür CSS Custom Properties.

    ```css
    :root {
      /* Farben */
      --color-primary: #007bff;
      --color-text: #333;
      --color-background: #fff;
    
      /* Schriftarten */
      --font-family-base: 'Helvetica Neue', Arial, sans-serif;
      --font-size-base: 16px;
    
      /* Abstände */
      --spacing-small: 8px;
      --spacing-medium: 16px;
      --spacing-large: 32px;
    }
    ```
    Deine Komponenten (`button.css` etc.) sollten dann auf diese Variablen zurückgreifen, anstatt feste Werte wie `#007bff` zu verwenden. Das macht deine Bibliothek extrem flexibel. Willst du das Farbschema ändern? Du musst nur eine einzige Datei anpassen.

*   **`typography.css`**: Hier definierst du grundlegende typografische Stile für HTML-Elemente wie `body`, `h1`-`h6`, `p`, `a` usw. Dies stellt sicher, dass einfacher Text im gesamten Projekt einheitlich aussieht.

#### Der Build-Prozess und die Auslieferung

Die bisher beschriebene Struktur mit vielen kleinen CSS- und JavaScript-Dateien ist fantastisch für die Entwicklung. Sie ist übersichtlich und gut zu verwalten. Für den Einsatz auf einer Webseite ist sie jedoch nicht optimal, da der Browser viele einzelne Anfragen senden müsste, was die Ladezeit verlangsamt.

Hier kommt ein "Build-Prozess" ins Spiel. Das ist ein automatisierter Schritt, bei dem Werkzeuge (wie z.B. Vite, Parcel oder Webpack) all deine einzelnen CSS-Dateien zu einer einzigen, optimierten `style.css`-Datei zusammenfassen. Dasselbe geschieht mit deinen JavaScript-Dateien.

Du musst diesen Prozess nicht von Grund auf selbst erfinden. Viele moderne Frameworks und Werkzeuge nehmen dir diese Arbeit ab. Wichtig ist das Verständnis, dass deine Entwicklungsstruktur (viele kleine, logische Dateien) nicht dieselbe ist wie deine Produktionsstruktur (wenige, gebündelte Dateien). Deine saubere Ordnerstruktur ist die Voraussetzung dafür, dass solche Werkzeuge überhaupt effektiv arbeiten können.

Indem du dir von Anfang an die Zeit nimmst, eine durchdachte und skalierbare Struktur für deine Komponenten-Bibliothek aufzubauen, investierst du in die Zukunft. Du schaffst eine verlässliche Grundlage, die dir nicht nur im aktuellen Projekt, sondern auch in allen zukünftigen Projekten wertvolle Zeit und Nerven sparen wird. Deine Werkzeugkiste ist nun nicht mehr nur eine chaotische Ansammlung, sondern ein professionelles, gut sortiertes System, in dem du jedes Werkzeug mit einem Griff findest.
