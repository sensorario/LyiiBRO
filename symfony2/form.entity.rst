===========
Form Entity
===========

We have two entities. Task entity and Project Entity. When we create new tasks
we need to choose the entity. Also, we want entities ordered by name.

First of all we need to use the repository of our entity.

::

    use Billing\ProjectBundle\Entity\ProjectRepository;

Second, we need to add to the build form "query_builder" option to create our
own queryBuilder.

::

    public function buildForm(FormBuilder $builder, array $options)
    {
        $builder->add('project', 'entity', array(
                    'class' => 'BillingProjectBundle:Project',
                    'query_builder' => function(ProjectRepository $er) {
                        return $er->createQueryBuilder('p')
                                ->orderBy('p.name');
                    }
                ))
        ;
    }