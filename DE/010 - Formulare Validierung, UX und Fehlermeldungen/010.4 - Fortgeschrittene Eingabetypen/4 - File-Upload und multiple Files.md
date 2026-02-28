# File-Upload und multiple Files

# Dateien hochladen: Das `input` Element vom Typ `file`

In der modernen Webentwicklung kommst du kaum an einem Punkt vorbei, an dem Benutzer keine Dateien hochladen müssen. Ob es sich um ein Profilbild in einem sozialen Netzwerk, einen Lebenslauf auf einer Job-Plattform oder eine Sammlung von Urlaubsfotos in einer Galerie handelt – die Interaktion mit Dateien ist ein fundamentaler Bestandteil des Webs. HTML stellt uns dafür ein spezielles Eingabeelement zur Verfügung: `<input type="file">`.

Auf den ersten Blick wirkt es täuschend einfach, doch hinter diesem Element verbergen sich einige wichtige Konzepte und Techniken, die du verstehen musst, um es korrekt und benutzerfreundlich einzusetzen.

### Das grundlegende File-Input-Element

Beginnen wir mit der einfachsten Form des File-Upload-Feldes. Um in einem Formular eine Dateiauswahl zu ermöglichen, fügst du folgenden Code ein:

```html
<form action="/upload-script" method="post" enctype="multipart/form-data">
  <label for="userfile">Wähle eine Datei aus:</label>
  <input type="file" id="userfile" name="userfile">
  <button type="submit">Hochladen</button>
</form>
```

Schauen wir uns die Teile dieses Beispiels genauer an, denn hier gibt es zwei entscheidende Details.

1.  **`<input type="file">`**: Dieses Element rendert der Browser als eine Schaltfläche (z. B. "Datei auswählen" oder "Durchsuchen...") und daneben meist einen Textbereich, der den Namen der ausgewählten Datei anzeigt. Aus Sicherheitsgründen hast du mit HTML oder CSS keinen direkten Zugriff auf den Inhalt dieses Textbereichs oder den genauen Pfad der Datei auf dem Computer des Nutzers. Der Browser schirmt das Dateisystem des Anwenders strikt ab. Ein Klick auf die Schaltfläche öffnet den systemeigenen Dateiauswahldialog, in dem der Nutzer navigieren und eine Datei auswählen kann.

2.  **`enctype="multipart/form-data"`**: Dieses Attribut im `<form>`-Tag ist absolut essenziell für den Datei-Upload. Wenn du es weglässt, wird das Formular mit dem Standard-`enctype` (`application/x-www-form-urlencoded`) gesendet. Dieser Typ kann jedoch nur Textdaten kodieren und senden. Der Browser würde in diesem Fall nur den Dateinamen als einfachen Text an den Server schicken, nicht aber die eigentlichen Dateidaten.
    `multipart/form-data` hingegen weist den Browser an, die Formulardaten in mehrere Teile aufzuteilen (engl. "multi-part"). Jeder Teil entspricht einem Formularfeld. Für das `input`-Feld vom Typ `file` wird ein eigener Teil erstellt, der die binären Daten der Datei enthält, zusammen mit Metadaten wie dem Dateinamen und dem Medientyp (MIME-Type). Nur so kann der Server die Datei korrekt empfangen und verarbeiten.

Vergiss also niemals das `enctype`-Attribut, wenn dein Formular einen Datei-Upload beinhaltet. Es ist einer der häufigsten Fehler, der zu stundenlanger, frustrierender Fehlersuche führen kann.

### Das Styling-Dilemma und die Label-Lösung

Eine der größten Herausforderungen bei der Arbeit mit `<input type="file">` ist das Styling. Jeder Browser stellt dieses Element anders dar, und die Möglichkeiten, es direkt mit CSS zu gestalten, sind extrem begrenzt. Versuche, die Hintergrundfarbe, den Rahmen oder die Schriftart der Schaltfläche zu ändern, scheitern meist oder führen zu inkonsistenten Ergebnissen.

Glücklicherweise gibt es eine elegante und weit verbreitete Lösung für dieses Problem. Die Idee ist, das originale, unschöne `input`-Element zu verstecken und stattdessen ein schick gestaltetes `<label>` als Klick-Ziel zu verwenden. Da ein `<label>`, das über das `for`-Attribut mit der `id` eines `input`-Feldes verknüpft ist, bei einem Klick das `input`-Feld aktiviert, können wir diesen Mechanismus nutzen.

So funktioniert es:

**HTML-Struktur:**

```html
<form action="/upload-script" method="post" enctype="multipart/form-data">
  <!-- Das eigentliche Input-Feld, das wir verstecken werden -->
  <input type="file" id="file-upload" name="userfile" class="hidden-input">

  <!-- Unser individuell gestaltetes Label, das wie ein Button aussieht -->
  <label for="file-upload" class="custom-file-upload">
    <i class="icon-upload"></i> Datei auswählen
  </label>
  
  <button type="submit">Hochladen</button>
</form>
```

**CSS-Styling:**

```css
/* Verstecke das originale Input-Feld. 
   Wir nutzen position: absolute und eine geringe Größe, anstatt display: none, 
   um Probleme mit der Barrierefreiheit zu vermeiden. */
.hidden-input {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}

/* Style das Label wie einen Button */
.custom-file-upload {
  display: inline-block;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border-radius: 5px;
  cursor: pointer;
  font-family: sans-serif;
  text-align: center;
  transition: background-color 0.3s;
}

.custom-file-upload:hover {
  background-color: #0056b3;
}

/* Ein kleines Icon, optional */
.icon-upload {
  /* Hier könntest du ein SVG-Icon oder eine Icon-Font verwenden */
  margin-right: 8px;
}
```

Mit dieser Technik klickt der Nutzer auf das schön gestaltete `<label>`. Der Klick wird an das versteckte `<input type="file">` weitergeleitet, wodurch sich der Dateiauswahldialog öffnet. So erhältst du volle Kontrolle über das Design, ohne die Funktionalität zu verlieren.

### Dateitypen einschränken mit dem `accept`-Attribut

Oft möchtest du dem Nutzer signalisieren, welche Art von Dateien erwartet wird. Wenn du ein Profilbild hochladen lässt, sind wahrscheinlich nur Bilddateien wie JPG, PNG oder GIF relevant. Für diesen Zweck gibt es das `accept`-Attribut.

Es dient als Hinweis für den Browser, die Anzeige im Dateiauswahldialog zu filtern.

```html
<!-- Akzeptiere nur PNG-Bilder -->
<input type="file" name="profile_pic" accept="image/png">

<!-- Akzeptiere alle Arten von Bilddateien -->
<input type="file" name="gallery_image" accept="image/*">

<!-- Akzeptiere PDF-Dokumente und Microsoft Word-Dateien -->
<input type="file" name="document" accept=".pdf,.doc,.docx">

<!-- Eine Kombination aus MIME-Typen und Dateiendungen -->
<input type="file" name="mixed_files" accept="image/jpeg,image/png,.pdf">
```

Du kannst das `accept`-Attribut auf drei Arten verwenden:

1.  **MIME-Typen:** Eine genaue Angabe wie `image/jpeg` oder `application/pdf`. Dies ist die zuverlässigste Methode.
2.  **Wildcards:** Ein Sternchen `*` kann einen Teil des MIME-Typs ersetzen, z. B. `image/*` für alle Bildtypen oder `audio/*` für alle Audio-Dateien.
3.  **Dateiendungen:** Angaben wie `.jpg` oder `.pdf`. Diese Methode ist weniger zuverlässig, da ein Nutzer eine Datei mit einer falschen Endung versehen könnte, wird aber von den meisten Browsern verstanden.

**Wichtiger Sicherheitshinweis:** Das `accept`-Attribut ist eine reine Komfortfunktion für den Nutzer. Es ist **keine Sicherheitsmaßnahme**. Ein technisch versierter Nutzer kann den Filter im Dateidialog einfach umgehen oder eine Anfrage manuell an deinen Server senden. Du musst **immer** auf dem Server überprüfen, ob die hochgeladene Datei tatsächlich dem erwarteten Typ und Inhalt entspricht. Verlasse dich niemals allein auf clientseitige Validierungen.

### Der Upload mehrerer Dateien

Was aber, wenn der Nutzer nicht nur eine, sondern gleich mehrere Dateien auf einmal hochladen soll, zum Beispiel für eine Fotogalerie? Auch dafür hat HTML eine einfache Lösung: das `multiple`-Attribut.

Dieses boolesche Attribut signalisiert dem Browser, dass der Nutzer im Dateiauswahldialog mehrere Dateien auswählen darf (üblicherweise durch Halten der `Strg`- oder `Cmd`-Taste).

```html
<form action="/upload-gallery" method="post" enctype="multipart/form-data">
  <label for="gallery-files">Wähle deine Bilder aus (mehrere möglich):</label>
  <input type="file" id="gallery-files" name="galleryfiles[]" multiple>
  <button type="submit">Galerie erstellen</button>
</form>
```

Hier gibt es eine wichtige Konvention zu beachten: den `name`-Attributwert `galleryfiles[]`. Die eckigen Klammern `[]` am Ende des Namens sind ein Hinweis für viele serverseitige Sprachen (insbesondere PHP), die eingehenden Dateien als Array oder Liste zu interpretieren. Ohne die Klammern würde der Server möglicherweise nur die erste ausgewählte Datei verarbeiten und die anderen ignorieren. Dein Backend-Code kann dann durch dieses Array iterieren und jede Datei einzeln speichern.

### Ein kleiner Ausblick: Clientseitige Verarbeitung mit JavaScript

Obwohl dies ein HTML-Kapitel ist, ist es wichtig zu wissen, dass du mit JavaScript noch viel mehr aus dem File-Input herausholen kannst. Über das `files`-Property des DOM-Elements erhältst du Zugriff auf eine `FileList`, die alle vom Nutzer ausgewählten Dateien enthält.

```html
<input type="file" id="file-input" multiple>
<div id="file-list"></div>

<script>
  const fileInput = document.getElementById('file-input');
  const fileListDiv = document.getElementById('file-list');

  fileInput.addEventListener('change', (event) => {
    // Leere die bisherige Liste
    fileListDiv.innerHTML = '';
    
    // Die event.target.files Eigenschaft ist ein FileList-Objekt
    const files = event.target.files;

    if (files.length === 0) {
      fileListDiv.innerHTML = '<p>Keine Dateien ausgewählt.</p>';
      return;
    }

    const list = document.createElement('ul');
    fileListDiv.appendChild(list);

    for (const file of files) {
      const listItem = document.createElement('li');
      // Zeige Name und Größe der Datei an (Größe in Bytes)
      const sizeInKB = (file.size / 1024).toFixed(2);
      listItem.textContent = `${file.name} (${sizeInKB} KB)`;
      list.appendChild(listItem);
    }
  });
</script>
```

Dieser Code lauscht auf das `change`-Ereignis des `input`-Feldes, das ausgelöst wird, sobald der Nutzer eine oder mehrere Dateien ausgewählt hat. Anschließend iteriert das Skript durch die `FileList` und zeigt die Namen und Größen der ausgewählten Dateien an.

Dies eröffnet viele Möglichkeiten für eine verbesserte User Experience:
*   **Vorschau von Bildern:** Du kannst Bilder vor dem Upload direkt im Browser anzeigen.
*   **Clientseitige Validierung:** Du kannst die Dateigröße oder den Dateityp bereits im Browser prüfen und dem Nutzer sofort Feedback geben, wenn eine Datei zu groß ist oder das falsche Format hat.
*   **Fortschrittsanzeigen:** Mit fortgeschritteneren Techniken (wie `XMLHttpRequest` oder der `fetch`-API) kannst du den Upload-Fortschritt in Echtzeit anzeigen.

Diese JavaScript-Interaktionen bauen jedoch alle auf dem soliden Fundament auf, das du mit einem korrekt strukturierten HTML-Formular, dem passenden `enctype`-Attribut und den Attributen `accept` und `multiple` legst.
