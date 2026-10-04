# 12.4 Lezione 4 --- Primo utilizzo del sistema Linux

## Obiettivi

Lo studente deve imparare a:

-   effettuare il login;
-   aggiornare il sistema operativo;
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

`whoami` stampa il nome dell'utente con cui è in esecuzione la sessione corrente. Dopo il login dovrebbe mostrare il nome dell'account appena creato.

Poi:

``` bash
hostname
```

`hostname` stampa il nome assegnato al computer nella rete, impostato durante l'installazione.

Nel terminale, il prompt è la scritta che precede il cursore e indica il contesto in cui verrà eseguito il prossimo comando. Spesso ha una forma simile a:

``` text
utente@hostname:posizione$
```

Per esempio, `studente@debian:~$` indica che la sessione è dell'utente `studente`, la macchina si chiama `debian` e la directory corrente è la sua cartella personale (`~`, cioè `/home/studente`). Il simbolo `$` indica normalmente un utente senza privilegi amministrativi; in una shell di `root` compare spesso `#`. La forma esatta del prompt può variare.

Il comando `pwd` mostra il percorso completo della directory corrente, per esempio `/home/studente`:

``` bash
pwd
```

## Attività 2 --- Utente normale e root

In Linux l'account normale e l'account `root` sono distinti. L'account normale viene usato per il login e per le attività quotidiane: i suoi permessi sono limitati e i suoi file personali si trovano in `/home/nome_utente`. `root` è l'amministratore del sistema, può modificare file e impostazioni di tutti gli utenti e ha la propria directory personale in `/root`.

È preferibile lavorare come utente normale e ottenere i privilegi amministrativi solo per i comandi che ne hanno bisogno. In questo modo si riduce il rischio di modificare o cancellare per errore parti importanti del sistema.

Se durante l'installazione è stata impostata una password di `root`, si può passare all'account amministratore con:

``` bash
su -
```

Inserire la password di `root`. Il prompt termina normalmente con `#`; per tornare all'utente normale digitare `exit`.

Se la password di `root` è stata lasciata vuota, usare `sudo` per eseguire un singolo comando con privilegi amministrativi, per esempio:

``` bash
sudo apt update
```

In questo caso viene richiesta la password dell'utente normale. Per aprire una shell amministrativa temporanea si può usare `sudo -i`; `exit` chiude la shell. Verificare i privilegi con:

``` bash
sudo whoami
```

Se la configurazione è corretta, il comando stampa `root`.

Se `sudo` non è disponibile e si è impostata una password di `root`, installarlo da una shell di root:

``` bash
su -
apt update
apt install sudo
adduser nome_utente sudo
exit
```

Sostituire `nome_utente` con il proprio nome utente. Poi uscire e accedere nuovamente affinché l'appartenenza al gruppo `sudo` venga applicata. Alle volte è necessario riavviare la macchina virtuale.

### Domande

1. Qual è la differenza tra un account normale e l'account `root`?
2. Perché è preferibile usare l'account normale per le attività quotidiane?
3. Qual è la differenza tra `su -` e `sudo`?
4. Quale password viene richiesta da `su -`? E quale da `sudo`?
5. Che cosa comporta lasciare vuota la password di `root` durante l'installazione?
6. Perché occorre uscire e accedere nuovamente dopo aver aggiunto l'utente al gruppo `sudo`?

## Attività 3 --- Aggiornare il sistema al primo avvio

Al primo avvio dopo l'installazione è importante aggiornare Debian. Gli
aggiornamenti correggono problemi, migliorano la stabilità e includono
correzioni di sicurezza. Prima di procedere, verificare che la macchina
virtuale sia connessa a Internet.

Da questo punto del laboratorio si presume che `sudo` sia installato e
configurato. Eseguire i comandi da utente normale:

``` bash
sudo apt update
sudo apt upgrade
```

`apt update` aggiorna l'elenco dei pacchetti disponibili; `apt upgrade`
scarica e installa gli aggiornamenti. Quando viene chiesta conferma,
leggere il riepilogo e rispondere `y` per procedere.

È buona pratica controllare regolarmente la disponibilità di nuovi
aggiornamenti, non soltanto al primo avvio.

## Attività 4 --- Esplorare il filesystem

``` bash
pwd
```

`pwd` (print working directory) mostra il percorso completo della directory in cui ci si trova.

``` bash
ls
```

`ls` elenca i file e le directory presenti nella directory corrente. Questo comando non dovrebbe mostrare nulla inizialmente, perché la home directory dell'utente normale è vuota subito dopo l'installazione e contriene solamente file e directory nascoste come `.bashrc` e `.profile`. Per visualizzare anche questi file nascosti, si utilizza `ls -al`. I file e le directory nascoste sono quelli il cui nome inizia con un punto.

``` bash
ls -al
```

Con le opzioni `-l` e `-a`, `ls -al` mostra un elenco dettagliato, includendo anche i file nascosti, i cui nomi iniziano con un punto. Le colonne riportano, tra le altre informazioni, permessi, proprietario, dimensione e data di modifica.

``` bash
cd /
```

`cd` (change directory) cambia la directory corrente; `/` indica la radice del filesystem. Dopo questo comando ci si sposta quindi alla directory principale del sistema.

``` bash
ls
```

Ora `ls` elenca il contenuto di `/`, non quello della directory in cui ci si trovava prima. Le voci mostrate sono le directory e i file al livello principale del filesystem.

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
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

La directory `/` è la radice dell'intero filesystem: tutte le altre
directory si trovano al suo interno. Le directory principali hanno
questi scopi:

-   `/bin`: comandi essenziali utilizzabili dagli utenti, per esempio
	`ls` e `cp`.
-   `/boot`: file necessari all'avvio, come il kernel Linux e i file del
	bootloader.
-   `/dev`: file speciali che rappresentano dispositivi e periferiche.
-   `/etc`: file di configurazione del sistema e dei servizi.
-   `/home`: directory personali degli utenti normali.
-   `/lib`: librerie necessarie ai programmi essenziali e moduli del
	kernel.
-   `/media`: punti di montaggio usati normalmente per supporti
	rimovibili.
-   `/mnt`: punto di montaggio temporaneo, usato spesso
	dall'amministratore.
-   `/opt`: software aggiuntivo installato al di fuori della normale
	gerarchia dei pacchetti.
-   `/proc`: filesystem virtuale con informazioni sui processi e sul
	kernel; i suoi contenuti sono generati dal sistema.
-   `/root`: directory personale dell'utente amministratore `root`;
	non va confusa con `/`, che è la radice dell'intero filesystem.
-   `/run`: dati temporanei relativi ai programmi e ai servizi in
	esecuzione, ricreati durante l'avvio.
-   `/sbin`: strumenti essenziali di amministrazione del sistema.
-   `/srv`: dati forniti dai servizi del sistema, per esempio quelli di
	un server Web.
-   `/sys`: filesystem virtuale che espone informazioni e dispositivi
	del kernel.
-   `/tmp`: file temporanei; il sistema può eliminarli, quindi non è
	adatto a conservare dati importanti.
-   `/usr`: gran parte dei programmi, delle librerie e della
	documentazione installati nel sistema. Non è la directory personale
	dell'utente.
-   `/var`: dati che cambiano durante l'uso, come log, cache e code dei
	servizi.

Su Debian moderno, `/bin` e `/sbin` possono essere collegamenti alle rispettive directory dentro `/usr`; anche `/lib` può essere un collegamento. Per questo, a seconda dell'installazione, alcune voci possono apparire come collegamenti simbolici o non essere presenti.

## Attività 5 --- Creare una struttura di laboratorio

Il comando `mkdir` (make directory) crea una nuova directory nel percorso indicato. In `mkdir ~/laboratorio`, `~` rappresenta la directory personale dell'utente: viene quindi creata la cartella `laboratorio` al suo interno.

``` bash
cd /home/nome_utente
mkdir laboratorio
cd laboratorio
```

Una volta entrati in `laboratorio`, i comandi seguenti creano al suo interno tre directory: `lezione1`, `lezione2` ed `esercizi`.

``` bash
mkdir lezione1
mkdir lezione2
mkdir esercizi
```

Verificare:

``` bash
ls
```

## Attività 6 --- Creare e modificare file

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

`nano` è un editor di testo che si usa direttamente nel terminale. Il comando apre `informazioni.txt`; se il file non esiste ancora, lo crea quando viene salvato. Inserire alcune informazioni sulla macchina.

Per salvare le modifiche e uscire:

1. Premere `Ctrl+X` per chiudere `nano`.
2. Alla richiesta di salvare le modifiche, premere `Y` (Yes, cioè Sì).
3. Quando viene mostrato il nome `informazioni.txt`, premere `Invio` per confermarlo.

Successivamente:

``` bash
cat informazioni.txt
```
`cat` è un comando che mostra nel terminale il contenuto di un file.


## Riepilogo dei comandi Linux

| Comando | Funzione |
| --- | --- |
| `whoami` | Mostra il nome dell'utente della sessione corrente. |
| `hostname` | Mostra il nome assegnato al computer nella rete. |
| `pwd` | Mostra il percorso della directory corrente. |
| `su -` | Apre una shell di login come `root`, chiedendone la password. |
| `sudo <comando>` | Esegue un singolo comando con privilegi amministrativi. |
| `sudo -i` | Apre una shell interattiva con privilegi amministrativi. |
| `sudo whoami` | Verifica l'identità effettiva con cui viene eseguito un comando amministrativo; normalmente stampa `root`. |
| `sudo apt update` | Aggiorna l'elenco dei pacchetti disponibili con privilegi amministrativi. |
| `sudo apt upgrade` | Scarica e installa gli aggiornamenti dei pacchetti con privilegi amministrativi. |
| `apt update` | Aggiorna l'elenco dei pacchetti disponibili. Va eseguito con privilegi amministrativi. |
| `apt install sudo` | Installa il pacchetto `sudo`. Va eseguito come `root`. |
| `adduser nome_utente sudo` | Aggiunge l'utente indicato al gruppo `sudo`. Va eseguito come `root`. |
| `exit` | Chiude la shell corrente o termina la sessione amministrativa. |
| `ls` | Elenca file e directory nella directory corrente. |
| `ls -al` | Mostra un elenco dettagliato, includendo i file nascosti. |
| `ls -l` | Mostra un elenco dettagliato di file e directory. |
| `cd /` | Sposta la directory corrente alla radice del filesystem. |
| `cd /home/nome_utente` | Sposta la directory corrente alla home dell'utente indicato. Sostituire `nome_utente` con il proprio nome. |
| `cd laboratorio` | Entra nella directory `laboratorio`, se si trova nella directory corrente. |
| `mkdir ~/laboratorio` | Crea la directory `laboratorio` nella home dell'utente. |
| `mkdir laboratorio` | Crea la directory `laboratorio` nella directory corrente. |
| `mkdir lezione1`, `mkdir lezione2`, `mkdir esercizi` | Creano le tre sottodirectory per organizzare il lavoro del laboratorio. |
| `touch informazioni.txt` | Crea il file vuoto se non esiste; se esiste, ne aggiorna la data di modifica. |
| `nano informazioni.txt` | Apre `informazioni.txt` nell'editor di testo `nano`. |
| `cat informazioni.txt` | Mostra nel terminale il contenuto del file. |

------------------------------------------------------------------------
