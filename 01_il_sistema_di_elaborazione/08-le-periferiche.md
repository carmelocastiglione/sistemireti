# 8. Le periferiche
## Approfondimento: controller e driver

Una periferica non è normalmente controllata dalla CPU attraverso semplici istruzioni generiche. Tra sistema operativo e dispositivo intervengono spesso:

1. **driver**;
2. **controller**;
3. **interfaccia hardware**;
4. **protocollo di comunicazione**.

Il **driver** è il componente software che permette al sistema operativo di utilizzare una specifica classe o modello di dispositivo.

Il **controller** è invece una componente hardware/elettronica che gestisce il funzionamento del dispositivo o dell'interfaccia.

### Interrupt

Le periferiche devono poter segnalare alla CPU che un evento richiede attenzione.

Gli **interrupt** permettono a un dispositivo di richiamare l'attenzione del processore.

Per esempio:

```text
tastiera → viene premuto un tasto
        → controller genera un evento
        → interrupt
        → CPU esegue il gestore appropriato
```

In questo modo la CPU non deve interrogare continuamente la periferica chiedendo se è successo qualcosa.

### Polling

Nel **polling**, invece, la CPU o il software verifica periodicamente lo stato della periferica.

| Metodo | Caratteristica |
|---|---|
| Polling | Il processore controlla periodicamente |
| Interrupt | La periferica segnala quando necessario |
| DMA | Il trasferimento di blocchi può essere eseguito senza coinvolgere la CPU per ogni singolo dato |


Una **periferica** è un dispositivo che permette al sistema di elaborazione di interagire con l'esterno.

## 8.1 Periferiche di input

Forniscono dati al computer.

| Periferica | Funzione |
|---|---|
| Tastiera | Inserimento caratteri e comandi |
| Mouse | Puntamento e selezione |
| Scanner | Acquisizione immagini/documenti |
| Microfono | Acquisizione audio |
| Webcam | Acquisizione immagini/video |
| Sensore | Acquisizione di grandezze fisiche |

---

## 8.2 Periferiche di output

Presentano informazioni all'esterno.

| Periferica | Funzione |
|---|---|
| Monitor | Visualizzazione |
| Stampante | Stampa |
| Altoparlanti | Riproduzione audio |
| Proiettore | Visualizzazione su grande schermo |

---

## 8.3 Periferiche di input/output

Possono sia ricevere sia trasmettere dati.

| Periferica | Input | Output |
|---|---|---|
| SSD/HDD | Sì | Sì |
| Scheda di rete | Sì | Sì |
| Modem | Sì | Sì |
| Touchscreen | Sì | Sì |
| Scheda audio | Sì | Sì |

---
