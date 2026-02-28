# Preload und Prefetch

### Preload und Prefetch: Dem Browser einen Schritt voraus sein

Stell dir den Webbrowser als einen fleißigen, aber anfangs ahnungslosen Assistenten vor. Wenn du ihm eine HTML-Datei gibst, beginnt er, sie von oben nach unten zu lesen und abzuarbeiten. Er liest eine Zeile, versteht sie, führt sie aus und geht zur nächsten. Wenn er auf einen Link zu einer CSS-Datei stößt, hält er inne und sagt sich: "Ah, das brauche ich, um die Seite zu gestalten. Ich lade das mal herunter." Nachdem die CSS-Datei heruntergeladen und analysiert wurde, entdeckt er vielleicht darin eine `@font-face`-Regel, die auf eine Schriftart verweist. "Oh, diese Schriftart wird auch benötigt! Lade ich die auch mal herunter."

Du siehst das Problem? Der Browser entdeckt wichtige Ressourcen oft erst spät in einer langen Kette von Abhängigkeiten. Jede dieser späten Entdeckungen führt zu einer Verzögerung, einem Moment, in dem der Nutzer auf eine unvollständig gerenderte Seite starrt. Die Zeit, bis die Seite benutzbar und visuell ansprechend ist, verlängert sich unnötig.

Genau hier kommen Resource Hints wie `preload` und `prefetch` ins Spiel. Sie sind deine Möglichkeit, dem Browser proaktiv zu sagen: "Hey, auch wenn du es noch nicht weißt, du wirst diese Ressource gleich *unbedingt* brauchen. Lade sie doch schon mal im Voraus." Du gibst dem Browser quasi einen Wissensvorsprung und hilfst ihm, seine Arbeit effizienter zu gestalten.

#### `preload`: Kritische Ressourcen für die aktuelle Seite vorladen

`preload` ist der wichtigste und direkteste Hinweis, den du dem Browser geben kannst. Mit `<link rel="preload">` signalisierst du, dass eine bestimmte Ressource für die *aktuelle Seite* von entscheidender Bedeutung ist und mit hoher Priorität heruntergeladen werden sollte. Der Browser wird den Download dieser Ressource sofort starten, parallel zum Parsen des restlichen Dokuments, ohne darauf zu warten, dass er sie organisch entdeckt.

Die grundlegende Syntax sieht so aus:

```html
<link rel="preload" href="/pfad/zur/ressource.js" as="script">
```

Schauen wir uns die Teile genauer an:

*   `rel="preload"`: Damit teilst du dem Browser deine Absicht mit.
*   `href`: Der Pfad zur Ressource, die du vorladen möchtest.
*   `as`: Dieses Attribut ist **entscheidend**. Du musst dem Browser mitteilen, um welche Art von Ressource es sich handelt. Warum? Weil der Browser je nach Typ unterschiedliche Prioritäten vergibt und Sicherheitsrichtlinien anwendet. Eine Schriftart (`font`) hat eine andere Priorität als ein Skript (`script`) oder ein Bild (`image`). Ohne das `as`-Attribut weiß der Browser nicht, was er mit der vorgeladenen Ressource anfangen soll, und der `preload`-Hinweis wäre nutzlos.

Gängige Werte für `as` sind:
*   `script` für JavaScript-Dateien.
*   `style` für CSS-Dateien.
*   `font` für Schriftarten (z.B. WOFF2).
*   `image` für Bilder (z.B. JPG, PNG, WebP).
*   `fetch` für Daten, die per `fetch()` oder `XMLHttpRequest` geladen werden (z.B. JSON-Dateien).

**Ein klassisches Anwendungsbeispiel: Spät entdeckte Schriftarten**

Erinnerst du dich an das Problem mit der Schriftart, die in einer CSS-Datei versteckt ist? Das ist der perfekte Fall für `preload`. Normalerweise sieht der Ladevorgang so aus:

1.  Browser lädt `index.html`.
2.  Browser entdeckt `<link rel="stylesheet" href="style.css">`.
3.  Browser lädt `style.css`.
4.  Browser analysiert `style.css` und findet `@font-face { src: url('meine-schrift.woff2'); }`.
5.  Browser lädt `meine-schrift.woff2`.

Zwischen Schritt 1 und 5 vergeht wertvolle Zeit, in der Text vielleicht unsichtbar ist oder mit einer falschen Schriftart angezeigt wird (Flash of Unstyled Text/Flash of Invisible Text). Mit `preload` optimieren wir das:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Meine Seite</title>

  <!-- Sag dem Browser sofort, dass er die Schriftart laden soll -->
  <link rel="preload" href="/fonts/meine-schrift.woff2" as="font" type="font/woff2" crossorigin>

  <!-- Die CSS-Datei, die die Schriftart später referenziert -->
  <link rel="stylesheet" href="/css/style.css">
</head>
<body>
  ...
</body>
</html>
```

Ein wichtiges Detail siehst du hier: das `crossorigin`-Attribut. Schriftarten werden aus Sicherheitsgründen oft über eine sogenannte "CORS-Anfrage" geladen. Damit der vorgeladene Font später auch wirklich genutzt werden kann, muss der `preload`-Request mit dem tatsächlichen Request übereinstimmen. Daher ist `crossorigin` bei Schriftarten fast immer notwendig.

Durch diesen `preload`-Hinweis startet der Browser den Download der Schriftart fast zeitgleich mit dem Download der CSS-Datei. Wenn das CSS dann die Schriftart anfordert, liegt sie bereits im Cache des Browsers bereit und kann sofort verwendet werden. Das Ergebnis ist eine deutlich schnellere Darstellung des korrekten Texts.

**Wann solltest du `preload` verwenden?**

*   Für Ressourcen, die für das erste Rendern der Seite (First Paint, First Contentful Paint) kritisch sind, aber vom Browser erst spät entdeckt werden.
*   Für Schriftarten, die im "Above the Fold"-Bereich (dem sofort sichtbaren Teil der Seite) verwendet werden.
*   Für das "Largest Contentful Paint" (LCP) Bild, um dessen Ladezeit zu minimieren.
*   Für CSS- oder JavaScript-Dateien, die dynamisch per JavaScript geladen werden, deren Notwendigkeit du aber schon beim initialen HTML-Laden kennst.

**Eine wichtige Warnung:** `preload` ist eine Anweisung, kein Vorschlag. Der Browser *muss* die Ressource laden. Setze es daher mit Bedacht ein. Wenn du zu viele oder unwichtige Ressourcen vorlädst, konkurrieren diese um die begrenzte Bandbreite des Nutzers und können das Laden wirklich kritischer Ressourcen (wie dem HTML selbst oder dem blockierenden CSS) verlangsamen. Lade nur das vor, was du wirklich frühzeitig brauchst.

#### `prefetch`: Ressourcen für die nächste Seite vorbereiten

Während `preload` sich auf die *aktuelle* Seite konzentriert, blickt `prefetch` in die Zukunft. Mit `<link rel="prefetch">` gibst du dem Browser einen sehr niedrigpriorisierte Hinweis, eine Ressource zu laden, die der Nutzer *wahrscheinlich* auf der *nächsten* Seite benötigen wird.

Die Syntax ist einfacher, da das `as`-Attribut optional ist:

```html
<link rel="prefetch" href="/naechste-seite.html">
<link rel="prefetch" href="/assets/wichtiges-bild-fuer-produkt-detail.jpg">
```

Der Browser behandelt `prefetch`-Hinweise als "nice to have". Er wird diese Ressourcen nur dann herunterladen, wenn er gerade nichts Besseres zu tun hat, also wenn die aktuelle Seite vollständig geladen ist und die Netzwerkverbindung frei ist (im sogenannten "idle time"). Er stört damit nicht das Laden der aktuellen Seite.

**Wann ist `prefetch` sinnvoll?**

Stell dir einen mehrstufigen Bestellprozess vor. Wenn der Nutzer auf Seite 1 seine Adresse eingibt, ist die Wahrscheinlichkeit hoch, dass er als Nächstes zur Zahlungsseite (Seite 2) navigiert. Während der Nutzer also das Formular ausfüllt, kann der Browser im Hintergrund bereits das Haupt-JavaScript oder die CSS-Datei für die Zahlungsseite laden.

```html
<!-- Auf der Adress-Seite (Schritt 1) -->
<link rel="prefetch" href="/js/payment-scripts.js">
<link rel="prefetch" href="/css/payment-styles.css">
```

Wenn der Nutzer dann auf "Weiter" klickt, sind diese Ressourcen bereits im Cache. Die nächste Seite baut sich gefühlt augenblicklich auf, da die wichtigsten Bausteine schon da sind.

Weitere Anwendungsfälle:
*   Auf einer Suchergebnisseite könntest du die HTML-Seite des wahrscheinlichsten Suchergebnisses vorab laden.
*   In einem Bildergalerie-Slider könntest du das nächste Bild per `prefetch` laden, während der Nutzer das aktuelle betrachtet.
*   Auf einer Blog-Startseite könntest du den wahrscheinlichsten nächsten Artikel, den ein Nutzer anklickt (z.B. den neuesten), vorab laden.

`prefetch` ist eine fantastische Möglichkeit, die Navigation zwischen den Seiten deiner Anwendung extrem flüssig und schnell zu gestalten.

#### Der direkte Vergleich: `preload` vs. `prefetch`

| Kriterium | `preload` | `prefetch` |
| :--- | :--- | :--- |
| **Zweck** | Kritische Ressourcen für die **aktuelle** Navigation laden. | Wahrscheinlich benötigte Ressourcen für eine **zukünftige** Navigation laden. |
| **Priorität** | Hoch. Wird als wichtige Ressource für die aktuelle Seite behandelt. | Sehr niedrig. Wird nur geladen, wenn der Browser Leerlauf hat. |
| **Verbindlichkeit** | Obligatorisch. Der Browser muss die Ressource laden. | Optional. Der Browser kann die Ressource laden, muss aber nicht. |
| **Auswirkung** | Verbessert die Lade-Metriken der **aktuellen** Seite (FCP, LCP, TTI). | Verbessert die Ladezeit der **nächsten** Seite, auf die navigiert wird. |
| **`as`-Attribut** | Zwingend erforderlich. | Optional. |

#### Verwandte Technologien: `preconnect` und `dns-prefetch`

Neben `preload` und `prefetch` gibt es zwei weitere nützliche Hinweise, die sich nicht auf das Laden von Ressourcen, sondern auf den Aufbau von Verbindungen konzentrieren.

*   **`dns-prefetch`**: Dies ist der kleinste Hinweis. Du sagst dem Browser: "Ich werde später eine Verbindung zu dieser Domain aufbauen. Finde doch schon mal die IP-Adresse heraus." Der DNS-Lookup (die Umwandlung eines Domainnamens in eine IP-Adresse) kann 20-120 Millisekunden dauern. Diese Zeit sparst du.

    ```html
    <!-- Nützlich für z.B. Google Analytics oder andere Drittanbieter-Skripte -->
    <link rel="dns-prefetch" href="//www.google-analytics.com">
    ```

*   **`preconnect`**: Dieser Hinweis geht einen Schritt weiter. Er führt nicht nur den DNS-Lookup durch, sondern baut auch die komplette Verbindung zur Domain auf (TCP-Handshake und TLS-Verschlüsselung). Das kann mehrere hundert Millisekunden einsparen, besonders bei langsamen Verbindungen. Dies ist extrem nützlich für APIs oder CDNs, von denen du weißt, dass du gleich kritische Ressourcen laden wirst.

    ```html
    <!-- Baue schon mal die Verbindung zum Google Fonts CDN auf -->
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    ```

Du kannst diese Techniken kombinieren. Wenn du zum Beispiel eine Schriftart von Google Fonts lädst, ist es eine bewährte Methode, die Verbindung zuerst per `preconnect` aufzubauen und die spezifische Schriftartdatei dann per `preload` vorzuladen. So optimierst du sowohl den Verbindungsaufbau als auch den Ressourcendownload und gibst dem Browser die bestmöglichen Anweisungen, um deine Seite blitzschnell zu rendern.
