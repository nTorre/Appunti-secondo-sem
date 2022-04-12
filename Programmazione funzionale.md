## Programmazione funzionale

### To do:
- Installare polyML.

#### Link utili:
- [Magica pagina github](https://github.com/Pater999/UNITN-linguaggi-programmazione-SML)
- [Pagina corso]()

### 1 Linguaggi

- #### Fortran
    - FORmula TRANslation language
    - Array di dimensione fissa
    - Procedurale, no ricorsione (entrambe facilitano la gestione di dati)
    - Le procedure possono essere compilate indipendentemente
    - Formattazione di I/O
    - Programmi solitamente run in batch mode
    - Input: Stack of punched cards
- #### Algol
    - Struttura a blocchi, conscope per variabili locali
    - Tipicizzato
    - Varibili statiche e dinamiche
    - If-then-else
    - Chiamata per noem e per valore
    - Ricorsione
    - Array dinamici
    - Non pensato per un uso partcolare
    - Tre versioni principali: 1958, 1960, 1968
    - Influenzato da linguaggi imperativi
- #### Cobol
- #### PL/I
- #### Simula 67
- #### LISP
- #### APL
- #### Smaltalk
- #### Pascal
- #### ADA
    - In the ALGO tradition
- #### C
- #### C++
- #### Logic Programming (Prolog)
- #### Java
    - OO, portable
    - Compilato in *Bytecode*, che viene eseguito su qualsiasi Java Virtial Machine (JVM)
    - Inizialmente per embedded system, molto utilizzato in Internet.
- #### Scripting languages
    - JCL, MS-DOS
    - Unix: csh, sed, awk
    - Seguito da: perl, python, etc.
    - Colmipati e interpretati
    - Economy of expression
    - No dichiarazioni, semplici regole di scope.

### ML
###### Utilizzare ML
Scivere poly sul terminale. Se *file* fosse il nome di un file, utilizzare il comando:
```
poly < file
```
oppure, una volta avviato polyML

```
> use "file"
```

##### Variabili
I tipi base forniti da ML sono: **unit, bool, int, real, char** e **string**.

Il tipo **unit** è composto da un unico valore () e viene utilizzato come tipo di ritorno per espressioni che non ritornano alcun valore (e che sono importanti solo per i propri effetti collaterali).

Il tipo **bool**, invece, è composto da due valori (*true* e *false*).

Il tipo **int** è composto (come il nome suggerisce) dai numeri interi, positivi e negativi. Su tali numeri
è definito l’operatore **~**, che nega il segno di un numero; quindi, per esempio, ~3 rappresenta il numero -3.

Altri operatori definiti sul tipo int sono le operazioni aritmetiche di base *, + e -. L’operatore / di
divisione non è definito sugli interi (mentre esiste la divisione intera **div**). Inoltre esiste l'operatore **mod** per fare il modulo: *3 mod 2*

*Da notare la differenza tra* ***-*** *e* ***~.*** *La prima si riferisce all'operazione, mentre la seconda al segno*

Il tipo **real** è composto da un insieme di approssimazioni di numeri reali, che possono essere espressi tramite parte intera e parte frazionaria (per esempio, 3.14) o usando la forma esponenziale (per esempio, 314e~2). Ancora, il simbolo ~ può essere usato per negare un numero (invertirne il segno). Due valori speciali **NaN** (Not a Number) e **inf** possono essere usati per indicare valori non rappresentabili come numeri reali (per esempio, la radice quadrata di un numero negativo) o valori infiniti (il risultato della divisione di un numero reale per 0). E infine da notare che i valori di tipo real sono confrontabili con gli operatori **<**, **>**, **<=** e **>=** (che vengono valutati a valori di tipo bool), ma non si può usare il testi di uguaglianza su di essi.

Il tipo **char** è composto dall’insieme dei caratteri. Un valore di tale tipo viene rappresentato con il prefisso # e fra virgolette; per esempio, *#"a"*.

Il tipo **string** è composto dall’insieme delle stringhe, rappresentate fra virgolette; per esempio "test". Sulle stringhe, ML definisce l’operatore di concatenazione **^** (*non funziona per char*):<br>
*"Ciao, " ^ "mondo" = "Ciao, Mondo".*

###### Inizializzazione
Le espressioni che compongono un programma ML possono fare riferimento a valori o ad identificatori definiti in un *ambiente*, (un insieme di coppie (identificatore, valore)). L’ambiente può essere modificato (in realtà, esteso) associando un valore (di qualsiasi tipo) ad un nome (identificatore) tramite la keyword **val**:
```ML
val <name> = <value >;
val <name>:<type> = <value >;
```


######Conversioni
ML non esegue conversioni automaticamente.<br>
Per convertire un *char* in un *int* si utilizza **ord**. <br>
Viceversa, da *int* a *char* **chr**

#### If, then e else
La sintassi è:
```ML
if <p> then <exp1> else <exp2>;
```

#### Liste
Dichiarazione:
```ML
val L = [2,4,5];
```

Concatenazione (simbolo **@**):
```ML
[1,2] @ [3,4];
```
*Nota: Le liste devono essere dello stesso tipo. Concatenare liste di caratteri con liste di interi dà errore.*

*Nota: esiste l'operatore ::, serve per unire elementi in una lista, ma dev'essere seguito dall'espressione nil*
```ML
1::3::nil;
```
L'espressione realmente è:
```ML
[[1,2],nil,[3]];
//output
val it = [[1, 2], [], [3]]: int list list
```
*// non è un commento, ma lo considero tale in questo pdf*

L'espressione **nil** serve per terminare una lista.<br>
non ho ancora capito perchè in alcuni casi serve e in altri no (e anzi segnala errore), come il seguente:
```ML
"r"::["e","s"];
```
Sicuramente non è legato al fatto che sono caratteri, perchè nella basica situazione ```"r"::"s";``` non è necessario.

######Explode/Implode:
Viene utilizzato per scomporre una stringa in una lista di char.
```ML
explode("Ciao");
(*output*)
val it = [#"C", #"i", #"a", #"o"]: char list
```

```ML
implode(explode("Ciao"));
(*output*)
val it = "Ciao": string
```

##### "Liste miste"
Per creare liste di tipi diversi si utilizzano le parentesi tonde **()** invece di quelle quadrate:
```ML
(1,"2",true);
(*output*)
val it = (1, "2", true): int * string * bool
```

#### Funzioni
Dichiarazione:
```ML
fun upper(c) = chr(ord(c)-32);
(*output*)
val upper = fn: char -> char
```

*Nota: fun per dichiarare, fn indica il tipo, fn: tipo_input -> tipo_output*

Chiamata della funzione:
```ML
upper #"a";
(*output*)
val it = #"A": char
```

Per creare una funzione che abbia *real* come default:
```ML
fun square (x:real) = x*x;
(*output*)
val square = fn: real -> real
```

Funzione più complessa:
```ML
fun max(a:real,b,c) = (*maximum of reals*)
# if a > b then if a > c then a else c else if b < c then c else b;
(*output*)
val max = fn: real * real * real -> real
```

#### Altro modo per scrivere le funzioni
La funzione somma:
```ML
fun somma(a,b) = a+b;
```
può essere riscritta come:
```ML
val somma = fn (a,b) => a+b;
```


###### Esercizio
[$a_1$, $a_2$, $a_n$,] $\rightarrow$ [$a_2$, $a_n$, $a_1$]

```ML
> fun cycle l = tl(l) @ [hd(l)];
(*output*)
val cycle = fn: 'a list -> 'a list
> cycle[1,2,3];
(*output*
val it = [2, 3, 1]: int list
```
*Nota: ```hd``` prende il primo valore della lista, mentre ```tl``` restituisce la lista senza il primo elemento*

##### Restituire più di un valore (e chiamata di funzione in funzione)
Dopo aver dichiarato le funzioni max3 e min3 che restituiscono rispettivamente il minimo e il massimo fra 3 valori, scriviamo la seuente funzione:
```ML
fun maxmin3(a,b,c) = (min3(a,b,c), max3(a,b,c));
```

###### Altre funzioni (esempi esercizi)
Rimuovere il secondo elemento di una lista (qualsiasi dimensione):
```ML
fun rwm l = hd(l)::tl (tl (l));
```

Caso particolare:
```ML
> val a = 3;
val a = 3: int
> fun f(b) = a*b;
val f = fn: int -> int
> f(9);
val it = 27: int
> val a = 2;
val a = 2: int
> f(4);
val it = 12: int
```

Invertire una lista ricorsivamente:
```ML
> fun reverse L =
# if L = nil then nil
# else reverse (tl L) @ [hd (L)];
val reverse = fn: ''a list -> ''a list
> reverse [1,2,3,4];
val it = [4, 3, 2, 1]: int list
```

###### Funzione getindex (fatta da me)
```ML
fun find(list, i) =
if i = 0 then hd(list) else find(tl(list), i-1);
```

#### Funzione in funzione ma non acora dichiarata
```ML
> fun take(L) = if L = nil then nil else hd(L)::skip(tl(L))
# and
# skip (L) = if L = nil then nil else take(tl(L));
(*Output: *)
val skip = fn: ''a list -> ''a list
val take = fn: ''a list -> ''a list
```

###### Lunghezza lista
```ML
fun length (L) = if L = nil then 0 else 1+length(tl(L));
```

###### Potenza
```ML
fun pow(x,i) = if i=0 then 1 else x*pow(x,i-1);
```

#### Funzioni
```ML
print("...") (*\n carattere escape*)
str(carattere) (*Da carattere a stringa*)
Real.toString(3.2)
Int.toString(3)
Bool.toString(true)
```

Es di stampa
```ML
> fun printList nil = ()
# | printList (x::xs) =
# (    
# print(Int.toString(x));
# print "\n";
# printList xs;
# );
```

```ML
val infile = TextIO.openIn("test");
val infile = ?: TextIO.instream;
TextIO.endOfStrem(infile);
TextIO.inputN(infile, 4); (*4 caratteri*)
TextIO.inputLine(infile)
TextIO.lookhead(infile);
```


SOME NONE, non so cosa siano.
