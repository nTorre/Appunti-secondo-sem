## Calcolatori

#### To do
- sistemare intro corso (testo, sito, esame etc.)
- completare conversione binaria

####[Sito corso](https://didatticaonline.unitn.it/dol/course/view.php?id=33305)

#### 1.0 Storia dei Calcolatori
- ##### 1.1 Eniac
Nel 1943 il Dipartimento della Difesa degli USA commisisiona una macchina per il calcolo delle traiettorie dei proiettili di artiglieria.<br>
Nel '46 entra in funzione, occpuava una stanza 30mx9m
- ##### 1.2 Apollo Guidance Computer
Sviluppato nel 1969 dalla IBM, fu il computer utilizzato per andare sulla luna.<br>
Non più valvore termoioniche, vengono utilizzati i circuiti integrati (trnsistor). Il funzionamento è lo stesso, ma diminuiscono le dimensioni. <br>
Uno dei primi sistemi display and keyboard. 152 KB di ROM e RAM

#### 2.0 Tipi di Calcolatori
I Calcolatori possono essere di diversi tipi:
- Calcolatori personali (Desktp e laptop)
- Server, pensati oer grandi carichi di lavoro oppure per siti web
- Embedded:
    - vasto uso (gaming, mobile, automobtive, etc.)
    - sono spesso dedicate e operano a dtretto contatto con l'hardware

#### 3.0  Sofwtare di sistema
Sistema Operativo (SO):
- gestisce le operazioni di I/O
- alloca la memoria
- consente il multitasking

Compilatore:
- traduce da linguaggio ad alto livello a linguaggio macchina

#### 4.0 Linguaggio macchina
Il componente base di un calcolatore sono le porte logiche, che corrispodono a *interruttori* elettrici.<br>
L'unità base dio informazioone è il bit: un interruttore vale 1 se acceso, 0 se spento.<br>
Anche un'istruzione dev'essere codificate come una stringa i di zeri e uni

#### 4.1 Programmazione Assembly
Programmare in sequenza di bit è estremamente difficle, motivo per cui è stato introdotto l'Assembly. <br>
```
add A,B -> 000100000001000100100101010...
```
Questo è il compito dell'assembler, mentre il compilatore traduce da linguaggio di alto livello a assembler. Alcuni compilatori possono saltare questo passaggio intermedio.
``` c++
int main(){
    int a = 5+4;
}
```
si trduce nella somma prima scritta.

#### 5.0 Il processore
E' la parte attiva di ogni calcolatore. Si compone di:
- Datapth: esegue le operazioni aritmetiche sui dati
- Parte di controllo: idica al datapath, alla memoria e ai componenti di I/O cosa fare sulla base di quanto stabilito nel programma.

Ogni core è costituito da questi componenti. I vari core sono collegati dal Northbridge e vi è una RAM aggiuntiva (cache). <br>
Questa complessità viene nascosta. C'è una sorta di **astrazione**. Il porcessore viene nascosto nei suoi dettagli e offre un'**ISA** (Instruction Set Architecture), un insieme di di istruzioni macchina. <br>
Inoltre si affianca dall'ISA un **ABI** (Application Binary Interface), l'interfaccia binaria delle applicazioni. Grazie a questi due strumenti lo sviluppatore software è svincolato dai dattagli HW.

#### 6.0 La memoria
Si distingue in volatile e non volatile (dischi rigidi e memorie a stato solido o SSD).
Quest'ultime sono importanti perchè mantengono lo stato dopo lo spegnimento e sono:
- Memorie Flash (es. SSD)
- Dischi rigidi
- CD/DVD

Le **memorie flash** utilizzano cariche elettriche. <br>
Gli **hard disk** magnetizzano particelle metalliche disposte su trutture sovrapposte (cilindri). Un braccetto legge e scrive le informazioni, rallentando i tempi di accesso, ma aumenta la densità di memorizzazrione (si arriva tranquillamente a TeraByte).
I **dischi ottici** sfruttano la riflessione della luce. Un laser viene rifelsso dai *rilievi* e *assorbito* dalle buche. Nei dischi riscrivibili uno substrato permette di ritornare allo stato iniziale (spianando le buche) tramite riscaldamento.

#### 7.0 Prestazioni
Le prestazioni sono:
- il **tempo medio di risposta**, tempo tra avvio e termine di un task;
- il **throughput**, ovvero quanti task vengono eseguiti nell'unità di tempo.

Il tempo di esecuzione in una macchina multitask dipende anche dagli altri task e dalle loro priorità.

Il **tempo di CPU Utente** insieme al **tempo CPU di Sistema** costituiscono il **Tempo di esecuzione della CPU**, che insieme al **Interferenza dovuta agli altri task**, costituisce il tempo di risposta.

I moderni processori, come vedremo, sono costruiti usando un segnale periodico che ne sincronizza le operazioni (clock). Il ciclo di clock è il tempo che trascorre tra due clock (secondi), la frequenza di Hertz.

La maniera migliore par valutare  prestazioni di un computer è misurare il temopo di esecuzione di un programma. Tale tempo è determinato da:
- numero di istruzioni;
- cicli di clock per istruzione (CPI);
- frequenza di un clock (1/ciclo di clock).

Tempo CPU = Numero Istruzioni * CPI * Periodo Clock = Numero Istruzioni * CPI / Frequenza Clock.

L'efficienza di un algoritmo è dovuta alla quantità di istruzioni e dalla scelta di quelle che risultano essere più efficienti per l'ISA.

Il linguaggio di programmazione influenza il numero di istruzioni e il CPI. <br>
Il compilatore sicuramente influenza sia il numero
di istruzioni che il CPI. Un compilatore più efficiente genera struzioni macchina diverse da un compilatore non efficiente.


#### 8.0 ISA

L’architettura del set di istruzioni (ISA) consiste nell’interfaccia che la macchina offre al software. <br>
Essa ha impatto sul numero di istruzioni, sul CPI, e sulla frequenza di clock. <br>
Esistono 3 tipi:
- RISC-V (architettura RISC);
- Intel (architettura CISC);
- ARM (architettura Advanced RISC).


#### 9.0 Numeri e codifica
Un numero naturale è espresso da una sequenza di cifre. Esistono *B* possibili cifre (da 0 a *B*-1). <br>
B è detta base di numerazione. Le basi pù utilizzate sono 2, 8, 10 e 16.

###### Sistema binario
- cifra binaria: binary digit (bit)
- numero massimo di cifre decimali rappresentabili: (2^k)-1

# Recuperare parte sulla conversione


##### Virgola fissa
Ho a disposizione un certo numero di bit. Un certo numero di bit fissi viene  utilizzata per rappresentare la parte del numero intera, una parte per la parte decimale. <br>
$k$ cifre, $k-f$ alla parte intera e $f$ alla parte decimale. <br>
Tutte le operazioni sono semplificate e diminuisce il lavoro per la CPU. <br>
Tuttavia non riesco a rappresentare un range esteso di numeri.

Esempio: <br>
101.100 da binario a decimale
La parte intera è semplice: $1*2^2+0*2^1+1*2^0 = 5$ <br>
La parte decimale: $1*2^{-1}+0*2^{-2}+0*2^{-3} = 0.5$ <br>
Il risultato sarà la somma: 5.5.

Conversione decimale da decimale a binario di 6.125: <br>
La parte intera si converte direttamente: 110. <br>
Per la parte decimale moltiplico la parte decimale ricorsivamente per 2, tante volte quanto sono i bit della parte decimale e considero nell'ordine le **parti intere** della moltiplicazione:
- 0.125 * 2 = 0.25 $\Rightarrow$ parte intera = 0
- 0.25 * 2 = 0.5 $\Rightarrow$ parte intera = 0
- 0.5 * 2 = 1 $\Rightarrow$ parte intera = 1

Mettendo insieme 6.125 = 110.001


##### Virgola mobile
Un numero $x$ pulò essere scritto come: $x=M*B^E$, dove $M$ = Mantissa e E = esponente.


#### Codifica del testo
L'idea è di utilizzare la codifica binaria per rappresentare i caratteri testuali. <br>
Con 7 bit rappresentiamo 128 possibili caratteri. ASCII, (**A**merican **S**tandard **C**ode for **I**nformation **I**nterchange). <br>
Esite la versione a 8 bit (**Exrended ASCII**) per altre lingue. <br>
Se il primo bit è 0 ci si riferisce all'ASCII. <br>
Se invece è a 1, l'interpretazione del carattere dipende dalla codifica, ad esempio:
- ISO 8859-1 (Latin 1): caratteri Europa Occidentale (lettere accentate, etc.)

Tuttavia se volessi rappresentare più caratteri, come quello arabo o cinese, ci servono molti più caratteri. Si utilizza **Unicode**, a 32 bit (più utilizzata). Altri sono UTF-16, a 16 bit o lunghezza variabile, UTF-8 8 o più bit. Con 8 bit corrisponde all'ASCII.

## Reti logiche
All'interno di un PC abbiamo due livelli fondamentali:
- Alto, asserito (1), associato alla tensione di alimentazione Vdd.
- Basso, negato (0): associato alla massa (tensione = 0).

Altri valori sono assunti solo in fase di transizione.
In un computer sono presenti dei transistor, successori delle valvole. Mettendo inseme tanti transistor posso creare circuiti integrati. <br>
Le reti logiche sono dei circuite che composte da transistor implementano una certa funzionalità, un mapping che dice come tradurre dei bit in ingresso in bit in uscita.

Le reti logiche sono di due tipi:
- Combinatorie, senza memoria, nulla dipende da ciò che è successo prima.
- Sequeqnziali, l'output dipende dalla storia degli ingressi passati (hanno memoria)

##### Tabella della verità
Una tabella in cui vi è il mapping dell'input e il conseguente output. Ad esempio la tabella della verità di AND è:
<table>
  <tr>
    <td>A</td>
    <td>B</td>
    <td>A AND B</td>
  </tr>
  <tr>
    <td>0</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>1</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>0</td>
    <td>1</td>
    <td>0</td>
  </tr>
  <tr>
    <td>1</td>
    <td>1</td>
    <td>1</td>
  </tr>
</table>

##### Algebra di Boule
Esitono 3 operatori di base:
- **AND**, rappresentato con il simbolo di prodotto *, produce 1 se entrambi gli operandi sono 1, 0 altrimenti.
- **OR**, rappresentato con il simbolo della somma +, restituisce 1 se almeno un operando è 1.
- **NOT**, inverte il bit.

Regole di semplificazione:
- Identità: A+0=A, A•1=A
- Regola «zero e uno»: A + 1 = 1, A•0=0
- Regola dell’inversa: A + Ā=1, A•Ā=0
- Regola commutativa: A+B=B+A, A•B=B•A
- Regola associativa: A+(B+C)=(A+B)+C, A•(B•C)=(A•B)•C
- Regola distributiva: A•(B+C)=(A•B)+(A•C),
A+(B•C)=(A+B)•(A+C)

Leggi di de Morgan:
- <p style="text-decoration: overline; display: inline">A•B</p> = Ā + <p style="text-decoration: overline; display: inline">B</p>
- <p style="text-decoration: overline; display: inline">A+B</p> = Ā • <p style="text-decoration: overline; display: inline">B</p>

#### Decoder standard a 3 bit
| In1 | In2 | In3 | Out7 | Out6 | Out5 | Out4 | Out3 | Out2 | Out1 | Out0 |
|-----|-----|-----|------|------|------|------|------|------|------|------|
| 0   | 0   | 0   | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 1    |
| 0   | 0   | 1   | 0    | 0    | 0    | 0    | 0    | 0    | 1    | 0    |
| 0   | 1   | 0   | 0    | 0    | 0    | 0    | 0    | 1    | 0    | 0    |
| 0   | 1   | 1   | 0    | 0    | 0    | 0    | 1    | 0    | 0    | 0    |
| 1   | 0   | 0   | 0    | 0    | 0    | 1    | 0    | 0    | 0    | 0    |
| 1   | 0   | 1   | 0    | 0    | 1    | 0    | 0    | 0    | 0    | 0    |
| 1   | 1   | 0   | 0    | 1    | 0    | 0    | 0    | 0    | 0    | 0    |
| 1   | 1   | 1   | 1    | 0    | 0    | 0    | 0    | 0    | 0    | 0    |


#### Conversione da tabella di verità a formula

| A | B | C | D |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 1 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 1 |

D = ($\overline A$ · $\overline B$ · C) + ($\overline A$ · B · $\overline C$)+  (A · $\overline B$ · $\overline C$) + (A · B · C)

## Assembly

La macchina esegue istruzioni costituite solo da 0 e 1, e l'uomo programma in c, c++, java, etc. Serve un linguaggio intermedio, l'assembly.

Il programma assembly è un file ASCII che contiene la descrizione testuale delle istruzioni. Viene compilato dall'assembler.

Ad ogni istruzione assembly corrisponde un'istruzione in linguaggio macchina, salvo eccezioni, come label, macro e riordinamento istruzioni). Le istruzioni dipendono dalla CPU e di conseguenza l'assembly non è portabile.

Ogni assembly è definito da un'ISA (Instruction Set Architecture), ovvero un insieme di istruzioni riconosciute dalla CPU, che l'assembler è in grado di convertire. Vi è una sintassi e una semantica ed è disponibile l'accesso diretto ai registri (in quanto presenti nel processore), mentre per la memoria RAM serve un sistema di indirizzamento. Vi sono casi in cui un processore supporta più ISA.

La Struttura di un programma Assembly deriva direttamente dal meccanismo di funzionamento di una CPU:
1. Fetch: preleva istruzione dalla memoria. Indirizzo memorizzato in apposito registro (Program Counter PC / Instruction Pointer IP)
2. Decode: decodifica l’istruzione (per capire cosa fare)
3.  Execute: esegue l’istruzione (operazione aritmetico / logica, accesso alla memoria, ecc.).

Il programma assembly è una lista di istruzioni solitamente eseguite in maniera sequenziale. Esistono istruzioni di salto (per rompere l’esecuzione sequenziale). Si tratta però di un linguaggio di basso livello: niente salti, cicli o selezioni.

##### Registri
Le istruzioni Assembly lavorano su dati:
- Immediati (costanti)
- Contenuti in registri
- Contenuti in memoria (varie modalita di indirizzamento)

Dove stanno gli operandi? Dove salvare il risultato (destinazione)?
• Due possibili “filosofie” diverse:
1. Tutto nei registri (operandi immediati) implementazione CPU piu semplice (e più elegante!)
2. Possibilita di avere operandi o destinazione in memoria linguaggio Assembly piu potente e più semplice da usare.
Talvolta, migliori performance

*La prima soluzione porta ad ISA RISC, la seconda ad ISA CISC*

**RISC** Reduced Instruction Set Computer<br>
Meno istruzioni, più semplice e meno potente. Uniche istruzioni che accedono alla memoria sono *load* e *store*

**CISC** Complex Instruction Set Computer<br>
Maggior numero di istruzioni; istruzioni piu “potenti” <br>
Tutte le istruzioni possono avere operandi (o destinazione) in memoria

Nel primo caso la destinazione dei calcoli sono i registri. I dati possono essere salvati e recuperati tramite le due istruzioni.

- **Intel**: tipico esempio di ISA CISC, ma ha “rubato” alcune idee a RISC (numero di registri, cmov, ecc.)
- **ARM**: ISA RISC “pragmatica” con modalita di indirizzamento più complesse, molte istruzioni (anche “complesse” e potenti), meno registri (16)

*Durante il corso vedremo tre ISA: MIPS (RISC “duro e puro”), Intel (CISC) ed ARM (RISC “pragmatico”)*

#### Accesso alla memoria
Istruzioni che accedono alla memoria:
- Istruzioni load e store per RISC
- Istruzioni generiche per CISC
In ogni caso, hanno argomento <memory location>

Come si esprime <memory location>?
Varie modalita di indirizzamento: `
1. Indirizzo di memoria costante espresso come valore immediato
2. Indirizzo di memoria contenuto in un registro
3. Indirizzo di memoria ottenuto shiftando (o comunque manipolando) il contenuto di un registro
4. Combinazione dei metodi precedenti

###### Modalità di indirizzamento
1. Assoluto: indirizzo codificato nell’istruzione Assembly <br>
Problematico per RISC perchè ho una sintassi regolare e per definire una costante ho un numero limitato di bit, ma la memoria può essere più grande.
2. Indiretto: registro contenente indirizzo codificato nell’istruzione Assembly
3. Base + Spiazzamento (2 + 1): indirizzo ottenuto sommando registro a valore immediato
4. Base + Indice (2 + 3): indirizzo ottenuto sommando registro a registro scalato / shiftato. <br>
Utile per implementare array con elementi di dimensione > 1
5.  Base + Indice + Spiazzamento (1 + 2 + 3): indirizzo ottenuto sommando registro, registro scalato / shiftato e valore immediato


Application Binary Interface (ABI): insieme di convenzioni software
che dicono come usare i registri

#### Instruction set
Insieme di istruzioni che il processore ci mette a disposizione. Un processore ne ha almeno una. Possono essere RISC E CISC. L'idea di IS proviene da Von Neumann. Egli pensò che alcuni comandi possono controllare lo stato dell'hardware (modificare lo stato, ovvero programmarlo).

## RISC-V
Già Von Neumann disse che all'interno di un processore ci devono essere operatori fondamentali algebrici.

Le istruzioni sono regolari. Ad esempio: <br>
a = b+c, diventa `add a,b,c`

Somma:
```c
a = b+c+d+e
```

In RISC-V si spezzettano le operazioni
```RISCV
add a,b,c
add a,a,d
add a,a,e
```

Sottrazione:
```RISCV
sub a,b,c   #quesa corrispone a a=b-c
```

Ci sono Assembly dove i commenti si fanno in stile c (/* */) e il risultato di un'operazione si immagazzina nel terzo valore passato.

Gli operandi (argomenti e destinazione), sono in realtà registri. <br>
RISC-V dispone di 32 registri da 64 bit.

La quantità di registri determina la lunghezza minima di un ciclo di clock.

L'istruzione `f = (g+h) - (i+j)` diventa:
```RISCV
add x5, x20, x21  # Il registro temporaneo# x5 viene settato alla
                  # somma dei registri:
                  # x20+x21 (g+h)
add x6, x22, x23  # Idem, x6 conterrà la
                  # somma x22+x23 (i+j)
sub x19, x5, x6   # f = x5 – x6
```

Tuttavia non sempre i registri bastano. E' necessario salvare informazioni in memoria.

##### La memoria
La memoria è una sequenza di bit organizzati in gruppi di 8 bit (1 byte). Ogni volta che salvo il valore di un registro in memoria trasferisco 64 bit (grandezza registri RISC-V). La maggior parte delle architetture non permette di leggere il singolo byte (singola cella), ma prendo l'intero valore (64 bit = 8 celle). Gli indirizzi saranno 0, 8, 16, ... <br>
Nell’assemblatore RISC-V l’indirizzo si specifica tramite una base (in un registro) e uno spiazzamento o offset (costante).

```RISCV
ld x9, 8(x22)     #Load Double (64 bit alla volta)
```

L’effetto di questa istruzione è di caricare in *x9* la parola doppia all’indirizzo dato da *x22* + 8

###### Istruzione leggermente più complessa
La seguente istruzione in c
```c
A[12] = h + A[8]
```

Diventa:
```RISCV
ld x9, 64(x22)      # il puntatore di A è in x22
                    # e l’ottava parola doppia
                    # comincia all’indirizzo
                    # x22 + 8*8
add x9, x21, x9     # h è in x21
sd x9, 96(x22)      # memorizzo il contenuto
                    # del registro x9 in A[12],
                    # ovvero all’indirizzo
                    # x22 + 12*8
```

###### Register spilling
Automaticamente il compilatore quando compila codice di alto livello, se ci sono più variabili che registri, vengono salvati in memoria e io valori recuperati quando necessario.

###### I registri
x0 è fisso a 0. In sola lettura.

##### Shift logico

Consideriamo per prima cosa lo shift logico a sinistra. L’idea è di inserire degli zeri nella posizione meno significativa e traslare tutto a sinistra perdendo (nel caso di overflow) i bit più significativi <br>
Ad esempio, supponiamo che x19 contenga il valore 9:
```
00000000 00000000 00000000 00000000 00000000 00000000 00000000 00001001
```

```RISCV
slli x11, x19, 4    # shift logical left immediate
```
```
00000000 00000000 00000000 00000000 00000000 00000000 00000000 10010000  
```

L’effetto è di memorizzare in x11 valore 9*2^4=144
