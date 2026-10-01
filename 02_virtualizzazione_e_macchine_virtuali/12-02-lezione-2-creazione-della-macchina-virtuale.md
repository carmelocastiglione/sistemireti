# 12.2 Lezione 2 --- Creazione della macchina virtuale

## Obiettivi

Lo studente deve imparare a:

-   creare una VM;
-   assegnare CPU e RAM;
-   creare un disco virtuale;
-   comprendere la differenza tra disco fisso e disco virtuale;
-   configurare una scheda di rete virtuale.

## Configurazione proposta

``` text
Sistema operativo: Debian Linux
Architettura: 64 bit
CPU: 2 vCPU
RAM: 2 GB
Disco: 20 GB
Tipo disco: VDI
Allocazione: dinamica
Rete: NAT
Interfaccia grafica: no
```

## Attività 1 --- Creare la VM

In VirtualBox:

``` text
Nuova
```

Impostare:

``` text
Nome: Debian-Lab
Tipo: Linux
Versione: Debian (64-bit)
```

Assegnare:

``` text
RAM: 2048 MB
CPU: 2
```

Creare un nuovo disco virtuale.

Impostare:

``` text
VDI
Allocazione dinamica
20 GB
```

## Attività 2 --- Analizzare la configurazione

Prima di avviare la VM, aprire:

``` text
Impostazioni → Sistema
```

e osservare la quantità di RAM e CPU assegnate.

Poi:

``` text
Impostazioni → Archiviazione
```

e individuare il disco virtuale.

Infine:

``` text
Impostazioni → Rete
```

e osservare la scheda di rete virtuale.

### Domande

1.  Quanta RAM rimane al sistema host?
2.  Il disco virtuale occupa immediatamente 20 GB?
3.  Che cosa significa "allocazione dinamica"?
4.  La scheda di rete della VM è una scheda fisica?
5.  Quale dispositivo reale permette alla VM di comunicare con Internet?

------------------------------------------------------------------------
