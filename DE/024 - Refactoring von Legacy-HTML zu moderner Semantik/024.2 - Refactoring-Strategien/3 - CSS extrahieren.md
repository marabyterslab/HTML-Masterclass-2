# CSS extrahieren

### CSS extrahieren: Die Trennung von Stil und Struktur

Wenn du ein älteres Webprojekt übernimmst oder deinen eigenen, vor Jahren geschriebenen Code refaktorierst, wirst du unweigerlich auf ein Phänomen stoßen, das heute als eine der größten Sünden der Webentwicklung gilt: die Vermischung von HTML-Struktur und CSS-Styling. In den frühen Tagen des Webs war dies gang und gäbe, doch moderne Webstandards predigen eine strikte **Trennung der Belange** (Separation of Concerns). Dein HTML-Dokument sollte ausschließlich die Struktur und Bedeutung deines Inhalts beschreiben – was ist eine Überschrift, was ein Absatz, was eine Liste? Das Aussehen, also Farben, Schriftarten, Abstände und Layout, gehört ausschließlich in eine separate CSS-Datei.

Das Extrahieren von CSS ist daher einer der ersten und wichtigsten Schritte beim Refactoring von Legacy-HTML. Es macht deinen Code nicht nur sauberer und lesbarer, sondern auch dramatisch einfacher zu warten, wiederverwendbar und performanter. Betrachten wir die drei Hauptschauplätze, an denen du auf vermischten Code treffen wirst, und wie du ihn Schritt für Schritt bereinigst.

#### 1. Inline-Styles: Der direkte Weg ins Chaos

Inline-Styles sind CSS-Regeln, die direkt im `style`-Attribut eines HTML-Elements notiert werden. Sie sind der hartnäckigste und problematischste Fall, da sie eine extrem hohe Spezifität haben und jede externe CSS-Regel überschreiben können.

**Vorher: Das Problem**

Stell dir vor, du findest folgenden HTML-Code in einem alten Projekt:

```html
<div style="background-color: #f2f2f2; border: 1px solid #cccccc; padding: 15px; margin-bottom: 20px;">
  <h2 style="color: #333; font-family: Arial, sans-serif; border-bottom: 2px solid #a0a0a0;">
    Wichtige Ankündigung
  </h2>
  <p style="font-size: 14px; line-height: 1.6; color: #555;">
    Dies ist eine wichtige Information für alle Benutzer unserer Plattform. Bitte lies sie sorgfältig durch.
  </p>
  <a href="/details" style="background-color: #007bff; color: white; padding: 10px 15px; text-decoration: none; border-radius: 5px;">
    Mehr erfahren
  </a>
</div>
```

Auf den ersten Blick mag dieser Code funktionieren – er erzeugt eine visuell gestaltete Box. Doch die Probleme liegen auf der Hand:

*   **Wiederholung:** Wenn du eine zweite, identisch aussehende Box auf der Seite oder auf einer anderen Seite brauchst, musst du diesen gesamten Wust an CSS-Regeln kopieren und einfügen.
*   **Wartbarkeit:** Stell dir vor, der Kunde möchte die Hintergrundfarbe aller dieser Boxen von grau auf ein helles Blau ändern. Du müsstest jede einzelne Instanz im gesamten Projekt manuell suchen und ersetzen. Ein Albtraum.
*   **Lesbarkeit:** Das HTML wird durch die langen `style`-Attribute unübersichtlich. Die eigentliche Struktur – ein `div` mit einer Überschrift, einem Absatz und einem Link – geht im visuellen Lärm unter.

**Nachher: Die Lösung durch Klassen**

Die Lösung besteht darin, die stilistischen Muster zu erkennen, ihnen semantische Namen in Form von CSS-Klassen zu geben und die Regeln in eine externe CSS-Datei auszulagern.

1.  **Analysiere die Komponenten:** Wir haben hier eine Benachrichtigungsbox, eine Überschrift innerhalb der Box und einen Button.
2.  **Vergib sinnvolle Klassennamen:** Nenne die Klassen nach ihrer Funktion, nicht nach ihrem Aussehen. Statt `.graue-box-mit-rand` nennst du sie `.notification-box` oder `.content-card`. Der Button könnte `.btn` oder `.btn-primary` heißen.
3.  **Erstelle die CSS-Regeln:** Lege eine neue Datei an, z. B. `styles.css`, und übertrage die Inline-Styles in die entsprechenden Klassen.

In deiner `styles.css` könnte das dann so aussehen:

```css
.notification-box {
  background-color: #f2f2f2;
  border: 1px solid #cccccc;
  padding: 15px;
  margin-bottom: 20px;
}

.notification-box .title {
  color: #333;
  font-family: Arial, sans-serif;
  border-bottom: 2px solid #a0a0a0;
}

.notification-box .text {
  font-size: 14px;
  line-height: 1.6;
  color: #555;
}

.btn-primary {
  background-color: #007bff;
  color: white;
  padding: 10px 15px;
  text-decoration: none;
  border-radius: 5px;
  display: inline-block; /* Wichtig für korrekte Darstellung von Padding */
}
```

4.  **Bereinige das HTML:** Ersetze die Inline-Styles durch die neuen Klassen.

```html
<div class="notification-box">
  <h2 class="title">Wichtige Ankündigung</h2>
  <p class="text">
    Dies ist eine wichtige Information für alle Benutzer unserer Plattform. Bitte lies sie sorgfältig durch.
  </p>
  <a href="/details" class="btn-primary">Mehr erfahren</a>
</div>
```

Das Ergebnis ist sauberes, semantisches HTML, das seine Struktur klar kommuniziert. Die gesamte Darstellung wird zentral in der CSS-Datei gesteuert. Eine Änderung an der `.notification-box` wirkt sich nun sofort auf alle Elemente aus, die diese Klasse verwenden.

#### 2. Interne Stylesheets: Die Insellösung

Interne Stylesheets sind CSS-Regeln, die innerhalb eines `<style>`-Blocks im `<head>`-Bereich eines HTML-Dokuments platziert werden. Sie sind zwar schon ein Schritt besser als Inline-Styles, da sie zumindest das Styling vom HTML-Markup trennen, aber sie haben einen entscheidenden Nachteil: Sie gelten nur für dieses eine HTML-Dokument.

**Vorher: Das Problem**

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Unsere Startseite</title>
  <style>
    body {
      font-family: 'Helvetica', sans-serif;
      line-height: 1.5;
      background-color: #fff;
    }
    .container {
      max-width: 960px;
      margin: 0 auto;
      padding: 20px;
    }
    header {
      padding: 20px 0;
      border-bottom: 1px solid #eee;
    }
  </style>
</head>
<body>
  <!-- ... Seiteninhalt ... -->
</body>
</html>
```

Wenn du nun eine "Über uns"-Seite erstellst, die dasselbe Grundlayout haben soll, müsstest du den gesamten `<style>`-Block kopieren. Das führt zu denselben Wartungsproblemen wie bei Inline-Styles, nur auf einer höheren Ebene. Außerdem kann der Browser die CSS-Regeln nicht zwischenspeichern. Bei jedem Seitenaufruf muss er den Stilblock erneut herunterladen und parsen.

**Nachher: Die globale Lösung**

Der Prozess hier ist noch einfacher als bei Inline-Styles:

1.  **Erstelle eine externe CSS-Datei:** Falls noch nicht geschehen, erstelle eine Datei wie `main.css`.
2.  **Verschiebe den CSS-Code:** Kopiere den gesamten Inhalt zwischen den `<style>`- und `</style>`-Tags (ohne die Tags selbst) und füge ihn in deine `main.css`-Datei ein.
3.  **Verlinke die externe Datei:** Entferne den kompletten `<style>`-Block aus deinem HTML und ersetze ihn durch einen `<link>`-Tag, der auf deine neue CSS-Datei verweist.

Dein HTML-`<head>` sieht danach so aus:

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Unsere Startseite</title>
  <link rel="stylesheet" href="css/main.css">
</head>
<body>
  <!-- ... Seiteninhalt ... -->
</body>
</html>
```

Jetzt wird die `main.css` von allen Seiten geladen, die sie einbinden. Der Browser lädt sie beim ersten Besuch herunter und speichert sie im Cache. Bei nachfolgenden Seitenaufrufen wird sie direkt aus dem Cache geladen, was die Ladezeit spürbar verbessert.

#### 3. Veraltete HTML-Attribute und -Tags: Relikte der Vergangenheit

Der älteste und "schmutzigste" Weg, Styling zu definieren, sind veraltete HTML-Attribute wie `bgcolor`, `align`, `border` oder `width` und rein präsentationsbezogene Tags wie `<font>` oder `<center>`. Diese sind in HTML5 offiziell als veraltet (deprecated) markiert und sollten unter keinen Umständen mehr verwendet werden.

**Vorher: Das Problem**

```html
<body bgcolor="#ffffff" text="#000000">

  <center>
    <h1><font color="red" face="Arial">Willkommen!</font></h1>
  </center>

  <p align="justify">
    Ein langer Textabschnitt, der hier steht und den Blocksatz rechtfertigt.
  </p>

  <table width="100%" border="1" cellpadding="5">
    <tr>
      <td bgcolor="#dddddd">Zelle 1</td>
      <td>Zelle 2</td>
    </tr>
  </table>

</body>
```

Dieser Code ist ein Paradebeispiel für die totale Vermischung von Inhalt und Präsentation. Er ist schwer zu lesen, nicht barrierefrei und widerspricht allen modernen Webentwicklungsprinzipien.

**Nachher: Die moderne semantische Lösung**

Hier geht es nicht nur darum, CSS zu extrahieren, sondern auch darum, das HTML semantisch zu modernisieren.

1.  **Ersetze präsentationsbezogene Tags:**
    *   Das `<center>`-Tag wird entfernt. Zentrierung erreichst du mit CSS, z. B. durch `text-align: center;` für Text oder `margin: 0 auto;` für Block-Elemente.
    *   Das `<font>`-Tag wird durch ein semantisch passendes Element ersetzt, oft ein `<span>` oder, wenn der Text eine besondere Betonung hat, ein `<strong>` oder `<em>`.

2.  **Eliminiere präsentationsbezogene Attribute:**
    *   Attribute wie `bgcolor`, `text`, `align`, `border`, `width` und `cellpadding` werden restlos aus dem HTML entfernt.
    *   Ihre Funktionalität wird vollständig durch CSS-Klassen abgebildet.

Die refaktorierte Version könnte so aussehen:

**HTML:**

```html
<body>

  <header class="page-header">
    <h1 class="welcome-title">Willkommen!</h1>
  </header>

  <p class="text-justify">
    Ein langer Textabschnitt, der hier steht und den Blocksatz rechtfertigt.
  </p>

  <table class="data-table">
    <thead>
      <tr>
        <th>Spalte 1</th>
        <th>Spalte 2</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="cell-highlight">Zelle 1</td>
        <td>Zelle 2</td>
      </tr>
    </tbody>
  </table>

</body>
```

**CSS (`main.css`):**

```css
body {
  background-color: #ffffff;
  color: #000000;
}

.page-header {
  text-align: center;
}

.welcome-title {
  color: red;
  font-family: Arial, sans-serif;
}

.text-justify {
  text-align: justify;
}

.data-table {
  width: 100%;
  border-collapse: collapse; /* Bessere Alternative zu border="1" */
  border: 1px solid #000;
}

.data-table th,
.data-table td {
  border: 1px solid #000;
  padding: 5px;
}

.data-table .cell-highlight {
  background-color: #dddddd;
}
```

Durch diesen Prozess hast du nicht nur das CSS extrahiert, sondern auch die Semantik deines HTML-Dokuments deutlich verbessert (z. B. durch die Verwendung von `<thead>` und `<tbody>` in der Tabelle). Das Ergebnis ist ein sauberes, zukunftssicheres und professionelles Fundament, auf dem du aufbauen kannst. Die Trennung von Stil und Struktur ist kein optionaler Luxus, sondern die Grundlage für skalierbare und wartbare Webanwendungen.
