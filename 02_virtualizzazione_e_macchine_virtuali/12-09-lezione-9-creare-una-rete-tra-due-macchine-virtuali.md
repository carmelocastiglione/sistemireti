# 12.9 Lezione 9 --- Creare una rete tra due macchine virtuali

In questa attività si realizza una piccola rete con due VM Debian. Le
macchine potranno comunicare tra loro e accedere a Internet. Per ottenere
entrambi i risultati, ogni VM userà due schede di rete virtuali:

- una scheda in modalità **NAT**, per accedere a Internet;
- una scheda collegata alla stessa **Internal Network**, per comunicare
  direttamente con l'altra VM.

La modalità NAT da sola non collega tra loro le VM; la rete interna da
sola non fornisce accesso a Internet. L'uso di due schede permette di
combinare le due funzioni.

## Topologia

``` mermaid
flowchart LR
    I[Internet] --- N[VirtualBox NAT]
    N --- C1[Scheda 1<br>Client]
    N --- S1[Scheda 1<br>Server]
    C2[Client<br>Scheda 2] --- R[Rete interna<br>rete-lab]
    R --- S2[Server<br>Scheda 2]
```

Indirizzi della rete interna:

``` text
Client: 192.168.100.10/24
Server: 192.168.100.20/24
```

Gli indirizzi della rete NAT vengono invece assegnati automaticamente da
VirtualBox.

## Configurazione delle schede in VirtualBox

Creare o utilizzare due VM chiamate `Debian-Client` e `Debian-Server`.
Per ciascuna VM, aprire:

``` text
Impostazioni
→ Rete
```

Configurare le schede nello stesso modo su entrambe le VM:

``` text
Scheda 1: abilitata → NAT
Scheda 2: abilitata → Internal Network
Nome della rete interna: rete-lab
```

Il nome della rete interna deve essere identico sulle due VM. Avviare
entrambe le macchine.

## Attività 1 --- Riconoscere le interfacce

Su ciascuna VM eseguire:

``` bash
ip -br addr
ip route
```

Individuare le due interfacce di rete. L'interfaccia NAT dovrebbe avere
un indirizzo assegnato automaticamente e una rotta predefinita verso
Internet. L'interfaccia collegata a `rete-lab` inizialmente potrebbe non
avere un indirizzo IP.

I nomi delle interfacce dipendono dal sistema e dalla configurazione;
negli esempi seguenti `enp0s3` è la scheda NAT e `enp0s8` è la scheda
interna. Verificare i nomi effettivi con `ip -br addr` e sostituirli nei
comandi successivi.

## Attività 2 --- Assegnare gli indirizzi della rete interna

La rete interna non assegna automaticamente gli indirizzi in questa
configurazione. Attivare la seconda interfaccia e assegnare un indirizzo
diverso a ciascuna VM.

Sul client:

``` bash
sudo ip link set enp0s8 up
sudo ip address add 192.168.100.10/24 dev enp0s8
```

Sul server:

``` bash
sudo ip link set enp0s8 up
sudo ip address add 192.168.100.20/24 dev enp0s8
```

Sostituire `enp0s8` con il nome effettivo della scheda collegata alla
rete interna. Questi indirizzi sono temporanei e vengono persi al
riavvio.

Verificare su entrambe le VM:

``` bash
ip -br addr
ip route
```

La rotta predefinita deve continuare a usare la scheda NAT. Non aggiungere
un gateway alla scheda della rete interna.

## Attività 3 --- Verificare la comunicazione tra le VM

Dal client raggiungere il server:

``` bash
ping -c 4 192.168.100.20
```

Dal server raggiungere il client:

``` bash
ping -c 4 192.168.100.10
```

Annotare gli esiti. Se il ping non riceve risposta, verificare che
entrambe le schede siano collegate a `rete-lab`, che gli indirizzi siano
corretti e che il firewall delle VM non blocchi ICMP.

## Attività 4 --- Verificare l'accesso a Internet

Su ciascuna VM controllare le rotte e provare a raggiungere un indirizzo
Internet e un nome DNS:

``` bash
ip route
ping -c 4 8.8.8.8
ping -c 4 deb.debian.org
```

La prima prova verifica la connettività verso un indirizzo IP; la seconda
verifica anche la risoluzione dei nomi DNS. Un ping senza risposta non
dimostra da solo che la rete sia interrotta: firewall o rete potrebbero
bloccare ICMP.

## Attività 5 --- Rappresentare e riepilogare la rete

Completare la tabella:

| VM | IP sulla rete interna | Ping all'altra VM | Ping a 8.8.8.8 | Ping a deb.debian.org |
| --- | --- | --- | --- | --- |
| Debian-Client | 192.168.100.10 | | | |
| Debian-Server | 192.168.100.20 | | | |

Disegnare la topologia indicando entrambe le schede di ciascuna VM:

``` mermaid
flowchart TB
    I[Internet] --- N[NAT]
    N --- C1[Debian Client<br>Scheda NAT]
    N --- S1[Debian Server<br>Scheda NAT]
    C2[Debian Client<br>Scheda interna] --- R[rete-lab]
    R --- S2[Debian Server<br>Scheda interna]
```

### Domande

1. Quale funzione svolge la scheda NAT?
2. Quale funzione svolge la seconda scheda collegata a `rete-lab`?
3. Perché le due VM devono avere indirizzi IP diversi ma appartenere alla
   stessa rete?
4. Quale scheda fornisce la rotta predefinita verso Internet?
5. Che cosa accadrebbe se una VM fosse collegata a una rete interna con
   un nome diverso?

------------------------------------------------------------------------
