# Das lang-Attribut und seine Bedeutung

### Das lang-Attribut und seine Bedeutung

Wenn du die grundlegende Struktur einer HTML-Datei betrachtest, beginnend mit dem `<!DOCTYPE html>` und gefolgt vom `<html>`-Element, stößt du auf eines der wichtigsten, aber oft übersehenen Attribute: das `lang`-Attribut. Es mag auf den ersten Blick unscheinbar wirken, doch es ist ein entscheidender Schlüssel dafür, wie Maschinen – von Suchmaschinen bis hin zu Screenreadern – den Inhalt deiner Webseite interpretieren.

Das `lang`-Attribut teilt dem Browser und anderen Systemen mit, in welcher menschlichen Sprache der Inhalt des Dokuments verfasst ist. Seine grundlegendste Form sieht so aus:

```html
<!DOCTYPE html>
<html lang="de">
  <head>
    <!-- Metadaten kommen hier hin -->
  </head>
  <body>
    <!-- Der sichtbare Inhalt kommt hier hin -->
  </body>
</html>
```

In diesem Beispiel signalisiert `lang="de"`, dass die Hauptsprache dieser Webseite Deutsch ist. Diese kleine Angabe hat weitreichende Konsequenzen und ist aus mehreren Gründen unverzichtbar.

#### Warum die Sprachangabe so entscheidend ist

Stell dir vor, du hörst einer Person zu, weißt aber nicht, welche Sprache sie spricht. Du müsstest raten, was die Aussprache, die Betonung und die Bedeutung der Wörter angeht. Genau vor diesem Problem stehen Computerprogramme, wenn sie auf deine Webseite treffen und das `lang`-Attribut fehlt. Indem du die Sprache klar deklarierst, schaffst du eine verlässliche Grundlage für eine ganze Reihe von Technologien.

**1. Barrierefreiheit (Accessibility)**

Der wohl wichtigste Grund für die Verwendung des `lang`-Attributs ist die Barrierefreiheit. Menschen mit Sehbehinderungen nutzen sogenannte Screenreader – Programme, die den Inhalt einer Webseite vorlesen. Ein Screenreader ist im Grunde eine synthetische Stimme, die auf bestimmte Sprachregeln und Aussprachedatenbanken angewiesen ist.

Wenn du `lang="de"` setzt, weiß der Screenreader, dass er die deutsche Aussprache verwenden muss. Fehlt diese Angabe, versucht er oft, auf die Standardeinstellung des Systems zurückzugreifen, was häufig Englisch ist. Das Ergebnis kann für den Nutzer katastrophal sein. Deutsche Wörter werden mit englischer Phonetik vorgelesen, was den Text unverständlich und frustrierend macht.

Ein klassisches Beispiel ist das deutsche Wort „Gift“. Für einen deutschen Screenreader ist die Bedeutung klar. Ein englischer Screenreader würde es jedoch wie das englische Wort „gift“ (Geschenk) aussprechen, was nicht nur falsch, sondern im Kontext auch völlig irreführend ist. Durch die korrekte Sprachdeklaration stellst du sicher, dass alle Nutzer, unabhängig von ihren Fähigkeiten, deine Inhalte so erleben können, wie du sie gedacht hast.

**2. Suchmaschinenoptimierung (SEO)**

Auch Suchmaschinen wie Google, Bing und DuckDuckGo sind auf das `lang`-Attribut angewiesen. Sie nutzen es, um den Inhalt deiner Seite zu kategorisieren und ihn den richtigen Nutzern zuzuordnen. Wenn jemand in Deutschland eine Suche auf Deutsch durchführt, werden Seiten mit `lang="de"` mit höherer Wahrscheinlichkeit in den Suchergebnissen angezeigt.

Die Sprachangabe hilft Suchmaschinen dabei, ihre Ergebnisse geografisch und sprachlich zu filtern. Eine Webseite über „Autos“ mit `lang="de"` wird eher einem deutschen Nutzer angezeigt, während eine Seite mit dem gleichen Thema und `lang="en"` für einen englischsprachigen Nutzer relevanter ist. Ohne diese Information müssen Suchmaschinen raten, was die Relevanz deiner Seite in bestimmten Regionen und für bestimmte Zielgruppen mindern kann.

**3. Browser-Funktionen**

Moderne Webbrowser bieten eine Vielzahl intelligenter Funktionen, die auf der korrekten Sprachangabe aufbauen:

*   **Automatische Übersetzung:** Wenn ein Nutzer, dessen Browser auf Englisch eingestellt ist, deine deutsche Webseite (`lang="de"`) besucht, kann der Browser automatisch anbieten, die Seite zu übersetzen. Diese Funktion wird durch das `lang`-Attribut ausgelöst.
*   **Rechtschreibprüfung:** In Formularfeldern, wie zum Beispiel `<textarea>`, kann der Browser eine integrierte Rechtschreibprüfung aktivieren. Ist die Sprache des Dokuments korrekt angegeben, verwendet der Browser das passende Wörterbuch. Das erspart deinen Nutzern Tippfehler und Frustration.
*   **Silbentrennung:** CSS erlaubt eine automatische Silbentrennung (`hyphens: auto;`), um den Textfluss in schmalen Layouts zu verbessern. Die Regeln für die Silbentrennung sind jedoch von Sprache zu Sprache völlig unterschiedlich. Der Browser kann die korrekten Trennregeln nur anwenden, wenn er dank des `lang`-Attributs weiß, um welche Sprache es sich handelt.
*   **Korrekte Darstellung von Anführungszeichen:** Obwohl dies primär über CSS gesteuert wird, liefert das `lang`-Attribut die semantische Grundlage. Im Deutschen verwenden wir typischerweise die Anführungszeichen „unten und oben“, im Englischen hingegen “beide oben”.

#### Der richtige Code: ISO-Sprachcodes

Du kannst nicht einfach „deutsch“ oder „german“ in das `lang`-Attribut schreiben. Die Werte müssen einem standardisierten Format folgen, um weltweit verstanden zu werden. Der gängigste Standard ist ISO 639-1, der für die meisten Sprachen einen Zwei-Buchstaben-Code definiert.

Hier sind einige gängige Beispiele:

*   `de`: Deutsch
*   `en`: Englisch
*   `fr`: Französisch
*   `es`: Spanisch
*   `it`: Italienisch
*   `ja`: Japanisch
*   `zh`: Chinesisch

**Regionale Varianten angeben**

Manchmal reicht der Zwei-Buchstaben-Code nicht aus. Englisch ist nicht gleich Englisch, und Deutsch ist nicht gleich Deutsch. Es gibt Unterschiede zwischen britischem und amerikanischem Englisch oder zwischen dem in Deutschland, Österreich und der Schweiz gesprochenen Deutsch.

Um diese Varianten zu spezifizieren, kannst du dem Sprachcode einen Ländercode nach dem Standard ISO 3166-1 hinzufügen, getrennt durch einen Bindestrich.

*   `en-US`: Englisch (Vereinigte Staaten)
*   `en-GB`: Englisch (Großbritannien)
*   `de-DE`: Deutsch (Deutschland)
*   `de-AT`: Deutsch (Österreich)
*   `de-CH`: Deutsch (Schweiz)

Die Verwendung einer regionalen Variante ist dann sinnvoll, wenn dein Inhalt spezifisch auf eine bestimmte Region ausgerichtet ist, zum Beispiel durch die Verwendung regionaler Begriffe, Währungsangaben oder Datumsformate. Für allgemeine Texte in deutscher Sprache ist `lang="de"` jedoch völlig ausreichend und die beste Wahl.

#### Sprache für einzelne Textabschnitte ändern

Das `lang`-Attribut ist ein sogenanntes globales Attribut. Das bedeutet, du kannst es nicht nur auf dem `<html>`-Element verwenden, sondern auf fast jedem anderen HTML-Tag auch. Das ist äußerst nützlich, wenn du innerhalb deines Dokuments einen Textabschnitt in einer anderen Sprache hast.

Stell dir vor, du schreibst einen deutschen Blogartikel und zitierst darin einen englischen Satz. So würdest du das korrekt auszeichnen:

```html
<p>In seinem berühmten Werk schrieb Shakespeare den unsterblichen Satz: <q lang="en">To be, or not to be, that is the question.</q> Das fasst die menschliche Zerrissenheit perfekt zusammen.</p>
```

Durch das `lang="en"` am `<q>`-Tag (dem Tag für kurze Zitate) weiß ein Screenreader, dass er für diesen Satz kurz in den englischen Aussprachemodus wechseln muss. Danach kehrt er wieder zur Hauptsprache des Dokuments (Deutsch) zurück. Auch die automatische Übersetzung des Browsers weiß nun, dass dieser Teil nicht übersetzt werden muss, da er bereits in einer anderen Sprache vorliegt.

#### Was du vermeiden solltest

Ein häufiger Fehler aus der Vergangenheit war die Verwendung eines `<meta>`-Tags zur Angabe der Sprache, etwa so:

```html
<!-- Veraltet und falsch! Nicht verwenden! -->
<meta http-equiv="content-language" content="de">
```

Diese Methode ist veraltet (deprecated) und wird von modernen Browsern und Standards nicht mehr unterstützt. Sie hat keine semantische Wirkung auf den Inhalt. Der einzig korrekte und wirksame Weg, die Sprache eines Dokuments oder eines Textabschnitts zu deklarieren, ist das `lang`-Attribut.

Das `lang`-Attribut ist also weit mehr als nur eine Formalität. Es ist ein fundamentaler Baustein für eine zugängliche, suchmaschinenfreundliche und funktionale Webseite. Es ist eine einfache, aber wirkungsvolle Geste des Respekts gegenüber all deinen Nutzern und den Technologien, die sie verwenden, um auf deine Inhalte zuzugreifen. Gewöhne dir an, es in jedem einzelnen HTML-Dokument von Anfang an korrekt zu setzen.
