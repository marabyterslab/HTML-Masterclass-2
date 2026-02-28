# Abgrenzung zu bloßen Ortsangaben

### Abgrenzung zu bloßen Ortsangaben

Wenn du im Web auf eine Adresse stößt, ist dein erster Impuls vielleicht, nach einem speziellen HTML-Element dafür zu suchen. Und tatsächlich, es gibt das `<address>`-Element. Doch hier lauert eine der häufigsten semantischen Fallen in HTML. Der Name ist etwas irreführend, denn `<address>` ist nicht für *jede beliebige* Adresse gedacht. Seine Aufgabe ist weitaus spezifischer und hat viel mit dem Kontext zu tun.

Die Kernaufgabe des `<address>`-Elements ist es, **Kontaktinformationen** für den Autor oder Eigentümer eines Dokuments oder eines Teils eines Dokuments bereitzustellen. Es geht also nicht um den Ort, sondern um die Erreichbarkeit der Person oder Organisation, die für den Inhalt verantwortlich ist.

#### Der semantische Zweck: Wer ist der Ansprechpartner?

Stell dir eine Webseite als ein digitales Dokument vor. Dieses Dokument hat einen Urheber. Vielleicht ist es ein Blogartikel, eine wissenschaftliche Arbeit oder die Startseite eines Unternehmens. Das `<address>`-Element liefert die notwendigen Informationen, um mit diesem Urheber in Kontakt zu treten.

Diese Kontaktinformationen können vielfältig sein:
*   Eine physische Postanschrift
*   Eine E-Mail-Adresse (typischerweise als `mailto:`-Link)
*   Eine Telefonnummer (oft mit dem `tel:`-Protokoll)
*   Ein Link zu einer Webseite oder einem Social-Media-Profil
*   Der Name des Autors oder der Organisation

Der entscheidende Punkt ist die **Verbindung zum Inhalt**. Die im `<address>`-Tag enthaltenen Informationen müssen sich auf den nächstgelegenen übergeordneten Kontext beziehen. Das kann entweder der gesamte `<body>` des Dokuments sein oder ein bestimmter Abschnitt, wie zum Beispiel ein `<article>`-Element.

**Ein korrektes Beispiel im Kontext eines Artikels:**

Stell dir vor, du schreibst einen Blogbeitrag. Am Ende des Beitrags möchtest du deine Kontaktdaten angeben, damit Leser dir Feedback geben können. Das ist der perfekte Anwendungsfall für `<address>`.

```html
<article>
  <h2>Die Bedeutung von semantischem HTML</h2>
  <p>Semantisches HTML ist mehr als nur eine Ansammlung von Tags. Es verleiht dem Inhalt Struktur und Bedeutung...</p>
  <!-- ... weiterer Inhalt des Artikels ... -->
  
  <footer>
    <p>Veröffentlicht am 10. Oktober 2023</p>
    <address>
      Geschrieben von Alex Meier<br>
      Erreichbar per E-Mail: <a href="mailto:alex.meier@beispiel.de">alex.meier@beispiel.de</a><br>
      Besuche mein Profil auf <a href="https://social.example.com/ameier">Social Media</a>.
    </address>
  </footer>
</article>
```
In diesem Beispiel ist klar: Die Kontaktinformationen in `<address>` beziehen sich auf Alex Meier, den Autor des `<article>`. Ein Browser, eine Suchmaschine oder ein Screenreader versteht, dass dies die Kontaktperson für genau diesen Inhalt ist.

**Ein korrektes Beispiel im globalen Kontext der Seite:**

Wenn die Kontaktinformationen für die gesamte Webseite gelten, platziert man das `<address>`-Element oft im `<footer>` der Seite, der direkt im `<body>` liegt.

```html
<body>
  <header>
    <h1>Mein Unternehmen GmbH</h1>
  </header>

  <main>
    <!-- Hauptinhalt der Webseite -->
  </main>
  
  <footer>
    <address>
      <strong>Mein Unternehmen GmbH</strong><br>
      Musterstraße 123<br>
      10115 Berlin<br>
      Deutschland<br>
      Telefon: <a href="tel:+49301234567">+49 (0)30 123 456 7</a>
    </address>
    <p>&copy; 2023 Mein Unternehmen GmbH</p>
  </footer>
</body>
```
Hier ist `<address>` nicht innerhalb eines `<article>` verschachtelt. Daher beziehen sich die Informationen auf das gesamte Dokument – also auf den Betreiber der Webseite.

#### Was `<address>` nicht ist: Eine Markierung für jeden Ort

Jetzt kommen wir zur entscheidenden Abgrenzung. Wann solltest du `<address>` auf keinen Fall verwenden? Die Antwort ist einfach: für jede Ortsangabe, die **keine Kontaktinformation** für den Autor oder Eigentümer des Inhalts darstellt.

Stell dir vor, du schreibst einen Reisebericht über Paris und erwähnst die Adresse des Louvre.

**Falsche Verwendung:**

```html
<!-- SO NICHT! -->
<p>
  Der Haupteingang des Louvre befindet sich bei
  <address>
    Rue de Rivoli, 75001 Paris, Frankreich
  </address>.
  Dort steht die berühmte Glaspyramide.
</p>
```
Diese Verwendung ist semantisch falsch. Die Adresse des Louvre ist eine Information *innerhalb* deines Inhalts, aber sie ist nicht die Kontaktadresse von dir, dem Autor des Reiseberichts. Suchmaschinen könnten fälschlicherweise annehmen, du wärst der Betreiber des Louvre. Ein Screenreader könnte seinem Nutzer anbieten, den "Autor des Dokuments" unter dieser Adresse zu kontaktieren. Beides wäre irreführend.

**Korrekte Vorgehensweise:**

Eine solche Adresse gehört einfach in einen normalen Absatz (`<p>`) oder ein anderes passendes Element, ohne spezielle Auszeichnung.

```html
<!-- Korrekt -->
<p>
  Der Haupteingang des Louvre befindet sich bei der Rue de Rivoli, 75001 Paris, Frankreich. 
  Dort steht die berühmte Glaspyramide.
</p>
```
Die Information ist für den menschlichen Leser perfekt verständlich, und du vermeidest es, Maschinen mit falscher Semantik in die Irre zu führen.

Hier sind weitere Beispiele für die falsche Verwendung von `<address>`:
*   Die Adresse eines Unternehmens in einem Nachrichtenartikel über dessen Quartalszahlen.
*   Die fiktive Adresse einer Romanfigur in einer Online-Buchbesprechung.
*   Die Postanschrift eines historischen Ereignisses in einem Geschichtsaufsatz.

In all diesen Fällen ist die Adresse ein Teil des Inhalts (ein "Datum"), aber keine Kontaktmöglichkeit für den Urheber des Inhalts.

#### Warum ist diese Unterscheidung so wichtig?

Die korrekte Verwendung von semantischem HTML ist kein Selbstzweck. Sie hat konkrete Vorteile:

1.  **Maschinenlesbarkeit:** Suchmaschinen wie Google nutzen semantische Tags, um Inhalte besser zu verstehen. Wenn du `<address>` korrekt einsetzt, kann eine Suchmaschine die Kontaktinformationen einer Webseite zuverlässig extrahieren und sie beispielsweise in einem lokalen Suchergebnis oder einem "Knowledge Panel" anzeigen. Bei falscher Verwendung kann dies zu fehlerhaften Daten führen.
2.  **Barrierefreiheit:** Screenreader, die von Menschen mit Sehbehinderungen genutzt werden, können `<address>`-Elemente erkennen. Sie können dem Nutzer mitteilen, dass nun Kontaktinformationen folgen, oder es ihm sogar ermöglichen, direkt zu diesem Abschnitt zu springen. Dies verbessert die Navigation und das Verständnis der Seitenstruktur erheblich.
3.  **Zukunftssicherheit:** Das Web entwickelt sich ständig weiter. Browser, Apps oder Browser-Erweiterungen könnten in Zukunft Funktionen einführen, die speziell mit Kontaktinformationen interagieren – zum Beispiel das direkte Speichern in einem Adressbuch oder das Starten einer Navigations-App. Korrekt ausgezeichnete Daten sind die Voraussetzung dafür.

Ein letzter Hinweis zum Styling: Browser stellen den Inhalt von `<address>`-Elementen standardmäßig kursiv dar. Lass dich davon nicht leiten! Diese Standardformatierung ist eine reine Konvention und kein Indikator für die korrekte Verwendung. Du kannst das Aussehen jederzeit mit CSS nach Belieben anpassen. Die Entscheidung für oder gegen `<address>` sollte immer auf der semantischen Bedeutung basieren, niemals auf dem visuellen Standard-Erscheinungsbild. Denke immer an die Frage: "Handelt es sich hierbei um die Kontaktinformation des Seiten- oder Artikelautors?" Wenn die Antwort "Nein" lautet, ist `<address>` das falsche Werkzeug.
