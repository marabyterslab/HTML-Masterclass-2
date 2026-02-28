# Live-Schaltung und Monitoring

### Live-Schaltung und Monitoring: Der Moment der Wahrheit

Dein Projekt ist fertig. Jeder Link funktioniert, jedes Bild sitzt an seinem Platz und der Code ist sauber und validiert. Auf deinem lokalen Rechner sieht alles perfekt aus. Doch der Sinn einer Webseite ist es, von der Welt gesehen zu werden. Der Schritt, der dein Projekt aus seiner geschützten, lokalen Umgebung in das riesige, unvorhersehbare World Wide Web bringt, wird als Live-Schaltung oder Deployment bezeichnet. Dieser Moment ist aufregend, kann aber auch ein wenig nervenaufreibend sein. Doch keine Sorge, mit der richtigen Vorbereitung wird alles glattgehen. Und wenn die Seite erst einmal online ist, beginnt der zweite, ebenso wichtige Teil: das Monitoring.

#### Die Live-Schaltung – Vom lokalen Rechner ins World Wide Web

Die Live-Schaltung ist im Grunde ein Umzug. Deine HTML-, CSS-, JavaScript-Dateien, Bilder und anderen Ressourcen müssen von deinem Computer auf einen speziellen Computer kopiert werden, der rund um die Uhr mit dem Internet verbunden ist: einen Webserver.

##### Der digitale Grundbesitz: Domain und Hosting

Bevor du deine Daten umziehen kannst, brauchst du zwei grundlegende Dinge:

1.  **Eine Domain:** Das ist die Adresse, unter der deine Webseite erreichbar sein wird, zum Beispiel `dein-tolles-projekt.de`. Eine Domain registrierst du bei einem sogenannten Registrar. Sie ist deine einzigartige Identität im Netz. Stell sie dir wie die Adresse deines Hauses vor.
2.  **Ein Webhosting-Paket:** Das ist der Speicherplatz auf einem Webserver, den du mietest. Hier werden deine Dateien liegen. Um bei der Haus-Analogie zu bleiben: Wenn die Domain die Adresse ist, ist das Hosting das Grundstück, auf dem dein Haus (deine Webseite) steht.

Für ein reines HTML/CSS/JavaScript-Projekt reicht in den allermeisten Fällen ein einfaches „Shared Hosting“-Paket aus. Du teilst dir dabei die Ressourcen eines Servers mit anderen Kunden, was sehr kostengünstig ist und für den Start völlig genügt.

##### Der Umzug: Deine Daten auf den Server laden

Sobald du deine Domain und dein Hosting-Paket hast, bekommst du von deinem Hoster Zugangsdaten für den Server. Die gängigste Methode, um deine Dateien auf diesen Server zu übertragen, ist das **File Transfer Protocol (FTP)** oder seine sichere Variante, **SFTP (Secure File Transfer Protocol)**.

Dafür nutzt du ein FTP-Programm (einen sogenannten FTP-Client) wie FileZilla oder Cyberduck. Die Funktionsweise ist denkbar einfach: Du verbindest dich mit den erhaltenen Zugangsdaten (Server-Adresse, Benutzername, Passwort) mit deinem Webspace. Das Programm zeigt dir dann zwei Fenster an: links die Dateien auf deinem lokalen Computer und rechts die Ordnerstruktur auf dem Server.

Auf dem Server gibt es meist einen speziellen Ordner, der für die Öffentlichkeit zugänglich ist. Er heißt oft `public_html`, `www`, `htdocs` oder ähnlich. In genau diesen Ordner ziehst du per Drag-and-drop alle deine Projektdateien – genau so, wie sie auf deinem Rechner strukturiert sind. Deine `index.html` muss sich im Hauptverzeichnis dieses Ordners befinden, damit sie als Startseite erkannt wird.

##### Die Verbindung schaffen: DNS-Einträge setzen

Damit deine Domain auch wirklich auf deinen Webspace zeigt, muss eine Verbindung hergestellt werden. Das geschieht über das **Domain Name System (DNS)**. Stell es dir wie das Adressbuch des Internets vor. Es übersetzt den für Menschen lesbaren Domainnamen (z. B. `dein-tolles-projekt.de`) in die für Computer verständliche IP-Adresse des Servers (z. B. `198.51.100.123`).

Normalerweise musst du hier nicht viel tun. Wenn du Domain und Hosting beim selben Anbieter gekauft hast, ist diese Verknüpfung oft schon vorkonfiguriert. Falls nicht, musst du in der Verwaltung deiner Domain die sogenannten „Nameserver“ deines Hosters eintragen oder einen A-Record setzen, der auf die IP-Adresse deines Servers verweist. Das klingt komplizierter, als es ist; die Support-Dokumentation deines Hosters wird dir hier genaue Anweisungen geben. Beachte, dass es nach einer DNS-Änderung einige Stunden dauern kann, bis sie weltweit aktiv ist.

##### Die Checkliste vor dem Start

Bevor du der Welt stolz den Link zu deiner neuen Seite schickst, gehe noch einmal diese kurze Checkliste durch:

*   **Alle Pfade relativ?** Überprüfe, ob alle Verlinkungen zu CSS-Dateien, Bildern oder anderen Seiten relativ (`/bilder/foto.jpg` oder `../css/style.css`) und nicht absolut auf deine lokale Festplatte (`C:/Users/Du/Projekt/...`) verweisen.
*   **Favicon vorhanden?** Das kleine Symbol im Browser-Tab sorgt für einen professionellen Eindruck.
*   **Meta-Tags gesetzt?** Sind der `<title>` und die `<meta name="description">` für jede Seite sinnvoll ausgefüllt? Sie sind entscheidend für die Darstellung in Suchmaschinen.
*   **HTTPS aktiviert?** Eine sichere Verbindung über `https` ist heute Standard. Die meisten Hoster bieten kostenlose SSL/TLS-Zertifikate (z. B. von Let's Encrypt) an, die du mit wenigen Klicks aktivieren kannst. Eine unverschlüsselte `http`-Seite wird von Browsern als „nicht sicher“ markiert und von Suchmaschinen benachteiligt.

Wenn alles passt: Herzlichen Glückwunsch! Deine Webseite ist live!

#### Nach dem Launch – Das wachsame Auge des Monitorings

Deine Seite ist online. Aber damit ist die Arbeit nicht getan. In gewisser Weise beginnt sie jetzt erst richtig. Du musst sicherstellen, dass deine Seite erreichbar, schnell und fehlerfrei bleibt. Das nennt man Monitoring.

##### Erreichbarkeit (Uptime): Ist überhaupt jemand zu Hause?

Ein Server ist auch nur ein Computer. Er kann ausfallen, ein Update kann fehlschlagen oder das Rechenzentrum hat einen Stromausfall. Du möchtest sofort wissen, wenn deine Seite nicht mehr erreichbar ist.

Dafür gibt es **Uptime-Monitoring-Dienste**. Anbieter wie UptimeRobot oder Pingdom bieten oft kostenlose Pakete an, die für ein einzelnes Projekt ausreichen. Du gibst dort die URL deiner Webseite an, und der Dienst „pingt“ deine Seite in regelmäßigen Abständen (z. B. alle 5 Minuten) an. Wenn die Seite nicht antwortet, schickt dir der Dienst sofort eine E-Mail oder eine Push-Benachrichtigung. So kannst du schnell reagieren und musst nicht darauf warten, dass ein Besucher dich darauf hinweist.

##### Performance: Niemand wartet gerne

Die Ladezeit deiner Webseite ist einer der wichtigsten Faktoren für den Erfolg. Eine langsame Seite frustriert Besucher und wird von Google im Ranking abgestraft. Du musst also im Auge behalten, wie schnell deine Seite ist.

Tools wie **Google PageSpeed Insights**, **GTmetrix** oder **WebPageTest** sind hier deine besten Freunde. Du gibst einfach deine URL ein und bekommst einen detaillierten Bericht darüber, wie lange das Laden dauert und wo es Engpässe gibt. Diese Tools geben dir auch konkrete Hinweise zur Optimierung, zum Beispiel:
*   „Komprimiere dieses Bild, um 50 KB zu sparen.“
*   „Reduziere ungenutztes CSS.“
*   „Aktiviere Browser-Caching.“

Gerade bei HTML-Projekten sind die häufigsten Bremsen zu große, unkomprimierte Bilder. Es lohnt sich, die Performance regelmäßig zu überprüfen, besonders nachdem du neue Inhalte hinzugefügt hast.

##### Besucheranalyse: Wer kommt zu Besuch und was tun sie?

Woher kommen deine Besucher? Welche Seiten schauen sie sich am liebsten an? Wie lange bleiben sie? Antworten auf diese Fragen geben dir Webanalyse-Tools.

Der Branchenstandard ist **Google Analytics**. Es ist extrem mächtig und kostenlos, erfordert aber einen klaren Hinweis in deiner Datenschutzerklärung, da es viele Daten sammelt. Um es zu nutzen, meldest du dich an, erstellst eine „Property“ für deine Webseite und erhältst einen kleinen JavaScript-Code-Schnipsel. Diesen Schnipsel fügst du in den `<head>`- oder `<body>`-Bereich jeder deiner HTML-Seiten ein. Nach kurzer Zeit siehst du in deinem Analytics-Dashboard die ersten Daten einlaufen.

Wenn du eine datenschutzfreundlichere Alternative suchst, sind Dienste wie **Matomo** (kannst du selbst hosten) oder **Plausible Analytics** eine hervorragende Wahl. Sie sammeln weniger Daten, oft anonymisiert, und geben dir trotzdem die wichtigsten Einblicke in das Verhalten deiner Nutzer.

##### Fehler- und Integritätsprüfung: Läuft alles rund?

Fehler passieren. Du benennst eine Bilddatei um, vergisst aber, den Pfad im HTML-Code anzupassen. Ein externer Link, auf den du verweist, existiert nicht mehr. Das Ergebnis sind „tote Links“ und fehlende Bilder, die zu einer 404-Fehlermeldung („Not Found“) führen.

Solche Fehler findest du auf verschiedene Weisen:
*   **Manuelle Prüfung:** Klicke regelmäßig deine eigene Seite durch.
*   **Web-Crawler-Tools:** Programme wie Screaming Frog SEO Spider (in der kostenlosen Version für kleine Seiten ausreichend) crawlen deine komplette Seite und listen dir alle fehlerhaften Links auf.
*   **Google Search Console:** Wenn du deine Seite hier anmeldest (was du ohnehin tun solltest), zeigt dir Google unter dem Punkt „Crawling-Fehler“ an, wenn sein Bot auf nicht funktionierende Links gestoßen ist.

Die Live-Schaltung ist der Startschuss, aber das Monitoring ist das Langstreckenrennen. Indem du deine Seite im Auge behältst, stellst du sicher, dass die harte Arbeit, die du in die Entwicklung gesteckt hast, auch langfristig zu einem positiven und professionellen Erlebnis für deine Besucher führt.
