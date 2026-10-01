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

e un normale utente. Per le attività quotidiane è preferibile usare un
account normale e ottenere i privilegi amministrativi solo quando
servono.

### Diventare root con `su`

Su Debian minimal potrebbe essere installato `su` ma non `sudo`. Per
aprire una shell di root si usa:

``` bash
su -
```

Inserire la **password dell'utente root**, impostata durante
l'installazione. Il trattino avvia una sessione di login e carica
l'ambiente di root. Il prompt termina normalmente con `#`, mentre quello
di un utente normale termina con `$`. Per tornare all'utente normale,
chiudere la shell di root:

``` bash
exit
```

### Usare `sudo`

`sudo` consente a un utente autorizzato di eseguire singoli comandi con
privilegi amministrativi. Per esempio:

``` bash
sudo apt update
```

Quando richiesto, inserire la **password del proprio utente**, non quella
di root. Per aprire una shell amministrativa si può usare `sudo -i`;
`exit` chiude la shell e ripristina l'utente normale.

### Installare e configurare `sudo`

Se `sudo` non è installato, da utente normale annotare il proprio nome
utente:

``` bash
whoami
```

Poi diventare root con `su -`, aggiornare l'elenco dei pacchetti e
installare `sudo`:

``` bash
su -
apt update
apt install sudo
```

Dopo l'installazione, aggiungere l'utente annotato al gruppo
amministrativo `sudo`, sostituendo `nome_utente` con il nome annotato:

``` bash
adduser nome_utente sudo
```

Su Debian, `adduser` permette di aggiungere l'utente esistente al gruppo
senza rimuoverlo dagli altri gruppi. La configurazione predefinita di
`sudo` autorizza normalmente i membri del gruppo `sudo`. Per controllare
la sintassi della configurazione:

``` bash
visudo -c
```

Se il controllo segnala errori o il gruppo non è autorizzato, aprire la
configurazione in modo sicuro con `visudo` e aggiungere, se manca, la
regola:

``` text
%sudo ALL=(ALL:ALL) ALL
```

Se `visudo` apre Vim, per aggiungere la regola alla fine del file:

1. Premere `G` per andare all'ultima riga.
2. Premere `o` per creare una nuova riga e iniziare a scrivere.
3. Digitare `%sudo ALL=(ALL:ALL) ALL`.
4. Premere `Esc`, digitare `:wq` e premere `Invio` per salvare e uscire.

Se non si vuole salvare, premere `Esc`, digitare `:q!` e premere
`Invio`. Se la regola è già presente, non aggiungerne una duplicata.
`visudo` controlla la sintassi prima di salvare; non modificare
direttamente `/etc/sudoers` con un editor normale. Dopo aver aggiunto
l'utente al gruppo, uscire e accedere nuovamente a Linux affinché la
nuova appartenenza venga applicata. Verificare poi da utente normale:

``` bash
sudo whoami
```

Se la configurazione è corretta, il comando stampa `root`.

### Domande

1.  Che cos'è `root`?
2.  Perché non è consigliabile utilizzare sempre root?
3.  Qual è la differenza tra `su -` e `sudo`?
4.  Quale password viene richiesta da `su -`? E quale da `sudo`?
5.  Come si installa `sudo` se non è presente?
6.  Perché occorre uscire e accedere nuovamente dopo aver aggiunto
    l'utente al gruppo `sudo`?
7.  Perché un sistema server può essere utilizzato senza interfaccia
    grafica?

------------------------------------------------------------------------
