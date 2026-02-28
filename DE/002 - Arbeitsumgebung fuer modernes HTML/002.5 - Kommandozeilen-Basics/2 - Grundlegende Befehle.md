# Grundlegende Befehle

### Grundlegende Befehle

Stell dir die Kommandozeile als ein direktes Gespräch mit deinem Computer vor. Anstelle von Klicks und Fenstern gibst du kurze, präzise Textbefehle ein und der Computer antwortet dir – ebenfalls in Textform. Anfangs mag das fremd wirken, aber du wirst schnell merken, wie unglaublich effizient und mächtig diese Art der Interaktion ist. In der Webentwicklung wirst du die Kommandozeile ständig nutzen, sei es für Versionskontrolle mit Git, die Installation von Paketen mit einem Paketmanager wie npm oder einfach nur, um schnell deine Projektdateien zu verwalten.

Dieser Werkzeugkasten an Befehlen ist dein Fundament. Die meisten dieser Befehle sind auf Unix-ähnlichen Systemen wie macOS und Linux zu Hause. Wenn du unter Windows arbeitest, ist die Verwendung des Windows Subsystem for Linux (WSL) dringend zu empfehlen, da es dir eine native Linux-Umgebung und damit den Zugang zu denselben Standardwerkzeugen ermöglicht, die in der Webentwicklung vorherrschen.

#### Navigieren im Dateisystem

Das Erste, was du beherrschen musst, ist die Bewegung. Du musst wissen, wo du bist und wie du von einem Ort zum anderen kommst.

**`pwd` (Print Working Directory)**

Der einfachste und oft erste Befehl, den man lernt. Er tut genau eine Sache: Er sagt dir, in welchem Verzeichnis (Ordner) du dich gerade befindest.

```bash
pwd
```

Die Ausgabe ist ein Pfad, der vom Wurzelverzeichnis deines Systems bis zu deinem aktuellen Standort führt. Auf einem Mac oder Linux-System könnte das so aussehen:

```bash
/Users/deinname/Projekte/HTML-Masterclass
```

Dieser absolute Pfad ist deine genaue Adresse im Dateisystem.

**`ls` (List)**

Nachdem du weißt, *wo* du bist, willst du wissen, *was* um dich herum ist. Der Befehl `ls` listet den Inhalt des aktuellen Verzeichnisses auf.

```bash
ls
```

Die Ausgabe könnte so aussehen:

```bash
Modul-1  Modul-2  Modul-3  README.md
```

`ls` hat sehr nützliche Erweiterungen, sogenannte "Flags" oder "Optionen", die du mit einem Bindestrich hinzufügst.

*   **`ls -l`**: Zeigt eine lange Liste an (long format). Hier bekommst du viel mehr Details: Dateiberechtigungen, Besitzer, Dateigröße und das Datum der letzten Änderung.
*   **`ls -a`**: Zeigt alle Dateien an (all), auch die versteckten. Versteckte Dateien beginnen mit einem Punkt (z. B. `.git` oder `.env`). Diese sind in der Entwicklung extrem wichtig.

Du kannst Flags auch kombinieren:

```bash
ls -la
```

Dieser Befehl ist einer der am häufigsten genutzten, um sich schnell einen Überblick zu verschaffen.

**`cd` (Change Directory)**

Jetzt kommt die Bewegung ins Spiel. Mit `cd` wechselst du das Verzeichnis.

Um in das Verzeichnis `Modul-2` zu wechseln, das wir mit `ls` gesehen haben, tippst du:

```bash
cd Modul-2
```

Wenn du jetzt `pwd` ausführst, siehst du, dass sich dein Standort geändert hat.

Es gibt ein paar spezielle Abkürzungen für `cd`, die du dir unbedingt merken solltest:

*   **`cd ..`**: Wechselt eine Ebene nach oben, also in das übergeordnete Verzeichnis. Das ist essenziell für die Navigation.
*   **`cd ~`** oder einfach nur **`cd`**: Bringt dich immer direkt in dein Heimatverzeichnis (Home Directory), egal wo du dich gerade befindest.
*   **`cd /`**: Bringt dich in das Wurzelverzeichnis (Root Directory) deines Dateisystems.

Ein wichtiger Unterschied ist der zwischen relativen und absoluten Pfaden. Wenn du `cd Modul-2` eingibst, ist das ein relativer Pfad – er funktioniert nur, weil sich `Modul-2` in deinem aktuellen Verzeichnis befindet. Ein absoluter Pfad wie `cd /Users/deinname/Projekte` funktioniert von überall aus, weil er den kompletten Weg vom Startpunkt des Systems beschreibt.

#### Dateien und Verzeichnisse erstellen und löschen

Wenn du dich bewegen kannst, ist der nächste logische Schritt, deine Umgebung zu gestalten.

**`mkdir` (Make Directory)**

Dieser Befehl erstellt ein neues, leeres Verzeichnis. Wenn du in deinem Projekt einen Ordner für Stylesheets anlegen möchtest, geht das so:

```bash
mkdir css
```

Du kannst auch mehrere Verzeichnisse auf einmal erstellen:

```bash
mkdir css js images
```

**`touch` (Create File)**

Mit `touch` erstellst du eine neue, leere Datei. Dies ist perfekt, um die Grundstruktur für ein Webprojekt anzulegen.

```bash
touch index.html
```

Wenn du nun `ls` ausführst, siehst du deine frisch erstellte `index.html`-Datei.

**`rm` (Remove)**

Mit `rm` löschst du Dateien.

```bash
rm alte-datei.txt
```

**Wichtiger Hinweis:** Der `rm`-Befehl ist endgültig. Es gibt keinen Papierkorb. Eine mit `rm` gelöschte Datei ist in der Regel unwiederbringlich verloren. Gehe also sehr bewusst damit um.

Um ein leeres Verzeichnis zu löschen, kannst du `rmdir` (Remove Directory) verwenden.

```bash
rmdir leeres-verzeichnis
```

Wenn das Verzeichnis jedoch Inhalt hat, wird `rmdir` mit einer Fehlermeldung abbrechen. Um ein Verzeichnis und seinen gesamten Inhalt rekursiv zu löschen, verwendest du `rm` mit dem Flag `-r`.

```bash
rm -r altes-projekt
```

**Sei extrem vorsichtig mit diesem Befehl!** Er fragt nicht nach und löscht alles im angegebenen Verzeichnis und allen Unterverzeichnissen. Ein falscher `rm -r`-Befehl kann großen Schaden anrichten.

#### Dateien bearbeiten

Nun, da du Dateien und Ordner erstellen und löschen kannst, musst du sie auch verschieben und kopieren können.

**`cp` (Copy)**

Der Befehl `cp` kopiert eine Datei. Du gibst zuerst die Quelle an und dann das Ziel.

```bash
cp index.html backup.html
```

Dieser Befehl erstellt eine exakte Kopie von `index.html` unter dem Namen `backup.html` im selben Verzeichnis.

Du kannst eine Datei auch in ein anderes Verzeichnis kopieren:

```bash
cp index.html archiv/
```

Um ein ganzes Verzeichnis samt Inhalt zu kopieren, benötigst du wieder das rekursive Flag `-r`:

```bash
cp -r projekt-vorlage mein-neues-projekt
```

**`mv` (Move)**

Der `mv`-Befehl hat zwei Hauptfunktionen: das Verschieben und das Umbenennen von Dateien und Verzeichnissen.

Zum Verschieben einer Datei gibst du Quelle und Zielverzeichnis an:

```bash
mv style.css css/
```

Dieser Befehl verschiebt die Datei `style.css` in den Ordner `css`.

Die zweite Funktion ist das Umbenennen. Technisch gesehen ist Umbenennen nichts anderes, als eine Datei an denselben Ort, aber unter einem neuen Namen zu "verschieben".

```bash
mv alte-bezeichnung.html neue-bezeichnung.html
```

Hiermit wird die Datei `alte-bezeichnung.html` in `neue-bezeichnung.html` umbenannt. Dasselbe funktioniert auch mit Verzeichnissen.

#### Inhalte anzeigen

Manchmal willst du nur schnell einen Blick in eine Datei werfen, ohne sie in einem Editor zu öffnen.

**`cat` (Concatenate)**

Der `cat`-Befehl liest eine oder mehrere Dateien und gibt ihren Inhalt direkt im Terminal aus.

```bash
cat index.html
```

Das ist sehr praktisch für kleine Konfigurationsdateien oder um schnell den Inhalt eines HTML-Dokuments zu überprüfen. Bei sehr langen Dateien ist `cat` unpraktisch, da der gesamte Inhalt auf einmal durchrauscht.

**`less`**

Für längere Dateien ist `less` die bessere Wahl. Es ist ein sogenannter "Pager", der dir den Inhalt seitenweise anzeigt.

```bash
less sehr-lange-datei.log
```

Du kannst mit den Pfeiltasten nach oben und unten scrollen. Um `less` zu beenden, drückst du einfach die Taste `q`.

#### Ein praktischer Workflow

Stellen wir uns vor, du startest ein neues, kleines Webprojekt namens "portfolio". Mit den gelernten Befehlen kannst du die gesamte Grundstruktur in wenigen Sekunden anlegen:

```bash
# 1. Erstelle das Hauptverzeichnis für das Projekt
mkdir portfolio

# 2. Wechsle in das neue Verzeichnis
cd portfolio

# 3. Erstelle die typische Ordnerstruktur
mkdir css js images

# 4. Erstelle die grundlegenden Dateien
touch index.html css/styles.css js/app.js

# 5. Überprüfe deine Struktur
ls -R
```

Der letzte Befehl, `ls -R`, listet den Inhalt rekursiv auf und zeigt dir den gesamten Verzeichnisbaum, den du gerade erstellt hast. Die Ausgabe würde etwa so aussehen:

```bash
.:
index.html  css/  js/  images/

./css:
styles.css

./js:
app.js

./images:
```

Mit nur fünf Befehlen hast du eine saubere, organisierte Projektstruktur geschaffen. Das ist die Eleganz und Geschwindigkeit der Kommandozeile. Diese grundlegenden Werkzeuge bilden das Rückgrat deiner täglichen Arbeit und ermöglichen es dir, schnell und präzise mit deinem Computer zu kommunizieren.
