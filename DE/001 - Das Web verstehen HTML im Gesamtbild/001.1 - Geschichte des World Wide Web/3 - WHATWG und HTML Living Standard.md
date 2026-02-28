# WHATWG und HTML Living Standard

### WHATWG und der HTML Living Standard: Eine stille Revolution

Stell dir vor, du bist im Internet der frühen 2000er Jahre. Das Web wächst explosionsartig, aber die Regeln, nach denen es gebaut wird, scheinen in der Zeit steckengeblieben zu sein. Die offizielle Hüterin der Webstandards, das World Wide Web Consortium (W3C), arbeitete an einer Zukunft, die für viele Entwickler und vor allem für die Macher der Webbrowser wie ein Irrweg aussah. Dieser Irrweg hieß XHTML 2.0.

#### Der Scheideweg: Strikte Regeln gegen gelebte Realität

Das W3C hatte eine Vision von einem sauberen, logischen und strengen Web. XHTML 2.0 sollte auf XML basieren, einer sehr rigiden Auszeichnungssprache. Das bedeutete: Jeder kleinste Fehler in deinem HTML-Code, etwa ein nicht geschlossenes Tag, hätte dazu geführt, dass der Browser die gesamte Seite nicht anzeigt. Einfach eine Fehlermeldung. Aus. Vorbei. Diese Vision war akademisch sauber, aber sie ignorierte eine fundamentale Eigenschaft des Webs: Es war und ist chaotisch.

Browser wie Internet Explorer, Firefox und Opera hatten über Jahre hinweg gelernt, mit fehlerhaftem HTML-Code umzugehen. Sie versuchten immer, das Beste aus dem zu machen, was sie bekamen, um dem Nutzer *irgendetwas* anzuzeigen. Dieser Ansatz, bekannt als "Fehlertoleranz", war entscheidend für den Erfolg des Webs. XHTML 2.0 wollte damit brechen. Es war nicht abwärtskompatibel, was bedeutet hätte, dass Millionen existierender Webseiten plötzlich veraltet oder sogar unbrauchbar geworden wären.

Die Entwickler der führenden Browser sahen diese Entwicklung mit großer Sorge. Sie sahen, dass die Bedürfnisse der Entwickler und Nutzer von den theoretischen Diskussionen des W3C abgekoppelt waren. Entwickler wollten keine strengeren Regeln, sie wollten neue, nützliche Funktionen: bessere Formulare, die Möglichkeit, Video und Audio direkt im Browser abzuspielen, und APIs, um komplexe Webanwendungen zu bauen, die sich wie Desktop-Programme anfühlten.

#### Die Gründung der WHATWG: Eine pragmatische Rebellion

Im Jahr 2004 zogen einige der wichtigsten Akteure die Konsequenzen. Mitarbeiter von Apple (zuständig für den Safari-Browser), der Mozilla Foundation (Firefox) und Opera Software (Opera-Browser) gründeten eine neue Arbeitsgruppe: die **Web Hypertext Application Technology Working Group**, kurz **WHATWG**.

Der Name war Programm. Es ging ihnen nicht primär um "Dokumente", wie es beim W3C der Fall war, sondern um "Web Applications" – also um dynamische, interaktive Anwendungen im Browser. Ihr Ziel war es, die Weiterentwicklung von HTML pragmatisch und nutzerorientiert voranzutreiben. Anstatt das Rad neu zu erfinden, wollten sie HTML so erweitern, wie es in der Praxis bereits verwendet wurde und neue, dringend benötigte Funktionen hinzufügen. Ihr Leitprinzip war die Abwärtskompatibilität. Nichts, was heute funktioniert, sollte morgen kaputt sein.

Die WHATWG begann ihre Arbeit an einer Spezifikation, die sie "HTML5" nannte (ein Name, der später noch für Verwirrung sorgen sollte) und parallel dazu an "Web Forms 2.0", um die unzureichenden Formular-Elemente von HTML4 zu verbessern.

#### Das Konzept des "Living Standard"

Das wirklich Revolutionäre an der Arbeitsweise der WHATWG war nicht nur, *was* sie entwickelten, sondern *wie* sie es taten. Anstelle des W3C-Modells, bei dem alle paar Jahre eine riesige, in Stein gemeißelte Version eines Standards (wie HTML 4.01 oder XHTML 1.0) verabschiedet wurde, führte die WHATWG das Konzept des **Living Standard** ein.

Ein Living Standard ist genau das, wonach es klingt: ein lebendiges Dokument, das sich kontinuierlich weiterentwickelt. Es gibt keine Versionsnummern wie HTML5, HTML6 oder HTML7 mehr. Es gibt nur noch "HTML". Die Spezifikation wird ständig durch kleine, inkrementelle Änderungen aktualisiert. Ein Fehler wird gefunden? Er wird korrigiert. Ein neues Feature wird von Browsern implementiert und von Entwicklern angenommen? Es wird in den Standard aufgenommen.

Stell es dir vor wie den Unterschied zwischen einer gedruckten Enzyklopädie und Wikipedia. Die Enzyklopädie wird alle paar Jahre neu aufgelegt und ist in der Zwischenzeit veraltet. Wikipedia wird in dem Moment aktualisiert, in dem neue Informationen verfügbar sind. Der HTML Living Standard ist die Wikipedia der Webentwicklung. Er ist immer auf dem neuesten Stand und spiegelt den aktuellen Konsens und die Implementierungen in den Browsern wider.

Dieser Prozess ist offen und getrieben von der Realität. Eine neue Idee wird diskutiert, experimentell in einem Browser implementiert, und wenn sie sich bewährt, findet sie ihren Weg in den Standard. Das stellt sicher, dass die Spezifikation nicht im luftleeren Raum entsteht, sondern die tatsächliche Funktionsweise des Webs beschreibt.

#### HTML5: Die Versöhnung und die Verwirrung

Die Arbeit der WHATWG war so überzeugend und praxisnah, dass das W3C schließlich einlenken musste. 2007 gab das Konsortium die Arbeit an XHTML 2.0 auf und entschied, die Arbeit der WHATWG als Grundlage für die nächste offizielle HTML-Version zu nutzen. Das war der Moment, in dem die "Rebellen" gewonnen hatten.

Jetzt arbeiteten beide Gruppen eine Zeit lang zusammen an dem, was die Welt als "HTML5" kennenlernte. Doch die unterschiedlichen Philosophien führten weiterhin zu Spannungen. Während die WHATWG ihren Living Standard kontinuierlich weiterpflegte, hielt das W3C am alten Modell fest und veröffentlichte 2014 eine "fertige" Empfehlung für "HTML 5.0", gefolgt von "HTML 5.1" und "HTML 5.2" in den Jahren danach.

Das sorgte für enorme Verwirrung. Welcher Standard galt nun? Der sich ständig ändernde "HTML Living Standard" der WHATWG oder die versionierten "HTML5.x"-Snapshots des W3C?

#### Die heutige Situation: Es gibt nur einen Standard

Diese unklare Situation endete erst 2019 mit einer historischen Einigung. Das W3C und die WHATWG unterzeichneten eine Vereinbarung, die die Rollen klar verteilt:

**Der HTML Living Standard der WHATWG ist der alleinige, maßgebliche und offizielle Standard für HTML und DOM.**

Das W3C hat seine eigene Version der HTML-Spezifikation eingestellt. Stattdessen veröffentlicht das W3C nun regelmäßig "Recommendations", die im Wesentlichen geprüfte Momentaufnahmen (Snapshots) des WHATWG Living Standards sind.

Für dich als Entwickler bedeutet das eine enorme Vereinfachung. Es gibt nur noch eine Quelle der Wahrheit, der du folgen musst. Wenn du wissen willst, was aktuelles, korrektes HTML ist, schaust du in den HTML Living Standard der WHATWG.

#### Was das für deine tägliche Arbeit bedeutet

Dieser Wandel von starren Versionen zu einem lebendigen Standard hat direkte Auswirkungen auf deine Arbeit:

1.  **Du schreibst einfach "HTML".** Du musst dir keine Gedanken machen, ob du für "HTML5" oder "HTML5.2" entwickelst. Du verwendest die Features, die im heutigen HTML-Standard definiert und von den Browsern, die du unterstützen möchtest, implementiert sind.

2.  **Der Doctype ist für immer einfach.** Der Grund, warum wir heute nur noch `<!DOCTYPE html>` an den Anfang unserer Dokumente schreiben, ist eine direkte Folge dieser Entwicklung. Dieser einfache Doctype sagt dem Browser schlicht: "Bitte rendere diese Seite im modernsten Standard-Modus, den du kennst." Er ist nicht an eine Version gebunden und wird sich wahrscheinlich nie wieder ändern.

    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <title>Ein modernes HTML-Dokument</title>
      </head>
      <body>
        <p>So einfach ist das.</p>
      </body>
    </html>
    ```

3.  **Features kommen und gehen fließend.** Neue HTML-Tags oder Attribute werden nicht mehr in großen Batches alle paar Jahre eingeführt. Sie werden hinzugefügt, sobald sie bereit sind. Deshalb ist es wichtig, Ressourcen wie das Mozilla Developer Network (MDN) oder caniuse.com zu nutzen, um zu prüfen, welche Browser ein bestimmtes neues Feature bereits unterstützen.

4.  **Abwärtskompatibilität ist heilig.** Das Kernprinzip der WHATWG sorgt dafür, dass dein heute geschriebener Code auch in zehn Jahren noch funktionieren wird. Die Weiterentwicklung des Webs geschieht durch Hinzufügen, nicht durch Wegnehmen.

Die Gründung der WHATWG und die Etablierung des HTML Living Standard waren mehr als nur ein technisches Detail in der Geschichte des Webs. Es war eine fundamentale Verschiebung hin zu einem pragmatischen, kollaborativen und entwicklerfreundlichen Prozess, der sicherstellt, dass sich HTML gemeinsam mit den realen Anforderungen des Internets weiterentwickelt.
