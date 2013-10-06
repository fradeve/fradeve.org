Title: How do I blog?
Date:  2011-03-06 15:55:00
tags: socialnetwork, blog, ubuntu,
lastupdated: 2012-08-03

## Pippe ##

[Per molto tempo][casa] questo blog è servito ad unico scopo: tenere aggiornata la comunità di Ubuntu-it sull'andamento delle attività nei vari progetti in cui ero coinvolto: gruppo promozione, gruppo documentazione, wiki di Ubuntu-it, ecc. Non a caso è nato in contemporanea con il mio ingresso nella Comunità. Con il passare degli anni, è diventato molto di più: un sistema per condividere annunci, esperienze, riflessioni, appuntamenti con gli eventi della Cultura Libera, ecc.

Ad un certo punto dello sviluppo di internet, ogni progetto aderente alla cultura del _Free Software_ si è adeguato alla necessità di raccogliere le testimonianze e gli aggiornamenti all'interno di un blog o di un planet, moltiplicando le fonti e le novità relative al tema in questione.

Con il tempo, anche le mie esigenze sono cambiate, ed in questi mesi si stanno evolvendo rapidamente anche le necessità di postare miei articoli, non inerenti le attività all'interno della comunità di Ubuntu, su altri blog. Quando si gestiscono blog in collaborazione con altre persone (come nel caso del [blog dei rappresentanti del corso di laurea][2] nel quale scrivo) non si può chiaramente obbligare tutti ad utilizzare Ikiwiki, e così si sceglie una comoda installazione di Wordpress. D'altro canto, non ho nessuna intenzione di:

* rinunciare allo straordinario combo: Ikiwiki + GIT + Vim + rsync;
* disperdere i miei articoli; desidero che ne resti una copia comunque sul mio blog.

Considerato che il blog dei rappresentanti non sarà l'unico blog nel quale andrò a postare quest'anno, come risolvere? E soprattutto, come evitare che lunghi e noiosi post riguardanti le attività didattiche del mio corso di laurea inquinino l'interessantissimo planet di Ubuntu-it?

La soluzione è arrivata da un semisconosciuto servizio di Yahoo!, [_Pipes_][3], un efficace strumento online per la creazione di sistemi che gestiscono, smistano, filtrano informazioni di tipo testuale e soprattutto caratterizzate da una sintassi ordinata (come quella dell'XML). Su Pipes ho appunto [creato][4] un semplicissimo filtro per il mio feed RSS principale, dal quale vengono esclusi tutti i post taggati con [diagnostica][diagnostica]. In questo modo il feed finale risulterà pulito e potrà arricchire il planet di Ubuntu-it.

Certo, la pipe è ancora da migliorare, ma per cominciare mi sembra un'ottima soluzione :)

## Configurazioni dei feed ##

Da qualche tempo, Facebook si rifiuta di importare i miei post dal feed RSS/Atom generato da Ikiwiki, restituitendomi un sempreverde "Import failed - We couldn't find a feed using the URL you provided.". Ottimo. Pensando che Ping.fm potesse venirmi in aiuto importando i feed RSS dal blog e rispammandoli su Facebook, ho scoperto con gran rammarico che anche Ping.fm dai primi giorni del 2011 si sta impegnando per fornire disservizi (d'altro canto, è gratis, quindi di cosa ci lamentiamo?).

E allora?

Allora ho deciso di attivare un account su [Twitterfeed][6], che ogni mezz'ora parsa i feed sia del blog che degli elementi condivisi di Google Reader (altro servizio che Ping.fm allegramente condivideva sul mio account di Facebook) e li riversa nei maggiori social network ai quali sono iscritto: Facebook, Twitter, Identi.ca.

Questo basta? No. Per giocare un po' con [Graphviz][7] (cosa che volevo fare da tempo) ho deciso di riassumere questo bel giochetto in un grafico, il cui codice è riportato di seguito. Per _pingare_ da cellulare invio una email da un altro account di posta su Gmail, che viene filtrata e spostata in una certa cartella, il cui feed RSS viene dato in pasto a [Brdcst it!][9] che lo posterà sui vari social network. I feed provenienti dal blog e dagli articoli condivisi sul mio aggregatore di feed RSS devono passare prima da [FeedBurner][10] per essere formattati in Atom (invece che RSS) prima di essere inoltrati via Brdcst. Purtroppo Brdcst non inoltra verso Linkedin, per cui i retweet (Twitter RT, presi via RSS pubblico) devono passare a questo scopo attraverso [Iffft][11]. Tutti i servizi in verde sono realizzati utilizzando software libero, quelli in rosso sono proprietari.

<center>![][8]<br>_Collegamenti tra i vari servizi di social networking_</center>

    digraph G {
        graph [ dpi = 300 ];
        // table size
        size ="4,6";
        rankdir=RL;

        //// LABELING ////

        // means
        ttrss [label="TT-RSS",shape=record,color=green]
        brdcst [label="brdcst \nit!", shape=record,color=green]
        ifttt [label="ifttt", shape=record,color=red]
        pipes[label="Yahoo! \nPipes",shape=record,color=red]
        identicapubfeed [label="Identi.ca\npublic feed",shape=record,color=green]

        // sources
        ttrssshared [label="TT-RSS \nshared",shape=egg,color=green]
        blog [label="Fradeve \nOpenblog",shape=egg,color=green]
        mobile [label="mobile \ninput \n(identi.ca web)",shape=egg,color=green]
        desktop [label="bitlbee",shape=egg,color=green]
        github [label="GitHub \nactivity",shape=egg,color=green]
        twitter [label="Twitter RT",shape=egg,color=red]
        flickr [label="Flickr shared",shape=egg,color=red]

        // destinations
        identica [label="Identi.ca",color=green]
        linkedin [label="Linkedin \nstatus update",color=red]
        facebook [label="Facebook \nstatus update",color=red]
        planetub [label="planet Ubuntu-it",shape=tab,color=green]
        oiablog [label="Blog O.I.A.",shape=tab,color=green]
        pubwich [label="Pubwich\nfork",shape=tab,color=green]

        //// CONNECTIONS ////

        // ping
        mobile -> identica [arrowhead=dot, color=darkorange];
        desktop -> identica [arrowhead=dot, color=darkorange];
        identica -> identicapubfeed [arrowhead=dot, color=darkorange];
        identicapubfeed -> brdcst [arrowhead=dot, color=darkorange];
        brdcst -> facebook [arrowhead=dot,color=darkorange];
        identicapubfeed -> pubwich [arrowhead=dot,color=darkorange];

        // connecting aggregators to blog
        blog -> planetub [arrowhead=crow];
        blog -> oiablog [arrowhead=crow];

        // blog
        subgraph cluster_drop {
            style=filled;
            color=grey;
            label = "blog";

            blog -> pubwich
        }

        // RSS shared
        ttrss -> ttrssshared [color=orchid];
        ttrssshared -> pubwich [color=orchid];

        // GitHub
        github -> ifttt -> linkedin [style=bold,color=blue];
        github -> pubwich [style=bold,color=blue];

        // Twitter
        twitter -> pipes -> brdcst -> facebook;
        brdcst -> identica;
        pipes -> pubwich;
        
        //Flickr
        flickr -> pubwich
    }

Il comando per generarlo partendo dal file `graph.dot`:

	dot graph.dot -Tpng -o hello.png

   [casa]: [[log/2007/09/finalmente-a-casa.html]]
   [2]: http://www.tecnologiebcuniba.org/wordpress/
   [3]: http://pipes.yahoo.com/
   [4]: http://pipes.yahoo.com/pipes/pipe.info?_id=71bcdf728b59016dd430d09863e0f731
   [diagnostica]: [[tags/diagnostica.html]]
   [6]: http://twitterfeed.com
   [7]: http://www.graphviz.org/
   [8]: http://dl.dropbox.com/u/369614/blog/img_red/dot_sn.png
   [9]: http://www.brdcst.it 
   [10]: http://feedburner.google.com 
   [11]: http://www.iffft.com 
