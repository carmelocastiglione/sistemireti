# 3. Macchina fisica e macchina virtuale

È importante distinguere i due livelli.

## Host

L'**host** è il computer fisico che fornisce le risorse.

Dispone realmente di:

-   CPU;
-   RAM;
-   disco;
-   scheda di rete;
-   periferiche.

## Guest

Il **guest** è il sistema operativo installato nella macchina virtuale.

Dal suo punto di vista esiste un computer sul quale può essere
installato e utilizzato.

``` mermaid
flowchart TB
    H[Host - computer fisico]

    HV[Hypervisor]

    VM[Guest - macchina virtuale]

    OS[Linux]
    CPU[CPU virtuale]
    RAM[RAM virtuale]
    DISK[Disco virtuale]
    NIC[Scheda di rete virtuale]

    H --> HV
    HV --> VM

    VM --> OS
    VM --> CPU
    VM --> RAM
    VM --> DISK
    VM --> NIC
```

## 3.1 Allocazione delle risorse

Quando creiamo una VM dobbiamo stabilire quante risorse assegnarle.

Per esempio:

``` text
CPU: 2 vCPU
RAM: 2 GB
Disco: 20 GB
```

Questi valori non rappresentano nuovo hardware fisico.

Se il computer possiede 16 GB di RAM e assegniamo 2 GB a una VM, quei 2
GB devono essere ricavati dalla RAM fisica disponibile.

Per questo motivo bisogna evitare di assegnare alle VM più risorse di
quelle che il computer host può gestire.

------------------------------------------------------------------------
