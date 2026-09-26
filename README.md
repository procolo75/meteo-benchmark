# Meteo Benchmark

**Sito online:** https://procolo75.github.io/meteo-benchmark/

Quale modello meteo è più affidabile nella tua città, per temperatura, vento e pioggia? Scegli una località italiana e la pagina confronta, ora per ora, le previsioni emesse **3, 2 e 1 giorno prima** dai principali modelli meteo con i dati realmente misurati nell’aeroporto più vicino o, per gli ultimi 7 giorni, in una stazione meteo regionale o MeteoNetwork. Funziona interamente nel browser, senza installazioni e senza server.

---

## Come funziona

1. Cerchi una località italiana (ricerca per nome, via geocoding Open-Meteo).
2. La pagina propone l’**aeroporto con bollettino METAR più vicino** e, in alternativa, le **stazioni meteo** entro 25 km: reti regionali ufficiali e rete amatoriale MeteoNetwork. Scarica le misure reali della stazione scelta.
3. Per ogni ora del periodo scarica il valore che ciascun modello **aveva previsto 3, 2 e 1 giorno prima** (non la previsione di oggi: l’archivio delle corse passate). Una sola richiesta per modello scarica tutte e tre le scadenze.
4. Confronta previsto vs misurato e, per ogni tipo di previsione, indica i modelli più affidabili sulle tre scadenze insieme.

Il confronto è alla pari: le previsioni sono richieste sulle **coordinate dell’aeroporto**, non del centro città, così tutti i modelli vengono valutati sullo stesso punto in cui si misura.

## Come giudica i modelli

Una sola misura: lo **scarto per l’80%**. Per ogni modello e ogni tipo di previsione è lo scarto più piccolo entro cui cade l’80% delle sue previsioni: «±1,8 °C» = nell’80% dei casi ha sbagliato al massimo di 1,8 °C, in più o in meno. Più basso è meglio. La percentuale è impostabile (50–99%).

| Tipo di previsione | Casi confrontati |
|---|---|
| Temperatura ora per ora | ogni ora |
| Temperatura massima e minima del giorno | ogni giorno |
| Vento medio ora per ora | ogni ora |
| Vento massimo del giorno | ogni giorno |
| Pioggia del giorno, oraria, a 3 ore (mm) | solo con le stazioni meteo, e solo quando è piovuto o era prevista pioggia (≥ 0,2 mm) |

Lo scarto si calcola tre volte, sulle previsioni emesse **3, 2 e 1 giorno prima**. A ogni scadenza i modelli vengono messi in fila dal più preciso (1°, 2°…); la **posizione media** sulle tre scadenze dice quale modello è più affidabile per quel tipo di previsione. A parità di posizione media vince chi ha lo scarto più basso rispetto al migliore. Un modello senza abbastanza casi a una scadenza (per la pioggia servono almeno 5) non riceve una posizione media.

**Ore della pioggia.** Come indica Open-Meteo, la pioggia oraria è la *somma dell’ora precedente*: il valore delle 11:00 è la pioggia caduta tra le 10 e le 11. Le misure sono abbinate allo stesso modo, e il totale di un giorno va dal valore delle 01:00 a quello delle 24:00. Temperatura e vento sono invece i valori a quell’ora. Tutti gli orari sono in ora italiana (le stazioni MeteoHub, in UTC, vengono convertite).

## Cosa mostra la pagina

- **Modelli più affidabili**: per ogni tipo di previsione i tre modelli con la posizione media migliore sulle previsioni a 3, 2 e 1 giorno, con la posizione media tra parentesi. Un clic su una riga apre il dettaglio.
- **Dettaglio**: per il tipo di previsione scelto, tutti i modelli con lo scarto per l’80% a 3, 2 e 1 giorno (con il numero di casi e il piazzamento a quella scadenza) e la posizione media. Il migliore di ogni colonna è in giallo; si ordina cliccando l’intestazione di una colonna.
- **Periodo selezionabile**: ultimi 7, 14 o 30 giorni (default 30).

## Modelli

Attivi di default (tutti): ECMWF IFS 0,25°, ECMWF IFS 9 km, ECMWF AIFS (IA), DWD ICON seamless, ItaliaMeteo ICON-2I, NOAA GFS seamless, NOAA AIGFS (IA), Météo-France seamless, UK Met Office seamless, GEM Canada seamless. Ognuno si può spegnere; **Tutti** e **Predefiniti** li riaccendono. Oltre l’ottavo modello i colori si ripetono con pallino vuoto.

**Cosa sono i *seamless*.** Ogni ente meteo ha più modelli: uno globale (tutta la Terra, meno dettaglio), uno regionale (per esempio l’Europa, più dettaglio) e a volte uno locale ancora più fine che prevede solo 1–2 giorni. Il *seamless* è una combinazione fatta da Open-Meteo: per ogni luogo e ogni ora usa il modello più dettagliato che copre quel punto a quella distanza di tempo, e passa al successivo quando quello si ferma. Per questo di ogni famiglia c’è solo il seamless, non i singoli componenti. A 3 giorni di anticipo, in Italia, i modelli locali non arrivano più e ogni seamless coincide con un solo componente (ICON con ICON-EU, Météo-France con ARPEGE Europa, GFS, UK Met Office e GEM con il rispettivo globale). A 1–2 giorni il seamless può invece usare anche i modelli locali dove coprono (per esempio ICON-D2 al Nord).

**Best match** (la scelta automatica di Open-Meteo per il luogo) non è in elenco: in tutta Italia dà gli stessi valori di DWD ICON seamless (verificato su 10 città, da Bolzano a Lampedusa).

ECMWF non ha un seamless: ci sono le due versioni di IFS (griglia 0,25° e 9 km) e AIFS, la versione a intelligenza artificiale. KNMI, DMI e MET Norway seamless in Italia danno gli stessi valori di ECMWF IFS 9 km e non sono in elenco.

ItaliaMeteo ICON-2I, ad alta risoluzione, non arriva a 3 giorni: è giudicato solo sulle previsioni di 2 e 1 giorno prima e la sua posizione media è calcolata su quelle due (etichetta gialla «fino a 2 gg»). A 3 giorni resta vuoto invece di usare la previsione di 2 giorni, che sarebbe più facile.

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
- Stazioni meteo: senza registrazione MeteoHub conserva solo gli ultimi 10 giorni, quindi per queste stazioni il periodo è limitato a **7 giorni**. Non ci sono stazioni ufficiali in Valle d’Aosta e Abruzzo, e il Lazio ne ha una sola (MeteoNetwork copre anche queste zone). Molte stazioni non hanno l’anemometro (nel menu sono segnate «senza vento») e alcune MeteoNetwork non misurano la pioggia: in quei casi si giudicano solo le grandezze misurate. Le stazioni MeteoNetwork sono amatoriali e la qualità dipende dall’installazione.
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
