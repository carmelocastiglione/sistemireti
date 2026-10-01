# 12.6 Lezione 6 --- Snapshot e clonazione

## Obiettivi

Comprendere:

-   che cos'è uno snapshot;
-   quando utilizzarlo;
-   perché è utile durante un laboratorio;
-   differenza tra snapshot e backup;
-   differenza tra snapshot e clone.

## Attività 1 --- Creare una configurazione di riferimento

Portare la macchina virtuale a una situazione "pulita":

``` text
Linux installato
Utente configurato
Rete funzionante
Sistema aggiornato
```

Spegnere la VM.

In VirtualBox creare uno snapshot denominato:

``` text
debian-pulito
```

## Attività 2 --- Modificare la VM

``` bash
mkdir ~/esperimento
touch ~/esperimento/file1.txt
touch ~/esperimento/file2.txt
```

Apportare anche altre modifiche concordate con il docente.

## Attività 3 --- Ripristinare lo snapshot

Spegnere la macchina e ripristinare:

``` text
debian-pulito
```

Riavviare.

Verificare che le modifiche effettuate dopo lo snapshot non siano più
presenti.

### Domanda

Perché lo snapshot è particolarmente utile durante un'attività
didattica?

## Attività 4 --- Clonazione

Creare un clone della macchina virtuale.

Utilizzare nomi come:

``` text
Debian-Client
Debian-Server
```

L'obiettivo è arrivare ad avere **due computer virtuali indipendenti**.

------------------------------------------------------------------------
