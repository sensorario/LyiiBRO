========
Sessions
========

A short snippet to set some value in session

::

    $session = $this->getRequest()->getSession();
    $session->set('name', 'Sensorario');

And a very very simple example to get this value

::

    echo $session->get('name');