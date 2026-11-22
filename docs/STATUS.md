# Status

## P03

**Panel View → Dips** visar Active Dip och historisk frekvens för bekräftat avslutade nedgångsepisoder. Varje avslut startar om den lokala referensen. Reversal och de fyra trösklarna är valbara. Overview visar P02-måtten. [Beslutad episodmetod](METRICS.md#lokala-nedgångsepisoder-och-frekvens)

### Verifiering den 22 november 2026

- Slutkällan kompilerades i TradingView Desktop och sparades i den befintliga privata Macro Analysis-indikatorn från VS Code. På **XETR_DLY:SXR8, 1D, SEK** matchade Overview P02:s avkastning, drawdowns och SMA 200D. Ändringen berör ingen SMA-beräkning.
- Med standardtrösklar och 5 % reversal gav SXR8 42, 9, 3 och 0 avslutade episoder vid ≥5, ≥10, ≥20 respektive ≥30 % under 5 904 observerade kalenderdagar. Panelen visade `2.6/y`, `1/1.8y`, `1/5.4y` och `0`. Active Dip var −8,26 %. Tooltips visade antal, datumspann, täckning och båda frekvensmåtten vid positivt antal.
- **BINANCE:PUMPU, 1D** visade −45,73 % Active Dip och `N/A` för frekvenserna. Tooltipen för ≥5 % visade 11 avslutade episoder och 87 observerade kalenderdagar till 2026-11-21 medan dagsbaren den 22 november var öppen.
- **BINANCE:BTCUSDT, 1D** behöll −30,48 % Active Dip och samma frekvenser till 2026-11-21 när priset i den öppna dagsbaren ändrades från 60 744,99 till 60 740,01 USDT.
- **SXR8, 1W** visade **Use a 1D chart**. En dubblett bland trösklarna visade **Enter increasing dip thresholds** med Active Dip kvar. En extra rad med vynamnet placerar Active Dip under TradingViews överliggande chartknappar.
- Nio syntetiska sekvenser passerade i Pine och i en oberoende Python-beräkning med exakta rationella tal. De täckte separata och ofullständiga episoder, exakt reversal och tröskel, upprepade toppar och bottnar, återtagen topp och explicita dataluckor. Pine kontrollerade även 365/366 dagar, kort historik, noll episoder och visning i år per episod. [Syntetiska fall](METRICS.md#deterministiska-p03-exempel)

Frekvenserna beskriver laddade data. En verklig sessionsstängning där en pågående episod avslutades följdes inte.

### Nästa steg

Avgränsa P04 till varaktighet för de lokala episoderna. Mät kalenderdagar från topp till botten och från botten till bekräftat avslut, och verifiera hur lika bottnar och avbrott påverkar datumen.

## P02

Macro Analysis visar nu kalenderbaserad prisavkastning för 1Y, 3Y, 5Y och 10Y med referensdatum i tooltips. SMA har valbar längd och beräkningsintervall på en gemensam inställningsrad med kryssruta för linjen. Weekly och Monthly har valbar utjämning för både linjen och SMA-måtten. Panelen visar datum och mått på sju rader och kan placeras i valfritt hörn. [Måttdefinitioner](METRICS.md#beslutat)

### Verifiering den 22 november 2026

- Slutkällan kompilerades i TradingView Desktop efter kopiering från VS Code. Den befintliga privata Macro Analysis-instansen uppdaterades.
- **XETR_DLY:SXR8, 1D, SEK** med utdelningsjustering av. P01-värdena för 2010-09-21 till 2026-11-20 stämde vid Daily 200, inklusive 797,60 % Return, 14,54 % CAGR, −8,26 % aktuell DD, −31,66 % max-DD, 2,51 % SMA-distans och 85,28 % av 3 865 jämförbara dagar över SMA. 1Y, 3Y, 5Y och 10Y visade 13,78 %, 55,72 %, 81,33 % respektive 306,08 %. 10Y-tooltipen visade fredagen 2016-11-18 som referens för söndagens måldatum.
- En oberoende rullande summa och separata historiska räknare i Pine gav för Daily 50 SMA 8 186,43, distans −5,28 %, andel 72,48 % och 4 015 jämförbara dagar. Daily 100 gav 8 023,34, −3,35 %, 78,06 % och 3 965 dagar. Daily 200 gav 7 564,29, 2,51 %, 85,28 % och 3 865 dagar. Linjen och panelmåtten följde valda inställningar. Kryssrutan dolde linjen med panelen kvar.
- Weekly 2 respektive Monthly 2 kördes på samma SXR8-chart. Med utjämning av blev MA Distance −3,41 % respektive −5,31 % och Above MA 61,85 % respektive 69,80 %. Med **Smooth SMA** visade Weekly 2 −3,41 % och 63,50 %, och Monthly 2 −4,98 % och 73,06 %. Den omärkta kryssrutan ändrade linjens synlighet med samma panelvärden. Panelen flyttades till nedre vänster och återställdes till standardhörnet övre höger.
- **SXR8, 1W** visade **Use a 1D chart**. **BINANCE:PUMPUSDT, 1D** visade 1Y −14,12 % med referens 2025-11-21 och `N/A` för 3Y, 5Y och 10Y. Panelen låg kvar på 2026-11-21 när den öppna dagsbarens pris ändrades från 0,002555 till 0,002554 USDT den 22 november.
- En tillfällig Pine-kontroll passerade kalenderfall för helg, börshelgdag, 29 februari och sekelår, för kort historik samt ogiltig och senare giltig referensstängning. Den tillfälliga kontrollinstansen togs bort. En lokal Python-kontroll jämförde den begränsade datumuppslagningen med full historik efter att lagringsfönstret hade gått runt. [Reproducerbara exempel](METRICS.md#deterministiska-p02-exempel)

Historiken och dess eventuella luckor beror på TradingViews prisserie. En verklig övergång mellan två bekräftade vecko- eller månadsperioder följdes inte.

## P01

[Macro Analysis i Pine Script v6](../indicators/macro-analysis.pine) visar prisavkastning, CAGR, mätperiod, aktuell och maximal drawdown, distans till SMA 200D samt andel och antal jämförbara dagar. SMA-linjen kan döljas i indikatorns inställningar. P01 stöder standardgrafer på exakt 1D. [Måttdefinitioner](METRICS.md#beslutat)

### Verifiering

Indikatorn kompilerades och kördes i TradingView Desktop. På SXR8 växlade **Show SMA 200D** linjen medan panelen behöll sina värden. Observationerna avser laddad historik den 22 november 2026.

| Chart | Observerat |
| --- | --- |
| `XETR_DLY:SXR8` · 1D · SEK | 2010-09-21 till 2026-11-20, 5 904 kalenderdagar. Prisavkastning 797,60 %, CAGR 14,54 %, aktuell DD −8,26 %, max DD −31,66 %. SMA 200D 7 564,29 i datafönstret, 2,51 % över SMA och 85,28 % av 3 865 jämförbara dagar över SMA. Utdelningsjustering var av. |
| `XETR_DLY:SXR8` · 1W | Panelen visade **Use a 1D chart**. Macro Analysis visade inga mått och ingen SMA-linje. |
| `BINANCE:PUMPU` · 1D | 2026-08-26 till 2026-11-21, 87 kalenderdagar. Prisavkastning −51,80 %. Båda SMA-måtten visade `N/A` och ingen SMA-linje ritades. Dagsbaren den 22 november var öppen. |
| `BINANCE:BTCUSDT` · 1D | Panelen slutade 2026-11-21 och behöll sina värden när livepriset rörde sig från 60 355,44 till 60 302,97 USDT. Andel dagar över SMA var 52,75 % av 3 185 jämförbara dagar. |

En tillfällig Pine-testvariant matade indikatorns beräkningslogik med [syntetiska stängningar och sessionsdatum](METRICS.md#deterministiska-p01-exempel). Kontrollerna passerade för 46,41 % prisavkastning och 10,00 % CAGR, återhämtning med 0 % aktuell DD och −25 % max-DD, SMA-värdena 100, 100,05 och 100 samt en andel dagar över SMA på 1/3. Kontrollen omfattade även enstaka och sammanfallande datum, `na`, noll och negativa stängningar, 199 och 200 giltiga barer i rad, lika stängning och SMA vid decimalpriser samt en simulerad öppen bar. Ett ogiltigt senaste pris visade `N/A` för aktuella mått och lämnade de historiska värdena tillgängliga.

En verklig övergång från öppen till stängd dagsbar följdes inte. Täckningen är begränsad till den laddade prisserien. Luckor där datakällan saknar en hel bar kan påverka resultaten.

## P00 · 22 november 2026

Projektgrund med arbetsregler, produktmål, måttförslag och lokal mätlogg. [P00 på GitHub](https://github.com/block-dev-mats/Macro-Analysis/commit/38bf755704f9281827d9c34d84cc5523684f13e1)
