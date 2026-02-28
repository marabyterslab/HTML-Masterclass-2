# Titel-Attribut und Tooltips

### Das `title`-Attribut: Mehr als nur ein Tooltip

Wenn du einen Link erstellst, ist dein primäres Ziel klar: Du möchtest dem Nutzer ermöglichen, zu einer anderen Ressource zu navigieren. Der Anker-Tag `<a>` ist dafür das zentrale Werkzeug. Doch manchmal reicht der reine Linktext nicht aus, um dem Nutzer alle notwendigen Informationen zu geben, ohne den Lesefluss zu stören. Hier kommt das `title`-Attribut ins Spiel.

Auf den ersten Blick ist seine Funktion schnell erklärt: Fügst du einem HTML-Element ein `title`-Attribut hinzu, erscheint ein kleiner, vom Browser gestalteter Kasten mit dem Attribut-Text, sobald ein Nutzer mit der Maus über das Element fährt. Dieser Kasten wird gemeinhin als "Tooltip" bezeichnet.

Schauen wir uns ein einfaches Beispiel an:

```html
<a href="httpsg://www.w3.org/" title="Besuche die offizielle Website des World Wide Web Consortiums">
  Mehr über das W3C erfahren
</a>
```

Fährst du in einem Desktop-Browser mit dem Mauszeiger über diesen Link, erscheint nach einer kurzen Verzögerung ein kleines Fenster mit dem Text: "Besuche die offizielle Website des World Wide Web Consortiums". Das ist praktisch. Es liefert zusätzlichen Kontext, ohne den sichtbaren Linktext unnötig aufzublähen.

#### Wofür du das `title`-Attribut verwenden solltest (und wofür nicht)

Die wichtigste Regel für die Verwendung des `title`-Attributs lautet: **Verstecke niemals kritische Informationen darin.** Der Grund dafür ist einfach: Nicht jeder Nutzer kann oder wird diesen Tooltip sehen.

1.  **Touch-Geräte:** Auf Smartphones und Tablets gibt es keinen Mauszeiger und somit kein "Hover"-Ereignis. Nutzer, die deine Seite auf diesen Geräten besuchen, werden den Inhalt des `title`-Attributs in den allermeisten Fällen nie zu Gesicht bekommen.
2.  **Tastaturnavigation:** Nutzer, die aus verschiedenen Gründen (z. B. motorische Einschränkungen) ausschließlich mit der Tastatur navigieren, können ebenfalls nicht über ein Element "schweben". Sie springen mit der Tab-Taste von einem interaktiven Element zum nächsten. Auch ihnen bleibt der Tooltip verborgen.
3.  **Screenreader:** Obwohl einige Screenreader das `title`-Attribut auslesen können, ist dies oft nicht die Standardeinstellung oder erfordert eine spezielle Tastenkombination. Sich darauf zu verlassen, dass Screenreader-Nutzer diese Information erhalten, ist ein Glücksspiel und widerspricht den Prinzipien der Barrierefreiheit.

Das `title`-Attribut eignet sich daher ausschließlich für **ergänzende, nicht-essenzielle Informationen**. Es ist eine "Nice-to-have"-Erweiterung, kein Ersatz für klaren und verständlichen Inhalt.

Gute Anwendungsfälle für das `title`-Attribut bei Links sind:

*   **Zusätzliche Information zum Linkziel:** Wie im obigen Beispiel kann der Titel erläutern, was den Nutzer auf der Zielseite erwartet.
*   **Warnungen oder Hinweise:** Du könntest darauf hinweisen, dass der Link eine große Datei zum Download anbietet oder zu einer externen Website führt.
    ```html
    <a href="/downloads/jahresbericht_2023.pdf" title="PDF, ca. 5 MB">
      Jahresbericht 2023 herunterladen
    </a>
    ```
*   **Ausschreiben von Abkürzungen:** Obwohl das `<abbr>`-Element hierfür semantisch korrekter ist, wird das `title`-Attribut oft verwendet, um Akronyme oder Abkürzungen im Fließtext oder in Links zu erläutern.
    ```html
    <p>
      Die Spezifikationen werden vom 
      <a href="https://www.w3.org/" title="World Wide Web Consortium">W3C</a> 
      definiert.
    </p>
    ```

Ein klassischer Fehler ist die Duplizierung des Linktextes im `title`-Attribut. Das ist nicht nur nutzlos, sondern kann für Nutzer von Screenreadern sogar störend sein, wenn die Software denselben Text zweimal hintereinander vorliest.

```html
<!-- SCHLECHTES BEISPIEL: Redundant und nicht hilfreich -->
<a href="/kontakt" title="Kontakt">Kontakt</a>

<!-- GUTES BEISPIEL: Bietet echten Mehrwert -->
<a href="/kontakt" title="Hier findest du unsere Adresse und ein Kontaktformular">Kontakt</a>
```

#### Abgrenzung zum `alt`-Attribut bei Bildern

Ein Bereich, in dem es oft zu Verwirrung kommt, ist die Verwendung des `title`-Attributs bei Bildern (`<img>`). Viele verwechseln es mit dem `alt`-Attribut. Die beiden haben jedoch völlig unterschiedliche Aufgaben.

*   Das **`alt`**-Attribut (Alternativtext) ist für die **Barrierefreiheit essenziell**. Sein Inhalt wird angezeigt, wenn das Bild nicht geladen werden kann. Viel wichtiger noch: Er wird von Screenreadern vorgelesen, um blinden und sehbehinderten Nutzern zu beschreiben, was auf dem Bild zu sehen ist. Der `alt`-Text ist ein **Ersatz** für das Bild.
*   Das **`title`**-Attribut ist, wie bei Links, eine **Ergänzung**. Es liefert zusätzliche, nicht-kritische Informationen zum Bild und erzeugt den bekannten Tooltip beim Überfahren mit der Maus.

Stell dir ein Foto von einer Katze vor, die auf einem sonnigen Fensterbrett schläft. Eine korrekte Verwendung beider Attribute könnte so aussehen:

```html
<img 
  src="bilder/katze-felix.jpg"
  alt="Eine schwarz-weiße Katze schläft zusammengerollt auf einem Fensterbrett, Sonnenstrahlen fallen auf ihr Fell."
  title="Unser Kater Felix an seinem Lieblingsplatz."
>
```

Der `alt`-Text beschreibt objektiv die Szene für jemanden, der sie nicht sehen kann. Der `title`-Text gibt eine persönliche, kontextbezogene Zusatzinformation, deren Fehlen das Verständnis des Bildes nicht beeinträchtigt.

#### Ein globales Attribut für fast alle Fälle

Das `title`-Attribut ist nicht auf `<a>`- und `<img>`-Tags beschränkt. Es handelt sich um ein **globales Attribut**, was bedeutet, dass du es auf fast jedem HTML-Element verwenden kannst. Du kannst es einem Paragrafen, einer Überschrift, einem `<div>`-Container oder einem Formularelement hinzufügen.

Beispielsweise könntest du es verwenden, um eine komplexere Anforderung an ein Eingabefeld zu erläutern, ohne den Platz für ein sichtbares Label zu verwenden:

```html
<label for="passwort">Passwort:</label>
<input 
  type="password" 
  id="passwort" 
  name="passwort"
  title="Muss mindestens 8 Zeichen, einen Großbuchstaben und eine Zahl enthalten."
>
```

Auch hier gilt die Regel: Die Information sollte hilfreich, aber nicht zwingend erforderlich sein, da sie nicht allen Nutzern zur Verfügung steht.

#### Moderne Alternativen: Gestaltbare Tooltips mit CSS

Ein großer Nachteil des nativen Browser-Tooltips ist, dass du sein Aussehen nicht kontrollieren kannst. Jeder Browser stellt ihn anders dar – meist in einem schlichten, systemeigenen Stil (z.B. gelber Kasten mit schwarzer Schrift). Er kann auch nicht formatiert werden und bricht bei langen Texten oft unschön um.

Für Situationen, in denen du mehr Kontrolle über das Design und die Zugänglichkeit eines Tooltips benötigst, greifen Entwickler heute oft auf benutzerdefinierte Lösungen mit CSS und manchmal auch JavaScript zurück. Eine beliebte und einfache Methode nutzt `data-*`-Attribute in Kombination mit CSS-Pseudo-Elementen wie `::before` und `::after`.

So könntest du einen stilisierten Tooltip erstellen, der auch für Tastaturnutzer zugänglich gemacht werden kann:

```html
<!DOCTYPE html>
<html lang="de">
<head>
<style>
  /* Grundlegende Stile für den Link */
  .custom-tooltip {
    position: relative; /* Wichtig für die Positionierung des Tooltips */
    text-decoration: underline dotted;
    cursor: help;
  }

  /* Der eigentliche Tooltip, standardmäßig unsichtbar */
  .custom-tooltip::after {
    content: attr(data-tooltip); /* Holt den Text aus dem data-tooltip Attribut */
    position: absolute;
    bottom: 125%; /* Positioniert den Tooltip über dem Element */
    left: 50%;
    transform: translateX(-50%);
    
    background-color: #333;
    color: #fff;
    padding: 8px 12px;
    border-radius: 4px;
    white-space: nowrap; /* Verhindert Zeilenumbrüche */
    
    opacity: 0; /* Unsichtbar machen */
    visibility: hidden;
    transition: opacity 0.2s, visibility 0.2s;
  }

  /* Tooltip sichtbar machen, wenn über das Element gehovert oder es fokussiert wird */
  .custom-tooltip:hover::after,
  .custom-tooltip:focus::after {
    opacity: 1;
    visibility: visible;
  }
</style>
</head>
<body>

  <p>
    HTML steht für 
    <span 
      class="custom-tooltip" 
      tabindex="0" 
      data-tooltip="Hypertext Markup Language"
    >HTML</span>.
  </p>

</body>
</html>
```

In diesem Beispiel wird kein `title`-Attribut verwendet. Stattdessen speichern wir den Tooltip-Text in einem `data-tooltip`-Attribut. Das CSS erzeugt dann ein Pseudo-Element (`::after`), das diesen Text anzeigt, wenn der Nutzer mit der Maus über das `<span>` fährt (`:hover`) oder es mit der Tastatur ansteuert (`:focus`). Durch `tabindex="0"` machen wir das `<span>`, das normalerweise nicht fokussierbar wäre, für Tastaturnutzer erreichbar.

Diese Methode bietet volle gestalterische Freiheit und eine bessere Kontrolle über die Zugänglichkeit. Sie zeigt, dass das `title`-Attribut zwar ein nützliches und einfaches Werkzeug für grundlegende Tooltips ist, die moderne Webentwicklung aber oft flexiblere Lösungen erfordert.

Dennoch bleibt das `title`-Attribut ein fester Bestandteil von HTML. Wenn du es bewusst und korrekt einsetzt – als eine Quelle für ergänzende, nicht-kritische Informationen – ist es ein wertvolles Werkzeug in deinem Repertoire.
