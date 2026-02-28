# CSS und JS im Head

### CSS und JS im Head: Die Weichensteller des Renderings

Der `<head>`-Bereich deines HTML-Dokuments ist weit mehr als nur ein Ablageort für Metadaten und den Seitentitel. Er ist die Kommandozentrale, die dem Browser mitteilt, wie er deine Seite darstellen und zum Leben erwecken soll. Insbesondere die Art und Weise, wie du CSS und JavaScript hier einbindest, hat einen dramatischen Einfluss darauf, wie schnell deine Nutzer etwas sehen und mit deiner Seite interagieren können. Um das zu verstehen, müssen wir uns kurz mit dem sogenannten „Kritischen Rendering-Pfad“ (Critical Rendering Path) befassen.

Stell dir den Browser als einen fleißigen, aber sehr methodischen Arbeiter vor. Wenn er dein HTML-Dokument erhält, beginnt er, es Zeile für Zeile zu lesen und daraus eine Struktur im Speicher aufzubauen – das Document Object Model, kurz DOM. Das ist quasi der Bauplan deiner Seite. Sobald der Browser im `<head>` auf eine Anweisung zum Laden einer CSS-Datei stößt, passiert etwas Wichtiges: Er muss diesen Lade- und Verarbeitungsvorgang abwarten, bevor er die Seite für den Nutzer sichtbar machen kann. Warum? Weil er nicht weiß, wie die Elemente aussehen sollen. Er kann keinen Absatz malen, ohne zu wissen, welche Schriftart, Farbe oder Größe er hat.

Dieser Prozess – vom ersten Byte HTML bis zum Malen der ersten Pixel auf dem Bildschirm – ist der Kritische Rendering-Pfad. Und alles, was diesen Pfad blockiert, verzögert den Moment, in dem dein Nutzer die Seite sieht. CSS und JavaScript sind die häufigsten Blockierer.

#### CSS im Head – Der notwendige Stilist

Grundsätzlich gehört CSS in den `<head>`. Das ist eine goldene Regel. Platzierst du deine Stylesheets stattdessen am Ende des `<body>`, riskierst du einen unschönen Effekt, den man „Flash of Unstyled Content“ (FOUC) nennt. Der Browser würde in diesem Fall zuerst das ungestaltete HTML rendern – also reinen, schmucklosen Text und Bilder – und erst Augenblicke später, wenn das CSS geladen ist, alles neu formatieren. Das sieht unprofessionell aus und sorgt für ein unruhiges Ladeerlebnis.

Also laden wir CSS im `<head>`, um FOUC zu vermeiden.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meine Webseite</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <!-- ... Seiteninhalt ... -->
</body>
</html>
```

Diese Standardmethode mit `<link rel="stylesheet">` ist einfach und korrekt, hat aber einen entscheidenden Nachteil: Sie ist **render-blockierend**. Der Browser hält den gesamten Rendering-Prozess an, bis die Datei `style.css` vollständig heruntergeladen und verarbeitet wurde. Erst dann hat er das CSS Object Model (CSSOM) erstellt – das Pendant zum DOM für Stile – und kann beide kombinieren, um die Seite zu zeichnen.

Bei einer kleinen CSS-Datei und einer schnellen Verbindung ist das kein Problem. Aber was, wenn die Datei groß ist oder die Netzwerkverbindung langsam? Dann starrt der Nutzer auf eine weiße Seite, obwohl das HTML vielleicht längst geladen ist.

**Optimierung 1: Kritisches CSS einbetten**

Die Lösung für dieses Dilemma ist eine Technik namens „Critical CSS“. Die Idee dahinter ist, nur die absolut notwendigsten CSS-Regeln zu identifizieren, die für die Darstellung des sofort sichtbaren Bereichs der Seite („above the fold“) erforderlich sind. Das sind typischerweise Stile für den Header, die Navigation und vielleicht den ersten Inhaltsabschnitt.

Dieses winzige CSS-Paket wird nicht in einer externen Datei geladen, sondern direkt in einem `<style>`-Tag im `<head>` platziert.

```html
<head>
    <style>
        /* Kritisches CSS: Nur das Nötigste für den sichtbaren Bereich */
        body { font-family: sans-serif; margin: 0; }
        header { background-color: #333; color: white; padding: 1rem; }
        .hero-image { width: 100%; height: auto; }
    </style>
    <!-- Das restliche CSS wird später asynchron geladen -->
</head>
```

Der Effekt ist enorm: Da kein Netzwerkanfrage für die grundlegenden Stile notwendig ist, kann der Browser sofort mit dem Rendern beginnen. Die Seite erscheint fast augenblicklich.

**Optimierung 2: Den Rest des CSS asynchron laden**

Und was ist mit dem Rest des CSS? Den wollen wir natürlich auch laden, aber ohne das initiale Rendering zu blockieren. Dafür gibt es einen cleveren Trick mit dem `<link>`-Tag. Wir weisen den Browser an, die CSS-Datei vorzuladen, aber erst anzuwenden, wenn sie komplett da ist.

```html
<head>
    <!-- ... kritisches CSS in <style> ... -->

    <!-- Lade das restliche CSS vor, ohne zu blockieren -->
    <link rel="preload" href="restliches-style.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
    
    <!-- Fallback für Browser, die JavaScript deaktiviert haben -->
    <noscript><link rel="stylesheet" href="restliches-style.css"></noscript>
</head>
```

Schauen wir uns das genauer an:
*   `rel="preload"`: Sagt dem Browser, er soll die Ressource mit hoher Priorität herunterladen, aber noch nicht anwenden.
*   `as="style"`: Definiert, dass es sich um eine Stylesheet-Datei handelt.
*   `onload="..."`: Dieser kleine JavaScript-Schnipsel wird ausgeführt, sobald die Datei fertig geladen ist. Er ändert das `rel`-Attribut von `preload` auf `stylesheet`. Erst in diesem Moment wendet der Browser die Stile an. Da dies nach dem initialen Rendern geschieht, wurde nichts blockiert.

Mit dieser Kombination – kritisches CSS inline und der Rest asynchron – erreichst du die schnellstmögliche wahrgenommene Ladezeit.

#### JavaScript im Head – Der potenziell stärkere Bremser

Noch kritischer als CSS verhält sich JavaScript, wenn es im `<head>` platziert wird. Ein herkömmliches `<script>`-Tag ist nicht nur **render-blockierend**, sondern sogar **parser-blockierend**.

```html
<head>
    <!-- SCHLECHTES BEISPIEL: Blockiert alles! -->
    <script src="mein-script.js"></script>
</head>
```

Wenn der Browser-Parser auf dieses Tag stößt, passiert Folgendes:
1.  Das Parsen des HTML-Dokuments wird sofort angehalten.
2.  Die Datei `mein-script.js` wird heruntergeladen.
3.  Das heruntergeladene Skript wird ausgeführt.
4.  Erst danach wird das Parsen des HTML fortgesetzt.

Dieser drastische Schritt ist eine Sicherheitsmaßnahme. Der Browser muss davon ausgehen, dass das Skript möglicherweise das DOM manipuliert, zum Beispiel mit `document.write()`. Um Inkonsistenzen zu vermeiden, legt er lieber alles auf Eis. Für die Performance ist das katastrophal. Jedes Skript im `<head>` wird so zu einem Flaschenhals, der die gesamte Seitenkonstruktion aufhält.

Glücklicherweise gibt es seit langem zwei Attribute, die dieses Verhalten steuern: `async` und `defer`.

**`defer`: Die empfohlene Lösung**

Das `defer`-Attribut ist in den meisten Fällen dein bester Freund.

```html
<head>
    <script src="mein-script.js" defer></script>
    <script src="ein-weiteres-script.js" defer></script>
</head>
```

Mit `defer` weist du den Browser an:
1.  Lade das Skript parallel zum Parsen des HTML herunter (keine Blockade des Parsers).
2.  Führe das Skript erst dann aus, wenn das gesamte HTML-Dokument fertig geparst wurde, aber noch bevor das `DOMContentLoaded`-Event ausgelöst wird.

Ein weiterer entscheidender Vorteil von `defer` ist, dass die Ausführungsreihenfolge der Skripte beibehalten wird. Wenn du also `mein-script.js` vor `ein-weiteres-script.js` einbindest, wird es auch zuerst ausgeführt. Das ist ideal für Skripte, die voneinander abhängig sind oder auf das vollständige DOM zugreifen müssen.

**`async`: Für unabhängige Skripte**

Das `async`-Attribut verhält sich etwas anders.

```html
<head>
    <script src="analytics.js" async></script>
    <script src="ads.js" async></script>
</head>
```

Mit `async` sagst du dem Browser:
1.  Lade das Skript parallel zum Parsen des HTML herunter.
2.  Sobald der Download abgeschlossen ist, halte das Parsen an und führe das Skript sofort aus.
3.  Setze danach das Parsen fort.

Der Haken bei `async` ist, dass die Ausführungsreihenfolge nicht garantiert ist. Das Skript, das zuerst fertig geladen ist, wird auch zuerst ausgeführt, egal in welcher Reihenfolge die `<script>`-Tags im HTML stehen. Das macht `async` zur perfekten Wahl für unabhängige Skripte von Drittanbietern, wie zum Beispiel Tracking-Codes (Google Analytics) oder Werbeskripte. Diese Skripte haben keine Abhängigkeiten zu deinem eigenen Code oder dem DOM und sollten den Seitenaufbau so wenig wie möglich stören.

| Attribut | Parser-Blockade beim Download? | Parser-Blockade bei Ausführung? | Ausführung wann? | Reihenfolge garantiert? |
| :--- | :--- | :--- | :--- | :--- |
| (keins) | Ja | Ja (direkt nach Download) | Sofort | Ja |
| `async` | Nein | Ja (sobald Download fertig) | Unvorhersehbar | Nein |
| `defer` | Nein | Nein | Nach dem HTML-Parsing | Ja |

**Faustregel:** Verwende `defer` für deine eigenen Skripte, die das DOM manipulieren oder in einer bestimmten Reihenfolge laufen müssen. Verwende `async` für unabhängige Drittanbieter-Skripte. Vermeide `<script>`-Tags im `<head>` ohne eines dieser beiden Attribute, es sei denn, du hast einen sehr guten Grund dafür.

#### Das ideale `<head>` für Performance

Wenn wir all diese Prinzipien zusammenführen, ergibt sich eine klare Struktur für einen performanten `<head>`-Bereich. Die Reihenfolge der Elemente ist dabei nicht zufällig, sondern folgt einer Logik, die dem Browser hilft, seine Aufgaben optimal zu priorisieren.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <!-- 1. Grundlegende Metadaten zuerst, damit der Browser sofort Bescheid weiß -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hochperformante Webseite</title>
    
    <!-- 2. Kritisches CSS direkt einbetten für einen sofortigen ersten Render -->
    <style>
        /* Minimale Stile für Header, Navigation, Layout... */
    </style>

    <!-- 3. Anweisung zum Vorladen des restlichen, nicht-kritischen CSS -->
    <link rel="preload" href="styles.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
    <noscript><link rel="stylesheet" href="styles.css"></noscript>

    <!-- 4. JavaScript mit defer laden, um das Parsen nicht zu blockieren -->
    <script src="app.js" defer></script>
    <script src="components.js" defer></script>

    <!-- 5. Unabhängige Drittanbieter-Skripte mit async laden -->
    <script src="https://example.com/analytics.js" async></script>
</head>
<body>
    <!-- Der sichtbare Inhalt deiner Seite -->
</body>
</html>
```

Indem du bewusst entscheidest, *wie* und *wann* deine CSS- und JavaScript-Ressourcen geladen und verarbeitet werden, verwandelst du den `<head>` von einem potenziellen Flaschenhals in ein mächtiges Werkzeug zur Performance-Optimierung. Du gibst dem Browser eine klare, effiziente Anweisung, wie er deine Seite so schnell wie möglich für deine Nutzer sichtbar und nutzbar machen kann.
