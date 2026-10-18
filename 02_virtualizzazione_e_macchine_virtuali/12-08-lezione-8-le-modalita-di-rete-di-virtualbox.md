# 12.8 Lezione 8 --- Le modalità di rete di VirtualBox

## Prima dei test

In questa lezione si confronta la connettività della macchina virtuale (VM) nelle diverse modalità di rete. Per ogni modalità annotare l'indirizzo IP, il gateway e l'esito dei test. Il comando `ping` invia richieste ICMP per verificare se un dispositivo risponde; un ping senza risposta non dimostra sempre che la rete sia interrotta, perché firewall o reti possono bloccare ICMP.

Per individuare l'interfaccia di rete, l'indirizzo IP e il gateway:

``` bash
ip addr show
ip route
```

Nell'output di `ip addr show`, cercare l'interfaccia attiva e il suo indirizzo IPv4. In `ip route`, la riga che inizia con `default via` indica il gateway predefinito, se presente.

Usare i test adatti alla modalità configurata:

``` bash
ping -c 4 INDIRIZZO_GATEWAY
ping -c 4 8.8.8.8
ping -c 4 deb.debian.org
```

Sostituire `INDIRIZZO_GATEWAY` con l'indirizzo trovato in `ip route`. Il primo test controlla il collegamento al gateway, il secondo la connettività verso un indirizzo Internet e il terzo anche la risoluzione dei nomi DNS. Non eseguire il test del gateway se non compare una rotta predefinita.

Per verificare il collegamento con l'host o con una seconda VM, usare anche:

``` bash
ping -c 4 IP_DELL_HOST
ping -c 4 IP_DELLA_SECONDA_VM
```

Sostituire i segnaposto con gli indirizzi effettivi. Su Windows, l'host mostra i propri indirizzi con `ipconfig`; su Linux, usare `ip addr show`. Il test tra VM richiede che la seconda macchina sia accesa e collegata alla stessa rete appropriata.

## Attività 1 --- NAT

La modalità NAT permette alla VM di accedere a Internet tramite la rete dell'host, senza essere direttamente raggiungibile dagli altri dispositivi della rete locale.

Configurare la scheda di rete della VM su `NAT`, avviare Linux e visualizzare IP e rotte:

``` bash
ip addr show
ip route
```

Con la configurazione NAT predefinita di VirtualBox, il gateway è normalmente `10.0.2.2`. Eseguire i test adatti descritti in "Prima dei test" e provare anche:

``` bash
ping -c 4 10.0.2.2
```

Annotare:

``` text
IP della VM:
Gateway:
Ping al gateway:
Ping a 8.8.8.8:
Ping a deb.debian.org:
```

## Attività 2 --- Host-only Adapter

La modalità Host-only Adapter permette alla VM di comunicare con l'host e con altre VM sulla stessa rete host-only. Da sola, normalmente non fornisce accesso a Internet.

In VirtualBox modificare la scheda:

``` text
Impostazioni
→ Rete
→ Scheda 1
→ Host-only Adapter
```

Avviare Linux, controllare IP e rotte ed eseguire i test adatti descritti in "Prima dei test". Ricavare l'IP host-only dell'host con `ipconfig` (Windows) o `ip addr show` (Linux) e provare a raggiungerlo. Se è
disponibile una seconda VM collegata alla stessa rete host-only, provare anche a raggiungere il suo indirizzo.

Annotare gli esiti e verificare se compare una rotta predefinita e se Internet è raggiungibile.

## Attività 3 --- Bridged Adapter

La modalità Bridged Adapter collega la VM alla rete fisica tramite l'interfaccia di rete dell'host. La VM può ottenere un indirizzo dal router e comportarsi come un dispositivo distinto sulla rete locale.

In VirtualBox modificare la scheda:

``` text
Impostazioni
→ Rete
→ Scheda 1
→ Bridged Adapter
```

Selezionare l'interfaccia di rete dell'host, avviare Linux e controllare IP e rotte. Eseguire i test adatti descritti in "Prima dei test"; provare inoltre a raggiungere l'host e, se disponibile, una seconda VM sulla rete locale.

Annotare gli esiti e confrontare l'indirizzo della VM con quello dell'host: dovrebbero appartenere alla stessa rete locale, pur essendo indirizzi distinti. L'accesso può dipendere dalla rete e dalle sue regole, per esempio quelle del Wi-Fi o del router.

## Attività 4 --- Internal Network

La modalità Internal Network permette alla VM di comunicare con altre VM collegate alla stessa rete interna. Non dà accesso all'host o a Internet. Le VM devono usare lo stesso nome di rete interna; normalmente non è disponibile un server DHCP, quindi si assegnano indirizzi manualmente.

Collegare due VM alla stessa rete interna, per esempio chiamata `laboratorio`, e avviarle. In ciascuna VM individuare il nome dell'interfaccia con `ip link` e assegnare un indirizzo diverso nella stessa rete. Sostituire `enp0s3` con il nome effettivo dell'interfaccia:

Nella prima VM:

``` bash
sudo ip address add 192.168.100.1/24 dev enp0s3
```

Nella seconda VM:

``` bash
sudo ip address add 192.168.100.2/24 dev enp0s3
```

Questi indirizzi sono temporanei e si perdono al riavvio. Controllare l'indirizzo con `ip addr show`, poi dalla prima VM eseguire:

``` bash
ping -c 4 192.168.100.2
```

Ripetere il test in direzione opposta, usando `192.168.100.1`. Provare anche il ping verso `8.8.8.8` e verso l'host: normalmente non rispondono, perché la rete interna è isolata. Se il ping tra le VM fallisce, controllare che siano collegate alla stessa rete interna, che gli indirizzi siano corretti e che il firewall non blocchi ICMP.

## Attività 5 --- Confronto

Completare la tabella usando i risultati osservati. Per i test verso host e altre VM, considerare l'eventuale blocco delle richieste ICMP da parte dei firewall.

| Modalità | Gateway raggiungibile | Internet (IP) | DNS | Host raggiungibile | Altre VM raggiungibili |
| --- | --- | --- | --- | --- | --- |
| NAT | | | | | |
| Host-only | | | | | |
| Bridged | | | | | |
| Internal Network | | | | | |

### Risultati attesi

Gli esiti sono indicativi: possono cambiare in base alla configurazione di VirtualBox, del router e dei firewall.

| Modalità | Gateway e Internet | Comunicazione con l'host | Comunicazione tra VM |
| --- | --- | --- | --- |
| NAT | In genere sì, tramite il gateway virtuale | In genere non direttamente | Non tra VM in NAT separate |
| Host-only | In genere senza accesso a Internet; il gateway dipende dalla configurazione | Sì, se gli indirizzi appartengono alla rete host-only | Sì, sulla stessa rete host-only |
| Bridged | In genere sì, se la rete fisica lo consente | Sì, se le regole di rete e firewall lo consentono | Sì, se la rete lo consente |
| Internal Network | No, salvo servizi configurati appositamente | No | Sì, se le VM condividono la rete e hanno indirizzi compatibili |

Rispondere:

1. Quale differenza c'è tra raggiungere `8.8.8.8` e raggiungere
   `deb.debian.org`?
2. In quale modalità la VM può comunicare con l'host senza essere
   direttamente esposta alla rete fisica?
3. Perché in Internal Network è stato necessario assegnare manualmente
   gli indirizzi IP?
4. Un ping senza risposta è sufficiente per concludere che un dispositivo
   sia spento o irraggiungibile? Perché?

------------------------------------------------------------------------
