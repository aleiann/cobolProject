# cobolProject

Questo progetto include:

Modularità con subprogrammi, che simulano varie operazioni bancarie come prelievi, depositi e consultazione del saldo.

Condivisione di variabili tramite un'area globale (usando una COPYBOOK).

Uso della Communication Area (COMMAREA) in un ambiente transazionale (simile a CICS).

File condivisi per memorizzare i dati dei conti correnti.

Struttura del Progetto

MAINPROGRAM.CBL: Programma principale che riceve input dall'utente e gestisce le operazioni.

TRANSACTIONMODULE.CBL: Subprogramma per eseguire transazioni bancarie (deposito/prelievo).

BALANCEMODULE.CBL: Subprogramma per controllare e restituire il saldo corrente.

ACCOUNT-STRUCTURE.CPY: Copybook che definisce la struttura dei dati condivisi (numero di conto e saldo).

CONTIDB.DAT: File contenente i conti correnti e i saldi.

1. Modularità con subprogrammi

Il progetto è suddiviso in più moduli. Il programma principale (MAINPROGRAM.CBL) gestisce l'input dell'utente e decide quale operazione eseguire (consultazione saldo o transazione).
Il modulo di transazione (TRANSACTIONMODULE.CBL) gestisce l'aggiornamento del saldo in base alla transazione (deposito o prelievo).
Il modulo di saldo (BALANCEMODULE.CBL) legge il saldo corrente dal file dei conti.
Questo approccio rende il progetto modulare e facilmente manutenibile. Ogni funzione (consultazione saldo e transazione) è gestita da subprogrammi separati.

3. Condivisione di variabili tramite una Copybook
   
La copybook ACCOUNT-STRUCTURE.CPY definisce la struttura comune del record del conto bancario (numero di conto e saldo). Questa copybook viene inclusa sia nei subprogrammi che nel programma principale, assicurando che la struttura del record sia la stessa in tutto il progetto.
Ciò semplifica la manutenzione e garantisce che eventuali modifiche alla struttura dei dati (ad esempio, l'aggiunta di nuovi campi) possano essere propagate automaticamente a tutti i moduli.

3. Uso della Communication Area (COMMAREA)
   
La COMMAREA viene utilizzata per passare informazioni tra il programma principale e i subprogrammi. Questo approccio è tipico nei sistemi transazionali come CICS, dove la COMMAREA agisce come area di memoria condivisa tra moduli COBOL.

La COMMAREA (01 COMMAREA) contiene il numero del conto, l'importo della transazione e il nuovo saldo.
Quando viene chiamato un subprogramma, i dati vengono passati attraverso la COMMAREA, che viene definita nella Linkage Section del subprogramma.

4. File condivisi
I dati dei conti correnti sono memorizzati in un file di dati sequenziale (CONTIDB.DAT), che contiene il numero di conto e il saldo. Questo file viene aperto e modificato sia dal modulo di transazione che dal modulo di saldo.

Nel modulo di transazione, il saldo viene aggiornato in base alla transazione (deposito o prelievo).
Nel modulo di saldo, il saldo corrente viene letto e restituito al programma principale per la visualizzazione.
