# IP-Adressen und DNS

### IP-Adressen und DNS: Das Adressbuch des Internets

Stell dir das Internet wie ein gigantisches, weltumspannendes Netzwerk von Städten vor. In diesem Netzwerk ist jeder Computer, jeder Server und sogar dein Smartphone ein Haus. Damit eine Postkarte (also ein Datenpaket) von deinem Haus zu einem anderen Haus gelangen kann, braucht es eine eindeutige Adresse. Ohne eine solche Adresse wäre das ganze System ein unvorstellbares Chaos. Genau hier kommen IP-Adressen ins Spiel.

#### Die IP-Adresse – Deine digitale Hausnummer

Eine IP-Adresse (Internet Protocol Address) ist nichts anderes als eine einzigartige numerische Kennzeichnung für ein Gerät in einem Netzwerk. So wie die Post deine Briefe nur zustellen kann, wenn sie eine Straße und eine Hausnummer hat, können Router im Internet Datenpakete nur dann an das richtige Ziel schicken, wenn sie eine IP-Adresse haben.

Wenn du dich mit dem Internet verbindest, weist dir dein Internetanbieter (Provider) eine IP-Adresse zu. Diese Adresse ist für die Dauer deiner Online-Sitzung – oder manchmal auch für einen längeren Zeitraum – deine Identität im Netz. Jede Webseite, die du besuchst, jeder Dienst, den du nutzt, sieht diese Absenderadresse auf den Datenpaketen, die du schickst, und nutzt sie, um dir die Antwort zurückzusenden.

**IPv4: Der bewährte Klassiker**

Die längste Zeit war die gebräuchlichste Form die IP-Version 4 (IPv4). Du hast sie sicher schon einmal gesehen. Sie besteht aus vier Zahlenblöcken, die durch Punkte getrennt sind. Jeder Block kann eine Zahl von 0 bis 255 enthalten.

Ein typisches Beispiel für eine IPv4-Adresse ist:
`193.99.144.80`

Dieses System bietet ungefähr 4,3 Milliarden einzigartige Adressen. Das klang in den Anfängen des Internets nach einer unvorstellbar großen Zahl. Doch mit der explosionsartigen Zunahme von Computern, Smartphones, Servern und mittlerweile sogar Kühlschränken und Uhren, die online gehen, wurde schnell klar: Diese Adressen werden knapp. Das Problem ist vergleichbar mit einer Stadt, in der alle Grundstücke bebaut sind und es keine neuen Adressen mehr zu vergeben gibt.

**IPv6: Die Zukunft hat mehr Ziffern**

Um dieses Problem zu lösen, wurde die IP-Version 6 (IPv6) entwickelt. Sie ist der Nachfolger von IPv4 und bietet eine schier unbegrenzte Anzahl an Adressen. Statt aus vier Zahlenblöcken besteht eine IPv6-Adresse aus acht Blöcken mit hexadezimalen Zeichen (Zahlen von 0-9 und Buchstaben von a-f), die durch Doppelpunkte getrennt sind.

Ein Beispiel für eine IPv6-Adresse sieht so aus:
`2001:0db8:85a3:0000:0000:8a2e:0370:7334`

Diese Adressen sind deutlich länger und komplizierter, aber sie stellen sicher, dass uns die Adressen für die absehbare Zukunft nicht ausgehen werden. Heute existieren beide Systeme parallel, und der Übergang zu IPv6 vollzieht sich langsam aber stetig im Hintergrund, ohne dass du als Nutzer viel davon mitbekommst.

#### Das Domain Name System (DNS) – Der Übersetzer des Internets

Jetzt weißt du, dass Computer über IP-Adressen miteinander kommunizieren. Aber mal ehrlich: Könntest du dir die Adresse `172.217.16.67` merken, um Google zu besuchen? Oder `93.184.216.34`, um eine Beispiel-Webseite aufzurufen? Wahrscheinlich nicht. Wir Menschen sind viel besser darin, uns Namen zu merken, wie `google.com` oder `beispiel.de`.

Und genau hier kommt das Domain Name System, kurz DNS, ins Spiel. Das DNS ist im Grunde das riesige, dezentrale Telefonbuch des Internets. Seine einzige, aber unglaublich wichtige Aufgabe ist es, für Menschen lesbare Domainnamen in maschinenlesbare IP-Adressen zu übersetzen.

Wenn du also `www.wikipedia.org` in die Adresszeile deines Browsers eingibst, passiert im Hintergrund ein faszinierender Prozess, der nur Millisekunden dauert:

1.  **Die Anfrage:** Dein Computer weiß nicht, welche IP-Adresse sich hinter `www.wikipedia.org` verbirgt. Also fragt er nach. Der erste Ansprechpartner ist in der Regel ein DNS-Server, der von deinem Internetanbieter betrieben wird. Man nennt diesen auch einen "Resolver".

2.  **Die Suche:** Der Resolver schaut in seinem Zwischenspeicher (Cache) nach, ob er die Anfrage kürzlich schon einmal beantwortet hat. Wenn ja, schickt er die IP-Adresse sofort zurück. Das spart Zeit.

3.  **Die Hierarchie:** Wenn der Resolver den Eintrag nicht kennt, beginnt eine Kette von Anfragen. Er kontaktiert einen der sogenannten Root-DNS-Server. Diese Root-Server kennen nicht die Antwort für jede einzelne Domain, aber sie wissen, wer für die Top-Level-Domain (wie `.org`, `.com` oder `.de`) zuständig ist. Der Root-Server verweist den Resolver also an den zuständigen Server für `.org`.

4.  **Die Auflösung:** Der Resolver fragt nun den `.org`-Server nach `wikipedia.org`. Dieser Server kennt wiederum die IP-Adresse des finalen, autoritativen DNS-Servers, der von Wikipedia selbst betrieben wird.

5.  **Die Antwort:** Schließlich fragt dein Resolver diesen autoritativen Server, der die offizielle und korrekte IP-Adresse für `www.wikipedia.org` kennt (z. B. `91.198.174.192`) und schickt diese Information zurück an den Resolver.

6.  **Das Ergebnis:** Dein Resolver speichert diese Antwort für zukünftige Anfragen in seinem Cache und leitet die IP-Adresse an deinen Computer weiter.

Erst jetzt, nachdem dein Browser die numerische IP-Adresse erhalten hat, kann er eine Verbindung zum Webserver von Wikipedia aufbauen und die Webseite anfordern. Das alles passiert jedes Mal, wenn du eine neue Webseite besuchst, und es ist so schnell, dass du es gar nicht bemerkst. Ohne das DNS wäre das Internet, wie wir es heute kennen, nicht nutzbar.

#### Ein Blick unter die Haube

Du musst nicht glauben, dass dieser Prozess im Verborgenen stattfindet. Du kannst ihn selbst nachvollziehen. Auf fast jedem Betriebssystem gibt es Kommandozeilen-Tools, mit denen du das DNS direkt abfragen kannst. Ein gängiges Werkzeug dafür ist `nslookup` (Name Server Lookup).

Öffne eine Kommandozeile (Terminal auf macOS/Linux, Eingabeaufforderung oder PowerShell auf Windows) und gib Folgendes ein:

```bash
nslookup google.com
```

Als Antwort erhältst du wahrscheinlich etwas Ähnliches wie das hier:

```
Server:  dein-dns-server.com
Address: 192.168.1.1

Nicht autorisierende Antwort:
Name:    google.com
Addresses: 2a00:1450:4001:82b::200e
         142.250.185.110
```

Hier siehst du genau, was passiert: Dein Computer hat einen DNS-Server gefragt und als Antwort sowohl eine IPv6-Adresse als auch eine IPv4-Adresse für `google.com` erhalten. Dein Browser kann sich nun eine davon aussuchen, um die Verbindung herzustellen.

IP-Adressen und das DNS sind also zwei der fundamentalen Säulen, auf denen die gesamte Kommunikation im Web aufbaut. Die IP-Adresse ist das Ziel, der exakte Ort, an den die Daten müssen. Das DNS ist der freundliche und unverzichtbare Wegweiser, der uns erlaubt, einfache Namen statt kryptischer Zahlen zu verwenden, um dorthin zu gelangen.
