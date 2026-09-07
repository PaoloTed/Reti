# Riassunto Approfondito: Reti di Calcolatori (Capitoli 11-17)

> Questo è il terzo e ultimo modulo del riassunto. Tratta le logiche software che guidano i pacchetti (Routing), l'accesso al mezzo fisico locale (Livello Collegamento), i fondamenti della sicurezza e una review tecnica degli esercizi d'esame e dei laboratori Wireshark.

---

## 11. Il Piano di Controllo: Gli Algoritmi di Routing
Il **Piano di Controllo (Control Plane)** è il "cervello" della rete. Il suo scopo è scambiarsi informazioni globali sulla topologia e generare le Forwarding Table che ogni router userà per lo smistamento fisico locale dei pacchetti.
La rete è calcolata matematicamente come un **Grafo pesato** in cui i Nodi sono i router e gli Archi (Link) hanno un Costo (ritardo, congestione, spesa).

### 11.1 Distance Vector (DV) - L'Algoritmo di Bellman-Ford
È un algoritmo distribuito e decentralizzato storicamente usato da RIP e BGP.
- **Visione Locale**: Ogni router parla **solo ed esclusivamente con i suoi vicini diretti**.
- **Processo**: A intervalli regolari, il router $X$ invia ai suoi vicini il proprio vettore delle distanze (ovvero quanto costa, secondo $X$, arrivare a tutti i possibili target su Internet).
- **Aggiornamento**: Quando un nodo $Y$ riceve il vettore dal vicino $X$, aggiorna la propria stima scegliendo il percorso più breve usando la formula di Bellman-Ford:
  $$D_Y(dest) = \min_X \{ costo(Y, X) + D_X(dest) \}$$
- **Il Problema (Count-to-Infinity)**: Le "buone notizie" (nuovi percorsi più corti) viaggiano velocemente; le "cattive notizie" (un link si rompe) causano cicli infiniti (*routing loop*) in cui due nodi si ingannano a vicenda aumentando all'infinito la stima dei costi.

### 11.2 Link-State (LS) - L'Algoritmo di Dijkstra
È l'algoritmo usato dai protocolli moderni come OSPF.
- **Visione Globale (Flooding)**: Ogni router parla **con tutta la rete**, inviando pacchetti di Link-State che contengono solo l'identità dei suoi vicini diretti.
- **Processo**: Alla fine del flooding, **tutti i nodi possiedono un database topologico identico** dell'intera rete.
- **Calcolo Locale**: Ogni router lancia in memoria l'Algoritmo di Dijkstra usando se stesso come Nodo Radice, calcolando l'albero dei percorsi minimi (Shortest Path Tree) ed estrudendo da esso la tabella di routing.

---

## 12. Il Livello di Collegamento (Link Layer e MAC)
Se IP si preoccupa dell'intero viaggio coast-to-coast, il Livello di Collegamento (Livello 2) si assicura che il pacchetto non sbandi mentre percorre **il singolo filo/link tra due nodi diretti**. Il datagramma IP viene imbustato in un **Frame**.

### Error Detection
Durante il transito sui cavi, variazioni di tensione elettromagnetica possono flippare i bit (corruzione).
Il mittente calcola un controllo matematico sui dati tramite il **CRC (Cyclic Redundancy Check)**:
Sfruttando l'algebra polinomiale, il messaggio viene diviso per un Polinomio Generatore $G$. Il resto della divisione (il CRC) è appeso alla fine del Frame. Se il ricevente non ottiene resto zero rifacendo l'operazione, il frame viene scartato (nessuna correzione, solo drop).

### MAC Address e ARP (Address Resolution Protocol)
Il Livello 2 usa l'**Indirizzo MAC** (es. `1A:23:F9:CD:06:9B`, lungo 48 bit e *fisso* nella scheda di rete).
**Come fa il Livello 3 a tradurre un IP nel corrispondente MAC del prossimo salto?** Usa l'ARP:
1. L'Host A chiede in Broadcast a tutta la rete locale (`FF:FF:FF:FF:FF:FF`): *"Chi ha l'IP 192.168.1.10?"*
2. Il dispositivo che ha quell'IP (o il gateway) risponde con un pacchetto unicast: *"Sono io, e il mio MAC è AA:BB:CC..."*.
3. L'Host A salva la coppia IP $\leftrightarrow$ MAC nella propria **ARP Cache** locale (scade in 20 min).

### Gestione delle Collisioni: CSMA/CD su Ethernet
Se due PC trasmettono simultaneamente su un cavo condiviso le loro onde collidono, distruggendo entrambi i frame. L'Ethernet classica (IEEE 802.3) usa la strategia **Carrier Sense Multiple Access / Collision Detection (CSMA/CD)**:
- **Listen Before Talk (CS)**: Il PC ascolta il cavo. Se è silenzioso, inizia a inviare bit.
- **Listen While Talking (CD)**: Se il PC sente un picco di voltaggio (collisione), ferma subito l'invio e trasmette un segnale di Jamming.
- **Binary Exponential Backoff**: Dopo la collisione, i due PC attendono un tempo *random* prima di riprovare. L'attesa è calcolata lanciando un dado in un range di $\{0 \dots 2^N - 1\}$, dove $N$ è il numero di collisioni consecutive. Al crescere dei conflitti, la finestra di attesa esplode esponenzialmente smaltendo il traffico.

### Gli Switch di Rete (Self-learning)
Gli Switch sono "trasparenti" alla rete (non hanno IP propri). Popolano automaticamente la loro *Switch Table* registrando la porta fisica da cui entra ogni MAC sorgente.
Se uno Switch riceve un pacchetto per un MAC che non ha mai visto in tabella, esegue il **Flooding** (inoltra la copia a tutte le sue porte inondando la rete).

---

## 13. Sicurezza delle Reti
Gli obiettivi della sicurezza sono **Confidenzialità** (cifratura), **Integrità** (hash/MAC), e **Autenticazione**.
Vulnerabilità principali: *Eavesdropping* (intercettazione passiva), *Man-in-the-Middle* (alterazione attiva come ARP Poisoning), e *Denial of Service* (inondamento di banda o esaurimento RAM tramite SYN Flood).

### Crittografia Base vs TLS
- **Simmetrica (es. AES-256)**: Singola chiave condivisa per cifrare/decifrare. Molto veloce computazionalmente, ma impossibile da scambiarsi apertamente su Internet se si è sconosciuti.
- **Asimmetrica (es. RSA)**: Usa due chiavi (Pubblica visibile a tutti, Privata nascosta). Risolve il problema dello scambio chiavi e permette la Firma Digitale, ma è lentissima.
- **La Soluzione Industriale (HTTPS/TLS)**: Il Client e Server usano la crittografia asimmetrica *solo* durante l'Handshake iniziale per scambiarsi (in segreto, dopo aver verificato i certificati di integrità) una chiave simmetrica master usa e getta. Da quel momento il traffico massiccio del sito scorrerà cifrato velocemente tramite AES.

---

## 14-17. Esercizi Risolti e Laboratori Wireshark (Pratica d'Esame)

### Formule e Calcoli Matematici d'Esame
1. **Tempi di trasferimento HTTP (Non-Persistenti)**
   - Il costo base in connessioni multiple non-persistenti per un Oggetto è: $2 \times RTT + t_{trasm}$ ($t_{trasm} = Lunghezza / Capacità \text{ del link}$).
   - *Nota Esame*: Se vi chiedono di valutare i ritardi di 5 immagini JPG sequenziali, il ritardo è $N \times (2 \cdot RTT + t_{trasm})$. Se il testo dice *connessioni parallele*, l'RTT si sconta una volta sola.
2. **Subnetting (CIDR)**
   - Data la rete `192.168.10.0/24`, scomporla in 4 sottoreti uguali.
   - Soluzione: $2^x = 4 \rightarrow$ servono $x=2$ bit rubati alla porzione Host. Il nuovo prefisso diventa $/26$ ($24+2$).
   - Salti (Delta): I salti sono calcolati dai bit rimanenti. L'host id è di 6 bit, $2^6 = 64$. Le reti saranno `.0/26`, `.64/26`, `.128/26`, `.192/26`.
3. **Longest Prefix Matching (LPM in Binario)**
   - Convertite in binario solo il byte dove differisce l'IP del pacchetto con le rotte in tabella. Confrontate quanti bit di testa combaciano tra la rotta (es. un $/21$) e l'IP in ingresso. La rotta che "matcha" il numero più lungo di bit (più specifico) è il Next-Hop vincitore.

### Approfondimenti Laboratori Wireshark
- **Analisi TCP (L05)**: Il fenomeno della segmentazione in TCP appare in Wireshark con messaggi `[TCP segment of a reassembled PDU]`. Accade quando l'applicazione passa al socket TCP un body HTML più grosso della MTU della scheda Ethernet. Wireshark li raggruppa virtualmente, ma fisicamente viaggiano come pacchetti frammentati separati.
- **Analisi DNS (nslookup)**: Si osserva l'uso nativo del protocollo UDP su porta `53`. Nelle query di tipo `NS` (Name Server Autoritativi), le risposte contengono non solo i nomi dei server ma spesso anche dei record `A` aggiuntivi chiamati *Glue Records*, i quali indicano preventivamente l'IP di tali server per far risparmiare all'host una successiva query di DNS resolving superflua.
- **Analisi ICMP e Traceroute**: Per scovare i Router lungo un percorso sconosciuto, `traceroute` lancia intenzionalmente dei pacchetti datagramma IP con un campo TTL corrotto artificialmente, settandolo a `1`, poi `2`, poi `3`. Al router in hop-1 il TTL scade (diventa `0`) e questo scarta il pacchetto inviando al client un errore di "Time Exceeded" ICMP, rivelando così il proprio indirizzo IP e smascherandosi. Il processo si ripete svelando la mappa topologica dell'instradamento hop-by-hop.
