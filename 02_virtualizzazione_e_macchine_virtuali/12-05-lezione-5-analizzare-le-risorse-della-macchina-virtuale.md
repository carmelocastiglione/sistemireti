# 12.5 Lezione 5 --- Analizzare le risorse della macchina virtuale

## Obiettivi

Lo studente deve essere in grado di verificare dal sistema Linux:

-   CPU;
-   RAM;
-   disco;
-   filesystem;
-   dispositivi disponibili.

## Attività 1 --- Sistema Operativo installato

Per verificare il sistema operativo installato, utilizzare il comando:

``` bash
uname -a
```

## Attività 2 --- CPU

Il comando `lscpu` mostra informazioni dettagliate sulla CPU del sistema.

``` bash
lscpu
```

Individuare:

``` text
CPU(s)
Model name
Architecture
Core(s) per socket
Thread(s) per core
```

### Domanda

> Perché Linux vede una CPU virtuale anche se il computer possiede una
> CPU fisica?

## Attività 3 --- RAM

``` bash
free -h
```

Annotare la quantità di memoria disponibile.

Confrontare il risultato con la quantità configurata in VirtualBox.

## Attività 4 --- Disco

``` bash
lsblk
```

e:

``` bash
df -h
```

Confrontare i due risultati.

Distinguere:

-   dispositivo di memoria;
-   partizione;
-   filesystem;
-   spazio utilizzato;
-   spazio disponibile.

## Attività 5 --- Confronto host/guest

|  Risorsa               | Computer fisico   | VM |
|----------------------|-----------------|----|
|  CPU                  |                 |    |
|  RAM                  |                 |    |
|  Disco                |                 |    |
|  Sistema operativo    |                 |    |

### Domanda finale

Spiegare con parole proprie perché la VM può essere considerata un
**computer virtuale completo**, pur funzionando all'interno di un altro
computer.

## Riepilogo dei comandi principali

| Comando | Funzione |
| --- | --- |
| `lscpu` | Mostra informazioni dettagliate sulla CPU e sull'architettura del sistema. |
| `free -h` | Mostra la quantità di RAM totale, usata e disponibile, in formato leggibile. |
| `lsblk` | Elenca i dispositivi di blocco, le partizioni e i dischi presenti nel sistema. |
| `df -h` | Mostra lo spazio totale e disponibile dei filesystem montati. |
| `uname -a` | Fornisce informazioni generali sul kernel e sul sistema operativo. |

## Obiettivo del capitolo

Alla fine di questa lezione lo studente deve essere in grado di analizzare le risorse principali di una macchina virtuale e confrontarle con quelle del computer host, riconoscendo il rapporto tra hardware virtualizzato e risorse fisiche disponibili.

------------------------------------------------------------------------
