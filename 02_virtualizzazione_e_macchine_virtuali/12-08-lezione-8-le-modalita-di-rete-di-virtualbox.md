# 12.8 Lezione 8 --- Le modalità di rete di VirtualBox

## NAT

Configurazione iniziale:

``` text
VM → VirtualBox → rete dell'host → Internet
```

## Attività 1 --- NAT

La modalità NAT permette alla macchina virtuale di accedere a Internet tramite la rete dell'host, senza che sia direttamente visibile sulla rete locale.

Con la VM configurata come:

``` text
NAT
```

eseguire:

``` bash
ip addr show
```

``` bash
ip route
```

``` bash
ping 8.8.8.8
```

Annotare:

``` text
IP della VM:
Gateway:
Connettività Internet:
```

## Attività 2 --- Host-only Adapter

La modalità Host-only Adapter permette alla macchina virtuale di comunicare solo con l'host e con altre VM configurate sulla stessa rete host-only, senza accesso diretto a Internet.

Modificare:

``` text
Impostazioni
→ Rete
→ Scheda 1
→ Host-only Adapter
```

Avviare nuovamente Linux.

Controllare:

``` bash
ip addr show
```

e:

``` bash
ip route
```

Verificare se Internet è ancora raggiungibile.

## Attività 3 --- Bridged Adapter

La modalità Bridged Adapter permette alla macchina virtuale di essere vista come un dispositivo a sé stante sulla rete locale, con accesso diretto a Internet e agli altri dispositivi della rete.

Modificare:

``` text
Impostazioni
→ Rete
→ Scheda 1
→ Bridged Adapter
```

Avviare nuovamente Linux.

Controllare:

``` bash
ip addr show
```

e:

``` bash
ip route
```

Verificare se Internet è raggiungibile.

## Attività 4 --- Internal Network

La modalità Internal Network permette alla macchina virtuale di comunicare solo con altre VM configurate sulla stessa rete interna, senza accesso diretto a Internet e senza comunicare con l'host.

Modificare:

``` text
Impostazioni
→ Rete
→ Scheda 1
→ Internal Network
```

Avviare nuovamente Linux.

Controllare:

``` bash
ip addr show
```

e:

``` bash
ip route
```

Verificare se Internet è raggiungibile.

## Attività 4 --- Confronto

Completare:

|  Modalità           | Internet   | Host   | Altre VM |
|------------------|------------|--------|----------|
|  NAT             |            |        |          |
|  Host-only       |            |        |          |
|  Bridged         |            |        |          |
|  Internal Network|            |        |          |

------------------------------------------------------------------------
