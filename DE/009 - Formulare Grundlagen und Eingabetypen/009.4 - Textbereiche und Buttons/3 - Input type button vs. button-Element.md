# Input type button vs. button-Element

### Der feine Unterschied: `<input type="button">` vs. das `<button>`-Element

Wenn du beginnst, interaktive Elemente in deine Webseiten einzubauen, stößt du unweigerlich auf die Notwendigkeit, Klickflächen zu erstellen – Buttons. In HTML gibt es dafür auf den ersten Blick zwei Kandidaten, die sehr ähnlich wirken: `<input type="button">` und das `<button>`-Element. Beide erzeugen eine Schaltfläche, die ein Benutzer anklicken kann. Doch obwohl sie ein ähnliches Ziel verfolgen, gibt es grundlegende Unterschiede in ihrer Funktionsweise, Flexibilität und ihrem semantischen Einsatz. Die Entscheidung für das eine oder andere Element kann weitreichende Konsequenzen für die Gestaltung, Funktionalität und Barrierefreiheit deiner Formulare und Interfaces haben.

Lass uns diese beiden Wege, einen Button zu erstellen, im Detail beleuchten.

#### Der Klassiker: `<input type="button">`

Das `<input>`-Element ist ein Urgestein von HTML-Formularen. Es ist ein sogenanntes leeres oder "void" Element, was bedeutet, dass es keinen schließenden Tag hat. Seine gesamte Konfiguration geschieht über Attribute. Um einen einfachen Button zu erzeugen, verwendest du das `type`-Attribut mit dem Wert `button`.

```html
<input type="button" value="Klick mich">
```

Die Beschriftung des Buttons – also der Text, der darauf angezeigt wird – wird ausschließlich über das `value`-Attribut festgelegt. Und genau hier liegt die größte Einschränkung von `<input type="button">`: Du kannst als Inhalt nur reinen, unformatierten Text verwenden.

**Die wichtigsten Eigenschaften von `<input type="button">`:**

1.  **Nur-Text-Inhalt:** Der Inhalt wird durch das `value`-Attribut bestimmt und kann keinen HTML-Code enthalten. Du kannst also kein Wort fett hervorheben, keinen Zeilenumbruch einfügen oder gar ein Icon-Bild platzieren.

    ```html
    <!-- Funktioniert NICHT wie erwartet -->
    <input type="button" value="<strong>Wichtig!</strong> Speichern">
    ```

    Dieser Code würde einen Button mit dem exakten Text `<strong>Wichtig!</strong> Speichern` erzeugen, anstatt das Wort "Wichtig!" fett darzustellen.

2.  **Kein Standardverhalten:** Ein `<input>` mit dem Typ `button` hat von Natur aus keine vordefinierte Funktion innerhalb eines `<form>`-Elements. Er sendet das Formular nicht ab und setzt es auch nicht zurück. Seine einzige Aufgabe ist es, auf einen Klick zu warten, um dann in der Regel eine JavaScript-Funktion auszulösen.

3.  **Die Familie:** Es ist wichtig zu wissen, dass `<input type="button">` Teil einer Familie ist. Es gibt auch `<input type="submit">` und `<input type="reset">`. Diese sehen zwar ähnlich aus, haben aber im Kontext eines Formulars eine feste Aufgabe:
    *   `<input type="submit">`: Sendet das Formular an die im `action`-Attribut des `<form>`-Tags angegebene Adresse.
    *   `<input type="reset">`: Setzt alle Eingabefelder im Formular auf ihre ursprünglichen Werte zurück.

Diese Verwandtschaft ist wichtig, um zu verstehen, warum `<input type="button">` als die "neutrale" Variante konzipiert wurde – ein Button ohne vordefinierte Formular-Aktion.

#### Der moderne Alleskönner: Das `<button>`-Element

Das `<button>`-Element wurde später in den HTML-Standard (mit HTML 4.01) eingeführt, um die Einschränkungen des `<input>`-Buttons zu überwinden. Im Gegensatz zum `<input>`-Element ist `<button>` ein Container-Element. Das bedeutet, es hat einen öffnenden und einen schließenden Tag: `<button>...</button>`.

```html
<button>Klick mich</button>
```

Der entscheidende Vorteil liegt darin, was du *zwischen* diese beiden Tags platzieren kannst.

**Die wichtigsten Eigenschaften des `<button>`-Elements:**

1.  **Reichhaltiger Inhalt (Rich Content):** Zwischen `<button>` und `</button>` kannst du nahezu beliebigen HTML-Code platzieren. Das eröffnet dir eine Welt voller gestalterischer Möglichkeiten. Du kannst Text formatieren, Bilder einfügen, Icons verwenden und vieles mehr.

    ```html
    <!-- Ein Button mit einem Icon und fettgedrucktem Text -->
    <button>
      <img src="icons/save.svg" alt="" width="16" height="16">
      <strong>Jetzt Speichern</strong>
    </button>
    
    <!-- Ein Button mit mehrzeiligem Text -->
    <button>
      Akzeptieren &<br>
      Fortfahren
    </button>
    ```

    Diese Flexibilität macht das `<button>`-Element zur ersten Wahl für modernes, ansprechendes Webdesign.

2.  **Das `type`-Attribut ist entscheidend:** Ähnlich wie das `<input>`-Element kann auch das `<button>`-Element ein `type`-Attribut haben. Die möglichen Werte sind `submit`, `reset` und `button`. Hier gibt es jedoch einen sehr wichtigen Unterschied im Standardverhalten:

    *   `<button type="submit">`: Sendet das Formular ab.
    *   `<button type="reset">`: Setzt das Formular zurück.
    *   `<button type="button">`: Hat keine Standard-Formularaktion und dient, genau wie `<input type="button">`, als Ziel für JavaScript.

    **Achtung, Falle:** Wenn du bei einem `<button>`-Element innerhalb eines `<form>`-Tags das `type`-Attribut weglässt, ist der Standardwert in allen modernen Browsern `type="submit"`! Das ist eine häufige Fehlerquelle. Du erstellst vielleicht einen Button, der nur eine JavaScript-Aktion auslösen soll (z. B. ein Modal öffnen), wunderst dich dann aber, warum bei jedem Klick die Seite neu lädt. Der Grund ist, dass der Button ohne explizites `type="button"` versucht, das Formular abzusenden.

    **Eine goldene Regel lautet daher: Gib einem `<button>`-Element immer explizit ein `type`-Attribut, es sei denn, es soll tatsächlich ein Submit-Button sein.**

    ```html
    <form action="/speichern" method="post">
      <!-- ... Formularfelder ... -->
    
      <!-- Dieser Button sendet das Formular ab (Standardverhalten) -->
      <button>Speichern</button> 
    
      <!-- Dieser Button tut nichts von sich aus, er wartet auf JavaScript -->
      <button type="button" onclick="showHelp()">Hilfe anzeigen</button>
    </form>
    ```

#### Direkte Gegenüberstellung

Um die Unterschiede noch klarer zu machen, hier eine Zusammenfassung der wichtigsten Punkte:

| Kriterium | `<input type="button">` | `<button>`-Element |
| :--- | :--- | :--- |
| **Inhalt** | Nur reiner Text, definiert über das `value`-Attribut. | Beliebiger HTML-Inhalt (Text, Bilder, Icons, Formatierungen) zwischen den Tags. |
| **Syntax** | Leeres (void) Element: `<input ...>` | Container-Element: `<button>...</button>` |
| **Standardverhalten im Formular** | Keines. Es ist ein neutraler Button für Skripting. | `type="submit"` ist der Standard. Löst ohne explizite Angabe von `type="button"` eine Formularübermittlung aus. |
| **Styling mit CSS** | Schwieriger zu gestalten. Pseudoelemente wie `::before` und `::after` funktionieren nicht, da es ein "replaced element" ist. Das Aussehen kann je nach Betriebssystem stark variieren. | Sehr flexibel und konsistent mit CSS zu gestalten. Verhält sich wie ein normaler Block/Inline-Block und unterstützt Pseudoelemente uneingeschränkt. |
| **Barrierefreiheit (Accessibility)** | Der zugängliche Name wird aus dem `value`-Attribut generiert. | Der zugängliche Name wird aus dem Inhalt der Tags generiert. Dies bietet mehr Flexibilität, um z. B. für Screenreader unsichtbaren, aber für die Barrierefreiheit wichtigen Text hinzuzufügen. |

#### Wann solltest du was verwenden? Eine klare Empfehlung

Nachdem wir die technischen Unterschiede beleuchtet haben, stellt sich die praktische Frage: Welches Element ist die bessere Wahl?

In der modernen Webentwicklung hat sich das **`<button>`-Element fast vollständig durchgesetzt**. Die Gründe dafür sind offensichtlich:

1.  **Überlegene Gestaltungsfreiheit:** Die Möglichkeit, Icons und formatierten Text zu verwenden, ist für heutige Benutzeroberflächen unerlässlich. Mit `<input type="button">` bist du extrem eingeschränkt. Mit `<button>` kannst du komplexe, visuell ansprechende Schaltflächen erstellen, die sich nahtlos in dein Design einfügen.

2.  **Bessere CSS-Kontrolle:** Das Styling von Formularelementen wie `<input>` kann frustrierend sein, da Browser und Betriebssysteme oft ihre eigenen Standard-Designs durchsetzen. Das `<button>`-Element verhält sich in dieser Hinsicht weitaus berechenbarer und gibt dir die volle Kontrolle über Aussehen und Verhalten, inklusive Pseudoelementen für fortgeschrittene Effekte.

3.  **Semantische Klarheit:** Obwohl beide einen Button erzeugen, kommuniziert `<button>Ein Formular absenden</button>` die Absicht oft klarer als `<input type="submit" value="Ein Formular absenden">`.

Gibt es überhaupt noch einen Grund, `<input type="button">` zu verwenden?
Die Anwendungsfälle sind heutzutage sehr selten. Man könnte es in Betracht ziehen, wenn:
*   Du einen extrem simplen, reinen Text-Button benötigst und dir sicher sein willst, dass er keinerlei Standard-Styling-Komplikationen mit sich bringt.
*   Du in einem sehr alten Projekt arbeitest, das konsistent `<input>`-Elemente für alle Formular-Interaktionen verwendet.
*   Du absolut sicherstellen willst, dass der Button keine Submit-Funktion hat und die explizite Angabe von `type="button"` beim `<button>`-Element vermeiden möchtest (was aber kein guter Grund ist).

Für praktisch alle neuen Projekte und modernen Webanwendungen gilt jedoch: **Verwende das `<button>`-Element.** Es ist flexibler, leistungsfähiger und der de-facto-Standard für interaktive Schaltflächen. Denk nur immer daran, das `type`-Attribut bewusst zu setzen, um unerwartetes Verhalten zu vermeiden.
