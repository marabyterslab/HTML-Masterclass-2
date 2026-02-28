# Unterstreichungen und Durchstreichungen

### Unterstreichungen und Durchstreichungen: Mehr als nur Dekoration

Auf den ersten Blick scheinen Unterstreichungen und Durchstreichungen rein visuelle Elemente zu sein – einfache Striche, die Text hervorheben oder entwerten. Im semantischen HTML geht es jedoch selten nur um das Aussehen. Es geht um die Bedeutung, das „Warum“. Warum ist ein Wort unterstrichen? Warum ist ein Satz durchgestrichen? Die HTML-Elemente, die wir für diese Effekte nutzen, tragen eine spezifische Bedeutung in sich, die weit über reine Dekoration hinausgeht. Dieses Kapitel beleuchtet die feinen, aber entscheidenden Unterschiede und zeigt dir, wann du zu welchem Werkzeug greifen solltest.

#### Der missverstandene Strich: Das `<u>`-Element

Das `<u>`-Element ist wohl eines der historisch am meisten missbrauchten Elemente in HTML. Sein Name leitet sich von „underline“ (unterstreichen) ab, und genau das tut es auch: Es stellt den enthaltenen Text unterstrichen dar. In den Anfangstagen des Webs, als die Trennung von Inhalt (HTML) und Darstellung (CSS) noch nicht konsequent gelebt wurde, nutzten Entwickler das `<u>`-Tag, um Text einfach nur zu unterstreichen – aus rein ästhetischen Gründen.

Das Problem dabei? Eine reine Unterstreichung ohne Kontext hat keine semantische Bedeutung. Sie sagt einem Browser, einem Screenreader oder einer Suchmaschine nichts darüber, *warum* dieser Text anders ist. Er ist einfach nur … unterstrichen.

Mit HTML5 wurde die Bedeutung des `<u>`-Elements daher neu und sehr spezifisch definiert. Es soll nicht mehr für stilistische Hervorhebungen verwendet werden. Stattdessen markiert es heute einen Textabschnitt, der sich stilistisch vom umgebenden Text unterscheidet, aber keine besondere Wichtigkeit oder Betonung impliziert. Die offizielle Definition spricht von einer „unartikulierten, nicht-textuellen Anmerkung“.

Das klingt kompliziert, aber die Anwendungsfälle sind recht klar:

1.  **Kennzeichnung von Eigennamen in chinesischem Text:** Im Chinesischen gibt es ein spezielles Unterstreichungszeichen (專名號), um Eigennamen zu markieren. Das `<u>`-Element ist hierfür die semantisch korrekte Wahl.
2.  **Hervorhebung von Rechtschreibfehlern:** Ein Texteditor, der in einem Browser läuft, könnte absichtlich falsch geschriebene Wörter mit `<u>` umschließen, um sie für den Benutzer als fehlerhaft zu kennzeichnen, oft dargestellt durch eine rote Wellenlinie (was via CSS gesteuert wird).

Ein Beispiel für den letzteren Fall könnte so aussehen:

```html
<p>Ich glaube, ich habe einen Schreibfeler gemacht.</p>
<!-- Ein Tool zur Rechtschreibprüfung könnte daraus Folgendes machen: -->
<p>Ich glaube, ich habe einen Schreib<u class="rechtschreibfehler">feler</u> gemacht.</p>
```

**Wann solltest du `<u>` also nicht verwenden?**
Fast immer. Wenn du ein Wort oder einen Satz aus stilistischen Gründen unterstreichen möchtest, weil du es für ein Designelement hältst, ist CSS die einzig richtige Wahl. Du nimmst dafür ein neutrales Element wie `<span>` und weist ihm die entsprechende Stilregel zu.

```html
<p>Ein besonders <span class="wichtiger-hinweis">wichtiger Hinweis</span> für dich.</p>
```

Und im zugehörigen CSS:

```css
.wichtiger-hinweis {
  text-decoration: underline;
}
```

Diese Trennung ist fundamental: HTML beschreibt die Bedeutung („dies ist ein Hinweis“), während CSS das Aussehen festlegt („dieser Hinweis soll unterstrichen sein“).

**Eine wichtige Warnung zur Barrierefreiheit:**
Im Web hat sich eine universelle Konvention etabliert: **Unterstrichener Text signalisiert einen Link.** Nutzer sind darauf konditioniert, auf unterstrichene Inhalte zu klicken. Wenn du Text unterstreichst, der kein Link ist, schaffst du Verwirrung und eine schlechte Benutzererfahrung, insbesondere für Menschen mit kognitiven Einschränkungen. Vermeide Unterstreichungen für nicht-interaktive Elemente daher, wo immer es geht.

#### Durchgestrichen, aber nicht vergessen: `<s>` und `<del>`

Ähnlich wie bei der Unterstreichung gibt es auch für durchgestrichenen Text mehrere HTML-Elemente. Und auch hier ist die semantische Bedeutung der entscheidende Faktor für die Wahl des richtigen Tags. Die beiden relevanten Elemente sind `<s>` und `<del>`.

##### `<s>`: Inhalte, die nicht mehr relevant sind

Das `<s>`-Element (von „strikethrough“) markiert Inhalte, die nicht mehr korrekt oder nicht mehr relevant sind. Die Information wird aber bewusst im Dokument belassen, weil sie Teil des Kontexts ist. Sie ist veraltet, aber nicht im eigentlichen Sinne „gelöscht“.

Der klassische Anwendungsfall sind Preise in einem Onlineshop oder zeitlich begrenzte Angebote:

```html
<p>Sonderangebot diese Woche!</p>
<ul>
  <li>Produkt A: <s>19,99 €</s> nur 9,99 €</li>
  <li>Produkt B: Nur für kurze Zeit verfügbar!</li>
</ul>
```

Hier ist der alte Preis von 19,99 € nicht mehr gültig, aber seine Anzeige gibt dem Nutzer den wichtigen Kontext, dass es sich um einen reduzierten Preis handelt. Der alte Preis wurde nicht aus dem Dokument „gelöscht“, er hat nur seine Relevanz verloren.

##### `<del>`: Inhalte, die gelöscht wurden

Das `<del>`-Element (von „delete“) hat eine stärkere und spezifischere Bedeutung. Es markiert Inhalt, der aus dem Dokument entfernt wurde. Es wird typischerweise verwendet, um Änderungen in einem Dokument nachzuverfolgen, ähnlich wie die „Änderungen nachverfolgen“-Funktion in einem Textverarbeitungsprogramm.

Stell dir vor, du überarbeitest einen Satz. Anstatt den alten Text einfach zu löschen, kannst du ihn mit `<del>` markieren, um die Änderung transparent zu machen.

```html
<p>Unsere Produkte sind <del>gut</del> hervorragend verarbeitet.</p>
```

Dieser Satz kommuniziert semantisch: „Das Wort ‚gut‘ stand hier ursprünglich, wurde aber entfernt und ersetzt.“

Das logische Gegenstück zu `<del>` ist das `<ins>`-Element (von „insert“), das hinzugefügten Inhalt markiert. Zusammen ergeben sie ein mächtiges Werkzeug, um Bearbeitungshistorien direkt im HTML-Code abzubilden:

```html
<p>
  Die Konferenz findet am
  <del>Dienstag, den 15. Oktober</del>
  <ins>Mittwoch, den 16. Oktober</ins>
  statt.
</p>
```

Browser stellen `<ins>`-Inhalte standardmäßig unterstrichen dar, was erneut die Gefahr der Verwechslung mit Links birgt. Hier ist es oft sinnvoll, das Aussehen via CSS anzupassen, zum Beispiel durch eine dezente Hintergrundfarbe.

Sowohl `<del>` als auch `<ins>` können zwei nützliche Attribute haben:

*   `cite`: Eine URL, die auf eine Ressource verweist, welche die Änderung erklärt. Das könnte ein Link zu einem Ticket in einem Projektmanagement-Tool oder ein Protokoll sein.
*   `datetime`: Ein Zeitstempel, der angibt, wann die Änderung vorgenommen wurde. Das Datum sollte im Format `YYYY-MM-DDThh:mm:ssZ` angegeben werden.

Ein voll ausgestattetes Beispiel sieht so aus:

```html
<p>
  Der Projektstatus wurde von
  <del datetime="2023-10-26T10:00:00Z" cite="/changes/ticket-123">In Bearbeitung</del>
  <ins datetime="2023-10-26T10:01:00Z" cite="/changes/ticket-123">Abgeschlossen</ins>
  geändert.
</p>
```

Diese Attribute sind für den Endnutzer nicht direkt sichtbar, liefern aber wertvolle Metadaten für Maschinen oder Skripte, die das Dokument verarbeiten.

##### Rein stilistisches Durchstreichen

Und was, wenn du etwas einfach nur aus ästhetischen Gründen durchstreichen möchtest? Vielleicht als ironisches Stilmittel in einem Blogbeitrag? Auch hier gilt: Wenn es keine semantische Bedeutung von „nicht mehr relevant“ oder „gelöscht“ gibt, ist CSS die richtige Wahl.

```html
<p>Ich würde das <span style="text-decoration: line-through;">niemals</span> tun.</p>
```

Hier transportiert die Durchstreichung keine maschinenlesbare Bedeutung, sondern dient ausschließlich der visuellen Betonung der ironischen Aussage.

#### Das Leitprinzip: Bedeutung vor Aussehen

Die Beispiele für Unter- und Durchstreichungen illustrieren eines der wichtigsten Prinzipien modernen Webdesigns: die strikte Trennung von Inhalt und Präsentation. HTML ist die Sprache, um die Struktur und die semantische Bedeutung deines Inhalts zu beschreiben. CSS ist das Werkzeug, um diesem Inhalt ein Aussehen zu verleihen.

Bevor du also ein Element wie `<u>`, `<s>` oder `<del>` verwendest, stelle dir immer die entscheidende Frage: **„Was möchte ich damit semantisch ausdrücken?“**

*   Will ich einen Rechtschreibfehler markieren? Dann ist `<u>` vielleicht korrekt.
*   Will ich einen alten Preis anzeigen? Dann ist `<s>` die richtige Wahl.
*   Will ich eine dokumentierte Änderung darstellen? Dann sind `<del>` und `<ins>` deine Werkzeuge.
*   Will ich einfach nur einen Strich durch oder unter dem Text, weil es gut aussieht? Dann gehört diese Anweisung unmissverständlich ins CSS.

Indem du dieses Prinzip verinnerlichst, schreibst du nicht nur sauberen und wartbaren Code, sondern erstellst auch Webseiten, die für alle zugänglicher, verständlicher und für Maschinen wie Suchmaschinen besser interpretierbar sind.
