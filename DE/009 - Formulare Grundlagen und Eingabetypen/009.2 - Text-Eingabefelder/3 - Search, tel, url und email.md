# Search, tel, url und email

### Spezialisierte Textfelder: Search, Tel, URL und Email

Wenn du an ein Formular denkst, kommt dir wahrscheinlich als Erstes ein einfaches Textfeld in den Sinn – ein `input` vom Typ `text`. Es ist der universelle Klassiker für Namen, Adressen oder jeden beliebigen Freitext. Doch die Welt der Formulare ist weitaus differenzierter. HTML bietet dir eine Reihe spezialisierter `input`-Typen, die auf den ersten Blick wie gewöhnliche Textfelder aussehen, aber unter der Haube entscheidende Vorteile für dich und die Nutzer deiner Webseite bringen.

Diese Spezialisierung hat zwei zentrale Gründe: **Semantik** und **Benutzererfahrung (User Experience)**.

1.  **Semantik:** Indem du dem Browser mitteilst, welche Art von Information du erwartest – zum Beispiel eine E-Mail-Adresse statt nur irgendeinem Text –, gibst du dem Feld eine klare Bedeutung. Browser, Suchmaschinen und assistierende Technologien (wie Screenreader) können diese Information nutzen, um die Seite besser zu verstehen und zu verarbeiten.
2.  **Benutzererfahrung:** Moderne Browser, insbesondere auf mobilen Geräten, passen die Benutzeroberfläche an den erwarteten Eingabetyp an. Das kann eine spezielle Tastatur sein, die die Eingabe erleichtert, oder eine eingebaute Validierung, die dem Nutzer sofortiges Feedback gibt.

In diesem Kapitel schauen wir uns vier dieser intelligenten Textfeld-Varianten genauer an: `email`, `url`, `tel` und `search`.

#### `type="email"`: Das Tor zur digitalen Post

Fast jedes Registrierungs- oder Kontaktformular benötigt eine E-Mail-Adresse. Anstatt hierfür ein generisches Textfeld zu verwenden, solltest du immer auf `type="email"` zurückgreifen.

```html
<form>
  <label for="user-email">Deine E-Mail-Adresse:</label>
  <input type="email" id="user-email" name="user_email" required>
</form>
```

Was passiert, wenn du diesen Typ verwendest?

**Client-seitige Validierung:** Der Browser führt eine einfache, aber effektive Prüfung durch, bevor das Formular überhaupt abgeschickt wird. Er kontrolliert, ob die Eingabe dem grundlegenden Muster einer E-Mail-Adresse entspricht. Das bedeutet nicht, dass er prüft, ob die Adresse tatsächlich existiert, aber er schaut, ob ein `@`-Zeichen und eine Domain (wie `beispiel.de`) vorhanden sind. Fehlt dies, wird der Nutzer mit einer standardisierten Fehlermeldung darauf hingewiesen. Dies ist eine erste Verteidigungslinie gegen simple Tippfehler und erspart dir eine grundlegende Prüfung auf dem Server.

**Optimierte Tastatur auf Mobilgeräten:** Der wohl größte Vorteil für die Nutzererfahrung zeigt sich auf Smartphones und Tablets. Sobald der Nutzer in ein `email`-Feld tippt, blendet das Betriebssystem eine Tastatur ein, die speziell für die Eingabe von E-Mail-Adressen optimiert ist. Das `@`-Zeichen und der Punkt (`.`) sind prominent platziert und direkt zugänglich. Das mühsame Umschalten auf die Sonderzeichen-Tastatur entfällt, was die Eingabe spürbar beschleunigt und komfortabler macht.

**Mehrere Adressen erlauben:** Manchmal möchtest du dem Nutzer erlauben, mehrere E-Mail-Adressen in einem einzigen Feld einzugeben, zum Beispiel um mehrere Empfänger für eine Einladung anzugeben. Dafür gibt es das `multiple`-Attribut.

```html
<label for="recipients">Empfänger (kommagetrennt):</label>
<input type="email" id="recipients" name="recipients" multiple>
```

Wenn dieses Attribut gesetzt ist, validiert der Browser eine durch Kommas getrennte Liste von E-Mail-Adressen. Jede einzelne Adresse in der Liste muss dabei dem gültigen Format entsprechen.

#### `type="url"`: Der richtige Ort für Webadressen

Ähnlich wie bei E-Mail-Adressen gibt es auch für Webadressen (URLs) einen eigenen Eingabetyp. Wenn du den Nutzer nach seiner Webseite, seinem Social-Media-Profil oder einem anderen Link fragst, ist `type="url"` die korrekte semantische Wahl.

```html
<form>
  <label for="website">Deine Webseite:</label>
  <input type="url" id="website" name="website_url" placeholder="https://deine-website.de">
</form>
```

Die Vorteile sind analog zu `type="email"`:

**Client-seitige Validierung:** Der Browser prüft, ob die Eingabe eine syntaktisch korrekte URL ist. Dazu gehört in der Regel ein Protokoll wie `http://` oder `https://`. Gibt der Nutzer nur `meine-seite.de` ein, wird das Formular beim Absenden blockiert und eine entsprechende Hinweismeldung angezeigt. Dies hilft, unvollständige oder fehlerhafte Links von vornherein zu vermeiden.

**Optimierte Tastatur auf Mobilgeräten:** Auch hier passt sich die virtuelle Tastatur an. Sie bietet Tasten wie den Schrägstrich (`/`), den Punkt (`.`) und oft auch eine `.com`-Taste direkt an, um die Eingabe von Webadressen zu vereinfachen.

Die Verwendung von `type="url"` sorgt dafür, dass die Daten, die bei dir ankommen, eine höhere Grundqualität haben und die Nutzerführung auf allen Geräten optimal ist.

#### `type="tel"`: Für Telefonnummern optimiert

Das Feld für Telefonnummern, `type="tel"`, ist ein Sonderfall und wird oft missverstanden. Es bietet eine entscheidende Funktion, verzichtet aber bewusst auf eine andere.

```html
<form>
  <label for="phone">Deine Telefonnummer:</label>
  <input type="tel" id="phone" name="phone_number">
</form>
```

Der offensichtlichste Vorteil ist wieder die **optimierte Tastatur auf Mobilgeräten**. Wer eine Telefonnummer eingeben muss, bekommt direkt das numerische Tastenfeld (den Ziffernblock) angezeigt. Dies ist eine massive Verbesserung der Benutzerfreundlichkeit im Vergleich zur Standardtastatur.

Was `type="tel"` jedoch **nicht** tut, ist eine Validierung des Formats. Und das aus gutem Grund: Das Format von Telefonnummern ist weltweit extrem uneinheitlich. Es gibt Ländervorwahlen, Ortsvorwahlen, Durchwahlen, und die Schreibweisen variieren stark durch die Verwendung von Leerzeichen, Bindestrichen oder Klammern.

*   `+49 176 1234567` (Deutschland)
*   `(555) 123-4567` (USA)
*   `01 23 45 67 89` (Frankreich)

Ein Browser kann unmöglich wissen, welches Format du erwartest. Eine feste Validierungsregel würde Nutzer aus anderen Regionen oder mit abweichenden Schreibgewohnheiten aussperren.

Wenn du ein bestimmtes Format erzwingen musst, ist das `pattern`-Attribut dein Werkzeug der Wahl. Mit einem regulären Ausdruck kannst du eine exakte Vorlage definieren. Zum Beispiel für eine deutsche Handynummer im Format `+49 1...` oder `01...`:

```html
<form>
  <label for="mobile-de">Deutsche Handynummer:</label>
  <input type="tel" id="mobile-de" name="mobile_de" 
         pattern="(\+49|0)1[5-7][0-9]\s?[0-9]{7,8}"
         title="Bitte gib eine gültige deutsche Handynummer ein (z.B. 0176 1234567 oder +49 176 1234567).">
</form>
```

In diesem Beispiel prüft der reguläre Ausdruck, ob die Nummer mit `+49` oder `0` beginnt, gefolgt von den typischen Ziffern für Mobilfunknetze und der entsprechenden Anzahl weiterer Ziffern. Das `title`-Attribut ist hierbei wichtig, da sein Inhalt dem Nutzer als Teil der Fehlermeldung angezeigt wird und ihm erklärt, welches Format erwartet wird.

Die Kernbotschaft bei `type="tel"` lautet also: Semantik und eine optimierte mobile Eingabe sind garantiert. Für die Formatvalidierung bist du selbst verantwortlich, idealerweise mit dem `pattern`-Attribut.

#### `type="search"`: Das Feld für die Spurensuche

Auf den ersten Blick ist ein Suchfeld (`type="search"`) kaum von einem normalen Textfeld zu unterscheiden. Die Unterschiede sind subtil, aber wirkungsvoll und verbessern die Interaktion mit Suchfunktionen.

```html
<form action="/suche" method="get">
  <label for="site-search">Website durchsuchen:</label>
  <input type="search" id="site-search" name="q">
  <button type="submit">Suchen</button>
</form>
```

Die semantische Kennzeichnung als Suchfeld hat folgende Auswirkungen:

**Angepasstes Styling und Verhalten:** Viele Browser rendern ein `search`-Feld leicht anders. Ein häufiges Merkmal ist das kleine `x`-Symbol, das am rechten Rand des Feldes erscheint, sobald der Nutzer Text eingibt. Ein Klick auf dieses Symbol löscht den Inhalt des Feldes sofort. Dieses kleine Detail ist eine etablierte Konvention, die Nutzer von Suchfeldern erwarten und die das schnelle Ausführen neuer Suchanfragen erleichtert.

**Optimierte Tastatur:** Auch hier kann sich die mobile Tastatur anpassen. Statt einer normalen "Enter"- oder "Return"-Taste wird oft eine Taste mit der Aufschrift "Go", "Suchen" oder einem Lupen-Symbol angezeigt. Das Drücken dieser Taste löst typischerweise das Absenden des Formulars aus, was den Suchvorgang intuitiver gestaltet.

**Verlauf und Autovervollständigung:** Browser können den Verlauf von Eingaben in `search`-Feldern anders behandeln als bei anderen Feldern, um dem Nutzer frühere Suchanfragen schneller wieder vorzuschlagen.

Obwohl die visuellen Unterschiede gering sein mögen, signalisiert `type="search"` klar und deutlich den Zweck des Eingabefeldes. Es ist eine kleine, aber wichtige Geste, die die Konsistenz und Benutzerfreundlichkeit deiner Webseite erhöht.

Zusammenfassend lässt sich sagen, dass die Verwendung dieser spezialisierten Eingabetypen weit mehr als nur eine kosmetische Entscheidung ist. Du gibst dem Browser wertvolle kontextuelle Informationen, die er nutzt, um die Eingabe für den Nutzer einfacher, schneller und weniger fehleranfällig zu machen. Es ist ein Paradebeispiel dafür, wie durchdachtes, semantisches HTML direkt zu einer besseren User Experience führt.
