# Breadcrumb-Navigation

### Breadcrumb-Navigation: Der digitale Wegweiser deiner Website

Erinnerst du dich an das Märchen von Hänsel und Gretel? Die beiden Kinder verstreuten Brotkrümel im Wald, um den Weg zurück nach Hause zu finden. Genau dieses Prinzip – eine Spur zu hinterlassen, die den Rückweg weist – ist die geniale Idee hinter der Breadcrumb-Navigation. Sie ist ein kleiner, aber ungemein nützlicher Wegweiser auf einer Website.

Eine Breadcrumb-Navigation (auf Deutsch auch „Brotkrümelnavigation“ oder „Ariadnepfad“) ist eine sekundäre Navigationsleiste, die dem Nutzer anzeigt, wo er sich gerade in der Hierarchie der Website befindet. Sie visualisiert den Pfad von der Startseite bis zur aktuell aufgerufenen Seite. Du findest sie meist horizontal am oberen Rand des Hauptinhaltsbereichs, direkt unter der Hauptnavigation oder dem Seitentitel.

Ein typisches Beispiel in einem Onlineshop könnte so aussehen:

**Startseite > Herrenbekleidung > Hemden > Leinenhemden**

Jeder Teil dieses Pfades, außer dem letzten, ist ein klickbarer Link. Das erlaubt dir, mit nur einem Klick schnell eine oder mehrere Ebenen in der Seitenstruktur zurückzuspringen. Statt mühsam den „Zurück“-Button des Browsers zu benutzen oder dich erneut durch das Hauptmenü zu klicken, springst du einfach direkt zur Kategorie „Hemden“ oder „Herrenbekleidung“. Das spart Zeit, reduziert die Anzahl der benötigten Klicks und verbessert die Orientierung des Nutzers erheblich – ein riesiger Gewinn für die User Experience (UX).

#### Die verschiedenen Arten der Breadcrumb-Navigation

Auch wenn das Grundprinzip immer gleich ist, unterscheidet man in der Praxis drei Haupttypen von Breadcrumbs.

1.  **Hierarchie- oder standortbasierte Breadcrumbs (Location-based)**
    Dies ist die mit Abstand häufigste und nützlichste Art. Sie spiegelt die Struktur deiner Website wider. Unabhängig davon, wie du auf die Seite „Leinenhemden“ gelangt bist – ob über die Suche, einen direkten Link oder die Navigation –, der Breadcrumb-Pfad bleibt immer derselbe: `Startseite > Herrenbekleidung > Hemden > Leinenhemden`. Er zeigt deine feste Position in der Informationsarchitektur. Für die meisten Websites, insbesondere solche mit klaren, tiefen Hierarchien wie Shops, Blogs oder Wissensdatenbanken, ist dieser Typ die beste Wahl.

2.  **Verlaufs- oder pfadbasierte Breadcrumbs (Path-based)**
    Diese Art zeigt dynamisch den Weg an, den du persönlich auf der Website zurückgelegt hast, um zur aktuellen Seite zu gelangen. Sie funktioniert also ähnlich wie der „Zurück“-Button deines Browsers, nur eben als klickbare Liste. Ein Pfad könnte also so aussehen: `Startseite > Sale > Damenschuhe > Herrenbekleidung > Leinenhemden`. Dieser Typ ist heute nur noch selten anzutreffen, da die Klickpfade von Nutzern oft unlogisch und chaotisch sind und ein solcher Breadcrumb mehr Verwirrung als Nutzen stiftet.

3.  **Attribut- oder eigenschaftsbasierte Breadcrumbs (Attribute-based)**
    Dieser Typ kommt hauptsächlich bei E-Commerce-Websites mit komplexen Filterfunktionen zum Einsatz. Er zeigt nicht den hierarchischen Pfad an, sondern die vom Nutzer ausgewählten Attribute oder Filter, die zur aktuellen Produktliste geführt haben. Zum Beispiel: `Startseite > Hemden > Filter: Größe=M, Farbe=Blau, Material=Leinen`. Jeder Filter wird zu einem „Brotkrümel“, der oft entfernt werden kann, um die Suchergebnisse zu verfeinern.

Für den Rest dieses Kapitels konzentrieren wir uns auf den wichtigsten und universellsten Typ: die standortbasierte Breadcrumb-Navigation.

#### Die semantisch korrekte Umsetzung in HTML

Wie so oft in HTML gibt es mehrere Wege, eine Breadcrumb-Navigation zu erstellen. Aber nur einer davon ist semantisch korrekt und damit optimal für Suchmaschinen und Barrierefreiheit.

Eine Breadcrumb-Navigation ist, im Kern, eine geordnete Liste von Links, die einen sequenziellen Pfad darstellt. Daher ist die beste Struktur eine geordnete Liste (`<ol>`) innerhalb eines `<nav>`-Elements.

Schauen wir uns ein vollständiges, semantisch korrektes Beispiel an:

```html
<nav aria-label="Brotkrümelnavigation">
  <ol>
    <li><a href="/">Startseite</a></li>
    <li><a href="/herrenbekleidung/">Herrenbekleidung</a></li>
    <li><a href="/herrenbekleidung/hemden/">Hemden</a></li>
    <li aria-current="page">Leinenhemden</li>
  </ol>
</nav>
```

Lass uns diese Struktur im Detail analysieren:

*   **`<nav>`-Element:** Der gesamte Breadcrumb-Pfad wird von einem `<nav>`-Element umschlossen. Das signalisiert Browsern und assistiven Technologien (wie Screenreadern), dass es sich hier um einen Navigationsblock handelt.
*   **`aria-label="Brotkrümelnavigation"`:** Dieses ARIA-Attribut gibt dem `<nav>`-Block einen zugänglichen Namen. Ein Screenreader würde dann etwa ansagen: „Navigation: Brotkrümelnavigation“. Das hilft Nutzern mit Sehbehinderungen, den Zweck dieses Elements sofort zu verstehen.
*   **`<ol>` (Ordered List):** Wir verwenden eine geordnete Liste, weil die Reihenfolge der Elemente entscheidend ist. Es ist ein klar definierter Pfad von einem allgemeinen zu einem spezifischen Punkt. Eine ungeordnete Liste (`<ul>`) wäre hier semantisch falsch.
*   **`<li>` (List Item):** Jeder Schritt im Pfad ist ein eigenes Listenelement.
*   **`<a>` (Anchor-Tag):** Alle übergeordneten Ebenen sind Links, die den Nutzer zu der entsprechenden Seite führen.
*   **Die aktuelle Seite:** Das letzte Element in der Liste repräsentiert die Seite, auf der du dich gerade befindest. Wichtig: **Dieses Element sollte kein Link sein.** Es wäre sinnlos, auf die Seite zu verlinken, auf der man bereits ist. Stattdessen steht hier reiner Text.
*   **`aria-current="page"`:** Dieses Attribut am letzten `<li>`-Element ist ein weiterer wichtiger Baustein für die Barrierefreiheit. Es teilt Screenreadern explizit mit, dass dies der aktuelle Punkt in der Navigation ist.

#### Das Styling mit CSS: Trennzeichen richtig setzen

Früher wurden die Trennzeichen (wie `>` oder `/`) oft direkt in den HTML-Code geschrieben, etwa so:

```html
<!-- Alte, schlechte Methode. Nicht nachmachen! -->
<a href="/">Startseite</a> &gt;
<a href="/herrenbekleidung/">Herrenbekleidung</a> &gt;
<span>Leinenhemden</span>
```

Das ist aus mehreren Gründen problematisch. Erstens lesen Screenreader diese Zeichen vor („größer als“), was die Navigation unnötig „geschwätzig“ macht. Zweitens sind diese Trennzeichen schwer zu stylen und unflexibel.

Die moderne und korrekte Methode ist, die Trennzeichen ausschließlich mit CSS über Pseudo-Elemente zu erzeugen. Das hält deinen HTML-Code sauber und semantisch rein.

Hier ist ein einfaches CSS-Beispiel, das unser HTML von oben stilisiert:

```css
/* Grundlegende Gestaltung für den Navigationscontainer */
nav[aria-label="Brotkrümelnavigation"] {
  font-family: sans-serif;
  font-size: 0.9em;
  padding: 10px 0;
}

/* Die geordnete Liste horizontal anordnen */
nav[aria-label="Brotkrümelnavigation"] ol {
  list-style: none; /* Entfernt die Listennummerierung */
  padding: 0;
  margin: 0;
  display: flex; /* Richtet die Elemente nebeneinander aus */
  flex-wrap: wrap; /* Erlaubt Umbruch bei Platzmangel */
  gap: 0.5em; /* Abstand zwischen den Elementen */
}

/* Das Trennzeichen per CSS einfügen */
nav[aria-label="Brotkrümelnavigation"] li:not(:first-child)::before {
  content: '>';
  margin-right: 0.5em;
  color: #555;
}

/* Styling für die Links */
nav[aria-label="Brotkrümelnavigation"] a {
  color: #007bff;
  text-decoration: none;
}

nav[aria-label="Brotkrümelnavigation"] a:hover {
  text-decoration: underline;
}

/* Styling für die aktuelle Seite (kein Link) */
nav[aria-label="Brotkrümelnavigation"] li[aria-current="page"] {
  color: #333;
  font-weight: bold;
}
```

Die Magie passiert in dieser CSS-Regel: `li:not(:first-child)::before`.

*   **`li:not(:first-child)`:** Dieser Selektor wählt alle Listenelemente aus, *außer dem ersten*. Wir wollen ja kein Trennzeichen vor dem Startpunkt haben.
*   **`::before`:** Dieses Pseudo-Element erzeugt ein künstliches Element *innerhalb* des `<li>`, aber *vor* seinem eigentlichen Inhalt.
*   **`content: '>';`:** Hier definieren wir, was in diesem künstlichen Element stehen soll – in unserem Fall das „größer als“-Zeichen. Du könntest hier auch andere Zeichen wie `/`, `»` oder sogar SVG-Icons verwenden.
*   **`margin-right`:** Sorgt für etwas Abstand zwischen dem Trennzeichen und dem nachfolgenden Linktext.

Durch diesen Ansatz ist das Trennzeichen rein dekorativ. Es wird von Screenreadern ignoriert, aber visuell für alle Nutzer dargestellt.

#### Breadcrumbs und Suchmaschinenoptimierung (SEO)

Breadcrumbs sind nicht nur für deine Nutzer ein Segen, sondern auch für Suchmaschinen. Google und andere Crawler nutzen sie, um die Struktur deiner Website besser zu verstehen und die Beziehungen zwischen den Seiten zu erkennen.

Noch besser: Wenn du deine Breadcrumbs mit strukturierten Daten (Structured Data) nach dem Schema.org-Vokabular auszeichnest, kann Google diese Information nutzen, um deine Suchergebnisse aufzuwerten. Statt einer kryptischen URL zeigt Google dann den klickbaren Breadcrumb-Pfad direkt in den Suchergebnissen an.

**Standard-Suchergebnis:**
`https://beispielshop.de/kat/hb/p/1234-leinenhemd-blau.html`

**Suchergebnis mit Breadcrumb-Daten:**
`https://beispielshop.de > Herrenbekleidung > Hemden`

Das sieht nicht nur aufgeräumter aus, sondern gibt dem Suchenden sofort Kontext und steigert die Wahrscheinlichkeit, dass dein Link geklickt wird.

Die gängigste Methode zur Implementierung ist JSON-LD, ein Skript, das du einfach in den `<head>` oder `<body>` deines HTML-Dokuments einfügst.

Ein JSON-LD-Beispiel für unsere Leinenhemden-Seite könnte so aussehen:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [{
    "@type": "ListItem",
    "position": 1,
    "name": "Startseite",
    "item": "https://beispielshop.de/"
  },{
    "@type": "ListItem",
    "position": 2,
    "name": "Herrenbekleidung",
    "item": "https://beispielshop.de/herrenbekleidung/"
  },{
    "@type": "ListItem",
    "position": 3,
    "name": "Hemden",
    "item": "https://beispielshop.de/herrenbekleidung/hemden/"
  },{
    "@type": "ListItem",
    "position": 4,
    "name": "Leinenhemden"
  }]
}
</script>
```

Jedes `ListItem` repräsentiert einen Brotkrümel mit seiner Position im Pfad, seinem Namen und (außer beim letzten Element) seiner URL (`item`).

Obwohl sie klein und unauffällig sind, spielen Breadcrumbs eine entscheidende Rolle für eine intuitive und nutzerfreundliche Website-Struktur. Sie sind die leisen Helden der Navigation, die Nutzern Orientierung geben, die Absprungrate senken und sogar deine Sichtbarkeit in Suchmaschinen verbessern können. Ihre korrekte semantische Implementierung ist ein klares Zeichen für professionelle und durchdachte Webentwicklung.
