Proteggere una rotta
--------------------

Quando vogliamo proteggere una rotta dall'accesso di un utente. Possiamo
intervenire nel security.yml. In questa piccola guida spiegheremo come prendere
una rotta come inibirne l'accesso nel caso in cui un utente non sia in possesso
dei requisisiti minimi per terla visualizzare.

Questa à la nostra rotta.

::

    /congresso/new

Faremo in modo che un utente dovrà essere autenticato e con un ruolo maggiore o 
uguale a **ROLE_USER**.

::

    security:
        access_control:
            - { path: ^/congresso/new, role: ROLE_USER }

Ecco fatto. Da questo momento, se chi sta richiedendo la rotta /congresso/new
non ha i requisiti minimi, verrà automaticamente sbalzato nella pagina di login.