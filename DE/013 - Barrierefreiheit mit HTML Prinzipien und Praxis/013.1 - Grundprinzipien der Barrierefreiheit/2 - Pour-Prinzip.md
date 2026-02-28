# Pour-Prinzip

### Das POUR-Prinzip: Die vier Säulen der Barrierefreiheit

Wenn du beginnst, dich mit der digitalen Barrierefreiheit zu beschäftigen, wirst du sehr schnell auf ein fundamentales Konzept stoßen: das POUR-Prinzip. Es ist das Herzstück der international anerkannten Web Content Accessibility Guidelines (WCAG) und bildet das theoretische Fundament, auf dem barrierefreie Web-Erlebnisse aufgebaut werden. POUR ist ein Akronym, das für vier wesentliche Eigenschaften steht, die jede digitale Anwendung erfüllen sollte, um für möglichst viele Menschen zugänglich zu sein:

*   **P**erceivable (Wahrnehmbar)
*   **O**perable (Bedienbar)
*   **U**nderstandable (Verständlich)
*   **R**obust (Robust)

Stell dir diese vier Prinzipien wie die tragenden Säulen eines Gebäudes vor. Fehlt eine dieser Säulen oder ist sie brüchig, wird die gesamte Struktur instabil und für bestimmte Personengruppen unzugänglich. Es geht hierbei nicht um eine starre Checkliste, die du abhakst, sondern um eine Denkweise, die du dir aneignen solltest, wenn du Webseiten und Anwendungen konzipierst und entwickelst. Lass uns jede dieser Säulen genauer betrachten.

#### 1. Wahrnehmbar (Perceivable)

Das erste Prinzip ist das grundlegendste: Informationen und die Bestandteile der Benutzeroberfläche müssen für die Nutzenden so darstellbar sein, dass sie sie wahrnehmen können. Das bedeutet, dass Inhalte nicht für einen der Sinne unsichtbar sein dürfen.

**Textalternativen für Nicht-Text-Inhalte:**
Dies ist das wohl bekannteste Beispiel. Ein blinder Nutzer kann ein Bild nicht sehen. Wenn du jedoch einen alternativen Text (ein `alt`-Attribut) bereitstellst, kann sein Screenreader diesen Text vorlesen und so den Inhalt und die Funktion des Bildes vermitteln.

```html
<!-- Gut: Der alternative Text beschreibt den Inhalt und die Funktion des Bildes. -->
<img src="hund-im-park.jpg" alt="Ein goldener Retriever fängt einen roten Ball in einem sonnigen Park.">

<!-- Schlecht: Der alternative Text ist nicht aussagekräftig. -->
<img src="hund-im-park.jpg" alt="Bild">

<!-- Auch schlecht: Kein alt-Attribut vorhanden. Ein Screenreader liest dann vielleicht den Dateinamen vor. -->
<img src="hund-im-park.jpg">
```

Dieses Prinzip gilt aber nicht nur für Bilder. Ein Video benötigt Untertitel für gehörlose oder schwerhörige Menschen. Eine reine Audiodatei, wie ein Podcast, benötigt ein Transkript. Jede Information, die visuell oder auditiv vermittelt wird, braucht eine Alternative.

**Anpassungsfähigkeit des Inhalts:**
Der Inhalt deiner Seite muss so strukturiert sein, dass er auf verschiedene Weisen dargestellt werden kann, ohne dass Informationen oder die Struktur verloren gehen. Das Zauberwort hierfür lautet: semantisches HTML. Wenn du Überschriften korrekt mit `<h1>` bis `<h6>` auszeichnest, Listen mit `<ul>` oder `<ol>` und wichtige Texte mit `<strong>` oder `<em>`, gibst du der Maschine (und damit auch assistiven Technologien) eine klare Struktur vor. Ein Screenreader kann dann beispielsweise von Überschrift zu Überschrift springen und dem Nutzer so eine schnelle Navigation ermöglichen, ähnlich wie ein sehender Nutzer eine Seite überfliegt.

Verwendest du hingegen `<div>`-Elemente mit CSS, um eine Überschrift optisch größer darzustellen, geht diese semantische Information verloren. Für die assistive Technologie ist es nur ein beliebiger Textabschnitt.

**Unterscheidbarkeit:**
Inhalte müssen leicht zu sehen und zu hören sein. Das betrifft vor allem den Kontrast zwischen Vordergrund (Text) und Hintergrund. Menschen mit Sehschwächen oder Farbfehlsichtigkeiten können Texte mit geringem Kontrast nur schwer oder gar nicht lesen. Die WCAG geben hier klare Kontrastverhältnisse vor, die du mit Online-Werkzeugen leicht überprüfen kannst.

Ein weiterer wichtiger Punkt ist, dass Farbe niemals das *einzige* Mittel sein darf, um Informationen zu vermitteln. Ein Formularfeld, das bei einem Fehler nur einen roten Rahmen erhält, ist für einen farbenblinden Nutzer möglicherweise nicht als fehlerhaft erkennbar. Eine Kombination aus Farbe, einem Symbol (z.B. ein Ausrufezeichen) und einer klaren Fehlermeldung in Textform ist hier die barrierefreie Lösung.

#### 2. Bedienbar (Operable)

Es reicht nicht aus, dass Inhalte wahrnehmbar sind. Nutzer müssen auch in der Lage sein, mit der Benutzeroberfläche zu interagieren. Das Prinzip der Bedienbarkeit stellt sicher, dass niemand von der Interaktion ausgeschlossen wird.

**Tastaturbedienbarkeit:**
Dies ist ein Eckpfeiler der Bedienbarkeit. Jede Funktionalität, die mit einer Maus erreichbar ist, muss auch ausschließlich über die Tastatur zugänglich sein. Viele Menschen können oder wollen keine Maus benutzen, sei es aufgrund einer motorischen Einschränkung, weil sie fortgeschrittene Power-User sind oder weil sie einen Screenreader nutzen, der auf Tastaturbefehlen basiert.

Du kannst das ganz einfach testen: Versuche, durch deine Webseite nur mit der Tab-Taste (zum Springen zwischen interaktiven Elementen wie Links, Buttons und Formularfeldern) und der Enter- bzw. Leertaste (zum Aktivieren) zu navigieren. Kannst du jeden Link erreichen und klicken? Kannst du jedes Formular ausfüllen und absenden? Siehst du dabei immer, welches Element gerade den Fokus hat (der sogenannte "Fokus-Indikator", oft ein Rahmen um das Element)? Wenn nicht, gibt es hier Handlungsbedarf.

**Genügend Zeit:**
Menschen benötigen unterschiedlich viel Zeit, um Inhalte zu lesen und zu verstehen. Wenn du Inhalte hast, die sich bewegen, blinken oder automatisch aktualisieren (wie bei einem Nachrichten-Ticker oder einem Bilderkarussell), musst du den Nutzern die Möglichkeit geben, diese anzuhalten, zu pausieren oder die Geschwindigkeit anzupassen. Auch bei zeitlich begrenzten Sitzungen (z.B. im Online-Banking) sollte der Nutzer die Möglichkeit haben, die Zeit zu verlängern, bevor er automatisch ausgeloggt wird.

**Keine Anfälle verursachen:**
Bestimmte visuelle Muster, insbesondere schnell blinkende oder blitzende Inhalte, können bei manchen Menschen photosensitive epileptische Anfälle auslösen. Webseiten dürfen keine Inhalte enthalten, die bekanntermaßen Anfälle verursachen. Die Faustregel lautet: Vermeide Inhalte, die mehr als dreimal pro Sekunde aufblitzen.

**Navigierbarkeit:**
Den Nutzern zu helfen, sich zurechtzufinden, ist ein zentraler Aspekt der Bedienbarkeit. Dazu gehören:
*   Ein aussagekräftiger `<title>` für jede Seite, der im Browser-Tab und für Screenreader angezeigt wird.
*   Eine logische und konsistente Navigationsstruktur.
*   Die Möglichkeit, Blöcke von Inhalten zu überspringen, die auf mehreren Seiten wiederholt werden (z.B. ein "Zum Hauptinhalt springen"-Link, der für Tastaturnutzer am Anfang der Seite erscheint).
*   Eine klare Überschriftenstruktur, die es ermöglicht, die Seitenarchitektur schnell zu erfassen.

#### 3. Verständlich (Understandable)

Die Informationen und die Bedienung der Benutzeroberfläche müssen verständlich sein. Es nützt nichts, wenn ein Nutzer den Inhalt wahrnehmen und die Seite bedienen kann, aber nicht versteht, was er tun soll oder was die Texte bedeuten.

**Lesbarkeit:**
Der Text auf deiner Webseite sollte klar und verständlich sein. Das betrifft nicht nur die Wahl einfacher Worte und kurzer Sätze, sondern auch technische Aspekte. Ein ganz entscheidender Punkt ist die korrekte Angabe der Sprache des Dokuments im `<html>`-Tag.

```html
<!-- Korrekt für eine deutschsprachige Seite -->
<html lang="de">
```

Diese simple Angabe teilt dem Browser und assistiven Technologien mit, in welcher Sprache der Inhalt verfasst ist. Ein Screenreader kann dadurch die korrekte Aussprache und Betonung für die Sprachausgabe wählen, was die Verständlichkeit massiv erhöht.

**Vorhersehbarkeit:**
Eine gute Webseite verhält sich so, wie es die Nutzer erwarten. Wenn ein Klick auf einen Link eine Aktion auslöst, sollte diese vorhersehbar sein. Das bedeutet zum Beispiel, dass Links nicht ohne Vorwarnung in einem neuen Fenster öffnen oder dass das Ausfüllen eines Formularfeldes nicht plötzlich die ganze Seite neu lädt oder den Kontext ändert. Konsistenz in der Benennung, Positionierung und Funktionsweise von Navigationselementen und Bedienelementen auf der gesamten Webseite hilft den Nutzern enorm, sich zu orientieren.

**Hilfe bei der Eingabe:**
Fehler passieren. Eine verständliche Webseite hilft den Nutzern, Fehler zu vermeiden und sie, falls sie doch auftreten, einfach zu korrigieren.
*   **Beschriftungen:** Jedes Eingabefeld in einem Formular benötigt eine klare Beschriftung, die über das `<label>`-Element programmtechnisch mit dem Feld verknüpft ist.
*   **Anleitungen:** Wenn Eingaben ein bestimmtes Format erfordern (z.B. ein Datum als TT.MM.JJJJ), sollte dies klar kommuniziert werden, bevor der Nutzer etwas eingibt.
*   **Fehlererkennung und -beschreibung:** Wenn ein Nutzer einen Fehler macht, sollte dieser klar identifiziert werden. Die Fehlermeldung muss präzise beschreiben, *was* falsch ist und *wie* der Fehler behoben werden kann. Eine Meldung wie "Eingabe ungültig" ist nutzlos. Besser ist: "Bitte gib deine Postleitzahl im Format 12345 ein."

#### 4. Robust (Robust)

Das letzte Prinzip stellt sicher, dass deine Inhalte zuverlässig von einer Vielzahl von Programmen, Browsern und insbesondere assistiven Technologien interpretiert werden können. Deine Webseite muss mit aktuellen und zukünftigen Technologien kompatibel sein.

**Kompatibilität durch sauberen Code:**
Die Grundlage für Robustheit ist sauberes, valides HTML. Halte dich an die Standards des World Wide Web Consortium (W3C). Schließe alle Tags, verschachtle Elemente korrekt und verwende Attribute gemäß ihrer Spezifikation. Während moderne Browser oft sehr fehlerverzeihend sind und auch "kaputtes" HTML irgendwie darstellen, sind assistive Technologien viel stärker auf eine korrekte und logische Dokumentenstruktur (das DOM) angewiesen. Fehler im Code können dazu führen, dass Screenreader Inhalte falsch interpretieren oder wichtige Teile der Seite komplett ignorieren.

**Rolle, Name und Wert:**
Jedes Element einer Benutzeroberfläche muss für assistive Technologien eine klar definierte Rolle (Was ist es? Ein Button? Ein Tab?), einen Namen (Wie heißt es? "Senden", "Profil") und gegebenenfalls einen Wert oder Zustand (Ist die Checkbox aktiviert? Ist der Bereich aufgeklappt?) haben. Bei Standard-HTML-Elementen wie `<button>` oder `<input type="checkbox">` ist dies automatisch gegeben. Wenn du jedoch mit JavaScript und `<div>`- oder `<span>`-Elementen eigene, komplexe Widgets baust, musst du mit ARIA (Accessible Rich Internet Applications) nachhelfen, um diese semantischen Informationen bereitzustellen und die Robustheit zu gewährleisten.

Indem du diese vier Prinzipien – Wahrnehmbar, Bedienbar, Verständlich und Robust – bei jedem Schritt deiner Arbeit im Hinterkopf behältst, schaffst du nicht nur eine Webseite, die den WCAG-Richtlinien entspricht. Du schaffst eine bessere, offenere und fairere digitale Welt für alle.
