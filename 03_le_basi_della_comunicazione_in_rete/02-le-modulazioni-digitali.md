# 2. Le modulazioni digitali

La **modulazione** è il processo con cui l'informazione modifica una caratteristica di un segnale, detto **portante**, così da poter essere trasmessa attraverso un canale. Nel caso della modulazione digitale, i simboli da trasmettere determinano variazioni discrete della portante.

La **demodulazione** è l'operazione svolta al ricevitore per stimare i simboli trasmessi e ricostruire i dati. Un apparato che trasmette e riceve può integrare entrambe le funzioni.

## Modulazione e demodulazione

Il trasmettitore codifica i bit in simboli e li associa a parametri della portante; il ricevitore osserva il segnale ricevuto, che può essere attenuato o disturbato, e decide quale simbolo sia stato inviato.

La quantità di simboli trasmessi al secondo si misura in **baud**. Se ogni simbolo rappresenta \(k\) bit, in condizioni ideali il bit rate è:

\[
R_b = R_s \cdot k
\]

dove \(R_b\) è il bit rate e \(R_s\) è il symbol rate. Il valore effettivo utile può essere inferiore per la presenza di codifica, intestazioni, ridondanza e ritrasmissioni.

## ASK — variazione di ampiezza

Nella **Amplitude Shift Keying (ASK)** i simboli sono rappresentati usando ampiezze diverse della portante. Una forma elementare associa ampiezza bassa e alta ai bit 0 e 1.

- È semplice da realizzare.
- È sensibile alle variazioni di ampiezza e al rumore che altera il livello del segnale.

## FSK — variazione di frequenza

Nella **Frequency Shift Keying (FSK)** i simboli corrispondono a frequenze diverse. Nella FSK binaria si usano due frequenze per rappresentare 0 e 1.

- Le informazioni sono codificate nella frequenza, non nell'ampiezza.
- La separazione tra frequenze aiuta a distinguere gli stati, ma la banda occupata dipende dai parametri e dalla realizzazione.

## PSK — variazione di fase

Nella **Phase Shift Keying (PSK)** i simboli sono rappresentati da fasi diverse della portante. La BPSK usa due fasi separate; la QPSK ne usa quattro e può rappresentare due bit per simbolo.

Maggiore è il numero di stati, maggiore è il numero di bit rappresentabili per simbolo, ma può diventare più difficile distinguere simboli vicini in presenza di rumore.

## QAM — ampiezza e fase

La **Quadrature Amplitude Modulation (QAM)** varia congiuntamente ampiezza e fase. Per esempio, una costellazione 16-QAM presenta 16 stati possibili e può rappresentare 4 bit per simbolo; una 64-QAM ne rappresenta 6.

La QAM consente elevata efficienza spettrale in condizioni di canale adeguate. Richiede però una buona qualità del segnale: se gli stati ricevuti si spostano troppo a causa del rumore o della distorsione, il ricevitore può confonderli.

| Tecnica | Caratteristica variata | Esempio di informazione |
|---|---|---|
| ASK | Ampiezza | Livello basso / alto |
| FSK | Frequenza | Una frequenza per ciascuno stato |
| PSK | Fase | Due o più fasi |
| QAM | Ampiezza e fase | Combinazioni in una costellazione |

Queste tecniche sono famiglie di modulazione: gli standard reali possono aggiungere codifica, sincronizzazione e altre elaborazioni.

---
