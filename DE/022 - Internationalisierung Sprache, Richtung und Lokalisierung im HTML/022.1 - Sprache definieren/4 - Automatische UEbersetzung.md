# Automatische Übersetzung

### Automatische Übersetzung und ihre Rolle im Web

Stell dir vor, du landest auf einer japanischen Webseite, die ein seltenes Ersatzteil für dein altes Fahrrad anbietet. Du sprichst kein Wort Japanisch, aber dein Browser schlägt dir mit einem Klick vor: „Diese Seite übersetzen?“ Du klickst, und wie von Zauberhand erscheint der Text auf Deutsch. Das ist die Macht der automatischen Übersetzung – ein Werkzeug, das das World Wide Web für Millionen von Menschen zugänglicher macht, die sonst durch Sprachbarrieren ausgeschlossen wären.

Als Webentwickler ist es wichtig, dass du dieses Phänomen nicht nur aus der Nutzerperspektive kennst, sondern auch verstehst, wie es technisch funktioniert und wie du es beeinflussen kannst. Denn diese automatische Magie ist nicht immer perfekt und kann manchmal mehr schaden als nutzen.

#### Der Auslöser: Das `lang`-Attribut

Der wichtigste Ankerpunkt für jede automatische Übersetzung ist das `lang`-Attribut im `<html>`-Tag deiner Seite. Wir haben bereits darüber gesprochen, wie essenziell dieses Attribut für Barrierefreiheit und Suchmaschinen ist. Für Übersetzungsdienste ist es der Startschuss.

Ein Browser wie Chrome, Safari oder Firefox liest die Spracheinstellung des Betriebssystems oder des Browsers selbst aus. Nehmen wir an, deine Browsersprache ist auf Deutsch (`de`) eingestellt. Wenn du nun eine Webseite besuchst, deren `<html>`-Tag wie folgt aussieht, passiert etwas Entscheidendes:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Bicicletas Clásicas</title>
</head>
<body>
  <h1>Componentes para tu bicicleta</h1>
  <p>Encuentra piezas raras y de alta calidad.</p>
</body>
</html>
```

Dein Browser vergleicht seine eigene Spracheinstellung (`de`) mit der deklarierten Sprache der Webseite (`es`). Da sie nicht übereinstimmen, erkennt er eine Sprachbarriere und bietet dir proaktiv an, die Seite zu übersetzen. Wäre das `lang`-Attribut nicht gesetzt oder falsch (z.B. `lang="de"` für eine spanische Seite), würde dieser Mechanismus entweder gar nicht oder fehlerhaft greifen. Eine korrekt deklarierte Sprache ist also die absolute Grundvoraussetzung, damit automatische Übersetzungsdienste überhaupt wissen, was sie tun sollen.

#### Ein kurzer Blick unter die Haube: Von Statistik zu neuronalen Netzen

Die Technologie hinter diesen Diensten hat sich in den letzten Jahren dramatisch weiterentwickelt. Früher basierten Systeme wie der frühe Google Translate auf statistischer maschineller Übersetzung (SMT). Vereinfacht gesagt, wurden riesige Mengen an bereits übersetzten Texten (z.B. Dokumente der Vereinten Nationen) analysiert, um Muster zu erkennen. Das System lernte, dass die Wortgruppe „por favor“ im Spanischen sehr wahrscheinlich „bitte“ im Deutschen entspricht. Das funktionierte für einzelne Phrasen oft erstaunlich gut, führte aber bei komplexeren Sätzen zu holprigen und oft sinnentstellenden Ergebnissen, weil dem System das tiefere Verständnis für Grammatik und Kontext fehlte.

Heute dominieren neuronale maschinelle Übersetzungen (NMT). Diese Systeme, angetrieben durch künstliche Intelligenz und maschinelles Lernen, versuchen nicht mehr nur, Phrasen zu ersetzen. Sie analysieren den gesamten Satz, verstehen die Beziehungen der Wörter zueinander und erzeugen eine Übersetzung, die den Kontext, die Grammatik und sogar den Tonfall der Zielsprache berücksichtigt. Das Ergebnis ist eine weitaus flüssigere, natürlichere und genauere Übersetzung. Dienste wie DeepL, der moderne Google Translate oder der Microsoft Translator sind Paradebeispiele für die Leistungsfähigkeit von NMT.

#### Freund oder Feind? Die zwei Seiten der Medaille

Für dich als Entwickler ist die automatische Übersetzung ein zweischneidiges Schwert. Auf der einen Seite erhöht sie die Reichweite deiner Inhalte enorm, ohne dass du einen Cent für professionelle Übersetzer ausgeben musst. Ein Nutzer in Brasilien kann deinen deutschen Blogbeitrag über CSS-Tricks lesen und verstehen. Das ist ein unschätzbarer Vorteil für die globale Zugänglichkeit von Informationen.

Auf der anderen Seite verlierst du jegliche Kontrolle über die Qualität der Darstellung. Was passiert, wenn die automatische Übersetzung ...
-   **Fachbegriffe falsch übersetzt?** Aus „Server-Side Rendering“ wird vielleicht „Serverseitige Wiedergabe“, was technisch unpräzise ist und bei deiner Zielgruppe für Verwirrung sorgt.
-   **Kulturelle Nuancen und Humor zerstört?** Ein cleveres Wortspiel in deiner Überschrift wird zu einer platten, sinnlosen Aussage.
-   **Markennamen oder Produktbezeichnungen verstümmelt?** Dein Produkt „CloudHopper“ könnte zu „Wolkenhüpfer“ werden, was vielleicht niedlich, aber kaum professionell klingt und deine Marke schwächt.
-   **Rechtliche oder sicherheitsrelevante Texte verfälscht?** Eine Warnung wie „Do not ingest“ könnte ungenau übersetzt werden und zu gefährlichen Missverständnissen führen.

Eine schlechte Übersetzung kann deine Marke unprofessionell, unzuverlässig oder im schlimmsten Fall sogar lächerlich wirken lassen. Du hast hart daran gearbeitet, eine hochwertige Webseite mit präzisen Inhalten zu erstellen – und ein Klick auf „Übersetzen“ kann diese Mühe zunichtemachen.

#### Die Kontrolle zurückgewinnen: So steuerst du die Übersetzung

Glücklicherweise bist du diesen Automatismen nicht hilflos ausgeliefert. HTML und die Konventionen der großen Übersetzungsdienste geben dir Werkzeuge an die Hand, um die maschinelle Übersetzung zu lenken.

##### Einzelne Bereiche schützen mit `class="notranslate"`

Der gängigste und von Google etablierte Weg, um bestimmte Teile deiner Seite vor der Übersetzung zu schützen, ist die Verwendung der CSS-Klasse `notranslate`. Der Name ist hier Programm. Jeder Text innerhalb eines Elements mit dieser Klasse wird vom Übersetzungsdienst ignoriert.

Das ist besonders nützlich für:
-   **Marken- und Firmennamen:** Dein Firmenname sollte immer gleich bleiben.
-   **Produktnamen:** Damit „MacBook Pro“ nicht zu „Mohnbuch Profi“ wird.
-   **Code-Beispiele:** `<div>` oder `console.log()` dürfen auf keinen Fall übersetzt werden.
-   **Fachbegriffe:** Wenn du einen englischen Fachbegriff bewusst im deutschen Text verwendest.

So wendest du es an:

```html
<p>
  Unsere Firma, die <span class="notranslate">FutureWeb AG</span>, entwickelt die
  Software <span class="notranslate">ConnectSphere</span>.
</p>

<p>
  Um zu beginnen, gib einfach folgenden Befehl in dein Terminal ein:
  <code class="notranslate">npm install @futureweb/connectsphere</code>
</p>

<pre class="notranslate"><code>
function sayHello() {
  console.log("Hello, World!");
}
</code></pre>
```

Im obigen Beispiel werden die Namen „FutureWeb AG“ und „ConnectSphere“ sowie der gesamte Code-Block von der Übersetzung ausgeschlossen. Der restliche Text wird wie gewohnt übersetzt, was zu einem viel besseren und verständlicheren Ergebnis führt.

##### Die ganze Seite sperren mit einem Meta-Tag

In manchen Fällen möchtest du vielleicht die automatische Übersetzung für eine komplette Seite unterbinden. Das kann sinnvoll sein, wenn:
-   Die Seite bewusst mehrsprachig ist (z.B. ein Artikel, der deutsche und englische Zitate nebeneinanderstellt).
-   Die Seite eine Sprachlernplattform ist, auf der der Originaltext entscheidend ist.
-   Die Inhalte so technisch oder rechtlich sensibel sind, dass jede Form der maschinellen Übersetzung ein Risiko darstellt.

Dafür kannst du ein spezielles `meta`-Tag im `<head>` deiner HTML-Datei platzieren. Um die Übersetzung durch Google-Dienste (die in Chrome, Android etc. integriert sind) zu verhindern, lautet das Tag:

```html
<head>
  <meta name="google" content="notranslate">
</head>
```
Diese Anweisung ist eine klare Botschaft an den Browser: „Finger weg, diese Seite soll so angezeigt werden, wie sie ist.“ Andere Übersetzungsdienste haben möglicherweise eigene Meta-Tags, aber da Google Chrome der am weitesten verbreitete Browser ist, deckst du hiermit den wichtigsten Anwendungsfall ab.

#### Strategischer Umgang mit automatischer Übersetzung

Automatische Übersetzung ist kein Ersatz für eine professionelle Lokalisierung. Wenn du einen globalen Markt ernsthaft bedienen willst, führt kein Weg an professionell übersetzten und kulturell angepassten Versionen deiner Webseite vorbei, die du über `hreflang`-Tags verknüpfst.

Sieh die automatische Übersetzung stattdessen als das, was sie ist: ein mächtiges Werkzeug zur Verbesserung der Zugänglichkeit. Deine Aufgabe als Entwickler ist es, eine Brücke zu bauen. Sorge dafür, dass dieses Werkzeug so gut wie möglich funktioniert und so wenig Schaden wie möglich anrichtet.

Deine Checkliste sollte daher immer lauten:
1.  **Setze das `lang`-Attribut immer korrekt.** Das ist die Basis für alles.
2.  **Identifiziere kritische Inhalte.** Markennamen, Code, Fachjargon – alles, was nicht oder falsch übersetzt werden darf.
3.  **Schütze diese Inhalte gezielt** mit `class="notranslate"`.
4.  **Nutze das `meta`-Tag zur Deaktivierung nur dann**, wenn es wirklich notwendig ist, um die Funktion oder den Sinn deiner Seite zu erhalten.

Indem du die automatische Übersetzung nicht ignorierst, sondern aktiv gestaltest, verbesserst du die User Experience für ein globales Publikum und schützt gleichzeitig die Integrität und Professionalität deiner Inhalte.
