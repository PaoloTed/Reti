# Reti di Calcolatori I — Guida Completa allo Studio

> **Corso di Laurea in Informatica — A.A. 2025-2026**
> Questa guida copre **tutti gli argomenti** delle lezioni 1–26 del corso **Computer Networks I**.
> Il documento è completamente sostitutivo allo studio delle slide ed è scritto interamente in **italiano**.
> Include **tutte le 63 lavagne manoscritte originali** (board), i **laboratori pratici completi con Wireshark** e le **sessioni di domande d'esame (QA01)**.

---

<a id="indice"></a>
## Indice

1. [Introduzione alle Reti di Calcolatori](#1-introduzione-alle-reti-di-calcolatori) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-1)
2. [Il Livello Applicazione — Architetture e Protocolli Base](#2-il-livello-applicazione--architetture-e-protocolli-base) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-2)
3. [Il Protocollo HTTP](#3-il-protocollo-http) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-3)
4. [Posta Elettronica, P2P e DNS](#4-posta-elettronica-p2p-e-dns) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-4)
5. [Programmazione di Rete con i Socket](#5-programmazione-di-rete-con-i-socket) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-5)
6. [Il Livello di Trasporto — UDP e Trasferimento Affidabile](#6-il-livello-di-trasporto--udp-e-trasferimento-affidabile) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-6)
7. [Il Protocollo TCP](#7-il-protocollo-tcp) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-7)
8. [Controllo di Flusso e Controllo della Congestione](#8-controllo-di-flusso-e-controllo-della-congestione) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-8)
9. [Il Livello di Rete — IP e Router](#9-il-livello-di-rete--ip-e-router) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-9)
10. [Indirizzamento IP, DHCP, NAT e IPv6](#10-indirizzamento-ip-dhcp-nat-e-ipv6) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-10)
11. [Il Piano di Controllo — Algoritmi di Routing](#11-il-piano-di-controllo--algoritmi-di-routing) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-11)
12. [Il Livello di Collegamento (Link Layer) e il Livello Fisico](#12-il-livello-di-collegamento-link-layer-e-il-livello-fisico) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-12)
13. [Sicurezza delle Reti](#13-sicurezza-delle-reti) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-13)
14. [Programmazione REST e Formati di Scambio Dati](#14-programmazione-rest-e-formati-di-scambio-dati) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-14)
15. [Esercizi Risolti e Sessioni di Domande e Risposte](#15-esercizi-risolti-e-sessioni-di-domande-e-risposte) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-15)
16. [Guide Pratiche di Laboratorio con Wireshark](#16-guide-pratiche-di-laboratorio-con-wireshark) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-16)
17. [Sessione di Ripasso e Domande d'Esame Svolte (QA01)](#17-sessione-di-ripasso-e-domande-desame-svolte-qa01) — [Sottosezioni](#indice-delle-sottosezioni-capitolo-17)

---

## 1. Introduzione alle Reti di Calcolatori
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 1.1 Cos'è una Rete di Calcolatori

Una **rete di calcolatori** (*computer network*) è un insieme di dispositivi separati ma interconnessi che collaborano per svolgere un compito comune:
- È una **raccolta di dispositivi di calcolo autonomi interconnessi** che possono scambiare informazioni tra loro.
- Il termine "autonomi" distingue le reti dai sistemi multiprocessore: ogni nodo ha il proprio sistema operativo e funziona indipendentemente.
- La rete più importante ed estesa è **Internet**.

> [Cambridge Dictionary] *"Computer networking: the process of connecting computers together so that they can share information."*

**Utilizzi delle reti di calcolatori:**

| Utilizzo | Descrizione | Modello |
|----------|-------------|--------|
| **Accesso alle informazioni** | Navigazione web, ricerca, consultazione di risorse remote | Client-Server |
| **Comunicazione persona-persona** | E-mail, messaggistica istantanea, videoconferenza | Entrambi |
| **Commercio elettronico** | Acquisti online, servizi bancari, transazioni digitali | Client-Server |
| **Intrattenimento** | Streaming, giochi online, musica, video | Entrambi |
| **Internet delle Cose (IoT)** | Dispositivi intelligenti connessi (casa, industria, trasporti) | Client-Server |

**Accesso alle informazioni — modelli:**
- **Client-server**: un processo client invia una richiesta al processo server che risponde con l'informazione
- **Peer-to-peer**: non ci sono client e server fissi; ogni nodo può essere entrambi

### 1.2 Internet — La Rete delle Reti

**Internet** è la più grande rete di calcolatori al mondo. È tecnicamente un'enorme **Wide Area Network (WAN)** che permette a sotto-reti e dispositivi di connettersi tra nazioni e continenti.

**Breve storia di Internet:**

| Anno | Evento |
|------|--------|
| ~1950 | J.C.R. Licklider teorizza l'idea di una rete "universale" |
| 1969 | ARPA finanzia ARPANET con 4 nodi (SRI, UCLA, UCSB, UTAH) |
| 1974 | R. Kahn e V. Cerf progettano **TCP/IP** |
| 1986 | NSF finanzia **NSFNET** |
| 1990 | ARPANET dismessa |
| 1995 | Internet moderna: rimosse le ultime restrizioni commerciali |

### 1.3 Componenti di una Rete

Una rete è descritta con la terminologia della **teoria dei grafi**:

- **Nodi** (*nodes*): dispositivi connessi alla rete (router, switch, host)
- **Link di comunicazione** (*communication links*): connessioni fisiche o wireless tra i nodi
- **Cammino** (*path*): sequenza di nodi e link da sorgente a destinazione
- **Host** (end-system): nodi terminali (foglie) che forniscono o utilizzano servizi — laptop, smartphone, server, IoT devices
- **Dispositivi di routing**: nodi intermedi che instradano i pacchetti — router, switch

> Gli **host** sono idealmente le foglie del grafo di rete; i dispositivi intermedi (router, switch) non eseguono applicazioni utente ma si occupano solo dell'instradamento.

**Principali dispositivi di rete:**

| Dispositivo | Livello OSI | Funzione | Note |
|-------------|-------------|----------|----- |
| **Router** | Livello 3 (Rete) | Instrada i pacchetti tra reti diverse (basato su IP) | Cuore di Internet |
| **Switch** | Livello 2 (Link) | Commuta i frame all'interno di una LAN (basato su MAC) | Self-learning |
| **Hub** | Livello 1 (Fisico) | Ripete il segnale su tutti i port (obsoleto) | Causa collisioni |
| **Access Point** | Livello 2 | Permette connessioni wireless a una rete cablata | IEEE 802.11 |
| **Modem** | Livello 1 | Modulazione/demodulazione per linee telefoniche analogiche | ADSL |
| **ONT** | Livello 1 | Terminale di rete ottica per fibra | No (de)modulazione |

### 1.4 Comunicazione dei Dati

La **comunicazione dei dati** coinvolge 5 elementi fondamentali:

1. **Messaggio**: i dati da trasmettere (testo, numeri, immagini, audio, video)
2. **Mittente** (*sender*): l'entità che invia il messaggio
3. **Destinatario** (*receiver*): l'entità che deve ricevere il messaggio
4. **Mezzo** (*medium*): il canale attraverso cui il messaggio viaggia
5. **Protocollo** (*protocol*): l'insieme di regole di comunicazione

**Tipi di flusso dati:**

| Tipo | Descrizione |
|------|-------------|
| **Simplex** | Monodirezionale (un solo senso) |
| **Half-duplex** | Bidirezionale a turni |
| **Full-duplex** | Bidirezionale simultaneo |

**Concetti chiave di velocità:**

- **Transmission rate**: quantità massima di informazione trasmissibile da un dispositivo (bit/s)
- **Bandwidth**: quantità massima su un cammino completo (link + nodi), in bit/s
- **Throughput**: quantità istantanea effettiva trasmessa, in bit/s

### 1.5 Tipi di Connessione e Topologie di Rete

**Tipi di connessione:**
- **Point-to-point**: link dedicato tra due dispositivi (wireless o cablato)
- **Multipoint (broadcast)**: più di due dispositivi condividono un singolo link (wireless o cablato)

**Topologie di rete principali:**

| Topologia | Link fisici | Pro | Contro |
|-----------|-------------|-----|--------|
| **Bus** | 1 backbone + n link (o solo 1 condiviso) | Semplice, economico; buona per reti piccole | Singolo punto di guasto; collisioni possibili |
| **Ring** | n link duplex | Semplice, più performante del bus | Aggiungere nodi è difficile; un nodo guasto può bloccare la rete |
| **Star** | 1 controller + n link duplex | Meno costosa, semplice, robusta, più scalabile | Controller raggiungibile da tutti; singolo punto di guasto |
| **Tree** | Combinazione di star+bus | Versatile, scalabile, ben supportata da HW/SW | Difficile da configurare; debolezza del bus |
| **Mesh** | Full: n(n-1)/2 link duplex; Partial: meno | Basso traffico, robusta, sicura, dedicata | Difficilmente scalabile; costosa (dispositivi con molte porte) |
| **Hybrid** | Variabile | Flessibile, combinazione ottimale | Complessità aumentata |

> **Full Mesh:** n(n-1)/2 link fisici duplex. Con 10 nodi = 45 link!

**Esempio Hybrid:** Star-backbone con 3 reti bus collegate tramite un controller centrale.

### 1.6 Categorie di Reti

| Tipo | Acronimo | Portata | Esempio |
|------|----------|---------|---------|
| Personal Area Network | **PAN** | ~1-10 m | Bluetooth |
| Local Area Network | **LAN/WLAN** | Edificio, campus | Ethernet, Wi-Fi |
| Metropolitan Area Network | **MAN** | Città | Rete via cavo cittadina |
| Wide Area Network | **WAN** | Nazione, mondo | Internet |

### 1.7 Internet Service Providers (ISP)

Un **ISP** (Internet Service Provider) è un'organizzazione che fornisce servizi per l'accesso, l'utilizzo e la partecipazione a Internet. Può essere commerciale, comunitaria, non-profit o privata (es. università).

**Gerarchia degli ISP:**
- **PoP (Point of Presence)**: gruppo di uno o più router usati dall'ISP per raggiungere i clienti
- **ISP di accesso** (*Access ISP*): coprono aree locali (es. Fastweb, TIM in Italia)
- **ISP regionali**: coprono aree più ampie (regione, nazione)
- **ISP nazionali/globali**: backbone Internet
- **IXP (Internet Exchange Point)**: punto neutrale dove ISP diversi si scambiano traffico (spesso non gestito dagli ISP stessi)

```
[ISP Globale] ←──IXP──→ [ISP Globale]
      │                        │
[ISP Regionale]          [ISP Regionale]
      │                        │
[ISP di Accesso]         [ISP di Accesso]
      │                        │
  [Utenti]                [Utenti]
```

**Tecnologie di accesso privato (via Modem/ONT → rete telefonica → ISP → Internet):**

| Tecnologia | Velocità | Note |
|-----------|----------|------|
| Analogica | 56 kbps | Storica |
| ISDN | 128 kbps | Digitale base |
| ADSL | 1–20 Mbps | Doppino, asimmetrica |
| Doppino in rame | 10–100 Mbps | Twisted-pair |
| **Fibra ottica** | 50 Mbps – 40 Gbps | Via ONT, no (de)modulazione |

> Le aziende (soprattutto medio/grandi) possono avere una connessione diretta/dedicata all'ISP, bypassando la rete telefonica.

### 1.8 Il Modello a Strati (Stack Protocollare)

Le reti adottano un'**architettura a strati** per gestire la complessità. Ogni strato:
- Offre **servizi** allo strato superiore
- Usa i **servizi** dello strato inferiore
- Comunica con lo strato pari (*peer*) sull'altro host tramite un **protocollo**

**Modello TCP/IP (de facto — 5 strati):**

| Strato | Nome | Protocolli | Unità dati |
|--------|------|------------|------------|
| 5 | **Applicazione** | HTTP, FTP, DNS, SMTP, SSH | Messaggio |
| 4 | **Trasporto** | TCP, UDP | Segmento / Datagramma |
| 3 | **Rete (Network)** | IP, DHCP, NAT, ICMP | Datagramma IP |
| 2 | **Collegamento (Link)** | Ethernet, Wi-Fi, ARP | Frame |
| 1 | **Fisico (Physical)** | Cavi, fibra, onde radio | Bit |

**Modello ISO/OSI (de iure — 7 strati):**

| Strato | Nome | Funzione |
|--------|------|----------|
| 7 | **Applicazione** | Interfaccia con l'utente, protocolli applicativi |
| 6 | **Presentazione** | Formattazione dati, cifratura, compressione |
| 5 | **Sessione** | Gestione delle sessioni di comunicazione (sincronizzazione) |
| 4 | **Trasporto** | Consegna end-to-end, controllo flusso/congestione |
| 3 | **Rete** | Indirizzamento e routing dei pacchetti |
| 2 | **Collegamento** | Trasmissione frame tra nodi adiacenti, rilevamento errori |
| 1 | **Fisico** | Trasmissione bit sul mezzo fisico |

> **Confronto:** In TCP/IP i livelli Presentazione e Sessione (5,6 OSI) sono **assorbiti nel livello Applicazione**. ISO/OSI è il modello *de iure* (standard formale), TCP/IP è il modello *de facto* (usato in pratica su Internet).

**Principio di incapsulamento (Encapsulation):**

Ogni strato aggiunge il proprio header (e a volte trailer) ai dati provenienti dallo strato superiore:

```
Applicazione:  [           MESSAGGIO           ]
Trasporto:     [ TCP Hdr | MESSAGGIO           ]  → segmento
Rete:          [ IP Hdr | TCP Hdr | MESSAGGIO  ]  → datagramma
Collegamento:  [ ETH Hdr | ... | MESSAGGIO | CRC ] → frame
Fisico:        01001101010110...                   → bit stream
```

Il destinatario esegue il processo inverso (**decapsulamento**): ogni strato rimuove il proprio header e passa il payload allo strato superiore.

**Comunicazione tra strati in un percorso completo:**
```
Host A                    Router                   Host B
[App]                                              [App]
[Transport]                                        [Transport]
[Network]  ←──────────→  [Network]  ←──────────→  [Network]
[Link]     ←──────────→  [Link]     ←──────────→  [Link]
[Physical] ←──────────→  [Physical] ←──────────→  [Physical]
```
> I router operano solo fino al livello di rete (3); gli host operano su tutti e 5 i livelli.

### 1.9 Schemi e Appunti dalle Lavagne (Lezione 2)

I seguenti schemi riproducono fedelmente le lavagne manoscritte della lezione sull'architettura a livelli e il modello di rete:

![Board Lezione 02 - Pagina 1](assets/board_images/board_lecture02_p1.png)
*Figura 1.1 — Comunicazione tra due macchine a ogni strato e protocolli corrispondenti.*

![Board Lezione 02 - Pagina 2](assets/board_images/board_lecture02_p2.png)
*Figura 1.2 — Host terminali vs nodi intermedi di commutazione e instradamento.*

![Board Lezione 02 - Pagina 3](assets/board_images/board_lecture02_p3.png)
*Figura 1.3 — Stack protocollare e incapsulamento sequenziale dei dati.*

![Board Lezione 02 - Pagina 4](assets/board_images/board_lecture02_p4.png)
*Figura 1.4 — Percorso end-to-end dei dati attraverso la rete fisica.*

---

## 2. Il Livello Applicazione — Architetture e Protocolli Base
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 2.1 Applicazioni di Rete

Un'**applicazione di rete** è composta da più programmi che girano su diversi host (end-system) e comunicano attraverso la rete. I programmi non devono necessariamente essere scritti nello stesso linguaggio o girare sullo stesso OS.

**Applicazioni comuni:** social network, Web, messaggistica, e-mail, giochi online, streaming (YouTube, Netflix), P2P (BitTorrent), VoIP (Skype), videoconferenza, motori di ricerca, accesso remoto (SSH, Telnet).

> Le applicazioni di rete girano sugli **host** (end-system) e **non** sui dispositivi di rete intermedi (router, switch): questi non eseguono applicazioni utente. Questo approccio semplifica enormemente lo sviluppo.

### 2.2 Architetture delle Applicazioni di Rete

L'**architettura applicativa** è progettata dallo sviluppatore e determina come l'applicazione è strutturata sui vari end-system:

#### 2.2.1 Architettura Client-Server

- C'è un host **sempre attivo** (il **server**) con indirizzo fisso e ben noto
- I **client** richiedono servizi; non comunicano direttamente tra loro
- Il client conosce sempre l'indirizzo del server; il server non conosce a priori i client

**Organizzazione dei server per la scalabilità:**
1. **Data center locale**: un singolo luogo con molti server
2. **Server distribuiti nel mondo**: più data center in paesi diversi
3. **Data center distribuiti**: organizzazione gerarchica globale

> Il client è tipicamente **ignaro** dell'esistenza di più server e li percepisce come un unico server.

**Esempio**: applicazione web — il browser (client) invia richieste al processo web server; il server è sempre attivo e raggiungibile da tutti i client.

#### 2.2.2 Architettura Peer-to-Peer (P2P)

- Non esistono server fissi sempre attivi; le comunicazioni avvengono **direttamente tra coppie di host** (*peer*)
- I peer non sono di proprietà di un service provider ma sono desktop, laptop e smartphone degli utenti
- Ogni peer ha il proprio indirizzo (non fisso come il server)
- È usata tipicamente per applicazioni ad alta intensità di traffico

**Vantaggi:**
- **Scalabilità**: ogni nuovo peer aggiunge workload MA anche capacità di servizio
- **Costo basso**: non richiedono infrastrutture costose o grande banda centralizzata

**Svantaggi:**
- Problemi di **sicurezza** (comunicazione diretta tra client)
- **Performance e affidabilità** dipendono dalla disponibilità dei peer

#### 2.2.3 Architettura Ibrida (P2P + Client-Server)

La maggior parte delle applicazioni P2P **pure** sono rare. Nella pratica si usano architetture **ibride** che combinano elementi di entrambe:

**Esempi:**
- **Messaggistica istantanea**: i server tracciano gli indirizzi IP degli utenti (C-S), ma i messaggi utente-utente viaggiano direttamente tra i peer (P2P)
- **File-sharing**: il server può tenere traccia di tutti i file disponibili per velocizzare la ricerca (C-S), mentre il trasferimento avviene tra peer (P2P)
- **VoIP/Videoconferenza**: server per la segnalazione, P2P per i media

### 2.3 Comunicazione tra Processi

In un'applicazione di rete, i **processi** che girano su macchine diverse (con OS potenzialmente diversi) comunicano attraverso la rete. Si definisce:
- **Processo client**: avvia la comunicazione (invia messaggi per primo)
- **Processo server**: attende di essere contattato

> In P2P un processo può cambiare ruolo: è client quando scarica, server quando carica.

#### 2.3.1 Socket — L'interfaccia tra Applicazione e Rete

Un **socket** è l'interfaccia software tra livello applicazione e livello di trasporto. Analogia: come una **cassetta delle lettere** — il processo mette il messaggio nella cassetta (socket) e la rete lo recapita.

- È usato come **API** (Application Programming Interface) tra applicazione e rete
- Lo sviluppatore ha controllo completo del lato applicazione della socket
- Ha **poco controllo** sul lato trasporto: solo scelta del protocollo (TCP/UDP) e forse alcuni parametri (buffer, MSS)
- Una volta scelto il protocollo, l'applicazione usa i servizi che quel protocollo fornisce

```
  Processo Applicativo
  ─────────────────────────────────
          Socket (API)
  ─────────────────────────────────
  Livello Trasporto (TCP/UDP)
  ─────────────────────────────────
  Livello Rete (IP)
  ─────────────────────────────────
  Livello Link + Fisico
```

#### 2.3.2 Indirizzamento dei Processi

Poiché più applicazioni possono girare su un singolo host, per identificare il processo destinatario servono **due elementi**:
1. **Indirizzo IP** (32 bit) — identifica l'host sulla rete (livello di rete)
2. **Numero di porta** (16 bit, 0-65535) — identifica il processo sull'host (livello di trasporto)

**Porte well-known (0-1023)** — riservate a protocolli noti, gestite da IANA ([www.iana.org](http://www.iana.org)):

| Porta | Protocollo | Uso |
|-------|-----------|-----|
| 20 | FTP | Trasferimento dati |
| 21 | FTP | Controllo comandi |
| 22 | SSH | Accesso remoto sicuro |
| 23 | Telnet | Accesso remoto (non cifrato) |
| 25 | SMTP | Invio email |
| 53 | DNS | Risoluzione nomi |
| 80 | HTTP | Web |
| 110 | POP3 | Ricezione email |
| 119 | NNTP | News groups |
| 123 | NTP | Sincronizzazione orario |
| 143 | IMAP | Gestione email avanzata |
| 161 | SNMP | Gestione rete |
| 443 | HTTPS | Web sicuro |

### 2.4 QoS — Servizi dello Strato di Trasporto

Il livello di trasporto offre servizi di **Quality of Service (QoS)**:

| Servizio | Descrizione | Note |
|----------|-------------|------|
| **Affidabilità** | Dati arrivano corretti e completi all'altra estremità | Essenziale per email, FTP |
| **Throughput** | Velocità garantita (bit/s) | Utile per streaming |
| **Timing** | Ogni bit arriva entro un intervallo di tempo | Critico per VoIP, gaming |
| **Sicurezza** | Cifratura e decifratura dei messaggi | TLS su TCP (livello app) |

**Protocolli di trasporto e le loro scelte applicative:**

| Protocollo | Caratteristiche | Uso tipico |
|------------|-----------------|-----------|
| **TCP** | Connection-oriented, affidabile, controllo flusso/congestione; handshake iniziale | Web, e-mail, FTP, SSH |
| **UDP** | Connectionless, nessuna garanzia, veloce, overhead minimo (8B header) | DNS, streaming, VoIP, gaming |

> **TLS/SSL**: tecnicamente la sicurezza è un problema del livello trasporto, ma protocolli sicuri come TLS sono spesso implementati sopra TCP a livello applicazione.

### 2.5 Protocolli del Livello Applicazione

Un **protocollo applicativo** definisce:
1. **Tipi di messaggi** scambiati (richieste e risposte)
2. **Sintassi** dei messaggi (campi, delimitatori, encoding)
3. **Semantica** dei campi (significato delle informazioni)
4. **Regole** su quando e come i processi inviano/rispondono ai messaggi

**Tipi di protocolli:**
- **Open protocols** (protocolli aperti): regole pubbliche, definite in RFC (es. HTTP, SMTP, DNS) — consentono interoperabilità
- **Proprietary protocols** (protocolli proprietari): non pubblicati apertamente (es. protocolli interni di Skype, WhatsApp)

**Tabella principali protocolli applicativi:**

| Applicazione | Protocollo | Trasporto | Nota |
|--------------|------------|-----------|------|
| Web | HTTP/HTTPS | TCP (o UDP/QUIC per H3) | Base del WWW |
| E-mail invio | SMTP/SMTPS | TCP (porta 25) | Tra mail server |
| E-mail ricezione | POP3, IMAP | TCP (110, 143) | Client-server |
| DNS | DNS | UDP (porta 53) | Risoluzione nomi |
| Configurazione IP | DHCP | UDP | Plug-and-play |
| Trasferimento file | FTP/FTPS | TCP (20/21) | Storico |
| Accesso remoto sicuro | SSH | TCP (22) | Cifrato |
| Accesso remoto | Telnet | TCP (23) | Non cifrato (deprecato) |
| Gestione rete | SNMP | UDP (161) | Dispositivi rete |

### 2.6 FTP — File Transfer Protocol

**FTP** (prima versione 1971) trasferisce file tra host attraverso la rete. È uno dei protocolli più antichi di Internet.

**Due versioni:**
- **FTP base**: trasferimento **in chiaro** (username, password, file)
- **FTPS** (FTP Secure): protegge credenziali e cifra il contenuto

**Entrambe hanno due componenti:**
1. Il protocollo che specifica i comandi
2. Un'applicazione software client-side e server-side che implementa il protocollo

**Setup su Linux:**
```bash
# Installazione server FTP (vsftpd - very secure FTP daemon)
sudo apt-get install vsftpd
service vsftpd status         # controlla che il daemon sia in esecuzione

# Installazione client FTP
sudo apt-get install ftp
ftp INDIRIZZO_SERVER          # username e password richiesti
exit                          # chiude la connessione
```

> Il server FTP è implementato come **daemon**: un programma che gira in background e aspetta che i client si connettano. È un approccio comune per i server di rete.

**Comandi FTP principali:**

| Comando | Descrizione |
|---------|-------------|
| `help` | Elenca tutti i comandi disponibili |
| `ls` | Elenca file nella directory remota |
| `cd DIR` | Cambia directory remota |
| `lcd DIR` | Cambia directory locale |
| `pwd` | Stampa directory corrente sul server |
| `get FILE` | Scarica file dal server |
| `put FILE` | Carica file sul server |
| `mkdir DIR` | Crea directory remota |
| `rmdir DIR` | Rimuove directory remota |
| `delete FILE` | Cancella file remoto |

### 2.7 Schemi e Appunti dalle Lavagne (Lezione 3)

![Board Lezione 03 - Pagina 1](assets/board_images/board_L03_p1.png)
*Figura 2.1 — Principio di disaccoppiamento: le applicazioni delegano la gestione del flusso al livello di trasporto.*

![Board Lezione 03 - Pagina 2](assets/board_images/board_L03_p2.png)
*Figura 2.2 — Servizi del trasporto visti dal livello applicazione (astrazione logica).*

---

## 3. Il Protocollo HTTP
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 3.1 World Wide Web e HTTP

Fino ai primi anni '90, Internet era usata principalmente da ricercatori, accademici e studenti universitari (Telnet, FTP, email). Il **World Wide Web** è stata la prima applicazione Internet a raggiungere il grande pubblico.

**HTTP (HyperText Transfer Protocol)** è il protocollo alla base del WWW. Definisce:
- La **struttura dei messaggi** scambiati tra client e server
- Come client e server **scambiano questi messaggi**
- (Non definisce come le applicazioni client/server vanno implementate)

**Caratteristiche fondamentali:**
- **Client-server**: il browser (client) traduce le richieste dell'utente in messaggi HTTP; il server esegue la richiesta e risponde
- **Stateless**: il server **non mantiene** informazioni sulle interazioni precedenti con un client specifico → semplifica enormemente il design del server
  - Un tipico server gestisce **~1000 richieste HTTP/secondo**; grandi motori di ricerca gestiscono **centinaia di migliaia** di query/secondo
- Piattaforma per YouTube, Gmail, social network, app mobili

**Evoluzione di HTTP:**

| Versione | Anno | Cambiamento principale |
|----------|------|------------------------|
| HTTP/1.0 | 1996 | Prima versione diffusa; connessioni **non persistenti** di default |
| HTTP/1.1 | 1997 | Connessioni **persistenti** di default, pipelining |
| HTTP/2 | 2015 | Multiplexing richieste/risposte sulla stessa connessione, priorità, compressione header (HPACK) |
| HTTP/3 | 2022 | Basato su **UDP/QUIC** (Quick UDP Internet Connection); ~30% più veloce; ~30% del traffico HTTP nel 2024 |

### 3.2 URL — Uniform Resource Locator

Le informazioni sul web sono chiamate **risorse** (o oggetti) e sono identificate da un **URL**:

```
[protocollo]://[usrinfo@][host][:porta][/path][?query][#fragment]
```

| Componente | Obbligatorio | Descrizione | Esempio |
|------------|-------------|-------------|--------|
| `[protocollo]` | Sì | Protocollo di accesso | `http`, `https`, `ftp` |
| `[usrinfo@]` | No | Username:password (deprecato per sicurezza) | `user:pass@` |
| `[host]` | Sì | Nome o IP del server | `www.unina.it` |
| `[:porta]` | No | Porta (inferita dal protocollo se assente) | `:8080` |
| `[/path]` | Sì | Percorso della risorsa nel server | `/someDept/page.html` |
| `[?query]` | No | Parametri di richiesta (preceduto da `?`) | `?title=SSC_Napoli` |
| `[#fragment]` | No | Elemento/sezione nella risorsa (preceduto da `#`) | `#sezione2` |

**Esempio:**
```
https://en.wikipedia.org/w/index.php?title=SSC_Napoli
# equivalente a:
https://en.wikipedia.org/wiki/SSC_Napoli
```

La maggior parte delle pagine web = **1 file HTML base** + oggetti aggiuntivi referenziati (immagini JPEG, video, applet, ecc.)

### 3.3 HTTP e il Protocollo di Trasporto

**HTTP usa principalmente TCP** per la sua affidabilità:
- Il client inizia una connessione TCP col server (porta 80 di default)
- Una volta stabilita, browser e server comunicano tramite le rispettive socket
- Il client invia messaggi HTTP nella propria socket, il server li riceve dalla propria
- TCP garantisce che le richieste/risposte HTTP arrivino integre a destinazione (**reliable data transfer**)

**HTTP/3 usa UDP/QUIC** (Quick UDP Internet Connection):
- Implementa affidabilità sopra UDP
- Stima ~30% più veloce della comunicazione TCP-only
- Circa il 30% del traffico HTTP è oggi su UDP [Wikipedia, 2024]

**Vantaggio dell'architettura a strati:** le applicazioni HTTP **non devono preoccuparsi** di raggiungibilità, perdita dati, correzione errori — delegano tutto al livello di trasporto.

### 3.4 Connessioni HTTP: Persistenti vs. Non Persistenti

#### 3.4.1 Connessioni Non Persistenti

Una connessione TCP per ogni oggetto. Esempio: 1 HTML + 10 JPEG → **11 connessioni TCP separate** (e 11 coppie di socket).

> HTTP definisce il **protocollo di comunicazione**, NON come i contenuti vengono visualizzati (quello è compito del browser).

**Tempo di risposta per ogni oggetto (con TCP):**
```
Totale ≈ 2 RTT + tempo di trasmissione del file
```
- **1° RTT**: TCP three-way handshake (SYN → SYN-ACK → ACK)
- **2° RTT**: richiesta HTTP + risposta HTTP

```
Client                    Server
  │── ACK + req HTTP ────►│
  │◄─ risposta HTTP ──────│
```

#### 3.4.2 Connessioni Persistenti

La connessione TCP rimane aperta dopo ogni risposta:
- Tutti gli oggetti di una pagina su **una singola connessione TCP**
- Risparmio di ~1-2 RTT per oggetto

**Pipelining (HTTP/1.1+):** richieste inviate senza aspettare le risposte precedenti.

| Tipo | Velocità | Risorse |
|------|----------|---------|
| Non persistente | Lenta | Molte |
| Persistente | Veloce | Poche |
| Persistente + Pipelining | Molto veloce | Poche |

### 3.5 Formato dei Messaggi HTTP

#### 3.5.1 Messaggio di Richiesta

I messaggi HTTP sono scritti in **ASCII text**, leggibili dagli umani. I campi sono separati da:
- `sp`: spazio ` `
- `cr`: carriage return `\r`
- `lf`: line feed `\n`

```
GET /somedir/page.html HTTP/1.1\r\n
Host: www.someschool.edu\r\n
Connection: close\r\n
User-agent: Mozilla/5.0\r\n
Accept-language: fr\r\n
\r\n
[corpo vuoto per GET]
```

**Struttura del messaggio:**
- **Linea di richiesta**: `METODO URL HTTP/Versione`
- **Header lines**: parametri della richiesta (numero e tipo variabili; possono essere anche personalizzati)
- **Corpo (body)**: specifico del metodo, contiene i dati

**Analisi degli header dell'esempio:**
- `Host: www.someschool.edu` — host dove risiede la risorsa (necessario perché un proxy potrebbe essere un intermediario)
- `Connection: close` — connessione non persistente (chiudi dopo la risposta)
- `User-Agent: Mozilla/5.0` — tipo di browser (il server può inviare versioni diverse dello stesso oggetto in base al tipo)
- `Accept-Language: fr` — il client preferisce la versione francese (se esiste)

**Metodi HTTP:**

| Metodo | Descrizione | Body richiesta | Uso |
|--------|-------------|----------------|-----|
| **GET** | Recupera una risorsa dal server | Vuoto | Navigazione web |
| **POST** | Invia dati al server (il body li contiene) | Contiene i dati | Form, upload |
| **HEAD** | Come GET ma il server risponde senza corpo | Vuoto | Debug, verifica esistenza risorse |
| **PUT** | Carica/sostituisce un oggetto su un percorso specifico | Contiene l'oggetto | Web publishing, REST API |
| **DELETE** | Cancella un oggetto sul server | Vuoto | REST API |

> **GET vs POST per i form**: un form HTML non usa necessariamente POST; spesso usa GET includendo i dati dell'utente nell'URL come query string (es. `?nome=Mario&email=mario@ex.it`).

#### 3.5.2 Messaggio di Risposta

```
HTTP/1.1 200 OK\r\n
Connection: close\r\n
Date: Tue, 18 Aug 2015 15:44:04 GMT\r\n
Server: Apache/2.2.3 (CentOS)\r\n
Last-Modified: Tue, 18 Aug 2015 15:11:03 GMT\r\n
Content-Length: 6821\r\n
Content-Type: text/html\r\n
\r\n
(dati oggetto...)
```

**Struttura del messaggio di risposta:**
- **Status line**: `HTTP/Versione CodiceStato Frase`
- **Header lines**: metadati della risposta
- **Corpo**: l'oggetto richiesto

**Analisi degli header dell'esempio:**
- `Connection: close` — il server chiuderà la connessione dopo questo messaggio
- `Date:` — data/ora di creazione/invio della risposta HTTP (non dell'oggetto)
- `Server:` — tipo di server web (analogo a User-Agent lato client)
- `Last-Modified:` — data/ora dell'ultima modifica dell'oggetto (importante per il **caching**)
- `Content-Length:` — numero di byte nel payload
- `Content-Type:` — tipo MIME dell'oggetto (es. `text/html`) — questo è il tipo "ufficiale", NON l'estensione del file

**Classi di codici di stato HTTP:**

| Classe | Range | Significato |
|--------|-------|-------------|
| **1xx** | 100-199 | Informazionale: info sulla richiesta |
| **2xx** | 200-299 | Successo: richiesta eseguita con successo |
| **3xx** | 300-399 | Reindirizzamento: azioni aggiuntive richieste al client |
| **4xx** | 400-499 | Errore client: richiesta non eseguibile per un problema del client |
| **5xx** | 500-599 | Errore server: richiesta non eseguibile per un problema del server |

**Codici più comuni:**

| Codice | Messaggio | Descrizione |
|--------|-----------|-------------|
| **200** | OK | Richiesta riuscita, informazione nella risposta |
| **301** | Moved Permanently | Risorsa spostata definitivamente; nuovo URL nell'header `Location` |
| **400** | Bad Request | Richiesta non comprensibile dal server (errore generico client) |
| **404** | Not Found | La risorsa richiesta non esiste su questo server |
| **505** | HTTP Version Not Supported | Versione HTTP non supportata dal server |

### 3.6 Cookie

**Cookie**: token digitale (ID alfanumerico) usato dai server per identificare un cliente specifico, aggirando la statelessness di HTTP.

**Motivazione:** la statelessness pura è una limitazione forte: il carrello Amazon dipende dal cliente, Netflix suggerisce contenuti in base alle preferenze, ecc.

**4 componenti della tecnologia cookie:**
1. Header `Set-cookie: ID` nella **risposta HTTP** del server (il server crea il cookie e lo invia)
2. Header `Cookie: ID` nelle **richieste successive** del client (il client lo allega automaticamente)
3. **File cookie** sul sistema del client (gestito dal browser)
4. **Database di back-end** sul server (associa ID cookie alle info del cliente)

**Flusso completo (esempio Amazon):**
```
Client                          Server Amazon
  │── HTTP request (senza cookie) ►│  Server crea ID=1678, entry nel DB
  │◄─ HTTP response + Set-cookie: 1678 │
  │  [browser salva cookie 1678]       │
  │── HTTP request + Cookie: 1678 ►│  Server riconosce utente 1678
  │◄─ HTTP response personalizzata │  traccia attività nel database
```

**Utilizzi:** carrello acquisti, login automatico, raccomandazioni prodotti, sessioni utente, preferenze.

**Attenzione — invasione della privacy:**
- Combinando cookie e informazioni dell'account (nome, email, indirizzo, carta di credito), i siti sanno molto sull'utente
- Alcune piattaforme vendono queste informazioni a terzi
- La GDPR europea impone consenso esplicito prima di impostare cookie non essenziali

### 3.7 Web Caching (Proxy)

Un **web cache** (o **proxy server**) soddisfa le richieste HTTP per conto del server originale, mantenendo copie degli oggetti recentemente richiesti nel proprio storage.

**Funzionamento:**
1. Browser invia tutte le richieste al proxy
2. **Hit** (oggetto trovato nella cache): proxy risponde direttamente → risposta rapida, nessuna trasmissione verso Internet
3. **Miss** (oggetto non trovato): proxy contatta il server originale, memorizza una copia locale, invia al browser

La cache è contemporaneamente **server** (quando fornisce oggetti ai client) e **client** (quando richiede oggetti ai server originali).

**Due motivi per cui il web caching è utile:**
1. **Riduzione del tempo di risposta**: connessione ad alta velocità tra client e cache — molto più veloce del server lontano su Internet
2. **Riduzione del traffico**: meno richieste verso Internet, riduzione dei costi di banda

**Hit rate tipico:** da 0.2 a 0.7 (20%-70% delle richieste servite localmente). Aumenta con più client che usano la cache.

**Cache del browser:** il browser stesso mantiene copie locali degli oggetti visitati — stesso principio, ma solo per quell'utente. La copia locale potrebbe non essere aggiornata (errore frequente).

**GET Condizionale** — meccanismo per evitare cache obsoleta:
```
Cache → Server:   GET /oggetto.html HTTP/1.1
                   If-Modified-Since: Tue, 18 Aug 2015 15:11:03 GMT

Se NON modificato: Server risponde  304 Not Modified  (nessun body, usa copia locale)
Se modificato:     Server risponde  200 OK  + nuovo oggetto
```

**Proxy istituzionali:** oltre alle prestazioni, i proxy possono essere usati per accedere a servizi istituzionali. Es: il proxy dell'UniNA (`proxy.unina.it`) fa sì che dal punto di vista del server originale tutte le richieste sembrino provenire dall'istituzione (utile per accesso a riviste scientifiche, risorse riservate, ecc.). Ci sono anche molti proxy commerciali/gratuiti su Internet.

### 3.8 Schemi e Appunti dalle Lavagne (Lezione 4)

![Board Lezione 04 - Pagina 1](assets/board_images/board_L04_p1.png)
*Figura 3.1 — Diagramma temporale dello scambio messaggi HTTP, handshaking TCP e stima dell'RTT.*

---

## 4. Posta Elettronica, P2P e DNS
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 4.1 Architettura della Posta Elettronica

La **posta elettronica** (e-mail) è una delle applicazioni Internet più antiche e importanti.

**Differenza da HTTP:** nella posta elettronica la comunicazione avviene **anche tra server** (non solo client-server). Servono quindi due protocolli distinti:
1. Tra **user agent e mail server** — POP3, IMAP, HTTP
2. Tra **mail server e mail server** — SMTP

**Componenti:**
- **User agent** (*client email*): applicazione per la gestione delle email (Outlook, Thunderbird, K-9 Mail, Pine)
- **Mail Server**: server sempre attivo che archivia email e mantiene **caselle di posta** (*mailbox*) specifiche per ogni utente

```
 Alice's User Agent                          Bob's User Agent
         │                                         │
         │ SMTP                                    │ POP3/IMAP/HTTP
         │                                         │
   Alice's Mail Server ──── SMTP ──── Bob's Mail Server
         (sender)                                 (receiver)
```

> Gli utenti non si scambiano le email direttamente (come avviene nella messaggistica istantanea). Si preferisce usare i mail server, più affidabili e specializzati.

**Protocolli:**
- **SMTP** (porta 25): tra mail server (invio) — client-side (sender) e server-side (receiver) su mail server
- **POP3** (porta 110): ricezione da mail server a user agent
- **IMAP**: ricezione avanzata da mail server a user agent
- **HTTP**: accesso web (Gmail, Yahoo!, webmail istituzionale)

### 4.2 SMTP — Simple Mail Transfer Protocol

SMTP usa **TCP porta 25**. È il protocollo principale tra mail server. Processo di invio (Alice → Bob):

1. Alice invoca il suo user agent, fornisce l'indirizzo email di Bob (`bob@someschool.edu`), compone il messaggio e istruisce l'user agent di inviarlo
2. L'user agent di Alice invia il messaggio al **mail server di Alice**, che lo mette in una **coda di messaggi** (*message queue*)
3. Il **client SMTP** di Alice (lato mail server) vede il messaggio nella coda, apre una **connessione TCP** al server SMTP di Bob (porta 25)
4. Se il server di Bob è down, il client riproverà più tardi
5. Dopo l'**handshake SMTP** (dove client e server si presentano), il client invia il messaggio nella connessione TCP
6. Il server SMTP di Bob riceve il messaggio e lo deposita nella **mailbox di Bob**
7. Bob invoca il suo user agent per leggere il messaggio quando preferisce

> **Vantaggio dei mail server:** i server sono sempre attivi, certificati, e possono ritentare la consegna in caso di fallimento (un processo computazionalmente costoso che non conviene delegare all'user agent).

**Handshake SMTP — esempio di sessione testuale:**
```
S: 220 hamburger.edu
C: EHLO crepes.fr
S: 250 Hello crepes.fr, pleased to meet you
C: MAIL FROM: <alice@crepes.fr>
S: 250 alice@crepes.fr ... Sender ok
C: RCPT TO: <bob@hamburger.edu>
S: 250 bob@hamburger.edu ... Recipient ok
C: DATA
S: 354 Enter mail, end with "." on a line by itself
C: Do you like ketchup?
C: How about pickles?
C: .
S: 250 Message accepted for delivery
C: QUIT
S: 221 hamburger.edu closing connection
```

### 4.3 Accesso alle Email — POP3, IMAP, HTTP

> Ricorda: SMTP è tra **mail server**. POP3/IMAP/HTTP sono tra **user agent e mail server**.

#### 4.3.1 POP3 — Post Office Protocol v3

Protocollo di accesso email estremamente semplice. TCP **porta 110**.

**3 fasi della sessione POP3:**

| Fase | Descrizione |
|------|-------------|
| **Authorization** | L'user agent invia username e password per autenticarsi |
| **Transaction** | L'user agent recupera messaggi, marca per cancellazione, ottiene statistiche |
| **Update** | Dopo il comando `quit`, il server cancella i messaggi marcati |

**Esempio di comandi POP3:**
```
C: USER alice
S: +OK
C: PASS secret
S: +OK user successfully logged on
C: LIST
S: 1 498   (messaggio 1, 498 byte)
S: 2 912   (messaggio 2, 912 byte)
S: .
C: RETR 1   (recupera messaggio 1)
S: [dati del messaggio]
S: .
C: DELE 1   (marca per cancellazione)
C: RETR 2
S: [dati del messaggio]
S: .
C: DELE 2
C: QUIT
S: +OK POP3 server signing off
```

**Limitazioni POP3:** solo download o cancellazione. Non supporta nativamente: ricerca in cartelle remote, organizzazione in cartelle sul server, accesso da più dispositivi.

#### 4.3.2 IMAP — Internet Mail Access Protocol

Funzionalità avanzate rispetto a POP3:
- **Gestione e creazione di cartelle** sul server
- **Ricerca** in cartelle remote per messaggi con criteri specifici
- Recupero **parziale dei messaggi** (es. solo header, solo allegati)
- Supporto per **più client** connessi contemporaneamente allo stesso server

Al contrario di POP3, con IMAP le email rimangono sul server (meglio per accesso da più dispositivi).

#### 4.3.3 HTTP per la Posta

Approccio mainstream introdotto da Hotmail negli anni '90, oggi dominante (Gmail, Yahoo!, UniNA Webmail):
- L'**user agent è il browser web** (non un'applicazione dedicata)
- La comunicazione tra utente e server avviene via **HTTP** (non POP3/IMAP)
- I **mail server continuano a usare SMTP** per scambiarsi email tra loro

**Confronto protocolli di accesso email:**

| Protocollo | Porta | Pro | Contro |
|------------|-------|-----|--------|
| **POP3** | 110 | Semplice, scarica email localmente | No cartelle remote, no multi-device |
| **IMAP** | 143 | Cartelle remote, multi-device, ricerca | Più complesso |
| **HTTP** | 80/443 | Nessuna installazione, ovunque | Dipende dalla connessione |

### 4.4 Applicazioni P2P e BitTorrent

A differenza di client-server, l'architettura P2P fa uso minimo (o nullo) di server centralizzati. Coppie di host (*peer*) intermittentemente connessi comunicano direttamente tra loro.

**P2P per il file sharing:** applicazione naturale del P2P
- In client-server: il server deve inviare il file a tutti i client (bottleneck sul server)
- In P2P: ogni peer che riceve il file può condividerlo con altri peer → più scalabile

**BitTorrent** — il protocollo P2P più popolare:
- ~150-170 milioni di utenti nel 2023

**Terminologia:**
- **Torrent**: insieme dei peer che partecipano alla distribuzione di un file specifico
- **Chunk**: parte del file (tipicamente **256 KB**)
- **Tracker**: nodo infrastrutturale che tiene traccia dei peer nel torrent (essenzialmente un server)

**Ciclo di vita di un peer:**
1. Si unisce al torrent → non ha ancora nessun chunk
2. Si registra con il **tracker** → riceve un sottoinsieme casuale di indirizzi IP dei peer attuali
3. Tenta connessioni TCP simultane con tutti i peer della lista (**vicini**)
4. Scarica chunk dai vicini e contemporaneamente carica chunk ai vicini
5. Periodicamente aggiorna la lista dei chunk disponibili dai vicini
6. Alla fine: può **uscire** (selfishly) o **restare** a fare seeding (altruistic)

**Strategia di download — Rarest-First:**
- I chunk con **meno copie disponibili** tra i vicini vengono prioritizzati
- Questo equalizza il numero di copie nel torrent e accelera la distribuzione

**Strategia di upload — Tit-for-Tat (Trading):**
- **Top-4 unchoked**: priorità ai 4 vicini con il **rate di upload più alto** verso di noi
  - La lista dei 4 best viene aggiornata ogni **10 secondi**
- **Optimistic unchoking**: ogni **30 secondi**, viene scelto casualmente un vicino aggiuntivo e gli vengono inviati chunk
  - Se lo scambio va bene, potrebbero entrare entrambi nelle rispettive liste top-4
  - Permette a peer con rate compatibili di trovarsi

> Il meccanismo tit-for-tat incentiva i peer a **contribuire**: chi carica di più ottiene download più veloci. I **free rider** (chi scarica senza caricare) vengono penalizzati.

### 4.5 DNS — Domain Name System

#### 4.5.1 Cos'è il DNS e perché è distribuito

Il **Domain Name System (DNS)** risolve la necessità di identificare gli host in due modi complementari:
- Gli **esseri umani** preferiscono nomi mnemonici (hostname): es. `www.unina.it`
- I **dispositivi di rete** preferiscono indirizzi IP a lunghezza fissa e struttura gerarchica: es. `143.225.15.50`

Il DNS è un **protocollo di livello applicazione** che gestisce la traduzione hostname → indirizzo IP in modalità client-server: un *DNS client* chiede a un *DNS server* la traduzione per un hostname specifico.

> I server DNS sono tipicamente macchine UNIX che eseguono il software **BIND** (Berkeley Internet Name Domain), in ascolto su **porta UDP 53**.

**Perché un DNS centralizzato sarebbe impossibile?**

Un singolo repository centralizzato non è praticabile per tre motivi fondamentali:
1. **Volume enorme di host**: miliardi di dispositivi connessi
2. **Distanza geografica**: latenze insopportabili tra utenti lontani
3. **Single point of failure**: un guasto blocca tutta Internet

Per questo il DNS è **distribuito e decentralizzato**.

---

#### 4.5.2 Gerarchia dello Spazio dei Nomi DNS

Lo spazio dei nomi DNS è organizzato da **ICANN** (Internet Corporation for Assigning Names and Numbers) in una struttura ad albero invertito con circa **250 TLD (Top-Level Domain)**.

```
                        . (root)
          ┌──────────────┼──────────────┐
         com            edu             it       ...
     ┌────┴────┐     ┌───┴───┐      ┌───┴───┐
  google    amazon  mit    unina  google  amazon
               |          |
             maps        dei
```

**Tipi di TLD:**
- **Generici (gTLD)**: `.com`, `.org`, `.edu`, `.net`, `.aero`, ...
- **Nazionali (ccTLD)**: `.it`, `.uk`, `.us`, `.tv`, ...
- Tutti gestiti da **registrar** nominati da ICANN

**Nomi di dominio — sintassi:**
- I nomi si leggono **dal basso verso l'alto** verso la root: es. `eng.mit.edu`
- **Percorso assoluto**: termina con un punto finale (es. `eng.mit.edu.`) → path dalla foglia alla radice
- **Percorso relativo**: interpretato rispetto a un dominio di riferimento
- Ogni dominio controlla l'allocazione dei sottodomini sotto di sé
- La creazione di un nuovo sottodominio richiede il **permesso del dominio padre**
- I nomi **non seguono confini geografici o fisici**
- È possibile registrarsi sotto più TLD (es. `ibm.com` e `ibm.us`)

> **Cyber-squatting**: pratica di acquistare domini solo per rivenderli successivamente a prezzi elevati alle aziende interessate.

---

#### 4.5.3 Zone DNS e Name Server

Lo spazio dei nomi DNS è suddiviso in **zone** (partizioni non sovrapposte). La suddivisione è a discrezione dell'amministratore della zona.

**Ogni zona contiene uno o più name server:**
- **Name server primario** (*primary*): ha il database autoritativo per la zona
- **Name server secondario** (*secondary*): copia di backup del primario, per ridondanza

```
          Zona A
    ┌─────────────────┐
    │   . (root)      │
    │    com          │
    └────────┬────────┘
             │
          Zona B
    ┌─────────────────┐
    │   example.com   │
    │  ┌───┐  ┌────┐  │
    │  │www│  │mail│  │
    └──┴───┴──┴────┴──┘
```

**Root server:** Ci sono **13 root server** (da `a.root-servers.net` a `m.root-servers.net`), altamente replicati in tutto il mondo. Essendo molto occupati, di norma restituiscono informazioni sulle **zone inferiori** (cioè i riferimenti ai TLD server), non record individuali.

---

#### 4.5.4 Resource Record DNS

Ogni entry nel database DNS è un **Resource Record (RR)** con 5 campi:

| Campo | Nome | Descrizione |
|-------|------|-------------|
| `NAME` | Domain Name | Il dominio a cui il record si applica; è la **chiave di ricerca** principale per le query DNS. Normalmente esistono più record per ciascun dominio, distribuiti su server diversi. |
| `TTL` | Time To Live | Durata del record in secondi. Lunga per host stabili (es. `86400` = 1 giorno), breve per host volatili (es. `60` = 1 minuto). Valore massimo: 2³¹−1 ≈ 68 anni. |
| `CLASS` | Classe | Sempre `IN` (Internet) per i record Internet; altri codici raramente usati. |
| `TYPE` | Tipo | Indica il tipo di record (vedi tabella sotto). |
| `RDATA` | Value | Il valore effettivo; dipende dal tipo di record: può essere un dominio, un valore numerico o una stringa ASCII. |

**Tipi di record DNS:**

| Tipo | Descrizione | Uso |
|------|-------------|-----|
| **A** | Indirizzo IPv4 a 32 bit per un'interfaccia dell'host | Mappatura hostname → IP |
| **AAAA** | Indirizzo IPv6 (equivalente di A per IPv6) | Mappatura hostname → IPv6 |
| **NS** | Name Server: fornisce il nome del name server autorevole per il dominio | Delegazione della zona |
| **MX** | Mail eXchange: indica l'host che accetta email per il dominio | Instradamento email |
| **CNAME** | Canonical Name: permette alias; la risoluzione DNS procede col nuovo nome | Alias hostname |
| **PTR** | Pointer: alias usato per **reverse lookup** (IP → nome); la risoluzione NON procede, viene restituito il nome | Reverse DNS |
| **SOA** | Start of Authority: informazioni sul server della zona, email dell'amministratore, numeri di serie | Metadati zona |

**Esempio di insieme di record per il dominio `cs.vu.nl`:**
```
cs.vu.nl.    86400  IN  SOA   ns1.cs.vu.nl. admin.vu.nl. 2024010101 3600 900 604800 86400
cs.vu.nl.    86400  IN  NS    ns1.cs.vu.nl.
cs.vu.nl.    86400  IN  NS    ns2.cs.vu.nl.
cs.vu.nl.    86400  IN  MX    10 mail.cs.vu.nl.
www.cs.vu.nl 86400  IN  A     130.37.20.20
ftp.cs.vu.nl 86400  IN  CNAME www.cs.vu.nl.
ns1.cs.vu.nl 86400  IN  A     130.37.20.1
```

---

#### 4.5.5 DNS Resolver (Local DNS Server)

Il **local DNS server** (o **DNS resolver**) è un tipo speciale di server DNS che:
- **Non appartiene strettamente** alla gerarchia dei name server
- È tipicamente gestito dagli **ISP** o dalle organizzazioni locali
- Quando un host si connette a un ISP, l'ISP gli fornisce l'indirizzo IP del local DNS server

**Funzionamento del resolver:**
- Quando un host esegue una query DNS, la invia al **local DNS server**
- Il local DNS server agisce da **proxy**, inoltrandola alla gerarchia DNS
- Restituisce la risposta finale all'host (risposta completa o errore)

**Resolver pubblici noti:**
| Provider | Indirizzo primario | Indirizzo secondario |
|----------|--------------------|----------------------|
| Google Public DNS | `8.8.8.8` | `8.8.4.4` |
| Cloudflare | `1.1.1.1` | `1.0.0.1` |
| OpenDNS | `208.67.222.222` | `208.67.220.220` |

---

#### 4.5.6 Risoluzione dei Nomi DNS: Query Ricorsive e Iterative

Il processo di risoluzione avviene in due modalità che spesso coesistono nella stessa richiesta.

**Query ricorsiva:** il client chiede al server di fornire la risposta completa, e il server si occupa di tutta la risoluzione iterativa (il client riceve o la risposta finale o un errore).

**Query iterativa:** il server risponde con il "meglio che sa" — se non ha la risposta, restituisce l'indirizzo di un altro server DNS da contattare; il client poi contatta direttamente il prossimo server.

**Schema tipico di una risoluzione (esempio: `www.amazon.com`):**

```
  Host (client)             Local DNS server            Root Server
      │                           │                          │
      │── query ricorsiva ────────►│                          │
      │   "www.amazon.com?"        │── query iterativa ──────►│
      │                           │   "www.amazon.com?"      │
      │                           │◄──────────────────────── │
      │                           │   "Non so, vai su        │
      │                           │    TLD server .com"      │
      │                           │                      TLD Server (.com)
      │                           │── query iterativa ──────►│
      │                           │   "www.amazon.com?"      │
      │                           │◄─────────────────────────│
      │                           │   "Non so, vai su        │
      │                           │    ns1.amazon.com"       │
      │                           │                      Authoritative DNS
      │                           │── query iterativa ──────►│ (amazon.com)
      │                           │   "www.amazon.com?"      │
      │                           │◄─────────────────────────│
      │                           │   "205.251.242.103"      │
      │◄── risposta completa ─────│                          │
      │    "205.251.242.103"       │                          │
```

**Regola pratica:**
- I **local DNS server** gestiscono le query ricorsive (servizio per i loro host)
- I **server occupati** (root, TLD) gestiscono quasi sempre solo query **iterative** (non ricorsive), per non sovraccaricarsi

**Processo di risoluzione — algoritmo:**
1. L'host invia la query al **local name server**
2. Se il dominio rientra nella giurisdizione (zona) del server locale → viene restituito un **record autoritativo**
3. Altrimenti, il local server gestisce la query ricorsivamente:
   - Se ha l'indirizzo → lo restituisce
   - Se ha l'indirizzo del name server per una zona inferiore → lo usa per una query diretta
   - Il processo continua iterativamente fino a trovare l'indirizzo

> **I root server** sono consultati solo **in assenza di qualsiasi informazione** su un certo dominio.

---

#### 4.5.7 Record Autoritativi vs. Cached

I record DNS si distinguono in due categorie fondamentali:

| Tipo | Descrizione |
|------|-------------|
| **Autoritativo** | Proviene direttamente dal name server che gestisce la zona; è sempre aggiornato e affidabile |
| **Cached (in cache)** | Proveniente da una risposta precedente, memorizzato temporaneamente; **scade alla scadenza del TTL** |

**Caching DNS — ottimizzazione delle prestazioni:**
- **Tutte le risposte DNS vengono messe in cache** dal local DNS server
- Se arriva una richiesta per `cs.mit.edu` e il server ha già in cache l'indirizzo del name server per `mit.edu`, può interrogare direttamente quel server senza passare dai root
- I root server vengono interrogati **solo** in assenza di qualsiasi informazione su un certo dominio
- I record cached hanno un TTL che, alla scadenza, li rende invalidi

> **Prestazioni:** La caching riduce drasticamente il numero di query ai root server e accelera le risoluzioni per i domini frequentemente visitati.

---

#### 4.5.8 Aliasing DNS (CNAME) e Host Aliasing

Il DNS fornisce un **servizio di aliasing** che permette di associare nomi complicati/lunghi (nomi *canonici*) a nomi più semplici/corti (*alias*).

**Host aliasing:** host con hostname complicati possono essere associati ad alias più mnemonici.

Esempio:
```
# Il nome canonico (reale):
relay1.west-coast.enterprise.com.   IN  A      192.0.2.1

# L'alias (più semplice):
www.enterprise.com.   IN  CNAME  relay1.west-coast.enterprise.com.
```

Quando si risolve `www.enterprise.com`:
1. Il DNS trova il record CNAME → ottiene il nome canonico `relay1.west-coast.enterprise.com`
2. Risolve il nome canonico → ottiene l'IP `192.0.2.1`
3. **Differenza con PTR**: con CNAME la risoluzione prosegue con il nuovo nome; con PTR la risoluzione si ferma e viene restituito il nome.

> Un'applicazione può invocare il DNS per ottenere sia il nome canonico per un alias sia il corrispondente IP.

---

#### 4.5.9 DNS e Distribuzione del Carico (Round-Robin DNS)

Il DNS può essere usato per la **distribuzione del carico** tra server replicati.

- Siti molto trafficati (Google, Amazon, CNN, ecc.) sono replicati su **più server**, ognuno su un end-system diverso con un IP diverso
- Il database DNS contiene l'**insieme di indirizzi IP** per lo stesso hostname canonico
- Quando i client eseguono una query DNS per quel nome, il server **ruota l'ordine** in cui gli indirizzi vengono restituiti → i client tendono a usare IP diversi → il carico si distribuisce

```
# Esempio: amazon.com con 3 server replicati
amazon.com.   IN  A  205.251.242.103
amazon.com.   IN  A  205.251.242.104
amazon.com.   IN  A  205.251.242.105
# Il DNS ruota l'ordine ad ogni risposta
```

---

#### 4.5.10 Strumento pratico: `nslookup`

`nslookup` è un tool da riga di comando che permette di eseguire manualmente le query DNS che normalmente gestisce il local DNS server.

**Utilizzo base:**
```bash
# Query A record (hostname → IP)
nslookup www.unina.it

# Query con server DNS specifico
nslookup www.unina.it 8.8.8.8

# Reverse lookup (IP → hostname)
nslookup 143.225.15.50

# Query di tipo specifico
nslookup -type=MX unina.it
nslookup -type=NS unina.it
nslookup -type=SOA unina.it
```

**Interpretazione dell'output:**
```
Server:   127.0.0.53          ← Il default server è il router locale (porta 53)
Address:  127.0.0.53#53

Non-authoritative answer:      ← I record sono cached (non vengono dal server autoritativo)
Name:     www.unina.it
Address:  143.225.15.50
```

> I record **non-authoritativi** (cached) **non provengono** dal DNS server che gestisce la zona; il local server ha gestito tutta la risoluzione tramite query iterative e ha messo in cache il risultato.

---

#### 4.5.11 Riepilogo: Caratteristiche Principali del DNS

| Caratteristica | Dettaglio |
|----------------|-----------|
| **Trasporto** | UDP, porta 53 (TCP per trasferimenti di zona) |
| **Architettura** | Distribuita, gerarchica, decentralizzata |
| **Root server** | 13 (a–m.root-servers.net), altamente replicati |
| **Gestione** | ICANN per TLD; registrar per sottodomini |
| **Caching** | Tutti i record vengono cachati con scadenza TTL |
| **Query ricorsive** | Gestite dai local DNS server per i loro client |
| **Query iterative** | Usate dai server occupati (root, TLD) |
| **Software tipico** | BIND (Berkeley Internet Name Domain) su UNIX |

### 4.6 Schemi e Appunti dalle Lavagne (Lezione 7)

![Board Lezione 07 - Pagina 1](assets/board_images/board_L07_p1.png)
*Figura 4.1 — Tabella dei record DNS e formati di risorsa.*

![Board Lezione 07 - Pagina 2](assets/board_images/board_L07_p2.png)
*Figura 4.2 — Flusso delle interrogazioni DNS nella gerarchia dei server.*

![Board Lezione 07 - Pagina 3](assets/board_images/board_L07_p3.png)
*Figura 4.3 — Esempio pratico di risoluzione dei nomi tra server autoritativi.*

![Board Lezione 07 - Pagina 4](assets/board_images/board_L07_p4.png)
*Figura 4.4 — Caching locale e gestione del campo Time To Live (TTL).*

---

## 5. Programmazione di Rete con i Socket
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 5.1 Socket nell'Architettura a Strati

Le socket implementano (come black-box) le funzionalità TCP/UDP e IP.

```
  La Tua Applicazione
  ──────────────────────
  Transport   Socket API
  ──────────────────────
  Network (IP)
  ──────────────────────
  Access Layer  (OS + HW)
```

In Unix: **Berkeley sockets** (BSD/POSIX) — API native in C.

### 5.2 Strutture Dati per le Socket

```c
#include <netinet/in.h>
#include <arpa/inet.h>

struct sockaddr_in {
    short          sin_family;   // AF_INET (IPv4)
    unsigned short sin_port;     // es. htons(3490)
    struct in_addr sin_addr;     // indirizzo IP
    char           sin_zero[8];  // padding (zero)
};

struct in_addr {
    unsigned long s_addr;  // IP (usa inet_addr() o INADDR_ANY)
};
```

### 5.3 Creazione della Socket

```c
#include <sys/socket.h>
int sockfd = socket(int domain, int type, int protocol);
// domain: AF_INET
// type: SOCK_STREAM (TCP) o SOCK_DGRAM (UDP)
// protocol: tipicamente 0
```

> Le socket seguono la filosofia Unix "tutto è un file": associate a un file descriptor.

### 5.4 Binding della Socket

```c
int val = bind(int socket, const struct sockaddr *address, socklen_t address_len);
// socket: file descriptor della socket
// address: puntatore a sockaddr con IP e porta
//   address.sin_addr spesso impostato a INADDR_ANY: accetta connessioni da tutti gli indirizzi
// address_len: sizeof(struct sockaddr)
// Ritorna 0 su successo, -1 su errore
```

> `bind()` è **obbligatorio per i server** (devono essere raggiungibili su una porta nota). Per i client è **opzionale** (l'OS assegna automaticamente una porta libera).

### 5.4.1 Chiusura della Socket

```c
#include <unistd.h>
int val = close(int socket);
// socket: file descriptor della socket da chiudere
// val: 0 su successo, -1 su errore
```

> Le socket seguono la filosofia Unix "tutto è un file": `close()` rilascia il file descriptor proprio come per i file normali.

### 5.5 Programmazione Socket UDP

**Flusso client-server:**

```
Client UDP              Server UDP
──────────────          ──────────────
Crea Socket             Crea Socket
                        Bind (porta)
                        Attendi msg
Invia Msg ────────────►
◄───────────── Risposta
Chiudi Socket
```

**Funzioni di invio/ricezione:**

```c
// Invio UDP
int ob = sendto(int osock, const void *obuf, size_t olen, int flags,
                const struct sockaddr *oaddr, socklen_t oaddr_len);

// Ricezione UDP
int ib = recvfrom(int isock, void *ibuf, size_t ilen, int flags,
                  struct sockaddr *iaddr, socklen_t *iaddr_len);
```

**Esempio Client UDP:**

```c
int main() {
    int sockfd = socket(AF_INET, SOCK_DGRAM, 0);
    struct sockaddr_in servaddr;
    memset(&servaddr, 0, sizeof(servaddr));
    servaddr.sin_family    = AF_INET;
    servaddr.sin_port      = htons(8080);
    servaddr.sin_addr.s_addr = INADDR_ANY; // o inet_addr("192.168.1.10")

    sendto(sockfd, "Hello", 5, 0, (struct sockaddr*)&servaddr, sizeof(servaddr));

    char buf[1024]; socklen_t len = sizeof(servaddr);
    int n = recvfrom(sockfd, buf, 1024, MSG_WAITALL, (struct sockaddr*)&servaddr, &len);
    buf[n] = '\0'; printf("Ricevuto: %s\n", buf);
    close(sockfd); return 0;
}
```

**Esempio Server UDP:**

```c
int main() {
    int sockfd = socket(AF_INET, SOCK_DGRAM, 0);
    struct sockaddr_in servaddr, cliaddr;
    memset(&servaddr, 0, sizeof(servaddr));
    servaddr.sin_family = AF_INET;
    servaddr.sin_addr.s_addr = INADDR_ANY;
    servaddr.sin_port = htons(8080);
    bind(sockfd, (struct sockaddr*)&servaddr, sizeof(servaddr));

    char buf[1024]; socklen_t len = sizeof(cliaddr);
    int n = recvfrom(sockfd, buf, 1024, MSG_WAITALL, (struct sockaddr*)&cliaddr, &len);
    buf[n] = '\0'; printf("Ricevuto: %s\n", buf);
    sendto(sockfd, "Hello from server", 17, 0, (struct sockaddr*)&cliaddr, len);
    close(sockfd); return 0;
}
```

> **Socket UDP identificata da:** indirizzo IP di destinazione + porta di destinazione.

### 5.6 Programmazione Socket TCP

In TCP si effettua un **handshake** prima di trasmettere. Server-side: **due socket**.
- **Welcoming socket**: sempre attiva, accetta handshake
- **Socket client-specifica**: creata dopo l'handshake

```
Client TCP              Server TCP
──────────────          ──────────────────────────
Crea Socket             Crea Socket + Bind
                        listen() — coda connessioni
Connetti (SYN) ───────►
                        accept() — nuova socket
Invia Msg ────────────►
◄───────────── Risposta
Chiudi Socket           Chiudi socket client
```

**Funzioni specifiche TCP:**

```c
int val = connect(int socket, const struct sockaddr *address, socklen_t len);
int val = listen(int socket, int backlog);  // backlog = max connessioni in coda
int new_sockfd = accept(int socket, struct sockaddr *address, socklen_t *len);
int ob = send(int osock, const void *obuf, size_t olen, int flags);
int ib = read(int isock, void *ibuf, size_t ilen);
```

**Esempio Server TCP:**

```c
int main() {
    int sockfd = socket(AF_INET, SOCK_STREAM, 0);
    struct sockaddr_in servaddr, cliaddr;
    memset(&servaddr, 0, sizeof(servaddr));
    servaddr.sin_family = AF_INET;
    servaddr.sin_addr.s_addr = INADDR_ANY;
    servaddr.sin_port = htons(8080);

    bind(sockfd, (struct sockaddr*)&servaddr, sizeof(servaddr));
    listen(sockfd, 3);

    int addrlen = sizeof(cliaddr);
    int new_socket = accept(sockfd, (struct sockaddr*)&cliaddr, (socklen_t*)&addrlen);

    char buf[1024];
    int n = read(new_socket, buf, 1024);
    printf("Ricevuto: %s\n", buf);
    send(new_socket, "Hello from server", 17, 0);

    close(new_socket); close(sockfd); return 0;
}
```

> **Socket TCP identificata da 4 elementi:** IP sorgente, porta sorgente, IP destinazione, porta destinazione.

> **Socket UDP identificata da 2 elementi:** IP destinazione + porta destinazione. Questo permette a un server UDP di ricevere messaggi da più client sulla stessa socket; con TCP serve una socket diversa per ogni client.

**Riepilogo funzioni socket:**

| Funzione | UDP/TCP | Descrizione |
|----------|---------|-------------|
| `socket()` | Entrambi | Crea una socket |
| `bind()` | Entrambi | Associa socket a IP:porta (obbligatorio per server) |
| `sendto()` | UDP | Invia datagramma (include indirizzo destinazione) |
| `recvfrom()` | UDP | Riceve datagramma (ottiene indirizzo sorgente) |
| `connect()` | TCP | Avvia connessione (client-side) |
| `listen()` | TCP | Apre coda connessioni (server-side, max = backlog) |
| `accept()` | TCP | Crea socket client-specific (server-side) |
| `send()` | TCP | Invia dati su connessione esistente |
| `read()` | TCP | Riceve dati da connessione esistente |
| `close()` | Entrambi | Chiude la socket |

### 5.7 Schemi e Appunti dalle Lavagne (Lezioni 8 e 9)

![Board Lezione 08 - Pagina 1](assets/board_images/board_L08_p1.png)
*Figura 5.1 — Comunicazione tra processi remoti tramite socket come porta di interfaccia tra applicazione e SO.*

![Board Lezione 08 - Pagina 2](assets/board_images/board_L08_p2.png)
*Figura 5.2 — Incapsulamento del payload applicativo all'interno del segmento di trasporto.*

![Board Lezione 09 - Pagina 1](assets/board_images/board_L09_p1.png)
*Figura 5.3 — Costruzione di una richiesta HTTP raw da zero inviata direttamente su socket TCP.*

---

## 6. Il Livello di Trasporto — UDP e Trasferimento Affidabile
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 6.1 Dal Livello Applicazione al Livello di Trasporto

Un **protocollo di trasporto** fornisce **comunicazione logica process-to-process** tra processi applicativi su host diversi. Dal punto di vista dell'applicazione, i due processi sembrano direttamente connessi, anche se si trovano su reti fisicamente lontane.

Il livello di rete (IP) si occupa di consegnare datagrammi **da host a host** (host-to-host delivery). Il livello di trasporto va un passo oltre: smista i messaggi al **processo corretto** all'interno di quell'host, usando le **socket** e i **numeri di porta** come meccanismo di indirizzamento applicativo.

> [!NOTE]
> Il software del livello di trasporto viene eseguito **solo negli host terminali** (edge della rete), non nei router intermedi, che operano solo fino al livello di rete.

### 6.2 Responsabilità del Livello di Trasporto

I protocolli di trasporto (UDP e TCP) hanno quattro responsabilità principali. UDP garantisce solo le prime due, TCP le garantisce tutte:

| # | Responsabilità | UDP | TCP | Descrizione |
|---|---------------|:---:|:---:|-------------|
| 1 | **Process-to-process delivery** | ✅ | ✅ | Consegna al processo corretto tramite porte e socket (Mux/Demux). |
| 2 | **Integrity checking** | ✅ | ✅ | Verifica integrità del dato tramite Checksum. |
| 3 | **Reliable data transfer (RDT)** | ❌ | ✅ | Consegna in ordine, senza perdite o duplicati. |
| 4 | **Congestion & Flow control** | ❌ | ✅ | Regola il tasso di invio per non sovraccaricare la rete o il buffer del ricevente. |

### 6.3 Multiplexing e Demultiplexing

A livello applicativo, più processi (browser, Spotify, client email) accedono alla rete simultaneamente. Per smistare i messaggi al processo corretto si usano le **socket**, identificate da **numeri di porta** (16 bit, range 0–65535):
- **Well-known ports (0–1023)**: riservate per protocolli noti (vedi tabella), gestite da IANA.
- **Registered ports (1024–49151)**: usabili da applicazioni note ma non "standard".
- **Ephemeral ports (49152–65535)**: assegnate dinamicamente dall'OS ai client.

| Porta | Protocollo |
|-------|-----------|
| 20/21 | FTP (dati/controllo) |
| 22 | SSH |
| 25 | SMTP (email) |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |
| 110 | POP3 |
| 143 | IMAP |
| 161 | SNMP |

- **Multiplexing (Mittente)**: raccoglie dati da più socket, incapsula ognuno con header (porte sorgente/destinazione) e li passa al livello di rete come segmenti o datagrammi.
- **Demultiplexing (Destinatario)**: esamina l'header del segmento in arrivo e dirige i dati alla socket corretta.

> [!TIP]
> **Identificazione delle socket:**
> - **Socket UDP**: identificata da **2 elementi** — IP destinazione + Porta destinazione. Due datagrammi da client distinti verso lo stesso IP/porta finiranno nella **stessa socket** server.
> - **Socket TCP**: identificata da **4 elementi** — IP sorgente, Porta sorgente, IP destinazione, Porta destinazione. Il server crea una **socket dedicata per ogni singolo client** (e spesso un thread separato).

**Strumento nmap** per esplorare le porte aperte su un host:
```bash
sudo nmap [target]              # Port-scan classico
sudo nmap -sV [target]          # Identifica i servizi sulle porte
sudo nmap --top-port N [target] # Scansiona solo le prime N porte più usate
```

### 6.4 UDP — User Datagram Protocol

**UDP** è il protocollo minimalista del livello di trasporto: aggiunge le porte (mux/demux) e un checksum a IP, null'altro. È **connectionless** (nessun handshake) e **best-effort** (nessuna garanzia di consegna, ordine o controllo di flusso/congestione).

**Perché usare UDP invece di TCP?**

| Motivo | Spiegazione |
|--------|-------------|
| **Controllo applicativo** | L'applicazione decide esattamente quando e quanto spedire, senza subire i ritardi delle ritrasmissioni TCP. Cruciale nel real-time (VoIP, streaming live, giochi online). |
| **Connessione immediata** | Nessun handshake iniziale → nessun ritardo di setup. Per questo DNS usa UDP: aggiunge latenza zero. |
| **Nessuno stato** | Il server UDP non mantiene tabelle di connessione, timer, parametri di congestione → può gestire **molti più client** contemporaneamente (scalabilità). |
| **Overhead minimo** | Header UDP di soli **8 byte** vs. 20 byte dell'header TCP. |

**Applicazioni tipiche:**

| Servizio | Trasporto | Motivo |
|----------|-----------|--------|
| DNS | UDP | Latenza minima, query brevi, retry applicativo se perso |
| SNMP | UDP | Monitoring di rete in condizioni già stressate |
| Streaming multimediale | UDP o TCP | Piccola perdita tollerabile; ritardi no |
| VoIP / conferenze | UDP o TCP | Priorità: bassa latenza |
| HTTP, FTP, Email | TCP | Integrità del dato obbligatoria |

> [!WARNING]
> Usare UDP massivamente senza controllo applicativo del tasso (es. streaming aggressivo) porta a *UDP-induced packet loss*: i router vanno in overflow e crollano anche le connessioni TCP vicine. Alcune implementazioni aggiungono controllo di congestione a livello applicativo (**QUIC**, usato da HTTP/3, fa proprio questo sopra UDP).

### 6.5 Formato e Checksum del Datagramma UDP

```
  0      7 8     15 16    23 24    31
 ┌────────────────┬────────────────┐
 │  Source Port   │  Dest Port     │  ← 4 byte
 ├────────────────┼────────────────┤
 │    Length      │   Checksum     │  ← 4 byte
 ├────────────────┴────────────────┤
 │         Data (N byte)           │
 └─────────────────────────────────┘
```

Il campo **Length** include header + dati (minimo 8 byte, solo header vuoto).

**Calcolo del Checksum (lato mittente):**
1. Si divide il datagramma in parole da 16 bit.
2. Si sommano tutte le parole; se la somma supera 16 bit, il riporto viene aggiunto al risultato (wrap-around).
3. Si fa il **complemento a 1** (si invertono tutti i bit): questo è il Checksum.

**Verifica (lato destinatario):** Si sommano tutte le parole del datagramma ricevuto (checksum incluso). Se il risultato è `1111111111111111` (tutti 1), il pacchetto è integro. Se un solo bit è `0`, c'è un errore e il pacchetto viene scartato.

**Esempio numerico completo:**
```
Parola 1:  0110011001100000
Parola 2:  0101010101010101
Parola 3:  1000111100001100

Somma 1+2: 1011101110110101
+ Parola 3: 1000111100001100
=         10100101011000001  ← overflow!
Wrap:      0100101011000010  (+1 per il riporto)

Checksum = complemento a 1 = 1011010100111101

Verifica: 0100101011000010 + 1011010100111101 = 1111111111111111 ✅
```

### 6.6 Il Problema del Trasferimento Dati Affidabile (RDT)

Come si costruisce un canale affidabile sopra un livello di rete inaffidabile (IP)?

**L'analogia del treno:** Siamo in stazione ad aspettare il Treno 6. Un altoparlante gracchiante (canale inaffidabile) annuncia: *"Il Treno 6 arriverà sul binario 9"*. Se la comunicazione è corrotta, potremmo sentire:
- `"Il Treno 7 arriverà sul binario 9"` → alterazione non evidente
- `"Il Treno %&! arriverà sul binario 9"` → corruzione riconoscibile
- Nessun annuncio → pacchetto smarrito

Capire che c'è stato un errore è solo il primo passo. Rimediare è il cuore dell'RDT.

**Tre garanzie che un canale affidabile deve offrire:**
1. Nessun bit corrotto durante il trasferimento.
2. Nessun bit perso o duplicato.
3. I bit arrivano nell'esatto ordine di invio.

### 6.7 Stop-and-Wait (ARQ — Automatic Repeat reQuest)

Il protocollo più semplice per implementare l'RDT è lo **Stop-and-Wait**: il mittente spedisce un pacchetto e **si ferma** ad aspettare il feedback prima di inviarne un altro.

**Tipi di feedback:**
- **ACK** (*Positive Acknowledgment*): pacchetto ricevuto correttamente.
- **NCK** (*Negative Acknowledgment*): errore rilevato, ritrasmettere.

**Problema 1 — ACK corrotto:** Se l'ACK stesso si corrompe in transito, il mittente non sa se ritrasmettere (rischio di duplicati). **Soluzione:** aggiungere un **Numero di Sequenza** al pacchetto. In stop-and-wait basta **1 bit** (alternante tra `0` e `1`) per distinguere il pacchetto corrente da una sua ritrasmissione.

**Problema 2 — Pacchetto perso (Deadlock):** Se il pacchetto sparisce nel nulla, il ricevente non manda nulla, e il mittente aspetta per sempre. **Soluzione:** il **Timeout**. Se l'ACK non arriva entro un certo tempo, il mittente ritrasmette. Il timeout deve essere > RTT (ma stimarlo esattamente è difficile).

#### Prestazioni dello Stop-and-Wait: un disastro annunciato

**Scenario tipico** (due host coast-to-coast USA):
- Link **R** = 1 Gbps
- RTT = 30 ms
- Pacchetto **L** = 1000 byte = 8000 bit

> **t_trasm** = L / R = 8000 / 10^9 = 0.000008 s = **8 µs**

> **U_mittente** = t_trasm / (RTT + t_trasm) = 0.000008 / 0.030008 ≈ **0.00027 (0.027%)**

Il mittente lavora solo lo 0.027% del tempo, con un **throughput effettivo di soli 27 kbps** su un link da 1 Gbps. La soluzione è il Pipelining.

### 6.8 Pipelining: Go-Back-N e Selective Repeat

Per sfruttare la larghezza di banda, il mittente invia più pacchetti senza aspettare gli ACK — riempie la "pipeline". Ciò richiede:
- Numeri di sequenza con range più ampio.
- Buffer (sia lato mittente che ricevente).

Esistono due approcci principali:

#### Go-Back-N (GBN)

Il mittente mantiene una **finestra scorrevole** di al massimo **N** pacchetti non ancora confermati.

**Regole lato mittente:**
- Può inviare i pacchetti nella finestra `[base, base+N-1]` senza aspettare.
- Mantiene **un unico timer** per il pacchetto più vecchio non ACK-ato (il `base`).
- In caso di Timeout, ritrasmette **tutti** i pacchetti nella finestra, dal `base` in poi.

**Regole lato ricevente (semplicissimo):**
- Accetta **solo pacchetti in ordine** (seq == `expected`).
- Se arriva un pacchetto fuori ordine, lo **scarta** (non lo bufferizza) e ri-invia l'ACK cumulativo dell'ultimo pacchetto in ordine ricevuto.
- Mantiene un solo variabile: `nextseqnum` (il prossimo numero atteso).

**Vantaggi:** Ricevente semplice (nessun buffer). **Svantaggi:** Se un pacchetto viene perso in una finestra grande, si ritrasmettono inutilmente tutti i pacchetti successivi già ricevuti correttamente.

#### Selective Repeat (SR)

Il mittente ritrasmette **solo i pacchetti specificamente persi** (identificati dal loro timeout individuale).

**Regole lato mittente:**
- Finestra di dimensione **N**, come GBN.
- **Timer individuale** per ogni pacchetto inviato ma non ancora ACK-ato.
- In caso di Timeout su `n`, ritrasmette **solo** `n`.

**Regole lato ricevente (più complesso):**
- **Bufferizza** i pacchetti fuori ordine nella sua finestra ricevente.
- Invia ACK **individuali** (non cumulativi) per ogni pacchetto correttamente ricevuto, anche se fuori ordine.
- Quando tutti i gap sono colmati, consegna il blocco all'applicazione e fa avanzare la finestra.

> [!CAUTION]
> **Vincolo fondamentale di SR:** Per evitare che il ricevente scambi un pacchetto *ritrasmesso* con uno *nuovo* (aliasing), il numero di sequenza deve essere sufficientemente grande:
> > **Seq. Space ≥ 2 × Window Size  ⇒  Seq ≥ 2N**

**Confronto riepilogativo:**

| Caratteristica | Go-Back-N | Selective Repeat |
|----------------|-----------|-----------------|
| Buffer al ricevente | ❌ No | ✅ Sì |
| In caso di perdita | Ritrasmette tutta la finestra | Ritrasmette solo il perso |
| Tipo di ACK | Cumulativo | Individuale |
| Timer | Uno solo (per `base`) | Uno per pacchetto |
| Req. Seq. Space | `≥ N` | `≥ 2N` |
| Efficienza con alta perdita | Bassa | Alta |
| Complessità ricevente | Bassa | Media |

### 6.9 Schemi e Appunti dalle Lavagne (Lezioni 10, 11 e 12)

![Board Lezione 10 - Pagina 1](assets/board_images/board_L10_p1.png)
*Figura 6.1 — Trasporto: comunicazione logica process-to-process vs. host-to-host del livello rete.*

![Board Lezione 11 - Pagina 1](assets/board_images/board_L11_p1.png)
*Figura 6.2 — Caso critico: Timeout < RTT in stop-and-wait, duplicazione dei pacchetti con s=0/1.*

![Board Lezione 12 - Pagina 1](assets/board_images/board_L12_p1.png)
*Figura 6.3 — Perché l'affidabilità end-to-end non può essere delegata al livello di rete IP.*

---

## 7. Il Protocollo TCP
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 7.1 Caratteristiche di TCP

**TCP (Transmission Control Protocol)** è il protocollo di trasporto affidabile di Internet. Si distingue da UDP per le seguenti proprietà:

| Proprietà | Descrizione |
|-----------|-------------|
| **Connection-oriented** | Prima della trasmissione, i due host eseguono un **handshake** per sincronizzarsi e allocare le risorse (buffer, variabili). |
| **Affidabile** | Implementa ACK, ritrasmissioni, checksum, numeri di sequenza e timer per garantire consegna corretta e ordinata. |
| **Full-duplex** | Due flussi indipendenti e simultanei: A→B e B→A sullo stesso segmento. |
| **Point-to-point** | Una connessione TCP è sempre tra **un solo mittente** e **un solo destinatario**. Non supporta multicast o broadcast (al contrario di UDP). |
| **Stream-oriented** | TCP vede i dati come uno **stream ordinato di byte**, non come messaggi discreti. L'applicazione ricevente ricostruisce il flusso originale. |

### 7.2 Buffer TCP

TCP usa buffer sia lato mittente che lato ricevente per disaccoppiare i ritmi dell'applicazione dalla velocità della rete:

```
Applicazione A                          Applicazione B
      │                                       ▲
      ▼                                       │
 [Send-Buffer A]                        [Rcv-Buffer B]
      │                                       │
      ▼     segmenti TCP sulla rete           │
      └─────────────────────────────────────►─┘
```

Il buffer lato mittente accumula i dati che l'applicazione ha scritto ma che non sono ancora stati inviati (o non ancora confermati). Il buffer lato ricevente accumula i dati ricevuti ma non ancora letti dall'applicazione.

### 7.3 Maximum Segment Size (MSS)

La dimensione massima del payload di un segmento TCP è determinata dall'**MTU del link layer** (es. 1500 byte per Ethernet), sottraendo gli header:

> **MSS** = MTU - Header IP (20B) - Header TCP (20B) = 1500 - 40 = **1460 byte**

TCP non spedisce un segmento per ogni byte scritto dall'applicazione; accumula dati nel buffer e forma segmenti fino a MSS byte (o li invia prima se lo richiede il timing o l'applicazione).

### 7.4 Il Segmento TCP (Anatomia Completa)

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
┌─────────────────────────────┬───────────────────────────────────┐
│      Source Port (16)       │      Destination Port (16)        │
├─────────────────────────────┴───────────────────────────────────┤
│                      Sequence Number (32)                        │
├─────────────────────────────────────────────────────────────────┤
│                    Acknowledgment Number (32)                    │
├──────┬──────────┬─────────────────────────────┬─────────────────┤
│HdrLen│ Reserved │ Flags (URG,ACK,PSH,RST,SYN,FIN,CWR,ECE) │ Receive Window (16)  │
├──────┴──────────┴─────────────────────────────┴─────────────────┤
│         Checksum (16)        │    Urgent Data Pointer (16)      │
├─────────────────────────────────────────────────────────────────┤
│                      Options (variabile)                         │
├─────────────────────────────────────────────────────────────────┤
│                    Data (≤ MSS byte)                             │
└─────────────────────────────────────────────────────────────────┘
```

**Campi principali:**

| Campo | Dimensione | Descrizione |
|-------|-----------|-------------|
| Source / Dest Port | 16+16 bit | Porte di sorgente e destinazione |
| Sequence Number | 32 bit | Posizione nel byte-stream del primo byte del payload |
| Acknowledgment Number | 32 bit | Prossimo byte atteso dal ricevente (ACK cumulativo) |
| Header Length | 4 bit | Dimensione dell'header in parole da 32 bit (variabile per Options) |
| **ACK** flag | 1 bit | Indica che il campo Ack Number è valido |
| **SYN** flag | 1 bit | Setup connessione (three-way handshake) |
| **FIN** flag | 1 bit | Chiusura connessione (teardown) |
| **RST** flag | 1 bit | Reset: chiusura immediata e anomala della connessione |
| **PSH** flag | 1 bit | Richiede il passaggio immediato dei dati all'applicazione (raro) |
| **URG** flag | 1 bit | I dati urgenti puntati dall'Urgent Pointer devono essere processati subito (raro) |
| **CWR / ECE** flag | 1+1 bit | Explicit Congestion Notification: feedback di congestione dalla rete (opzionale) |
| Receive Window | 16 bit | Numero di byte che il ricevente è disposto ad accettare (flow control) |
| Checksum | 16 bit | Controllo di integrità su header + dati |
| Options | variabile | Es. negoziazione MSS, Window Scale, Timestamp |

### 7.5 Numeri di Sequenza e Acknowledgment

> [!IMPORTANT]
> Il **Sequence Number** TCP non numera i pacchetti, ma **i singoli byte del payload**. È la posizione nel flusso di byte del primo byte portato da quel segmento.

**Esempio** — file di 500.000 byte, MSS = 1000 byte:
- Segmento 1: `Seq = 0` (byte 0–999)
- Segmento 2: `Seq = 1000` (byte 1000–1999)
- Segmento 3: `Seq = 2000` (byte 2000–2999) … e così via per 500 segmenti.

**Acknowledgment Number:** il valore inviato è quello del **prossimo byte atteso**, non dell'ultimo ricevuto. Se il ricevente ha ottenuto correttamente il segmento con `Seq=0` (byte 0–999), manderà `ACK = 1000` ("aspetto il byte numero 1000").

**Piggybacking in full-duplex:** TCP è full-duplex, quindi ogni segmento porta contemporaneamente dati in una direzione **e** un ACK per l'altra direzione. Esempio con Telnet (A invia 'c', B fa eco):

| Step | Da | A | Seq | Ack | Data |
|------|-----|---|-----|-----|------|
| 1 | A→B | | 42 | 79 | 'c' |
| 2 | B→A | | 79 | 43 | 'c' (eco + ACK per il 'c' di A) |
| 3 | A→B | | 43 | 80 | (solo ACK, nessun dato) |

### 7.6 Stima RTT e Timeout

TCP stima continuamente l'RTT per calibrare il timeout di ritrasmissione. Il valore campionato (`SampleRTT`) è volatile (varia col traffico e la congestione), quindi si usa una **media mobile esponenziale ponderata (EWMA)**:

> **EstimatedRTT** = (1 - α) × EstimatedRTT + α × SampleRTT    *(con α = 0.125)*

Si misura anche la variabilità dell'RTT:
> **DevRTT** = (1 - β) × DevRTT + β × |SampleRTT - EstimatedRTT|    *(con β = 0.25)*

Il timeout viene impostato con un margine proporzionale alla variabilità:
> **TimeoutInterval** = EstimatedRTT + 4 × DevRTT

> [!TIP]
> Il valore iniziale del timeout (prima di ricevere qualsiasi SampleRTT) è **1 secondo**. Se scade un timeout, il valore di `TimeoutInterval` viene **raddoppiato** ad ogni ritrasmissione successiva (exponential backoff) per evitare di sovraccaricare una rete già congestionata.

**Nota:** Il SampleRTT viene calcolato solo per segmenti trasmessi **senza ritrasmissioni** (Algoritmo di Karn): i segmenti ritrasmessi sono ambigui (non si sa se l'ACK si riferisce alla prima o alla seconda trasmissione).

### 7.7 Ritrasmissione Rapida (Fast Retransmit)

Aspettare la scadenza del timeout è lento (può richiedere secondi). TCP implementa il **Fast Retransmit** per reagire più prontamente alle perdite:

1. Se il ricevente riceve un segmento con numero di sequenza **maggiore** di quello atteso (gap), invia un **ACK duplicato** con l'Ack Number dell'ultimo byte in ordine ricevuto.
2. Se il mittente riceve **3 ACK duplicati** consecutivi per lo stesso numero, assume che il segmento corrispondente sia andato perso.
3. Il mittente **ritrasmette immediatamente** il segmento senza aspettare il timeout.

> [!NOTE]
> **Perché 3 e non 1?** Un singolo ACK duplicato può essere causato da un semplice riordinamento dei pacchetti nella rete (due segmenti arrivano in ordine invertito). Con 3 duplicati è molto più probabile una vera perdita. TCP usa una soglia abbastanza alta da evitare falsi allarmi, ma abbastanza bassa da non aspettare il timeout.

### 7.8 Connection Management: Three-Way Handshake

Essendo TCP connection-oriented, i due host devono concordare l'apertura della connessione prima di trasmettere dati. Questo genera un problema teorico noto come **Two-Army Problem** (Problema dei Due Eserciti): due entità non possono mai raggiungere un accordo perfetto su un canale inaffidabile (è dimostrabile formalmente). TCP usa il Three-Way Handshake come soluzione pratica "abbastanza buona":

**Apertura connessione:**
```
CLIENT                                    SERVER
  │──── SYN, SEQ=client_isn ──────────────►│
  │     (SYN=1, no payload)                │  Server alloca buffer e variabili
  │                                        │
  │◄─── SYN+ACK, SEQ=server_isn ───────────│
  │     ACK=client_isn+1                   │  
  │     (SYN=1, ACK=1, no payload)         │
  │                                        │
  │──── ACK, SEQ=client_isn+1 ────────────►│
  │     ACK=server_isn+1                   │  Client alloca buffer e variabili
  │     (SYN=0, ACK=1, può avere payload)  │
  │                                        │
  └──────────── ESTABLISHED ───────────────┘
```

**Dettagli dei tre passi:**
1. **SYN**: Client invia segmento con `SYN=1`, `SEQ=client_ISN` (Initial Sequence Number, scelto casualmente). Nessun payload.
2. **SYN-ACK**: Server risponde con `SYN=1, ACK=1`, `SEQ=server_ISN` (anch'esso casuale), `ACK=client_ISN+1`. Alloca buffer e variabili.
3. **ACK**: Client conferma con `SYN=0, ACK=1`, `SEQ=client_ISN+1`, `ACK=server_ISN+1`. Alloca buffer. Può includere i primi dati applicativi.

> [!WARNING]
> **SYN Flood (attacco DoS):** Un attaccante inonda il server di messaggi SYN (step 1) con IP sorgente falsificati, senza mai completare lo step 3. Il server alloca risorse (buffer) per ogni SYN ricevuto, esaurendole rapidamente. La **mitigazione** principale è il **SYN Cookie**: il server non alloca risorse al SYN ma codifica le informazioni di connessione nel `server_ISN`. Le risorse vengono allocate solo quando arriva il terzo messaggio (ACK), che può essere verificato tramite il SYN cookie.

**Chiusura connessione (Four-Way Teardown):**
```
CLIENT                                    SERVER
  │──── FIN, SEQ=u ────────────────────────►│  Client chiude la sua metà (A→B)
  │                                        │
  │◄─── ACK, ACK=u+1 ──────────────────────│  Server conferma
  │                                        │  (Server può ancora inviare dati a Client)
  │◄─── FIN, SEQ=v ────────────────────────│  Server chiude la sua metà (B→A)
  │                                        │
  │──── ACK, ACK=v+1 ──────────────────────►│  Client conferma (entra in TIME_WAIT)
  │                                        │
  └────── Connessione rilasciata ───────────┘
```

**TIME_WAIT:** Dopo l'ultimo ACK, il client aspetta per un tempo pari a **2×MSL** (Maximum Segment Lifetime, tipicamente 1-2 minuti). Serve a garantire che l'ultimo ACK arrivi al server (se si perde, il server ri-invia FIN e il client può rispondere). Previene che vecchi segmenti in ritardo vengano interpretati da una nuova connessione sulle stesse porte.

> [!NOTE]
> Il tempo di connessione TCP (handshake) aggiunge tipicamente un RTT alla latenza iniziale rispetto a UDP. HTTPS/TLS aggiunge ulteriori RTT per la negoziazione crittografica. Questo è il principale motivo per cui HTTP/3 usa **QUIC** (basato su UDP) che integra handshake TLS e connessione in un unico step.

### 7.9 Schemi e Appunti dalle Lavagne (Lezioni 12, 13 e 16)

![Board Lezione 13 - Pagina 1](assets/board_images/board_L13_p1.png)
*Figura 7.1 — Flusso di byte TCP: numerazione progressiva dei segmenti e il campo Sequence Number.*

![Board Lezione 13 - Pagina 2](assets/board_images/board_L13_p2.png)
*Figura 7.2 — ACK cumulativi e avanzamento della finestra scorrevole in TCP.*

![Board Lezione 13 - Pagina 3](assets/board_images/board_L13_p3.png)
*Figura 7.3 — Diagramma temporale del Three-Way Handshake e dei primi scambi dati.*

---

## 8. Controllo di Flusso e Controllo della Congestione
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 8.1 Flow Control vs. Congestion Control

TCP gestisce due problemi distinti di regolazione del traffico che spesso vengono confusi:

> [!IMPORTANT]
> - **Flow Control**: Protegge il **buffer del ricevente** dall'overflow. Il problema è tra i due endpoint della connessione.
> - **Congestion Control**: Protegge la **rete** (i router intermedi) dall'overflow. Il problema è globale e riguarda tutti i flussi che condividono un link.

| | Flow Control | Congestion Control |
|--|---|---|
| **Chi è protetto?** | Il buffer del ricevente (host B) | I buffer dei router nella rete |
| **Chi segnala?** | Il ricevente, tramite campo `rwnd` nel segmento TCP | La rete stessa (timeout, ACK duplicati) o i router (ECN) |
| **Come reagisce il mittente?** | Limita i byte in volo a ≤ `rwnd` | Limita i byte in volo a ≤ `cwnd` |
| **Meccanismo** | Receive Window nel header TCP | Congestion Window (cwnd) gestita da Jacobson |

### 8.2 Flow Control (Controllo di Flusso)

**Il problema:** Il ricevente (B) ha un buffer limitato. Se l'applicazione su B è lenta a leggere i dati (es. è impegnata in operazioni CPU intensive), il buffer può riempirsi. Se il mittente (A) continua a inviare, i nuovi dati che arrivano vengono scartati, causando ritrasmissioni.

**Il meccanismo:** In ogni segmento TCP inviato da B verso A, B include nel campo **Receive Window (`rwnd`)** il numero di byte liberi nel suo buffer di ricezione:

> **rwnd** = RcvBuffer - (LastByteRcvd - LastByteRead)

dove `RcvBuffer` è la dimensione totale del buffer, `LastByteRcvd` è l'ultimo byte ricevuto dalla rete, e `LastByteRead` è l'ultimo byte letto dall'applicazione.

Il mittente A si impegna a mantenere sempre:
> **LastByteSent - LastByteAcked ≤ rwnd**

cioè il numero di byte "in volo" (inviati ma non ancora confermati) non supera mai lo spazio libero nel buffer di B.

**Il problema del rwnd = 0 (stallo):**

Quando B notifica `rwnd = 0`, A smette di inviare. Ma se B poi libera del buffer e non invia nessun segmento ad A (perché non ha dati da mandare), A non saprà mai che può riprendere. Il protocollo gestisce questo caso con i **probe segment**: A invia periodicamente segmenti da 1 byte di payload che forzano B a rispondere con un ACK aggiornato contenente il nuovo valore di `rwnd`.

### 8.3 Congestion Control (Controllo della Congestione)

**Il problema della congestione:** Se i dati vengono inviati a un ritmo superiore alla capacità di un link (il "collo di bottiglia"), i buffer dei router si riempiono. I pacchetti vengono scartati (drop), causando timeout e ritrasmissioni, che a loro volta aggiungono traffico, peggiorando la congestione — un effetto a spirale.

**Analogia dell'imbuto:** Un router con un link da R bps in uscita e N connessioni che arrivano ciascuna a λ bps. Se N×λ > R, i pacchetti si accumulano. Con buffer infinito il delay cresce all'infinito; con buffer finito i pacchetti vengono persi.

**Due approcci al congestion control:**
1. **End-to-end (TCP standard):** Nessun supporto dalla rete. Il mittente inferisce la congestione dai **loss events** (timeout o 3 ACK duplicati) e riduce il tasso.
2. **Network-assisted (ECN — Explicit Congestion Notification):** I router usano i bit **ECE** e **CWR** nell'header TCP per segnalare esplicitamente la congestione prima che avvengano perdite.

### 8.4 L'Algoritmo di Jacobson (TCP Reno)

TCP regola il proprio tasso di invio tramite la **Congestion Window (`cwnd`)**. Il vincolo complessivo del mittente diventa:

> **LastByteSent - LastByteAcked ≤ min(cwnd, rwnd)**

Il rate approssimativo di invio è **≈ cwnd / RTT** byte/sec. L'algoritmo di Jacobson controlla `cwnd` attraverso tre fasi:

#### Fase 1: Slow Start

**Obiettivo:** trovare rapidamente la banda disponibile partendo da zero.

- Inizio: `cwnd = 1 MSS`
- Ad ogni ACK ricevuto: `cwnd += 1 MSS` → la finestra **raddoppia ogni RTT** (crescita esponenziale)
- Si continua finché `cwnd` non supera la soglia `ssthresh` (Slow Start Threshold)

**Loss event in Slow Start:**
- **Timeout:** `ssthresh = cwnd / 2`, `cwnd = 1 MSS` → ripartenza dall'inizio
- **3 ACK duplicati:** `ssthresh = cwnd / 2`, `cwnd = ssthresh + 3 MSS` → entra in Fast Recovery

#### Fase 2: Congestion Avoidance (Additive Increase)

**Obiettivo:** aumentare la finestra con cautela per non causare congestione.

- Attivata quando `cwnd ≥ ssthresh`
- Ad ogni RTT: `cwnd += 1 MSS` (crescita **lineare**)
- In pratica per ogni ACK ricevuto: `cwnd += MSS × (MSS / cwnd)` (incremento proporzionale)

**Loss event in Congestion Avoidance:**
- **Timeout:** `ssthresh = cwnd / 2`, `cwnd = 1 MSS` → torna a Slow Start
- **3 ACK duplicati:** `ssthresh = cwnd / 2`, `cwnd = ssthresh + 3 MSS` → entra in Fast Recovery

#### Fase 3: Fast Recovery (solo TCP Reno, non TCP Tahoe)

**Obiettivo:** Recuperare rapidamente dopo una perdita rilevata tramite 3 ACK duplicati (senza tornare a Slow Start).

- `cwnd = ssthresh + 3 MSS` (il +3 per tenere conto dei 3 pacchetti che hanno generato i dup-ACK e che sono già nel buffer del ricevente)
- Per ogni ulteriore ACK duplicato ricevuto: `cwnd += 1 MSS`
- Quando arriva l'ACK del segmento ritrasmesso: `cwnd = ssthresh`, si entra in Congestion Avoidance

#### Il comportamento a "dente di sega" (Sawtooth)

```
cwnd (MSS)
   │
 32│           /|         /|
   │          / |        / |
 16│    ssth /  |  ssth /  |
   │       /|  |      /|  |
  8│      / |  |     / |  |
   │     /  |  |    /  |  |
  4│    /   |  |   /   |  |
   │   /    |  |  /    |  |
  2│  /     |  | /     |  |
   │ /      |  |/      |  |
  1│/       |  |       |  |
   └────────────────────────────► RTT
         SS→CA  loss  SS→CA loss
```

La `cwnd` cresce (lentamente o velocemente) finché un loss event la dimezza, poi ricomincia. Questo schema "a dente di sega" è il comportamento caratteristico di TCP visibile in Wireshark analizzando un trasferimento file di lunga durata.

**TCP Tahoe vs. TCP Reno:**

| | TCP Tahoe | TCP Reno |
|--|-----------|----------|
| **Loss con timeout** | Slow Start da 1 MSS | Slow Start da 1 MSS |
| **Loss con 3 dup-ACK** | Slow Start da 1 MSS | Fast Recovery (non torna a 1 MSS) |
| **Introdotto** | 1988 | 1990 |
| **Performance** | Peggiore | Migliore (Fast Recovery evita full restart) |

> [!TIP]
> Le implementazioni moderne (Linux, Windows) usano varianti ancora più avanzate di TCP come **TCP CUBIC** (Linux default) o **TCP BBR** (Google), che stimano direttamente la banda disponibile invece di inferirla solo dalle perdite, ottenendo performance migliori su link ad alta velocità e alto RTT.

### 8.5 ECN — Explicit Congestion Notification

L'**ECN** è un meccanismo opzionale che permette ai router di segnalare la congestione *prima* che i buffer si riempiano (evitando drop):

1. Il router in stato di congestione imposta i bit **ECN** nell'header IP del datagramma in transito.
2. Il ricevente segnala la congestione al mittente impostando il flag **ECE** nel prossimo ACK.
3. Il mittente riduce `cwnd` come se avesse ricevuto 3 ACK duplicati, e imposta il flag **CWR** per confermare al ricevente di aver ridotto il rate.

ECN migliora le performance perché riduce il rate *prima* della perdita, evitando la latenza aggiuntiva causata da timeout e ritrasmissioni.

### 8.6 Schemi e Appunti dalle Lavagne (Lezioni 14 e 15)

![Board Lezione 14 - Pagina 1](assets/board_images/board_L14_p1.png)
*Figura 8.1 — I router usano store-and-forward: i buffer si riempiono e producono packet loss in congestione.*

![Board Lezione 15 - Pagina 1](assets/board_images/board_L15_p1.png)
*Figura 8.2 — Algoritmo di Jacobson: evoluzione di cwnd e ssthresh con loss event da timeout e 3 dup-ACK.*

---

## 9. Il Livello di Rete — IP e Router
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 9.1 Funzioni del Livello di Rete

Il livello di rete si occupa della **host-to-host delivery**: riceve i segmenti dal livello di trasporto dell'host mittente, li incapsula in **datagrammi IP**, e li consegna all'host destinatario attraverso una catena di router intermedi. A ogni nodo intermedio (router), il datagramma viene decapsulato, esaminato e inoltrato verso il nodo successivo del percorso — questa operazione è detta **hop**.

> [!NOTE]
> Mentre il livello di trasporto opera solo negli host terminali (edge), il livello di rete opera in **tutti i nodi della rete**: host, router e switch di livello 3. Il software di routing gira nei router intermedi; gli host terminali ne hanno solo la porzione necessaria per formare e inviare i datagrammi.

I principali protocolli a questo livello sono: **IP** (Internet Protocol), **DHCP** (Dynamic Host Configuration Protocol), **NAT** (Network Address Translation) e **ICMP** (Internet Control Message Protocol, usato ad es. da `ping` e `traceroute`).

### 9.2 Best-Effort: il Contratto di Internet

Potenzialmente, Internet potrebbe offrire svariati servizi agli utenti, tra cui:
- **Consegna garantita** del pacchetto.
- **Consegna con ritardo massimo garantito** (es. entro 100 ms).
- **Consegna in ordine** dei pacchetti.
- **Banda minima garantita** (Quality of Service, QoS).
- **Sicurezza** (cifratura e autenticazione a livello rete).

In realtà, Internet offre **un solo servizio**: il **Best-Effort** (*fare del proprio meglio*).
- I pacchetti possono arrivare fuori ordine, in ritardo, duplicati, o non arrivare affatto.
- Non c'è alcuna garanzia su ritardo, banda o ordine.
- Questo modello semplice — con una larghezza di banda sufficiente — si è dimostrato straordinariamente efficace nella pratica. Applicazioni come Netflix, VoIP, videoconferenze, e streaming funzionano bene anche su un canale best-effort.

### 9.3 Router: Forwarding vs Routing

Il router svolge due funzioni concettualmente distinte, che operano a velocità completamente diverse:

| | **Forwarding (Piano dei Dati)** | **Routing (Piano di Controllo)** |
|---|---|---|
| **Ambito** | Locale (al singolo router) | Globale (intera rete) |
| **Operazione** | Trasferisce ogni pacchetto dall'input port all'output port corretto tramite una *forwarding table* | Costruisce e aggiorna la forwarding table decidendo i percorsi end-to-end |
| **Velocità** | Molto veloce — nanoseccondi (hardware dedicato, ASIC) | Lenta — secondi (software del routing processor) |
| **Analogia** | L'autista che gira a destra o sinistra all'incrocio | Il navigatore GPS che ha calcolato il percorso ottimale |

**Come vengono create le forwarding table?**
- **Approccio Distribuito**: ogni router esegue algoritmi di routing (es. OSPF, BGP) e scambia informazioni coi vicini. È l'approccio tradizionale e più diffuso.
- **Approccio Centralizzato (SDN)**: un controller software remoto calcola e distribuisce centralmente le forwarding table a tutti i router. È la base del **Software-Defined Networking (SDN)**, dove la logica di rete è separata dall'hardware.

### 9.4 Tipi di Router e Architettura Interna

**Tipi di router per contesto d'uso:**

| Tipo | Descrizione | Esempio Commerciale |
|------|-------------|---------------------|
| **Home router** | Uso domestico, spesso include NAT, DHCP, WiFi | TP-Link AX6600 |
| **Business router** | Uso aziendale, gestione di più sottoreti e connettività ridondante | Cisco RV016 |
| **Edge router** | Connette la rete di un'organizzazione all'ISP | Juniper MX2020 |
| **Core / Backbone router** | Cuore di Internet, gestisce traffico di enormi proporzioni | Cisco CRS-1 |

**Architettura interna di un router:**

```
Input Links ──► [Input Port 1...N] ──► [Switch Fabric] ──► [Output Port 1...N] ──► Output Links
                      │                                            │
                [Forwarding Table]               [Routing Processor]
```

I quattro componenti chiave sono:
- **Input Ports**: Ogni porta fisica esegue il lookup nella forwarding table per determinare l'output port di destinazione. *Ogni porta ha una copia locale della forwarding table* per non creare colli di bottiglia sul bus centrale.
- **Switch Fabric**: Connette fisicamente le input ports alle output ports. Esistono 3 tecnologie di switching:
  1. **Via memoria**: Il pacchetto viene scritto in memoria e il routing processor ne determina la copia nell'output port (metodo lento, usato nei router di prima generazione).
  2. **Via bus condiviso**: Il pacchetto attraversa un bus comune verso l'output port (un pacchetto alla volta, adatto a reti locali).
  3. **Via rete a crossbar** (crossbar switch): I punti di incrocio tra input e output possono essere aperti/chiusi, permettendo la trasmissione **parallela** di più pacchetti contemporaneamente (metodo moderno e più performante).
- **Output Ports**: Accodano e trasmettono i pacchetti sul link fisico di uscita.
- **Routing Processor**: Esegue gli algoritmi di routing, gestisce e aggiorna la forwarding table.

**Accodamento e perdita di pacchetti:**
Poiché lo switching richiede tempo, input e output ports hanno buffer (code) per pacchetti in attesa. Quando la velocità dei pacchetti in arrivo supera la capacità di switching o di trasmissione, i buffer possono saturarsi e i nuovi pacchetti vengono **scartati** (drop-tail, in modalità FIFO). Questo è lo scenario descritto nella board L14: i router operano in store-and-forward.

**Politiche di Packet Scheduling per i pacchetti in coda:**

| Politica | Descrizione |
|----------|-------------|
| **FIFO** | Serviti nell'ordine di arrivo. Semplice ma non differenzia il traffico. |
| **Priority Queuing** | Le classi di traffico ad alta priorità (es. VoIP) vengono servite prima. Dentro ogni classe vale il FIFO. |
| **Round-Robin (WFQ)** | I pacchetti sono divisi in classi, servite a turno secondo un peso. Garantisce equità tra i flussi. |

### 9.5 Longest Prefix Matching (LPM)

Un router non associa un singolo IP di destinazione a un'interfaccia, ma associa **prefissi** di indirizzi IP (blocchi di subnet) a interfacce. Quando un pacchetto arriva, il router cerca il prefisso che corrisponde ai bit più significativi dell'IP di destinazione.

**La regola aurea:** Se un indirizzo IP corrisponde a più voci nella forwarding table (perché i blocchi IP possono sovrapporsi in CIDR), vince sempre la voce col **prefisso più lungo** (il più specifico).

| Prefisso IP (binary) | Interfaccia |
|----------------------|-------------|
| `11001000 00010111 00010*** ********` | 0 |
| `11001000 00010111 00011000 ********` | 1 |
| `11001000 00010111 00011*** ********` | 2 |
| `otherwise` | 3 |

**Esempio pratico:** L'IP `11001000 00010111 00011000 10101010` corrisponde sia all'interfaccia 1 (i primi 24 bit fanno match) che all'interfaccia 2 (i primi 21 bit fanno match). Vince l'interfaccia 1, perché il suo match è più lungo (24 > 21 bit).

> [!TIP]
> Il lookup LPM è un'operazione critica che deve avvenire a velocità elevatissima (nanoseccondi per connessioni Gigabit). Si usano strutture dati specializzate come i **Trie** (alberi di prefissi) implementate in hardware dedicato (es. memorie TCAM).

La stessa logica di **match-plus-action** viene applicata anche da Firewall (dove l'azione è filtrare il pacchetto) e da NAT (dove l'azione è riscrivere l'indirizzo).

### 9.6 Schemi e Appunti dalle Lavagne (Lezioni 14 e 15)

![Board Lezione 14 - Pagina 1](assets/board_images/board_L14_p1.png)
*Figura 9.1 — Architettura interna del router: store-and-forward e buffer di memoria.*

![Board Lezione 15 - Pagina 1](assets/board_images/board_L15_p1.png)
*Figura 9.2 — Regola del Longest Matching Prefix calcolata bit a bit in binario.*

![Board Lezione 15 - Pagina 2](assets/board_images/board_L15_p2.png)
*Figura 9.3 — Longest Prefix Rule: risoluzione delle ambiguità tra blocchi sovrapposti con CIDR.*

---

## 10. Indirizzamento IP, DHCP, NAT e IPv6
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 10.1 L'Indirizzo IP (IPv4)

Un **indirizzo IPv4** è un numero di **32 bit** (4 byte) usato per identificare in modo univoco ogni interfaccia di rete su Internet. Si rappresenta in *notazione decimale puntata* (*dotted-decimal notation*), dove ogni byte è scritto in decimale separato da un punto:

```
193.32.216.9 = 11000001 00100000 11011000 00001001
```

Con 32 bit, lo spazio di indirizzamento è di circa **2^32 ≈** **4 miliardi** di indirizzi.

> [!IMPORTANT]
> L'indirizzo IP è **associato all'interfaccia di rete**, non all'host o al router in sé. Un laptop con una scheda di rete WiFi e una Ethernet ha **due interfacce** e potenzialmente due indirizzi IP diversi. Un router, avendo molte porte fisiche, ha molte interfacce e quindi molti IP.

### 10.2 Subnetting e Subnet Mask

Assegnare indirizzi IP in modo casuale sarebbe un disastro: le forwarding table dei router sarebbero enormi, non si saprebbe dove "cercare" gli host, e lo spazio di indirizzamento verrebbe sprecato. La soluzione è l'**indirizzamento gerarchico**: Internet è organizzata in sottoreti (subnet) annidate, proprio come la numerazione telefonica internazionale (+39 per l'Italia, poi il prefisso della città, poi il numero locale).

Un indirizzo IP è diviso in due parti:
- **Parte di rete (Net ID / Prefisso)**: i bit più a sinistra, identifica la subnet.
- **Parte host (Host ID)**: i bit più a destra, identifica la singola interfaccia nella subnet.

La **subnet mask** è una sequenza di bit che specifica dove finisce la parte di rete e dove inizia quella host. È sempre composta da una sequenza contigua di `1` seguita da `0`:

```
IP:          193.32.216.9  = 11000001 00100000 11011000 00001001
Subnet Mask: 255.255.255.0 = 11111111 11111111 11111111 00000000
Notazione CIDR: 193.32.216.0/24  (il /24 indica 24 bit di prefisso)
```

> [!CAUTION]
> Una subnet mask deve avere i bit `1` **obbligatoriamente contigui e tutti a sinistra**. Una maschera come `255.255.10.0` (`11111111 11111111 00001010 00000000`) **non è una subnet mask valida** perché ha bit `1` non contigui!

**Esempi di validità:**

| Dotted-Decimal | Binario | Valida? |
|----------------|---------|---------|
| `255.255.255.0` | `11111111 11111111 11111111 00000000` | ✅ `/24` |
| `255.255.128.0` | `11111111 11111111 10000000 00000000` | ✅ `/17` |
| `255.224.0.0` | `11111111 11100000 00000000 00000000` | ✅ `/11` |
| `255.255.10.0` | `11111111 11111111 00001010 00000000` | ❌ Non valida |
| `63.255.255.0` | `00111111 11111111 11111111 00000000` | ❌ Non valida |

**Come stabilire se due host sono nella stessa subnet?** Basta confrontare i loro prefissi (i bit coperti dalla subnet mask). Se i bit del prefisso sono identici, appartengono alla stessa subnet.

| IP 1 | Subnet Mask | IP 2 | Risultato |
|------|-------------|------|-----------|
| `231.23.11.117` | `/24` | `231.23.11.9` | ✅ Stessa subnet (i 24 bit di sinistra coincidono) |
| `10.54.32.1` | `/17` | `10.54.60.203` | ✅ Stessa subnet |
| `110.32.100.10` | `/11` | `110.64.100.11` | ❌ Subnet diverse |

> [!NOTE]
> Host in subnet diverse possono comunque comunicare, passando attraverso un router (che funge da **gateway**). L'amministratore di rete può però decidere di filtrare o bloccare questo traffico inter-subnet (tramite firewall).

### 10.3 Il Datagramma IPv4 (Struttura dell'Header)

Il datagramma IP è il "pacchetto" del livello di rete. Il suo header contiene campi cruciali:

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
├─────────────────────────────────────────────────────────────────┤
│ Ver(4) │ IHL(4) │  TOS (8)   │        Datagram Length (16)      │
├─────────────────────────────────────────────────────────────────┤
│       Identifier (16)        │ Flags(3) │  Frag Offset (13)     │
├─────────────────────────────────────────────────────────────────┤
│    TTL (8)    │  Protocol(8) │         Header Checksum (16)     │
├─────────────────────────────────────────────────────────────────┤
│                    Source IP Address (32)                        │
├─────────────────────────────────────────────────────────────────┤
│                  Destination IP Address (32)                     │
├─────────────────────────────────────────────────────────────────┤
│                   Options (variabile)                            │
├─────────────────────────────────────────────────────────────────┤
│                     Data (Payload)                               │
└─────────────────────────────────────────────────────────────────┘
```

**Campi notevoli:**
- **TTL (Time To Live)**: Ogni router che processa il datagramma decrementa il TTL di 1. Quando raggiunge 0, il datagramma viene scartato e viene inviato un messaggio ICMP al mittente. Previene loop infiniti nella rete.
- **Protocol**: Indica il protocollo del livello superiore (6 = TCP, 17 = UDP). Elenco completo su IANA.
- **Header Checksum**: Solo sull'header (a differenza del checksum TCP/UDP che copre anche i dati). Deve essere ricalcolato ad ogni hop perché il TTL cambia!
- **Identification, Flags, Fragment Offset**: Usati per la **frammentazione**: se un datagramma è troppo grande per il link successivo (superando l'MTU), il router lo spezza in frammenti. La riassemblatura avviene solo a destinazione (non nei router intermedi, per non appesantirne il carico).

### 10.4 Classful vs Classless Addressing (CIDR)

**Classful Addressing (obsoleto):** Le reti erano divise in classi rigide:
- Classe A (`/8`): es. `10.0.0.0/8` → oltre 16 milioni di host.
- Classe B (`/16`): es. `172.16.0.0/16` → 65.535 host.
- Classe C (`/24`): es. `192.168.1.0/24` → 254 host.

Il problema era lo spreco enorme. Un'organizzazione con 300 host riceveva una Classe B con 65.535 IP, sprecando 65.235 indirizzi!

**Classless Inter-Domain Routing (CIDR — pronuncia "cider"):** L'approccio moderno assegna blocchi di dimensione arbitraria nella forma `a.b.c.d/X`, dove X è scelto in base alle reali esigenze. Con 300 host si assegna un `/23` (512 IP), sprecandone solo 212. I blocchi CIDR supportano anche l'**address aggregation**: un ISP che gestisce un blocco `/20` può pubblicizzare ai router Internet una sola voce nella forwarding table, semplificando enormemente il routing globale.

### 10.5 DHCP — Dynamic Host Configuration Protocol

**DHCP** automatizza il processo di assegnazione degli indirizzi IP agli host che si connettono alla rete. È un protocollo **applicativo** (usa UDP, porta 67 server / porta 68 client) ma svolge un ruolo infrastrutturale cruciale. È **plug-and-play**: un nuovo host si collega e la rete si occupa di tutto.

Oltre all'IP, DHCP fornisce all'host:
- La **subnet mask**.
- L'indirizzo del **default gateway** (il router per uscire dalla subnet locale).
- L'indirizzo del **server DNS locale**.
- Un **lease time** (tempo di validità dell'assegnazione, dopo il quale l'IP può essere riassegnato).

**Il processo DHCP in 4 passi (DORA):**

```
Nuovo Host                               Server DHCP
    │                                          │
    │─── DHCP Discover ────────────────────────►│  Broadcast (src: 0.0.0.0, dst: 255.255.255.255)
    │    "Esiste un server DHCP? Ho bisogno     │  → "Chi sono? Ho bisogno di un IP!"
    │     di un indirizzo!"                     │
    │                                          │
    │◄── DHCP Offer ────────────────────────────│  Broadcast (offerta: IP=223.1.2.4,
    │    "Ti offro l'IP 223.1.2.4, per 86400s" │  mask, GW, DNS, lease)
    │                                          │
    │─── DHCP Request ─────────────────────────►│  "Accetto la tua offerta"
    │    (ancora broadcast, può esserci più      │  (ancora broadcast: possono esserci
    │     di un server DHCP)                    │   più server DHCP attivi)
    │                                          │
    │◄── DHCP ACK ──────────────────────────────│  "Confermato! L'IP è tuo."
    │                                          │
    └────────── Connesso! ──────────────────────┘
```

> [!TIP]
> **Relay DHCP**: Se il server DHCP si trova in una subnet diversa dall'host richiedente, i broadcast non arrivano a destinazione (i router non propagano i broadcast). Si configura il router di confine come **DHCP Relay Agent**: intercetta il Discover, lo incapsula in un datagramma unicast e lo inoltrata al server DHCP corretto, e viceversa.

**Comandi Linux per vedere la configurazione DHCP ricevuta:**
```bash
ip addr    # Vedi IP e maschera di subnet
ip route   # Vedi il gateway predefinito (default gateway)
```

### 10.6 NAT — Network Address Translation

**Il problema:** Con ~4 miliardi di indirizzi IPv4 e miliardi di dispositivi connessi, gli indirizzi pubblici scarseggiano. Esporre ogni dispositivo domestico (stampante, smart TV, termostato...) con un IP pubblico univoco è impraticabile e anche indesiderabile per la sicurezza.

**La soluzione:** Il **NAT** (o IP Masquerading) permette a un'intera rete locale privata di condividere un **singolo IP pubblico** per comunicare con Internet. Il router NAT funge da intermediario trasparente.

**Indirizzi privati riservati (non instradabili su Internet pubblico):**
- `10.0.0.0/8` (oltre 16 milioni di indirizzi privati)
- `172.16.0.0/12`
- `192.168.0.0/16` (il più comune nelle reti domestiche)
- `127.0.0.0/8` (loopback, indica "questa macchina stessa", tipicamente `127.0.0.1`)
- `0.0.0.0` (indica la rete corrente o "qualunque indirizzo")
- `255.255.255.255` (broadcast a tutta la subnet)

**Come funziona il NAT:**

```
LAN (privata)                                  WAN (Internet)
192.168.1.5:4321 ──►  Router NAT ──►  203.1.2.3:5001 ──► Server remoto
                      │ NAT Table │
                      │ 192.168.1.5:4321 ↔ 203.1.2.3:5001 │
Server remoto ──►  203.1.2.3:5001 ──►  Router NAT ──►  192.168.1.5:4321
```

1. Il pacchetto dell'host interno (`192.168.1.5:4321`) arriva al router NAT.
2. Il router **sostituisce** IP sorgente + porta con il suo IP pubblico + una porta casuale nuova (es. `203.1.2.3:5001`).
3. La mappatura `192.168.1.5:4321 ↔ 203.1.2.3:5001` viene registrata nella **NAT Translation Table**.
4. Quando il server risponde a `203.1.2.3:5001`, il router consulta la tabella e smista la risposta all'host interno corretto.

> [!WARNING]
> Siccome la porta è a 16 bit, un router NAT può teoricamente gestire oltre **60.000 connessioni simultanee** con un singolo IP pubblico. La tecnica si chiama **PAT (Port Address Translation)** o **NAPT**.
>
> Il NAT è controverso: viola il principio end-to-end di Internet (i server esterni non possono avviare connessioni verso host interni, cosa necessaria per es. i giochi online o VoIP P2P). La soluzione definitiva a lungo termine è IPv6.

### 10.7 IPv6

**Motivazione storica:** Nel 1990 ci si rese conto che lo spazio IPv4 (4 miliardi) si sarebbe esaurito. L'IETF (Internet Engineering Task Force) ha sviluppato **IPv6**, portando gli indirizzi a **128 bit** (**2^128 ≈ 3.4 × 10^38** indirizzi — abbastanza per assegnare un IP ad ogni granello di sabbia sul pianeta Terra).

**Oltre agli indirizzi, IPv6 ha migliorato strutturalmente IPv4:**

| Caratteristica | IPv4 | IPv6 |
|---------------|------|------|
| Lunghezza indirizzo | 32 bit | **128 bit** |
| Notazione | `192.168.1.1` (decimale puntato) | `2001:db8:85a3::8a2e:370:7334` (esadecimale con gruppi da 16 bit) |
| Header | Variabile (min 20 byte, con Options) | **Fisso a 40 byte** (le opzioni sono nei "next header") |
| Checksum header | Presente | **Rimosso** (ridondante: già calcolato dai link layer) |
| Frammentazione | Nei router | **Solo negli host** (i router scartano il datagramma e mandano "Packet Too Big") |
| NAT | Necessario | **Non necessario** (abbastanza indirizzi per tutti) |
| Flow Labeling | Non presente | Presente (per identificare flussi di traffico, es. streaming) |

**Formato indirizzo IPv6:**
```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
# Regole di abbreviazione:
# 1. Si possono omettere gli zeri iniziali di ogni gruppo: 0db8 → db8
# 2. Una singola sequenza di gruppi tutti zero si abbrevia con "::" (usabile una sola volta)
2001:db8:85a3::8a2e:370:7334
```

**Transizione IPv4 → IPv6 (Tunneling):**
Il passaggio non può avvenire con un "Flag Day" globale (troppi dispositivi). La strategia adottata è il **tunneling**: i datagrammi IPv6 vengono **incapsulati dentro datagrammi IPv4** per attraversare le porzioni della rete ancora in IPv4, e vengono poi decapsulati all'uscita del "tunnel" da un router IPv6-capable.

### 10.8 Schemi e Appunti dalle Lavagne (Lezione 17)

![Board Lezione 17 - Pagina 1](assets/board_images/board_L17_p1.png)
*Figura 10.1 — Calcolo in binario delle maschere di sottorete e separazione NetID / HostID.*

![Board Lezione 17 - Pagina 2](assets/board_images/board_L17_p2.png)
*Figura 10.2 — Individuazione dell'indirizzo di rete (tutti 0) e dell'indirizzo di broadcast (tutti 1).*

![Board Lezione 17 - Pagina 3](assets/board_images/board_L17_p3.png)
*Figura 10.3 — Esercizio svolto di subnetting: partizionamento dell'indirizzo 193.32.216.0/24.*

![Board Lezione 17 - Pagina 4](assets/board_images/board_L17_p4.png)
*Figura 10.4 — Tabella di riepilogo con range di host assegnabili per ciascuna sottorete.*

---

## 11. Il Piano di Controllo — Algoritmi di Routing
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 11.1 Introduzione al Routing

I router usano **algoritmi di routing** per determinare i percorsi ottimali (costo minimo) dai mittenti ai destinatari.

**I router non conoscono la rete all'avvio:** devono scoprire la topologia attraverso messaggi con i vicini.

### 11.2 Flooding

Ogni router inoltra tutti i pacchetti in ingresso a tutti i link (tranne quello di origine).

**Pro:** esplora tutti i percorsi, estremamente robusto.
**Contro:** traffico enorme, impraticabile per reti grandi.

### 11.3 Formulazione del Problema di Routing

Rete modellata come **grafo G=(N,E)**:
- **N**: nodi (router)
- **E**: archi (link) con costo `c(x,y)`
- Se `(x,y)∉E`: `c(x,y)=∞`
- Grafo non orientato: `c(x,y)=c(y,x)`

**Obiettivo:** trovare il percorso di costo minimo.

### 11.4 Algoritmo Distance Vector (DV)

**Approccio distribuito e asincrono.** Ogni router conosce solo la distanza dai vicini.

**Equazione di Bellman-Ford:**
```
D(x, y) = min_v { c(x,v) + D(v, y) }
```

**Funzionamento:**
1. Ogni nodo `x` mantiene `D(x, y)` per ogni destinazione `y`
2. Periodicamente invia il proprio vettore di distanze ai vicini
3. Aggiorna le stime quando riceve un vettore da un vicino:
   `D(x,y) = min_v{ c(x,v) + D_v(y) }`
4. Si ripete fino alla convergenza

**Problema Count-to-Infinity:** in caso di guasto, convergenza molto lenta o cicli.

**Soluzione parziale — Poisoned Reverse:** se Z raggiunge X attraverso Y, Z comunica a Y che `D(Z,X)=∞` (evita cicli a 2 nodi).

### 11.5 Algoritmo Link-State (LS) — Dijkstra

**Approccio centralizzato.** Sfrutta la conoscenza completa della rete.

**Come si ottiene la conoscenza completa (4 passi):**
1. **Scoperta vicini**: manda "hello" su tutti i link
2. **Setup costi**: imposta le distanze ai vicini
3. **Costruzione pacchetto**: ID vicini + costi
4. **Scambio broadcast**: invia il pacchetto a tutti gli altri router

**Algoritmo di Dijkstra (pseudocodice):**

```
LinkState(x):
    N' = {x}
    for all nodes v:
        D(v) = c(x,v) se vicino, else ∞
    repeat:
        w = nodo non in N' con D(w) minimo
        add w to N'
        for each neighbor v of w not in N':
            D(v) = min(D(v), D(w)+c(w,v))
    until N' = N
```

**Complessità:** O(n²) base, O(n log n) con heap.

### 11.6 Confronto DV vs. LS

| Caratteristica | Distance Vector (DV) | Link-State (LS) |
|----------------|---------------------|-----------------|
| **Conoscenza** | Solo dai vicini (locale) | Intera rete (globale) |
| **Complessità messaggi** | Bassa | Alta (broadcast) |
| **Convergenza** | Lenta, count-to-infinity | Veloce |
| **Robustezza** | Bassa (errori si propagano) | Alta (calcoli indipendenti) |

> **In Internet si usano entrambi:** OSPF usa LS, BGP usa DV.

### 11.7 Schemi e Appunti dalle Lavagne (Lezioni 18, 19, 20 e 21)

![Board Lezione 18 - Pagina 1](assets/board_images/board_L18_p1.png)
*Figura 11.1 — Rappresentazione formale della rete come grafo $G = (N, E)$ con pesi sui link.*

![Board Lezione 18 - Pagina 2](assets/board_images/board_L18_p2.png)
*Figura 11.2 — Proprietà di ottimalità dei percorsi e instradamento a costo minimo.*

![Board Lezione 19 - Pagina 1](assets/board_images/board_L19_p1.png)
*Figura 11.3 — Analisi dei pacchetti ICMP Echo Request ed Echo Reply.*

![Board Lezione 19 - Pagina 2](assets/board_images/board_L19_p2.png)
*Figura 11.4 — Meccanismo di Traceroute basato sul decremento del TTL e messaggi Time Exceeded.*

![Board Lezione 19 - Pagina 3](assets/board_images/board_L19_p3.png)
*Figura 11.5 — Esame dei campi del datagramma IP e del payload UDP nelle sonde di rete.*

![Board Lezione 19 - Pagina 4](assets/board_images/board_L19_p4.png)
*Figura 11.6 — Sequenza di risposte dai router intermedi lungo il cammino.*

![Board Lezione 20 - Pagina 1](assets/board_images/board_L20_p1.png)
*Figura 11.7 — Algoritmo Distance Vector: formulazione di Bellman-Ford e inizializzazione.*

![Board Lezione 20 - Pagina 2](assets/board_images/board_L20_p2.png)
*Figura 11.8 — Procedura di notifica periodica delle distanze ai soli vicini diretti.*

![Board Lezione 20 - Pagina 3](assets/board_images/board_L20_p3.png)
*Figura 11.9 — Aggiornamento delle tabelle di inoltro e convergenza del grafo.*

![Board Lezione 20 - Pagina 4](assets/board_images/board_L20_p4.png)
*Figura 11.10 — Analisi del fenomeno del Count-to-Infinity in presenza di guasti ai link.*

![Board Lezione 21 - Pagina 1](assets/board_images/board_L21_p1.png)
*Figura 11.11 — Algoritmo Link-State: broadcast dei pacchetti LSP e conoscenza globale della topologia.*

![Board Lezione 21 - Pagina 2](assets/board_images/board_L21_p2.png)
*Figura 11.12 — Calcolo dell'albero di copertura dei cammini minimi da nodo radice.*

---

## 12. Il Livello di Collegamento (Link Layer) e il Livello Fisico
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 12.1 Funzioni del Link Layer

- Trasmissione di pacchetti su link (da nodo a nodo della rete)
- **Physical layer**: struttura dei link (mezzo, connettori, cavi) e rappresentazione dei bit

### 12.2 Framming e Rilevamento Errori

**Frame = incapsulamento del datagramma IP:**
```
┌──────────┬──────────┬────────────────────┬──────────┐
│ Header   │ Header   │      Payload        │  Trailer │
│ Ethernet │    IP    │   (TCP/UDP + dati)  │  (CRC)   │
└──────────┴──────────┴────────────────────┴──────────┘
```

**Parità semplice:** bit aggiunto per rendere il numero di '1' pari/dispari. Rileva errori su singoli bit.

**CRC (Cyclic Redundancy Check):** tecnica principale per rilevamento errori.
- Polinomio generatore `G` di r+1 bit (noto a mittente e destinatario)
- Mittente calcola r bit di CRC: `D,R` divisibile per `G`
- Destinatario divide per `G`: resto ≠ 0 → errore
- Rileva tutti i burst error di ≤ r bit

### 12.3 Protocolli MAC

In un mezzo condiviso (broadcast), più nodi trasmettono → **collisioni**.

**3 categorie MAC:**

#### 12.3.1 Channel Partitioning

- **TDMA**: slot temporali fissi per nodo
- **FDMA**: frequenza fissa per nodo
- **CDMA**: codice univoco per nodo
- Pro: nessuna collisione. Contro: spreco se slot/frequenze non usati.

#### 12.3.2 Random Access

**CSMA (Carrier Sense Multiple Access):** controlla se il canale è libero prima di trasmettere.

**CSMA/CD** (con Collision Detection — Ethernet):
1. Controlla se il canale è libero
2. Se libero, trasmette
3. Mentre trasmette, verifica collisioni
4. Se collisione: **stop**, aspetta K ∈ {0,...,2ⁿ-1} periodi (**binary exponential backoff**)

#### 12.3.3 Taking Turns

- **Polling**: master seleziona nodi a turno (es. Bluetooth)
  - Pro: nessuna collisione. Contro: overhead, singolo punto di guasto.
- **Token-passing**: token circolante; chi ha il token trasmette
  - Pro: nessuna collisione, decentralizzato. Contro: problemi se token non rilasciato.

### 12.4 Indirizzi MAC

- **6 byte** (2⁴⁸ possibili indirizzi)
- Notazione esadecimale: `1A:23:F9:CD:06:9B`
- **Broadcast MAC**: `FF:FF:FF:FF:FF:FF`
- Locale alla LAN (link-layer), mentre IP è globale (network-layer)

**Comunicazione in una LAN:**
1. A inserisce il MAC di B nel frame
2. B riceve il frame, confronta il MAC → accetta se uguale, scarta altrimenti

### 12.5 ARP — Address Resolution Protocol

**Problema:** come trovare il MAC di un host conoscendo solo il suo IP?

**Funzionamento ARP:**
1. A vuole il MAC di B (stessa subnet)
2. A invia **ARP Request in broadcast**: "Chi ha l'IP x.x.x.x?"
3. B risponde **unicast ad A** con il proprio MAC
4. A memorizza `(IP → MAC)` nella **ARP cache** (scade dopo ~20 min)

**Comunicazione fuori dalla subnet:**
A usa ARP per trovare il MAC del **gateway** (router), poi invia il frame al router.

### 12.6 Ethernet

Tecnologia LAN più diffusa. Sviluppata negli anni '70, standardizzata da **IEEE 802.3**.

**Frame Ethernet:**
```
┌──────────────┬──────────┬──────────┬──────┬────────────┬──────┐
│ Preamble (8B)│ Dst MAC  │ Src MAC  │ Type │ Data       │  CRC │
│              │  (6B)    │  (6B)    │ (2B) │ 46-1500 B  │ (4B) │
└──────────────┴──────────┴──────────┴──────┴────────────┴──────┘
```

| Campo | Descrizione |
|-------|-------------|
| **Preamble** | Sequenza di sync (`10101010...10101011`) |
| **Dst/Src MAC** | Indirizzi MAC destinazione/sorgente |
| **Type** | Protocollo superiore (es. 0x0800 = IPv4) |
| **Data** | Payload (46-1500 byte, MTU = 1500 byte) |
| **CRC** | Rilevamento errori |

> Ethernet è **connectionless** e **non affidabile**: nessun handshake, nessuna retransmission (gestiti da TCP).

### 12.7 Switch di Rete

- **Transparent**: gli host non sanno che esiste
- **Self-learning**: impara da solo quali MAC sono su quali porte
- **Store-and-forward**: riceve frame completo poi lo reinvia

**Switch Table (MAC table):**
- Frame da `src` su porta `p` → aggiunge `(src, p)` alla tabella
- Invio a `dst`:
  - In tabella → invia sulla porta corrispondente (filtering/forwarding)
  - Non in tabella → flood su tutte le porte tranne origine

### 12.8 Schemi e Appunti dalle Lavagne (Lezioni 22, 23 e 24)

![Board Lezione 22 - Pagina 1](assets/board_images/board_L22_p1.png)
*Figura 12.1 — Livello Link: trasmissione di stringhe di bit (frame) influenzata dalle proprietà fisiche del mezzo.*

![Board Lezione 22 - Pagina 2](assets/board_images/board_L22_p2.png)
*Figura 12.2 — Adattatore di rete (scheda NIC) e demarcazione tra host e canale fisico.*

![Board Lezione 22 - Pagina 3](assets/board_images/board_L22_p3.png)
*Figura 12.3 — Tecniche di framing e trasparenza dei dati.*

![Board Lezione 22 - Pagina 4](assets/board_images/board_L22_p4.png)
*Figura 12.4 — Rilevamento e correzione degli errori: bit di parità bidimensionale e CRC.*

![Board Lezione 22 - Pagina 5](assets/board_images/board_L22_p5.png)
*Figura 12.5 — Incapsulamento del datagramma IP all'interno del frame di livello 2.*

![Board Lezione 23 - Pagina 1](assets/board_images/board_L23_p1.png)
*Figura 12.6 — Reti ad accesso condiviso: diffusione in broadcast e ricezione da parte di tutte le stazioni.*

![Board Lezione 23 - Pagina 2](assets/board_images/board_L23_p2.png)
*Figura 12.7 — Concetto di collisione ed efficienza del canale condiviso.*

![Board Lezione 24 - Pagina 1](assets/board_images/board_L24_p1.png)
*Figura 12.8 — Protocollo CSMA/CD: ascolto del canale prima e durante la trasmissione.*

![Board Lezione 24 - Pagina 2](assets/board_images/board_L24_p2.png)
*Figura 12.9 — Condizione sul tempo minimo di trasmissione per rilevare collisioni su tutto il dominio.*

![Board Lezione 24 - Pagina 3](assets/board_images/board_L24_p3.png)
*Figura 12.10 — Algoritmo di backoff esponenziale binario: gestione dei ritrasferimenti post-collisione.*

![Board Lezione 24 - Pagina 4](assets/board_images/board_L24_p4.png)
*Figura 12.11 — Prestazioni di Ethernet e confronto con i protocolli ad accesso casuale puro.*

---

## 13. Sicurezza delle Reti
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 13.1 Obiettivi della Sicurezza

| Obiettivo | Descrizione |
|-----------|-------------|
| **Confidenzialità** | Solo mittente e destinatario possono capire il contenuto |
| **Integrità** | Il contenuto non deve essere alterato |
| **Disponibilità** | Servizi accessibili agli utenti autorizzati |
| **Autenticazione** | Verifica dell'identità di mittente/destinatario |
| **Non-ripudio** | Il mittente non può negare di aver inviato il messaggio |

### 13.2 Tipi di Attacchi

#### Eavesdropping (Intercettazione)
Un attaccante **legge** i messaggi (es. con Wireshark).
**Protezione:** cifratura.

#### Man-in-the-Middle (MitM)
L'attaccante **legge, altera o inietta** messaggi tra mittente e destinatario.
- **IP Spoofing**: pacchetti con IP sorgente falso
- **ARP Poisoning**: risposte ARP false per redirigere il traffico
- **DNS Poisoning**: modifica risposte DNS

#### Denial of Service (DoS/DDoS)
Rende un servizio non disponibile inondandolo di richieste.
- **Bandwidth flooding**: inonda il link di destinazione
- **SYN flood**: connessioni TCP half-open
- **DDoS**: attacco coordinato da botnet

### 13.3 Crittografia Simmetrica

Stessa chiave per cifrare e decifrare:
```
Testo chiaro ──[Chiave K]──► Cifrato
Cifrato ──[Chiave K]──► Testo chiaro
```

| Algoritmo | Chiave | Stato |
|-----------|--------|-------|
| DES | 56 bit | Insicuro |
| 3DES | 168 bit | Deprecato |
| **AES** | 128/192/256 bit | ✅ Standard attuale |

**Svantaggio:** Key distribution problem.

### 13.4 Crittografia Asimmetrica (Chiave Pubblica)

Due chiavi:
- **K⁺ (pubblica)**: nota a tutti, per **cifrare**
- **K⁻ (privata)**: solo al proprietario, per **decifrare**

```
Mittente:     Testo ──[K⁺ dest]──► Cifrato
Destinatario: Cifrato ──[K⁻ proprio]──► Testo
```

**Algoritmi:** RSA (fattorizzazione), Diffie-Hellman (scambio chiavi).

**Firma digitale:** il mittente "firma" con K⁻; chiunque verifica con K⁺.

### 13.5 Integrità — Hash e MAC

**Funzioni hash crittografiche:**
- Output di lunghezza fissa (digest)
- One-way: impossibile ricavare input dall'hash
- Collision-free

| Algoritmo | Bit | Stato |
|-----------|-----|-------|
| MD5 | 128 | Insicuro |
| SHA-1 | 160 | Deprecato |
| SHA-256 | 256 | ✅ Sicuro |

**MAC (Message Authentication Code):**
```
MAC = H(messaggio + chiave_segreta)
```
Garantisce **integrità** e **autenticità**.

### 13.6 TLS/SSL

**TLS** protegge la comunicazione HTTPS. Fornisce:
- **Cifratura** (confidenzialità)
- **Autenticazione del server** (certificato)
- **Integrità** dei messaggi

**Handshake TLS (semplificato):**
```
Client ──ClientHello (versione, cifrari) ──────────────────► Server
Client ◄── ServerHello (cifrario scelto) + Certificato ─────
Client ──ClientKeyExchange + ChangeCipherSpec + Finished ──► Server
Client ◄── ChangeCipherSpec + Finished ──────────────────────
Client ◄══════════ Comunicazione cifrata ════════════════════ Server
```

### 13.7 Firewall e IDS

**Firewall:** filtra il traffico in base a regole predefinite.

| Tipo | Livello |
|------|---------|
| **Packet filter** | Filtra su IP/porta/protocollo |
| **Stateful filter** | Tiene traccia dello stato delle connessioni |
| **Application gateway** | Filtra a livello applicativo |

**IDS (Intrusion Detection System):** monitora il traffico per pattern sospetti.
**IPS (Intrusion Prevention System):** come IDS ma può bloccare automaticamente.

### 13.8 Schemi e Appunti dalle Lavagne (Lezioni 25 e 26)

![Board Lezione 25 - Pagina 1](assets/board_images/board_L25_p1.png)
*Figura 13.1 — Protocollo di scambio di chiavi Diffie-Hellman: modulo primo $p$ e generatore $g$.*

![Board Lezione 25 - Pagina 2](assets/board_images/board_L25_p2.png)
*Figura 13.2 — Calcolo della chiave simmetrica comune senza trasmettere il segreto sul canale.*

![Board Lezione 25 - Pagina 3](assets/board_images/board_L25_p3.png)
*Figura 13.3 — Attacco Man-in-the-Middle (Intruder T) su Diffie-Hellman in assenza di autenticazione.*

![Board Lezione 25 - Pagina 4](assets/board_images/board_L25_p4.png)
*Figura 13.4 — Risoluzione della vulnerabilità MitM mediante certificati digitali e firma a chiave pubblica.*

![Board Lezione 26 - Pagina 1](assets/board_images/board_L26_p1.png)
*Figura 13.5 — Cifrari a sostituzione monoalfabetica: mappatura di ciascun simbolo con la chiave segreta.*

![Board Lezione 26 - Pagina 2](assets/board_images/board_L26_p2.png)
*Figura 13.6 — Cifrari a trasposizione e permutazione dell'ordine dei caratteri nel testo cifrato.*

![Board Lezione 26 - Pagina 3](assets/board_images/board_L26_p3.png)
*Figura 13.7 — Principi di crittanalisi: vulnerabilità delle sostituzioni all'analisi delle frequenze.*

---

## 14. Programmazione REST e Formati di Scambio Dati
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 14.1 REST — Representational State Transfer

Stile architetturale per web service basato su HTTP.

**Principi REST:**
1. **Architettura client-server**: separazione client/server
2. **Statelessness**: ogni richiesta è indipendente
3. **Cacheability**: le risposte indicano se cacheable
4. **Uniform Interface**: risorse + metodi HTTP
5. **Layered system**: client non sa se parla con server finale o intermediario
6. **Code on demand** (opzionale): server invia codice eseguibile

### 14.2 Risorse e URI

Tutto è una **risorsa** identificata da URI:

```
GET    /utenti           → Elenco utenti
GET    /utenti/123       → Utente con ID 123
POST   /utenti           → Crea nuovo utente
PUT    /utenti/123       → Aggiorna utente 123 (completo)
PATCH  /utenti/123       → Aggiorna utente 123 (parziale)
DELETE /utenti/123       → Elimina utente 123
```

### 14.3 Formati di Scambio Dati

**JSON:**
```json
{
    "nome": "Mario",
    "cognome": "Rossi",
    "età": 25,
    "email": "mario@esempio.it",
    "attivo": true
}
```

**XML:**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<utente>
    <nome>Mario</nome>
    <cognome>Rossi</cognome>
    <email>mario@esempio.it</email>
</utente>
```

### 14.4 Interazione con REST API (curl)

```bash
# GET
curl https://api.esempio.com/utenti

# GET con autenticazione
curl -H "Authorization: Bearer TOKEN" https://api.esempio.com/utenti/123

# POST
curl -X POST -H "Content-Type: application/json" \
     -d '{"nome": "Mario"}' https://api.esempio.com/utenti

# PUT
curl -X PUT -H "Content-Type: application/json" \
     -d '{"nome": "Mario Rossi"}' https://api.esempio.com/utenti/123

# DELETE
curl -X DELETE https://api.esempio.com/utenti/123
```

**Codici risposta REST comuni:**

| Codice | Significato |
|--------|-------------|
| 200 OK | Successo |
| 201 Created | Risorsa creata |
| 204 No Content | Successo senza risposta |
| 400 Bad Request | Parametri non validi |
| 401 Unauthorized | Autenticazione richiesta |
| 403 Forbidden | Accesso negato |
| 404 Not Found | Risorsa non trovata |
| 500 Internal Server Error | Errore del server |

---

## 15. Esercizi Risolti e Sessioni di Domande e Risposte
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### 15.1 Esercizi su HTTP (L04)

#### Esercizio 1 — RTT con connessioni non persistenti

**Testo:** Browser richiede 1 HTML + 5 JPEG. RTT=20ms, t_HTML=2ms, t_JPEG=5ms. Connessioni non persistenti sequenziali.

**Soluzione:**

Ogni oggetto: TCP handshake (1 RTT) + req/risposta HTTP (1 RTT + t_trasmissione).

- HTML: 20 + 20 + 2 = **42 ms**
- Ogni JPEG: 20 + 20 + 5 = **45 ms**

**Totale sequenziale:** 42 + 5×45 = 42 + 225 = **267 ms**

**Con connessioni parallele:** 42 + 45 = **87 ms**

### 15.2 Esercizi su UDP — Checksum

#### Esercizio 2 — Calcolo Checksum

**Testo:** 3 parole a 16 bit:
```
Parola 1: 1101011011000110
Parola 2: 0110110011001101
Parola 3: 1000000101001011
```

**Soluzione:**

Somma 1+2:
```
  1101011011000110
+ 0110110011001101
= 10100001110010011  → overflow → +1 → 0100001110010100
```

Somma con parola 3:
```
  0100001110010100
+ 1000000101001011
= 1100010011011111
```

Checksum = complemento a 1: `0011101100100000`

**Verifica:** `1100010011011111 + 0011101100100000 = 1111111111111111` ✅

### 15.3 Esercizi su Go-Back-N

#### Esercizio 3 — Analisi GBN

**Testo:** GBN con N=4, sequenza 3 bit (0-7). Ordine invio: 0,1,2,3,4,5. Pacchetto 2 perso.

**Soluzione:**

```
Mittente → pkt 0 → Destinatario: ricevuto, ACK 0
Mittente → pkt 1 → Destinatario: ricevuto, ACK 1
Mittente → pkt 2 → PERSO
Mittente → pkt 3 → Destinatario: fuori ordine, SCARTATO, invia ACK 1 (dup)
[Timeout per pkt 2]
Mittente → pkt 2 → Destinatario: ricevuto, ACK 2
Mittente → pkt 3 → Destinatario: ricevuto, ACK 3
...
```

Con GBN, pkt 3 viene scartato e **deve essere ritrasmesso** anche se correttamente ricevuto.

### 15.4 Esercizi su IP e Subnetting

#### Esercizio 4 — Suddivisione in Sottoreti

**Testo:** Suddividi `192.168.10.0/24` in 4 sottoreti uguali.

**Soluzione:**

256 indirizzi / 4 = 64 indirizzi per sottorete → **/26** (subnet mask /26 = 255.255.255.192)

| Sottorete | Rete | Range host | Broadcast |
|-----------|------|------------|-----------|
| 1 | 192.168.10.0/26 | .1 – .62 | .63 |
| 2 | 192.168.10.64/26 | .65 – .126 | .127 |
| 3 | 192.168.10.128/26 | .129 – .190 | .191 |
| 4 | 192.168.10.192/26 | .193 – .254 | .255 |

#### Esercizio 5 — ARP

**Testo:** Host A (`192.168.1.10`, `AA:BB:CC:DD:EE:01`) vuole comunicare con B (`192.168.1.20`). Descrivi il processo ARP.

**Soluzione:**

1. A controlla ARP cache → MAC di B non trovato
2. A invia **ARP Request in broadcast** (dst MAC: FF:FF:FF:FF:FF:FF): "Chi ha `192.168.1.20`?"
3. Tutti ricevono; solo B risponde con **ARP Reply unicast**: "Io ho `192.168.1.20`, il mio MAC è `BB:CC:DD:EE:FF:02`"
4. A aggiorna la ARP cache: `192.168.1.20 → BB:CC:DD:EE:FF:02`
5. A può ora inviare frame direttamente a B

### 15.5 Algoritmo di Dijkstra

#### Esercizio 6 — Link-State da nodo u

**Grafo:**
```
u ─2─ v ─3─ w
│     │     │
5     1     4
│     │     │
x ─3─ y ─2─ z
```

**Costi:** u-v:2, u-x:5, v-w:3, v-z:1, w-z:4, x-y:3, y-z:2

**Iterazioni Dijkstra da u:**

| Passo | N' | D(v) | D(w) | D(x) | D(y) | D(z) |
|-------|-----|------|------|------|------|------|
| Init | {u} | 2 | ∞ | 5 | ∞ | ∞ |
| 1 | {u,v} | 2 | 5 | 5 | ∞ | 3 |
| 2 | {u,v,z} | 2 | 5 | 5 | 5 | 3 |
| 3 | {u,v,z,w} | — | 5 | 5 | 5 | — |
| 4 | {u,v,z,w,x o y} | — | — | 5 | 5 | — |
| 5 | {u,v,z,w,x,y} | — | — | 5 | 5 | — |

**Percorsi ottimali da u:**

| Destinazione | Costo | Percorso |
|-------------|-------|---------|
| v | 2 | u→v |
| z | 3 | u→v→z |
| w | 5 | u→v→w |
| x | 5 | u→x |
| y | 5 | u→v→z→y |

---

---

## 16. Guide Pratiche di Laboratorio con Wireshark
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

Questo capitolo raccoglie e documenta dettagliatamente tutte le esercitazioni pratiche svolte con il packet sniffer **Wireshark** nel corso delle lezioni, con istruzioni sui comandi di sistema, filtri da applicare e analisi delle risposte.

### 16.1 Installazione e Configurazione di Wireshark su Linux (Ubuntu/Debian)

Per eseguire catture di rete come utente non privilegiato (evitando di eseguire l'intera GUI con `sudo`), è fondamentale configurare correttamente i gruppi di sistema e le Linux Capabilities sul binario `dumpcap`.

**1. Installazione via APT:**
```bash
sudo apt update
sudo apt install wireshark
```
Durante l'installazione, alla schermata interattiva di debconf che richiede:
> *"Should non-superusers be able to capture packets?"*
selezionare tassativamente **Sì (Yes)**.

**2. Verifica e configurazione dei gruppi utente:**
```bash
# Verifica se esiste il gruppo di sistema 'wireshark'
getent group wireshark

# Aggiungi l'utente corrente al gruppo wireshark
sudo usermod -aG wireshark $USER

# Riconfigura il pacchetto nel caso in cui fosse stato selezionato 'No' in precedenza
sudo dpkg-reconfigure wireshark-common
```

**3. Impostazione delle Capabilities su dumpcap:**
Il binario di cattura necessita dei permessi di accesso grezzo alla rete (`cap_net_raw`) e amministrazione delle interfacce (`cap_net_admin`):
```bash
# Assegna le capabilities
sudo setcap cap_net_raw,cap_net_admin+eip /usr/bin/dumpcap

# Verifica i permessi impostati
getcap /usr/bin/dumpcap
# Output corretto: /usr/bin/dumpcap = cap_net_admin,cap_net_raw+eip

# Assicura i permessi di esecuzione
sudo chmod +x /usr/bin/dumpcap

# Applica le modifiche senza riavviare
newgrp wireshark
```

---

### 16.2 Laboratorio HTTP GET Base (L04)

**Obiettivo:** Esaminare la struttura dettagliata di un'interazione HTTP client-server, osservando la richiesta `GET` e la risposta `200 OK`.

**Procedura passo-passo:**
1. Aprire Wireshark e selezionare l'interfaccia di rete principale (es. `eth0` o `wlan0`).
2. Nella barra del filtro di visualizzazione (*Display Filter*), inserire:
   ```
   http
   ```
3. Avviare la cattura dei pacchetti (icona della pinna blu).
4. Aprire il browser web e digitare l'URL di test:
   ```
   http://www.columbia.edu/~fdc/sample.html
   ```
5. Una volta visualizzata la pagina, fermare immediatamente la cattura (quadrato rosso).

**Analisi dei messaggi catturati:**
- **Messaggio di Richiesta (`GET /~fdc/sample.html HTTP/1.1`):**
  - **Versione HTTP:** Il browser moderno usa tipicamente `HTTP/1.1`.
  - **Campi Header:**
    - `Host: www.columbia.edu`
    - `User-Agent`: Stringa identificativa del browser e del SO.
    - `Accept`: Tipi MIME accettati (es. `text/html,application/xhtml+xml`).
    - `Accept-Language`: Lingue preferite dal client (es. `it-IT,it;q=0.9,en-US;q=0.8`).
    - `Accept-Encoding`: Algoritmi di compressione supportati (`gzip, deflate, br`).
- **Messaggio di Risposta (`HTTP/1.1 200 OK`):**
  - **Codice di stato:** `200 OK` (richiesta completata con successo).
  - `Content-Type: text/html; charset=ISO-8859-1`
  - `Content-Length`: Dimensione in byte del payload HTML.
  - `Last-Modified`: Data dell'ultimo aggiornamento del documento sul server (aggiornato periodicamente dal server di test per evitare caching permanente).

---

### 16.3 Laboratorio HTTP con Download Multi-segmento (L05)

**Obiettivo:** Comprendere il riassemblaggio di un messaggio a livello applicazione suddiviso in più segmenti TCP a causa dei limiti di MTU/MSS.

**Concetto chiave:**
Un singolo messaggio HTTP con un corpo (entity body) di dimensioni rilevanti non può entrare in un unico pacchetto IP (limitato dalla MTU standard di 1500 byte, pari a un MSS tipico di 1460 byte). Wireshark evidenzia i segmenti intermedi con la dicitura:
```
[TCP segment of a reassembled PDU]
```

**Analisi del flusso:**
1. Il client invia il pacchetto HTTP contenente il messaggio `GET`.
2. Il server invia una serie di pacchetti TCP contenenti frammenti del file HTML. Ciascun pacchetto trasporta un blocco di dati con numero di sequenza incrementale:
   - Pacchetto 1: `Seq = 1`, `Len = 1460`
   - Pacchetto 2: `Seq = 1461`, `Len = 1460`
   - Pacchetto N: `Seq = ...`, `Len = ...`
3. Il client invia i relativi riscontri (`ACK`) per confermare la ricezione dei byte.
4. L'ultimo segmento TCP chiude il trasferimento del corpo del messaggio: Wireshark riassembla tutti i segmenti e visualizza l'intestazione HTTP della risposta (`HTTP/1.1 200 OK`) associata a questo pacchetto finale.

---

### 16.4 Laboratorio Analisi DNS con nslookup (L10)

**Obiettivo:** Ispezionare i pacchetti DNS (UDP porta 53), identificando la struttura delle query e delle risposte, la gerarchia dei record e il comportamento dei server ricorsivi.

**Filtro Wireshark fondamentale:**
```
dns
```

**Parte 1 — Query Standard di Tipo A (Indirizzo IPv4):**
Eseguire nel terminale:
```bash
nslookup www.unina.it
```
- **Porto destinazione della Query:** `UDP 53`.
- **Porto sorgente della Risposta:** `UDP 53` (inviata dal resolver locale configurato sull'host).
- **Sezione *Queries*:** contiene il nome cercato (`www.unina.it`), la classe `IN` (Internet) e il Type `A` (IPv4).
- **Sezione *Answers*:** restituisce i record `A` contenenti gli indirizzi IP associati al nome di dominio.

**Parte 2 — Query di Tipo NS (Name Server autoritativi):**
Eseguire nel terminale:
```bash
nslookup -type=NS unina.it
```
- La risposta contiene l'elenco dei server autoritativi per il dominio (es. `ns1.unina.it`, `ns2.unina.it`).
- **Additional Records:** Spesso il server include record di tipo `A` (chiamati *Glue Records*) che specificano gli indirizzi IP dei name server elencati, consentendo al client di contattarli senza dover emettere ulteriori interrogazioni DNS separate.

---

### 16.5 Laboratorio Traceroute, ICMP e Frammentazione IP (L19)

**Obiettivo:** Ricostruire il percorso attraverso i router di rete tramite l'utility `traceroute` e analizzare la gestione del campo Time To Live (TTL) e della frammentazione dei datagrammi IP.

**Principio di funzionamento di Traceroute:**
Traceroute invia sonde UDP verso porte elevate non utilizzate (es. > 33434):
1. **Sonda con $TTL = 1$**: il primo router decrementa il TTL a 0, scarta il pacchetto e invia al mittente un messaggio:
   ```
   ICMP Type 11, Code 0: Time-to-live exceeded in transit
   ```
   L'indirizzo IP sorgente di questo pacchetto ICMP rivela l'identità del primo router (hop 1).
2. **Sonda con $TTL = 2$**: scade al secondo router, che risponde analogamente.
3. Il processo prosegue incrementando il TTL finché la sonda raggiunge l'host destinazione, il quale (non trovando alcun servizio in ascolto sulla porta UDP elevata) risponde con:
   ```
   ICMP Type 3, Code 3: Destination Unreachable (Port Unreachable)
   ```
   A questo punto Traceroute sa di aver raggiunto la meta e conclude la scansione.

**Comandi di test:**
```bash
# Traceroute standard
traceroute italia.it

# Traceroute con pacchetti di dimensione maggiorata (3000 byte per forzare la frammentazione)
traceroute italia.it 3000
```

**Analisi della Frammentazione IP in Wireshark:**
- Con datagrammi da 3000 byte su una rete con MTU di 1500 byte, il datagramma IP viene suddiviso in 3 frammenti:
  1. **Frammento 1:** `Offset = 0`, flag `More Fragments (MF) = 1`, lunghezza 1500 byte (20B header IP + 1480B payload).
  2. **Frammento 2:** `Offset = 185` (poiché $185 × 8 = 1480$ byte), flag `MF = 1`, lunghezza 1500 byte.
  3. **Frammento 3:** `Offset = 370` ($370 × 8 = 2960$ byte), flag `MF = 0` (ultimo frammento), lunghezza residua (~68 byte).
- Tutti i frammenti condividono lo stesso identico valore nel campo **Identification** dell'header IPv4.

---

### 16.6 Tabella Riepilogativa dei Filtri Wireshark per l'Esame

| Protocollo | Filtro di Visualizzazione (*Display Filter*) | Note ed Utilizzo |
|------------|---------------------------------------------|------------------|
| **HTTP** | `http` | Mostra solo le richieste e risposte HTTP |
| **HTTP Errori** | `http.response.code >= 400` | Isola solo errori client (`4xx`) e server (`5xx`) |
| **DNS** | `dns` | Mostra query e risposte DNS |
| **DNS Tipo A** | `dns.qry.type == 1` | Isola solo le query per indirizzi IPv4 |
| **TCP** | `tcp.port == 80` oppure `tcp.port == 443` | Traffico TCP su web (HTTP o HTTPS) |
| **Handshake TCP** | `tcp.flags.syn == 1` | Filtra solo pacchetti `SYN` e `SYN-ACK` di apertura |
| **Reset TCP** | `tcp.flags.reset == 1` | Identifica connessioni abortite o rifiutate |
| **ICMP** | `icmp` | Mostra messaggi ping e risposte traceroute |
| **Time Exceeded** | `icmp.type == 11` | Pacchetti TTL scaduto generati da Traceroute |
| **Host Specifico** | `ip.addr == 192.168.1.1` | Tutto il traffico da/verso uno specifico host IP |


---

## 17. Sessione di Ripasso e Domande d'Esame Svolte (QA01)
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

In questo capitolo sono raccolte le domande di ripasso formali ed aperte del documento d'esame **QA01**, con le relative soluzioni e approfondimenti numerici svolti dal docente.

### 17.1 Domande su HTTP (Application Layer)

#### Domanda 1(a) — Struttura dell'URL
*Spiegare quali sono le parti di un URL e qual è l'uso di ciascuna.*

**Risposta Svolta:**
Un **Uniform Resource Locator (URL)** identifica univocamente una risorsa sulla rete globale ed è strutturato come:
```
<protocollo>://<host>:<porta>/<percorso>?<parametri>#<frammento>
```
1. **Protocollo / Schema** (es. `http`, `https`, `ftp`): definisce le regole di comunicazione e il linguaggio da utilizzare per recuperare la risorsa.
2. **Host / Nome di Dominio** (es. `www.unina.it` o indirizzo IP `192.168.1.1`): individua la macchina server che ospita la risorsa.
3. **Porta** (opzionale, default 80 per HTTP, 443 per HTTPS): identifica il processo server a livello di trasporto a cui recapitare la richiesta.
4. **Percorso / Path** (es. `/dipartimento/corsi/reti.html`): specifica la collocazione gerarchica della risorsa nel file system logico del server.
5. **Query String** (es. `?id=42&lang=it`): serie di coppie chiave-valore per inviare parametri dinamici ad applicazioni o script lato server.
6. **Frammento / Anchor** (es. `#sezione-2`): riferimento interno al documento, interpretato solo dal browser del client senza essere inviato al server.

#### Domanda 1(b) — Three-Way Handshake prima di HTTP
*Spiegare brevemente il three-way handshake usato per stabilire una connessione HTTP.*

**Risposta Svolta:**
Poiché HTTP si basa sul protocollo affidabile orientato alla connessione **TCP**, prima di inviare qualsiasi richiesta HTTP deve essere completato il Three-Way Handshake:
1. **Client $\to$ Server (`SYN`):** Il client sceglie un numero di sequenza iniziale casuale $ISN_c$ e invia un segmento con flag `SYN = 1`, `Seq = ISN_c`.
2. **Server $\to$ Client (`SYN-ACK`):** Il server alloca i buffer, sceglie il proprio $ISN_s$ e risponde con `SYN = 1`, `ACK = 1`, `Seq = ISN_s`, `Ack = ISN_c + 1`.
3. **Client $\to$ Server (`ACK`):** Il client conferma con `ACK = 1`, `Seq = ISN_c + 1`, `Ack = ISN_s + 1`. In questo terzo pacchetto il client può già inserire i dati della prima richiesta `HTTP GET` (risparmiando un RTT).

#### Domanda 1(c) — Pipelining in HTTP
*Illustrare cosa è il pipelining in HTTP.*

**Risposta Svolta:**
In **HTTP/1.1 con connessioni persistenti**, il **pipelining** consente al client di inviare richieste successive per risorse multiple (es. immagini collegate in una pagina HTML) senza dover attendere la ricezione della risposta alla richiesta precedente.
Il server è vincolato a processare e restituire le risposte **nello stesso identico ordine** in cui ha ricevuto le relative richieste (FIFO). Questo meccanismo riduce drasticamente i tempi di attesa dell'RTT, ma è affetto dal problema dell'**Head-of-Line Blocking (HOL)** a livello applicativo: se la prima richiesta richiede un tempo di calcolo elevato sul server, tutte le risposte successive rimangono bloccate in coda.

#### Domanda 1(d) — Protocollo di trasporto di HTTP
*Su quali protocolli a livello di trasporto è basato il protocollo HTTP?*

**Risposta Svolta:**
- **HTTP/1.0, HTTP/1.1 e HTTP/2** sono basati tassativamente su **TCP**, sfruttando la sua garanzia di consegna affidabile, ordinata e senza duplicati, oltre al controllo di congestione e flusso.
- **HTTP/3** è basato su **QUIC**, un protocollo di trasporto di nuova generazione che poggia su **UDP**, spostando la gestione dell'affidabilità, della crittografia (TLS 1.3 integrata) e del multiplexing nativo a livello utente per eliminare completamente l'HOL blocking.

---

### 17.2 Domande su DNS (Application Layer)

#### Domanda 2(a) — Modifica dell'indirizzo IP e ruolo del TTL
*Supponiamo che si cambi l'indirizzo IP di una macchina denominata `server-1.ortofrutta.it`. Spiegare come è gestito l'aggiornamento affinché la modifica sia riflessa nel DNS.*

**Risposta Svolta:**
Nel sistema DNS **non esiste un meccanismo di invalidazione attiva (push / flush globale)** da parte del server autoritativo verso le cache di tutti gli altri DNS resolver distribuiti nel mondo:
1. L'amministratore aggiorna il record di tipo `A` sul **Name Server autoritativo** della zona `ortofrutta.it`.
2. I client e i server ricorsivi locali continuano a utilizzare le vecchie informazioni memorizzate nella propria **cache locale** fino alla scadenza naturale del contatore **Time To Live (TTL)** associato al record.
3. Durante questo intervallo di tempo (periodo di transizione), si verificano temporanei errori o fallimenti di connessione per gli host che consultano record cache non ancora scaduti. Questo comportamento è una scelta architetturale del DNS, che privilegia la scalabilità e le prestazioni globali rispetto alla consistenza immediata (modello *eventual consistency*).
4. Alla scadenza del TTL, la cache elimina la voce obsoleta; alla richiesta successiva emetterà una nuova query ricorsiva al server autoritativo, prelevando il nuovo indirizzo IP.
> **Best Practice:** Se è pianificata una migrazione di IP, gli amministratori riducono preventivamente il TTL (es. da 86400 secondi / 24 ore a 300 secondi / 5 minuti) qualche giorno prima, in modo che il disallineamento al momento del passaggio effettivo duri pochissimi minuti.

#### Domanda 2(b) — Risoluzione dei nomi e utilizzo dei record NS in cache
*Supponiamo di risolvere il nome `feijoada.dsc.utfpr.edu.br` da un portatile nei laboratori di UniNA (cache locale vuota). La richiesta va a `dscna2.unina.it`, che possiede già in cache un record NS con l'IP del server DNS per `dsc.utfpr.edu.br`. Spiegare come viene gestita la richiesta.*

**Risposta Svolta:**
1. Poiché il server DNS di UniNA (`dscna2.unina.it`) ha già in cache il record `NS` per il sotto-dominio `dsc.utfpr.edu.br`, **non deve risalire l'intera gerarchia globale** (Root server `.`, TLD `.br`, server per `edu.br` e `utfpr.edu.br`).
2. Il server di UniNA contatta direttamente l'indirizzo IP specificato nel record NS di `dsc.utfpr.edu.br`, inviando l'interrogazione per `feijoada.dsc.utfpr.edu.br`.
3. Il server autoritativo per `dsc.utfpr.edu.br` riceve la query, individua nel proprio database di zona il record `A` corrispondente all'host `feijoada` e risponde direttamente al server di UniNA con l'indirizzo IP cercato.
4. `dscna2.unina.it` memorizza il risultato nella propria cache e lo inoltra infine al calcolatore portatile richiedente.

---

### 17.3 Domande su Indirizzi IP e Routing CIDR (Network Layer)

#### Domanda 3(a) — Calcolo del Longest Prefix Match
*Si consideri la seguente tavola di routing di un router che implementa CIDR:*

| Subnet | Next Hop |
|---|---|
| `147.142.168.0/21` | `L1` |
| `147.142.172.0/23` | `L2` |
| `default` | `R0` |

*Due pacchetti IP arrivano al router con indirizzi di destinazione:*
- *Pacchetto 1: `147.142.203.165`*
- *Pacchetto 2: `147.142.173.85`*

*Descrivere dettagliatamente come tali pacchetti sono gestiti e inoltrati.*

**Risoluzione Matematica e Binaria:**

**1. Conversione dei prefissi della tabella in binario:**
I primi due ottetti (`147.142`) sono comuni a tutte le rotte:
- `147` = `10010011`
- `142` = `10001110`

Esaminiamo il terzo ottetto per ciascuna rotta:
- **Rotta 1 (`/21` = 16 + 5 bit del terzo ottetto):**
  - Terzo ottetto: `168` = `10101 000`
  - I primi 5 bit sono: **`10101`**
- **Rotta 2 (`/23` = 16 + 7 bit del terzo ottetto):**
  - Terzo ottetto: `172` = `1010110 0`
  - I primi 7 bit sono: **`1010110`**

---

**2. Analisi Pacchetto 1 (`147.142.203.165`):**
- Terzo ottetto: `203` = `11001011`
- Confronto con Rotta 1 (`/21`): i primi 5 bit di `203` sono `11001`. Il prefisso della rotta è `10101`. **Non c'è match!**
- Confronto con Rotta 2 (`/23`): i primi 7 bit di `203` sono `1100101`. Il prefisso della rotta è `1010110`. **Non c'è match!**
- **Inoltro:** Il pacchetto 1 non corrisponde ad alcuna subnet specifica e viene inoltrato sull'interfaccia di **`default` $\to$ `R0`**.

---

**3. Analisi Pacchetto 2 (`147.142.173.85`):**
- Terzo ottetto: `173` = `10101101`
- Confronto con Rotta 1 (`/21`):
  - Primi 5 bit di `173`: `10101`
  - Prefisso Rotta 1: `10101` $\implies$ **MATCH! (lunghezza prefisso = 21)**
- Confronto con Rotta 2 (`/23`):
  - Primi 7 bit di `173`: `1010110`
  - Prefisso Rotta 2: `1010110` $\implies$ **MATCH! (lunghezza prefisso = 23)**
- **Applicazione della regola del Longest Prefix Match:**
  Entrambe le rotte corrispondono, ma la Rotta 2 ha un prefisso più lungo e specifico ($23 > 21$).
- **Inoltro:** Il pacchetto 2 viene instradato verso il next-hop **`L2`**.

---

#### Domanda 3(b) — Perché i router degli ISP usano CIDR e subnet aggregate
*Spiegare perché i grandi router degli ISP operano con prefissi aggregati (es. `189.103.176.0/20`) anziché su singoli indirizzi IP.*

**Risposta Svolta:**
1. **Scalabilità delle tabelle di routing:** Lo spazio di indirizzamento IPv4 comprende $2^{32} ≈ 4.3$ miliardi di indirizzi. Se ogni host o server richiedesse una voce separata nella tabella di routing, la dimensione delle tabelle saturerebbe la memoria ad altissima velocità dei router (memorie TCAM - Ternary Content-Addressable Memory).
2. **Aggregazione delle rotte (Route Summarization / Supernetting):** Il CIDR consente a un ISP di annunciare al resto del mondo un unico blocco aggregato (es. `/20`, che comprende $2^{12} = 4096$ indirizzi IP individuali). I router della dorsale internet devono solo memorizzare questo singolo prefisso.
3. **Riduzione dell'overhead di elaborazione:** Prefissi aggregati riducono drasticamente sia la complessità della ricerca (lookup) per ogni pacchetto in transito sia il traffico di segnalazione dei protocolli di routing (BGP), che altrimenti dovrebbero propagare aggiornamenti continui per la caduta o l'accensione di singoli host.

---

### 17.4 Schemi e Appunti dalle Lavagne (Sessione QA01)

Di seguito sono riportate le lavagne manoscritte della sessione di ripasso con gli appunti grafici del docente:

![Board QA01 - Pagina 1](assets/board_images/board_QA01_p1.png)
*Figura 17.1 — Discussione sulle repliche DNS, campo TTL e tolleranza degli errori temporanei di caching.*

![Board QA01 - Pagina 2](assets/board_images/board_QA01_p2.png)
*Figura 17.2 — Calcoli di conversione binaria per il Longest Prefix Matching sui pacchetti d'esame.*

![Board QA01 - Pagina 3](assets/board_images/board_QA01_p3.png)
*Figura 17.3 — Regola del Longest Matching Prefix e suddivisione di spazi di indirizzamento senza ambiguità.*


---

## Indice delle Sottosezioni
<div align="right"><em><a href="#indice">Torna all'indice</a></em></div>

### Indice delle Sottosezioni Capitolo 1
- [1.1 Cos'è una Rete di Calcolatori](#11-cosè-una-rete-di-calcolatori)
- [1.2 Internet — La Rete delle Reti](#12-internet-la-rete-delle-reti)
- [1.3 Componenti di una Rete](#13-componenti-di-una-rete)
- [1.4 Comunicazione dei Dati](#14-comunicazione-dei-dati)
- [1.5 Tipi di Connessione e Topologie di Rete](#15-tipi-di-connessione-e-topologie-di-rete)
- [1.6 Categorie di Reti](#16-categorie-di-reti)
- [1.7 Internet Service Providers (ISP)](#17-internet-service-providers-isp)
- [1.8 Il Modello a Strati (Stack Protocollare)](#18-il-modello-a-strati-stack-protocollare)
- [1.9 Schemi e Appunti dalle Lavagne (Lezione 2)](#19-schemi-e-appunti-dalle-lavagne-lezione-2)

### Indice delle Sottosezioni Capitolo 2
- [2.1 Applicazioni di Rete](#21-applicazioni-di-rete)
- [2.2 Architetture delle Applicazioni di Rete](#22-architetture-delle-applicazioni-di-rete)
- [2.3 Comunicazione tra Processi](#23-comunicazione-tra-processi)
- [2.4 QoS — Servizi dello Strato di Trasporto](#24-qos-servizi-dello-strato-di-trasporto)
- [2.5 Protocolli del Livello Applicazione](#25-protocolli-del-livello-applicazione)
- [2.6 FTP — File Transfer Protocol](#26-ftp-file-transfer-protocol)
- [2.7 Schemi e Appunti dalle Lavagne (Lezione 3)](#27-schemi-e-appunti-dalle-lavagne-lezione-3)

### Indice delle Sottosezioni Capitolo 3
- [3.1 World Wide Web e HTTP](#31-world-wide-web-e-http)
- [3.2 URL — Uniform Resource Locator](#32-url-uniform-resource-locator)
- [3.3 HTTP e il Protocollo di Trasporto](#33-http-e-il-protocollo-di-trasporto)
- [3.4 Connessioni HTTP: Persistenti vs. Non Persistenti](#34-connessioni-http-persistenti-vs-non-persistenti)
- [3.5 Formato dei Messaggi HTTP](#35-formato-dei-messaggi-http)
- [3.6 Cookie](#36-cookie)
- [3.7 Web Caching (Proxy)](#37-web-caching-proxy)
- [3.8 Schemi e Appunti dalle Lavagne (Lezione 4)](#38-schemi-e-appunti-dalle-lavagne-lezione-4)

### Indice delle Sottosezioni Capitolo 4
- [4.1 Architettura della Posta Elettronica](#41-architettura-della-posta-elettronica)
- [4.2 SMTP — Simple Mail Transfer Protocol](#42-smtp-simple-mail-transfer-protocol)
- [4.3 Accesso alle Email — POP3, IMAP, HTTP](#43-accesso-alle-email-pop3-imap-http)
- [4.4 Applicazioni P2P e BitTorrent](#44-applicazioni-p2p-e-bittorrent)
- [4.5 DNS — Domain Name System](#45-dns-domain-name-system)
- [4.6 Schemi e Appunti dalle Lavagne (Lezione 7)](#46-schemi-e-appunti-dalle-lavagne-lezione-7)

### Indice delle Sottosezioni Capitolo 5
- [5.1 Socket nell'Architettura a Strati](#51-socket-nellarchitettura-a-strati)
- [5.2 Strutture Dati per le Socket](#52-strutture-dati-per-le-socket)
- [5.3 Creazione della Socket](#53-creazione-della-socket)
- [5.4 Binding della Socket](#54-binding-della-socket)
- [5.5 Programmazione Socket UDP](#55-programmazione-socket-udp)
- [5.6 Programmazione Socket TCP](#56-programmazione-socket-tcp)
- [5.7 Schemi e Appunti dalle Lavagne (Lezioni 8 e 9)](#57-schemi-e-appunti-dalle-lavagne-lezioni-8-e-9)

### Indice delle Sottosezioni Capitolo 6
- [6.1 Dal Livello Applicazione al Livello di Trasporto](#61-dal-livello-applicazione-al-livello-di-trasporto)
- [6.2 Responsabilità del Livello di Trasporto](#62-responsabilità-del-livello-di-trasporto)
- [6.3 Multiplexing e Demultiplexing](#63-multiplexing-e-demultiplexing)
- [6.4 UDP — User Datagram Protocol](#64-udp-user-datagram-protocol)
- [6.5 Formato del Datagramma UDP](#65-formato-del-datagramma-udp)
- [6.6 Checksum UDP](#66-checksum-udp)
- [6.7 Trasferimento Affidabile dei Dati](#67-trasferimento-affidabile-dei-dati)
- [6.8 Schemi e Appunti dalle Lavagne (Lezioni 10, 11 e 12)](#68-schemi-e-appunti-dalle-lavagne-lezioni-10-11-e-12)

### Indice delle Sottosezioni Capitolo 7
- [7.1 Caratteristiche di TCP](#71-caratteristiche-di-tcp)
- [7.2 Buffer TCP](#72-buffer-tcp)
- [7.3 Maximum Segment Size (MSS)](#73-maximum-segment-size-mss)
- [7.4 Segmento TCP](#74-segmento-tcp)
- [7.5 Numeri di Sequenza e Acknowledgment](#75-numeri-di-sequenza-e-acknowledgment)
- [7.6 Stima del RTT e Timeout](#76-stima-del-rtt-e-timeout)
- [7.7 Ritrasmissione Rapida (Fast Retransmit)](#77-ritrasmissione-rapida-fast-retransmit)
- [7.8 Three-Way Handshake (Stabilimento Connessione)](#78-three-way-handshake-stabilimento-connessione)
- [7.9 Teardown della Connessione](#79-teardown-della-connessione)
- [7.10 Schemi e Appunti dalle Lavagne (Lezioni 13 e 16)](#710-schemi-e-appunti-dalle-lavagne-lezioni-13-e-16)

### Indice delle Sottosezioni Capitolo 8
- [8.1 Flow Control (Controllo di Flusso)](#81-flow-control-controllo-di-flusso)
- [8.2 Congestion Control (Controllo della Congestione)](#82-congestion-control-controllo-della-congestione)
- [8.3 Algoritmo di Jacobson — Rate Regulation](#83-algoritmo-di-jacobson-rate-regulation)

### Indice delle Sottosezioni Capitolo 9
- [9.1 Funzioni del Livello di Rete](#91-funzioni-del-livello-di-rete)
- [9.2 Servizi del Livello di Rete](#92-servizi-del-livello-di-rete)
- [9.3 Router: Forwarding e Routing](#93-router-forwarding-e-routing)
- [9.4 Tipi di Router](#94-tipi-di-router)
- [9.5 Componenti di un Router](#95-componenti-di-un-router)
- [9.6 Longest Prefix Matching](#96-longest-prefix-matching)
- [9.7 Schemi e Appunti dalle Lavagne (Lezioni 14 e 15)](#97-schemi-e-appunti-dalle-lavagne-lezioni-14-e-15)

### Indice delle Sottosezioni Capitolo 10
- [10.1 Indirizzo IP (IPv4)](#101-indirizzo-ip-ipv4)
- [10.2 Subnetting](#102-subnetting)
- [10.3 DHCP — Dynamic Host Configuration Protocol](#103-dhcp-dynamic-host-configuration-protocol)
- [10.4 NAT — Network Address Translation](#104-nat-network-address-translation)
- [10.5 IPv6](#105-ipv6)
- [10.6 Schemi e Appunti dalle Lavagne (Lezione 17)](#106-schemi-e-appunti-dalle-lavagne-lezione-17)

### Indice delle Sottosezioni Capitolo 11
- [11.1 Introduzione al Routing](#111-introduzione-al-routing)
- [11.2 Flooding](#112-flooding)
- [11.3 Formulazione del Problema di Routing](#113-formulazione-del-problema-di-routing)
- [11.4 Algoritmo Distance Vector (DV)](#114-algoritmo-distance-vector-dv)
- [11.5 Algoritmo Link-State (LS) — Dijkstra](#115-algoritmo-link-state-ls-dijkstra)
- [11.6 Confronto DV vs. LS](#116-confronto-dv-vs-ls)
- [11.7 Schemi e Appunti dalle Lavagne (Lezioni 18, 19, 20 e 21)](#117-schemi-e-appunti-dalle-lavagne-lezioni-18-19-20-e-21)

### Indice delle Sottosezioni Capitolo 12
- [12.1 Funzioni del Link Layer](#121-funzioni-del-link-layer)
- [12.2 Framming e Rilevamento Errori](#122-framming-e-rilevamento-errori)
- [12.3 Protocolli MAC](#123-protocolli-mac)
- [12.4 Indirizzi MAC](#124-indirizzi-mac)
- [12.5 ARP — Address Resolution Protocol](#125-arp-address-resolution-protocol)
- [12.6 Ethernet](#126-ethernet)
- [12.7 Switch di Rete](#127-switch-di-rete)
- [12.8 Schemi e Appunti dalle Lavagne (Lezioni 22, 23 e 24)](#128-schemi-e-appunti-dalle-lavagne-lezioni-22-23-e-24)

### Indice delle Sottosezioni Capitolo 13
- [13.1 Obiettivi della Sicurezza](#131-obiettivi-della-sicurezza)
- [13.2 Tipi di Attacchi](#132-tipi-di-attacchi)
- [13.3 Crittografia Simmetrica](#133-crittografia-simmetrica)
- [13.4 Crittografia Asimmetrica (Chiave Pubblica)](#134-crittografia-asimmetrica-chiave-pubblica)
- [13.5 Integrità — Hash e MAC](#135-integrità-hash-e-mac)
- [13.6 TLS/SSL](#136-tlsssl)
- [13.7 Firewall e IDS](#137-firewall-e-ids)
- [13.8 Schemi e Appunti dalle Lavagne (Lezioni 25 e 26)](#138-schemi-e-appunti-dalle-lavagne-lezioni-25-e-26)

### Indice delle Sottosezioni Capitolo 14
- [14.1 REST — Representational State Transfer](#141-rest-representational-state-transfer)
- [14.2 Risorse e URI](#142-risorse-e-uri)
- [14.3 Formati di Scambio Dati](#143-formati-di-scambio-dati)
- [14.4 Interazione con REST API (curl)](#144-interazione-con-rest-api-curl)

### Indice delle Sottosezioni Capitolo 15
- [15.1 Esercizi su HTTP (L04)](#151-esercizi-su-http-l04)
- [15.2 Esercizi su UDP — Checksum](#152-esercizi-su-udp-checksum)
- [15.3 Esercizi su Go-Back-N](#153-esercizi-su-go-back-n)
- [15.4 Esercizi su IP e Subnetting](#154-esercizi-su-ip-e-subnetting)
- [15.5 Algoritmo di Dijkstra](#155-algoritmo-di-dijkstra)

### Indice delle Sottosezioni Capitolo 16
- [16.1 Installazione e Configurazione di Wireshark su Linux (Ubuntu/Debian)](#161-installazione-e-configurazione-di-wireshark-su-linux-ubuntudebian)
- [16.2 Laboratorio HTTP GET Base (L04)](#162-laboratorio-http-get-base-l04)
- [16.3 Laboratorio HTTP con Download Multi-segmento (L05)](#163-laboratorio-http-con-download-multi-segmento-l05)
- [16.4 Laboratorio Analisi DNS con nslookup (L10)](#164-laboratorio-analisi-dns-con-nslookup-l10)
- [16.5 Laboratorio Traceroute, ICMP e Frammentazione IP (L19)](#165-laboratorio-traceroute-icmp-e-frammentazione-ip-l19)
- [16.6 Tabella Riepilogativa dei Filtri Wireshark per l'Esame](#166-tabella-riepilogativa-dei-filtri-wireshark-per-lesame)

### Indice delle Sottosezioni Capitolo 17
- [17.1 Domande su HTTP (Application Layer)](#171-domande-su-http-application-layer)
- [17.2 Domande su DNS (Application Layer)](#172-domande-su-dns-application-layer)
- [17.3 Domande su Indirizzi IP e Routing CIDR (Network Layer)](#173-domande-su-indirizzi-ip-e-routing-cidr-network-layer)
- [17.4 Schemi e Appunti dalle Lavagne (Sessione QA01)](#174-schemi-e-appunti-dalle-lavagne-sessione-qa01)
