# Korrekte Syntax

### Der HTML5-Doctype: Dein allererstes Statement

Jedes HTML-Dokument, das du schreibst, beginnt mit einer fundamentalen, nicht verhandelbaren Regel: Die allererste Zeile muss die Dokumenttyp-Deklaration enthalten, kurz Doctype genannt. Bevor der Browser auch nur ein einziges deiner liebevoll gestalteten `<p>`- oder `<div>`-Tags liest, muss er wissen, mit welcher Art von Dokument er es zu tun hat. Der Doctype ist wie eine Gebrauchsanweisung, die du dem Browser reichst, noch bevor er die Schachtel öffnet.

Für modernes HTML, also HTML5, ist diese Anweisung erfrischend einfach und prägnant:

```html
<!DOCTYPE html>
```

Das ist alles. Diese eine Zeile, genau so geschrieben, ist der Schlüssel, der dem Browser signalisiert: „Achtung, was jetzt kommt, ist ein HTML5-Dokument. Bitte aktiviere deinen modernsten Interpretationsmodus und halte dich an die aktuellen Webstandards.“

#### Warum diese eine Zeile so entscheidend ist

Man könnte meinen, eine so kurze Zeichenfolge sei nur eine Formalität. In Wahrheit ist sie das Fundament für eine konsistente und vorhersagbare Darstellung deiner Webseite in allen modernen Browsern. Ihre wichtigste Aufgabe ist es, den sogenannten **Standardmodus** (Standards Mode) des Browsers zu aktivieren.

Um das zu verstehen, müssen wir einen kleinen Ausflug in die wilde Vergangenheit des Webs machen. In den frühen Tagen gab es noch keine einheitlichen Regeln. Browserhersteller kochten oft ihr eigenes Süppchen, was dazu führte, dass eine Webseite im Netscape Navigator völlig anders aussah als im Internet Explorer. Webentwickler mussten unzählige Tricks und Hacks anwenden, um ihre Seiten halbwegs konsistent darzustellen.

Um dieses Chaos zu beenden, begannen Gremien wie das World Wide Web Consortium (W3C), verbindliche Standards zu definieren. Die Browser zogen nach, standen aber vor einem Problem: Was sollten sie mit all den alten Webseiten tun, die nach den alten, nicht standardkonformen Regeln geschrieben waren? Würde man sie plötzlich nach den neuen, strengen Regeln interpretieren, würden Millionen von Seiten einfach kaputtgehen.

Die Lösung war die Einführung von zwei verschiedenen Darstellungsmodi (Rendering Modes):

1.  **Der Kompatibilitätsmodus (Quirks Mode):** Ein Rückwärtskompatibilitätsmodus, der das fehlerhafte und inkonsistente Verhalten alter Browser aus den 90er-Jahren imitiert. Er wird aktiviert, wenn ein Doctype fehlt oder veraltet und fehlerhaft ist. In diesem Modus versucht der Browser zu raten, was der Entwickler gemeint haben könnte – mit oft katastrophalen und unvorhersehbaren Ergebnissen. Layouts verhalten sich seltsam, CSS-Regeln werden falsch interpretiert und JavaScript kann auf unerwartete Weise mit dem Dokument interagieren. Der Quirks Mode ist der Feind jedes modernen Webentwicklers.

2.  **Der Standardmodus (Standards Mode):** Dieser Modus wird durch einen korrekten, modernen Doctype – wie `<!DOCTYPE html>` – aktiviert. Hier hält sich der Browser so eng wie möglich an die offiziellen HTML- und CSS-Spezifikationen. Das Ergebnis ist eine vorhersagbare, stabile und interoperable Darstellung über verschiedene Browser und Geräte hinweg. Du schreibst deinen Code nach den Regeln, und der Browser verspricht, ihn ebenfalls nach den Regeln zu interpretieren.

Die Deklaration `<!DOCTYPE html>` ist also dein unmissverständliches Kommando an den Browser, den Quirks Mode zu meiden und direkt in den verlässlichen Standardmodus zu wechseln. Lässt du sie weg, überlässt du die Darstellung deiner Seite dem Zufall.

#### Die Anatomie der Deklaration

Obwohl der HTML5-Doctype so kurz ist, folgt seine Syntax einem historischen Muster. Schauen wir uns die Bestandteile genauer an:

*   **`<! ... >`**: Die spitzen Klammern mit dem Ausrufezeichen am Anfang signalisieren, dass es sich hier nicht um ein normales HTML-Tag handelt, sondern um eine besondere Anweisung oder Deklaration für den Parser des Browsers.
*   **`DOCTYPE`**: Dieses Schlüsselwort steht für „Document Type Declaration“. Es ist historisch bedingt und bei der HTML5-Version ist die Großschreibung eine weitverbreitete Konvention, obwohl der Doctype selbst nicht case-sensitive ist. `<!doctype html>` wäre technisch ebenfalls gültig. Die Großschreibung verbessert jedoch die Lesbarkeit und hebt den besonderen Charakter der Anweisung hervor.
*   **`html`**: Dieser Teil gibt den Typ des Wurzelelements des Dokuments an. In unserem Fall ist das schlicht `<html>`.

Im Vergleich zu seinen Vorgängern ist dieser Doctype eine Offenbarung der Einfachheit. Frühere HTML- und XHTML-Versionen erforderten lange, kryptische Deklarationen, die auf eine sogenannte „Document Type Definition“ (DTD) verwiesen – eine externe Datei, die die exakten Grammatikregeln für diese spezielle HTML-Version definierte.

Hier nur als Beispiel, um den Unterschied zu würdigen, der Doctype für HTML 4.01 Strict:

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```

Und für XHTML 1.0 Strict:

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

Man musste sich nicht nur merken, welche dieser Deklarationen die richtige war, sondern auch sicherstellen, dass sie exakt kopiert wurde. Ein Tippfehler konnte bereits dazu führen, dass der Browser in den Quirks Mode zurückfiel.

HTML5 hat mit dieser Komplexität aufgeräumt. Es ist kein Teil einer spezifischen DTD mehr, sondern ein lebendiger Standard. Der Doctype `<!DOCTYPE html>` ist daher kein Verweis mehr, sondern einfach nur noch der Schalter, der den Standardmodus aktiviert. Er sagt dem Browser: „Benutze HTML, und zwar die modernste Version, die du kennst.“

#### Die unumstößliche Regel: Ganz an den Anfang

Die Position des Doctypes ist ebenso wichtig wie seine Anwesenheit. Er muss das **aller-, allererste** sein, was in deiner HTML-Datei steht. Es darf absolut nichts davor kommen: keine Leerzeichen, keine Kommentare, keine unsichtbaren Zeichen. Selbst ein einzelnes Leerzeichen vor `<!DOCTYPE html>` kann in manchen Browsern, insbesondere in älteren Versionen des Internet Explorers, dazu führen, dass die Seite in den Quirks Mode versetzt wird.

**Korrekt:**

```html
<!DOCTYPE html>
<html>
  <head>
    ...
  </head>
  <body>
    ...
  </body>
</html>
```

**Falsch:**

```html
<!-- Meine tolle Webseite -->
<!DOCTYPE html>
<html>
  ...
</html>
```

**Ebenfalls Falsch (mit einem Leerzeichen davor):**

```html
 <!DOCTYPE html>
<html>
  ...
</html>
```

Diese Regel ist absolut. Dein HTML-Dokument beginnt mit der linken spitzen Klammer von `<!DOCTYPE html>` in Zeile 1, Spalte 1. Dies ist eine der wenigen Stellen in der Webentwicklung, an denen es keine Flexibilität und keinen Interpretationsspielraum gibt. Es ist eine einfache, aber unverzichtbare Grundlage für jede moderne Webseite, die du erstellst. Betrachte es als das erste Versprechen, das du dem Browser gibst: Ich werde sauberen, standardkonformen Code schreiben. Im Gegenzug verspricht dir der Browser, sein Bestes zu tun, um diesen Code korrekt und konsistent darzustellen.
