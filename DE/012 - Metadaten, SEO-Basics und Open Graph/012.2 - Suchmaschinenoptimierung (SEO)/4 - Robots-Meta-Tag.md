# Robots-Meta-Tag

### Der Robots-Meta-Tag: Dein direkter Draht zu Suchmaschinen

Stell dir vor, du hast eine Website gebaut. Einige Seiten sind für die Öffentlichkeit bestimmt – dein Blog, deine Produktseiten, deine Startseite. Andere sind eher für den internen Gebrauch oder erfüllen einen Zweck, der sie für eine Google-Suche ungeeignet macht – zum Beispiel eine "Danke für Ihre Anmeldung"-Seite, die Login-Seite für deinen Admin-Bereich oder interne Suchergebnisse. Wie teilst du einer Suchmaschine wie Google oder Bing mit, welche Seiten sie in ihren Index aufnehmen und in den Suchergebnissen anzeigen soll und welche nicht?

Genau hier kommt der Robots-Meta-Tag ins Spiel. Er ist ein mächtiges Werkzeug direkt im `<head>`-Bereich deines HTML-Dokuments, mit dem du auf Seitenebene präzise Anweisungen an die Web-Crawler (auch "Robots" oder "Spider" genannt) geben kannst.

#### Die Grundlagen: Aufbau und Platzierung

Der Robots-Meta-Tag ist ein einfacher `<meta>`-Tag und sieht in seiner grundlegendsten Form so aus:

```html
<meta name="robots" content="index, follow">
```

Lass uns das kurz aufschlüsseln:
*   `name="robots"`: Dieses Attribut legt fest, dass die Anweisung für alle Suchmaschinen-Crawler gilt. Es ist der universelle Befehl an jeden Bot, der deine Seite besucht.
*   `content="..."`: Hier stehen die eigentlichen Anweisungen, die sogenannten Direktiven. Du kannst eine oder mehrere, durch Komma getrennte Anweisungen angeben.

Dieser Tag gehört, wie alle anderen Meta-Tags, in den `<head>`-Bereich deiner HTML-Datei:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Meine wunderbare Webseite</title>
    <meta name="description" content="Eine Beschreibung meiner Seite.">
    <meta name="robots" content="index, follow">
</head>
<body>
    <!-- Dein Seiteninhalt -->
</body>
</html>
```

Wichtig ist die Unterscheidung zur `robots.txt`-Datei. Die `robots.txt` liegt im Hauptverzeichnis deiner Domain und gibt grobe Anweisungen, welche Bereiche deiner Website ein Crawler gar nicht erst besuchen (*crawlen*) soll. Der Robots-Meta-Tag hingegen gibt Anweisungen für eine spezifische Seite, die der Crawler bereits besucht hat. Er sagt dem Crawler, was er mit dem Inhalt dieser Seite tun soll, *nachdem* er ihn gelesen hat. Man kann sagen: `robots.txt` ist das Schild "Betreten verboten" am Gartentor, während der Robots-Meta-Tag eine Anweisung auf dem Küchentisch ist, was der Besucher im Haus tun oder lassen soll.

#### Die wichtigsten Direktiven: `index` und `follow`

Die beiden fundamentalsten Anweisungen, die du im `content`-Attribut verwenden kannst, steuern die Indexierung und das Link-Following.

**`index` vs. `noindex`**

*   `index`: Diese Direktive erlaubt der Suchmaschine, die Seite in ihren Index aufzunehmen. Das bedeutet, die Seite kann in den Suchergebnissen erscheinen. Wenn du gar keinen Robots-Meta-Tag angibst, ist `index` das Standardverhalten. Du musst es also nicht explizit setzen, es schadet aber auch nicht.
*   `noindex`: Dies ist eine der wichtigsten SEO-Anweisungen überhaupt. Sie verbietet der Suchmaschine, die Seite in ihren Index aufzunehmen. Selbst wenn der Crawler die Seite besucht, wird sie nicht in den Suchergebnissen auftauchen.

Wann würdest du `noindex` verwenden?
*   **Danke-Seiten:** Eine Seite, die nach dem Absenden eines Kontaktformulars erscheint, hat in den Suchergebnissen nichts zu suchen.
*   **Admin-Bereiche:** Login-Seiten oder interne Dashboards sind nicht für die Öffentlichkeit bestimmt.
*   **Interne Suchergebnisseiten:** Wenn ein Nutzer auf deiner Seite sucht, erzeugt das oft eine URL wie `deine-seite.de/suche?q=html`. Solche Seiten bieten wenig einzigartigen Wert und sollten nicht indexiert werden.
*   **Seiten mit dünnem Inhalt ("Thin Content"):** Seiten mit sehr wenig oder qualitativ minderwertigem Inhalt können dein gesamtes Ranking negativ beeinflussen. Es ist besser, sie von der Indexierung auszuschließen.
*   **Entwicklungs- oder Staging-Umgebungen:** Seiten, die sich noch im Aufbau befinden, sollten auf keinen Fall indexiert werden.

Ein typischer Tag, um eine Seite von der Indexierung auszuschließen, sieht so aus:

```html
<meta name="robots" content="noindex">
```

**`follow` vs. `nofollow`**

*   `follow`: Diese Direktive erlaubt dem Crawler, den Links auf der aktuellen Seite zu folgen, um neue Seiten zu entdecken. Auch dies ist das Standardverhalten, wenn nichts anderes angegeben wird. Der Crawler nutzt die Links auf deiner Seite, um deine Website-Struktur zu verstehen und weitere Unterseiten zu finden.
*   `nofollow`: Diese Anweisung verbietet dem Crawler, den Links auf dieser Seite zu folgen. Er wird die Links zwar sehen, ihnen aber nicht nachgehen, um die verlinkten Seiten zu crawlen oder ihnen "Link-Autorität" (oft als "Link Juice" bezeichnet) zu vererben.

Wann würdest du `nofollow` auf einer ganzen Seite einsetzen?
Das ist seltener der Fall als `noindex`, aber es gibt Anwendungsfälle. Zum Beispiel auf Seiten mit sehr vielen externen Links, für deren Qualität du nicht bürgen möchtest, etwa in einem Kommentarbereich, den du nicht moderieren kannst.

#### Kombinationen für die Praxis

Die wahre Stärke des Robots-Meta-Tags liegt in der Kombination der Direktiven.

**`noindex, follow`**
Dies ist eine sehr häufige und nützliche Kombination.

```html
<meta name="robots" content="noindex, follow">
```

Du sagst dem Crawler damit: "Liebe Suchmaschine, nimm diese Seite bitte nicht in deine Suchergebnisse auf, aber schau dir die Links an, die ich hier platziert habe, und folge ihnen. Sie führen zu wertvollen Inhalten."

Ein perfektes Beispiel hierfür ist eine Archivseite eines Blogs, die alle Beiträge eines bestimmten Monats auflistet. Die Archivseite selbst ist als Suchergebnis nicht besonders wertvoll, aber die Links zu den einzelnen Blogartikeln sind es sehr wohl. Mit `noindex, follow` stellst du sicher, dass die wichtigen Artikel gefunden werden, ohne die Suchergebnisse mit der Archivseite zu "verschmutzen".

**`noindex, nofollow`**
Die restriktivste Kombination.

```html
<meta name="robots" content="noindex, nofollow">
```

Damit erteilst du ein komplettes Verbot: "Diese Seite gehört nicht in den Index, und ignoriere bitte auch alle Links, die du hier findest." Das ist die richtige Wahl für die bereits erwähnten Login-Seiten oder für Testseiten, die versehentlich online gegangen sind.

#### Spezifische Anweisungen für einzelne Crawler

Manchmal möchtest du vielleicht unterschiedliche Anweisungen an verschiedene Suchmaschinen geben. Während `name="robots"` für alle gilt, kannst du auch spezifische Crawler direkt ansprechen. Die Namen der bekanntesten lauten `googlebot` (Google), `bingbot` (Bing) oder `duckduckbot` (DuckDuckGo).

Angenommen, du möchtest, dass deine Seite bei Bing erscheint, aber nicht bei Google. Das ist zwar ein ungewöhnlicher Fall, aber technisch möglich:

```html
<meta name="googlebot" content="noindex">
<meta name="bingbot" content="index">
```

In der Praxis ist es üblicher, eine allgemeine Regel für alle zu definieren und für einen bestimmten Bot eine Ausnahme zu machen. Google hält sich dabei an die spezifischere und restriktivere Anweisung. Wenn du also Folgendes schreibst:

```html
<meta name="robots" content="index">
<meta name="googlebot" content="noindex">
```

... wird Google die Seite nicht indexieren, während andere Suchmaschinen es tun würden.

#### Weitere nützliche Direktiven

Neben den vier Hauptdirektiven gibt es noch weitere, die dir mehr Kontrolle geben:

*   **`noarchive`**: Verhindert, dass Suchmaschinen eine zwischengespeicherte Version (einen "Cache-Link") deiner Seite in den Suchergebnissen anzeigen. Nützlich für Seiten mit sehr zeitkritischen Informationen, wie Börsenkursen oder Nachrichten, bei denen eine veraltete, gecachte Version irreführend wäre.
*   **`nosnippet`**: Verhindert, dass in den Suchergebnissen ein Textausschnitt (Snippet) oder eine Videovorschau für deine Seite angezeigt wird. Die Suchmaschine zeigt dann nur den Titel und die URL an. Dies kann die Klickrate drastisch senken und wird nur in seltenen Fällen eingesetzt.
*   **`max-snippet:[zahl]`**: Erlaubt dir, die maximale Länge des Text-Snippets in Zeichen festzulegen. Mit `-1` erlaubst du jede Länge, mit `0` verhinderst du ein Snippet (wie bei `nosnippet`).
*   **`max-image-preview:[einstellung]`**: Steuert die Größe der Bildvorschau in den Suchergebnissen. Mögliche Einstellungen sind `none`, `standard` oder `large`.
*   **`max-video-preview:[zahl]`**: Legt die maximale Dauer einer Videovorschau in Sekunden fest.

Ein Beispiel für eine kombinierte, fortgeschrittene Anweisung könnte so aussehen:

```html
<meta name="robots" content="index, follow, max-snippet:150, max-image-preview:large">
```

Mit diesem Meta-Tag gibst du den Crawlern die volle Freiheit, deine Seite zu indexieren und den Links zu folgen, legst aber gleichzeitig fest, dass der Beschreibungstext in den Suchergebnissen nicht länger als 150 Zeichen sein soll und große Vorschaubilder angezeigt werden dürfen.

Der Robots-Meta-Tag ist somit weit mehr als nur ein An/Aus-Schalter für die Indexierung. Er ist ein feines Instrument, mit dem du die Darstellung und das Verhalten deiner einzelnen Seiten in der Welt der Suchmaschinen präzise steuern kannst. Ihn zu verstehen und korrekt einzusetzen, ist ein fundamentaler Schritt auf dem Weg zu einer professionell optimierten Website.
