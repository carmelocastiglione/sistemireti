# 3. Il canale di comunicazione

Il **canale di comunicazione** è il percorso attraverso cui un segnale passa dal trasmettitore al ricevitore. Il canale ha capacità e caratteristiche fisiche limitate: attenuazione, rumore, interferenze e distorsione possono influenzare la trasmissione.

## Multiplexing

Il **multiplexing** consente di condividere un mezzo o una risorsa di trasmissione tra più flussi. Un multiplexer combina i flussi in trasmissione; un demultiplexer li separa a destinazione.

- **TDM (Time Division Multiplexing)**: ogni flusso usa il canale in intervalli di tempo assegnati. Gli intervalli possono essere fissi o assegnati dinamicamente.
- **FDM (Frequency Division Multiplexing)**: i flussi occupano bande di frequenza differenti nello stesso intervallo temporale.
- **WDM (Wavelength Division Multiplexing)**: in fibra ottica, più flussi usano lunghezze d'onda luminose diverse.

Le varianti **CWDM** e **DWDM** identificano sistemi WDM con griglie e spaziature tra canali differenti. In generale, DWDM consente una spaziatura più fitta e un maggior numero di lunghezze d'onda sulla stessa fibra; capacità e distanze dipendono dall'apparato e dal progetto del collegamento.

## Codifica in linea

La **codifica in linea** trasforma una sequenza di bit in una forma d'onda adatta al mezzo. Deve consentire al ricevitore di riconoscere i bit e mantenere la sincronizzazione.

- **NRZ (Non-Return-to-Zero)**: il livello resta costante durante l'intervallo del bit. È semplice, ma lunghe sequenze senza transizioni possono rendere difficile recuperare il clock.
- **RZ (Return-to-Zero)**: il segnale ritorna a un livello di riferimento all'interno dell'intervallo del bit. Può facilitare la sincronizzazione, ma richiede più transizioni e banda.
- **Manchester**: ogni bit contiene una transizione a metà intervallo; la direzione della transizione distingue i valori. Offre transizioni regolari per la sincronizzazione, con maggiore attività di segnale rispetto a una codifica più semplice.

Questi nomi descrivono schemi di codifica di linea; gli standard possono specificarne diverse varianti e regole.

## Caratteristiche di una trasmissione dati

Una trasmissione si descrive considerando almeno:

- **bit rate**: numero di bit trasmessi al secondo, in bit/s;
- **baud rate**: numero di simboli trasmessi al secondo, in baud;
- **ritardo**: tempo necessario perché i dati arrivino a destinazione;
- **jitter**: variazione del ritardo nel tempo;
- **tasso di errore**: frequenza con cui i bit o i pacchetti arrivano corrotti;
- **throughput**: quantità di dati utili effettivamente consegnata nell'unità di tempo.

La **bandwidth** può indicare l'ampiezza della banda di frequenze di un canale (Hz) oppure, nel linguaggio comune delle reti, la sua capacità nominale di trasmissione (bit/s). È opportuno specificare il significato. Il throughput effettivo è normalmente inferiore alla capacità nominale per overhead, condivisione, congestione, errori e ritrasmissioni.

## Direzione della comunicazione

- **Simplex**: i dati viaggiano in una sola direzione.
- **Half-duplex**: la comunicazione è possibile in entrambe le direzioni, ma non contemporaneamente.
- **Full-duplex**: trasmissione e ricezione avvengono contemporaneamente.

## Collegamenti tra dispositivi

- **Point-to-point**: un collegamento collega direttamente due estremità.
- **Multipoint**: più dispositivi condividono lo stesso collegamento o mezzo; occorre coordinare l'accesso e gestire le possibili interferenze tra trasmissioni.

La topologia del collegamento, la modalità duplex e la tecnica di multiplexing sono aspetti distinti, anche se possono essere combinati nello stesso sistema.

---
