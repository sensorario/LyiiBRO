======
Events
======

--------
Scenario
--------

Vi è mai capitato di avere bisogno di eseguire una certa azione 
o di controllare dei dati ad ogni esecuzione di pagina? Yii ci permette di 
farlo. Nel forum italiano di Yii è stato posto il problema. Lo abbiamo 
analizzato un po'. Alla fine la soluzione migliore sembra essere quella di 
creare un comando da console, e di utilizzare un crontab per eseguirlo una 
tantum. Nel problema specifico le operazioni non andavano eseguite SEMPRE. Ma 
solo di tanto in tanto. Ma rimane il problema di poter eseguire un'azione ad 
ogni richiesta fatta. Ecco gli strumenti che ci mette a disposizione Yii 1.1:

Dopo aver creato una applicazione Yii, questo è il nostro file /index.php:

::

    <?php

    // change the following paths if necessary
    $yii=dirname(__FILE__).'/../yii/framework/yii.php';
    $config=dirname(__FILE__).'/protected/config/main.php';

    // remove the following lines when in production mode
    defined('YII_DEBUG') or define('YII_DEBUG',true);
    // specify how many levels of call stack should be shown in each log message
    defined('YII_TRACE_LEVEL') or define('YII_TRACE_LEVEL',3);

    require_once($yii);
    Yii::createWebApplication($config)->run();

Fate molta attenzione a queste due righe:

::

    require_once($yii);
    Yii::createWebApplication($config)->run();

Quando lanciamo run, viene eseguita tutta la nostra richiesta, cercando il 
controller, la action, ... e così via. Ma noi possiamo infilarci in mezzo. 
Possiamo utilizzare, per esempio, gli eventi di Yii. Esatto! Yii ha una 
programmazione ad eventi. Non è il solo framework ad avere questa feature, ma la
implementa in un modo davvero semplice ed interessante.

Non entro nel dettaglio. Fatto sta che se vogliamo possiamo usare alcuni eventi,
ovvero onBeginRequest oppure onEndRequest. Provate a vedere che cosa succede se
sostituite le due righe qui sopra con le due righe qui sotto all'interno della 
vostra applicazione.

::

    require_once($yii);
    $application = Yii::createWebApplication($config);

    Yii::app()->onBeginRequest = function ($event) {
    echo "onBeginRequest";
    };

    Yii::app()->onEndRequest = function ($event) {
    echo "onEndRequest";
    };

    $application->run();

Questa "tecnica" va usata con cautela: potrebbe appesantire l'esecuzione delle 
nostre pagine web. In ogni caso, può essere interessante conoscere queste 
potenzialità di Yii. Ci tenevo a raccontarvele =).