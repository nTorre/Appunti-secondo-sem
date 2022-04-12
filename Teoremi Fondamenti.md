# Teoremi per fondamenti
<hr>

#### 1. Teorema: L’ordinamento dei numeri naturali è un buon ordinamento (dimostrato utilizzando la prima forma del principio di induzione) e seconda forma del principio di induzione. (Pagina 20 pdf).

*L'ordinamento dei numeri naturali è un buon ordinamento*

###### Dimostrazione:

Supponiamo che l'insieme $A \subseteq \mathbb{N}$ non abbia minimo. e proviamo che allora A = $\emptyset$. Chiamiamo $B$ il suo complementare ($B = \mathbb{N}-A$) e dimostriamo per induzione che:
$$
\forall n \in  \mathbb{N} \:\:\:\: \{0, 1, ..., n\} \subseteq B
$$

$0 \notin A$, altrimenti ne sarebbe il minimo, quindi 0 $\in$ B e pertanto {0} $\subseteq B$. Supponiamo che $\{0, 1,...,n\} \subseteq B$, allora $0,1,...,n \notin A$ e quindi $n+1 \notin A$, altrimenti ne sarebbe il minimo, ma allora $n+1 \in B$ e pertanto $\{0,1,...,n,n+1\} \subseteq B$. <br>
Ma allora $B = \mathbb{N}$ e quindi $A=\emptyset$.


<hr>

#### 2. Teorema di esistenza e unicità del quoziente e del resto della divisione euclidea tra numeri interi.

*Siano $n,m \in \mathbb{Z}$ con $m \neq 0$, allora esistono unici $q,r \in \mathbb{Z}$ tali che*
$$
n = mq + r \\
0 \leq r < |m|
$$

###### Dimostrazione:

**Esistenza** <br>
Supponiamo dapprima che $n,m \in \mathbb{N}$ ed usiamo il principio di induzione nella seconda forma su $n$. Se $n = 0$ basta prendere $q=0$ e $r=0$. Supponiamo $n > 0$ e che la tesi sia vera per ogni $k < n$. Se $n < m$ basta prendere $q=0$ e $r=n$, altrimenti sia $k=n-m$ dato che $m \neq 0 \:\:\: 0 \leq k < n$, quindi per ipotesi di induzione esistono $q, r \in \mathbb{N}$ tali che:
$$
k = mq + r \\
0 \leq r < m
$$
ma allora $n=k+m=mq+r+m=(q+1)m+r$. <br>
Supponiamo ora $n<0$ e $m>0$. Allora $-n >0$ e quindi per il caso precedente si ha che esistono $q,r \in \mathbb{Z}$ tali che $-n=mq+r$ e $0 \leq r < m$ allora 

<hr>

3. Teorema di rappresentazione dei numeri naturali in una base arbitraria maggiore o uguale a 2.

4. Teorema di esistenza e unicità del massimo comun divisore e del minimo comune multiplo di due numeri interi non entrambi nulli.

5. Teorema fondamentale dell’Aritmetica (ogni numero maggiore o uguale a due è esprimibile come prodotto di numeri primi, e tale espressione è unica a meno di ordinamento).

6. Teorema cinese del resto.

7. Teorema di Fermat-Eulero (elevando ogni classe invertibile modulo n alla
Φ(n) si ottiene la classe di 1 modulo n) e crittografia RSA.

8. Teorema di equivalenza tra la congiungibilià con cammini e la congiungibilità con passeggiate e Teorema: La relazione di congiungibilità è una relazione di equivalenza.

9. Relazione fondamentale dei grafi finiti (la somma dei gradi è pari al doppio del numero dei lati) e lemma delle strette di mano.

10. Teorema di caratterizzazione degli alberi finiti mediante la formula di Eulero
(connessione e |E| = |V | − 1).

11. Teorema di esistenza dell’albero di copertura per i grafi connessi finiti.
