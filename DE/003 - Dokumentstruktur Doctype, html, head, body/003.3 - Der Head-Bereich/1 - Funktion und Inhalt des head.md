# Funktion und Inhalt des head

### Das Gehirn deiner Webseite: Funktion und Inhalt des `<head>`-Elements

Stell dir eine Webseite wie einen Menschen vor. Der `<body>`-Bereich, den wir später ausführlich behandeln, ist der sichtbare Körper – alles, was du auf der Seite siehst, liest und womit du interagierst. Der `<head>`-Bereich hingegen ist das Gehirn. Er ist für den Besucher nicht direkt sichtbar, aber er steuert entscheidende Hintergrundprozesse, speichert wichtige Informationen und gibt Anweisungen, wie der Körper (also der sichtbare Inhalt) dargestellt und verstanden werden soll.

In diesem Kapitel tauchen wir in dieses „Gehirn“ ein und entdecken, welche wichtigen Informationen und Befehle im `<head>`-Element deines HTML-Dokuments untergebracht sind. Jedes HTML-Dokument hat genau einen `<head>`, der direkt nach dem öffnenden `<html>`-Tag und vor dem `<body>`-Tag platziert wird. Er ist ein reiner Container für Metadaten – also Daten über Daten.

#### Das unverzichtbare Minimum: Zeichensatz und Titel

Auch wenn der `<head>`-Bereich sehr komplex werden kann, gibt es zwei Elemente, die du in absolut jedem deiner Projekte finden wirst und auch immer definieren solltest.

**1. Der Zeichensatz mit `<meta charset="...">`**

Computer verstehen im Grunde nur Zahlen. Damit sie Buchstaben, Satzzeichen und Symbole wie „ü“, „ß“ oder „€“ korrekt darstellen können, benötigen sie eine Art Übersetzungstabelle – den Zeichensatz. Das `<meta>`-Element ist ein vielseitiges Werkzeug für Metadaten, und seine wichtigste Aufgabe ist die Deklaration des Zeichensatzes.

```html
<head>
  <meta charset="UTF-8">
</head>
```

Die Angabe `charset="UTF-8"` teilt dem Browser mit, dass er den Text auf deiner Seite mit der UTF-8-Kodierung interpretieren soll. UTF-8 ist der universelle Standard im Web, da er nahezu alle Zeichen und Symbole aller Sprachen der Welt abbilden kann. Ohne diese Angabe könnte der Browser raten und im schlimmsten Fall Umlaute und Sonderzeichen als kryptische Zeichenfolgen (z. B. „f�r“ statt „für“) darstellen. Diese Zeile sollte daher immer ganz am Anfang deines `<head>`-Bereichs stehen, damit der Browser sofort weiß, wie er den nachfolgenden Inhalt lesen muss.

**2. Der Seitentitel mit `<title>`**

Das `<title>`-Element ist das einzige Element im `<head>`, dessen Inhalt für den Benutzer direkt sichtbar ist, wenn auch nicht auf der Seite selbst. Der hier definierte Text erscheint an drei prominenten Stellen:

*   **Im Browser-Tab:** Es ist der Text, den du ganz oben im Reiter deines Browsers siehst.
*   **In den Suchergebnissen:** Suchmaschinen wie Google nutzen den Titel als klickbare Überschrift für dein Suchergebnis.
*   **In Lesezeichen:** Wenn ein Benutzer deine Seite als Lesezeichen speichert, wird der Titel als Name für dieses Lesezeichen verwendet.

Ein guter Titel ist kurz, prägnant und beschreibt den Inhalt der Seite treffend. Er ist nicht nur für die Benutzerfreundlichkeit, sondern auch für die Suchmaschinenoptimierung (SEO) von entscheidender Bedeutung.

```html
<head>
  <meta charset="UTF-8">
  <title>Meine erste Webseite | Über mich</title>
</head>
```

#### Die Verbindung zur Außenwelt: `<link>`

Selten besteht eine Webseite nur aus einer einzigen HTML-Datei. Meistens benötigst du externe Ressourcen, um deine Seite zu gestalten oder mit zusätzlichen Funktionen auszustatten. Hier kommt das `<link>`-Element ins Spiel. Es stellt eine Verbindung zu externen Dateien her.

**Einbinden von CSS-Stylesheets**

Die häufigste Anwendung für `<link>` ist das Einbinden einer CSS-Datei. CSS (Cascading Style Sheets) ist die Sprache, mit der du das Aussehen deiner Webseite definierst – Farben, Schriftarten, Layout und vieles mehr.

```html
<link rel="stylesheet" href="css/style.css">
```

Schauen wir uns die Attribute genauer an:
*   `rel="stylesheet"`: Das `rel`-Attribut (von engl. *relationship*) beschreibt die Beziehung zwischen dem HTML-Dokument und der verlinkten Datei. `stylesheet` teilt dem Browser mit, dass es sich um eine Datei handelt, die Stilregeln für die aktuelle Seite enthält.
*   `href="css/style.css"`: Das `href`-Attribut (von engl. *hypertext reference*) gibt den Pfad zur Datei an. In diesem Beispiel liegt die CSS-Datei in einem Unterordner namens `css`.

**Einbinden eines Favicons**

Ein Favicon ist das kleine Symbol, das links neben dem Seitentitel im Browser-Tab erscheint. Es stärkt den Wiedererkennungswert deiner Seite.

```html
<link rel="icon" href="favicon.ico" type="image/x-icon">
```

Hier gibt das `rel`-Attribut an, dass es sich um ein `icon` handelt, und `href` verweist auf die Bilddatei. Das `type`-Attribut informiert den Browser über den Dateityp des Symbols.

#### Mehr Metadaten für Maschinen: `<meta>` im Detail

Wir haben das `<meta>`-Element bereits für den Zeichensatz kennengelernt, aber es kann noch viel mehr. Mithilfe der Attribute `name` und `content` kannst du eine Vielzahl von Metadaten bereitstellen, die vor allem von Suchmaschinen, Social-Media-Plattformen und anderen Web-Diensten ausgelesen werden.

**Der Viewport für responsive Designs**

Eine der wichtigsten `<meta>`-Angaben für moderne Webseiten ist die Konfiguration des Viewports. Der Viewport ist der für den Benutzer sichtbare Bereich einer Webseite auf dem Bildschirm. Diese Zeile ist unerlässlich, damit deine Webseite auf mobilen Geräten wie Smartphones und Tablets korrekt skaliert wird.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

*   `name="viewport"`: Gibt an, dass wir den Viewport konfigurieren.
*   `content="..."`: Enthält die eigentlichen Anweisungen.
    *   `width=device-width` setzt die Breite der Webseite auf die Breite des Geräts.
    *   `initial-scale=1.0` legt den anfänglichen Zoom-Faktor auf 100 % fest, sodass die Seite nicht verkleinert oder vergrößert startet.

Ohne diese Zeile würden mobile Browser versuchen, die gesamte Desktop-Version der Seite auf dem kleinen Bildschirm darzustellen, was zu winziger Schrift und einer schlechten Benutzererfahrung führt.

**Beschreibung für Suchmaschinen**

Möchtest du beeinflussen, welcher Beschreibungstext unter deinem Seitentitel in den Google-Suchergebnissen erscheint? Dafür gibt es das `description`-Meta-Tag.

```html
<meta name="description" content="Erfahre alles über die grundlegende Struktur eines HTML-Dokuments und die wichtige Rolle des head-Bereichs.">
```

Diese Beschreibung beeinflusst nicht direkt dein Ranking, aber eine gut formulierte Beschreibung kann die Klickrate (Click-Through-Rate) erheblich steigern, da sie den Suchenden einen klaren Anreiz gibt, dein Ergebnis anzuklicken.

**Weitere nützliche Meta-Tags**

Es gibt noch viele weitere Meta-Tags, von denen einige heute weniger relevant sind als früher.

*   `author`: Gibt den Autor der Seite an. ` <meta name="author" content="Max Mustermann"> `
*   `keywords`: Früher extrem wichtig für SEO, heute wird dieses Tag von großen Suchmaschinen weitgehend ignoriert. Es diente dazu, eine Liste von Schlüsselwörtern für den Seiteninhalt anzugeben.

#### Interaktivität und eingebettete Stile: `<script>` und `<style>`

Obwohl es die beste Praxis ist, JavaScript und CSS in externen Dateien zu halten und diese über `<link>` und `<script src="...">` zu verknüpfen, gibt es auch die Möglichkeit, Code direkt im `<head>` zu platzieren.

**JavaScript direkt einfügen mit `<script>`**

Mit dem `<script>`-Element kannst du JavaScript-Code ausführen. Meistens wird es verwendet, um eine externe JavaScript-Datei zu laden, was die bevorzugte Methode ist, da sie die Trennung von Inhalt (HTML), Präsentation (CSS) und Verhalten (JS) fördert.

```html
<!-- Bevorzugte Methode: Externe Datei laden -->
<script src="js/main.js" defer></script>
```

Das `defer`-Attribut ist hier eine wichtige Ergänzung. Es weist den Browser an, das HTML-Dokument zuerst vollständig zu analysieren, bevor er das Skript ausführt. Das verhindert, dass das Laden eines großen Skripts das Rendern der sichtbaren Seite blockiert, und sorgt für eine bessere Ladezeit.

Du könntest JavaScript auch direkt in den `<head>` schreiben, aber das wird nur für sehr kleine, seitenspezifische Skripte empfohlen.

```html
<!-- Weniger empfohlene Methode: Inline-Skript -->
<script>
  console.log("Diese Nachricht kommt direkt aus dem Head!");
</script>
```

**CSS direkt einfügen mit `<style>`**

Ähnlich wie bei JavaScript kannst du mit dem `<style>`-Element CSS-Regeln direkt in dein HTML-Dokument einbetten. Dies ist nützlich für kleine Anpassungen, die nur für eine einzige Seite gelten, oder zum schnellen Testen. Für das gesamte Design deiner Website solltest du jedoch immer externe Stylesheets verwenden, da sie leichter zu verwalten und wiederverwendbar sind.

```html
<style>
  body {
    font-family: sans-serif;
    line-height: 1.6;
  }
</style>
```

#### Ein vollständiges Beispiel

Lass uns all diese Elemente in einem gut strukturierten `<head>`-Bereich zusammenfassen. So könnte der „Kopf“ einer typischen Webseite aussehen:

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <!-- 1. Grundlegende Metadaten (immer zuerst) -->
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- 2. Titel (wichtig für SEO und Benutzer) -->
  <title>Der ultimative Guide zum HTML-Head</title>

  <!-- 3. Metadaten für SEO und Social Media -->
  <meta name="description" content="Ein umfassender Überblick über alle wichtigen Elemente im HTML-Head-Bereich.">
  <meta name="author" content="Dein Name">

  <!-- 4. Verknüpfung zu externen Ressourcen (CSS, Favicon, Fonts) -->
  <link rel="stylesheet" href="styles/main.css">
  <link rel="icon" href="favicon.ico" type="image/x-icon">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">

  <!-- 5. Eingebettete Stile (nur für spezifische, kleine Anpassungen) -->
  <style>
    /* Ein kleiner Stil, der nur für diese Seite gilt */
    .special-highlight {
      background-color: yellow;
    }
  </style>

  <!-- 6. JavaScript (am besten am Ende des Head oder Body mit defer) -->
  <script src="js/app.js" defer></script>
</head>
<body>
  <!-- Der sichtbare Inhalt deiner Seite kommt hier hin -->
</body>
</html>
```

Der `<head>` ist also weit mehr als nur ein notwendiger Teil des HTML-Grundgerüsts. Er ist die Kommandozentrale, die deinem Dokument eine Identität gibt, es mit der Außenwelt verbindet und sicherstellt, dass es auf allen Geräten und Plattformen korrekt funktioniert und gut aussieht. Ein sauberer und gut organisierter `<head>` ist das Fundament jeder professionellen Webseite.
