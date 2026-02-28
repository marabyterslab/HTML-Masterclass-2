# Attribute wie placeholder und maxlength

### Mehr Kontrolle und Hilfestellung: Die Attribute `placeholder` und `maxlength`

Nachdem du nun die Grundlagen von Texteingabefeldern kennst, wollen wir uns anschauen, wie du sie für deine Nutzerinnen und Nutzer verständlicher und robuster machen kannst. Ein einfaches `<input type="text">` ist zwar funktional, aber oft fehlt es an Kontext oder an nötigen Einschränkungen. Hier kommen spezielle Attribute ins Spiel, die dir mehr Kontrolle über das Verhalten und die Darstellung deiner Formularfelder geben. Zwei der wichtigsten und am häufigsten verwendeten Helfer sind `placeholder` und `maxlength`.

#### Der `placeholder`: Ein nützlicher Wegweiser

Stell dir vor, du siehst ein leeres Eingabefeld mit der Beschriftung "Benutzername". Das ist klar, aber was genau wird erwartet? Ein Spitzname? Der volle Name? Eine E-Mail-Adresse? Das `placeholder`-Attribut ermöglicht es dir, einen kurzen Hinweis oder ein Beispiel direkt in das Eingabefeld zu schreiben. Dieser Text ist meist grau dargestellt und verschwindet automatisch, sobald der Nutzer beginnt, etwas in das Feld einzutippen.

Die Anwendung ist denkbar einfach. Du fügst das Attribut direkt in dein `<input>`-Tag ein:

```html
<label for="username">Benutzername:</label>
<input type="text" id="username" name="username" placeholder="z.B. max_mustermann88">

<label for="email">E-Mail-Adresse:</label>
<input type="email" id="email" name="email" placeholder="deine.adresse@beispiel.de">
```

Im Browser sieht das dann so aus, dass die Texte "z.B. max_mustermann88" und "deine.adresse@beispiel.de" direkt in den leeren Feldern erscheinen. Sie geben eine klare Vorstellung davon, welches Format die Eingabe haben sollte. Sobald du in das Feld klickst und zu tippen beginnst, ist der Platzhaltertext verschwunden.

Das `placeholder`-Attribut ist nicht nur auf `<input type="text">` beschränkt. Du kannst es bei den meisten textbasierten Eingabetypen wie `email`, `password`, `search`, `tel` und `url` sowie bei mehrzeiligen Textfeldern (`<textarea>`) verwenden.

##### Eine wichtige Abgrenzung: `placeholder` ist kein Ersatz für `<label>`

Dies ist einer der häufigsten Fehler, der bei der Verwendung von `placeholder`-Texten gemacht wird. Es mag verlockend sein, auf das `<label>`-Element zu verzichten und die Beschriftung direkt als Platzhalter in das Feld zu schreiben, um ein minimalistisches Design zu erzielen.

**Ein Beispiel dafür, wie du es nicht machen solltest:**

```html
<!-- FALSCH: Unzugänglich und benutzerunfreundlich -->
<input type="text" name="firstname" placeholder="Vorname">
```

Warum ist das ein Problem? Aus mehreren entscheidenden Gründen:

1.  **Barrierefreiheit (Accessibility):** Screenreader, die blinden oder sehbehinderten Menschen Webseiten vorlesen, behandeln `placeholder`-Text oft nicht als vollwertige Beschriftung. Viele Screenreader ignorieren ihn komplett oder lesen ihn nur unter bestimmten Umständen vor. Ein `<label>`, das korrekt mit dem `for`-Attribut mit dem Eingabefeld verknüpft ist, ist hingegen die semantisch richtige und zuverlässigste Methode, um ein Formularfeld zu beschriften.

2.  **Benutzerfreundlichkeit (Usability):** Sobald der Nutzer in das Feld klickt und mit dem Tippen beginnt, verschwindet der `placeholder`. Was aber, wenn der Nutzer kurz abgelenkt wird und vergisst, was er in dieses Feld eintragen sollte? Er muss nun seine eigene Eingabe löschen, um den Platzhalter wieder sichtbar zu machen. Das ist umständlich und frustrierend. Ein permanent sichtbares `<label>` verhindert dieses Problem.

3.  **Kontrast und Lesbarkeit:** Platzhaltertexte werden von Browsern standardmäßig in einem helleren Grau dargestellt, um sie von der tatsächlichen Nutzereingabe zu unterscheiden. Dieser geringe Kontrast kann für Menschen mit Sehschwächen schwer zu lesen sein.

Die goldene Regel lautet also: **Verwende `placeholder` immer als Ergänzung, niemals als Ersatz für ein `<label>`.** Der Platzhalter dient als Beispiel oder Format-Hinweis, während das `<label>` die eigentliche, unveränderliche Beschriftung des Feldes darstellt.

**So machst du es richtig:**

```html
<label for="vorname">Vorname:</label>
<input type="text" id="vorname" name="vorname" placeholder="z.B. Erika">
```

Hier ist die Funktion klar getrennt: Das `<label>` sagt, *was* hier hingehört (der Vorname), und der `placeholder` gibt ein hilfreiches *Beispiel* (z.B. Erika).

#### Das `maxlength`-Attribut: Grenzen setzen

Manchmal möchtest du die Länge der Eingabe, die ein Nutzer machen kann, begrenzen. Stell dir eine Postleitzahl in Deutschland vor – sie hat immer genau fünf Ziffern. Oder denke an eine Kurznachricht auf einer Plattform, die auf 280 Zeichen begrenzt ist. Für solche Fälle gibt es das `maxlength`-Attribut.

Es definiert die maximale Anzahl an Zeichen, die in ein Eingabefeld eingegeben werden können. Der Browser verhindert dann automatisch, dass der Nutzer mehr Zeichen eingibt. Er kann einfach nicht weitertippen, sobald das Limit erreicht ist.

Die Anwendung ist wieder sehr direkt:

```html
<label for="plz">Postleitzahl:</label>
<input type="text" id="plz" name="plz" maxlength="5">

<label for="kurzbio">Kurzbiografie (max. 150 Zeichen):</label>
<textarea id="kurzbio" name="kurzbio" maxlength="150"></textarea>
```

Im ersten Beispiel kann der Nutzer nicht mehr als fünf Zeichen für die Postleitzahl eingeben. Im zweiten Beispiel stoppt die Eingabemöglichkeit in der `textarea` nach 150 Zeichen.

##### Usability-Überlegungen bei `maxlength`

Das `maxlength`-Attribut ist ein mächtiges Werkzeug, sollte aber mit Bedacht eingesetzt werden. Es ist eine "harte" Grenze. Der Nutzer erhält vom Browser standardmäßig kein visuelles Feedback, warum er nicht weitertippen kann. Die Eingabe stoppt einfach. Das kann verwirrend sein, wenn dem Nutzer nicht klar ist, dass es eine Längenbeschränkung gibt.

Daher ist es eine gute Praxis, dem Nutzer die Beschränkung mitzuteilen, so wie im Beispiel der Kurzbiografie: `(max. 150 Zeichen)`. Bei Feldern, deren Längenbeschränkung offensichtlich ist (wie bei einer Postleitzahl), ist dies weniger kritisch.

Für eine bessere Nutzererfahrung, insbesondere bei größeren Textfeldern wie einer `<textarea>`, wird oft JavaScript eingesetzt, um einen Zeichenzähler anzuzeigen (z.B. "120/150 Zeichen übrig"). Das HTML-Attribut `maxlength` sorgt hierbei für die grundlegende technische Begrenzung, während JavaScript die benutzerfreundliche Rückmeldung liefert.

#### Die Kombination macht's: `placeholder` und `maxlength` im Einklang

Natürlich kannst du beide Attribute problemlos miteinander kombinieren, um ein noch präziseres und benutzerfreundlicheres Eingabefeld zu schaffen. Nehmen wir an, du möchtest einen Aktivierungscode abfragen, der immer aus 6 Großbuchstaben besteht.

```html
<label for="activation_code">Aktivierungscode:</label>
<input type="text" id="activation_code" name="activation_code" 
       placeholder="z.B. AB12CD" 
       maxlength="6">
```

In diesem Beispiel geschieht Folgendes:
1.  Das `<label>` beschriftet das Feld klar als "Aktivierungscode".
2.  Der `placeholder` gibt dem Nutzer ein visuelles Beispiel für das erwartete Format ("z.B. AB12CD").
3.  Das `maxlength`-Attribut stellt sicher, dass technisch nicht mehr als 6 Zeichen eingegeben werden können.

Diese Kombination führt zu einem robusten und intuitiven Formularfeld, das die Wahrscheinlichkeit von Fehleingaben deutlich reduziert und den Nutzer sanft durch den Prozess leitet.

#### Ein kleiner Ausblick: Der kleine Bruder `minlength`

Passend zu `maxlength` gibt es auch das Attribut `minlength`, das eine Mindestanzahl an Zeichen vorschreibt. Im Gegensatz zu `maxlength`, das die Eingabe physisch stoppt, ist `minlength` ein Validierungsattribut. Das bedeutet, der Nutzer *kann* weniger Zeichen eingeben, aber das Formular lässt sich nicht absenden, solange die Bedingung nicht erfüllt ist. Der Browser zeigt eine Fehlermeldung an. Ein klassisches Beispiel wäre ein Passwort, das mindestens 8 Zeichen lang sein muss:

```html
<label for="passwort">Passwort:</label>
<input type="password" id="passwort" name="passwort" minlength="8">
```

Die Attribute `placeholder` und `maxlength` sind also weit mehr als nur Dekoration. Sie sind fundamentale Werkzeuge, um die Qualität deiner Formulare zu steigern, indem sie dem Nutzer klare Hinweise geben und gleichzeitig technische Grenzen für die Eingabe festlegen. Sie tragen maßgeblich zu einer besseren User Experience und einer höheren Datenqualität bei.
