# 11. Le reti virtuali

Una delle caratteristiche più importanti di VirtualBox è la possibilità
di creare reti virtuali.

Le modalità principali che utilizzeremo sono:

-   NAT;
-   Bridged Adapter;
-   Host-only Adapter;
-   Internal Network.

|  Modalità          | Internet                 | Host         | Altre VM |
|  ------------------| -------------------------| -------------| ------------------------|
|  NAT               | Sì                       | tramite NAT  | secondo configurazione |
|  Bridged           | Sì, tramite rete fisica  | Sì           | Sì |
|  Host-only         | No, normalmente          | Sì           | Sì |
|  Internal Network  | No                       | No           | Sì |

La modalità esatta e il comportamento possono dipendere dalla
configurazione della rete.

## 11.1 NAT

Con NAT la VM utilizza VirtualBox come intermediario per accedere alla
rete esterna.

``` mermaid
flowchart LR
    VM[VM]
    V[VirtualBox NAT]
    H[Host]
    I[Internet]

    VM --> V
    V --> H
    H --> I
```

## 11.2 Host-only Adapter

Una rete Host-only permette di creare una rete privata tra host e
macchine virtuali.

``` mermaid
flowchart LR
    H[Host]
    N[Rete Host-only]
    VM1[VM 1]
    VM2[VM 2]

    H --- N
    N --- VM1
    N --- VM2
```

È particolarmente utile per creare laboratori di rete isolati.

## 11.3 Internal Network

Una Internal Network permette di collegare tra loro le VM senza
collegarle direttamente alla rete dell'host.

È utile per simulare reti interne.

------------------------------------------------------------------------
