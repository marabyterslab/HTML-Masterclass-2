# Besuchte vs. unbesuchte Links

### besuchte vs. unbesuchte Links: Ein visueller Wegweiser für den Nutzer

Stell dir vor, du recherchierst ein komplexes Thema online. Du klickst dich durch Dutzende von Links, springst von einer Quelle zur nächsten und versuchst, den Überblick zu behalten. Nach einer Weile fragst du dich: "War ich auf dieser Seite schon? Habe ich diese Information bereits gelesen?" Genau hier kommt eine der grundlegendsten und gleichzeitig wichtigsten Funktionen der Web-Usability ins Spiel: die visuelle Unterscheidung zwischen besuchten und unbesuchten Links.

Dieses kleine Detail ist weit mehr als nur eine kosmetische Anpassung. Es ist ein fundamentaler Orientierungspunkt für jeden, der im Web navigiert. Es funktioniert wie ein visuelles Gedächtnis, das dir hilft, bereits erkundete Pfade zu erkennen und Doppelarbeit zu vermeiden. Für den Nutzer ist es ein unschätzbarer Dienst, der die kognitive Last reduziert und die Navigation effizienter und angenehmer gestaltet. Das Web wäre ohne diese Funktion ein deutlich chaotischerer Ort.

Die Magie dahinter geschieht nicht durch HTML allein. Dein Browser führt im Hintergrund eine Art Logbuch – deine Browser-Chronik. Jedes Mal, wenn du eine Seite besuchst, wird die URL in dieser Chronik vermerkt. Wenn du dann auf eine Webseite triffst, die einen Link zu dieser URL enthält, weiß der Browser: "Aha, hier war der Nutzer schon." Mit diesem Wissen können wir als Entwickler mithilfe von CSS eingreifen und dem Link ein anderes Aussehen verleihen.

#### Die CSS-Pseudo-Klassen `:link` und `:visited`

Um den Status eines Links zu gestalten, verwenden wir in CSS sogenannte Pseudo-Klassen. Das sind Schlüsselwörter, die an einen Selektor angehängt werden, um ein Element in einem bestimmten Zustand zu stylen. Für unsere Zwecke sind zwei Pseudo-Klassen entscheidend: `:link` und `:visited`.

**Die Pseudo-Klasse `:link`**

Die Pseudo-Klasse `:link` zielt auf alle `<a>`-Elemente ab, die ein `href`-Attribut besitzen, aber deren Zieladresse vom Nutzer **noch nicht** besucht wurde. Sie repräsentiert den Standardzustand eines Links, das "unberührte" Versprechen auf neue Inhalte.

```css
/* Stil für alle unbesuchten Links */
a:link {
  color: blue;
  text-decoration: underline;
}
```

In diesem Beispiel würden alle Links, die du noch nicht angeklickt hast, in der klassischen blauen Farbe mit einer Unterstreichung dargestellt werden.

**Die Pseudo-Klasse `:visited`**

Das Gegenstück dazu ist `:visited`. Diese Pseudo-Klasse wählt alle `<a>`-Elemente aus, deren `href`-Ziel sich bereits in deiner Browser-Chronik befindet. Sie ist das visuelle Signal dafür, dass du diesen Weg bereits beschritten hast.

```css
/* Stil für alle bereits besuchten Links */
a:visited {
  color: purple;
}
```

Traditionell wird für besuchte Links eine lila oder violette Farbe verwendet – eine Konvention, die sich seit den Anfängen des Webs etabliert hat und von den meisten Nutzern intuitiv verstanden wird.

Wenn wir beide Stile kombinieren, schaffen wir eine klare und sofort verständliche Navigationshilfe für unsere Nutzer.

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Link-Status Beispiel</title>
    <style>
        /* Grundlegender Link-Stil */
        a {
            font-family: sans-serif;
            font-size: 1.2rem;
            margin: 0 10px;
        }

        /* Stil für unbesuchte Links */
        a:link {
            color: #007BFF; /* Ein modernes, klares Blau */
            text-decoration: none; /* Wir entfernen die Standard-Unterstreichung */
            border-bottom: 2px solid #007BFF; /* ...und ersetzen sie durch einen Rahmen */
        }

        /* Stil für besuchte Links */
        a:visited {
            color: #6f42c1; /* Ein sattes Lila */
            border-bottom-color: #6f42c1; /* Der Rahmen passt sich farblich an */
        }
    </style>
</head>
<body>

    <h1>Recherche-Quellen</h1>
    <nav>
        <a href="https://de.wikipedia.org/wiki/HTML">HTML auf Wikipedia</a>
        <a href="https://developer.mozilla.org/de/docs/Web/HTML">MDN Web Docs: HTML</a>
        <a href="https://eine-zufaellige-unbesuchte-seite-123.org">Ein fiktiver, unbesuchter Link</a>
    </nav>

</body>
</html>
```

Wenn du diesen Code in deinem Browser öffnest, wirst du wahrscheinlich feststellen, dass die Links zu Wikipedia und MDN lila sind (da du sie als Webentwickler sicher schon einmal besucht hast), während der fiktive Link blau erscheint.

#### Eine wichtige Einschränkung: Der Schutz der Privatsphäre

Früher war es möglich, mit `:visited` eine Vielzahl von CSS-Eigenschaften zu ändern. Man hätte beispielsweise die Schriftgröße ändern, ein Hintergrundbild hinzufügen oder die Transparenz anpassen können. Doch findige Entwickler erkannten schnell ein massives Datenschutzproblem.

Stell dir eine bösartige Webseite vor. Diese Seite könnte eine unsichtbare Liste mit Tausenden von Links zu bekannten Webseiten (z. B. sozialen Netzwerken, Banken, politischen Seiten) enthalten. Mithilfe von JavaScript könnte die Seite dann den berechneten CSS-Stil jedes einzelnen Links überprüfen. Wenn der Stil dem `:visited`-Zustand entsprach (z. B. eine andere Schriftgröße hatte), wusste die Seite, dass du diese URL besucht hattest. Dieser Trick, bekannt als "CSS History Stealing", ermöglichte es Webseiten, heimlich deine Browser-Chronik auszulesen – ein gravierender Eingriff in deine Privatsphäre.

Um dies zu verhindern, haben moderne Browser die Möglichkeiten der `:visited`-Pseudo-Klasse drastisch eingeschränkt. Die Regel ist einfach: **Du darfst nur Eigenschaften ändern, die keine Informationen über die Dimensionen, Position oder den Inhalt des Elements preisgeben.**

In der Praxis bedeutet das, dass du für `:visited` fast ausschließlich Farb-Eigenschaften sicher ändern kannst. Dazu gehören:

*   `color`
*   `background-color`
*   `border-color` (und seine spezifischen Varianten wie `border-top-color`)
*   `outline-color`
*   `column-rule-color`
*   `fill` und `stroke` bei SVG-Grafiken

Alle anderen Eigenschaften, die du in einem `:visited`-Selektor definierst (wie `font-size`, `background-image`, `padding`, `display` etc.), werden vom Browser ignoriert. Stattdessen wird der Wert der `:link`-Regel (oder des generellen `a`-Selektors) verwendet. Selbst bei den erlaubten Farbeigenschaften gibt es eine Einschränkung: Wenn du versuchst, die Farbe mit `rgba()` transparent zu machen, behandelt der Browser sie so, als wäre sie vollständig opak, um zu verhindern, dass über die Transparenz Informationen ausgelesen werden können.

Dieser Kompromiss ist elegant: Er bewahrt die essenzielle Funktion der visuellen Unterscheidung für den Nutzer, während er gleichzeitig seine Privatsphäre schützt.

#### Die richtige Reihenfolge: LVHA

Die Zustände `:link` und `:visited` sind nicht die einzigen, die ein Link annehmen kann. Es gibt auch `:hover` (wenn du mit der Maus darüberfährst) und `:active` (im Moment des Klickens). Um sicherzustellen, dass alle Stile wie erwartet funktionieren, solltest du sie in einer bestimmten Reihenfolge in deinem CSS definieren. Die gebräuchlichste Eselsbrücke dafür ist **LVHA**:

1.  **L**ink
2.  **V**isited
3.  **H**over
4.  **A**ctive

Die Reihenfolge ist aufgrund der Spezifität von CSS-Regeln wichtig. Ein Link kann gleichzeitig "besucht" und "gehovert" sein. Wenn die `:hover`-Regel vor der `:visited`-Regel steht, würde der `:visited`-Stil den `:hover`-Stil überschreiben, und der Hover-Effekt wäre bei besuchten Links nicht sichtbar.

Ein vollständiges und robustes Link-Styling sieht daher oft so aus:

```css
/* 1. Unbesuchter Zustand (Link) */
a:link {
  color: #007BFF;
  text-decoration: underline;
}

/* 2. Besuchter Zustand (Visited) */
a:visited {
  color: #6f42c1;
}

/* 3. Maus-darüber-Zustand (Hover) - gilt für besuchte UND unbesuchte Links */
a:hover {
  color: #d9534f; /* Ein auffälliges Rot */
  text-decoration: none; /* Unterstreichung beim Hovern entfernen */
}

/* 4. Aktiver Klick-Zustand (Active) */
a:active {
  color: #f0ad4e; /* Ein leuchtendes Orange */
}
```

Mit dieser Struktur stellst du sicher, dass jeder Zustand klar definiert ist und die Interaktionen für den Nutzer intuitiv und vorhersehbar sind. Die Unterscheidung zwischen besuchten und unbesuchten Links ist dabei das Fundament, auf dem eine gute und nutzerfreundliche Navigation aufbaut. Es ist ein kleines, aber mächtiges Werkzeug in deinem Arsenal, um das Web für alle ein Stück übersichtlicher zu machen.
