# 12.9 Lezione 9 --- Creare una rete tra due macchine virtuali

In questa attività si realizza una piccola rete con due VM Debian. Le
macchine potranno comunicare tra loro, accedere a Internet e, nella
lezione successiva, essere raggiunte da altri computer. Ogni VM usa una
sola scheda di rete in modalità **Bridged Adapter**: VirtualBox la collega
direttamente alla rete fisica tramite l'interfaccia dell'host, e la VM si
comporta come un computer distinto della rete locale.

Gli indirizzi IP vengono assegnati automaticamente dal router (DHCP): non
sono noti in anticipo e vanno letti sulle VM.

## Topologia

``` mermaid
flowchart LR
    I[Internet] --- G[Router della rete locale]
    G --- H[Computer fisico<br>host]
    G --- C[Debian-Client<br>Bridged]
    G --- S[Debian-Server<br>Bridged]
```

Le due VM e il computer fisico appartengono alla stessa rete locale, ma
hanno indirizzi IP e indirizzi MAC distinti.

## Configurazione della scheda in VirtualBox

Creare o utilizzare due VM chiamate `Debian-Client` e `Debian-Server`.
Con le VM spente, per ciascuna aprire:

``` text
Impostazioni
→ Rete
→ Scheda 1
→ Abilitata → Connessa a: Bridged Adapter
→ Nome: interfaccia di rete dell'host in uso (Ethernet o Wi-Fi)
```

Selezionare l'interfaccia che l'host usa realmente per la rete. Se le VM
sono state clonate, nelle opzioni avanzate della scheda scegliere
`Genera nuovi indirizzi MAC per tutte le schede di rete`, perché due
macchine con lo stesso MAC creano conflitti. Avviare entrambe le VM.

> **Nota:** alcune reti (scolastiche o Wi-Fi pubbliche) possono bloccare
> più dispositivi sulla stessa porta o isolare i client. Se la VM non
> ottiene un indirizzo, chiedere al docente.

## Attività 1 --- Individuare gli indirizzi

Su ciascuna VM eseguire:

``` bash
ip -br addr
ip route
```

Annotare:

``` text
Nome dell'interfaccia:
Indirizzo IP della VM:
Gateway (default via):
```

L'indirizzo e il gateway devono appartenere alla stessa rete dell'host. Su
Windows, confrontare con `ipconfig` eseguito sull'host.

## Attività 2 --- Verificare la rete e l'accesso a Internet

Su ciascuna VM provare il gateway, un indirizzo Internet e un nome DNS:

``` bash
ping -c 4 INDIRIZZO_GATEWAY
ping -c 4 8.8.8.8
ping -c 4 deb.debian.org
```

Sostituire `INDIRIZZO_GATEWAY` con l'indirizzo trovato in `ip route`. Il
primo test verifica la rete locale, il secondo l'accesso a Internet e il
terzo anche la risoluzione dei nomi DNS.

## Attività 3 --- Verificare la comunicazione tra le VM

Dal client raggiungere il server, usando l'indirizzo annotato nell'Attività 1:

``` bash
ping -c 4 IP_DEL_SERVER
```

Dal server raggiungere il client:

``` bash
ping -c 4 IP_DEL_CLIENT
```

Provare anche a raggiungere l'host, usando l'indirizzo mostrato da
`ipconfig` (Windows) o `ip addr show` (Linux):

``` bash
ping -c 4 IP_DELL_HOST
```

Annotare gli esiti. Se un ping non riceve risposta, verificare gli
indirizzi e la rete scelta in VirtualBox; firewall (per esempio quello di
Windows sull'host) o la rete stessa possono bloccare ICMP anche se il
collegamento funziona.

## Attività 4 --- Riepilogare la rete

Completare la tabella:

| VM | Indirizzo IP | Gateway | Ping all'altra VM | Ping a 8.8.8.8 | Ping a deb.debian.org |
| --- | --- | --- | --- | --- | --- |
| Debian-Client | | | | | |
| Debian-Server | | | | | |

Disegnare la topologia della propria rete, indicando il router, l'host e
le due VM con i rispettivi indirizzi.

### Domande

1. Quale funzione svolge la modalità Bridged Adapter?
2. Perché le due VM hanno indirizzi IP diversi ma appartengono alla stessa
   rete?
3. Chi assegna gli indirizzi IP alle VM?
4. Quale indirizzo è il gateway e a che cosa serve?
5. Perché con Bridged le VM possono essere raggiunte anche da altri
   computer della rete, mentre con NAT no?
6. Quali rischi comporta collegare una VM direttamente alla rete locale?

------------------------------------------------------------------------
