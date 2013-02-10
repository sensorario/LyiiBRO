Test unitari con Yii
--------------------

Un breve esempio di test unitare fatto con Yii. Per lanciarlo bisogna ricordarsi di andare nella directory dei test: protected/tests e li lanciare il comando

::

    phpunit unit/

Questo, ovviamente, se si vogliono lanciare i test unitari. Per quelli funzionali basta sostituire unit/ con functional. Ma ecco un esempio di codice di test unitario. In verità questo è codice fine a se stesso: non stiamo testando del vedo codice nostro, ma del codice PHP.

::

    class FirstTest extends CTestCase
    {
            public function testQualcosa()
            {
                    preg_match_all("/@(\w+)/", 'Ciao mamma vado da @sensorario', $matches);
                    $occorrenze = array();
                    foreach ($matches[1] as $token) {
                            $occorrenze[] = $token;
                    }
                    $this->assertEquals(array('sensorario'), $occorrenze);
            }
    }

Supponiamo però di avere necessariamente bisogno di uno strumento in grado di parsare del testo, in grado di restituirci un array con l'elenco dei nickaname presenti. Per convenzione, diciamo che un nickname è composto dal simbolo "@" seguido da una sequenza di caratteri alfanumerici. Chiamerò questa classe NicknameParser. Ricordiamoci che dobbiamo sempre scrivere prima il test e poi il codice che lo soddisfa. Quindi andiamo a creare il file protected/tests/unit/NicknameParserTest. Il primo messaggio di errore che incontreremo ci dirà che non ci sono test. E' giusto: infatti non esiste all'interno di NicknameParserTest alcun metodo che inizia con test.

::

    class NicknameParserTest extends CTestCase
    {
    }

Adesso creiamo un primo test per assicurarci che la classe NicknameParser esista. Rimarremo delusi leggendo il messaggio "include(NicknameParser.php): failed to open stream: No such file or directory". E' giustissimo. Non la abbiamo ancora creata. Quindi creiamola in questo modo e proviamo a rilanciare i test. 

::

    class NicknameParser extends CComponent
    {

    }

Ecco il nuovo risultato dei nostri test:

::

    .

    Time: 0 seconds, Memory: 4.75Mb

    OK (1 test, 1 assertion)

Adesso voglio che sia possibile assegnare al NicknameParser un testo.

::

    class NicknameParserTest extends CTestCase
    {
        ...

        public function testAssignMessage()
        {
            $nnp = new NicknameParser();
            $nnp->setText('Ciao mamma sono andato da @stefano e @michela. Ciao ciao!');
            $this->assertEquals('Ciao mamma sono andato da @stefano e @michela. Ciao ciao!', $nnp->getText());
        }
    }

Lanciando questi test otterremo come messaggio di errore:

::

    CException: NicknameParser and its behaviors do not have a method or closure named "setText"

Questo messaggio lo elimineremo semplicemente creando un metodo. Il mio scopo non è scrivere codice per me, ma per il test.

::

    class NicknameParser extends CComponent
    {
        public function setText()
        {
        }
    }

Ancora una volta, lanciando i test, riceverò un messaggio di errore:

::

    CException: NicknameParser and its behaviors do not have a method or closure named "getText"

So cosa fare: 

::

    class NicknameParser extends CComponent
    {
        public function setText()
        {
        }
        public function getText()
        {
        }
    }

Il tipo di messaggio è cambiato:

::

    Failed asserting that null matches expected 'Ciao mamma sono andato da @stefano e @michela. Ciao ciao!'.


Questa volta PHPUnit ci dice che ci aspettavamo che un valore null fosse in verità: 'Ciao mamma sono andato da @stefano e @michela. Ciao ciao!'. Quindi andiamo a fare in modo che questo test diventi green. Proviamo così:

::

    class NicknameParser extends CComponent
    {
        private $text;
        public function setText($text)
        {
            $this->text = $text;
        }
        public function getText()
        {
            return $this->text;
        }
    }

Il risultato dovrebbe essere più o meno questo:

::

    ..

    Time: 0 seconds, Memory: 4.75Mb

    OK (2 tests, 2 assertions)

Cioè che vorrei adesso, è un metodo che sia in grado di restituirmi un array con tutti i nicknames presenti all'interno del messaggio che abbiamo assegnato al parser. Vorrei che questo metodo si chiamasse NicknameParser::getArrayNicknames();.

::

    class NicknameParserTest extends CTestCase
    {
        ...
        public function testParsingOfNicknames()
        {
            $npp = new NicknameParser();
            $nnp->setText('Ciao mamma sono andato da @stefano e @michela. Ciao ciao!');
            $nnp->assertEquals(array('stefano', 'michela'), $nnp->getArrayNicknames());
        }
        ...
    }

Esattamente come poco fa, prima lanciamo un test che ci avviserà della non esistenza di quel metodo:

::

    CException: NicknameParser and its behaviors do not have a method or closure named "getArrayNicknames".

e successivamente:

::

    null does not match expected type "array".

Effettivamente noi vorremmo che questo NicknameParser restituisse sempre un array. Facciamo in modo che sia così:

::

    class NicknameParser extends CComponent
    {
        ...
        public function getArrayNicknames()
        {
            return array();
        }
    }


E poi ecco il messaggio che stavo aspettando:

::

    Failed asserting that two arrays are equal.
    --- Expected
    +++ Actual
    @@ @@
     Array (
    -    0 => 'stefano'
    -    1 => 'michela'
     )

Facciamolo diventare green! Proviamo in questo modo:

::

    class NicknameParser extends CComponent
    {
        ...
        public function getArrayNicknames()
        {
            return array('stefano','michela');
        }
    }

Sembrerà stupida come soluzione, ma se ci pensate è esattamente quello che abbiamo richiesto nel test. PHPUnit ci mette a disposizione uno strumento molto importante. Questo strumento sono i provider. Possiamo infatti fare in modo che una serie di metodi e venga richiamata con diversi parametri.

::

    class NicknameParserTest extends CTestCase
    {
        ...
        public static function provider()
        {
            return array(
                array('Ciao io sono @sensorario',array('sensorario')),
                array('@michele ed @alessandro sono amici', array('michele','alessandro'))
            );
        }

        /**
         * @dataProvider provider
         */
        public function testParsingOfNicknames($text, $nicknames)
        {
            $nnp = new NicknameParser();
            $nnp->setText($text);
            $this->assertEquals($nicknames, $nnp->getArrayNicknames());
        }
    }

Ecco qui l'errore:

::

    Failed asserting that two arrays are equal.
    --- Expected
    +++ Actual
    @@ @@
     Array (
    -    0 => 'sensorario'
    +    0 => 'stefano'
    +    1 => 'michela'
     )

    /var/www/Bakyii/protected/tests/unit/NicknameParserTest.php:34

    2) NicknameParserTest::testParsingOfNicknames with data set #1 ('@michele ed @alessandro sono amici', array('michele', 'alessandro'))
    Failed asserting that two arrays are equal.
    --- Expected
    +++ Actual
    @@ @@
     Array (
    -    0 => 'michele'
    -    1 => 'alessandro'
    +    0 => 'stefano'
    +    1 => 'michela'
     )

    /var/www/Bakyii/protected/tests/unit/NicknameParserTest.php:34

    FAILURES!
    Tests: 4, Assertions: 4, Failures: 2.

Correggiamo il nostro componente:

::

    class NicknameParser extends CComponent
    {
        ...
        public function getArrayNicknames()
        {
            preg_match_all("/@(\w+)/", $this->text, $matches);
            $occorrenze = array();
            foreach ($matches[1] as $token) {
                $occorrenze[] = $token;
            };
            return $occorrenze;
        }
    }


Lanciare un test senza provider, può significare scrivere un test che risolve l'unico problema che abbiamo implementato. Ma noi non vogliamo che il nostro codice funzioni solo in un caso, ma in tutti quanti i casi che ci viene in mente di indicare nel provider. Vediamo ora che cosa succede se inseriamo come codice.

::

    ....

    Time: 0 seconds, Memory: 5.00Mb

    OK (4 tests, 4 assertions)

Ecco fatto. Abbiamo scritto un componente che è in grado di ricevere in ingresso del testo e di restituire tutti quanti i nickname presenti al suo interno.
