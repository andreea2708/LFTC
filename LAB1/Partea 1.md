# Lab 1

## Enunt general:
Scrierea unui ANALIZOR LEXICAL pentru un minilimbaj de programare (MLP),
ales ca subset al unui limbaj existent

### Specificarea Minilimbajului de Programare (MLP):

**Tipuri de Date:**
1. Integer: Tip de date reprezentând numere întregi.
2. Float: Tip de date reprezentând numere reale
3. String: Tip de date reprezentând un sir de litere


**Instrucțiuni:**
1. Atribuire (Assignment): variabilă "primeste" expresie;
2. Intrare/Ieșire (Input/Output): scrie(expresie); / citeste(variabilă);
3. Selecție (Conditional):
```
daca (condiție): 
    // bloc de instrucțiuni
 altfel:
    // bloc de instrucțiuni
sfd
```
4. Ciclare (Loop):
```
repeta (condiție);
    // bloc de instrucțiuni
stop
```
**Restricții:**
Identificatori: Pot conține litere, cifre și underscore (_) și trebuie să înceapă cu o literă. Nu pot fi identici cu cuvintele cheie.


### Analizor Lexical:

1. Simboluri:
    - operators:
		* arithmetic: +, -, *, /, %
        * equality testing: ==, !=
        * order relations: <, <=, >, >=
		* sequencing: ","
    - separators { }  ; ( )
    - Cuvinte cheie: 
       * int      = int
       * float    = float
       * string   = string
       * scrie    = cout <<
       * citeste  = cin >>
       * daca     = if  (nu sunt sigur daca e operator sau cuvant cheie)
       * altfel   = else
       * repeta   = while
  
2. Identificatori
    - identifier = letter [{letter | digit | "_"}]*
    - letter = "A" | "B" | . ..| "Z" | "a" | "b" | ... | "z"
    - non_zero_digit = "1" |...| "9"
    - zero_digit = "0" 
    - sign = ["+" | "-"]
    - comma = ","

**Codification table:**
```
ATOM    : COD
ID      : 0
CONST   : 1
(       : 2
)       : 3
,       : 4
int     : 5
float   : 6
string  : 7
{       : 8
}       : 9
;       : 10
primeste      : 11
scrie      : 12
citeste : 13
+       : 14
-       : 15
*       : 16
/       : 17
%       : 18
repeta      : 19
!=      : 20
==      : 21
<       : 22
>       : 23
<=      : 22
>=      : 25
daca      : 26
start      : 27
"       : 28
main    : 29
```

**Mapa Semne Regex:**
```
. = orice
| = sau
? = one ore zero times
+ = one or any amount of times
* = zero or any amount of times
() = grup
{} = specifici de cate ori
```


```html
	<program> ::= “#include <iostream>
	      int main(){” <lista instr> “}”
	<lista instr> ::= <instr> <lista instr> | <instr> “;”
	<instr> ::= <io> | <atr> | <cond> | <rep> | <decl>
	<io> ::= “citeste” (ID) | “scrie” (ID)
	<atr>::=  ID “ primeste ” ID | ID “ primeste ” CONST | ID “primeste” <expr>
	<expr> ::= ID | CONST | ID <op> ID | ID <op> CONST | ID <op> <expr>
	<op_relational> ::= != | == | < | > | <= | >=
	<decl> ::=  <type> ID
	<type>::= “int” | “bool” | “float” | “char” | <cerc>
	<cerc> ::= “float” ID
	<instr_if> ::= “daca ” ( <conditie> ) “:” <lista instr> “sfd”
	<instr_while> ::= “repeta ” (<conditie>) “:” <list instr> “stop”
	<conditie> ::= <expr_aritmetica> <op_relational> <expr_aritmetica> | <expr_aritmetica>
	ID ::= ^[_a-zA-Z]([_a-zA-Z0-9]){0,249}$
	CONST ::= <const_int> | <const_float> | <const_string>
	<const_int> ::= ^[+-]?[0-9]+$
	<const_float> ::= ^[+-]?[0-9]+(\.[0-9]*)?$
	<const_string> ::= ^".*"$

```

### 2. se cer textele sursa a 3 mini-programe  

1. calculeaza perimetrul si aria cercului de o raza data data
```cpp
#include <iostream>
int main()
{
	C cerc;
	cerc.raza primeste 12;
	pi CONST primeste 3.14;
	scrie (cerc.raza*cerc.raza*pi);
	scrie (cerc.raza*2*pi);
}

```

2. determina cmmdc a 2 nr naturale
```cpp
#include <iostream>
int main()
{
	int N1 primeste 8;
	int N2 primeste 10;
	int R primeste 0;
	repeta (N2!=0):
	R primeste N1%N2;
	N1 primeste N2;
	N2 primeste R;
	stop;
	scrie (N1);
}

```

3. calculeaza suma a n numere citite de la tastatura 
```cpp
#include <iostream>
int main()
{
	int N;
	int S primeste 0;
	int V;
	citeste N;
	repeta (N>0):
		N--;
		citeste V;
		S+=V;
		stop;
	scrie (S);
}

```

### 3. Se cer textele sursa a doua programe care contin erori conform MLP-ului definit:

1. Unul dintre programe contine doua erori care sunt in acelasi timp erori in limbajul original (pentru care MLP defineste un subset)

```cpp
🏁

int main() {
    float a // eroare

    a = 15.4;

    in b; // eroare
    citire (b);

    cout << a + 2;
}
```

2. Al doilea program contine doua erori conform MLP, dar care nu sunt erori in limbajul original. Se cere ca acesta sa fie compilat si executat in limbajul original ales

```cpp
🏁

int main() {
    int a, b; // eroare - fiecare pe o alta linie in MLP

    cin >> a;
    cin >> b;

    cout << a + b;

    return 0; // eroare - return nedefinit
}
```



### Diferente MLP si C++

1. nu exista for
2. nu se pot declara vectori
