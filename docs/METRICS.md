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

### MA Behavior

- SMA är det aritmetiska medelvärdet av det valda antalet på varandra följande giltiga bekräftade stängningar på **Daily**, **Weekly** eller **Monthly**. Standard är 200 dagar och minsta längd är 2 barer på det valda intervallet. En explicit ogiltig stängning på det valda intervallet bryter dess fönster.
- Daily inkluderar jämförelsedagens stängning. För Weekly och Monthly hämtas tidigare avslutade vecko- respektive månadsbarer från TradingView. Deras nya SMA tas i bruk vid den första bekräftade dagsbaren i nästa period. Det bekräftade grundvärdet är detsamma under hela perioden.
- **Smooth SMA** är valbart för Weekly och Monthly. På varje bekräftad dagsbar interpoleras linjärt från det föregående till det senast tillgängliga bekräftade SMA-värdet. Vikten är den del av den pågående veckan eller månaden som förflutit enligt barernas tidsstämplar. När ett föregående giltigt värde saknas används det tillgängliga SMA-värdet direkt. Både linjen och MA-måtten använder det utjämnade värdet. Linjen kan därför ligga efter den nya bekräftade nivån under övergången.
- **MA Distance** är `100 × (C_t / SMA_t − 1)` i procent för senaste bekräftade dagsstängningen. Visa `N/A` när fönstret behöver fler giltiga stängningar.
- **Above MA** är `100 × antal dagar strikt över SMA / antal jämförbara dagar`. En jämförbar dag har en giltig bekräftad dagsstängning och en giltig SMA för den valda längden och det valda intervallet. Dagar med stängning exakt på SMA ingår i nämnaren. Tooltipen visar antalet jämförbara dagar och vid noll visas `N/A` för andelen. Kryssrutan på inställningsraden styr linjens synlighet.

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

## Förslag

### Datatäckning

Markera identifierade datagap när det finns tillräckligt underlag för att skilja dem från planerade sessionsuppehåll. En framtida beräkning på 1W måste behandla hela den underliggande dagssekvensen innan resultatet visas på veckocharten. Samma krav på bevarade dagsobservationer gäller intraday.

### Drawdown-episoder

- En episod börjar vid första stängning under det löpande högsta värdet och avslutas vid första stängning på eller över den nivån. Använd den senaste stängningen på toppnivån före nedgången som toppdatum. Botten är den första lägsta stängningen inom episoden. Mät kalenderdagar från topp till botten och från botten till återhämtning. För en pågående episod är botten preliminär och återhämtningstiden `N/A`.
- Beräkna frekvens som antalet episoder under angiven mätperiod. Vid ett tröskelvärde, till exempel 10, 20 eller 30 procent, räknas en episod när dess största fall når eller passerar tröskeln. Siffrorna är kumulativa mellan trösklarna. Mellanliggande svängningar inom samma oåterhämtade drawdown ger ingen ytterligare episod.
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
