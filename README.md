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

- **Classifica dei modelli**: errore medio, minimo e massimo per temperatura e vento, indice pioggia, con il valore migliore evidenziato e un avviso automatico quando il periodo scelto è troppo breve per essere significativo.
- **Tabella giorno per giorno**: valore misurato a confronto con quello previsto da ogni modello.
- **Grafico ora per ora**, con selettore della grandezza: temperatura massima, temperatura minima, vento medio, vento massimo, pioggia.
- **Periodo selezionabile**: ultimi 7, 14 o 30 giorni (default 30).

## Modelli

Attivi di default: ECMWF IFS, ECMWF AIFS (IA), DWD ICON, ItaliaMeteo ICON-2I, NOAA GFS, Météo-France, UK Met Office, GEM Canada.

Attivabili dall’utente: NOAA AIGFS (IA), JMA Giappone, CMA Cina, MeteoSwiss ICON-CH2 (Nord Italia), DWD ICON-D2 (Nord Italia).

I modelli ad alta risoluzione che non arrivano a 3 giorni sono inclusi con il loro anticipo massimo e segnati con un’etichetta gialla:

- **ItaliaMeteo ICON-2I**: previsione di 2 giorni prima
- **DWD ICON-D2** (solo Nord Italia): previsione di 1 giorno prima

Un anticipo minore rende la previsione più facile: nel leggere la classifica va tenuto conto che questi modelli non giocano alla pari.

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
