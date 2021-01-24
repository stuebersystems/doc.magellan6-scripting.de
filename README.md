# MAGELLAN 6 Scripting

Dies ist die deutsche Dokumentation zum Scripting in MAGELLAN 6. Die Dokumentation ist Open Source und wir haben sie mit [GitBook](https://github.com/GitbookIO/gitbook) realisiert.

> ## Wichtiger Hinweis:
> Die hier verwendete Open Source-Version von GitBook wird nicht mehr weiterentwickelt. Die aktuelle Version von GitBook ist nicht Open Source. 

## Gitbook unter Windows installieren

1. Du musst zunächst [node.js installieren](https://nodejs.org/de/download). Node.js enthält bereits den Package Manager npm.

2. Starte das Installationspaket und beantworte alle Fragen.

3. Öffne die Eingabeaufforderung als Administrator.

4. Tippe jetzt den Befehl `npm install gitbook-cli -g` ein, um eine lokale Version von GitBook zu installieren.

## Repository klonen

Dieses Repository ist ein Git-Repository. Um das Repository auf deinem lokalen Computer zu klonen, benötigst Du einen Git-Client. Entweder Du installierst Dir [Git für Windows](https://gitforwindows.org/) und arbeitest mit der Eingabeaufforderung, oder Du installierst Dir eine der zahlreichen GUIs. Zu empfehlen wären [GitHub Desktop](https://desktop.github.com) oder [SourceTree](https://www.sourcetreeapp.com).

1. Erstelle einen lokalen Ordner für die Dokumentation, z.B. `c:\docs\magellan6-bibliothek`.

2. Starte die Eingabeaufforderung und wechsle in den Ordner `c:\docs\magellan6-bibliothek`.

3. Tippe den Befehl `git clone https://github.com/stuebersystems/doc.magellan6-bibliothek.de.git` ein, um das Repository zu klonen.

## Repository als Zip-Archiv herunterladen

Willst du mit Git erstmal nichts zu tun haben, kannst Du das Repository auch als Zip-Archiv herunterladen:

1. Öffne die URL `https://github.com/stuebersystems/doc.magellan6-bibliothek.de` in deinem Webbrowser

2. Klicke auf die Schaltfläche `Clone or download` und dann auf `Download ZIP`.

3. Entpacke das Zip-Archiv in einen lokalen Ordner Deiner Wahl, z.B. `c:\docs\magellan6-bibliothek`.

## Mit GitBook arbeiten

Du hast node.js und das Package GitBook installiert, Du hast dieses Repository geklont oder als Zip-Archiv heruntergeladen. Jetzt kannst Du die Dokumentation lokal auf deinem Rechner generieren:

1. Starte die Eingabeaufforderung und wechsle in den Ordner `c:\docs\magellan6\src`.

2. Zunächst musst Du alle für die Dokumentation benötigten GitBook-Plugins installieren. Tippe dazu den Befehl `gitbook install` ein. Die GitBook-Plugins werden installiert. Dies musst Du nur einmal für diese Dokumentation machen.

3. Tippe den Befehl `gitbook build` ein. Die Dokumentation wird neu generiert.

4. Um Dir das Ergebnis anzeigen zu lassen, wechsle in den Ordner `c:\docs\magellan6-bibliothek\src\_book` und öffne die Datei `index.html` in Deinem Webbrowser.

Das Inhaltsverzeichnis findest Du in der Datei `SUMMARY.md`. 

## Weitere Informationen

+ [Alles zum Thema Git](https://git-scm.com/book/de/v2)
+ [GitBook auf GitHub](https://github.com/GitbookIO/gitbook)
