# Måttdefinitioner

## Beslutat

- Referensen är symbolens ordinarie dagliga prisstängningar. `200D` avser 200 dagliga barer. Avslutade resultat bygger på bekräftade 1D-barer, med samma resultat när samma historik spelas upp på nytt.
- 1D är stödd startpunkt. Övriga chartintervall ska visa en tydlig begränsning tills dagsberäkningarna kan verifieras där. En beräkning på 1W måste behandla hela den underliggande dagssekvensen innan resultatet visas på veckocharten. Samma krav på bevarade dagsobservationer gäller intraday.
- Ange mätperiod och visa `N/A` när underlaget för ett mått saknas. Redovisa kända skillnader som påverkar jämförbarheten, till exempel historiklängd, datagap, sessionskalender, prissättning, valuta och tillgängliga justeringar. Märk avkastning från prisserien som prisavkastning. Beteckningen *total return* kräver verifierad utdelningsbehandling, övriga justeringar, avgifter och valuta.
- Redovisa ATH-baserad drawdown och swing-episoder som olika mått. Håll avslutade och pågående episoder åtskilda. Räkna varje identifierad episod en gång inom sitt mått.

## Förslag

### Datatäckning

En giltig observation för avkastning, drawdown och SMA-distans är en ändlig daglig stängning större än noll. Behandla `na` och övriga ogiltiga stängningar som saknade. Kalenderdagar utan ordinarie session räknas som planerade uppehåll. Markera identifierade datagap. Historiken börjar vid första tillgängliga giltiga observation, som kan ligga efter symbolens första handelsdag.

Panelen visar läget vid den senaste bekräftade dagsbaren. Ett aktuellt mått som kräver den barens stängning är `N/A` om stängningen saknas. Räkna kalendertid mellan sessionsdatum för symbolen.

### Performance

- Prisavkastning i procent är `100 × (C_slut / C_start − 1)`, med startpriset som nämnare. Sedan start används den första giltiga observationen och senaste bekräftade dagsstängningen. Kräv giltiga priser på två olika sessionsdatum. Redovisa faktiska start- och slutdatum.
- CAGR i procent per år är `100 × ((C_slut / C_start)^(365,25 / d) − 1)`, där `d > 0` är det faktiska antalet kalenderdagar mellan datumen. `365,25` är föreslagen konvention för kalenderdagar per år.
- För 1, 3, 5 och 10 år, gå motsvarande antal kalenderår bakåt från slutdatumet. Använd månadens sista dag om måldatumet saknas i kalendern. Välj senaste giltiga dagsstängning på eller före måldatumet. Redovisa det faktiska startdatumet. Visa `N/A` om historiken börjar efter måldatumet eller ett känt datagap gör referenspunkten osäker.

### Drawdowns från historiska toppar

- Mät från första giltiga observationen. Låt `H_t` vara den högsta observerade giltiga stängningen till och med dag `t`. Aktuell drawdown i procent är `100 × (C_t / H_t − 1)`. Vid en aktuell topp är drawdown `0 %`. Max drawdown är periodens lägsta drawdownvärde med samma teckenkonvention. Kräv minst två giltiga dagsobservationer för maxvärdet.
- En episod börjar vid första stängning under det löpande högsta värdet och avslutas vid första stängning på eller över den nivån. Använd den senaste stängningen på toppnivån före nedgången som toppdatum. Botten är den första lägsta stängningen inom episoden. Mät kalenderdagar från topp till botten och från botten till återhämtning. För en pågående episod är botten preliminär och återhämtningstiden `N/A`.
- Beräkna frekvens som antalet episoder under angiven mätperiod. Vid ett tröskelvärde, till exempel 10, 20 eller 30 procent, räknas en episod när dess största fall når eller passerar tröskeln. Siffrorna är kumulativa mellan trösklarna. Mellanliggande svängningar inom samma oåterhämtade drawdown ger ingen ytterligare episod.
- Räkna en episod som passerar ett identifierat datagap som osäker. Håll den utanför antalen för säkert avslutade och pågående episoder. Max drawdown bygger på observerade stängningar. Visa begränsad täckning om gap kan dölja en djupare botten.

### MA Behavior

- SMA 200D är det aritmetiska medelvärdet av de senaste 200 dagliga barernas stängningar, inklusive den dag som jämförs. Kräv 200 bekräftade barer med giltiga stängningar och utan kända datagap i fönstret. Distansen i procent är `100 × (C_t / SMA_t − 1)`.
- För historiska andelar är nämnaren alla dagar under angiven period med giltigt pris och giltig SMA. Dela antal dagar strikt över respektive strikt under SMA med nämnaren och multiplicera med 100. Exakt lika stängningar bidrar bara till nämnaren. Visa `N/A` vid noll jämförbara dagar.
- Typiskt avstånd kan visas som median, beräknad separat för positiva och negativa distanser. Ett extremt avstånd kan beskrivas med en övre percentil på den positiva sidan och en nedre percentil på den negativa. Kvantilmetod, gränser och minsta urval är öppna val. Visa `N/A` för en sida som saknar tillräckliga observationer.

### Deterministiska exempel

| Fall | Förväntat med förslaget |
| --- | --- |
| `100` den 2 januari 2020 och `146,41` den 2 januari 2024. | `46,41 %` prisavkastning och `10,00 %` CAGR över 1 461 kalenderdagar. |
| Senast `100` den 3 juni 2024. Äldsta observation `80` fredagen den 2 juni 2023. | Ettårsmålet är lördagen den 3 juni 2023. Använd fredagens stängning och visa `25 %` för 1 år. Visa `N/A` för 3, 5 och 10 år. |
| `100 → 85 → 95 → 75 → 100` den 5–9 februari 2024, en stängning per dag. | Aktuell drawdown `0 %` och max drawdown `−25 %`. En avslutad episod vid både 10 och 20 procent, noll vid 30 procent. Tre kalenderdagar till botten och en till återhämtning. Om sista `100` tas bort är episoden pågående med aktuell drawdown `−25 %`. |
| 200 stängningar på `100`, följda av `110` och `90`. | SMA är `N/A` under de första 199 barerna. De tre sista SMA-värdena är `100`, `100,05` och `100`. Över, under och exakt lika omfattar var sin dag, så andelen över och andelen under är vardera `1/3` av jämförbara dagar. |
| En dagsbar med `na` efter 200 giltiga stängningar. | Aktuella mått som kräver stängningen är `N/A`. SMA är `N/A` tills nästa fönster med 200 giltiga dagliga barer finns. |

## Senare

- **Swing-episoder.** Välj swing-punkter eller tröskelmetod och definiera vad som bekräftar start och slut, vilken dag bekräftelsen blir känd och hur nästlade rörelser räknas. Föreslagna utfall är storlek i procent av episodens startpris, kalenderdagar mellan valt start- och slutdatum samt antal episoder per redovisad mätperiod. Nivåer och segmentering är öppna.
- **Stöd och motstånd kring SMA.** Besluta vad som utlöser och avslutar ett test, vilken tolerans och vilket utfallsfönster som gäller samt hur upprepade kontakter räknas. Andelen lyckade test ska ha objektiva kriterier för täljare och nämnare.
