# Sistemi e Reti --- Capitolo 2: Virtualizzazione e macchine virtuali

## Introduzione

La virtualizzazione è una delle tecnologie fondamentali per comprendere
il funzionamento dei moderni sistemi informatici e delle infrastrutture
di rete.

Nel capitolo precedente abbiamo analizzato il **sistema di
elaborazione**, osservando come CPU, memoria, dispositivi di memoria,
periferiche e sistema operativo collaborino per permettere a un computer
di eseguire programmi.

In questo capitolo introduciamo un livello ulteriore di astrazione: la
**macchina virtuale**.

Una macchina virtuale permette di simulare, all'interno di un computer
fisico, un altro computer completo dal punto di vista logico. La
macchina virtuale possiede infatti una propria CPU virtuale, memoria
virtuale, disco virtuale, scheda di rete virtuale e sistema operativo.

Per le attività di laboratorio utilizzeremo **VirtualBox**, che si
assume già installato sul computer.

Il laboratorio utilizzerà una distribuzione Linux leggera, senza
interfaccia grafica, in modo da concentrarsi sui concetti di sistema
operativo, amministrazione e rete.

------------------------------------------------------------------------

# 1. La virtualizzazione

La **virtualizzazione** è una tecnica che permette di creare una
rappresentazione software di una risorsa informatica o di un intero
sistema di elaborazione.

Nel caso di una macchina virtuale, un singolo computer fisico può
ospitare contemporaneamente più computer virtuali indipendenti.

Ogni macchina virtuale può avere:

-   una propria CPU virtuale;
-   una propria quantità di RAM;
-   uno o più dischi virtuali;
-   una o più schede di rete virtuali;
-   un proprio sistema operativo;
-   propri programmi e propri dati.

Il computer fisico che ospita le macchine virtuali viene chiamato
**host**.

La macchina virtuale viene invece chiamata **guest**.

``` mermaid
flowchart TB
    H[Computer fisico - Host]
    C[CPU fisica]
    R[RAM fisica]
    D[Disco fisico]
    N[Scheda di rete fisica]

    H --> C
    H --> R
    H --> D
    H --> N
```

In un ambiente virtualizzato:

``` mermaid
flowchart TB
    H[Computer fisico - Host]

    V[Virtualizzazione / Hypervisor]

    VM1[Macchina virtuale 1]
    VM2[Macchina virtuale 2]

    CPU[CPU fisica]
    RAM[RAM fisica]
    DISK[Disco fisico]
    NET[Rete fisica]

    H --> V
    V --> VM1
    V --> VM2

    V --> CPU
    V --> RAM
    V --> DISK
    V --> NET
```

Il software di virtualizzazione distribuisce le risorse fisiche tra le
diverse macchine virtuali.

## 1.1 Cosa viene virtualizzato?

Una macchina virtuale presenta al sistema operativo un insieme di
dispositivi virtuali.

Tra questi possiamo trovare:

  Risorsa fisica   Rappresentazione virtuale
  ---------------- -------------------------------------
  CPU              CPU virtuale
  RAM              Memoria virtuale assegnata alla VM
  Disco            Disco virtuale
  Scheda di rete   NIC virtuale
  USB              Controller/dispositivi USB virtuali
  BIOS/UEFI        Firmware virtuale

La VM non possiede fisicamente questi componenti: il software di
virtualizzazione crea un ambiente che permette al sistema operativo
guest di utilizzarli come se fossero presenti.

------------------------------------------------------------------------

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

# 3. Macchina fisica e macchina virtuale

È importante distinguere i due livelli.

## Host

L'**host** è il computer fisico che fornisce le risorse.

Dispone realmente di:

-   CPU;
-   RAM;
-   disco;
-   scheda di rete;
-   periferiche.

## Guest

Il **guest** è il sistema operativo installato nella macchina virtuale.

Dal suo punto di vista esiste un computer sul quale può essere
installato e utilizzato.

``` mermaid
flowchart TB
    H[Host - computer fisico]

    HV[Hypervisor]

    VM[Guest - macchina virtuale]

    OS[Linux]
    CPU[CPU virtuale]
    RAM[RAM virtuale]
    DISK[Disco virtuale]
    NIC[Scheda di rete virtuale]

    H --> HV
    HV --> VM

    VM --> OS
    VM --> CPU
    VM --> RAM
    VM --> DISK
    VM --> NIC
```

## 3.1 Allocazione delle risorse

Quando creiamo una VM dobbiamo stabilire quante risorse assegnarle.

Per esempio:

``` text
CPU: 2 vCPU
RAM: 2 GB
Disco: 20 GB
```

Questi valori non rappresentano nuovo hardware fisico.

Se il computer possiede 16 GB di RAM e assegniamo 2 GB a una VM, quei 2
GB devono essere ricavati dalla RAM fisica disponibile.

Per questo motivo bisogna evitare di assegnare alle VM più risorse di
quelle che il computer host può gestire.

------------------------------------------------------------------------

# 4. L'hypervisor

Il software responsabile della gestione delle macchine virtuali viene
chiamato **hypervisor**.

L'hypervisor si occupa di:

-   creare e gestire le VM;
-   assegnare CPU e RAM;
-   gestire i dischi virtuali;
-   gestire le schede di rete virtuali;
-   controllare l'esecuzione delle VM;
-   fornire un livello di isolamento tra le macchine virtuali.

## 4.1 Hypervisor di tipo 1

Un hypervisor di tipo 1, detto anche **bare metal**, viene eseguito
direttamente sull'hardware.

``` mermaid
flowchart TB
    H[Hardware fisico]
    HV[Hypervisor tipo 1]
    VM1[VM 1]
    VM2[VM 2]
    VM3[VM 3]

    H --> HV
    HV --> VM1
    HV --> VM2
    HV --> VM3
```

Questa soluzione è tipica di molti ambienti server e data center.

## 4.2 Hypervisor di tipo 2

Un hypervisor di tipo 2 viene eseguito sopra un normale sistema
operativo.

``` mermaid
flowchart TB
    HW[Hardware]
    HOST[Windows / Linux / macOS]
    HV[VirtualBox]
    VM1[VM 1]
    VM2[VM 2]

    HW --> HOST
    HOST --> HV
    HV --> VM1
    HV --> VM2
```

**VirtualBox** viene utilizzato in questo modo.

Il computer dispone quindi di un sistema operativo principale,
all'interno del quale viene eseguito VirtualBox, che a sua volta esegue
le macchine virtuali.

------------------------------------------------------------------------

# 5. VirtualBox

VirtualBox è un software di virtualizzazione che permette di creare e
gestire macchine virtuali.

Nel nostro laboratorio VirtualBox è già installato.

Gli elementi principali da conoscere sono:

-   macchina virtuale;
-   configurazione della VM;
-   disco virtuale;
-   immagine ISO;
-   memoria;
-   CPU;
-   scheda di rete;
-   snapshot;
-   rete virtuale.

## 5.1 L'immagine ISO

Per installare un sistema operativo utilizziamo normalmente un'immagine
**ISO**.

L'ISO è un file che contiene una rappresentazione del contenuto di un
supporto ottico o di un supporto di installazione.

VirtualBox può presentare l'ISO alla macchina virtuale come se fosse un
supporto inserito nel lettore.

------------------------------------------------------------------------

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

# 7. Installazione di Linux

La macchina virtuale viene avviata dall'immagine ISO.

Durante l'installazione vengono configurati:

-   lingua;
-   tastiera;
-   rete;
-   nome della macchina;
-   utenti;
-   password;
-   partizionamento;
-   pacchetti software.

Per il laboratorio è consigliata un'installazione minimale, senza
ambiente desktop.

Il sistema verrà quindi utilizzato principalmente attraverso il
terminale.

## 7.1 Utente root e utente normale

Linux distingue tra utenti normali e utenti con privilegi
amministrativi.

L'utente `root` dispone di privilegi molto elevati.

Un utente normale può utilizzare `sudo` per eseguire singoli comandi con
privilegi amministrativi, quando autorizzato.

Esempio:

``` bash
sudo apt update
```

Questa distinzione sarà approfondita nel capitolo dedicato
all'amministrazione Linux.

------------------------------------------------------------------------

# 8. Configurazione della macchina virtuale

La configurazione di VirtualBox e la configurazione del sistema
operativo guest sono due livelli differenti.

In VirtualBox possiamo configurare:

-   numero di CPU;
-   quantità di RAM;
-   dischi;
-   controller;
-   schede di rete;
-   dispositivi virtuali.

All'interno di Linux possiamo invece configurare:

-   filesystem;
-   utenti;
-   servizi;
-   indirizzi IP;
-   DNS;
-   applicazioni.

È importante non confondere i due livelli.

------------------------------------------------------------------------

# 9. Avvio e gestione della macchina virtuale

Una macchina virtuale può trovarsi in diversi stati.

Tra i principali:

-   spenta;
-   in esecuzione;
-   in pausa;
-   salvata.

Quando possibile, una VM Linux deve essere spenta attraverso il normale
sistema operativo.

Per esempio:

``` bash
sudo shutdown now
```

oppure:

``` bash
sudo poweroff
```

Lo spegnimento forzato deve essere evitato quando non necessario, perché
equivale a interrompere bruscamente l'alimentazione di un computer.

------------------------------------------------------------------------

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

# 11. Le reti virtuali

Una delle caratteristiche più importanti di VirtualBox è la possibilità
di creare reti virtuali.

Le modalità principali che utilizzeremo sono:

-   NAT;
-   Bridged Adapter;
-   Host-only Adapter;
-   Internal Network.

  Modalità           Internet                  Host          Altre VM
  ------------------ ------------------------- ------------- ------------------------
  NAT                Sì                        tramite NAT   secondo configurazione
  Bridged            Sì, tramite rete fisica   Sì            Sì
  Host-only          No, normalmente           Sì            Sì
  Internal Network   No                        No            Sì

La modalità esatta e il comportamento possono dipendere dalla
configurazione della rete.

## 11.1 NAT

Con NAT la VM utilizza VirtualBox come intermediario per accedere alla
rete esterna.

``` mermaid
flowchart LR
    VM[VM]
    V[VirtualBox NAT]
    H[Host]
    I[Internet]

    VM --> V
    V --> H
    H --> I
```

## 11.2 Host-only Adapter

Una rete Host-only permette di creare una rete privata tra host e
macchine virtuali.

``` mermaid
flowchart LR
    H[Host]
    N[Rete Host-only]
    VM1[VM 1]
    VM2[VM 2]

    H --- N
    N --- VM1
    N --- VM2
```

È particolarmente utile per creare laboratori di rete isolati.

## 11.3 Internal Network

Una Internal Network permette di collegare tra loro le VM senza
collegarle direttamente alla rete dell'host.

È utile per simulare reti interne.

------------------------------------------------------------------------

# 12. Laboratorio: VirtualBox e Linux

La parte laboratoriale accompagna progressivamente lo studente dalla
creazione della prima macchina virtuale fino alla realizzazione di un
piccolo ambiente di rete composto da più macchine Linux.

L'obiettivo non è soltanto imparare a utilizzare VirtualBox, ma
comprendere cosa avviene a livello hardware, sistema operativo e rete
quando viene creata una macchina virtuale.

## Percorso delle lezioni

  -----------------------------------------------------------------------
  Lezione                 Argomento               Obiettivo principale
  ----------------------- ----------------------- -----------------------
  1                       Virtualizzazione e      Comprendere il concetto
                          VirtualBox              di macchina virtuale

  2                       Creazione della VM      Creare e configurare
                                                  una macchina virtuale

  3                       Installazione di Linux  Installare un sistema
                                                  Linux minimale

  4                       Primo utilizzo di Linux Familiarizzare con
                                                  terminale e sistema

  5                       Risorse hardware        Analizzare CPU, RAM e
                          virtuali                disco virtuali

  6                       Snapshot e cloni        Salvare e replicare una
                                                  VM

  7                       Rete della macchina     Comprendere NAT e
                          virtuale                configurazione IP

  8                       Reti virtuali           Creare una rete tra più
                          VirtualBox              VM

  9                       Client e server Linux   Realizzare una semplice
                                                  architettura
                                                  client/server

  10                      Laboratorio finale      Integrare
                                                  virtualizzazione, Linux
                                                  e rete
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 12.1 Lezione 1 --- Conoscere l'ambiente di virtualizzazione

## Obiettivi

Al termine della lezione lo studente deve essere in grado di:

-   distinguere macchina fisica e macchina virtuale;
-   distinguere host e guest;
-   spiegare il ruolo dell'hypervisor;
-   riconoscere le principali risorse virtualizzate;
-   utilizzare le principali funzioni di VirtualBox;
-   comprendere il significato di ISO, disco virtuale e snapshot.

## Attività 1 --- Osservare il computer fisico

Prima di creare la macchina virtuale, raccogliere alcune informazioni
sul computer utilizzato.

Su Windows è possibile utilizzare:

``` text
Impostazioni → Sistema → Informazioni
```

oppure:

``` text
Gestione attività → Prestazioni
```

Annotare:

``` text
Processore:
RAM:
Spazio disponibile sul disco:
Sistema operativo:
```

### Domande

1.  Quanti core ha il processore?
2.  Quanta RAM è disponibile?
3.  Quanto spazio libero è presente sul disco?
4.  Qual è il sistema operativo dell'host?
5.  Quali di queste risorse dovranno essere assegnate anche alla
    macchina virtuale?

## Attività 2 --- Esplorare VirtualBox

Avviare VirtualBox e osservare l'interfaccia.

Individuare:

-   elenco delle macchine virtuali;
-   pulsante per creare una nuova VM;
-   impostazioni;
-   avvio;
-   spegnimento;
-   snapshot;
-   configurazione della rete;
-   configurazione dell'archiviazione.

Per ogni elemento, cercare di capire quale componente della macchina
reale viene rappresentato virtualmente.

  VirtualBox       Concetto reale
  ---------------- ----------------------------
  Processori       CPU
  Memoria          RAM
  Disco virtuale   Disco
  Scheda di rete   NIC
  ISO              Supporto di installazione
  USB              Controller/dispositivi USB

### Attività di riflessione

Rispondere:

> Se creo una VM con 2 GB di RAM, quei 2 GB vengono "creati" dal
> computer?

Spiegare la risposta distinguendo tra **risorsa fisica** e **risorsa
virtuale**.

------------------------------------------------------------------------

# 12.2 Lezione 2 --- Creazione della macchina virtuale

## Obiettivi

Lo studente deve imparare a:

-   creare una VM;
-   assegnare CPU e RAM;
-   creare un disco virtuale;
-   comprendere la differenza tra disco fisso e disco virtuale;
-   configurare una scheda di rete virtuale.

## Configurazione proposta

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

## Attività 1 --- Creare la VM

In VirtualBox:

``` text
Nuova
```

Impostare:

``` text
Nome: Debian-Lab
Tipo: Linux
Versione: Debian (64-bit)
```

Assegnare:

``` text
RAM: 2048 MB
CPU: 2
```

Creare un nuovo disco virtuale.

Impostare:

``` text
VDI
Allocazione dinamica
20 GB
```

## Attività 2 --- Analizzare la configurazione

Prima di avviare la VM, aprire:

``` text
Impostazioni → Sistema
```

e osservare la quantità di RAM e CPU assegnate.

Poi:

``` text
Impostazioni → Archiviazione
```

e individuare il disco virtuale.

Infine:

``` text
Impostazioni → Rete
```

e osservare la scheda di rete virtuale.

### Domande

1.  Quanta RAM rimane al sistema host?
2.  Il disco virtuale occupa immediatamente 20 GB?
3.  Che cosa significa "allocazione dinamica"?
4.  La scheda di rete della VM è una scheda fisica?
5.  Quale dispositivo reale permette alla VM di comunicare con Internet?

------------------------------------------------------------------------

# 12.3 Lezione 3 --- Installazione di Linux

## Obiettivi

Installare un sistema Linux minimale e comprendere le principali fasi
dell'installazione.

## Attività 1 --- Utilizzare l'immagine ISO

Utilizzare l'immagine ISO della distribuzione Linux scelta per il
laboratorio.

Configurare VirtualBox affinché la VM possa avviarsi dall'immagine ISO.

## Attività 2 --- Avviare l'installazione

Avviare:

``` text
Debian-Lab
```

e procedere con l'installazione.

Durante l'installazione prestare particolare attenzione a:

-   lingua;
-   tastiera;
-   nome della macchina;
-   rete;
-   utenti;
-   password;
-   partizionamento;
-   software da installare.

Per il laboratorio utilizzare una configurazione minimale.

**Non installare un ambiente desktop**, se l'obiettivo è lavorare
prevalentemente da terminale.

## Attività 3 --- Utente root e utente normale

Durante l'installazione osservare la differenza tra:

``` text
root
```

e un normale utente.

Un utente normale può utilizzare `sudo` per eseguire temporaneamente
operazioni amministrative.

### Domande

1.  Che cos'è `root`?
2.  Perché non è consigliabile utilizzare sempre root?
3.  A cosa serve `sudo`?
4.  Perché un sistema server può essere utilizzato senza interfaccia
    grafica?

------------------------------------------------------------------------

# 12.4 Lezione 4 --- Primo utilizzo del sistema Linux

## Obiettivi

Lo studente deve imparare a:

-   effettuare il login;
-   utilizzare il terminale;
-   eseguire comandi;
-   muoversi nel filesystem;
-   creare file e directory;
-   ottenere informazioni sul sistema.

## Attività 1 --- Login

Effettuare il login con l'utente creato durante l'installazione.

``` bash
whoami
```

Poi:

``` bash
hostname
```

## Attività 2 --- Esplorare il filesystem

``` bash
pwd
```

``` bash
ls
```

``` bash
ls -la
```

``` bash
cd /
```

``` bash
ls
```

Osservare le principali directory:

``` text
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── srv
├── tmp
├── usr
└── var
```

## Attività 3 --- Creare una struttura di laboratorio

``` bash
mkdir ~/laboratorio
```

``` bash
cd ~/laboratorio
```

``` bash
mkdir lezione1
mkdir lezione2
mkdir esercizi
```

Verificare:

``` bash
ls
```

## Attività 4 --- Creare e modificare file

``` bash
touch informazioni.txt
```

``` bash
ls -l
```

Utilizzare:

``` bash
nano informazioni.txt
```

Inserire alcune informazioni sulla macchina.

Successivamente:

``` bash
cat informazioni.txt
```

------------------------------------------------------------------------

# 12.5 Lezione 5 --- Analizzare le risorse della macchina virtuale

## Obiettivi

Lo studente deve essere in grado di verificare dal sistema Linux:

-   CPU;
-   RAM;
-   disco;
-   filesystem;
-   dispositivi disponibili.

## Attività 1 --- CPU

``` bash
lscpu
```

Individuare:

``` text
CPU(s)
Model name
Architecture
Core(s) per socket
Thread(s) per core
```

### Domanda

> Perché Linux vede una CPU virtuale anche se il computer possiede una
> CPU fisica?

## Attività 2 --- RAM

``` bash
free -h
```

Annotare la quantità di memoria disponibile.

Confrontare il risultato con la quantità configurata in VirtualBox.

## Attività 3 --- Disco

``` bash
lsblk
```

e:

``` bash
df -h
```

Confrontare i due risultati.

Distinguere:

-   dispositivo di memoria;
-   partizione;
-   filesystem;
-   spazio utilizzato;
-   spazio disponibile.

## Attività 4 --- Confronto host/guest

  Risorsa               Computer fisico   VM
  ------------------- ----------------- ----
  CPU                                   
  RAM                                   
  Disco                                 
  Sistema operativo                     

### Domanda finale

Spiegare con parole proprie perché la VM può essere considerata un
**computer virtuale completo**, pur funzionando all'interno di un altro
computer.

------------------------------------------------------------------------

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

``` bash
ip addr
```

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

  Modalità           Internet   Host   Altre VM
  ------------------ ---------- ------ ----------
  NAT                                  
  Host-only                            
  Bridged                              
  Internal Network                     

------------------------------------------------------------------------

# 12.9 Lezione 9 --- Creare una rete tra due macchine virtuali

Ora utilizziamo le conoscenze acquisite per creare una piccola rete
composta da due computer.

## Topologia

``` mermaid
flowchart LR
    C[Debian Client<br>192.168.56.10]
    R[Rete virtuale<br>Host-only]
    S[Debian Server<br>192.168.56.20]

    C --- R
    R --- S
```

Le due VM rappresentano due computer distinti collegati alla stessa
rete.

## Configurazione

Creare:

``` text
Debian-Client
Debian-Server
```

Configurare entrambe utilizzando la stessa rete virtuale.

Assegnare, secondo la configurazione scelta per il laboratorio,
indirizzi appartenenti alla stessa rete, ad esempio:

``` text
Client: 192.168.56.10
Server: 192.168.56.20
```

## Attività 1 --- Verificare gli indirizzi

Sul client:

``` bash
ip addr
```

Sul server:

``` bash
ip addr
```

Controllare che le due macchine appartengano alla stessa rete.

## Attività 2 --- Testare la comunicazione

Dal client:

``` bash
ping 192.168.56.20
```

Dal server:

``` bash
ping 192.168.56.10
```

## Attività 3 --- Disegnare la rete

``` mermaid
flowchart TB
    H[Computer fisico]

    H --> V[VirtualBox]

    V --> C[Debian Client]
    V --> S[Debian Server]

    C --- N[Rete virtuale]
    S --- N
```

### Domande

1.  Qual è il ruolo di VirtualBox?
2.  Le due VM possiedono la stessa scheda di rete?
3.  Le due VM possiedono lo stesso indirizzo IP?
4.  Perché possono comunicare?
5.  Che cosa succederebbe se appartenessero a reti diverse?

------------------------------------------------------------------------

# 12.10 Lezione 10 --- SSH: amministrare Linux da remoto

Una volta costruita una rete tra due VM, possiamo introdurre il concetto
di **amministrazione remota**.

## Obiettivi

Comprendere:

-   il modello client/server;
-   il protocollo SSH;
-   la porta TCP utilizzata da SSH;
-   autenticazione;
-   accesso remoto al terminale.

## Attività 1 --- Installare il server SSH

Sul server:

``` bash
sudo apt update
```

``` bash
sudo apt install openssh-server
```

Verificare il servizio:

``` bash
systemctl status ssh
```

## Attività 2 --- Individuare l'indirizzo del server

``` bash
ip addr
```

Annotare l'indirizzo IP.

## Attività 3 --- Collegarsi dal client

Dal client:

``` bash
ssh nomeutente@192.168.56.20
```

Dopo l'autenticazione, il terminale del client permetterà di eseguire
comandi sul server.

Il modello è:

``` text
Client SSH
     │
     │ rete
     ▼
Server SSH
```

Questo rappresenta già una semplice **architettura client/server**.

------------------------------------------------------------------------

# 12.11 Lezione 11 --- Realizzare un semplice server Web

A questo punto la macchina Linux può svolgere il ruolo di **server**.

## Obiettivi

Comprendere:

-   servizio;
-   server;
-   porta;
-   protocollo;
-   client;
-   richiesta e risposta.

## Attività 1 --- Installare un Web server

``` bash
sudo apt update
```

``` bash
sudo apt install apache2
```

Verificare:

``` bash
systemctl status apache2
```

## Attività 2 --- Verificare il server dal client

Dal client aprire un browser e utilizzare:

``` text
http://192.168.56.20
```

La pagina visualizzata proviene dalla macchina virtuale server.

``` mermaid
flowchart LR
    B[Browser<br>Client]
    N[Rete virtuale]
    W[Apache<br>Web Server]

    B --> N
    N --> W
```

## Attività 3 --- Modificare la pagina

Sul server individuare la directory del sito e modificare la pagina
iniziale.

Creare una pagina che riporti, ad esempio:

``` text
SERVER WEB DEL LABORATORIO

Nome macchina:
Indirizzo IP:
Classe:
```

Dal client ricaricare la pagina.

### Domanda

Che cosa è successo quando il browser ha richiesto:

``` text
http://192.168.56.20
```

Ricostruire il percorso:

``` text
Browser
   ↓
indirizzo IP
   ↓
rete virtuale
   ↓
server
   ↓
porta 80
   ↓
Apache
   ↓
pagina HTML
```

------------------------------------------------------------------------

# 12.12 Lezione 12 --- Laboratorio finale: una piccola rete virtuale

## Obiettivo

Realizzare un piccolo ambiente virtuale composto da:

-   un client Linux;
-   un server Linux;
-   una rete virtuale;
-   accesso SSH;
-   Web server;
-   verifica della connettività.

## Architettura

``` mermaid
flowchart TB
    PC[Computer fisico]

    VB[VirtualBox]

    PC --> VB

    VB --> C[Debian Client]

    VB --> S[Debian Server]

    C --- R[Rete virtuale]
    S --- R

    C -->|SSH| S
    C -->|HTTP| S
```

## Configurazione prevista

### Client

``` text
Nome: Debian-Client
IP: 192.168.56.10
Ruolo: client
```

### Server

``` text
Nome: Debian-Server
IP: 192.168.56.20
Ruolo: server
```

### Servizi

Sul server:

``` text
SSH
Apache
```

## Fase 1 --- Verifica della rete

Dal client:

``` bash
ping 192.168.56.20
```

## Fase 2 --- Accesso SSH

Dal client:

``` bash
ssh nomeutente@192.168.56.20
```

Verificare di essere effettivamente sul server:

``` bash
hostname
```

## Fase 3 --- Verifica del Web server

Dal client:

``` text
http://192.168.56.20
```

## Fase 4 --- Modifica del server

Collegarsi tramite SSH e modificare la pagina Web.

Tornare sul client e verificare che la modifica sia visibile.

Il percorso complessivo è:

``` text
CLIENT
  │
  │ SSH
  ▼
SERVER
  │
  └── Apache
        │
        ▼
     Pagina Web
```

------------------------------------------------------------------------

# 12.13 Attività di approfondimento

## Attività A --- Due schede di rete

Configurare il server con:

``` text
Scheda 1 → NAT
Scheda 2 → Host-only
```

``` mermaid
flowchart LR
    I[Internet]
    N[NAT]
    S[Debian Server]
    H[Host-only]
    C[Debian Client]

    I --> N
    N --> S
    S --> H
    H --> C
```

Lo studente deve comprendere che il server possiede **due interfacce di
rete**.

## Attività B --- Server raggiungibile da Internet?

Partendo dalla configurazione precedente, discutere:

> Il Web server è raggiungibile direttamente da Internet?

La risposta deve essere motivata analizzando:

-   NAT;
-   indirizzi IP;
-   rete fisica;
-   rete virtuale;
-   routing;
-   porte.

## Attività C --- Cambiare indirizzo IP

Modificare l'indirizzo IP del server.

Verificare cosa accade quando il client continua a utilizzare il vecchio
indirizzo:

``` bash
ping 192.168.56.20
```

e successivamente utilizza quello nuovo.

L'attività serve a evidenziare che **il nome della macchina e
l'indirizzo IP sono concetti distinti**.

------------------------------------------------------------------------

# 12.14 Scheda di verifica del laboratorio

## Virtualizzazione

1.  Che cos'è una macchina virtuale?
2.  Qual è la differenza tra host e guest?
3.  Che cos'è un hypervisor?
4.  Qual è la differenza tra hypervisor di tipo 1 e tipo 2?
5.  Perché VirtualBox può essere utilizzato per creare un laboratorio di
    rete?

## Hardware virtuale

6.  Che cosa rappresentano CPU e RAM virtuali?
7.  Che cos'è un disco virtuale?
8.  Che cosa significa allocazione dinamica?
9.  Una VM può avere più dischi virtuali?

## Linux

10. Perché utilizzare una distribuzione Linux senza interfaccia grafica?
11. A cosa serve `sudo`?
12. Qual è la differenza tra utente normale e root?
13. A cosa servono `lscpu`, `free`, `lsblk` e `df`?

## Rete

14. Che cos'è un indirizzo IP?
15. Che cos'è un gateway?
16. A cosa serve il DNS?
17. Che differenza c'è tra NAT e Host-only?
18. Come possono comunicare due VM sulla stessa rete virtuale?

## Client/server

19. Che cos'è SSH?
20. Che cos'è un servizio?
21. Che cos'è una porta TCP?
22. Qual è la differenza tra client e server?
23. Come fa un browser sul client a visualizzare una pagina presente sul
    server?

------------------------------------------------------------------------

# 12.15 Consegna finale per gli studenti

Al termine del percorso ogni gruppo deve consegnare una breve
documentazione contenente.

## 1. Configurazione delle VM

Per ogni macchina:

``` text
Nome:
Sistema operativo:
CPU:
RAM:
Disco:
Schede di rete:
Indirizzo IP:
Ruolo:
```

## 2. Schema della rete

Un diagramma che rappresenti:

-   computer fisico;
-   VirtualBox;
-   client;
-   server;
-   rete virtuale;
-   collegamenti;
-   indirizzi IP.

## 3. Comandi utilizzati

Inserire i principali comandi utilizzati durante il laboratorio,
spiegandone brevemente la funzione.

## 4. Servizi installati

Indicare:

``` text
SSH
Apache
```

e spiegare quale ruolo svolgono.

## 5. Test effettuati

Documentare almeno:

``` bash
ping
ip addr
ip route
ssh
```

e il test HTTP tramite browser.

## 6. Problemi incontrati

Per ogni problema indicare:

``` text
Problema
↓
Ipotesi
↓
Comandi/verifiche effettuate
↓
Soluzione
```

Nel laboratorio di Sistemi e Reti non è sufficiente arrivare al
risultato: bisogna imparare a diagnosticare il motivo per cui qualcosa
non funziona.

------------------------------------------------------------------------

# 12.16 Collegamento con il capitolo successivo

Al termine di questo capitolo lo studente avrà costruito un ambiente
Linux virtualizzato che verrà utilizzato anche nelle attività
successive.

``` mermaid
flowchart TB
    C1[Capitolo 1<br>Il sistema di elaborazione]
    C2[Capitolo 2<br>Virtualizzazione]
    V[VirtualBox]
    L[VM Linux]
    F[Filesystem]
    U[Utenti e permessi]
    P[Processi]
    S[Servizi]
    N[Rete]

    C1 --> C2
    C2 --> V
    V --> L
    L --> F
    L --> U
    L --> P
    L --> S
    L --> N
```

Il percorso didattico complessivo diventa:

``` text
TEORIA
Sistema di elaborazione
        ↓
Virtualizzazione
        ↓
LABORATORIO
Creazione VM
        ↓
Installazione Linux
        ↓
Terminale
        ↓
Filesystem
        ↓
Utenti e permessi
        ↓
Processi e servizi
        ↓
Rete
        ↓
SSH
        ↓
Web server
        ↓
Client / Server
        ↓
LABORATORIO FINALE
Piccola infrastruttura di rete
```

VirtualBox non viene quindi trattato come un argomento isolato, ma
diventa l'ambiente di laboratorio che accompagnerà il successivo
percorso di Sistemi e Reti.
