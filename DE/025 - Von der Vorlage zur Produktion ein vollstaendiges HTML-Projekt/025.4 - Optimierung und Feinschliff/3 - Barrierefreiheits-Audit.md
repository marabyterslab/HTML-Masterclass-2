# Barrierefreiheits-Audit

### Das Barrierefreiheits-Audit: Der finale Qualitätscheck

Dein Projekt steht. Das Design ist umgesetzt, die Inhalte sind eingepflegt und die Funktionalität ist getestet. Du bist kurz davor, deine Arbeit der Welt zu präsentieren. Doch bevor du auf den großen "Veröffentlichen"-Knopf drückst, gibt es einen letzten, aber entscheidenden Schritt, der oft übersehen wird: das Barrierefreiheits-Audit. Dieser Schritt stellt sicher, dass deine Website nicht nur für dich oder für einen idealtypischen Nutzer funktioniert, sondern für so viele Menschen wie möglich – unabhängig von ihren körperlichen oder kognitiven Fähigkeiten.

Ein Audit ist keine Bestrafung für Fehler, sondern eine professionelle Qualitätskontrolle. Es ist der Moment, in dem du die Brille wechselst und deine eigene Arbeit aus einer völlig neuen Perspektive betrachtest. Es geht darum, Empathie in Code zu übersetzen und sicherzustellen, dass die digitale Welt, die du erschaffst, offen und einladend für alle ist.

#### Was ist ein Barrierefreiheits-Audit?

Ein Barrierefreiheits-Audit ist eine systematische Überprüfung deiner Website anhand etablierter Richtlinien, allen voran der Web Content Accessibility Guidelines (WCAG). Ziel ist es, Hürden zu identifizieren, die Menschen mit Behinderungen an der Nutzung deiner Seite hindern könnten. Dabei geht es um weit mehr als nur blinde Nutzer und Screenreader. Barrierefreiheit betrifft Menschen mit:

*   **Sehbehinderungen:** Von Farbenblindheit über schwache Sehkraft bis hin zur vollständigen Blindheit.
*   **Hörbehinderungen:** Menschen, die auf Untertitel oder Transkripte für Audio- und Videoinhalte angewiesen sind.
*   **Motorischen Einschränkungen:** Nutzer, die keine Maus bedienen können und ausschließlich auf die Tastatur oder andere assistierende Technologien angewiesen sind.
*   **Kognitiven und neurologischen Einschränkungen:** Personen, die von klaren Strukturen, einfacher Sprache und einer vorhersehbaren Navigation profitieren, wie zum Beispiel Menschen mit Legasthenie oder ADHS.

Ein gutes Audit kombiniert drei verschiedene Prüfmethoden: automatisierte Tests, manuelle Überprüfungen und im Idealfall Tests mit echten Nutzern.

#### 1. Automatisierte Tests: Die schnelle Erstdiagnose

Automatisierte Tools sind der erste und einfachste Schritt deines Audits. Sie scannen deinen Code und prüfen ihn auf häufige, maschinell erkennbare Fehler. Sie sind unglaublich schnell und decken eine gute Basis an Problemen ab.

Beliebte Werkzeuge hierfür sind:

*   **Lighthouse:** Direkt in den Chrome DevTools integriert. Du kannst einen Report erstellen, der neben Performance und SEO auch einen detaillierten Accessibility-Score liefert.
*   **axe DevTools:** Eine Browser-Erweiterung, die deine Seite analysiert und dir genau anzeigt, wo im Code die Probleme liegen, inklusive Lösungsvorschlägen.
*   **WAVE:** Eine weitere beliebte Browser-Erweiterung, die deine Seite visuell überlagert und Fehler direkt im Kontext anzeigt.

Was finden diese Tools? Typische Funde sind:

*   **Fehlende `alt`-Attribute:** Bilder ohne alternativen Text sind für Screenreader unsichtbar.
    ```html
    <!-- SCHLECHT: Der Screenreader sagt nur "Bild". -->
    <img src="firmenlogo.svg">

    <!-- GUT: Der Screenreader liest den Alternativtext vor. -->
    <img src="firmenlogo.svg" alt="Firmenname - Zur Startseite">
    ```
*   **Fehlende Formular-Labels:** Eingabefelder ohne verknüpfte `<label>`-Elemente sind für Nutzer assistiver Technologien ein Rätsel.
*   **Kontrastfehler:** Texte, deren Farbe sich nicht ausreichend vom Hintergrund abhebt, sind für Menschen mit Sehschwäche schwer oder gar nicht lesbar.
*   **Fehlende Sprachangabe:** Wenn im `<html>`-Tag das `lang`-Attribut fehlt, weiß ein Screenreader nicht, in welcher Sprache er den Inhalt vorlesen soll.

**Die Grenzen der Automatisierung:**
So nützlich diese Tools auch sind, sie finden nur etwa 30-40 % aller potenziellen Barrieren. Ein Tool kann prüfen, *ob* ein `alt`-Attribut vorhanden ist, aber nicht, *ob der Text darin sinnvoll ist*. Ein Tool kann die syntaktisch korrekte Überschriftenhierarchie prüfen, aber nicht, ob die Struktur logisch für einen Menschen ist. Daher ist der nächste Schritt unverzichtbar.

#### 2. Manuelle Überprüfung: Dein menschlicher Verstand im Einsatz

Hier kommst du ins Spiel. Bei der manuellen Prüfung schlüpfst du in die Rolle verschiedener Nutzer und testest die Bedienbarkeit deiner Seite unter erschwerten Bedingungen. Eine systematische Checkliste ist hier Gold wert.

**Die Tastatur-Navigation:**
Dies ist einer der wichtigsten manuellen Tests. Trenne dich von deiner Maus und versuche, deine komplette Website nur mit der Tastatur zu bedienen.

*   **Tab-Taste:** Springe von einem interaktiven Element (Link, Button, Formularfeld) zum nächsten.
*   **Shift + Tab:** Springe rückwärts.
*   **Enter/Leertaste:** Aktiviere einen Link oder Button.
*   **Pfeiltasten:** Navigiere innerhalb von Komponenten wie Dropdown-Menüs oder Radio-Buttons.

Achte dabei auf zwei Dinge:
1.  **Ist jedes interaktive Element erreichbar?** Kannst du das Menü öffnen, durch die Links navigieren und Formulare ausfüllen?
2.  **Siehst du immer, wo du bist?** Ein klar sichtbarer Fokus-Indikator (oft ein blauer Rahmen, der `:focus`-Zustand) ist essenziell. Wenn du die Tab-Taste drückst und nicht siehst, welches Element gerade aktiv ist, hast du eine massive Barriere gefunden. Oft wird dieser Fokus-Rahmen aus ästhetischen Gründen mit `outline: none;` im CSS entfernt – ein Kardinalfehler.

**Die Screenreader-Erfahrung:**
Um zu verstehen, wie blinde Nutzer deine Seite erleben, musst du sie selbst mit einem Screenreader testen. Die gängigsten sind NVDA (kostenlos für Windows), VoiceOver (in macOS und iOS integriert) und TalkBack (in Android integriert).

Schließe deine Augen oder schaue vom Bildschirm weg und versuche, folgende Aufgaben zu erledigen:
*   **Verstehe den Seitenaufbau:** Liest der Screenreader die Überschriften (`<h1>`, `<h2>` etc.) korrekt vor? Kannst du über die Überschriften-Navigation schnell zu den relevanten Abschnitten springen? Hier zeigt sich der Wert von semantischem HTML.
*   **Navigiere durch die Seite:** Erkennst du die Navigation als solche (dank `<nav>`), den Hauptinhalt (dank `<main>`) und den Footer (dank `<footer>`)?
*   **Interagiere mit Formularen:** Werden die Labels korrekt vorgelesen, wenn du in ein Eingabefeld kommst? Erhältst du verständliche Fehlermeldungen?

Ein typisches Problem, das hier auffällt, ist die Verwendung von `<div>`s mit Klick-Events anstelle von echten `<button>`-Elementen. Ein Screenreader erkennt ein `<div>` nicht als interaktives Element, ein `<button>` hingegen schon.

```html
<!-- SCHLECHT: Für Screenreader und Tastaturnutzer unzugänglich. -->
<div onclick="doSomething()">Aktion ausführen</div>

<!-- GUT: Semantisch korrekt, von Natur aus fokussierbar und klickbar. -->
<button onclick="doSomething()">Aktion ausführen</button>
```

**Weitere manuelle Prüfpunkte:**

*   **Inhaltsstruktur:** Ist die Überschriftenhierarchie logisch? Gibt es nur eine `<h1>` pro Seite? Werden Listen (`<ul>`, `<ol>`) korrekt für Aufzählungen verwendet und nicht nur zur Einrückung?
*   **Zoom und Textvergrößerung:** Vergrößere den Zoom deines Browsers auf 200 %. Bricht das Layout? Entsteht unleserlicher, überlappender Text oder musst du horizontal scrollen, um Inhalte zu lesen?
*   **Verständlichkeit:** Ist die Sprache klar und einfach? Sind Links aussagekräftig formuliert ("Mehr erfahren" ist weniger hilfreich als "Mehr über unsere Dienstleistungen erfahren")?
*   **Multimedia:** Haben Videos Untertitel und idealerweise eine Transkription? Werden Audioinhalte ebenfalls transkribiert?

#### 3. Nutzertests: Der ultimative Realitätscheck

Der Goldstandard eines jeden Audits ist der Test mit echten Menschen, die auf assistierende Technologien angewiesen sind. Ihre Erfahrungen sind unbezahlbar und decken oft Probleme auf, an die du im Traum nicht gedacht hättest.

Auch wenn dies für kleinere Projekte oft den Rahmen sprengt, ist es wichtig, diesen Schritt zu kennen. Agenturen, die sich auf Barrierefreiheit spezialisiert haben, können solche Tests vermitteln. Das Feedback, das du hier erhältst, geht weit über technische Korrektheit hinaus – es gibt dir Einblicke in die tatsächliche *Benutzbarkeit* deines Produkts.

#### Ergebnisse dokumentieren und priorisieren

Ein Audit endet nicht mit dem Finden von Fehlern, sondern mit deren Dokumentation. Erstelle eine klare Liste aller gefundenen Probleme. Jeder Eintrag sollte enthalten:

*   **Problem:** Eine kurze, verständliche Beschreibung der Barriere.
*   **Ort:** Die URL und ggf. ein Screenshot oder eine Beschreibung, wo das Problem auftritt.
*   **Betroffene Nutzergruppe:** Z. B. "Tastaturnutzer", "Screenreader-Nutzer", "Nutzer mit Sehschwäche".
*   **Schweregrad:** Priorisiere die Fehler. Eine "kritische" Barriere blockiert einen Nutzer komplett (z. B. ein nicht bedienbarer Checkout-Button). Ein "mittelschwerer" Fehler macht eine Aufgabe schwierig, aber nicht unmöglich.
*   **WCAG-Kriterium:** Verweise auf das relevante Erfolgskriterium der WCAG (z. B. "1.4.3 Kontrast (Minimum)").
*   **Lösungsvorschlag:** Beschreibe, wie das Problem behoben werden kann.

Diese Dokumentation ist deine Roadmap für den Feinschliff. Arbeite die Punkte von kritisch nach niedrig ab und teste nach der Behebung erneut.

Ein Barrierefreiheits-Audit ist kein Hindernis auf dem Weg zur Veröffentlichung, sondern ein integraler Bestandteil der professionellen Webentwicklung. Es ist der Prozess, der sicherstellt, dass dein fertiges Projekt nicht nur technisch exzellent, sondern auch zutiefst menschlich und inklusiv ist. Es ist der letzte, entscheidende Pinselstrich, der dein Werk wirklich vollendet.
