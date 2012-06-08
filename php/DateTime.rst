Differenza tra date
-------------------

Eccome come sfruttare la classe DateTime per calcolare la differenza tra due
date.

::

    $primaData = new DateTime($dataDa);
    $secondaData = new DateTime($dataA);
    $differenza = $secondaData->diff($primaData);