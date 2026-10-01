# 9. Avvio e gestione della macchina virtuale

Una macchina virtuale può trovarsi in diversi stati.

Tra i principali:

-   spenta;
-   in esecuzione;
-   in pausa;
-   salvata.

Quando possibile, una VM Linux deve essere spenta attraverso il normale
sistema operativo.

Per esempio:

``` bash
sudo shutdown now
```

oppure:

``` bash
sudo poweroff
```

Lo spegnimento forzato deve essere evitato quando non necessario, perché
equivale a interrompere bruscamente l'alimentazione di un computer.

------------------------------------------------------------------------
