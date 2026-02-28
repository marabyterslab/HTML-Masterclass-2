# Schrittweise Modernisierung

### Schrittweise Modernisierung

Wenn du vor einem Berg von Legacy-HTML stehst – einem über Jahre gewachsenen Projekt, das vielleicht noch auf Tabellenlayouts, `<font>`-Tags und Inline-Styles basiert – kann der Impuls überwältigend sein, alles wegzuwerfen und von vorne anzufangen. Dieser "Big Bang"-Ansatz, ein kompletter Rewrite, ist jedoch oft die riskanteste und teuerste Strategie. Projekte dieser Art neigen dazu, Budgets und Zeitpläne zu sprengen, und während der monate- oder gar jahrelangen Neuentwicklung bleibt die bestehende Seite auf ihrem veralteten Stand. Am Ende steht man vielleicht vor einem neuen, aber bereits wieder veralteten Produkt.

Eine weitaus pragmatischere, sicherere und oft auch schnellere Methode ist die schrittweise Modernisierung. Die Grundidee ist einfach: Statt das ganze Haus auf einmal abzureißen, renovierst du es Raum für Raum. Du zerlegst die gewaltige Aufgabe des Refactorings in viele kleine, überschaubare und vor allem sichere Schritte. Jeder Schritt verbessert den Code ein klein wenig, ohne die Funktionalität der gesamten Anwendung zu gefährden. Jeder Schritt ist ein kleiner Sieg, der sofort live gehen kann und den Code Stück für Stück in einen modernen, wartbaren Zustand überführt.

#### Die Philosophie der kleinen Schritte

Der Kern dieses Ansatzes liegt darin, das Risiko zu minimieren. Jede Änderung, die du vornimmst, ist isoliert und leicht nachvollziehbar. Wenn nach einem kleinen Refactoring ein Fehler auftritt, weißt du sofort, wo du suchen musst. Du musst nicht hunderte von geänderten Dateien durchforsten, sondern nur die letzte kleine Anpassung. Das macht den Prozess nicht nur sicherer, sondern auch psychologisch viel weniger belastend.

Die Arbeit mit Versionskontrolle wie Git ist hierbei dein wichtigstes Werkzeug. Die Regel lautet: Mache eine kleine, logische Änderung, teste sie und committe sie. Zum Beispiel: Ersetze alle `<b>`-Tags durch `<strong>`-Tags auf einer Seite. Testen. Commit. Nächster Schritt: Strukturiere den Footer mit einem `<footer`>-Element. Testen. Commit. Dieser atomare Ansatz gibt dir ein Sicherheitsnetz. Geht etwas schief, kannst du jederzeit zum letzten funktionierenden Zustand zurückkehren.

#### Eine Strategie entwickeln: Wo anfangen?

Bevor du die erste Zeile Code anfasst, brauchst du einen Plan. Ein unkoordiniertes Vorgehen führt schnell zu Chaos. Deine Strategie sollte auf einer gründlichen Analyse des bestehenden Codes basieren.

1.  **Bestandsaufnahme machen:** Schau dir das Projekt genau an. Welche archaischen Techniken werden am häufigsten verwendet? Sind es Layout-Tabellen? Inline-JavaScript-Handler wie `onclick`? Exzessive Nutzung von `<div>`s, wo semantische Elemente besser wären? Erstelle eine Liste der "Code Smells" und priorisiere sie.
2.  **Die "Low-Hanging Fruits" identifizieren:** Beginne mit den einfachsten Änderungen, die den größten Nutzen bringen. Das Ersetzen von rein präsentationsbezogenen Tags ist oft ein guter Startpunkt. Diese Änderungen sind meist risikoarm und können oft sogar projektweit mit einer intelligenten Suchen-und-Ersetzen-Funktion durchgeführt werden.
3.  **Struktur vor Präsentation:** Konzentriere dich zunächst darauf, die Dokumentenstruktur zu verbessern. Die Umstellung von einem Tabellenlayout auf ein semantisches Layout mit `<header>`, `<nav>`, `<main>` und `<footer>` ist ein großer, aber fundamental wichtiger Schritt. Auch wenn sich das visuelle Erscheinungsbild dadurch zunächst kaum ändert (da das CSS noch auf die alte Struktur abzielt), legst du damit das Fundament für alles Weitere.
4.  **Komponente für Komponente vorgehen:** Statt zu versuchen, die gesamte Website auf einmal zu modernisieren, nimm dir wiederkehrende Komponenten vor. Beginne mit dem globalen Header, dann dem Footer, dann der Navigation. Danach kannst du dich kleineren, wiederverwendbaren Blöcken wie Teaser-Boxen, Formularen oder Bildergalerien widmen.

#### Praktische Umsetzung: Vom Alten zum Neuen

Schauen wir uns einige typische Szenarien an und wie du sie schrittweise angehen kannst.

##### Schritt 1: Einfache semantische Ersetzungen

Dies sind die einfachsten Gewinne. Du ersetzt veraltete, rein stilistische Tags durch ihre modernen, semantischen Gegenstücke.

**Vorher:**
```html
<p>
  <b>Wichtiger Hinweis:</b> Die Anmeldefrist endet bald. 
  Bitte beachte auch die <i>neuen</i> Teilnahmebedingungen.
</p>
```

Die Tags `<b>` und `<i>` beschreiben nur, wie der Text aussehen soll (fett und kursiv), aber nicht, warum. Die korrekte semantische Alternative teilt dem Browser und assistiven Technologien wie Screenreadern die Bedeutung des Textes mit.

**Nachher:**
```html
<p>
  <strong>Wichtiger Hinweis:</strong> Die Anmeldefrist endet bald. 
  Bitte beachte auch die <em>neuen</em> Teilnahmebedingungen.
</p>
```

`<strong>` signalisiert eine starke Wichtigkeit, während `<em>` eine besondere Betonung anzeigt. Die Standarddarstellung im Browser ist zwar identisch, die semantische Bedeutung ist jedoch eine völlig andere und wertvollere.

##### Schritt 2: Die Befreiung aus dem Tabellen-Gefängnis

Layout-Tabellen waren vor 20 Jahren der Standard, um Webseiten zu strukturieren. Heute sind sie ein Albtraum für Barrierefreiheit, responsives Design und Wartbarkeit. Die Umstellung ist ein größerer Eingriff, aber unerlässlich.

**Vorher (ein typisches Zwei-Spalten-Layout):**
```html
<table width="100%" border="0" cellpadding="10" cellspacing="0">
  <tr>
    <td width="200" valign="top" bgcolor="#f0f0f0">
      <!-- Navigation -->
      <b>Navigation</b><br>
      <a href="/">Startseite</a><br>
      <a href="/about">Über uns</a><br>
    </td>
    <td valign="top">
      <!-- Hauptinhalt -->
      <h1>Willkommen auf unserer Seite!</h1>
      <p>Dies ist der Hauptinhalt...</p>
    </td>
  </tr>
</table>
```

Der erste Schritt ist, die logische Struktur zu erkennen: Es gibt eine Navigation und einen Hauptinhaltsbereich. Diese übersetzen wir in semantische HTML5-Elemente.

**Nachher (nur HTML, CSS folgt separat):**
```html
<div class="page-container">
  <nav class="main-navigation">
    <h2>Navigation</h2>
    <ul>
      <li><a href="/">Startseite</a></li>
      <li><a href="/about">Über uns</a></li>
    </ul>
  </nav>

  <main class="main-content">
    <h1>Willkommen auf unserer Seite!</h1>
    <p>Dies ist der Hauptinhalt...</p>
  </main>
</div>
```

Beachte, dass das visuelle Layout nun verschwunden ist. Im nächsten Schritt müsstest du das entsprechende CSS hinzufügen, um das Zwei-Spalten-Layout wiederherzustellen, zum Beispiel mit Flexbox oder Grid.

```css
.page-container {
  display: flex;
  gap: 20px;
}

.main-navigation {
  flex: 0 0 200px;
  background-color: #f0f0f0;
  padding: 10px;
}
```

Dieser zweistufige Prozess – erst HTML-Struktur korrigieren, dann CSS anpassen – ist typisch für die schrittweise Modernisierung. Du trennst sauber die Belange von Struktur und Darstellung.

##### Schritt 3: Inline-Styles und -Attribute auslagern

Ein weiteres Relikt aus alten Zeiten sind präsentationsbezogene Attribute und Inline-Styles direkt im HTML. Sie vermischen Struktur mit Darstellung und machen jede globale Designänderung zur Qual.

**Vorher:**
```html
<h2 align="center" style="color: blue; font-family: Arial, sans-serif;">
  Unsere Produkte
</h2>
<p>
  <font color="red" size="2">Achtung: Sonderangebot!</font>
</p>
```

Das Ziel ist es, das HTML komplett von Stilinformationen zu befreien und diese stattdessen über Klassen in einer zentralen CSS-Datei zu steuern.

**Nachher (HTML):**
```html
<h2 class="section-title text-center">
  Unsere Produkte
</h2>
<p>
  <span class="notice notice-special-offer">Achtung: Sonderangebot!</span>
</p>
```

**Nachher (CSS):**
```css
.section-title {
  color: blue;
  font-family: Arial, sans-serif;
}

.text-center {
  text-align: center;
}

.notice {
  font-size: 0.875rem; /* Entspricht ca. size="2" */
}

.notice-special-offer {
  color: red;
  font-weight: bold; /* Oft ist hier auch semantische Stärke gemeint */
}
```
Durch die Verwendung von Klassen wird dein HTML sauberer und beschreibt nur noch, *was* etwas ist (z.B. ein `section-title` oder ein `notice`), nicht, *wie* es aussieht. Das Design kannst du nun an einer einzigen Stelle, in deiner CSS-Datei, ändern.

#### Der Weg ist das Ziel

Die schrittweise Modernisierung ist kein Projekt mit einem festen Enddatum, sondern eher eine kontinuierliche Praxis. Du verbesserst den Code in dem Moment, in dem du ihn anfasst. Wenn du eine neue Funktion implementierst oder einen Fehler in einem alten Teil der Website behebst, nimm dir fünf Minuten extra Zeit, um das umliegende HTML ein wenig aufzuräumen. Ersetze ein paar `<div>`s durch `<section>` oder `<article>`, füge fehlende `<label>`-Tags in einem Formular hinzu oder lagere einen Inline-Style aus.

Dieser Ansatz, oft auch als "Pfadfinder-Regel" ("Hinterlasse den Campingplatz sauberer, als du ihn vorgefunden hast") bezeichnet, sorgt dafür, dass deine Codebasis mit der Zeit organisch besser wird, anstatt weiter zu verfallen. Es ist eine nachhaltige Strategie, die den Wert deines Projekts langfristig sichert, ohne den laufenden Betrieb durch riskante Mammutprojekte zu gefährden. Jeder kleine Schritt bringt dich näher an einen modernen, wartbaren und zugänglichen Code.
