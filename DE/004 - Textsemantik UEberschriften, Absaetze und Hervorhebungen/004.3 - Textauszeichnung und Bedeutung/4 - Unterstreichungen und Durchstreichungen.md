# Unterstreichungen und Durchstreichungen

### Unterstreichungen und Durchstreichungen: Mehr als nur Stil

Wenn du an unterstrichenen oder durchgestrichenen Text im Web denkst, kommen dir wahrscheinlich sofort visuelle Effekte in den Sinn. Eine Unterstreichung hebt etwas hervor, eine Durchstreichung signalisiert, dass etwas nicht mehr gültig ist. Lange Zeit war das auch in HTML die ganze Geschichte. Tags wie `<u>` (underline) und `<s>` (strikethrough) waren reine Stil-Anweisungen an den Browser: „Zeichne hier eine Linie drunter“ oder „Zeichne hier eine Linie durch“.

Mit der Entwicklung von HTML5 hat sich diese Sichtweise grundlegend geändert. Der Fokus liegt nun auf der **semantischen Bedeutung** – also auf dem „Warum“ und nicht nur auf dem „Wie“. Ein Tag sollte dem Browser (und damit auch Suchmaschinen oder Screenreadern) mitteilen, welche Bedeutung ein bestimmter Textabschnitt hat. Die rein visuelle Gestaltung ist heute die Aufgabe von CSS.

Lass uns die modernen, semantischen Rollen dieser alten Bekannten und ihrer Verwandten genauer betrachten.

#### Das `<u>`-Element: Eine neue Rolle für die Unterstreichung

Das `<u>`-Element hat eine der interessantesten Wandlungen in der HTML-Geschichte durchgemacht. Früher wurde es einfach verwendet, um Text zu unterstreichen. Das Problem dabei war, dass unterstrichener Text im Web universell als Link verstanden wird. Die Verwendung von `<u>` für nicht-verlinkten Text führte also schnell zu Verwirrung bei den Nutzern. Aus diesem Grund wurde das Element lange Zeit als „schlechter Stil“ angesehen und man riet von seiner Verwendung ab.

In HTML5 wurde dem `<u>`-Element jedoch eine neue, sehr spezifische semantische Bedeutung zugewiesen: die Kennzeichnung einer **nicht-textuellen Anmerkung** (non-textual annotation). Das klingt erst einmal kompliziert, aber die Anwendungsfälle sind recht klar. Du verwendest `<u>`, um Text hervorzuheben, der sich stilistisch oder qualitativ vom umgebenden Text unterscheidet, ohne ihm eine besondere Wichtigkeit oder Betonung zu verleihen.

Der häufigste Anwendungsfall, den du unbewusst schon kennst, ist die Markierung von **Rechtschreibfehlern**. Viele Texteditoren oder Browser-Plugins unterstreichen falsch geschriebene Wörter mit einer roten Wellenlinie. Würde man dies in HTML semantisch korrekt auszeichnen, wäre das `<u>`-Element die richtige Wahl.

```html
<p>Mein Computer hat ein Problem mit der Rechtschreibkorrektur. Er markiert ständig das Wort <u>Feler</u> als falsch.</p>
```

Ein anderer legitimer Anwendungsfall ist die Kennzeichnung von Eigennamen in Texten, in denen diese Konvention üblich ist, beispielsweise bei der Annotation von chinesischen Namen, um sie von anderen Wörtern abzugrenzen.

```html
<p>In diesem Absatz sprechen wir über <u>Li Na</u>, eine berühmte Tennisspielerin.</p>
```

**Wann du `<u>` nicht verwenden solltest:**

*   **Zur Betonung:** Wenn du ein Wort betonen möchtest, nutze das `<em>`-Element (emphasis).
*   **Für Wichtigkeit:** Um anzuzeigen, dass etwas besonders wichtig ist, ist `<strong>` die korrekte Wahl.
*   **Für Titel:** Überschriften haben ihre eigenen Tags (`<h1>` bis `<h6>`).
*   **Wenn es wie ein Link aussehen könnte:** Vermeide `<u>` immer dann, wenn auch nur die geringste Gefahr besteht, dass Nutzer den Text für einen anklickbaren Link halten.

Wenn du Text aus rein gestalterischen Gründen unterstreichen möchtest, ist CSS die richtige Adresse. Mit der Eigenschaft `text-decoration: underline;` erreichst du denselben visuellen Effekt, ohne dem Text eine falsche semantische Bedeutung zu geben.

#### Durchgestrichener Text: Der Unterschied zwischen „falsch“ und „gelöscht“

Auch für durchgestrichenen Text gibt es in HTML zwei verschiedene Elemente mit feinen, aber wichtigen semantischen Unterschieden: `<s>` und `<del>`. Beide lassen den Text im Browser standardmäßig durchgestrichen erscheinen, aber sie erzählen eine unterschiedliche Geschichte über den Inhalt.

##### Das `<s>`-Element: Nicht mehr relevant oder korrekt

Das `<s>`-Element (strikethrough) verwendest du für Inhalte, die **nicht mehr korrekt oder nicht mehr relevant** sind. Es signalisiert, dass die Information veraltet ist, aber aus einem bestimmten Grund im Dokument verbleiben soll, zum Beispiel um einen Kontext zu wahren.

Ein klassisches Beispiel hierfür sind Preise in einem Onlineshop. Der alte, höhere Preis ist nicht mehr gültig, wird aber oft neben dem neuen Preis angezeigt, um das Angebot attraktiver zu machen.

```html
<p>Sonderangebot!</p>
<p>Kopfhörer-Modell X2000: <s>99,95 €</s> nur noch <strong>79,95 €</strong>!</p>
```

Ein anderes Beispiel könnte eine To-do-Liste sein, in der erledigte Aufgaben durchgestrichen werden. Die Aufgabe ist erledigt (also nicht mehr relevant für das, was noch zu tun ist), aber sie bleibt sichtbar, um den Fortschritt zu dokumentieren.

```html
<ul>
  <li><s>Projektplanung abschließen</s></li>
  <li>Kundenfeedback einholen</li>
  <li>Präsentation vorbereiten</li>
</ul>
```

Der Inhalt innerhalb von `<s>`-Tags ist also nicht falsch im Sinne eines Fehlers, sondern einfach überholt.

##### Das `<del>`-Element: Explizit gelöschter Inhalt

Das `<del>`-Element (delete) hat eine präzisere und stärkere Bedeutung. Es kennzeichnet Text, der aus dem Dokument **entfernt oder gelöscht** wurde. Es wird typischerweise verwendet, um Änderungen an einem Dokument nachzuverfolgen, ähnlich wie die „Änderungen nachverfolgen“-Funktion in einem Textverarbeitungsprogramm.

Das `<del>`-Element hat ein direktes Gegenstück: das `<ins>`-Element (insert), das Text kennzeichnet, der hinzugefügt wurde. Zusammen bilden sie ein mächtiges Paar, um Bearbeitungen und Versionen eines Textes darzustellen.

Stell dir vor, du überarbeitest einen Satz in einem Blogbeitrag und möchtest für die Leser transparent machen, was sich geändert hat.

```html
<p>Unsere Konferenz findet am <del>Dienstag</del><ins>Mittwoch</ins> statt.</p>
```

Dieser Code teilt dem Browser (und assistiven Technologien) mit: „Das Wort ‚Dienstag‘ wurde gelöscht und durch das Wort ‚Mittwoch‘ ersetzt.“ Browser stellen `<del>`-Inhalte standardmäßig durchgestrichen und `<ins>`-Inhalte unterstrichen dar, um diesen Bearbeitungsprozess visuell zu verdeutlichen.

Die Attribute `cite` und `datetime` können diesen Elementen zusätzlichen Kontext geben. `cite` kann auf eine URL verweisen, die die Änderung erklärt, und `datetime` gibt den Zeitpunkt der Änderung an.

```html
<p>
  Das Team besteht nun aus
  <del datetime="2023-10-26T10:00:00Z">fünf</del>
  <ins datetime="2023-10-26T10:01:00Z" cite="/aenderungs-log.html#team-groesse">sechs</ins>
  Experten.
</p>
```

**Der entscheidende Unterschied:**

*   Verwende `<s>`, wenn etwas seinen Wert oder seine Relevanz verloren hat (ein alter Preis, eine erledigte Aufgabe).
*   Verwende `<del>`, um eine explizite Löschung im Rahmen einer Textbearbeitung zu markieren, oft in Kombination mit `<ins>`.

#### Die Gestaltung bleibt bei CSS

Es ist wichtig, immer wieder zu betonen: Die semantischen Tags in HTML definieren die *Bedeutung* des Inhalts, nicht sein Aussehen. Auch wenn Browser Standard-Stile für `<u>`, `<s>`, `<del>` und `<ins>` haben, liegt die volle Kontrolle über die Darstellung bei dir – und zwar mit CSS.

Möchtest du gelöschten Text nicht durchstreichen, sondern rot und leicht ausgegraut darstellen? Kein Problem.

```css
del {
  text-decoration: none; /* Entfernt die Standard-Durchstreichung */
  color: #c00;
  opacity: 0.7;
}

ins {
  text-decoration: none; /* Entfernt die Standard-Unterstreichung */
  background-color: #d4edda; /* Heller grüner Hintergrund */
  color: #155724;
}
```

Mit diesem CSS-Code wird der zuvor erwähnte Satz „Unsere Konferenz findet am <del>Dienstag</del><ins>Mittwoch</ins> statt.“ ganz anders dargestellt, aber die semantische Information für Maschinen bleibt dieselbe. Diese Trennung von Struktur (HTML) und Präsentation (CSS) ist eines der fundamentalen Prinzipien der modernen Webentwicklung. Sie macht deinen Code sauberer, flexibler und zugänglicher.
