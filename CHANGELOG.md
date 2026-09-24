# Changelog

## v1.9.0 — 24/09/2026
- Classifica a punti: tutte le soglie sono **impostabili** sulla pagina (temperatura, vento medio, vento massimo, oltre alla pioggia), con un pulsante per tornare ai valori predefiniti; il browser le ricorda e la classifica si ricalcola subito.
- Spiegazione estesa, con esempi, della pioggia oraria e a 3 ore e del significato di «x su y».
- Nelle due classifiche si ordina la tabella **cliccando sull’intestazione** di una colonna (il migliore prima; di nuovo per invertire; su # si torna all’ordine della classifica).
- I modelli ora sono scaricati fino alla mezzanotte che chiude l’ultimo giorno: conta anche l’ora 24:00 (per esempio 710 ore su 30 giorni invece di 709).

## v1.8.0 — 24/09/2026
- Tolto il grafico a linee «Andamento ora per ora» (e la libreria Chart.js): la pagina non ha più dipendenze esterne.
- Classifica per errore: il valore migliore di ogni colonna è evidenziato in giallo, come nella classifica a punti.
- Stazioni MeteoNetwork indicate con la località (es. «MeteoNetwork · Vomero, Napoli (cmp080)»), ricavata dalle coordinate con OpenStreetMap.
- Corretto il totale giornaliero della pioggia prevista: il valore orario è la pioggia dell’ora precedente, quindi il giorno va dal valore delle 01:00 a quello delle 24:00 (prima dalle 00:00 alle 23:00, cioè spostato di un’ora). Stessa regola per i millimetri misurati dalle stazioni.
- Verificato l’allineamento degli orari: aeroporti, stazioni MeteoHub (convertite da UTC) e modelli sono tutti in ora italiana.

## v1.7.0 — 24/09/2026
- Classifica a punti: nuove colonne **Pioggia oraria** e **Pioggia a 3 ore**. Contano solo le ore (o i blocchi 00–03, 03–06…) in cui è piovuto o il modello prevedeva almeno 0,2 mm; 1 punto quando ha previsto pioggia ed è piovuto davvero. Con le stazioni meteo serve anche che la quantità prevista sia entro una **tolleranza in mm impostabile** sulla pagina (predefinita 1 mm, ricordata dal browser); per gli aeroporti conta solo sì/no.
- La posizione in queste due colonne si basa sulla percentuale di punti sulle ore piovute o previste, così chi prevede sempre pioggia non viene premiato. Passando sopra i numeri si vedono falsi allarmi, ore mancate e prese fuori tolleranza.
- L’ordine generale è la media dei piazzamenti in tutte le colonne disponibili.

## v1.6.0 — 24/09/2026
- Oltre agli aeroporti, si possono scegliere le **stazioni meteo** entro 25 km dalla località: reti regionali ufficiali (ARPA, Protezione Civile, Meteotrentino, SIR Toscana…) e rete amatoriale MeteoNetwork, tramite MeteoHub – Agenzia ItaliaMeteo (CC-BY 4.0). Il menu le divide in gruppi e segna quelle «senza vento».
- Per queste stazioni il periodo è limitato agli ultimi **7 giorni** (senza registrazione MeteoHub conserva 10 giorni). Di default resta proposto l’aeroporto più vicino.
- Con le stazioni meteo la pioggia si misura in **millimetri** (giorno piovoso se ≥ 0,2 mm) e la tabella giorno per giorno mostra i mm misurati.
- Se la stazione non misura il vento o la pioggia, le classifiche usano solo le grandezze disponibili invece di lasciare tutti senza posizione.
- Valutate e scartate: LineaMeteo, Rete Meteo Amatori (nessuna API), Weather Underground (chiave solo per chi possiede una stazione), Meteostat (dati fermi a novembre 2025).

## v1.5.1 — 24/09/2026
- Tolto **Open-Meteo Best match**: in tutta Italia dà gli stessi valori di DWD ICON seamless (verificato su 10 città), quindi era solo un doppione. Restano 10 modelli.

## v1.5.0 — 24/09/2026
- Modelli ridotti a Best match, un *seamless* per famiglia e i modelli IA, più ECMWF IFS (0,25° e 9 km, ECMWF non ha un seamless) e ItaliaMeteo ICON-2I: 11 in tutto, tutti attivi di default.
- Tolti i componenti globali ed europei (ICON globale ed Europa, GFS globale, ARPEGE globale ed Europa, UK Met Office globale, GEM globale): a 3 giorni in Italia ogni seamless coincide già con uno di loro.
- README: spiegato cosa sono i modelli seamless.

## v1.4.0 — 24/09/2026
- La **Classifica a punti** è ora la prima tabella, con città, stazione e periodo; la classifica principale diventa «Classifica per errore» e segue.
- Tolti JMA Giappone, CMA Cina, MeteoSwiss ICON seamless e DWD ICON-D2.
- Per ogni famiglia, accanto al seamless ci sono ora il globale e l’europeo (dove esistono): aggiunti DWD ICON Europa, NOAA GFS globale, Météo-France ARPEGE Europa, UK Met Office globale, GEM Canada globale. A 3 giorni in Italia i seamless coincidono con uno di questi e risultano a pari merito.

## v1.3.2 — 24/09/2026
- Classifica a punti: il migliore di ogni voce è evidenziato con lo sfondo giallo invece che in grassetto, per leggerlo più facilmente.

## v1.3.1 — 24/09/2026
- Classifica a punti: il vento si divide in **vento medio** (ora per ora, soglia abbassata da 10 a 5 km/h, perché con 10 quasi tutti i modelli prendevano oltre il 90% dei punti) e **vento massimo** (giorno per giorno, 1 punto se il massimo del giorno è entro 10 km/h dal misurato). L’ordine è ora la media di quattro piazzamenti.

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
