# Das address-Element

### Das `<address>`-Element: Mehr als nur eine Anschrift

Wenn du im Web auf Kontaktinformationen stößt – eine E-Mail-Adresse, eine Telefonnummer oder die Anschrift eines Unternehmens –, dann steckt dahinter idealerweise das HTML-`<address>`-Element. Auf den ersten Blick scheint seine Aufgabe klar zu sein, doch seine korrekte Anwendung ist feiner und kontextabhängiger, als du vielleicht denkst. Es geht hierbei nicht nur darum, eine Adresse auf der Seite darzustellen, sondern darum, dem Browser und assistiven Technologien eine ganz bestimmte semantische Information zu geben: „Hier findest du die Kontaktmöglichkeiten für den Autor oder Besitzer dieses Inhalts.“

#### Die semantische Bedeutung: Wer ist der Ansprechpartner?

Das Wichtigste zuerst: Das `<address>`-Element ist nicht für *irgendeine* Adresse gedacht. Du würdest es zum Beispiel nicht verwenden, um die Anschrift eines Restaurants in einem Blogartikel über deine Lieblingspizzen zu markieren. Stattdessen dient es ausschließlich dazu, die Kontaktinformationen für den Autor oder Herausgeber des Dokuments oder eines bestimmten Abschnitts davon bereitzustellen.

Hier wird es interessant, denn der Geltungsbereich des `<address>`-Elements hängt von seiner Position im HTML-Dokument ab. Die goldene Regel lautet: Das `<address>`-Element liefert Kontaktinformationen für das nächstgelegene übergeordnete `<article>`- oder `<body>`-Element.

**1. Kontaktinformationen für die gesamte Webseite**

Wenn du das `<address>`-Element direkt innerhalb des `<body>`-Tags platzierst (aber außerhalb eines `<article>`-Elements), beziehen sich die darin enthaltenen Informationen auf das gesamte Dokument. In der Praxis ist dies meist der Fall, wenn du es im `<footer>` deiner Webseite einsetzt, um die Kontaktdaten des Webseitenbetreibers, des Unternehmens oder der Organisation anzugeben.

Stell dir vor, du erstellst die Webseite für ein fiktives Designstudio namens „Pixelperfekt“. Die Kontaktinformationen im Fußbereich der Seite könnten so aussehen:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Pixelperfekt Designstudio</title>
</head>
<body>
    <header>
        <h1>Willkommen bei Pixelperfekt</h1>
    </header>

    <main>
        <p>Wir gestalten einzigartige digitale Erlebnisse.</p>
        <!-- Hauptinhalt der Seite hier ... -->
    </main>

    <footer>
        <address>
            Pixelperfekt GmbH<br>
            Kreativstraße 123<br>
            10115 Berlin<br>
            <a href="mailto:hallo@pixelperfekt.de">hallo@pixelperfekt.de</a><br>
            <a href="tel:+493012345678">+49 30 12345678</a>
        </address>
    </footer>
</body>
</html>
```

In diesem Beispiel ist das `<address>`-Element im `<footer>` platziert, der wiederum ein direktes Kind des `<body>` ist. Somit ist klar: Diese Kontaktdaten gehören zum Betreiber der gesamten Webseite, der Pixelperfekt GmbH.

**2. Kontaktinformationen für einen bestimmten Artikel**

Anders verhält es sich, wenn du das `<address>`-Element innerhalb eines `<article>`-Elements verwendest. Das `<article>`-Element repräsentiert einen in sich geschlossenen, eigenständigen Inhalt, wie einen Blogbeitrag, einen Forenpost oder einen Nachrichtenartikel. Wenn du `<address>` hier platzierst, lieferst du die Kontaktinformationen spezifisch für den Autor *dieses einen Artikels*. Das ist besonders nützlich für Blogs mit Gastautoren oder Nachrichtenseiten mit Beiträgen von verschiedenen Journalisten.

Nehmen wir an, auf der Webseite des Designstudios gibt es einen Blog. Ein Gastautor namens Alex Schmidt hat einen Fachartikel geschrieben. Die Kontaktinformationen für Alex sollten direkt mit seinem Artikel verknüpft sein:

```html
<main>
    <article>
        <h2>Die Psychologie der Farben im Webdesign</h2>
        <p>Farben sind mehr als nur Dekoration. Sie beeinflussen Emotionen, Handlungen und die Wahrnehmung einer Marke ...</p>
        <!-- ... weiterer Inhalt des Artikels ... -->
        
        <footer>
            <p>Verfasst von Alex Schmidt.</p>
            <address>
                Kontakt zu Alex Schmidt:<br>
                <a href="mailto:alex.schmidt@email.com">alex.schmidt@email.com</a><br>
                Oder besuche sein Profil auf <a href="https://socialmedia.example/alexschmidt">Social Media</a>.
            </address>
        </footer>
    </article>
</main>
```

Hier ist das `<address>`-Element innerhalb des `<article>`-Elements verschachtelt. Damit teilst du dem Browser und Suchmaschinen eindeutig mit: Diese Kontaktdaten gehören zu Alex Schmidt, dem Autor dieses spezifischen Artikels, und nicht zur Pixelperfekt GmbH, die die Webseite betreibt.

#### Was gehört hinein – und was nicht?

Die Spezifikation ist recht klar darin, welche Art von Informationen in ein `<address>`-Element gehören. Dazu zählen:

*   **Name des Autors oder der Organisation:** Der Name der Person oder Firma, die kontaktiert werden kann.
*   **Physische Adresse:** Straße, Postleitzahl, Stadt, Land.
*   **URL:** Ein Link zur Webseite, zum Kontaktformular oder zu einem Social-Media-Profil.
*   **E-Mail-Adresse:** Idealerweise als klickbarer `mailto:`-Link.
*   **Telefonnummer:** Oft als klickbarer `tel:`-Link für mobile Geräte.
*   **Koordinaten:** Geografische Angaben können ebenfalls Teil der Kontaktinformation sein.

**Ein gutes, umfassendes Beispiel:**

```html
<address>
  <p>
    <strong>Anna Musterfrau</strong><br>
    Chefredakteurin<br>
    Beispiel-Magazin<br>
    Musterstraße 1<br>
    12345 Musterstadt
  </p>
  <p>
    Telefon: <a href="tel:+491234567890">+49 123 456 78 90</a><br>
    E-Mail: <a href="mailto:anna.musterfrau@beispiel.de">anna.musterfrau@beispiel.de</a>
  </p>
  <p>
    Folge Anna auf <a href="https://social.example/amusterfrau">ihrem Profil</a>.
  </p>
</address>
```

Genauso wichtig wie zu wissen, was hineingehört, ist zu verstehen, was du unbedingt vermeiden solltest. Das `<address>`-Element ist **nicht** für folgende Informationen gedacht:

*   **Beliebige Adressen:** Wie bereits erwähnt, gehört die Anschrift eines im Text erwähnten Ortes (z.B. ein Hotel, ein Veranstaltungsort) nicht in ein `<address>`-Element. Diese ist eine normale Textinformation und sollte in einem `<p>`-Tag stehen.
*   **Veröffentlichungsdatum:** Das Datum, an dem ein Artikel geschrieben oder veröffentlicht wurde, hat eine eigene semantische Heimat: das `<time>`-Element.
*   **Copyright-Informationen:** Obwohl sie oft im `<footer>` in der Nähe der Adresse stehen, gehören Copyright-Vermerke nicht direkt in das `<address>`-Element. Sie stehen besser in einem `<p>`- oder `<small>`-Tag.

**Ein falsches Anwendungsbeispiel:**

```html
<!-- FALSCH! -->
<p>
  Unser Firmenevent findet dieses Jahr im Hotel "Zum Goldenen Anker" statt.
  Die Adresse ist:
  <address>
    Am Hafen 5, 20457 Hamburg
  </address>
</p>
```

Diese Verwendung ist semantisch inkorrekt, da die Adresse des Hotels keine Kontaktinformation für den Autor der Webseite ist.

#### Standard-Styling und wie du damit umgehst

Standardmäßig rendern die meisten Webbrowser den Inhalt eines `<address>`-Elements kursiv. Dieser Umstand verleitet viele Anfänger dazu, das Element fälschlicherweise für rein stilistische Zwecke zu missbrauchen, wann immer sie kursiven Text benötigen. Das ist ein fundamentaler Fehler. Für kursiven Text, der keine spezielle semantische Bedeutung hat, solltest du das `<i>`-Element oder besser noch CSS (`font-style: italic;`) verwenden.

Die semantische Bedeutung ist immer wichtiger als die Standarddarstellung. Wenn dir der kursive Stil nicht gefällt, kannst du ihn ganz einfach mit CSS überschreiben:

```css
address {
  font-style: normal;
  line-height: 1.5; /* Verbessert die Lesbarkeit von mehrzeiligen Adressen */
}
```

Mit dieser einfachen CSS-Regel entfernst du die Kursivschrift und stellst sicher, dass deine Adresse wie normaler Text aussieht. Gleichzeitig behältst du den enormen semantischen Vorteil, den das korrekte HTML-Element bietet. Maschinenlesbarkeit, Barrierefreiheit für Screenreader und eine bessere Indexierung durch Suchmaschinen sind die wahren Stärken, die weit über das Visuelle hinausgehen.

Das `<address>`-Element ist also ein kleines, aber mächtiges Werkzeug in deinem HTML-Baukasten. Wenn du seinen kontextabhängigen Geltungsbereich verstanden hast, kannst du es präzise einsetzen, um deine Dokumente strukturierter, verständlicher und für Mensch und Maschine gleichermaßen wertvoller zu machen.
