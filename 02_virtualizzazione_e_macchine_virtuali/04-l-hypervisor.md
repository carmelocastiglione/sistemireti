# 4. L'hypervisor

Il software responsabile della gestione delle macchine virtuali viene
chiamato **hypervisor**.

L'hypervisor si occupa di:

-   creare e gestire le VM;
-   assegnare CPU e RAM;
-   gestire i dischi virtuali;
-   gestire le schede di rete virtuali;
-   controllare l'esecuzione delle VM;
-   fornire un livello di isolamento tra le macchine virtuali.

## 4.1 Hypervisor di tipo 1

Un hypervisor di tipo 1, detto anche **bare metal**, viene eseguito
direttamente sull'hardware.

``` mermaid
flowchart TB
    H[Hardware fisico]
    HV[Hypervisor tipo 1]
    VM1[VM 1]
    VM2[VM 2]
    VM3[VM 3]

    H --> HV
    HV --> VM1
    HV --> VM2
    HV --> VM3
```

Questa soluzione è tipica di molti ambienti server e data center.

## 4.2 Hypervisor di tipo 2

Un hypervisor di tipo 2 viene eseguito sopra un normale sistema
operativo.

``` mermaid
flowchart TB
    HW[Hardware]
    HOST[Windows / Linux / macOS]
    HV[VirtualBox]
    VM1[VM 1]
    VM2[VM 2]

    HW --> HOST
    HOST --> HV
    HV --> VM1
    HV --> VM2
```

**VirtualBox** viene utilizzato in questo modo.

Il computer dispone quindi di un sistema operativo principale,
all'interno del quale viene eseguito VirtualBox, che a sua volta esegue
le macchine virtuali.

------------------------------------------------------------------------
