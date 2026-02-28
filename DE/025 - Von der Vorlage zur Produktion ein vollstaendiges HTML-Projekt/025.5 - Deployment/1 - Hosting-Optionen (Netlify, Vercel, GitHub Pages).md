# Hosting-Optionen (Netlify, Vercel, GitHub Pages)

### Hosting-Optionen: Netlify, Vercel und GitHub Pages

Du hast dein HTML-Projekt fertiggestellt. Die Struktur steht, das CSS sorgt für eine ansprechende Optik und vielleicht hast du mit JavaScript sogar für Interaktivität gesorgt. Alles funktioniert perfekt – auf deinem eigenen Computer. Aber wie kommt deine Kreation nun von deiner lokalen Festplatte ins globale Netz, sodass jeder sie über eine URL aufrufen kann? Die Antwort liegt im Hosting.

Früher war das Hosten einer Website ein komplexer Vorgang. Du musstest einen Server mieten, dich per FTP verbinden, Dateien manuell hochladen und dich um Konfigurationen kümmern. Heute ist dieser Prozess dank moderner Plattformen, die speziell für die Bedürfnisse von Entwicklern geschaffen wurden, radikal vereinfacht worden. Diese Dienste setzen auf einen Git-basierten Workflow: Du verwaltest deinen Code in einem Git-Repository (zum Beispiel auf GitHub), und die Hosting-Plattform kümmert sich um den Rest.

In diesem Kapitel schauen wir uns drei der populärsten und einsteigerfreundlichsten Optionen für das Hosting von statischen Websites an: GitHub Pages, Netlify und Vercel. Alle drei bieten großzügige kostenlose Tarife, die für persönliche Projekte, Portfolios oder Prototypen mehr als ausreichend sind.

#### GitHub Pages: Der unkomplizierte Klassiker

GitHub Pages ist die direkteste und einfachste Möglichkeit, ein Projekt zu hosten, das bereits auf GitHub liegt. Der Dienst ist tief in die Plattform integriert und wurde ursprünglich dafür geschaffen, Dokumentationen für Open-Source-Projekte bereitzustellen. Heute ist es eine vollwertige Hosting-Lösung für jede statische Website.

**Wie es funktioniert**

Der Prozess ist denkbar einfach. Du hast zwei primäre Möglichkeiten:

1.  **Benutzer- oder Organisationsseite:** Du erstellst ein spezielles Repository mit dem Namen `dein-benutzername.github.io`. Alles, was du in den `main`-Branch dieses Repositories hochlädst, wird automatisch unter der URL `https://dein-benutzername.github.io` veröffentlicht.
2.  **Projektseite:** Für jedes beliebige andere Repository kannst du in den Einstellungen unter dem Reiter „Pages“ das Hosting aktivieren. Dort wählst du aus, welcher Branch als Quelle dienen soll (üblicherweise `main` oder ein dedizierter `gh-pages`-Branch). Deine Seite wird dann unter einer URL wie `https://dein-benutzername.github.io/dein-projektname` erreichbar sein.

Jedes Mal, wenn du neuen Code in den ausgewählten Branch pushst, wird GitHub Pages deine Seite automatisch aktualisieren.

**Vorteile:**

*   **Extrem einfache Einrichtung:** Wenn dein Code ohnehin auf GitHub liegt, sind es nur wenige Klicks, bis deine Seite live ist.
*   **Vollständig kostenlos:** Es gibt keine versteckten Kosten für das Hosting von öffentlichen Repositories.
*   **Direkte Integration:** Dein Code und deine gehostete Seite leben am selben Ort. Das macht die Verwaltung sehr übersichtlich.

**Nachteile:**

*   **Reines Static-Hosting:** Du kannst keine serverseitige Logik ausführen (wie z. B. PHP oder eine Node.js-Datenbankanbindung). Es ist ausschließlich für HTML, CSS und clientseitiges JavaScript gedacht.
*   **Begrenzte Build-Prozesse:** Während du mit GitHub Actions komplexere Build-Schritte einrichten kannst, sind die Standardoptionen sehr rudimentär. Für Projekte, die einen Build-Schritt erfordern (wie bei vielen modernen JavaScript-Frameworks), sind andere Dienste oft komfortabler.
*   **Funktionsumfang:** Im Vergleich zu Netlify und Vercel fehlen fortgeschrittene Funktionen wie automatische Formularverarbeitung, A/B-Tests oder Serverless Functions.

GitHub Pages ist die perfekte Wahl für dein erstes Portfolio, die Dokumentation eines Projekts oder eine einfache Landingpage. Es ist robust, zuverlässig und nimmt dir fast jeglichen Konfigurationsaufwand ab.

#### Netlify: Das Kraftpaket für die Jamstack-Ära

Netlify hat sich als eine der führenden Plattformen für die moderne Webentwicklung etabliert, die oft unter dem Schlagwort „Jamstack“ (JavaScript, APIs, Markup) zusammengefasst wird. Netlify ist weit mehr als nur ein Hoster; es ist eine komplette Automatisierungsplattform, die den gesamten Prozess von der Code-Änderung bis zum Live-Deployment optimiert.

**Wie es funktioniert**

Du verbindest dein Git-Repository (von GitHub, GitLab oder Bitbucket) mit Netlify. Die Plattform analysiert dein Projekt und erkennt in der Regel automatisch, wie es gebaut werden muss. Bei einem reinen HTML/CSS/JS-Projekt ist kein Build-Schritt nötig. Bei einem Projekt, das ein Framework wie Hugo, Eleventy oder React verwendet, führt Netlify die notwendigen Build-Befehle aus.

Der Kern von Netlify ist das Konzept des **Continuous Deployment (CD)**: Jedes Mal, wenn du einen `git push` zu deinem Haupt-Branch machst, startet Netlify automatisch den Build-Prozess und stellt die neue Version deiner Website bereit – und das in Sekundenschnelle.

**Vorteile:**

*   **Globales CDN (Content Delivery Network):** Deine Website wird nicht von einem einzigen Server, sondern von einem weltweiten Netzwerk von Servern ausgeliefert. Das bedeutet, dass deine Seite für Besucher aus der ganzen Welt extrem schnell lädt, da die Inhalte vom geografisch nächstgelegenen Server kommen.
*   **Atomic Deploys und sofortige Rollbacks:** Netlify stellt eine neue Version deiner Seite erst dann live, wenn sie vollständig und erfolgreich gebaut wurde. Dieser „atomare“ Prozess verhindert, dass Besucher jemals eine kaputte oder unvollständige Seite sehen. Außerdem kannst du mit einem einzigen Klick zu jeder beliebigen vorherigen Version deiner Website zurückkehren.
*   **Umfangreiche Zusatzfunktionen:** Netlify bietet eine beeindruckende Palette an integrierten Diensten, die weit über das Hosting hinausgehen:
    *   **Form Handling:** Füge ein einfaches Attribut zu deinem HTML-Formular hinzu, und Netlify sammelt die Einsendungen für dich, ohne dass du einen Backend-Server benötigst.
    *   **Serverless Functions:** Du kannst kleine Backend-Funktionen in JavaScript oder Go schreiben, die bei Bedarf ausgeführt werden, zum Beispiel um mit einer API zu kommunizieren.
    *   **Identity & Authentication:** Füge deiner Seite ganz einfach eine Benutzeranmeldung hinzu.
    *   **A/B-Testing:** Teste verschiedene Versionen einer Seite gegeneinander.
*   **Deploy Previews:** Für jeden Pull Request erstellt Netlify eine eigene, live einsehbare Vorschauversion deiner Seite. Das ist unglaublich wertvoll für die Zusammenarbeit, da Teammitglieder Änderungen in einer realen Umgebung prüfen können, bevor sie in den Haupt-Branch übernommen werden.

**Nachteile:**

*   **Potenziell überladen:** Für eine extrem einfache HTML-Seite kann der Funktionsumfang von Netlify überwältigend wirken.
*   **Build-Minuten:** Im kostenlosen Tarif ist die Zeit, die Netlify für das Bauen deiner Projekte aufwendet, begrenzt. Für die meisten statischen Seiten ist dieses Limit jedoch sehr großzügig bemessen.

Netlify ist die ideale Wahl, wenn du eine robuste, skalierbare und zukunftssichere Plattform suchst, die mit deinen Projekten wachsen kann.

#### Vercel: Performance und Developer Experience im Fokus

Vercel ist der Hauptkonkurrent von Netlify und wurde vom Team hinter Next.js, einem populären React-Framework, entwickelt. Obwohl die Plattform eine erstklassige Unterstützung für Next.js bietet, ist sie ein ebenso exzellenter Hoster für jede Art von statischer Website. Vercel legt einen extremen Fokus auf Performance und eine reibungslose Entwicklererfahrung (Developer Experience, DX).

**Wie es funktioniert**

Der Workflow ist dem von Netlify sehr ähnlich: Du verbindest dein Git-Repository, Vercel erkennt dein Projekt, und bei jedem `git push` wird deine Seite automatisch gebaut und bereitgestellt. Vercel optimiert dabei deine Assets (Bilder, Skripte, Stylesheets) aggressiv, um die schnellstmöglichen Ladezeiten zu garantieren.

**Vorteile:**

*   **Herausragende Performance:** Vercel ist bekannt für sein globales Edge-Netzwerk, das nicht nur statische Inhalte, sondern auch Serverless Functions extrem schnell ausliefert. Automatische Bildoptimierung und andere Caching-Strategien sind standardmäßig aktiviert.
*   **Exzellente Developer Experience:** Die Benutzeroberfläche ist extrem aufgeräumt und intuitiv. Der gesamte Prozess vom Verbinden des Repositories bis zum Live-Deployment fühlt sich nahtlos und durchdacht an.
*   **Branchenführende Preview Deployments:** Ähnlich wie Netlify erstellt Vercel Vorschau-Deployments für jeden Push und jeden Pull Request. Das Besondere bei Vercel ist die Integration eines Kommentar-Tools direkt auf diesen Vorschauseiten, was das Feedback-Einholen im Team noch einfacher macht.
*   **Analytics:** Vercel bietet ein eingebautes, datenschutzfreundliches Analytics-Tool, mit dem du Besucherzahlen und die Performance deiner Seite messen kannst, ohne auf externe Dienste wie Google Analytics zurückgreifen zu müssen.
*   **Serverless und Edge Functions:** Wie Netlify ermöglicht auch Vercel das einfache Hosten von Backend-Funktionen, die eng mit deinem Frontend-Code verzahnt sind.

**Nachteile:**

*   **Starker Fokus auf Next.js:** Obwohl jede statische Seite unterstützt wird, sind einige der fortschrittlichsten Funktionen und Dokumentationen stark auf das Next.js-Ökosystem ausgerichtet.
*   **Ähnlichkeit zu Netlify:** Die Wahl zwischen Vercel und Netlify kann schwierig sein, da sich ihre Kernfunktionen stark überschneiden. Oft entscheiden persönliche Präferenz oder spezifische Projektanforderungen.

Vercel ist die erste Wahl, wenn absolute Spitzenperformance dein Hauptziel ist oder wenn du planst, mit modernen JavaScript-Frameworks wie Next.js oder SvelteKit zu arbeiten. Die nahtlose Entwicklererfahrung macht es zu einer Freude, damit zu arbeiten.

#### Welche Option ist die richtige für dich?

Die Wahl der richtigen Hosting-Plattform hängt von deinem Projekt und deinen Zielen ab. Hier ist eine einfache Entscheidungshilfe:

*   **Wähle GitHub Pages, wenn...**
    *   ...du dein allererstes Projekt online stellen möchtest.
    *   ...dein Code bereits auf GitHub ist und du die schnellste und einfachste Lösung suchst.
    *   ...du eine einfache Portfolio-Seite, einen Blog oder eine Projekt-Dokumentation hosten willst und keine erweiterten Funktionen benötigst.

*   **Wähle Netlify, wenn...**
    *   ...du eine leistungsstarke All-in-One-Lösung suchst, die mit deinem Projekt mitwächst.
    *   ...du von integrierten Features wie Formularverarbeitung, Authentifizierung oder A/B-Testing profitieren möchtest, ohne ein eigenes Backend aufzusetzen.
    *   ...du eine robuste CI/CD-Pipeline mit atomaren Deploys und einfachen Rollbacks schätzt.

*   **Wähle Vercel, wenn...**
    *   ...maximale Ladegeschwindigkeit und Performance für dich oberste Priorität haben.
    *   ...du eine erstklassige Entwicklererfahrung mit einem sauberen Interface und nahtlosen Prozessen suchst.
    *   ...du in einem Team arbeitest und die kollaborativen Features der Preview Deployments voll ausnutzen willst.

Unabhängig von deiner Wahl machen es dir alle drei Plattformen erstaunlich einfach, den letzten und wichtigsten Schritt zu gehen: dein Werk mit der Welt zu teilen. Der Sprung von `localhost` zu einer öffentlich erreichbaren URL war noch nie so zugänglich und unkompliziert.
