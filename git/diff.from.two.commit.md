Verificare la differenza che c'è tra due distinti commit
--------------------------------------------------------

Con il comando git diff è possibile vedere le differenza tra l'object store e la nostra working directory. Al più possiamo vedere le differenze tra il nostro object store e cià che abbiamo in stage aggiungendo il parametro --cache. Esiste comunque la possibilità di ottere il numero di righe che sono state modificate tra due differenti commits a prescindere dalla loro distanza.

    git diff --shortstat "@{7 day}"

Tra parentesi graffe, possiamo indicare il periodo che preferiamo: ore, minuti, secondi, giorni, anni.
