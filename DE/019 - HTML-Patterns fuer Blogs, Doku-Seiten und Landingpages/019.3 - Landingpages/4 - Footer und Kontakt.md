# Footer und Kontakt

# Footer und Kontakt: Der letzte Eindruck zählt

Am Ende einer langen Reise, nachdem du deine Besucher durch eine fesselnde Geschichte, überzeugende Argumente und brillante Call-to-Actions geführt hast, kommen sie an: ganz unten auf deiner Landingpage. Dieser Bereich, der Footer, wird oft stiefmütterlich behandelt – ein Sammelsurium für Links, die sonst nirgends Platz fanden. Doch gerade hier, am Ende der Seite, hast du die Chance, einen bleibenden, professionellen Eindruck zu hinterlassen, Vertrauen zu festigen und rechtliche Sicherheit zu schaffen. Ein gut gemachter Footer ist kein Abstellgleis, sondern das Fundament, auf dem deine Seite ruht.

### Die semantische Grundlage: Das `<footer>`-Element

Bevor wir uns den Inhalten widmen, lass uns über die richtige Verpackung sprechen. In HTML gibt es für fast alles ein passendes semantisches Element, und der Seitenfuß ist keine Ausnahme. Anstatt ein unspezifisches `<div id="footer">` zu verwenden, greifst du zum `<footer>`-Element.

```html
<footer>
  <!-- Alle Inhalte des Footers kommen hier hinein -->
</footer>
```

Warum ist das wichtig? Das `<footer>`-Element teilt dem Browser und assistiven Technologien (wie Screenreadern) unmissverständlich mit: „Hier beginnen die Abschlussinformationen der Seite.“ Das verbessert nicht nur die Barrierefreiheit, sondern hilft auch Suchmaschinen, die Struktur deiner Seite besser zu verstehen. Ein Footer enthält typischerweise Informationen über den Autor, Copyright-Daten, Links zu verwandten Dokumenten und Kontaktinformationen.

### Die Kernbestandteile eines Landingpage-Footers

Ein Footer auf einer Landingpage verfolgt andere Ziele als der einer riesigen Unternehmenswebsite. Während Letzterer oft eine komplette Sitemap abbildet, muss der Landingpage-Footer fokussiert bleiben. Sein Hauptzweck ist es, Vertrauen zu schaffen und die notwendigsten Informationen bereitzustellen, ohne vom eigentlichen Ziel – der Conversion – abzulenken.

#### 1. Rechtliche Sicherheit: Impressum und Datenschutz

In vielen Ländern, insbesondere in Deutschland, sind Impressum und Datenschutzerklärung gesetzlich vorgeschrieben. Diese Links sind nicht verhandelbar und gehören in jeden Footer. Sie signalisieren deinem Besucher, dass du ein seriöser Anbieter bist, der sich an die Regeln hält. Das schafft enormes Vertrauen.

Strukturell setzt du diese Links am besten als einfache, ungeordnete Liste um.

```html
<div class="footer-legal">
  <ul>
    <li><a href="/impressum">Impressum</a></li>
    <li><a href="/datenschutz">Datenschutz</a></li>
  </ul>
</div>
```

Diese Links sollten klar erkennbar und leicht zugänglich sein. Verstecke sie nicht. Ein Nutzer, der nach diesen Informationen sucht und sie nicht findet, wird deine Seite mit einem unguten Gefühl verlassen.

#### 2. Kontaktinformationen: Erreichbarkeit schafft Vertrauen

Nichts sagt „Wir sind für dich da“ so deutlich wie eine klare Kontaktmöglichkeit. Selbst wenn der primäre Call-to-Action deiner Landingpage ein Formular ist, schafft eine sichtbare Adresse oder Telefonnummer eine zusätzliche Ebene der Glaubwürdigkeit. Dein Unternehmen ist greifbar, keine anonyme Entität im Internet.

Für die Auszeichnung von Kontaktinformationen bietet HTML das `<address>`-Element. Wichtig ist hierbei zu verstehen, wofür es gedacht ist: Es zeichnet Kontaktinformationen für den nächstgelegenen übergeordneten `<article>`- oder `<body>`-Kontext aus. Im Footer bezieht es sich also auf das gesamte Dokument oder das Unternehmen dahinter.

```html
<address>
  <strong>Deine Firma GmbH</strong><br>
  Musterstraße 123<br>
  12345 Musterstadt<br>
  <a href="mailto:hallo@deinefirma.de">hallo@deinefirma.de</a><br>
  <a href="tel:+49123456789">+49 (0) 123 456 789</a>
</address>
```

Achte auf die Verwendung von `mailto:`- und `tel:`-Links. Klickt ein Nutzer auf einem Smartphone auf die Telefonnummer, öffnet sich direkt die Wähl-App. Ein Klick auf die E-Mail-Adresse startet das E-Mail-Programm des Nutzers. Das ist eine kleine, aber feine nutzerfreundliche Geste.

#### 3. Copyright-Hinweis: Der Klassiker

Der Copyright-Hinweis ist ein Standardelement in fast jedem Footer. Er ist zwar rechtlich nicht immer zwingend, gehört aber zum guten Ton und signalisiert, dass die Inhalte auf der Seite geschützt sind. Die Struktur ist simpel: das Copyright-Symbol, das aktuelle Jahr und der Name deines Unternehmens oder deiner Marke.

Für das ©-Symbol verwendest du die HTML-Entität `&copy;`.

```html
<div class="footer-copyright">
  <p>&copy; 2024 Deine Firma GmbH. Alle Rechte vorbehalten.</p>
</div>
```

Das Jahr kannst du manuell pflegen oder mit ein wenig JavaScript automatisch aktualisieren lassen, damit es immer aktuell ist. Für eine statische Landingpage reicht es aber oft, es einmal pro Jahr anzupassen.

#### 4. Social-Media-Links: Eine zweischneidige Klinge

Links zu deinen Social-Media-Profilen können deine Markenpräsenz stärken und Besuchern eine alternative Möglichkeit bieten, mit dir in Kontakt zu bleiben. Auf einer Landingpage sind sie jedoch mit Vorsicht zu genießen.

**Die Gefahr:** Jeder externe Link ist ein potenzieller Fluchtweg. Das Ziel deiner Landingpage ist eine bestimmte Aktion (Kauf, Anmeldung, Download). Wenn ein Besucher auf dein Instagram-Profil klickt, verlässt er deine Seite und wird vielleicht nie wieder zurückkehren, abgelenkt von Katzenvideos und Urlaubsfotos.

**Die Lösung:** Wenn du Social-Media-Links einbindest, gestalte sie dezent. Sie sollten nicht mit deinem primären Call-to-Action konkurrieren. Oft werden dafür kleine Icons ohne Text verwendet. Platziere sie unauffällig, aber auffindbar.

Die semantisch korrekte Umsetzung ist eine Liste von Links, oft mit SVG-Icons für die Darstellung.

```html
<div class="footer-social">
  <ul>
    <li>
      <a href="https://twitter.com/deinprofil" aria-label="Folge uns auf Twitter">
        <!-- SVG Icon für Twitter hier einfügen -->
      </a>
    </li>
    <li>
      <a href="https://linkedin.com/deinprofil" aria-label="Verbinde dich mit uns auf LinkedIn">
        <!-- SVG Icon für LinkedIn hier einfügen -->
      </a>
    </li>
  </ul>
</div>
```

Beachte das `aria-label`-Attribut. Da ein Icon allein keine beschreibende Information für Screenreader liefert, gibst du mit dem `aria-label` eine textliche Alternative an. Das ist ein wichtiger Beitrag zur Barrierefreiheit.

### Das Gesamtbild: Ein komplettes Footer-Beispiel

Fügen wir nun alle Teile zu einem vollständigen, gut strukturierten Footer zusammen. Wir nutzen `<div>`-Elemente, um die einzelnen Bereiche für das spätere Styling mit CSS zu gruppieren.

```html
<footer>
  <div class="footer-container">
    
    <div class="footer-contact">
      <h3>Kontakt</h3>
      <address>
        <strong>Deine Firma GmbH</strong><br>
        Musterstraße 123<br>
        12345 Musterstadt<br>
        <a href="mailto:hallo@deinefirma.de">hallo@deinefirma.de</a><br>
        <a href="tel:+49123456789">+49 (0) 123 456 789</a>
      </address>
    </div>

    <div class="footer-social">
      <h3>Folge uns</h3>
      <ul>
        <li><a href="#" aria-label="Twitter"><!-- Icon --></a></li>
        <li><a href="#" aria-label="Facebook"><!-- Icon --></a></li>
        <li><a href="#" aria-label="LinkedIn"><!-- Icon --></a></li>
      </ul>
    </div>
    
  </div>

  <div class="footer-bottom">
    <div class="footer-legal">
      <ul>
        <li><a href="/impressum">Impressum</a></li>
        <li><a href="/datenschutz">Datenschutz</a></li>
      </ul>
    </div>
    <div class="footer-copyright">
      <p>&copy; 2024 Deine Firma GmbH</p>
    </div>
  </div>
</footer>
```

Dieses HTML-Gerüst ist logisch und semantisch sauber. Der obere Teil (`footer-container`) enthält die interaktiveren Elemente wie Kontakt und Social Media, während der untere, oft optisch abgesetzte Teil (`footer-bottom`) die rechtlichen Pflichtangaben und das Copyright bündelt.

### Ein Hauch von Stil: Grundlegendes CSS für den Footer

Obwohl dies ein HTML-Kapitel ist, ist die Struktur nur die halbe Miete. Ein wenig CSS hilft, die Funktionalität und Lesbarkeit des Footers zu visualisieren. Mit modernen Layout-Techniken wie Flexbox oder CSS Grid kannst du die Elemente flexibel anordnen.

Hier ist ein einfaches CSS-Beispiel, das unser HTML-Konstrukt in eine ansehnliche Form bringt:

```css
footer {
  background-color: #2c3e50; /* Dunkler Hintergrund */
  color: #ecf0f1; /* Heller Text */
  padding: 40px 20px;
  font-size: 0.9em;
}

.footer-container {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  gap: 20px;
  padding-bottom: 30px;
  margin-bottom: 30px;
  border-bottom: 1px solid #34495e; /* Trennlinie */
}

.footer-contact,
.footer-social {
  flex: 1;
  min-width: 250px;
}

footer h3 {
  color: #ffffff;
  margin-bottom: 15px;
}

footer a {
  color: #ecf0f1;
  text-decoration: none;
  transition: color 0.3s ease;
}

footer a:hover {
  color: #3498db; /* Akzentfarbe bei Hover */
}

footer address {
  font-style: normal;
  line-height: 1.6;
}

.footer-social ul {
  list-style: none;
  padding: 0;
  display: flex;
  gap: 15px;
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 20px;
  text-align: center;
}

.footer-legal ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  gap: 20px;
}

.footer-copyright p {
  margin: 0;
}
```

Dieses CSS erzeugt einen zweigeteilten Footer. Der obere Bereich ordnet Kontakt und Social-Media-Links nebeneinander an (dank Flexbox), während der untere Bereich die rechtlichen Links und das Copyright sauber aufteilt. Die Farbgebung ist dezent, die Links haben einen Hover-Effekt für besseres Feedback, und die Abstände sorgen für eine gute Lesbarkeit.

Der Footer ist weit mehr als nur das Ende deiner Seite. Er ist eine Visitenkarte, ein Vertrauensanker und ein rechtliches Schutzschild. Indem du ihm die gleiche Sorgfalt widmest wie dem Rest deiner Landingpage und ihn mit sauberem, semantischem HTML aufbaust, rundest du das Nutzererlebnis professionell ab und sorgst dafür, dass der letzte Eindruck ein positiver ist.
