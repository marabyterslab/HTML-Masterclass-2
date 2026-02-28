# Zeitbegrenzungen und Timeouts

### Zeitbegrenzungen und Timeouts: Wenn die Uhr tickt

Stell dir vor, du füllst ein langes, kompliziertes Formular aus. Vielleicht eine Reisebuchung, ein Antrag bei einer Behörde oder eine Online-Prüfung. Du bist konzentriert, liest jede Frage sorgfältig und gibst deine Daten ein. Plötzlich wirst du abgelenkt – das Telefon klingelt, jemand steht an der Tür. Als du nach wenigen Minuten zum Bildschirm zurückkehrst, wirst du mit einer knappen Meldung begrüßt: "Ihre Sitzung ist abgelaufen. Bitte beginnen Sie von vorne." All deine Eingaben sind verloren.

Frustrierend, oder? Was für dich vielleicht nur ein Ärgernis ist, stellt für viele Menschen eine unüberwindbare Barriere dar. Zeitbegrenzungen sind eine der häufigsten Hürden in der digitalen Welt, besonders wenn es um das Ausfüllen von Formularen geht.

#### Warum Zeitdruck eine Barriere ist

Die Gründe, warum jemand mehr Zeit zum Ausfüllen eines Formulars benötigt, sind vielfältig. Menschen mit kognitiven Einschränkungen oder Lernschwierigkeiten brauchen oft länger, um Informationen zu verarbeiten und zu verstehen. Jemand mit einer motorischen Einschränkung tippt möglicherweise langsamer oder navigiert mühsamer mit assistiven Technologien wie einer Kopfmaus oder Sprachsteuerung.

Auch Nutzerinnen und Nutzer von Screenreadern benötigen in der Regel mehr Zeit, da sie sich den Inhalt einer Seite linear vorlesen lassen müssen. Genauso kann es sein, dass jemand mit einer Sehbehinderung eine Bildschirmvergrößerung nutzt und dadurch immer nur einen kleinen Ausschnitt der Seite sieht, was die Orientierung und das Ausfüllen verlangsamt.

Letztlich kann jeder von uns von einer plötzlichen Unterbrechung betroffen sein oder einfach mehr Zeit benötigen, um eine Information nachzuschlagen. Ein Design, das von allen Nutzern erwartet, eine Aufgabe in einer vorgegebenen, knappen Zeitspanne zu erledigen, ist von Natur aus exklusiv. Es schließt Menschen aus, die nicht in dieses starre Schema passen.

#### Die Regeln der Barrierefreiheit: Was die WCAG verlangt

Die Web Content Accessibility Guidelines (WCAG) haben dieses Problem erkannt und ihm ein eigenes Erfolgskriterium gewidmet: **2.2.1 Timing Adjustable (Zeitliche Steuerung anpassbar)**. Dieses Kriterium legt klare Regeln für jede Art von Zeitlimit fest, das von einer Webseite oder Anwendung gesetzt wird.

Die Grundregel ist einfach: Wenn du ein Zeitlimit einsetzt, musst du dem Nutzer die Kontrolle darüber geben. Konkret bedeutet das, dass der Nutzer eine der folgenden Möglichkeiten haben muss, *bevor* das Zeitlimit abläuft:

1.  **Abschalten:** Der Nutzer kann das Zeitlimit komplett deaktivieren.
2.  **Anpassen:** Der Nutzer kann das Zeitlimit in einem großzügigen Rahmen anpassen (die WCAG schlagen vor, dass die neue Grenze mindestens zehnmal so lang wie die ursprüngliche sein sollte).
3.  **Verlängern:** Der Nutzer wird rechtzeitig gewarnt (mindestens 20 Sekunden vor Ablauf) und kann das Limit mit einer einfachen Aktion (z. B. einem Klick) um mindestens das Zehnfache des ursprünglichen Limits verlängern.

Diese Anforderungen stellen sicher, dass niemand unerwartet aus einer Sitzung geworfen wird und seine Arbeit verliert.

#### Ausnahmen bestätigen die Regel

Natürlich gibt es Situationen, in denen ein Zeitlimit absolut notwendig und ein fester Bestandteil der Aktivität ist. Die WCAG sehen hierfür Ausnahmen vor:

*   **Echtzeit-Ereignisse:** Bei einer Online-Auktion ist das Zeitlimit für ein Gebot Teil des Spiels. Auch bei einem Konzertkartenverkauf, bei dem Tickets für wenige Minuten im Warenkorb reserviert werden, ist das Limit essentiell, um die Plätze fair wieder für andere freizugeben.
*   **Essentielle Notwendigkeit:** Wenn das Zeitlimit für den Zweck der Anwendung unerlässlich ist und eine Verlängerung die Aktivität ungültig machen würde. Ein klassisches Beispiel ist eine Online-Prüfung, bei der die Zeitmessung Teil der Bewertung ist.
*   **Sehr lange Limits:** Wenn ein Zeitlimit länger als 20 Stunden ist, wird es nicht als unmittelbare Barriere angesehen und ist von der Regel ausgenommen.

Der Schlüssel liegt darin, kritisch zu hinterfragen, ob ein Zeitlimit wirklich in eine dieser Kategorien fällt. Oft werden Timeouts aus Sicherheitsgründen implementiert, obwohl es bessere, nutzerfreundlichere Alternativen gäbe.

#### Praktische Umsetzung: Gib die Kontrolle zurück

Die beste und einfachste Lösung ist oft, gänzlich auf serverseitige Timeouts zu verzichten, die den Nutzer ausloggen. Wenn dies aus Sicherheitsgründen – zum Beispiel im Online-Banking – unumgänglich ist, gibt es bewährte Methoden, um die Erfahrung barrierefrei zu gestalten.

##### 1. Vorab informieren

Wenn ein Prozess ein Zeitlimit hat, informiere den Nutzer darüber, bevor er beginnt. Eine einfache Nachricht zu Beginn eines mehrstufigen Formulars schafft Transparenz und verhindert böse Überraschungen.

```html
<div class="hinweis-box" role="status">
  <p>Bitte beachte: Aus Sicherheitsgründen wird deine Sitzung nach 15 Minuten Inaktivität beendet. Du wirst rechtzeitig gewarnt, bevor dies geschieht.</p>
</div>
```

##### 2. Rechtzeitig und klar warnen

Die Warnung vor dem Timeout ist das Herzstück einer barrierefreien Lösung. Sie darf den Nutzer nicht bei seiner aktuellen Tätigkeit stören, muss aber unmissverständlich sein. Ein modales Dialogfenster, das über dem restlichen Inhalt der Seite erscheint, ist hierfür eine gängige und effektive Methode.

Dieser Dialog muss selbst barrierefrei sein:

*   **Fokusmanagement:** Sobald der Dialog erscheint, muss der Tastaturfokus in den Dialog verschoben werden. Er darf nicht dahinter "gefangen" bleiben.
*   **Semantik:** Der Dialog sollte als solcher ausgezeichnet sein, idealerweise mit `role="alertdialog"`.
*   **Klare Botschaft und Aktionen:** Der Text im Dialog muss klar beschreiben, was passiert, und einfache Handlungsoptionen anbieten.

Hier ist ein einfaches HTML-Grundgerüst für einen solchen Dialog:

```html
<div id="timeout-dialog" class="modal" role="alertdialog" aria-labelledby="dialog-titel" aria-describedby="dialog-beschreibung" hidden>
  <h2 id="dialog-titel">Sitzung läuft bald ab</h2>
  <p id="dialog-beschreibung">
    Deine Sitzung wird in <span id="countdown">60</span> Sekunden beendet.
  </p>
  <button id="extend-session-btn">Sitzung verlängern</button>
  <button id="logout-btn">Jetzt ausloggen</button>
</div>
```

##### 3. Die Technik dahinter

Die Logik zur Anzeige und Steuerung dieses Dialogs wird mit JavaScript umgesetzt. Du würdest zwei Timer einrichten: einen für die eigentliche Timeout-Dauer (z. B. 15 Minuten) und einen kürzeren, der die Warnung anzeigt (z. B. nach 14 Minuten).

Hier ist ein konzeptionelles JavaScript-Beispiel, das die Logik verdeutlicht:

```js
// Die Elemente aus dem DOM holen
const timeoutDialog = document.getElementById('timeout-dialog');
const extendBtn = document.getElementById('extend-session-btn');
const countdownSpan = document.getElementById('countdown');

const sessionDuration = 15 * 60 * 1000; // 15 Minuten in Millisekunden
const warningTime = 14 * 60 * 1000;     // Warnung nach 14 Minuten

let warningTimer;
let logoutTimer;

function startTimers() {
  // Timer für die Warnung
  warningTimer = setTimeout(() => {
    // Dialog anzeigen und Fokus setzen
    timeoutDialog.hidden = false;
    extendBtn.focus();
    startCountdown();
  }, warningTime);

  // Timer für den automatischen Logout
  logoutTimer = setTimeout(forceLogout, sessionDuration);
}

function resetTimers() {
  // Bestehende Timer löschen
  clearTimeout(warningTimer);
  clearTimeout(logoutTimer);
  
  // Dialog ausblenden, falls er sichtbar war
  timeoutDialog.hidden = true;

  // Timer neu starten
  startTimers();
}

function forceLogout() {
  // Hier würde die Logik für den Logout stehen
  window.location.href = '/logout';
}

// Event-Listener für den "Verlängern"-Button
extendBtn.addEventListener('click', () => {
  // Hier würdest du eine Anfrage an den Server senden,
  // um die serverseitige Session ebenfalls zu verlängern.
  console.log("Sitzung wird verlängert.");
  resetTimers();
});

// Bei jeder Nutzeraktivität (Klick, Tastendruck) die Timer zurücksetzen
document.addEventListener('click', resetTimers);
document.addEventListener('keydown', resetTimers);

// Die Timer initial starten, wenn die Seite geladen wird
startTimers();

// Die Countdown-Funktion ist hier der Einfachheit halber nicht implementiert.
```

Dieser Code zeigt das Prinzip: Nutzeraktivität setzt die Timer zurück. Wenn keine Aktivität stattfindet, erscheint die Warnung, und der Nutzer hat die einfache Möglichkeit, die Sitzung durch einen Klick zu verlängern, was wiederum die Timer zurücksetzt.

##### 4. Fortschritt speichern

Für besonders lange oder komplexe Formulare ist die beste Lösung oft, dem Nutzer zu ermöglichen, seinen Fortschritt zu speichern und später fortzufahren. Dies umgeht das Problem des Datenverlusts durch Timeouts vollständig und bietet den größten Komfort. Eine "Zwischenspeichern"-Funktion ist ein starkes Zeichen dafür, dass du die Zeit und Mühe deiner Nutzer respektierst.

Letztendlich geht es bei der Gestaltung von Zeitlimits nicht nur darum, eine WCAG-Checkbox abzuhaken. Es geht um Empathie und Respekt. Indem du den Menschen die Kontrolle über ihre Zeit gibst, baust du nicht nur barrierefreie, sondern auch fundamental benutzerfreundlichere und robustere Anwendungen. Du schaffst eine Umgebung, in der sich jeder in seinem eigenen Tempo bewegen kann, ohne Angst haben zu müssen, dass ein digitaler Countdown seine Arbeit zunichtemacht.
