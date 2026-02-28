# Untertitel und Captions (track)

### Mehr als nur Ton: Untertitel und Captions mit dem `<track>`-Element

Wenn du ein Video oder eine Audiodatei in deine Webseite einbettest, ist der sicht- oder hörbare Inhalt nur die halbe Miete. Ein wirklich inklusives und professionelles Web-Erlebnis berücksichtigt alle Nutzerinnen und Nutzer – auch jene, die den Ton nicht hören können oder wollen, eine andere Sprache sprechen oder einfach nur den Inhalt besser verstehen möchten. Genau hier kommt das `<track>`-Element ins Spiel. Es ist ein unauffälliger, aber unglaublich mächtiger Helfer, um deine Medieninhalte für alle zugänglich und verständlicher zu machen.

#### Warum textbasierte Spuren so wichtig sind

Bevor wir in den Code eintauchen, lass uns kurz innehalten und verstehen, warum dieses Thema so relevant ist. Stell dir folgende Szenarien vor:

1.  **Barrierefreiheit:** Jemand mit einer Hörbehinderung besucht deine Seite. Ohne Untertitel oder Transkripte ist dein Video für diese Person wertlos.
2.  **Laute oder leise Umgebungen:** Ein Nutzer sitzt in einer lauten U-Bahn oder in einer stillen Bibliothek. In beiden Fällen ist es praktischer, den Ton stummzuschalten und stattdessen Untertitel zu lesen.
3.  **Internationale Zielgruppen:** Dein Video ist auf Deutsch, aber du möchtest auch ein englisches oder spanisches Publikum erreichen. Übersetzte Untertitel sind hier die Lösung.
4.  **Verständlichkeit und SEO:** Manchmal sind Sprecher schwer zu verstehen oder es werden Fachbegriffe verwendet. Mitlesbare Texte helfen beim Verständnis. Außerdem können Suchmaschinen Textinhalte viel besser indizieren als reine Audio- oder Videodaten. Das verbessert dein Ranking.

Du siehst, textbasierte Spuren sind kein Nischen-Feature, sondern ein zentraler Baustein für eine moderne und nutzerfreundliche Webseite.

#### Das `<track>`-Element im Einsatz

Das `<track>`-Element ist ein Kind-Element von `<audio>` oder `<video>`. Es wird also direkt innerhalb dieser Tags platziert und verlinkt auf eine externe Datei, die die Zeit- und Textinformationen enthält.

Schauen wir uns eine grundlegende Struktur an:

```html
<video controls poster="poster-bild.jpg" width="640" height="360">
  <source src="mein-video.mp4" type="video/mp4">
  <source src="mein-video.webm" type="video/webm">
  
  <!-- Hier kommt unsere Textspur für deutsche Untertitel -->
  <track src="untertitel-de.vtt" kind="subtitles" srclang="de" label="Deutsch">
  
  <!-- Ein Fallback-Text für sehr alte Browser -->
  Dein Browser unterstützt das Video-Tag nicht.
</video>
```

Auf den ersten Blick sieht das einfach aus, aber die Magie steckt in den Attributen des `<track>`-Elements. Lass uns diese im Detail durchgehen.

*   `src`: Dieses Attribut ist das wichtigste. Es enthält den Pfad zur Textdatei. Das gängigste Format hierfür ist WebVTT (`.vtt`), das wir uns gleich genauer ansehen werden.
*   `kind`: Hier legst du die Art der Textspur fest. Dies ist entscheidend für das Verhalten des Browsers und die Benutzererfahrung. Es gibt fünf mögliche Werte:
    *   `subtitles`: Das sind Untertitel im klassischen Sinne. Sie dienen der Übersetzung des gesprochenen Inhalts in eine andere Sprache. Wenn der Nutzer die Audiosprache nicht versteht, sind `subtitles` die richtige Wahl.
    *   `captions`: Auf Deutsch oft als "erweiterte Untertitel" bezeichnet. Sie sind für Gehörlose oder Schwerhörige gedacht. Sie transkribieren nicht nur den Dialog, sondern beschreiben auch wichtige Geräusche, die zum Verständnis der Szene beitragen, wie z.B. "[Tür knarrt]", "[Handy klingelt]" oder "[sanfte Musik spielt]".
    *   `descriptions`: Dies ist für sehbehinderte Nutzer gedacht. Die Textdatei enthält eine Beschreibung dessen, was im Video visuell passiert. Ein Screenreader liest diesen Text dann zur passenden Zeit vor. Die Spur ist also nicht sichtbar, sondern hörbar.
    *   `chapters`: Hiermit kannst du Kapitelmarken für dein Video definieren. Der Nutzer kann dann schnell zu bestimmten Abschnitten des Videos springen, was besonders bei langen Inhalten wie Tutorials oder Vorträgen hilfreich ist.
    *   `metadata`: Dieser Typ ist für maschinenlesbare Daten gedacht, die von JavaScript verarbeitet werden können. Sie sind für den Endnutzer nicht direkt sichtbar und dienen fortgeschrittenen, interaktiven Anwendungen.
*   `srclang`: Dieses Attribut gibt die Sprache der Textspur an, z.B. `de` für Deutsch, `en` für Englisch oder `es` für Spanisch. Es ist zwingend erforderlich, wenn `kind="subtitles"` gesetzt ist.
*   `label`: Dies ist der Text, der dem Nutzer im Menü des Videoplayers zur Auswahl der Spur angezeigt wird, z.B. "Deutsch (Untertitel)" oder "English Captions". Ohne dieses Attribut zeigt der Browser oft nur die Sprache an, was weniger aussagekräftig sein kann.
*   `default`: Wenn du dieses boolesche Attribut setzt, wird diese Spur standardmäßig aktiviert, sobald das Video lädt (vorausgesetzt, die Browsereinstellungen des Nutzers erlauben dies). Du solltest es nur für eine Spur pro Video verwenden.

Du kannst übrigens problemlos mehrere `<track>`-Elemente für ein einziges Video bereitstellen, um verschiedene Sprachen oder Arten von Spuren anzubieten:

```html
<video controls width="640" height="360">
  <source src="tutorial.mp4" type="video/mp4">
  
  <!-- Deutsche Captions für Hörgeschädigte, standardmäßig aktiviert -->
  <track src="captions-de.vtt" kind="captions" srclang="de" label="Deutsch (für Hörgeschädigte)" default>
  
  <!-- Englische Untertitel zur Übersetzung -->
  <track src="subtitles-en.vtt" kind="subtitles" srclang="en" label="English">
  
  <!-- Französische Untertitel zur Übersetzung -->
  <track src="subtitles-fr.vtt" kind="subtitles" srclang="fr" label="Français">

  <!-- Kapitel zur Navigation -->
  <track src="kapitel.vtt" kind="chapters" srclang="de" label="Kapitel">

</video>
```

#### Das Herzstück: Das WebVTT-Dateiformat

Das `<track>`-Element ist nur der Verweis. Der eigentliche Inhalt liegt in der `.vtt`-Datei. Das WebVTT-Format (Web Video Text Tracks) ist ein einfacher Textstandard, der speziell für diesen Zweck entwickelt wurde. Eine VTT-Datei ist leicht zu erstellen und zu lesen.

Eine typische `.vtt`-Datei hat folgenden Aufbau:

```vtt
WEBVTT

1
00:00:02.500 --> 00:00:05.000
Hallo Welt, dies ist mein erstes Video.

2
00:00:06.100 --> 00:00:09.800
Hier zeige ich dir, wie das <track>-Element in HTML funktioniert.

NOTE Dies ist ein Kommentar und wird nicht angezeigt.

3
00:00:11.000 --> 00:00:14.500
[leise Hintergrundmusik]
Es ist wirklich ziemlich einfach, oder?

```

Lass uns diese Struktur aufschlüsseln:

1.  **Signatur:** Jede VTT-Datei muss zwingend mit `WEBVTT` in der ersten Zeile beginnen. Darauf kann eine Leerzeile folgen.
2.  **Cues:** Der Rest der Datei besteht aus "Cues" (dt. Einsätze). Jeder Cue repräsentiert einen Textblock, der für eine bestimmte Zeitspanne angezeigt wird.
    *   **Kennung (optional):** Eine Zeile mit einer eindeutigen ID wie `1`, `2` oder `intro-text`. Sie ist nicht zwingend erforderlich, hilft aber bei der Organisation.
    *   **Zeitstempel:** Dies ist der wichtigste Teil. Das Format ist `HH:MM:SS.mmm --> HH:MM:SS.mmm` (Stunden:Minuten:Sekunden.Millisekunden). Der erste Zeitstempel gibt an, wann der Text eingeblendet, der zweite, wann er ausgeblendet wird.
    *   **Textinhalt:** Der eigentliche Text, der angezeigt werden soll. Er kann sich über eine oder mehrere Zeilen erstrecken.
    *   **Kommentare:** Zeilen, die mit `NOTE` beginnen, werden vom Browser ignoriert und dienen nur als Notizen für dich.

#### Mehr als nur Text: Styling und Positionierung in VTT

WebVTT kann sogar noch mehr. Du kannst grundlegende Formatierungen und Positionierungen direkt in der `.vtt`-Datei vornehmen, um die Lesbarkeit zu verbessern oder zu verhindern, dass der Text wichtige Bildinhalte verdeckt.

**Textformatierung:**
Ähnlich wie in HTML kannst du einfache Tags verwenden:
*   `<b>Text</b>` für Fettdruck
*   `<i>Text</i>` für Kursivschrift
*   `<u>Text</u>` für unterstrichenen Text
*   `<v Sprechername>Text</v>` um anzuzeigen, wer gerade spricht. Dies ist besonders nützlich bei `captions`.

Beispiel:
```vtt
WEBVTT

00:00:20.150 --> 00:00:23.900
<v Anna>Bist du sicher, dass das eine <b>gute Idee</b> ist?</v>
<v Ben><i>Absolut</i> sicher!</v>
```

**Positionierung:**
Du kannst auch direkt am Zeitstempel Einstellungen für die Positionierung des Cues vornehmen. Dies ist nützlich, um Untertitel z. B. am oberen Bildschirmrand anzuzeigen, wenn unten bereits eine Texteinblendung im Video selbst vorhanden ist.

*   `line`: Gibt die vertikale Position an. Eine positive Zahl zählt von oben, eine negative von unten. `line:0` ist ganz oben, `line:-1` ist die erste Zeile von unten (Standard).
*   `position`: Gibt die horizontale Position des Textes an. `position:50%` ist die Mitte.
*   `align`: Legt die Ausrichtung des Textes fest (`start`, `middle`, `end`).

Beispiel:
```vtt
WEBVTT

00:00:30.000 --> 00:00:33.000 line:10% position:15% align:start
Dieser Text erscheint oben links im Video.

00:00:35.000 --> 00:00:38.000 line:-1 position:90% align:end
Und dieser Text erscheint unten rechts.
```

Durch die Kombination von `<track>` und dem flexiblen WebVTT-Format gibst du deinen Medieninhalten eine zusätzliche Ebene an Professionalität und Zugänglichkeit. Du ermöglichst es mehr Menschen, deine Inhalte zu konsumieren und zu verstehen – und das ist letztendlich das Ziel einer jeden guten Webseite.
