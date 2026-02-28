# WHATWG und HTML Living Standard

### Die lebendige Sprache des Webs: WHATWG und der HTML Living Standard

Stell dir vor, du befindest dich in den frühen 2000er Jahren. Das World Wide Web ist noch jung, wild und chaotisch. Die "Browserkriege" zwischen Netscape Navigator und dem Internet Explorer haben tiefe Spuren hinterlassen. Webentwickler kämpfen täglich mit den Eigenheiten und Inkompatibilitäten der verschiedenen Browser. Der offizielle Standard für die Struktur von Webseiten ist zu dieser Zeit HTML 4.01, veröffentlicht im Jahr 1999 vom World Wide Web Consortium (W3C), dem Gremium, das seit seiner Gründung durch Tim Berners-Lee die Webstandards hütet.

Doch das W3C hatte Pläne, die viele in der Web-Community beunruhigten. Die Zukunft sollte nicht HTML heißen, sondern XHTML 2.0. XHTML war der Versuch, HTML in die strikte, regelbasierte Welt von XML zu überführen. Jedes Tag musste perfekt geschlossen, alles kleingeschrieben und nach strengen Regeln formatiert sein. Ein einziger Fehler konnte dazu führen, dass die gesamte Seite im Browser nicht mehr angezeigt wurde. Während XHTML 1.0 noch eine Brücke von HTML 4 baute, war die Vision für XHTML 2.0 radikal: Es sollte nicht mehr abwärtskompatibel sein. Das bedeutete, dass Millionen von bestehenden Webseiten, die nach den lockeren Regeln von HTML geschrieben waren, mit diesem neuen Standard nicht mehr funktioniert hätten. Ein Bruch mit der Vergangenheit.

#### Die Rebellion der Praktiker

Während das W3C an dieser akademisch reinen, aber für die Praxis untauglichen Zukunft arbeitete, wuchs der Frust bei denjenigen, die das Web tagtäglich bauten: den Browser-Herstellern. Unternehmen wie Apple (mit Safari), die Mozilla Foundation (mit Firefox) und Opera sahen, wie das W3C sich von den realen Bedürfnissen der Entwickler und Nutzer entfernte. Sie sahen, dass das Web nicht nach starren, fehlerintoleranten Regeln funktionierte. Es brauchte eine Sprache, die mit der Realität des unperfekten, aber funktionierenden Internets umgehen konnte. Sie wollten HTML nicht ersetzen, sondern es weiterentwickeln und um die Funktionen erweitern, die für moderne Webanwendungen dringend benötigt wurden – bessere Formulare, die Einbettung von Video und Audio ohne Plugins und vieles mehr.

Im Jahr 2004 zogen sie die Konsequenzen. Auf einem W3C-Workshop wurde ihr Vorschlag, HTML pragmatisch weiterzuentwickeln, abgelehnt. Noch am selben Tag gründeten Mitarbeiter von Apple, Mozilla und Opera eine eigene Interessengruppe: die **WHATWG (Web Hypertext Application Technology Working Group)**. Ihr Ziel war kühn und direkt: Sie würden einen neuen HTML-Standard schaffen, der auf den Realitäten des Webs basiert und nicht auf theoretischen Idealen.

#### Eine neue Philosophie: Pragmatismus statt Perfektion

Die WHATWG verfolgte von Anfang an fundamental andere Prinzipien als das W3C zu jener Zeit. Diese Prinzipien prägen die Entwicklung von HTML bis heute:

1.  **Abwärtskompatibilität ist heilig:** Das Web darf nicht kaputtgehen. Jeder neue Standard muss so gestaltet sein, dass alte Webseiten weiterhin wie gewohnt funktionieren. Der Bruch, den XHTML 2.0 bedeutet hätte, war für die WHATWG undenkbar.

2.  **Pflastere die Trampelpfade ("Pave the Cowpaths"):** Statt Entwicklern vorzuschreiben, wie sie zu arbeiten haben, schaute die WHATWG darauf, was Entwickler bereits taten. Wenn viele Entwickler ein Problem auf eine bestimmte, inoffizielle Weise lösten (z. B. durch die Verwendung von `<div>`-Elementen für Buttons), sollte der Standard eine offizielle, semantisch korrekte Lösung dafür anbieten (wie das `<button>`-Element). Man beobachtet das Verhalten der Nutzer (der "Kühe") und baut dann eine befestigte Straße (den "Standard") dort, wo sie ohnehin schon entlanglaufen.

3.  **Detaillierte Fehlerbehandlung definieren:** Eines der größten Probleme der frühen Webentwicklung war, dass jeder Browser anders mit fehlerhaftem HTML-Code umging. Der eine zeigte die Seite trotzdem an, der andere verschluckte Inhalte, der dritte stürzte vielleicht sogar ab. Die WHATWG machte es sich zur Aufgabe, im Standard exakt zu definieren, wie ein Browser auf *jeden* denkbaren Fehler reagieren muss. Das Ergebnis: Ein fehlerhafter Code führt heute in allen modernen Browsern zu einem nahezu identischen Ergebnis. Diese Präzision machte die Webentwicklung unendlich viel berechenbarer und stabiler.

4.  **Fokus auf Webanwendungen:** Der Name der Gruppe war Programm. Es ging nicht mehr nur um statische Dokumente, sondern um komplexe, interaktive Anwendungen im Browser. Neue Elemente wie `<video>`, `<audio>`, `<canvas>` (für 2D-Zeichnungen) oder die vielen neuen Formular-Input-Typen (wie `date`, `email`, `range`) waren direkte Ergebnisse dieses Fokus.

#### Die Geburt des "Living Standard"

Während das W3C in Versionen dachte (HTML 4, XHTML 1.0, XHTML 2.0), führte die WHATWG ein revolutionäres Konzept ein: den **HTML Living Standard**.

Die Idee dahinter ist einfach und genial zugleich. Das Web entwickelt sich so rasant, dass ein jahrelanger Prozess zur Verabschiedung einer neuen, statischen "Version" wie HTML5 oder HTML6 viel zu langsam ist. Stattdessen wird HTML als ein einziges, lebendiges Dokument betrachtet, das kontinuierlich aktualisiert wird. Fehler werden behoben, neue Features hinzugefügt und veraltete Dinge präzisiert, sobald sie ausgereift und von den Browsern implementiert sind.

Es gibt also keine Version "HTML6" mehr, und eigentlich ist auch "HTML5" nur noch ein historischer Begriff für den großen Sprung, den die WHATWG initiiert hat. Wenn du heute von HTML sprichst, meinst du den HTML Living Standard. Es ist einfach nur "HTML".

Dieser Ansatz hat massive Vorteile:
*   **Geschwindigkeit:** Neue, nützliche Features können viel schneller standardisiert und für alle verfügbar gemacht werden.
*   **Stabilität:** Der Standard reflektiert immer den aktuellen Stand der Technik in den Browsern. Es gibt keine Verwirrung mehr darüber, welche "Version" denn nun die richtige ist.
*   **Klarheit:** Es gibt nur eine einzige, maßgebliche Quelle der Wahrheit: die Spezifikation auf **html.spec.whatwg.org**. Das ist die Lektüre, an der sich alle Browser-Hersteller orientieren.

Ein wunderbares Beispiel für diesen evolutionären Prozess sind die Elemente `<details>` und `<summary>`, mit denen du aufklappbare Inhaltsbereiche ("Akkordeons") nativ und ohne eine einzige Zeile JavaScript erstellen kannst.

```html
<details>
  <summary>Kapitel 1: Die Anfänge des Webs</summary>
  <p>
    In diesem Abschnitt erfährst du mehr über die Erfindung des World Wide Web
    durch Tim Berners-Lee am CERN.
  </p>
</details>
<details>
  <summary>Kapitel 2: Die Browserkriege</summary>
  <p>
    Eine turbulente Zeit, geprägt vom Wettstreit zwischen Netscape und Microsoft.
  </p>
</details>
```

Solche Elemente wurden dem Standard hinzugefügt, lange nachdem der Begriff "HTML5" populär wurde. Sie sind einfach Teil des lebendigen HTML.

#### Die Einigung: Ein Standard, um sie alle zu einen

Was geschah nun mit dem W3C? Sie erkannten, dass das XHTML-2.0-Projekt in eine Sackgasse führte und die Arbeit der WHATWG die eigentliche Zukunft des Webs darstellte. Im Jahr 2007 gaben sie ihre Arbeit an XHTML 2.0 auf und beschlossen, die Arbeit der WHATWG als Grundlage für ihren eigenen "HTML5"-Standard zu nutzen.

Für einige Jahre arbeiteten beide Gruppen parallel, was zu einiger Verwirrung führte. Das W3C veröffentlichte periodische "Schnappschüsse" des Standards (HTML 5.0, 5.1, 5.2), während die WHATWG kontinuierlich an ihrem Living Standard weiterarbeitete. Es gab zwei konkurrierende HTML-Spezifikationen.

Dieses Tauziehen fand 2019 ein offizielles Ende. Das W3C und die WHATWG unterzeichneten eine Vereinbarung, die die Situation endgültig klärte: Der **HTML Living Standard der WHATWG ist der alleinige, definitive HTML-Standard**. Das W3C wird keine eigene Version mehr entwickeln, sondern seine Energie darauf konzentrieren, die Arbeit der WHATWG zu überprüfen und als offizielle "W3C Recommendation" zu veröffentlichen.

Für dich als Webentwickler bedeutet das eine enorme Erleichterung. Die Grabenkämpfe sind vorbei. Es gibt nur noch eine maßgebliche Quelle für HTML. Wenn du wissen willst, wie ein Element funktioniert oder was die neueste, beste Methode ist, um etwas umzusetzen, ist die Spezifikation der WHATWG deine erste Anlaufstelle.

Die stille Revolution der Praktiker hatte Erfolg. Sie haben HTML gerettet, indem sie es aus dem Elfenbeinturm der reinen Theorie befreit und es zu dem gemacht haben, was es heute ist: eine robuste, pragmatische und sich ständig weiterentwickelnde Sprache für das lebendige, atmende und manchmal auch ein wenig chaotische World Wide Web.
