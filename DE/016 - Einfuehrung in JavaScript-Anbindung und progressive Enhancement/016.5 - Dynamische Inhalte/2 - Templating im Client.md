# Templating im Client

### Templating im Client: HTML-Strukturen dynamisch erzeugen

Wenn du Webseiten baust, stößt du schnell an einen Punkt, an dem statisches HTML nicht mehr ausreicht. Du möchtest Inhalte anzeigen, die sich ändern – eine Liste von Blogbeiträgen, Suchergebnisse, Benutzerprofile oder die Produkte in einem Online-Shop. Diese Daten kommen oft von einer externen Quelle, einer sogenannten API, und liegen meist als JavaScript-Objekte vor. Die große Frage ist nun: Wie verwandelst du diese Daten auf eine saubere, sichere und wartbare Weise in HTML, das der Browser anzeigen kann?

Genau hier kommt das Konzept des „Client-Side Templating“ ins Spiel. Es ist die Technik, eine HTML-Vorlage (ein Template) zu definieren und diese dann im Browser des Nutzers (dem Client) mit dynamischen Daten zu füllen.

#### Das Problem: HTML in JavaScript-Strings

Sehen wir uns zunächst den Weg an, den viele am Anfang gehen und der schnell zu Problemen führt: das Zusammenbauen von HTML-Strings direkt in JavaScript. Stell dir vor, du hast ein einfaches JavaScript-Objekt, das einen Nutzer repräsentiert:

```js
const user = {
  name: "Alex",
  username: "alex_codes",
  profileImage: "path/to/image.jpg",
  bio: "Entwickler & Kaffeeliebhaber."
};
```

Um daraus eine kleine Profilkarte zu erstellen, könntest du auf die Idee kommen, den HTML-Code als String zu verketten:

```js
const container = document.querySelector('#user-profile-container');

let userHtml = '<div class="profile-card">';
userHtml += '<img src="' + user.profileImage + '" alt="Profilbild von ' + user.name + '">';
userHtml += '<h2>' + user.name + '</h2>';
userHtml += '<p>@' + user.username + '</p>';
userHtml += '<p>' + user.bio + '</p>';
userHtml += '</div>';

container.innerHTML = userHtml;
```

Dieser Ansatz funktioniert, aber er hat gravierende Nachteile:

1.  **Schlechte Lesbarkeit:** Sobald die HTML-Struktur komplexer wird, ist der Code kaum noch zu entziffern. Verschachtelte Elemente und Attribute machen den String zu einem unübersichtlichen Monster.
2.  **Fehleranfälligkeit:** Ein fehlendes Anführungszeichen, ein vergessener schließender Tag – und schon ist die gesamte Struktur kaputt. Der Browser kann dir hierbei kaum helfen, Fehler zu finden.
3.  **Sicherheitsrisiko (XSS):** Der größte Nachteil ist die Verwendung von `.innerHTML`. Wenn die Daten (z. B. der `user.bio`) von einem Nutzer eingegeben wurden und schädlichen Code wie `<script>alert('gehackt!')</script>` enthalten, wird dieser Code ausgeführt! Dies nennt man Cross-Site Scripting (XSS) und es ist eine der häufigsten Sicherheitslücken im Web.

#### Eine erste Verbesserung: Template Literals (ES6)

Mit der Einführung von ECMAScript 2015 (ES6) kamen die Template Literals nach JavaScript, die das Arbeiten mit Strings deutlich angenehmer machen. Sie werden mit Backticks (`` ` ``) anstelle von Anführungszeichen umschlossen und erlauben es, Variablen und Ausdrücke direkt mit der `${...}`-Syntax einzubetten.

Unser Beispiel von oben sieht damit schon viel sauberer aus:

```js
const container = document.querySelector('#user-profile-container');

const userHtml = `
  <div class="profile-card">
    <img src="${user.profileImage}" alt="Profilbild von ${user.name}">
    <h2>${user.name}</h2>
    <p>@${user.username}</p>
    <p>${user.bio}</p>
  </div>
`;

container.innerHTML = userHtml;
```

Das ist ein riesiger Schritt nach vorn in Sachen Lesbarkeit und Wartbarkeit. Der HTML-Code sieht wieder wie HTML aus. Das grundlegende Sicherheitsproblem mit `.innerHTML` bleibt jedoch bestehen, wenn die Daten von externen Quellen stammen. Außerdem vermischen wir immer noch Struktur (HTML) und Logik (JavaScript) sehr stark.

#### Die professionelle Lösung: Das `<template>`-Element

HTML selbst bietet eine elegante und leistungsstarke Lösung für dieses Problem: das `<template>`-Element. Es ist ein verborgener Held im HTML-Standard, der genau für diesen Anwendungsfall geschaffen wurde.

Ein `<template>`-Tag im HTML-Dokument hat eine besondere Eigenschaft: Sein Inhalt wird vom Browser zwar geparst, aber **nicht gerendert**. Er ist inert, also untätig. JavaScript-Code darin wird nicht ausgeführt, Bilder werden nicht geladen und CSS-Regeln werden nicht angewendet. Es ist eine reine, wiederverwendbare Blaupause für ein HTML-Fragment, das darauf wartet, mit JavaScript zum Leben erweckt zu werden.

So definierst du eine Vorlage für unsere Nutzerkarte direkt in deiner HTML-Datei:

```html
<!-- Irgendwo in deinem <body> -->
<div id="user-profile-container">
  <!-- Hier werden die fertigen Karten eingefügt -->
</div>


<!-- Die Vorlage, die nicht direkt sichtbar ist -->
<template id="user-card-template">
  <div class="profile-card">
    <img src="" alt="" class="profile-image">
    <h2 class="profile-name"></h2>
    <p class="profile-username"></p>
    <p class="profile-bio"></p>
  </div>
</template>
```

Beachte, dass wir Platzhalter-Attribute (wie `src=""`) und leere Tags verwenden. Wir versehen die Elemente, die wir später füllen wollen, mit Klassen, um sie einfach per JavaScript ansteuern zu können.

Jetzt kommt der JavaScript-Teil, der die Magie vollbringt. Der Prozess besteht aus vier Schritten:

1.  **Vorlage holen:** Wir greifen auf das `<template>`-Element zu.
2.  **Inhalt klonen:** Wir erstellen eine Kopie des Inhalts der Vorlage. Es ist wichtig, eine Kopie zu erstellen, damit die Originalvorlage für weitere Instanzen erhalten bleibt.
3.  **Klon befüllen:** Wir füllen die geklonte Struktur mit unseren Daten.
4.  **Klon einfügen:** Wir fügen das fertige HTML-Fragment in den sichtbaren Teil der Webseite (den DOM) ein.

Hier ist der Code dazu:

```js
// Die Daten, die wir anzeigen wollen
const user = {
  name: "Alex",
  username: "alex_codes",
  profileImage: "path/to/image.jpg",
  bio: "Entwickler & Kaffeeliebhaber."
};

// 1. Vorlage holen
const template = document.querySelector('#user-card-template');

// 2. Inhalt klonen (true bedeutet, dass alle Kind-Elemente mitgeklont werden)
const userCardClone = template.content.cloneNode(true);

// 3. Klon mit Daten befüllen
// Wir verwenden .textContent statt .innerHTML, um XSS-Angriffe zu verhindern!
userCardClone.querySelector('.profile-name').textContent = user.name;
userCardClone.querySelector('.profile-username').textContent = `@${user.username}`;
userCardClone.querySelector('.profile-bio').textContent = user.bio;

const profileImage = userCardClone.querySelector('.profile-image');
profileImage.src = user.profileImage;
profileImage.alt = `Profilbild von ${user.name}`;

// 4. Klon in den DOM einfügen
const container = document.querySelector('#user-profile-container');
container.appendChild(userCardClone);
```

#### Vom Einzelstück zur Serie: Daten in einer Schleife verarbeiten

Die wahre Stärke dieses Ansatzes zeigt sich, wenn du nicht nur ein, sondern Dutzende oder Hunderte von Elementen erstellen musst. Nehmen wir an, du erhältst ein Array von Nutzern:

```js
const users = [
  { name: "Alex", username: "alex_codes", profileImage: "...", bio: "..." },
  { name: "Bea", username: "bea_builds", profileImage: "...", bio: "..." },
  { name: "Chris", username: "chris_creates", profileImage: "...", bio: "..." }
];

const template = document.querySelector('#user-card-template');
const container = document.querySelector('#user-profile-container');

// Wir iterieren über das Array
users.forEach(user => {
  // Für jeden Nutzer wiederholen wir den Klon- und Befüll-Prozess
  const userCardClone = template.content.cloneNode(true);

  userCardClone.querySelector('.profile-name').textContent = user.name;
  userCardClone.querySelector('.profile-username').textContent = `@${user.username}`;
  userCardClone.querySelector('.profile-bio').textContent = user.bio;
  // ... und so weiter für das Bild

  container.appendChild(userCardClone);
});
```

Mit wenigen Zeilen Code haben wir eine ganze Liste von Nutzern dynamisch generiert, und das auf eine saubere, sichere und wiederverwendbare Weise.

#### Warum dieser Ansatz überlegen ist

Die Verwendung des `<template>`-Elements ist mehr als nur eine stilistische Entscheidung. Sie bringt handfeste Vorteile mit sich, die für professionelle Webentwicklung unerlässlich sind.

*   **Trennung von Struktur und Logik (Separation of Concerns):** Dein HTML bleibt in der HTML-Datei, wo es hingehört. Dein JavaScript kümmert sich nur um die Logik, also das Holen der Daten und das Befüllen der Vorlage. Das macht deinen Code für dich und andere Teammitglieder viel einfacher zu verstehen und zu warten. Wenn ein Designer die Struktur der Karte ändern möchte, muss er nur die HTML-Datei anfassen, ohne den JavaScript-Code zu berühren.
*   **Sicherheit:** Indem du `.textContent` anstelle von `.innerHTML` verwendest, um die Daten einzufügen, wird der übergebene Text vom Browser immer als reiner Text behandelt. Eventuell enthaltener HTML- oder Skript-Code wird nicht interpretiert, sondern einfach als Text angezeigt. Das schließt die Tür für XSS-Angriffe effektiv.
*   **Performance:** Der Browser parst den Inhalt des `<template>`-Tags nur einmal beim Laden der Seite. Das Klonen eines bereits geparsten DOM-Fragments mit `cloneNode` ist deutlich performanter, als bei jedem Schleifendurchlauf einen neuen HTML-String zu parsen und in den DOM einzufügen.
*   **Wartbarkeit:** Stell dir vor, du musst eine Klasse in deiner Profilkarte ändern. Bei der String-Methode müsstest du dich durch unübersichtlichen JavaScript-Code wühlen. Mit dem `<template>`-Tag änderst du einfach das HTML an einer zentralen, klaren Stelle.

Das Templating im Client mit dem `<template>`-Element ist eine grundlegende Technik, die dir die volle Kontrolle über dynamische Inhalte gibt. Es ist die Brücke zwischen rohen Daten und einer lebendigen, interaktiven Benutzeroberfläche. Moderne JavaScript-Frameworks wie React, Vue oder Svelte treiben dieses Prinzip auf die Spitze, aber das hier gezeigte Fundament bleibt dasselbe: die saubere Trennung von Daten und ihrer visuellen Repräsentation.
