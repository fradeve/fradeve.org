Title: My muttrc
Date:  2012-01-12 15:00:00
tags: mutt, mail,

_AGGIORNAMENTO: una nuova versione di questo script è disponibile e spiegata ampiamente in [questo][update] post._

A grande richiesta, il mio `muttrc` per gestire due account (uno su Gmail e l'altro su [www.autistici.org][1]). Qualche chicca, spiegata:

 * `set editor` richiama uno script che esegue dei comandi in Vim che permettono di settare dei parametri all'interno della mail prima ancora che l'editor si apra;
 * `unset metoo` permette di evitare che il mio indirizzo email finisca nei destinatari quando rispondo ad una mail in cui sono stato messo in CC o tra i destinatari;
 * `set query_command` permette di aprire [goobook][2] per cercare gli indirizzi nella copia in locale della mia rubrica di Gmail;
 * `set print_command` rende accattivante la stampa delle mail utilizzando a2ps;
 * `set my_pass1` è un comando che lancia awk su un file nella mia home criptata, contenente le password degli account (utile quando si intende conservare il proprio muttrc in una cartella non cifrata: le password sono al sicuro);
 * `imaps://francesco.devirgilio@inventati.org@mail.autistici.org` le impostazioni dell'account imap per Austistici/Inventati; ci ho messo un bel po' a trovare la retta via, considerato che le indicazioni sull'accesso ad IMAP tramite Mutt sul sito di A/I sono molto generiche;
 * `macro index y` e seguenti, permettono di cambiare rapidamente account con la semplice pressione in successione di alcuni tasti;
 * `macro pager G` è un comando studiato per copiare la mail cifrata in una certa cartella, la decifra con la propria chiave privata, la apre ed all'uscita dal visualizzatore elimina il file decifrato;
 * `macro index Z` e seguente, permette di scaricare in blocco tutti gli allegati da una mail;
 * `macro index .r` permette di segnare come lette tutte le mail nella cartella corrente.

Ci sono tante altre funzioni integrate in questo muttrc, ma niente che non si trovi anche altrove sulla rete.

   [1]: http://www.autistici.org
   [2]: https://code.google.com/p/goobook/
   [update]: [[log/2012/03/muttrc-take-2.html]]