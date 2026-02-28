# Codecs und Formate

### Codecs und Formate: Das Herzstück digitaler Medien

Wenn du ein Video auf einer Webseite einbindest, gibst du im HTML-Code einfach den Pfad zu einer Datei an, zum Beispiel `video.mp4`. Doch was verbirgt sich wirklich hinter dieser einen Datei? Warum ist ein fünfminütiges Video manchmal nur 50 Megabyte groß, während eine unkomprimierte Aufnahme derselben Länge mehrere Gigabyte belegen würde? Die Antwort liegt in der cleveren Zusammenarbeit von zwei Konzepten, die oft verwechselt, aber entscheidend für das moderne Web sind: Codecs und Container-Formate.

Um zu verstehen, warum wir beides brauchen, stell dir das Problem vor: Ein einzelnes Bild eines Videos in Full-HD-Auflösung (1920x1080 Pixel) hat über zwei Millionen Pixel. Jeder Pixel benötigt drei Farbwerte (Rot, Grün, Blau). Wenn wir für jeden Farbwert ein Byte (8 Bit) ansetzen, sind das bereits rund 6 Megabyte für ein einziges Bild. Bei einem Video mit 30 Bildern pro Sekunde wären das 180 Megabyte – pro Sekunde! Ein einminütiges Video käme so auf über 10 Gigabyte. Das über das Internet zu streamen, wäre für die meisten Nutzer undenkbar.

Hier kommen die Magier der Datenreduktion ins Spiel: die Codecs.

#### Der Codec: Der Algorithmus, der komprimiert

Das Wort „Codec“ ist eine Abkürzung für **Co**der-**Dec**oder. Ein Codec ist also kein Dateityp, sondern ein Algorithmus – eine Reihe von Regeln und mathematischen Verfahren, die dazu dienen, Daten zu komprimieren (kodieren) und sie später wieder für die Wiedergabe zu dekomprimieren (dekodieren). Dein Browser nutzt den Decoder-Teil, um aus dem komprimierten Datenstrom wieder ein sichtbares Bild und hörbaren Ton zu machen.

Man unterscheidet grundsätzlich zwischen zwei Arten der Kompression:

1.  **Verlustbehaftete Kompression (Lossy):** Diese Methode ist die bei weitem gebräuchlichste für Web-Videos und -Audio. Die Idee dahinter ist clever und basiert auf der menschlichen Wahrnehmung. Der Algorithmus entfernt Informationen, die für das menschliche Auge oder Ohr schwer oder gar nicht wahrnehmbar sind. Bei einem Video könnten das feine Farbabstufungen in einem sich schnell bewegenden Bereich sein oder Bilddetails, die in aufeinanderfolgenden Frames nahezu identisch sind. Anstatt jedes Bild komplett neu zu speichern, speichert der Codec nur die Unterschiede zum vorherigen Bild. Das Ergebnis ist eine dramatische Reduzierung der Dateigröße, wobei die wahrgenommene Qualität oft erstaunlich hoch bleibt.
    *   **Bekannte Video-Codecs:** H.264 (auch AVC), H.265 (HEVC), VP9, AV1.
    *   **Bekannte Audio-Codecs:** AAC, MP3, Opus, Vorbis.

2.  **Verlustfreie Kompression (Lossless):** Hierbei werden Daten so komprimiert, dass sie nach der Dekomprimierung wieder zu 100 % dem Original entsprechen. Es geht kein einziges Bit an Information verloren. Dies funktioniert ähnlich wie bei einer ZIP-Datei: Wiederkehrende Muster in den Daten werden durch kürzere Platzhalter ersetzt. Die Dateigröße wird zwar reduziert, aber bei weitem nicht so stark wie bei der verlustbehafteten Kompression. Für professionelle Archivierung ist das ideal, für das Streaming im Web jedoch meist unpraktikabel.
    *   **Bekannte Audio-Codecs:** FLAC, ALAC.

Die Wahl des Codecs ist also immer ein Kompromiss zwischen Dateigröße, Qualität und der für die De- und Kodierung benötigten Rechenleistung.

#### Das Container-Format: Die Box für alles

Wenn der Codec die Sprache ist, in der Bild und Ton „geschrieben“ sind, dann ist das Container-Format das Buch, in dem diese Sprache abgedruckt wird. Ein Container ist die eigentliche Datei, die du auf deiner Festplatte siehst (z. B. mit der Endung `.mp4`, `.webm` oder `.mov`).

Seine Aufgabe ist es, die verschiedenen Datenströme – die komprimierte Videospur, eine oder mehrere Audiospuren, eventuell Untertitel – zu bündeln und mit wichtigen Metadaten zu versehen. Diese Metadaten sind essenziell, denn sie sagen dem Abspielprogramm, wie alles zusammengehört. Sie enthalten Informationen wie:

*   Welcher Video-Codec wurde verwendet?
*   Welcher Audio-Codec wurde verwendet?
*   Wie hoch ist die Bildrate (Frames pro Sekunde)?
*   Wie ist die Auflösung des Videos?
*   Synchronisationsdaten, damit Ton und Bild exakt zur selben Zeit abgespielt werden.

Ein Container-Format legt also nicht die Qualität des Inhalts fest, sondern nur, wie dieser Inhalt verpackt ist. Du kannst dir das so vorstellen: Ein und derselbe Text (die Daten) kann als Taschenbuch, als Hardcover oder als E-Book (die Container) veröffentlicht werden. Der Inhalt bleibt gleich, aber die Verpackung ist anders.

Genauso kann eine `.mp4`-Datei ein Video enthalten, das mit dem H.264-Codec kodiert wurde, aber theoretisch auch eines, das den neueren H.265-Codec nutzt. Die Dateiendung allein verrät uns also nur die Art der Verpackung, nicht den exakten Inhalt.

#### Die wichtigsten Formate und Codecs für das Web

Im Web haben sich über die Jahre einige Kombinationen aus Containern und Codecs als De-facto-Standards durchgesetzt. Der Grund dafür ist die Browser-Kompatibilität. Nicht jeder Browser unterstützt jeden Container und jeden Codec.

*   **MP4 (.mp4):** Der unangefochtene König der Kompatibilität. Das MP4-Format wird von praktisch allen modernen Browsern und Geräten unterstützt. Es verwendet in der Regel den **H.264**-Video-Codec und den **AAC**-Audio-Codec. Diese Kombination ist hocheffizient und bietet eine exzellente Balance aus Qualität und Dateigröße. H.264 ist allerdings patentrechtlich geschützt, was in der Open-Source-Community immer wieder zu Diskussionen führt.

*   **WebM (.webm):** Das offene und lizenzkostenfreie Gegenstück zu MP4. WebM wurde von Google entwickelt und wird von Browsern wie Chrome, Firefox und Opera nativ unterstützt. Es verwendet die Video-Codecs **VP8** oder dessen Nachfolger **VP9** (und zunehmend **AV1**) sowie die Audio-Codecs **Vorbis** oder **Opus**. WebM bietet oft eine noch bessere Kompression als MP4 bei vergleichbarer Qualität, vor allem mit dem VP9-Codec.

*   **Ogg (.ogg, .ogv):** Ein weiteres offenes Container-Format, das vor allem in den frühen Tagen von HTML5 eine wichtige Rolle spielte. Es wird hauptsächlich mit dem **Theora**-Video-Codec und dem **Vorbis**-Audio-Codec in Verbindung gebracht. Heute hat es im Videobereich gegenüber WebM an Bedeutung verloren, wird aber weiterhin für Audio verwendet (oft mit dem modernen Opus-Codec).

#### Praktische Anwendung in HTML5

Was bedeutet all dieses Wissen nun für deine tägliche Arbeit mit HTML? Es bedeutet, dass du nicht einfach eine einzige Videodatei bereitstellen und hoffen kannst, dass sie überall funktioniert. Um maximale Kompatibilität zu gewährleisten, solltest du dein Video in mindestens zwei verschiedenen Formaten anbieten. Das `<video>`-Element in HTML5 ist genau dafür ausgelegt.

Mithilfe des `<source>`-Elements kannst du dem Browser mehrere Quellen zur Auswahl stellen. Der Browser prüft dann von oben nach unten, welche Datei er abspielen kann, und wählt die erste passende aus.

```html
<video controls width="640" height="360">
  <!-- 
    Die erste Wahl für moderne Browser wie Chrome und Firefox.
    WebM bietet oft die beste Qualität bei kleiner Dateigröße.
  -->
  <source src="mein-video.webm" type="video/webm">

  <!-- 
    Das Fallback für Browser wie Safari oder ältere Geräte,
    die WebM nicht unterstützen. MP4 ist quasi universell.
  -->
  <source src="mein-video.mp4" type="video/mp4">

  <!-- 
    Dieser Text wird nur angezeigt, wenn der Browser das <video>-Tag
    überhaupt nicht versteht.
  -->
  Dein Browser unterstützt die Wiedergabe von Videos leider nicht.
</video>
```

In diesem Beispiel versucht der Browser zuerst, die `mein-video.webm`-Datei zu laden. Kann er mit dem WebM-Container und den darin enthaltenen Codecs (z. B. VP9 und Opus) umgehen, wird diese Datei abgespielt. Schlägt das fehl – wie zum Beispiel in Apples Safari-Browser, der lange Zeit keine Unterstützung für VP9 bot –, geht er zur nächsten `<source>` über und versucht es mit der `mein-video.mp4`-Datei. Da diese Kombination (MP4-Container mit H.264/AAC-Codecs) so gut wie überall unterstützt wird, dient sie als sicheres Fallback.

Das `type`-Attribut ist dabei eine wichtige Hilfe für den Browser. Es teilt ihm den MIME-Typ der Datei mit, der oft auch Informationen über die verwendeten Codecs enthält (z. B. `type='video/mp4; codecs="avc1.42E01E, mp4a.40.2"'`). Dadurch kann der Browser oft schon vor dem Herunterladen der Datei entscheiden, ob er sie abspielen kann, was Zeit und Bandbreite spart.

Das Zusammenspiel von Codecs und Containern mag auf den ersten Blick komplex erscheinen. Doch das Verständnis dieser Grundlagen ist der Schlüssel, um Medien im Web performant, qualitativ hochwertig und für alle Nutzer zugänglich zu machen. Du triffst damit bewusste Entscheidungen, statt nur auf eine funktionierende Dateiendung zu hoffen.
