# Changelog

## v1.3.0 — 24/09/2026
- Nuova **Classifica a punti**, sotto la classifica principale (che resta invariata): 1 punto per ogni ora con temperatura prevista entro ±1 °C dal misurato, 1 punto per ogni ora con vento entro ±10 km/h; per la pioggia l’indice. Posizione in ciascuna delle tre classifiche e ordine per media dei piazzamenti.

## v1.2.0 — 24/09/2026
- Tolto il limite di 8 modelli: ora si possono selezionare tutti, anche con i nuovi pulsanti **Tutti** e **Predefiniti**. Oltre l’ottavo, i colori si ripetono con linea tratteggiata e poi puntinata.
- Aggiunti **Open-Meteo Best match** (attivo di default), ECMWF IFS 9 km, DWD ICON globale, Météo-France ARPEGE globale.
- MeteoSwiss ICON-CH2 sostituito da MeteoSwiss ICON seamless; le etichette indicano ora quali modelli sono *seamless*.
- KNMI, DMI e MET Norway seamless non inclusi: in Italia, a 3 giorni, coincidono con ECMWF IFS 9 km.
- La tabella «Giorno per giorno» a sfondo colorato è sostituita da un grafico a corsie numeriche (come i Weather Charts di dradis): una riga per modello, i valori del giorno nel colore del modello, zeri in grigio. Interruttore **Previsto / Errore**; nomi e riepilogo del periodo restano fermi mentre i giorni scorrono.

## v1.1.0 — 24/09/2026
- Rimosso il riquadro del vincitore: la pagina non proclama più un modello migliore, restano la classifica ordinata e l’evidenziazione del valore migliore in ogni colonna.
- Rimosse le colonne «Temperatura tendenza» e «Vento tendenza».
- Aggiunte le colonne **errore minimo** ed **errore massimo** per temperatura e vento, riportate con il segno (previsto − misurato) e non in valore assoluto, per mostrare i casi peggiori nelle due direzioni.
- L’avviso sui periodi troppo brevi (meno di 14 giorni) resta, ora riferito alla classifica.

## v1.0.0 — 24/09/2026
- Prima versione: confronto delle previsioni emesse 3 giorni prima con i METAR dell’aeroporto più vicino.
- Temperatura e vento: errore medio e tendenza. Pioggia: indice sui giorni (presi, falsi allarmi, mancati).
- Riquadro del vincitore, tabella giorno per giorno, grafico ora per ora.
- Modelli a corto raggio (ICON-2I a 2 giorni, ICON-D2 a 1 giorno) inclusi con etichetta.
