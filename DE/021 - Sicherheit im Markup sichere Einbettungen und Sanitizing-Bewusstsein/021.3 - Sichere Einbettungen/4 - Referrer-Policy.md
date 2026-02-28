# Referrer-Policy

### Referrer-Policy: Kontrolle über geteilte Informationen

Stell dir vor, du klickst auf einen Link. Eine ganz alltägliche Handlung im Web. Doch im Hintergrund passiert mehr, als du vielleicht ahnst. Wenn dein Browser von einer Seite A zu einer Seite B navigiert, sendet er eine kleine, aber potenziell sehr aufschlussreiche Information mit: die genaue Adresse der Seite A. Diese Information wird im `Referer`-HTTP-Header übertragen. Und ja, das ist kein Tippfehler – der Header heißt historisch bedingt `Referer` mit einem "r", nicht `Referrer`.

Warum ist das wichtig? Die Zielseite (Seite B) weiß dadurch, woher du kommst. Das ist nützlich für Web-Analysen, um zu verstehen, welche Kanäle Besucher auf eine Website bringen. Aber es ist auch ein potenzielles Datenschutz- und Sicherheitsrisiko.

Was, wenn die URL der Seite A sensible Daten enthält? Denk an eine URL wie diese: `https://deine-bank.de/intern/passwort-zuruecksetzen?token=a1b2c3d4e5f6`. Wenn du von dieser Seite auf einen externen Link klickst, etwa zum Impressum, das auf einer anderen Domain liegt, würde die Zielseite diesen `token` erhalten. Ein Angreifer, der die Logs dieser Zielseite kontrolliert, könnte so deinen Account übernehmen. Auch scheinbar harmlose Informationen, wie die URL eines internen Projektmanagement-Tools, könnten einem Angreifer verraten, welche Software dein Unternehmen nutzt.

Genau hier kommt die `Referrer-Policy` ins Spiel. Sie ist ein Sicherheitsmechanismus, mit dem du als Entwickler exakt steuern kannst, welche Referrer-Informationen der Browser senden soll – oder ob er überhaupt welche senden soll.

#### Wie wird die Referrer-Policy festgelegt?

Du hast hauptsächlich drei Möglichkeiten, die `Referrer-Policy` für deine Website zu definieren.

1.  **Als HTTP-Header (serverseitig):** Dies ist die robusteste Methode, da sie vom Server für jede Antwort festgelegt wird. Der Header sieht so aus:
    ```http
    Referrer-Policy: strict-origin-when-cross-origin
    ```

2.  **Als `<meta>`-Tag im HTML-Dokument:** Für uns im Kontext von HTML ist dies der direkteste Weg. Du platzierst einfach ein `<meta>`-Tag im `<head>`-Bereich deiner Seite. Diese Methode ist besonders nützlich, wenn du keinen Zugriff auf die Serverkonfiguration hast.
    ```html
    <head>
      <meta name="referrer" content="strict-origin-when-cross-origin">
      ...
    </head>
    ```

3.  **Als Attribut an einzelnen Elementen:** Du kannst die Policy auch für einzelne Links, Bilder oder Skripte überschreiben, indem du das `referrerpolicy`-Attribut (diesmal korrekt mit zwei "r") direkt am Element setzt.
    ```html
    <a href="https://externe-seite.de" referrerpolicy="no-referrer">
      Dieser Link verrät nichts über seine Herkunft.
    </a>
    ```
    Die Spezifität gewinnt: Ein Attribut an einem Element überschreibt immer die allgemeine Policy, die per `<meta>`-Tag oder HTTP-Header für das gesamte Dokument festgelegt wurde.

#### Die verschiedenen Policy-Werte im Detail

Der wahre Kern der `Referrer-Policy` liegt in den verschiedenen Werten, die du für `content` bzw. im Header angeben kannst. Sie reichen von "gar nichts verraten" bis zu "alles verraten". Lass uns die wichtigsten Werte durchgehen, von den restriktivsten zu den freizügigsten.

##### `no-referrer`
Dies ist die strengste Einstellung. Wenn du diese Policy wählst, wird der `Referer`-Header **niemals** gesendet. Egal, ob der Benutzer auf einen internen oder externen Link klickt, die Zielseite erhält keinerlei Information darüber, woher der Klick kam.

*   **Was es tut:** Unterdrückt den `Referer`-Header vollständig.
*   **Wann du es nutzen könntest:** Wenn du maximalen Datenschutz für deine Benutzer gewährleisten willst und keine Analysedaten über die Herkunft von Klicks benötigst. Perfekt für Seiten, die sensible Aktionen durchführen.

```html
<meta name="referrer" content="no-referrer">
```

##### `same-origin`
Diese Policy ist schon etwas gesprächiger, aber nur mit sich selbst. Der `Referer`-Header wird nur dann gesendet, wenn das Ziel auf derselben "Origin" (Herkunft) liegt. Eine Origin ist die Kombination aus Protokoll, Hostname und Port (z.B. `https://deine-seite.de:443`). Bei einem Klick auf eine externe Seite wird kein `Referer`-Header gesendet.

*   **Was es tut:** Sendet den vollen Referrer nur für Anfragen innerhalb der eigenen Website.
*   **Wann du es nutzen könntest:** Ideal, wenn du internes Klick-Tracking benötigst, um das Benutzerverhalten auf deiner eigenen Seite zu analysieren, aber keine Informationen nach außen geben möchtest.

```html
<meta name="referrer" content="same-origin">
```

##### `strict-origin`
Hier wird ein Schritt weiter in Richtung Offenheit gegangen. Diese Policy sendet immer die Herkunfts-Origin (z. B. `https://deine-seite.de/`), aber **nicht** den vollständigen Pfad (z. B. `/artikel/geheim?q=123`). Der sensible Teil der URL bleibt also verborgen. Der Zusatz "strict" bedeutet, dass diese Information nicht gesendet wird, wenn ein Sicherheits-Downgrade stattfindet (Navigation von einer HTTPS- zu einer HTTP-Seite).

*   **Was es tut:** Sendet nur die Origin, aber nur bei gleichbleibendem oder verbessertem Sicherheitslevel.
*   **Wann du es nutzen könntest:** Eine gute, datenschutzfreundliche Option, die externen Seiten zumindest mitteilt, von welcher Domain der Traffic kommt, ohne Details preiszugeben.

```html
<meta name="referrer" content="strict-origin">
```

##### `strict-origin-when-cross-origin`
Dies ist eine sehr beliebte und ausgewogene Richtlinie und oft die **empfohlene Standardeinstellung** für moderne Websites. Sie kombiniert das Beste aus zwei Welten:
*   **Für Anfragen auf der gleichen Origin** (same-origin) wird die **vollständige URL** als Referrer gesendet. Das ermöglicht dir detaillierte Analysen auf deiner eigenen Seite.
*   **Für Anfragen zu einer anderen Origin** (cross-origin) wird **nur die Origin** gesendet, genau wie bei `strict-origin`.
*   Der "strict"-Teil stellt sicher, dass bei einem Downgrade von HTTPS zu HTTP gar kein Referrer gesendet wird.

*   **Was es tut:** Sendet die volle URL intern und nur die Origin extern, schützt aber vor Downgrade-Angriffen.
*   **Wann du es nutzen könntest:** Fast immer. Es ist der beste Kompromiss zwischen nützlichen Analysedaten für dich und dem Schutz der Privatsphäre deiner Nutzer gegenüber Dritten.

```html
<meta name="referrer" content="strict-origin-when-cross-origin">
```

##### `no-referrer-when-downgrade`
Dies war lange Zeit die Standardeinstellung in den meisten Browsern. Die volle URL wird als Referrer gesendet, **es sei denn**, die Navigation erfolgt von einer sicheren Seite (HTTPS) zu einer unsicheren (HTTP). In diesem "Downgrade"-Fall wird kein Referrer gesendet.

*   **Was es tut:** Sendet immer die volle URL, außer bei HTTPS-zu-HTTP-Navigation.
*   **Wann du es nutzen könntest:** Wenn du `strict-origin-when-cross-origin` aus irgendeinem Grund nicht verwenden kannst, ist dies eine vernünftige, sichere Basis. Es verhindert das Leaken von Informationen über unsichere Verbindungen.

```html
<meta name="referrer" content="no-referrer-when-downgrade">
```

##### `unsafe-url`
Der Name ist Programm. Diese Richtlinie sendet **immer die volle URL** als Referrer, einschließlich aller Pfade und Query-Parameter. Das gilt auch für Cross-Origin-Anfragen und sogar bei einem Downgrade von HTTPS zu HTTP.

*   **Was es tut:** Sendet immer und überall die vollständige Referrer-URL.
*   **Wann du es nutzen könntest:** Du solltest diese Einstellung **vermeiden**. Sie birgt erhebliche Sicherheits- und Datenschutzrisiken, da sensible Informationen leicht an Dritte oder über ungesicherte Verbindungen weitergegeben werden können. Es gibt kaum legitime Anwendungsfälle dafür.

```html
<!-- Dies ist in der Regel eine schlechte Idee! -->
<meta name="referrer" content="unsafe-url">
```

#### Welche Policy solltest du wählen?

Wenn du dir unsicher bist, ist die Antwort einfach: `strict-origin-when-cross-origin`.

Diese Richtlinie bietet den besten Schutz für die Daten deiner Nutzer, ohne dass du auf wertvolle interne Analysedaten verzichten musst. Du verhinderst, dass sensible Teile deiner URLs an Dritte gelangen, und schützt deine Nutzer vor dem Leaken von Informationen über unsichere Verbindungen.

Es ist wichtig zu wissen, dass moderne Browser inzwischen selbst strengere Standardeinstellungen haben. Verlässt du dich auf den Browser-Standard, wird wahrscheinlich eine Policy wie `strict-origin-when-cross-origin` angewendet. Es ist jedoch eine bewährte Praxis, die gewünschte Policy explizit in deinem HTML oder über den HTTP-Header festzulegen. So hast du die volle Kontrolle und bist nicht von den sich ändernden Standardeinstellungen der verschiedenen Browser abhängig.

Durch das bewusste Setzen einer `Referrer-Policy` leistest du einen wichtigen Beitrag zur Sicherheit und zum Datenschutz deiner Webanwendung. Es ist eine kleine Zeile Code mit großer Wirkung, die zeigt, dass du die Privatsphäre deiner Besucher ernst nimmst.
