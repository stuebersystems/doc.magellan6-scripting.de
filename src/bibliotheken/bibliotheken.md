# Bibliotheken{#Bibliotheken}

Die Leistungsfähigkeit eines Scripting-Mechanismus hängt vor allem von den integrierten Funktionsbibliotheken ab. Den Skripten in Magellan stehen folgende Bibliotheken zur Verfügung.

* **ODBC-Bibliothek: **
Diese Bibliothek stellt Funktionen für den Zugriff auf ODBC zur Verfügung. ODBC steht für Open Database Connectivity und ist eine Datenbank-Middleware, die einen universellen SQL-Zugriff auf verschiedene Datenbank- und Dateisysteme ermöglicht (z.B. Excel, Access, Firebird, SQL-Server usw.).
ODBC wird in Magellan vor allem für den Import und Export von Daten verwendet. So ist beispiels-weise ein Import aus einer alten dBase-Schulverwaltung nach Magellan problemlos möglich.

* **IB-Bibliothek:**  
Diese Bibliothek stellt die wichtigsten Zugriffsroutinen zur Verfügung, um direkt mit Firebird kommunizieren zu können. Dabei wird eine offene Datenbankverbindung von Seiten der Host-Anwendung vorausgesetzt. Das Nutzen dieser bereits vorhandenen Verbindung ermöglicht einen schnellen Zugriff auf die Daten-bank, ohne dass eine separate Verbindung aufgebaut werden muss. Außerdem laufen alle Datenbankoperationen im Transaktionskontext der Host-Anwendung ab.

In Magellan werden diese Funktionen überall dort verwendet, wo ausschließlich auf die Magellan-Datenbank zugegriffen wird (z.B. beim Synchronisieren oder Versetzen von Schülern).

* **SDTF-Bibliothek:** 
Diese Bibliothek stellt Funktionen für den Zugriff auf SDTF-Dateien zur Verfügung. SDTF steht für  Schuldatentransferformat und ist ein textbasiertes Austauschformat für Daten aus der Schulverwaltung. Jede Textzeile stellt einen Datensatz dar, der wie folgt aufgebaut ist:

````
<LineType>;<Field_1>;<Field_2>;...;<Field_n>
````

In Magellan wird ein Zugriff auf diese Dateien vor allem bei der Kommunikation mit daVinci ge-braucht.
*	**OBOX-Bibliothek:** 
Diese Bibliothek dient zur Ausgabe eines Fortschrittbalkens bzw. zur Ausgabe von Meldungen (Fehler, Warnungen, Hinweise usw.).

##	Die ODBC-Bibliothek{#Die ODBC-Bibliothek}

Die ODBC-Bibliothek stellte in früheren Zeiten Funktionen für den Zugriff auf die Datenbank über ODBC zur Verfügung. Dies sind vorallem Funktionen zum Ausführen von SQL- Anweisungen (z.B. DELETE, UPDATE, INSERT oder SELECT). 

Die Implementation der Bibliothek funktioniert jetzt über eine native Verbindung, so dass ein ODBC-Treiber nicht mehr benötigt wird. Aus Kompatiblitätsgründen, wurde die Bibliothek nicht umbenannt.

Es finden sich aber Routinen zum Ermitteln von Metadaten (Tabellennamen, Feldnamen usw.) und zum Auslesen von Fehlercodes. Alle Funktionen besitzen den Präfix odbc_.

Zu beachten ist, dass je nach Datenbankgrundlage der SQL-Dialekt verschieden sein kann (SQL89, SQL92 oder SQL3). Auch unterstützt z.B. ein Client-Server-System in der Regel viel mehr SQL-Befehle als ein Desktop-System.

<table class="table">
<caption></caption>
<thead>
<tr>
<th colspan=2 >ODBC-Bibliothek</th>
    </tr>
 </thead>
<tbody>
<tr>
    <th>Funktion</th>
        <th align=left>odbc_CreateAccessDB</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>odbc_CreateAccessDB(FileName: String): Boolean;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Erzeugt eine neue leerer Access-Datenbankdatei. Sollte diese Datei bereits existieren, dann wird sie ersetzt. Bei Erfolg liefert die Funktion TRUE zurück.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_ConnectToAccess</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_ConnectToAccess(FileName, WrkgrpFileName, UserName, 
Password: String): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Stellt eine Verbindung zu einer Access-Datenbank her. Sie müssen dabei den Dateinamen der Datenbank und den Dateinamen der Arbeitsgruppendatei übergeben. Handelt es sich um eine geschützte Access-Datenbank, dann müssen Sie auch UserName und Password übergeben. Der Rückgabewert ist ein Handle auf die aktive Datenbankverbindung.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_ConnectToDBase</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_ConnectToDBase(FolderName: String): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Stellt eine Verbindung zu einer dBase-Datenbank her. Sie müssen dabei in FolderName das Verzeichnis übergeben, indem sich die DBF-Dateien befinden. Der Rückgabewert ist ein Handle auf die aktive Datenbankverbindung.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_ConnectToExcel</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_ConnectToExcel(FileName: String): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Stellt eine Verbindung zu einer Excel-Datei her. Sie müssen dabei den Namen der Excel-Datei übergeben. Der Rückgabewert ist ein Handle auf die aktive Excel-Verbindung.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_ConnectToText</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_ConnectToText(FileName: String): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Stellt eine Verbindung zu einer CSV-Text-Datei her. Sie müssen dabei den Namen der Text-Datei übergeben. Der Rückgabewert ist ein Handle auf die aktive Verbindung.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_ConnectToFirebird</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>odbc_ConnectToFirebird(Server, Protocol, FileName, UserName, Password: String): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Stellt eine Verbindung zu einer Firebird-Datenbank her. Sie müssen den Namen/IP-Adresse des Datenbankservers, das Protokoll (LOCAL, TCPIP), den Namen der Datenbankdatei, den Benutzernamen und das Kennwort übergeben. Der Rückgabewert ist ein Handle auf die aktive Datenbankverbindung.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_Disconnect</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_Disconnect(Connection: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Löst eine Verbindung wieder auf und gibt die entsprechenden Ressourcen frei.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_StartTransaction</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_StartTransaction(Connection: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Beendet den Auto-Commit-Modus und startet eine neue Transaktion.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_EndTransaction</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_EndTransaction(Connection: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Beendet die aktuelle Transaktion durch ein Commit und schaltet um in den Auto-Commit-Modus.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_Commit</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_Commit(Connection: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Führt ein Commit durch und startet anschließend eine neue Transaktion.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_Rollback</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_Rollback(Connection: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Führt ein Rollback durch und startet anschließend eine neue Transaktion.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_CreateCatalog</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_CreateCatalog(Connection: Integer): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Erzeugt einen Katalog, mit dessen Hilfe Meta-Daten zur Datenbank ausgelesen werden können.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetTableCount</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetTableCount(Catalog: Integer): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert die Anzahl der definierten Tabellen einer Datenbank zurück.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetTableName</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetTableName(Catalog: Integer; Index: Integer): String;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert den Namen der mit Index indizierten Datenbanktabelle zurück.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetStoredProcCount</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetStoredProcCount(Catalog: Integer): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert die Anzahl der definierten Prozeduren einer Datenbank zurück.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
    <th align=left>    </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>    </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>   </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetStoredProcName</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetStoredProcName(Catalog: Integer; Index: Integer): String;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert den Namen der mit Index indizierten Datenbankprozedur zurück.</td>
    </td>
  </tr>
<tr>
    <th>Funktion</th>
        <th align=left>odbc_DestroyCatalog</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_DestroyCatalog(Catalog: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Gibt einen erstellten Katalog wieder frei.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_CreateCommand</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_CreateCommand(Connection: Integer; SQL: String): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Erstellt einen SQL-Befehl, führt ihn aber noch nicht aus. Die Funktion liefert bei Erfolg ein Handle auf den erstellten Befehl zurück, andern falls 0.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_DestroyCommand</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_DestroyCommand(Command: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Gibt einen mit odbc_CreateCommand erstellten SQL-Befehl wieder frei.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_Execute</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_Execute(Command: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Führt einen mit odbc_CreateCommand erstellten SQL-Befehl aus. Dabei darf es sich nur um SQL-Befehle handeln, die als Ergebnis keine Datenmenge liefern (z.B. INSERT, UPDATE, DELETE).</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_RowsAffected</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>Syntax:
function odbc_RowsAffected(Command: Integer): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Beschreibung:
Liefert die Anzahl der Datensätze zurück, die durch ein INSERT, UPDATE oder DELETE betroffen waren. Diese Funktion macht nur in Verbindung mit einem vorher ausgeführten odbc_Execute Sinn.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_Open</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_Open(Command: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Öffnet eine mit odbc_CreateCommand erstellte SQL-Abfrage.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_EOF</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_EOF(Query: Integer): Boolean;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert TRUE zurück, falls der Datensatzeiger der mit Query verbundenen Abfrage am Ende der aktiven Datenmenge steht.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_BOF</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_BOF(Query: Integer): Boolean;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert TRUE zurück, falls der Datensatzeiger der mit Query verbundenen Abfrage am Anfang der aktiven Datenmenge steht.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_First</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_First(Query: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Springt zum ersten Datensatz der mit Query verbundenen aktiven
Datenmenge.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_Next</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_Next(Query: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Springt zum nächsten Datensatz der mit Query verbundenen aktiven
Datenmenge.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_Prior</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_Prior(Query: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Springt zum vorherigen Datensatz der mit Query verbundenen aktiven
Datenmenge.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_Last</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_Last(Query: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Springt zum letzten Datensatz der mit Query verbundenen aktiven Datenmenge.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>    </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>    </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>   </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_RecordCount</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_RecordCount(Query: Integer): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Beschreibung:
Liefert die Anzahl der Datensätze innerhalb der mit Query verbundenen aktiven Datenmenge zurück.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_IsEmpty</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_IsEmpty(Query: Integer): Boolean;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert TRUE zurück, falls die mit Query verbundene aktive Datenmenge leer ist.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_IsActive</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_IsActive(Query: Integer): Boolean;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert TRUE zurück, falls die mit Query verbundene Datenmenge aktiv bzw. geöffnet ist.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetFieldCount</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetFieldCount(Query: Integer): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert die Anzahl der Felder der mit Query verbundenen aktiven Datenmenge zurück.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetFieldName</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetFieldName(Query: Integer; Index: Integer): String;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert den Feldnamen des mit Index indizierten Feldes der mit Query verbundenen aktiven Daten-menge zurück.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetFieldValue</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetFieldValue(Query: Integer; Name: String): Variant;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert den Feldwert des mit Name bezeichneten Feldes als Variante zurück. Der Feldwert hängt natürlich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetFieldAsText</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetFieldAsText(Query: Integer; Name: String): String;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert den Feldwert des mit Name bezeichneten Feldes als String zurück. Der Feldwert hängt natür-lich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab. Sollte der Feldwert nicht in einen String umgewandelt werden können, dann wird ein Leerstring zurückgeliefert.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetFieldAsInt</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetFieldAsInt(Query: Integer; Name: String; Default: Integer): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert den Feldwert des mit Name bezeichneten Feldes als Integer zurück. Der Feldwert hängt natür-lich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab. Sollte der Feldwert nicht in einen Integer-Wert umgewandelt werden können, dann wird Default zurückgeliefert.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetFieldAsFloat</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetFieldAsFloat(Query: Integer; Name: String; Default: Float): Float;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert den Feldwert des mit Name bezeichneten Feldes als Float zurück. Der Feldwert hängt natürlich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab. Sollte der Feldwert nicht in einen Float-Wert umgewandelt werden können, dann wird Default zurückgeliefert.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetFieldAsBool</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetFieldAsBool(Query: Integer; Name: String; Default: Boolean): Boolean;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Beschreibung:
Liefert den Feldwert des mit Name bezeichneten Feldes als Boolean zurück. Der Feldwert hängt natürlich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab. Sollte der Feldwert nicht in einen Boolean-Wert umgewandelt werden können, dann wird Default zurückgeliefert.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetFieldAsDate</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetFieldAsDate(Query: Integer; Name: String): DateTime;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert den Feldwert des mit Name bezeichneten Feldes als Datumsangabe zurück. Der Feldwert hängt natürlich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab. Sollte der Feldwert nicht in eine Datumsangabe umgewandelt werden können, dann wird 0 zurückgeliefert.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetFieldAsTime</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetFieldAsTime(Query: Integer; Name: String): DateTime;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert den Feldwert des mit Name bezeichneten Feldes als Zeitangabe zurück. Der Feldwert hängt natürlich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab. Sollte der Feldwert nicht in eine Zeitangabe umgewandelt werden können, dann wird 0 zurückgeliefert.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_BindParam</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_BindParam(Command: Integer; Param: String; Value: Variant);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Setzt den mit Param gekennzeichneten Parameter auf den Wert Value.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_BindParamToNull</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_BindParamToNull(Command: Integer; Param: String);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Setzt den mit Param gekennzeichneten Parameter auf den Status NULL.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetErrorCount</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetErrorCount: Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert die Anzahl der Fehler zurück, die seit dem letzten Löschen des Fehlerbuffers aufgelaufen sind.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetErrorMessage</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetErrorMessage(Index: Integer): String;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert den Text der mit Index indizierten Fehlermeldung zurück.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetErrorState</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetErrorState(Index: Integer): String;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert den Fehlerstatus der mit Index indizierten Fehlermeldung zurück.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_ClearErrors</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure odbc_ClearErrors;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Löscht den internen Fehlerpuffer.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>odbc_GetErrorTotalCount</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function odbc_GetErrorTotalCount: Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert die Anzahl aller jemals aufgetretenen Fehler zurück.</td>
    </td>
  </tr>
 </tbody>
</table>

##IB-Bibliothek{#IB-Bibliothek}

Die IB-Bibliothek stellt Funktionen für den direkten Zugriff auf die aktuelle Magellan-Datenbank zur Verfügung. Dies sind vor allem Funktionen zum Ausführen von SQL-Anweisungen (z.B. DELETE, UPDATE, INSERT oder SELECT).

Alle Funktionen besitzen den Präfix ib_.

Zu beachten ist, dass die SQL-Anweisungen im SQL3-Dialekt verlangt werden. Praktisch bedeutet dies, dass alle Feld- und Tabellennamen in Anführungszeichen und unter Beachtung der Groß- und Klein-schreibung angegeben werden müssen.

<table class="table">
<caption></caption>
<thead>
<tr>
<th colspan=2 >IB-Bibliothek</th>
    </tr>
 </thead>
<tbody>
<tr>
    <th>Funktion</th>
        <th align=left>ib_Commit</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure ib_Commit;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Führt ein Commit durch und startet anschließend eine neue Transaktion.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_Rollback</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure ib_Rollback;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Führt ein Rollback durch und startet anschließend eine neue Transaktion.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_CreateCommand</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function ib_CreateCommand(SQL: String): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Erstellt einen SQL-Befehl, führt ihn aber noch nicht aus. Die Funktion liefert bei Erfolg ein Handle auf den erstellten Befehl zurück, andern- falls 0.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_DestroyCommand</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure ib_DestroyCommand(Command: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Gibt einen mit ib_CreateCommand erstellten SQL-Befehl wieder frei.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_Execute</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure ib_Execute(Command: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Beschreibung:
Führt einen mit ib_CreateCommand erstellten SQL-Befehl aus. Dabei darf es sich nur um SQL-Befehle handeln, die als Ergebnis keine Datenmenge liefern (z.B. INSERT, UPDATE, DELETE).</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_RowsAffected</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function ib_RowsAffected(Command: Integer): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Beschreibung:
Liefert die Anzahl der Datensätze zurück, die durch ein INSERT, UP- DATE oder DELETE betroffen waren. Diese Funktion macht nur in Verbindung mit einem vorher ausgeführten ib_Execute Sinn.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_Open</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure ib_Open(Command: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Öffnet eine mit ib_CreateCommand erstellte SQL-Abfrage.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_EOF</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function ib_EOF(Query: Integer): Boolean;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert TRUE zurück, falls der Datensatzeiger der mit Query verbundenen Abfrage am Ende der aktiven Datenmenge steht.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_BOF</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function ib_BOF(Query: Integer): Boolean;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert TRUE zurück, falls der Datensatzeiger der mit Query verbundenen Abfrage am Anfang der aktiven Datenmenge steht.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_First</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure ib_First(Query: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Springt zum ersten Datensatz der mit Query verbundenen aktiven Datenmenge.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_Last</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure ib_Next(Query: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Springt zum nächsten Datensatz der mit Query verbundenen aktiven Datenmenge.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_Prior</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>procedure ib_Prior(Query: Integer);</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Springt zum vorherigen Datensatz der mit Query verbundenen aktiven Datenmenge.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_RecordCount</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function ib_RecordCount(Query: Integer): Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert die Anzahl der Datensätze innerhalb der mit Query verbundenen aktiven Datenmenge zurück.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_IsEmpty</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function ib_IsEmpty(Query: Integer): Boolean;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Beschreibung:
Liefert TRUE zurück, falls die mit Query verbundene aktive Datenmenge leer ist.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_IsActive</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function ib_IsActive(Query: Integer): Boolean;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Liefert TRUE zurück, falls die mit Query verbundenen Datenmenge aktiv bzw. geöffnet ist.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>
ib_GetFieldCount</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td> function ib_GetFieldCount(Query: Integer): Integer;   </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>   Liefert die Anzahl der Felder der mit Query verbundenen aktiven Datenmenge zurück.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>   ib_GetFieldName </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  function ib_GetFieldName(Query: Integer; Index: Integer): String;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Liefert den Feldnamen des mit Index indizierten Feldes der mit Query verbundenen aktiven Datenmenge zurück. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> ib_GetFieldValue   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>    function ib_GetFieldValue(Query: Integer; Name: String): Variant;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>   Liefert den Feldwert des mit Name bezeichneten Feldes als Variante zurück. Der Feldwert hängt natürlich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> ib_GetFieldAsText   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>   function ib_GetFieldAsText(Query: Integer; Name: String): String; </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Liefert den Feldwert des mit Name bezeichneten Feldes als String zurück. Der Feldwert hängt natürlich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab. Sollte der Feldwert nicht in einen String umgewandelt werden können, dann wird ein Leerstring zurückgeliefert. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_GetFieldAsInt</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>function ib_GetFieldAsInt(Query: Integer; Name: String; Default: Integer): 
Integer;</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Liefert den Feldwert des mit Name bezeichneten Feldes als Integer zurück. Der Feldwert hängt natürlich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab. Sollte der Feldwert nicht in einen Integer-Wert umgewandelt werden können, dann wird Default zurückgeliefert.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  ib_GetFieldAsFloat  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  function ib_GetFieldAsFloat(Query: Integer; Name: String; Default: Float): Float;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Beschreibung:
Liefert den Feldwert des mit Name bezeichneten Feldes als Float zurück. Der Feldwert hängt natürlich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab. Sollte der Feldwert nicht in einen Float-Wert umgewandelt werden können, dann wird Default zurückgeliefert. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> ib_GetFieldAsBool   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  function ib_GetFieldAsBool(Query: Integer; Name: String; Default: Boolean): Boolean;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Liefert den Feldwert des mit Name bezeichneten Feldes als Boolean zurück. Der Feldwert hängt natürlich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab. Sollte der Feldwert nicht in einen Boolean-Wert umgewandelt werden können, dann wird Default zurückgeliefert.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>   ib_GetFieldAsDate </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td> function ib_GetFieldAsDate(Query: Integer; Name: String): DateTime;   </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Liefert den Feldwert des mit Name bezeichneten Feldes als Datumsangabe zurück. Der Feldwert hängt natürlich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab. Sollte der Feldwert nicht in eine Datumsangabe umgewandelt werden können, dann wird 0 zurückgeliefert.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_GetFieldAsTime    </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  function ib_GetFieldAsTime(Query: Integer; Name: String): DateTime;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Liefert den Feldwert des mit Name bezeichneten Feldes als Zeitangabe zurück. Der Feldwert hängt natürlich von der Position des Datensatzzeigers innerhalb der aktiven Datenmenge ab. Sollte der Feldwert nicht in eine Zeitangabe umgewandelt werden können, dann wird 0 zurückgeliefert. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  ib_BindParam  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>   function ib_BindParam(Command: Integer; Param: String; Value: Variant); </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Setzt den mit Param gekennzeichneten Parameter auf den Wert Value.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_BindParamToNull    </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  function ib_BindParamToNull(Command: Integer; Param: String); </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Beschreibung:
Setzt den mit Param gekennzeichneten Parameter auf den Status NULL. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_GetErrorCount    </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  function ib_GetErrorCount: Integer;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Liefert die Anzahl der Fehler zurück, die seit dem letzten Löschen des Fehlerbuffers aufgelaufen sind.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>ib_GetErrorMessage</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  function ib_GetErrorMessage(Index: Integer): String;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Liefert den Text der mit Index indizierten Fehlermeldung zurück.  </td>
    </td>
  </tr>
<tr>
    <th>Funktion</th>
        <th align=left>  ib_GetErrorCode  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  function ib_GetErrorCode(Index: Integer): String;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Liefert den Fehlercode der mit Index indizierten Fehlermeldung zurück.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>   ib_ClearErrors </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  procedure ib_ClearErrors;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Löscht den internen Fehlerpuffer.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  ib_GetErrorTotalCount  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  function ib_GetErrorTotalCount: Integer;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Liefert die Anzahl aller jemals aufgetretenen Fehler zurück. </td>
    </td>
  </tr>
</tbody>
</table>

##SDTF-Bibliothek{#SDTF-Bibliothek}

Die SDTF-Bibliothek stellt Funktionen für den Zugriff auf das textbasierte Schuldatentransferformat zur Verfügung. 

Jede Textzeile stellt einen Datensatz dar, der wie folgt aufgebaut ist:

`<LineType>;<Field_1>;<Field_2>;...;<Field_n>`

Wichtig in diesem Zusammenhang ist, dass Felder, die ein Leerzeichen oder ein Semikolon enthalten, in Anführungszeichen (") geschrieben werden. Die Routinen dieser Bibliothek berücksichtigen dies automatisch, so dass ein Skript-Programmierer sich darum nicht kümmern braucht.


<table class="table">
<caption></caption>
<thead>
<tr>
<th colspan=2 >SDTF-Bibliothek</th>
    </tr>
 </thead>
<tbody>
<tr>
    <th>Funktion</th>
        <th align=left>sdtf_LoadFromFile</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  sdtf_LoadFromFile(FileName: String): Integer;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Lädt den gesamten Inhalt der Datei zur weiteren Bearbeitung in einen Buffer. Das Handle zum Buffer wird als Funktionsergebnis zurückgeliefert.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  sdtf_SaveToFile  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td> sdtf_SaveToFile(FileName: String; Buffer: Integer)</td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Schreibt den Inhalt eines Buffers in eine Datei. Existiert die Datei bereits, so wird sie überschrieben.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> sdtf_CreateBuffer   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td> sdtf_CreateBuffer: Integer; </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Erzeugt einen neuen und leeren Buffer zur weiteren Bearbeitung. Das Handle zum Buffer wird als Funktionsergebnis zurückgeliefert. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> sdtf_DestroyBuffer   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td> sdtf_DestroyBuffer(Buffer: Integer);   </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Erzeugt einen neuen und leeren Buffer zur weiteren Bearbeitung. Das Handle zum Buffer wird als Funktionsergebnis zurückgeliefert.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> sdtf_GetBufferLineCount   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td> sdtf_GetBufferLineCount(Buffer: Integer): Integer;   </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Beschreibung:
Liefert die Anzahl der Textzeilen im Buffer zurück.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> sdtf_GetBufferLine   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td> sdtf_GetBufferLine(Buffer: Integer; Index: Integer): String;   </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Liefert die Textzeile an der Position Index im Buffer zurück. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> sdtf_AddBufferLine   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  sdtf_AddBufferLine(Buffer: Integer; Line: String);  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Fügt eine neue Textzeile an den Buffer an. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  sdtf_DeleteBufferLine  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td> sdtf_DeleteBufferLine(Buffer: Integer; Index: Integer);   </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Löscht eine Textzeile an der Posiiton Index im Buffer. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>sdtf_GetFieldCount    </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>   sdtf_GetFieldCount(Line: String): Integer; </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Liefert die Anzahl der Felder (bzw. Werte) in der übergebenen Textzeile zurück. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> sdtf_GetFieldValue   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  sdtf_GetFieldValue(Line: String; Index: Integer): String;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>   Liefert den Wert an der Position Index in der übergebenen Textzeile zurück.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  sdtf_GetFieldValueAsText  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  sdtf_GetFieldValueAsText(Line: String; Index: Integer): Variant;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Liefert den Wert an der Position Index in der übergebenen Textzeile zurück.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  sdtf_GetFieldValueAsInteger  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  sdtf_GetFieldValueAsInteger(Line: String; Index: Integer): Variant;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Liefert den Wert an der Position Index in der übergebenen Textzeile zurück. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> sdtf_AddFieldValue   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  sdtf_AddFieldValue(Line: String; Value: Variant): String;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Fügt einen neuen Wert an das Ende der übergebenen Textzeile an.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> sdtf_IsError   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td> sdtf_IsError: Boolean;   </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Gibt TRUE zurück, falls ein oder mehrere Fehler beim Dateizugriff aufgetreten sind.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> sdtf_GetErrorCount   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  sdtf_GetErrorCount: Integer;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>   Liefert die Anzahl der Fehler zurück, falls ein oder mehrere Fehler beim Dateizugriff aufgetreten sind.</td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> sdtf_GetErrorMessage   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  sdtf_GetErrorMessage(Index: Integer): String;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Liefert die Fehlermeldungen zurück, falls ein oder mehrere Fehler beim Dateizugriff aufgetreten sind.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  sdtf_ClearErrors  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>   sdtf_ClearErrors;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Löscht alle angelaufenen Fehlermeldungen. </td>
    </td>
  </tr>
</tbody>
</table>

##	BOX-Bibliothek{#BOX-Bibliothek}

Diese Skript-Bibliothek stellt ein Ausgabefenster zur Verfügung, mit dessen Hilfe der aktuelle Status der Skriptbearbeitung visualisiert werden kann. Zudem bekommt der Benutzer die Möglichkeit, das Skript vorzeitig abzubrechen.


<table class="table">
<caption></caption>
<thead>
<tr>
<th colspan=2 >Titel</th>
    </tr>
 </thead>
<tbody>
<tr>
    <th>Funktion</th>
        <th align=left>obox_Create</th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  procedure obox_Create(Caption: String; Size: Integer);  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Initialisiert das Ausgabefenster, zeigt es aber noch nicht an. Mit „Caption“ kann die Überschrift des Fensters festgelegt werden. Mit „Size“ die Größe des Laufbalkens. Bei Size = 0 wird kein Laufbalken angezeigt. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  obox_Destroy  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  procedure obox_Destroy;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Gibt die mit dem Ausgabefenster verbundenen Ressourcen wieder frei.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> obox_Show   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>   procedure obox_Show; </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Zeigt das Ausgabefenster an. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>   obox_Hide </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  procedure obox_Hide;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Versteckt das Ausgabefenster.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  obox_Ready  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  procedure obox_Ready;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Zeigt an, dass der Vorgang beendet ist. Der Benutzer kann nur noch mit OK bestätigen.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>obox_KeepAlive    </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>   procedure obox_KeepAlive; </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Normalerweise muss diese Routine nicht aufgerufen werden. Sollte jedoch für längere Zeit keine neue Ausgabe im Fenster erscheinen, so kann das Multitasking-Verhalten darunter leiden. In diesen Fällen sollte man diese Routine häufiger aufrufen. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left> obox_StepIt   </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>   procedure obox_StepIt; </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Beschreibung:
Setzt den Fortschrittsbalken eins weiter.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>   obox_AddMsg </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  procedure obox_AddMsg(Value: String);  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Gibt eine neue Meldung in Form einer neuen Zeile aus.  </td>
    </td>
  </tr>
   <tr>
    <th>Funktion</th>
        <th align=left>obox_ExpandMsg    </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  procedure obox_ExpandMsg(Value: String);  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Fügt neuen Text an die aktuelle Meldung dran. Die aktuelle Meldung kann also erweitert werden. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  obox_ReplaceMsg  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td> procedure obox_ReplaceMsg(Value: String);   </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Ersetzt die aktuelle Meldung komplett durch eine neue Meldung. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>obox_IsAborted    </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>  function obox_IsAborted: Boolean;  </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td>  Liefert TRUE zurück, falls der Benutzer auf "Abbrechen" gedrückt hat. </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  obox_MsgCount  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>   function obox_MsgCount: Integer; </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Liefert die Anzahl der Meldungen zurück, die im Ausgabefenster angezeigt werden.  </td>
    </td>
  </tr>
</tbody>
</table>



##Weitere Dienstfunktionen{#Weitere Dienstfunktionen}

Neben den eben beschriebenen Bibliotheken gibt es noch eine Reihe von Dienstfunktionen, die einem das Leben sehr erleichtern können.

<table class="table">
<caption></caption>
<thead>
<tr>
<th colspan=2 >Titel</th>
    </tr>
 </thead>
<tbody>
<tr>
    <th>Funktion</th>
        <th align=left>VarIsNull    </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>   function VarIsNull(Value: Variant): Boolean; </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Diese Funktion liefert TRUE zurück, falls Value den Status NULL besitzt, ansonsten FALSE.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  MatchStr  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td> function MatchStr(InputStr, Wilds: String; IgnoreCase: Boolean): Boolean;   </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> MatchStr vergleicht InputStr mit Wilds. Der Parameter Wilds kann dabei die Wildcards "?" und "*" enthalten. Past Wilds zu InputStr, so liefert die Funktion TRUE zurück.  </td>
    </td>
  </tr>
  <tr>
    <th>Funktion</th>
        <th align=left>  ConcatStr  </th>
    </tr>
  <tr>
    <td>Syntax</td>
    <td>   function ConcatStr(S1, S2, Link: String): String; </td>
    </tr>
  <tr>
    <td>Beschreibung</td>
    <td> Verbindet die beiden Strings S1 und S2 miteinander. Ist weder S1 nochS2 leer, dann wird der Ver-bindungsstring Link dazwischengesetzt.  </td>
    </td>
  </tr>
</tbody>
</table>
