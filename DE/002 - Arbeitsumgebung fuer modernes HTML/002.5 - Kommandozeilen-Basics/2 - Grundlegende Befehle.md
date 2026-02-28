# Grundlegende Befehle

### Grundlegende Befehle: Dein Werkzeugkasten für die Kommandozeile

Du sitzt vor einem schwarzen Fenster, in dem ein Cursor blinkt. Das ist die Kommandozeile, auch Terminal oder Shell genannt. Sie ist kein Relikt aus vergangenen Tagen, sondern eines der mächtigsten Werkzeuge, die du als Entwickler besitzt. Anstatt dich durch Ordner zu klicken, sprichst du direkt mit deinem Computer. Diese Sprache besteht aus Befehlen, und in diesem Kapitel lernst du die wichtigsten Vokabeln, um dich sicher und effizient in deinem System zu bewegen.

Der blinkende Cursor wartet hinter einer Zeichenfolge, dem sogenannten „Prompt“. Er könnte so aussehen: `dein-name@computer:~$`. Das `~`-Symbol steht für dein Benutzerverzeichnis (dein „Home“-Verzeichnis), und das `$`-Zeichen signalisiert dir: „Ich bin bereit für deinen Befehl.“

#### Wo bin ich? Der `pwd`-Befehl

Die erste Frage, die sich in einer neuen Umgebung stellt, ist immer: Wo befinde ich mich gerade? In der grafischen Oberfläche siehst du den Pfad oft in der Titelleiste eines Fensters. In der Kommandozeile hilft dir der Befehl `pwd` (print working directory).

Gib einfach `pwd` ein und drücke die Eingabetaste:

```bash
pwd
```

Als Antwort gibt dir das System den vollständigen, absoluten Pfad zu dem Verzeichnis aus, in dem du dich gerade aufhältst. Das könnte zum Beispiel so aussehen:

```bash
/Users/dein-name
```

Oder unter Windows (im entsprechenden Terminal):

```bash
C:\Users\dein-name
```

Dieser Befehl ist deine ständige Orientierungshilfe. Immer wenn du unsicher bist, wo du gelandet bist, ist `pwd` dein Freund.

#### Was ist hier? Der `ls`-Befehl

Nachdem du weißt, *wo* du bist, möchtest du natürlich wissen, *was* sich dort befindet. Dafür gibt es den Befehl `ls` (list). Er listet alle Dateien und Unterverzeichnisse im aktuellen Verzeichnis auf.

```bash
ls
```

Die Ausgabe könnte so aussehen:

```bash
Desktop    Documents    Downloads    Music    Pictures    Projects
```

Das ist nützlich, aber oft brauchst du mehr Informationen. Befehle in der Kommandozeile können mit sogenannten „Flags“ oder „Optionen“ erweitert werden. Das sind kurze Zusätze, die mit einem Bindestrich beginnen und das Verhalten des Befehls modifizieren.

Für `ls` sind zwei Flags besonders wichtig:

*   `-l` für eine lange Liste (long format). Diese Ansicht zeigt dir Details wie Dateiberechtigungen, Besitzer, Dateigröße und das letzte Änderungsdatum.
*   `-a` für alle Dateien (all). Standardmäßig versteckt `ls` Dateien und Verzeichnisse, deren Namen mit einem Punkt beginnen (z. B. `.git` oder `.bash_profile`). Dies sind oft Konfigurationsdateien. Mit `-a` siehst du auch sie.

Du kannst diese Flags auch kombinieren:

```bash
ls -la
```

Die Ausgabe wird nun viel detaillierter sein und auch die versteckten Dateien anzeigen. Das ist die Ansicht, die du als Entwickler am häufigsten verwenden wirst, um dir einen vollständigen Überblick zu verschaffen.

#### Wie bewege ich mich? Der `cd`-Befehl

Der wahrscheinlich am häufigsten genutzte Befehl ist `cd` (change directory). Mit ihm wechselst du von einem Verzeichnis in ein anderes. Es ist das Äquivalent zum Doppelklick auf einen Ordner.

Um in das Verzeichnis `Projects` zu wechseln, das wir oben mit `ls` gesehen haben, gibst du ein:

```bash
cd Projects
```

Dein Prompt wird sich wahrscheinlich ändern, um den neuen Ort anzuzeigen, zum Beispiel zu `dein-name@computer:~/Projects$`. Ein `pwd` würde dir jetzt `/Users/dein-name/Projects` ausgeben.

Um `cd` meisterhaft zu beherrschen, musst du ein paar besondere Pfadangaben kennen:

*   `.` (ein einzelner Punkt) steht immer für das **aktuelle Verzeichnis**. Das ist selten für `cd` nützlich, aber für andere Befehle wichtig.
*   `..` (zwei Punkte) steht für das **übergeordnete Verzeichnis**. Es ist dein Weg „eine Ebene nach oben“.

Wenn du dich in `/Users/dein-name/Projects` befindest und `cd ..` eingibst, landest du wieder in `/Users/dein-name`.

*   `~` (die Tilde) ist eine Abkürzung für dein **Home-Verzeichnis**. Egal, wie tief du in der Verzeichnisstruktur vergraben bist, mit `cd ~` kommst du immer sofort zurück in dein persönliches Startverzeichnis.
*   `/` (der Schrägstrich am Anfang eines Pfades) steht für das **Stammverzeichnis** (root directory) des Dateisystems. Ein Pfad, der mit `/` beginnt, ist ein **absoluter Pfad**. Er beschreibt den Weg von der Wurzel des Systems bis zum Ziel, zum Beispiel `/Users/dein-name/Projects/website`. Ein Pfad ohne führenden Schrägstrich ist ein **relativer Pfad**. Er beschreibt den Weg vom *aktuellen* Standort aus.

#### Wie erstelle ich etwas? `mkdir` und `touch`

Als Entwickler musst du ständig neue Ordner und Dateien für deine Projekte anlegen.

##### Verzeichnisse erstellen mit `mkdir`

Der Befehl `mkdir` (make directory) erstellt ein neues, leeres Verzeichnis.

```bash
mkdir mein-neues-projekt
```

Dieser Befehl erstellt im aktuellen Verzeichnis einen neuen Ordner namens `mein-neues-projekt`. Du kannst auch mehrere Verzeichnisse auf einmal erstellen:

```bash
mkdir css js assets
```

Das erzeugt drei separate Ordner. Wenn du eine verschachtelte Struktur erstellen willst, zum Beispiel einen `img`-Ordner innerhalb von `assets`, würdest du normalerweise erst `assets` erstellen und dann hineinwechseln. Mit dem Flag `-p` (parent) geht das in einem Schritt:

```bash
mkdir -p assets/img
```

Dieser Befehl erstellt den Ordner `assets`, falls er noch nicht existiert, und darin den Ordner `img`.

##### Leere Dateien erstellen mit `touch`

Um eine leere Datei zu erstellen, verwendest du den Befehl `touch`. Das ist perfekt, um die Grundstruktur deines Webprojekts anzulegen.

```bash
touch index.html
```

Dies erzeugt eine leere Datei mit dem Namen `index.html` im aktuellen Verzeichnis. Auch hier kannst du mehrere Dateien auf einmal anlegen:

```bash
touch index.html style.css script.js
```

Jetzt hast du die drei grundlegenden Dateien für eine Webseite mit einem einzigen Befehl erstellt.

#### Wie verwalte ich Dateien? `cp`, `mv` und `rm`

Nun, da du Dateien und Ordner erstellen kannst, musst du sie auch kopieren, verschieben, umbenennen und löschen können.

##### Kopieren mit `cp`

Der Befehl `cp` (copy) kopiert Dateien oder Verzeichnisse. Die Syntax ist `cp [QUELLE] [ZIEL]`.

Um deine `index.html` in eine Datei namens `about.html` zu kopieren, tust du Folgendes:

```bash
cp index.html about.html
```

Um eine Datei in ein anderes Verzeichnis zu kopieren, gibst du das Verzeichnis als Ziel an:

```bash
cp style.css css/
```

Dies kopiert `style.css` in den Unterordner `css`.

Um ein ganzes Verzeichnis samt Inhalt zu kopieren, benötigst du das Flag `-r` (recursive):

```bash
cp -r mein-projekt mein-projekt-backup
```

##### Verschieben und Umbenennen mit `mv`

Der Befehl `mv` (move) hat zwei Funktionen: Er verschiebt Dateien und benennt sie um. Die Logik ist dieselbe.

Um die Datei `script.js` in den Ordner `js` zu verschieben:

```bash
mv script.js js/
```

Um die Datei `about.html` in `contact.html` umzubenennen, verschiebst du sie quasi an einen neuen Namen am selben Ort:

```bash
mv about.html contact.html
```

##### Löschen mit `rm`

Der Befehl `rm` (remove) löscht Dateien. **Dieser Befehl ist mit großer Vorsicht zu genießen!** Dateien, die über die Kommandozeile mit `rm` gelöscht werden, landen nicht im Papierkorb. Sie sind in der Regel unwiderruflich weg.

Um eine einzelne Datei zu löschen:

```bash
rm contact.html
```

Um ein leeres Verzeichnis zu löschen, kannst du `rmdir` (remove directory) verwenden. Um jedoch ein Verzeichnis und seinen gesamten Inhalt zu löschen, benötigst du wieder `rm` mit dem `-r` Flag (recursive):

```bash
rm -r assets
```

Sei bei der Verwendung von `rm -r` immer absolut sicher, dass du dich im richtigen Verzeichnis befindest und wirklich alles darin löschen möchtest. Ein Tippfehler kann katastrophale Folgen haben.

#### Wie sehe ich mir den Inhalt an? `cat` und `less`

Manchmal möchtest du schnell einen Blick in eine Datei werfen, ohne einen kompletten Editor zu öffnen.

Der Befehl `cat` (concatenate) gibt den gesamten Inhalt einer Datei direkt im Terminal aus.

```bash
cat index.html
```

Das ist ideal für kurze Dateien. Bei längeren Dateien rauscht der Text einfach durch. Hier kommt `less` ins Spiel. `less` ist ein sogenannter „Pager“, der dir den Inhalt seitenweise anzeigt.

```bash
less sehr-lange-datei.txt
```

Du kannst nun mit den Pfeiltasten oder der Leertaste (für eine ganze Seite) durch die Datei navigieren. Um `less` zu beenden, drückst du einfach die Taste `q` (quit).

#### Ein typischer Arbeitsablauf

Lass uns diese Befehle zu einem sinnvollen Arbeitsablauf für ein neues Projekt zusammensetzen:

1.  **Zum Projektverzeichnis navigieren:**
    ```bash
    cd Projects
    ```
2.  **Neuen Projektordner erstellen und hineinwechseln:**
    ```bash
    mkdir fancy-website
    cd fancy-website
    ```
3.  **Die grundlegende Ordnerstruktur anlegen:**
    ```bash
    mkdir css js img
    ```
4.  **Die Startdateien erstellen:**
    ```bash
    touch index.html css/style.css js/app.js
    ```
5.  **Die Struktur überprüfen:**
    ```bash
    ls -R
    ```
    (Das `-R` Flag zeigt den Inhalt rekursiv an, also auch in allen Unterordnern)

Mit diesen wenigen Befehlen hast du die Grundlage für ein komplettes Webprojekt geschaffen – schnell, effizient und vollständig über die Tastatur gesteuert. Dies ist die Kraft der Kommandozeile. Sie mag anfangs einschüchternd wirken, aber mit jedem Befehl, den du lernst, wird sie zu einem unverzichtbaren Teil deines Werkzeugkastens.
