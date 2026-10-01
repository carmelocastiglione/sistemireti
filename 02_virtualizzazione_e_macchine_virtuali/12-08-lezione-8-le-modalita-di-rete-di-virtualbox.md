# 12.8 Lezione 8 --- Le modalità di rete di VirtualBox

## NAT

Configurazione iniziale:

``` text
VM → VirtualBox → rete dell'host → Internet
```

## Attività 1 --- NAT

Con la VM configurata come:

``` text
NAT
```

eseguire:

``` bash
ip addr
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
ip addr
```

e:

``` bash
ip route
```

Verificare se Internet è ancora raggiungibile.

## Attività 3 --- Confronto

Completare:

|  Modalità           | Internet   | Host   | Altre VM |
|------------------|------------|--------|----------|
|  NAT             |            |        |          |
|  Host-only       |            |        |          |
|  Bridged         |            |        |          |
|  Internal Network|            |        |          |

------------------------------------------------------------------------
