# Verschachtelung von Listen

### Verschachtelte Listen: Struktur in der Struktur

Manchmal reicht eine einfache, flache Liste nicht aus, um Informationen logisch und übersichtlich darzustellen. Stell dir eine Einkaufsliste für ein komplexes Rezept vor. Es genügt nicht, nur „Spaghetti Bolognese“ auf die Liste zu schreiben. Du brauchst eine detaillierte Aufzählung der Zutaten, die direkt diesem Gericht zugeordnet sind. Oder denk an die Gliederung eines Buches: Kapitel haben Unterkapitel, und diese vielleicht sogar noch weitere Unterpunkte. Genau für solche hierarchischen Strukturen bietet dir HTML ein mächtiges Werkzeug: die Verschachtelung von Listen.

Das Prinzip ist erstaunlich einfach, aber fundamental für den Aufbau komplexer Dokumente. Du kannst eine komplette Liste (egal ob geordnet oder ungeordnet) innerhalb eines Listenpunktes (`<li>`) einer anderen Liste platzieren.

#### Die goldene Regel der Verschachtelung

Es gibt eine einzige, aber entscheidende Regel, die du dir merken musst: **Eine neue Liste wird immer innerhalb eines `<li>`-Elements der übergeordneten Liste platziert, niemals direkt innerhalb eines `<ul>`- oder `<ol>`-Elements.**

Warum ist das so? Semantisch betrachtet ist eine Unterliste ein Teil des Inhalts des übergeordneten Listenpunktes. Nehmen wir das Beispiel einer To-do-Liste für einen Wochenendausflug:

*   **Freitag:**
    *   Koffer packen
    *   Auto volltanken
    *   Route planen
*   **Samstag:**
    *   Fahrt zum Zielort
    *   Im Hotel einchecken
*   **Sonntag:**
    *   Aktivität am Vormittag
    *   Rückfahrt

Die Punkte „Koffer packen“, „Auto volltanken“ und „Route planen“ sind keine eigenständigen Hauptpunkte des Ausflugs. Sie sind spezifische Aufgaben, die zum übergeordneten Punkt „Freitag“ gehören. Deshalb muss die Liste, die diese Aufgaben enthält, ein direkter Bestandteil des `<li>`-Elements für „Freitag“ sein.

Schauen wir uns an, wie das im Code aussieht. Hier ist eine einfache ungeordnete Liste, die eine weitere ungeordnete Liste enthält:

```html
<ul>
  <li>Erster Hauptpunkt</li>
  <li>
    Zweiter Hauptpunkt
    <ul>
      <li>Erster Unterpunkt</li>
      <li>Zweiter Unterpunkt</li>
    </ul>
  </li>
  <li>Dritter Hauptpunkt</li>
</ul>
```

Beachte die Struktur genau: Das zweite `<ul>`-Element beginnt *nach* dem Text „Zweiter Hauptpunkt“, aber *vor* dem schließenden `</li>`-Tag des übergeordneten Listenpunktes. Der Browser versteht diese Struktur und stellt sie standardmäßig visuell dar, indem er die untergeordnete Liste einrückt und oft auch einen anderen Aufzählungsstil verwendet (z. B. Kreise statt ausgefüllter Punkte).

#### Kombinationen und tiefere Ebenen

Das Schöne an diesem System ist seine Flexibilität. Du bist nicht darauf beschränkt, nur ungeordnete Listen in ungeordneten Listen zu verschachteln. Jede Kombination ist möglich und semantisch sinnvoll, solange sie den Inhalt korrekt abbildet.

##### Geordnete Liste in einer ungeordneten Liste

Stell dir vor, du planst ein Projekt. Die Hauptphasen haben keine bestimmte Reihenfolge, aber die Schritte innerhalb einer Phase müssen sequenziell abgearbeitet werden.

```html
<ul>
  <li>Phase 1: Konzeption</li>
  <li>
    Phase 2: Entwicklung
    <ol>
      <li>Datenbank-Design erstellen</li>
      <li>Backend-Logik implementieren</li>
      <li>Frontend-Oberfläche entwickeln</li>
      <li>Testing und Fehlerbehebung</li>
    </ol>
  </li>
  <li>Phase 3: Veröffentlichung</li>
</ul>
```

Hier siehst du deutlich den Vorteil der Kombination: Die `<ul>` gruppiert die Phasen, während die `<ol>` die notwendige Schritt-für-Schritt-Anleitung innerhalb der Entwicklungsphase liefert. Der Browser wird die Unterpunkte korrekt mit 1., 2., 3. usw. nummerieren.

##### Mehrere Verschachtelungsebenen

Die Verschachtelung ist nicht auf eine einzige Ebene beschränkt. Du kannst Listen so tief ineinander schachteln, wie es für deine Inhaltsstruktur notwendig ist. Ein klassisches Beispiel hierfür ist die Navigation einer Website.

```html
<ul>
  <li><a href="/startseite">Startseite</a></li>
  <li>
    <a href="/produkte">Produkte</a>
    <ul>
      <li>
        Bücher
        <ul>
          <li>Sachbücher</li>
          <li>Romane</li>
          <li>Kinderbücher</li>
        </ul>
      </li>
      <li>
        Elektronik
        <ul>
          <li>Smartphones</li>
          <li>Laptops</li>
        </ul>
      </li>
    </ul>
  </li>
  <li><a href="/ueber-uns">Über uns</a></li>
  <li><a href="/kontakt">Kontakt</a></li>
</ul>
```

Dieser HTML-Code bildet die Grundlage für ein typisches Drop-down-Menü. Der Hauptpunkt „Produkte“ enthält eine Unterliste mit den Kategorien „Bücher“ und „Elektronik“. Jede dieser Kategorien ist wiederum ein Listenpunkt (`<li>`), der eine weitere, noch tiefere Liste mit den spezifischen Produktarten enthält.

Ohne CSS sieht diese Struktur vielleicht nicht wie eine schicke Navigation aus, aber die semantische HTML-Struktur ist perfekt. Sie ist logisch, für Suchmaschinen und Screenreader verständlich und bildet die ideale Basis für das spätere Styling mit CSS und die Interaktivität mit JavaScript.

#### Ein häufiger Fehler, den du vermeiden solltest

Der häufigste Fehler bei der Verschachtelung von Listen ist die Missachtung der goldenen Regel. Anfänger platzieren eine neue Liste oft fälschlicherweise direkt in die übergeordnete Liste, anstatt sie in ein `<li>`-Element zu packen.

**Falscher Code:**

```html
<!-- DIESER CODE IST UNGÜLTIG! -->
<ul>
  <li>Ein Punkt</li>
  <ul>
    <li>Ein Unterpunkt, aber falsch platziert</li>
  </ul>
  <li>Noch ein Punkt</li>
</ul>
```

Dieser Code ist invalides HTML. Gemäß der HTML-Spezifikation dürfen `<ul>`- und `<ol>`-Elemente als direkte Kinder nur `<li>`-Elemente (und einige script-unterstützende Elemente) enthalten. Ein `<ul>` direkt in einem anderen `<ul>` ist nicht erlaubt. Auch wenn manche Browser versuchen, diesen Fehler zu „reparieren“ und etwas halbwegs Sinnvolles anzuzeigen, verlässt du dich damit auf undefiniertes Verhalten. Dein Code ist semantisch falsch und kann zu unvorhersehbaren Problemen bei der Darstellung und bei der Verarbeitung durch andere Systeme (wie Screenreader) führen.

**Korrekter Code:**

```html
<ul>
  <li>
    Ein Punkt
    <ul>
      <li>Ein Unterpunkt, korrekt platziert</li>
    </ul>
  </li>
  <li>Noch ein Punkt</li>
</ul>
```

Hier ist die Unterliste korrekt in das `<li>`-Element des dazugehörigen Hauptpunktes eingebettet.

Die Fähigkeit, Listen korrekt zu verschachteln, ist mehr als nur eine technische Übung. Sie ist ein zentraler Baustein, um komplexe Informationen klar und logisch zu strukturieren. Du gibst deinen Inhalten eine saubere, hierarchische Form, die sowohl für Menschen als auch für Maschinen leicht zu interpretieren ist. Ob für Inhaltsverzeichnisse, Navigationsmenüs, Gliederungen oder detaillierte Anleitungen – verschachtelte Listen sind ein unverzichtbares Werkzeug in deinem HTML-Repertoire.
