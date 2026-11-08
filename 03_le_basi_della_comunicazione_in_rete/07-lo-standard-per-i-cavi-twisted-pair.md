# 7. Lo standard per i cavi twisted pair

Per realizzare collegamenti affidabili su doppino intrecciato non basta scegliere un cavo: occorre rispettare la categoria, la disposizione dei conduttori nei connettori e le regole di installazione.

## Categorie e cablaggio

Gli standard di cablaggio strutturato, come quelli della famiglia **TIA/EIA-568**, definiscono requisiti per componenti e collegamenti. Le categorie (per esempio Cat 5e, Cat 6 e Cat 6A) specificano prestazioni elettriche; frequenza supportata, lunghezza ammessa e prestazioni dipendono dallo standard applicabile e dalla configurazione completa del canale.

Le categorie non sono semplicemente sinonimi di una velocità Ethernet: contano anche lunghezza, qualità di posa, patch cord, prese e apparati. Per un cablaggio permanente si seguono i limiti e le specifiche dello standard pertinente.

## Connettore 8P8C

Il connettore comunemente chiamato **RJ-45** nelle reti Ethernet è un connettore modulare a otto posizioni e otto contatti (8P8C). Due schemi di cablaggio diffusi sono **T568A** e **T568B**.

| Pin | T568A | T568B |
|---:|---|---|
| 1 | Bianco/verde | Bianco/arancione |
| 2 | Verde | Arancione |
| 3 | Bianco/arancione | Bianco/verde |
| 4 | Blu | Blu |
| 5 | Bianco/blu | Bianco/blu |
| 6 | Arancione | Verde |
| 7 | Bianco/marrone | Bianco/marrone |
| 8 | Marrone | Marrone |

La differenza tra i due schemi è lo scambio delle coppie verde e arancione. Per un normale collegamento diritto si usa lo stesso schema alle due estremità. Un collegamento incrociato usa schemi diversi alle estremità; molte interfacce moderne supportano l'autocorrezione MDI/MDI-X, ma la pratica di cablaggio va comunque conforme al progetto e allo standard.

## Buone pratiche

- mantenere l'intreccio delle coppie il più possibile vicino alla terminazione;
- non danneggiare o schiacciare il cavo e rispettare il raggio di curvatura;
- evitare percorsi paralleli ravvicinati a sorgenti di disturbi, quando possibile;
- usare componenti della stessa categoria richiesta dal collegamento;
- verificare continuità, ordine dei fili e prestazioni con strumenti adeguati.

Un cavo con tutti gli otto fili collegati può comunque non rispettare le prestazioni previste se le coppie sono terminate male o il cablaggio non è conforme.

---
