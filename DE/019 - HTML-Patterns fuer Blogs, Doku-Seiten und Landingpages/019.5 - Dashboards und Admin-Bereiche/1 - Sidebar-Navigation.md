# Sidebar-Navigation

### Sidebar-Navigation: Das Rückgrat deines Dashboards

Wenn du an eine komplexe Webanwendung denkst – sei es ein Administrations-Dashboard, eine Dokumentationsseite oder ein Content-Management-System – fällt dir wahrscheinlich sofort ein zentrales Element ins Auge: die Sidebar-Navigation. Sie ist oft das erste, was wir sehen und das letzte, was wir benutzen, bevor wir eine Seite verlassen. Sie ist das stabile Rückgrat, das uns Orientierung gibt und den schnellen Zugriff auf alle wichtigen Bereiche einer Anwendung ermöglicht.

Im Gegensatz zu einer horizontalen Hauptnavigation, die du auf vielen öffentlichen Websites findest und die meist nur eine Handvoll Hauptkategorien enthält, ist eine Sidebar-Navigation für die Tiefe und Komplexität von internen Bereichen oder sehr inhaltsreichen Seiten konzipiert. Sie bietet Platz für Dutzende von Links, hierarchische Strukturen und Interaktionselemente, ohne den Hauptinhaltsbereich zu überladen. Lass uns gemeinsam erkunden, wie du eine solche Navigation semantisch korrekt mit HTML aufbaust und sie für den modernen Einsatz vorbereitest.

#### Die semantische Grundstruktur

Eine gute Sidebar beginnt mit sauberem, semantischem HTML. Es ist verlockend, alles einfach in `<div>`-Container zu packen, aber wir können es besser. Eine typische Seitenstruktur mit einer Sidebar besteht aus zwei Hauptteilen: der Navigation selbst und dem Hauptinhaltsbereich.

Das `<aside>`-Element ist hier dein Freund. Es ist per Definition für Inhalte gedacht, die nur am Rande mit dem Hauptinhalt der Seite zu tun haben – eine perfekte Beschreibung für eine Navigationsleiste, die das gesamte Anwendungs-Interface umgibt, aber nicht Teil des Artikels oder des Datensatzes ist, den du gerade bearbeitest.

Innerhalb des `<aside>`-Elements kommt dann das `<nav>`-Element zum Einsatz. Während `<aside>` den gesamten Bereich der Seitenleiste umschließt, signalisiert `<nav>` explizit, dass der Inhalt darin eine Navigation darstellt. Das ist nicht nur für Suchmaschinen, sondern vor allem für assistive Technologien wie Screenreader von unschätzbarem Wert.

Die Navigation selbst wird klassischerweise als ungeordnete Liste (`<ul>`) aufgebaut. Jeder Menüpunkt ist ein Listenelement (`<li>`), das einen Anker-Tag (`<a>`) für den eigentlichen Link enthält.

Schauen wir uns ein einfaches, aber robustes Grundgerüst an:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mein Dashboard</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <aside class="sidebar">
        <div class="sidebar-header">
            <a href="/" class="logo">Mein Projekt</a>
        </div>
        <nav class="sidebar-nav">
            <ul>
                <li><a href="/dashboard">Dashboard</a></li>
                <li><a href="/users">Benutzerverwaltung</a></li>
                <li><a href="/products">Produkte</a></li>
                <li><a href="/settings">Einstellungen</a></li>
                <li><a href="/logout">Abmelden</a></li>
            </ul>
        </nav>
    </aside>

    <main class="main-content">
        <h1>Willkommen im Dashboard</h1>
        <p>Hier siehst du alle wichtigen Informationen auf einen Blick.</p>
        <!-- Der restliche Inhalt der Seite kommt hier hin -->
    </main>

</body>
</html>
```

In diesem Beispiel haben wir:
1.  Ein `<aside>`-Element, das als Container für die gesamte Seitenleiste dient.
2.  Ein optionales Header-Element innerhalb der Sidebar für ein Logo oder einen Projektnamen.
3.  Das `<nav>`-Element, das die eigentliche Navigationsliste umschließt.
4.  Eine klassische `<ul>`-Liste für die Menüpunkte.
5.  Ein `<main>`-Element, das den Hauptinhalt aufnimmt. Diese Trennung ist essenziell für die Barrierefreiheit, da sie Screenreadern erlaubt, direkt zum wesentlichen Inhalt zu springen.

#### Das Layout mit CSS zum Leben erwecken

Ohne CSS würde unser HTML einfach untereinander dargestellt. Um das typische Sidebar-Layout zu erzeugen, bei dem die Navigation links und der Inhalt rechts steht, sind moderne CSS-Layout-Techniken wie Flexbox oder CSS Grid ideal. Flexbox ist für dieses zweispaltige Layout oft die einfachste und direkteste Lösung.

Wir wenden `display: flex` auf den `<body>`-Tag an, der unsere beiden Hauptcontainer (`<aside>` und `<main>`) enthält.

```css
/* Grundlegende Styles für den Body */
body {
    display: flex;
    min-height: 100vh;
    margin: 0;
    font-family: sans-serif;
}

/* Die Sidebar selbst */
.sidebar {
    width: 250px; /* Feste Breite für die Sidebar */
    flex-shrink: 0; /* Verhindert, dass die Sidebar schrumpft */
    background-color: #2c3e50;
    color: #ecf0f1;
    display: flex;
    flex-direction: column;
}

.sidebar-header {
    padding: 20px;
    font-size: 1.5rem;
    font-weight: bold;
    text-align: center;
}

.logo {
    color: #ecf0f1;
    text-decoration: none;
}

/* Die Navigation in der Sidebar */
.sidebar-nav ul {
    list-style: none;
    padding: 0;
    margin: 0;
}

.sidebar-nav a {
    display: block;
    padding: 15px 20px;
    color: #ecf0f1;
    text-decoration: none;
    transition: background-color 0.2s;
}

.sidebar-nav a:hover {
    background-color: #34495e;
}

/* Der Hauptinhaltsbereich */
.main-content {
    flex-grow: 1; /* Nimmt den restlichen verfügbaren Platz ein */
    padding: 30px;
    background-color: #f4f6f9;
}
```

Mit diesem CSS haben wir eine klassische, linksbündige und statische Sidebar erstellt. Das `flex-shrink: 0` auf der Sidebar ist wichtig, damit sie ihre feste Breite von `250px` behält, auch wenn der Viewport schmaler wird. Das `flex-grow: 1` auf dem `.main-content` sorgt dafür, dass dieser Bereich flexibel ist und den gesamten verbleibenden Platz ausfüllt.

#### Erweiterte Muster für moderne Anforderungen

Eine einfache, statische Sidebar ist ein guter Anfang, aber in der Praxis stoßen wir schnell auf weitere Anforderungen.

##### Hierarchische Navigation (Untermenüs)

Selten besteht eine Navigation nur aus einer Ebene. In Dashboards gibt es oft Bereiche mit Unterpunkten, wie zum Beispiel "Einstellungen" mit den Unterpunkten "Profil", "Sicherheit" und "Benachrichtigungen". Semantisch ist die Lösung dafür denkbar einfach: Wir nisten eine weitere `<ul>`-Liste in das `<li>`-Element des übergeordneten Menüpunkts.

```html
<nav class="sidebar-nav">
    <ul>
        <li><a href="/dashboard">Dashboard</a></li>
        <li><a href="/users">Benutzerverwaltung</a></li>
        <li class="has-submenu">
            <a href="/settings">Einstellungen</a>
            <ul class="submenu">
                <li><a href="/settings/profile">Profil</a></li>
                <li><a href="/settings/security">Sicherheit</a></li>
                <li><a href="/settings/notifications">Benachrichtigungen</a></li>
            </ul>
        </li>
    </ul>
</nav>
```

Die Logik zum Ein- und Ausklappen dieser Untermenüs wird typischerweise mit JavaScript umgesetzt, das auf einen Klick auf den übergeordneten Menüpunkt reagiert. Das HTML-Gerüst liefert dafür bereits die perfekte, logische Struktur.

##### Responsive und einklappbare Sidebar

Auf kleinen Bildschirmen ist eine permanent sichtbare Sidebar von 250 Pixeln Breite eine massive Platzverschwendung. Das gängigste Muster ist hier, die Sidebar standardmäßig auszublenden und sie über einen "Hamburger"-Button bei Bedarf einzublenden.

Dazu benötigen wir etwas JavaScript, um eine Klasse umzuschalten, und CSS, das auf diese Klasse reagiert.

**HTML-Anpassung:** Wir fügen einen Button zum Ein- und Ausklappen hinzu. Dieser sollte außerhalb der Sidebar platziert werden, damit er auch bei geschlossener Sidebar sichtbar ist, zum Beispiel im Header des Hauptinhalts.

```html
<!-- Irgendwo im main-content Header -->
<button class="sidebar-toggle" aria-expanded="false" aria-controls="sidebar">
    Menü
</button>

<!-- Die Sidebar bekommt eine ID für die Verknüpfung -->
<aside class="sidebar" id="sidebar">
    <!-- ... -->
</aside>
```

**CSS-Anpassung:** Wir nutzen `transform`, um die Sidebar aus dem sichtbaren Bereich zu schieben, und holen sie bei Vorhandensein einer `is-open`-Klasse (die wir per JS setzen) wieder herein.

```css
/* ... bestehendes CSS ... */

@media (max-width: 768px) {
    .sidebar {
        position: fixed; /* Aus dem normalen Fluss nehmen */
        left: 0;
        top: 0;
        height: 100%;
        transform: translateX(-100%); /* Standardmäßig versteckt */
        transition: transform 0.3s ease-in-out;
        z-index: 1000;
    }

    body.sidebar-is-open .sidebar {
        transform: translateX(0); /* Sichtbar machen */
    }

    .sidebar-toggle {
        display: block; /* Nur auf kleinen Bildschirmen anzeigen */
    }
}
```

**JavaScript:** Ein kurzer Skript-Block kümmert sich um die Logik.

```javascript
document.addEventListener('DOMContentLoaded', () => {
    const sidebarToggle = document.querySelector('.sidebar-toggle');
    const body = document.body;

    if (sidebarToggle) {
        sidebarToggle.addEventListener('click', () => {
            body.classList.toggle('sidebar-is-open');

            // ARIA-Attribut für Barrierefreiheit aktualisieren
            const isExpanded = body.classList.contains('sidebar-is-open');
            sidebarToggle.setAttribute('aria-expanded', isExpanded);
        });
    }
});
```
Dieser Code schaltet die Klasse `sidebar-is-open` auf dem `<body>` um und aktualisiert das `aria-expanded`-Attribut des Buttons. Dies ist ein entscheidender Schritt für die Barrierefreiheit, da er Screenreadern mitteilt, ob das Menü gerade geöffnet oder geschlossen ist.

##### Barrierefreiheit (Accessibility) im Fokus

Eine gute Sidebar-Navigation ist eine barrierefreie Sidebar-Navigation. Einige wichtige Punkte haben wir bereits berührt:

1.  **Semantisches HTML:** Die Verwendung von `<aside>`, `<nav>`, `<ul>`, `<li>` und `<a>` ist die Grundlage.
2.  **ARIA-Attribute:** `aria-expanded` am Toggle-Button ist unerlässlich. `aria-controls` verknüpft den Button logisch mit dem Element, das er steuert (in unserem Fall die Sidebar mit `id="sidebar"`).
3.  **Fokus-Management:** Wenn ein Nutzer die Sidebar per Button öffnet, sollte der Fokus idealerweise auf das erste interaktive Element in der Sidebar springen. Dies erfordert etwas mehr JavaScript, verbessert die Benutzererfahrung für Tastaturnutzer aber erheblich.
4.  **Tastaturbedienbarkeit:** Durch die Verwendung von Standard-HTML-Elementen wie `<button>` und `<a>` ist die grundlegende Bedienung per Tastatur (Tab-Taste zum Navigieren, Enter zum Auslösen) bereits sichergestellt.

Die Sidebar-Navigation ist weit mehr als nur eine Liste von Links. Sie ist ein mächtiges Werkzeug zur Strukturierung komplexer Anwendungen. Mit einem soliden semantischen Fundament, flexiblem CSS und einem durchdachten Ansatz für Interaktivität und Barrierefreiheit schaffst du eine intuitive und robuste Benutzererfahrung, die das Herzstück deines Dashboards oder deiner Dokumentationsseite bildet.
