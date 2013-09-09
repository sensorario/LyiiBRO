Creare un database sqlite3, una tabella e qualche record
--------------------------------------------------------

Questo codice serve solo da esempio ed è volutamente banale. Iniziamo con un semplice
codice che ci permette di creare un database sqlite3. Il database appena create andrà a
finire nella nostra home.

::

    $ sqilite3 spesa.sqlite
    -bash: sqilite3: command not found
    MacBook-di-Simone-Gentili:~ simonegentili$ sqlite3 spesa.sqlite
    SQLite version 3.7.7 2011-06-25 16:35:41
    Enter ".help" for instructions
    Enter SQL statements terminated with a ";"
    
Come creare una tabella

::
    
    sqlite> create table spesa(id integer primary key, nome varchar(250), prezzo integer);

Inserire un po' di dati.

::

    sqlite> insert into spesa (nome,prezzo) values ('Broccoli', 22.4);
    sqlite> insert into spesa (nome,prezzo) values ('Patate', 213.4);
    sqlite> insert into spesa (nome,prezzo) values ('Acqua', 1.4);

Fare una semplice select
    
::

    sqlite> select * from spesa;
    1|Broccoli|22.4
    2|Patate|213.4
    3|Acqua|1.4
    
Uscire dal programma:

::

	sqlite> .quit

