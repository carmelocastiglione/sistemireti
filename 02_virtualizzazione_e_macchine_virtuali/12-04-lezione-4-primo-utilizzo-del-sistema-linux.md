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

Poi:

``` bash
hostname
```

## Attività 2 --- Aggiornare il sistema al primo avvio

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

## Attività 3 --- Esplorare il filesystem

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

Su Debian moderno, `/bin` e `/sbin` possono essere collegamenti alle
rispettive directory dentro `/usr`; anche `/lib` può essere un
collegamento. Per questo, a seconda dell'installazione, alcune voci
possono apparire come collegamenti simbolici o non essere presenti.

## Attività 4 --- Creare una struttura di laboratorio

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

## Attività 5 --- Creare e modificare file

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
