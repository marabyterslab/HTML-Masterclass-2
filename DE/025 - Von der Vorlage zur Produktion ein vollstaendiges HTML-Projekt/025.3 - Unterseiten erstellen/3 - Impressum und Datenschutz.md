# Impressum und Datenschutz

### Impressum und Datenschutz: Die rechtlichen Pflichtseiten

Sobald dein Webprojekt über den Status einer rein privaten, familiären Spielwiese hinausgeht, betrittst du rechtliches Terrain. Zwei Unterseiten, die dann unerlässlich werden, sind das Impressum und die Datenschutzerklärung. Sie sind keine bloße Formalität, sondern gesetzlich vorgeschriebene Bestandteile vieler Webseiten, insbesondere im deutschsprachigen Raum. Ihre korrekte Umsetzung ist nicht nur eine Frage der Professionalität, sondern auch der rechtlichen Absicherung.

Wichtiger Hinweis vorab: Dieses Kapitel stellt keine Rechtsberatung dar und kann eine solche auch nicht ersetzen. Die Gesetze sind komplex und ändern sich. Die folgenden Erklärungen dienen dem technischen und konzeptionellen Verständnis, damit du weißt, worum es geht und wie du diese Inhalte in dein HTML-Projekt integrierst. Für die Erstellung rechtssicherer Texte solltest du immer einen Anwalt oder spezialisierte Online-Dienste (sogenannte Generatoren) zu Rate ziehen.

#### Das Impressum: Wer steckt hinter der Seite?

Das Impressum, auch als Anbieterkennzeichnung bekannt, dient einem einfachen Zweck: Transparenz. Besucher deiner Webseite sollen auf einen Blick erkennen können, wer für die Inhalte verantwortlich ist und wie sie diese Person oder Organisation kontaktieren können. Die Grundlage dafür ist in Deutschland das Telemediengesetz (TMG).

**Wer braucht ein Impressum?**

Die Faustregel lautet: Jede Webseite, die nicht ausschließlich persönlichen oder familiären Zwecken dient, benötigt ein Impressum. Sobald du also ein Portfolio zur Kundengewinnung erstellst, einen Blog mit Werbebannern betreibst oder einen Online-Shop planst, bist du in der Pflicht. Selbst ein scheinbar privater Blog kann impressumspflichtig werden, wenn er zum Beispiel Affiliate-Links enthält. Im Zweifel ist es immer sicherer, ein Impressum anzulegen.

**Was gehört hinein?**

Der genaue Inhalt hängt von deiner Rechtsform ab (Privatperson, Unternehmen, Verein etc.). Die grundlegenden Pflichtangaben für eine natürliche Person (z. B. ein Freelancer) sind jedoch meist:

*   **Vollständiger Name:** Max Mustermann
*   **Anschrift:** Musterstraße 1, 12345 Musterstadt (Ein Postfach reicht nicht aus, es muss eine ladungsfähige Anschrift sein.)
*   **Kontaktinformationen:** Eine E-Mail-Adresse ist Pflicht. Zusätzlich wird eine zweite, schnelle und unmittelbare Kontaktmöglichkeit gefordert, was in der Regel eine Telefonnummer ist.
*   **Zusätzliche Angaben (falls zutreffend):** Bei journalistisch-redaktionellen Inhalten (wie einem Blog) muss eine für den Inhalt verantwortliche Person genannt werden. Wenn du umsatzsteuerpflichtig bist, gehört auch deine Umsatzsteuer-Identifikationsnummer (USt-IdNr.) ins Impressum.

**Die technische Umsetzung des Impressums**

Die Erstellung der Impressumsseite selbst ist aus HTML-Sicht trivial. Du erstellst eine neue Datei, `impressum.html`, und füllst sie mit den notwendigen Informationen. Wichtig ist, dass du die Inhalte semantisch korrekt auszeichnest.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Impressum - Mein Projekt</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header>
        <!-- Deine Navigation -->
    </header>

    <main>
        <h1>Impressum</h1>

        <h2>Angaben gemäß § 5 TMG</h2>
        
        <!-- Die <address>-Tags sind semantisch korrekt für Kontaktinformationen -->
        <address>
            <p>
                Max Mustermann<br>
                Musterstraße 1<br>
                12345 Musterstadt
            </p>
        </address>

        <h2>Kontakt</h2>
        <!-- Eine Definitionsliste eignet sich gut für solche Schlüssel-Wert-Paare -->
        <dl>
            <dt>Telefon:</dt>
            <dd><a href="tel:+49123456789">+49 (0) 123 / 456 789</a></dd>
            <dt>E-Mail:</dt>
            <dd><a href="mailto:kontakt@maxmustermann.dev">kontakt@maxmustermann.dev</a></dd>
        </dl>
        
        <h2>Umsatzsteuer-ID</h2>
        <p>
            Umsatzsteuer-Identifikationsnummer gemäß § 27 a Umsatzsteuergesetz:<br>
            DE123456789
        </p>
        
        <h2>Verantwortlich für den Inhalt nach § 55 Abs. 2 RStV</h2>
        <address>
            <p>
                Max Mustermann<br>
                Musterstraße 1<br>
                12345 Musterstadt
            </p>
        </address>

    </main>

    <footer>
        <!-- Dein Footer-Inhalt -->
    </footer>
</body>
</html>
```

Wichtig ist die Verlinkung: Das Impressum muss von jeder einzelnen Seite deiner Website aus leicht erkennbar, unmittelbar erreichbar und ständig verfügbar sein. Der etablierte Standard ist ein Link mit dem Titel "Impressum" im Footer der Seite.

#### Die Datenschutzerklärung: Was passiert mit den Daten?

Während das Impressum statisch ist, ist die Datenschutzerklärung ein dynamisches Dokument. Ihr Inhalt hängt direkt davon ab, was auf deiner Webseite technisch passiert. Seit der Einführung der Datenschutz-Grundverordnung (DSGVO) in der EU ist dieses Thema noch präsenter und wichtiger geworden.

Das Grundprinzip der DSGVO ist die Informationspflicht. Du musst deine Nutzer klar, verständlich und vollständig darüber aufklären, welche personenbezogenen Daten du wann, warum und auf welcher Rechtsgrundlage erhebst, verarbeitest und speicherst. Du musst sie außerdem über ihre Rechte aufklären.

**Was gehört hinein?**

Eine Datenschutzerklärung ist oft sehr lang, weil sie jeden einzelnen datenverarbeitenden Prozess auf deiner Seite beschreiben muss. Zu den typischen Inhalten gehören:

*   **Name und Kontaktdaten des Verantwortlichen:** Das ist in der Regel dieselbe Person wie im Impressum.
*   **Erhebung von allgemeinen Daten (Server-Logfiles):** Jeder Webserver speichert bei einem Aufruf Daten wie deine IP-Adresse, den Browsertyp, die Uhrzeit und die aufgerufene Seite. Du musst erklären, dass diese Daten erhoben werden und warum (z. B. zur Gewährleistung der technischen Stabilität und Sicherheit).
*   **Cookies:** Verwendest du Cookies? Wenn ja, welche? Funktionale Cookies, die für den Betrieb der Seite notwendig sind, oder auch Tracking- und Marketing-Cookies? Du musst den Zweck und die Speicherdauer jedes Cookies erklären. Für nicht notwendige Cookies benötigst du die aktive Einwilligung des Nutzers (Stichwort: Cookie-Banner).
*   **Kontaktformulare:** Wenn du ein Kontaktformular anbietest, musst du erklären, welche Daten (Name, E-Mail etc.) du erhebst und dass du sie nur zur Beantwortung der Anfrage verwendest.
*   **Analyse-Dienste:** Nutzt du Tools wie Google Analytics oder Matomo, um die Besucherströme zu analysieren? Dann musst du dies detailliert beschreiben, inklusive der Information, ob IP-Adressen anonymisiert werden, und einen Hinweis auf die Widerspruchsmöglichkeit (Opt-out) geben.
*   **Einbindung von Drittanbieter-Inhalten:** Jedes eingebettete YouTube-Video, jede Google-Maps-Karte oder jede Schriftart von Google Fonts stellt eine Datenübertragung an einen Drittanbieter dar. Jeder dieser Dienste muss in der Datenschutzerklärung einzeln aufgeführt und erklärt werden.
*   **Rechte der betroffenen Personen:** Du musst die Nutzer über ihre Rechte aufklären, z. B. das Recht auf Auskunft, Berichtigung, Löschung ("Recht auf Vergessenwerden"), Einschränkung der Verarbeitung und Widerspruch.

**Die technische Umsetzung der Datenschutzerklärung**

Genau wie das Impressum erstellst du eine separate HTML-Datei, z. B. `datenschutz.html`. Da der Text oft sehr lang und juristisch formuliert ist, ist die Struktur entscheidend für die Lesbarkeit. Hier ist semantisches HTML Gold wert.

Verwende eine klare Überschriftenhierarchie (`<h1>`, `<h2>`, `<h3>`), um die verschiedenen Abschnitte zu gliedern. Nutze Absätze (`<p>`) für den Fließtext und Listen (`<ul>`, `<ol>`) oder Definitionslisten (`<dl>`), um Informationen übersichtlich darzustellen.

```html
<!-- Ausschnitt aus einer datenschutz.html -->
<main>
    <h1>Datenschutzerklärung</h1>
    
    <h2>1. Datenschutz auf einen Blick</h2>
    <p>Hier folgt ein allgemeiner, verständlicher Überblick...</p>
    
    <h2>2. Allgemeine Hinweise und Pflichtinformationen</h2>
    <h3>Datenschutz</h3>
    <p>Die Betreiber dieser Seiten nehmen den Schutz Ihrer persönlichen Daten sehr ernst...</p>
    
    <h3>Hinweis zur verantwortlichen Stelle</h3>
    <p>Die verantwortliche Stelle für die Datenverarbeitung auf dieser Website ist:</p>
    <address>
        Max Mustermann<br>
        Musterstraße 1<br>
        12345 Musterstadt
    </address>
    
    <h2>3. Datenerfassung auf dieser Website</h2>
    <h3>Server-Log-Dateien</h3>
    <p>Der Provider der Seiten erhebt und speichert automatisch Informationen in so genannten Server-Log-Dateien, die Ihr Browser automatisch an uns übermittelt. Dies sind:</p>
    <ul>
        <li>Browsertyp und Browserversion</li>
        <li>verwendetes Betriebssystem</li>
        <li>Referrer URL</li>
        <li>Hostname des zugreifenden Rechners</li>
        <li>Uhrzeit der Serveranfrage</li>
        <li>IP-Adresse</li>
    </ul>
    <p>Eine Zusammenführung dieser Daten mit anderen Datenquellen wird nicht vorgenommen. Grundlage für die Datenverarbeitung ist Art. 6 Abs. 1 lit. f DSGVO...</p>
    
    <!-- ... weitere Abschnitte für Cookies, Kontaktformular etc. -->
</main>
```

Da es fast unmöglich ist, als Laie eine vollständige und korrekte Datenschutzerklärung selbst zu verfassen, lautet die klare Empfehlung: Nutze einen professionellen Datenschutz-Generator. Es gibt mehrere seriöse Anbieter online (teils kostenlos, teils kostenpflichtig), die dich durch einen Fragenkatalog führen ("Welche Dienste nutzt du?") und am Ende einen maßgeschneiderten Text ausgeben, den du kopieren und in deine `datenschutz.html` einfügen kannst.

#### Die Einbindung in dein HTML-Projekt

Beide Seiten, `impressum.html` und `datenschutz.html`, sind nun inhaltlich gefüllt. Der letzte Schritt ist ihre nahtlose Integration in die Gesamtstruktur deiner Website. Wie bereits erwähnt, ist der Footer der Standardort für diese Links.

Ein sauber strukturierter Footer könnte so aussehen:

```html
<footer>
    <div class="footer-content">
        <p>&copy; 2024 Max Mustermann. Alle Rechte vorbehalten.</p>
        <nav class="footer-nav">
            <ul>
                <li><a href="/impressum.html">Impressum</a></li>
                <li><a href="/datenschutz.html">Datenschutz</a></li>
            </ul>
        </nav>
    </div>
</footer>
```

Dieser `<footer>`-Block gehört in jede einzelne HTML-Seite deines Projekts, damit die Links wirklich von überall aus erreichbar sind. In späteren Entwicklungsstadien, wenn du mit serverseitigen Sprachen oder Frameworks arbeitest, wirst du solche wiederkehrenden Elemente als "Includes" oder "Komponenten" auslagern, um den Code nicht auf jeder Seite duplizieren zu müssen. Für ein reines HTML/CSS-Projekt ist das manuelle Kopieren aber der gängige Weg.

Indem du diese beiden Seiten von Anfang an in deinem Projekt einplanst, schaffst du nicht nur rechtliche Sicherheit, sondern zeigst auch, dass du verantwortungsvoll und professionell mit deinem Webauftritt umgehst.
