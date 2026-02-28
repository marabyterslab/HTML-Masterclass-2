# Das video-Element

### Das `<video>`-Element: Bewegtbild im Web

Früher war das Einbinden von Videos in eine Webseite eine komplizierte Angelegenheit, die oft auf externe Plugins wie Adobe Flash angewiesen war. Diese Zeiten sind glücklicherweise vorbei. Mit der Einführung von HTML5 erhielten wir das native `<video>`-Element, das es uns ermöglicht, Videos direkt und ohne Umwege in unsere Webseiten zu integrieren. Es ist ein mächtiges Werkzeug, das dir die volle Kontrolle über die Darstellung und das Verhalten von Bewegtbildinhalten gibt.

#### Die einfachste Form eines Videos

Beginnen wir mit der grundlegendsten Implementierung. Um ein Video auf deiner Seite anzuzeigen, benötigst du lediglich das `<video>`-Tag und das `src`-Attribut, das auf deine Videodatei verweist.

```html
<video src="videos/mein-video.mp4"></video>
```

Wenn du diesen Code in deinem Browser öffnest, wirst du vermutlich erst einmal nur den ersten Frame des Videos als statisches Bild sehen – oder gar nichts, je nach Browser. Du kannst es nicht abspielen, anhalten oder die Lautstärke regeln. Es ist einfach nur da. Um das zu ändern, müssen wir dem Element mitteilen, dass es eine Benutzeroberfläche anzeigen soll.

Zusätzlich ist es eine bewährte Praxis, dem Video von vornherein eine feste Größe zuzuweisen. Das verhindert, dass die Seite beim Laden des Videos unschön „springt“, weil der Browser erst dann den benötigten Platz reserviert.

```html
<video src="videos/mein-video.mp4" width="640" height="360"></video>
```

#### Steuerelemente für den Benutzer

Damit deine Besucher das Video auch bedienen können, fügst du das boolesche Attribut `controls` hinzu. Boolesch bedeutet, dass das bloße Vorhandensein des Attributs es aktiviert. Du musst ihm keinen Wert zuweisen.

```html
<video src="videos/mein-video.mp4" width="640" height="360" controls></video>
```

Jetzt wird der Browser seine standardmäßigen Steuerelemente einblenden: einen Play/Pause-Button, einen Fortschrittsbalken, eine Zeitanzeige, einen Lautstärkeregler und oft auch eine Option für den Vollbildmodus. Das Aussehen dieser Steuerelemente unterscheidet sich von Browser zu Browser (Chrome, Firefox, Safari etc.), aber ihre Funktionalität ist immer die gleiche.

#### Autoplay, Stummschaltung und Endlosschleifen

Manchmal möchtest du, dass ein Video sofort startet, sobald die Seite geladen ist, zum Beispiel bei einem atmosphärischen Hintergrundvideo. Dafür gibt es das `autoplay`-Attribut.

```html
<video src="videos/hintergrund.mp4" width="1920" height="1080" autoplay></video>
```

Hier gibt es jedoch eine wichtige Einschränkung: Moderne Browser blockieren in der Regel das automatische Abspielen von Videos mit Ton, da dies von Nutzern als sehr störend empfunden wird. Die Regel lautet fast immer: `autoplay` funktioniert nur, wenn das Video stummgeschaltet ist. Um das zu erreichen, fügst du das `muted`-Attribut hinzu.

```html
<video src="videos/hintergrund.mp4" width="1920" height="1080" autoplay muted></video>
```

Wenn ein solches Hintergrundvideo nach dem Ende wieder von vorne beginnen soll, kommt das `loop`-Attribut ins Spiel. Es sorgt für eine nahtlose Endlosschleife.

```html
<video src="videos/hintergrund.mp4" width="1920" height="1080" autoplay muted loop></video>
```

#### Das Vorschaubild: Das `poster`-Attribut

Videos können eine Weile zum Laden brauchen. Während dieser Zeit zeigt der Browser oft einen schwarzen Kasten an, was nicht besonders ansprechend ist. Mit dem `poster`-Attribut kannst du ein Bild festlegen, das als Platzhalter angezeigt wird, bevor das Video geladen ist oder bevor der Nutzer auf „Play“ klickt.

```html
<video src="videos/produkt-demo.mp4" width="854" height="480" controls poster="images/produkt-vorschau.jpg"></video>
```

Das `poster`-Bild gibt dem Besucher sofort einen visuellen Kontext und verbessert die Ladeerfahrung erheblich.

#### Das Format-Dilemma: `<source>` für maximale Kompatibilität

Jetzt kommen wir zu einem der wichtigsten Aspekte bei der Arbeit mit Videos im Web: die Browserkompatibilität. Nicht jeder Browser unterstützt jedes Videoformat. Die drei gängigsten Formate sind:

1.  **MP4 (mit H.264-Codec):** Das mit Abstand am weitesten verbreitete und von fast allen modernen Browsern unterstützte Format. Es bietet eine gute Balance aus Qualität und Dateigröße. Wenn du dich für nur ein Format entscheiden müsstest, wäre es dieses.
2.  **WebM (mit VP8- oder VP9-Codec):** Ein offenes, von Google entwickeltes Format, das speziell für das Web optimiert ist. Es bietet oft eine bessere Kompression als MP4 bei vergleichbarer Qualität und wird von den meisten modernen Browsern (außer Safari auf älteren Systemen) unterstützt.
3.  **Ogg (mit Theora-Codec):** Ein weiteres offenes Format, das früher eine größere Rolle spielte, heute aber an Bedeutung verloren hat.

Um sicherzustellen, dass dein Video in so vielen Browsern wie möglich abgespielt werden kann, solltest du es in mehreren Formaten bereitstellen. Hier kommt das `<source>`-Element ins Spiel. Anstatt das `src`-Attribut direkt im `<video>`-Tag zu verwenden, verschachtelst du mehrere `<source>`-Elemente darin.

Der Browser liest die `<source>`-Tags von oben nach unten und verwendet die erste Datei, deren Format er versteht und abspielen kann.

```html
<video width="640" height="360" controls poster="images/vorschau.jpg">
  <source src="videos/mein-video.webm" type="video/webm">
  <source src="videos/mein-video.mp4" type="video/mp4">
  Dein Browser unterstützt das video-Element leider nicht.
</video>
```

In diesem Beispiel versucht der Browser zuerst, die WebM-Datei zu laden. Kann er das nicht (weil er z. B. ein älterer Safari ist), ignoriert er diese Zeile und versucht es mit der nächsten: der MP4-Datei. Diese wird von fast allen Browsern unterstützt. Das `type`-Attribut hilft dem Browser, schnell zu entscheiden, ob er das Format unterstützt, ohne die Datei erst herunterladen und analysieren zu müssen.

Der Text, den du zwischen das öffnende `<video>`- und das schließende `</video>`-Tag schreibst, dient als **Fallback-Inhalt**. Er wird nur dann angezeigt, wenn der Browser des Besuchers das `<video>`-Element überhaupt nicht kennt, was heute nur noch auf sehr alten Systemen der Fall ist.

#### Barrierefreiheit: Untertitel und Bildbeschreibungen mit `<track>`

Ein professionelles und zugängliches Webangebot stellt sicher, dass Inhalte für alle Menschen konsumierbar sind – auch für solche mit Hör- oder Seheinschränkungen. Das `<track>`-Element ermöglicht es dir, zeitbasierte Textspuren zu deinem Video hinzuzufügen.

Die häufigsten Anwendungsfälle sind:

*   **`subtitles`:** Übersetzungen des gesprochenen Textes für Zuschauer, die eine andere Sprache sprechen.
*   **`captions`:** Transkriptionen des Dialogs und wichtiger Geräusche (z. B. „[Tür knallt]“ oder „[dramatische Musik]“) für gehörlose oder schwerhörige Zuschauer.
*   **`descriptions`:** Audiobeschreibungen einer Szene für sehbehinderte Zuschauer.
*   **`chapters`:** Kapitelmarken, um die Navigation in langen Videos zu erleichtern.

Diese Textspuren werden im WebVTT-Format (`.vtt`) erstellt, einer einfachen Textdatei, die Zeitstempel und den zugehörigen Text enthält.

So bindest du eine Untertitelspur ein:

```html
<video width="640" height="360" controls>
  <source src="videos/tutorial.mp4" type="video/mp4">
  <track 
    kind="captions" 
    srclang="de" 
    src="subtitles/tutorial-de.vtt" 
    label="Deutsch"
    default>
  <track 
    kind="subtitles" 
    srclang="en" 
    src="subtitles/tutorial-en.vtt" 
    label="English">
</video>
```

*   **`kind`**: Gibt die Art der Textspur an.
*   **`srclang`**: Der Sprachcode (z. B. `de` für Deutsch, `en` für Englisch).
*   **`src`**: Der Pfad zur `.vtt`-Datei.
*   **`label`**: Der Name der Spur, der dem Benutzer in der Auswahl angezeigt wird.
*   **`default`**: Dieses Attribut gibt an, dass diese Spur standardmäßig aktiviert sein soll.

#### Videos responsiv gestalten

Feste Breiten- und Höhenangaben sind in der Welt des responsiven Webdesigns ein Problem. Ein Video mit `width="640"` wird auf einem Smartphone-Display über den Rand hinausragen. Die Lösung ist einfach und wird mit CSS umgesetzt.

Wir entfernen die `width`- und `height`-Attribute aus dem HTML und steuern die Größe stattdessen über CSS.

**HTML:**

```html
<video class="responsive-video" controls>
  <source src="videos/mein-video.mp4" type="video/mp4">
</video>
```

**CSS:**

```css
.responsive-video {
  width: 100%;
  height: auto;
}
```

Mit `width: 100%` passt sich das Video immer an die volle Breite seines Elternelements an (z. B. eines `<div>` oder des `<body>`). `height: auto` ist der entscheidende Teil: Der Browser passt die Höhe automatisch an, um das ursprüngliche Seitenverhältnis des Videos beizubehalten. Dadurch wird das Video nicht verzerrt oder gestreckt. Es skaliert perfekt auf jeder Bildschirmgröße.

Das `<video>`-Element ist ein Paradebeispiel für die Stärke von modernem HTML. Es bietet eine robuste, native und zugängliche Möglichkeit, eines der fesselndsten Medienformate direkt in deine Webseiten zu integrieren und gibt dir alle Werkzeuge an die Hand, um ein großartiges Benutzererlebnis zu schaffen.
