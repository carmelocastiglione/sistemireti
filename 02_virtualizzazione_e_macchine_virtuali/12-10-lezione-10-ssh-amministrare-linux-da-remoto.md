# 12.10 Lezione 10 --- SSH: amministrare Linux da remoto

Una volta costruita una rete tra due VM, possiamo introdurre il concetto
di **amministrazione remota**.

## Obiettivi

Comprendere:

-   il modello client/server;
-   il protocollo SSH;
-   la porta TCP utilizzata da SSH;
-   autenticazione;
-   accesso remoto al terminale;
-   creazione di un utente che possa accedere al server.

Si usa la rete costruita nella lezione 9: server e client sono due VM con
scheda Bridged Adapter, quindi appartengono alla rete locale e ricevono
l'indirizzo dal router. Negli esempi `IP_DEL_SERVER` indica l'indirizzo del
server annotato nella lezione 9; va sostituito con il valore reale.

## Attività 1 --- Installare il server SSH

Sul server:

``` bash
sudo apt update
```

``` bash
sudo apt install openssh-server
```

Verificare il servizio:

``` bash
systemctl status ssh
```

Il servizio deve risultare `active (running)`; per uscire dalla
schermata premere `q`. Il server SSH è in ascolto sulla porta TCP 22,
verificabile con:

``` bash
ss -tln
```

## Attività 2 --- Individuare l'indirizzo del server

``` bash
ip -br addr
```

Annotare l'indirizzo IP della scheda di rete. Poiché è assegnato dal
router, può cambiare dopo un riavvio: controllarlo di nuovo prima di ogni
collegamento.

Sul client, verificare che il server sia raggiungibile:

``` bash
ping -c 4 IP_DEL_SERVER
```

## Attività 3 --- Creare un nuovo utente sul server

Per permettere a un'altra persona di accedere, sul server si crea un
account dedicato. Ogni persona dovrebbe avere un proprio utente, senza
condividere le credenziali.

Sul server:

``` bash
sudo adduser ospite
```

Il comando chiede la password del nuovo utente (scelta con cura, perché
sarà usata per l'accesso remoto) e alcune informazioni facoltative, che
si possono lasciare vuote premendo `Invio`. Verificare l'utente:

``` bash
id ospite
```

L'utente `ospite` è un utente normale e non ha privilegi amministrativi:
non va aggiunto al gruppo `sudo`, salvo che sia necessario.

## Attività 4 --- Collegarsi dal client

Dal client:

``` bash
ssh nomeutente@IP_DEL_SERVER
```

Al primo collegamento SSH mostra l'impronta (fingerprint) della chiave
del server e chiede di confermare: rispondere `yes` solo se ci si sta
collegando al server corretto. Poi inserire la password.

Dopo l'autenticazione, il terminale del client permetterà di eseguire
comandi sul server. Per chiudere la connessione:

``` bash
exit
```

## Attività 5 --- Far accedere un altro utente

Un altro studente può ora collegarsi al server con l'account creato. Il
suo computer (o la sua VM, anch'essa in Bridged) deve trovarsi nella
stessa rete locale. Comunicargli l'indirizzo del server e il nome
dell'utente; la password va comunicata di persona o con un canale sicuro,
non scritta in chiaro in chat pubbliche.

Dal computer dell'altro utente, prima verificare che il server risponda:

``` bash
ping -c 4 IP_DEL_SERVER
ssh ospite@IP_DEL_SERVER
```

Da un computer Windows, SSH è disponibile anche da PowerShell con lo
stesso comando. Il server è esposto a tutta la rete locale: usare una
password robusta e, finito l'esercizio, bloccare o eliminare l'account.

Una volta collegato, l'utente verifica la propria identità e la
posizione:

``` bash
whoami
hostname
pwd
```

Sul server, l'amministratore può vedere chi è collegato e le connessioni
SSH attive:

``` bash
who
ss -tn state established '( sport = :22 )'
```

Per interrompere l'accesso di un utente, l'amministratore può bloccare
l'account:

``` bash
sudo passwd -l ospite
```

e riabilitarlo con `sudo passwd -u ospite`. Il blocco impedisce nuovi
accessi con password; le sessioni già aperte non vengono chiuse
automaticamente. Per eliminare l'utente e la sua home directory:

``` bash
sudo deluser --remove-home ospite
```

### Se l'accesso non funziona

-   `Connection timed out` o `No route to host`: controllare indirizzi e
    rete con `ping` e `ip -br addr`; la rete potrebbe isolare i client
    o l'indirizzo del server potrebbe essere cambiato.
-   `Connection refused`: il servizio SSH non è in esecuzione; verificare
    con `systemctl status ssh`.
-   `Permission denied`: nome utente o password errati.

## Attività 6 --- Accesso con chiave (facoltativa)

L'autenticazione con chiave pubblica è più sicura della password. Sul
computer dell'utente che deve accedere:

``` bash
ssh-keygen -t ed25519
ssh-copy-id ospite@IP_DEL_SERVER
```

`ssh-keygen` crea una coppia di chiavi (privata e pubblica); la chiave
privata non va mai condivisa. `ssh-copy-id` copia la chiave pubblica nel
file `~/.ssh/authorized_keys` dell'utente sul server. Il comando richiede
ancora la password dell'utente `ospite`. Provare quindi:

``` bash
ssh ospite@IP_DEL_SERVER
```

Il collegamento non dovrebbe più chiedere la password dell'account
(se si è impostata una passphrase per la chiave, verrà chiesta
quella).

Il modello è:

``` text
Client SSH
     │
     │ rete
     ▼
Server SSH
```

Questo rappresenta già una semplice **architettura client/server**.

### Domande

1.  Su quale porta TCP è in ascolto il server SSH?
2.  Perché conviene creare un utente per ogni persona?
3.  Perché l'utente `ospite` non è stato aggiunto al gruppo `sudo`?
4.  Che cosa indica l'impronta della chiave mostrata al primo accesso?
5.  Quale vantaggio ha l'accesso con chiave rispetto alla password?
------------------------------------------------------------------------
