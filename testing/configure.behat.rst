Aggiungere Behat ad un progetto yii esistente
---------------------------------------------

Scrivo questa piccola guida perché ho sempre e solo usato Behat all'interno di un contesto Symfony2 e quindi all'interno di un Bundle. Ho sempre fatto questo e non mi sono mai spinto oltre arrivando ad usare Behat anche in progetti già avviati, che magari fanno uno di altri framework per esempio Yii. Vorrei, quindi unire la versatilità di Yii con la potenza di Behat.

Configurare il composer.json
============================

Per prima cosa si deve aggiungere il composer.json. Il composer scaricerà per noi anche un bel po' di componenti di Symfony2 che ci saranno utili per poter usare file ".yml" nel nostro lavoro, ma non solo.

::

    {
        "require": {
            "behat/behat": "2.4.*@stable",
            "behat/mink": "1.4.*@stable",
            "behat/mink-extension": "*",
            "behat/mink-goutte-driver": "*",
            "behat/mink-selenium2-driver": "*"
        },
        "minimum-stability": "dev",
        "config": {
            "bin-dir": "bin/"
        }
    }

Scaricare il composer
=====================

Dopo aver creato il nostro composer.json, possiamo finalmente scaricare il composer e quindi lanciarlo per l'installazione di tutti i componenti di cui abbiamo bisogno.

::

    $ curl http://getcomposer.org/installer | php
    $ php composer.phar install

Scaricare il composer
=====================

Una volta che abbiamo aggiunto al nostro progetto il composer, possiamo inizializzare behat (che deve essere installato nella nostra macchina).

::

    $ behat --init

File di configurazione di behat
===============================

A questo punto possiamo creare un file behat.yml minimale. In questa configurazione mi limito ad indicare il base_url dei nostri test. In questo modo potremo indicare anche solo il percorso relativo delle nostre url.

::

    default:
        extensions:
            Behat\MinkExtension\Extension:
                base_url: http://localhost/website:
                goutte: ~
                selenium2: ~

Aggiungere MinkContext
======================

Adesso possiamo andare nel nostro features/bootstrap/FeatureContext.php e caricare il MinkContext ed estendere questo al posto di BehatContext.

::

    use Behat\MinkExtension\Context\MinkContext;

Lanciare bin/behat
==================

Abbiamo terminato il nostro lavoro. Tutto quello che dobbiamo fare ora, è lanciare behat.

::

    $ bin/behat

