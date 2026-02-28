# Öffnen in neuem Tab (target_blank)

### Das `target`-Attribut: Links in neuen Tabs öffnen und die Welt dahinter

Wenn du im Web unterwegs bist, ist dir dieses Verhalten unzählige Male begegnet: Du klickst auf einen Link und anstatt dass sich die aktuelle Seite ändert, öffnet sich wie von Zauberhand ein neuer Tab in deinem Browser. Dieses simple, aber mächtige Feature ist kein Zufall, sondern das Ergebnis eines einzigen HTML-Attributs: `target`. Es steuert, *wo* der Inhalt eines Links geladen werden soll.

In diesem Kapitel tauchen wir tief in die Funktionsweise des `target`-Attributs ein. Wir klären, wann sein Einsatz sinnvoll ist, welche Fallstricke du vermeiden solltest und warum ein kleiner Zusatz für die Sicherheit deiner Nutzer unerlässlich ist.

#### Die Grundlagen: `target="_blank"`

Das Standardverhalten eines Links (`<a>`-Element) ist es, die verlinkte Ressource im selben Fenster oder Tab zu öffnen, in dem der Link angeklickt wurde. Das aktuelle Dokument wird also durch das neue ersetzt.

Möchtest du dieses Verhalten ändern und den Link in einem neuen Tab öffnen, kommt das `target`-Attribut ins Spiel. Der gängigste und wichtigste Wert für dieses Attribut ist `_blank`.

Schauen wir uns die Syntax an:

```html
<a href="https://www.wikipedia.org/" target="_blank">Entdecke Wikipedia in einem neuen Tab</a>
```

So einfach ist das. Durch das Hinzufügen von `target="_blank"` gibst du dem Browser die Anweisung, den Link in einem neuen, unbenannten Browser-Kontext zu öffnen. In der Praxis bedeutet das heutzutage fast immer einen neuen Tab. Der Unterstrich am Anfang von `_blank` signalisiert dem Browser, dass es sich um ein spezielles Schlüsselwort handelt und nicht um den Namen eines Fensters.

#### Wann ist der Einsatz von `target="_blank"` sinnvoll?

Die Entscheidung, einen Link in einem neuen Tab zu öffnen, sollte immer bewusst und im Sinne der Nutzerfreundlichkeit getroffen werden. Es geht darum, den Lesefluss oder den Arbeitsprozess des Nutzers nicht unnötig zu unterbrechen. Hier sind einige klassische Szenarien, in denen `target="_blank"` eine gute Wahl ist:

1.  **Links zu externen Websites:** Dies ist der häufigste Anwendungsfall. Wenn du von deiner Website auf eine andere, externe Seite verlinkst, möchtest du deine Besucher nicht verlieren. Indem du den externen Link in einem neuen Tab öffnest, bleibt deine Seite im ursprünglichen Tab erhalten. Der Nutzer kann die externe Information einsehen und danach nahtlos zu deiner Seite zurückkehren, ohne den „Zurück“-Button mehrfach betätigen zu müssen.

2.  **Links zu Dokumenten und Dateien:** Wenn ein Link auf ein PDF, ein Bild in voller Auflösung, ein Word-Dokument oder eine andere Datei verweist, die der Browser eventuell direkt anzeigt oder zum Download anbietet, ist ein neuer Tab ideal. Der Nutzer kann das Dokument betrachten oder herunterladen, während der Kontext deiner Webseite – zum Beispiel ein ausgefülltes Formular oder eine bestimmte Scroll-Position – unangetastet bleibt.

3.  **Links zu Hilfeseiten oder Glossaren:** Stell dir vor, ein Nutzer füllt ein komplexes Online-Formular aus und stößt auf einen Fachbegriff, den er nicht kennt. Ein Link auf eine Erklärungsseite, der sich in einem neuen Tab öffnet, erlaubt es ihm, die Definition nachzulesen, ohne die bereits eingegebenen Formulardaten zu verlieren.

#### Die Kehrseite: Wann du `target="_blank"` vermeiden solltest

So nützlich `target="_blank"` auch sein kann, ein übermäßiger oder falscher Gebrauch kann die Nutzererfahrung empfindlich stören. Die goldene Regel lautet: **Verwende `target="_blank"` niemals für die interne Navigation auf deiner eigenen Website.**

Wenn ein Nutzer von deiner Startseite zu deiner „Über uns“-Seite navigiert, erwartet er, dass dies im selben Tab geschieht. Er verlässt ja deine Website nicht. Jeder interne Klick, der einen neuen Tab öffnet, führt zu einer unübersichtlichen Ansammlung von Tabs deiner eigenen Seite und bricht die erwartete Funktionsweise des „Zurück“-Buttons. Der Nutzer verliert die Kontrolle über seine Navigation, was schnell zu Frustration führt. Gib dem Nutzer die Wahl: Er kann jederzeit selbst entscheiden, einen Link per Rechtsklick oder mit einer Tastenkombination (z. B. `Strg` + Klick) in einem neuen Tab zu öffnen. Zwinge ihm dieses Verhalten nicht auf, wenn es nicht absolut notwendig ist.

#### Der entscheidende Sicherheitsaspekt: `rel="noopener noreferrer"`

Jetzt kommen wir zu einem Punkt, der oft übersehen wird, aber für die Professionalität und Sicherheit deiner Website von entscheidender Bedeutung ist. Wenn du `target="_blank"` verwendest, solltest du **immer** auch das `rel`-Attribut mit den Werten `noopener` und `noreferrer` hinzufügen.

Der vollständige, sichere Code sieht also so aus:

```html
<a href="https://externe-seite.com" target="_blank" rel="noopener noreferrer">Sicherer Link zu einer externen Seite</a>
```

Aber warum ist das so wichtig?

Das Problem, das hier gelöst wird, ist eine Sicherheitslücke namens „Tabnabbing“. Wenn eine Seite über `target="_blank"` in einem neuen Tab geöffnet wird, erhält diese neue Seite über JavaScript Zugriff auf das `window.opener`-Objekt der ursprünglichen Seite. Das bedeutet, die neu geöffnete Seite (die du nicht unter Kontrolle hast) könnte potenziell deine Seite im Hintergrund manipulieren. Ein bösartiges Skript auf der Zielseite könnte deine Seite zum Beispiel auf eine gefälschte Login-Seite umleiten. Der Nutzer bemerkt dies vielleicht nicht sofort, kehrt zu deinem Tab zurück und gibt ahnungslos seine Zugangsdaten auf der Phishing-Seite ein.

Hier kommen `noopener` und `noreferrer` ins Spiel:

*   **`rel="noopener"`:** Dieser Wert verhindert den Zugriff auf das `window.opener`-Objekt. Die Verbindung zwischen den beiden Tabs wird gekappt, und der neue Tab kann deine ursprüngliche Seite nicht mehr manipulieren. Das `window.opener`-Objekt wird auf `null` gesetzt.

*   **`rel="noreferrer"`:** Dieser Wert tut alles, was `noopener` tut, und geht noch einen Schritt weiter: Er verhindert, dass der Browser den `Referer`-HTTP-Header an die Zielseite sendet. Das bedeutet, die neue Seite erfährt nicht, von welcher URL der Besucher gekommen ist. Das ist ein kleiner, aber feiner Beitrag zum Datenschutz.

Auch wenn moderne Browser inzwischen oft automatisch ein `noopener`-Verhalten für `target="_blank"`-Links anwenden, solltest du dich niemals darauf verlassen. Die explizite Angabe von `rel="noopener noreferrer"` ist der saubere, korrekte und abwärtskompatible Weg, um deine Nutzer und deine Website zu schützen. Mach es dir zur Gewohnheit: Immer wenn du `target="_blank"` schreibst, folgt direkt danach `rel="noopener noreferrer"`.

#### Weitere Werte für das `target`-Attribut

Obwohl `_blank` der mit Abstand häufigste Wert ist, gibt es noch weitere, die du kennen solltest, auch wenn sie heute seltener verwendet werden. Sie waren vor allem in der Ära der `frameset`-basierten Websites relevant.

*   **`_self`:** Dies ist das Standardverhalten. Der Link öffnet sich im selben Frame oder Fenster. Du musst diesen Wert eigentlich nie explizit angeben, es sei denn, du möchtest ein globales `target` (z. B. im `<base>`-Tag) für einen einzelnen Link überschreiben.

*   **`_parent`:** Öffnet den Link im übergeordneten Frameset. Wenn deine Seite in einem `<iframe>` geladen wird, würde ein Link mit `target="_parent"` in dem Dokument geladen, das den `<iframe>` enthält.

*   **`_top`:** Bricht aus allen Frames aus und lädt den Link im vollständigen Browserfenster. Das ist nützlich, wenn deine Seite tief in mehreren `<iframe>`s verschachtelt ist und der Link die gesamte Seite neu laden soll.

*   **Ein benannter Frame (`<framename>`):** Du kannst dem `target`-Attribut auch einen eigenen Namen geben, zum Beispiel `target="hauptinhalt"`. Wenn ein Nutzer auf einen solchen Link klickt, sucht der Browser nach einem Fenster oder `<iframe>` mit diesem Namen. Findet er eines, wird der Link dort geladen. Findet er keines, öffnet er einen neuen Tab und gibt ihm diesen Namen. Klickt der Nutzer später auf einen anderen Link mit demselben `target`-Namen, wird dieser im bereits geöffneten und benannten Tab geladen, anstatt einen weiteren neuen Tab zu öffnen.

Ein Beispiel für die Wiederverwendung eines Tabs:

```html
<!-- Dieser Link öffnet einen neuen Tab mit dem Namen "infofenster" -->
<a href="seite1.html" target="infofenster">Info 1 anzeigen</a>

<!-- Dieser Link lädt seinen Inhalt in denselben Tab, der zuvor geöffnet wurde -->
<a href="seite2.html" target="infofenster">Info 2 anzeigen</a>
```

Diese Technik kann in bestimmten Webanwendungen nützlich sein, ist aber im alltäglichen Webdesign eher eine Seltenheit geworden.

Für deine tägliche Arbeit als Webentwickler sind vor allem zwei Dinge entscheidend: das bewusste und nutzerfreundliche Einsetzen von `target="_blank"` und das obligatorische Hinzufügen von `rel="noopener noreferrer"` aus Sicherheitsgründen. Damit beherrschst du das Verhalten von Links wie ein Profi.
