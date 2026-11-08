# 11. Le commutazioni

La **commutazione** è l'insieme delle operazioni che trasferiscono dati attraverso una rete usando nodi intermedi. Due modelli fondamentali sono la commutazione di circuito e quella di pacchetto.

## Circuit switching

Nella **commutazione di circuito**, prima della comunicazione viene stabilito un percorso o una risorsa dedicata tra i due estremi. La rete mantiene lo stato della connessione per la durata della sessione.

**Vantaggi**

- risorse e percorso sono predisposti per la comunicazione;
- ritardo e capacità possono essere più prevedibili quando le risorse sono riservate.

**Svantaggi**

- le risorse possono restare occupate anche quando non vengono inviati dati;
- instaurare il circuito richiede una fase preliminare;
- un guasto lungo il percorso può interrompere la comunicazione.

La telefonia tradizionale è un esempio classico di rete a commutazione di circuito.

## Packet switching

Nella **commutazione di pacchetto**, i dati vengono suddivisi in pacchetti che condividono i collegamenti con il traffico di altri utenti. Ogni pacchetto contiene informazioni necessarie al trasferimento e può attraversare nodi intermedi.

Nella modalità **datagramma** ogni pacchetto viene inoltrato in modo indipendente: pacchetti della stessa comunicazione possono seguire percorsi diversi e arrivare fuori ordine. Nelle reti a **circuito virtuale** si stabilisce invece un percorso logico, pur continuando a trasmettere pacchetti e a condividere le risorse fisiche.

**Vantaggi**

- uso efficiente dei collegamenti condivisi, soprattutto quando il traffico è intermittente;
- capacità di instradare i pacchetti intorno ad alcuni guasti;
- possibilità di servire molte comunicazioni sulla stessa infrastruttura.

**Svantaggi**

- ritardo e throughput possono variare con la congestione;
- i pacchetti possono essere persi, duplicati o riordinati;
- protocolli di livello superiore possono dover gestire affidabilità e ordinamento.

Internet usa la commutazione di pacchetto. Circuit switching e packet switching descrivono il modo in cui la rete gestisce le risorse e trasferisce i dati, non il tipo di cavo impiegato.

---
