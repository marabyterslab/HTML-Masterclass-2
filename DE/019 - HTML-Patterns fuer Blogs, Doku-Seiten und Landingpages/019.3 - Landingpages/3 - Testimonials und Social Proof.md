# Testimonials und Social Proof

### Vertrauen schaffen: Testimonials und Social Proof

Stell dir vor, du stehst in einer fremden Stadt vor zwei Restaurants. Das eine ist leer, im anderen drängen sich die Leute. Welches wählst du? Wahrscheinlich das volle. Du gehst davon aus, dass die vielen Menschen dort sind, weil das Essen gut ist. Dieses unbewusste Verhalten nennt man Social Proof – sozialer Beweis. Wir Menschen neigen dazu, den Handlungen und Meinungen anderer zu vertrauen, besonders wenn wir uns unsicher sind.

Auf einer Landingpage ist dieser Effekt pures Gold. Ein Besucher kennt dich oder dein Produkt vielleicht noch nicht und ist von Natur aus skeptisch. Deine Aufgabe ist es, diese Skepsis in Vertrauen umzuwandeln. Und genau hier kommen Testimonials und andere Formen von Social Proof ins Spiel. Sie sind nicht nur schmückendes Beiwerk, sondern ein fundamentaler Baustein, um die Brücke zum potenziellen Kunden zu bauen.

#### Das klassische Testimonial: Mehr als nur ein Zitat

Ein Testimonial ist die direkteste Form von Social Proof. Eine echte Person bestätigt, dass dein Produkt oder deine Dienstleistung ihr geholfen hat. Doch wie baust du so etwas semantisch korrekt in HTML auf? Ein einfacher `<div>` mit einem `<p>`-Tag ist zwar schnell getippt, verschenkt aber wertvolles Potenzial in Sachen Semantik und Barrierefreiheit.

Die eleganteste und korrekteste Struktur für ein Zitat mit einer Quellenangabe bietet die Kombination aus `<figure>`, `<blockquote>` und `<figcaption>`.

-   `<blockquote>`: Dieses Element ist speziell für Zitate gedacht, die aus einer anderen Quelle stammen. Es signalisiert dem Browser und Screenreadern, dass der darin enthaltene Text ein Zitat ist.
-   `<figure>`: Ursprünglich für Bilder und Diagramme gedacht, ist `<figure>` ein Container für in sich geschlossene Inhalte, die im Dokument referenziert werden. Ein Testimonial – bestehend aus Zitat und Autor – ist ein perfekter Anwendungsfall.
-   `<figcaption>`: Dieses Element gehört untrennbar zu `<figure>` und beschreibt dessen Inhalt. Hier platzierst du den Namen des Autors, seine Position oder Firma.

So sieht das in der Praxis aus:

```html
<figure class="testimonial">
  <blockquote>
    <p>Die Zusammenarbeit hat unsere Erwartungen übertroffen. Innerhalb von drei Monaten konnten wir unsere Conversion-Rate um 30 % steigern. Ein absoluter Game-Changer für unser Business!</p>
  </blockquote>
  <figcaption>
    <img src="path/to/max-mustermann.jpg" alt="Foto von Max Mustermann" class="testimonial-author-image">
    <cite>Max Mustermann</cite>, CEO von Beispiel GmbH
  </figcaption>
</figure>
```

In diesem Beispiel haben wir sogar noch ein paar Details verfeinert:

1.  **Das Bild**: Ein Foto der Person schafft sofort mehr Authentizität. Achte auf ein aussagekräftiges `alt`-Attribut.
2.  **Das `<cite>`-Element**: Es wird verwendet, um den Titel eines Werks (z. B. Buch, Film) zu kennzeichnen, aber in der Praxis oft auch für den Namen der zitierten Person. Es ist semantisch passender als ein einfacher `<span>`.

Diese Struktur ist nicht nur sauber, sondern auch für Maschinen verständlich. Ein Screenreader kann einem Nutzer klar vermitteln: "Hier beginnt ein Zitat. Es lautet: [...]. Das Zitat stammt von Max Mustermann."

#### Testimonials mit Sternen: Bewertungen visuell und semantisch korrekt darstellen

Besonders im E-Commerce oder bei Dienstleistungen sind Sternebewertungen ein extrem starkes Signal. Sie fassen die Zufriedenheit in einem einzigen, leicht verständlichen Symbol zusammen. Doch die Implementierung birgt Tücken. Einfach fünf Stern-Emojis (⭐️⭐️⭐️⭐️⭐️) in den Text zu kopieren, ist aus Sicht der Barrierefreiheit eine schlechte Idee. Screenreader lesen diese Emojis oft umständlich oder inkonsistent vor.

Eine bessere Lösung kombiniert visuelle Darstellung mit verstecktem, aber maschinenlesbarem Text.

```html
<div class="star-rating" role="img" aria-label="Bewertung: 4 von 5 Sternen">
  <span class="star filled" aria-hidden="true">★</span>
  <span class="star filled" aria-hidden="true">★</span>
  <span class="star filled" aria-hidden="true">★</span>
  <span class="star filled" aria-hidden="true">★</span>
  <span class="star" aria-hidden="true">☆</span>
</div>
```

Oder noch einfacher, mit einem expliziten Text für Screenreader:

```html
<div class="star-rating">
  <!-- Visuelle Darstellung der Sterne (z.B. mit SVGs oder Icon-Font) -->
  <svg>...</svg> <svg>...</svg> <svg>...</svg> <svg>...</svg> <svg class="empty">...</svg>
  <span class="visually-hidden">Bewertung: 4 von 5 Sternen</span>
</div>
```

Der Schlüssel hierbei ist, die tatsächliche Bewertung ("4 von 5 Sternen") in einer Form bereitzustellen, die für assistierende Technologien zugänglich ist. Das `aria-label` im ersten Beispiel oder die Klasse `.visually-hidden` im zweiten (die per CSS aus dem sichtbaren Bereich verschoben wird) stellen genau das sicher. Die visuellen Sterne werden mit `aria-hidden="true"` für Screenreader versteckt, da ihre Bedeutung bereits durch den Text vermittelt wird.

Integriert in unser Testimonial-Beispiel könnte das so aussehen:

```html
<figure class="testimonial">
  <div class="testimonial-header">
    <div class="star-rating" role="img" aria-label="Bewertung: 5 von 5 Sternen">
      <!-- 5 gefüllte Sterne als SVGs oder Icons -->
    </div>
  </div>
  <blockquote>
    <p>Einfach das beste Tool auf dem Markt. Ich kann es jedem nur empfehlen!</p>
  </blockquote>
  <figcaption>
    <!-- ... Autor, Firma, etc. ... -->
  </figcaption>
</figure>
```

#### Die Königsdisziplin: Video-Testimonials

Nichts ist überzeugender als eine echte Person, die mit eigener Stimme und Mimik von ihren positiven Erfahrungen berichtet. Video-Testimonials haben eine enorme emotionale Wirkung. Technisch sind sie meist einfach über Plattformen wie YouTube oder Vimeo einzubetten.

Das Standard-HTML dafür ist ein `<iframe>`:

```html
<div class="video-testimonial-wrapper">
  <iframe 
    width="560" 
    height="315" 
    src="https://www.youtube.com/embed/VIDEO_ID" 
    title="Kundenstimme von Erika Musterfrau" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen
    loading="lazy">
  </iframe>
</div>
```

Achte hier auf zwei wichtige Attribute:

1.  `title`: Dieses Attribut ist entscheidend für die Barrierefreiheit. Es beschreibt den Inhalt des iframes für Nutzer, die ihn nicht sehen können.
2.  `loading="lazy"`: Ein absolutes Muss! Dieses Attribut weist den Browser an, das Video erst dann zu laden, wenn es in den sichtbaren Bereich des Nutzers scrollt. Das verbessert die Ladezeit deiner Landingpage drastisch, da nicht sofort mehrere Megabyte an Videodaten geladen werden müssen.

#### Über den Tellerrand hinaus: Weitere Formen von Social Proof

Testimonials sind mächtig, aber sie sind nicht die einzige Möglichkeit, Vertrauen aufzubauen. Oft ist eine Kombination verschiedener Elemente am wirkungsvollsten.

##### Die "Bekannt aus"-Logowand

Hast du für bekannte Unternehmen gearbeitet oder wurdest du in bekannten Medien erwähnt? Zeig es! Eine Logowand schafft durch Assoziation Vertrauen ("Wenn Firma X ihnen vertraut, dann kann ich das auch").

Der HTML-Code dafür ist denkbar einfach: eine semantische Liste.

```html
<section class="logo-wall" aria-labelledby="logo-wall-title">
  <h3 id="logo-wall-title" class="visually-hidden">Vertraut von</h3>
  <ul>
    <li><img src="logos/firma-a.svg" alt="Logo von Firma A"></li>
    <li><img src="logos/magazin-b.svg" alt="Logo von Magazin B"></li>
    <li><img src="logos/konzern-c.svg" alt="Logo von Konzern C"></li>
  </ul>
</section>
```

Hier ist das `alt`-Attribut der Bilder wieder von größter Bedeutung. Es muss den Namen des Unternehmens enthalten, damit der Kontext auch für Screenreader-Nutzer klar ist. Die Überschrift, die mit `aria-labelledby` mit der Sektion verknüpft ist, gibt der gesamten Sektion einen barrierefreien Namen, auch wenn die Überschrift visuell versteckt ist.

##### Die Macht der Zahlen

Konkrete Zahlen sind schnell zu erfassen und extrem überzeugend. Beispiele sind:
-   "Über 100.000 zufriedene Kunden"
-   "Schon 2.500 Teams nutzen unser Tool täglich"
-   "4.9/5 Sterne aus 1.200 Bewertungen"

HTML-seitig sind hier keine komplexen Strukturen nötig. Wichtig ist, die Zahlen hervorzuheben.

```html
<div class="stats-container">
  <div class="stat-item">
    <p class="stat-number">100.000+</p>
    <p class="stat-label">zufriedene Kunden</p>
  </div>
  <div class="stat-item">
    <p class="stat-number">4.9 / 5</p>
    <p class="stat-label">Durchschnittsbewertung</p>
  </div>
</div>
```

#### Für die Suchmaschine: Testimonials mit strukturierten Daten anreichern

Stell dir vor, deine Sternebewertungen erscheinen direkt in den Google-Suchergebnissen neben dem Link zu deiner Seite. Das erhöht die Klickrate enorm. Möglich wird das durch strukturierte Daten, genauer gesagt durch das Vokabular von Schema.org.

Du erweiterst deinen bestehenden HTML-Code um spezielle Attribute, die den Suchmaschinen die genaue Bedeutung des Inhalts erklären. Für ein Testimonial ist der Typ `Review` relevant.

Schauen wir uns unser ursprüngliches Testimonial-Beispiel an und reichern es mit Schema.org-Mikrodaten an:

```html
<figure class="testimonial" itemscope itemtype="https://schema.org/Review">
  <div class="testimonial-header" itemprop="reviewRating" itemscope itemtype="https://schema.org/Rating">
    <meta itemprop="worstRating" content="1">
    <meta itemprop="bestRating" content="5">
    <span itemprop="ratingValue" class="visually-hidden">5</span>
    <div class="star-rating" role="img" aria-label="Bewertung: 5 von 5 Sternen">
      <!-- 5 gefüllte Sterne -->
    </div>
  </div>
  
  <blockquote itemprop="reviewBody">
    <p>Die Zusammenarbeit hat unsere Erwartungen übertroffen. Innerhalb von drei Monaten konnten wir unsere Conversion-Rate um 30 % steigern. Ein absoluter Game-Changer für unser Business!</p>
  </blockquote>

  <figcaption itemprop="author" itemscope itemtype="https://schema.org/Person">
    <img src="path/to/max-mustermann.jpg" alt="Foto von Max Mustermann" class="testimonial-author-image">
    <cite itemprop="name">Max Mustermann</cite>, <span itemprop="jobTitle">CEO</span> von <span itemprop="affiliation">Beispiel GmbH</span>
  </figcaption>
</figure>
```

Was passiert hier genau?

-   `itemscope` eröffnet einen neuen "Daten-Block".
-   `itemtype="https://schema.org/Review"` teilt der Suchmaschine mit: "Alles innerhalb dieses Blocks beschreibt eine Bewertung."
-   `itemprop="..."` weist den einzelnen Elementen ihre Rolle zu:
    -   `reviewRating` für die Bewertung selbst (die wiederum ein eigener `Rating`-Typ ist).
    -   `ratingValue` für den numerischen Wert der Bewertung.
    -   `reviewBody` für den eigentlichen Text des Testimonials.
    -   `author` für die Person, die die Bewertung abgegeben hat (ein `Person`-Typ).
    -   `name`, `jobTitle`, `affiliation` beschreiben die Person genauer.

Das mag auf den ersten Blick komplex aussehen, aber die Logik dahinter ist simpel: Du machst deine semantisch bereits gute HTML-Struktur für Suchmaschinen noch verständlicher. Der Aufwand lohnt sich, denn er macht deine wertvollen sozialen Beweise auch außerhalb deiner Webseite sichtbar.
