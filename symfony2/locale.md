==============================
Gestire il locale con Symfony2
==============================

Il codice che segue, mostra un controller molto semplice che risponde a due
tipologia di rotta. La rotta può essere "/", ed in quel caso $_locale verrà
impostato ad valore di default che sarà 'it'. Nel caso in cui, invece, la lingua
venisse espressa nella rotta, sovrascriverà il valore di default.

::

    <?php

    namespace Sensorario\AlimentazioneBundle\Controller;

    use Symfony\Bundle\FrameworkBundle\Controller\Controller;
    use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
    use Sensio\Bundle\FrameworkExtraBundle\Configuration\Template;

    class DefaultController extends Controller
    {
        /**
         * @Route("/{_locale}/", name="homepage")
         * @Route("/")
         * @Template()
         */
        public function indexAction($_locale = 'it')
        {
            return array();
        }
    }

Ma questo non basta per poter tradurre una applicazione con Symfony2.3. Dentro
al file app/config/config.yml bisogna importare il valore di
framekork.translator:

::

    framework:
        translator:      { fallback: %locale% }

%locale% è una variabile che è stata impostata in app/config/parameters.yml.

All'interno della vista, le traduzioni si possono "chiamare" in questo modo:

::

    {% trans %}traduzione{% endtrans %}

Le traduzioni vanno inserite nel file yml

::

    src/Acme/DemoBundle/Resources/translations/messages.it.yml

Ed al suo interno deve esserci un contenuto come questo:

::

    traduzione: Traduzione yaml

Ovviamente è possibile impostare una traduzione anche in formati diversi dal 
formato yml. Possiamo usare anche i formati xml e php.

## Documentazione ufficiale

 - [Traduzioni](http://symfony.com/it/doc/current/book/translation.html#tradurre-i-messaggi-dei-vincoli)