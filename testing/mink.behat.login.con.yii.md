Effettuare login usando Mink+Behat
----------------------------------

Nel forum italiano è sorto il problema di "come testare il login di un utente". Tra una prova e l'altra, ho creato una nuova applicazione che effettua il login con diversi utenti e per farlo ogni mio test eseguiva i passi elementari:

 * andare alla pagina di login
 * compilare username e password
 * premere login

A quel punto ho pensato di creare un unico metodo che facesse tutto in un uno cpassaggio

::

    /**
     * @Given /^I am logged as "([^"]*)" with password "([^"]*)"$/
     */
    public function iAmLoggedAsWithPassword($username, $password)
    {
        $this->getSession()->visit($this->locatePath('/index.php?r=site/login'));
        $this->getSession()->getPage()->fillField('LoginForm[username]', $this->fixStepArgument($username));
        $this->getSession()->getPage()->fillField('LoginForm[password]', $this->fixStepArgument($password));
        $this->getSession()->getPage()->pressButton('Login');
    }

Aggiungendo questo step al mio FeatureContext posso scrivere test ancora più rapidamente.