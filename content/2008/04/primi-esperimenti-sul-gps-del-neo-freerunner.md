Title: Primi esperimenti sul GPS del Neo FreeRunner
Date:  2008-04-29 21:41:41
tags: freerunner, nokia, openmoko,

{% from "macros.j2" import render_image %}

Uno studente dell'Europa dell'Est (o per lo meno
così sembra dal nome) [Andrzej "balrog-kun" Zaborowski][1], ha avuto la
geniale idea di mettere nel proprio zaino un Neo1973 (GTA01), un[ Neo
FreeRunner][2] (GTA02) ed un N800, attivando il tracking del GPS e catturando
in questo modo i file .GPX delle strade che ha percorso nel giro di qualche
ora. I risultati sono piuttosto incoraggianti, per essere il Neo un
dispositivo ancora in fase di sviluppo; tuttavia, i 3 hanno catturato una
diversa "lunghezza" del percorso pur essendo stati trasportati tutti insieme
nello stesso percorso.

 * GTA01: 11.28km
 * GTA02: 12.12km
 * N800: 11.07km

Da queste cifre si desume chiaramente che non tutti i dispositivi recepiscono
alla stessa maniera il segnale GPS, e addirittura il FreeRunner ha "catturato"
quasi 1 km in più dell'N800. Per esperienza, ho notato che l'N800 non ha una
ricezione GPS "splendida": dalle mie parti ci mette molto tempo ad agganciare
i satelliti e spesso perde la connessione. Comunque, il nostro amico ha
caricato sul suo blog i tracciati GPX, che mi son preso la libertà di caricare
in [JOSM][3], un programma usato dagli [OpenStreetMap][4] per elaborare le
tracce che poi verranno caricate sui server del progetto. Questa è la mappa
con i 3 percorsi catturati dai 3 dispositivi, elaborata su JOSM da Andrzej:

{{ render_image('', 'josmsr5.png', 'alt description', '') }}

Questi di seguito invece sono degli screenshot di JOSM su cui ho caricato i 3 GPX.
Ho fatto delle foto ravvicinate per mettere in evidenza la scala (in alto a
sinistra) con cui sono state effettuate le misurazioni; la legenda è la
seguente:

  * GTA01 = BLU
  * GTA02 = VERDE
  * Nokia N800 = ROSSO

{{ render_image('', 'osmneo1mdu6.png', 'alt description', '') }}

In questa immagine il Neo1973 e il Neo FreeRunner hanno catturato due
serie di coordinate molto vicine tra loro (con uno scarto di circa 25 cm),
però entrambe distanti dall'N800 di circa 1 metro se non di più.

{{ render_image('', 'osmneo2mog7.png', 'alt description', '') }}

In questa
situazione i 3 dispositivi hanno registrato uno scarto quasi uguale, di circa
1 m.

{{ render_image('', 'osmneo3mml1.png', 'alt description', '') }}

Qui la situazione cambia: il FreeRunner sembra essere completamente
sballato rispetto al Neo1973 GTA01 e all'N800, che invece hanno registrato
quasi esattamente le stesse coordinate. Tra questi ed il FreeRunner c'è uno
scarto di circa 3 m.

{{ render_image('', 'osmneo3m2bz1.png', 'alt description', '') }}

Qui la situazione comincia a farsi complicata: a
quanto pare il FreeRunner tende ad "amplificare" le coordinate che riceve,
registrando lo stesso percorso dell'N800, ma "traslando" i valori e
spostandoli. In questo caso, la differenza è parecchia: tra FreeRunner ed N800
ci sono più di 5m.

{{ render_image('', 'osmneo4m3wv6.png', 'alt description', '') }}

In questo screen si comprende meglio cosa intendevo
con "amplificare" e "traslare" nell'immagine precedente.

{{ render_image('', 'osmneo6mik3.png', 'alt description', '') }}

Qui invece l'amplificazione diventa non solo
evidente, ma spaventosa.

## Conclusioni ##

Credo si possa dire che sulla questione GPS del Neo c'è
ancora un po' da lavorare. I driver GPS sono chiusi (i cosiddetti **gllin**) e
qualcuno ha detto che in città è riuscito ad usarlo come navigatore con un
errore di 1 m circa. Senza dubbio, questo non è stato un esperimento
scientifico, ma una dimostrazione "amatoriale". Aspettiamo quindi ulteriori
sviluppi e dimostrazioni. Intanto, l'entrata in vendita del Neo FreeRunner si
fa sempre più vicina ;)

   [1]: http://unadventure.wordpress.com/2008/04/28/unscientific-gps-note/

   [2]: http://fradeve.org/log/2008/04/le-sbalorditive-prestazioni-gps-del-neo-freerunner.html

   [3]: http://wiki.openstreetmap.org/index.php/It:JOSM

   [4]: http://www.openstreetmap.org/