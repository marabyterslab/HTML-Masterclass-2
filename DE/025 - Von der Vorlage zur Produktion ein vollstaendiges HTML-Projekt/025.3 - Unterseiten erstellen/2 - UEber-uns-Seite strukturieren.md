# Über-uns-Seite strukturieren

### Die "Über uns"-Seite strukturieren

Eine "Über uns"-Seite ist oft das Herzstück einer Website. Sie ist mehr als nur eine formale Notwendigkeit; sie ist der Ort, an dem du eine menschliche Verbindung zu deinen Besuchern aufbaust. Hier erzählst du deine Geschichte, stellst die Menschen hinter dem Projekt vor und baust das Vertrauen auf, das für jede erfolgreiche Online-Präsenz unerlässlich ist. Deine Aufgabe als Webentwickler ist es, dieser Geschichte eine klare, logische und semantisch korrekte Struktur zu geben. Eine gut strukturierte HTML-Seite ist nicht nur für Suchmaschinen und Screenreader besser verständlich, sondern bildet auch eine stabile Grundlage für jedes Design, das du mit CSS darauf anwenden wirst.

Lass uns gemeinsam eine typische "Über uns"-Seite in ihre logischen Bestandteile zerlegen und sie mit passendem HTML-Markup versehen.

#### Das Grundgerüst: Semantik ist der Schlüssel

Bevor wir in die einzelnen Sektionen eintauchen, ist es wichtig, das Fundament richtig zu legen. Jede Unterseite deines Projekts sollte in die grundlegende HTML-Struktur eingebettet sein, mit einem `<header>`, einem `<footer>` und dem Hauptinhalt, der von einem `<main>`-Element umschlossen wird. Der gesamte Inhalt, den wir hier besprechen, gehört in dieses `<main>`-Element. Innerhalb von `<main>` unterteilen wir die Seite in logische Abschnitte mit dem `<section>`-Tag. Dieses Vorgehen hilft assistiven Technologien dabei, die Seitenstruktur zu verstehen und ermöglicht es den Nutzern, schnell zwischen den Abschnitten zu navigieren.

#### Der Einstieg: Die Helden-Sektion

Der erste Eindruck zählt. Die sogenannte "Hero Section" ist der Bereich, den Besucher sofort sehen, ohne zu scrollen. Ihr Ziel ist es, die Aufmerksamkeit zu fesseln und die zentrale Botschaft der Seite zu vermitteln. Hier steht in der Regel eine kraftvolle Überschrift und ein kurzer, einleitender Text, der den Ton für den Rest der Seite angibt.

Strukturell ist das recht unkompliziert. Wir verwenden eine `<section>`, um diesen Bereich klar vom Rest abzugrenzen. Die Hauptüberschrift der Seite, "Über uns", bekommt das `<h1>`-Tag – das wichtigste Überschriftenelement auf jeder Seite. Der einleitende Text wird in einen einfachen `<p>`-Tag gepackt.

```html
<main>
  <section class="hero">
    <h1>Wer wir sind und was uns antreibt</h1>
    <p>
      Wir sind ein Team aus kreativen Denkern, Entwicklern und Strategen, 
      die eine gemeinsame Leidenschaft teilen: digitale Erlebnisse zu schaffen,
      die begeistern und einen echten Mehrwert bieten.
    </p>
  </section>
  
  <!-- Weitere Sektionen folgen hier -->
</main>
```

#### Das Herzstück: Unsere Geschichte und Mission

Nach dem einleitenden Paukenschlag folgt der erzählerische Teil. Hier hast du die Gelegenheit, die Entstehungsgeschichte deines Projekts, deine Mission oder deine Vision zu teilen. Dieser Abschnitt ist textlastiger und lebt von einer guten Gliederung durch Zwischenüberschriften.

Auch hierfür eignet sich ein `<section>`-Element hervorragend. Innerhalb dieser Sektion kannst du mit `<h2>`-Überschriften arbeiten, um die verschiedenen Aspekte deiner Geschichte zu unterteilen, zum Beispiel "Unsere Geschichte" und "Unsere Mission". Fließtext gehört wie immer in `<p>`-Tags. Wenn du ein besonders prägnantes Zitat oder ein Leitmotiv hervorheben möchtest, ist das `<blockquote>`-Element die semantisch korrekte Wahl.

```html
<section class="story-mission">
  <h2>Unsere Geschichte</h2>
  <p>
    Alles begann 2018 in einer kleinen Garage, angetrieben von einer einfachen Idee: 
    Technologie sollte für jeden zugänglich und einfach zu bedienen sein. Aus dieser 
    Vision wuchs ein kleines Team, das sich der Entwicklung intuitiver Software 
    verschrieben hat.
  </p>
  <p>
    Über die Jahre sind wir gewachsen, aber unsere Gründungsprinzipien sind die 
    gleichen geblieben. Wir glauben fest daran, dass gute Software das Leben 
    der Menschen verbessern kann.
  </p>

  <h2>Unsere Mission</h2>
  <blockquote>
    <p>
      Wir wollen die Brücke zwischen komplexer Technologie und menschlichen 
      Bedürfnissen schlagen, um Werkzeuge zu schaffen, die nicht nur funktionieren, 
      sondern Freude bereiten.
    </p>
  </blockquote>
</section>
```

#### Gesichter zeigen: Das Team vorstellen

Menschen verbinden sich mit Menschen, nicht mit anonymen Marken. Die Vorstellung des Teams ist daher ein entscheidender Baustein für den Aufbau von Vertrauen. Normalerweise wird das Team in einer Art Raster oder als eine Liste von Profilen dargestellt.

Für die gesamte Team-Sektion nehmen wir wieder ein `<section>`-Element. Aber wie strukturieren wir die einzelnen Teammitglieder? Jedes Mitglied ist eine in sich geschlossene Einheit mit Bild, Name, Position und einer kurzen Beschreibung. Dafür ist das `<article>`-Element ideal. Ein `<article>` repräsentiert eine eigenständige, potenziell wiederverwendbare Komponente – genau das, was ein Teammitglied-Profil ist.

Innerhalb des `<article>`-Elements gibt es mehrere bewährte Vorgehensweisen. Eine sehr saubere Methode ist die Verwendung eines `<figure>`-Elements für das Bild, gefolgt von den textlichen Informationen.

- **`<img>`**: Das Bild des Teammitglieds. Vergiss niemals das `alt`-Attribut! Es ist essenziell für die Barrierefreiheit und beschreibt das Bild für Nutzer, die es nicht sehen können.
- **`<h3>` oder `<h4>`**: Der Name der Person. Da "Das Team" unsere `<h2>`-Überschrift ist, sind `<h3>` oder `<h4>` hier hierarchisch passend.
- **`<p>`**: Ein Absatz für die Berufsbezeichnung und ein weiterer für die kurze Biografie. Du kannst Klassen verwenden, um diese später mit CSS gezielt zu gestalten (z. B. `<p class="role">`).

```html
<section class="team">
  <h2>Unser Team</h2>
  <div class="team-grid">
    <article class="team-member">
      <figure>
        <img src="bilder/max-mustermann.jpg" alt="Porträtfoto von Max Mustermann">
      </figure>
      <h3>Max Mustermann</h3>
      <p class="role">Gründer & CEO</p>
      <p>
        Max ist der visionäre Kopf hinter allem. Wenn er nicht gerade neue Ideen 
        entwickelt, findet man ihn beim Wandern in den Bergen.
      </p>
    </article>

    <article class="team-member">
      <figure>
        <img src="bilder/erika-musterfrau.jpg" alt="Porträtfoto von Erika Musterfrau">
      </figure>
      <h3>Erika Musterfrau</h3>
      <p class="role">Lead-Entwicklerin</p>
      <p>
        Erika sorgt dafür, dass aus Ideen funktionierender Code wird. Ihre 
        Leidenschaft für saubere und effiziente Lösungen treibt unser Team an.
      </p>
    </article>
    
    <!-- Weitere Teammitglieder hier -->
  </div>
</section>
```
Hier habe ich die `<article>`-Elemente zusätzlich in ein `<div class="team-grid">` gepackt. Dieses `<div>` hat keine semantische Bedeutung, dient aber als praktischer Container, um mit CSS später ein Grid- oder Flexbox-Layout zu erstellen.

#### Wofür wir stehen: Werte und Prinzipien

Viele "Über uns"-Seiten enthalten einen Abschnitt über die Kernwerte oder Arbeitsprinzipien des Unternehmens. Diese werden oft als eine Liste von Begriffen mit dazugehörigen Erklärungen dargestellt.

Für eine solche "Begriff-Erklärung"-Struktur bietet HTML ein perfektes, aber oft übersehenes Werkzeug: die Definitionsliste (`<dl>`). Sie besteht aus drei Elementen:
- **`<dl>` (Description List)**: Das umschließende Element für die gesamte Liste.
- **`<dt>` (Description Term)**: Der Begriff, der definiert wird (z. B. der Wert "Innovation").
- **`<dd>` (Description Details)**: Die Beschreibung oder Erklärung des Begriffs.

Diese Struktur ist semantisch weitaus aussagekräftiger als eine einfache ungeordnete Liste (`<ul>`), da sie die direkte Beziehung zwischen einem Begriff und seiner Definition abbildet.

```html
<section class="values">
  <h2>Unsere Werte</h2>
  <dl>
    <dt>Innovation</dt>
    <dd>
      Wir hinterfragen den Status quo und suchen ständig nach besseren Wegen, 
      Probleme zu lösen. Stillstand ist für uns ein Fremdwort.
    </dd>

    <dt>Transparenz</dt>
    <dd>
      Wir kommunizieren offen und ehrlich – sowohl intern im Team als auch 
      extern mit unseren Kunden und Partnern.
    </dd>

    <dt>Qualität</dt>
    <dd>
      Was wir tun, tun wir richtig. Wir legen Wert auf Details und liefern 
      Produkte, auf die wir stolz sein können.
    </dd>
  </dl>
</section>
```

#### Der rote Faden: Ein vollständiges Beispiel

Nachdem wir die einzelnen Bausteine betrachtet haben, fügen wir sie nun zu einer vollständigen, gut strukturierten HTML-Seite zusammen. Dieses Beispiel zeigt dir, wie alle Teile ineinandergreifen und eine logische, lesbare und wartbare Struktur bilden.

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF--8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Über uns - Unser Unternehmen</title>
  <!-- Verlinkung zu CSS etc. würde hier stehen -->
</head>
<body>

  <!-- Annahme: Ein globaler Header ist auf jeder Seite vorhanden -->
  <header>
    <!-- Navigation etc. -->
  </header>

  <main>
    <!-- 1. HERO-SEKTION -->
    <section class="hero">
      <h1>Wer wir sind und was uns antreibt</h1>
      <p>
        Wir sind ein Team aus kreativen Denkern, Entwicklern und Strategen, 
        die eine gemeinsame Leidenschaft teilen: digitale Erlebnisse zu schaffen,
        die begeistern und einen echten Mehrwert bieten.
      </p>
    </section>

    <!-- 2. GESCHICHTE UND MISSION -->
    <section class="story-mission">
      <h2>Unsere Geschichte</h2>
      <p>
        Alles begann 2018 in einer kleinen Garage, angetrieben von einer einfachen Idee: 
        Technologie sollte für jeden zugänglich und einfach zu bedienen sein. Aus dieser 
        Vision wuchs ein kleines Team, das sich der Entwicklung intuitiver Software 
        verschrieben hat.
      </p>
      
      <h2>Unsere Mission</h2>
      <blockquote>
        <p>
          Wir wollen die Brücke zwischen komplexer Technologie und menschlichen 
          Bedürfnissen schlagen, um Werkzeuge zu schaffen, die nicht nur funktionieren, 
          sondern Freude bereiten.
        </p>
      </blockquote>
    </section>

    <!-- 3. TEAM-SEKTION -->
    <section class="team">
      <h2>Unser Team</h2>
      <div class="team-grid">
        <article class="team-member">
          <figure>
            <img src="bilder/max-mustermann.jpg" alt="Porträtfoto von Max Mustermann">
          </figure>
          <h3>Max Mustermann</h3>
          <p class="role">Gründer & CEO</p>
          <p>
            Max ist der visionäre Kopf hinter allem. Wenn er nicht gerade neue Ideen 
            entwickelt, findet man ihn beim Wandern in den Bergen.
          </p>
        </article>

        <article class="team-member">
          <figure>
            <img src="bilder/erika-musterfrau.jpg" alt="Porträtfoto von Erika Musterfrau">
          </figure>
          <h3>Erika Musterfrau</h3>
          <p class="role">Lead-Entwicklerin</p>
          <p>
            Erika sorgt dafür, dass aus Ideen funktionierender Code wird. Ihre 
            Leidenschaft für saubere und effiziente Lösungen treibt unser Team an.
          </p>
        </article>
      </div>
    </section>
    
    <!-- 4. WERTE-SEKTION -->
    <section class="values">
      <h2>Unsere Werte</h2>
      <dl>
        <dt>Innovation</dt>
        <dd>
          Wir hinterfragen den Status quo und suchen ständig nach besseren Wegen, 
          Probleme zu lösen. Stillstand ist für uns ein Fremdwort.
        </dd>

        <dt>Transparenz</dt>
        <dd>
          Wir kommunizieren offen und ehrlich – sowohl intern im Team als auch 
          extern mit unseren Kunden und Partnern.
        </dd>
      </dl>
    </section>

  </main>

  <!-- Annahme: Ein globaler Footer ist auf jeder Seite vorhanden -->
  <footer>
    <!-- Copyright, Links etc. -->
  </footer>

</body>
</html>
```

Mit dieser semantischen Gliederung hast du eine "Über uns"-Seite geschaffen, deren Struktur nicht nur für den Browser, sondern auch für Mensch und Maschine verständlich ist. Du hast der Geschichte einen Rahmen gegeben, der sie klar und zugänglich macht – die perfekte Basis für das anschließende visuelle Design mit CSS.
