# Måttdefinitioner

## Beslutat

### Data och mätperiod

- Indikatorn använder prisstängningarna på standardgrafer med exakt intervallet `1D`. Andra intervall och syntetiska charttyper som Heikin Ashi visar en instruktion i panelen.
- En giltig observation är en tillgänglig dagsstängning större än noll. `na`, noll och negativa stängningar behandlas som saknade. En explicit ogiltig bar bryter SMA-fönstret. En utebliven bar i datakällan kan vara ett planerat uppehåll eller ett datagap. Beräkningarna använder de barer som TradingView laddat.
- Panelen visar det första laddade giltiga sessionsdatumet och det senaste bekräftade sessionsdatumet. Pine anger datumen genom `time_tradingday`. CAGR använder hela kalenderdagar mellan dem, även vid sommartidsbyten.
- Statistik, historiska räknare och SMA-linjen uppdateras när dagsbaren bekräftas. Om den senaste bekräftade barens stängning är ogiltig visar panelen slutdatum och `N/A` för de mått som behöver stängningen. Historiskt max-DD använder tidigare giltiga stängningar och andelen dagar över SMA använder tidigare jämförbara dagar.
- Chartens val av historik, prisserie, valuta och prisjusteringar påverkar resultat och jämförbarhet. Beteckningen *total return* kräver verifierad utdelningsbehandling, övriga justeringar, avgifter och valuta.

### Performance

- **Return** är prisavkastningen i procent, `100 × (C_slut / C_start − 1)`. Utgå från första giltiga stängningen och stängningen på den senaste bekräftade dagsbaren. Kräv två giltiga priser på olika sessionsdatum. Annars visas `N/A`.
- CAGR i procent per år är `100 × ((C_slut / C_start)^(365,25 / d) − 1)`, där `d` är antalet kalenderdagar mellan sessionsdatumen med samma krav som för prisavkastning.
- **1Y, 3Y, 5Y och 10Y** använder samma bekräftade slutkurs. Flytta slutdatumet 1, 3, 5 eller 10 kalenderår bakåt. Om den 29 februari saknas i målåret används den 28 februari.
- Använd den senaste laddade sessionen på eller före måldatumet. Om måldatumet infaller under ett uppehåll kan referensen därför ligga tidigare. Visa `N/A` om historiken saknar en sådan session eller om dess stängning är explicit ogiltig. En senare giltig stängning på eller före måldatumet ersätter en tidigare ogiltig observation. Tooltipen visar referensdatumet för respektive mått.

### Drawdowns från historiska toppar

- Låt `H_t` vara den högsta observerade giltiga stängningen fram till dag `t`. Aktuell drawdown är `100 × (C_t / H_t − 1)`. Vid ny eller återtagen topp visas `0 %`.
- Max drawdown är det lägsta observerade drawdownvärdet sedan första giltiga stängningen. En återhämtning behåller det historiska maxvärdet. Kräv två giltiga dagsobservationer. Utan dem visas `N/A`.
- Redovisa drawdowns från historiska toppar och swing-episoder som egna mått. Redovisa avslutade respektive pågående episoder och räkna varje identifierad episod en gång inom sitt mått.

### Lokala nedgångsepisoder och frekvens

- **Dips** använder bekräftade dagsstängningar. Den första giltiga stängningen i varje sammanhängande avsnitt sätter en lokal topp. Toppen följer stigande stängningar tills en lägre stängning startar en episod. Lika toppar startar ingen episod. Under en pågående episod ligger toppen fast och botten är den lägsta stängningen som hittills observerats.
- Episoden avslutas när en stängning når den lokala toppen eller stiger minst **Reversal %** från episodens botten. Resultatet registreras vid den stängningen, som också blir nästa lokala referenstopp. Standard är 5 %. Episodens djup är `100 × (1 − botten / episodtopp)`. Historiska toppar används separat för **Current DD** och **Max DD**.
- Varje avslutad episod räknas en gång per uppnådd tröskel, inklusive exakt träff. Trösklarna har standardvärdena 5, 10, 20 och 30 %. Ange fyra strikt stigande värden. Dubbletter och omvänd ordning ger ett inställningsmeddelande i Dips tills värdena rättats.
- **Active Dip** är `100 × (senaste bekräftade stängning / lokal topp − 1)`. En stängning som etablerar en topp eller avslutar en episod ger 0 %. En ogiltig senaste stängning ger `N/A`. En pågående episod bidrar först till frekvensen när den har avslutats.
- En explicit ogiltig stängning bryter det pågående avsnittet. En öppen episod vid avbrottet utelämnas ur episodantalen och nästa giltiga stängning sätter en ny topp. Observerad kalendertid är summan av dagar mellan intilliggande giltiga stängningar inom varje avsnitt. Intervall över en explicit ogiltig bar räknas bort. Normala sessionsuppehåll ingår. En helt utebliven bar kan inte skiljas från ett sessionsuppehåll. Om laddad historik börjar mitt i en äldre nedgång kan mätningen börja först vid den första laddade giltiga stängningen.
- Observerade år är observerade kalenderdagar dividerat med 365,25. Frekvensen per år är antal avslutade episoder dividerat med observerade år. Genomsnittliga år per episod är det omvända vid positivt antal. Annualisering kräver minst lika många observerade dagar som från första giltiga sessionsdatumet till dess ettårsdag, med 28 februari i målår utan skottdag. Vid kortare täckning visas `N/A`. Med tillräcklig täckning och noll avslutade episoder visas `0`.
- Dips visar återkomst per år när frekvensen är minst en gång per år och annars en gång per genomsnittligt antal år. Tooltipen ger antal, datumspann och observerad täckning. Värdena beskriver historisk förekomst.

### Symboljämförelse

- **Compare** visar chartsymbolen och upp till fyra valda symboler. En avstängd eller tom input utelämnas. Samma standardiserade börs- och tickersymbol visas en gång. **Compare currency** är som standard SEK. **Native** använder chartens prisserie och respektive extrasymbols ursprungliga dagliga prisserie. Prisjusteringar följer respektive källa i båda lägena.
- För SEK hämtas den enskilda dagsstängningen med `request.security(..., currency = currency.SEK)` i symbolens egen dagskontext innan någon statistik beräknas. TradingView använder föregående dags valutakurs för omräkningen. Föregående stängning hämtas från den redan omräknade serien på sitt ursprungliga sessionsdatum. En serie som redan är uttryckt i SEK används direkt. Om en giltig dagsstängning saknar omräknad kurs visas `N/A` för symbolen i SEK-läget. Overview och Dips följer chartens prisserie som tidigare. [TradingViews valutakonvertering](https://www.tradingview.com/pine-script-docs/concepts/other-timeframes-and-data/#currency)
- CAGR, ATH-baserad Current DD och Max DD, Active Dip och historisk dipfrekvens använder samma definitioner som Overview och Dips. Compare använder den valda **Reversal %** och en fast, inkluderande tröskel på **≥10 %**. `N/A` följer måttets ordinarie datakrav.
- **1Y**, **3Y** och **5Y** visar prisavkastning och använder dagens UTC-datum som gemensamt kalendermål för periodslut. Startmålet ligger motsvarande antal kalenderår tidigare, med samma skottdagsregel som Overview. Varje symbol använder sin senaste tillgängliga bekräftade stängning för periodslutet och senaste session på eller före startmålet för referensen. En ogiltig referensstängning ger `N/A`. Periodslutet måste ligga efter startmålet. Både måldatum och faktiska sessionsdatum visas i tooltipen, tillsammans med annualiserad avkastning för 3Y och 5Y. Overview förankrar perioderna i chartsymbolens senaste bekräftade session.
- **1Y**, **3Y** och **5Y** färgsätts vid samma prisvaluta, referens- och slutdatum. **CAGR** och **Max DD** kräver samma valuta och hela datumperiod. När visade värden skiljer sig markeras högsta i grönt och lägsta i rött, även när alla är negativa. För **Max DD** innebär det att värdet närmast noll markeras grönt. För **Current DD** tolkas större nedgång som större rabatt inom en grupp med positiv Quality, samma valutabas och samma slutdatum. **Active Dip** och **Dips ≥10%** visas neutralt.
- Varje extern symbols statistik räknas i symbolens eget dagskontext, inklusive sessioner som saknas i värddiagrammets kalender. `request.security()` med `lookahead_off` returnerar skalära mått och högst fem färska daterade resultat för Opportunity och Dip Rarity per symbol. TradingView samplar resultaten på värddiagrammets tidsaxel. På ett helgstängt värddiagram kan en kryptokolumn därför ligga kvar på fredagen. Vid övergångar och fördröjda data kan en fjärrsymbol behöva nästa uppdatering innan en stängning syns. Tooltips visar det faktiska senaste sessionsdatumet och den observerade perioden. Vyn använder den aktuella UTC-dagen och är avsedd för löpande jämförelse. [TradingViews datamodell](https://www.tradingview.com/pine-script-docs/concepts/other-timeframes-and-data/)

### Opportunity

- **Quality** är `0,70 × CAGR 3Y + 0,30 × CAGR 5Y` i procentenheter. För ett gemensamt jämförelsedatum används respektive symbols sista bekräftade stängning på eller före datumet. 3Y och 5Y har gemensamma kalenderbaserade startmål. Varje symbol använder sin sista session på eller före respektive startmål, högst fyra kalenderdagar tidigare. En explicit ogiltig referens ger `N/A`. Annualiseringen använder det faktiska antalet kalenderdagar mellan kurserna och 365,25 dagar per år.
- **Recovery Upside** är `|DD| / (100 − |DD|)`, med drawdown i procentenheter mätt från den historiska toppen till och med jämförelsedatumet. **Opportunity** är positiv Quality multiplicerad med Recovery Upside. En giltig poäng kräver båda perioderna samt en bekräftad drawdown strikt mellan 0 och −100 %. Tooltipen visar datum, Quality och det drawdown-värde som faktiskt användes. Compare-raden **Current DD** behåller senaste bekräftade datum enligt sin ordinarie metod.
- Per prisvaluta väljs det datum som ger flest kvalificerade symboler, med senaste datum vid lika antal. Möjliga datum sträcker sig från dagens UTC-datum till fyra kalenderdagar bakåt. Symbolen måste ha ett giltigt underlag på sin senaste bekräftade session och en bekräftad serie som når jämförelsedatumet. Stängningen som används måste också ligga inom de senaste fyra kalenderdagarna. Det tillåter olika föregående sessioner vid börshelgdagar och utesluter för gamla data. Saknad SEK-kurs, kort historik eller övrigt ogiltigt underlag utesluter bara den berörda kandidaten.
- Inom en grupp med minst två kvalificerade symboler färgas högsta visade poäng grön och lägsta röd när värdena skiljer sig. En unik vinnare vid visad precision på en decimal får grön ticker och stjärna om endast en valutagrupp går att rangordna. Vid flera rangordningsbara grupper i Native går det att jämföra färgerna inom respektive valuta. Enstaka kvalificerade symboler visas neutralt. Opportunity är en historisk heuristik.

| CAGR 3Y | CAGR 5Y | Current DD | Quality | Visad Opportunity |
| ---: | ---: | ---: | ---: | ---: |
| 30 % | 20 % | −2 % | 27 % | 0,6 |
| −10 % | 5 % | −60 % | −5,5 % | `N/A` |
| 15 % | 10 % | −25 % | 13,5 % | 4,5 |

### Dip Rarity

- **Dip Rarity** visar andelen observerade dagsstängningar med grundare ATH-baserad drawdown än vid jämförelsedatumet. Beräkna `100 × (1 − antal lika djupa eller djupare / antal jämförbara dagar)`. Med 50 av 1 000 sådana dagar blir värdet 95,0 %. Den aktuella stängningen räknas om den ligger i mätperioden. Vid en bekräftad drawdown på 0 % räknas alla jämförbara dagar som minst lika djupa och resultatet blir 0,0 %.
- Perioden omfattar de senaste fem kalenderåren till och med valutagruppens jämförelsedatum för Opportunity, med samma skottdagsregel som övriga perioder. Symbolens senast bekräftade stängning på eller före datumet ger jämförelsens drawdown. För varje tidigare dag används dess egen historiska topp i den valda prisvalutan. Toppen kan ligga före femårsperioden och beror på den laddade historiken.
- En giltig stängning krävs på eller högst fyra kalenderdagar före periodens start. Referensen ingår i urvalet om den infaller på startdatumet. Kort historik, explicit ogiltig stängning i perioden, otillgänglig aktuell stängning eller saknad SEK-omräkning ger `N/A`. Vanliga sessionsuppehåll påverkar urvalet genom sina faktiska handelsdagar. En bar som saknas helt i datakällan kan se ut som ett sessionsuppehåll.
- Om Opportunity saknar jämförelsedatum i en valuta väljs för Dip Rarity det senaste datumet med flest giltiga femårsunderlag inom samma fyradagarsfönster. Det ger till exempel 0,0 % vid en ny ATH med giltig historik. Raden visas med en decimal och neutrala färger. Tooltipen visar mätperiod, jämförelsedatum, faktisk slutstängningsdag när den avviker samt antal dagar. Opportunity påverkas inte av måttet.

### MA Behavior

- SMA är det aritmetiska medelvärdet av det valda antalet på varandra följande giltiga bekräftade stängningar på **Daily**, **Weekly** eller **Monthly**. Standard är 200 dagar och minsta längd är 2 barer på det valda intervallet. En explicit ogiltig stängning på det valda intervallet bryter dess fönster.
- Daily inkluderar jämförelsedagens stängning. För Weekly och Monthly hämtas tidigare avslutade vecko- respektive månadsbarer från TradingView. Deras nya SMA tas i bruk vid den första bekräftade dagsbaren i nästa period. Det bekräftade grundvärdet är detsamma under hela perioden.
- **Smooth SMA** är valbart för Weekly och Monthly. På varje bekräftad dagsbar interpoleras linjärt från det föregående till det senast tillgängliga bekräftade SMA-värdet. Vikten är den del av den pågående veckan eller månaden som förflutit enligt barernas tidsstämplar. När ett föregående giltigt värde saknas används det tillgängliga SMA-värdet direkt. Både linjen och MA-måtten använder det utjämnade värdet. Linjen kan därför ligga efter den nya bekräftade nivån under övergången.
- **MA Distance** är `100 × (C_t / SMA_t − 1)` i procent för senaste bekräftade dagsstängningen. Visa `N/A` när fönstret behöver fler giltiga stängningar.
- **Above MA** är `100 × antal dagar strikt över SMA / antal jämförbara dagar`. En jämförbar dag har en giltig bekräftad dagsstängning och en giltig SMA för den valda längden och det valda intervallet. Dagar med stängning exakt på SMA ingår i nämnaren. Tooltipen visar antalet jämförbara dagar och vid noll visas `N/A` för andelen. Kryssrutan på inställningsraden styr linjens synlighet.

#### Fördelningar och perioder

- **Panel View → MA Behavior** visar två kolumner för chartsymbolens dagsstängningar över och under samma SMA som linjen använder. **MA Statistics Period** är fem kalenderår som standard. Tio kalenderår och all laddad historik är valbara. Fönstret för varje bar slutar på dess sessionsdatum och börjar på kalenderårsdagen, inklusive gränsdatumet. Den 29 februari flyttas till den 28 februari vid behov. Ett valt kalenderfönster kräver giltiga MA-observationer tillbaka till eller före startdatumet. All Available använder all laddad giltig historik.
- **Time %** kräver minst 20 jämförbara sessioner. Lika pris och SMA ingår i nämnaren och hör till ingen sida. **Median Distance** är medianen av de absoluta procentavstånden på respektive sida. **P90 Distance** är den sorterade observationen med rang `ceil(0,90 × antal)`. Båda kräver minst 30 avstånd per sida. Medianen använder medelvärdet av de två mittersta observationerna vid jämnt antal. Avstånden i tabellen visar sidans tecken.
- **Median Duration** och **P90 Duration** använder samma definitioner på längderna hos minst tio fullständiga avslutade perioder per sida. En giltig korsning eller en exakt träff på SMA avslutar perioden. En ogiltig bar avbryter perioden och gör längden osäker. Perioden måste ha observerad start inom valt fönster och observerat avslut. Start mitt i en period vid första giltiga MA eller efter ett datagap ger en ofullständig period. Färdiga perioder som började före fönstret utesluts från fördelningen.
- **Current Duration** räknar den pågående periodens observerade handelssessioner, även om starten ligger före fönstret. `≥` markerar att den faktiska starten är okänd. **Current Stretch** är andelen av minst 30 tidigare avstånd på samma sida som är högst lika stora som den aktuella avvikelsen, uttryckt i procent. Den bedöms före dagens observation läggs till. Historikmåtten i tabellen inkluderar den senaste bekräftade dagen. En session som saknas helt i datakällan kan se ut som ett handelsuppehåll.

#### Extremfärger

- **Color Extreme Candles** är av som standard. En bekräftad dagsbar över SMA kan färgas röd och en under SMA grön när avvikelsen är minst den valda historiska percentilen. Standard är P90 och intervallet är P50–P100. Färgen kan också utlösas när den aktuella periodlängden når historisk P90 Duration och avståndet minst når sidans median. Trösklarna räknas på respektive sida i aktuellt fönster före dagens stängning och före ett eventuellt periodavslut som bekräftas samma dag. De två villkoren kräver giltigt underlag var för sig.
- Färgsättningen ritar endast markerade candles på originalbarens öppning, högsta, lägsta och stängning, så kropp och veke får samma extremfärg. Övriga bars behåller diagrammets färger och stil.
- I tabellen markeras Current Stretch när avståndsvillkoret nås och Current Duration när längd- och medianvillkoren nås. Färgerna beskriver historisk ovanlighet. När diagrammet laddar mer äldre historik eller om datakällan ändras kan en tidigare fördelning få ett annat underlag.

### Deterministiska P01-exempel

| Fall | Förväntat |
| --- | --- |
| `100` den 2 januari 2020 och `146,41` den 2 januari 2024. | `46,41 %` prisavkastning och `10,00 %` CAGR över 1 461 kalenderdagar. |
| `100 → 85 → 95 → 75 → 100`. | Aktuell drawdown `0 %` och max drawdown `−25 %`. |
| 200 stängningar på `100`, följda av `110` och `90`. | SMA är `N/A` under de första 199 barerna. De tre sista SMA-värdena är `100`, `100,05` och `100`. Andelen över SMA är `1/3` av jämförbara dagar. |
| En dagsbar med `na` efter 200 giltiga stängningar. | Aktuella mått som kräver stängningen är `N/A`. SMA återkommer vid den 200:e giltiga stängningen i följd efter den ogiltiga baren. |
| En giltig stängning, eller två giltiga stängningar med samma sessionsdatum. | Prisavkastning och CAGR är `N/A`. Max drawdown är `N/A` när det bara finns en giltig stängning. |
| En öppen dagsbar med pris över tidigare topp. | Panelen visar föregående bekräftade dagsbar. Topp och räknare behåller värdena från den avslutade historiken. |

### Deterministiska P02-exempel

| Fall | Förväntat |
| --- | --- |
| Slutkurs `100` den 3 juni 2024. Äldsta stängning `80` fredagen den 2 juni 2023. | Lördagens måldatum ger fredagen som referens. 1Y är `25 %`. 3Y, 5Y och 10Y är `N/A`. |
| Slutdatum 4 juli 2024. Sessioner 3 och 5 juli 2023, inga barer den 4 juli. | 1Y använder den 3 juli 2023. |
| Slutdatum 29 februari 2024. | 1Y, 3Y, 5Y och 10Y har måldatum den 28 februari i respektive målår. |
| Måldatum 21 november 2023. Stängningen den 20 november är `na` och den 22 november är giltig. | Referensen för den 21 november är osäker och ger `N/A`. Med måldatum 22 november används den giltiga stängningen. |

### Deterministiska P03-exempel

| Stängningar med 5 % reversal | Avslutade episoddjup och aktiv nedgång |
| --- | --- |
| `100 → 94 → 100 → 80 → 100` | 6 % och 20 %. Antal vid ≥5, ≥10, ≥20 och ≥30 % är 2, 1, 1 och 0. |
| `100 → 94 → 95 → 80 → 84` | En episod på 20 %. Stängning 84 uppfyller exakt 5 % reversal från 80. |
| `100 → 94 → 95 → 80` | 0 avslutade. Active Dip är −20 %. |
| `100 → 90 → 96 → 89 → 95` | Två episoder på 10 % och cirka 7,29 %. Den andra lokala toppen är 96. |
| `100 → 100 → 95 → 95 → 99,74 → 99,75` | Lika topp och botten ger inga dubletter. En episod träffar 5 % djup och reversal exakt. |
| `100 → 70 → na → 80 → 72 → 76` | Första avsnittets pågående episod avbryts. En bekräftad episod på 10 % räknas från den nya toppen 80. |

## Förslag

### Datatäckning

Markera identifierade datagap när det finns tillräckligt underlag för att skilja dem från planerade sessionsuppehåll. En framtida beräkning på 1W måste behandla hela den underliggande dagssekvensen innan resultatet visas på veckocharten. Samma krav på bevarade dagsobservationer gäller intraday.

### Varaktighet och återhämtning till historisk topp

- En episod börjar vid första stängning under det löpande högsta värdet och avslutas vid första stängning på eller över den nivån. Använd den senaste stängningen på toppnivån före nedgången som toppdatum. Botten är den första lägsta stängningen inom episoden. Mät kalenderdagar från topp till botten och från botten till återhämtning. För en pågående episod är botten preliminär och återhämtningstiden `N/A`.
- Räkna en episod som passerar ett identifierat datagap som osäker. Håll den utanför antalen för säkert avslutade och pågående episoder. Max drawdown bygger på observerade stängningar. Visa begränsad täckning om gap kan dölja en djupare botten.

### MA Behavior

- Andelen dagar under SMA beräknas med samma nämnare som andelen över SMA och med antalet dagar strikt under SMA som täljare. Om datagap senare kan identifieras ska fönster som korsar dem uteslutas.
- Typiskt avstånd kan visas som median, beräknad separat för positiva och negativa distanser. Ett extremt avstånd kan beskrivas med en övre percentil på den positiva sidan och en nedre percentil på den negativa. Kvantilmetod, gränser och minsta urval är öppna val. Visa `N/A` för en sida som saknar tillräckliga observationer.

### Deterministiska exempel för förslagen

| Fall | Förväntat med förslaget |
| --- | --- |
| `100 → 85 → 95 → 75 → 100` den 5–9 februari 2024, en stängning per dag. | En avslutad episod vid både 10 och 20 procent, noll vid 30 procent. Tre kalenderdagar till botten och en till återhämtning. Om sista `100` tas bort är episoden pågående med aktuell drawdown `−25 %`. |
| 200 stängningar på `100`, följda av `110` och `90`. | Andelen under SMA är `1/3` av jämförbara dagar. |

## Senare

- **Swing-episoder.** Välj swing-punkter eller tröskelmetod och definiera vad som bekräftar start och slut, vilken dag bekräftelsen blir känd och hur nästlade rörelser räknas. Föreslagna utfall är storlek i procent av episodens startpris, kalenderdagar mellan valt start- och slutdatum samt antal episoder per redovisad mätperiod. Nivåer och segmentering är öppna.
- **Stöd och motstånd kring SMA.** Besluta vad som utlöser och avslutar ett test, vilken tolerans och vilket utfallsfönster som gäller samt hur upprepade kontakter räknas. Andelen lyckade test ska ha objektiva kriterier för täljare och nämnare.
