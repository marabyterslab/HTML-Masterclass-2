# Zugriff via JavaScript (dataset)

### Zugriff via JavaScript (dataset)

Du hast nun gelernt, wie du mit `data-*`-Attributen benutzerdefinierte Daten direkt in dein HTML einbetten kannst. Das ist an sich schon eine nützliche Methode, um Metainformationen oder Konfigurationsdaten an ein Element zu heften. Aber die wahre Stärke dieser Attribute entfaltet sich erst, wenn du beginnst, mit JavaScript auf sie zuzugreifen und sie zu manipulieren. Sie bilden die Brücke zwischen der statischen Struktur deines HTML-Dokuments und der dynamischen Logik deiner Anwendung.

Früher, bevor es eine dedizierte Schnittstelle gab, war der Zugriff auf diese Attribute etwas umständlich. Man musste Methoden wie `getAttribute('data-attribut-name')` und `setAttribute('data-attribut-name', 'wert')` verwenden. Das funktioniert zwar bis heute, ist aber recht wortreich und nicht besonders elegant.

Glücklicherweise gibt es eine moderne, saubere und wesentlich intuitivere Methode: die `dataset`-Eigenschaft.

#### Die `dataset`-Eigenschaft: Dein direkter Draht zu den Daten

Jedes HTML-Element in JavaScript, genauer gesagt jedes `HTMLElement`-Objekt, besitzt eine spezielle Eigenschaft namens `dataset`. Diese Eigenschaft ist ein Objekt (`DOMStringMap`), das eine Live-Sammlung aller `data-*`-Attribute des jeweiligen Elements darstellt. Es ist dein zentrales Werkzeug, um diese benutzerdefinierten Daten zu lesen, zu ändern und sogar neue zu erstellen.

Stell dir folgendes HTML-Element vor:

```html
<div id="user-profile" 
     data-user-id="42" 
     data-user-name="Alex" 
     data-is-active="true">
  <!-- Profilinhalt -->
</div>
```

Um mit JavaScript auf dieses Element und seine Daten zuzugreifen, würdest du es zuerst wie gewohnt selektieren:

```javascript
const profile = document.getElementById('user-profile');
```

Jetzt kommt die Magie von `dataset` ins Spiel. Anstatt `getAttribute()` zu verwenden, kannst du die `data-*`-Attribute wie einfache Objekteigenschaften ansprechen.

#### Die Umwandlungsregel: Von Kebab-Case zu CamelCase

Es gibt eine wichtige Regel, die du verinnerlichen musst: Die Benennung der Attribute im HTML und der Eigenschaften im `dataset`-Objekt unterscheidet sich geringfügig. HTML-Attribute verwenden die sogenannte **Kebab-Case**-Schreibweise, bei der Wörter mit Bindestrichen getrennt werden (z. B. `data-user-id`). JavaScript-Eigenschaften hingegen verwenden typischerweise die **CamelCase**-Schreibweise, bei der das erste Wort klein- und jedes folgende Wort großgeschrieben wird (z. B. `userId`).

Die `dataset`-Eigenschaft übernimmt diese Konvertierung für dich automatisch:

*   `data-user-id` wird zu `profile.dataset.userId`
*   `data-user-name` wird zu `profile.dataset.userName`
*   `data-is-active` wird zu `profile.dataset.isActive`

Ein einfaches Attribut ohne Bindestrich wie `data-status` wird einfach zu `profile.dataset.status`.

Schauen wir uns den Lesezugriff im Detail an:

```javascript
const profile = document.getElementById('user-profile');

const userId = profile.dataset.userId;       // Ergibt den String "42"
const userName = profile.dataset.userName;   // Ergibt den String "Alex"
const isActive = profile.dataset.isActive;   // Ergibt den String "true"

console.log(`Benutzer ${userName} (ID: ${userId}) hat den Status: ${isActive}`);
// Ausgabe: Benutzer Alex (ID: 42) hat den Status: true
```

Wie du siehst, ist dieser Zugriff wesentlich lesbarer und fühlt sich natürlicher an als `profile.getAttribute('data-user-id')`.

#### Achtung, Datentyp: Alles ist ein String

Ein extrem wichtiger Punkt, der oft zu Fehlern führt: **Alle Werte, die du aus dem `dataset` liest, sind immer Strings.** Selbst wenn du eine Zahl (`data-user-id="42"`) oder einen booleschen Wert (`data-is-active="true"`) in dein HTML schreibst, erhältst du in JavaScript zunächst einen String.

Das bedeutet, du kannst nicht einfach so damit rechnen oder eine `if`-Bedingung darauf aufbauen:

```javascript
// FALSCH! Dieser Vergleich wird fehlschlagen.
if (profile.dataset.userId === 42) { 
  // Dieser Code wird nie ausgeführt, weil "42" (String) nicht gleich 42 (Number) ist.
}

// FALSCH! Dieser Vergleich funktioniert, aber aus den falschen Gründen.
if (profile.dataset.isActive) { 
  // Dieser Code wird immer ausgeführt, solange der String nicht leer ist,
  // also auch bei "false"! Denn der nicht-leere String "false" ist "truthy".
}
```

Du musst die Werte explizit in den gewünschten Datentyp umwandeln:

```javascript
const profile = document.getElementById('user-profile');

// Korrekte Umwandlung in eine Zahl
const numericUserId = parseInt(profile.dataset.userId, 10);
if (numericUserId === 42) {
  console.log('ID ist korrekt!');
}

// Korrekte Umwandlung in einen Boolean
const booleanIsActive = (profile.dataset.isActive === 'true');
if (booleanIsActive) {
  console.log('Der Benutzer ist aktiv.');
} else {
  console.log('Der Benutzer ist inaktiv.');
}
```

Behalte diese Regel immer im Hinterkopf. Das explizite Umwandeln von Datentypen ist ein Zeichen von sauberem und robustem Code.

#### Daten dynamisch ändern, hinzufügen und löschen

Die `dataset`-Eigenschaft ist keine Einbahnstraße. Du kannst damit nicht nur Daten lesen, sondern sie auch zur Laufzeit verändern, neue hinzufügen oder bestehende entfernen. Diese Änderungen wirken sich direkt auf die `data-*`-Attribute im HTML-Element aus, was du auch in den Entwicklerwerkzeugen deines Browsers live beobachten kannst.

**Wert ändern:**
Um den Wert eines bestehenden `data-*`-Attributs zu ändern, weist du der entsprechenden `dataset`-Eigenschaft einfach einen neuen Wert zu.

```javascript
const profile = document.getElementById('user-profile');

// Ändern wir den Benutzernamen
profile.dataset.userName = 'Erika';

// Im HTML sieht das Element nun so aus:
// <div id="user-profile" data-user-id="42" data-user-name="Erika" data-is-active="true">
```

**Neues Attribut hinzufügen:**
Wenn du einer `dataset`-Eigenschaft einen Wert zuweist, die es noch nicht gibt, wird automatisch ein neues `data-*`-Attribut im HTML erstellt. Auch hier gilt die Umwandlungsregel, nur in die andere Richtung (CamelCase zu Kebab-Case).

```javascript
// Fügen wir eine neue Information hinzu
profile.dataset.lastLogin = '2023-10-27';

// Das HTML wird aktualisiert zu:
// <div id="user-profile" ... data-last-login="2023-10-27">
```

**Attribut löschen:**
Um ein `data-*`-Attribut vollständig vom Element zu entfernen, verwendest du den `delete`-Operator von JavaScript.

```javascript
// Entfernen wir die Information zum Aktiv-Status
delete profile.dataset.isActive;

// Das HTML sieht danach so aus:
// <div id="user-profile" data-user-id="42" data-user-name="Erika" data-last-login="2023-10-27">
```

Diese Fähigkeit, Daten dynamisch zu manipulieren, ist unglaublich mächtig. Sie erlaubt es dir, den Zustand von UI-Komponenten direkt am Element zu speichern, ohne auf globale Variablen oder komplexe Zustandsmanagement-Systeme zurückgreifen zu müssen.

#### Ein praktisches Beispiel: Ein konfigurierbarer Like-Button

Stellen wir uns einen einfachen "Like"-Button vor, der seinen Zustand und die ID des zugehörigen Beitrags in `data-*`-Attributen speichert.

**HTML:**
```html
<button class="like-button" 
        data-post-id="789" 
        data-liked="false">
  Gefällt mir
</button>
```

**JavaScript:**
```javascript
const likeButton = document.querySelector('.like-button');

likeButton.addEventListener('click', function() {
  // 1. Aktuellen Zustand auslesen und in einen Boolean umwandeln
  let isLiked = (this.dataset.liked === 'true');
  const postId = this.dataset.postId;

  // 2. Zustand umkehren
  isLiked = !isLiked;

  // 3. Zustand zurück ins dataset schreiben
  this.dataset.liked = isLiked;

  // 4. Button-Text und Aussehen anpassen
  if (isLiked) {
    this.textContent = 'Gefällt mir nicht mehr';
    this.classList.add('liked');
    console.log(`Beitrag ${postId} wurde geliked.`);
    // Hier könnte ein API-Aufruf an den Server erfolgen
  } else {
    this.textContent = 'Gefällt mir';
    this.classList.remove('liked');
    console.log(`Like für Beitrag ${postId} wurde entfernt.`);
    // Hier könnte ein API-Aufruf an den Server erfolgen
  }
});
```

In diesem Beispiel dient das `data-liked`-Attribut als einfache Zustandsmaschine. Wir lesen den Zustand, verändern ihn und schreiben ihn zurück. Das `data-post-id`-Attribut liefert uns die notwendigen Daten, um eine serverseitige Aktion (z. B. via `fetch`) auszulösen. Der Zustand der Komponente lebt direkt am HTML-Element, was den Code übersichtlich und leicht verständlich macht.

Die `dataset`-Eigenschaft ist ein perfektes Beispiel für eine elegante und durchdachte API. Sie vereinfacht den Code, verbessert die Lesbarkeit und etabliert einen klaren, standardisierten Weg, um die Lücke zwischen deiner HTML-Struktur und deiner JavaScript-Logik zu schließen. Sie ist ein unverzichtbares Werkzeug im modernen Webentwicklungs-Alltag.
