How to properly rename a directory
----------------------------------

In a Git repository, we can rename a directory in a git way? It should work to 
copy the directory to be renamed to a new directory with desired name, and 
delete the old directory, and git add, git commit and push everything. But is 
this the best way? I do not think.

The correct way is:

::

    git mv <old-name> <new-name>