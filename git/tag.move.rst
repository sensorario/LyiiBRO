Spostare un tag
---------------

Taggare è un modo fantastico per segnare l'avanzamento della versione del proprio software. Però può capitare che una versione sia stata taggata ma anche che il tag debba essere spostato per via del fatto che dei bug sono stati fissati o altre questioni di questo tipo. Il comando per taggare il nostro repository è semplice:

::

    git tag v0.3

Se per qualsiasi ragione continuamo a sviluppare per questa versione del software, abbiamo la necessità di spostare spostare il tag, per farlo possiamo semplicemente posizionarci nel commit che ci interessa e li lanciare il comando.

::

    git tag -f v0.3
