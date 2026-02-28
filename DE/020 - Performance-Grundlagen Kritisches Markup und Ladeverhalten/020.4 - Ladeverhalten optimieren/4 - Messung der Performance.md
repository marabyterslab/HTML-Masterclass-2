# Messung der Performance

### Messung der Performance: Wissen statt Raten

Bevor du auch nur eine Zeile Code änderst, um die Ladezeit deiner Webseite zu verbessern, musst du einen entscheidenden Schritt tun: messen. Ohne eine fundierte Messung ist jede Optimierung ein reiner Blindflug. Du könntest Stunden damit verbringen, ein Problem zu beheben, das gar nicht existiert, während der eigentliche Flaschenhals unentdeckt bleibt. Die Aussage „Auf meinem Rechner ist die Seite schnell“ ist die vielleicht gefährlichste Falle in der Webentwicklung. Dein schneller Computer mit einer starken Internetverbindung ist nicht der Maßstab. Der Maßstab sind die vielfältigen Geräte und Netzwerkbedingungen deiner tatsächlichen Nutzer.

Performance-Messung ist wie die Diagnose eines Arztes: Sie liefert die Daten, auf deren Grundlage du eine wirksame Behandlung – also Optimierung – einleiten kannst. In diesem Kapitel lernst du die wichtigsten Metriken und Werkzeuge kennen, um die Leistung deiner Webseite objektiv zu bewerten.

#### Was ist „schnell“? Die Core Web Vitals

Was eine Webseite „schnell“ macht, ist für den Nutzer eine gefühlte Erfahrung. Google hat versucht, diese subjektive Wahrnehmung in messbare, technische Kennzahlen zu übersetzen. Das Ergebnis sind die **Core Web Vitals**, ein Set von drei zentralen Metriken, die sich auf die User Experience konzentrieren. Sie sind heute der De-facto-Standard zur Bewertung der Web-Performance.

##### 1. Largest Contentful Paint (LCP)

Der LCP misst die Ladeleistung. Genauer gesagt: Er misst die Zeit vom Beginn des Ladevorgangs bis zu dem Moment, an dem das größte sichtbare Element (meist ein Bild, Video oder ein großer Textblock) im Viewport vollständig gerendert ist.

*   **Was es für den Nutzer bedeutet:** „Wann sehe ich den Hauptinhalt der Seite?“
*   **Ein guter Wert:** unter 2,5 Sekunden.

Ein hoher LCP-Wert deutet oft darauf hin, dass kritische Ressourcen, wie das große Hero-Image oder die Schriftarten, zu langsam geladen werden. Der Nutzer starrt auf eine leere oder unvollständige Seite und hat das Gefühl, dass nichts passiert.

##### 2. Interaction to Next Paint (INP)

Der INP misst die Reaktionsfähigkeit (Responsiveness) deiner Seite. Er erfasst die Latenz aller Klicks, Taps und Tastatureingaben, die ein Nutzer auf der Seite vornimmt, und gibt den schlechtesten Wert (abgesehen von einigen Ausreißern) an. Er misst die gesamte Zeit von der Nutzeraktion (z. B. Klick auf einen Button) bis zur visuellen Rückmeldung auf dem Bildschirm (z. B. das Aufklappen eines Menüs).

*   **Was es für den Nutzer bedeutet:** „Wie schnell reagiert die Seite, wenn ich etwas tun möchte?“
*   **Ein guter Wert:** unter 200 Millisekunden.

Ein hoher INP-Wert ist frustrierend. Der Nutzer klickt auf einen Button und nichts passiert, weil der Browser im Hintergrund mit langen JavaScript-Tasks beschäftigt ist. Die Seite fühlt sich träge oder „eingefroren“ an. INP hat im März 2024 den älteren Messwert *First Input Delay (FID)* abgelöst, da er die gesamte Interaktionsdauer und nicht nur die anfängliche Verzögerung misst und damit ein umfassenderes Bild der Responsiveness liefert.

##### 3. Cumulative Layout Shift (CLS)

Der CLS misst die visuelle Stabilität. Er erfasst, wie sehr sich das Layout der Seite während des Ladevorgangs unerwartet verschiebt. Solche Verschiebungen passieren oft, wenn Bilder, Werbebanner oder iframes ohne feste Größenangaben nachgeladen werden und den bereits sichtbaren Inhalt nach unten drücken.

*   **Was es für den Nutzer bedeutet:** „Bleibt die Seite stabil, während ich versuche, sie zu lesen oder zu bedienen?“
*   **Ein guter Wert:** unter 0,1.

Ein hoher CLS-Wert ist ein klassischer Störfaktor. Stell dir vor, du möchtest auf einen Link klicken, aber kurz bevor dein Finger den Bildschirm berührt, lädt ein Werbebanner darüber und du klickst versehentlich darauf. Das ist ein Layout Shift, und der CLS-Wert quantifiziert, wie stark diese Verschiebungen auf deiner Seite sind.

#### Labor vs. Echtes Leben: Zwei Arten der Messung

Um diese Metriken zu erfassen, gibt es zwei grundlegend verschiedene Ansätze, die du beide kennen und nutzen solltest.

**1. Lab-Daten (Synthetische Messung)**
Lab-Daten werden in einer kontrollierten, simulierten Umgebung erhoben. Du nutzt ein Werkzeug, das deine Seite unter vordefinierten Bedingungen lädt (z. B. auf einem simulierten Mittelklasse-Smartphone mit einer gedrosselten 4G-Verbindung).

*   **Vorteil:** Die Ergebnisse sind reproduzierbar. Du kannst eine Änderung vornehmen, erneut messen und die Ergebnisse direkt vergleichen. Das ist ideal für die Entwicklungsphase und das Debugging.
*   **Nachteil:** Sie spiegeln nicht unbedingt die Realität deiner Nutzer wider, die eine riesige Bandbreite an Geräten, Netzwerkgeschwindigkeiten und Browsern verwenden.

**2. Feld-Daten (Real User Monitoring, RUM)**
Feld-Daten stammen von echten Nutzern, die deine Webseite besuchen. Deren Browser sammeln anonymisierte Performance-Daten und senden sie an einen Analysedienst.

*   **Vorteil:** Diese Daten zeigen die tatsächliche Performance, wie sie von deinen Nutzern erlebt wird. Sie sind der ultimative Realitätscheck.
*   **Nachteil:** Die Daten sind „verrauschter“, da sie von unzähligen verschiedenen Faktoren beeinflusst werden. Es ist schwieriger, direkte Vorher-Nachher-Vergleiche für eine spezifische Code-Änderung anzustellen.

Die goldene Regel lautet: **Entwickle mit Lab-Daten, validiere mit Feld-Daten.**

#### Dein Werkzeugkasten: So misst du die Performance

Glücklicherweise benötigst du keine teure Spezialsoftware. Die wichtigsten Werkzeuge sind kostenlos und oft bereits in deinem Browser integriert.

##### Lighthouse in den Chrome DevTools

Das wichtigste Werkzeug für Lab-Messungen ist Lighthouse. Es ist direkt in die Entwicklertools von Google Chrome (und anderen Chromium-basierten Browsern) integriert.

So führst du eine Messung durch:
1.  Öffne deine Webseite in einem Inkognito-Fenster. Das ist wichtig, um zu verhindern, dass Browser-Erweiterungen die Messergebnisse verfälschen.
2.  Öffne die Entwicklertools (mit F12, `Cmd+Opt+I` auf dem Mac oder per Rechtsklick -> „Untersuchen“).
3.  Wechsle zum Tab „Lighthouse“.
4.  Wähle die Kategorien aus, die du prüfen möchtest (für uns ist „Performance“ am wichtigsten).
5.  Wähle das Gerät („Mobil“ oder „Desktop“). Beginne immer mit der mobilen Messung, da hier die meisten Performance-Probleme auftreten.
6.  Klicke auf „Seitenaufbau analysieren“.

Nach einem kurzen Moment präsentiert dir Lighthouse einen umfassenden Bericht.

##### PageSpeed Insights

PageSpeed Insights ist ein Online-Tool von Google, das das Beste aus beiden Welten vereint. Du gibst eine URL ein, und das Tool führt eine Lighthouse-Messung durch (Lab-Daten). Wenn für deine Seite genügend öffentliche Nutzerdaten vorhanden sind (aus dem Chrome User Experience Report), zeigt es dir zusätzlich die Feld-Daten für die Core Web Vitals der letzten 28 Tage an.

Dies ist ein hervorragendes Werkzeug, um einen schnellen Überblick zu bekommen und Lab- mit echten Nutzerdaten zu vergleichen.

#### Einen Lighthouse-Report verstehen

Ein Lighthouse-Report kann auf den ersten Blick überwältigend wirken. Konzentriere dich auf die folgenden Bereiche:

1.  **Der Performance-Score:** Oben siehst du eine Gesamtpunktzahl von 0 bis 100. Dies ist ein gewichteter Durchschnitt verschiedener Metriken. Er gibt dir eine schnelle Einschätzung, ist aber weniger wichtig als die einzelnen Metriken darunter.

2.  **Die Metriken:** Hier siehst du die konkreten Werte für LCP, CLS und andere wichtige Kennzahlen wie den *Total Blocking Time (TBT)*. TBT ist eine Lab-Metrik, die eng mit dem INP korreliert und die Zeit misst, in der der Haupt-Thread durch lange Tasks blockiert war und somit nicht auf Nutzereingaben reagieren konnte. Die Werte sind farblich markiert: Grün ist gut, Orange bedeutet verbesserungswürdig, Rot ist schlecht.

3.  **Chancen (Opportunities):** Dies ist der wichtigste Abschnitt für deine Optimierungsarbeit. Lighthouse gibt dir hier konkrete, umsetzbare Empfehlungen. Beispiele sind:
    *   **Bilder in modernen Formaten bereitstellen:** Wandle JPGs oder PNGs in effizientere Formate wie WebP oder AVIF um.
    *   **Renderblockierende Ressourcen beseitigen:** Identifiziert CSS- und JavaScript-Dateien, die den Browser am schnellen Anzeigen der Seite hindern.
    *   **Nicht verwendetes JavaScript reduzieren:** Weist auf Code in deinen JS-Bundles hin, der für die aktuelle Seite nicht benötigt wird.

4.  **Diagnosen (Diagnostics):** Dieser Abschnitt liefert zusätzliche Informationen und tiefere Einblicke in das Ladeverhalten deiner Seite, zum Beispiel die Größe deines DOMs oder die Länge kritischer Anfrageketten.

Beginne deine Arbeit immer im Abschnitt „Chancen“. Gehe die Liste von oben nach unten durch, denn Lighthouse sortiert sie nach dem geschätzten Einsparpotenzial.

#### Der Blick unter die Haube: Der Performance-Tab

Wenn Lighthouse dir sagt, *was* langsam ist, aber nicht genau *warum*, ist der nächste Schritt der „Performance“-Tab in den Chrome DevTools. Dies ist das EKG deiner Webseite. Du kannst eine Aufzeichnung des Ladevorgangs starten und bekommst einen detaillierten Wasserfall-Graphen und eine Flame-Chart, die jede einzelne Aktivität des Browsers auf die Millisekunde genau anzeigt: Netzwerkanfragen, HTML-Parsing, CSS-Berechnungen, JavaScript-Ausführung und Rendering.

Die Analyse dieses Tabs erfordert Übung, aber sie ist das mächtigste Werkzeug, um komplexe Performance-Engpässe zu identifizieren, insbesondere wenn es um rechenintensives JavaScript geht, das den INP in die Höhe treibt.

Die Messung ist der erste und wichtigste Schritt auf dem Weg zu einer performanten Webseite. Sie verwandelt vage Vermutungen in harte Fakten und gibt dir einen klaren Fahrplan für die Optimierung. Nutze diese Werkzeuge regelmäßig, um den Zustand deiner Seite zu überwachen und die Auswirkungen deiner Arbeit zu überprüfen.
