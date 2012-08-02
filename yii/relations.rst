===========================================
Aggiungere una relazione con una condizione
===========================================

--------
Scenario
--------

E' possibile indicare una relazione nel proprio model, e fare in modo che 
esista solo in una determinata condizione.

::

    public function relations () {
        return array(
            'user' => array(self::HAS_ONE, 'Users', 'foreign_key', array(
                'condition' => 'user.type = :type',
                'params' => array(':type' => 3)
            )),
        );
    }
