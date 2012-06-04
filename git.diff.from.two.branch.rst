Verficare se ci sono conflitti tra due branch
---------------------------------------------

Vogliamo sapere se ci sono conflitti tra due branch. Supponiamo di trovarci nel
master e di voler testare se il branch di test può essere mergiato senza 
conflitti all'interno del master.

**Nel branch master**

::

    git merge dev --no-ff --no-commit

Dopo aver fatto questo, saremo in grado di sapere se ci sono conflitti o meno.
Per tornare alla situazione precedente, limitiamoci a fare un abort del merge:

::

    git merge --abort

Come da documentazione di git:

::

    --ff Do not generate a merge commit if the merge resolved as a fast-forward, only update the branch pointer. This is the default behavior.

    -no-ff Generate a merge commit even if the merge resolved as a fast-forward.

    --commit Perform the merge and commit the result. This option can be used to override --no-commit.

    --no-commit With --no-commit perform the merge but pretend the merge failed and do not autocommit, to give the user a chance to inspect and further tweak the merge result before committing.