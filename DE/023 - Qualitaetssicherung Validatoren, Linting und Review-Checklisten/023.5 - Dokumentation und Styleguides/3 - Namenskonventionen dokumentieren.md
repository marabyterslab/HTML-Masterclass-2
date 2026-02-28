# Namenskonventionen dokumentieren

### Klarheit durch Konvention: Wie du Namenskonventionen dokumentierst

Stell dir vor, du betrittst eine riesige Bibliothek, in der alle Bücher willkürlich in die Regale gestellt wurden. Keine Kategorien, keine alphabetische Sortierung, nichts. Du suchst ein bestimmtes Buch und beginnst eine schier endlose Odyssee. Genau dieses Gefühl stellt sich bei Entwicklern ein, wenn sie ein Projekt ohne klare Namenskonventionen vorfinden. Der Code mag funktionieren, aber ihn zu verstehen, zu warten oder zu erweitern, wird zu einer frustrierenden Schnitzeljagd.

Namenskonventionen sind das Ordnungssystem deiner Code-Bibliothek. Sie schaffen eine einheitliche Sprache, die jeder im Team versteht – auch dein zukünftiges Ich, das sich in sechs Monaten fragt, was `const a = document.querySelector('.x_1');` eigentlich bedeuten sollte. Doch Regeln zu haben, ist nur die halbe Miete. Wenn niemand sie kennt oder sie nur mündlich überliefert werden, verblassen sie mit der Zeit oder werden unterschiedlich interpretiert. Deshalb ist die Dokumentation dieser Regeln kein optionaler Luxus, sondern ein fundamentaler Baustein für professionelle und nachhaltige Projekte.

#### Warum das Festhalten von Regeln so entscheidend ist

Bevor wir ins Detail gehen, was und wie du dokumentieren solltest, lass uns kurz innehalten und das „Warum“ verstehen. Eine gut dokumentierte Sammlung von Namenskonventionen dient mehreren Zwecken:

1.  **Konsistenz:** Der offensichtlichste Vorteil. Ob eine CSS-Klasse `btn-primary` oder `button--primary` heißt, ist technisch egal. Aber wenn beides im selben Projekt existiert, stiftet es Verwirrung. Konsistenz senkt die kognitive Last, weil du nicht bei jeder neuen Datei oder Komponente überlegen musst, welchem Schema du nun folgst.
2.  **Lesbarkeit:** Code wird weitaus häufiger gelesen als geschrieben. Ein Name wie `isUserAuthenticated` ist selbsterklärend. `usrAuth` ist es nicht. Klare Namen machen den Code verständlicher, ohne dass du jeden zweiten Satz mit einem Kommentar erklären musst.
3.  **Onboarding:** Neue Teammitglieder finden sich in einem Projekt mit dokumentierten Regeln ungleich schneller zurecht. Statt wochenlang durch den Code zu irren, um die ungeschriebenen Gesetze zu entschlüsseln, können sie ein zentrales Dokument lesen und sind sofort produktiv.
4.  **Teamarbeit:** In einem Team verhindern Konventionen endlose Diskussionen über Stilfragen in Code-Reviews. Der Fokus kann auf der Logik und Funktionalität liegen, anstatt auf der Frage, ob eine Variable nun `camelCase` oder `snake_case` verwenden sollte.
5.  **Wartbarkeit:** Wenn du weißt, dass alle JavaScript-Dateien für Komponenten in einem Ordner namens `components` liegen und `kebab-case` verwenden, findest du die Datei `user-profile.js` auf Anhieb. Du musst nicht raten, ob sie `UserProfile.js` oder `user_profile.js` heißt und in `/js/modules/` oder `/src/components/` liegt.

#### Was genau gehört in die Dokumentation?

Eine gute Dokumentation von Namenskonventionen ist präzise, aber nicht überladen. Sie sollte die wichtigsten Bereiche abdecken, in denen Namen vergeben werden. Ein guter Startpunkt sind die folgenden Kategorien.

##### CSS-Klassen und IDs

Hier herrscht oft das größte Chaos. Eine Methodik wie BEM (Block, Element, Modifier) ist ein beliebter Standard, um Ordnung zu schaffen. Wenn du dich dafür entscheidest, sollte deine Dokumentation das klar festhalten.

**Beispiel für eine Dokumentation (BEM):**

Wir verwenden die BEM-Methodik (Block, Element, Modifier) für alle unsere CSS-Klassen, um Spezifitätskonflikte zu vermeiden und die Struktur unserer Komponenten klar abzubilden.

*   **Block:** Der Name der eigenständigen Komponente. Wird in `kebab-case` geschrieben.
    *   Gut: `.card`, `.main-navigation`
    *   Schlecht: `.Card`, `.main_navigation`
*   **Element:** Ein Teil des Blocks, der nicht eigenständig existieren kann. Wird mit zwei Unterstrichen (`__`) an den Block angehängt.
    *   Gut: `.card__title`, `.main-navigation__link`
    *   Schlecht: `.card-title`, `.main-navigation .link` (vermeidet unnötige Spezifität)
*   **Modifier:** Eine Variante oder ein Zustand des Blocks oder Elements. Wird mit zwei Bindestrichen (`--`) angehängt.
    *   Gut: `.card--featured`, `.main-navigation__link--active`
    *   Schlecht: `.featured-card`, `.active-link`

**IDs:**

IDs werden nur sparsam eingesetzt. Ihr primärer Zweck sind Anker für Seiten-Sprungmarken oder als eindeutiger Hook für JavaScript.

*   Für JavaScript-Hooks verwenden wir `camelCase`: `id="userProfileModal"`
*   Für Sprungmarken verwenden wir `kebab-case`: `id="section-contact"`

##### HTML-Attribute

Auch hier sorgt Klarheit für Effizienz. Besonders bei `data-*`-Attributen lohnt sich eine Regel.

**Beispiel für eine Dokumentation:**

*   **`data-*`-Attribute für JavaScript:** Wenn ein Element ausschließlich als JavaScript-Hook dient und keine stilistische Klasse benötigt, verwenden wir ein `data-`Attribut. Dies entkoppelt das Styling vom Verhalten. Das Attribut sollte den Zweck beschreiben.
    *   Gut: `data-element="toggle-button"`, `data-component="modal"`
    *   Schlecht: `data-js="toggle"`, `data-thing="modal"`
*   **`data-*`-Attribute für Test-IDs:** Für End-to-End-Tests verwenden wir `data-testid`, um Elemente eindeutig zu identifizieren.
    *   Gut: `data-testid="login-submit-button"`

##### JavaScript-Variablen, -Funktionen und -Klassen

Im JavaScript-Umfeld haben sich bestimmte Konventionen weitgehend durchgesetzt. Es ist dennoch wichtig, sie explizit zu dokumentieren, um sicherzustellen, dass jeder sie befolgt.

**Beispiel für eine Dokumentation:**

*   **Variablen und Funktionen:** Werden in `camelCase` geschrieben. Der Name sollte den Inhalt oder die Funktion klar beschreiben.
    *   Gut: `const userProfile = {};`, `function getUserData() {}`
    *   Schlecht: `const user = {};`, `function data() {}`
*   **Konstanten:** Werte, die sich zur Laufzeit garantiert nicht ändern (z.B. Konfigurationswerte), werden in `UPPER_SNAKE_CASE` geschrieben.
    *   Gut: `const API_ENDPOINT = 'https://api.example.com';`, `const MAX_RETRIES = 3;`
    *   Schlecht: `const apiEndpoint = '...';`
*   **Klassen und Komponenten:** Werden in `PascalCase` (auch `UpperCamelCase`) geschrieben. Dies signalisiert, dass sie mit `new` instanziiert werden können oder eine Komponente (wie in React oder Vue) darstellen.
    *   Gut: `class UserService { ... }`, `function UserProfile() { ... }` (im Kontext von React)
*   **Booleansche Variablen:** Sollten mit einem Präfix wie `is`, `has` oder `should` beginnen, um ihren wahren/falschen Charakter sofort erkennbar zu machen.
    *   Gut: `const isLoggedIn = true;`, `const hasPermissions = false;`
    *   Schlecht: `const loggedIn = true;`, `const permissions = false;`

##### Datei- und Ordnernamen

Die Struktur deines Projekts ist das Fundament. Eine logische und konsistente Benennung von Dateien und Ordnern macht die Navigation zum Kinderspiel.

**Beispiel für eine Dokumentation:**

Alle Datei- und Ordnernamen werden in `kebab-case` geschrieben. Dies stellt die Kompatibilität zwischen verschiedenen Betriebssystemen sicher und verbessert die Lesbarkeit in URLs.

*   Gut: `user-profile.css`, `api-helpers.js`, `/components/modal-dialog/`
*   Schlecht: `UserProfile.css`, `apiHelpers.js`, `/components/ModalDialog/`

**Ordnerstruktur:**

Wir folgen einer komponentenbasierten Ordnerstruktur. Alle zusammengehörigen Dateien (HTML-Template, CSS, JavaScript) für eine Komponente liegen in einem eigenen Ordner.

```
/src
├── /components
│   ├── /button
│   │   ├── button.html
│   │   ├── button.css
│   │   └── button.js
│   ├── /card
│   │   ├── card.html
│   │   ├── card.css
│   │   └── card.js
└── /assets
    ├── /images
    └── /fonts
```

Diese Struktur fördert die Modularität und macht es einfach, Komponenten zu finden, zu bearbeiten oder wiederzuverwenden.

#### Die Kunst der guten Dokumentation: Ort und Format

Wo sollte diese Dokumentation leben? Die beste Antwort ist: dort, wo dein Team sie am einfachsten findet.

*   **Im Projekt-Repository:** Eine Markdown-Datei wie `STYLEGUIDE.md` oder ein Abschnitt in der `CONTRIBUTING.md` ist eine exzellente Wahl. Der Vorteil: Die Dokumentation ist versioniert, liegt direkt beim Code und kann über Pull Requests aktualisiert werden – genau wie der Code selbst.
*   **Im Team-Wiki:** Für größere Organisationen oder teamübergreifende Standards kann ein zentrales Wiki (z.B. in Confluence oder Notion) sinnvoll sein. Wichtig ist, dass vom Projekt-Repository aus dorthin verlinkt wird.

Halte die Dokumentation selbst einfach und direkt. Nutze Überschriften, Listen und Code-Beispiele. Das "Gut vs. Schlecht"-Format ist extrem wirkungsvoll, weil es die Regeln sofort greifbar macht. Erkläre bei wichtigen Entscheidungen kurz das „Warum“. Ein Satz wie „Wir verwenden BEM, um Spezifitätskriege zu vermeiden“ schafft mehr Akzeptanz als eine reine Anweisung.

#### Ein lebendiges Dokument

Namenskonventionen sind kein in Stein gemeißeltes Gesetz. Projekte entwickeln sich weiter, neue Technologien kommen hinzu und das Team lernt dazu. Deine Dokumentation sollte daher ein lebendiges Dokument sein. Ermutige dein Team, Verbesserungen vorzuschlagen. Wenn eine Regel in der Praxis umständlich ist oder ein neuer Fall auftritt, der nicht abgedeckt ist, sollte der Prozess zur Anpassung der Dokumentation klar sein.

Indem du deine Namenskonventionen sorgfältig dokumentierst und pflegst, investierst du direkt in die Qualität und Langlebigkeit deines Codes. Du baust eine Brücke zwischen den Teammitgliedern und schaffst eine gemeinsame Basis, auf der effiziente und freudvolle Zusammenarbeit erst möglich wird.
