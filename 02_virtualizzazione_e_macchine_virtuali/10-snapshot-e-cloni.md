# 10. Snapshot e cloni

## 10.1 Snapshot

Uno snapshot permette di memorizzare lo stato di una macchina virtuale
in un determinato momento.

Per esempio, possiamo creare:

``` text
debian-pulito
```

dopo aver completato l'installazione e la configurazione iniziale.

Successivamente possiamo effettuare esperimenti e, se necessario,
ritornare allo stato precedente.

### Attenzione

Uno snapshot non deve essere considerato automaticamente un backup.

Uno snapshot dipende dalla macchina virtuale e dalla sua infrastruttura
di virtualizzazione.

## 10.2 Clonazione

Un clone permette di creare una nuova VM a partire da una macchina
esistente.

Questo è particolarmente utile per creare rapidamente:

``` text
Debian-Client
Debian-Server
```

partendo dalla stessa installazione di base.

------------------------------------------------------------------------
