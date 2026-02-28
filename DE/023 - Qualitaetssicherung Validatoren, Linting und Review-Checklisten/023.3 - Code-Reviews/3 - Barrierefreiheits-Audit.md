# Barrierefreiheits-Audit

### Barrierefreiheits-Audit: Dein Wegweiser zur inklusiven Website

Ein Code-Review dient dazu, die Qualität deines Codes zu sichern. Doch Qualität bemisst sich nicht nur an Eleganz, Performance oder Fehlerfreiheit. Eine der wichtigsten, aber oft übersehenen Dimensionen der Qualität ist die Barrierefreiheit (Accessibility). Ein Barrierefreiheits-Audit ist im Grunde ein spezialisiertes Code- und Design-Review mit dem Ziel, Hürden für Menschen mit Behinderungen zu identifizieren und zu beseitigen. Es ist der Prozess, bei dem du deine Webanwendung systematisch darauf überprüfst, wie gut sie für alle Nutzergruppen zugänglich ist.

Stell dir vor, du hast eine Tür entworfen. Sie ist stabil, sieht gut aus und lässt sich leicht öffnen und schließen. Aber sie hat eine hohe Stufe und keinen Griff, den eine Person im Rollstuhl erreichen kann. Technisch ist die Tür perfekt, aber praktisch schließt sie Menschen aus. Ein Barrierefreiheits-Audit findet genau solche "Stufen" und "zu hohen Griffe" in deiner digitalen Welt.

Der Prozess lässt sich grob in drei Phasen unterteilen: automatisierte Tests, manuelle Überprüfungen und Tests mit assistiven Technologien. Jede dieser Phasen deckt unterschiedliche Arten von Problemen ab, und erst ihr Zusammenspiel ergibt ein vollständiges Bild.

#### Automatisierte Tests: Das Sicherheitsnetz

Den ersten Schritt auf dem Weg zu einer barrierefreien Seite bilden automatisierte Werkzeuge. Sie sind wie ein Rechtschreibprogramm für deinen Code – sie fangen die offensichtlichen und häufigen Fehler ab. Diese Tools existieren meist als Browser-Erweiterungen (wie axe DevTools oder WAVE) oder als Kommandozeilen-Tools, die du in deinen Build-Prozess integrieren kannst (wie Pa11y).

Sie scannen den DOM-Baum deiner Seite und prüfen ihn gegen eine Reihe vordefinierter Regeln, die oft auf den Web Content Accessibility Guidelines (WCAG) basieren. Typische Fehler, die sie zuverlässig finden, sind:

*   **Fehlende `alt`-Attribute:** Bilder ohne alternativen Text sind für Screenreader-Nutzer unsichtbar.
*   **Geringe Kontraste:** Texte, deren Farbe sich zu wenig vom Hintergrund abhebt, sind für Menschen mit Sehschwächen schwer oder gar nicht lesbar.
*   **Fehlende Formular-Labels:** Eingabefelder ohne verknüpfte `<label>`-Elemente sind kontextlos. Ein Screenreader weiß nicht, welche Information hier erwartet wird.
*   **Inkorrekte ARIA-Implementierungen:** Falsch verwendete ARIA-Attribute können mehr schaden als nutzen.

Ein automatisiertes Tool könnte zum Beispiel folgenden fehlerhaften Code anmahnen:

```html
<!-- Falsch: Keine Verknüpfung zwischen Label und Input -->
<div>
  <span>E-Mail-Adresse</span>
  <input type="email" name="email">
</div>
```

Das Tool würde hier bemängeln, dass das `<input>`-Feld kein zugeordnetes Label hat. Die korrekte Implementierung wäre:

```html
<!-- Richtig: Klare Verknüpfung durch for/id-Attribute -->
<div>
  <label for="email-input">E-Mail-Adresse</label>
  <input type="email" name="email" id="email-input">
</div>
```

Automatisierte Tests sind schnell, einfach durchzuführen und decken etwa 20-30 % aller potenziellen Barrierefreiheitsprobleme ab. Ihr größter Nachteil ist jedoch, dass sie keinen Kontext verstehen. Ein Tool kann prüfen, *ob* ein `alt`-Attribut vorhanden ist, aber nicht, *ob der Text darin sinnvoll* ist. Es kann nicht beurteilen, ob die Lesereihenfolge logisch ist oder ob eine Interaktion intuitiv funktioniert. Deshalb sind sie nur der Anfang.

#### Manuelle Tests: Wo deine Expertise zählt

Hier kommst du als Entwickler ins Spiel. Manuelle Tests erfordern menschliches Urteilsvermögen und Empathie. Du versuchst, die Seite so zu nutzen, wie es jemand mit einer bestimmten Einschränkung tun würde. Eine systematische Checkliste ist hier Gold wert.

**1. Die Tastaturnavigation**

Dies ist der grundlegendste und vielleicht wichtigste manuelle Test. Ziehe den Stecker deiner Maus und versuche, deine gesamte Website nur mit der Tastatur zu bedienen.

*   **Tab-Reihenfolge:** Drücke wiederholt die `Tab`-Taste. Bewegt sich der Fokus logisch durch die Seite – von oben nach unten, von links nach rechts? Springt er unvorhersehbar umher oder landet in einer "Fokus-Falle", aus der du mit `Tab` nicht mehr entkommst?
*   **Sichtbarer Fokus:** Ist zu jeder Zeit klar ersichtlich, welches Element gerade den Fokus hat? Browser bieten einen Standard-Fokusindikator (meist einen blauen Rahmen), der jedoch oft aus ästhetischen Gründen mit `outline: none;` entfernt wird. Das ist ein K.o.-Kriterium für die Barrierefreiheit. Wenn du den Standard-Indikator entfernst, musst du ihn durch eine gut sichtbare Alternative ersetzen.
*   **Interaktivität:** Kannst du alle interaktiven Elemente (Links, Buttons, Formularfelder, Menüs) nicht nur erreichen, sondern auch bedienen? Links und Buttons werden mit `Enter` aktiviert. Checkboxen und Radio-Buttons mit der `Leertaste`.

**2. Screenreader-Simulation**

Um zu verstehen, wie blinde oder stark sehbehinderte Menschen deine Seite erleben, musst du einen Screenreader benutzen. Auf macOS ist VoiceOver vorinstalliert, für Windows ist NVDA eine kostenlose und ausgezeichnete Wahl. Aktiviere den Screenreader und schließe die Augen oder schau vom Bildschirm weg.

*   **Struktur:** Ist die Seite durch Überschriften (`<h1>` bis `<h6>`) logisch gegliedert? Navigiere nur durch die Überschriften. Bekommst du so einen guten Überblick über den Inhalt?
*   **Landmarks:** Werden semantische HTML-Elemente wie `<header>`, `<nav>`, `<main>` und `<footer>` genutzt? Screenreader-Nutzer verwenden diese "Landmarks", um schnell zu wichtigen Bereichen der Seite zu springen.
*   **Link-Texte:** Sind deine Link-Texte aussagekräftig? Ein Dutzend Links mit dem Text "Hier klicken" oder "Mehr erfahren" sind ohne den visuellen Kontext nutzlos. Der Link-Text sollte das Ziel des Links beschreiben, z. B. "Weitere Informationen zu unseren Datenschutzrichtlinien".
*   **Bilder und Grafiken:** Werden die `alt`-Texte vorgelesen? Vermitteln sie den Inhalt und die Funktion des Bildes korrekt? Ist das Bild rein dekorativ, sollte das `alt`-Attribut leer sein (`alt=""`), damit der Screenreader es ignoriert.

**3. Visuelle und inhaltliche Überprüfungen**

*   **Zoom:** Vergrößere die Seite im Browser auf 200 %. Bricht das Layout zusammen? Überlappen sich Inhalte oder werden unlesbar? Müssen Nutzer horizontal scrollen, um Textzeilen zu lesen? Eine gut gestaltete responsive Seite sollte hier keine Probleme haben.
*   **Farbverwendung:** Wird Farbe als einziges Mittel zur Informationsvermittlung eingesetzt? Ein klassisches Beispiel sind Fehlermeldungen, die nur durch rote Schrift gekennzeichnet sind. Für farbenblinde Nutzer ist diese Information nicht zugänglich. Ergänze solche Hinweise immer durch Text oder ein Icon.
*   **Formulare und Fehlermeldungen:** Wenn du ein Formular absendest und Fehler auftreten, sind die Meldungen klar und direkt mit den fehlerhaften Feldern verknüpft? Eine gute Praxis ist es, ARIA-Attribute wie `aria-describedby` zu verwenden, um eine programmatische Verbindung zwischen einem Input und seiner Fehlermeldung herzustellen.

Ein Beispiel für ein barrierefreies Fehlermanagement:

```html
<label for="user-password">Passwort</label>
<input
  type="password"
  id="user-password"
  aria-invalid="true"
  aria-describedby="password-error"
>
<div id="password-error" role="alert">
  Das Passwort muss mindestens 8 Zeichen lang sein.
</div>
```

Ein Screenreader liest hier nicht nur das Label vor, sondern auch den Zustand "ungültige Eingabe" und die dazugehörige Fehlermeldung.

#### Tests mit Nutzern: Der Realitätscheck

Die dritte und aufschlussreichste Phase eines Audits ist der Test mit echten Menschen, die auf assistive Technologien angewiesen sind. Du kannst noch so viele Simulationen durchführen – du wirst nie die gelebte Erfahrung, die Gewohnheiten und die Frustrationen eines täglichen Screenreader-Nutzers nachbilden können.

Dieser Schritt mag aufwendig erscheinen, aber der Erkenntnisgewinn ist unbezahlbar. Beobachte, wie ein Nutzer mit einer Behinderung versucht, eine zentrale Aufgabe auf deiner Seite zu erledigen, zum Beispiel ein Produkt zu kaufen oder einen Artikel zu finden. Wo bleibt er hängen? Was verwirrt ihn? Diese Beobachtungen decken oft Probleme auf, die weder automatisierte Tools noch manuelle Experten-Checks finden würden.

#### Dokumentation und Integration in den Workflow

Ein Audit ist nur nützlich, wenn seine Ergebnisse umgesetzt werden. Jedes gefundene Problem sollte dokumentiert werden. Ein guter Audit-Bericht enthält:

1.  **Beschreibung des Problems:** Was genau ist falsch?
2.  **Ort:** Wo auf der Seite tritt das Problem auf (URL, Komponente)?
3.  **Betroffene Nutzergruppe:** Wer wird durch dieses Problem behindert?
4.  **Verletztes WCAG-Kriterium:** (Optional, aber hilfreich) Welche offizielle Richtlinie wird missachtet?
5.  **Lösungsvorschlag:** Wie kann das Problem behoben werden (inklusive Code-Snippets)?

Die größte Herausforderung besteht darin, Barrierefreiheit nicht als einmaliges Projekt, sondern als kontinuierlichen Prozess zu etablieren. Integriere automatisierte Tests in deine CI/CD-Pipeline, um Regressionen zu verhindern. Mache eine kurze Tastatur- und Screenreader-Prüfung zu einem festen Bestandteil deiner Code-Reviews für neue Features.

Ein Barrierefreiheits-Audit ist mehr als nur eine technische Prüfung. Es ist ein Akt der Empathie. Es zwingt dich, deine eigene Perspektive zu verlassen und dein Produkt durch die Augen – oder Ohren und Hände – anderer zu erleben. Es macht dich nicht nur zu einem besseren Entwickler, sondern trägt auch dazu bei, ein Web zu schaffen, das wirklich für alle da ist.
