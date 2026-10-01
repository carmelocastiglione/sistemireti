# 12.10 Lezione 10 --- SSH: amministrare Linux da remoto

Una volta costruita una rete tra due VM, possiamo introdurre il concetto
di **amministrazione remota**.

## Obiettivi

Comprendere:

-   il modello client/server;
-   il protocollo SSH;
-   la porta TCP utilizzata da SSH;
-   autenticazione;
-   accesso remoto al terminale.

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

## Attività 2 --- Individuare l'indirizzo del server

``` bash
ip addr
```

Annotare l'indirizzo IP.

## Attività 3 --- Collegarsi dal client

Dal client:

``` bash
ssh nomeutente@192.168.56.20
```

Dopo l'autenticazione, il terminale del client permetterà di eseguire
comandi sul server.

Il modello è:

``` text
Client SSH
     │
     │ rete
     ▼
Server SSH
```

Questo rappresenta già una semplice **architettura client/server**.

------------------------------------------------------------------------
