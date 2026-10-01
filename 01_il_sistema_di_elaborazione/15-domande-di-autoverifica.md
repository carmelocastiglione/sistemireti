# 15. Domande di autoverifica

## Livello 1 — Conoscenze

1. Che cosa si intende per sistema di elaborazione?
2. Quali sono i componenti fondamentali del modello di Von Neumann?
3. Che cosa significa programma memorizzato?
4. Qual è la funzione della CPU?
5. Che cosa fa l'ALU?
6. Che cosa fa l'unità di controllo?
7. Che cos'è un registro?
8. Che cos'è il clock?
9. Qual è la differenza tra bus dati e bus indirizzi?
10. A cosa serve la cache?
11. Che cosa significa cache hit?
12. Qual è la differenza tra RAM e memoria secondaria?
13. Che cos'è un SSD?
14. Che cosa significa RAID?
15. Che cos'è la memoria virtuale?
16. Che cosa distingue una periferica di input da una di output?
17. Che cosa significa PCI Express?
18. Che cosa significa NVMe?
19. Che cosa accade durante la fase di fetch?
20. Che cos'è una pipeline?
21. Che cosa sono gli hazard?
22. Che cosa significano CISC e RISC?

---

## Livello 2 — Comprensione

1. Perché la CPU può rimanere in attesa della memoria?
2. Perché una cache piccola può essere più veloce della RAM?
3. Perché un SSD non necessita di una testina di lettura?
4. Perché RAID 0 non aumenta l'affidabilità?
5. Perché la memoria virtuale non può essere considerata equivalente alla RAM?
6. Perché una CPU a 4 GHz non è necessariamente più veloce di una CPU a 3 GHz?
7. Qual è il vantaggio della pipeline?
8. Che differenza c'è tra un data hazard e un control hazard?
9. Perché il modello load/store è importante nelle architetture RISC?
10. Perché oggi la distinzione CISC/RISC è meno netta rispetto alle prime generazioni di processori?

---

## Livello 3 — Esercizi

### Esercizio 1 — Spazio di indirizzamento

Un processore dispone di un bus indirizzi di 20 bit.

1. Quanti indirizzi diversi può rappresentare?
2. Se ogni indirizzo identifica un byte, qual è la memoria massima indirizzabile?

Formula:

\[
N = 2^n
\]

---

### Esercizio 2 — Banda del bus

Un bus trasferisce 64 bit per operazione e realizza 200 milioni di trasferimenti al secondo.

Calcolare la banda teorica in:

1. bit/s;
2. byte/s;
3. GB/s.

---

### Esercizio 3 — RAID

Un sistema possiede quattro dischi identici.

Confrontare concettualmente:

- RAID 0;
- RAID 1;
- RAID 5;
- RAID 10.

Per ciascuno indicare:

- capacità utile;
- tolleranza ai guasti;
- vantaggio principale.

---

### Esercizio 4 — Pipeline

Considerare una pipeline a 5 stadi:

```text
F → D → E → M → W
```

Disegnare l'esecuzione di 4 istruzioni su almeno 8 cicli di clock.

Indicare in quale ciclo ogni istruzione completa il proprio percorso.

---

### Esercizio 5 — Hazard

Considerare:

```text
I1: ADD R1, R2, R3
I2: SUB R4, R1, R5
```

1. Quale dipendenza esiste?
2. Quale tipo di hazard può verificarsi?
3. Quali tecniche possono ridurne l'impatto?

---
