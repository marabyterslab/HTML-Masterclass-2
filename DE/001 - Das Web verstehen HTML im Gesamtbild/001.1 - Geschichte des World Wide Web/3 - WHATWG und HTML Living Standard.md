# WHATWG und HTML Living Standard

### WHATWG und der HTML Living Standard: Eine stille Revolution

Stell dir vor, du arbeitest an einem riesigen, weltweiten Projekt. Die Regeln dafür wurden vor Jahren in einem dicken Buch festgeschrieben. Jedes Mal, wenn eine neue Idee aufkommt, muss ein Komitee jahrelang diskutieren, um eine komplett neue Ausgabe dieses Buches zu veröffentlichen. In der Zwischenzeit hat sich die Welt aber schon weitergedreht. Klingt langsam und unpraktisch, oder? Genau das war lange Zeit die Realität für HTML. Doch dann kam eine Veränderung, die alles auf den Kopf stellte – und die bis heute deine tägliche Arbeit als Webentwickler prägt.

#### Der Bruch mit der Tradition: Warum eine Veränderung nötig war

Um zu verstehen, warum die WHATWG entstand, müssen wir einen kurzen Blick zurück in die frühen 2000er Jahre werfen. Das World Wide Web Consortium (W3C) war die unangefochtene Autorität für Webstandards. Nach dem Erfolg von HTML 4.01 richtete das W3C seinen Fokus auf XHTML, eine strengere, auf XML basierende Version von HTML. Die Vision war eine saubere, maschinenlesbare und fehlerfreie Web-Welt. Das nächste große Ding sollte XHTML 2.0 werden – ein Standard, der so radikal neu war, dass er nicht mehr abwärtskompatibel zum bestehenden HTML gewesen wäre. Webseiten, die nach altem Muster gebaut waren, hätten nicht mehr funktioniert.

Während das W3C diesen akademisch reinen, aber für die Praxis schwierigen Weg verfolgte, sahen die Menschen, die die Browser entwickelten, ein ganz anderes Bild. Sie sahen ein Web, das nicht aus perfekt strukturierten Dokumenten bestand, sondern aus dynamischen, interaktiven Anwendungen. Entwickler bauten mit JavaScript und cleveren Hacks Funktionen, für die HTML gar nicht gemacht war. Die Browserhersteller – allen voran Apple, Mozilla (Firefox) und Opera – erkannten, dass der Weg des W3C nicht die realen Bedürfnisse von Entwicklern und Nutzern widerspiegelte. Sie brauchten neue Elemente für Videos, Audio und interaktive Formulare, nicht strenge XML-Regeln, die bei kleinsten Fehlern die gesamte Seite lahmlegten.

Die Frustration wuchs. Im Jahr 2004 trafen sich Vertreter dieser Browserhersteller und gründeten eine eigene Gruppe: die **Web Hypertext Application Technology Working Group**, kurz **WHATWG**. Ihr Ziel war einfach und revolutionär zugleich: Sie wollten HTML nicht neu erfinden, sondern es pragmatisch weiterentwickeln – basierend auf den realen Anforderungen des modernen Webs.

#### Die Geburt des Living Standard

Die WHATWG hatte eine fundamentally andere Philosophie als das W3C. Anstatt alle paar Jahre eine neue, starre Version eines Standards zu veröffentlichen (wie HTML 4, dann HTML5, dann vielleicht HTML6), schlugen sie ein völlig neues Modell vor: den **Living Standard**.

Die Idee dahinter ist brillant und einfach zugleich. Ein Living Standard ist kein abgeschlossenes Buch, das irgendwann veraltet ist. Stell es dir eher wie eine ständig aktualisierte Wissensdatenbank vor, ähnlich wie Wikipedia. Es gibt nur *eine* Version von HTML – die aktuelle. Diese Version wird kontinuierlich verbessert, erweitert und korrigiert. Wenn ein neues Feature gebraucht wird, wie zum Beispiel das `<dialog>`-Element für Pop-up-Dialoge oder das `loading="lazy"`-Attribut für Bilder, wird es diskutiert, spezifiziert und in den Standard aufgenommen. Browser können es dann implementieren. Es gibt keinen großen, monumentalen "HTML6"-Launch, sondern eine stetige, fließende Evolution.

Dieser Ansatz hat mehrere entscheidende Vorteile:

1.  **Pragmatismus:** Der Standard reflektiert, was Browser tatsächlich implementieren und was Entwickler wirklich brauchen. Die Entwicklung wird von der Praxis angetrieben, nicht von der Theorie.
2.  **Abwärtskompatibilität:** Ein zentrales Prinzip der WHATWG war von Anfang an, das bestehende Web nicht zu zerstören. Neue Features müssen so gestaltet sein, dass sie alte Browser nicht beeinträchtigen. Das berühmte Zitat von Ian Hickson, einem der frühen treibenden Kräfte, lautet: "Don't break the web."
3.  **Fehlerbehandlung:** Der HTML Living Standard definiert nicht nur, wie korrektes HTML aussehen soll, sondern auch, wie Browser mit fehlerhaftem Code umgehen müssen. Das ist der Grund, warum eine Webseite auch dann noch (meistens) angezeigt wird, wenn du ein schließendes `</div>` vergisst. Diese fehlertolerante Natur ist ein Eckpfeiler des heutigen Webs.
4.  **Geschwindigkeit:** Neue Ideen können viel schneller in den Standard und damit in die Browser gelangen. Der Prozess ist agil und an die schnelle Entwicklung des Internets angepasst.

#### HTML5: Zwei Standards und eine Wiedervereinigung

Eine Zeit lang gab es eine etwas verwirrende Situation. Die WHATWG arbeitete an ihrem "HTML"-Living-Standard, während das W3C, das den Druck aus der Praxis spürte, seine Arbeit an XHTML 2.0 einstellte und ebenfalls einen neuen Standard namens "HTML5" begann. Beide Gruppen arbeiteten eine Weile parallel, und ihre Spezifikationen waren sich sehr ähnlich, aber nicht identisch.

Du hast in dieser Zeit vielleicht viel über "HTML5" als die große neue Sache gelesen. Technisch gesehen war das, was alle als HTML5 bezeichneten (also neue Elemente wie `<article>`, `<section>`, `<video>` und APIs wie Canvas), größtenteils die Arbeit der WHATWG. Das W3C veröffentlichte im Jahr 2014 eine offizielle "HTML5 Recommendation", die im Grunde ein Schnappschuss des damals aktuellen Living Standard war.

Diese Doppelgleisigkeit führte zu Reibung und Verwirrung. Welcher Standard war nun der "echte"? Die Browserhersteller richteten sich ohnehin nach dem Living Standard der WHATWG, weil sie dort selbst die treibenden Kräfte waren. Schließlich kam es 2019 zu einer historischen Einigung: Das W3C und die WHATWG unterzeichneten eine Vereinbarung, die festlegte, dass es fortan nur noch **einen** maßgeblichen HTML-Standard geben würde – den HTML Living Standard der WHATWG. Das W3C hat seitdem die Rolle, diesen Standard zu überprüfen und als offizielle Empfehlung zu veröffentlichen, aber die eigentliche Entwicklungsarbeit findet bei der WHATWG statt.

#### Was das für dich als Entwickler heute bedeutet

Diese Geschichte ist mehr als nur eine historische Anekdote. Sie hat ganz konkrete Auswirkungen auf deine tägliche Arbeit:

*   **Es gibt kein "HTML6".** Du lernst und schreibst einfach HTML. Die Jagd nach Versionsnummern ist vorbei. Wenn du heute eine Webseite baust, nutzt du den aktuellen HTML-Standard, so wie er im Living Standard definiert ist.
*   **Deine wichtigste Referenz ist der HTML Living Standard.** Wenn du die exakte, offizielle Definition eines Elements oder Attributs suchst, findest du sie auf [html.spec.whatwg.org](https://html.spec.whatwg.org).
*   **Praktische Ressourcen sind dein Freund.** Für den Alltag sind Dokumentationen wie die **MDN Web Docs** (früher Mozilla Developer Network) noch nützlicher. Sie erklären nicht nur, was der Standard sagt, sondern zeigen auch, welche Browser ein bestimmtes Feature bereits unterstützen – was für deine Arbeit entscheidend ist.
*   **Fokus auf Features, nicht auf Versionen.** Anstatt zu fragen: "Ist mein Browser HTML5-kompatibel?", fragst du heute: "Unterstützt mein Zielbrowser das `<dialog>`-Element oder die CSS Grid Layouts?". Dieser Wandel hin zur Feature-Detektion ist eine direkte Folge des Living-Standard-Modells.

Die stille Revolution der WHATWG hat die Art und Weise, wie sich das Web weiterentwickelt, für immer verändert. Sie hat einen theoretischen, langsamen Prozess durch ein praktisches, kollaboratives und dynamisches Modell ersetzt. Dank des HTML Living Standard ist die Sprache, die du jeden Tag schreibst, keine verstaubte Reliquie, sondern ein lebendiges, atmendes System, das sich gemeinsam mit den Ideen und Bedürfnissen von Entwicklern wie dir weiterentwickelt.
