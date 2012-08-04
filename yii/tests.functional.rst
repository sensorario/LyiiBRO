=========================
Functional tests with yii
=========================

--------
Scenario
--------

In this recipe, I'll show you hot to do functional tests with your Yii
applications. We'll follow some steps:

#. clone a yii project;
#. checkout latest yii version (1.1.11);
#. create new yii webapp;
#. download and start selenium;
#. define TEST_BASE_URL constant;
#. run functional tests;

-------------------
Clone a yii project
-------------------

Clone yii project is the easy thing to do. Just go on you /var/www directory and
type this command:

::

    $ git clone git@github.com:yiisoft/yii

------------------------------------
Checkout latest yii version (1.1.11)
------------------------------------

With clone we download master repository. The right thing to do is to checkout 
1.1.11 version (or the latesta one).

::

    $ git checkout 1.1.11

---------------------
Create new yii webapp
---------------------

Noew we have our /var/www/yii folder. I'll create new one for our website, and 
I'll put it on yii directory:

::

    $ mkdir test-yii
    $ mv yii test-yii
    $ cd test-yii
    $ ./yii/framework/yiic webapp .

---------------------------
Download and start selenium
---------------------------

Selenium can be found in http://seleniumhq.org/download/. After download just
run this command:

::

    $ java -jar selenium-server-standalone-2.25.0.jar 

-----------------------------
Define TEST_BASE_URL constant
-----------------------------

::

    /**
     * Change the following URL based on your server configuration
     * Make sure the URL ends with a slash so that we can use relative URLs in test cases
     */
    define('TEST_BASE_URL','http://localhost/test-yii/index-test.php/');

--------------------
Run functional tests
--------------------

::

    $ cd protected/tests
    $ phpunit functional/
