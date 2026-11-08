# 1. Il segnale: analogico e digitale

Un **segnale** è una grandezza fisica che varia nel tempo e che può essere usata per rappresentare e trasportare informazioni. In un collegamento elettrico può essere una tensione o una corrente; in una fibra è un'onda luminosa; in una comunicazione wireless è un'onda elettromagnetica.

## Grandezze fondamentali

Un segnale periodico può essere descritto con:

- **ampiezza**: valore massimo della grandezza;
- **periodo** \(T\): tempo necessario per un ciclo completo;
- **frequenza** \(f\): numero di cicli al secondo, misurato in hertz (Hz);
- **fase**: posizione del ciclo rispetto a un riferimento.

Frequenza e periodo sono legati dalla relazione:

\[
f = \frac{1}{T}
\]

## Segnale analogico

Un segnale **analogico** può assumere, in teoria, un insieme continuo di valori. Una voce acquisita da un microfono, per esempio, produce una forma d'onda la cui ampiezza cambia continuamente.

```text
ampiezza
   ^
   |      /‾\       /‾\
   |  ___/   \_____/   \___
   +--------------------------> tempo
```

Il rumore può modificare gradualmente la forma del segnale e rendere meno precisa la ricostruzione dell'informazione.

## Segnale digitale

Un segnale **digitale** rappresenta l'informazione mediante un insieme finito di simboli. Nei sistemi binari i simboli sono normalmente 0 e 1. Il mezzo fisico non trasporta numeri astratti: trasporta livelli elettrici, impulsi luminosi o stati elettromagnetici che il ricevitore interpreta secondo regole concordate.

```text
livello
  1  ┌─────┐       ┌─────┐
     │     │       │     │
  0 ─┘     └───────┘     └──> tempo
```

La forma d'onda può essere deformata dal rumore, ma finché il ricevitore riesce a distinguere correttamente gli stati previsti può rigenerare una sequenza digitale pulita.

## Campionamento e quantizzazione

Per convertire un segnale analogico in forma digitale si effettuano, in genere:

1. **campionamento**: si misura il segnale a intervalli regolari;
2. **quantizzazione**: ogni misura viene approssimata a uno tra un numero finito di livelli;
3. **codifica**: i livelli vengono rappresentati con sequenze di bit.

La frequenza di campionamento e il numero di livelli influenzano la fedeltà della rappresentazione e la quantità di dati prodotta.

## Bit, simboli e trasmissione

Un **bit** è un'unità di informazione binaria. Un **simbolo** è uno stato del segnale scelto da un sistema di trasmissione. Un simbolo può rappresentare uno o più bit: per questo velocità in bit/s e velocità in baud non sono sempre uguali.

La scelta tra forme analogiche e digitali dipende dall'applicazione; nei sistemi di rete moderni i dati sono in genere digitali, anche quando il collegamento fisico usa una portante analogica modulata.

---
