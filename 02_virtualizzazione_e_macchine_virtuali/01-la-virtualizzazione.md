# 1. La virtualizzazione

La **virtualizzazione** è una tecnica che permette di creare una
rappresentazione software di una risorsa informatica o di un intero
sistema di elaborazione.

Nel caso di una macchina virtuale, un singolo computer fisico può
ospitare contemporaneamente più computer virtuali indipendenti.

Ogni macchina virtuale può avere:

-   una propria CPU virtuale;
-   una propria quantità di RAM;
-   uno o più dischi virtuali;
-   una o più schede di rete virtuali;
-   un proprio sistema operativo;
-   propri programmi e propri dati.

Il computer fisico che ospita le macchine virtuali viene chiamato
**host**.

La macchina virtuale viene invece chiamata **guest**.

``` mermaid
flowchart TB
    H[Computer fisico - Host]
    C[CPU fisica]
    R[RAM fisica]
    D[Disco fisico]
    N[Scheda di rete fisica]

    H --> C
    H --> R
    H --> D
    H --> N
```

In un ambiente virtualizzato:

``` mermaid
flowchart TB
    H[Computer fisico - Host]

    V[Virtualizzazione / Hypervisor]

    VM1[Macchina virtuale 1]
    VM2[Macchina virtuale 2]

    CPU[CPU fisica]
    RAM[RAM fisica]
    DISK[Disco fisico]
    NET[Rete fisica]

    H --> V
    V --> VM1
    V --> VM2

    V --> CPU
    V --> RAM
    V --> DISK
    V --> NET
```

Il software di virtualizzazione distribuisce le risorse fisiche tra le
diverse macchine virtuali.

## 1.1 Cosa viene virtualizzato?

Una macchina virtuale presenta al sistema operativo un insieme di
dispositivi virtuali.

Tra questi possiamo trovare:

|  Risorsa fisica   | Rappresentazione virtuale               |
|  ---------------- | -------------------------------------
|  CPU              | CPU virtuale                               |
|  RAM              | Memoria virtuale assegnata alla VM         |
|  Disco            | Disco virtuale                             |
|  Scheda di rete   | NIC virtuale                               |
|  USB              | Controller/dispositivi USB virtuali       |
|  BIOS/UEFI        | Firmware virtuale                         |

La VM non possiede fisicamente questi componenti: il software di
virtualizzazione crea un ambiente che permette al sistema operativo
guest di utilizzarli come se fossero presenti.

------------------------------------------------------------------------
