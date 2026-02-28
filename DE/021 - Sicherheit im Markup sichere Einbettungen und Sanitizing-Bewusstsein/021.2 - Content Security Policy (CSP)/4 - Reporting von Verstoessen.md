# Reporting von Verstößen

### Wenn Deine CSP Alarm schlägt: Reporting von Verstößen

Eine Content Security Policy (CSP) ohne Reporting ist wie eine Alarmanlage, die bei einem Einbruch still bleibt. Sie mag den Einbrecher aufhalten, aber du erfährst nie, dass es einen Versuch gab, wo er stattfand oder welche Schwachstelle ausgenutzt wurde. Das Reporting ist das entscheidende Puzzleteil, das deine CSP von einem passiven Schutzschild zu einem aktiven Überwachungssystem macht. Es gibt dir die nötigen Einblicke, um deine Richtlinien zu verfeinern, Angriffe zu erkennen und sicherzustellen, dass deine Webseite nicht versehentlich legitime Inhalte blockiert.

#### Warum du Verstöße überhaupt protokollieren solltest

Stell dir vor, du führst eine neue, sehr strenge CSP ein. Plötzlich funktioniert ein wichtiger Teil deiner Anwendung nicht mehr, weil ein Skript von einem Drittanbieter blockiert wird, das du übersehen hast. Ohne Reporting stocherst du im Dunkeln. Du weißt nur, *dass* etwas kaputt ist, aber nicht *was* oder *warum*.

Mit aktiviertem Reporting sendet der Browser des Nutzers bei jedem Verstoß gegen deine CSP einen kleinen, detaillierten Bericht an einen von dir festgelegten Endpunkt. Dieser Bericht ist eine Goldgrube an Informationen. Er verrät dir:

*   **Was** blockiert wurde (z. B. ein Skript, ein Bild, ein Stylesheet).
*   **Woher** die blockierte Ressource laden sollte (`blocked-uri`).
*   **Auf welcher Seite** der Verstoß aufgetreten ist (`document-uri`).
*   **Welche Direktive** der CSP den Verstoß ausgelöst hat (`violated-directive`).

Diese Daten ermöglichen es dir, deine CSP präzise anzupassen. Du kannst legitime Quellen, die du vergessen hast, zur Whitelist hinzufügen oder unbeabsichtigte Inline-Skripte aufspüren und entfernen. Noch wichtiger ist, dass du dadurch reale Angriffsversuche, wie Cross-Site-Scripting (XSS), in Echtzeit erkennen kannst.

#### Die alten und neuen Wege des Reportings: `report-uri` und `report-to`

Um das Reporting zu aktivieren, gibt es zwei Direktiven, die du in deinem CSP-Header verwenden kannst.

##### Der Klassiker: `report-uri`

Die Direktive `report-uri` ist der ältere und weiter verbreitete Mechanismus. Ihre Einrichtung ist denkbar einfach: Du gibst eine URL an, an die der Browser die Berichte senden soll.

```http
Content-Security-Policy: default-src 'self'; 
                         script-src 'self' https://stats.example.com;
                         report-uri /csp-reports;
```

In diesem Beispiel würde jeder Verstoß gegen die Richtlinie dazu führen, dass der Browser eine `POST`-Anfrage mit einem JSON-Payload an die Adresse `deine-domain.com/csp-reports` sendet. Dieser Endpunkt muss auf deinem Server existieren und in der Lage sein, die eingehenden JSON-Daten zu verarbeiten und zu speichern.

Der JSON-Bericht, den der Browser sendet, sieht typischerweise so aus:

```json
{
  "csp-report": {
    "document-uri": "https://deinedomain.com/artikel/toller-beitrag",
    "referrer": "https://google.com",
    "violated-directive": "script-src-elem",
    "effective-directive": "script-src-elem",
    "original-policy": "default-src 'self'; script-src 'self' https://stats.example.com; report-uri /csp-reports;",
    "disposition": "enforce",
    "blocked-uri": "https://boesewebsite.net/malware.js",
    "line-number": 25,
    "source-file": "https://deinedomain.com/artikel/toller-beitrag",
    "status-code": 200,
    "script-sample": ""
  }
}
```

*   **`document-uri`**: Die Seite, auf der der Fehler passierte.
*   **`violated-directive`**: Die spezifische Regel, die verletzt wurde.
*   **`blocked-uri`**: Die URL der Ressource, die blockiert wurde. Dies ist oft die wichtigste Information.
*   **`original-policy`**: Deine komplette CSP, die den Verstoß gemeldet hat.

Obwohl `report-uri` funktioniert und eine breite Browser-Unterstützung genießt, gilt es als veraltet. Es hat den Nachteil, dass bei vielen Verstößen in kurzer Zeit eine Flut von Anfragen an deinen Server gesendet wird, was diesen belasten kann.

##### Die Zukunft: `report-to` und die Reporting API

Der modernere Ansatz ist die `report-to` Direktive in Verbindung mit dem `Report-To` HTTP-Header. Dieses System ist Teil der allgemeineren Reporting API und bietet mehr Flexibilität und Kontrolle.

Die Konfiguration besteht aus zwei Teilen:

1.  **Der `Report-To`-Header:** Hier definierst du einen oder mehrere "Reporting-Endpunkte" in einer JSON-Struktur. Du gibst ihnen einen Gruppennamen, eine Lebensdauer (`max_age`) und die eigentliche URL.

    ```http
    Report-To: {
      "group": "csp-violations",
      "max_age": 10886400,
      "endpoints": [
        { "url": "https://reports.deinedomain.com/csp" }
      ]
    }
    ```

2.  **Die `report-to`-Direktive in der CSP:** In deiner CSP verweist du dann einfach auf den zuvor definierten Gruppennamen.

    ```http
    Content-Security-Policy: default-src 'self'; 
                             report-to csp-violations;
    ```

Der große Vorteil dieses Ansatzes ist, dass der Browser die Berichte bündeln und asynchron senden kann. Das entlastet sowohl das Netzwerk des Nutzers als auch deinen Server. Außerdem ist die Reporting API darauf ausgelegt, auch andere Arten von Berichten (z. B. über veraltete Features oder Abstürze) zu verarbeiten, was sie zu einer zukunftssicheren Lösung macht.

Da die Browser-Unterstützung für die Reporting API noch nicht bei 100 % liegt, ist es eine bewährte Praxis, beide Direktiven zu verwenden. Browser, die `report-to` verstehen, werden es bevorzugen, während ältere Browser auf `report-uri` als Fallback zurückgreifen.

```http
Content-Security-Policy: default-src 'self'; 
                         report-uri /csp-reports-fallback; 
                         report-to csp-violations;
```

#### Der sichere Hafen: Testen mit `Content-Security-Policy-Report-Only`

Eine neue, strenge CSP direkt in einer produktiven Umgebung zu aktivieren, ist riskant. Du könntest versehentlich wichtige Funktionen deiner Webseite lahmlegen. Genau für dieses Szenario gibt es den `Content-Security-Policy-Report-Only`-Header.

Wie der Name schon sagt, erzwingt dieser Header die Richtlinien nicht. Stattdessen werden Verstöße nur gemeldet. Die blockierte Ressource wird trotzdem geladen und ausgeführt, als ob es keine CSP gäbe.

```http
Content-Security-Policy-Report-Only: 
  default-src 'self';
  script-src 'self' https://cdn.jquery.com;
  style-src 'self' 'unsafe-inline';
  report-uri /csp-audit-reports;
```

Dieser "Nur-Melden-Modus" ist das perfekte Werkzeug, um eine neue oder verschärfte CSP zu entwickeln und zu testen. Der typische Arbeitsablauf sieht so aus:

1.  **Entwerfe eine Richtlinie:** Erstelle eine möglichst strenge CSP, von der du glaubst, dass sie für deine Seite funktionieren sollte.
2.  **Implementiere im Nur-Melden-Modus:** Setze diese Richtlinie in den `Content-Security-Policy-Report-Only`-Header und spiele sie auf deiner Webseite aus.
3.  **Sammle Daten:** Lasse die Seite für einige Tage oder Wochen laufen und sammle die eingehenden Berichte. Analysiere, welche Ressourcen Verstöße verursachen.
4.  **Verfeinere die Richtlinie:** Passe deine CSP basierend auf den Berichten an. Füge legitime Quellen hinzu, die du übersehen hast, oder überarbeite Teile deines Codes, um beispielsweise Inline-Skripte zu eliminieren.
5.  **Wechsle in den Erzwingungsmodus:** Wenn du über einen längeren Zeitraum keine Berichte mehr über blockierte legitime Inhalte erhältst, bist du bereit. Du kannst die Richtlinie nun aus dem `Report-Only`-Header in den scharfen `Content-Security-Policy`-Header verschieben.

Dieser iterative Prozess stellt sicher, dass der Übergang zu einer sicheren CSP reibungslos verläuft, ohne die Benutzererfahrung zu beeinträchtigen.

#### Den Endpunkt einrichten und Berichte verarbeiten

Die Berichte müssen irgendwo ankommen. Du hast zwei Möglichkeiten, einen Endpunkt für die CSP-Berichte bereitzustellen:

1.  **Selbst hosten:** Du kannst eine einfache Server-Anwendung schreiben (z. B. mit Node.js, Python oder PHP), die `POST`-Anfragen auf einer bestimmten URL entgegennimmt. Diese Anwendung muss den JSON-Body der Anfrage lesen, validieren und die Daten in einer für dich geeigneten Form speichern – sei es in einer Log-Datei, einer Datenbank oder einem Monitoring-Tool.
2.  **Drittanbieter-Dienste nutzen:** Der Aufbau und die Wartung einer eigenen Reporting-Infrastruktur können aufwendig sein. Es gibt spezialisierte Dienste wie [Sentry.io](https://sentry.io/) oder [report-uri.com](https://report-uri.com/), die dir einen fertigen Endpunkt zur Verfügung stellen. Du musst nur die URL des Dienstes in deiner CSP eintragen. Diese Dienste nehmen die Berichte nicht nur entgegen, sondern aggregieren sie auch, filtern Rauschen heraus und präsentieren dir die Daten in einem übersichtlichen Dashboard. Das spart enorm viel Zeit bei der Analyse.

Unabhängig davon, welchen Weg du wählst, ist die Analyse der Berichte der entscheidende Schritt. Halte Ausschau nach Mustern. Wenn plötzlich hunderte Berichte über ein blockiertes Skript von `evil-hacker.com` eintreffen, weißt du, dass deine CSP gerade einen aktiven Angriff abwehrt. Wenn du wiederholt Berichte über eine blockierte Schriftart von `fonts.gstatic.com` siehst, hast du wahrscheinlich vergessen, diese Domain in deiner `font-src`-Direktive zu erlauben.

Das Reporting verwandelt deine CSP von einer Blackbox in ein transparentes Sicherheitssystem, das dir hilft, deine Webseite kontinuierlich sicherer und robuster zu machen.
