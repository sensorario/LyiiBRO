Accedere al repository di un'entità che è chiave esterna con Doctrine2
----------------------------------------------------------------------

Il concetto è semplice. Supponiamo di avere un'entità macchina ed un'entità
gomme. Come possiamo fare per accedere alle gomme, partendo dall'entità 
macchina.

Se ci trovassimo nel controller potremmo usare questa soluzione.

::

    $car = $this->getCar();
    $wheels= $car->getWheels();

Ma se volessimo incapsulare dentro al repositori di Car questa query, potremmo
accedere alle gomme di ogni macchina con questo nuovo metodo da aggiungere al
CarRepository.

::

    /**
    * Get all non flat wheels
    *
    * @return Result
    */
    public function getNonFlatWheels()
    {
        $em = $this->getEntityManager();

        $query = $em
                ->createQuery("
                    SELECT g
                    FROM Acme\DemoBundle\Entity\Car c
                    JOIN c.wheels w
                    WHERE w.flat = :flat
                ")
                ->setParameter('flat', 0);

        return $query->getResult();
    }

Non è il solo metodo per scrivere query, anzi.

::

    public function getNonFlatWheels(Car $car)
    {
        $qb = $this->createQueryBuilder('c')
                ->join('c.wheel', 'w')
                ->where("w.flat = :flat")
                ->setParameters('flat', 0);
        return $qb->getQuery()->getResult();
    }