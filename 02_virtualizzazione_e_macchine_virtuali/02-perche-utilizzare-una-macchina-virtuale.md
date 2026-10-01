# 2. Perché utilizzare una macchina virtuale?

Le macchine virtuali sono utilizzate in molti contesti differenti.

## 2.1 Sperimentazione

Una macchina virtuale permette di installare un sistema operativo e
sperimentare liberamente senza modificare direttamente il sistema
operativo principale.

Per esempio, possiamo:

-   installare Linux su un computer Windows;
-   provare configurazioni di rete;
-   installare servizi;
-   modificare file di configurazione;
-   effettuare esperimenti;
-   simulare una rete composta da più computer.

## 2.2 Isolamento

La macchina virtuale è separata dal sistema host.

Questo isolamento non significa che una VM sia automaticamente sicura in
qualsiasi situazione, ma permette di creare un ambiente controllato per
le attività didattiche.

## 2.3 Simulare una rete reale

Possiamo creare più macchine virtuali sullo stesso computer.

Per esempio:

``` text
Debian-Client
Debian-Server
Debian-Router
```

e collegarle tramite reti virtuali.

In questo modo un singolo computer fisico può simulare una piccola
infrastruttura di rete.

## 2.4 Eseguire sistemi operativi differenti

Un computer Windows può ospitare una VM Linux.

Analogamente, un computer Linux può ospitare una VM Windows o altri
sistemi operativi compatibili.

------------------------------------------------------------------------
