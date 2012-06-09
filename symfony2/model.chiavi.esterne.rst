=========================
Creare una chiave esterna
=========================

--------
Premessa
--------

Nel database di Accreditamenti abbiamo due grandi entità. Una è Congresso e
l'altra si chiama Accreditamento. Queste due entità sono legate tra loro. In 
particolare un congresso può avere molti accreditamenti, ed un accreditamento
appartiene ad un solo congresso.

---------------------------------------
Cosa fare per relazionare le due entità
---------------------------------------

Per relazionare le due entità dovremo seguire una serie di passaggi.

#. Modificare l'entità Accreditamento
#. Modificare l'entità Congresso
#. Completare le entità
#. Creare la nuova migration

----------------------------------
Modificare l'entità Accreditamento
----------------------------------

Vanno caricate le annotation:

::

    use Doctrine\ORM\Mapping\ManyToOne;
    use Doctrine\ORM\Mapping\JoinColumn;

e collegate le entità

::
    
    /**
     * @ManyToOne(targetEntity="Congresso", inversedBy="accreditamenti")
     * @JoinColumn(name="congresso_id", referencedColumnName="id")
     */
    private $congresso;

-----------------------------
Modificare l'entità Congresso
-----------------------------

Va caricata la nuova annotation

::

    use Doctrine\ORM\Mapping\OneToMany;

e collegate le due entità

::

    /**
     * @OneToMany(targetEntity="Accreditamento", mappedBy="congresso")
     */
    private $accreditamenti;

--------------------
Completare le entità
--------------------

Abbiamo aggiunto dei campi, ma mancano ancora i getter, i setter, ... ma
sopratutto __toString. Quando visualizzeremo un form per gli Accreditamenti
il campo congresso_id generato, mostrerà automaticamente una select con tutti i
congressi inseriti. Ma per funzionare correttamente, Congresso necessita di un 
metodo __toString.

-------------------------
Creare la nuova migration
-------------------------

Dopo aver modificato le due entità, possiamo lanciare la migration.

::

    $ php app/console doctrine:migrations:diff
    $ php app/console doctrine:migrations:migrate

A questo punto il database sarà allineato alle entitrà.