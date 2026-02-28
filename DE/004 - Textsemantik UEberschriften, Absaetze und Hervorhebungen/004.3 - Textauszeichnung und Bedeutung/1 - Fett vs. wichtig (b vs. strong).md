# Fett vs. wichtig (b vs. strong)

### Fett vs. Wichtig: Der feine, aber entscheidende Unterschied zwischen `<b>` und `<strong>`

Auf den ersten Blick scheinen die HTML-Tags `<b>` und `<strong>` genau dasselbe zu tun: Sie lassen Text in deinem Browser fett erscheinen. Wenn du einen Text mit `<b>Hallo Welt</b>` und einen anderen mit `<strong>Hallo Welt</strong>` auszeichnest, wirst du visuell wahrscheinlich keinen Unterschied feststellen. Beide Male siehst du ein fettes „Hallo Welt“. Das führt unweigerlich zu der Frage: Warum gibt es zwei verschiedene Tags für denselben Effekt? Ist einer davon veraltet oder überflüssig?

Die Antwort ist ein klares Nein. Der Unterschied zwischen diesen beiden Tags ist fundamental und liegt nicht in der Darstellung, sondern in der Bedeutung – der Semantik. Und genau das ist der Kern von modernem, professionellem HTML: Du beschreibst nicht, wie etwas *aussehen* soll, sondern was etwas *ist*. Das Aussehen überlässt du vollständig dem CSS.

#### Die semantische Bedeutung: Was sagst du der Maschine?

Stell dir vor, du schreibst nicht nur für Menschen, die mit ihren Augen eine Webseite lesen, sondern auch für Maschinen. Zu diesen Maschinen gehören zum Beispiel die Crawler von Suchmaschinen wie Google oder Screenreader, die blinden und sehbehinderten Menschen den Inhalt einer Seite vorlesen. Diese Maschinen können „fett“ nicht sehen, aber sie können die Bedeutung eines HTML-Tags interpretieren. Hier trennen sich die Wege von `<b>` und `<strong>` dramatisch.

##### `<strong>`: Wenn etwas wirklich wichtig ist

Der `<strong>`-Tag steht für „strong importance“, also für starke Wichtigkeit, Ernsthaftigkeit oder Dringlichkeit. Wenn du ein Wort oder einen Satz in `<strong>`-Tags einfasst, teilst du dem Browser und allen anderen Systemen mit: „Achtung, dieser Teil des Inhalts hat eine besondere Bedeutung. Er ist wichtiger als der umgebende Text.“

Denk an einen Warnhinweis in einer Bedienungsanleitung. Der Satz „Trennen Sie das Gerät vor der Reinigung vom Stromnetz“ ist nicht nur eine beiläufige Information – er ist entscheidend für die Sicherheit. Eine korrekte semantische Auszeichnung würde so aussehen:

```html
<p>Bevor du das Gehäuse öffnest, stelle sicher, dass alle Schritte befolgt wurden. <strong>Trenne das Gerät unbedingt vor der Reinigung vom Stromnetz.</strong> Ein Nichtbeachten kann zu schweren Verletzungen führen.</p>
```

Ein Screenreader, der auf diesen Text trifft, könnte seine Stimme ändern. Er könnte den `<strong>`-Teil mit mehr Betonung oder einer höheren Lautstärke vorlesen, um die Wichtigkeit zu signalisieren. Eine Suchmaschine erkennt, dass die Keywords innerhalb des `<strong>`-Tags für das Verständnis des gesamten Absatzes von zentraler Bedeutung sind.

Du verwendest `<strong>` also für:

*   **Warnungen:** „**Achtung:** Rutschgefahr!“
*   **Dringende Hinweise:** „Deine Testversion läuft in **24 Stunden** ab.“
*   **Inhaltlich entscheidende Aussagen:** „Das Kernkonzept dieser Theorie ist die **Relativität**.“

Du hebst hier nicht nur visuell etwas hervor, du gibst dem Inhalt Gewicht und eine klare semantische Botschaft.

##### `<b>`: Wenn etwas nur anders aussehen soll

Der `<b>`-Tag ist im Vergleich dazu semantisch neutral. Sein Name kommt ursprünglich von „bold“ (fett), aber in der modernen HTML5-Spezifikation wurde seine Bedeutung neu definiert als „Bring Attention To“. Du nutzt ihn, um Text stilistisch vom Rest abzuheben, ohne ihm eine höhere Wichtigkeit oder Bedeutung zu verleihen. Der Inhalt ist nicht wichtiger, er soll nur ins Auge fallen.

Klassische Anwendungsfälle für den `<b>`-Tag sind:

*   **Produktnamen** in einem Testbericht: „Das neue <b>Pixel 8 Pro</b> überzeugte uns im Test besonders durch seine Kamera.“
*   **Schlüsselwörter** in einem erklärenden Text: „Ein <b>Funktionsprototyp</b> ist ein frühes Modell eines Produkts, das zur Überprüfung der Funktionalität dient.“
*   Die **Lead-Sätze** eines Zeitungsartikels, die oft fett gedruckt sind.

Schauen wir uns das Beispiel mit dem Produktnamen an:

```html
<p>In unserem aktuellen Smartphone-Vergleich haben wir uns das <b>SuperPhone 2000</b> und das <b>MegaDevice X</b> genauer angesehen. Beide Geräte bieten eine beeindruckende Leistung, doch das <b>SuperPhone 2000</b> hat bei der Akkulaufzeit die Nase vorn.</p>
```

Hier sind die Produktnamen `SuperPhone 2000` und `MegaDevice X` nicht wichtiger als der Rest des Satzes. Sie zu betonen, würde die Aussage des Satzes verfälschen. Sie werden lediglich visuell hervorgehoben, um dem Leser das Scannen des Textes zu erleichtern. Ein Screenreader würde diese Wörter ganz normal vorlesen, ohne besondere Betonung. Eine Suchmaschine würde sie als normale Wörter werten.

#### Die Macht von CSS: Trennung von Struktur und Design

Jetzt kommt der entscheidende Punkt, der das Konzept zementiert: Die Tatsache, dass beide Tags standardmäßig fett dargestellt werden, ist nur eine Voreinstellung des Browsers. Du kannst dieses Verhalten jederzeit mit CSS ändern.

Stell dir vor, du möchtest auf deiner Webseite alle wichtigen Warnungen nicht fett, sondern rot und unterstrichen darstellen. Alle Produktnamen hingegen sollen nicht fett, sondern nur kursiv und in einer anderen Farbe erscheinen.

Dein CSS könnte so aussehen:

```css
strong {
  font-weight: normal; /* Das standardmäßige "fett" entfernen */
  color: red;
  text-decoration: underline;
}

b {
  font-weight: normal; /* Auch hier das "fett" entfernen */
  font-style: italic;
  color: #005A9C; /* Ein dunkles Blau */
}
```

Mit diesem CSS würde unser Warnhinweis von vorhin so aussehen:

<p>Bevor du das Gehäuse öffnest, stelle sicher, dass alle Schritte befolgt wurden. <strong style="color: red; text-decoration: underline; font-weight: normal;">Trenne das Gerät unbedingt vor der Reinigung vom Stromnetz.</strong> Ein Nichtbeachten kann zu schweren Verletzungen führen.</p>

Und der Text mit den Produktnamen so:

<p>In unserem aktuellen Smartphone-Vergleich haben wir uns das <b style="font-style: italic; color: #005A9C; font-weight: normal;">SuperPhone 2000</b> und das <b style="font-style: italic; color: #005A9C; font-weight: normal;">MegaDevice X</b> genauer angesehen. ...</p>

Obwohl der Text nun nicht mehr fett ist, bleibt die semantische Information im HTML-Code vollständig erhalten. Ein Screenreader würde den `<strong>`-Text immer noch als wichtig erkennen und entsprechend betonen. Eine Suchmaschine ebenfalls. Der `<b>`-Text bliebe semantisch neutral. Du hast die Darstellung komplett von der Bedeutung entkoppelt. Das ist sauberes, professionelles und zukunftssicheres Webdesign.

#### Die Entscheidungshilfe: Was will ich ausdrücken?

Wenn du das nächste Mal vor der Wahl zwischen `<b>` und `<strong>` stehst, stelle dir nicht die Frage: „Soll dieser Text fett sein?“. Stelle dir stattdessen diese Fragen:

1.  **Ist dieser Text inhaltlich wichtiger, ernster oder dringlicher als der umgebende Text?**
    *   **Ja:** Verwende `<strong>`.
    *   **Nein:** Gehe zu Frage 2.

2.  **Möchte ich diesen Text lediglich stilistisch hervorheben, um die Aufmerksamkeit des Lesers darauf zu lenken, ohne ihm eine besondere Bedeutung zu geben (wie bei einem Schlüsselwort oder Eigennamen)?**
    *   **Ja:** Verwende `<b>`.
    *   **Nein:** Dann sind wahrscheinlich weder `<b>` noch `<strong>` die richtige Wahl. Vielleicht suchst du nach `<em>` (Betonung), `<mark>` (Hervorhebung wie mit einem Textmarker) oder einfach einem `<span>` mit einer CSS-Klasse, um es frei zu gestalten.

Die korrekte Verwendung dieser Tags ist mehr als nur eine technische Spitzfindigkeit. Sie ist ein Zeichen für professionelles Handwerk. Sie macht deine Webseiten zugänglicher (Accessibility), verbessert potenziell dein Suchmaschinenranking (SEO) und sorgt für einen sauberen, wartbaren Code, bei dem Inhalt und Design klar getrennt sind. Indem du die semantische Bedeutung über die visuelle Darstellung stellst, schreibst du HTML so, wie es gedacht ist: als eine Sprache zur Strukturierung von Information.
