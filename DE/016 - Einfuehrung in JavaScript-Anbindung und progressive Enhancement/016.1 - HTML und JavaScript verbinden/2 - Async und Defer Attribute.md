# Async und Defer Attribute

### Async und Defer: Die Kunst des asynchronen Skriptladens

Wenn du JavaScript in deine HTML-Seite einbindest, ist der einfachste Weg, den du kennst, wahrscheinlich dieser:

```html
<script src="mein-skript.js"></script>
```

Platziert im `<head>` oder am Ende des `<body>`, scheint dieser Ansatz unkompliziert. Doch hinter dieser einfachen Zeile verbirgt sich ein kritisches Detail, das die Ladezeit und das Nutzererlebnis deiner Webseite maßgeblich beeinflussen kann: das **synchrone, blockierende Laden**.

#### Das Standardverhalten: Eine Geduldsprobe für den Browser

Stell dir den Browser wie einen fleißigen Bauarbeiter vor, der Zeile für Zeile dein HTML-Dokument liest und daraus die Webseite aufbaut (diesen Prozess nennt man „Parsing“). Wenn dieser Bauarbeiter auf einen normalen `<script>`-Tag ohne zusätzliche Attribute stößt, passiert Folgendes:

1.  **Stopp!** Der Bauarbeiter legt sofort seine Arbeit nieder. Das Parsen des HTML-Dokuments wird angehalten.
2.  **Abholen:** Er geht los, um die JavaScript-Datei vom Server herunterzuladen (Fetch). Währenddessen steht die Baustelle still. Nichts passiert auf der Seite.
3.  **Ausführen:** Sobald die Datei heruntergeladen ist, wird sie sofort ausgeführt (Execution). Auch in dieser Zeit ruht die Baustelle.
4.  **Weiterarbeiten:** Erst nachdem das Skript vollständig ausgeführt wurde, nimmt der Bauarbeiter seine Arbeit wieder auf und parst den Rest des HTML-Dokuments.

Dieses Verhalten wird als **„parser-blocking“** bezeichnet. Es ist ein Flaschenhals für die Performance deiner Webseite. Wenn du ein großes Skript im `<head>` deiner Seite hast, kann es sein, dass der Nutzer für mehrere Sekunden eine leere, weiße Seite sieht, weil der Browser blockiert ist und noch keine sichtbaren Inhalte rendern konnte. Das ist eine schlechte User Experience und wird auch von Suchmaschinen negativ bewertet.

Genau hier kommen die Attribute `async` und `defer` ins Spiel. Sie sind deine Werkzeuge, um dem Browser mitzuteilen, wie er mit deinen Skripten umgehen soll, um diese Blockade zu umgehen.

#### Das `defer`-Attribut: Geordnet und geduldig

Das `defer`-Attribut (von engl. *to defer* = aufschieben) ist eine elegante Lösung für das Blockadeproblem. Wenn du ein Skript mit `defer` versiehst, gibst du dem Browser eine klare Anweisung:

```html
<script src="mein-skript.js" defer></script>
<script src="ein-weiteres-skript.js" defer></script>
```

Was passiert nun?

1.  **Herunterladen im Hintergrund:** Der Browser entdeckt den `<script>`-Tag, beginnt aber sofort mit dem Herunterladen der Datei im Hintergrund.
2.  **Kein Stopp:** Ganz wichtig: Der Browser hält das Parsen des HTML-Dokuments **nicht** an. Er arbeitet einfach weiter, während das Skript im Hintergrund lädt. Deine Seite wird also weiterhin aufgebaut und für den Nutzer sichtbar.
3.  **Ausführung nach dem Parsen:** Das Skript wird erst dann ausgeführt, wenn das gesamte HTML-Dokument fertig geparst wurde, aber noch bevor das `DOMContentLoaded`-Ereignis ausgelöst wird.
4.  **Garantierte Reihenfolge:** Wenn du mehrere Skripte mit `defer` einbindest, garantiert der Browser, dass sie in der Reihenfolge ausgeführt werden, in der sie im HTML-Dokument erscheinen. Das ist extrem wichtig, wenn ein Skript von einem anderen abhängt (z.B. wenn `ein-weiteres-skript.js` eine Funktion aus `mein-skript.js` benötigt).

Stell es dir wie bei einer Essensbestellung vor. Du gibst deine Bestellung auf (`defer`-Skript) und der Koch beginnt in der Küche mit der Zubereitung. Währenddessen kannst du dich in Ruhe an deinen Tisch setzen, die Speisekarte studieren und dich unterhalten (der Browser parst das HTML). Das Essen wird erst dann serviert (das Skript wird ausgeführt), wenn der Tisch vollständig gedeckt ist (HTML ist fertig geparst). Wenn du mehrere Gänge bestellt hast, werden sie in der richtigen Reihenfolge serviert.

**Wann solltest du `defer` verwenden?**
`defer` ist fast immer die beste Wahl für Skripte, die mit dem DOM interagieren oder deren Ausführungsreihenfolge wichtig ist. Da sie erst nach dem vollständigen Parsen des Dokuments laufen, kannst du sicher sein, dass alle HTML-Elemente verfügbar sind, wenn dein Code ausgeführt wird. Für die meisten deiner eigenen Anwendungsskripte ist `defer` die sicherste und performanteste Option.

#### Das `async`-Attribut: Schnell und unabhängig

Das `async`-Attribut (von engl. *asynchronous* = asynchron) verfolgt einen etwas anderen, aggressiveren Ansatz.

```html
<script src="analytics.js" async></script>
<script src="werbung.js" async></script>
```

So verhält sich ein Skript mit `async`:

1.  **Herunterladen im Hintergrund:** Genau wie bei `defer` wird das Skript im Hintergrund heruntergeladen, ohne das Parsen des HTML zu blockieren.
2.  **Sofortige Ausführung:** Hier liegt der entscheidende Unterschied. Sobald das Skript fertig heruntergeladen ist, wird das HTML-Parsing **sofort unterbrochen**, und das Skript wird ausgeführt.
3.  **Weiterarbeiten:** Nach der Ausführung wird das Parsen des HTML fortgesetzt.
4.  **Keine garantierte Reihenfolge:** Wenn du mehrere `async`-Skripte hast, gibt es keine Garantie für die Ausführungsreihenfolge. Es gilt das Prinzip: „Wer zuerst fertig ist, mahlt zuerst.“ Das Skript, das zuerst heruntergeladen wurde, wird auch zuerst ausgeführt, unabhängig von seiner Position im HTML.

Um bei unserer Analogie zu bleiben: `async` ist wie eine dringende E-Mail-Benachrichtigung. Du arbeitest an einer wichtigen Aufgabe (HTML parsen), während im Hintergrund E-Mails eintreffen (Skripte laden). Sobald eine E-Mail ankommt, lässt du alles stehen und liegen, liest sie und antwortest sofort (Skript ausführen), bevor du zu deiner ursprünglichen Aufgabe zurückkehrst. Die Reihenfolge, in der du die E-Mails beantwortest, hängt nur davon ab, wann sie in deinem Posteingang landen.

**Wann solltest du `async` verwenden?**
`async` eignet sich hervorragend für unabhängige Skripte, die nicht auf andere Skripte oder auf das vollständige DOM angewiesen sind. Typische Beispiele sind Tracking-Skripte (wie Google Analytics), Werbebanner oder Social-Media-Widgets. Diese Skripte laufen für sich allein und es ist oft nicht kritisch, *wann genau* sie ausgeführt werden, solange sie irgendwann laufen. Ihre Ausführung sollte den Aufbau des sichtbaren Teils deiner Seite nicht verzögern.

#### Der direkte Vergleich: Standard vs. `defer` vs. `async`

Um die Unterschiede noch klarer zu machen, hier eine Übersicht:

| Verhalten | `script` (ohne Attribut) | `script defer` | `script async` |
| :--- | :--- | :--- | :--- |
| **HTML-Parsing** | Blockiert während Download & Ausführung | Wird nicht blockiert | Wird nur während der Ausführung blockiert |
| **Download** | Sequenziell und blockierend | Parallel zum HTML-Parsing | Parallel zum HTML-Parsing |
| **Ausführung** | Sofort nach dem Download | Nach dem HTML-Parsing | Sofort nach dem Download |
| **Reihenfolge**| Garantiert (Reihenfolge im HTML) | Garantiert (Reihenfolge im HTML) | Nicht garantiert (Ladezeit entscheidet) |

![Ein Diagramm, das den Lade- und Ausführungsprozess von Skripten mit und ohne async/defer im Vergleich zum HTML-Parsing darstellt, wäre hier ideal platziert.]

#### Wichtige Hinweise und bewährte Praktiken

*   **Nur für externe Skripte:** `async` und `defer` haben nur eine Wirkung auf externe Skripte, die über das `src`-Attribut eingebunden werden. Inline-Skripte (Code direkt zwischen `<script>` und `</script>`) werden immer sofort und blockierend ausgeführt.
*   **Moderne Strategie:** Eine gängige und sehr gute Praxis ist es, alle Skripte in den `<head>` zu packen und ihnen `defer` zu geben. Dadurch startet der Download so früh wie möglich, ohne das Rendern der Seite zu blockieren, und die Ausführungsreihenfolge bleibt erhalten. Das alte Vorgehen, Skripte ans Ende des `<body>` zu setzen, löste dasselbe Problem, aber `defer` ist die sauberere und oft performantere Methode.
*   **Kombination ist möglich:** Du kannst `async`- und `defer`-Skripte auf derselben Seite mischen. Nutze `async` für die unabhängigen Drittanbieter-Skripte und `defer` für deine eigene Anwendungslogik.
*   **Was, wenn beides da ist?** Wenn du versehentlich `async` und `defer` auf denselben Skript-Tag schreibst, hat `async` Vorrang bei modernen Browsern. Ältere Browser, die `async` nicht kennen, könnten auf `defer` zurückfallen. Es ist jedoch am besten, sich für eines von beiden zu entscheiden.

Durch den bewussten Einsatz von `async` und `defer` nimmst du die Kontrolle über den Ladeprozess deiner Webseite zurück. Du verwandelst potenzielle Performance-Bremsen in einen effizienten, parallelen Prozess, der zu schnelleren Ladezeiten, einem flüssigeren Nutzererlebnis und letztendlich zu einer besseren Webseite führt.
