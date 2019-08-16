# Skriptsprache{#Skriptsprache}

Die benutzte Skriptsprache „DelphiWebScript“ ist eine Variante der bekannten Programmiersprache „Object Pascal“. Wer also schon einmal mit der Entwicklungsumgebung Delphi gearbeitet hat, der wird sich gleich zu Hause füllen. Aber auch für Basic-Programmierer wird der Umstieg nicht schwer fallen.
Eine detaillierte Beschreibung aller Sprachkonstrukte würde den Rahmen dieser Dokumentation sprengen. Sollten Sie mit Pascal bzw. mit Delphi nicht vertraut sein, so sollten Sie sich ein entsprechen-des Buch aus dem Fachhandel besorgen. Aber auch im Internet werden Sie zu diesem Thema fündig.
Die beste Referenz stellen jedoch immer noch die mitgelieferten Skripte dar.
Im Folgenden geben wir die vollständige Beschreibung der Syntax wieder und gehen auf Besonderhei-ten der Skriptsprache ein.

## Die Syntax {#Die Syntax}

Die Syntax von DelphiWebScipt wird im folgenden Abschnitt in EBNF (Erweiterter Backus-Naur-Form) beschrieben. Wer mit dieser Beschreibungssprache nicht vertraut ist, kann unter diesem Stichwort weitere Erläuterungen z.B. in Fachbüchern oder über eine Internet-Recherche finden.

Es gelten folgende Beschreibungskonventionen:

Wert|Bedeutung
--|--
„[ ]“|Angaben in eckigen Klammern („[ ]“) sind optional.
„{ }“|Angaben in geschweiften Klammern („{ }“) können sich gar nicht, einmal oder mehrmals wiederholen.
Bezeichner in Großbuchstaben|Bezeichner in Großbuchstaben sind Symbole, d.h. Nicht-Terminal- Symbole.
Bezeichner in Anführungszeichen|Bezeichner in Anführungszeichen („Bezeichner“) sind Teil des Eingabetexts, d.h. Terminal-Symbole.
SCRIPT|Das Startsymbol ist SCRIPT.



```
SCRIPT =

[ ROOTSTATEMENT { ";" ROOTSTATEMENT } [ ";" ] ]


ROOTSTATEMENT =
TYPEDECL | PROCDECL | STATEMENT


STATEMENT =
VARDECL | CONSTDECL | BLOCK


VARDECL =
"var" NAME ":" TYPEDEF [ "=" EXPR ]


TYPEDECL =
"type" NAME "=" TYPEDEF


TYPEDEF =
„Boolean" | "Integer" | "Float" | "String" | „DateTime" | "Variant" | NAME | ARRAY-DEF | RECORDDEF | CLASSDEF

ARRAYDEF =
"array" "[" EXPR ".." EXPR {"," EXPR ".." EXPR} "]" "of" TYPEDEF


RECORDDEF =
"record" ARGLIST "end"


ARGLIST =
ARGDECL { ";" ARGDECL }


ARGDECL =
NAME ":" TYPEDEF


CLASSDEF =
"class" [ "(" NAME ")" ]
[ "private" | "public" | "protected" ] [ ARGLIST ";" ]
[ METHODDECL { ";" METHODDECL } ";" ]
[ "property" NAME ":" TYPEDEF [ "read" NAME ] [ "write" NAME ] ";" ]
"end"
 
METHODDECL =
[ "class" ] "procedure" NAME ["(" [ARGLIST] ")"]
[ ";" "override" | "virtual" | "reintroduce" ] | 
[ "class" ] "function" NAME ["(" [ARGLIST] ")"]
":" TYPEDEF [ ";" "override" | "virtual" | "reintroduce" ] |
"constructor" NAME ["(" [ARGLIST] ")"] [ ";" "override" |
"virtual" | "reintroduce" ] |
"destructor" NAME ["(" [ARGLIST] ")"] [ ";" "override" | virtual" | 
     "reintroduce" ]
     
PROCDECL =
PROCHEAD ";" PROCBODY | 
PROCHEAD ";" "forward" | 
METHODDEF ";" PROCBODY


PROCHEAD
"procedure" NAME ["(" [ARGLIST] ")"]
"function" NAME ["(" [ARGLIST] ")"] ":" TYPEDEF


PROCBODY =
{VARDECL ";"} "begin" SCRIPT "end"


METHODDEF =
[ "class" ] "procedure" NAME "." NAME ["(" [ARGLIST] ")"] |
[ "class" ] "function" NAME "." NAME ["(" [ARGLIST] ")"] ":" TYPEDEF |
"constructor" NAME "." NAME ["(" [ARGLIST] ")"] | 
"destructor" NAME "." NAME ["(" [ARGLIST] ")"]


CONSTDECL =
"const" "=" EXPR


BLOCK =
"begin" [STATEMENT {";" STATEMENT} [";"]] "end" | INSTR


INSTR =
"if" EXPR "then" BLOCK |
"if" EXPR "then" BLOCK "else" BLOCK | CASEINSTR |
"for" VAR ":=" EXPR "to" EXPR "do" BLOCK | 
"for" VAR ":=" EXPR "downto" EXPR "do" BLOCK | 
"while" EXPR "do" BLOCK |
"repeat" [BLOCK {";" BLOCK} [";"]] "until" EXPR | 
VAR ":=" EXPR |
FUNC | 
EXCEPT | 
FINALLY | 
BLOCK
 
 
CASECOND =
EXPR | EXPR ".." EXPR |


CASEINSTR =
"case" EXPR "of"
{ CASECOND {"," CASECOND } : BLOCK ";" } 
[ "default" ":" BLOCK ";" ]
"end"


FUNC =
NAME [ "(" [EXPR {, EXPR}] ")" ]


EXCEPT = 
"try"
BLOCK { ";" BLOCK } [ ";" ] 
"except"
{ "on" NAME ":" NAME "do" BLOCK; } 
"end"


FINALLY = 
"try"
BLOCK { ";" BLOCK } [ ";" ]
"finally"
{ "on" NAME ":" NAME "do" BLOCK; }
"end"


EXPR =
EXPRADD [ "=" | "+" | "-" | "OR" EXPRADD]


EXPRADD =
EXPRMUL [ "+" | "-" | "OR" EXPRADD]


EXPRMUL =
TERM [ "*" | "/" | "mod" | "div" EXPRMUL]


TERM =
"+" TERM | 
"-" TERM | 
"not" TERM |
CONST | VAR | FUNC | "(" EXPR ")"


CONST =
INT |HEXINT |FLOAT | 
STR |CHAR |
"True" | "False"


VAR =
NAME |
NAME "[" INT "]" | 
NAME "." VAR |
VAR "." FUNC


NAME =
LIT {LIT | "0".."9" | "_"}
 
 
LIT =
"A".."Z", "a".."z"


STR =
	CHAR | STRING { CHAR [ STRING ] }
 
 
STRING =
" ' " { STRINGCHAR } " ' " { " ' " STRING }


STRINGCHAR =
ASCII(0)..ASCII(255) - " ' " - ASCII(13) | " ' ' "


CHAR =
"#" INT | "#" HEXINT


HEXINT =
"$" HEXNUM { HEXNUM }


HEXNUM =
"0".."9" | "A".."F" | "a".."f"


FLOAT =
INT [ "." INT] [ "E" | "e" ["+" | "-"] INT ]
 
 
INT =
NUM {NUM}


NUM =
"0".."9"
```

## Reservierte Worte {#Reservierte Worte}

Die folgenden Worte sind reserviert und können nicht beliebig im Skript verwendet werden. So dürfen Sie beispielsweise keine Variable deklarieren, die BEGIN heißt.


<table class="table">
<caption></caption>
<thead>
<tr>
<th colspan= 5 >Reservierte Worte</th>
</tr>
</thead>
<tbody>
<tr>
 <th>A</th>
    <td>and</td>
     <td>array</td>
     <td>as</td>
     <td>  </td>
     <td>  </td>
</tr>
<tr>
  <th> B</th>
     <td>begin</td>
     <td> </td>
     <td> </td>
     <td> </td>
     <td>  </td>
</tr>
<tr>
    <th> C</th>
     <td>case</td>
     <td>class</td>
      <td>const</td>
      <td>const</td>
      <td>constructor</td>
</tr>
<tr>
    <th> D</th>
     <td>destructor</td>
     <td>div </td>
     <td>do </td>
     <td> downto</td>
     <td> </td>
</tr> 
<tr>
    <th> E</th>
     <td>else</td>
     <td>end</td>
     <td>except </td>
     <td> </td>
     <td> </td>
</tr>    
<tr>
    <th> F</th>
     <td>finally </td>
     <td> for</td>
     <td> forward</td>
     <td> function</td>
     <td> </td>
</tr> 
<tr>
    <th> I</th>
     <td>if </td>
     <td> inherited</td>
     <td> is</td>
     <td> </td>
     <td> </td>
</tr> 
<tr>
    <th> L</th>
     <td>label </td>
     <td> </td>
     <td> </td>
     <td> </td>
     <td> </td>
</tr> 
<tr>
    <th> M</th>
     <td>mod </td>
     <td> </td>
     <td> </td>
     <td> </td>
     <td> </td>
</tr> 
<tr>
    <th> N</th>
     <td> nil</td>
     <td> not</td>
     <td> </td>
     <td> </td>
     <td> </td>
</tr> 
<tr>
    <th> O</th>
     <td>of </td>
     <td> or</td>
     <td> </td>
     <td> </td>
     <td> </td>
</tr> 
<tr>
    <th> P</th>
     <td>procedure </td>
     <td> property</td>
     <td> </td>
     <td> </td>
     <td> </td>
</tr> 
<tr>
    <th> R</th>
     <td> raise</td>
     <td> record</td>
     <td>repeat </td>
     <td> </td>
     <td> </td>
</tr> 
<tr>
    <th> S</th>
     <td>string </td>
     <td> </td>
     <td> </td>
     <td> </td>
     <td> </td>
</tr> 
<tr>
    <th> T</th>
     <td> then</td>
     <td>to </td>
     <td>try </td>
     <td> type</td>
     <td> </td>
</tr> 
<tr> 
    <th> U</th>
     <td> until</td>
     <td>  </td>
     <td>  </td>
     <td>  </td>
     <td> </td>
</tr> 
<tr> 
    <th> V</th>
     <td> var</td>
     <td>  </td>
     <td>  </td>
     <td>  </td>
     <td> </td>
</tr> 
<tr> 
    <th>W</th>
     <td>while</td>
     <td>  </td>
     <td>  </td>
     <td>  </td>
     <td> </td>
</tr> 
<tr> 
    <th>X</th>
     <td>xor</td>
     <td>  </td>
     <td>  </td>
     <td>  </td>
     <td> </td>
</tr> 
</tbody>
</table>

## Besonderheiten {#Besonderheiten}

Da DelphiWebScript an die Programmiersprache der Entwicklungsumgebung Delphi angelehnt ist, ist es das Beste, die Unterschiede zu Delphi zu erläutern.

###Struktur{#Struktur}

Die Syntax von DelphiWebScript unterscheidet sich in einigen Punkten von einem Delphi-Programm. Ein wesentlicher Unterschied ist die Tatsache, dass in DelphiWebScript nicht zwischen Deklarationsteil und Programmteil unterschieden wird.

Ein Delphi-Programm hat die folgende Struktur:

```
program ProgramName; 

Declarations

begin

Instructions 

end.
```

Ein DelphiWebScript hat keine Struktur. Man kann Deklarationen und Instruktionen überall im Skript platzieren. Daher beginnt jede Deklaration mit einem Schlüsselwort und endet mit einem Semikolon.
Beispiel:
```
var i: Integer = 2;
type TPoint = record x, y: Integer; end;
type TRect = record x, y, w, h: Integer end;

var r: TRect;
r.x := 3;

procedure Proc(x: Integer); begin end; 

Proc(x);
```

###Deklarationen{#Deklarationen}

Sie können innerhalb einer Prozedur-Deklaration keine Deklaration platzieren.

**Beispiel:**
```
// FALSCH
procedure Proc(x: Integer);
type
TMyRec = record a, b: string end;
begin end;
```

```
// RICHTIG
procedure Proc(x: Integer);
begin
type TMyRec = record a, b: string end;
end;
```

Dafür kann man Variablen auch innerhalb eines Blocks (BEGIN..END) deklarieren. Die Deklaration ist nur innerhalb dieses Blocks und inner- halb der entsprechenden Unterblöcke sichtbar.

**Beispiel:**
```
var i: Integer; 
if i = 0 then begin
var j: Integer;
j := 2;
while j > 0 do 
begin
var k: Integer;
k := 2;
j := j - k;
end;
end;

var j: String;
// Variable "j"´, die innerhalb des
// if-Blocks deklariert wurde, ist hier nicht sichtbar!
```

### Datentypen{#Datentypen}

DelphiWebScript unterstützt nur folgende elementare Datentypen:

Typ|Beschreibung
---|-----------
Integer| 32Bit-Integer
Float|64Bit-Fließkommawert
String| Textfeld beliebiger Länge
Boolean|Kann die Werte TRUE oder FALSE annehmen.
DateTime|Datum-Zeit-Angabe, ist kompatibel zu Float.
Variant|Umfasst alle anderen Typen. Sie können einer Variable des Typs Variant jeden anderen elementaren Typ zuweisen.


### Mengentypen{#Mengentypen}

DelphiWebScript unterstützt keine Mengentypen und keine Aufzählungstypen.
#####Case-Anweisung{#Case-Anweisung}
In DelphiWebSkript können Sie innerhalb einer CASE-Anweisung alle Datentypen verwenden: 

**Beispiel:**
```
var s: string;

s := 'Alpha';

case s of
'Alpha': DoSomething;
'Beta', 'Gamma': DoSomethingElse;
end;
```

#####Initialisierung{#Initialisierung}
Sie können eine Variable mit einer modifizierten VAR-Anweisung initialisieren:

**Beispiel:**
 ```
var s: Integer = 2;
var str: String = 'Hello' + IntToStr(s);
var i: Integer = 12;
 ```
 
Eine Initialisierung entspricht einer Deklaration gefolgt von einer Zuweisung. Sie ist lediglich eine Abkürzung dafür. Der Unterschied be-steht allerdings in der Ausführung der Anweisung: Die Initialisierung wird nur genau einmal vom Compiler durchlaufen. Die Anweisung wird zur Ausführungszeit des Programms ggf. mehrmals durchlaufen.

**Beispiel:**
 ```
var i: Integer = 12;
//…entspricht… 
var i: Integer; i := 12;
```
