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
sudo apt install nginx
```

Verificare:

``` bash
systemctl status nginx
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
   W[Nginx<br>Web Server]

    B --> N
    N --> W
```

## Attività 3 --- Modificare la pagina

Su Debian, la directory del sito predefinita di Nginx è
`/var/www/html`. Modificare la pagina iniziale con:

``` bash
sudo nano /var/www/html/index.html
```

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
Nginx
   ↓
pagina HTML
```

------------------------------------------------------------------------
