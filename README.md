# Meteo Benchmark

**Sito online:** https://procolo75.github.io/meteo-benchmark/

Quale modello meteo prevede meglio nella tua città? Scegli una località italiana e la pagina confronta, giorno per giorno, le previsioni emesse **3 giorni prima** dai principali modelli meteo con i dati realmente misurati nell’aeroporto più vicino. Funziona interamente nel browser, senza installazioni e senza server.

---

## Come funziona

1. Cerchi una località italiana (ricerca per nome, via geocoding Open-Meteo).
2. La pagina individua l’**aeroporto con bollettino METAR più vicino** e ne scarica le misure reali.
3. Per ogni ora del periodo scarica il valore che ciascun modello **aveva previsto 3 giorni prima** (non la previsione di oggi: l’archivio delle corse passate).
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

## Cosa mostra la pagina

- **Classifica a punti**: ora per ora il modello prende 1 punto se la temperatura prevista è entro ±1 °C da quella misurata e 1 punto se il vento medio è entro ±5 km/h; giorno per giorno, 1 punto se il vento massimo del giorno è entro ±10 km/h; per la pioggia resta l’indice. Per ognuna delle quattro voci c’è la posizione, e i modelli sono ordinati per media dei piazzamenti.
- **Classifica per errore**: errore medio, minimo e massimo per temperatura e vento, indice pioggia, con il valore migliore evidenziato e un avviso automatico quando il periodo scelto è troppo breve per essere significativo.
- **Giorno per giorno**, a corsie numeriche: una riga per modello con il valore di ogni giorno stampato nel colore del modello, sotto la riga del misurato. Si può vedere il valore previsto o l’errore (previsto − misurato; per la pioggia ✓ presa, FA falso allarme, M mancata). Accanto al nome, l’errore medio o l’indice pioggia del periodo.
- **Grafico ora per ora**, con selettore della grandezza: temperatura massima, temperatura minima, vento medio, vento massimo, pioggia.
- **Periodo selezionabile**: ultimi 7, 14 o 30 giorni (default 30).

## Modelli

Attivi di default (tutti): ECMWF IFS 0,25°, ECMWF IFS 9 km, ECMWF AIFS (IA), DWD ICON seamless, ItaliaMeteo ICON-2I, NOAA GFS seamless, NOAA AIGFS (IA), Météo-France seamless, UK Met Office seamless, GEM Canada seamless. Ognuno si può spegnere; **Tutti** e **Predefiniti** li riaccendono. Oltre l’ottavo modello i colori si ripetono con linea tratteggiata.

**Cosa sono i *seamless*.** Ogni ente meteo ha più modelli: uno globale (tutta la Terra, meno dettaglio), uno regionale (per esempio l’Europa, più dettaglio) e a volte uno locale ancora più fine che prevede solo 1–2 giorni. Il *seamless* è una combinazione fatta da Open-Meteo: per ogni luogo e ogni ora usa il modello più dettagliato che copre quel punto a quella distanza di tempo, e passa al successivo quando quello si ferma. Per questo di ogni famiglia c’è solo il seamless, non i singoli componenti. A 3 giorni di anticipo, in Italia, i modelli locali non arrivano più e ogni seamless coincide con un solo componente (ICON con ICON-EU, Météo-France con ARPEGE Europa, GFS, UK Met Office e GEM con il rispettivo globale).

**Best match** (la scelta automatica di Open-Meteo per il luogo) non è in elenco: in tutta Italia dà gli stessi valori di DWD ICON seamless (verificato su 10 città, da Bolzano a Lampedusa).

ECMWF non ha un seamless: ci sono le due versioni di IFS (griglia 0,25° e 9 km) e AIFS, la versione a intelligenza artificiale. KNMI, DMI e MET Norway seamless in Italia danno gli stessi valori di ECMWF IFS 9 km e non sono in elenco.

ItaliaMeteo ICON-2I, ad alta risoluzione, non arriva a 3 giorni: si usa la previsione di 2 giorni prima ed è segnato con un’etichetta gialla. Un anticipo minore rende la previsione più facile: nel leggere la classifica va tenuto conto che non gioca alla pari.

Se un modello non copre la località scelta, viene escluso dal confronto e indicato nella barra di stato.

## Fonti dei dati

- **Previsioni:** [Open-Meteo – Previous Runs API](https://open-meteo.com/en/docs/previous-runs-api), l’archivio delle corse passate dei modelli (dal 2024).
- **Misure:** bollettini METAR degli aeroporti italiani (Aeronautica Militare / ENAV), dall’archivio dell’[Iowa Environmental Mesonet](https://mesonet.agron.iastate.edu/request/download.phtml?network=IT__ASOS).
- **Ricerca località:** [Open-Meteo Geocoding API](https://open-meteo.com/en/docs/geocoding-api).

Nessuna chiave API, nessuna registrazione: tutte le richieste partono dal browser.

## Limiti

- I bollettini degli aeroporti italiani dicono **se** piove, non **quanto**: la pioggia si verifica solo come sì/no.
- La temperatura dei METAR è arrotondata al grado intero.
- Con pochi giorni (7) o pochi giorni di pioggia il risultato è poco stabile: meglio usare 30 giorni.
- La località viene confrontata tramite l’aeroporto più vicino, che in zone montuose o molto estese può avere un clima diverso dal centro città.

## Uso in locale

Basta aprire `index.html` con un browser (serve la connessione internet per scaricare i dati):

```bash
open index.html          # macOS
```

Non ci sono dipendenze da installare né build da eseguire. L’unica libreria esterna è **Chart.js 4.4.1**, caricata da CDN per il grafico.

## Struttura del progetto

```
meteo-benchmark/
├── index.html      # L’applicazione (HTML + CSS + JavaScript in un unico file)
├── README.md
└── CHANGELOG.md
```

## Pubblicazione

Il sito è pubblicato con **GitHub Pages** dal ramo `main`, cartella root. Ogni push su `main` aggiorna automaticamente https://procolo75.github.io/meteo-benchmark/.
