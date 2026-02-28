# Sicherheitsaspekte (rel_noopener)

### Sicherheitsaspekte: Die unsichtbare Gefahr von `target="_blank"` und die Rolle von `rel="noopener"`

Wenn du einen Link erstellst, der in einem neuen Browser-Tab oder -Fenster geöffnet werden soll, ist das Attribut `target="_blank"` dein Mittel der Wahl. Es ist eine der bekanntesten und am häufigsten verwendeten Funktionen des `<a>`-Tags, besonders wenn du Besucher auf deiner Seite halten und sie gleichzeitig auf externe Ressourcen verweisen möchtest.

```html
<!-- Ein typischer Link, der in einem neuen Tab öffnet -->
<a href="https://beispiel-externe-seite.com" target="_blank">Besuche diese interessante Webseite</a>
```

Was auf den ersten Blick wie eine reine Komfortfunktion aussieht, birgt jedoch eine subtile, aber potenziell gefährliche Sicherheitslücke. Diese Lücke ist nicht sofort ersichtlich, kann aber von bösartigen Akteuren ausgenutzt werden, um deine Nutzer zu täuschen und an ihre Daten zu gelangen. Um dieses Problem zu verstehen, müssen wir uns ansehen, was im Hintergrund passiert, wenn ein Browser einen solchen Link öffnet.

#### Die unsichtbare Verbindung: Das `window.opener`-Objekt

Wenn du von deiner Seite (nennen wir sie Seite A) auf eine andere Seite (Seite B) mit `target="_blank"` verlinkst, stellt der Browser eine Verbindung zwischen den beiden Tabs her. Die neu geöffnete Seite B erhält über JavaScript Zugriff auf ein spezielles Objekt: `window.opener`.

Dieses `window.opener`-Objekt ist im Grunde eine Referenz auf das `window`-Objekt der ursprünglichen Seite A. Das bedeutet, der JavaScript-Code, der auf Seite B ausgeführt wird, hat eine gewisse Kontrolle über Seite A. Zwar sind die meisten direkten Manipulationen aus Sicherheitsgründen durch die Same-Origin-Policy blockiert (der Code auf Seite B kann nicht einfach den Inhalt von Seite A auslesen), aber eine entscheidende Eigenschaft bleibt zugänglich: `window.opener.location`.

Mit `window.opener.location` kann die neue Seite die URL der ursprünglichen Seite ändern und sie auf eine völlig andere Adresse weiterleiten. Und genau hier liegt die Gefahr.

#### Das Angriffsszenario: "Tabnabbing" und Phishing

Stell dir folgendes Szenario vor: Du betreibst einen Blog und erlaubst Nutzern, Kommentare mit Links zu hinterlassen. Ein Angreifer postet einen Link zu seiner scheinbar harmlosen Webseite. Ein Besucher deines Blogs klickt auf diesen Link.

1.  **Der Klick:** Der Nutzer klickt auf den Link in deinem Kommentarbereich. Dank `target="_blank"` öffnet sich die Webseite des Angreifers in einem neuen Tab. Der ursprüngliche Tab mit deinem Blog bleibt im Hintergrund geöffnet.
2.  **Der Trick im neuen Tab:** Während der Nutzer sich die neue Seite ansieht (die vielleicht nur eine Katze zeigt oder langsam lädt, um Zeit zu gewinnen), führt der Angreifer im Hintergrund ein kleines JavaScript aus. Dieses Skript greift auf `window.opener` zu und ändert die URL deines im Hintergrund geöffneten Blog-Tabs.
3.  **Die Fälschung:** Der Angreifer leitet deinen ursprünglichen Tab auf eine gefälschte Version deiner Login-Seite um. Diese Seite sieht exakt so aus wie deine echte Login-Seite, wird aber auf dem Server des Angreifers gehostet.
4.  **Die Rückkehr:** Wenn der Nutzer mit der Seite des Angreifers fertig ist und den Tab schließt, kehrt er zu deinem ursprünglichen Tab zurück. Er sieht eine Login-Maske und denkt sich vielleicht: "Oh, meine Sitzung ist abgelaufen, ich muss mich wohl neu anmelden." Da die URL-Leiste bei einem schnellen Blick echt aussieht und die Seite vertraut wirkt, gibt er seine Anmeldedaten ein.

In diesem Moment hat der Angreifer sein Ziel erreicht. Er hat die Anmeldeinformationen deines Nutzers abgefangen (Phishing), weil er die Kontrolle über den ursprünglichen Tab übernehmen konnte. Diese Angriffsmethode wird als "Reverse Tabnabbing" bezeichnet.

**Ein konkretes Code-Beispiel:**

Angenommen, dies ist der Link auf deiner Seite:

```html
<!-- Deine Seite: blog.html -->
<p>
  Schaut euch diesen tollen Link an, den ein Nutzer geteilt hat:
  <a href="boesewebsite.html" target="_blank">Harmloser Link</a>
</p>
```

Die `boesewebsite.html` könnte folgenden JavaScript-Code enthalten:

```html
<!-- Die bösartige Zielseite: boesewebsite.html -->
<!DOCTYPE html>
<html>
<head>
  <title>Eine interessante Seite</title>
</head>
<body>
  <h1>Willkommen!</h1>
  <p>Schau dich ruhig um...</p>

  <script>
    // Prüfe, ob die Seite in einem neuen Tab von einer anderen Seite geöffnet wurde
    if (window.opener) {
      // Leite die ursprüngliche Seite auf eine gefälschte Login-Seite um
      window.opener.location.href = "https://fake-login-seite.com/login";
    }
  </script>
</body>
</html>
```

Sobald ein Nutzer auf den Link klickt, wird der Code im neuen Tab ausgeführt und die ursprüngliche Seite im Hintergrund auf die Phishing-Seite umgeleitet. Die Gefahr ist real und erstaunlich einfach umzusetzen.

#### Die Lösung: Die Verbindung kappen mit `rel="noopener"`

Glücklicherweise gibt es eine sehr einfache und effektive Lösung für dieses Problem: das `rel`-Attribut mit dem Wert `noopener`.

Wenn du dieses Attribut zu deinem Link hinzufügst, weist du den Browser an, die Verbindung zwischen den beiden Tabs zu kappen. Technisch ausgedrückt: Das `window.opener`-Objekt wird im neuen Tab auf `null` gesetzt.

```html
<!-- Ein sicherer Link, der in einem neuen Tab öffnet -->
<a href="https://beispiel-externe-seite.com" target="_blank" rel="noopener">
  Besuche diese interessante Webseite (sicher)
</a>
```

Wenn nun die bösartige Seite versucht, auf `window.opener` zuzugreifen, erhält sie nur `null` zurück. Der Versuch, `window.opener.location` zu ändern, führt zu einem Fehler, und der Angriff scheitert. Deine ursprüngliche Seite bleibt unberührt und sicher.

#### Ein verwandtes Attribut: `rel="noreferrer"`

Oft siehst du `noopener` in Kombination mit einem weiteren Wert: `noreferrer`.

```html
<a href="https://beispiel-externe-seite.com" target="_blank" rel="noopener noreferrer">
  Besuche diese Webseite (sicher und privat)
</a>
```

Was macht `noreferrer`? Wenn ein Nutzer von einer Seite auf eine andere klickt, sendet der Browser normalerweise einen sogenannten `Referer`-HTTP-Header an die Zielseite. Dieser Header enthält die URL der Herkunftsseite. Das ist nützlich für Web-Analytics, um zu sehen, woher die Besucher kommen.

`rel="noreferrer"` unterbindet das Senden dieses Headers. Die Zielseite erfährt also nicht, von welcher Seite der Nutzer gekommen ist. Dies hat primär Auswirkungen auf die Privatsphäre und das Tracking, bietet aber auch einen Nebeneffekt: In älteren Browsern, die `noopener` noch nicht kannten, hatte `noreferrer` ebenfalls die Wirkung, das `window.opener`-Objekt zu entfernen.

Die Kombination `rel="noopener noreferrer"` ist daher eine sehr robuste Methode:
*   **`noopener`**: Blockiert den Zugriff auf `window.opener` und schützt vor Tabnabbing (Sicherheit).
*   **`noreferrer`**: Verhindert die Weitergabe der Herkunfts-URL (Privatsphäre) und bietet als Nebeneffekt Abwärtskompatibilität für den `noopener`-Schutz.

#### Moderne Browser und die heutige Best Practice

Die gute Nachricht ist, dass die Entwickler von Browsern dieses Problem erkannt haben. Moderne Browser wie Chrome, Firefox, Safari und Edge haben ihr Standardverhalten geändert. Wenn du `target="_blank"` in einem `<a>`-Tag verwendest, behandeln sie es so, als ob du `rel="noopener"` bereits hinzugefügt hättest. Das `window.opener`-Objekt ist also standardmäßig `null`.

Warum solltest du `rel="noopener"` dann überhaupt noch explizit schreiben? Es gibt mehrere gute Gründe:

1.  **Rückwärtskompatibilität:** Nicht alle deine Nutzer verwenden die allerneueste Browser-Version. Um auch Nutzer mit älteren Browsern zu schützen, die dieses neue Standardverhalten noch nicht implementiert haben, ist die explizite Angabe unerlässlich.
2.  **Klarheit und Absicht:** Code sollte selbsterklärend sein. Wenn ein anderer Entwickler deinen HTML-Code liest und `rel="noopener"` sieht, weiß er sofort, dass du dir der Sicherheitsimplikationen bewusst bist und bewusst gehandelt hast. Sich auf implizites Verhalten zu verlassen, kann zu Verwirrung führen.
3.  **Konsistenz:** Es ist eine gute Angewohnheit, Sicherheitspraktiken konsequent anzuwenden, anstatt sich auf die sich ständig ändernde Landschaft der Browser-Standardeinstellungen zu verlassen.

**Als Faustregel gilt daher:** Immer wenn du `target="_blank"` verwendest, solltest du auch `rel="noopener"` (oder `rel="noopener noreferrer"`) hinzufügen. Es kostet dich nichts und macht deine Webseite für deine Nutzer sicherer.

#### Ein letzter Gedanke zur Performance

Neben dem Sicherheitsaspekt gibt es auch einen kleinen Performance-Vorteil. Da eine mit `window.opener` geöffnete Seite im selben Prozess wie die ursprüngliche Seite laufen kann, könnten ressourcenintensive Skripte auf der neuen Seite (z.B. komplexe Animationen oder Berechnungen) die Performance deiner Seite beeinträchtigen und sie verlangsamen. Durch `rel="noopener"` wird der neue Tab in einem eigenen, separaten Prozess geöffnet, was diese gegenseitige Beeinträchtigung verhindert und die Reaktionsfähigkeit deiner Seite schützt. Sicherheit und Performance gehen hier also Hand in Hand.
