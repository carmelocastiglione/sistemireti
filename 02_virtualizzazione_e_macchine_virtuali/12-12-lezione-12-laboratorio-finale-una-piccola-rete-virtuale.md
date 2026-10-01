# 12.12 Lezione 12 --- Laboratorio finale: una piccola rete virtuale

## Obiettivo

Realizzare un piccolo ambiente virtuale composto da:

-   un client Linux;
-   un server Linux;
-   una rete virtuale;
-   accesso SSH;
-   Web server;
-   verifica della connettività.

## Architettura

``` mermaid
flowchart TB
    PC[Computer fisico]

    VB[VirtualBox]

    PC --> VB

    VB --> C[Debian Client]

    VB --> S[Debian Server]

    C --- R[Rete virtuale]
    S --- R

    C -->|SSH| S
    C -->|HTTP| S
```

## Configurazione prevista

### Client

``` text
Nome: Debian-Client
IP: 192.168.56.10
Ruolo: client
```

### Server

``` text
Nome: Debian-Server
IP: 192.168.56.20
Ruolo: server
```

### Servizi

Sul server:

``` text
SSH
Apache
```

## Fase 1 --- Verifica della rete

Dal client:

``` bash
ping 192.168.56.20
```

## Fase 2 --- Accesso SSH

Dal client:

``` bash
ssh nomeutente@192.168.56.20
```

Verificare di essere effettivamente sul server:

``` bash
hostname
```

## Fase 3 --- Verifica del Web server

Dal client:

``` text
http://192.168.56.20
```

## Fase 4 --- Modifica del server

Collegarsi tramite SSH e modificare la pagina Web.

Tornare sul client e verificare che la modifica sia visibile.

Il percorso complessivo è:

``` text
CLIENT
  │
  │ SSH
  ▼
SERVER
  │
  └── Apache
        │
        ▼
     Pagina Web
```

------------------------------------------------------------------------
