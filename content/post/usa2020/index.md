---
title: Usa 2020, chi vincerà le elezioni? L’analisi dei tweet vede in testa Biden
subtitle: 'Un team di ricercatori Unical ha utilizzato l’intelligenza artificiale per interpretare l’orientamento di voto degli elettori attraverso gli hashtag usati. La tecnica era stata testata con successo sulle Presidenziali 2016 e sulle Politiche italiane'
disable_comments: true
markup: kramdown
authors:
- admin
tags:
- Social Media Analysis
- Opinion Mining
- User Polarization
- Neural Networks
- Sentiment Analysis
- USA2020
date: "2020-11-03T12:30:00Z"
lastmod: "2020-11-03T12:30:00Z"
featured: false
draft: false	
---

Chi sarà il prossimo presidente degli Stati Uniti? Secondo l’algoritmo messo a punto da un team di ricercatori dell’Università della Calabria per l’analisi del *sentiment* sui social media, sarà **Joe Biden** a vincere oggi le elezioni.

Il sistema utilizza le reti neurali per interpretare l’orientamento di voto degli elettori su Twitter, analizzando gli hashtag utilizzati dagli utenti. L’algoritmo è stato già testato con successo sulle Presidenziali Usa del 2016 e le Politiche italiane. In entrambi i casi ha restituito una previsione di voto molto vicina ai risultati reali e ancora più accurata rispetto ai sondaggi tradizionali e ad altre tecniche di rilevazione basate su intelligenza artificiale (maggiori dettagli [qui](/post/iom/)).

Per le Presidenziali Usa 2020 sono stati presi in esame 550.979 tweet, pubblicati da 308.262 utenti nel periodo compreso tra il 18 e il 27 ottobre.

Il risultato vede Joe Biden in vantaggio con il 53,1% dei voti, seguito da Donald Trump con il 41,7% (il restante 5,2% è diviso tra i candidati rimanenti). Allo studio hanno collaborato il professor Domenico Talia, ordinario di Sistemi di Elaborazione delle Informazioni, i ricercatori del DIMES (Dipartimento di Ingegneria Informatica, Modellistica, Elettronica e Sistemistica) Loris Belcastro, **Riccardo Cantini**, Fabrizio Marozzo e Paolo Trunfio. All’analisi dei dati ha partecipato anche Giovanni Bruno, dello spin-off dell’Unical DtoK Lab.

## La metodologia
I ricercatori hanno fornito al sistema un primo set di hashtag per la classificazione dei tweet in base all’orientamento di voto espresso. Tutti hashtag "istituzionali" e di facile interpretazione, per iniziare l’analisi:
> - ***Pro Biden***: 'democrats', 'votebiden', 'bidenharris2020', ‘americaneedspennsylvania', 'bidentownhall', 'trumptaxreturns', 'bidenriots', 'trumpisaloser', 'trumpknew', 'trumpcoupplot', 'thepresidentisacrybaby', 'trumplethinskin', 'voteblue', 'lyingtrump', 'votebidenharris', 'militaryforbiden'.
> - ***Pro Trump***: 'americafirst', 'maga', 'trump2020', 'republicans', 'kag', 'kag2020', 'moscowhunter', 'maga2020', 'makeamericagreatagain', 'crookedjoebiden', 'draintheswamp', 'teamtrump2020', 'gop', 'votered', 'fourmoreyears', 'blacksfortrump', 'trumptrain'.

Partendo da questo primo gruppo di hashtag, il sistema ne ha aggiunto altri che ha imparato a interpretare iterando il processo di analisi e riconoscendo l’associazione con le ‘parole chiave’ di partenza.

Sono stati applicati dei filtri per garantire la validità del campione e quindi l’autenticità degli account: la lingua in cui erano scritti i tweet e la localizzazione dell’utente nel Paese chiamato al voto, sulla base della georeferenziazione o delle dichiarazioni nella bio del profilo. Sono stati anche individuati e rimossi i bot. Sono stati poi presi in considerazione solo utenti con un numero di tweet tra 5 e 100, per evitare che elettori poco attivi o eccessivamente prolifici sul social falsassero il risultato finale.

## Gli stati in bilico
Grazie alla georeferenziazione dei tweet, è stato possibile formulare previsioni anche per alcuni degli Stati in bilico (*Swing States*). In particolare, fra gli Stati più critici, in cui il vantaggio di un candidato sull'altro è sottilissimo se non nullo, a Biden dovrebbe andare la vittoria in almeno uno fra Georgia, North Carolina e Ohio, cosa che ne decreterebbe l'ascesa alla Casa Bianca. 

[!(featured.png)](https://www.youtube.com/watch?v=XqDVzj0IiYs&feature=emb_logo)

<hr>
<p><span style="font-size:14.0pt;line-height:90%;font-family:
&quot;Open Sans&quot;,sans-serif">Link all'articolo originale: <a href="https://www.unical.it/portale/portaltemplates/view/view.cfm?103993" target="_blank">Portale UNICAL - Notizie</a></span></p>
<p><span style="font-size:14.0pt;line-height:90%;font-family:
&quot;Open Sans&quot;,sans-serif">Link alla pubblicazione: <a href="https://ieeexplore.ieee.org/document/9026882" target="_blank">Learning political polarization on social media using neural networks</a></span></p>