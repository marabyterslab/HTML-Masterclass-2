# Sicherheitsaspekte (rel_noopener)

### Sicherheitsaspekte: Die unsichtbare Gefahr von `target="_blank"` und die Rolle von `rel="noopener"`

Du kennst das sicher: Du erstellst einen Link und möchtest, dass er sich in einem neuen Tab oder Fenster öffnet, damit der Nutzer deine Seite nicht verlässt. Die naheliegendste und bekannteste Lösung dafür ist das Attribut `target="_blank"`.

```html
<a href="https://beispiel-externe-seite.de" target="_blank">Besuche unsere Partnerseite</a>
```

Auf den ersten Blick wirkt das harmlos und unkompliziert. Es ist eine grundlegende Funktion, die täglich millionenfach im Web genutzt wird. Was jedoch viele Entwickler, insbesondere am Anfang ihrer Reise, nicht wissen: Hinter diesem einfachen Attribut verbirgt sich eine potenzielle Sicherheitslücke, die als "Tabnabbing" bekannt ist. Sie ist subtil, aber ihre Auswirkungen können gravierend sein.

#### Die unsichtbare Verbindung: Das `window.opener`-Objekt

Wenn du einen Link mit `target="_blank"` öffnest, ohne weitere Vorkehrungen zu treffen, erschafft der Browser eine unsichtbare Verbindung zwischen deiner ursprünglichen Seite (dem "Opener") und der neu geöffneten Seite. Die neue Seite erhält über das JavaScript-Objekt `window.opener` einen Verweis und damit teilweise Kontrolle über das Fenster, aus dem sie geöffnet wurde.

Stell es dir wie eine unsichtbare Nabelschnur vor. Obwohl die neue Seite in einem eigenen Tab läuft, bleibt sie mit ihrer Herkunftsseite verbunden. Über `window.opener` kann ein auf der neuen Seite ausgeführtes Skript auf bestimmte Eigenschaften des ursprünglichen Fensters zugreifen. Die meisten Eigenschaften sind aus Sicherheitsgründen blockiert, aber eine entscheidende ist es nicht: `window.opener.location`.

Mit `window.opener.location` kann die neu geöffnete Seite die URL deiner ursprünglichen Seite verändern und den Nutzer auf eine komplett andere Webseite umleiten.

#### Das Angriffsszenario: Tabnabbing in der Praxis

Lass uns das an einem konkreten Beispiel durchspielen, um die Gefahr zu verdeutlichen. Stell dir vor, du betreibst einen Blog. Ein Nutzer hinterlässt einen Kommentar mit einem Link zu seiner angeblich harmlosen Fotogalerie. Du hast die Kommentare so konfiguriert, dass alle Links automatisch mit `target="_blank"` versehen werden, um deine Besucher auf der Seite zu halten.

Ein anderer Besucher deines Blogs liest diesen Kommentar und klickt auf den Link. Ein neuer Tab öffnet sich und zeigt die Fotogalerie. Der Besucher schaut sich die Bilder an, abgelenkt vom Inhalt des neuen Tabs.

In diesem Moment passiert der Angriff: Ein bösartiges Skript, das auf der Fotogalerie-Seite versteckt ist, wird aktiv. Es prüft, ob es über `window.opener` geöffnet wurde, und führt dann folgenden Code aus:

```js
if (window.opener) {
  // Leite die ursprüngliche Seite auf eine Phishing-Seite um
  window.opener.location = "https://deine-blog-login-seite.fake.com";
}
```

Während der Besucher noch im Tab der Fotogalerie ist, wird der Tab deines Blogs im Hintergrund unbemerkt auf eine gefälschte Login-Seite umgeleitet, die exakt so aussieht wie deine.

Wenn der Besucher nun zur Registerkarte deines Blogs zurückkehrt, sieht er nicht mehr den Artikel, den er gelesen hat, sondern eine Login-Maske mit der Meldung: "Ihre Sitzung ist abgelaufen. Bitte melden Sie sich erneut an." Da die URL und das Design vertraut aussehen, wird der Besucher wahrscheinlich arglos seine Anmeldedaten eingeben. Diese Daten landen direkt beim Angreifer. Das ist ein klassischer und sehr effektiver Phishing-Angriff, ermöglicht durch eine simple Unachtsamkeit im HTML-Code.

#### Die Lösung: `rel="noopener"`

Glücklicherweise ist die Lösung für dieses Problem ebenso einfach wie effektiv. Um diese Sicherheitslücke zu schließen, musst du dem `<a>`-Tag ein weiteres Attribut hinzufügen: `rel="noopener"`.

Das Attribut `rel` (kurz für "relationship") beschreibt die Beziehung zwischen dem aktuellen Dokument und dem verlinkten Dokument. Der Wert `noopener` weist den Browser an, die Verbindung zwischen den beiden Fenstern zu kappen. Wenn der neue Tab geöffnet wird, wird das `window.opener`-Objekt auf `null` gesetzt. Das bösartige Skript auf der Zielseite hat somit keine Möglichkeit mehr, auf deine Seite zuzugreifen oder sie zu manipulieren.

Der korrekte und sichere Code sieht also so aus:

```html
<a href="https://beispiel-externe-seite.de" target="_blank" rel="noopener">
  Besuche unsere Partnerseite (jetzt sicher)
</a>
```

Diese kleine Ergänzung hat eine große Wirkung und sollte zur Standardpraxis für jeden Link werden, der mit `target="_blank"` geöffnet wird.

#### Ein naher Verwandter: `rel="noreferrer"`

Im Zusammenhang mit `noopener` wirst du oft auf einen weiteren Wert für das `rel`-Attribut stoßen: `noreferrer`. Obwohl sie oft zusammen verwendet werden, dienen sie unterschiedlichen Zwecken.

*   **`rel="noopener"`**: Ein reines Sicherheitsmerkmal. Es verhindert den Zugriff auf das `window.opener`-Objekt und schützt so vor Tabnabbing.
*   **`rel="noreferrer"`**: Ein Datenschutzmerkmal. Es verhindert, dass der Browser den `Referer`-HTTP-Header an die Zielseite sendet. Normalerweise erfährt eine Webseite, von welcher anderen Webseite ein Besucher gekommen ist. Mit `noreferrer` bleibt diese Information verborgen. Die Zielseite weiß also nicht, dass der Klick von deiner Seite kam.

Der interessante Nebeneffekt ist, dass `rel="noreferrer"` auch das Verhalten von `noopener` impliziert. Ein Browser, der `noreferrer` versteht, wird ebenfalls `window.opener` auf `null` setzen.

Warum also nicht einfach immer nur `noreferrer` verwenden? Es gibt zwei gute Gründe, explizit zu sein:

1.  **Klarheit im Code:** `rel="noopener"` kommuniziert klar deine Absicht: Du möchtest die bekannte Sicherheitslücke schließen. `noreferrer` kommuniziert eine Datenschutzabsicht. Beides zu verwenden, macht deinen Code für andere Entwickler (und für dich selbst in der Zukunft) verständlicher.
2.  **Browser-Kompatibilität:** Obwohl moderne Browser die Implikation verstehen, ist es für die Abdeckung älterer Versionen und die absolute Sicherheit am besten, beide anzugeben.

Die Goldstandard-Empfehlung lautet daher:

```html
<a href="https://beispiel-externe-seite.de" target="_blank" rel="noopener noreferrer">
  Der sicherste Link in einem neuen Tab
</a>
```

Damit schlägst du zwei Fliegen mit einer Klappe: Du schützt deine Nutzer vor Tabnabbing und wahrst gleichzeitig ihre Privatsphäre, indem du keine Referrer-Informationen weitergibst.

#### Ein unerwarteter Bonus: Performance

Die Verwendung von `rel="noopener"` hat nicht nur Sicherheits-, sondern auch Performance-Vorteile. Wenn eine Seite ohne `noopener` in einem neuen Tab geöffnet wird, läuft sie oft im selben Browser-Prozess wie die ursprüngliche Seite.

Wenn die neu geöffnete Seite nun sehr ressourcenintensiven JavaScript-Code ausführt – zum Beispiel komplexe Animationen, Datenverarbeitung oder Krypto-Mining-Skripte –, kann dies die Leistung deiner ursprünglichen Seite beeinträchtigen. Dein Tab könnte langsam werden, ruckeln oder sogar komplett einfrieren, weil er sich die Rechenleistung mit dem schlecht programmierten oder bösartigen neuen Tab teilen muss.

Durch `rel="noopener"` wird der neue Tab in einem eigenen, separaten Prozess geöffnet (je nach Browser-Architektur). Die beiden Seiten sind voneinander isoliert, und die Performance-Probleme der einen Seite wirken sich nicht auf die andere aus. Deine Webseite bleibt also auch dann schnell und reaktionsfähig, wenn der verlinkte Inhalt ressourcenhungrig ist.

#### Was machen moderne Browser heute?

Die Browser-Hersteller haben auf die Verbreitung dieser Sicherheitslücke reagiert. Viele moderne Browser wie Chrome, Firefox, Safari und Edge haben ihr Standardverhalten geändert. Sie wenden nun implizit das `noopener`-Verhalten auf alle `<a>`-Tags an, die `target="_blank"` enthalten, auch wenn `rel="noopener"` nicht explizit gesetzt ist.

Das ist eine großartige Entwicklung für die allgemeine Sicherheit im Web. Du solltest dich jedoch niemals blind darauf verlassen. Es ist und bleibt eine bewährte Praxis, `rel="noopener noreferrer"` manuell hinzuzufügen. Die Gründe dafür sind:

*   **Abwärtskompatibilität:** Du kannst nicht garantieren, dass alle deine Nutzer die neueste Browser-Version verwenden. Ältere Versionen oder weniger verbreitete Browser haben dieses implizite Verhalten möglicherweise nicht.
*   **Explizit ist besser als implizit:** Dein Code sollte deine Absichten klar widerspiegeln. Das manuelle Hinzufügen des Attributs ist eine Form der Selbst-Dokumentation und zeigt, dass du dir der Sicherheitsimplikationen bewusst bist.
*   **Einheitlichkeit:** Es schafft eine konsistente Codebasis und verhindert Verwirrung, warum das Attribut bei manchen Links vorhanden ist und bei anderen nicht.

Die Regel ist einfach: Immer wenn du `target="_blank"` schreibst, solltest du reflexartig `rel="noopener noreferrer"` hinzufügen. Es ist eine kleine Mühe mit einem erheblichen Gewinn an Sicherheit, Datenschutz und sogar Performance.
