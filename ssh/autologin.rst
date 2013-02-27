Generazione chiave rsa
-----------------------------------------
ssh-keygen -t rsa
//inserire password per la chiave
//per il percorso di default premere invio (~/.ssh/id_rsa.pub)


autologin su server
-----------------------------------------
cat id_rsa.pub | ssh nomeUtente@indirizzoIpServer 'cat >> ~/.ssh/authorized_keys'

