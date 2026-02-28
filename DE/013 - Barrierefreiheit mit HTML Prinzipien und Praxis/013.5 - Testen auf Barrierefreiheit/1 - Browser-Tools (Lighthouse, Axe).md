# Browser-Tools (Lighthouse, Axe)

### Automatisierte Helfer im Browser: Lighthouse und Axe

Nachdem du die fundamentalen Prinzipien der Barrierefreiheit kennengelernt hast, stehst du vor der praktischen Frage: Wie überprüfst du, ob dein Code diesen Anforderungen tatsächlich gerecht wird? Manuelles Testen, bei dem du dich durch deine Seite navigierst, nur die Tastatur benutzt oder einen Screenreader einschaltest, ist unerlässlich und unersetzbar. Doch bevor du diesen Schritt gehst, gibt es eine erste, mächtige Verteidigungslinie direkt in deinem Browser: automatisierte Test-Tools.

Stell dir diese Werkzeuge wie einen unermüdlichen Assistenten vor, der dir über die Schulter schaut und auf offensichtliche Fehler hinweist. Sie können nicht den gesamten Kontext oder die menschliche Erfahrung erfassen, aber sie finden zuverlässig eine Vielzahl von technischen Problemen – die sogenannten „niedrig hängenden Früchte“. Damit erledigen sie einen Großteil der Vorarbeit, sodass du dich beim manuellen Testen auf die komplexeren, kontextbezogenen Aspekte konzentrieren kannst.

Zwei der prominentesten und nützlichsten Werkzeuge in diesem Bereich sind Lighthouse, das direkt in Google Chrome integriert ist, und Axe, eine weitverbreitete Browser-Erweiterung, die als De-facto-Standard für automatisierte Barrierefreiheitstests gilt.

#### Lighthouse – Der eingebaute Leuchtturm

Fast jeder Webentwickler hat die Chrome DevTools (Entwicklertools) schon einmal genutzt. Versteckt zwischen den Tabs für „Elements“, „Console“ und „Network“ findest du auch den Tab „Lighthouse“. Lighthouse ist ein Open-Source-Tool von Google, das als eine Art umfassender Gesundheitscheck für Webseiten konzipiert ist. Es analysiert eine Seite nicht nur auf Barrierefreiheit, sondern auch auf Leistung (Performance), SEO (Suchmaschinenoptimierung) und allgemeine Best Practices. Für uns ist hier natürlich der Bereich „Accessibility“ (Barrierefreiheit) von zentraler Bedeutung.

**Wie du einen Lighthouse-Report erstellst**

Der Prozess ist denkbar einfach:
1.  Öffne die Webseite, die du testen möchtest.
2.  Öffne die Chrome DevTools (mit `F12`, `Ctrl+Shift+I` oder `Cmd+Opt+I` auf dem Mac).
3.  Wechsle zum Tab „Lighthouse“.
4.  Unter „Categories“ stellst du sicher, dass zumindest „Accessibility“ angehakt ist. Du kannst die anderen Kategorien für einen fokussierten Test auch deaktivieren.
5.  Wähle unter „Device“, ob du die Seite als „Mobile“ oder „Desktop“ analysieren möchtest. Barrierefreiheitsprobleme sind oft geräteunabhängig, aber das Layout kann eine Rolle spielen.
6.  Klicke auf „Analyze page load“.

Nach einem kurzen Moment präsentiert dir Lighthouse einen detaillierten Bericht.

**Den Lighthouse-Bericht verstehen**

An der Spitze des Berichts siehst du einen Score von 0 bis 100. Dieser Wert gibt dir eine schnelle, allgemeine Einschätzung. Ein hoher Wert ist gut, ein niedriger deutet auf erhebliche Probleme hin. Aber lass dich von dieser Zahl nicht blenden oder davon besessen machen, die 100 zu erreichen. Der wahre Wert von Lighthouse liegt nicht im Score, sondern in den detaillierten Ergebnissen darunter.

Der Bericht ist in mehrere Abschnitte unterteilt:

*   **Fehler (Errors):** Dies sind die eindeutigen Verstöße gegen die WCAG (Web Content Accessibility Guidelines). Lighthouse listet hier konkret auf, was falsch ist. Ein klassisches Beispiel wäre ein Bild ohne `alt`-Attribut oder ein Formularelement, dem ein `<label>` fehlt.

    ```html
    <!-- Von Lighthouse als Fehler erkannt: Kein Label für das Eingabefeld -->
    <input type="email" id="user-email">
    ```

    Zu jedem gefundenen Problem zeigt Lighthouse die verantwortlichen HTML-Elemente an und, das ist besonders wertvoll, verlinkt auf eine ausführliche Erklärung. Du erfährst nicht nur, *was* falsch ist, sondern auch, *warum* es ein Problem darstellt und *wie* du es beheben kannst.

*   **Manuelle Prüfungen (Manual Checks):** Dieser Abschnitt listet Aspekte auf, die ein automatisiertes Tool nicht abschließend bewerten kann. Das Tool erinnert dich daran, Dinge wie die logische Tab-Reihenfolge, die Lesbarkeit von Inhalten oder die Interaktivität mit der Tastatur manuell zu überprüfen. Es ist eine eingebaute To-do-Liste für deine manuellen Tests.

*   **Bestandene Prüfungen (Passed Audits):** Hier siehst du, was du bereits richtig gemacht hast. Das ist nicht nur eine schöne Bestätigung, sondern hilft dir auch zu lernen, welche Praktiken korrekt sind.

Lighthouse ist der perfekte Einstiegspunkt. Es ist bereits da, erfordert keine Installation und gibt dir ein breites Bild über den Zustand deiner Seite.

#### Axe DevTools – Das spezialisierte Skalpell

Wenn Lighthouse das vielseitige Schweizer Taschenmesser ist, dann sind die Axe DevTools das präzise Skalpell des Chirurgen. Axe ist eine Test-Engine, die von Deque Systems entwickelt wurde, einem führenden Unternehmen im Bereich der digitalen Barrierefreiheit. Ironischerweise ist die Axe-Engine sogar das Herzstück der Barrierefreiheitsprüfung von Lighthouse. Warum also ein separates Werkzeug verwenden?

Die Antwort liegt in der Detailtiefe und dem Entwickler-Workflow. Während Lighthouse einen allgemeinen Bericht erstellt, ist die Axe DevTools Browser-Erweiterung (verfügbar für Chrome, Firefox und Edge) speziell für Entwickler konzipiert, die Barrierefreiheitsprobleme direkt im Entwicklungsprozess finden und beheben wollen.

**Wie du Axe DevTools nutzt**

1.  Installiere die „Axe DevTools“ Erweiterung aus dem Web Store deines Browsers.
2.  Öffne die DevTools auf deiner Webseite. Du wirst einen neuen Tab namens „axe DevTools“ finden.
3.  Klicke in diesem Tab auf den großen Button, meist beschriftet mit „Scan ALL of my page“.

Innerhalb von Sekunden präsentiert Axe einen interaktiven Bericht, der oft detaillierter und einfacher zu handhaben ist als der von Lighthouse.

**Den Axe-Bericht verstehen**

Der Bericht von Axe ist klar nach Problemen strukturiert und bietet einige unschätzbare Vorteile:

*   **Problembeschreibung:** Jedes Problem wird klar benannt, zum Beispiel „Images must have alternate text“ oder „Form elements must have labels“.
*   **Schweregrad:** Axe kategorisiert Probleme nach ihrem Schweregrad (Critical, Serious, Moderate, Minor). Dies hilft dir, Prioritäten zu setzen und die kritischsten Fehler zuerst anzugehen.
*   **Element-Referenz:** Axe zeigt dir den exakten CSS-Selektor des problematischen Elements. Du weißt also sofort, wo im Code du suchen musst.
*   **Highlight-Funktion:** Mit einem Klick auf den „Highlight“-Button wird das fehlerhafte Element direkt auf der Webseite visuell hervorgehoben. Das erspart dir das mühsame Suchen im DOM-Baum.
*   **Konkrete Lösungsvorschläge (Remediation):** Das ist vielleicht die stärkste Funktion. Axe gibt dir nicht nur eine allgemeine Erklärung, sondern oft auch konkrete Code-Snippets oder Anweisungen, wie du das Problem lösen kannst. Zum Beispiel wird es bei einem fehlenden Label vorschlagen, ein `<label>`-Element mit einem `for`-Attribut hinzuzufügen, das auf die `id` des `input`-Elements verweist.

    ```html
    <!-- Problem von Axe gefunden: -->
    <input type="text" id="nachname">

    <!-- Lösungsvorschlag von Axe: -->
    <label for="nachname">Nachname</label>
    <input type="text" id="nachname">
    ```
*   **Verweise:** Wie Lighthouse bietet auch Axe Links zu weiterführenden Informationen (z. B. zur Deque University), um dein Wissen zu vertiefen.

Axe ist das Werkzeug der Wahl für die tägliche Arbeit. Es integriert sich nahtlos in deinen Entwicklungs-Workflow und macht das Aufspüren und Beheben von Barrierefreiheitsproblemen so effizient wie möglich.

#### Die Grenzen der Automatisierung: Wo der Mensch unersetzlich ist

So leistungsfähig diese Werkzeuge auch sind, es ist entscheidend, ihre Grenzen zu verstehen. Automatisierte Tests können etwa 20-50 % der potenziellen Barrierefreiheitsprobleme finden. Sie sind exzellent darin, technische Regelverstöße zu erkennen, aber sie können keinen menschlichen Verstand oder Kontext ersetzen.

Folgende Aspekte können von Tools wie Lighthouse und Axe nicht oder nur unzureichend geprüft werden:

*   **Sinnhaftigkeit von Alternativtexten:** Ein Tool kann prüfen, *ob* ein `<img>`-Tag ein `alt`-Attribut hat. Es kann aber nicht beurteilen, ob der Text `alt="Ein Golden Retriever fängt einen roten Ball im Park"` gut ist und `alt="bild123.jpg"` nutzlos ist.
*   **Logische Reihenfolge:** Ein Tool kann nicht wissen, ob die Fokus-Reihenfolge beim Navigieren mit der Tab-Taste logisch und intuitiv für einen sehenden Benutzer ist. Es kann nur prüfen, *ob* Elemente fokussierbar sind.
*   **Farbkontrast im Kontext:** Ein Tool kann das Kontrastverhältnis zwischen Text und Hintergrund berechnen. Es kann aber nicht erkennen, ob Farbe als einziges Mittel zur Informationsvermittlung eingesetzt wird (z. B. in einem Diagramm, wo rote Balken „Verluste“ und grüne „Gewinne“ bedeuten, ohne weitere Kennzeichnung).
*   **Verständlichkeit von Link-Texten:** Ein Tool kann einen Link mit dem Text „Hier klicken“ als potenzielles Problem markieren. Es kann aber nicht beurteilen, ob der umgebende Satz den Zweck des Links ausreichend erklärt.
*   **Tastaturfallen:** Ein Tool kann kaum feststellen, ob ein Benutzer mit der Tastatur in ein interaktives Element (z. B. ein komplexes Widget) navigieren, aber nicht wieder heraus kann.

Diese Werkzeuge sind dein Startpunkt, nicht dein Ziel. Nutze sie, um die offensichtlichen Fehler schnell aus dem Weg zu räumen. Sie säubern das Feld, damit du dich bei der anschließenden manuellen Prüfung voll und ganz auf die Benutzererfahrung konzentrieren kannst – denn am Ende baust du Webseiten für Menschen, nicht für Test-Software.
