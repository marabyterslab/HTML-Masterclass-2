# Das lang-Attribut und seine Bedeutung

### Das `lang`-Attribut und seine Bedeutung

Stell dir vor, du schreibst ein Dokument. Eine deiner ersten Handlungen wäre wahrscheinlich, oben auf der Seite festzuhalten, in welcher Sprache du schreibst, besonders wenn es in einem internationalen Umfeld gelesen wird. Im Web ist das nicht anders. Das `<html>`-Element, die Wurzel deines gesamten Dokuments, hat genau für diesen Zweck ein fundamentales Attribut: das `lang`-Attribut.

Es ist wie der Reisepass deines HTML-Dokuments. Es deklariert unmissverständlich die primäre Sprache des Inhalts. Auf den ersten Blick mag das wie eine kleine, vielleicht sogar optionale Formalität wirken. Doch in der vernetzten Welt des Internets hat diese eine Zeile Code weitreichende und wichtige Konsequenzen.

Die grundlegende Syntax ist denkbar einfach. Du fügst das `lang`-Attribut direkt in das öffnende `<html>`-Tag ein:

```html
<!DOCTYPE html>
<html lang="de">
  <head>
    <meta charset="UTF-8">
    <title>Meine deutschsprachige Webseite</title>
  </head>
  <body>
    <p>Dies ist ein Absatz in deutscher Sprache.</p>
  </body>
</html>
```

In diesem Beispiel teilt `lang="de"` jedem, der es wissen muss – Browsern, Suchmaschinen, Hilfstechnologien –, mit, dass der Hauptinhalt dieser Seite auf Deutsch verfasst ist.

#### Warum diese Deklaration so entscheidend ist

Die Bedeutung dieses kleinen Attributs entfaltet sich in mehreren Bereichen, die für eine moderne, funktionale und zugängliche Webseite unerlässlich sind.

**1. Zugänglichkeit (Accessibility)**

Einer der wichtigsten, wenn nicht sogar der wichtigste Grund für die Verwendung des `lang`-Attributs ist die Barrierefreiheit. Screenreader, also Programme, die Bildschirminhalte für Menschen mit Sehbehinderungen vorlesen, sind auf diese Information angewiesen, um den Text korrekt auszusprechen.

Die Ausspracheregeln unterscheiden sich von Sprache zu Sprache drastisch. Ein englisches Wort wie "gift" (Geschenk) wird völlig anders ausgesprochen als das deutsche Wort "Gift" (poison). Ohne die Sprachangabe `lang="de"` würde ein Screenreader mit englischer Standardeinstellung versuchen, deutsche Wörter mit englischer Phonetik vorzulesen. Das Ergebnis wäre im besten Fall komisch und im schlimmsten Fall völlig unverständlich.

Durch die korrekte Deklaration stellst du sicher, dass die synthetische Stimme die richtigen Betonungen, den richtigen Satzrhythmus und die korrekte Aussprache verwendet. Für einen Menschen, der auf diese Technologie angewiesen ist, kann dies den Unterschied zwischen einem verständlichen und einem unbrauchbaren Weberlebnis ausmachen.

**2. Suchmaschinenoptimierung (SEO)**

Suchmaschinen wie Google oder DuckDuckGo sind wahre Sprachgenies. Sie möchten ihren Nutzern die relevantesten Ergebnisse liefern. Wenn jemand in Deutschland eine Suche auf Deutsch durchführt, erwartet er auch deutschsprachige Ergebnisse. Das `lang`-Attribut ist ein starkes Signal für die Suchmaschine, um den Inhalt deiner Seite korrekt zu katalogisieren und ihn der richtigen Zielgruppe zuzuordnen.

Betreibst du eine mehrsprachige Webseite, ist diese Kennzeichnung überlebenswichtig. Ohne sie könnte die Suchmaschine Schwierigkeiten haben, die englische Version deiner Seite von der spanischen oder deutschen zu unterscheiden, was zu einer schlechteren Platzierung in den Suchergebnissen für alle Sprachversionen führen kann.

**3. Browser-Funktionalität**

Auch der Webbrowser selbst nutzt die Sprachinformation für verschiedene interne Funktionen, die das Nutzererlebnis direkt verbessern:

*   **Automatische Übersetzung:** Browser wie Google Chrome bieten Nutzern an, fremdsprachige Seiten automatisch zu übersetzen. Um diesen Vorschlag machen zu können, muss der Browser zunächst die Ausgangssprache der Seite kennen. Das `lang`-Attribut liefert diese Information zuverlässig.
*   **Rechtschreibprüfung:** In Formularfeldern wie `<textarea>` oder bei `contenteditable`-Elementen nutzen Browser die deklarierte Sprache des Dokuments, um eine kontextbezogene Rechtschreibprüfung zu aktivieren. Wenn du `lang="de"` setzt, werden deutsche Wörter korrekt geprüft und falsch geschriebene englische Wörter als Fehler markiert – und umgekehrt.
*   **Typografie und Darstellung:** CSS bietet Eigenschaften wie `hyphens` zur automatischen Silbentrennung. Die Regeln für die Trennung von Wörtern sind sprachspezifisch. Der Browser kann korrekte Silbentrennung nur dann anwenden, wenn er dank des `lang`-Attributs weiß, welche sprachlichen Regeln er befolgen muss. Auch die Darstellung von Anführungszeichen innerhalb des `<q>`-Elements (quote) kann vom Browser sprachabhängig angepasst werden (z. B. „deutsche“ im Vergleich zu “englischen” Anführungszeichen).

#### Die richtigen Sprachcodes verwenden

Der Wert des `lang`-Attributs ist kein frei erfundener Text. Er folgt einem international standardisierten Format, das durch den ISO-Standard 639 definiert ist. Am gebräuchlichsten sind die zweibuchstabigen Codes nach ISO 639-1.

*   `de` für Deutsch
*   `en` für Englisch
*   `fr` für Französisch
*   `es` für Spanisch
*   `it` für Italienisch

Oft ist es jedoch sinnvoll, noch präziser zu sein und eine regionale Variante anzugeben. Dies ist besonders wichtig, wenn sich Vokabular, Schreibweise oder kulturelle Kontexte unterscheiden. Dazu hängst du nach einem Bindestrich den Ländercode (nach ISO 3166) an.

*   `de-DE`: Deutsch, wie es in Deutschland gesprochen wird.
*   `de-AT`: Deutsch für Österreich.
*   `de-CH`: Deutsch für die Schweiz.
*   `en-GB`: Britisches Englisch (z. B. "colour", "theatre").
*   `en-US`: Amerikanisches Englisch (z. B. "color", "theater").

Die allgemeine Regel lautet: Sei so spezifisch wie nötig, aber so allgemein wie möglich. Wenn dein Text für alle Deutschsprachigen gleichermaßen relevant ist, reicht `lang="de"`. Wenn er sich aber spezifisch auf den deutschen Markt bezieht und zum Beispiel deutsches Recht oder deutsche Kultur thematisiert, ist `lang="de-DE"` die präzisere und bessere Wahl.

#### Sprachwechsel innerhalb eines Dokuments

Das `lang`-Attribut ist nicht auf das `<html>`-Element beschränkt. Du kannst und solltest es auf jedem Element verwenden, wenn ein Teil deines Inhalts von der Hauptsprache des Dokuments abweicht. Dies ist ein weiterer wichtiger Aspekt für die Barrierefreiheit und die technische Korrektheit.

Stell dir einen deutschen Blogartikel vor, in dem du ein englisches Zitat einfügst.

```html
<p>
  Wie Winston Churchill treffend bemerkte: 
  <q lang="en">Success is not final, failure is not fatal: it is the courage to continue that counts.</q>
  Dieser Gedanke ist auch heute noch sehr relevant.
</p>
```

In diesem Fall wird der Screenreader für den Haupttext die deutsche Aussprache verwenden. Sobald er das `<q>`-Element mit `lang="en"` erreicht, schaltet er auf die englische Aussprache um, liest das Zitat korrekt vor und schaltet danach wieder zurück ins Deutsche. Ohne diese spezifische Auszeichnung würde er versuchen, die englischen Wörter deutsch auszusprechen.

#### Ein häufiges Missverständnis: Das `meta`-Tag

In älteren HTML-Versionen war es üblich, die Sprache auch über ein `<meta>`-Tag im `<head>` zu deklarieren:

```html
<!-- Veraltete Methode! Nicht mehr verwenden. -->
<meta http-equiv="Content-Language" content="de">
```

Diese Methode ist veraltet und sollte nicht mehr verwendet werden. Der moderne und korrekte Standard ist einzig und allein die Verwendung des `lang`-Attributs im `<html>`-Tag. Es ist direkter, wird von allen modernen Technologien besser unterstützt und gilt als die einzig wahre Quelle für die Sprachinformation des Dokuments.

Das `lang`-Attribut ist also weit mehr als eine formale Deklaration. Es ist ein kleines, aber mächtiges Werkzeug, das die Brücke zwischen deinem Code und der menschlichen Sprache schlägt. Es sorgt für eine bessere Nutzererfahrung, eine höhere Reichweite deiner Inhalte und macht das Web für alle Menschen ein Stück zugänglicher und verständlicher. Es zu setzen ist kein optionaler Bonus, sondern ein grundlegender Bestandteil eines professionell erstellten HTML-Dokuments.
