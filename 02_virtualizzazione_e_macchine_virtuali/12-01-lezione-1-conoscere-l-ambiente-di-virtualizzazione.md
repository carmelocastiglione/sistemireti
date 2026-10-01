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

|  VirtualBox       | Concetto reale |
|------------------|----------------|
| Processori       | CPU            |
| Memoria          | RAM            |
| Disco virtuale   | Disco          |
| Scheda di rete   | NIC            |
| ISO              | Supporto di installazione |
| USB              | Controller/dispositivi USB |

### Attività di riflessione

Rispondere:

> Se creo una VM con 2 GB di RAM, quei 2 GB vengono "creati" dal
> computer?

Spiegare la risposta distinguendo tra **risorsa fisica** e **risorsa
virtuale**.

------------------------------------------------------------------------
