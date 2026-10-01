# 12.9 Lezione 9 --- Creare una rete tra due macchine virtuali

Ora utilizziamo le conoscenze acquisite per creare una piccola rete
composta da due computer.

## Topologia

``` mermaid
flowchart LR
    C[Debian Client<br>192.168.56.10]
    R[Rete virtuale<br>Host-only]
    S[Debian Server<br>192.168.56.20]

    C --- R
    R --- S
```

Le due VM rappresentano due computer distinti collegati alla stessa
rete.

## Configurazione

Creare:

``` text
Debian-Client
Debian-Server
```

Configurare entrambe utilizzando la stessa rete virtuale.

Assegnare, secondo la configurazione scelta per il laboratorio,
indirizzi appartenenti alla stessa rete, ad esempio:

``` text
Client: 192.168.56.10
Server: 192.168.56.20
```

## Attività 1 --- Verificare gli indirizzi

Sul client:

``` bash
ip addr
```

Sul server:

``` bash
ip addr
```

Controllare che le due macchine appartengano alla stessa rete.

## Attività 2 --- Testare la comunicazione

Dal client:

``` bash
ping 192.168.56.20
```

Dal server:

``` bash
ping 192.168.56.10
```

## Attività 3 --- Disegnare la rete

``` mermaid
flowchart TB
    H[Computer fisico]

    H --> V[VirtualBox]

    V --> C[Debian Client]
    V --> S[Debian Server]

    C --- N[Rete virtuale]
    S --- N
```

### Domande

1.  Qual è il ruolo di VirtualBox?
2.  Le due VM possiedono la stessa scheda di rete?
3.  Le due VM possiedono lo stesso indirizzo IP?
4.  Perché possono comunicare?
5.  Che cosa succederebbe se appartenessero a reti diverse?

------------------------------------------------------------------------
