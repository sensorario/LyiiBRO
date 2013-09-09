Ottenere l'entity manager facendo BDD
-------------------------------------

Quando si eseguono dei test, si tratti di BDD o TDD, i test devono essere fatti
in modo tale che il sistema non venga alterato durante l'esecuzione del test.
Questo vuole dire che il sistema può essere inizializzato all'inizio di ogni 
test. Quando si crea una feature, è possibile definire un background che pulisca
il database prima che venga lanciato uno scenario. Il background viene lanciato
prima di ogni scenario e non solo all'inizio della feature.

    Feature: Some stuff

        Background: Database is empty
           Given There is no "User" in database
           And exists admin "demo" with password "demo"

        Scenario: As User I cant make an empty donation

La frase che bisogna aggiungere al FeatureContext deve essere in grado di
accedere al database e quindi di caricare Doctrine.

    class FeatureContext extends MinkContext implements KernelAwareInterface
    {

        /**
         * @Given /There is no "([^"]*)" in database/
         */
        public function thereIsNoRecordInDatabase($entityName)
        {

            $em = $this->getManager();

            $entityRepository = $em
                ->getRepository("AcmeDemoBundle:{$entityName}");

            $entities = $entityRepository->findAll();

            foreach ($entities as $entity) {
                $em->remove($entity);
                $em->flush();
            }

        }

        private function getManager()
        {

            return $this
                    ->kernel
                    ->getContainer()
                    ->get('doctrine')
                    ->getManager();
            ;

        }

    }
