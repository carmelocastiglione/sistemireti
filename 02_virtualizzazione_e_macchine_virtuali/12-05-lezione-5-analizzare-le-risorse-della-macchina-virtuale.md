# 12.5 Lezione 5 --- Analizzare le risorse della macchina virtuale

## Obiettivi

Lo studente deve essere in grado di verificare dal sistema Linux:

-   CPU;
-   RAM;
-   disco;
-   filesystem;
-   dispositivi disponibili.

## Attività 1 --- CPU

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

## Attività 2 --- RAM

``` bash
free -h
```

Annotare la quantità di memoria disponibile.

Confrontare il risultato con la quantità configurata in VirtualBox.

## Attività 3 --- Disco

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

## Attività 4 --- Confronto host/guest

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

------------------------------------------------------------------------
