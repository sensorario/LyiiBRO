=================
Linux Permissions
=================

::

    sudo rm -rf app/cache/*
    sudo rm -rf app/logs/*
    sudo setfacl -R -m u:www-data:rwX -m u:abdemo:rwX app/cache app/logs
    sudo setfacl -dR -m u:www-data:rwx -m u:abdemo:rwx app/cache app/logs

