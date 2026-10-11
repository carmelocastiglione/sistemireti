# 12.7 Lezione 7 --- La rete della macchina virtuale

## Obiettivi

Comprendere:

-   indirizzo IP;
-   scheda di rete;
-   gateway;
-   DNS;
-   NAT;
-   rete virtuale.

## Attività 1 --- Analizzare la configurazione di rete

Per visualizzare la configurazione di rete, utilizzare il comando:

``` bash
ip addr show
```

Tramite questo comando si possono visualizzare tutte le interfacce di rete e i relativi indirizzi IP.

Individuare l'interfaccia di rete.

Poi:

``` bash
ip route
```

Individuare il gateway predefinito.

## Attività 2 --- Verificare la connettività

``` bash
ping 8.8.8.8
```

Poi:

``` bash
ping google.com
```

Confrontare i due risultati.

### Domanda

Se:

``` bash
ping 8.8.8.8
```

funziona ma:

``` bash
ping google.com
```

non funziona, quale componente potrebbe essere responsabile del
problema?

## Attività 3 --- Analizzare DNS

Visualizzare i DNS configurati utilizzando gli strumenti disponibili nel
sistema.

Ragionare sulla differenza tra:

``` text
indirizzo IP
```

e:

``` text
nome DNS
```

------------------------------------------------------------------------
