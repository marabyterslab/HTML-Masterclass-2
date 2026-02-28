# Öffnen in neuem Tab (target_blank)

### Das `target`-Attribut: Links in einem neuen Tab öffnen

Stell dir vor, du liest einen spannenden Artikel auf einer Webseite. Mitten im Text findest du einen Link zu einer externen Quelle, die eine erwähnte Studie belegt. Du klickst darauf, und plötzlich ist der Artikel, in den du so vertieft warst, verschwunden. An seiner Stelle siehst du nun die wissenschaftliche Abhandlung. Um zum ursprünglichen Artikel zurückzukehren, musst du den Zurück-Button deines Browsers nutzen. Dieses Verhalten ist das Standardverhalten von Hyperlinks im Web: Sie laden die neue Ressource im selben Browserfenster oder Tab.

Es gibt jedoch unzählige Situationen, in denen dieses Standardverhalten nicht ideal ist. Vielleicht möchtest du deine Besucher nicht von deiner Seite wegführen, sondern ihnen zusätzliche Informationen in einem separaten Kontext anbieten. Genau hier kommt das `target`-Attribut des `<a>`-Elements ins Spiel. Es gibt dir die Kontrolle darüber, *wo* der verlinkte Inhalt geöffnet wird.

#### Die Grundlagen: `target="_blank"`

Die mit Abstand häufigste und wichtigste Anwendung des `target`-Attributs ist das Öffnen eines Links in einem neuen Tab. Um dies zu erreichen, weist du dem Attribut den speziellen Wert `_blank` zu.

Der Code dafür ist denkbar einfach:

```html
<a href="https://beispiel-externe-seite.com" target="_blank">
  Besuche unsere Partnerseite
</a>
```

Wenn ein Benutzer auf diesen Link klickt, weist der Browser an, einen neuen Tab (oder, bei älteren Browser-Konfigurationen, ein neues Fenster) zu öffnen und die URL `https://beispiel-externe-seite.com` darin zu laden. Der ursprüngliche Tab, auf dem sich der Benutzer befand, bleibt unberührt im Hintergrund geöffnet.

Der Unterstrich am Anfang von `_blank` ist entscheidend. Es handelt sich um ein reserviertes Schlüsselwort, das dem Browser signalisiert: „Öffne dies immer in einem brandneuen, unbenannten Kontext.“ Würdest du den Unterstrich weglassen und stattdessen einen Namen wie `target="meinFenster"` verwenden, würde der erste Klick einen neuen Tab mit diesem Namen öffnen. Jeder weitere Klick auf einen Link mit demselben `target`-Wert würde jedoch diesen bereits geöffneten Tab wiederverwenden und seinen Inhalt ersetzen, anstatt immer wieder neue Tabs zu erzeugen. `_blank` garantiert also bei jedem Klick einen frischen Tab.

#### Wann solltest du einen neuen Tab erzwingen?

Die Entscheidung, einen Link in einem neuen Tab zu öffnen, sollte immer bewusst getroffen werden, da sie das gewohnte Nutzerverhalten durchbricht. Der Zurück-Button verliert im neuen Tab seine ursprüngliche Funktion. Es gibt jedoch klare Anwendungsfälle, in denen `target="_blank"` die Benutzererfahrung deutlich verbessert.

1.  **Links zu externen Webseiten:** Dies ist der klassische Anwendungsfall. Wenn du von deiner Webseite auf eine völlig andere Domain verlinkst, möchtest du deine Besucher nicht verlieren. Indem du den externen Link in einem neuen Tab öffnest, bleibt deine Seite im Browser präsent. Der Nutzer kann die externe Information einsehen und anschließend einfach den neuen Tab schließen, um nahtlos auf deiner Seite weiterzumachen.

2.  **Links zu Dokumenten (PDFs, Bilder, etc.):** Wenn du einen Link zum Download oder zur Anzeige einer PDF-Datei, eines hochauflösenden Bildes oder einer anderen Mediendatei anbietest, wollen Benutzer selten die aktuelle Seite verlassen. Sie möchten das Dokument einsehen oder herunterladen und dann zur ursprünglichen Seite zurückkehren. Ein neuer Tab ist hierfür die perfekte Lösung.

    ```html
    <a href="/dokumente/jahresbericht-2023.pdf" target="_blank">
      Jahresbericht 2023 (PDF) herunterladen
    </a>
    ```

3.  **Links zu Hilfeseiten oder Glossaren:** Stell dir ein komplexes Formular vor. Neben einem bestimmten Eingabefeld befindet sich ein Hilfe-Icon, das auf eine Seite mit Erklärungen verweist. Wenn dieser Link die aktuelle Seite ersetzen würde, wären alle bereits ausgefüllten Formulardaten verloren. Das Öffnen der Hilfeseite in einem neuen Tab bewahrt den Kontext und den Fortschritt des Nutzers.

#### Die Sicherheitsfalle: `rel="noopener noreferrer"`

So nützlich `target="_blank"` auch ist, es birgt eine oft übersehene Sicherheitslücke. Wenn eine Seite A eine Seite B in einem neuen Tab öffnet, erhält Seite B über JavaScript Zugriff auf das `window.opener`-Objekt. Dieses Objekt repräsentiert die ursprüngliche Seite A.

Das bedeutet, eine bösartige Seite B könnte potenziell die Kontrolle über den Tab von Seite A übernehmen und ihn zum Beispiel auf eine Phishing-Seite umleiten, die wie deine Anmeldeseite aussieht. Der Benutzer, der nur kurz auf den neuen Tab geschaut hat, bemerkt die Änderung im Hintergrund vielleicht nicht und gibt ahnungslos seine Zugangsdaten ein. Dieses Angriffsszenario wird als „Tabnabbing“ bezeichnet.

Glücklicherweise ist die Lösung einfach und sollte zur Standardpraxis werden. Du musst dem `<a>`-Element ein weiteres Attribut hinzufügen: `rel` (für „relationship“).

```html
<a href="https://eine-fremde-webseite.com" target="_blank" rel="noopener noreferrer">
  Ein sicherer Link zu einer externen Seite
</a>
```

Schauen wir uns die beiden Werte genauer an:

*   **`noopener`**: Dieser Wert weist den Browser an, die Verbindung zwischen den beiden Tabs zu kappen. Das `window.opener`-Objekt im neuen Tab wird auf `null` gesetzt, wodurch jeglicher Zugriff auf den ursprünglichen Tab unterbunden wird. Das Problem des Tabnabbing ist damit gelöst.

*   **`noreferrer`**: Dieser Wert tut alles, was `noopener` tut, und verhindert zusätzlich, dass der Browser den `Referer`-Header an die neue Seite sendet. Der `Referer`-Header teilt der Zielseite mit, von welcher URL der Besucher gekommen ist. Das Weglassen dieses Headers erhöht die Privatsphäre des Nutzers.

**Die goldene Regel lautet also: Immer wenn du `target="_blank"` verwendest, solltest du auch `rel="noopener noreferrer"` hinzufügen.** Moderne Browser setzen `noopener` oft schon automatisch, wenn `target="_blank"` verwendet wird, aber es ist eine bewährte Praxis, es explizit anzugeben, um auch ältere Browser abzudecken und die Intention im Code klar zu machen.

#### Barrierefreiheit: Nutzer informieren

Ein Link, der sich anders verhält als erwartet, kann für manche Nutzer verwirrend sein, insbesondere für Menschen, die Screenreader verwenden oder motorische Einschränkungen haben. Sie bemerken möglicherweise nicht sofort, dass sich ein neuer Tab geöffnet hat, und wundern sich, warum der Zurück-Button nicht funktioniert.

Es ist daher eine gute Praxis, den Nutzer darüber zu informieren, was passieren wird. Dafür gibt es zwei gängige Methoden, die sich gut ergänzen.

1.  **Visuelle Indikatoren:** Ein kleines Icon neben dem Linktext, das ein Fenster mit einem Pfeil nach außen zeigt, ist eine weit verbreitete und schnell verständliche Konvention. Es signalisiert visuell: „Diese Aktion verlässt den aktuellen Kontext.“

2.  **Textuelle Hinweise für Screenreader:** Ein visueller Indikator allein hilft Nutzern von Screenreadern nicht. Du kannst jedoch unsichtbaren Text hinzufügen, den nur assistierende Technologien wahrnehmen.

Ein barrierefreier und sicherer Link könnte so aussehen:

```html
<style>
  /* Dieses CSS versteckt das Element visuell, aber nicht für Screenreader */
  .visually-hidden {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border-width: 0;
  }
</style>

<a href="https://beispiel-externe-seite.com" target="_blank" rel="noopener noreferrer">
  Besuche die offizielle Dokumentation
  <span class="visually-hidden">(öffnet in neuem Tab)</span>
  <!-- Hier könnte noch ein SVG-Icon für die visuelle Darstellung platziert werden -->
</a>
```

Der Screenreader liest in diesem Fall vor: „Link: Besuche die offizielle Dokumentation (öffnet in neuem Tab)“. Damit ist die Aktion für alle Nutzer transparent und vorhersehbar.

#### Andere Werte für das `target`-Attribut

Obwohl `_blank` der mit Abstand relevanteste Wert ist, gibt es historisch bedingt noch andere. Du wirst ihnen in der modernen Webentwicklung selten begegnen, aber es ist gut, sie zu kennen.

*   **`_self`**: Dies ist das Standardverhalten. Der Link wird im selben Fenster oder Tab geöffnet. Du musst diesen Wert nie explizit angeben, es sei denn, du möchtest ein anderes, übergeordnetes `target`-Verhalten (z. B. durch ein `<base>`-Tag im `<head>`) für einen einzelnen Link überschreiben.
*   **`_parent`**: Öffnet den Link im übergeordneten Frameset.
*   **`_top`**: Bricht aus allen Frames aus und öffnet den Link im obersten, also dem vollständigen Browserfenster.

Die Werte `_parent` und `_top` stammen aus der Ära der `framesets`, einer heute veralteten Technik zur Seitengestaltung. In modernen Kontexten mit `<iframe>`-Elementen können sie jedoch in Nischenfällen noch eine Rolle spielen, um aus einem eingebetteten Inhalt auszubrechen.

Für deine tägliche Arbeit als Webentwickler ist die Kombination aus `target="_blank"` und `rel="noopener noreferrer"` jedoch das entscheidende Wissen, das du aus diesem Kapitel mitnehmen solltest. Es ist ein kleines Detail mit großer Wirkung auf Benutzerfreundlichkeit, Sicherheit und Professionalität deiner Webseiten.
