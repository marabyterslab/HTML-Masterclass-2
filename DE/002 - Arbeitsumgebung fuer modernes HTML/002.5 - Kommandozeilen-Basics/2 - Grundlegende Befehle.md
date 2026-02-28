# Grundlegende Befehle

### Grundlegende Befehle: Dein Werkzeugkasten für die Kommandozeile

Die Kommandozeile, auch Terminal oder Shell genannt, ist auf den ersten Blick vielleicht etwas einschüchternd. Ein schwarzes Fenster mit blinkendem Cursor, das auf deine Eingaben wartet. Doch lass dich nicht täuschen: Dieses unscheinbare Werkzeug ist eines der mächtigsten Instrumente in deinem Entwickler-Alltag. Es ermöglicht dir, direkt mit dem Betriebssystem deines Computers zu kommunizieren, ohne dich durch unzählige Menüs und Fenster klicken zu müssen. Du sprichst quasi direkt mit dem Herzen der Maschine.

Bevor wir in die Befehle eintauchen, müssen wir ein zentrales Konzept verstehen: das **aktuelle Arbeitsverzeichnis** (current working directory). Stell dir das Dateisystem deines Computers wie ein riesiges Haus mit unzähligen Räumen (Verzeichnissen) vor. Wenn du das Terminal öffnest, befindest du dich in einem bestimmten Raum, meistens in deinem persönlichen Benutzerverzeichnis (Home-Verzeichnis). Jeder Befehl, den du ausführst, bezieht sich standardmäßig auf diesen Raum.

#### Orientierung: Wo bin ich und was ist hier?

Die ersten Fragen, die du dir im Terminal stellst, sind immer dieselben: Wo genau bin ich gelandet? Und was befindet sich hier um mich herum? Dafür gibt es zwei fundamentale Befehle.

**`pwd` (Print Working Directory)**

Dieser Befehl ist so einfach wie genial. Er tut genau eine Sache: Er zeigt dir den vollständigen, absoluten Pfad deines aktuellen Standorts an. Ein absoluter Pfad beginnt immer an der Wurzel (Root) des Dateisystems, die unter Linux und macOS durch einen einzelnen Schrägstrich (`/`) symbolisiert wird.

```bash
pwd
```

Die Ausgabe könnte zum Beispiel so aussehen:

```bash
/Users/deinbenutzername/Documents/Projekte
```

Jetzt weißt du genau, in welchem "Raum" du dich befindest.

**`ls` (List)**

Nachdem du weißt, wo du bist, möchtest du natürlich wissen, was sich in diesem Verzeichnis befindet. Der Befehl `ls` listet alle Dateien und Unterverzeichnisse im aktuellen Arbeitsverzeichnis auf.

```bash
ls
```

Die Ausgabe ist oft eine einfache, nach Spalten sortierte Liste:

```bash
index.html   style.css   images   scripts
```

Diese einfache Form ist nützlich für einen schnellen Überblick. Oft benötigst du jedoch mehr Informationen. Hier kommen die sogenannten "Flags" oder "Optionen" ins Spiel. Das sind kleine Zusätze, die das Verhalten eines Befehls modifizieren. Sie werden meist mit einem Bindestrich eingeleitet.

Eine der nützlichsten Kombinationen ist `ls -la`:

```bash
ls -la
```

*   Das `-l` steht für "long format" und gibt eine detaillierte Listenansicht aus. Du siehst nun Zugriffsrechte, den Besitzer der Datei, die Dateigröße, das letzte Änderungsdatum und den Dateinamen.
*   Das `-a` steht für "all" und zeigt auch versteckte Dateien an. Versteckte Dateien erkennen wir daran, dass ihr Name mit einem Punkt beginnt (z.B. `.git` oder `.gitignore`). Diese sind für die Konfiguration von Programmen und Projekten essenziell, werden aber standardmäßig ausgeblendet, um die Ansicht nicht zu überladen.

Die Ausgabe von `ls -la` ist wesentlich informativer:

```bash
drwxr-xr-x   5 deinbenutzername  staff   160 18 Okt 10:30 .
drwxr-xr-x  12 deinbenutzername  staff   384 18 Okt 10:28 ..
drwxr-xr-x   3 deinbenutzername  staff    96 18 Okt 10:29 images
drwxr-xr-x   3 deinbenutzername  staff    96 18 Okt 10:29 scripts
-rw-r--r--   1 deinbenutzername  staff  1234 18 Okt 10:30 index.html
-rw-r--r--   1 deinbenutzername  staff   567 18 Okt 10:30 style.css
```

#### Navigation: Von einem Ort zum anderen

Jetzt, da du dich orientieren kannst, ist es an der Zeit, dich zu bewegen. Der Befehl dafür ist `cd` (Change Directory).

**`cd` (Change Directory)**

Mit `cd` wechselst du in ein anderes Verzeichnis. Du gibst einfach `cd` gefolgt von deinem Ziel an.

Um in das Unterverzeichnis `scripts` zu wechseln, das wir eben mit `ls` gesehen haben, tippst du:

```bash
cd scripts
```

Dein Prompt im Terminal wird sich wahrscheinlich ändern und dir anzeigen, dass du dich nun im Verzeichnis `scripts` befindest. Wenn du jetzt `pwd` ausführst, siehst du den neuen Pfad.

Es gibt einige nützliche Abkürzungen für die Navigation:

*   **`cd ..`**: Wechselt in das übergeordnete Verzeichnis. Wenn du in `/Users/deinbenutzername/Projekte` bist, landest du mit `cd ..` in `/Users/deinbenutzername`.
*   **`cd ~`** oder einfach nur **`cd`**: Bringt dich immer direkt zurück in dein Home-Verzeichnis, egal wo du dich gerade im Dateisystem verirrt hast. Die Tilde (`~`) ist das universelle Symbol für dein Benutzerverzeichnis.
*   **`cd /`**: Bringt dich zur Wurzel (Root) des gesamten Dateisystems.

Du kannst sowohl relative als auch absolute Pfade verwenden. Ein relativer Pfad (wie `scripts` oder `..`) geht von deinem aktuellen Standort aus. Ein absoluter Pfad (wie `/Users/deinbenutzername/Projekte`) ist eine vollständige Adresse, die von überall aus funktioniert.

#### Erschaffen und Verändern: Dateien und Verzeichnisse anlegen

Als Webentwickler wirst du ständig neue Projekte, Ordnerstrukturen und Dateien erstellen. Auch das geht blitzschnell auf der Kommandozeile.

**`mkdir` (Make Directory)**

Dieser Befehl erstellt ein neues Verzeichnis. Um eine typische Projektstruktur für eine Webseite anzulegen, könntest du Folgendes tun:

```bash
mkdir mein-neues-projekt
```

Du kannst auch mehrere Verzeichnisse auf einmal erstellen:

```bash
mkdir css js assets
```

**`touch` (Create Empty File)**

Der Befehl `touch` hat eigentlich die Aufgabe, den Zeitstempel einer Datei zu aktualisieren. Ein praktischer Nebeneffekt, der heute seine Hauptanwendung ist: Wenn die angegebene Datei nicht existiert, wird sie einfach leer erstellt. Perfekt, um schnell neue HTML-, CSS- oder JavaScript-Dateien anzulegen.

```bash
touch index.html
touch css/style.css
```

Im zweiten Beispiel erstellen wir die Datei `style.css` direkt im bereits existierenden Unterverzeichnis `css`.

**`cp` (Copy)**

Mit `cp` kopierst du Dateien oder Verzeichnisse. Die Syntax lautet `cp [QUELLE] [ZIEL]`.

Um eine Datei zu duplizieren:

```bash
cp index.html about.html
```

Um eine Datei in ein anderes Verzeichnis zu kopieren:

```bash
cp logo.png assets/
```

**`mv` (Move)**

Der Befehl `mv` hat zwei Funktionen: Verschieben und Umbenennen. Die Syntax ist identisch mit `cp`: `mv [QUELLE] [ZIEL]`.

Um eine Datei umzubenennen, verschiebst du sie quasi an einen neuen Namen am selben Ort:

```bash
mv script.js main.js
```

Um eine Datei in ein anderes Verzeichnis zu verschieben:

```bash
mv main.js js/
```

Nach diesem Befehl befindet sich die Datei `main.js` im Ordner `js` und nicht mehr am ursprünglichen Ort.

#### Aufräumen: Dateien und Verzeichnisse entfernen

Genauso wichtig wie das Erstellen ist das saubere Entfernen von Dingen, die du nicht mehr benötigst. Hier ist allerdings Vorsicht geboten! Die Kommandozeile hat keinen Papierkorb. Was einmal mit diesen Befehlen gelöscht wurde, ist in der Regel endgültig weg.

**`rm` (Remove)**

Mit `rm` löschst du Dateien.

```bash
rm temp.html
```

**`rmdir` (Remove Directory)**

Dieser Befehl löscht **leere** Verzeichnisse. Wenn sich noch Dateien im Verzeichnis befinden, wird sich `rmdir` weigern, es zu löschen.

```bash
rmdir leeres-verzeichnis
```

**`rm -r` (Remove Recursively)**

Oft möchtest du ein Verzeichnis und seinen gesamten Inhalt auf einmal löschen. Hierfür nutzt du den `rm`-Befehl mit der Option `-r` (rekursiv). Dieser Befehl steigt in das Verzeichnis hinab, löscht alle Inhalte und schließlich das Verzeichnis selbst. **Sei extrem vorsichtig mit diesem Befehl!** Eine falsche Eingabe kann ganze Teile deines Systems löschen.

```bash
rm -r altes-projekt
```

#### Inhalte ansehen: Ein kurzer Blick in Dateien

Manchmal willst du nicht gleich einen ganzen Editor öffnen, nur um kurz nachzusehen, was in einer Datei steht.

**`cat` (Concatenate)**

Der Befehl `cat` gibt den gesamten Inhalt einer Datei direkt im Terminal aus. Das ist super für kleine Konfigurationsdateien oder kurze HTML-Schnipsel.

```bash
cat index.html
```

Bei längeren Dateien rauscht der Inhalt einfach durch das Fenster. Hierfür gibt es eine bessere Alternative.

**`less`**

`less` ist ein sogenannter Pager. Er zeigt dir den Inhalt einer Datei seitenweise an und erlaubt dir, mit den Pfeiltasten oder der Leertaste bequem durchzuscrollen. Das ist ideal für längere Log-Dateien oder Quelltexte.

```bash
less main.js
```

Um `less` wieder zu verlassen, drückst du einfach die Taste `q` (für "quit").

Diese Handvoll Befehle – `pwd`, `ls`, `cd`, `mkdir`, `touch`, `cp`, `mv`, `rm` und `less` – bilden das absolute Fundament für deine Arbeit auf der Kommandozeile. Sie geben dir die volle Kontrolle über die Struktur deines Projekts. Mit ihnen navigierst, erschaffst und verwaltest du dein digitales Arbeitsumfeld präzise und effizient.
