# Meteo Benchmark

**Sito online:** https://procolo75.github.io/meteo-benchmark/

Quale modello meteo prevede meglio nella tua città? Scegli una località italiana e la pagina confronta, giorno per giorno, le previsioni emesse **3 giorni prima** dai principali modelli meteo con i dati realmente misurati nell’aeroporto più vicino. Funziona interamente nel browser, senza installazioni.

---

## Cosa confronta

| Grandezza | Come si misura l’errore |
|---|---|
| Temperatura | Errore medio (°C) e tendenza (se il modello prevede in media troppo caldo o troppo freddo) |
| Vento | Errore medio (km/h) e tendenza |
| Pioggia | Indice sui giorni: presi ÷ (presi + falsi allarmi + mancati) |

Il **vincitore** è il modello con la media dei piazzamenti migliore nelle tre classifiche.

La pagina mostra anche una tabella **giorno per giorno** (misurato vs previsto da ogni modello) e un **grafico ora per ora**.

## Modelli

ECMWF IFS, ECMWF AIFS (IA), DWD ICON, NOAA GFS, Météo-France, UK Met Office, GEM Canada, NOAA AIGFS (IA), JMA, CMA, MeteoSwiss ICON-CH2.

I modelli ad alta risoluzione che non arrivano a 3 giorni sono inclusi con il loro anticipo massimo e segnati con un’etichetta gialla:
- **ItaliaMeteo ICON-2I**: previsione di 2 giorni prima
- **DWD ICON-D2** (solo Nord Italia): previsione di 1 giorno prima

## Fonti dei dati

- **Previsioni:** [Open-Meteo – Previous Runs API](https://open-meteo.com/en/docs/previous-runs-api), l’archivio delle corse passate dei modelli (dal 2024).
- **Misure:** bollettini METAR degli aeroporti italiani (Aeronautica Militare / ENAV), dall’archivio dell’[Iowa Environmental Mesonet](https://mesonet.agron.iastate.edu/request/download.phtml?network=IT__ASOS).

Le previsioni vengono calcolate sulle coordinate dell’aeroporto, non del centro città, così il confronto è alla pari.

## Limiti

- I bollettini degli aeroporti italiani dicono **se** piove, non **quanto**: la pioggia si verifica solo come sì/no.
- La temperatura dei METAR è arrotondata al grado intero.
- Con pochi giorni (7) o pochi giorni di pioggia il risultato è poco stabile: meglio usare 30 giorni.

## Uso in locale

Basta aprire `index.html` con un browser (serve la connessione internet per scaricare i dati).

## Struttura del progetto

```
meteo-benchmark/
├── index.html      # L’applicazione (HTML + CSS + JavaScript in un unico file)
├── README.md
└── CHANGELOG.md
```
