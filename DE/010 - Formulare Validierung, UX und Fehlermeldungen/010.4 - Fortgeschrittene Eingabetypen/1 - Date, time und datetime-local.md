# Date, time und datetime-local

### Datum und Uhrzeit: Die Eingabetypen `date`, `time` und `datetime-local`

In der Welt der Formulare sind wenige Eingaben so fehleranfällig wie die Abfrage von Datum und Uhrzeit. Jeder hat schon einmal vor drei separaten Dropdown-Feldern für Tag, Monat und Jahr gesessen oder versucht, ein Datum im "korrekten" Format (`TT.MM.JJJJ`? `MM/TT/JJ`?) in ein einfaches Textfeld einzutippen. Diese Ansätze sind nicht nur umständlich für deine Nutzer, sondern auch eine Quelle ständiger Kopfschmerzen bei der serverseitigen Verarbeitung.

Glücklicherweise bietet HTML moderne Eingabetypen, die diese Probleme elegant lösen. Mit `date`, `time` und `datetime-local` überlässt du die Darstellung und Auswahl dem Browser, der wiederum auf die nativen Steuerelemente des Betriebssystems zurückgreift. Das Ergebnis ist eine intuitive User Experience für den Nutzer und ein standardisiertes, verlässliches Datenformat für dich.

#### Der `date`-Typ – Ein Kalender für deine Formulare

Der einfachste und wahrscheinlich am häufigsten genutzte Typ in dieser Familie ist `date`. Er ist speziell für die Auswahl eines Datums – also Tag, Monat und Jahr – konzipiert.

Wenn du ein `<input>`-Feld mit `type="date"` definierst, rendert der Browser eine Benutzeroberfläche, die für die Datumsauswahl optimiert ist. Auf den meisten Desktop-Systemen erscheint ein kleines Kalendersymbol, das bei einem Klick einen interaktiven Kalender öffnet. Auf mobilen Geräten wird oft die native, für Touch-Bedienung optimierte Datumsauswahl des Betriebssystems angezeigt.

Ein einfaches Beispiel sieht so aus:

```html
<label for="geburtsdatum">Dein Geburtsdatum:</label>
<input type="date" id="geburtsdatum" name="geburtsdatum">
```

Das Entscheidende passiert jedoch hinter den Kulissen. Unabhängig davon, wie das Datum dem Nutzer angezeigt wird (z. B. als "15. Oktober 2023" in Deutschland oder "October 15, 2023" in den USA), ist der Wert, der mit dem Formular an den Server gesendet wird, immer im international standardisierten ISO-8601-Format: `YYYY-MM-DD`. Für das genannte Beispiel wäre der Wert also `2023-10-15`. Diese Konsistenz ist ein enormer Vorteil, da du dich auf der Serverseite nicht mehr mit der Interpretation verschiedener Datumsformate herumschlagen musst.

##### Einschränkung der Datumsauswahl mit `min` und `max`

Oft möchtest du die Auswahl auf einen bestimmten Zeitraum beschränken. Stell dir vor, du baust eine Buchungsmaske für ein Hotelzimmer, das erst ab morgen und nur für die nächsten 90 Tage verfügbar ist. Hierfür gibt es die Attribute `min` und `max`. Ihre Werte müssen ebenfalls im Format `YYYY-MM-DD` angegeben werden.

```html
<label for="anreisedatum">Anreisedatum:</label>
<input type="date" id="anreisedatum" name="anreisedatum" min="2024-03-16" max="2024-06-13">
```

Moderne Browser setzen diese Einschränkungen direkt in der Benutzeroberfläche um. Daten außerhalb des erlaubten Bereichs sind im Kalender-Widget oft ausgegraut und können nicht ausgewählt werden. Dies ist eine Form der clientseitigen Validierung, die die Nutzererfahrung erheblich verbessert, da ungültige Eingaben von vornherein verhindert werden.

Das `step`-Attribut existiert zwar auch für den `date`-Typ, seine Unterstützung und Nützlichkeit sind jedoch begrenzt. Es soll die Auswahl in bestimmten Intervallen (z. B. nur jeden zweiten Tag) ermöglichen, wird aber von vielen Browsern nicht intuitiv umgesetzt.

#### Der `time`-Typ – Präzision auf die Minute genau

Analog zum `date`-Typ dient `type="time"` der Auswahl einer Uhrzeit, ohne ein Datum zu berücksichtigen. Der Browser stellt hierfür typischerweise ein Eingabefeld mit Drehreglern oder eine Auswahlliste für Stunden und Minuten zur Verfügung.

```html
<label for="termin-zeit">Uhrzeit für den Termin:</label>
<input type="time" id="termin-zeit" name="termin-zeit">
```

Der Wert, der für den Server generiert wird, folgt dem 24-Stunden-Format `hh:mm` (Stunden:Minuten) oder, falls Sekunden relevant sind, `hh:mm:ss`. Ein Termin um halb drei nachmittags wird also als `14:30` gesendet.

##### Zeitfenster definieren mit `min`, `max` und `step`

Auch hier sind `min` und `max` äußerst nützlich, um die Auswahl einzugrenzen. Denk an die Öffnungszeiten eines Geschäfts von 9:00 Uhr bis 18:00 Uhr.

```html
<label for="abholzeit">Gewünschte Abholzeit:</label>
<input type="time" id="abholzeit" name="abholzeit" min="09:00" max="18:00">
```

Besonders mächtig wird der `time`-Typ in Kombination mit dem `step`-Attribut. `step` definiert die erlaubten Intervalle in Sekunden. Der Standardwert ist `60`, was bedeutet, dass der Nutzer nur ganze Minuten auswählen kann.

*   `step="1"`: Erlaubt die Auswahl von Sekunden. Das Eingabefeld zeigt dann auch ein Feld für Sekunden an.
*   `step="900"`: Erlaubt die Auswahl nur in 15-Minuten-Schritten (900 Sekunden = 15 Minuten).
*   `step="1800"`: Erlaubt die Auswahl nur zur vollen und halben Stunde.

```html
<label for="beratungsstart">Beginn der Beratung (alle 30 Min.):</label>
<input type="time" id="beratungsstart" name="beratungsstart" min="10:00" max="16:30" step="1800">
```

Diese Attribute ermöglichen dir eine sehr feingranulare Kontrolle über die erlaubten Eingaben, was die Datenqualität deutlich erhöht und Fehleingaben reduziert.

#### `datetime-local` – Das Beste aus beiden Welten

Manchmal müssen Datum und Uhrzeit gemeinsam in einem einzigen Feld erfasst werden. Genau dafür wurde `datetime-local` geschaffen. Es kombiniert die Funktionalität von `date` und `time` in einem einzigen Steuerelement. Der Browser präsentiert dem Nutzer eine kombinierte Oberfläche, in der er zuerst das Datum und anschließend die Uhrzeit auswählen kann.

```html
<label for="flug-abflug">Abflugzeitpunkt:</label>
<input type="datetime-local" id="flug-abflug" name="flug-abflug">
```

Der Name `datetime-local` ist dabei Programm: Es wird die lokale Zeit des Nutzers ohne Informationen zur Zeitzone erfasst. Der Wert, der an den Server übermittelt wird, ist eine Kombination der beiden zuvor besprochenen Formate, getrennt durch ein `T`: `YYYY-MM-DDThh:mm`. Ein Abflug am 20. Mai 2024 um 18:45 Uhr wird also zum Wert `2024-05-20T18:45`.

Auch für `datetime-local` kannst du `min`, `max` und `step` verwenden, um den gültigen Bereich präzise zu definieren.

```html
<label for="webinar-start">Beginn des Webinars:</label>
<input type="datetime-local"
       id="webinar-start"
       name="webinar-start"
       min="2024-04-01T09:00"
       max="2024-04-30T17:00">
```

In diesem Beispiel kann der Nutzer einen Zeitpunkt im April 2024 auswählen, aber nur werktags zwischen 9:00 und 17:00 Uhr, falls du die Wochenenden serverseitig oder mit zusätzlichem JavaScript herausfilterst. Die `min`- und `max`-Attribute beschränken hier den gesamten Zeitstempel.

#### Browser-Kompatibilität und die User Experience

Der größte Vorteil dieser Eingabetypen ist zugleich ihr charakteristisches Merkmal: Du gibst die Kontrolle über die Darstellung an den Browser ab. Ein Datums-Picker unter Chrome auf Windows sieht anders aus als unter Safari auf einem iPhone oder Firefox auf Linux.

Das ist aber kein Nachteil, sondern ein Feature. Nutzer sind mit den nativen Steuerelementen ihres Systems vertraut. Ein iPhone-Nutzer erwartet die typische iOS-Datumsauswahl, die er aus anderen Apps kennt. Ihm eine fremde, mit JavaScript gebaute Kalender-Komponente aufzuzwingen, kann die Usability sogar verschlechtern. Du bekommst also Barrierefreiheit und eine optimierte mobile Erfahrung quasi geschenkt.

Was passiert jedoch, wenn ein veralteter Browser einen dieser Typen nicht kennt? Die HTML-Spezifikation ist hier sehr robust: Der Browser fällt auf `type="text"` zurück. Das Formular bleibt also benutzbar. Der Nutzer sieht ein einfaches Textfeld und muss das Datum manuell eintippen. In diesem Fall verlierst du zwar die komfortable Benutzeroberfläche und die clientseitige Validierung, aber die grundlegende Funktionalität bleibt erhalten. Für solche Fälle ist es unerlässlich, dass du auf dem Server immer eine robuste Validierung implementierst, die auch mit manuell eingegebenen Datums- und Zeitwerten umgehen kann. Niemals solltest du dich allein auf die clientseitige Validierung des Browsers verlassen.

Für Projekte, bei denen ein absolut einheitliches Erscheinungsbild über alle Browser hinweg zwingend erforderlich ist, kommen oft JavaScript-Bibliotheken zum Einsatz, die die nativen Steuerelemente ersetzen. Dies erkaufst du dir jedoch mit zusätzlicher Komplexität und einer höheren Ladezeit. Für die meisten Anwendungsfälle ist der native Ansatz die beste, performanteste und nutzerfreundlichste Wahl.
