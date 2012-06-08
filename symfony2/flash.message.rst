Flash Messages
--------------

Alcune azioni, potrebbero richiedere di visualizzare un messaggio nella pagina
per comunicarne l'esito all'utente. Per fare degli esempi:

#. quando si cancella un record.
#. quando si modifica un record.
#. quando si crea un nuovo record.
#. e così via ...

Questo genere di cose si chiama "flash message". La prima cosa da fare per
creare un flash message, è salvare il messaggio in sessione. Symfony2 ci
permette di usare setFlash in questo modo.

::

    $this->get('session')->setFlash('notice', 'Record creato con successo');

A questo punto mi basterà andare nel template twig e mettere questo codice 
dove vogliamo visualizzare il messaggio

:: 

    {% if app.session.hasFlash('notice') %}
        <div class="flash-notice">
            {{ app.session.flash('notice') }}
        </div>
    {% endif %}


Se stiamo usando Twig, molto presumibilmente abbiamo un template di base dal
quale estendono tutti gli altri template. Quindi quello è anche il luogo più
adatto ad ospitare il nostro snippet di codice.