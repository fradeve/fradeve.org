Title: Installare TeXLive da CTAN su Ubuntu Lucid
Date:  2010-08-10 10:10:31
featured: yes
tags: ubuntu, latex, gnulinux,

_L'articolo è stato aggiornato dopo la pubblicazione iniziale_

<center><img src="http://www.sitmo.com/gg/latex/latex2png.2.php?z=120&eq=S_%7Br%7D%3D%5Cfrac%7BV_%7Bw%7D%7D%7BV_%7Bv%7D%7D%3D%5Cleft%5C%7B%5Cfrac%7BG_%7Bw%7D%5Ccdot%20w%7D%7Be%7D%5Cright%5C%7D"></center>

_Per i puristi del TeX: in questo post cerco di semplificare la situazione per
i niubbi come me, abbiate pazienza :) Aggiungo anche: questa guida è stata
scritta un mesetto dopo aver fatto esperienza con TeXLive, se c'è qualche
errore segnalatemelo! Il tutto è da intendersi testato su Ubuntu Lucid._


Recentemente, grazie a qualche dritta da parte di un "passante", [Roberto][1] (il
cui blog è vivamente consigliato a tutti gli appassionati _LaTeXsisti_),
e motivato da qualche [disavventura][2], ho scoperto un sistema alternativo
per l'utilizzo di TeXLive su Ubuntu/Debian. In effetti, senza niente togliere
al fantastico lavoro dei contributor e dei mantainer Debian/Ubuntu, trovo
inefficiente la gestione dei pacchetti LaTeX. Ma andiamo con ordine.


[LaTeX][3] è un linguaggio di markup per la redazione di documenti
professionali, particolarmente utile in ambito scientifico perché permette di
ottenere risultati incomparabili rispetto a qualsiasi altro editor per
qualità, semplicità ed efficienza del sistema. LaTeX è distribuito in
pacchetti, ognuno dei quali ha una propria funzione. I pacchetti sono
organizzati in un repository online ([CTAN][4], Comprehensive TeX Archive
Network). Debian non fa altro che creare raccolte di questi pacchetti in base
alle loro funzioni, e li distribuisce. Com'è ovvio, i pacchetti vengono
aggiornati molto più spesso di quanto la stessa Debian non faccia, ma
utilizzando i pacchetti della distribuzione ci si costringe a "congelare" la
propria versione dei pacchetti LaTeX per uno o due anni, rinunciando alle
features che possono essere introdotte nel frattempo.


Partendo da CTAN, su
base annuale vengono sfornate distribuzioni di pacchetti LaTeX, tra le quali
le più famose sono TeXLive (per Unix) e MikTeX (per Linux). E installare
TeXLive dai repository di Debian, come abbiamo visto sopra, è forse la maniera
più inefficiente di gestire uno strumento che si aggiorna molto più
frequentemente di quanto la stessa Debian non faccia. Ma lo svantaggio è anche
un altro: ogni pacchetto di TeXLive in Debian contiene per ovvie ragioni
decine di pacchetti LaTeX, molti dei quali probabilmente a noi non servono ed
occupano solo spazio sul disco fisso (sul PC di casa possiamo anche
soprassedere, ma vogliamo parlare di quanto spazio TeXLive si mangia sul
netbook?). Quindi, o tutto o niente: su Debian non è possibile installare da
repository solo il pacchettino LaTeX che ci interessa per le funzioni
matematiche, tocca beccarci tutto il "latex-science", con decine di tool che
non useremo mai.

## Come risolvere? ##
Semplice: disinstalliamo i pacchetti TeXLive
di Debian e facciamo partire l'installer di TeXLive per Unix/Linux.

	sudo apt-get remove --purge texlive*

È probabile che con
TeXLive vengano disinstallati anche altri programmi che su questo si
appoggiavano, come LyX o Kyle. Non ci pensate, risolveremo dopo, anche perché
solo TeXLive verrà rimosso integralmente con tutti i suoi file di
configurazione, mentre LyX e gli altri verranno rimossi in maniera "soft",
mantenendo tutte le impostazioni e configurazioni, che ritroveremo dopo una
nuova installazione.


A questo punto puliamo anche tutti i file della vecchia
TeXLive:

	sudo rm -r /usr/share/texmf

Scarichiamo ed estraiamo l'installer da rete di TeXLive:

	wget http://ftp.uniroma2.it/TeX/systems/texlive/tlnet/install-tl.zip
	unzip install-tl.zip
	rm install-tl.zip

Adesso siamo pronti ad installare le librerie
Wx di Perl per avviare l'interfaccia grafica dell'installer, e far partire
l'installazione. L'installazione dei pacchetti avviene interamente scaricando
i vari file da internet, quindi assicuratevi di poter tenere acceso il PC
anche per mezza giornata (a seconda della quantità di pacchetti di default che
vorrete installare, ed in funzione della velocità della vostra connessione).
Il "sudo" dell'ultimo comando è importante perché l'installazione di default
di TeXLive è in una cartella di sistema (`/usr/local/texlive` per la
precisione).

	sudo apt-get install libwx-perl perl-tk
	cd install-tl*
	sudo perl install-tl --gui -repository ftp://ftp.snt.utwente.nl/pub/software/tex/systems/texlive/tlnet/

Le opzioni da selezionare in questa fase sono altamente soggettive, ma grossomodo:

  * _Schemi selezionati_: evitate scheme-full, installerà l'intera TeXLive, son
diversi Gib e probabilmente non vi servirà mai tutto; basic-scheme per la mia
esperienza è andato più che bene.

  * _collezioni di base_: permette di selezionare collezioni di pacchetti da
installare in base alle loro funzioni; consigliati quelli scientifici, quelli
per la grafica e quelli relativi alle bibliografie; se avete paura di mettere
troppo o troppo poco, non vi preoccupate, TeXLive è cosi flessibile che dopo
potrete aggiungere/rimuovere pacchetti senza sforzo e senza sporcare il
sistema.

  * _collezioni di lingue_: spuntate solo quelle che realmente vi interessano
(italiano, inglese, francese, tedesco, spagnolo, latino, ecc.)

  * _installa la documentazione per font e macro_: ho inserito "No" e vivo
benissimo; idem per "Installa i sorgenti per font e macro";

  * _crea i collegamenti nelle directory di sistema_: cambiando in "Si",
e spuntando anche "_crea i collegamenti simbolici nelle directory standard_", 
TeXLive installerà dei link nella propria cartella degli eseguibili (solitamente
`/usr/bin`), utile per avere tutti i comandi di LaTeX a portata di mano anche dal terminale;
sarebbe una scelta consigliata, se non fosse per il fatto che ciò sporca la suddetta
cartella. Meglio è (come suggerito da RobiTeX) esportare il $PATH nel proprio file
`.profile` così da mantenere tutti i file in `/usr/local`: ciò creerà meno problemi in fase
di aggiornamento.

		echo 'export PATH=/usr/local/texlive/2010/bin/i386-linux:${PATH}' >> .profile

Considerato che gli eseguibili d'ora in poi saranno in tale percorso, è comodo utilizzare un alias
per tlmgr, visto che tutte le operazioni andranno svolte con i permessi di amministratore:

		alias sutlmgr='sudo /usr/local/texlive/2010/bin/i386-linux/tlmgr'


Non resta che avviare l'installazione con "Installa TeXLive". Al termine,
avrete un sistema LaTeX personalizzato, perfettamente funzionante, flessibile
e decisamente più leggero di quello installabile dai pacchetti Debian. Nei
prossimi post vedremo come installare/rimuovere pacchetti LaTeX, come
aggiornarli o esportare la lista dei pacchetti installati per l'installazione
speculare su un'altra macchina.

## Aggiornamento annuale ##
TeXLive esce in una nuova versione ogni anno. Di seguito i passi per aggiornare
la propria distribuzione.

 * recarsi nella cartella di installazione e creare una copia di backup della propria installazione:

		sudo cp -a 2010 2011

 * per risparmiare dello spazio, eliminare il contenuto della cartella dei backup annui della distribuzione vecchia:

		sudo rm /usr/local/texlive/2011/tlpkg/backups/*

 * modificare l'anno della distribuzione nei file `.profile` e `.bashrc` da 2010 a 2011

 * avviare tlmgr, caricare l'archivio di default (definito al momento dell'installazione) ed eseguire l'aggiornamento di tlmgr:
		
		sutlmgr --gui

 * aggiornare i pacchetti con il comando classico:

		sutlmgr update --all

 * dopo aver provato a compilare qualche documento, se tutto funziona bene, potrete anche eliminare la distribuzione vecchia:

		sudo rm -r /usr/local/texlive/2010

## Ringraziamenti ##
Si ringraziano Alvise e [Sdonk][5] per i preziosi suggerimenti.


   [1]: http://robitex.wordpress.com/

   [2]: http://dl.dropbox.com/u/369614/blog/public_html/FradeveOpenblog/posts/2010/07/usare-il-pacchetto-latex-xfrac-su-ubuntu-lucid.html

   [3]: http://it.wikipedia.org/wiki/Latex

   [4]: http://www.ctan.org/

   [5]:http://blog.sdonk.org/ 