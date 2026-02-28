# Verlinkung von Telefonnummern

### Anrufe direkt aus dem Browser: Telefonnummern verlinken

Stell dir vor, du besuchst die Website eines Restaurants auf deinem Smartphone, weil du einen Tisch reservieren möchtest. Du findest die Telefonnummer, aber anstatt sie mühsam abzutippen oder zu kopieren, tippst du einfach darauf, und dein Telefon öffnet die Wählanwendung mit der bereits eingefügten Nummer. Ein Klick auf den grünen Hörer, und schon bist du verbunden. Diese nahtlose Benutzererfahrung ist kein Zufall, sondern das Ergebnis einer korrekt implementierten Verlinkung von Telefonnummern in HTML.

In diesem Kapitel tauchen wir tief in die Welt der `tel:`-Links ein. Du lernst, wie du Telefonnummern so in deine Website integrierst, dass sie für Nutzer auf allen Geräten einen echten Mehrwert bieten.

#### Das `tel:`-Schema: Die Grundlage für Anrufe

Genau wie `http://` dem Browser signalisiert, dass eine Webseite aufgerufen werden soll, oder `mailto:` den E-Mail-Client startet, gibt es ein spezielles URI-Schema (Uniform Resource Identifier) für Telefonnummern: das `tel:`-Schema.

Die grundlegende Syntax ist denkbar einfach und folgt dem bekannten Muster des `<a>`-Tags:

```html
<a href="tel:TELEFONNUMMER">Ruf uns an!</a>
```

Wenn ein Nutzer auf diesen Link klickt, versucht das Betriebssystem, die Aktion mit einer passenden Anwendung zu verknüpfen. Auf einem Smartphone ist das die Telefon-App. Auf einem Desktop-Computer könnte es eine VoIP-Anwendung wie Skype, FaceTime oder Microsoft Teams sein. Wenn keine passende Anwendung installiert ist, passiert in der Regel nichts.

Ein einfaches Beispiel für eine fiktive Berliner Nummer könnte so aussehen:

```html
<a href="tel:03012345678">030 12345678</a>
```

Das funktioniert zwar in den meisten Fällen innerhalb Deutschlands, ist aber nicht die empfohlene Vorgehensweise. Warum? Weil das Web global ist. Ein Nutzer aus der Schweiz oder den USA wüsste nicht, was er mit dieser Nummer anfangen soll. Hier kommt ein internationaler Standard ins Spiel.

#### Die korrekte Formatierung: Einmal um die Welt nach RFC 3966

Um sicherzustellen, dass deine Telefonnummern weltweit verstanden und korrekt gewählt werden, solltest du dich an den internationalen Standard E.164 halten, der im RFC 3966 für das `tel:`-Schema spezifiziert ist. Das klingt komplizierter, als es ist. Die Regeln sind einfach:

1.  **Das Pluszeichen (`+`) am Anfang:** Es ersetzt die internationale Vorwahl (wie `00` in Deutschland oder `011` in den USA).
2.  **Die Ländervorwahl:** Direkt nach dem Pluszeichen folgt die Ländervorwahl (z. B. `49` für Deutschland, `43` für Österreich, `41` für die Schweiz).
3.  **Die Ortsvorwahl ohne führende Null:** Die führende Null der Ortsvorwahl, die wir bei nationalen Anrufen verwenden (z. B. `030` für Berlin), entfällt. Aus `030` wird also `30`.
4.  **Die eigentliche Rufnummer.**
5.  **Keine Leerzeichen, Klammern oder Bindestriche:** Im `href`-Attribut selbst sollte die Nummer als eine durchgehende Zeichenkette ohne Trennzeichen geschrieben werden. Das Betriebssystem des Geräts kümmert sich um die korrekte Formatierung für den Wählvorgang.

Unsere Berliner Beispielnummer `030 12345678` wird nach diesem Standard zu `+493012345678`. Der korrekte HTML-Code sieht demnach so aus:

```html
<a href="tel:+493012345678">Ruf die Berliner Nummer an</a>
```

Diese Schreibweise garantiert, dass ein Nutzer aus jedem Land der Welt mit nur einem Klick die richtige Verbindung herstellen kann. Sein Telefonanbieter weiß dank des `+` und der `49` genau, dass ein Anruf nach Deutschland gehen soll.

#### Maschinenlesbarkeit vs. menschliche Lesbarkeit

Nun haben wir ein Dilemma. Die Nummer `+493012345678` im `href`-Attribut ist perfekt für Maschinen, aber für Menschen schwer zu lesen und zu erfassen. Niemand schreibt oder liest Telefonnummern in diesem Format. Die Schönheit von HTML liegt darin, dass wir beides haben können: eine maschinenlesbare Verlinkung und einen menschenlesbaren Text.

Der Text zwischen dem öffnenden `<a>`- und dem schließenden `</a>`-Tag ist das, was der Nutzer auf der Webseite sieht. Hier kannst du die Telefonnummer in einem gewohnten, gut lesbaren Format darstellen, inklusive Leerzeichen, Bindestrichen oder Klammern, um die Lesbarkeit zu erhöhen.

Die optimale Lösung verbindet beide Welten:

```html
<a href="tel:+493012345678">+49 (0)30 123 45 678</a>
```

**Was hier passiert:**

*   **`href="tel:+493012345678"`:** Der Browser und das Betriebssystem erhalten die international standardisierte, fehlerfreie Nummer für den Wählvorgang.
*   **`+49 (0)30 123 45 678`:** Der Nutzer sieht eine klar formatierte, leicht verständliche Nummer. Die `(0)` wird oft hinzugefügt, um Nutzern aus dem Inland zu signalisieren, dass sie die Null mitwählen müssen, wenn sie die Nummer manuell eingeben.

Diese Methode ist die professionelle und benutzerfreundlichste Art, Telefonnummern zu verlinken.

#### Mehr als nur Anrufen: Durchwahlen und Pausen

Manchmal reicht es nicht, nur die Hauptnummer eines Unternehmens anzurufen. Oft muss man nach dem Verbindungsaufbau eine Durchwahl oder eine Menüoption eingeben. Auch das `tel:`-Schema bietet hierfür eine Lösung.

Du kannst spezielle Zeichen verwenden, um nach dem Wählen der Hauptnummer eine Pause oder eine Wartezeit einzufügen, gefolgt von der Durchwahl.

*   **Das Komma (`,`)** fügt eine kurze Pause ein. Das ist nützlich für automatisierte Systeme, die sofort nach dem Verbindungsaufbau bereit für die Eingabe einer Durchwahl sind. Jedes Komma steht typischerweise für eine Pause von einigen Sekunden.
*   **Das Semikolon (`;`)** ist etwas spezieller. Es bewirkt, dass die nachfolgenden Ziffern (die Durchwahl) erst dann gesendet werden, wenn der Nutzer es auf dem Bildschirm bestätigt. Dies ist ideal, wenn man erst eine Ansage abwarten muss, bevor man die Durchwahl eingeben kann. In der Praxis wird das Semikolon jedoch nicht von allen Geräten und Anwendungen unterstützt, weshalb das Komma die sicherere Wahl ist.

Angenommen, unsere Beispielnummer hat die Durchwahl `99`. Der Code sähe so aus:

```html
<a href="tel:+493012345678,99">Marketing-Abteilung (Durchwahl 99)</a>
```

Wenn ein Nutzer auf diesen Link klickt, wählt sein Telefon `+493012345678`, wartet einen Moment und wählt dann automatisch die `99`.

#### Ein Hauch von Stil: Telefon-Links mit CSS gestalten

Ein Link zu einer Telefonnummer ist immer noch ein ganz normaler `<a>`-Tag. Das bedeutet, du kannst ihn mit CSS nach Belieben gestalten. Oft ist es wünschenswert, Telefon-Links anders darzustellen als normale Links zu Webseiten, um ihre Funktion visuell zu verdeutlichen.

Hierfür eignet sich ein CSS-Attribut-Selektor hervorragend. Mit `a[href^="tel:"]` kannst du gezielt alle `<a>`-Elemente ansprechen, deren `href`-Attribut mit `tel:` beginnt.

Stell dir vor, du möchtest allen Telefon-Links ein kleines Telefonsymbol voranstellen und die standardmäßige Unterstreichung entfernen. Das könntest du mit folgendem CSS-Code erreichen:

```css
/* Wähle alle Links, deren href mit "tel:" beginnt */
a[href^="tel:"] {
  text-decoration: none; /* Entfernt die Unterstreichung */
  color: #333; /* Gibt dem Link eine andere Farbe */
  font-weight: bold;
}

/* Füge ein Telefon-Icon vor dem Link ein */
a[href^="tel:"]::before {
  content: '📞 '; /* Hier kannst du ein Emoji oder ein Icon-Font-Zeichen verwenden */
  margin-right: 0.5em;
  font-style: normal;
}
```

Durch solche kleinen stilistischen Anpassungen wird die Benutzerführung auf deiner Seite sofort klarer. Der Nutzer erkennt auf den ersten Blick, dass es sich hier nicht um einen gewöhnlichen Link, sondern um eine interaktive Telefonnummer handelt.

#### Barrierefreiheit nicht vergessen

Wie bei allen interaktiven Elementen im Web spielt auch bei Telefon-Links die Barrierefreiheit eine wichtige Rolle. Ein Screenreader, den blinde oder sehbehinderte Menschen nutzen, wird den Link korrekt als solchen erkennen. Wichtig ist, dass der Link-Text aussagekräftig ist.

Ein Link-Text, der nur aus der Nummer besteht, ist bereits gut:

```html
<a href="tel:+493012345678">+49 (0)30 123 45 678</a>
```

Ein Screenreader würde hier etwa vorlesen: "Link, plus vier neun null drei null eins zwei drei vier fünf sechs sieben acht".

Noch besser ist es, dem Nutzer Kontext zu geben, was passiert, wenn er den Link aktiviert:

```html
<a href="tel:+493012345678">Reservierungs-Hotline anrufen: +49 (0)30 123 45 678</a>
```

Hier ist unmissverständlich klar, welche Aktion ausgelöst wird. Vermeide vage Formulierungen wie "Hier klicken". Wenn du aus Designgründen nur ein Icon verwenden möchtest, solltest du unbedingt ein `aria-label` setzen, um den Zweck des Links für assistierende Technologien zu beschreiben:

```html
<!-- Weniger empfohlen, aber möglich, wenn es das Design erfordert -->
<a href="tel:+493012345678" aria-label="Reservierungs-Hotline anrufen">
  <img src="telefon-icon.svg" alt="">
</a>
```

Die Verlinkung von Telefonnummern ist ein kleines, aber mächtiges Detail in der Webentwicklung. Korrekt umgesetzt, senkt sie die Hürde für Nutzer, mit dir oder deinem Unternehmen in Kontakt zu treten, und trägt maßgeblich zu einer positiven und effizienten Benutzererfahrung bei – besonders in unserer mobilen Welt.
