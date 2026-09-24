# Meteo Benchmark

**Sito online:** https://procolo75.github.io/meteo-benchmark/

Quale modello meteo prevede meglio nella tua città? Scegli una località italiana e la pagina confronta, giorno per giorno, le previsioni emesse **3, 2 o 1 giorno prima** (a scelta) dai principali modelli meteo con i dati realmente misurati nell’aeroporto più vicino o, per gli ultimi 7 giorni, in una stazione meteo regionale o MeteoNetwork. Funziona interamente nel browser, senza installazioni e senza server.

---

## Come funziona

1. Cerchi una località italiana (ricerca per nome, via geocoding Open-Meteo).
2. La pagina propone l’**aeroporto con bollettino METAR più vicino** e, in alternativa, le **stazioni meteo** entro 25 km: reti regionali ufficiali e rete amatoriale MeteoNetwork. Scarica le misure reali della stazione scelta.
3. Per ogni ora del periodo scarica il valore che ciascun modello **aveva previsto 3, 2 e 1 giorno prima** (non la previsione di oggi: l’archivio delle corse passate). Tre schede sopra la classifica a punti permettono di passare dall’una all’altra senza nuovi download, per vedere quanto i modelli migliorano avvicinandosi al giorno.
4. Confronta previsto vs misurato e stila tre classifiche — temperatura, vento, pioggia — riunite in un’unica tabella ordinata.

Il confronto è alla pari: le previsioni sono richieste sulle **coordinate dell’aeroporto**, non del centro città, così tutti i modelli vengono valutati sullo stesso punto in cui si misura.

## Cosa confronta

| Grandezza | Come si misura l’errore |
|---|---|
| Temperatura | Errore medio (°C), più errore minimo e massimo con il segno |
| Vento | Errore medio (km/h), più errore minimo e massimo con il segno |
| Pioggia | Indice sui giorni: presi ÷ (presi + falsi allarmi + mancati) |

L’errore è calcolato come **previsto − misurato**, quindi minimo e massimo sono riportati **con il segno, non in valore assoluto**:

- il **massimo** è il caso peggiore in eccesso (`+6,0 °C` = una volta ha previsto 6 gradi più del reale);
- il **minimo** è il caso peggiore in difetto (`−4,5 °C` = 4 gradi e mezzo in meno).

Un modello che sottostima sempre avrà anche il massimo negativo. I due estremi mostrano quanto può sbagliare nel singolo caso, che la sola media nasconde.

I modelli sono **ordinati** per media dei piazzamenti nelle tre classifiche, e in ogni colonna il valore migliore è evidenziato. La pagina non proclama un vincitore: il confronto resta aperto alla lettura.

**Esempio di indice pioggia:** in 30 giorni piove 4 volte; il modello prevede pioggia 5 volte e 3 sono giuste. Presi 3, falsi allarmi 2, mancati 1 → 3 ÷ (3+2+1) = **0,50**. Un modello che non prevede mai pioggia fa 0. Se nel periodo non piove mai e il modello non prevede mai pioggia, l’indice vale 1 (non ha sbagliato niente).

**Ore della pioggia.** Come indica Open-Meteo, la pioggia oraria è la *somma dell’ora precedente*: il valore delle 11:00 è la pioggia caduta tra le 10 e le 11. Le misure sono abbinate allo stesso modo, e il totale di un giorno va dal valore delle 01:00 a quello delle 24:00. Temperatura e vento sono invece i valori a quell’ora. Tutti gli orari sono in ora italiana (le stazioni MeteoHub, in UTC, vengono convertite).

## Cosa mostra la pagina

- **Classifica a punti**: ogni colonna è una piccola gara. Temperatura e vento medio: 1 punto per ogni ora in cui la previsione è entro la soglia dal misurato; vento massimo: 1 punto per ogni giorno. Le **soglie sono impostabili** sulla pagina (predefinite ±1 °C, ±5 km/h, ±10 km/h, ±1 mm per la pioggia) e il browser le ricorda. «x su y» = x punti su y ore (o giorni) confrontate. Per la pioggia: indice di pioggia giornaliera, più **pioggia oraria** e **a 3 ore** (blocchi 00–03, 03–06…), dove contano solo le ore piovute o previste piovose e la posizione si basa sulla percentuale; la pagina spiega il calcolo con esempi. I modelli sono ordinati per media dei piazzamenti nelle colonne disponibili.
- **Classifica per errore**: errore medio, minimo e massimo per temperatura e vento, indice pioggia, con il valore migliore evidenziato in giallo e un avviso automatico quando il periodo scelto è troppo breve per essere significativo.
- In entrambe le classifiche basta **cliccare l’intestazione di una colonna** per ordinare la tabella in base a quella; un secondo clic inverte l’ordine, un clic su # torna all’ordine della classifica.
- **Giorno per giorno**, a corsie numeriche: una riga per modello con il valore di ogni giorno stampato nel colore del modello, sotto la riga del misurato. Si può vedere il valore previsto o l’errore (previsto − misurato; per la pioggia ✓ presa, FA falso allarme, M mancata). Accanto al nome, l’errore medio o l’indice pioggia del periodo.
- **Periodo selezionabile**: ultimi 7, 14 o 30 giorni (default 30).

## Modelli

Attivi di default (tutti): ECMWF IFS 0,25°, ECMWF IFS 9 km, ECMWF AIFS (IA), DWD ICON seamless, ItaliaMeteo ICON-2I, NOAA GFS seamless, NOAA AIGFS (IA), Météo-France seamless, UK Met Office seamless, GEM Canada seamless. Ognuno si può spegnere; **Tutti** e **Predefiniti** li riaccendono. Oltre l’ottavo modello i colori si ripetono con linea tratteggiata.

**Cosa sono i *seamless*.** Ogni ente meteo ha più modelli: uno globale (tutta la Terra, meno dettaglio), uno regionale (per esempio l’Europa, più dettaglio) e a volte uno locale ancora più fine che prevede solo 1–2 giorni. Il *seamless* è una combinazione fatta da Open-Meteo: per ogni luogo e ogni ora usa il modello più dettagliato che copre quel punto a quella distanza di tempo, e passa al successivo quando quello si ferma. Per questo di ogni famiglia c’è solo il seamless, non i singoli componenti. A 3 giorni di anticipo, in Italia, i modelli locali non arrivano più e ogni seamless coincide con un solo componente (ICON con ICON-EU, Météo-France con ARPEGE Europa, GFS, UK Met Office e GEM con il rispettivo globale). A 1–2 giorni il seamless può invece usare anche i modelli locali dove coprono (per esempio ICON-D2 al Nord).

**Best match** (la scelta automatica di Open-Meteo per il luogo) non è in elenco: in tutta Italia dà gli stessi valori di DWD ICON seamless (verificato su 10 città, da Bolzano a Lampedusa).

ECMWF non ha un seamless: ci sono le due versioni di IFS (griglia 0,25° e 9 km) e AIFS, la versione a intelligenza artificiale. KNMI, DMI e MET Norway seamless in Italia danno gli stessi valori di ECMWF IFS 9 km e non sono in elenco.

ItaliaMeteo ICON-2I, ad alta risoluzione, non arriva a 3 giorni: nella scheda «3 giorni prima» si usa la sua previsione di 2 giorni prima ed è segnato con un’etichetta gialla (un anticipo minore rende la previsione più facile, quindi lì non gioca alla pari). Nelle schede a 2 e 1 giorno è confrontato alla pari con gli altri.

Se un modello non copre la località scelta, viene escluso dal confronto e indicato nella barra di stato.

## Fonti dei dati

- **Previsioni:** [Open-Meteo – Previous Runs API](https://open-meteo.com/en/docs/previous-runs-api), l’archivio delle corse passate dei modelli (dal 2024).
- **Misure (aeroporti):** bollettini METAR degli aeroporti italiani (Aeronautica Militare / ENAV), dall’archivio dell’[Iowa Environmental Mesonet](https://mesonet.agron.iastate.edu/request/download.phtml?network=IT__ASOS).
- **Misure (stazioni meteo):** reti regionali ufficiali (ARPA, Protezione Civile, Meteotrentino, SIR Toscana…) e rete amatoriale [MeteoNetwork](https://www.meteonetwork.it/), tramite [MeteoHub – Agenzia ItaliaMeteo](https://meteohub.agenziaitaliameteo.it/), licenza CC-BY 4.0. Temperatura e vento ogni 10 minuti (MeteoNetwork di solito ogni ora), pioggia in millimetri. Le stazioni MeteoNetwork, di cui MeteoHub dà solo il codice, sono indicate con la località ricavata dalle coordinate tramite [OpenStreetMap Nominatim](https://nominatim.openstreetmap.org/).
- **Ricerca località:** [Open-Meteo Geocoding API](https://open-meteo.com/en/docs/geocoding-api).

Nessuna chiave API, nessuna registrazione: tutte le richieste partono dal browser.

## Limiti

- I bollettini degli aeroporti italiani dicono **se** piove, non **quanto**: la pioggia si verifica solo come sì/no.
- La temperatura dei METAR è arrotondata al grado intero.
- Stazioni meteo: senza registrazione MeteoHub conserva solo gli ultimi 10 giorni, quindi per queste stazioni il periodo è limitato a **7 giorni**. Non ci sono stazioni ufficiali in Valle d’Aosta e Abruzzo, e il Lazio ne ha una sola (MeteoNetwork copre anche queste zone). Molte stazioni non hanno l’anemometro (nel menu sono segnate «senza vento») e alcune MeteoNetwork non misurano la pioggia: in quei casi la classifica usa solo le grandezze misurate. Le stazioni MeteoNetwork sono amatoriali e la qualità dipende dall’installazione.
- Con pochi giorni (7) o pochi giorni di pioggia il risultato è poco stabile: meglio usare 30 giorni.
- La località viene confrontata tramite la stazione scelta (di default l’aeroporto più vicino), che in zone montuose o molto estese può avere un clima diverso dal centro città.

## Uso in locale

Basta aprire `index.html` con un browser (serve la connessione internet per scaricare i dati):

```bash
open index.html          # macOS
```

Non ci sono dipendenze da installare né build da eseguire, e nessuna libreria esterna.

## Struttura del progetto

```
meteo-benchmark/
├── index.html      # L’applicazione (HTML + CSS + JavaScript in un unico file)
├── README.md
└── CHANGELOG.md
```

## Pubblicazione

Il sito è pubblicato con **GitHub Pages** dal ramo `main`, cartella root. Ogni push su `main` aggiorna automaticamente https://procolo75.github.io/meteo-benchmark/.
