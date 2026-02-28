# Download-Attribute

### Das `download`-Attribut: Wenn ein Klick zum Speichern führt

Stell dir vor, du bietest auf deiner Webseite wichtige Dokumente an: einen Geschäftsbericht als PDF, ein Portfolio als ZIP-Archiv oder vielleicht ein hochauflösendes Bild, das deine Besucher als Desktophintergrund verwenden können. Normalerweise, wenn ein Nutzer auf einen Link zu einer solchen Datei klickt, versucht der Browser sein Bestes, diese Datei direkt im Browserfenster darzustellen. Ein PDF öffnet sich im integrierten PDF-Viewer, ein Bild wird auf einer leeren Seite angezeigt, und bei einem Textdokument siehst du den rohen Inhalt.

Das ist oft nicht das, was du oder dein Besucher beabsichtigen. In den meisten Fällen sollen solche Ressourcen direkt auf dem Computer des Nutzers gespeichert werden. Genau hier kommt das `download`-Attribut ins Spiel. Es ist ein einfaches, aber äußerst mächtiges Werkzeug, das das Standardverhalten eines Links grundlegend verändert.

#### Die grundlegende Funktion

Das `download`-Attribut ist ein sogenanntes boolesches Attribut für das `<a>`-Element. Das bedeutet, du kannst es einfach ohne einen zugewiesenen Wert verwenden. Wenn es vorhanden ist, signalisiert es dem Browser: „Hey, die Datei, auf die dieser Link verweist, soll nicht angezeigt, sondern heruntergeladen werden.“

Sehen wir uns ein einfaches Beispiel an. Angenommen, du hast eine PDF-Datei, die heruntergeladen werden soll:

```html
<!-- Ohne das download-Attribut -->
<a href="dokumente/jahresbericht-2023.pdf">Jahresbericht 2023 ansehen</a>

<!-- Mit dem download-Attribut -->
<a href="dokumente/jahresbericht-2023.pdf" download>Jahresbericht 2023 herunterladen</a>
```

Im ersten Fall würde der Klick auf den Link den Browser dazu veranlassen, die PDF-Datei im aktuellen Tab oder in einem neuen Tab zu öffnen (je nach Browsereinstellungen und anderen Attributen wie `target="_blank"`). Der Nutzer müsste dann manuell auf ein „Speichern“-Symbol im PDF-Viewer des Browsers klicken, um die Datei zu sichern.

Im zweiten Fall ändert das `download`-Attribut alles. Ein Klick auf diesen Link öffnet direkt den „Speichern unter…“-Dialog des Betriebssystems. Der Browser versucht nicht mehr, die Datei zu interpretieren oder anzuzeigen. Er behandelt sie als eine Ressource, die der Nutzer auf seiner Festplatte ablegen möchte. Der ursprüngliche Dateiname (`jahresbericht-2023.pdf`) wird dabei als Vorschlag im Speicher-Dialog verwendet.

#### Den Dateinamen beim Download festlegen

Die wahre Stärke des `download`-Attributs zeigt sich, wenn du ihm einen Wert zuweist. Der Wert, den du dem Attribut gibst, wird zum vorgeschlagenen Dateinamen im „Speichern unter…“-Dialog. Das ist unglaublich nützlich, insbesondere wenn deine Dateien auf dem Server kryptische oder dynamisch generierte Namen haben.

Stell dir vor, dein Content-Management-System speichert Dateien mit einer eindeutigen ID anstatt eines lesbaren Namens. Der Link zu deinem Bericht könnte so aussehen:

```html
<a href="/files/f3d2a-v5-report_final_rev2.pdf">Bericht herunterladen</a>
```

Wenn ein Nutzer auf diesen Link klickt (selbst mit einem leeren `download`-Attribut), würde der vorgeschlagene Dateiname `f3d2a-v5-report_final_rev2.pdf` lauten. Das ist nicht sehr nutzerfreundlich.

Indem du dem `download`-Attribut einen Wert gibst, kannst du einen sauberen und verständlichen Dateinamen vorschlagen:

```html
<a href="/files/f3d2a-v5-report_final_rev2.pdf" download="Jahresbericht-2023-final.pdf">
  Finalen Jahresbericht (2023) herunterladen
</a>
```

Wenn der Nutzer nun auf diesen Link klickt, öffnet sich der Speicher-Dialog und schlägt als Dateinamen `Jahresbericht-2023-final.pdf` vor. Dies verbessert die Benutzererfahrung erheblich. Der Nutzer weiß sofort, was er herunterlädt, und muss den Dateinamen nicht manuell korrigieren.

Du kannst hier auch die Dateiendung weglassen, aber es ist eine gute Praxis, sie beizubehalten, damit das Betriebssystem die Datei korrekt zuordnen kann. Der Browser ist in der Regel intelligent genug, die korrekte Endung basierend auf dem Dateityp (MIME-Typ), den der Server sendet, hinzuzufügen, falls du sie vergisst. Dich darauf zu verlassen, ist aber nicht empfehlenswert.

#### Die wichtigste Einschränkung: Die Same-Origin-Policy

Das `download`-Attribut ist ein fantastisches Werkzeug, aber es hat eine sehr wichtige Einschränkung, die du unbedingt verstehen musst: Es funktioniert zuverlässig nur für Dateien, die von derselben *Origin* (Herkunft) stammen wie deine Webseite.

Was bedeutet "Same-Origin"? Eine Herkunft ist definiert durch die Kombination aus Protokoll (z. B. `https`), Hostname (z. B. `www.deine-domain.de`) und Port (z. B. `:80` oder `:443`). Wenn sich auch nur einer dieser drei Teile unterscheidet, handelt es sich um eine andere Herkunft (*Cross-Origin*).

*   **Gleiche Herkunft:** Ein Link von `https://www.deine-domain.de/seite.html` auf `https://www.deine-domain.de/files/datei.zip`.
*   **Andere Herkunft (Cross-Origin):** Ein Link von `https://www.deine-domain.de` auf `https://cdn.another-domain.com/files/datei.zip`.

Wenn du versuchst, das `download`-Attribut für eine Cross-Origin-Ressource zu verwenden, werden die meisten modernen Browser es aus Sicherheitsgründen ignorieren. Der Link verhält sich dann so, als wäre das `download`-Attribut gar nicht vorhanden. Der Browser navigiert einfach zur URL, anstatt einen Download auszulösen.

Diese Einschränkung ist ein Teil der *Same-Origin-Policy*, eines grundlegenden Sicherheitskonzepts im Web. Sie verhindert, dass eine bösartige Webseite Ressourcen von einer anderen Domain herunterlädt und potenziell manipuliert, ohne dass der Nutzer dies beabsichtigt.

Was also tun, wenn deine Dateien auf einem anderen Server liegen, zum Beispiel auf einem Content Delivery Network (CDN)? In diesem Fall liegt die Kontrolle nicht mehr allein bei deinem HTML-Code. Der Server, der die Datei ausliefert, muss dem Browser explizit mitteilen, dass die Datei als Download behandelt werden soll. Dies geschieht über einen HTTP-Header namens `Content-Disposition`. Wenn der Server diesen Header mit dem Wert `attachment` sendet, wird der Browser einen Download erzwingen, unabhängig von der Herkunft und unabhängig davon, ob im HTML ein `download`-Attribut gesetzt ist. Der `Content-Disposition`-Header hat immer Vorrang.

#### Kreative Anwendungsfälle: Dynamisch erzeugte Downloads

Eine besonders spannende Anwendung des `download`-Attributs ergibt sich im Zusammenspiel mit JavaScript. Du bist nicht darauf beschränkt, nur auf existierende Dateien auf deinem Server zu verlinken. Du kannst Daten auch direkt im Browser des Nutzers erzeugen und sie ihm dann als Datei zum Download anbieten.

Stell dir eine Web-Anwendung vor, in der ein Nutzer Daten in ein Formular eingibt. Du könntest ihm die Möglichkeit geben, diese Daten als Textdatei oder CSV-Datei zu exportieren.

Der Prozess funktioniert so:

1.  Du sammelst die Daten mit JavaScript und erstellst daraus einen String.
2.  Du wandelst diesen String in ein `Blob`-Objekt um. Ein Blob (Binary Large Object) ist im Grunde ein dateiähnliches Objekt mit unveränderlichen Rohdaten.
3.  Du erzeugst mit `URL.createObjectURL()` eine temporäre, lokale URL, die auf diesen Blob im Speicher des Browsers verweist. Diese URL sieht typischerweise so aus: `blob:http://...`.
4.  Du setzt diese Blob-URL als `href`-Attribut eines `<a>`-Elements.
5.  Du fügst das `download`-Attribut mit dem gewünschten Dateinamen hinzu.

Hier ist ein konkretes Beispiel, das einen einfachen Text-Download erzeugt:

```html
<a id="downloadLink" href="#" download="meine-notiz.txt">Notiz herunterladen</a>

<script>
  // Der Inhalt, der in die Datei geschrieben werden soll
  const textInhalt = "Hallo Welt! Dies ist eine dynamisch erzeugte Textdatei.";

  // 1. & 2. Erstelle einen Blob aus dem Text
  const textBlob = new Blob([textInhalt], { type: 'text/plain' });

  // 3. Erzeuge eine temporäre URL für den Blob
  const downloadUrl = URL.createObjectURL(textBlob);

  // 4. & 5. Weise die URL und den Dateinamen dem Link zu
  const linkElement = document.getElementById('downloadLink');
  linkElement.href = downloadUrl;

  // Optional: Aufräumen, nachdem der Link nicht mehr gebraucht wird
  // URL.revokeObjectURL(downloadUrl);
</script>
```

Wenn ein Nutzer nun auf den Link "Notiz herunterladen" klickt, wird eine Datei mit dem Namen `meine-notiz.txt` und dem Inhalt "Hallo Welt! ..." heruntergeladen. Das alles geschieht, ohne dass eine einzige Anfrage an einen Server gesendet wird. Die Datei wird vollständig im Client, also im Browser des Nutzers, erstellt.

Diese Technik ist unglaublich vielseitig. Du kannst damit CSV-Dateien aus Tabellendaten generieren, den Inhalt eines `<canvas>`-Elements als PNG-Bild speichern oder Konfigurationsdaten als JSON-Datei exportieren. Das `download`-Attribut ist der entscheidende Schlüssel, der es dem Browser ermöglicht, diese im Speicher erzeugten Daten als eine greifbare Datei zu behandeln.
