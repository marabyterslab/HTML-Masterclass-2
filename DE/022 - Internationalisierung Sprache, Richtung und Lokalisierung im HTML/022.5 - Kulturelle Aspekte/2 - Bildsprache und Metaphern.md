# Bildsprache und Metaphern

### Bildsprache und Metaphern: Mehr als nur Worte

Stell dir vor, du betrittst eine Website und siehst ein Sparschwein-Symbol neben einem Angebot. In vielen westlichen Kulturen, insbesondere in Deutschland, verstehst du sofort: Hier geht es ums Sparen, um Geld, um einen guten Deal. Das Sparschwein ist eine tief verankerte Metapher für finanzielle Vorsorge. Doch was passiert, wenn ein Nutzer aus einer Kultur, in der Schweine als unrein gelten, diese Seite besucht? Die gut gemeinte Metapher verfehlt nicht nur ihr Ziel, sie kann sogar negative Assoziationen hervorrufen.

Dieses einfache Beispiel zeigt die enorme Kraft und das gleichzeitige Risiko von Bildsprache und Metaphern im Web. Sie sind mächtige Werkzeuge, um komplexe Ideen schnell und emotional verständlich zu machen. Sie schaffen Abkürzungen im Gehirn deines Nutzers und bauen eine Verbindung auf, die reiner Text nur schwer erreichen kann. Doch diese Abkürzungen sind nicht universell. Sie sind das Ergebnis gemeinsamer kultureller Erfahrungen, Geschichten und Werte. Wenn du international agierst, betrittst du ein Feld, auf dem diese gemeinsamen Erfahrungen auseinanderdriften.

#### Die kulturelle Codierung von Symbolen

Jedes Icon, jedes Bild, jede Farbwahl auf deiner Website ist kulturell codiert. Als Entwickler denkst du vielleicht primär in Funktionalität, aber für den Nutzer ist die Benutzeroberfläche eine visuelle Erzählung. Betrachten wir einige gängige Beispiele:

*   **Farben:** Die Symbolik von Farben ist eines der bekanntesten Minenfelder der Internationalisierung. Während Weiß in westlichen Ländern für Reinheit, Hochzeit und Frieden steht, ist es in vielen Teilen Asiens die Farbe der Trauer und des Todes. Rot kann in Europa und Nordamerika Gefahr, Stopp oder Fehler signalisieren, aber auch Liebe und Leidenschaft. In China hingegen ist es die Farbe des Glücks, des Wohlstands und der Feste. Eine Fehlermeldung in leuchtendem Rot könnte dort also Verwirrung stiften, während ein roter "Kaufen"-Button vielleicht besonders einladend wirkt.

*   **Tiere und Objekte:** Wir haben das Sparschwein bereits erwähnt. Ein anderes Beispiel ist die Eule. In der westlichen Welt symbolisiert sie Weisheit und Wissen. In Teilen Afrikas und des Nahen Ostens wird sie jedoch mit Unglück und bösen Omen in Verbindung gebracht. Eine Wissensdatenbank mit einer Eule im Logo könnte dort unbewusst ein Gefühl des Unbehagens auslösen. Selbst der allgegenwärtige „Daumen hoch“ ist nicht universell positiv. In einigen Ländern des Nahen Ostens, Westafrikas und Südamerikas ist diese Geste eine schwere Beleidigung.

*   **Gesten und Menschen:** Die Darstellung von Menschen ist besonders heikel. Stockfotos, die ein diverses Team in einem modernen Büro in San Francisco zeigen, repräsentieren nicht die Arbeitswelt aller deiner Nutzer. Kleidung, Gestik und die Art der Interaktion zwischen Personen auf Bildern können in verschiedenen Kulturen unterschiedlich interpretiert werden. Eine lockere, freundschaftliche Umarmung zwischen Kollegen mag in einer Kultur normal sein, in einer anderen aber als unangemessen empfunden werden.

#### Von der visuellen zur sprachlichen Metapher

Was für Bilder und Symbole gilt, setzt sich nahtlos in der Sprache fort. Redewendungen und Metaphern sind das Salz in der Suppe einer jeden Sprache, aber sie sind selten direkt übersetzbar. Eine deutsche Website könnte einen erfolgreichen Projektabschluss mit der Überschrift „Den Nagel auf den Kopf getroffen!“ feiern. Eine wörtliche Übersetzung ins Englische – „You hit the nail on the head!“ – funktioniert hier zufällig. Aber was ist mit „Das ist nicht das Gelbe vom Ei“? Eine wörtliche Übersetzung wäre für die meisten Menschen auf der Welt reines Kauderwelsch.

Im Webdesign betrifft das vor allem die sogenannte „Microcopy“: die Beschriftungen von Buttons, Fehlermeldungen, Platzhaltertexte und kleine Hilfestellungen. Eine verspielte, metaphorische Sprache, die in einer Kultur als charmant und markenbildend empfunden wird, kann in einer anderen als unprofessionell, verwirrend oder gar respektlos wahrgenommen werden. Eine Kultur, die Direktheit und Klarheit schätzt (wie die deutsche), bevorzugt vielleicht einen Button mit der klaren Aufschrift „In den Warenkorb legen“. Eine andere Kultur schätzt eventuell eine emotionalere, bildhaftere Sprache wie „Ich will das haben!“.

#### Praktische Lösungsansätze für deine Entwicklungsarbeit

Als Entwickler bist du nicht nur für den Code verantwortlich, sondern auch für die Schaffung einer flexiblen Struktur, die kulturelle Anpassungen ermöglicht. Es geht nicht darum, dass du zum Experten für jede Kultur der Welt wirst. Es geht darum, deine Architektur so zu bauen, dass Experten für Lokalisierung – Übersetzer, Kulturanthropologen, lokale Marketing-Teams – ihre Arbeit effektiv erledigen können.

**1. Entkopple Inhalte und Darstellung**

Eine der fundamentalsten Regeln ist es, visuelle, kulturabhängige Elemente nicht fest im Code oder im CSS zu verankern.

Ein schlechtes Beispiel wäre, ein Icon direkt im CSS als `background-image` für eine generische Klasse zu definieren:

```css
/* Schlecht: Fest verdrahtet und schwer zu lokalisieren */
.icon-save {
  background-image: url('../images/floppy-disk.svg');
  width: 16px;
  height: 16px;
}
```
Die Floppy-Diskette ist selbst eine aussterbende Metapher. Für jüngere Generationen hat sie keinerlei Bedeutung mehr. In einem internationalen Kontext kommt hinzu, dass das Symbol selbst vielleicht angepasst werden muss.

Ein besserer Ansatz ist, die Sprach- und Ländereinstellung zu nutzen, um spezifische Stile anzuwenden. Das `lang`-Attribut im `<html>`-Tag ist hier dein bester Freund. Mit der CSS-Pseudoklasse `:lang()` kannst du unterschiedliche Stile für unterschiedliche Sprachen definieren.

Stell dir vor, du hast ein Icon, das je nach Kulturkreis ausgetauscht werden soll. Dein HTML bleibt dabei gleich:

```html
<!-- Seite auf Deutsch -->
<html lang="de">
<body>
  <button class="button-save">
    <span class="icon icon-save" aria-hidden="true"></span>
    Speichern
  </button>
</body>
</html>

<!-- Seite auf Japanisch -->
<html lang="ja">
<body>
  <button class="button-save">
    <span class="icon icon-save" aria-hidden="true"></span>
    保存 (Hozon)
  </button>
</body>
</html>
```
Im CSS kannst du nun gezielt die Darstellung anpassen:

```css
/* Allgemeines Icon-Styling */
.icon-save {
  display: inline-block;
  width: 20px;
  height: 20px;
  background-repeat: no-repeat;
  background-size: contain;
}

/* Spezifische Icons pro Sprache */
.icon-save:lang(de) {
  background-image: url('../images/de/save-icon.svg');
}

.icon-save:lang(ja) {
  background-image: url('../images/ja/save-icon.svg');
}

.icon-save:lang(en) {
  background-image: url('../images/en/save-icon.svg');
}
```
Dieser Ansatz ermöglicht es, die visuellen Assets (Bilder, Icons) getrennt vom HTML-Markup und der allgemeinen CSS-Logik zu verwalten. Ein Lokalisierungsteam kann nun einfach die Bilder im Ordner `/images/ja/` austauschen, ohne den Code anfassen zu müssen.

**2. Asset-Management-Strategien**

Lege eine klare Ordnerstruktur für lokalisierte Assets an. Eine bewährte Methode ist die Verwendung von Locale-Codes (z. B. `de-DE`, `en-US`, `ja-JP`) in deinen Pfaden:

```
/assets/
  /images/
    /de-DE/
      header-background.jpg
      promo-image.png
    /ja-JP/
      header-background.jpg
      promo-image.png
  /icons/
    /de-DE/
      save.svg
    /ja-JP/
      save.svg
```
Dein Backend oder dein Build-Prozess kann dann basierend auf der ausgewählten Sprache des Nutzers den korrekten Pfad zu den Assets generieren.

**3. Transkreation statt reiner Übersetzung**

Erkenne an, dass eine 1:1-Übersetzung oft nicht ausreicht. Das Konzept, das du hier anwenden musst, nennt sich **Transkreation**. Es ist eine Mischung aus „Translation“ (Übersetzung) und „Creation“ (Schöpfung). Bei der Transkreation wird nicht nur der Text wörtlich übersetzt, sondern die gesamte Botschaft – inklusive ihrer Tonalität, Bildsprache und emotionalen Wirkung – wird für den Zielmarkt neu erschaffen.

Das Sparschwein-Beispiel von vorhin würde bei einer Transkreation für den Nahen Osten vielleicht durch ein Bild von einer Dattelpalme ersetzt, die als Symbol für Wohlstand und Wachstum gilt. Die Metapher „Sparen“ wird also nicht übersetzt, sondern durch eine kulturell äquivalente Metapher ersetzt, die das gleiche Gefühl von Sicherheit und Gewinn vermittelt.

Deine Rolle als Entwickler ist es, die technischen Systeme zu schaffen, die diese Art von tiefgreifender Anpassung zulassen. Das kann bedeuten, dass nicht nur Textelemente in einer Übersetzungsdatenbank liegen, sondern auch Bild-URLs, Icon-Identifier oder sogar ganze HTML-Struktur-Snippets, die je nach Region ausgetauscht werden können.

Letztendlich geht es bei der Berücksichtigung von Bildsprache und Metaphern um Empathie. Es geht darum, zu verstehen, dass deine Wahrnehmung der Welt nicht die einzig gültige ist. Eine international erfolgreiche Website fühlt sich für jeden Nutzer so an, als sei sie speziell für ihn und seine Kultur geschaffen worden. Sie spricht seine Sprache – nicht nur in Worten, sondern auch in Bildern, Farben und Symbolen. Deine Aufgabe ist es, das technische Fundament zu legen, damit diese globale Konversation reibungslos stattfinden kann.
