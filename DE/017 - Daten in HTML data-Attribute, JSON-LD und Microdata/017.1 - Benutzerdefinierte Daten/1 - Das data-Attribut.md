# Das data-Attribut

### Das `data-`Attribut: Dein eigener Datenspeicher in HTML

Stell dir vor, du baust ein interaktives Element auf deiner Webseite – vielleicht eine Bildergalerie, eine dynamische Produktliste oder ein anpassbares Benutzerprofil. Oft benötigst du zusätzliche Informationen, die direkt mit einem HTML-Element verknüpft sind, aber für den Besucher nicht sichtbar sein sollen. Diese Daten sind nicht für die Anzeige gedacht, sondern als Futter für deine JavaScript-Skripte oder sogar für dein CSS.

Früher behalfen sich Entwickler mit Notlösungen. Sie packten Daten in das `class`-Attribut, missbrauchten das `id`-Attribut oder erfanden eigene, nicht standardkonforme Attribute. Das führte zu unsauberem, fehleranfälligem und semantisch falschem HTML. Mit HTML5 wurde eine saubere, elegante und standardisierte Lösung eingeführt: die benutzerdefinierten `data-`Attribute.

#### Was genau sind `data-`Attribute?

`data-`Attribute sind eine spezielle Klasse von Attributen, die es dir erlauben, private, benutzerdefinierte Daten an jedes beliebige HTML-Element anzuhängen. Der Name sagt es schon: Sie sind für *Daten* da. Diese Daten sind für die Maschine (deinen Code) bestimmt, nicht primär für den Menschen.

Die Syntax ist einfach und flexibel. Jedes Attribut, dessen Name mit `data-` beginnt, ist ein gültiges `data-`Attribut.

Die Regeln für den Namen sind unkompliziert:
1.  Er muss mit der Zeichenfolge `data-` anfangen.
2.  Nach dem Präfix `data-` muss mindestens ein Zeichen folgen.
3.  Der Name darf keine Großbuchstaben enthalten. Technisch gesehen wird er von Browsern in Kleinbuchstaben umgewandelt, aber die Konvention ist, von vornherein nur Kleinbuchstaben, Zahlen und Bindestriche zu verwenden.

Hier sind ein paar Beispiele, wie das in der Praxis aussehen könnte:

```html
<!-- Ein einfaches Beispiel an einem Button -->
<button data-click-counter="0">Klick mich!</button>

<!-- Komplexere Daten an einem Listenelement -->
<li data-product-id="12345" data-category="electronics" data-in-stock="true">
  Super-Smartphone Modell X
</li>

<!-- Informationen für eine interaktive Karte -->
<div id="berlin" data-lat="52.5200" data-lng="13.4050" data-zoom-level="13">
  Hauptstadt-Marker
</div>
```

Wie du siehst, kannst du so viele `data-`Attribute an ein Element hängen, wie du benötigst. Die Werte dieser Attribute sind immer Zeichenketten (Strings). Auch wenn du `data-in-stock="true"` schreibst, ist der Wert `"true"` ein String, keine boolesche Variable. Das ist wichtig zu wissen, wenn du diese Daten später mit JavaScript verarbeitest.

#### Der Zugriff mit JavaScript: Die `dataset`-Eigenschaft

Der Hauptzweck von `data-`Attributen ist die Interaktion mit JavaScript. Es wäre umständlich, wenn du komplexe Methoden bräuchtest, um an diese Werte zu gelangen. Glücklicherweise bietet die DOM-API eine sehr bequeme Schnittstelle dafür: die `dataset`-Eigenschaft.

Jedes HTML-Element-Objekt in JavaScript hat eine `dataset`-Eigenschaft. Diese Eigenschaft ist ein Objekt (`DOMStringMap`), das alle `data-`Attribute des Elements als Schlüssel-Wert-Paare enthält.

Der Clou dabei ist die Umwandlung des Attributnamens:
Ein `data-`Attribut im HTML wie `data-product-id` wird in JavaScript zu einem Schlüssel in `camelCase`-Schreibweise: `productId`. Die Regel lautet: Das `data-`-Präfix wird entfernt, und jeder Bindestrich (`-`) wird ebenfalls entfernt, während der darauffolgende Buchstabe in einen Großbuchstaben umgewandelt wird.

Schauen wir uns das an einem konkreten Beispiel an. Gegeben sei folgendes HTML:

```html
<div id="user-profile"
     data-user-id="987"
     data-user-role="editor"
     data-last-login="2023-10-27T10:00:00Z">
  Max Mustermann
</div>
```

Mit JavaScript kannst du nun ganz einfach auf diese Daten zugreifen:

```js
const profileElement = document.getElementById('user-profile');

// Auslesen der Daten
const userId = profileElement.dataset.userId; // -> "987"
const userRole = profileElement.dataset.userRole; // -> "editor"
const lastLogin = profileElement.dataset.lastLogin; // -> "2023-10-27T10:00:00Z"

console.log(`Der Benutzer mit der ID ${userId} hat die Rolle "${userRole}".`);
// Ausgabe: Der Benutzer mit der ID 987 hat die Rolle "editor".

// Bedenke: Die Werte sind immer Strings!
console.log(typeof userId); // -> "string"
```

Du kannst die Daten nicht nur lesen, sondern auch direkt über die `dataset`-Eigenschaft ändern oder neue `data-`Attribute hinzufügen.

```js
// Ein data-Attribut ändern
profileElement.dataset.userRole = 'administrator';
// Im HTML steht jetzt: data-user-role="administrator"

// Ein neues data-Attribut hinzufügen
profileElement.dataset.status = 'active';
// Im HTML wurde hinzugefügt: data-status="active"

// Ein data-Attribut entfernen
delete profileElement.dataset.lastLogin;
// Das Attribut data-last-login wurde aus dem HTML-Element entfernt.
```

Diese Vorgehensweise ist sauber, lesbar und die empfohlene Methode. Alternativ könntest du auch die älteren Methoden `getAttribute()` und `setAttribute()` verwenden, müsstest dann aber den vollen Attributnamen angeben:

```js
// Alternativer Lesezugriff (weniger elegant)
const userIdOld = profileElement.getAttribute('data-user-id');

// Alternativer Schreibzugriff
profileElement.setAttribute('data-new-info', 'wichtiger Hinweis');
```

Für `data-`Attribute ist `dataset` jedoch fast immer die bessere Wahl.

#### Styling mit CSS: Eine überraschende Superkraft

Obwohl `data-`Attribute primär für JavaScript gedacht sind, können sie auch von CSS genutzt werden, um das Styling von Elementen basierend auf ihren Daten zu steuern. Dies geschieht über Attribut-Selektoren.

Stell dir eine To-do-Liste vor, bei der jede Aufgabe eine Priorität hat:

```html
<ul>
  <li data-priority="high">Wichtigen Bericht fertigstellen</li>
  <li data-priority="medium">Team-Meeting vorbereiten</li>
  <li data-priority="low">Büropflanzen gießen</li>
</ul>
```

Mit CSS kannst du diese Prioritäten nun visuell hervorheben:

```css
li[data-priority="high"] {
  border-left: 5px solid red;
  font-weight: bold;
}

li[data-priority="medium"] {
  border-left: 5px solid orange;
}

li[data-priority="low"] {
  border-left: 5px solid green;
  color: #555;
}
```

Das ist extrem nützlich, um Zustände darzustellen, die von JavaScript dynamisch geändert werden. Wenn dein Skript die Priorität eines Elements von `medium` auf `high` ändert (`taskElement.dataset.priority = 'high'`), passt der Browser das Styling automatisch an, ohne dass du manuell CSS-Klassen hinzufügen oder entfernen musst.

Eine noch fortschrittlichere Technik ist die Verwendung der `attr()`-Funktion in CSS, um den Inhalt eines `data-`Attributs direkt im Layout anzuzeigen, meist in Kombination mit den Pseudo-Elementen `::before` oder `::after`.

Ein klassisches Beispiel hierfür ist ein einfacher Tooltip:

```html
<span data-tooltip="Dies ist ein nützlicher Hinweis!">Hilfe</span>
```

```css
[data-tooltip] {
  position: relative; /* Notwendig für die Positionierung des Tooltips */
  cursor: help;
}

/* Der Tooltip selbst, initial unsichtbar */
[data-tooltip]::after {
  content: attr(data-tooltip); /* Hier wird der Wert des Attributs geholt! */
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  
  background-color: #333;
  color: white;
  padding: 5px 10px;
  border-radius: 4px;
  font-size: 0.9em;
  white-space: nowrap; /* Verhindert Zeilenumbrüche im Tooltip */
  
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.2s, visibility 0.2s;
}

/* Der Tooltip wird beim Hovern sichtbar */
[data-tooltip]:hover::after {
  opacity: 1;
  visibility: visible;
}
```
In diesem Beispiel liest CSS den Text für den Tooltip direkt aus dem `data-tooltip`-Attribut und zeigt ihn an, wenn der Benutzer mit der Maus über das `<span>`-Element fährt. Das alles geschieht ohne eine einzige Zeile JavaScript.

#### Wann du `data-`Attribute verwenden solltest (und wann nicht)

`data-`Attribute sind ein mächtiges Werkzeug, aber sie sind nicht für jeden Anwendungsfall die beste Lösung.

**Verwende `data-`Attribute, wenn:**
*   Du einfache Daten hast, die eng mit einem bestimmten Element auf der Seite verknüpft sind.
*   Diese Daten hauptsächlich von clientseitigem JavaScript benötigt werden, um die Interaktivität oder das Verhalten des Elements zu steuern.
*   Die Information für Crawler, Suchmaschinen oder Screenreader nicht von Bedeutung ist.

**Vermeide `data-`Attribute, wenn:**
*   Die Daten für die Zugänglichkeit (Accessibility) relevant sind. Nutze stattdessen ARIA-Attribute (z. B. `aria-label`, `aria-describedby`).
*   Die Daten eine standardisierte Bedeutung haben, die von Suchmaschinen oder anderen Diensten verstanden werden soll. Hierfür sind Formate wie Microdata oder JSON-LD die richtige Wahl. `data-`Attribute sind privat und haben keine semantische Bedeutung für Dritte.
*   Du komplexe, verschachtelte Daten speichern musst. Technisch könntest du einen JSON-String in ein `data-`Attribut packen und ihn dann mit `JSON.parse()` in JavaScript umwandeln. Bei komplexen Anwendungslogiken führt dies jedoch schnell zu unübersichtlichem Code. In solchen Fällen ist es oft besser, die Daten in JavaScript-Objekten zu halten und nur eine ID im `data-`Attribut zu speichern, um die Verbindung zwischen Element und Datenobjekt herzustellen.

Indem du `data-`Attribute bewusst und gezielt einsetzt, schreibst du sauberen, wartbaren und validen HTML-Code und schaffst eine robuste Brücke zwischen deiner statischen Struktur und deiner dynamischen Anwendungslogik.
