# Domain-Konfiguration

### Domain-Konfiguration: Deine Adresse im Web

Dein HTML-Projekt ist fertig, der Code ist sauber, und du hast bereits einen Ort im Netz gefunden, wo deine Dateien liegen – dein Hosting. Doch wie finden Besucher nun den Weg dorthin? Niemand wird sich eine komplizierte IP-Adresse wie `192.0.2.1` merken. Hier kommt die Domain-Konfiguration ins Spiel. Sie ist der entscheidende Schritt, um deinem Projekt eine einprägsame und professionelle Adresse zu geben, wie zum Beispiel `mein-projekt.de`. In diesem Kapitel verbinden wir deine Domain mit deinem Webserver.

#### Das Domain Name System (DNS) – Das Telefonbuch des Internets

Bevor wir in die technischen Details eintauchen, ist es wichtig, das grundlegende Prinzip zu verstehen: das Domain Name System, kurz DNS. Stell es dir wie ein riesiges, globales Telefonbuch vor. Früher, als es noch keine Smartphones gab, hast du im Telefonbuch nach dem Namen einer Person gesucht, um ihre Telefonnummer zu finden. Das DNS macht genau dasselbe, nur für das Internet.

Wenn du `www.beispiel.de` in deinen Browser eingibst, weiß der Browser zunächst nicht, welcher Computer (Server) auf der Welt damit gemeint ist. Computer kommunizieren über IP-Adressen – eindeutige Nummernfolgen. Dein Browser fragt also das DNS: "Hey, welche IP-Adresse gehört zu `www.beispiel.de`?" Das DNS schlägt in seinen gewaltigen Verzeichnissen nach und antwortet zum Beispiel mit `93.184.216.34`. Erst mit dieser Information kann dein Browser eine Verbindung zum richtigen Server aufbauen und deine Webseite anfordern.

Deine Aufgabe bei der Domain-Konfiguration ist es also, in diesem globalen Telefonbuch den richtigen Eintrag für deine Domain zu erstellen. Du musst dem DNS mitteilen, unter welcher IP-Adresse dein Webserver zu finden ist.

#### Die wichtigsten DNS-Einträge für dein Projekt

Die Einträge im DNS werden "Records" genannt. Für den Start deines HTML-Projekts sind vor allem zwei bis drei Typen von Records von entscheidender Bedeutung. Diese Konfiguration nimmst du in der Regel im Verwaltungsbereich deines Domain-Anbieters (auch "Registrar" genannt) vor, also dort, wo du deine Domain gekauft hast.

##### A-Record (Address Record)

Der A-Record ist der grundlegendste und wichtigste Eintrag. Er verbindet deinen Domainnamen direkt mit der IPv4-Adresse deines Servers. IPv4-Adressen sind das gängigste Format und sehen so aus: `192.0.2.1`.

Ein typischer A-Record für deine Hauptdomain (auch "Root-Domain" oder "Apex-Domain" genannt) würde so aussehen:

*   **Name/Host:** `@` oder `mein-projekt.de`
*   **Typ:** `A`
*   **Wert/Ziel:** `192.0.2.1` (die IP-Adresse deines Webservers)

Das Zeichen `@` ist eine gängige Abkürzung und bedeutet "die Domain selbst". Wenn also jemand `mein-projekt.de` (ohne `www`) eingibt, wird er dank dieses Eintrags direkt zu deinem Server mit der IP `192.0.2.1` geleitet.

##### AAAA-Record (Quad A Record)

Der AAAA-Record ist das Pendant zum A-Record, jedoch für IPv6-Adressen. IPv6 ist der neuere Adressstandard, der eingeführt wurde, weil die IPv4-Adressen langsam knapp werden. IPv6-Adressen sind deutlich länger und komplexer, zum Beispiel `2001:0db8:85a3:0000:0000:8a2e:0370:7334`.

Wenn dein Hosting-Anbieter dir eine IPv6-Adresse zur Verfügung stellt, ist es eine gute Praxis, auch einen AAAA-Record anzulegen:

*   **Name/Host:** `@` oder `mein-projekt.de`
*   **Typ:** `AAAA`
*   **Wert/Ziel:** `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

Dadurch ist deine Webseite auch über das modernere Protokoll erreichbar.

##### CNAME-Record (Canonical Name Record)

Viele Nutzer sind es gewohnt, eine Webadresse mit `www` davor einzugeben, also `www.mein-projekt.de`. Diese sogenannte Subdomain muss ebenfalls konfiguriert werden. Du könntest dafür einen weiteren A-Record anlegen, der `www` auf dieselbe IP-Adresse wie deine Hauptdomain verweist. Das ist aber nicht die eleganteste Lösung. Was passiert, wenn sich die IP-Adresse deines Servers ändert? Dann müsstest du beide A-Records manuell anpassen.

Hier kommt der CNAME-Record ins Spiel. Er erstellt keinen direkten Verweis auf eine IP-Adresse, sondern einen Alias oder eine Verknüpfung zu einem anderen Domainnamen.

Die bewährte Methode ist, die Subdomain `www` per CNAME auf deine Hauptdomain zu verweisen:

*   **Name/Host:** `www`
*   **Typ:** `CNAME`
*   **Wert/Ziel:** `mein-projekt.de`

Dieser Eintrag bedeutet: "Wer auch immer nach `www.mein-projekt.de` fragt, soll bitte bei `mein-projekt.de` nachschauen." Das DNS löst dann `mein-projekt.de` über den dort hinterlegten A-Record auf und findet die richtige IP-Adresse. Der große Vorteil: Wenn du jemals deine Server-IP ändern musst, passt du nur noch den einen A-Record deiner Hauptdomain an, und der `www`-Alias funktioniert automatisch weiterhin korrekt.

#### Die Konfiguration Schritt für Schritt

Obwohl die Benutzeroberflächen bei jedem Domain-Anbieter etwas anders aussehen, sind die grundlegenden Schritte immer die gleichen.

**1. Informationen sammeln:**
Bevor du beginnst, benötigst du zwei Dinge:
*   Die Zugangsdaten zum Kundenbereich deines Domain-Anbieters.
*   Die IPv4-Adresse (und optional die IPv6-Adresse) deines Webservers. Diese Information erhältst du von deinem Hosting-Anbieter, oft in der Willkommens-E-Mail oder im Dashboard des Hostings.

**2. DNS-Verwaltung finden:**
Logge dich bei deinem Domain-Anbieter ein und navigiere zur Domain-Verwaltung. Dort suchst du nach einem Menüpunkt wie "DNS-Verwaltung", "DNS-Einstellungen", "Nameserver-Konfiguration" oder Ähnlichem.

**3. Die Einträge erstellen oder anpassen:**
Du wirst eine Liste oder eine Tabelle mit bestehenden DNS-Einträgen sehen. Oft sind bereits Standardeinträge vom Anbieter vorhanden. Diese musst du nun anpassen oder durch deine eigenen ersetzen.

*   **Für die Hauptdomain (ohne www):**
    *   Suche nach einem A-Record mit dem Namen `@` oder `mein-projekt.de`.
    *   Bearbeite diesen Eintrag und ersetze den Wert durch die IP-Adresse deines Webservers.
    *   Falls kein solcher Eintrag existiert, erstelle einen neuen: Typ `A`, Name `@`, Wert `deine.server.ip.adresse`.

*   **Für die www-Subdomain:**
    *   Suche nach einem Eintrag für `www`. Dies könnte ein A-Record oder bereits ein CNAME-Record sein.
    *   Die beste Vorgehensweise ist, ihn als CNAME-Record zu konfigurieren. Erstelle (oder ändere) den Eintrag wie folgt: Typ `CNAME`, Name `www`, Wert `mein-projekt.de`.

Ein typisches, korrektes Setup könnte am Ende so aussehen:

```dns
# DNS-Einträge für mein-projekt.de

@            A       192.0.2.1
@            AAAA    2001:0db8:85a3:0000:0000:8a2e:0370:7334
www          CNAME   mein-projekt.de
```

#### Ein Wort zur Geduld: TTL (Time to Live)

Nachdem du die DNS-Einträge gespeichert hast, passiert eines: Warten. DNS-Änderungen sind nicht sofort weltweit aktiv. Der Grund dafür ist ein Mechanismus namens "Time to Live" (TTL). Jeder DNS-Eintrag hat einen TTL-Wert, der in Sekunden angegeben wird (z. B. 3600 für eine Stunde). Dieser Wert sagt den DNS-Servern im ganzen Internet, wie lange sie eine einmal abgerufene Information in ihrem Zwischenspeicher (Cache) behalten dürfen, bevor sie erneut beim autoritativen Server nachfragen müssen.

Dieses Caching ist essenziell für die Geschwindigkeit des Internets, da nicht jede Anfrage den ganzen Weg zurück zum Ursprungsserver gehen muss. Für dich bedeutet das aber, dass es von wenigen Minuten bis zu 24 Stunden (in seltenen Fällen auch länger) dauern kann, bis deine Änderungen von allen Servern weltweit übernommen wurden. Also keine Panik, wenn deine Domain nicht sofort auf deinen Server verweist.

#### Der letzte Schliff: Subdomains und HTTPS

Mit dem Wissen über A- und CNAME-Records kannst du nicht nur deine Hauptseite erreichbar machen. Du kannst auch beliebige Subdomains einrichten. Möchtest du zum Beispiel einen Blog unter `blog.mein-projekt.de` betreiben, der auf demselben Server liegt, erstellst du einfach einen weiteren CNAME-Record:

*   **Name/Host:** `blog`
*   **Typ:** `CNAME`
*   **Wert/Ziel:** `mein-projekt.de`

Ein letzter, aber unverzichtbarer Punkt ist **HTTPS**. Eine sichere, verschlüsselte Verbindung ist heute Standard und ein Muss für jede Webseite. Die Einrichtung eines SSL/TLS-Zertifikats (was für HTTPS benötigt wird) erfolgt in der Regel auf deinem Webserver, nicht in den DNS-Einstellungen. Viele moderne Hosting-Anbieter bieten kostenlose Zertifikate, zum Beispiel über "Let's Encrypt", und integrieren deren Einrichtung direkt in ihr Control Panel. Manchmal wird für die Validierung deiner Domain ein spezieller `TXT`-Record im DNS benötigt, aber dein Hoster wird dich in diesem Fall durch den Prozess leiten. Stelle sicher, dass nach der Domain-Konfiguration auch die Verschlüsselung aktiviert ist, damit deine Besucher deine Seite sicher über `https://mein-projekt.de` erreichen können.
