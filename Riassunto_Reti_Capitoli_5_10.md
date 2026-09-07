# Riassunto Approfondito: Reti di Calcolatori (Capitoli 5-10)

> Questo secondo blocco si concentra sulle logiche interne della comunicazione affidabile (Livello di Trasporto) e sull'instradamento globale (Livello di Rete). Include le formule e gli algoritmi matematici richiesti all'esame.

---

## 5. Programmazione di Rete con i Socket
Le socket rappresentano l'**API (Application Programming Interface)** fornita dal sistema operativo (Livello di Trasporto) alle Applicazioni.
In ambienti Unix/POSIX, le socket seguono il paradigma *"tutto è un file"* e sono gestite tramite un file descriptor intero (FD).

### Flusso Socket UDP (Connectionless)
Essendo privo di connessione, un server UDP non crea una nuova socket per ogni client. Ne mantiene una sola aperta su cui convergono tutti i datagrammi diretti a quella porta.
- **Primitive base**: `socket()` (creazione), `bind()` (obbligatoria sul server per assegnare IP e Porta locale), `sendto()` (invia dati includendo l'indirizzo destinazione), `recvfrom()` (riceve dati restituendo anche l'indirizzo del mittente).

### Flusso Socket TCP (Connection-oriented)
TCP richiede un *three-way handshake* prima di poter trasmettere payload. Per questo motivo, **il server TCP fa uso di due tipi di socket**:
1. **Welcoming Socket**: Esegue il `bind()` alla porta pubblica e ascolta passivamente tramite `listen()`. Il suo unico scopo è gestire le richieste di handshake in arrivo.
2. **Connection Socket**: Quando l'handshake è accettato, la funzione `accept()` genera al volo una **nuova socket dedicata** specificamente a quel particolare client. Da questo momento, i dati scorrono su questa connessione dedicata usando `send()` e `read()`.

---

## 6. Il Livello di Trasporto: UDP e Trasferimento Affidabile (RDT)
Mentre il Livello di Rete si assicura che il pacchetto arrivi dalla macchina A alla macchina B (host-to-host delivery), il Livello di Trasporto usa **Multiplexing e Demultiplexing** (tramite le Porte) per distribuire i pacchetti all'interno della macchina B al processo corretto (process-to-process delivery).

### L'approccio essenziale: UDP
**UDP (User Datagram Protocol)** si limita al multiplexing/demultiplexing e a un semplice **Checksum** per l'integrità, ereditando tutte le inaffidabilità del livello IP sottostante.
- **Vantaggi**: Nessun ritardo di connessione (ideale per DNS), header leggerissimo da soli **8 byte** (contro i 20B di TCP), nessun limite imposto su quanto velocemente l'applicazione può iniettare dati in rete (il Rate control è applicativo, ideale per lo streaming real-time).
- **Algoritmo di Checksum**: Si raggruppano i dati in blocchi da 16 bit e se ne fa la somma (aggiungendo il riporto eccedente ai 16 bit al totale). Il checksum è il *complemento a 1* del risultato. 

### RDT: Reliable Data Transfer (Trasferimento Affidabile)
Costruire un canale affidabile su Internet (che fa drop, duplicazione e riordinamento) richiede quattro elementi logici: *Sequence Numbers, Timer, ACK/NAK, e Buffer*.

#### Protocolli Pipelined: Go-Back-N (GBN) vs Selective Repeat (SR)
Il protocollo basilare *Stop-and-Wait* attende l'ACK di ogni singolo pacchetto prima di procedere. È lentissimo. Si risolve inviando una finestra di $N$ pacchetti simultanei (Pipelining).
1. **Go-Back-N (GBN)**: 
   - Il ricevente ha buffer zero: accetta i pacchetti **solo in ordine sequenziale perfetto**. Se ne arriva uno fuori ordine, lo droppa.
   - Il ricevente usa **ACK cumulativi**: "ho ricevuto in ordine tutto fino al byte X".
   - Il mittente mantiene un solo timer (per il primo pacchetto non-ACKato). Se scade, il mittente **ritrasmette l'intera finestra** dal pacchetto perso in poi (inefficiente su reti affollate).
2. **Selective Repeat (SR)**:
   - Il ricevente ha un buffer e accetta pacchetti fuori ordine, confermandoli con **ACK singoli/individuali**.
   - Il mittente ha un timer per *ogni* pacchetto in volo. Se scade un timer, **ritrasmette solo quel singolo pacchetto**.
   - *Vincolo Matematico*: Per evitare che pacchetti vecchi si sovrappongano ai nuovi (Aliasing), lo spazio totale dei numeri di sequenza disponibili deve essere almeno il doppio della dimensione della finestra: $Spazio \geq 2 \times Finestra$.

---

## 7. Il Protocollo TCP in Dettaglio
**TCP** implementa i concetti teorici del Trasferimento Affidabile in un protocollo industriale full-duplex, point-to-point e basato su un flusso di byte (stream-oriented).

### Struttura del Segmento TCP e Sequence Numbers
- **MSS (Maximum Segment Size)**: È la grandezza del payload massimo inseribile in TCP, derivato dalla MTU della scheda di rete meno gli header IP e TCP (es. MTU 1500 - 40 = 1460 Byte di MSS).
- **Numerazione a Byte**: I *Sequence Number* (32 bit) in TCP **contano i singoli byte**, non i segmenti. Se si invia un file in blocchi da 1000 byte, i numeri di sequenza dei pacchetti saranno 0, 1000, 2000, 3000.
- **ACK Number (32 bit)**: Segnala al mittente il numero di sequenza del **prossimo byte che il ricevente si aspetta**. È un ACK di tipo *cumulativo*.
- **Piggybacking**: Dato che TCP è full-duplex, ogni segmento TCP che viaggia da B ad A può trasportare contemporaneamente dati (payload) verso A e l'ACK relativo all'ultimo pacchetto inviato da A.

### Gestione dei Timeout e RTT (Round Trip Time)
TCP stima l'RTT della rete campionandolo. Visto che la rete fluttua costantemente, usa una **Media Mobile Esponenziale Ponderata (EWMA)** per smussare i picchi:
$$EstimatedRTT = (1-\alpha) \cdot EstimatedRTT_{vecchio} + \alpha \cdot SampleRTT$$
Il Timeout è dinamico e impostato su $EstimatedRTT$ più un margine di sicurezza legato alla variabilità statistica ($4 \times DevRTT$).

**Fast Retransmit (Ritrasmissione Rapida)**:
Il Timeout calcolato è spesso superiore al secondo, troppo lungo se si perde un pacchetto in streaming. TCP sfrutta gli ACK per accorgersi in anticipo di un buco. Se il mittente riceve **3 ACK duplicati** di seguito (ovvero riceve per tre volte l'avviso che il ricevente sta aspettando lo stesso byte X), assume immediatamente la perdita del segmento e lo **ritrasmette istantaneamente**, saltando l'attesa del Timeout.

### Setup della Connessione
L'handshake è **A Tre Vie (Three-Way)** per aggirare il *Problema dei Due Eserciti*.
1. `SYN`: Client avvia (Seq=$X$, nessun dato).
2. `SYN-ACK`: Server risponde (Seq=$Y$, Ack=$X+1$).
3. `ACK`: Client conferma (Seq=$X+1$, Ack=$Y+1$, può includere dati).

*Nota Sicurezza*: Gli attacchi **SYN Flood (DDoS)** sfruttano il fatto che il server alloca buffer al passo 2, intasando la RAM. Si difende tramite **SYN Cookies** (non si alloca nulla finché non torna l'ACK finale).

La chiusura è un **Four-Way Teardown**, dove le due controparti usano indipendentemente il flag `FIN` per chiudere la propria direzione del tubo full-duplex.

---

## 8. Controllo di Flusso e Congestione (TCP Reno)
TCP risolve due problemi di inondazione del traffico che operano su scale diverse:

### Flow Control (Protezione del Ricevente)
Il problema è strettamente end-to-end. Il buffer dell'applicazione ricevente potrebbe riempirsi se il processo è impegnato.
**Meccanismo**: L'header TCP contiene un campo da 16 bit chiamato `Receive Window (rwnd)`. Ad ogni segmento di risposta, il ricevente scrive in `rwnd` quanto spazio libero gli è rimasto nel buffer. Il mittente si blocca se `rwnd` tocca zero (inviando *probe segments* da 1 byte per sbloccare la situazione quando il buffer si svuota).

### Congestion Control (Protezione della Rete)
Il problema coinvolge l'intera infrastruttura di internet: troppi host iniettano troppi dati, intasando le code dei router centrali, causando perdite prolungate e stalli.
**Meccanismo (Algoritmo di Jacobson - AIMD)**: Il mittente mantiene una variabile locale `Congestion Window (cwnd)`. La regola aurea di TCP è che i pacchetti in volo (*Unacked*) non possono superare il minimo tra rwnd e cwnd.
Il rate di invio si approssima con $\frac{cwnd}{RTT}$.
L'algoritmo regola `cwnd` seguendo un andamento a "dente di sega" (*Sawtooth*):

1. **Slow Start (Partenza Lenta ma esponenziale)**: Parte con $cwnd = 1 \text{ MSS}$. Per ogni ACK ricevuto `cwnd` sale di $1 \text{ MSS}$, causando il raddoppio della finestra ad ogni RTT. Questa fase cerca rapidamente il limite della banda, fermandosi quando tocca un valore soglia `ssthresh`.
2. **Congestion Avoidance (Incremento Lineare)**: Superata `ssthresh`, si sale cautamente aggiungendo $1 \text{ MSS}$ ogni RTT complessivo.
3. **Reazione alla Perdita (Loss Events)**:
   - Se c'è **Timeout** (congestione critica): `ssthresh` dimezza, ma `cwnd` viene **resettata a 1 MSS**. Si ricomincia dallo Slow Start.
   - Se ci sono **3 Dup-ACKs** (congestione lieve e Fast Retransmit): `ssthresh` dimezza, ma si entra nella fase di **Fast Recovery**. Anziché azzerare la `cwnd` a 1, la si imposta pari al nuovo `ssthresh + 3` e si riprende con crescita lineare. Questo evita crolli drastici di banda.

> **ECN (Explicit Congestion Notification)**: Approccio supportato dalla rete. Se i buffer di un router superano l'80%, il router imposta due bit di alert sull'header IP. Quando arrivano al ricevente, questi li rispecchia nel flag TCP (ECE), dicendo al mittente di rallentare *prima* che avvenga un effettivo packet loss e un conseguente Timeout.

---

## 9. Livello di Rete (Piano dei Dati e Router)
Il Livello di Rete assicura la mobilità dei pacchetti globalmente.
- Non garantisce nulla se non un servizio **Best-Effort**. Nessuna garanzia di ritardo minimo o perdita nulla.
- La distinzione principale all'interno dei router è tra:
  - **Data Plane (Forwarding)**: Basato su hardware ASIC. L'azione fulminea del router che guarda l'IP di destinazione, cerca sulla *Forwarding Table* locale, e sposta il pacchetto dal link di input a quello di output via *Switch Fabric*.
  - **Control Plane (Routing)**: Basato su software e CPU. Esegue algoritmi come Dijkstra o Bellman-Ford per "disegnare" la mappa globale e inviare aggiornamenti della Forwarding Table alle porte fisiche.

### Architettura e Switching
I router subiscono ritardi di accodamento. Se le code superano la RAM disponibile, scartano i pacchetti (solitamente con logica FIFO e Drop-Tail).
La logica di inoltro usa la **Longest Prefix Matching (LPM)**:
Quando un indirizzo IP destinazione matcha due diverse reti presenti in tabella (es. `192.168.1.0/24` e `192.168.0.0/16`), il router inoltrerà SEMPRE il pacchetto sulla rotta che ha la maschera (il prefisso) **più lungo e specifico** (nell'esempio il /24).

---

## 10. Indirizzamento: Subnetting, DHCP e NAT

### Subnetting e CIDR
L'IPv4 è a 32 bit, garantendo circa 4 miliardi di indirizzi unici, suddivisi concettualmente in `Parte Rete` e `Parte Host`.
La separazione è dettata dalla **Subnet Mask** (es. `255.255.255.0` o in CIDR notazione `/24`).
Il CIDR (*Classless Inter-Domain Routing*) permette di tagliare le reti su misura (non più vincolate a enormi e spreconi blocchi di classe A/B/C). 
- Permette anche l'**Aggregazione di rotta (Route Summarization)**: un ISP con 4 blocchi contigui `/24` annuncia al resto di Internet una singola rotta `/22`, sfoltendo immensamente le tabelle globali BGP e risparmiando TCAM preziosa sui core router.

### Configurazione Dinamica: DHCP
**DHCP** (UDP) alloca automaticamente gli IP ai nuovi host secondo 4 passaggi di rete (*DORA*):
1. **D**iscover: Il client manda un pacchetto IP broadcast `255.255.255.255` cercando un server.
2. **O**ffer: Il server DHCP risponde offrendo un IP.
3. **R**equest: Il client accetta ufficialmente.
4. **A**ck: Il server finalizza, concedendo un *Lease Time*, la Subnet Mask, l'indirizzo del Gateway e il DNS locale.

### Sicurezza e Scarsità IPv4: NAT
Il **Network Address Translation** risolve l'insufficienza cronica degli IPv4 rendendo le intere reti casalinghe dipendenti da **un singolo IP Pubblico** visibile su Internet, mentre internamente usano indirizzi riservati privati (es. il classico `192.168.1.x`).
- **Funzionamento**: Quando un pacchetto esce di casa, il NAT Router modifica l'header IP sostituendo l'IP privato sorgente e una porta effimera in una combinazione IP Pubblico : Nuova Porta, salvandola in una NAT Table. Quando il pacchetto risponde, il router fa l'inverso.
- **Infrange le regole a strati**: Il NAT è considerato un hack architetturale perché un apparato di Rete (Livello 3) ficca il naso negli header di Trasporto (Livello 4, porte TCP/UDP) per alterarle, violando il principio di incapsulamento OSI puro.
