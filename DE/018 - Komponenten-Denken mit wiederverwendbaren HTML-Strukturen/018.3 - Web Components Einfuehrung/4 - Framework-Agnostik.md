# Framework-Agnostik

### Die Unabhängigkeitserklärung: Framework-Agnostik

Stell dir vor, du baust ein beeindruckendes Haus aus Legosteinen. Du hast rote, blaue und gelbe Steine, und sie alle passen perfekt zusammen. Jetzt kommt jemand und sagt: „Ab heute benutzen wir nur noch Duplo. Deine Legosteine sind nutzlos.“ All die kunstvollen Türme, Mauern und Fahrzeuge, die du entworfen hast, musst du von Grund auf neu bauen. Frustrierend, oder?

In der Welt der Webentwicklung erleben wir eine ähnliche Situation. Die „Bausteine“ sind hier deine Komponenten – wiederverwendbare UI-Elemente wie Buttons, Eingabefelder oder komplexe Karten-Layouts. Die „Bausysteme“ sind JavaScript-Frameworks wie React, Angular, Vue oder Svelte. Jedes dieser Frameworks ist fantastisch und hat seine eigenen Stärken, aber sie haben ein gemeinsames Problem: Eine Komponente, die du in React schreibst, funktioniert nicht in Angular. Eine Vue-Komponente ist in einem Svelte-Projekt unbrauchbar.

Wenn dein Team oder dein Unternehmen sich entscheidet, von einem Framework auf ein anderes umzusteigen – eine Entscheidung, die aus vielen guten Gründen getroffen werden kann –, bedeutet das oft eine komplette Neuentwicklung deiner gesamten Komponentenbibliothek. Das ist nicht nur teuer und zeitaufwändig, sondern bindet dich auch eng an die technologischen Entscheidungen der Vergangenheit. Man spricht hier von einem „Vendor Lock-in“ oder, in unserem Fall, einem „Framework Lock-in“. Du bist an die Regeln und die Lebensdauer eines bestimmten Systems gebunden.

Genau hier kommt das Konzept der **Framework-Agnostik** ins Spiel. Der Begriff „agnostisch“ bedeutet hier so viel wie „unabhängig von“ oder „gleichgültig gegenüber“. Eine framework-agnostische Komponente ist eine Komponente, der es egal ist, in welchem Framework sie verwendet wird. Sie funktioniert einfach. Überall.

Wie ist das möglich? Die Antwort liegt nicht in einem neuen, besseren Framework, das alle anderen ersetzt. Die Antwort liegt in der Rückbesinnung auf die fundamentalen Technologien des Webs, die in jedem modernen Browser vorhanden sind: HTML, CSS und JavaScript. Die Technologie, die dies ermöglicht, sind die **Web Components**.

#### Der native Weg: Web Components als universelle Bausteine

Web Components sind keine Erfindung eines einzelnen Unternehmens. Sie sind ein Satz von Web-Standards, die vom World Wide Web Consortium (W3C) entwickelt und von allen großen Browser-Herstellern implementiert wurden. Sie sind also ein nativer Teil der Web-Plattform, genau wie das `<p>`-Tag oder das `<div>`-Element.

Eine Web Component ist im Wesentlichen ein von dir selbst definiertes, vollständig gekapseltes und wiederverwendbares HTML-Element. Du kannst ein Element wie `<user-profile-card>` oder `<special-button>` erstellen, das seine eigene Logik, sein eigenes Markup und seine eigenen Stile mitbringt.

Der entscheidende Punkt ist: Weil diese Komponenten auf Web-Standards basieren, versteht sie jeder moderne Browser von Haus aus. Sie benötigen kein Framework, um zu funktionieren. Und weil sie wie ganz normale HTML-Tags aussehen und sich auch so verhalten, können sie problemlos in jedem Framework eingesetzt werden, das HTML rendert – und das tun sie alle.

Stell es dir so vor: Ein React-Component ist wie ein speziell geformtes Puzzleteil, das nur in ein React-Puzzle passt. Eine Web Component ist wie ein universeller Legostein. Du kannst ihn mit anderen Legosteinen verbauen, aber er passt auch in ein Duplo-Projekt oder kann ganz für sich allein stehen.

#### Ein praktisches Beispiel: Deine erste agnostische Komponente

Lass uns eine einfache Komponente bauen, eine `user-profile-card`, die einen Namen und ein Avatar-Bild anzeigt. Wir schreiben sie einmal mit reinem JavaScript und nutzen sie dann in verschiedenen Umgebungen.

Der Code für eine solche Web Component könnte so aussehen:

```javascript
// user-profile-card.js

const template = document.createElement('template');
template.innerHTML = `
  <style>
    .card {
      display: flex;
      align-items: center;
      font-family: sans-serif;
      background: #f4f4f4;
      border: 1px solid #ddd;
      border-radius: 8px;
      padding: 16px;
      width: 300px;
    }
    .avatar {
      width: 60px;
      height: 60px;
      border-radius: 50%;
      margin-right: 16px;
      object-fit: cover;
    }
    .name {
      font-size: 1.2em;
      font-weight: bold;
    }
  </style>
  <div class="card">
    <img class="avatar" src="" alt="User Avatar" />
    <span class="name"></span>
  </div>
`;

class UserProfileCard extends HTMLElement {
  constructor() {
    super();
    // Shadow DOM für die Kapselung anhängen
    this.attachShadow({ mode: 'open' });
    this.shadowRoot.appendChild(template.content.cloneNode(true));

    // Elemente im Shadow DOM referenzieren
    this.nameElement = this.shadowRoot.querySelector('.name');
    this.avatarElement = this.shadowRoot.querySelector('.avatar');
  }

  // Dieser Lifecycle-Callback wird aufgerufen, wenn das Element zum DOM hinzugefügt wird.
  connectedCallback() {
    this.updateContent();
  }
  
  // Dieser Callback reagiert auf Änderungen an beobachteten Attributen.
  attributeChangedCallback(name, oldValue, newValue) {
    if (oldValue !== newValue) {
      this.updateContent();
    }
  }

  // Definiert, welche Attribute beobachtet werden sollen.
  static get observedAttributes() {
    return ['name', 'avatar'];
  }
  
  updateContent() {
    // Lese die Werte aus den HTML-Attributen
    const name = this.getAttribute('name') || 'Unbekannt';
    const avatar = this.getAttribute('avatar') || 'default-avatar.png';
    
    // Setze die Werte in den Elementen im Shadow DOM
    this.nameElement.textContent = name;
    this.avatarElement.src = avatar;
  }
}

// Definiere das neue Custom Element, damit der Browser es kennt.
window.customElements.define('user-profile-card', UserProfileCard);
```

In diesem Code passieren drei magische Dinge, die für Web Components zentral sind:

1.  **Custom Elements API (`customElements.define`):** Wir registrieren ein neues HTML-Tag namens `user-profile-card` und verknüpfen es mit unserer JavaScript-Klasse `UserProfileCard`. Ab jetzt kennt der Browser dieses Tag.
2.  **Shadow DOM (`this.attachShadow`):** Wir erstellen eine gekapselte Welt innerhalb unserer Komponente. Das HTML (`<div>`, `<img>`) und das CSS (`<style>`) existieren in diesem „Schatten-DOM“. Das bedeutet, dass das CSS unserer Karte nicht versehentlich den Rest der Seite beeinflusst und umgekehrt. Die Stile sind sicher eingesperrt.
3.  **Templates (`<template>`):** Wir definieren die Struktur unserer Komponente in einem `<template>`-Tag. Das ist effizient, da der Browser den Inhalt erst parst und rendert, wenn er tatsächlich gebraucht wird.

#### Die Komponente im Einsatz: Einmal schreiben, überall nutzen

Nachdem wir diese JavaScript-Datei in unsere HTML-Seite eingebunden haben, können wir unsere Komponente so einfach verwenden wie jedes andere HTML-Tag.

**In reinem HTML:**

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <title>Web Components Test</title>
  <script src="user-profile-card.js" defer></script>
</head>
<body>
  <h1>Meine Kontakte</h1>
  <user-profile-card 
    name="Anna Schmidt" 
    avatar="https://example.com/anna.jpg">
  </user-profile-card>
  
  <user-profile-card 
    name="Ben Müller" 
    avatar="https://example.com/ben.jpg">
  </user-profile-card>
</body>
</html>
```

Das ist der Beweis: Es funktioniert ohne ein einziges Framework. Aber jetzt kommt der wirklich spannende Teil. Wie sieht es in den Frameworks aus?

**In einem React-Projekt:**

In einer React-Komponente kannst du unser Custom Element direkt im JSX verwenden. Es fühlt sich fast wie ein natives HTML-Element an.

```jsx
// ProfilePage.js (React Component)
import React from 'react';
import './user-profile-card.js'; // Sicherstellen, dass die Web Component registriert ist

function ProfilePage() {
  const user = {
    name: 'Carla Lopez',
    avatar: 'https://example.com/carla.jpg'
  };

  return (
    <div>
      <h1>React App mit Web Component</h1>
      <user-profile-card name={user.name} avatar={user.avatar}></user-profile-card>
    </div>
  );
}
```

**In einem Vue-Projekt:**

Vue hat eine exzellente Unterstützung für Custom Elements. Du importierst die Komponente und benutzt sie im Template.

```html
<!-- App.vue (Vue Component) -->
<template>
  <div>
    <h1>Vue App mit Web Component</h1>
    <user-profile-card 
      :name="user.name" 
      :avatar="user.avatar">
    </user-profile-card>
  </div>
</template>

<script>
import './user-profile-card.js';

export default {
  data() {
    return {
      user: {
        name: 'David Chen',
        avatar: 'https://example.com/david.jpg'
      }
    }
  }
}
</script>
```

**In einem Angular-Projekt:**

Auch in Angular ist die Integration unkompliziert. Du musst deinem Modul lediglich mitteilen, dass es auch Nicht-Angular-Tags geben kann, indem du das `CUSTOM_ELEMENTS_SCHEMA` hinzufügst.

```typescript
// app.module.ts (Angular Module)
import { NgModule, CUSTOM_ELEMENTS_SCHEMA } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';

// Importiere die Web Component, um sie zu registrieren
import './user-profile-card.js'; 

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  providers: [],
  bootstrap: [AppComponent],
  schemas: [CUSTOM_ELEMENTS_SCHEMA] // Erlaube Custom Elements
})
export class AppModule {}
```

```html
<!-- app.component.html (Angular Template) -->
<div>
  <h1>Angular App mit Web Component</h1>
  <user-profile-card 
    [attr.name]="user.name" 
    [attr.avatar]="user.avatar">
  </user-profile-card>
</div>
```

Du siehst das Muster: Der Code der Web Component (`user-profile-card.js`) bleibt **exakt derselbe**. Er wurde nicht für React, Vue oder Angular angepasst. Er wurde einmal geschrieben und funktioniert überall. Das ist die Macht der Framework-Agnostik.

#### Warum das für dich wichtig ist

Die Entscheidung für einen framework-agnostischen Ansatz mit Web Components ist eine Investition in die Langlebigkeit und Flexibilität deiner Codebasis.

1.  **Zukunftssicherheit:** JavaScript-Frameworks kommen und gehen. Die Web-Standards aber bleiben und entwickeln sich weiter. Eine auf Standards basierende Komponentenbibliothek wird auch in fünf oder zehn Jahren noch relevant und nutzbar sein, unabhängig davon, welches Framework dann gerade angesagt ist.

2.  **Interoperabilität:** In großen Unternehmen arbeiten oft mehrere Teams mit unterschiedlichen Technologiestacks. Ein Team nutzt React für die öffentliche Webseite, ein anderes Angular für ein internes Dashboard. Mit Web Components können beide Teams auf dieselbe zentrale Design-System-Bibliothek zugreifen. Das sorgt für ein konsistentes Markenbild und spart enormen Entwicklungsaufwand.

3.  **Einfachheit und Stabilität:** Eine Web Component hat keine externen Abhängigkeiten von einem Framework. Sie ist ein kleines, in sich geschlossenes Paket aus HTML, CSS und JavaScript. Das macht sie robust, leichtgewichtig und einfach zu verstehen.

Wenn du also beginnst, in Komponenten zu denken, denke einen Schritt weiter. Denke nicht nur in „React-Komponenten“ oder „Vue-Komponenten“. Denke in „Web-Komponenten“. Damit baust du nicht für ein einzelnes Ökosystem, sondern für das gesamte Web. Du schreibst Code, der nicht gefangen ist, sondern frei und universell einsetzbar bleibt. Das ist deine persönliche Unabhängigkeitserklärung vom Framework-Dschungel.
