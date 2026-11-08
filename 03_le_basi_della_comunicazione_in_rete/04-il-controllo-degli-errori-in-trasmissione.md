# 4. Il controllo degli errori in trasmissione

Durante una trasmissione, il rumore o un'interferenza possono alterare uno o più bit. Per rilevare o correggere gli errori si aggiungono informazioni ridondanti ai dati, secondo una regola nota sia al trasmettitore sia al ricevitore.

## Rilevazione e correzione

- Un **codice rilevatore** consente di accorgersi che i dati ricevuti potrebbero essere errati, ma non necessariamente di ricostruirli.
- Un **codice correttore** aggiunge ridondanza sufficiente a individuare e correggere alcuni errori senza chiedere una nuova trasmissione.

Un sistema può reagire a un errore rilevato scartando i dati, richiedendone la ritrasmissione (ARQ) o correggendoli localmente (FEC). La scelta dipende dal protocollo e dai requisiti del collegamento.

## Bit di parità

La **parità** aggiunge un bit al gruppo di bit trasmesso.

- **Parità pari**: il numero totale di bit a 1, incluso il bit di parità, deve essere pari.
- **Parità dispari**: il numero totale di bit a 1 deve essere dispari.

La parità semplice rileva ogni numero dispari di errori nel gruppo protetto, ma non rileva un numero pari di bit invertiti. Non indica da sola quale bit sia errato e quindi non lo corregge.

## Codici a ridondanza ciclica (CRC)

Il **CRC (Cyclic Redundancy Check)** interpreta i bit come coefficienti di un polinomio binario. Il trasmettitore esegue un calcolo basato su un polinomio generatore e aggiunge al messaggio una sequenza di controllo; il ricevitore ripete il calcolo e verifica il resto.

Il CRC è molto efficace nell'individuare numerosi errori comuni, in particolare sequenze di errori consecutive (burst), ma è un codice di rilevazione: in genere non corregge i dati. La capacità concreta dipende dal polinomio scelto e dalla lunghezza del messaggio.

## Codice di Hamming

Il **codice di Hamming** inserisce bit di controllo in posizioni definite. Ciascun bit di controllo verifica un insieme di posizioni; il risultato dei controlli, detto **sindrome**, può indicare la posizione di un singolo bit errato.

La forma classica del codice di Hamming consente di correggere un singolo errore. Aggiungendo una parità globale si ottiene una variante SECDED (*Single Error Correction, Double Error Detection*): corregge un errore singolo e rileva, in condizioni previste dal codice, un errore doppio.

## Confronto

| Metodo | Uso principale | Limite essenziale |
|---|---|---|
| Parità | Rilevare alcuni errori | Non individua la posizione; può non rilevare errori pari |
| CRC | Rilevare con affidabilità molti errori | Normalmente non corregge |
| Hamming | Correggere errori singoli (e, con estensione, rilevare doppi) | Richiede bit di controllo e ha capacità di correzione limitata |

La ridondanza migliora l'affidabilità, ma occupa parte della capacità del collegamento. I protocolli possono combinare controllo degli errori e ritrasmissione.

---
