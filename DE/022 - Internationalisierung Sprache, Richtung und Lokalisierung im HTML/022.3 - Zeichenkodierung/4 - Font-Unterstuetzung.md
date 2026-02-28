# Font-Unterstützung

### Font-Unterstützung: Wenn Zeichen ein Gesicht bekommen

Nachdem wir die Zeichenkodierung verstanden haben, wissen wir, wie ein Browser einen Strom von Bytes in eine Folge von Zeichen umwandelt. Ein `U+0041` wird als der Buchstabe "A" interpretiert, und ein `U+8A9E` als das japanische Zeichen "語". Aber diese Interpretation ist nur die halbe Miete. Der Browser weiß nun, *welches* Zeichen er darstellen soll, aber noch nicht, *wie* es aussehen soll. An dieser Stelle kommt die Font-Unterstützung ins Spiel.

Ein Font (eine Schriftart) ist im Grunde eine Sammlung von grafischen Darstellungen für Zeichen, die sogenannten Glyphen. Für jedes Zeichen, das ein Font unterstützt, enthält er eine präzise gezeichnete Vektorgrafik. Wenn dein Browser also ein "A" rendern soll, sucht er im ausgewählten Font nach der Glyphe für "A" und zeichnet sie auf den Bildschirm.

Was aber passiert, wenn du eine Schriftart wie "Lobster" für deine Überschrift wählst und diese Überschrift den Text "Привет мир" (Russisch für "Hallo Welt") enthält? Die Schriftart "Lobster" wurde primär für das lateinische Alphabet entworfen und enthält wahrscheinlich keine Glyphen für kyrillische Zeichen. Das Ergebnis ist frustrierend und unschön: Der Browser kann die Zeichen nicht darstellen und greift auf ein Fallback-Symbol zurück. Oft siehst du dann ein leeres Rechteck (□), das liebevoll "Tofu" genannt wird, weil es wie ein kleiner Block Tofu aussieht. Manchmal erscheint auch ein Fragezeichen in einer Raute (�).

Dieses Problem zeigt, dass die richtige Zeichenkodierung allein nicht ausreicht. Du musst auch sicherstellen, dass die von dir gewählten Schriftarten die Zeichen deines Inhalts unterstützen.

#### Der klassische Ansatz – Die `font-family`-Kette

Die grundlegendste Methode, um mit fehlenden Glyphen umzugehen, ist die `font-family`-Eigenschaft in CSS. Du gibst hier nicht nur eine einzige Schriftart an, sondern eine priorisierte Liste, einen sogenannten "Font-Stack".

```css
body {
  font-family: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
}
```

Wenn der Browser nun ein Zeichen rendern muss, geht er diese Liste von links nach rechts durch:
1.  Er prüft: Ist die Schriftart "Open Sans" auf dem System des Nutzers installiert und enthält sie eine Glyphe für das benötigte Zeichen? Wenn ja, wird sie verwendet.
2.  Wenn nicht, prüft er "Helvetica Neue".
3.  Dann "Helvetica".
4.  Dann "Arial".
5.  Wenn keine dieser spezifischen Schriftarten das Zeichen enthält, greift der Browser auf die erste verfügbare generische `sans-serif`-Schriftart des Betriebssystems zurück.

Dieser Ansatz ist ein gutes Sicherheitsnetz für lateinische Alphabete, aber für eine globale Website ist er unzureichend. Du kannst dich nicht darauf verlassen, dass ein Nutzer in Japan eine Schriftart installiert hat, die auch kyrillische oder arabische Zeichen unterstützt, nur weil du sie in deine `font-family`-Kette aufnimmst. Die installierten Schriftarten variieren von Betriebssystem zu Betriebssystem und von Nutzer zu Nutzer.

#### Die Lösung für eine globale Welt – Web Fonts

Um eine konsistente und zuverlässige Darstellung deiner Texte auf allen Geräten und für alle Sprachen zu gewährleisten, sind Web Fonts die moderne und beste Lösung. Anstatt dich auf die lokal installierten Schriftarten des Nutzers zu verlassen, lieferst du die benötigten Font-Dateien einfach zusammen mit deiner Website aus. Der Browser des Nutzers lädt sie herunter und verwendet sie, um den Text zu rendern.

Die Einbindung erfolgt in CSS über die `@font-face`-Regel.

```css
@font-face {
  font-family: "MeineTolleSchrift";
  src: url("pfad/zu/meiner-schrift.woff2") format("woff2");
  font-weight: normal;
  font-style: normal;
}

body {
  font-family: "MeineTolleSchrift", sans-serif;
}
```

Mit `@font-face` definierst du eine neue Schriftfamilie für deine Website.
- `font-family`: Hier gibst du den Namen an, unter dem du die Schriftart später im CSS verwenden möchtest.
- `src`: Dies ist der wichtigste Teil. Hier verweist du auf die Font-Datei. Es ist Best Practice, das Format der Datei mit `format()` anzugeben.

**Font-Formate**

Es gibt verschiedene Formate für Web Fonts, aber für die moderne Webentwicklung sind vor allem zwei relevant:
- **WOFF2 (Web Open Font Format 2):** Dies ist das modernste und effizienteste Format. Es bietet die beste Kompression und sollte immer deine erste Wahl sein. Es wird von allen modernen Browsern unterstützt.
- **WOFF (Web Open Font Format):** Der Vorgänger von WOFF2. Es ist eine gute Fallback-Option für ältere Browser.

Andere Formate wie TTF (TrueType Font) oder OTF (OpenType Font) sind eher für die Desktop-Nutzung gedacht. Sie sind unkomprimiert und daher deutlich größer als WOFF/WOFF2. Du kannst sie aber als Fallback für sehr alte Browser einbinden.

Eine robuste `@font-face`-Regel für maximale Kompatibilität könnte so aussehen:

```css
@font-face {
  font-family: "Open Sans Regular";
  src: url("opensans-regular.woff2") format("woff2"),
       url("opensans-regular.woff") format("woff");
  font-weight: 400; /* 400 ist normal */
  font-style: normal;
  font-display: swap; /* Wichtige Performance-Eigenschaft */
}
```

Der Browser versucht, die erste Quelle (`.woff2`) zu laden. Nur wenn er dieses Format nicht versteht, geht er zur nächsten über.

Die Eigenschaft `font-display: swap;` ist eine wichtige Performance-Optimierung. Sie weist den Browser an, den Text sofort mit einer Fallback-Schriftart anzuzeigen und die Web Font auszutauschen (`swap`), sobald sie fertig geladen ist. Das verhindert, dass der Nutzer auf einen leeren Bildschirm starrt, während die Schriftart lädt.

#### Optimierung für Internationalisierung – `unicode-range`

Web Fonts sind mächtig, haben aber einen Nachteil: Jede Font-Datei, die du einbindest, muss heruntergeladen werden. Eine Schriftart, die Tausende von Zeichen für viele verschiedene Sprachen enthält (wie z.B. Google's Noto Sans), kann mehrere Megabyte groß sein. Es wäre eine massive Verschwendung von Bandbreite, eine komplette chinesische Schriftart für einen Nutzer zu laden, der nur eine englische Seite besucht.

Hier kommt die `@font-face`-Eigenschaft `unicode-range` ins Spiel. Sie ist das entscheidende Werkzeug für die Internationalisierung von Schriftarten. Mit ihr kannst du festlegen, für welchen Bereich von Unicode-Zeichen eine bestimmte Font-Datei zuständig ist.

Stell dir vor, deine Website ist hauptsächlich auf Deutsch, hat aber auch einige Abschnitte mit griechischen Zitaten. Anstatt eine riesige Font-Datei zu laden, die sowohl lateinische als auch griechische Glyphen enthält, kannst du zwei separate, kleinere Font-Dateien verwenden.

```css
/* 1. Schriftart nur für lateinische Grundzeichen */
@font-face {
  font-family: "MyWebAppFont";
  src: url("mywebapp-latin.woff2") format("woff2");
  font-weight: normal;
  font-style: normal;
  unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, 
                 U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, 
                 U+2212, U+2215, U+FEFF, U+FFFD;
}

/* 2. Schriftart nur für griechische Zeichen */
@font-face {
  font-family: "MyWebAppFont";
  src: url("mywebapp-greek.woff2") format("woff2");
  font-weight: normal;
  font-style: normal;
  unicode-range: U+0370-03FF;
}
```

Was hier passiert, ist genial:
- Beide `@font-face`-Regeln definieren dieselbe `font-family`: "MyWebAppFont".
- Der Browser parst nun den HTML-Inhalt.
- Wenn er nur Zeichen aus dem lateinischen Bereich findet (wie `U+0041` für "A"), lädt er **ausschließlich** die Datei `mywebapp-latin.woff2`.
- Sobald er auf der Seite auf ein griechisches Zeichen stößt (z.B. `U+03A3` für "Σ"), merkt er, dass dieses Zeichen im `unicode-range` der zweiten Regel liegt und lädt **zusätzlich** die Datei `mywebapp-greek.woff2` herunter.

Diese Technik wird "Font Subsetting" genannt. Du teilst eine große Schriftart in kleinere, sprachspezifische Teile auf. Ein Nutzer, der nur Deutsch liest, lädt nur wenige Kilobytes. Ein Nutzer, der eine Seite mit griechischen Zitaten aufruft, lädt die zweite, ebenfalls kleine Datei bei Bedarf nach. Das verbessert die Ladezeit deiner Seite dramatisch und ist ein Schlüsselelement für die Entwicklung performanter, internationaler Websites.

#### Praktische Umsetzung – Font-Dienste und Selbsthosting

Du musst diese Subset-Dateien nicht immer selbst erstellen. Es gibt zwei gängige Wege, Web Fonts zu nutzen:

1.  **Font-Dienste (z.B. Google Fonts, Adobe Fonts):** Dies ist der einfachste Weg. Diese Dienste übernehmen das Hosting und die Optimierung für dich. Wenn du eine Schriftart von Google Fonts einbindest, erhältst du einen `<link>`-Tag für deinen HTML-`<head>`.

    ```html
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    ```

    Das CSS, das von dieser URL geliefert wird, enthält bereits hochentwickelte `@font-face`-Regeln mit `unicode-range` für Dutzende von Sprachen. Google's Server erkennen, welche Zeichen vom Browser des Nutzers benötigt werden, und liefern oft dynamisch die kleinstmögliche Font-Datei.

2.  **Selbsthosting:** Hierbei lädst du die Font-Dateien (z.B. im WOFF2-Format) herunter und legst sie auf deinem eigenen Webserver ab. Du schreibst die `@font-face`-Regeln selbst in deine CSS-Datei. Dies gibt dir die volle Kontrolle, keine Abhängigkeit von Drittanbietern und ist oft aus Datenschutzgründen (DSGVO) in Europa die bevorzugte Methode. Tools wie `glyphhanger` oder der `google-webfonts-helper` können dir dabei helfen, Font-Dateien herunterzuladen und die passenden CSS-Regeln inklusive der `unicode-range`-Werte zu generieren.

Egal welchen Weg du wählst, das Prinzip bleibt dasselbe: Die Kombination aus Zeichenkodierung, die dem Browser sagt, *welches* Zeichen gemeint ist, und Web Fonts, die ihm sagen, *wie* es auszusehen hat, ist die Grundlage für eine typografisch reiche, konsistente und global funktionierende Website.
