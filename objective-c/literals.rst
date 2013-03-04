N.B literals supportati da Xcode 4.4 
============================================

literals NSNumber
---------------------

::

  NSNumber *quarantaDue = @42;             // equivalente [NSNumber numberWithInt:42]
  NSNumber *quarantaDueUnsigned = @42U;    // equivalente [NSNumber numberWithUnsignedInt:42U]
  NSNumber *quarantaDueLong = @42L;        // equivalente [NSNumber numberWithLong:42L]
  NSNumber *quarantaDueLongLong = @42LL;   // equivalente [NSNumber numberWithLongLong:42LL]

  // floating point literals.
  NSNumber *piFloat = @3.141592654F;    // equivalente [NSNumber numberWithFloat:3.141592654F]
  NSNumber *piDouble = @3.1415926535;   // equivalente [NSNumber numberWithDouble:3.1415926535]

  // BOOL literals.
  NSNumber *yesNumber = @(YES);           // equivalente [NSNumber numberWithBool:YES]
  NSNumber *noNumber = @(NO);             // equivalente [NSNumber numberWithBool:NO]

  //espressioni
  NSNumber *piGrecoMezzi = @(M_PI / 2);        // [NSNumber numberWithDouble:(M_PI / 2)]

literals collezioni
-----------------------------------------

::

  //array
  NSMutableArray *array = @[oggetto1, oggetto2]; //non mettere nil come carattere di terminazione!

  array[0];//restituisce oggetto1
  array[1]=@"nuovoOggetto";

  //dizionario
  NSMutableDictionary *dictionary = @{
    chiave1 : valore1,
    chiave2 : valore2,
    chiave3 : valore3
  };

  dictionary[chiave1];//restituisce valore1
  dictionary[@"nuovaChiave"]=@"nuovoValore";

