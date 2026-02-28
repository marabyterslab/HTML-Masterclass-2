# Das time-Element

### Das `<time>`-Element: Semantik für Zeit und Datum

In der Welt des Webs sind Zeit- und Datumsangaben allgegenwärtig. Du findest sie in Blogartikeln („Veröffentlicht am …“), bei Veranstaltungshinweisen („Beginn um 20:00 Uhr“), in Nachrichten-Tickern oder bei Fahrplänen. Für uns Menschen sind diese Angaben meistens intuitiv verständlich. Wir können Kontexte wie „gestern“, „nächsten Dienstag“ oder „im Sommer 2026“ ohne Probleme deuten.

Für eine Maschine, sei es eine Suchmaschine, ein Screenreader oder ein Kalenderprogramm, sind solche relativen oder uneindeutigen Angaben jedoch nur schwer zu verarbeiten. Hier kommt das `<time>`-Element ins Spiel. Seine Aufgabe ist es, eine Brücke zwischen der für Menschen lesbaren Form einer Zeitangabe und einer standardisierten, maschinenlesbaren Form zu schlagen. Es verleiht Zeit und Datum eine semantische Bedeutung.

#### Die grundlegende Struktur

Auf den ersten Blick sieht das `<time>`-Element sehr unscheinbar aus. In seiner einfachsten Form umschließt es lediglich eine für den Menschen lesbare Datums- oder Zeitangabe.

```html
<p>Unser nächstes Team-Meeting findet am <time>2025-10-26</time> statt.</p>
```

Visuell verändert dieser Code erst einmal nichts an der Darstellung im Browser. Der Text „2025-10-26“ wird genauso angezeigt, als stünde er in einem einfachen `<p>`- oder `<span>`-Tag. Die wahre Magie verbirgt sich jedoch in seiner semantischen Kraft und dem dazugehörigen `datetime`-Attribut.

#### Das `datetime`-Attribut: Das Herzstück des Elements

Während der Inhalt zwischen den `<time>`-Tags für deine menschlichen Besucher bestimmt ist, liefert das `datetime`-Attribut die präzise, standardisierte Information für Maschinen. Der Wert dieses Attributs muss einem gültigen Datums- oder Zeitformat folgen, das auf dem internationalen Standard ISO 8601 basiert.

Das Tolle daran ist die Flexibilität: Der für Menschen lesbare Text kann ganz anders aussehen als der maschinenlesbare Wert.

Stell dir vor, du möchtest den Veröffentlichungstag eines Artikels angeben. Für deine Leser schreibst du etwas Freundliches und Leichtlesbares. Im Hintergrund gibst du der Maschine die exakte Information.

```html
<p>Veröffentlicht am <time datetime="2025-10-26">26. Oktober 2025</time>.</p>
```

Hier sehen deine Besucher den Text „26. Oktober 2025“. Eine Suchmaschine wie Google oder ein Browser-Plugin, das diesen Artikel indexiert, liest jedoch den Wert `2025-10-26` aus dem `datetime`-Attribut und weiß unmissverständlich: Dieser Artikel stammt vom 26. Oktober 2025. Diese Information kann für die Sortierung von Suchergebnissen nach Aktualität oder für automatische Archivierungsfunktionen entscheidend sein.

#### Gültige Formate für das `datetime`-Attribut

Die Stärke des `datetime`-Attributs liegt in seiner klar definierten Syntax. Es gibt verschiedene gültige Formate, die du je nach Anwendungsfall nutzen kannst. Lass uns die wichtigsten durchgehen.

##### 1. Ein vollständiges Datum
Das am häufigsten verwendete Format ist `YYYY-MM-DD` (Jahr-Monat-Tag).

```html
<time datetime="1991-08-06">Am Tag, als das World Wide Web öffentlich wurde</time>
```

##### 2. Nur Jahr und Monat
Manchmal ist der genaue Tag nicht relevant. Dann kannst du das Format `YYYY-MM` verwenden.

```html
<p>Unsere nächste große Software-Version ist für <time datetime="2026-03">März 2026</time> geplant.</p>
```

##### 3. Nur das Jahr
Wenn du dich nur auf ein Jahr beziehen möchtest, reicht `YYYY`.

```html
<p>Das Unternehmen wurde <time datetime="2018">2018</time> gegründet.</p>
```

##### 4. Kalenderwoche
Auch die Angabe einer spezifischen Kalenderwoche ist möglich mit dem Format `YYYY-Www` (W ist ein fester Buchstabe, ww steht für die zweistellige Wochennummer).

```html
<p>Die Projekt-Deadline ist in der <time datetime="2025-W48">48. Kalenderwoche 2025</time>.</p>
```

##### 5. Uhrzeit
Wenn das Datum keine Rolle spielt, kannst du auch nur eine Uhrzeit angeben. Das Format ist `hh:mm` (Stunden:Minuten) oder `hh:mm:ss` (mit Sekunden).

```html
<p>Die Vorstellung beginnt pünktlich um <time datetime="20:00">20:00 Uhr</time>.</p>
```

##### 6. Datum und Uhrzeit mit Zeitzoneninformation
Dies ist das wohl mächtigste und präziseste Format. Es kombiniert Datum und Uhrzeit und fügt eine Information über die Zeitzone hinzu. Das ist unerlässlich für globale Anwendungen, bei denen Nutzer aus verschiedenen Teilen der Welt zugreifen.

Das Standardformat ist `YYYY-MM-DDThh:mm:ssZ`.

*   Das `T` ist ein fester Trenner zwischen dem Datumsteil und dem Zeitteil.
*   Das `Z` am Ende steht für „Zulu Time“, was der Koordinierten Weltzeit (UTC) entspricht.

```html
<article>
  <h2>Live-Übertragung vom Mars Rover</h2>
  <p>Die Übertragung beginnt am <time datetime="2026-02-18T19:55Z">18. Februar 2026 um 19:55 Uhr UTC</time>.</p>
</article>
```

Wenn du eine spezifische Zeitzone angeben möchtest, die von UTC abweicht, ersetzt du das `Z` durch den Offset, zum Beispiel `+02:00` für die mitteleuropäische Sommerzeit.

```html
<p>
  Unser Webinar findet um 
  <time datetime="2026-04-15T10:00+02:00">10:00 Uhr vormittags (MESZ)</time> 
  statt.
</p>
```
Browser und andere Programme können diese Information nutzen, um die Zeit automatisch in die lokale Zeitzone des Nutzers umzurechnen.

##### 7. Zeitdauer
Eine weniger bekannte, aber sehr nützliche Anwendung des `<time>`-Elements ist die Angabe einer Zeitdauer. Hierfür wird das Format `P...` (für "Period") verwendet.

*   `PT2H30M` steht für eine Dauer von 2 Stunden und 30 Minuten (Time: 2 Hours, 30 Minutes).
*   `P3D` steht für eine Dauer von 3 Tagen (Period: 3 Days).

```html
<p>Die Kochzeit für den Braten beträgt <time datetime="PT2H15M">2 Stunden und 15 Minuten</time>.</p>
<p>Die Standard-Lieferzeit beträgt <time datetime="P5D">fünf Tage</time>.</p>
```

#### Warum solltest du das `<time>`-Element verwenden?

Der Einsatz des `<time>`-Elements ist ein Paradebeispiel für semantisches HTML. Du fügst deinem Inhalt eine unsichtbare, aber wertvolle Informationsebene hinzu. Die Vorteile sind vielfältig:

1.  **Suchmaschinenoptimierung (SEO):** Suchmaschinen wie Google erkennen das `<time>`-Element und können den Inhalt besser kontextualisieren. Bei einem Nachrichtenartikel kann das Veröffentlichungsdatum entscheidend für das Ranking sein. Bei einem Event-Eintrag kann die Suchmaschine das Datum direkt in den Suchergebnissen als Rich Snippet anzeigen.

2.  **Barrierefreiheit (Accessibility):** Screenreader, die von Menschen mit Sehbehinderungen genutzt werden, können Datums- und Zeitangaben, die mit `<time>` ausgezeichnet sind, korrekt und standardisiert vorlesen. Eine vage Angabe wie „letzten Freitag“ kann für jemanden, der den Kontext nicht schnell erfassen kann, verwirrend sein. `<time datetime="2025-10-24">letzten Freitag</time>` löst dieses Problem.

3.  **Interoperabilität und Zukunftsfähigkeit:** Browser und andere Software (User Agents) können auf diese strukturierten Daten zugreifen. Denkbar sind Browser-Erweiterungen, die automatisch alle Termine auf einer Seite erkennen und einen Export in den persönlichen Kalender anbieten. Klickt ein Nutzer auf eine so ausgezeichnete Zeit, könnte der Browser direkt vorschlagen, einen Kalendereintrag zu erstellen.

4.  **Einfachere Verarbeitung mit JavaScript:** Wenn du mit JavaScript auf Datumsangaben im DOM zugreifen musst, ist es deutlich einfacher und robuster, den standardisierten Wert aus dem `datetime`-Attribut zu lesen, anstatt zu versuchen, einen menschenlesbaren Text wie „Dienstag, der 5. November“ zu parsen. Der Zugriff erfolgt simpel über die `dateTime`-Eigenschaft des DOM-Elements: `document.querySelector('time').dateTime`.

#### Was das `<time>`-Element nicht ist

Es ist wichtig zu verstehen, dass das `<time>`-Element ausschließlich für die semantische Auszeichnung von präzisen Daten und Zeiten im proleptischen gregorianischen Kalender gedacht ist.

*   **Es ist kein Styling-Element:** Du solltest `<time>` nicht verwenden, nur weil du eine Zeitangabe visuell hervorheben möchtest. Dafür sind CSS-Klassen in Verbindung mit `<span>` oder anderen Elementen die richtige Wahl.
*   **Es ist nicht für fiktive oder antike Daten geeignet:** Die Angabe des Datums „Im Jahre 123 vor Christus“ fällt nicht in den Gültigkeitsbereich des gregorianischen Kalenders und sollte daher nicht mit dem `<time>`-Element ausgezeichnet werden. Der Standard ist hier sehr spezifisch.

Indem du das `<time>`-Element konsequent und korrekt einsetzt, machst du deine Webseiten nicht nur für heutige Technologien verständlicher, sondern auch robuster für zukünftige Anwendungen, die wir uns heute vielleicht noch gar nicht vorstellen können. Du gibst einer der fundamentalsten menschlichen Informationen – der Zeit – eine klare und universelle digitale Identität.
