# Sistemi e Reti --- Capitolo 2: Virtualizzazione e macchine virtuali

## Introduzione

La virtualizzazione è una delle tecnologie fondamentali per comprendere
il funzionamento dei moderni sistemi informatici e delle infrastrutture
di rete.

Nel capitolo precedente abbiamo analizzato il **sistema di
elaborazione**, osservando come CPU, memoria, dispositivi di memoria,
periferiche e sistema operativo collaborino per permettere a un computer
di eseguire programmi.

In questo capitolo introduciamo un livello ulteriore di astrazione: la
**macchina virtuale**.

Una macchina virtuale permette di simulare, all'interno di un computer
fisico, un altro computer completo dal punto di vista logico. La
macchina virtuale possiede infatti una propria CPU virtuale, memoria
virtuale, disco virtuale, scheda di rete virtuale e sistema operativo.

Per le attività di laboratorio utilizzeremo **VirtualBox**, che si
assume già installato sul computer.

Il laboratorio utilizzerà una distribuzione Linux leggera, senza
interfaccia grafica, in modo da concentrarsi sui concetti di sistema
operativo, amministrazione e rete.

------------------------------------------------------------------------

## Sezioni

- [La virtualizzazione](01-la-virtualizzazione.md)
- [Perché utilizzare una macchina virtuale?](02-perche-utilizzare-una-macchina-virtuale.md)
- [Macchina fisica e macchina virtuale](03-macchina-fisica-e-macchina-virtuale.md)
- [L'hypervisor](04-l-hypervisor.md)
- [VirtualBox](05-virtualbox.md)
- [Creazione della macchina virtuale](06-creazione-della-macchina-virtuale.md)
- [Installazione di Linux](07-installazione-di-linux.md)
- [Configurazione della macchina virtuale](08-configurazione-della-macchina-virtuale.md)
- [Avvio e gestione della macchina virtuale](09-avvio-e-gestione-della-macchina-virtuale.md)
- [Snapshot e cloni](10-snapshot-e-cloni.md)
- [Le reti virtuali](11-le-reti-virtuali.md)
- [Laboratorio: VirtualBox e Linux](12-laboratorio-virtualbox-e-linux.md)
