# 9. Gli standard di interfacciamento alle periferiche
## Approfondimento: interfaccia, protocollo e connettore

Questi tre concetti non sono sinonimi.

- **Connettore**: elemento fisico attraverso il quale si realizza il collegamento.
- **Interfaccia**: definisce come due componenti possono comunicare.
- **Protocollo**: insieme di regole che stabiliscono come devono essere scambiate le informazioni.

Un singolo connettore può supportare più protocolli o modalità operative. Per esempio, USB-C descrive soprattutto un tipo di connettore e non identifica da solo una singola velocità o un singolo protocollo.

### Esempio: USB-C

La presenza di una porta USB-C non permette da sola di dedurre:

- la velocità massima;
- il supporto video;
- la potenza di alimentazione;
- la compatibilità Thunderbolt.

È quindi necessario verificare le specifiche del dispositivo e della porta.

### Interfacce seriali e parallele

Storicamente le interfacce potevano trasferire più bit contemporaneamente attraverso linee parallele. Le interfacce seriali trasferiscono invece i bit secondo una sequenza temporale.

Le moderne interfacce seriali ad alta velocità hanno però raggiunto prestazioni molto elevate grazie a frequenze, codifiche e tecniche di comunicazione sofisticate.


Un'interfaccia definisce modalità e regole attraverso cui due componenti comunicano.

Gli standard permettono di stabilire:

- connettori;
- segnali elettrici;
- protocolli;
- velocità;
- modalità di trasferimento;
- gestione degli errori;
- identificazione dei dispositivi.

---

## 9.1 Collegamento con la CPU

Il collegamento tra CPU e altre componenti avviene tramite sistemi di interconnessione.

Esempi moderni:

- PCI Express;
- interfacce interne del processore;
- controller integrati;
- bus e collegamenti dedicati.

### PCI Express

PCIe utilizza collegamenti organizzati in **lane**.

Una connessione può essere indicata come:

```text
x1
x4
x8
x16
```

Il numero indica il numero di lane utilizzate.

---

## 9.2 Collegamento con le memorie di massa

### SATA

Utilizzato soprattutto per:

- HDD;
- SSD SATA;
- unità ottiche.

### NVMe

È un protocollo progettato per sfruttare meglio le caratteristiche delle memorie flash moderne.

Gli SSD NVMe comunicano generalmente tramite **PCI Express**.

Confronto:

| SATA | NVMe |
|---|---|
| Protocollo storico per storage | Progettato per storage flash moderno |
| Banda inferiore | Banda maggiore |
| Latenza generalmente superiore | Latenza generalmente inferiore |
| Diffuso con SSD SATA | Diffuso con SSD M.2 PCIe |

> **M.2** identifica principalmente un formato fisico; non significa automaticamente NVMe.

---

## 9.3 Collegamento con il video

I principali standard moderni includono:

- HDMI;
- DisplayPort;
- USB-C con modalità video supportate.

### HDMI

Molto diffuso per:

- monitor;
- TV;
- proiettori;
- audio/video digitale.

### DisplayPort

Molto diffuso nel collegamento tra computer e monitor.

Può supportare elevate risoluzioni e frequenze di aggiornamento e più monitor tramite tecnologie specifiche.

---

## 9.4 Altri collegamenti

| Standard | Utilizzo |
|---|---|
| USB | Periferiche, dati, alimentazione |
| Thunderbolt | Dati, video e periferiche ad alta velocità |
| Ethernet | Rete cablata |
| Wi-Fi | Rete wireless |
| Bluetooth | Collegamenti wireless a breve distanza |
| I²C | Comunicazione tra circuiti integrati |
| SPI | Comunicazione seriale tra componenti elettronici |
| UART | Comunicazione seriale asincrona |

---
