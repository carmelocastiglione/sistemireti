# 12. Architetture CISC e RISC
## Approfondimento: ISA e microarchitettura

È fondamentale distinguere **ISA** e **microarchitettura**.

L'ISA definisce ciò che il software vede: istruzioni, registri, modalità di indirizzamento e comportamento previsto.

La microarchitettura descrive invece come il processore realizza fisicamente quelle funzionalità.

Due processori possono implementare la stessa ISA ma avere microarchitetture molto diverse e quindi prestazioni differenti.

### CISC e micro-operazioni

Le moderne CPU x86 possono tradurre alcune istruzioni dell'ISA in operazioni interne più semplici, spesso chiamate **micro-operazioni**.

Questo permette di combinare:

- compatibilità con una ISA complessa;
- pipeline;
- esecuzione fuori ordine;
- previsione dei salti;
- parallelismo interno.

### RISC non significa "pochi transistor"

Un'ISA RISC può essere implementata con microarchitetture estremamente complesse. La semplificazione riguarda soprattutto la struttura e la regolarità del set di istruzioni.

Questa distinzione è importante perché evita una contrapposizione troppo semplicistica:

```text
CISC = complesso = lento
RISC = semplice = veloce
```

che non descrive correttamente i processori moderni.


## 12.1 Linguaggio macchina e architettura

Il **set di istruzioni (ISA — Instruction Set Architecture)** definisce il modello che mette in relazione software e processore.

Comprende, tra gli altri elementi:

- istruzioni;
- registri;
- modalità di indirizzamento;
- tipi di dati;
- comportamento delle istruzioni;
- gestione della memoria.

L'ISA è distinta dall'implementazione fisica del processore.

---

# 12.2 CISC

**CISC = Complex Instruction Set Computer**

L'idea tradizionale del CISC è fornire un insieme ampio di istruzioni, alcune delle quali possono essere relativamente complesse.

Caratteristiche tipiche:

- numerose istruzioni;
- istruzioni di lunghezza variabile in molte ISA;
- numerose modalità di indirizzamento;
- alcune istruzioni possono svolgere operazioni articolate.

Un esempio importante è la famiglia **x86**.

> CISC non significa semplicemente "CPU lenta" e RISC non significa semplicemente "CPU veloce": sono caratteristiche dell'ISA e della progettazione, mentre le CPU moderne possono implementare tecniche molto sofisticate.

---

# 12.3 RISC

**RISC = Reduced Instruction Set Computer**

L'approccio RISC punta a un insieme di istruzioni più regolare e semplice da gestire.

Caratteristiche tipiche:

- istruzioni relativamente semplici;
- molte operazioni eseguite sui registri;
- numerosi registri;
- uso frequente del modello load/store;
- istruzioni spesso di lunghezza fissa o più regolare, a seconda dell'ISA;
- progettazione favorevole alla pipeline.

Esempi di ISA RISC:

- ARM;
- RISC-V;
- MIPS;
- Power.

---

## 12.4 Modello load/store

In molte architetture RISC, le operazioni aritmetiche lavorano sui registri.

Per accedere alla memoria vengono utilizzate istruzioni specifiche.

Esempio concettuale:

```text
LOAD  R1, [indirizzo]
LOAD  R2, [indirizzo]

ADD   R3, R1, R2

STORE R3, [indirizzo]
```

La memoria viene quindi utilizzata principalmente tramite:

- **LOAD** → memoria → registro;
- **STORE** → registro → memoria.

---

## 12.5 Confronto CISC e RISC

| Caratteristica | CISC | RISC |
|---|---|---|
| Set di istruzioni | Tradizionalmente ampio | Tradizionalmente più contenuto |
| Complessità istruzioni | Può essere elevata | Generalmente più semplice |
| Lunghezza istruzioni | Spesso variabile | Spesso più regolare |
| Accesso memoria | Può essere integrato in molte istruzioni | Tipicamente concentrato in LOAD/STORE |
| Registri | Dipende dall'ISA | Generalmente numerosi |
| Pipeline | Possibile, ma progettazione complessa | Storicamente favorita dalla regolarità |
| Esempi | x86-64 | ARM, RISC-V |

### Una distinzione importante

Le moderne CPU non sono classificabili in modo semplicistico.

Ad esempio, processori x86 moderni possono tradurre istruzioni complesse in operazioni interne più semplici (**micro-operazioni**), mentre processori RISC moderni possono avere implementazioni molto sofisticate.

Quindi:

> **CISC e RISC descrivono principalmente filosofie e caratteristiche dell'ISA, non una semplice misura delle prestazioni.**

---
