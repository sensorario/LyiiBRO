================================
Check roles of a particular user
================================

--------
Scenario
--------

Suppose to need to know if a user has a particular role:

---------------------------------------
Here the snippet of code
---------------------------------------

::

    Yii::app()->authManager->checkAccess($roleName, $userId)
