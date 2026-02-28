# WCAG-Richtlinien (Wahrnehmbar, Bedienbar, Verständlich, Robust)

### WCAG-Richtlinien (Wahrnehmbar, Bedienbar, Verständlich, Robust)

Wenn wir über Barrierefreiheit im Web sprechen, landen wir schnell bei den Web Content Accessibility Guidelines, kurz WCAG. Diese Richtlinien sind der international anerkannte Standard, der uns den Weg zu inklusiven digitalen Erlebnissen weist. Anstatt dich mit einer unüberschaubaren Liste von Einzelregeln zu überfordern, basieren die WCAG auf vier fundamentalen Prinzipien. Man kann sie sich wie die vier Säulen vorstellen, auf denen das gesamte Gebäude der digitalen Barrierefreiheit ruht. Wenn du diese vier Prinzipien verinnerlichst, entwickelst du ein intuitives Verständnis dafür, worauf es wirklich ankommt. Im Englischen werden sie oft mit dem Akronym POUR zusammengefasst: Perceivable, Operable, Understandable, Robust. Auf Deutsch übersetzen wir das mit: Wahrnehmbar, Bedienbar, Verständlich und Robust.

Lass uns diese vier Säulen genauer betrachten.

#### 1. Wahrnehmbar (Perceivable)

Das erste Prinzip ist vielleicht das offensichtlichste: Informationen und Bestandteile der Benutzeroberfläche müssen so dargestellt werden, dass Nutzer sie wahrnehmen können. „Wahrnehmen“ bedeutet hier weit mehr als nur „sehen“. Es schließt alle menschlichen Sinne mit ein. Wenn ein Inhalt nur über einen einzigen Sinneskanal zugänglich ist – zum Beispiel nur visuell –, schließt du automatisch all jene aus, die diesen Kanal nicht oder nur eingeschränkt nutzen können.

Deine Aufgabe ist es also, Alternativen bereitzustellen.

**Textalternativen für nicht-textuelle Inhalte**
Das klassischste Beispiel hierfür ist das `alt`-Attribut für Bilder. Ein blinder Nutzer, der einen Screenreader verwendet, kann ein Bild nicht sehen. Die Software liest ihm stattdessen den Alternativtext vor. Dieser Text sollte den Inhalt und die Funktion des Bildes prägnant beschreiben.

```html
<!-- Gut: Der Alternativtext beschreibt, was auf dem Bild zu sehen ist. -->
<img src="golden-retriever.jpg" alt="Ein Golden Retriever fängt einen roten Ball im Sprung.">

<!-- Schlecht: Der Alternativtext ist nicht aussagekräftig. -->
<img src="golden-retriever.jpg" alt="Bild">
```

Ist ein Bild rein dekorativ und trägt keine Information, lässt du das `alt`-Attribut leer (`alt=""`). Dadurch wird es von assistiven Technologien ignoriert und stört den Lesefluss nicht.

```html
<!-- Ein dekoratives Trennelement, das ignoriert werden soll. -->
<img src="wellen-muster.svg" alt="">
```

Dieses Prinzip gilt aber nicht nur für Bilder. Ein Video benötigt Untertitel für gehörlose oder schwerhörige Nutzer und idealerweise eine Audiodeskription für blinde Nutzer. Eine Audiodatei, wie ein Podcast, sollte durch ein Transkript ergänzt werden, also eine Abschrift des Gesprochenen.

**Anpassbare Darstellung**
Zur Wahrnehmbarkeit gehört auch, dass sich Inhalte an die Bedürfnisse der Nutzer anpassen lassen. Das bedeutet vor allem, dass deine Webseite mit semantisch korrektem HTML aufgebaut sein muss. Wenn du Überschriften mit `<h1>` bis `<h6>`, Absätze mit `<p>` und Listen mit `<ul>` oder `<ol>` auszeichnest, gibst du der Seite eine klare Struktur. Ein Screenreader kann diese Struktur erkennen und es dem Nutzer ermöglichen, von Überschrift zu Überschrift zu springen, um sich einen schnellen Überblick zu verschaffen. Verwendest du stattdessen nur `<div>`-Elemente mit CSS-Klassen, um eine Überschrift optisch hervorzuheben, geht diese strukturelle Information verloren. Für assistive Technologien ist es dann nur noch ein unstrukturierter Block aus Text.

**Kontraste**
Auch die visuelle Wahrnehmbarkeit ist entscheidend. Text muss sich ausreichend vom Hintergrund abheben, damit er auch von Menschen mit Sehschwäche oder Farbfehlsichtigkeit gut gelesen werden kann. Ein hellgrauer Text auf weißem Hintergrund mag minimalistisch aussehen, ist für viele Menschen aber schlicht unlesbar. Die WCAG geben hier klare Mindestwerte für Farbkontraste vor.

#### 2. Bedienbar (Operable)

Das zweite Prinzip stellt sicher, dass Nutzer mit der Webseite interagieren können. Alle interaktiven Elemente müssen zugänglich und steuerbar sein, und zwar nicht nur mit einer Maus.

**Tastaturbedienbarkeit**
Dies ist einer der wichtigsten Aspekte der Bedienbarkeit. Jeder interaktive Bestandteil deiner Webseite – Links, Buttons, Formularfelder, Menüs – muss ausschließlich mit der Tastatur erreichbar und aktivierbar sein. Viele Menschen können oder wollen keine Maus benutzen, sei es aufgrund einer motorischen Einschränkung, weil sie fortgeschrittene Power-User sind oder weil ihr Trackpad gerade defekt ist.

Du kannst das ganz einfach selbst testen: Versuche, durch deine Webseite nur mit der Tabulator-Taste (zum Springen zum nächsten Element) und der Enter- oder Leertaste (zum Aktivieren) zu navigieren. Erreichst du jedes interaktive Element? Siehst du jederzeit deutlich, welches Element gerade den Fokus hat (oft durch einen Rahmen gekennzeichnet)?

Die Verwendung von nativem, semantischem HTML hilft dir hier enorm. Ein `<button>`-Element oder ein `<a>`-Link ist von Natur aus per Tastatur fokussierbar und aktivierbar. Wenn du hingegen ein `<div>`-Element mit einem JavaScript-`onclick`-Handler versiehst, um es wie einen Button agieren zu lassen, musst du dich selbst darum kümmern, es in die Tab-Reihenfolge aufzunehmen (mit `tabindex="0"`) und auf Tastendrücke reagieren zu lassen. Der einfachere und robustere Weg ist fast immer, das dafür vorgesehene HTML-Element zu verwenden.

```html
<!-- Schlecht: Nicht per Tastatur erreichbar oder aktivierbar. -->
<div class="pseudo-button" onclick="openDialog()">Einstellungen</div>

<!-- Gut: Von Natur aus bedienbar und für assistive Technologien als Button erkennbar. -->
<button onclick="openDialog()">Einstellungen</button>
```

**Genügend Zeit**
Nutzer benötigen unterschiedlich viel Zeit, um Inhalte zu lesen und Aufgaben zu erledigen. Inhalte, die sich bewegen, blinken oder automatisch aktualisieren, können extrem störend sein und für manche Menschen sogar Anfälle auslösen. Gib deinen Nutzern daher immer die Kontrolle. Ein Bilderkarussell sollte Pausen-, Vor- und Zurück-Buttons haben. Wenn eine Sitzung aus Sicherheitsgründen abläuft, warne den Nutzer vor und gib ihm die Möglichkeit, die Zeit zu verlängern.

**Einfache Navigation**
Eine klare und konsistente Navigation hilft allen Nutzern, sich auf deiner Seite zurechtzufinden. Ein sogenannter „Skip-Link“ ist hier eine wertvolle Hilfe. Das ist ein Link, der ganz am Anfang des HTML-Dokuments steht und oft visuell verborgen ist, bis er per Tastatur fokussiert wird. Er erlaubt es Tastaturnutzern, wiederkehrende Navigationsblöcke zu überspringen und direkt zum Hauptinhalt der Seite zu springen.

#### 3. Verständlich (Understandable)

Dieses Prinzip zielt auf die kognitive Barrierefreiheit ab. Es reicht nicht, wenn Inhalte wahrnehmbar und bedienbar sind – sie müssen auch verständlich sein. Das betrifft sowohl den Inhalt selbst als auch die Funktionsweise der Benutzeroberfläche.

**Lesbarkeit und Sprache**
Schreibe in einer klaren, einfachen Sprache und vermeide unnötig kompliziertes Vokabular oder Jargon, wo immer es möglich ist. Definiere Abkürzungen bei ihrer ersten Verwendung.

Ein entscheidender technischer Aspekt ist die korrekte Deklaration der Sprache deiner Seite. Mit dem `lang`-Attribut im `<html>`-Tag teilst du dem Browser und assistiven Technologien mit, in welcher Sprache der Inhalt verfasst ist. Das ist unerlässlich, damit ein Screenreader den Text mit der richtigen Aussprache und Betonung vorlesen kann.

```html
<html lang="de">
  <!-- ... -->
</html>
```

Wenn ein Teil deines Textes in einer anderen Sprache verfasst ist, solltest du auch diesen entsprechend auszeichnen:

```html
<p>
  Sein liebster Ausspruch war <span lang="fr">"C'est la vie"</span>.
</p>
```

**Vorhersehbarkeit**
Eine gute Webseite verhält sich konsistent und vorhersehbar. Die Navigation sollte auf jeder Seite an derselben Stelle sein und gleich funktionieren. Wenn ein Element wie ein Link aussieht, sollte es auch ein Link sein und zu einer anderen Seite oder einem anderen Seitenabschnitt führen. Eine unerwartete Änderung des Kontexts, wie das automatische Öffnen eines neuen Fensters ohne Vorwarnung, kann Nutzer verwirren und desorientieren.

**Hilfe bei der Eingabe und Fehlervermeidung**
Formulare sind ein häufiger Stolperstein. Um sie verständlich zu machen, braucht jedes Eingabefeld eine klare und immer sichtbare Beschriftung. Das `<label>`-Element ist hierfür dein wichtigstes Werkzeug. Verknüpfe es explizit über das `for`-Attribut mit der `id` des zugehörigen `<input>`-Elements.

```html
<label for="user-name">Benutzername:</label>
<input type="text" id="user-name" name="username">
```

Platzhaltertexte sind kein Ersatz für ein `<label>`, da sie verschwinden, sobald der Nutzer zu tippen beginnt, und oft einen schlechten Farbkontrast haben.

Wenn ein Nutzer einen Fehler macht, müssen die Fehlermeldungen hilfreich und präzise sein. Statt eines vagen „Fehlerhafte Eingabe“ solltest du genau beschreiben, was falsch ist und wie es korrigiert werden kann, zum Beispiel: „Das Passwort muss mindestens acht Zeichen lang sein.“

#### 4. Robust (Robust)

Das vierte Prinzip ist technischer Natur. Es besagt, dass Inhalte robust genug sein müssen, um von einer Vielzahl von Programmen – einschließlich assistiver Technologien – zuverlässig interpretiert werden zu können. Während sich die Technologien und Browser weiterentwickeln, muss deine Webseite funktionsfähig bleiben.

**Sauberes, valides HTML**
Die Grundlage für Robustheit ist sauberes, standardkonformes HTML. Moderne Browser sind extrem fehlerverzeihend und versuchen, auch aus kaputtem Code noch etwas Sinnvolles zu rendern. Assistive Technologien sind da oft weitaus strenger. Ein nicht geschlossenes Tag, falsch verschachtelte Elemente oder doppelte IDs können einen Screenreader komplett aus dem Takt bringen und Teile deiner Seite unzugänglich machen. Nutze regelmäßig einen HTML-Validator, um sicherzustellen, dass dein Code den Standards entspricht.

**Name, Rolle, Wert**
Jedes interaktive Element auf deiner Seite muss für assistive Technologien einen Namen, eine Rolle und gegebenenfalls einen Wert haben.
*   **Rolle:** Was ist das für ein Element? (z.B. ein Button, ein Link, ein Kontrollkästchen)
*   **Name:** Wofür ist es da? (z.B. „Suchen“, „Profil bearbeiten“)
*   **Wert/Zustand:** In welchem Zustand befindet es sich? (z.B. aktiviert/deaktiviert, eingeklappt/ausgeklappt)

Wenn du Standard-HTML-Elemente verwendest, bekommst du vieles davon geschenkt. Ein `<button>Senden</button>` hat automatisch die Rolle „Button“ und den Namen „Senden“.

Für komplexe, benutzerdefinierte Komponenten, die mit `<div>` und JavaScript gebaut werden (wie ein aufklappbares Akkordeon), reicht reines HTML oft nicht aus. Hier kommt ARIA (Accessible Rich Internet Applications) ins Spiel. Mit ARIA-Attributen kannst du die fehlenden semantischen Informationen ergänzen, um die Rolle (`role="button"`), den Namen (`aria-label="..."`) oder den Zustand (`aria-expanded="true"`) für assistive Technologien explizit zu definieren. ARIA ist jedoch ein mächtiges Werkzeug, das mit Bedacht eingesetzt werden sollte. Die erste Regel von ARIA lautet: Verwende es nicht, wenn es ein natives HTML-Element gibt, das die gleiche Funktion erfüllt.

Diese vier Prinzipien – Wahrnehmbar, Bedienbar, Verständlich und Robust – bilden das Fundament, auf dem du barrierefreie Webseiten baust. Sie sind keine Checkliste zum Abhaken, sondern eine Denkweise, die dich bei jeder Entscheidung leiten sollte.
