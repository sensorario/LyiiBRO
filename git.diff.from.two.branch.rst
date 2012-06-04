Diff from two branch
--------------------

We want to know whether there are conflict of two branch. How can I do this?

Suppose you are on the master branch and you would like to test if the dev 
branch can be merged without conflict into the master.

**In the master branch**

::

    git merge dev --no-ff --no-commit

After that, you will be able to know if there's a conflict or not.
To return in a normal situation, just abort the merge:

::

    git merge --abort

According to the git documentation:

::

    --ff Do not generate a merge commit if the merge resolved as a fast-forward, only update the branch pointer. This is the default behavior.

    -no-ff Generate a merge commit even if the merge resolved as a fast-forward.

    --commit Perform the merge and commit the result. This option can be used to override --no-commit.

    --no-commit With --no-commit perform the merge but pretend the merge failed and do not autocommit, to give the user a chance to inspect and further tweak the merge result before committing.