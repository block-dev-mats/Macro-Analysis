# Status

## Färger för Current DD

- TradingView Desktop kompilerade slutkällan som **revision 49**, med tre tidigare `CW10003`-varningar. På BTCUSDT 1D den 26 november 2026 visade Compare i SEK/Wicks grönt för BTCUSDT:s preliminära **−50,07 %** och rött för XACTHDIV:s bekräftade **−2,93 %**. VWCE:s bekräftade **−6,52 %** samma dag var neutralt mellan yttervärdena. ACWI:s värde var från den 25 november och var neutralt. BTCUSDT var också grönt i SEK/Close. I Native var BTCUSDT ensam i USDT och neutral. I EUR färgades VWCE **−6,36 %** grönt och EUNL **−5,35 %** rött på samma bekräftade sessionsdag.
- Ett separat kontrollerat Pine-fall på den öppna BTC-dagsbaren visade att grönt flyttade från bekräftade **−10,00 %** till det preliminära värdet när det växlade från **−9,98 %** till **−10,02 %**. Lokala referensfall och Pine-kontroller täckte även lika visad precision, färskhet, väntande och saknade kurser samt Quality. Färgväxlingen framkallades med syntetiska värden. [Metod](METRICS.md#symboljämförelse)

## Drawdowns, rörelseben och SEK för BTCUSDT

- TradingView Desktop kompilerade källan från VS Code och sparade **revision 47** i den befintliga privata indikatorn. Tre tidigare `CW10003`-varningar kvarstår för `maForDailyClose` (550:9), `ta.sma` (556:25) och `remoteComparison` (1270:14). Femkolumnsvyn körde på BTCUSDT och SXR8 i SEK och Native. På SXR8 1W visades intervallinstruktionen.
- **Close/Wicks** styr ATH-drawdown, dippar, Dip Rarity och drawdownledet i Opportunity. Quality, avkastning och SMA använder stängningskurser. **Max DD** visar största ATH-drawdown, medan **Max Dip** visar djupaste avslutade strukturella nedben. Tooltips anger exakta datum och priser. [Metoddefinitioner](METRICS.md)
- **Swing scale** använder två gånger medianen av det logaritmiska relativa prisspannet från 52 tidigare avslutade veckor som standard. Graf och tabell använder samma regel. I BTCUSDT Native/Wicks gick nedbenet 21 september till 21 november från 87 395,67 till 55 130 USDT (−36,92 %) och bekräftades 23 november vid high 64 603,12. De exakta priserna stämdes av mot dagsseriens OHLC. Det följande uppbenet visades som pågående. **Chart lines** växlar mellan Swing legs, Dip episodes och Off. Dip Rarity har eget grafreglage.
- På BTCUSDT 1D visade intervallet november 2023 till maj 2025 flera automatiska äldre ben, bland annat −21,3 % i början av 2024 och −30,1 % i augusti 2024. Opportunity **14,46**, dipfrekvens **3,3/y** och Dip Rarity **70,7 %** låg kvar när intervallet flyttades. På SXR8 Native/Wicks visade samma skala bland annat **+33,2 %** från 480,14 EUR den 22 april 2025 till 639,36 den 3 november, bekräftat den 18 november. På BTC syntes både −36,9 % och streckat +17,2 % med enbart signerade procentsatser.
- Med **Dip episodes** syntes de kvalificerade nedbenen. Den prickade referensen **Dip Rarity 70,7 %** matchade tabellraden för BTCUSDT Native/Wicks. Tooltipen visade 535 av 1 827 lika djupa eller djupare dagsobservationer från 2021-11-25 till 2026-11-25. Referensen gick från **126 199,63 USDT den 6 oktober 2025** till **57 300,38 USDT den 25 november 2026**, motsvarande −54,60 %.
- Oberoende Decimal-kontroll av bekräftad historik t.o.m. **2026-11-25** gav ändringarna nedan jämfört med den tidigare 5 %-reversalmetoden. På BTCUSDT Native/Wicks visade TradingView 3,3/y och Max Dip −63,98 %. På SXR8 SEK/Wicks gav tooltipen 17 strukturella dippar ≥10 %. Prefixjämförelser kontrollerade att senare data inte ändrar färdiga vändningar.

| Prisbas | Avslutade ≥10 % före → efter | Max Dip | Max DD |
| --- | ---: | ---: | ---: |
| SXR8 SEK Close | 9 → 8 | −28,14 % | −31,66 % |
| SXR8 SEK Wicks | 18 → 17 | −23,94 % | −31,75 % |
| BTCUSDT Native Close | 98 → 29 | −60,01 % | −83,19 % |
| BTCUSDT Native Wicks | 190 → 31 | −63,98 % | −84,06 % |

- SXR8 i SEK vid cutoff 2026-11-25 stämdes av mot export. Close gav Current DD −8,43 %, Dip Rarity 86,3 % (175/1 275) och Opportunity 1,35. Wicks gav −9,12 %, 85,3 % (187/1 275) och 1,47. Wick-referensen gick från 8 485,62 SEK den 7 oktober till 7 711,55 den 25 november.
- För BTCUSDT saknade TradingViews ordinarie SEK-omräkning **1 357** bekräftade observationer för både stängning och H/L, från 2017-08-17 till 2021-05-04. Med Kraken USDT/USD gånger FX_IDC USD/SEK visade tabellen täckning från 2017-08-17. BTC fick stjärnan på cutoff **2026-11-25** med **10,94 i Close och 13,22 i Wicks**, Quality 12,08 % och DD −47,51 % respektive −52,25 %. I revision 47 gav Wicks **13,22 / 1,34 / 1,22 / 1,38 / 0,32** för BTCUSDT, ACWI, EUNL, VWCE och XACTHDIV. Som extrasymbol på SXR8 gav BTC samma poäng och hade 28 respektive 29 avslutade dippar ≥10 % i SEK. I Native hade BTC 14,46 i Wicks och stod ensam i USDT, medan VWCE hade stjärnan i EUR-gruppen.
- Bekräftad BTC-kurs för 25 november var **617 172,94 SEK**. Native-exportens 60 458,01 USDT multiplicerat med observerade FX-benen 0,998610 och 10,222500 gav samma värde. På öppen dagsbar visade Price cirka 619 583 SEK med kurserna 0,998700 och 10,222250. Äldre Wick-ankare för Max DD gav implicita faktorer 8,54470 SEK/USDT den 17 december 2017 och 8,96415 den 15 december 2018, rimliga jämfört med Fed:s separata USD/SEK-mittdagsnoteringar. De historiska komponenternas exakta värden kontrollerades inte mot fullständiga oberoende FX-exporter. [Fed DEXSDUS](https://fred.stlouisfed.org/data/DEXSDUS)
- **BTCUSDC** fick SEK-täckning från **2018-12-15**, innan Kraken började handla USDC/USD i januari 2020. På den öppna baren användes observerad USDC/USD **0,999800** tillsammans med USD/SEK **10,222250**. I revision 47 fick BTCUSDT och BTCUSDC båda grön ticker och stjärna i femsymbolstestet i SEK/Wicks med **13,22** vid cutoff 2026-11-25. På Native bildar USDT, USDC, EUR och USD skilda grupper. Syntetiska testfall täckte delad ledning, ensam kandidat, separata rangordningsbara valutor och ogiltigt datum. Valutatesterna täckte mätt kurs före reserv, utebliven USD/SEK, åldersgränser, framtida kurser och en gemensam faktor för hela dagens OHLC. [Kraken USDC/USD](https://blog.kraken.com/news/usd-coin-usdc-listed-on-kraken)
- **SPYI** hade bekräftad TradingView-historik från 2022-08-30 till 2026-11-25. I SEK visades 1Y **+1,65 %**, 3Y **+2,03 %**, MA Distance **+1,14 %** och Max DD **−28,47 %**. 5Y, Opportunity, Dip Rarity och femårspercentilen visade **Missing** i dämpad neutral färg. Native visade MA Distance på SPYI:s eget datum med 865 tidigare MA-sessioner även när USD-gruppen saknade Opportunity-datum. [SPYI från fondbolaget](https://neosfunds.com/spyi/)
- **Price**, Current DD och Overview-avståndet till senast bekräftad SMA kan uppdateras medan dagsbaren är öppen. Max DD och Active Dip får `~` vid en preliminär djupare nedgång. På BTCUSDT Native följde Price grafen från 60 512,20 till 60 518,72 USDT mellan två avläsningar åtta sekunder isär. Wicks Current DD stannade kring −52,52 % med dagens low 59 915. BTC-sessionens faktiska stängning och Pine Profiler mättes inte.
- **Show Extreme Entry Markers** använder P10:s inträdeshändelser. **Color Extreme Candles** färgar högst två bekräftade dagar i följd per svans. Oberoende femårskontroll t.o.m. 2026-11-20 gav 26 röda och 15 gröna bars för SXR8 50D, 26/10 för SXR8 200D, 12/14 för BTCUSDT 50D och 0/6 för BTCUSDT 200D. De ursprungliga inträdesdatumen matchade P10 i alla fyra fallen.

## P12

**Compare** visar **MA Distance** och **MA Percentile** vid Opportunity-datumet för respektive valutagrupp. SMA, historikperiod och extremgränser följer befintliga inställningar. Rött och grönt visar svansar i den egna historiken. [Metod och datakrav](METRICS.md#ma-stretch-in-compare)

### Verifiering den 23 november 2026

- TradingView Desktop kompilerade slutkällan från VS Code och sparade **revision 35** i den befintliga indikatorn. Avanza sparades på SXR8 1D med Compare i SEK, 200D, femårsperiod och P95/P5. ACWI behöll stjärnan. Opportunity-raden visade **0,9 / 1,0 / 0,8 / 0,9 / 0,3** och Dip Rarity **61,7 / 85,0 / 69,4 / 80,1 / 33,0 %**.
- En separat Pine-kontroll använde MA Behavior i varje fonds egen dagskontext och tog fram percentilen oberoende från tidigare avstånd. Den stämde med de visade värdena för **50D, 200D, 50W och 12M i SEK**, med och utan Smooth för 50W och 12M. Vecko- och månads-omräkningen kontrollerades mot ett separat medelvärde av avslutade perioders SEK-dagsstängningar. I Native stämde 12M för alla fem. EUR-gruppen använde **2026-11-20**, SEK och USD **2026-11-19**. ACWI 12M visade **+5,15 % / P46,9** i SEK och **−2,22 % / P18,4** i USD.
- P90/P10 gav grön text för ACWI och VWCE med 50D. P70/P30 gav röd text för XACTHDIV med 200D. Tioårsfönstret visade percentil `N/A` för VWCE och XACTHDIV med 200D och behöll deras avstånd. All Available kunde visa percentil igen. 200M visade `N/A` enbart där respektive underlag saknades. På 1W visade Compare instruktionen att använda 1D medan SMA-linjen och candle-färger visades.
- Syntetiska Pine-kontroller passerade för exakt P95/P5, interpolation, neutral exakt MA-träff, 29 tidigare observationer på aktuell sida, kort historik, olika sessionsdatum, saknad valuta och avgränsning mot data efter cutoff. En separat lokal beräkning från SXR8:s exporterade dagskurser matchade 50D och 200D inklusive de 1 274 tidigare sessionerna. P10:s inträdesantal röd/grön återkom för SXR8 (**12/8** och **11/4**) och BTCUSDT spot (**3/4** och **0/1**) med 50D respektive 200D.
- Pine Profiler på femsymbolsvyn i SEK med 200D och candle-färger på gav ungefär **0,57 s för P10** och **0,68 s för P12**. Den externa statistikförfrågan tog **381,7 ms** respektive **429 ms**, båda med **29 495 exekveringar**. Varje kontext sorterar en kopia av avstånden enbart vid färska stängningar. Högst fem skalära MA-resultat hämtas per extern symbol tillsammans med befintlig statistik. Tiderna är enskilda mätningar. Pine kompilerar med konsistensvarningar kring kontextberoende anrop och kombinationerna ovan körde utan exekveringsfel. [Pines resursgränser](https://www.tradingview.com/pine-script-docs/writing/limitations/)

| Symbol, SEK 2026-11-19 | MA Distance 50D | MA Percentile 50D | MA Distance 200D | MA Percentile 200D |
| --- | ---: | ---: | ---: | ---: |
| SXR8 | −2,15 % | P13,1 | +6,04 % | P48,6 |
| ACWI | −4,16 % | P5,3 | +2,54 % | P33,5 |
| EUNL | −2,22 % | P11,3 | +5,11 % | P47,7 |
| VWCE | −2,87 % | P7,9 | +4,01 % | P40,8 |
| XACTHDIV | +0,84 % | P50,7 | +4,67 % | P74,8 |

## P10

SMA, **MA Behavior** och extremfärger följer med vid byte av tidsintervall. Måtten använder symbolens dagssekvens. Extremfärger markerar inträdet i en svans av signerade avstånd, med P95/P5 som standard och ett separat återställningsband. Overview, Dips och Compare kör vidare på 1D. [Tidsintervall och extremmodell](METRICS.md#ma-behavior)

### Verifiering den 22–23 november 2026

- TradingView Desktop kompilerade från VS Code och sparade **revision 33** i den befintliga privata indikatorn. Avanza sparades på SXR8 1D med Compare i SEK, 200D och användarens tidigare aktiverade färgning med den nya standardgränsen 95. ACWI behöll stjärnan, Opportunity 1,0 och Dip Rarity 85,0 %.
- En Pine-kontroll mot en separat daglig `ta.sma` gav **7 564,288604** på 4H, 1D, 1W och 1M, med **1 275** jämförbara dagsobservationer till och med **2026-11-20** i varje femårsfönster. 4H visade 21 unika markeringar i den laddade historiken, varav en på första efterföljande värdbar. Ingen markering kom före dagsstängningen eller upprepades. 1W hade 21 markerade värdbars och 1M 17. SXR8 50W gav +4,95 % på 1W med och utan utjämning vid veckans slut. 12M gav +5,80 % utan och +6,29 % med utjämning. 1D och motsvarande högre graf stämde för de jämförda värdena.
- På en faktiskt öppen BYBIT:BTCUSDT.P-vecka visade 1W, 4H och 1D samma senaste bekräftade datum **2026-11-21**, **1 827** jämförbara sessioner och ett avstånd på **−16,93 %**. Den öppna dagsobservationen den 22 november ingick inte. Historiska färgade veckocandles och den pågående veckans SMA visades. SXR8 på 1M visade 1D-instruktionen för Compare med SMA-linjen kvar. Syntetiska Pine-tester täckte inklusiva svansgränser, återställningsband, saknad observation, kort historik och otillräckligt urval på ena sidan.
- Pine Profiler med MA Behavior och färgning på gav **121,3 ms totalt på 1W** och **70,5 ms på 1M**. På dessa två grafer körs dagsmotorn i en förfrågan till symbolens dagskontext. Diagrammens egen historik, datakällans täckning och Pine-gränserna kan begränsa äldre markeringar. [Resursgränser](https://www.tradingview.com/pine-script-docs/writing/limitations/#intrabars)

### Extremhändelser mot P09

Fönstret 2021-11-20–2026-11-20 omfattade 1 275 sessioner för SXR8 i SEK och 1 827 för BINANCE:BTCUSDT. Båda modellerna använde samma femårshistorik per dag och sina respektive standardtrösklar. En P09-händelse var den första dagen i en sammanhängande följd med samma extremfärg. P10 räknar inträden efter återställning.

| Symbol och SMA | P09 händelser röd/grön | P10 händelser röd/grön | Längsta röda period P09 → P10 | Längsta gröna period P09 → P10 |
| --- | ---: | ---: | ---: | ---: |
| SXR8 50D | 31 / 10 | 12 / 8 | 23 → 1 | 46 → 1 |
| SXR8 200D | 18 / 2 | 11 / 4 | 103 → 1 | 71 → 1 |
| BTCUSDT 50D | 17 / 11 | 3 / 4 | 16 → 1 | 9 → 1 |
| BTCUSDT 200D | 4 / 9 | 0 / 1 | 3 → 0 | 72 → 1 |

Med SXR8 200D minskade antalet röda dagsbars från 471 till 11. P10:s nya färgfördelning är verifierad på dessa serier. Färgen på en pågående veckocandle kan bytas när en senare bekräftad dagsstängning samma vecka ger en ny extremhändelse. En fördröjd dagsfeed kan flytta markeringen till första efterföljande intradagsbar. Reviderad eller utökad prishistorik kan ändra tidigare statistiskt underlag.

## P09

**MA Behavior** visar tid, avstånd och periodlängder över och under vald SMA. **Color Extreme Candles** kan markera bekräftade bars med ovanligt stort avstånd eller en ovanligt lång period vid minst medianavståndet. [Metod och minimiurval](METRICS.md#ma-behavior)

### Verifiering den 22 november 2026

- TradingView Desktop kompilerade slutkällan från VS Code som revision **32** av den befintliga privata indikatorn. Avanza sparades med **SXR8 1D**, Compare i SEK, SMA 200D, femårsperiod och extremfärger av. Overview, Dips och femsymbolsvyn matchade tidigare mått. I Compare hade ACWI kvar stjärnan, Opportunity 1,0 och Dip Rarity 85,0 %.
- På SXR8 med **SMA 200D och fem år** var mediana avstånd **+7,57 % / −3,04 %** och P90-avstånden **+13,17 % / −9,65 %**. P90 Duration var **46 / 15 handelssessioner** ovanför respektive under. Den pågående perioden ovanför var 162 sessioner och Current Stretch var 17,20 %. SMA 50D gav P90-avstånd **+6,43 % / −7,10 %** och P90 Duration **77 / 27**.
- Desktop visade aktuellt avstånd **−5,28 %** för 50D, **+4,95 %** för 50W med och utan Smooth SMA på den aktuella fredagsstängningen, samt **+5,80 %** för 12M och **+6,29 %** med Smooth SMA. SMA 200D hade 2 539 jämförbara dagar för tio år och 3 865 i All Available.
- Röda och gröna extremcandles sågs på SXR8 med 50D och P50. Röda historiska extremcandles sågs även vid 200D och P90. Ordinarie färger återgick när funktionen stängdes av. På en faktiskt öppen BTCUSDT.P-dagsbar den 22 november slutade MA-statistiken den **21 november**. Den öppna baren behöll sin ordinarie färg när föregående kvalificerade bar var grön.
- Pine med produktionsfunktionerna matchade ett separat Python-facit för 2 700 syntetiska observationer i 5 Years, 10 Years och All Available. Testerna täckte inklusiva gränser, median, oavslutade och avbrutna perioder, uteslutning vid fönstrets start, lika stängningar, kort historik och den kronologiska extremklassificeringen. Värden ordnas med binär sökning och gamla värden tas bort när fönstret flyttas.
- Pine Profiler på slutkällan mätte **455,6 ms** för femsymbolsvyn med färger av och **cirka 0,5 s** med femårsfärgning på. P08:s observerade baslinje var **421,9 ms**. Den externa statistikförfrågan hade fortsatt **29 495** exekveringar i båda P09-körningarna. En tidigare profilering av samma MA-beräkning i All Available på SXR8 mätte 95 ms totalt. Tiderna är enskilda körningar. [Pines resursgränser](https://www.tradingview.com/pine-script-docs/writing/limitations/)

## P08

Compare visar en neutral rad för **Dip Rarity**, andelen dagsstängningar med grundare ATH-baserad drawdown än vid jämförelsedatumet. Urvalet omfattar fem kalenderår och följer Opportunity-datumet per valuta. [Metod och datakrav](METRICS.md#dip-rarity)

### Verifiering den 22 november 2026

- TradingView Desktop kompilerade slutkällan från VS Code som revision **27** av den befintliga privata indikatorn. Alla fem symbolerna visade Dip Rarity på **SXR8 1D** med samma Opportunity-poäng, stjärna och övriga mått som i P07. Avanza-layouten är sparad med Compare i SEK. Dip Rarity-cellerna var neutrala i både SEK och Native.
- I SEK, med gemensamt datum **2026-11-19**, visade SXR8 **61,7 %**, ACWI **85,0 %**, EUNL **69,4 %**, VWCE **80,1 %** och XACTHDIV **33,0 %**. ACWI-tooltipen visade perioden från 2021-11-19 och **188 av 1 255** dagar med minst lika djup drawdown. I Native var värdena 61,7 %, 66,7 %, 72,7 %, 78,3 % och 33,0 %. EUR använde 2026-11-20 medan SEK och USD använde 2026-11-19.
- Pine-tester med produktionsfunktionerna verifierade 50 av 1 000 dagar, lika djupa drawdowns, ny ATH, djupaste drawdown, helgdag, skottdag, kort och explicit ogiltig historik, saknad FX, oförändrad Opportunity-ledare och att senare priser inte ändrade ett tidigare resultat. En separat Python-beräkning gav **764 av 1 827** dagar för en syntetisk serie med 5 200 stängningar. Pine gav samma resultat efter att den cirkulära historikbufferten fyllts.
- Pine Profiler mätte **421,9 ms** totalt i en femsymbolskörning i SEK, med **327,2 ms** över **29 495** exekveringar på den externa statistikförfrågan. Koden sparar ett drawdownvärde per bekräftad session i den befintliga historikbufferten. För färska jämförelsedatum skannas enbart femårsperioden. Den befintliga förfrågan returnerar två extra räknare per daterat resultat. [Pines resursgränser](https://www.tradingview.com/pine-script-docs/writing/limitations/)
- Desktop-testet gjordes när marknaderna var stängda. Måttet använder laddade sessioner. TradingView ger inget säkert sätt att skilja en helt utebliven bar från ett börsuppehåll utifrån prisserien.

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
