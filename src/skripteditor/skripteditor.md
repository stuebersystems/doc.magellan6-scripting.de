#Skripteditor

Der Magellan-Skripteditor ist das Werkzeug, mit dem Sie Skripte editieren oder neu erstellen können.

![Der Skripteditor](../skripteditor/skripteditor.png)

##Starten des Editors {#Starten des Editors}

Um den Magellan Skripteditor zu starten, gehen Sie in den Windows-Explorer und starten Sie die Datei MagScriptEditor.exe. Sie finden diese Datei in Abhängigkeit vom Betriebssystem unter folgendem Verzeichnis:

Betriebssystem|Pfad
--|--
Windows 2000/XP|C:\Programme\Stueber Systems\Magellan 6
Windows Vista|C:\Program Files\Stueber Systems\Magellan 6
Windows Windows 7 (32-bit)|C:\Programme\Stueber Systems\Magellan 6
Windows Server 2008/Windows 7 (64-bit)|C:\Program Files (x86)\Stueber Systems\Magellan 6

Sie können nun ein Magellan-Skript auswählen, indem Sie im Menü ```Datei``` auf ```Öffnen``` klicken. Der Skripteditor versucht automatisch das gerade aktuelle Skripteverzeichnis anzuzeigen, so dass Sie sofort alle verfügbaren Skripte angezeigt bekommen.

Wenn Sie beispielsweise die Datei Schüler einschulen.dws auswählen, dann wird das Skript zum Einschulen von Schülern geladen.

Sie können nun das Skript durchblättern, um sich den Quellcode anzuschauen. Die Skripte sind in der Regel sauber strukturiert und mit Kommentaren versehen, so dass Sie sich schnell zurechtfinden werden.

##Skriptstruktur {#Skriptstruktur}

Bei einem Magellan-Skript wird zwischen dem Quellcode-Teil und dem Interface-Teil unterschieden.
Der Quellcode-Teil enthält den eigentlichen Skriptcode. Damit sind die Prorammanweisungen gemeint, die später im Kontext von Magellan ausgeführt werden. 

Der Interface-Teil dagegen dient als Bindeglied zwischen Magellan und dem Skripteditor. Hier wird die Schnittstelle zwischen Magellan und dem Skript definiert, d.h. es werden Konstanten und zum Teil auch Funktionen deklariert, die später von Magellan automatisch zur Verfügung gestellt werden.

![2 Der Skripteditor mit dem Interface-Teil des geöffnetem Skript in der Ansicht “Interface-Emulation“](../skripteditor/interfaceemulation.png)

Betrachten wir uns beispielsweise den Interface-Teil des bereits erwähnten Importskripts für das Einschulen von Schülern. Sie finden dort die Deklaration von diversen Variablen des Objektes TSchueler. Dies sind genau jene Variablen, die durch den Magellan-Administrator beim Aufruf des Einschulens von Schülern zur Verfügung gestellt werden, d.h. die Angaben werden automatisch ermittelt und übergeben.

Während Sie mit dem Skripteditor arbeiten, steht Magellan aber nicht zur Verfügung. In diesem Fall werden die Variablen einfach „von Hand“ gesetzt, um einen Stand-alone-Einsatz des Skripts zu gewährleisten. 

Dieser Ansatz hat zudem den Vorteil, dass Sie sehr schnell die Eingabeparameter für Testzwecke umsetzen können, indem Sie einfach andere Werte eintragen. Sie müssen in diesem Fall nicht erst Magellan aufrufen, um eine Änderung am Skript auszutesten.

Es gilt, dass alles, was Sie im Interface-Teil des Skripts eintippen, später nicht mehr genutzt wird.
Die Trennung zwischen eigentlichem Quellcode und der Interface-Definition spiegelt sich auch in der Dateiaufteilung wieder. Jedes Magellan- Skript wird immer in Form von zwei Dateien gespeichert. 
>Der Quellcode befindet sich in einer Datei mit der Endung .dws und der Interface-Teil in einer Datei mit der Endung .int. Wenn Magellan auf das Skript zugreift, dann wird die Interface-Datei einfach ignoriert.

##Skripte ändern und testen {#Skripte ändern und testen}

Wenn Sie Lust haben eigene Änderungen vorzunehmen, dann probieren Sie es einfach aus. Der beste Einstieg ist immer, dem aktuellen Skript ein paar syntaktische Fehler zu spendieren, um dann zu beobachten, wie der Skripteditor darauf reagiert.

![Syntaxfehler werden direkt im Skripteditor markiert](../skripteditor/skripteditor fehler.png)

Tippen Sie z.B. ein paar Sonderzeichen ein oder eine unsinnige Buchstabenfolge wie in der Abbildung. Klicken Sie anschließend im Menü ```Extras``` auf ```Skript compilieren```. 

Der Skripteditor wird zu Recht meckern und die geänderte Zeile rot markieren. Wenn Sie die Eingabe wieder entfernen und erneut den Befehl ```Skript compilieren``` ausführen, wird die Meldung „Script compiled, no messages“ erscheinen, d.h. das Skript ist (zumindest syntaktisch) wieder in Ordnung.

Sie können auch auf den Befehl ```Ausführen```  klicken, um das gesamte Skript auszuführen. Hierbei müssen Sie allerdings auf ein paar Punkte achten:

*	Beim ersten Ausführen eines Skripts wird das Skript wahrscheinlich kein sinnvolles Ergebnis liefern. Das liegt daran, dass die Vorgabewerte im Interface-Teil nicht zu Ihrem System passen. Womöglich ist Ihre Datenbankdatei in einem ganz anderen Verzeichnis untergebracht oder das Passwort ist geändert worden. Sie müssen also darauf achten, dass die Werte richtig gesetzt sind.
	
*	Einige Skripte führen ohne Ihre Magellan-Host-Anwendung schlichtweg keine Operationen aus. Dies ist immer dann der Fall, wenn der Datenbankzugriff ausschließlich im Kontext von Magellan erfolgen kann. Diese Skripte setzen eine bereits offene Datenbankverbindung voraus, die der Skripteditor nicht liefern kann. Hierzu gehören z.B. die Skripte für die Notenberechnungen (Abitur, Berufsschule usw.). In diesen Fällen müssen Sie das Skript doch aus Magellan heraus aufrufen, um Änderungen testen zu können.

* Ein syntaktisch korrektes Skript muss nicht immer ein sinnvolles Ergebnis liefern. Wenn Sie eine Endlosschleife programmiert haben, dann „hängt“ das Skript, obwohl die Kompilierung keine Fehler angezeigt hat.

Wenn Sie ein wenig mit dem Skripteditor gearbeitet haben, werden Sie sehr schnell ein Gefühl für dieses Werkzeug bekommen.

##Weitere Funktionen {#Weitere Funktionen}

Der Magellan-Skripteditor bietet für die Skriptprogrammierung eine ganze Reihe von Annehmlichkeiten:

Funktion|Inhalt
--|--
Drucken| Sie können das ganze Skript oder auch nur einen markierten Teil des Skripts ausdrucken. Wenn Sie einen Farbdrucker besitzen können Sie den Skriptcode sogar mit farbiger Syntaxunterscheidung auf Papier bringen.
Suchen und Ersetzen|Wer schon einmal selbst programmiert hat, der weiß, wie wichtig die Funktionen zum Suchen und Ersetzen sein können. Wenn Sie beispielsweise eine Variable umbenennen wollen, dann müssen Sie nicht mühsam den ganzen Quellcode nach jedem Vorkommen dieser Variable durchforsten, sondern können dies bequem über ein Dialogfenster erledigen.
Editor-Optionen|Sie können das Erscheinungsbild, d.h. Farben, Schriftarten usw., Ihrem Geschmack entsprechend einstellen.
