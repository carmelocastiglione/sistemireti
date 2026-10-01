# 6. Creazione della macchina virtuale

Per il laboratorio utilizzeremo una distribuzione Linux leggera e senza
interfaccia grafica.

Una configurazione indicativa può essere:

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

La configurazione può essere adattata alle caratteristiche dei computer
del laboratorio.

## 6.1 Disco virtuale

Il disco virtuale viene normalmente rappresentato da un file presente
sul computer host.

Possiamo quindi avere:

``` text
Computer fisico
└── Disco fisico
    └── File del disco virtuale
        └── Sistema Linux della VM
```

Un disco virtuale con dimensione massima di 20 GB non significa
necessariamente che il file occupi immediatamente 20 GB sul computer
host.

Con l'allocazione dinamica, il file può crescere man mano che il sistema
guest utilizza spazio.

------------------------------------------------------------------------
