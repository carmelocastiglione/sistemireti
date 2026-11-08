# 8. La trasmissione in fibra ottica

La **fibra ottica** trasporta informazioni mediante impulsi di luce. La luce resta confinata nel nucleo grazie alla differenza di indice di rifrazione tra nucleo e mantello e al fenomeno della riflessione interna totale, quando sono rispettate le condizioni fisiche richieste.

## Struttura e principi dell'ottica

Una fibra è composta principalmente da:

- **nucleo (core)**: regione in cui si propaga la luce;
- **mantello (cladding)**: circonda il nucleo e favorisce il confinamento ottico;
- **rivestimenti protettivi**: proteggono la fibra da umidità, piegature e danni meccanici.

La luce può propagarsi lungo percorsi o modi diversi. Piegature eccessive, giunzioni o impurità possono causare perdite; connettori e terminazioni devono mantenere pulite le superfici ottiche.

## Fibre monomodali e multimodali

- **Multimodale (MMF)**: il nucleo è più ampio e consente la propagazione di più modi. È usata spesso per collegamenti relativamente brevi, per esempio all'interno di edifici o data center.
- **Monomodale (SMF)**: il nucleo è più piccolo e propaga essenzialmente un solo modo. È adatta a collegamenti più lunghi e ad alte capacità.

Distanza e prestazioni dipendono anche da lunghezza d'onda, apparati, qualità delle giunzioni e specifiche del sistema: la sola etichetta della fibra non determina la portata.

## Connettori ottici

I connettori terminano le fibre e ne allineano con precisione i nuclei. Tra i tipi diffusi si trovano **LC**, **SC** e **ST**. Possono inoltre essere classificati per forma della superficie di contatto, ad esempio PC/UPC o APC, che non sono sempre intercambiabili.

Polvere e graffi possono degradare il collegamento. Le estremità vanno ispezionate e pulite con strumenti appositi; non si deve guardare direttamente dentro una fibra o una porta ottica attiva.

## Sistema di trasmissione ottico

```text
dati → trasmettitore ottico → fibra → ricevitore ottico → dati
```

- Il **trasmettitore** converte i dati elettrici in un segnale luminoso, usando tipicamente un LED o un laser secondo il sistema.
- La **fibra** trasporta gli impulsi luminosi, con perdite e dispersione dipendenti dal mezzo e dalla distanza.
- Il **ricevitore** rileva la luce con un fotodiodo e ricostruisce il segnale elettrico e i dati.

Per collegamenti molto lunghi o sistemi ad alta capacità possono essere necessari amplificatori ottici, rigeneratori o apparati di multiplexing. La fibra non è soggetta alle interferenze elettromagnetiche che influenzano i cavi in rame ed è difficile da intercettare senza accesso fisico, ma non è automaticamente sicura: occorrono protezioni e controlli adeguati.

---
