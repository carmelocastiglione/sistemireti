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
