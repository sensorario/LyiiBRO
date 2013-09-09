Literals (da Xcode 4.4)
=======================

literals NSNumber
-----------------

::

    /* [NSNumber numberWithInt:42] */
    NSNumber * quarantaDue = @42;

::

    /* [NSNumber numberWithUnsignedInt:42U] */
    NSNumber * quarantaDueUnsigned = @42U;

::

    /* [NSNumber numberWithLong:42L] */
    NSNumber * quarantaDueLong = @42L;

::

    /* [NSNumber numberWithLongLong:42LL] */
    NSNumber * quarantaDueLongLong = @42LL;

Floating point literals
-----------------------

::

    /* [NSNumber numberWithFloat:3.141592654F] */
    NSNumber * piFloat = @3.141592654F;

::

    /* [NSNumber numberWithDouble:3.1415926535] */
    NSNumber * piDouble = @3.1415926535;

BOOL literals
-------------
    
::

    /* equivalente [NSNumber numberWithBool:YES] */
    NSNumber * yesNumber = @(YES);
    
::

    /* equivalente [NSNumber numberWithBool:NO] */
    NSNumber * noNumber = @(NO);

Espressioni
-----------

::

    /* [NSNumber numberWithDouble:(M_PI / 2)] */
    NSNumber * piGrecoMezzi = @(M_PI / 2);

literals collezioni
-------------------

Pre creare un array non è necessario aggiungere nil come ultimo elemento.

::

  NSMutableArray * array = @[oggetto1, oggetto2];

  array[0]; /* restituisce oggetto1 */
  array[1] = @"nuovoOggetto";

  /* dizionario */
  NSMutableDictionary * dictionary = @{
    chiave1 : valore1,
    chiave2 : valore2,
    chiave3 : valore3
  };

  dictionary[chiave1]; /* restituisce valore1 */
  dictionary[@"nuovaChiave"] = @"nuovoValore";
