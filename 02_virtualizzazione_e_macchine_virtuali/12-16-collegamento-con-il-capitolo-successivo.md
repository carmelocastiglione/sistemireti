# 12.16 Collegamento con il capitolo successivo

Al termine di questo capitolo lo studente avrà costruito un ambiente
Linux virtualizzato che verrà utilizzato anche nelle attività
successive.

``` mermaid
flowchart TB
    C1[Capitolo 1<br>Il sistema di elaborazione]
    C2[Capitolo 2<br>Virtualizzazione]
    V[VirtualBox]
    L[VM Linux]
    F[Filesystem]
    U[Utenti e permessi]
    P[Processi]
    S[Servizi]
    N[Rete]

    C1 --> C2
    C2 --> V
    V --> L
    L --> F
    L --> U
    L --> P
    L --> S
    L --> N
```

Il percorso didattico complessivo diventa:

``` text
TEORIA
Sistema di elaborazione
        ↓
Virtualizzazione
        ↓
LABORATORIO
Creazione VM
        ↓
Installazione Linux
        ↓
Terminale
        ↓
Filesystem
        ↓
Utenti e permessi
        ↓
Processi e servizi
        ↓
Rete
        ↓
SSH
        ↓
Web server
        ↓
Client / Server
        ↓
LABORATORIO FINALE
Piccola infrastruttura di rete
```

VirtualBox non viene quindi trattato come un argomento isolato, ma
diventa l'ambiente di laboratorio che accompagnerà il successivo
percorso di Sistemi e Reti.
