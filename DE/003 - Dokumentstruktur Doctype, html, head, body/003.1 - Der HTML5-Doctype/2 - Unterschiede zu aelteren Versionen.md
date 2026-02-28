# Unterschiede zu älteren Versionen

### Unterschiede zu älteren Versionen

Wenn du heute eine HTML-Datei erstellst, ist die erste Zeile, die du schreibst, fast schon ein Reflex: `<!DOCTYPE html>`. Sie ist kurz, prägnant und leicht zu merken. Doch dieser einfache Startpunkt war nicht immer so unkompliziert. Um die Genialität und die Bedeutung dieses simplen Befehls wirklich zu verstehen, müssen wir eine kleine Zeitreise in die Ära vor HTML5 unternehmen. Du wirst schnell sehen, dass der Doctype eine Geschichte von Komplexität, strengen Regeln und einer schlussendlichen Befreiung erzählt.

#### Die Welt vor HTML5: Ein Dschungel aus DTDs

Vor HTML5 basierte HTML auf SGML (Standard Generalized Markup Language), einer sehr formalen und komplexen Metasprache zur Definition von Auszeichnungssprachen. Das bedeutet, HTML war nicht eigenständig, sondern eine „Anwendung“ von SGML. Damit ein Browser verstehen konnte, nach welchen genauen Regeln dein HTML-Code strukturiert war, musste ihm dies explizit mitgeteilt werden.

Diese Mitteilung erfolgte über die „Document Type Definition“ (DTD). Die DTD war im Grunde eine Art Grammatik- und Regelbuch für die jeweilige HTML-Version. Der Doctype am Anfang deines Dokuments war der Verweis auf dieses Regelbuch. Und diese Verweise waren alles andere als kurz und einprägsam. Sie waren lange, kryptische Zeichenketten, die man sich unmöglich merken konnte und meist aus Vorlagen kopierte.

Schauen wir uns einige der häufigsten Doctypes aus der Vergangenheit an, um den Unterschied greifbar zu machen.

**HTML 4.01 Strict**

Der „Strict“-Doctype war der Favorit von Webentwicklern, die auf sauberen, semantischen und zukunftssicheren Code setzten. Er verbot veraltete, sogenannte „präsentationsbezogene“ Tags wie `<font>` oder Attribute wie `align`. Die Struktur sollte strikt vom Design (das in CSS ausgelagert wurde) getrennt werden.

So sah der Doctype dafür aus:

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```

Lass uns das kurz aufschlüsseln:
*   `<!DOCTYPE HTML ...>`: Dies deklariert den Dokumententyp als HTML.
*   `PUBLIC`: Gibt an, dass die DTD öffentlich zugänglich ist.
*   `"-//W3C//DTD HTML 4.01//EN"`: Dies ist der sogenannte „Formal Public Identifier“ (FPI), eine eindeutige, maschinenlesbare Kennung für das Regelwerk.
*   `"http://www.w3.org/TR/html4/strict.dtd"`: Das ist die URL, unter der die DTD-Datei tatsächlich zu finden war. Der Browser konnte (theoretisch) diese Datei abrufen, um die Validierungsregeln zu laden.

**HTML 4.01 Transitional**

Dieser Doctype war sozusagen die „entspanntere“ Variante. Er wurde eingeführt, um den Übergang von älteren Webseitenpraktiken zu den neuen Standards zu erleichtern. Er erlaubte weiterhin die Nutzung von veralteten Tags und Attributen, die in der Strict-Version bereits verboten waren. Viele Entwickler nutzten ihn aus Bequemlichkeit oder weil sie mit alten Codebasen arbeiten mussten.

Der Doctype war ähnlich lang, verwies aber auf eine andere DTD:

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
```

Der entscheidende Unterschied liegt im Detail: `Transitional` statt `Strict` und `loose.dtd` statt `strict.dtd`.

**XHTML 1.0 Strict**

Um die Verwirrung komplett zu machen, kam um die Jahrtausendwende XHTML (Extensible HyperText Markup Language) auf. XHTML war im Grunde HTML, das nach den strengeren Regeln von XML formuliert wurde. Das bedeutete: Alle Tags mussten klein geschrieben werden, alle Tags mussten geschlossen werden (also `<br>` wurde zu `<br />`) und Attributwerte mussten immer in Anführungszeichen stehen.

Der Doctype für XHTML 1.0 Strict war noch einmal eine Spur länger und komplizierter:

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

Du siehst das Muster: Jede Variante von HTML hatte ihren eigenen, furchtbar langen und fehleranfälligen Doctype. Die Wahl des richtigen Doctypes war wichtig, denn er entschied darüber, in welchem Modus der Browser die Seite darstellte. Ein fehlender oder falscher Doctype konnte den Browser in den sogenannten „Quirks Mode“ versetzen, einen Kompatibilitätsmodus, der versuchte, das fehlerhafte Layout alter Webseiten nachzuahmen – was oft zu unvorhersehbarem und inkonsistentem Verhalten führte. Ziel war es immer, den „Standards Mode“ zu aktivieren, und dafür war einer dieser langen Doctypes notwendig.

#### Die Revolution: Der HTML5-Doctype

Und dann kam HTML5. Mit HTML5 wurde eine der größten Hürden für Einsteiger und eine der nervigsten Formalien für Profis einfach aus dem Weg geräumt. Der neue Doctype lautet, wie du weißt:

```html
<!DOCTYPE html>
```

Das ist alles. Keine PUBLIC-Kennung, kein Verweis auf eine externe DTD-URL, keine Versionsnummer. Aber warum ist das so? Warum konnte man plötzlich auf all diese Informationen verzichten?

Die Antwort liegt in einem fundamentalen Wandel in der Philosophie von HTML. HTML5 ist nicht länger eine Anwendung von SGML. HTML5 ist sein eigener, klar definierter Standard. Die Entwickler der Spezifikation haben erkannt, dass Browser in der Praxis sowieso nie die DTDs heruntergeladen haben, um den Code zu validieren. Stattdessen haben sie über die Jahre eigene, auf Fehler-Toleranz ausgelegte Parser entwickelt.

Der HTML5-Standard wurde also pragmatisch geschrieben: Er beschreibt exakt, wie ein Browser HTML-Code verarbeiten soll, inklusive des Umgangs mit Fehlern. Er braucht kein externes Regelbuch mehr, weil die Regeln nun fester Bestandteil des Standards selbst sind.

Der Doctype in HTML5 hat daher nur noch einen einzigen, entscheidenden Zweck: Er ist ein Schalter. Sobald ein Browser `<!DOCTYPE html>` am Anfang einer Datei liest, weiß er: „Aha, das ist eine moderne Webseite. Ich aktiviere meinen standardkonformen Rendering-Modus und interpretiere alles Folgende nach den aktuellen HTML5-Regeln.“

Er ist also kein Verweis mehr, sondern ein Signal.

#### Was sich dadurch in der Praxis änderte

Diese Vereinfachung war mehr als nur eine kosmetische Korrektur. Sie hatte tiefgreifende, positive Auswirkungen auf die Webentwicklung:

1.  **Keine Verwirrung mehr:** Du musst nicht mehr zwischen Strict, Transitional oder Frameset wählen. Es gibt nur noch *ein* HTML. Das macht den Einstieg leichter und beseitigt eine unnötige Fehlerquelle.
2.  **Pragmatismus statt Dogma:** Der HTML5-Doctype ist das Symbol für die gesamte Philosophie von HTML5. Statt sich an akademischen, theoretischen Definitionen (wie SGML) zu orientieren, konzentriert sich der Standard auf die realen Bedürfnisse und Praktiken von Entwicklern und Browsern.
3.  **Geniale Abwärtskompatibilität:** Die Form `<!DOCTYPE html>` wurde clever gewählt. Auch ältere Browser, die HTML5 noch nicht kannten, interpretieren diese Zeile korrekt als Anweisung, in den „Standards Mode“ zu wechseln. Sie wussten zwar nichts von den neuen HTML5-Elementen wie `<main>` oder `<nav>`, aber sie versuchten zumindest, das CSS und die grundlegende Struktur korrekt darzustellen. Dies sorgte für einen nahtlosen Übergang, ohne das halbe Internet lahmzulegen.

Der Wandel vom komplexen DTD-Verweis zum einfachen `<!DOCTYPE html>` ist also weit mehr als nur eine Vereinfachung der Syntax. Er markiert den Punkt, an dem HTML erwachsen wurde – sich von seinen akademischen Wurzeln löste und zu einem praktischen, lebendigen Standard wurde, der für das moderne Web gemacht ist. Wenn du heute diese eine Zeile schreibst, tust du das also auf den Schultern von Giganten – und profitierst von einer der besten Entscheidungen in der Geschichte des Webs.
