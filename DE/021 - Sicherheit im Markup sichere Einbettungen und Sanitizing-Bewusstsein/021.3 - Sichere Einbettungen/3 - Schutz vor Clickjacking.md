# Schutz vor Clickjacking

### Schutz vor Clickjacking: Wenn Klicks zur Falle werden

Stell dir vor, du surfst auf einer scheinbar harmlosen Webseite. Vielleicht lockt ein Gewinnspiel oder ein lustiges Katzenvideo. Du siehst einen großen, einladenden Button mit der Aufschrift „Jetzt Video ansehen!“. Du klickst darauf – aber anstatt eines Videos zu sehen, hast du unwissentlich auf deinem Social-Media-Profil gepostet, einen Artikel in einem Online-Shop gekauft oder sogar dein Konto gelöscht.

Was ist passiert? Du bist Opfer eines „Clickjacking“-Angriffs geworden. Dieser Begriff, der sich aus „Click“ und „Hijacking“ (Entführung) zusammensetzt, beschreibt eine Technik, bei der deine Klicks auf einer Webseite „entführt“ und auf ein anderes, unsichtbares Element umgeleitet werden. Der technische Fachbegriff lautet auch „UI-Redress-Angriff“, da die Benutzeroberfläche (User Interface, UI) manipuliert wird, um dich zu täuschen.

#### Wie funktioniert ein Clickjacking-Angriff?

Die grundlegende Mechanik hinter Clickjacking ist clever und erschreckend einfach. Sie nutzt eine Standardfunktion von HTML, die du bereits kennst: den `<iframe>`. Ein Angreifer geht dabei typischerweise wie folgt vor:

1.  **Erstellen der Köder-Seite:** Der Angreifer erstellt eine Webseite mit einem verlockenden Inhalt, zum Beispiel einem Button oder einem Link, der dich zum Klicken animieren soll.
2.  **Einbetten der Ziel-Seite:** Auf dieser Köder-Seite wird die Webseite, die das eigentliche Ziel des Angriffs ist, in einem `<iframe>` eingebettet. Das könnte deine Banking-Webseite, dein Social-Media-Profil oder ein Online-Shop sein – jede Seite, auf der du eingeloggt bist und Aktionen durchführen kannst.
3.  **Manipulation der Darstellung:** Jetzt kommt der entscheidende Trick. Der Angreifer manipuliert den `<iframe>` mit CSS so, dass er für dich komplett unsichtbar ist. Meistens wird dafür die `opacity`-Eigenschaft auf `0` gesetzt. Der unsichtbare iFrame wird dann per `position: absolute` und einem hohen `z-index` exakt über dem sichtbaren Köder-Element platziert.
4.  **Die Falle schnappt zu:** Du besuchst die Seite des Angreifers und siehst nur den Köder-Button. Wenn du darauf klickst, geht dein Klick aber nicht an diesen Button, sondern „fällt“ durch die sichtbare Ebene hindurch und trifft stattdessen auf das unsichtbare Element innerhalb des iframes – zum Beispiel den „Geld überweisen“-Button auf deiner Banking-Seite oder den „Account löschen“-Button in deinen Profileinstellungen. Da du auf der Zielseite bereits angemeldet bist, wird die Aktion sofort ausgeführt, ohne dass du es merkst.

Hier ist ein vereinfachtes Beispiel, wie der Code einer Angreifer-Seite aussehen könnte:

**HTML:**
```html
<!DOCTYPE html>
<html>
<head>
  <title>Gewinne ein tolles Auto!</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Klicke hier, um am Gewinnspiel teilzunehmen!</h1>
  <button class="koeder-button">Teilnehmen</button>
  
  <!-- Der unsichtbare iFrame mit der Ziel-Seite -->
  <iframe src="https://deine-social-media-seite.de/einstellungen/profil-loeschen" class="hidden-frame"></iframe>
</body>
</html>
```

**CSS:**
```css
/* Der sichtbare Köder-Button */
.koeder-button {
  padding: 20px;
  font-size: 24px;
  cursor: pointer;
}

/* Der unsichtbare, manipulierte iFrame */
.hidden-frame {
  position: absolute;
  /* Exakte Positionierung über dem Köder-Button */
  top: 50px; 
  left: 20px;
  
  /* Größe des "Löschen"-Buttons innerhalb des iframes */
  width: 120px;
  height: 40px;
  
  /* Der entscheidende Trick: Der iFrame wird unsichtbar gemacht */
  opacity: 0;
  
  /* Stellt sicher, dass der iFrame über allem anderen liegt */
  z-index: 2;
}
```

Du siehst nur den „Teilnehmen“-Button. Der unsichtbare iFrame liegt aber genau darüber. Dein Klick trifft also nicht den Button, den du siehst, sondern den Button zum Löschen des Profils auf der eingebetteten Seite.

#### Die Verteidigung: Serverseitige HTTP-Header

Du fragst dich jetzt sicher, wie du deine eigene Webseite vor solchen Angriffen schützen kannst. Die gute Nachricht ist: Die Lösung ist sehr effektiv und relativ einfach umzusetzen. Der Schutz vor Clickjacking findet nicht primär in deinem HTML-Markup statt, sondern auf der Serverseite. Du teilst dem Browser über HTTP-Header mit, ob und wie deine Seite in einem `<iframe>`, `<frame>`, `<object>` oder `<embed>` dargestellt werden darf.

Es gibt zwei zentrale HTTP-Header, die du dafür kennen und nutzen solltest.

##### 1. X-Frame-Options (Der Klassiker)

Der `X-Frame-Options`-Header war die erste standardisierte Antwort auf Clickjacking und wird auch heute noch von allen gängigen Browsern sehr gut unterstützt. Er ist einfach zu konfigurieren und bietet drei mögliche Anweisungen:

*   `DENY`: Dies ist die restriktivste und sicherste Option. Sie verbietet es jeder anderen Seite, deine Webseite in einem Frame darzustellen. Wenn du nicht explizit vorhast, dass deine Inhalte woanders eingebettet werden sollen, ist dies die beste Wahl.
*   `SAMEORIGIN`: Diese Option erlaubt das Einbetten deiner Seite nur dann, wenn die einbettende Seite vom selben Ursprung (gleiches Protokoll, gleicher Host, gleicher Port) stammt. Das ist nützlich, wenn du innerhalb deiner eigenen Webanwendung Frames verwendest.
*   `ALLOW-FROM uri`: Diese Direktive erlaubte das Einbetten von einer spezifischen URL. **Achtung:** Diese Option ist veraltet, wurde nie von allen Browsern unterstützt und sollte nicht mehr verwendet werden.

**Konfigurationsbeispiel für Apache (`.htaccess` oder `httpd.conf`):**
```apache
# Verbietet das Einbetten komplett
Header always set X-Frame-Options "DENY"

# Oder: Erlaubt das Einbetten nur von der eigenen Domain
Header always set X-Frame-Options "SAMEORIGIN"
```

**Konfigurationsbeispiel für Nginx (`nginx.conf`):**
```nginx
# Verbietet das Einbetten komplett
add_header X-Frame-Options "DENY" always;

# Oder: Erlaubt das Einbetten nur von der eigenen Domain
add_header X-Frame-Options "SAMEORIGIN" always;
```

##### 2. Content-Security-Policy (CSP) mit `frame-ancestors` (Der moderne Standard)

Die Content Security Policy (CSP) ist ein umfassenderes Sicherheitskonzept, das als HTTP-Header gesendet wird und dem Browser eine ganze Reihe von Sicherheitsregeln vorgibt. Für den Schutz vor Clickjacking ist die Direktive `frame-ancestors` relevant. Sie ist der Nachfolger von `X-Frame-Options` und bietet mehr Flexibilität.

Die `frame-ancestors`-Direktive kontrolliert, welche Eltern-Dokumente (also welche Seiten) deine Seite einbetten dürfen. Die gängigsten Werte sind:

*   `'none'`: Entspricht `X-Frame-Options: DENY`. Kein Einbetten erlaubt.
*   `'self'`: Entspricht `X-Frame-Options: SAMEORIGIN`. Nur die eigene Domain darf einbetten.
*   `https://*.beispiel.de https://partner.com`: Du kannst eine oder mehrere spezifische Quellen (Domains, Subdomains) angeben, die deine Seite einbetten dürfen. Das ist der große Vorteil gegenüber `X-Frame-Options`.

Wenn ein Browser sowohl einen `X-Frame-Options`-Header als auch eine `CSP frame-ancestors`-Direktive erhält, hat die CSP-Direktive Vorrang.

**Konfigurationsbeispiel für Apache:**
```apache
# Verbietet das Einbetten komplett
Header set Content-Security-Policy "frame-ancestors 'none';"

# Oder: Erlaubt das Einbetten von der eigenen Domain und einer Partnerseite
Header set Content-Security-Policy "frame-ancestors 'self' https://partner.com;"
```

**Konfigurationsbeispiel für Nginx:**
```nginx
# Verbietet das Einbetten komplett
add_header Content-Security-Policy "frame-ancestors 'none';" always;

# Oder: Erlaubt das Einbetten von der eigenen Domain und einer Partnerseite
add_header Content-Security-Policy "frame-ancestors 'self' https://partner.com;" always;
```

#### Eine veraltete Methode: Frame-Busting mit JavaScript

Bevor es die HTTP-Header-Lösungen gab, versuchten Entwickler, Clickjacking mit clientseitigem JavaScript zu verhindern. Diese Technik wird als „Frame-Busting“ oder „Frame-Breaking“ bezeichnet. Die Idee dahinter ist, dass ein Skript auf deiner Seite prüft, ob sie in einem Frame geladen wird. Wenn ja, „bricht“ sie aus diesem Frame aus.

Ein einfaches Frame-Buster-Skript könnte so aussehen:

```javascript
// Prüft, ob das oberste Fenster (top) nicht das aktuelle Fenster (self) ist.
// Wenn das zutrifft, wird die Seite in einem Frame geladen.
if (top !== self) {
  // Lädt die eigene Seite im obersten Fenster neu und bricht so aus dem Frame aus.
  top.location.href = self.location.href;
}
```

**Aber Vorsicht:** Diese Methode ist heute nicht mehr zuverlässig! Angreifer haben Wege gefunden, solche Skripte zu umgehen. Beispielsweise kann der `sandbox`-Attribut des `<iframe>`-Elements die Navigation des Top-Levels verhindern. Frame-Busting-Skripte können daher ein falsches Gefühl von Sicherheit vermitteln und sollten **nicht** als primärer Schutzmechanismus eingesetzt werden. Sie sind bestenfalls eine zusätzliche, aber unzuverlässige Verteidigungslinie für sehr alte Browser, die die modernen Header nicht unterstützen.

#### Deine beste Verteidigungsstrategie

Um den bestmöglichen Schutz zu gewährleisten, solltest du eine „Defense in Depth“-Strategie verfolgen und beide Header-Methoden kombinieren. So schützt du sowohl moderne als auch ältere Browser.

Die empfohlene Konfiguration für eine Webseite, die nicht eingebettet werden soll, lautet:

1.  **Setze den CSP-Header:** `Content-Security-Policy: frame-ancestors 'none';`
2.  **Setze zusätzlich den X-Frame-Options-Header:** `X-Frame-Options: DENY;`

Wenn deine Seite nur von deiner eigenen Domain eingebettet werden soll:

1.  **Setze den CSP-Header:** `Content-Security-Policy: frame-ancestors 'self';`
2.  **Setze zusätzlich den X-Frame-Options-Header:** `X-Frame-Options: SAMEORIGIN;`

Indem du deinem Server beibringst, diese Header mit jeder Antwort zu senden, gibst du dem Browser eine klare Anweisung, das Einbetten deiner Seite zu blockieren. Ein Angreifer, der versucht, deine Seite in einen unsichtbaren `<iframe>` zu laden, wird scheitern – der Browser wird das Laden des Frames einfach verweigern. Damit ist die Grundlage für einen Clickjacking-Angriff von vornherein zerstört.
