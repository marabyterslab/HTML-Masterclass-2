# Verknüpfung mit footer

### Der `<footer>`: Adresse, Kontakt und die Verknüpfung mit der Welt

Stell dir eine Webseite wie ein gutes Buch vor. Sie hat einen Anfang, einen Mittelteil und einen Schluss. Der `<footer>`-Tag in HTML ist genau das: der formale Abschluss deiner Seite. Aber er ist weit mehr als nur ein schmückendes Ende. Er ist der Ort für wichtige, aber nicht primäre Informationen – dein digitaler Briefkopf, dein Impressum und dein Wegweiser zu weiterführenden Inhalten. In diesem Kapitel tauchen wir tief in die Rolle des Footers ein, insbesondere wie du ihn nutzt, um Kontaktinformationen bereitzustellen und wichtige Verknüpfungen zu schaffen.

#### Was gehört in einen Footer? Die semantische Bedeutung

Bevor wir Code schreiben, müssen wir verstehen, *warum* es den `<footer>`-Tag gibt. HTML ist eine semantische Sprache. Das bedeutet, dass die Tags nicht nur das Aussehen bestimmen (das ist die Aufgabe von CSS), sondern dem Inhalt eine Bedeutung geben. Wenn du etwas in einen `<footer>`-Tag packst, sagst du dem Browser und den Suchmaschinen: „Hey, diese Information gehört zum Abschluss des übergeordneten Abschnitts.“

Dieser übergeordnete Abschnitt ist meistens der gesamte `<body>` deiner Webseite. In diesem Fall enthält der Footer Informationen, die für die gesamte Seite gelten:
*   Copyright-Hinweise
*   Links zu Impressum, Datenschutz und AGB
*   Kontaktinformationen
*   Links zu Social-Media-Profilen
*   Manchmal eine vereinfachte Sitemap oder wichtige Navigationslinks

Ein `<footer>` kann aber auch innerhalb anderer strukturierender Elemente wie `<article>` oder `<section>` vorkommen. Dann bezieht er sich nur auf diesen spezifischen Abschnitt und könnte zum Beispiel Informationen zum Autor des Artikels oder das Veröffentlichungsdatum enthalten. Wir konzentrieren uns hier aber auf den globalen Seiten-Footer, da er für Adressen und Verknüpfungen die größte Rolle spielt.

#### Kontaktinformationen korrekt auszeichnen mit `<address>`

Eine der Kernaufgaben des Footers ist die Bereitstellung von Kontaktinformationen. Du könntest jetzt einfach einen `<p>`-Tag nehmen und die Adresse hineinschreiben. Das würde zwar angezeigt, wäre aber semantisch ungenau. HTML bietet uns hierfür ein spezielles Element: den `<address>`-Tag.

Der `<address>`-Tag ist dafür gedacht, Kontaktinformationen für den nächstgelegenen `<article>`- oder `<body>`-Vorfahren zu enthalten. Wenn du ihn also direkt im `<footer>` der Seite platzierst, wird klar, dass es sich um die Kontaktadresse des Seitenbetreibers handelt.

Ein einfaches Beispiel könnte so aussehen:

```html
<footer>
  <address>
    Webseiten-Manufaktur GmbH<br>
    Musterstraße 123<br>
    10115 Berlin<br>
    Deutschland
  </address>
</footer>
```

Beachte die Verwendung von `<br>`-Tags. Während du im Fließtext Zeilenumbrüche sparsam einsetzen solltest, sind sie innerhalb einer Postanschrift absolut legitim und notwendig, um die korrekte Formatierung zu gewährleisten.

Doch `<address>` kann mehr als nur eine Postanschrift aufnehmen. Es ist der richtige Ort für jede Art von Kontaktinformation. Besonders mächtig wird es, wenn wir es mit Links kombinieren.

#### Klickbare Kontaktmöglichkeiten: `mailto:` und `tel:`

Eine Adresse nur anzuzeigen, ist gut. Sie direkt nutzbar zu machen, ist besser. Zwei weitverbreitete Protokolle helfen dir dabei: `mailto:` für E-Mails und `tel:` für Telefonnummern. Indem du sie in `<a>`-Tags verwendest, ermöglichst du deinen Besuchern, mit einem Klick eine E-Mail zu schreiben oder einen Anruf zu starten.

Erweitern wir unser Beispiel:

```html
<footer>
  <address>
    <strong>Webseiten-Manufaktur GmbH</strong><br>
    Musterstraße 123<br>
    10115 Berlin<br>
    <br>
    E-Mail: <a href="mailto:kontakt@webseiten-manufaktur.de">kontakt@webseiten-manufaktur.de</a><br>
    Telefon: <a href="tel:+493012345678">+49 (0)30 123 456 78</a>
  </address>
</footer>
```

Schauen wir uns die Links genauer an:
*   `href="mailto:kontakt@webseiten-manufaktur.de"`: Der `mailto:`-Präfix sorgt dafür, dass sich beim Klick auf den Link das Standard-E-Mail-Programm des Nutzers öffnet, mit der angegebenen Adresse bereits im „An“-Feld.
*   `href="tel:+493012345678"`: Der `tel:`-Präfix bewirkt auf einem Smartphone, dass die Telefon-App mit der gewählten Nummer gestartet wird. Auf dem Desktop könnte es eine Anwendung wie Skype oder FaceTime öffnen. Achte auf das internationale Format mit `+` und der Landesvorwahl (hier `49` für Deutschland) und ohne Leerzeichen oder Sonderzeichen im `href`-Attribut selbst. Den für Menschen lesbaren Text kannst du hingegen frei formatieren.

#### Die Verknüpfung zur rechtlichen Welt: Impressum & Datenschutz

In vielen Ländern, insbesondere in Deutschland, ist ein Footer ohne Links zum Impressum und zur Datenschutzerklärung kaum denkbar. Diese Links sind nicht nur eine nette Geste, sondern gesetzlich vorgeschrieben. Der Footer ist der ideale und erwartete Ort für diese Verknüpfungen, da sie auf jeder einzelnen Unterseite deiner Website erreichbar sein müssen.

Semantisch gesehen handelt es sich hierbei um eine Liste von Navigationspunkten. Daher ist es die beste Praxis, diese Links in einer ungeordneten Liste (`<ul>`) zu strukturieren. Das hilft Screenreadern und Suchmaschinen, die Struktur zu verstehen.

```html
<footer>
  <ul>
    <li><a href="/impressum.html">Impressum</a></li>
    <li><a href="/datenschutz.html">Datenschutzerklärung</a></li>
    <li><a href="/agb.html">AGB</a></li>
  </ul>
</footer>
```

Diese Liste ist das Rückgrat der rechtlichen Absicherung deiner Webseite. Sie schafft Vertrauen und sorgt dafür, dass du rechtlichen Anforderungen nachkommst.

#### Ein vollständiger Footer: Alles zusammenfügen

Bringen wir nun alle Elemente zusammen, um einen realistischen, gut strukturierten Footer zu erstellen. Ein typischer Footer kombiniert oft mehrere Bereiche: Kontakt, rechtliche Links, Social Media und einen Copyright-Hinweis. Wir können diese Bereiche mit separaten Listen oder einfach durch die Strukturierung innerhalb des `<address>`-Elements und zusätzlicher `<p>`-Tags oder `<ul>`-Listen organisieren.

Hier ist ein umfassendes Beispiel, wie ein moderner Footer aussehen könnte:

```html
<footer>
  <div class="footer-container">
    
    <div class="footer-contact">
      <h3>Kontakt</h3>
      <address>
        <strong>Webseiten-Manufaktur GmbH</strong><br>
        Musterstraße 123<br>
        10115 Berlin<br>
        <br>
        <a href="mailto:kontakt@webseiten-manufaktur.de">kontakt@webseiten-manufaktur.de</a><br>
        <a href="tel:+493012345678">+49 (0)30 123 456 78</a>
      </address>
    </div>

    <div class="footer-legal">
      <h3>Rechtliches</h3>
      <ul>
        <li><a href="/impressum.html">Impressum</a></li>
        <li><a href="/datenschutz.html">Datenschutzerklärung</a></li>
        <li><a href="/agb.html">AGB</a></li>
        <li><a href="/kontakt.html">Kontaktformular</a></li>
      </ul>
    </div>

    <div class="footer-social">
      <h3>Folge uns</h3>
      <ul>
        <li><a href="https://twitter.com/deinprofil">Twitter</a></li>
        <li><a href="https://linkedin.com/in/deinprofil">LinkedIn</a></li>
        <li><a href="https://github.com/deinprofil">GitHub</a></li>
      </ul>
    </div>

  </div>

  <div class="footer-copyright">
    <p>&copy; 2023 Webseiten-Manufaktur GmbH. Alle Rechte vorbehalten.</p>
  </div>

</footer>
```
In diesem Beispiel haben wir `<div>`-Elemente zur Gruppierung verwendet und Überschriften (`<h3>`) hinzugefügt, um die einzelnen Sektionen klar voneinander zu trennen. Das `div class="footer-copyright"` am Ende enthält den Copyright-Hinweis. Das `&copy;`-Symbol ist eine HTML-Entität für das Copyright-Zeichen (©). Diese Struktur ist nicht nur für Menschen gut lesbar, sondern auch für Maschinen verständlich.

Der Footer ist also weit mehr als nur eine Fußzeile. Er ist ein fundamentales, semantisches Element, das Vertrauen schafft, rechtliche Sicherheit bietet und deinen Nutzern zentrale Informationen und Kontaktmöglichkeiten an einem leicht auffindbaren Ort zur Verfügung stellt. Eine gut durchdachte Verknüpfung im Footer ist ein Zeichen von Professionalität und Sorgfalt im Webdesign.
