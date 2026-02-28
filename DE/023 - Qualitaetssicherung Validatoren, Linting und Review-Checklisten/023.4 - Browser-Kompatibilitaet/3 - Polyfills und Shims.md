# Polyfills und Shims

### Polyfills und Shims: Brücken in die Vergangenheit bauen

Stell dir vor, du hast eine brillante Idee für eine Webanwendung. Du möchtest die neuesten, elegantesten und effizientesten Werkzeuge nutzen, die das moderne Web zu bieten hat – sei es eine neue JavaScript-Funktion, die deinen Code dramatisch vereinfacht, oder eine CSS-Eigenschaft, die ein komplexes Layout zum Kinderspiel macht. Du baust deine Anwendung, und in deinem aktuellen Browser sieht alles fantastisch aus und funktioniert perfekt.

Doch dann kommt die Realität ins Spiel: die weite, unzurechenbare Welt der Browser. Nicht jeder deiner Nutzer verwendet die neueste Version von Chrome oder Firefox. Einige sind vielleicht an Firmenrichtlinien gebunden und müssen einen älteren Microsoft Edge oder gar einen Internet Explorer verwenden. Andere haben ihre mobilen Browser seit Jahren nicht mehr aktualisiert. Plötzlich bricht deine Anwendung in diesen älteren Umgebungen zusammen. Funktionen fehlen, das Layout ist zerschossen, und die Benutzererfahrung ist ruiniert.

Dies ist eines der fundamentalsten Probleme in der Webentwicklung: der Wunsch nach modernem Code versus die Notwendigkeit, eine breite Palette von Browsern zu unterstützen. Genau hier kommen Polyfills und Shims ins Spiel. Sie sind keine Hacks oder schmutzigen Tricks, sondern eine etablierte und professionelle Methode, um diese Kompatibilitätslücke zu schließen. Sie sind die Brücken, die du baust, damit deine moderne Anwendung auch auf der älteren Infrastruktur der Vergangenheit lauffähig ist.

#### Was ist der Unterschied? Ein Shim und ein Polyfill

Obwohl die Begriffe oft synonym verwendet werden, gibt es einen feinen, aber wichtigen historischen Unterschied zwischen einem Shim und einem Polyfill.

Ein **Shim** ist ein allgemeinerer Begriff. Stell dir einen wackeligen Tisch vor. Um ihn zu stabilisieren, schiebst du ein kleines Stück gefaltetes Papier oder einen Holzkeil (einen „shim“ im Englischen) unter eines der Beine. Das Bein selbst wird nicht verändert, aber das externe Hilfsmittel korrigiert das Problem. In der Softwareentwicklung ist ein Shim ein Stück Code, das eine API abfängt und deren Verhalten korrigiert oder verändert. Es „unterlegt“ eine bestehende, aber fehlerhafte oder inkonsistente Implementierung, um sie an einen Standard anzupassen.

Ein **Polyfill** ist eine spezifische Art von Shim. Der Begriff wurde von Remy Sharp geprägt und ist eine Anspielung auf die Spachtelmasse „Polyfilla“. Wenn du ein Loch in einer Wand hast, füllst du es mit Spachtelmasse, schleifst es glatt, und nach dem Überstreichen ist das Loch unsichtbar. Ein Polyfill tut genau das für einen Browser: Wenn eine moderne Funktionalität (eine API) im Browser komplett fehlt – also ein „Loch“ vorhanden ist –, stellt der Polyfill diese Funktionalität mit den Mitteln zur Verfügung, die der alte Browser bereits versteht (meistens JavaScript). Er füllt die Lücke so, dass der Rest deines Codes die Funktion nutzen kann, als wäre sie von Haus aus vorhanden gewesen.

In der heutigen Praxis hat sich der Begriff „Polyfill“ weitgehend durchgesetzt, um Code zu beschreiben, der fehlende Web-APIs in älteren Browsern nachbildet. Wir werden ihn daher im Folgenden primär verwenden.

#### Ein praktisches JavaScript-Beispiel: `Array.prototype.includes()`

Eine sehr nützliche Methode für Arrays in modernem JavaScript ist `.includes()`. Sie prüft, ob ein Array einen bestimmten Wert enthält, und gibt `true` oder `false` zurück. Das ist deutlich lesbarer als die ältere `indexOf() !== -1`-Methode.

```js
const tiere = ['Hund', 'Katze', 'Maus'];

// Moderne, lesbare Art
console.log(tiere.includes('Katze')); // Gibt true aus

// Ältere, etwas umständlichere Art
console.log(tiere.indexOf('Katze') !== -1); // Gibt ebenfalls true aus
```

Ein Browser wie der Internet Explorer 11 kennt `.includes()` jedoch nicht. Wenn du diesen Code dort ausführst, erhältst du einen Fehler, und dein Skript bricht ab.

Ein Polyfill für `Array.prototype.includes()` löst dieses Problem. Das Geniale an einem gut geschriebenen Polyfill ist, dass er zuerst prüft, ob die Funktionalität bereits existiert. Nur wenn sie fehlt, wird er aktiv.

```js
// Ein einfacher Polyfill für Array.prototype.includes()

// 1. Prüfe, ob die Funktion bereits existiert.
if (!Array.prototype.includes) {
  // 2. Wenn nicht, füge sie dem Prototyp von Array hinzu.
  Object.defineProperty(Array.prototype, 'includes', {
    value: function(searchElement, fromIndex) {
      
      // Dieser Code ahmt das Verhalten von .includes() nach.
      if (this == null) {
        throw new TypeError('"this" is null or not defined');
      }

      var o = Object(this);
      var len = o.length >>> 0;

      if (len === 0) {
        return false;
      }

      var n = fromIndex | 0;
      var k = Math.max(n >= 0 ? n : len - Math.abs(n), 0);

      while (k < len) {
        if (o[k] === searchElement) {
          return true;
        }
        k++;
      }

      return false;
    }
  });
}
```

Wenn du diesen Code-Block am Anfang deiner JavaScript-Datei einfügst, passiert Folgendes:
- In einem modernen Browser wie Chrome sieht der `if`-Check, dass `Array.prototype.includes` bereits existiert, und überspringt den gesamten Block. Du verwendest die schnelle, native Implementierung des Browsers.
- Im Internet Explorer 11 stellt der `if`-Check fest, dass die Funktion fehlt. Der Code im Block wird ausgeführt und fügt deine JavaScript-Implementierung von `.includes()` zum `Array.prototype` hinzu.

Von diesem Moment an kann dein gesamter restlicher Code `tiere.includes('Katze')` verwenden, egal in welchem Browser er läuft. Der Polyfill hat das „Loch“ nahtlos gefüllt.

#### Polyfills gibt es nicht nur für JavaScript

Während die meisten Polyfills in JavaScript geschrieben sind, erstreckt sich das Konzept auch auf HTML und CSS.

##### HTML-Polyfills (oder Shims)

Ein klassisches Beispiel ist die Einführung von HTML5. Ältere Browser, insbesondere der Internet Explorer 8 und früher, kannten die neuen semantischen Elemente wie `<header>`, `<section>`, `<article>` oder `<main>` nicht. Sie behandelten sie als unbekannte Inline-Elemente, was bedeutete, dass man sie nicht mit CSS formatieren konnte (z. B. ihnen `display: block;` geben).

Die Lösung war ein cleverer, winziger JavaScript-Shim, der oft als „HTML5 Shiv“ bezeichnet wird:

```html
<!--[if lt IE 9]>
  <script src="path/to/html5shiv.js"></script>
<![endif]-->
```

Die `html5shiv.js`-Datei enthielt im Wesentlichen nur Code, der für jedes neue HTML5-Element einmal `document.createElement('elementname')` aufrief.

```js
// Vereinfachtes Konzept des HTML5 Shiv
['article', 'aside', 'figure', 'footer', 'header', 'nav', 'section'].forEach(function(tag) {
  document.createElement(tag);
});
```

Dieser einfache Akt „lehrte“ den alten Internet Explorer, die Elemente zu erkennen. Sobald er sie kannte, erlaubte er auch, sie per CSS zu stylen. Dies war ein entscheidender Shim, der den Übergang zu HTML5 erst ermöglichte.

##### CSS-Polyfills

Auch für fehlende CSS-Funktionen gibt es Polyfills. Diese sind oft komplexer, da sie in der Regel mit JavaScript das Verhalten einer CSS-Eigenschaft nachahmen müssen. Wenn ein Browser zum Beispiel CSS Grid Layout nicht unterstützt, könnte ein JavaScript-Polyfill die Position und Größe der Kind-Elemente manuell berechnen und als Inline-Styles (`style="..."`) setzen, um ein Grid-ähnliches Verhalten zu simulieren. Ein bekanntes Beispiel aus der Vergangenheit ist `flexibility.js`, ein Polyfill, der eine Teilmenge von Flexbox-Eigenschaften im Internet Explorer 8 und 9 ermöglichte.

#### Wie du Polyfills findest und einsetzt

Du musst diese Polyfills selten selbst schreiben. Die Web-Community hat bereits robuste und gut getestete Lösungen für die meisten gängigen Probleme geschaffen.

1.  **MDN Web Docs**: Die Mozilla Developer Network (MDN) Dokumentation ist eine unschätzbare Ressource. Für viele moderne Web-APIs findest du am Ende des Artikels einen Abschnitt „Polyfill“, der oft einen sofort einsatzbereiten Code-Schnipsel enthält.

2.  **Automatisierte Dienste**: Dienste wie `Polyfill.io` (oder dessen Nachfolger und Alternativen) verfolgen einen eleganten Ansatz. Du bindest ein einziges Skript-Tag von deren Server in deine Seite ein. Der Server analysiert den User-Agent des anfragenden Browsers, ermittelt, welche Funktionen ihm fehlen, und liefert ein JavaScript-Bündel zurück, das *nur die für diesen spezifischen Browser notwendigen Polyfills* enthält. Ein moderner Chrome-Browser erhält vielleicht eine leere Datei, während ein alter Browser ein Bündel mit Dutzenden von Polyfills bekommt. Dies ist extrem effizient.

3.  **Build-Tools (der moderne Ansatz)**: In modernen Entwicklungsumgebungen, die Werkzeuge wie Babel, Webpack oder Vite verwenden, ist das Polyfilling oft ein integrierter Teil des Build-Prozesses. Mit Projekten wie `core-js` kannst du genau definieren, welche Browserversionen du unterstützen möchtest (z. B. „die letzten 2 Versionen aller Browser“ oder „> 0.5% Marktanteil“). Dein Build-Tool sorgt dann automatisch dafür, dass alle notwendigen Polyfills in dein finales JavaScript-Bündel aufgenommen werden. Babel kümmert sich nicht nur um die fehlenden Funktionen (Polyfills), sondern auch um neue Syntax, die alte Browser nicht verstehen (das nennt man Transpilation).

#### Der Preis der Kompatibilität

Polyfills sind ein fantastisches Werkzeug, aber sie sind nicht kostenlos. Jeder Polyfill fügt deinem Code zusätzliches Gewicht hinzu. Das bedeutet größere Dateigrößen, längere Ladezeiten und eine zusätzliche Auslastung des Prozessors auf dem Client-Gerät, da der nachgeahmte Code oft langsamer ist als eine native Browser-Implementierung.

Deshalb ist es so wichtig, Polyfills gezielt und bedingt zu laden. Lade sie niemals für Browser, die sie nicht benötigen. Die automatisierten Dienste und modernen Build-Tools sind hier deine besten Freunde, da sie diese Optimierung für dich übernehmen.

Die Verwendung von Polyfills ist immer ein Kompromiss zwischen dem Wunsch, sauberen, modernen Code zu schreiben, dem Ziel, eine breite Nutzerbasis zu erreichen, und der Notwendigkeit, die Performance deiner Website im Auge zu behalten. Sie sind eine temporäre Brücke, keine permanente Lösung. Die beste Zukunft für einen Polyfill ist, überflüssig zu werden, weil alle Browser die Funktion, die er nachbildet, nativ unterstützen. Bis dieser Tag für jede Funktion gekommen ist, bleiben sie ein unverzichtbares Werkzeug im Arsenal eines jeden professionellen Webentwicklers.
