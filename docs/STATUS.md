# Status

## P07

**Opportunity** räknar om Quality och drawdown vid ett gemensamt bekräftat jämförelsedatum per valuta. P06 krävde identiska sessionsdatum och kunde stoppa hela rankningen vid saknad SEK-kurs i en kolumn. P07 accepterar olika faktiska referenssessioner för samma kalendermål och låter giltiga kandidater bilda en egen jämförelsegrupp. [Metod och färger](METRICS.md#opportunity)

### Verifiering den 22 november 2026

- Slutkällan kompilerades från VS Code och sparades som revision 26 i den befintliga privata indikatorn. På Avanza-flikens **SXR8 1D** visade Compare i **SEK** `ACWI ★` i grönt på det gemensamma datumet **2026-11-19**. Opportunity var 0,9 för SXR8, 1,0 för ACWI, 0,8 för EUNL, 0,9 för VWCE och 0,3 för XACTHDIV. ACWI:s värde var grönt och XACTHDIV:s rött. I **Native** färgsattes grupperna SEK och EUR var för sig. ACWI var ensam i USD, med neutral poäng, och vyn hade ingen stjärna.
- Syntetiska Pine-kontroller använde produktionsfunktionerna och förväntade poäng från en oberoende beräkning. De passerade för helgdagar, skilda referens- och slutdatum, en senare topp utanför jämförelsedatumet, saknad FX, kort och gammal historik, oavgjort, giltig ledare med övriga kandidater uteslutna samt Opportunity-färger. Övriga Compare-rader följde tidigare regler i TradingView. Overview, Dips och SMA 200D stämdes av på SXR8. 1W visade instruktionen att byta till 1D.
- Fem kolumner kördes med **496,5 ms** total tid enligt Pine Profiler. Den externa statistikförfrågan tog **382,4 ms** över **29 495** exekveringar. P07 lägger till högst fem små daterade Opportunity-resultat i den befintliga förfrågan. Antalet förfrågningar är oförändrat. [Pines resursgränser](https://www.tradingview.com/pine-script-docs/writing/limitations/)
- Verifieringen i Desktop gjordes vid stängd marknad. Fördröjningen när dessa börser stänger i realtid och vid långa sammanhängande marknadsuppehåll återstår att följa. TradingViews värddiagram kan senarelägga när en extern stängning blir synlig. Datumet i Opportunity-tooltipen anger underlaget som faktiskt användes.

## P06

Compare har **3Y** och **Opportunity**, med gemensam SEK som standard och **Native** som alternativ. 3Y- och 5Y-tooltipen visar kalenderbaserad CAGR. En stjärna vid symbolen markerar en unik högsta poäng när de kvalificerade symbolerna har jämförbara datum och valuta. [Metod och färger](METRICS.md#opportunity)

### Verifiering den 22 november 2026

- Lokal och publicerad `main` utgick från P04 (`c0d0b9d`). P05 fanns som uppdragsbeskrivning i projektchatten. Någon verifierad P05-leverans hittades inte. P06 använder P04:s verifierade dagslogik och avstår från en global stjärna vid förskjutna slut- eller referensdatum.
- Pine-fixturer med produktionsfunktionerna verifierade kalenderdagar, viktad Quality och Opportunity för hög tillväxt med liten rabatt, svag tillväxt med stor rabatt och god tillväxt med betydande rabatt. De täckte även negativa avkastningar, Max DD närmast noll, neutrala färger för svag Quality, lika poäng vid visad precision, noll rabatt, kort historik, en kvalificerad symbol, saknad valuta samt olika valuta och sessionsdatum.
- Dagsstängningarna i SEK jämfördes med direkta SEK-prisförfrågningar i TradingView för EUNL, VWCE, ACWI och XACTHDIV. På SXR8:s tidsaxel matchade 4 064, 1 865, 4 064 respektive 2 441 jämförda observationer. EUNL, VWCE och ACWI fick omräknade priser. XACTHDIV och SXR8:s redan SEK-uttryckta priser behölls.
- Slutkällan kompilerades och sparades från VS Code i den befintliga privata indikatorn i TradingView Desktop. Revision 24 körs på SXR8 1D. En tvåsymbolskörning visade en stjärna när både valuta och datum matchade och poängen skilde sig. Fem förvalda symboler i SEK visade poäng med förskjutna datum och ingen stjärna. Native behöll P04:s pris- och dipmått. Overview, Dips och SMA 200D matchade SXR8-baslinjen. 1W visade 1D-instruktionen.
- Fem symboler kördes inom Pine-gränserna. Koden har upp till fyra externa statistikförfrågningar med 21 skalära fält vardera, upp till fem skalära förfrågningar för dagsstängningar i SEK och högst en separat vecko- eller månadsförfrågan för SMA. Pine Profiler mätte **467,7 ms** totalt för slutrevisionen på SXR8 i SEK. Statistikförfrågan stod för **365,9 ms** och **29 495** exekveringar enligt profileraren. [Pines resursgränser](https://www.tradingview.com/pine-script-docs/writing/limitations/)

Minsta nästa steg är att följa en faktisk sessionsövergång på en värdgraf med blandade börskalendrar och dokumentera när symbolerna får samstämmiga slutdatum för Opportunity.

## P04

**Panel View → Compare** visar chartsymbolen och upp till fyra extra symboler. Förvalen är **ACWI**, **EUNL**, **VWCE** och **XACTHDIV**. Tabellen visar CAGR, 1Y, 5Y, Current DD, Max DD, Active Dip och historisk frekvens för avslutade nedgångar på minst 10 %. [Jämförelseregler](METRICS.md#symboljämförelse)

### Verifiering den 22 november 2026

- Slutkällan kompilerades och sparades från VS Code i den befintliga privata Macro Analysis-indikatorn i TradingView Desktop. Avanza-fliken sparades på **SXR8, 1D, SEK** med Compare valt, fyra fondförval aktiva och SMA 200D synlig.
- Overview och Dips stämdes av för SXR8, ACWI, EUNL, VWCE, XACTHDIV, BTCUSDT och PUMPU. CAGR, drawdowns, Active Dip och ≥10 %-frekvenser stämde vid samma bekräftade slutdatum och prisserie. På SXR8 behöll Overview till exempel 797,60 % Return, 14,54 % CAGR, −8,26 % Current DD, −31,66 % Max DD, 2,51 % MA Distance och 85,28 % Above MA. Dips behöll −8,26 % Active Dip och frekvenserna från P03. Fem kolumner fungerade även med utjämnad 200W SMA.
- EUNL och VWCE delade datum och EUR för 1Y och 5Y, så EUNL:s 13,34 % och 55,10 % var gröna och VWCE:s 13,17 % och 51,84 % röda. CAGR och Max DD var neutrala när historiklängderna skilde sig. Current DD, Active Dip och dipfrekvens förblev neutrala. XACTHDIV:s 1Y hade slutdatum 2026-11-19 på SXR8 trots samma visade valuta. På BTCUSDT nådde XACTHDIV 2026-11-20 och stämde mot den fristående vyn med 6,07 % CAGR och −3,21 % Active Dip. Skillnader i 1Y och 5Y mellan vyerna följer deras olika kalendermål.
- Fem symboler med både börs- och kryptokalendrar kördes. På söndagen den 22 november gav PUMPU 2026-11-21 som slutdatum på BTCUSDT, −45,73 % Active Dip och `N/A` för 1Y, 5Y och dipfrekvens, i linje med den fristående vyn. På det helgstängda SXR8 slutade samma externa serie den 20 november. Ändringar i den öppna kryptobarens pris påverkade inte måtten.
- En avstängd symbol försvann och övriga värden stod kvar. En symbol som även var chartsymbol visades en gång, inklusive EUNL med fördröjd Xetra-feed. SXR8 på 1W visade **Use a 1D chart** utan jämförelse eller SMA-linje. En lokal syntetisk referenskontroll i Python täckte fem historiker, kalendergränser, ogiltig referens, övergång till nytt måldatum, ringbuffert och färggrupper.
- Pine Profiler mätte en körning med slutkällan och fem symboler på SXR8 till **359,9 ms**. Raden för den externa begäran stod för **258,1 ms** och **29 492** exekveringar enligt profileraren. Compare använder högst fyra externa dagliga kontext plus ett valfritt SMA-kontext. Varje jämförelsebegäran skickar 16 skalära fält utan en kopia av historiken. Ingen minnesgräns observerades under körningarna. [Pines resursgränser](https://www.tradingview.com/pine-script-docs/writing/limitations/)

Minsta nästa steg är att följa en verklig sessionsövergång för Xetra, Stockholm och USA på samma värdchart och kontrollera när respektive bekräftad stängning blir tillgänglig.

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
