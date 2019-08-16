# Änderungen


## MAGELLAN 6.5.x

Mit der MAGELLAN-Version 6.5 wurde der Skriptingmechanismus auf eine neue Version aktualisiert.
Darüber hinaus haben wir Korrekturen vorgenommen, da unter bestimmten Umständen Skripte im Netzwerk nicht
korrekt ausgeführt wurden.

### Verbindungsaufruf bei ODBC_Skripten

Wenn Sie in Ihren Skripten die ODBC_ Aufrufe verwenden, dann müssen Sie die Anbindung an die MAGELLAN Datenbank wie folgt ändern. 

Der Aufruf `odbc_ConnectToFirebird` müsste wie folgt geändert werden:



```
con_Magellan := odbc_ConnectToFirebird(Server, Protocol, MagellanDatabase, MagellanUserName, MagellanPassword);

```


Tragen Sie dazu den Server als IP oder Hostname und das Protocol als Zahl ein, z.B. im Skripteditor in der .int Datei, passend zu den anderen Connect Variablen.


### Datentypen

Datentypen werden in der neuen Version strikter behandelt. Somit muss man sorgfältiger bei der Angabe der Datentypen für lokale Variablen sein, dass diese auch mit dem auszulesenden Datenbankfeld übereinstimmen.

Ein Beispiel dazu:


```

var Note: integer;
Note := odbc_GetFieldValue(SelectQuery, 'Note');
```



Es wird die lokale Variable Note als Ganze Zahl deklariert.
Ausgelesen aus der Datenbank wird aber mit GetFieldValue, was einen Variant Datentypen zurückliefert. Dieser kann allerdings auch NULL sein.
In dem Falle würde das Skript fehlerhaft abbrechen, wenn die Note in der Datenbank nicht eingetragen wäre, da eine Integer Variable den Wert NULL nicht führen kann.

Mögliche Lösungen, Sie deklarieren die lokale Variable als Variant:

ODBC_Skripte

```
  var Note: Variant;
  Note := odbc_GetFieldValue(SelectQuery, 'Note');
  
```

IB_Skripte

```
  var Note: Variant;
  Note := ib_GetFieldValue(SelectQuery, 'Note');
  
```



Oder Sie ändern die Datenbankabfrage der Note auf Integer:



```
  var Note: Integer;
  // -1 wäre hier in diesem Fall der Wert der rauskäme, wenn Note nicht gefüllt wäre.
  Note := odbc_GetFieldAsInt(SelectQuery, 'Note', -1);  
```


Entsprechend was erreicht werden soll, bzw. wie der Wert im Skript weiterhin genutzt wird, eignet sich eine der beiden Varianten.


#### DateTime

Der Skriptmechanismus kennt kein DateTime Datentyp. Lokale Variablen sollten vom Datentyp Float oder Variant deklariert werden.

Mögliche Lösungen, Sie deklarieren die lokale Variable als Variant:

ODBC_Skripte

```
var MeinDatum: Variant;
MeinDatum := odbc_GetFieldValue(SelectQuery, 'MeinDatumsfeld');
```

IB_Skripte

```
var MeinDatum: Variant;
MeinDatum := ib_GetFieldValue(SelectQuery, 'MeinDatumsfeld');
```


Oder Sie ändern die Datenbankabfrage des Datums auf Float:


ODBC_Skripte

```
var MeinDatum: Float;
// 0.0 wäre hier in diesem Fall der Wert der rauskäme, wenn MeinDatumsfeld nicht gefüllt wäre.
MeinDatum := odbc_GetFieldAsFloat(SelectQuery, 'MeinDatumsfeld', 0.0);
```

IB_Skripte

```
var MeinDatum: Float;
MeinDatum := ib_GetFieldAsFloat(SelectQuery, 'MeinDatumsfeld', 0.0);
```