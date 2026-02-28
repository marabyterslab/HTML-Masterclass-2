# Video und Audio nativ einbinden

### Video und Audio nativ einbinden

Erinnerst du dich an die Zeiten, als das Einbetten eines Videos auf einer Webseite ein kleines Abenteuer war? Du musstest dich mit externen Plugins wie Adobe Flash, Microsoft Silverlight oder Apple QuickTime herumschlagen. Jedes Plugin hatte seine eigenen Tücken, erforderte eine Installation beim Nutzer und war oft eine Quelle für Sicherheitslücken und Performance-Probleme. Für mobile Geräte war dieser Ansatz ein kompletter Albtraum und funktionierte meist gar nicht. Die Migration zu HTML5 hat diesen ganzen Plugin-Wirrwarr mit einem Schlag überflüssig gemacht.

Mit den neuen, nativen Elementen `<video>` und `<audio>` wurde die Einbindung von multimedialen Inhalten zu einem Kernbestandteil des Webs – einfach, standardisiert und ohne die Notwendigkeit externer Software.

#### Das `<video>`-Element: Bewegtbild direkt im Browser

Das Einbinden eines Videos ist heute erstaunlich unkompliziert. Im einfachsten Fall brauchst du nur das `<video>`-Tag und das `src`-Attribut, das auf deine Videodatei verweist.

```html
<video src="videos/mein-grossartiges-video.mp4"></video>
```

Wenn du diesen Code in deinem Browser öffnest, wirst du vermutlich erst einmal nur das erste Bild des Videos sehen – ein statisches Poster. Du kannst es nicht abspielen, die Lautstärke nicht regeln und nicht spulen. Das liegt daran, dass dem Browser die Anweisung fehlt, eine Steuerungsoberfläche anzuzeigen. Dafür gibt es das `controls`-Attribut. Es ist ein boolesches Attribut, was bedeutet, dass du es einfach nur hinschreiben musst, ohne einen Wert zuzuweisen.

```html
<video src="videos/mein-grossartiges-video.mp4" controls></video>
```

Jetzt zeigt der Browser seine standardmäßigen Steuerelemente an: einen Play/Pause-Button, einen Zeitstrahl, Lautstärkeregler und oft auch eine Option für den Vollbildmodus.

Die Größe des Videos kannst du mit den Attributen `width` und `height` festlegen. Es ist eine gute Praxis, diese Maße anzugeben, damit der Browser den benötigten Platz auf der Seite reservieren kann, noch bevor das Video geladen ist. Das verhindert ein unschönes "Springen" des Layouts, wenn das Video schließlich erscheint.

```html
<video src="videos/mein-grossartiges-video.mp4" width="640" height="360" controls></video>
```

##### Verschiedene Formate für verschiedene Browser: Das `<source>`-Element

Leider gibt es nicht das *eine* Videoformat, das von allen Browsern gleichermaßen unterstützt wird. Während MP4 (mit dem H.264-Codec) heute eine sehr breite Unterstützung genießt, gibt es auch offene Formate wie WebM (mit dem VP9-Codec) oder Ogg (mit dem Theora-Codec), die von einigen Browsern bevorzugt oder besser unterstützt werden.

Um sicherzustellen, dass dein Video überall abgespielt werden kann, solltest du es in mehreren Formaten bereitstellen. Anstatt das `src`-Attribut direkt im `<video>`-Tag zu verwenden, nutzt du dafür das `<source>`-Element. Du kannst mehrere `<source>`-Elemente innerhalb des `<video>`-Tags platzieren. Der Browser geht diese Liste von oben nach unten durch und verwendet die erste Videodatei, deren Format er versteht und abspielen kann.

Zusätzlich solltest du innerhalb des `<video>`-Tags einen Fallback-Text einfügen. Dieser Text wird nur von sehr alten Browsern angezeigt, die das `<video>`-Element überhaupt nicht kennen.

```html
<video width="640" height="360" controls>
  <source src="videos/mein-grossartiges-video.webm" type="video/webm">
  <source src="videos/mein-grossartiges-video.mp4" type="video/mp4">
  Dein Browser unterstützt das Video-Tag leider nicht.
  Hier ist ein <a href="videos/mein-grossartiges-video.mp4">Link zum Video</a>.
</video>
```

Das `type`-Attribut im `<source>`-Tag ist optional, aber sehr zu empfehlen. Es hilft dem Browser, schnell zu entscheiden, ob er ein Format unterstützt, ohne erst einen Teil der Datei herunterladen und analysieren zu müssen.

##### Nützliche Attribute für die Videosteuerung

Neben `controls`, `width` und `height` gibt es noch weitere Attribute, die dir mehr Kontrolle über das Verhalten des Videos geben:

*   **`autoplay`**: Startet das Video automatisch, sobald die Seite geladen ist. Aber Achtung: Die meisten modernen Browser blockieren Autoplay mit Ton, um die Nutzererfahrung zu schützen. Wenn du `autoplay` verwenden möchtest, musst du das Video meistens gleichzeitig stummschalten, indem du das `muted`-Attribut hinzufügst.
*   **`muted`**: Schaltet den Ton des Videos standardmäßig aus. Der Nutzer kann ihn über die Steuerelemente wieder aktivieren.
*   **`loop`**: Spielt das Video in einer Endlosschleife ab.
*   **`poster`**: Verweist auf ein Bild, das angezeigt wird, bevor das Video geladen oder abgespielt wird. Das ist ideal für ein ansprechendes Vorschaubild.
*   **`preload`**: Gibt dem Browser einen Hinweis, wie die Videodatei geladen werden soll. Mögliche Werte sind:
    *   `none`: Das Video wird erst geladen, wenn der Nutzer auf "Play" klickt. Das spart Bandbreite.
    *   `metadata`: Nur die Metadaten des Videos (z. B. Dauer, Dimensionen) werden vorgeladen.
    *   `auto`: Der Browser entscheidet selbst, ob er das gesamte Video im Voraus lädt. Dies ist oft die Standardeinstellung.

Hier ein Beispiel mit einigen dieser Attribute in Aktion:

```html
<video width="640" height="360" controls poster="images/video-poster.jpg" preload="metadata">
  <source src="videos/mein-grossartiges-video.webm" type="video/webm">
  <source src="videos/mein-grossartiges-video.mp4" type="video/mp4">
  Dein Browser unterstützt das Video-Tag leider nicht.
</video>
```

#### Das `<audio>`-Element: Klangwelten für deine Seite

Das Einbinden von Audio funktioniert nach genau demselben Prinzip wie bei Videos, ist aber naturgemäß etwas einfacher, da es keine visuellen Dimensionen wie Breite oder Höhe gibt. Das grundlegende Element ist `<audio>`.

Auch hier ist das `controls`-Attribut essenziell, damit der Nutzer die Wiedergabe steuern kann. Ohne `controls` wäre das Audio-Element auf der Seite unsichtbar und könnte nur über JavaScript gesteuert werden.

```html
<audio src="audio/podcast-episode-1.mp3" controls></audio>
```

Genau wie bei Videos gibt es auch bei Audioformaten Unterschiede in der Browserunterstützung. MP3 ist zwar sehr weit verbreitet, aber auch hier ist es eine gute Praxis, Alternativen wie Ogg oder WAV anzubieten, um eine maximale Kompatibilität zu gewährleisten. Das `<source>`-Element kommt wieder zum Einsatz:

```html
<audio controls>
  <source src="audio/podcast-episode-1.ogg" type="audio/ogg">
  <source src="audio/podcast-episode-1.mp3" type="audio/mpeg">
  Dein Browser unterstützt das Audio-Tag leider nicht.
  Du kannst die Audiodatei <a href="audio/podcast-episode-1.mp3">hier herunterladen</a>.
</audio>
```

Die Attribute `autoplay`, `loop`, `muted` und `preload` funktionieren exakt so wie beim `<video>`-Element und geben dir die gleiche Kontrolle über das Lade- und Wiedergabeverhalten.

#### Barrierefreiheit mit dem `<track>`-Element

Moderne Webentwicklung bedeutet auch, Inhalte für alle zugänglich zu machen. Für Video- und Audioinhalte ist das besonders wichtig. HTML5 bietet mit dem `<track>`-Element eine native Lösung, um zeitgesteuerte Textspuren wie Untertitel oder Bildbeschreibungen einzubinden.

Das `<track>`-Element wird innerhalb eines `<video>`- oder `<audio>`-Tags platziert und verweist auf eine Textdatei im WebVTT-Format (`.vtt`), die den Text und die zugehörigen Zeitstempel enthält.

Die wichtigsten Attribute für `<track>` sind:

*   **`kind`**: Definiert die Art der Textspur. Die häufigsten Werte sind:
    *   `subtitles`: Untertitel für Nutzer, die den Ton verstehen, aber eine Übersetzung in eine andere Sprache benötigen.
    *   `captions`: Bildunterschriften für Gehörlose oder Schwerhörige. Sie enthalten nicht nur den Dialog, sondern auch Beschreibungen wichtiger Geräusche (z. B. "[Tür knarrt]" oder "[dramatische Musik]").
    *   `descriptions`: Textbeschreibungen der visuellen Handlung für sehbehinderte Nutzer, die von einem Screenreader vorgelesen werden.
    *   `chapters`: Kapitelmarken zur Navigation innerhalb des Mediums.
    *   `metadata`: Für maschinenlesbare Daten, die von Skripten verwendet werden.
*   **`src`**: Der Pfad zur `.vtt`-Datei.
*   **`srclang`**: Der Sprachcode der Textspur (z. B. `en` für Englisch, `de` für Deutsch).
*   **`label`**: Der Titel der Spur, der dem Nutzer im Auswahlmenü der Steuerelemente angezeigt wird.
*   **`default`**: Wenn dieses boolesche Attribut gesetzt ist, wird die Spur standardmäßig aktiviert.

Hier ist ein Beispiel für ein Video mit deutschen und englischen Untertiteln:

```html
<video width="640" height="360" controls poster="images/video-poster.jpg">
  <source src="videos/mein-grossartiges-video.webm" type="video/webm">
  <source src="videos/mein-grossartiges-video.mp4" type="video/mp4">
  
  <!-- Untertitel-Spuren -->
  <track kind="subtitles" src="subtitles/video-de.vtt" srclang="de" label="Deutsch">
  <track kind="subtitles" src="subtitles/video-en.vtt" srclang="en" label="English" default>
  
  Dein Browser unterstützt das Video-Tag leider nicht.
</video>
```

Mit diesen nativen HTML5-Elementen hast du ein mächtiges und zugleich einfaches Werkzeugset an der Hand. Du kannst multimediale Inhalte performant, zugänglich und ohne Abhängigkeiten von Drittanbieter-Plugins in deine Webseiten integrieren – ein gewaltiger Fortschritt gegenüber dem alten, fragmentierten Web.
