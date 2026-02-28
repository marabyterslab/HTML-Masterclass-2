# WHATWG und HTML Living Standard

### WHATWG und der HTML Living Standard: Die Revolution der ständigen Erneuerung

Um die heutige Webentwicklung zu verstehen, müssen wir eine Geschichte von Meinungsverschiedenheiten, pragmatischen Entscheidungen und einer grundlegenden Veränderung in der Philosophie der Standardisierung erzählen. Es ist die Geschichte, wie HTML aufhörte, eine nummerierte Version zu sein, und zu einem lebendigen, sich ständig weiterentwickelnden Standard wurde. Im Zentrum dieser Geschichte steht eine Gruppe namens WHATWG.

#### Der Bruch mit der Vergangenheit: XHTML 2.0 und die Unzufriedenheit

Stell dir die Welt des Webs um das Jahr 2004 vor. Das World Wide Web Consortium (W3C), die bis dahin unangefochtene Autorität für Webstandards, hatte große Pläne. Nach dem Erfolg von HTML 4 und der Einführung von XHTML 1.0, einer strengeren, XML-basierten Version von HTML, arbeitete das W3C an der nächsten großen Sache: XHTML 2.0.

Doch dieser geplante Nachfolger war radikal anders. Er war nicht abwärtskompatibel. Das bedeutet, dass Webseiten, die für frühere HTML-Versionen geschrieben wurden, unter XHTML 2.0 nicht mehr funktioniert hätten. Der Standard war auf eine akademische Reinheit und strikte XML-Konformität ausgelegt. Ein einziger kleiner Fehler im Code, wie ein nicht geschlossenes Tag, und die Seite würde dem Besucher im Browser eine unschöne Fehlermeldung präsentieren, anstatt einfach das Beste daraus zu machen und den Inhalt so gut wie möglich darzustellen.

Diese Vision stieß bei denjenigen auf großen Widerstand, die das Web tagtäglich bauten und nutzten: die Browserhersteller. Firmen wie Apple (mit Safari), die Mozilla Foundation (mit Firefox) und Opera sahen, dass die Richtung des W3C nicht mit der Realität des Webs übereinstimmte. Das Web war unordentlich, voller kleiner Fehler, und die Browser waren seit jeher darauf ausgelegt, tolerant zu sein und fehlerhaften Code so gut wie möglich zu interpretieren. XHTML 2.0 fühlte sich an wie ein Rückschritt in eine weniger benutzer- und entwicklerfreundliche Welt.

#### Die Geburt der WHATWG

Im Jahr 2004, während eines Workshops des W3C, trafen die unterschiedlichen Philosophien aufeinander. Die Browserhersteller schlugen eine sanftere Weiterentwicklung des bestehenden HTML vor, die neue Funktionen für Web-Anwendungen hinzufügen und gleichzeitig abwärtskompatibel bleiben sollte. Ihre Vorschläge wurden jedoch abgelehnt. Das W3C wollte an seinem Kurs mit XHTML 2.0 festhalten.

Die Reaktion der enttäuschten Browserhersteller war entscheidend für die Zukunft des Webs. Statt sich dem Diktat des W3C zu beugen, gründeten sie ihre eigene Organisation: die **Web Hypertext Application Technology Working Group**, kurz **WHATWG**. Ihr Ziel war klar formuliert: Sie wollten einen Webstandard entwickeln, der sich an den praktischen Bedürfnissen von Entwicklern, Browserherstellern und Nutzern orientiert – nicht an theoretischer Perfektion.

Die Gründungsprinzipien der WHATWG standen im direkten Gegensatz zur damaligen W3C-Philosophie:

1.  **Rückwärtskompatibilität als oberstes Gebot:** Das bestehende Web durfte nicht kaputtgehen. Neue Features sollten das vorhandene HTML erweitern, nicht ersetzen.
2.  **Pragmatismus statt Purismus:** Anstatt Regeln vorzuschreiben, wie das Web sein *sollte*, analysierte die WHATWG, wie Entwickler das Web *tatsächlich* nutzten. Sie standardisierten gängige, aber bisher nicht offizielle Praktiken und schufen Lösungen für reale Probleme. Das Motto lautete sinngemäß: „Pflastere die Trampelpfade“ („Pave the cowpaths“).
3.  **Detaillierte Spezifikationen für Browser:** Der neue Standard sollte nicht nur definieren, wie korrekter Code aussieht, sondern auch exakt vorschreiben, wie Browser mit fehlerhaftem Code umgehen müssen. Dies sollte sicherstellen, dass eine Webseite in allen Browsern möglichst identisch dargestellt wird, selbst wenn der Code nicht perfekt ist.
4.  **Fokus auf Web-Applikationen:** Der Name der Gruppe verrät es bereits. Es ging nicht mehr nur darum, statische Dokumente zu strukturieren, sondern darum, eine robuste Plattform für komplexe, interaktive Anwendungen direkt im Browser zu schaffen. Dies führte zur Entwicklung von heute selbstverständlichen Elementen wie `<video>`, `<audio>`, `<canvas>` und verbesserten Formular-Elementen.

#### HTML5: Zwei Standards, eine Richtung

Die WHATWG begann ihre Arbeit an Spezifikationen, die sie zunächst „Web Applications 1.0“ und „Web Forms 2.0“ nannten. Diese Arbeiten bildeten die Grundlage für das, was wir bald als **HTML5** kennenlernen sollten.

Während die WHATWG mit ihrer pragmatischen Herangehensweise schnell an Fahrt gewann und die Unterstützung der Entwicklergemeinde fand, geriet das XHTML-2.0-Projekt des W3C ins Stocken. Es wurde immer deutlicher, dass die Zukunft des Webs nicht in einem radikalen Bruch, sondern in der evolutionären Weiterentwicklung von HTML lag.

Schließlich vollzog das W3C eine Kehrtwende. 2007 kündigten sie an, ebenfalls an einer HTML5-Spezifikation zu arbeiten und nahmen die Arbeit der WHATWG als Grundlage dafür. Die Entwicklung von XHTML 2.0 wurde 2009 offiziell eingestellt.

Für einige Jahre gab es nun eine etwas verwirrende Situation: Sowohl das W3C als auch die WHATWG veröffentlichten HTML5-Spezifikationen. Während das W3C weiterhin dem Modell von versionierten „Snapshots“ folgte (HTML5, dann HTML 5.1, HTML 5.2), verfolgte die WHATWG eine radikal neue Idee: den **Living Standard**.

#### Der HTML Living Standard: Ein Paradigmenwechsel

Die WHATWG argumentierte, dass das Web sich zu schnell entwickelt, um es in starre Versionen zu pressen. Ein Standard, der alle paar Jahre aktualisiert wird, ist in dem Moment, in dem er veröffentlicht wird, bereits wieder veraltet.

Ihre Lösung war der **HTML Living Standard**. Stell es dir nicht wie ein Buch vor, das alle paar Jahre in einer neuen Auflage erscheint. Stell es dir eher wie ein ständig aktualisiertes Online-Lexikon vor. HTML ist niemals "fertig". Es ist ein lebendiges Dokument, das kontinuierlich verbessert und erweitert wird.

*   **Keine Versionsnummern mehr:** Es gibt kein HTML6, HTML7 oder HTML8. Es gibt nur noch "HTML". Wenn du heute HTML lernst, lernst du den aktuellen Stand des Living Standards.
*   **Kontinuierliche Updates:** Änderungen, Korrekturen und neue Features werden über einen transparenten Prozess (oft über Plattformen wie GitHub) vorgeschlagen, diskutiert und bei Zustimmung direkt in den Standard integriert.
*   **Browser als treibende Kraft:** Da die Browserhersteller die treibende Kraft hinter der WHATWG sind, kannst du davon ausgehen, dass die im Standard beschriebenen Features auch tatsächlich in den Browsern implementiert werden (oder es bereits sind). Der Standard dokumentiert die lebendige Realität des Webs.

#### Die Einigung und die heutige Situation

Die Koexistenz von zwei konkurrierenden HTML-Spezifikationen führte zu Verwirrung. Welche war die "richtige"? Auf welche sollte man sich verlassen?

Diese unklare Situation endete im Mai 2019. In einer historischen Vereinbarung (einem "Memorandum of Understanding") erkannten das W3C und die WHATWG an, dass die Entwicklung von HTML und DOM (Document Object Model) unter dem Dach der WHATWG stattfinden sollte.

Seitdem ist der **WHATWG HTML Living Standard die alleinige, maßgebliche Quelle für den HTML-Standard**. Das W3C hat seine eigene Version eingestellt und beteiligt sich nun am Prozess der WHATWG, indem es den Standard prüft und als offizielle Empfehlung ("W3C Recommendation") veröffentlicht.

Für dich als Entwickler bedeutet das vor allem eines: Klarheit und Stabilität. Wenn du wissen willst, was aktuelles HTML ist, gibt es nur noch eine Anlaufstelle: den Living Standard der WHATWG. Ressourcen wie das Mozilla Developer Network (MDN) orientieren sich eng an diesem Standard und sind deine verlässlichsten Quellen im Entwickleralltag.

Die Geschichte der WHATWG ist mehr als nur eine Anekdote aus der Webgeschichte. Sie markiert den Sieg des Pragmatismus über die Theorie und etablierte ein agiles, kollaboratives Modell für die Standardisierung, das der rasanten Entwicklung des Webs gerecht wird. Dank dieser Revolution musst du dir heute keine Gedanken mehr über Versionsnummern machen. HTML ist einfach HTML – lebendig, atmend und immer im Wandel.
