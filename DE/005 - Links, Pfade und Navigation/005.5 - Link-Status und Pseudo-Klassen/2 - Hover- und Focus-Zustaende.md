# Hover- und Focus-Zustände

### Interaktion sichtbar machen: Hover- und Focus-Zustände

Stell dir vor, du gehst durch einen Raum voller Lichtschalter. Einige Schalter leuchten sanft, wenn du deine Hand in ihre Nähe bringst, noch bevor du sie berührst. Andere wiederum klicken hörbar und rasten in einer neuen Position ein, sobald du sie betätigst. Diese kleinen Rückmeldungen sind entscheidend. Sie bestätigen dir, dass deine Handlung eine Reaktion auslöst und dass das Objekt interaktiv ist.

Im Web ist es nicht anders. Eine Webseite ist eine Sammlung von interaktiven und nicht-interaktiven Elementen. Ein einfacher Textabsatz ist passiv, aber ein Link oder ein Button schreit förmlich danach, angeklickt zu werden. Damit der Benutzer diese Interaktivität nicht nur vermutet, sondern auch visuell bestätigt bekommt, gibt es Zustände. Zwei der wichtigsten Zustände, die du mit CSS gestalten kannst, sind der `:hover`- und der `:focus`-Zustand. Sie sind das digitale Äquivalent zum leuchtenden Lichtschalter und dem spürbaren Klick.

#### Der `:hover`-Zustand: Die digitale Annäherung

Der `:hover`-Zustand wird immer dann ausgelöst, wenn du den Mauszeiger über ein Element bewegst. Es ist die erste, subtile Bestätigung für den Nutzer: „Hey, dieses Element hier ist besonders. Du kannst damit etwas tun.“ Für Links und Buttons ist dieser Zustand praktisch unverzichtbar. Er schlägt eine Brücke zwischen dem Sehen eines Elements und der Entscheidung, darauf zu klicken.

Die CSS-Syntax dafür ist denkbar einfach. Du nimmst den Selektor des Elements, das du gestalten möchtest (zum Beispiel den `a`-Selektor für alle Links), und hängst die Pseudoklasse `:hover` direkt daran an.

Schauen wir uns ein einfaches Beispiel an. Wir haben einen Standardlink, der im unberührten Zustand blau und nicht unterstrichen ist.

```html
<a href="produkte.html">Unsere Produkte</a>
```

Mit CSS können wir nun definieren, wie dieser Link aussehen soll, wenn der Mauszeiger darüber schwebt.

```css
/* Grundstil für alle Links */
a {
  color: #007bff;
  text-decoration: none;
  font-weight: bold;
}

/* Stil, der nur bei Mouse-Over aktiv wird */
a:hover {
  color: #0056b3;
  text-decoration: underline;
}
```

In diesem Beispiel passiert Folgendes: Standardmäßig ist der Link kräftig blau und hat keine Unterstreichung. Sobald du aber mit der Maus darüberfährst, ändert sich die Farbe zu einem dunkleren Blau und es erscheint eine Unterstreichung. Der Nutzer erhält sofortiges, klares Feedback.

Die Möglichkeiten sind hierbei fast grenzenlos. Du kannst nicht nur Farben und Textdekorationen ändern, sondern praktisch jede CSS-Eigenschaft:

*   `background-color`: Eine subtile Hintergrundfarbe für einen Button hinzufügen.
*   `transform`: Das Element leicht vergrößern (`transform: scale(1.1);`).
*   `box-shadow`: Einen leichten Schatten hinzufügen, um das Element „anheben“ zu lassen.
*   `opacity`: Andere Elemente leicht ausblenden, um den Fokus auf das gehoverte Element zu lenken.

Ein wichtiger Aspekt des `:hover`-Zustands ist jedoch seine Limitierung: Er funktioniert naturgemäß nur mit einem Zeigegerät wie einer Maus oder einem Trackpad. Auf Touch-Geräten wie Smartphones oder Tablets gibt es kein „Schweben“. Ein Nutzer kann ein Element nur direkt antippen. Und für Menschen, die aus verschiedenen Gründen auf eine Tastaturnavigation angewiesen sind, ist der `:hover`-Zustand ebenfalls irrelevant. Hier kommt der zweite wichtige Zustand ins Spiel: `:focus`.

#### Der `:focus`-Zustand: Der Schlüssel zur Barrierefreiheit

Der `:focus`-Zustand tritt ein, wenn ein Element aktiv ausgewählt wird. Dies geschieht in der Regel auf zwei Wegen:

1.  Der Nutzer klickt auf ein interaktives Element wie ein Eingabefeld (`<input>`).
2.  Der Nutzer navigiert mit der Tastatur (meistens mit der Tab-Taste) durch die interaktiven Elemente einer Seite.

Während der erste Punkt eher für Formulare relevant ist, ist der zweite Punkt für die gesamte Navigation und Zugänglichkeit (Accessibility) einer Webseite von fundamentaler Bedeutung. Nutzer ohne Maus, zum Beispiel Menschen mit motorischen Einschränkungen oder Power-User, die Tastenkürzel bevorzugen, verlassen sich darauf, dass sie jederzeit sehen können, welches Element gerade den „Fokus“ hat.

Standardmäßig zeigen die meisten Browser ein fokussiertes Element durch einen Umriss (eine `outline`) an. Dieser blaue oder schwarze Rahmen ist oft das Einzige, was einem Tastaturnutzer anzeigt, wo er sich gerade auf der Seite befindet.

Leider ist eine der ersten Dinge, die viele Entwickler lernen, diesen Umriss aus ästhetischen Gründen zu entfernen:

```css
/* BITTE NICHT MACHEN! Dies ist ein Anti-Pattern. */
a:focus {
  outline: none;
}
```

Das ist ein fataler Fehler für die Barrierefreiheit. Ohne visuellen Fokusindikator navigiert der Tastaturbenutzer im Blindflug. Er drückt die Tab-Taste und nichts scheint zu passieren, weil er nicht sehen kann, welcher Link oder Button als Nächstes dran ist.

Die richtige Vorgehensweise ist nicht, den Fokus-Stil zu entfernen, sondern ihn an das Design der Webseite anzupassen. Du kannst die `outline`-Eigenschaft genauso gestalten wie andere CSS-Eigenschaften.

```css
/* Ein guter, sichtbarer Fokus-Stil */
a:focus {
  outline: 2px solid #ff4500;
  outline-offset: 2px;
  background-color: #fff0e6;
}
```

Hier geben wir dem Link im Fokus-Zustand einen leuchtend orangen Rahmen, der einen kleinen Abstand zum Element selbst hat (`outline-offset`), und heben ihn zusätzlich mit einer zarten Hintergrundfarbe hervor. Das ist nicht nur barrierefrei, sondern kann auch ein bewusstes Design-Element sein.

#### Die Synergie: `:hover` und `:focus` kombinieren

Da sowohl Maus- als auch Tastaturnutzer eine klare Rückmeldung über Interaktivität erhalten sollten, ist es eine gängige und empfohlene Praxis, die Stile für `:hover` und `:focus` zu kombinieren. So stellst du sicher, dass das visuelle Feedback konsistent ist, egal welches Eingabegerät verwendet wird.

Du kannst die Selektoren einfach mit einem Komma verketten:

```css
a {
  color: #1a1a1a;
  background-color: #f0f0f0;
  padding: 8px 12px;
  border-radius: 4px;
  text-decoration: none;
  /* Sanfter Übergang für alle Änderungen */
  transition: all 0.2s ease-in-out;
}

/* Kombinierter Stil für Hover und Focus */
a:hover,
a:focus {
  color: #ffffff;
  background-color: #007bff;
}
```

In diesem Beispiel haben wir einen Link, der wie ein schlichter Button aussieht. Sowohl beim Überfahren mit der Maus als auch beim Ansteuern mit der Tastatur ändert er seine Text- und Hintergrundfarbe. Durch die `transition`-Eigenschaft im Basis-Selektor (`a`) geschieht dieser Wechsel nicht abrupt, sondern als sanfte Animation über 0,2 Sekunden. Dies sorgt für eine angenehmere und hochwertigere Benutzererfahrung.

#### Der moderne Ansatz: `:focus-visible`

Ein häufiges Argument gegen auffällige `:focus`-Stile war, dass der Fokus-Rahmen auch dann erscheint, wenn ein Nutzer mit der Maus auf einen Button klickt, was manche Designer als störend empfinden. Für dieses Problem gibt es eine moderne Lösung: die Pseudoklasse `:focus-visible`.

Diese Pseudoklasse ist intelligenter als `:focus`. Der Browser versucht selbst zu erkennen, ob der Nutzer den Fokus-Indikator wahrscheinlich benötigt. Die Faustregel lautet:

*   Wenn der Nutzer per Tastatur (Tab-Taste) zu einem Element navigiert, wird der `:focus-visible`-Stil angewendet.
*   Wenn der Nutzer mit der Maus auf ein Element klickt, das auch ohne Fokus-Ring klar als aktiv erkennbar ist (wie ein Button), wird der Stil oft *nicht* angewendet.

Damit kannst du den Fokus-Stil gezielt für Tastaturnutzer bereitstellen, ohne die Ästhetik für Mausnutzer zu beeinträchtigen.

Die Implementierung sieht oft so aus:

```css
/* Entferne den Standard-Fokus-Stil nur dann, wenn :focus-visible unterstützt wird */
a:focus {
  outline: none;
}

/* Definiere einen klaren Stil für den "intelligenten" Fokus */
a:focus-visible {
  outline: 3px dashed #007bff;
  outline-offset: 3px;
}
```

Mit dieser Methode stellst du eine robuste und moderne Form der Barrierefreiheit sicher. Du lieferst Tastaturnutzern ein klares Signal, während du die volle Kontrolle über das visuelle Erscheinungsbild bei Mausklicks behältst.

Die Zustände `:hover` und `:focus` sind also weit mehr als nur eine technische Spielerei. Sie sind fundamentale Werkzeuge der User Experience und der digitalen Barrierefreiheit. Sie machen deine Webseite nicht nur schöner und dynamischer, sondern auch verständlicher, zugänglicher und letztendlich für alle Menschen besser bedienbar.
