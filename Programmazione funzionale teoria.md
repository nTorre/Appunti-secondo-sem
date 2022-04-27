## Appunti di teoria di programmazione funzionale

### 1 Introduzione alle macchine

#### 1.1 Abstract machines
Un computer è composto almeno dalle seguent componenti:
- un processore (CPU), il quale **esegue** le instruzioni macchina e per farlo **accede alla memoria** per caricare e recuperare dati.
- Una memoria principale (RAM), nella quale vengono salvati dati e programmi (lista di istruzioni). E' veloce ma volatile.
- Memoria di massa, più lenta della RAM, ma persistente
- Periferiche di I/O

#### 1.2 Architettura
Le diverse componenti del computer sono collegate tramite il **bus**, composto da una serie di connessioni elettriche. Trasmette, inoltre, istruzioni macchina tra CPU e RAM e i dati salvati nella memoria di massa.

#### 1.3 Macchina di Von Neumann
L'architettura di Von Neumann è una tipologia di architettura hardware per computer digitali programmabili a programma memorizzato la quale condivide i dati del programma e le istruzioni del programma nello stesso spazio di memoria.

<img src="Images/vonneumann.png">
<br><br>

Lo schema si basa su cinque componenti fondamentali:

1. **Unità centrale di elaborazione (CPU)**, che si divide a sua volta in unità aritmetica e logica (ALU o unità di calcolo) e unità di controllo;
2. **Unità di memoria**, intesa come memoria di lavoro o memoria principale (RAM, Random Access Memory);
3. **Unità di input**, tramite la quale i dati vengono inseriti nel calcolatore per essere elaborati;
4. **Unità di output**, necessaria affinché i dati elaborati possano essere restituiti all'operatore;
5. **Bus**, un canale che collega tutti i componenti fra loro.

#### 1.4 Il processore
Il processore ottiene le istruzioni dalla memoria e le esegue. Durante l'esecuzione di un'istruzione può essere necessario accedere alla memoria per scrivere o ottenere dati. Il processore è composto da due parti:
- parte di controllo, la quale ottiene ed esegue le istruzioni.
- Parte operativa, detta anche Arithmetic Logic Unit (ALU) che esegue istruzioni logiche e aritmetiche
- Nelle CPU moderne vi è anche l'FPU, Floating Point Unit che si occupa del calcolo della virgola mobile.

Contiene, inoltre, dei **registri** i quali possono essere visibili o invisibili al programmatore.

#### 1.5 I registri
I registri sono di due tipi:
- **invisibili** ovvero non accessibili direttamente dalle istruzioni. Essi sono **Address Register (AR)**, ovvero l'indirizzo per accedere al bus e il **Data Register (DR)** dati da leggere e scrivere
- **visibili** accessibili dalle istruzioni macchina e sono:
  - **Program Counter**, indirizzo dell'istruzione macchina successiva a execute (chiamato anche **Instruction Pointer** IP)
  - **Status Register** (SR): flag che descrivono il risultato di un'operazione dell'ALU e lo stato della macchina (detta anche F, per Flag Register)
  - Diversi registri per dati e indirizzi

#### 1.6 Esecuzione di istruzioni
I passaggi sono i seguenti:
- 1 **Fetch**, leggo l'istruzione che dev'essere eseguita. I passaggi sono i seguenti:
  - Copia il Program Counter nell'Address Register
  - Trasferimento del dato in memoria corrispondente all'AR dalla RAM al Data Register
  - Salvo il DR in un regiatro invisibile
  - Incermento il PC
- 2 **Decode**, decodifica dell'istruzione
- 3 **Execute**, esecuzione dell'istruzione. Se necessario:
  - salvo dati in memoria
  - leggo dati dalla memoria
  - modifico il PC (instruzioni salto)

#### 1.7 Memoria principale
Nel modello di Von Neumann, istruzioni e dati sono contanuti entrambi nella memoria. Si accede tramite il bus ed è costituita da celle di grandezza di 8 bit. L'accesso avviene tramite i seguenti passaggi:
1. Carica l'indirizzo al quale bisogna accedere nell'AR
2. In caso di operazioni di scrittura, si salva il dato da scrivere nel DR
3. Viene inviato il segnale tramite il bus
4. In caso di lettura, il risultato viene salvato nel DR

#### 1.8 Physical Machine and Abstract Machine
Le Physical Machines sono la concretizzazione delle Abstract Machines. Nelle abstract machines:
- $M_L$ è un'abstract machine che capisce ed esegue un linguaggio $L$.
- $L$ è il linguaggio macchina per $M_L$
- programma A: A è una lista di istruzioni $L$

*$M_L$ è un modo di descrivere $L$*

#### 1.8 Implementazione di un linguaggio

Esiste un solo linguaggio macchina per macchina astratta, ma un linguaggio può essere compreso da diverse macchine, ma può cambiare la sua implementazione. Implementare un linguaggio $L$ significa realizzare una macchina astratta $M_L$ che può eseguire un programma scritto in $L$.

Il software esegue su un Host Machine $MO_{LO}$ (con linguaggio macchina $LO$) tramite due approcci:
- interpretato, ovvero un programma scritto in $LO$ che capisce ed esegue il linguaggio $L$
- compilato, un programma che può tradurre altri programmi da $L$ a $LO$
- versione ibrida, il programma viene tradotto in un linguaggio intermedio $LI$, interpretato poi da un programma $MO_{LO}$ scritto il $LI$ (bytecode, ...).

#### 1.9 Linker e loader

I compilers non sempre compilano completamente un programma. Per efficienza alcune parti del programma sono compilate separatamente (ad esempio le librerie). I **linker** collegano le varie componenti. Esso può essere statico o dinamico. Rimpiazza gli indirizzi realtivi con quelli assoluti


### 2 Names and environments
I nomi sono sequenze di caratteri utilizzati per denotare qualcos'altro. Nei linguaggi di programmazione sono spesso identificatori (token alfanumerici)

#### 2.1 Denotable objects
Essi sono gli oggetti che possono essere associati a nomi. Vengono assegnati dal programmatore (variabili, parametri formali, tipi definiti dall'utente, labels, procedure, costanti, eccezioni, ...). Altri vengono definiti dal linguaggio (tipi primitivi, operazioni primitive). <br>
Il **Binding** è la procedura di associazione tra nome e oggetto. Il nome e l'oggetto non sono la stessa cosa. Il primo è solo una stringa di caratteri, mentre il secondo può essere complesso (funzione, tipo etc). Un nome può identificare più oggetti.

#### 2.2 Binding
Quando avviene?
- Con le parole chiave di un linguaggio
- Scrittura del programma, ovvero quando l'associazione nome-oggetto viene fatta nel programma, ma ha effettivamente luogo solo quando la variabile è allocata in memoria.
- In compilazione, ad esempio per le variabili di dimensioni nota a priori
- Runtime, tutte le associazioni non fatte prima avvengono in questa fase.

Statico o dinamico?
- Statico quando tutto avviene prima dell'esecuzione
- Dinamico se avviene durante l'esecuzione

 Basta pensare all'allocazione statica e dinamica. La prima avviene staticamente, la seconda dinamicamente :*

#### 2.3 Environments
Esso rappresenta l'insieme delle associazioni tra nomi e denotable objects che esistono runtime in un certo punto dell'esecuzione. La **dichiarazione** è un meccanismo, implicito o esplicito, che crea un'associazione in un environment.

Inoltre è possibile il fenomeno dell'**aliasing**, ovvero due nomi che si riferiscono allo stesso oggetto:
```c
int *X, *Y;
*X = 5;
Y = X ; // Y points to the same object as X
```

#### 2.4 Blocchi

Nei moderni linguaggi di programmazione l'environment è *strutturato*. Un **blocco** è una sezione di un programma delimitata da simboli di apertura e chiusure che contiene dichiarazioni *locali* per questa determinata regione:
- Algol, Pascal `begin end`
- Java, c `{...}`
- Lisp `(...)`
- ML `let in end`
- Altri casi:
  - Anonimo (o inline)
  - Associato ad una procedura

Vi sono diverse ragioni per utilizzare i blocchi. Ad esempio per comodità di visibilità di variabili, chiarezza, migliore utilizzo della memoria, ricorsione.

L'utilizzo dei blocchi introduce il concetto di **nesting**. Una dichiarazione locale è visibile nel blocco in cui si trova e in tutti quelli contenuti dal blocco stesso (nested) fino al momento in cui non viene dichiarata un'altra variabile con lo stesso nome, questo nasconde o maschera la dichiarazione precedente.


#### 2.5 Suddivisione dell'environment
L'environment in uno specifico blocco può essere suddiviso in:
- **local environment**, che comprende le associazioni effettuate all'interno del blocco locale
- **non local environment**, ovvero le associazioni che vengono ereditate da altre blocchi
- **global environment**, l'environment che comprende tutte le associazioni visibili in tutti i blocchi

Un'associazione creata quando si entra in un blocco locale (naming), può essere utilizzata (referecing) all'interno del blocco. Eventualmente può disattivare un'associazione effettuata precedentemente in un blocco "padre" che viene riattivata quando si esce dal blocco locale e l'associazione viene distrutta. Dunque le operazioni effettuabili sui denotable objects sono:
- Creazione
- Accesso
- Modifica (se l'oggetto è modificabile)
- Distruzione

*Nota: la creazione e distruzione di un oggetto non sono la stessa cosa della distruzione e creazione dell'associazione*

Eventi fondamentali:
1. Creazione di un oggetto
2. Creazione di un'associazione per l'oggetto
3. Reference ad un oggetto tramite associazione
4. Disattivazione di un'associazione
5. Riattivazione di un'associazione
6. Distruzione di un'associazione
7. Distruzione di un oggetto

*Note: da 1 a 7 si tratta della lifetime di un oggetto* <br>
*Note: da 2 a 6 si tratta della lifetime di un'associazione*


#### 2.6 Lifetime
