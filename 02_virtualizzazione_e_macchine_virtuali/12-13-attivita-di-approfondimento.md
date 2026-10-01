# 12.13 Attività di approfondimento

## Attività A --- Due schede di rete

Configurare il server con:

``` text
Scheda 1 → NAT
Scheda 2 → Host-only
```

``` mermaid
flowchart LR
    I[Internet]
    N[NAT]
    S[Debian Server]
    H[Host-only]
    C[Debian Client]

    I --> N
    N --> S
    S --> H
    H --> C
```

Lo studente deve comprendere che il server possiede **due interfacce di
rete**.

## Attività B --- Server raggiungibile da Internet?

Partendo dalla configurazione precedente, discutere:

> Il Web server è raggiungibile direttamente da Internet?

La risposta deve essere motivata analizzando:

-   NAT;
-   indirizzi IP;
-   rete fisica;
-   rete virtuale;
-   routing;
-   porte.

## Attività C --- Cambiare indirizzo IP

Modificare l'indirizzo IP del server.

Verificare cosa accade quando il client continua a utilizzare il vecchio
indirizzo:

``` bash
ping 192.168.56.20
```

e successivamente utilizza quello nuovo.

L'attività serve a evidenziare che **il nome della macchina e
l'indirizzo IP sono concetti distinti**.

------------------------------------------------------------------------
